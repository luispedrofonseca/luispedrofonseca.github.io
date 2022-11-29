---
title: "Unity Quick Tips — Enum Description Extension Method"
date: 2014-08-08 00:00:00 +0000
categories: Unity  CSharp
permalink: /unity-quick-tips-enum-description-extension-method/
header:
  overlay_image: /static/hero-images/unity_quick_tips_enum_description.png
  teaser: /static/hero-images/unity_quick_tips_enum_description.png
  overlay_filter: 0.5
  show_overlay_excerpt: false
---
While this tip is not Unity specific, it's still very useful for all C# Unity devs out there.

Recently I needed to get a name/description out of a enum. After some digging around, I found this subject is far from consensual and <a href="http://stackoverflow.com/questions/424366/c-sharp-string-enums" target="_blank">there are dozens of different solutions</a> to accomplish the same result. For me, by far, the simplest and cleanest way to do it is by using a cool feature in C# called extension methods.

Extension methods enable you to "add" methods to existing types without creating a new derived type, recompiling, or otherwise modifying the original type. That's what we're going to do to the `Enum` type to get the results we want.

Consider the following scenario: You need an enum with the characters in your game:

```c
public enum CharactersEnum
{
	MAINCHARACTER,
	ENEMY1,
	ENEMY2,
	FINALBOSS
}
```

However at some point, you might want to show the characters names. While `FINALBOSS` is a perfectly fine name for a character, sometimes you might feel a little bit more creative. In that case, you could add the `Description` parameter to your enum entries, like this:

```c
using System.ComponentModel;

public enum CharactersEnum
{
	MAINCHARACTER,
	ENEMY1,
	ENEMY2,
	[Description("Mr. Bad Guy")]
	FINALBOSS
}
```

And then, all you have to do is create an extension method for the `Enum` type that can grab that description:

```c
using System;
using System.ComponentModel;

public static class EnumsHelperExtension
{
	public static string ToDescription(this Enum value)
	{
		DescriptionAttribute[] da = (DescriptionAttribute[])(value.GetType().GetField(value.ToString())).GetCustomAttributes(typeof(DescriptionAttribute), false);
		return da.Length > 0 ? da[0].Description : value.ToString();
	}
}
```

Save this class in a file somewhere on your project and from now on you can simply do:

```c
string charName = CharactersEnum.FinalBoss.ToDescription();
```

All your `Enum`'s can now have a description and in case the they don't, it will simply return the attribute name as a simple `ToString()` usually would.

Please comment or <a href="https://twitter.com/lpfonseca" target="_blank">add me on Twitter</a>, if you have any questions or suggestions for more quick tips!