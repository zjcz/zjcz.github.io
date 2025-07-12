---
layout: post
title: "What I Learnt This Week - 04 July 2025"
date: 2025-07-05 10:24:00
categories: what-i-learnt-this-week
tags: [gemini CLI, gemini, AI, coding assistant]
---

This week (and last) I have been playing with the new [Gemini CLI](https://github.com/google-gemini/gemini-cli) coding assistant.

<!--more-->

I was recently impressed while experimenting with Gemini in Android Studio for Flutter development, so I was eager to try Gemini CLI to see how well the AI agent performed.

While I haven't done any side-by-side comparisons or measured metrics like I'm sure some online sources will have, I have found Gemini to be a better coding agent than Github Copilot.  I found myself having to make less manual edits to the generated code than Github Copilot.  I am only basing this on my use on Flutter projects, which is a Google language so is probably favoured when training Gemini, whereas Github Copilot will probably favour popular languages like Javascript and Python over Flutter when training their models.  

I have been using Gemini CLI for almost a week now, building a new mobile app using Flutter and Firebase.  The apps logic isn't complex, but the code Gemini has generated has often been similar to how I would have written it myself and I haven't felt the need to do much refactoring. 

### Testing

While the quality of the code to generate the screens was generally good, the tests were less so and often required a number of manual fixes.  The issues seem like trivial things I have come across before so was quicker to fix them rather than execting Gemini to provide a solution.

- Generating tests that fail when a widget uses a [NetworkImage](https://api.flutter.dev/flutter/painting/NetworkImage-class.html) widget (This will always result in a HTTP status 400 response).  This can be avoided by using the [Network_Image_Mock](https://pub.dev/packages/network_image_mock) package.  Interestingly this happened for the first tests it generated, but later ones did use this package.  I'm unsure if it 'learned' this from the manual change I made to the tests.  
- Test for longer screens often fail as finder failed to find widgets that may be off the bottom of the screen.  Again manually adding code to scroll the widget into view fixed this.
- Tapping TextSpan widgets within a RichText widget fail.  Luckily this is a problem I have had before so I could port the fix manually. (See this [GitHub Issue](https://github.com/flutter/flutter/issues/56023#issuecomment-764985456) for a solution).
- Using old versions of packages when generating code.  It's always best to check the pubspec.yaml to see if a later version is available, although at times there could be a valid reason it has used an older version..

Maybe adding these to the `Gemini.md` will help avoid them in the future.

### Updating Gemini CLI

Finally as pointed out on this [reddit post](https://www.reddit.com/r/Bard/comments/1lmy2oi/if_youre_using_geminicli_dont_forget_to_update/), don't forget to update regularly:

```bash
sudo npm update -g @google/gemini-cli
```

## And Finally...

This week I have also...

🎧 Listened to: [Paradise Lost](https://www.last.fm/music/Paradise+Lost)  
🍿 Watched: [Cold Case](https://www.imdb.com/title/tt0368479) (Still!)
