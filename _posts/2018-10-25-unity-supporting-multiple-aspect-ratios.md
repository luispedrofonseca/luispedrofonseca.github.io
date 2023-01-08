---
title: "Unity - Supporting Multiple Aspect Ratios"
date: 2018-10-25 00:00:00 +0000
permalink: /unity-supporting-multiple-aspect-ratios/
image:  /static/hero-images/unity-multiple-aspect-ratios.jpg
tags:   [Unity, CSharp, Mobile]
layout: post
---
One of the biggest doubts people have when creating mobile games is how to handle the myriad of screen resolutions and aspect ratios. Just on iOS there are currently 4 different aspect ratios: 4:3, 3:2, 16:9 and 19.5:9. On Android, given the thousands of different devices, it ranges anywhere between those.
Here's how those aspect ratios compare to each other (in portrait mode):

![](/static/images/unity-supporting-multiple-aspect-ratios/aspect-ratios.png)

So what's the solution to make your game look great on these screens while avoiding black bars or stretching?

You start by defining your target aspect ratio - this should usually be 16:9 since it's the most common. Then, place your target aspect ratio image inside the other aspect ratios and figure out how it should align. Here's an example:

![](/static/images/unity-supporting-multiple-aspect-ratios/game-view-aspect-ratio.png)

In the example above, the blue areas represent what's outside of your target aspect ratio. You need to plan what you want to put here. Ideally your game backgrounds should be made taking this in consideration, otherwise as a last resort you'll have to use black bars.

But how exactly do you achieve this camera behaviour? It's easier said than done, but the gist of it is:

1. Define in world units what's the size of your camera at your target aspect ratio.
2. Calculate based on the current camera aspect, what width and height you'll need to maintain the target aspect ratio
3. Scale the camera accordingly

A simpler way is to use the <a href="http://www.procamera2d.com/user-guide/extension-content-fitter/" target="_blank">Content Fitter</a> extension for <a href="http://www.procamera2d.com" target="_blank">Pro Camera 2D</a> and get done with it, but I'm not here to advertise it. :)

![](http://www.procamera2d.com/images/gifs/content_fitter.gif)

