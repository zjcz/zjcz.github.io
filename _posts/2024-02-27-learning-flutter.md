---
layout: post
title:  "Learning Flutter"
date:   2024-02-27 10:15:00
categories: flutter
tags: [flutter]
---

I have recently been learning Flutter.  Here's my thoughts so far.
<!--more-->

## Introduction
After spending last year learning AWS, Linux and refreshing my Java skills I decided I wanted a new challenge for 2024.  I enjoyed my past experiences of mobile app development and decided to give Flutter a go.  I previously attempted to pick it up in 2022 but never really found the time and the learning material just didn't work for me.  Here's how it went the second time round.

## What is Flutter?
[Flutter](https://flutter.dev/){:target="_blank"} is a toolkit from Google for building natively compiled applications for mobile, web, and desktop from a single codebase. You write your app once and flutter will compile it to run on Android, iOS, Web and Desktop.  It uses Dart as it's programming language, which feels like it has taken the best bits of Java and Javascript and mashed them into a single modern language.  

## Learning Flutter
Previously I had tried to learn Flutter by using the official documentation and a free ebook I found on the Internet.  However this didn't really work for me so this time around I purchased [The Complete Flutter Development Bootcamp with Dart](https://www.udemy.com/course/flutter-bootcamp-with-dart/){:target="_blank"} from Udemy.  I find following video tutorials much easier than reading these days.  While the course was well put together and included lots of valuable information, unfortunately it is a little dated now.  Flutter has moved on and some of the code examples no longer work.  I found myself having to look up the new way of doing things to get the code to compile, which was a little frustrating.  If you are an experienced developer you can figure these problems out and work round them, but if you are new to coding it could be a little off putting.

## Initial Thoughts
I am really enjoying using the Flutter but there were a few things I was surprised at.  What I consider core functionality of the mobile dev ecosystem are provided by 3rd party packages.  I would have expected things like notifications and background worker tasks to be built into Flutter.  This isn't a big problem but it does mean you are relying on the community to address any issues rather than the Flutter/Dart team.  

Another thing that surprised me was the need to delve into the Android or iOS generated code to make changes.  For example configuring the app icon requires editing the Android and iOS projects, and I had to edit the AndroidManifest.xml to give permissions for the app to display notifications.  Not a big issue and both tasks were well documented but it was something I wasn't expecting.

## What's Next?
I feel like I have only scratch the surface with Flutter and there is still lots to learn.  I have a few ideas for apps I want to develop and I am looking forward to putting my new skills to the test.  As well as continuing to grow my Dart and Flutter skills in general, there are a couple of topics which I have seen mentioned several times in various blogs and articles which I want to investigate more:
- code generation
- adaptive apps to work with different screen sizes
- integrating AI

## Summary
So far I am loving my Flutter journey and intend to continue building on it.  While I don't think it is perfect, I think for anyone starting a new mobile app project it is a serious contender.
