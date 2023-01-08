---
title: "Unity Quick Tips — Global Conditional Attributes"
date: 2014-07-18 00:00:00 +0000
permalink: /unity-quick-tips-global-conditional-attributes/
image:  /static/hero-images/unity_quick_tips_global_conditional_attributes.png
tags:   [Unity, CSharp]
layout: post
---
A very useful trick you can do on your Unity projects is to setup some global conditional attributes. Let's see how and what for in a very a simple example.

First go to your **Player Settings** (Edit > Project Settings > Player) and under the **Other Settings** tab, type "DEBUG" on the **Scripting Define Symbols**.

![](/static/images/unity-quick-tips-global-conditional-attributes/unity_define_symbols.png)

You can now in your scripts do something like:

```c
[System.Diagnostics.Conditional("DEBUG")]
void DrawRay(Vector2 start, Vector2 dir, Color color, float duration)
{
	Debug.DrawRay(start, dir, color, duration);
}

void SomeMethod()
{
	... 
	DrawRay(rayOrigin, rayDirection, Color.red, 1f);
	...
}
```

What the conditional attribute does, in this case, is only executing the `DrawRay` method if the "DEBUG" conditional is defined. But the good news is that the code won't give you any warnings or errors in case it isn't!

So, no more having to comment out or removing code before making a final build. Just wrap all of your debug code with a similar approach and save yourself some headaches.

This simple trick can obviously be applied in many other situations and once you get the hang of it I'm sure you'll find some very interesting uses for it. Let me know if you have any questions or suggestions for more quick tips!