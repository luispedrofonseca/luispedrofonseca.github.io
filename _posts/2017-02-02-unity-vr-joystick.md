---
title: "Unity VR Joystick"
date: 2017-02-02 00:00:00 +0000
permalink: /unity-vr-joystick/
image:  /static/hero-images/unity-vr-joystick.png
tags:   [Unity, CSharp, VR]
layout: post
---
Over the last couple of years, I've become more and more interested in virtual reality, especially after trying out a bunch of demos at the last Unite in LA. So much, in fact, that I have decided to go ahead and buy an <a href="http://www.vive.com" target="_blank">HTC Vive</a>. Being a new technology, it is still quite expensive, not only because of the price of the device itself but also because you need to have a pretty beefy PC to support it. I have put together a <a href="https://www.tonymacx86.com" target="_blank">Hackintosh</a> (maybe more about that in a future post), so I can still use OSX for my daily job but also run Windows which is a requirement for desktop VR.

To put the Vive to good use I have decided to create a simple flying game. The first challenge I faced was figuring out how to control a plane using only the Vive controllers. The solution that made most sense to me was to recreate an airplane joystick (aka HOTAS), inside the game itself and then let the player grab it and move it using their own hands like in real life.

This is how it looks:


![](/static/images/unity-vr-joystick/unity-vr-joystick.gif)


To speed up the development, I have been using the amazing <a href="https://github.com/thestonefox/VRTK" target="_blank">VRTK library</a> which is a collection of useful scripts and concepts to aid building VR solutions rapidly. It handles stuff like locomotion, interactions, physics, UI, etc. If you are planning to develop in VR using Unity, trust me, you will want to use this library. Best of all, it is free and open-source!

Using VRTK made things really simple and all I had to do was create a configurable joint between the stick and the base. Here are the settings I used:


![](/static/images/unity-vr-joystick/unity-vr-joystick-configurable-joint.png)



After creating the configurable joint, you will need to create a new class that overrides the VRTK_InteractableObject class (from the VRTK library I mentioned earlier). This class provides everything you need to know about when the player grabbed, dropped or moved the joystick. With this in place, you now have all the data needed to maneuver the plane, including the roll and pitch (mapped to XPercentage and ZPercentage here):

{% highlight csharp %}
using System;
using System.Collections;
using UnityEngine;
using VRTK;

public class VRJoystick : VRTK_InteractableObject
{
    public Action OnUseStarted;
    public Action OnUseStopped;

    [Header("Joystick")]
    [SerializeField]
    Transform _handle;

    [SerializeField]
    float _maxXAngle = 45;

    [SerializeField]
    float _maxZAngle = 45;

    [SerializeField]
    [Range(0, 1)]
    float _vibrationStrenght = .1f;

    [SerializeField]
    [Range(0, 1)]
    float _vibrationInterval = .05f;

    public float XPercentage;
    public float ZPercentage;

    VRTK_ControllerActions _controllerActions;

    bool _grabbing;
    
    override protected void Update ()
    {
        base.Update();

        var angleX = _handle.localRotation.eulerAngles.x;
        if (angleX > 180)
            angleX -= 360;

        var angleZ = _handle.localRotation.eulerAngles.z;
        if (angleZ > 180)
            angleZ -= 360;

        XPercentage = angleX / _maxXAngle;
        ZPercentage = angleZ / _maxZAngle;
    }

    public override void StartTouching(GameObject currentTouchingObject)
    {
        base.StartTouching(currentTouchingObject);
        _controllerActions = currentTouchingObject.GetComponent<VRTK_ControllerActions>();
        Vibrate(.5f);
    }

    public override void StopTouching(GameObject previousTouchingObject)
    {
        base.StopTouching(previousTouchingObject);
        _controllerActions = previousTouchingObject.GetComponent<VRTK_ControllerActions>();
        Vibrate(.5f);
    }
    
    override public void Grabbed(GameObject grabbingObject)
    {
        base.Grabbed(grabbingObject);
        _controllerActions = grabbingObject.GetComponent<VRTK_ControllerActions>();
        Vibrate(.5f);
        _grabbing = true;

        StartCoroutine(DetectJoystickMovement());
    }

    override public void Ungrabbed(GameObject previousGrabbingObject)
    {
        base.Ungrabbed(previousGrabbingObject);

        _grabbing = false;
    }

    IEnumerator DetectJoystickMovement()
    {
        var currentXPercentage = XPercentage;
        var currentZPercentage = ZPercentage;
        while (_grabbing)
        {
            if(Mathf.Abs(currentXPercentage - XPercentage) > _vibrationInterval)
            {
                Vibrate(_vibrationStrenght);
                currentXPercentage = XPercentage;
            }
            else if (Mathf.Abs(currentZPercentage - ZPercentage) > _vibrationInterval)
            {
                Vibrate(_vibrationStrenght);
                currentZPercentage = ZPercentage;
            }

            yield return null;
        }
    }

    public override void StartUsing(GameObject currentUsingObject)
    {
        base.StartUsing(currentUsingObject);

        if (OnUseStarted != null)
            OnUseStarted();
    }

    public override void StopUsing(GameObject previousUsingObject)
    {
        base.StopUsing(previousUsingObject);

        if (OnUseStopped != null)
            OnUseStopped();
    }

    public void Vibrate(float vibrationStrength)
    {
        if(_controllerActions != null)
            _controllerActions.TriggerHapticPulse(vibrationStrength);
    }
}
{% endhighlight %}

With those two pieces in place you can now map the joystick movement to anything you see fit. In my case, a simple airplane.
Let me know what you think about this solution and if you have any doubts about the implementation.
