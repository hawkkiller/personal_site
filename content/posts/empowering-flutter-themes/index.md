---
title: "Unleashing the power of Flutter themes"
date: 2023-04-10T17:27:13+0200
draft: true
summary: "A few months ago, I embarked on a journey exploring the mystical land of Flutter themes. Like any adventurer worth their salt, I started with the basics: default themes, global colour variables, and theme extensions.
Unfortunately, they were all fraught with cons! But fear not, dear reader, for I am about to reveal the approach that I have used for the past few months and it has brought great happiness to my coding lif"
resources:
  - name: "featured-image"
    src: "images/preview.webp"
tags:
  - "theme"
  - "flutter"
  - "dart"
  - "Material3"
---

## Introduction

A couple of moons ago, I set out on a thrilling quest to uncover the enigmatic realm of Flutter themes. As any self-respecting adventurer would, I began with the basics: default themes, global color variables, and theme extensions. To my dismay, they all had their share of pitfalls! But fret not, dear reader, for I am about to unveil an approach that has brought immense joy to my coding life over the past months. Let's venture forth and unravel the journey together.

## Global colour variables

```dart
const black = Color(0xFF000000);
const white = Color(0xFFFFFFFF);
const grey = Color(0xFF9E9E9E);
const red = Color(0xFFD32F2F);
const green = Color(0xFF388E3C);

// Usage
Text(
  'Hello World',
  style: TextStyle(
    color: black,
  ),
);
```

Using __color variables__ is the most primitive way to theme your app. You simply define a set of colors in one file and use them throughout your app. This method is as easy as pie, but it comes with a few drawbacks:

- You must set the style for every SDK widget you use. For instance, if you want to change the color of a TextButton, you must set the style property. This can be rather cumbersome and lead to heaps of boilerplate code. This method is not very flexible. You're restricted to using a single set of colors throughout your app. If you want to change the color scheme, you'll have to refactor your entire app.
- This method doesn't harness the power of Material naming.
- You'll miss out on the snazzy theme-switching animations.

Although this method isn't quite perfect, it's better than nothing. It's fine for small apps or MVPs. But now, let's move on to something more exciting.

## Colour containers

```dart
abstract class ColorContainer {
  Color get black;
  Color get white;
  Color get grey;
}

class ColorContainerLight implements ColorContainer {
  @override
  Color get black => Color(0xFF000000);

  @override
  Color get white => Color(0xFFFFFFFF);

  @override
  Color get grey => Color(0xFF9E9E9E);
}

class ColorContainerDark implements ColorContainer {
  @override
  Color get black => Color(0xFFFFFFFF);

  @override
  Color get white => Color(0xFF000000);

  @override
  Color get grey => Color(0xFF616161);
}
```

__Color containers__ are a marvelous upgrade from the previous approach. They allow you to define multiple color schemes and switch between them. This method is incredibly flexible, making it a breeze to change your app's color scheme. Let's list the pros and cons of this method:

__Pros__:

- Effortlessly switch between color schemes.
- Define multiple color schemes.
- Easily add new color schemes.

__Cons__:

- SDK widgets still don't inherit styles from your themes, so you need to set the style for every widget.
- This method still doesn't harness the power of Material naming.
- You'll still miss out on those fancy theme-switching animations.

## Theme extensions

```dart
class ColorsExtension extends ThemeExtension<ColorsExtension> {
  final Color black;
  final Color white;
  final Color grey;

  ColorsExtension({
    required this.black,
    required this.white,
    required this.grey,
  });

  // copywith
  // lerp (for animations)
}
```

__Theme Extensions__ are another delightful step up from the previous approach. They are akin to __color containers__, but with native support. As a result, you can enjoy those fancy animations when switching between themes at no extra cost. However, this method does require a fair bit of boilerplate code.

## Material color system

{{< figure src="https://lh3.googleusercontent.com/G_2Z3lRMdADfzbQyJZcZFAv61QpImyb9OhdmEpu_lAaxgPa01iY-QHPhIgCbkqPQTn9C4Jwzr2OufMQSmPcwJnmSdkmpmix_8HSrctOUjVo=s0" >}}

Material color system is a snazzy naming convention that enables you to define a set of colors used in the Material Design system. This method is highly flexible and makes it a cinch to change your app's color scheme.

There's a treasure trove of theory on the Material color system, but we won't dive too deep here. In a nutshell, it's all about deterministic color definitions:

- __primary__ (used to derive roles for key components)
- __secondary__ (used for less prominent components)
- __tertiary__ (used to derive the roles of contrasting accents)
- __neutral__ (used to derive surface color roles for backgrounds)
- __neutral__ variant (used to derive color roles for medium emphasis elements)
- __error__ (used to derive color roles for error states)
- __custom colors__ (pin specific hues that often are needed alongside expressive colors)

Here's a handy link for you:
<https://m3.material.io/styles/color>

__Pros__:

- Create design systems with ease
- Benefit from a large community of UX/UI specialists and developers using this approach
- Easily switch between color schemes
- Dynamic themes supported out of the box
- Flutter adores this stuff!

## Applying Color System

```dart
abstract class ColorContainer {
  Color get primary;
  Color get secondary;
  Color get tertiary;
}

class ColorContainerLight implements ColorContainer {
  @override
  Color get primary => Color(0xFF6200EE);

  @override
  Color get secondary => Color(0xFF03DAC6);

  @override
  Color get tertiary => Color(0xFF018786);
}

class ColorsExtension extends ThemeExtension<ColorsExtension> {
  final Color primary;
  final Color secondary;
  final Color tertiary;

  ColorsExtension({
    required this.primary,
    required this.secondary,
    required this.tertiary,
  });

  // copywith
  // lerp (for animations)
}
```

Things are looking much better now! We can easily switch between color schemes and create design systems. However, there's still work to be done. We need to define all the colors used in the __Material Design system__. Luckily, there's a magical tool that can help us: the __Material Color Tool__, available on the official Material Design website. Behold the link:
<https://m3.material.io/theme-builder#/dynamic>

Alas, this method doesn't support dynamic themes and doesn't utilize native Flutter features. But we can remedy that!

## Recommended way

{{< figure src="https://s3-alpha.figma.com/hub/file/3248391748/c8266c68-b5d6-4fc2-9fc6-d41b3cc8af6f-cover.png" >}}

Recalling earlier, almost every approach had the same cons. We need to define the style for every widget from the SDK. Thankfully, Flutter offers a solution with the new Material 3 design, which is nearly implemented in the Flutter framework. It's called __Material 3 Theme__.

Venture to the [theme builder](https://m3.material.io/theme-builder#/dynamic) and create a theme. Copy the code and paste it into your project, and you'll get something like this:

```dart
final defaultThemeData = ThemeData(
  useMaterial3: true,
);

final lightThemeData = defaultThemeData.copyWith(
  colorScheme: lightColorScheme,
);

final darkThemeData = defaultThemeData.copyWith(
  colorScheme: darkColorScheme,
);

const lightColorScheme = ColorScheme(
  brightness: Brightness.light,
  primary: Color(0xFF6750A4),
  onPrimary: Color(0xFFFFFFFF),
  primaryContainer: Color(0xFFEADDFF),
  onPrimaryContainer: Color(0xFF21005D),
  secondary: Color(0xFF625B71),
  onSecondary: Color(0xFFFFFFFF),
  secondaryContainer: Color(0xFFE8DEF8),
  onSecondaryContainer: Color(0xFF1D192B),
  tertiary: Color(0xFF7D5260),
  onTertiary: Color(0xFFFFFFFF),
  tertiaryContainer: Color(0xFFFFD8E4),
  onTertiaryContainer: Color(0xFF31111D),
  error: Color(0xFFB3261E),
  onError: Color(0xFFFFFFFF),
  errorContainer: Color(0xFFF9DEDC),
  onErrorContainer: Color(0xFF410E0B),
  outline: Color(0xFF79747E),
  background: Color(0xFFFFFBFE),
  onBackground: Color(0xFF1C1B1F),
  surface: Color(0xFFFFFBFE),
  onSurface: Color(0xFF1C1B1F),
  surfaceVariant: Color(0xFFE7E0EC),
  onSurfaceVariant: Color(0xFF49454F),
  inverseSurface: Color(0xFF313033),
  onInverseSurface: Color(0xFFF4EFF4),
  inversePrimary: Color(0xFFD0BCFF),
  shadow: Color(0xFF000000),
  surfaceTint: Color(0xFF6750A4),
  outlineVariant: Color(0xFFCAC4D0),
  scrim: Color(0xFF000000),
);

// dark ... 

```

Now we can use the Material 3 Theme in our project, and everything is ready to go! The best part is that Flutter Widgets from the material library use this theme by default. So, we don't need to define the style for every widget. We just need to define the color scheme, and the rest is handled by Flutter. I've concocted a small showcase app that employs this approach. You can find it [here](https://github.com/hawkkiller/theme_example).

{{< admonition type=note >}}
Keep in mind that only widgets from the material library inherit colors from this theme. Thus, widgets like Container or Scaffold will not use `backgroundColor` by default.
{{</ admonition >}}

And there you have it, fellow adventurer! We've journeyed through the mystical land of Flutter themes and discovered the secrets to a coding life filled with joy and satisfaction. Happy theming!

## Conclusion

And there you have it, brave adventurer! We have journeyed through the treacherous lands of Flutter themes, from the humble beginnings of global color variables to the awe-inspiring Material 3 Theme. As we have grown and learned, we have left behind the drudgery of boilerplate code, stepping into a world where Flutter widgets inherit styles by default, making our lives as developers infinitely more enjoyable.
