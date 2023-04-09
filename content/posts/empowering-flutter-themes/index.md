---
title: "Empowering Flutter Themes"
date: 2023-04-05T18:00:35+02:00
draft: true
summary: "A few months ago, I embarked on a journey exploring the mystical land of Flutter themes. Like any adventurer worth their salt, I started with the basics: default themes, global colour variables, and theme extensions.
Unfortunately, they were all fraught with cons! But fear not, dear reader, for I am about to reveal the approach that I have used for the past few months and it has brought great happiness to my coding lif"
featuredImage: ""
images:
  - ""
tags:
  - "theme"
  - "flutter"
  - "dart"
  - "Material3"
---

## Introduction

A few months ago, I embarked on a journey exploring the mystical land of Flutter themes. Like any adventurer worth their salt, I started with the basics: default themes, global colour variables, and theme extensions.
Unfortunately, they were all fraught with cons! But fear not, dear reader, for I am about to reveal the approach that I have used for the past few months and it has brought great happiness to my coding life.

## What is a theme?

A theme is a collection of colours, fonts, and other visual properties that are used to style a widget. In Flutter, themes are defined in the `ThemeData` class. The `ThemeData` class is a collection of properties that are used to style the widgets. For example, `ThemeData` has a property for setting a theme for about each widget in the Material and Flutter library. Here below I want to compare different approaches to theme management in Flutter.

## Default Themes

The first approach is to manually set the theme for each widget. This approach is the most straightforward and is the default approach that Flutter provides. However, this approach has a few cons:

- It is not scalable. If you have a large application, you will have to set the theme for each widget.
- It is not easy to maintain. If you want to change the theme, you will have to change it in each widget.
- It is not easy to extend. If you want to add a new theme, you will have to add it to each widget.
