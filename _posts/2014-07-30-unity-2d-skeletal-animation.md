---
title: "Unity 2D Skeletal Animation"
date: 2014-07-30 00:00:00 +0000
permalink: /unity-2d-skeletal-animation/
image:  /static/hero-images/unity_2d_skeletal_animation_featured_image.png
tags:   [Unity, Plugins, Project-Cuba]
layout: post
---
One of the biggest draws, if not the biggest, of doing my own games is the opportunity to spend as much time on a feature as I feel is needed — not something you can say about most client projects where you have the constant pressure of a strict deadline on your shoulders. While most of the time, you just have to step back and realize when you're pushing a certain feature or detail too far, sometimes you also need to bite the bullet and re-do some of your previous work.

That's what happened on Project Cuba when I realized my character animations were not up to the quality level I was targeting for the game. There are several reasons for that — besides my lack of animation experience — but one of the biggest is that Unity's 2D tools are still in its infancy and there really isn't anything built-in to handle 2D animations. You have to rely on simple rotations, translations and scaling. And while sometimes that is enough to do proper animations, the workflow is cumbersome and far from ideal.

Fortunately, there are some plugins on the Asset Store that will greatly improve the process and bring to the table some very interesting features. Amongst those, I've tried <a href="http://www.puppet2d.com" target="_blank">Puppet2D</a> and the free <a href="http://forum.unity3d.com/threads/release-free-unity-sprites-and-bones-2d-skeleton-animation.219915/" target="_blank">Unity Sprites And Bones</a>, but there's also <a href="http://echo17.com/smoothmoves.html" target="_blank">SmoothMoves</a> which seems to be pretty popular as well. While these will help you immensely in comparison to what's provided built-in, neither of them seems to be particularly polished or a one-stop solution for all of you animation needs.

The advantages of these plugins far exceed the disadvantages, but you'll probably find yourself fighting against the framework for a fair share of the time spent with it. I know I did with _Puppet2D_ and _Unity Sprites and Bones_ but also with Mecanim itself. Don't take me wrong, Mecanim is an incredible piece of Unity and if you're doing 3D humanoid animations I'm pretty sure there's nothing out there that can compete with it. It makes animations transitions and blending a breeze and the editor is quite useful for those who prefer a more visual approach. However, at this stage, is still not focused and/or optimised for 2D games. It has a fairly large overhead, especially on mobile, and the API is lacking. As an example here's what my main character setup looked like with Mecanim:

![Main Character Mecanim layout](/static/images/unity-2d-skeletal-animation/jack_mecanim.png)

As you can see, it's a bit convoluted since I have well over 20 animations for my main character, but it did the work reasonably well. However, with Mecanim once your animation logic starts getting too large, performance will suffer. There are some <a href="http://docs.unity3d.com/Manual/MecanimPeformanceandOptimization.html" target="_blank">optimizations you can do</a> to minimize the problem but that's not the purpose of today's post.

Today I want to show you what I think is the state-of-the-art tool for 2D animations. Meet <a href="http://esotericsoftware.com" target="_blank">Spine</a>!

<iframe width="560" height="315" src="https://www.youtube.com/embed/5RTkImAOJKM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

With an extensive, and impressive, list of features (FFD, skinning, IK, etc), but most importantly, a standalone editor and support for over 20 runtimes it's, in my opinion, currently the way to go in terms of 2D animations in Unity (or really any other game engine). I'm not going to give you an extensive overview of what Spine is or does since you can get that from the video and link above.

I want to show you an example of an animation I did with _Spine_ for my _Project Cuba_ main character (Jack). Two of his most distinguishable trademarks are his pompadour hairstyle and his big donut belly. Without Spine it would be really complicated and cumbersome to get a decent animation of these elements without recurring to multiple images.

![](/static/images/unity-2d-skeletal-animation/jack_belly1.gif)
![](/static/images/unity-2d-skeletal-animation/jack_hair1.gif)

As you can see above, with Spine support for FFD (free-form deformation) and skinning (attaching bones to a mesh), I was able to accomplish a simplistic 3D effect on his belly and a bouncy effect on his hair. All without having to recur to multiple images stealing precious memory space.

I'm still in the process of converting all my animations to Spine but I can say that from what I've seen I'm pretty sure I won't regret to have taken this step. In the meantime, I'll leave you with the almost final version of Jack's run animation.

![](/static/images/unity-2d-skeletal-animation/jack_run1.gif)

Don't forget to <a href="https://twitter.com/lpfonseca" target="_blank">follow me on Twitter</a> for updates on this game and more of my ramblings. 😉