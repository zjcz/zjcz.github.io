---
layout: post
title: "What I Learnt This Week"
date: 2025-05-09 17:00:00
categories: what-i-learnt-this-week
tags: [flutter, github copilot, ai]
---

After a few months (15 to be exact) of not posting I thought it was time to get back into the habit of writing. Rather than traditional blog posts I have decided to document what I have been working on from week to week.

<!--more-->

## Why the change?

I have decided the internet has enough blog posts on how to do this, that and the other and doesn't need me adding to them. Rather than writing a blog post on how to do something which would probably be a re-write of someone elses blog posts I decided to simply summarise what I have been working on each week. This will allow me to document my progress and hopefully help others who are on a similar journey.

## Github Copilot

I have been using AI code assistants for a while with Flutter and while the code completions have been ok, I've found Agent mode to be a little underwelming. Possibly because Flutter is a relatively less common language compared to the likes of Javascript and Python, so there is less training data for the models.

This week I've been tinkering with the settings and have seen a massive improvement in the code it generates. Here's what I've done:

- Added a `copilot-instructions.md` file to the .github folder of my project. This file contains information for Copilot on how the project is structured, the libraries I use and how I want things such as tests generating. See [Use a .github/copilot-instructions.md file](https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilotinstructionsmd-file) for more information.
- Add the `hithub.copilot.chat.*` settings to the `settings.json` file. This allows me to configure the behaviour of Copilot in more detail for different tasks, such as code generation, test generation and commit message generation. For more information see [Specify custom instructions in settings](https://code.visualstudio.com/docs/copilot/copilot-customization#_specify-custom-instructions-in-settings)
- Added the [Context7](https://github.com/upstash/context7) MCP server. For more information on how to configure MCP servers in VS Code see [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers).
- Added a combined file from [flutter-ai-rules](https://github.com/evanca/flutter-ai-rules) which covers the technologies I use and how I want the code to be structured. This file is referenced in the `settings.json` to ensure it is pulled in when Copilot is generating code.

## Refreshing My Website

On Friday I decided to refresh my website. Nothing major, just fixing a few things, and I had the idea to update [Bulma](https://bulma.io/) to the latest version (I'm currently using v0.9.4). Unfortunately between v0.9.4 and now (currently v1.0.4) there has been a few changes, most notably alterations to the typeography and primary colours which changed the look of the site more than I liked.

What followed was a few hours of tinkering with the CSS to try and get it back to how I liked it. In the end I have decided to stick with v0.9.4 for now and will look at updating in the future when I have more time.

This has made me rethink my opinion on CSS frameworks. Over the years, I’ve read numerous articles advocating for pure CSS or less opinionated frameworks like [Tailwind](https://tailwindcss.com/). I’ve always preferred more opinionated frameworks like Bootstrap and Bulma – it's quicker to get up and running, and you don't have to wrestle with CSS as much. However, with ease of use comes the risk of adopting someone else's design choices, especially when upgrading.

## What Else?

I have continued to work on my current Flutter app, currently with the working title of [Pet Journal](https://github.com/zjcz/petjournal). More on this soon hopefully!
