---
layout: post
title: "What I Learnt This Week - 11 July 2025"
date: 2025-07-12 09:59:00
categories: what-i-learnt-this-week
tags: [Flutter, icons, figma, AI coding assistant]
---

This week I have been trying to add icons to a Flutter app.  As this is a part of the development lifecycle I do so infrequently I often forget how its done, leading to lots of internet searching and head scratching.

<!--more-->

I recently came across [How to Design Your Flutter App Icons in Figma (for Beginners)](https://www.youtube.com/watch?v=yxg9yrZdDlw) which shows how to use [Figma](https://www.figma.com/) to design icons, then add them to apps using the [flutter_launcher_icons](https://pub.dev/packages/flutter_launcher_icons) package.  This package worked fine for iOS but the Android icons weren't formatted properly (Android scaled them to add the rounded edges).  Perhaps it was a configuration problem on my behalf.

Next I came across [Flutter: How to Add App Icons to the iOS and Android Apps: Step by Step](https://www.youtube.com/watch?v=oRBWPm7nCV0), which shows how to use [App Icon Generator](https://www.appicon.co/) to generate the icons.  Again iOS worked fine but I had the same problem with Android icons.

For me, the best way to add icons to Android apps is to use the [Configure Image Asset](https://developer.android.com/studio/write/create-app-icons) screen in Android Studio (apps -> res, right click, New -> Image Asset).  Upload a 1024 x 1024 image and this screen handles all the scaling.

As an aside, I use [Flutter Native Splash](https://pub.dev/packages/flutter_native_splash) to generate the app splash screens.

## Using AI to Check if Your App is Ready for Production

This week I also came across this post on reddit - [Think twice before you go production with your vibe coded made SaaS mobile app.](https://www.reddit.com/r/ClaudeAI/comments/1luraop/think_twice_before_you_go_production_with_your/), which contains some handy prompts to use with AI code assistants to validate your code before releasing it to production.

## And Finally...

This week I have also...

🎧 Listened to: [Black Sabbath](https://www.last.fm/music/Black+Sabbath)  
🍿 Watched: [Cold Case](https://www.imdb.com/title/tt0368479) (Nearly Done!)
