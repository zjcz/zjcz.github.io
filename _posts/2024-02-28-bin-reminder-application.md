---
layout: post
title:  "Bin Reminder Application"
date:   2024-02-28 12:37:00
categories: flutter
tags: [flutter, mobile app, android, dart]
---

Bin Reminder Application is a simple mobile application designed to remind the user when a bin is due for collection.
<!--more-->

## Introduction
About 10 years ago I developed an app for Windows Mobile using .Net which allowed the user to enter information about the collection days of their dustbins and displayed a notification the day before the collection was due to remind them to put them out.  When Windows Mobile died I always intended on re-writing it for Android but never found the time.  After spending the last few weeks [Learning Flutter](/2024/02/27/learning-flutter) I decided to give it a go.

## What is it?
The main screen of the app will display a list of bins and the next collection date.  The user can add, edit and delete bins.  Using a background worker the app will display a notification the day before the collection is due.  Data is stored locally on the device.

![Home Screen](/assets/images/2024-02-28-bin-reminder-home-screenshot.png)
![Edit Screen](/assets/images/2024-02-28-bin-reminder-edit-screenshot.png)

## Development
The app was developed in Flutter using Android Studio.  The functionality of the app is quite simple, it contains one table in the database to store the bins.  The application has a main screen to display the list of bins and an edit screen to add and edit bins.  

The background worker is configured to check daily if any collection dates fall either today and tomorrow and if they do a notification is displayed.  To achieve this the worker triggers every hour and if it is the first time it has run on a certain date it runs it's checks.  I couldn't find a way of scheduling the worker to trigger at a set time each day, so I settled for this approach.  It is something I'd like to improve in the future.

To avoid an issue with always having to recalculate the next collection date to ensure it is in the future I decided to refresh them (a) as part of the background worker and (b) when the application loads.  This means the user can add a bin with a collection date of today, then tomorrow when the date is in the past it will be corrected either the next time the worker runs or when the app loads (whichever happens first).

I structured the app code using the following folders:
- helpers - contains wrapper code for the 3rd party packages
- models - contains the data model for the bin object
- screens - contains the UI for the app.  This includes:
    - home_screen - the main screen showing the list of existing
    - edit_screen - the screen for adding and editing bins
    - loading_screen - a screen to display while the app is loading
- services - contains the code for database access, the background worker and the notification service
- widgets - contains the custom widgets used in the app.  This includes:
    - bin_color_selector - a custom widget used on the edit screen to display the list of possible bin colors
    - bin_tile - used by the bin_list widget to show the details of a bin record in the list
    - bin_type_selector - a custom widget used on the edit screen to display the list of possible bin types
    - bin_list - a custom list widget used on the home screen to display the list of bins
    - collection_frequency_selector - a custom dropdown widget used on the edit screen to select the collection frequency
    - delete_confirmation_dialog - a confirmation popup used when deleting a bin

I also developed a set of unit tests for the helper, model and services classes, and the UI widgets.  I have been trying to be more disciplined with my unit testing and while it is not TDD it is the approach I am trying to take.  Unfortunately I often find my enthusiasm gets the better of me and I end up writing more code than is required for the test!  Integration and UI testing is an area I need to get better at with Flutter and something I plan to address in the near future.

Some of the 3rd party packages used include:
- [sqflite](https://pub.dev/packages/sqflite){:target="_blank"} - For storing the data in a local database
- [workmanager](https://pub.dev/packages/workmanager){:target="_blank"} - For running the background worker
- [flutter_local_notifications](https://pub.dev/packages/flutter_local_notifications){:target="_blank"} - For displaying the notifications

As this was the first Flutter application I had developed there was a big learning curve.  While the learning material I had used as a great help, you don't really start learning until you start developing your first app.  I found myself having to lookup a lot of things, and I making sure I was following best practices.  I also disabled GitHub Copilot for this project as I wanted to make sure I was writing the code myself rather than just accepting code suggestions.

Some of the challenges I faced included:

### Android Only Development
Currently the app has only been tested on Android.  I don't own a mac so I have been unable to test the iOS version and while the app should work I suspect it will need some UI tweaks to make it look right.  I also haven't tested on desktop or web yet, partly because Android was my priority for this project.

### Background Worker and Notifications
By their nature background workers are difficult to debug.  After following the documentation and sample apps provided I had implemented the work manager and local notification packages but it took a bit of head scratching and debug logging to get it working.  The main issue here turned out to be I wasn't awaiting and async function.  I can't help but think it would be nice if the compiler or linter warned you of things like this.  It's times like this I miss the .Net naming convention were all async methods end with the word Async so issues like this stand out.

### Edit Form Validation
Flutter provides a Form widget with built in validation, however this only works with DropDownButton control and not DropDownMenu. I felt the DropDownMenu provided a much nicer UI with the ability to show icons in the dropdown items, so I ended up writing custom validation code to ensure the dropdowns had been populated before saving.

### Icons
To illustrate the bins I used icons from [Font Awesome](https://fontawesome.com/){:target="_blank"} , using the [Flutter Font Awesome Package](https://pub.dev/packages/font_awesome_flutter){:target="_blank"}.  However this didn't provide all the icons I needed so I created my own set using Inkscape to generate the SVG icons and [Flutter Icon Generator](https://fluttericon.com/){:target="_blank"} to package them.  I also created my own icon for the application - I am not very good when it comes to drawing icons and logos as you can probably tell.

## Summary

You can view the complete code at [GitHub - Flutter Bin Reminder](https://github.com/zjcz/flutter-bin-reminder){:target="_blank"}.