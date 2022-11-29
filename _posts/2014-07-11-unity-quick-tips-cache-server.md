---
title: "Unity Quick Tips — Local Cache Server"
date: 2014-07-11 00:00:00 +0000
categories: Unity  CSharp
permalink: /unity-quick-tips-cache-server/
header:
  overlay_image: /static/hero-images/unity_quick_tips_local_cache_server.png
  teaser: /static/hero-images/unity_quick_tips_local_cache_server.png
  overlay_filter: 0.5
  show_overlay_excerpt: false
---
After many years working with Unity, I've realised that one of the most overlooked features of the Unity's Team License, by myself and other fellow developers, is the <a href="http://docs.unity3d.com/Manual/CacheServer.html" target="_blank">Cache Server</a>.

Like the name says, what it basically does is caching your assets in order to make them load faster. This is particularly great if you're working on a multi-platform game where you need to switch platforms constantly. As you all know, every time you do that Unity has to reimport all the assets, which can be a pretty painful depending on the size and number of resources on your project.

![](/static/images/unity-quick-tips-cache-server/unity_importing.png)

Now, what most people don't realize is that by using the Cache Server you can reduce that time to a couple of seconds and switch platforms pretty much instantaneously!

If you have a medium to large team working on the same office it makes sense to have the Cache Server setup on a local machine connected to your, preferably wired, network. However — and this is where my tip comes in — if you're a lone wolf, work on a remote team, or just don't have the time/money to spend on a dedicated Cache Server machine, you can (and should) install it locally!

![](/static/images/unity-quick-tips-cache-server/unity_cache_server_localhost.png)

Just follow this <a href="http://docs.unity3d.com/Manual/CacheServer.html" target="_blank">setup tutorial</a> but instead, use localhost as the IP address and you're done! At the (relatively) small expense of RAM and disk space you get instant platform switch!

Hope you liked this tip and stay tuned for more!