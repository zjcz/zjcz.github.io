---
layout: post
title: "What I Learnt This Week - 20 June 2025"
date: 2025-06-20 18:02:00
categories: what-i-learnt-this-week
tags: [flutter]
---

This week I learnt that using a `ListView` for data entry screens in Flutter is a bad idea.  

<!--more-->

## Flutter ListViews on Data Entry screens are a Bad Idea
Normally when working on a data entry screen in Flutter I use a `SingleChildScrollView` and a `Column` to display the form fields.  On a recent project, I asked AI to generate the screen for me as it had a large number of fields and I thought it would be quicker. AI generated the code using a `ListView` to display the form fields, which I thought was a good idea at the time.  Everything looked neat and tidy and I was able to scroll through the form fields easily. 

However, I quickly realised that this was not the best approach.  Mandatory fields contain validation logic, but this logic wasn't always triggered.  Thanks to [This Stack Overflow Post](https://stackoverflow.com/questions/58708752/flutter-textformfield-validator-not-called-when-field-is-not-visible-in-listvie) I realised that when the user scrolls to the bottom of the screen and some fields are no longer visible, the `ListView` removes them from the widget tree to save memory. This means that the validation logic for those fields is not executed, and the user can submit the form without filling in all the required fields.  I reverted the code to use a `SingleChildScrollView` and a `Column` for the form fields, which solved the problem.

## And Finally...

This week I have also...

🎧 Listened to: [Iron Maiden](https://www.last.fm/music/Iron+Maiden)  
🍿 Watched: [Cold Case](https://www.imdb.com/title/tt0368479)  
