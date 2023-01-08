---
title: "Unity Custom Rect Editor"
date: 2016-10-08 00:00:00 +0000
permalink: /unity-custom-rect-editor/
image:  /static/hero-images/unity-custom-rect-editor.png
tags:   [Unity, Plugins, ProCamera2D]
layout: post
---
One of the main goals of <a href="http://www.procamera2d.com/user-guide/rooms" target="_blank">ProCamera2D</a>'s new extension - <a href="http://www.procamera2d.com/user-guide/extension-rooms/" target="_blank">Rooms</a> - was to make it as user-friendly as possible.

Each room is basically a rectangle with some extra data to allow custom transitions. To make it easy to edit the rooms the user should be able to interact with them on the scene. However, Unity does not have a built-in rectangle (Rect) editor tool. 

Gladly, Unity is very flexible and easy to extend, so I created a simple one. Here you go:

<script src="https://gist.github.com/luispedrofonseca/c81c26f6a30108893387292965d524b2.js"></script>

And then, to use it, all you have to do in your custom editor is something like:

{% highlight csharp %}
using UnityEngine;
using System.Collections;
using UnityEditor;

public class RectExample : MonoBehaviour
{
    public Rect MyRect;
}

[CustomEditor(typeof(RectExample))]
public class RectExampleEditor : Editor
{
    void OnSceneGUI()
    {
        var rectExample = (RectExample)target;

        var rect = RectUtils.ResizeRect(
            rectExample.MyRect,
            Handles.CubeCap,
            Color.green,
            Color.yellow,
            HandleUtility.GetHandleSize(Vector3.zero) * .1f,
            .1f);

        rectExample.MyRect = rect;
    }
}
{% endhighlight %}

In the end you get something like this:

![](/static/images/unity-custom-rect-editor/rect-editor.gif)

Instead of the boring default editor:

![](/static/images/unity-custom-rect-editor/rect-editor-manual.gif)

Hope you enjoy this little tool and feel free to improve on it!