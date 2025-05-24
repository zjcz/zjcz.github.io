---
layout: post
title: "What I Learnt This Week - 23 May 2025"
date: 2025-05-23 14:20:00
categories: what-i-learnt-this-week
tags: [selfhosting, plex, jellyfin, memos, home server, docker]
---

This week I have been adding some self-hosted applications to my home server.

<!--more-->

## Home Server and Self Hosting

I have seen many videos and articles about self-hosting applications over the last year and it is something I have always wanted to do. A few months ago I setup a Proxmox server and installed a few containers but then decided I needed the machine for something else.  At the same time my Mac Mini, which I use as my main daily PC, kind of evolved into a home server as well. 

It started with installing [Ollama](https://ollama.com/), coupled with [Open Web UI](https://openwebui.com/) to have a fully local Chat GPT alternative. I also started running [Docker](https://www.docker.com/) to host some other applications, such as [IT Tools](https://it-tools.tech/). The beauty of Macs with M series chips is they are very powerful machines but very energy efficient so having it running 24/7 isn't too expensive. 

## Plex and Jellyfin

We use Plex as our home media server for music and movies (this is installed natively rather than through Docker). Generally it works very well but one annoying limitation I discovered this week is the Amazon Fire tablet version will only play 1 minute of a song, which a small child in our house isn't happy with. This can be fixed by signing up to Plex Pass which is a possibility.  I have been tempted to go with the Plex Lifetime Pass for a while now, but I know [lifetime doesn't always mean lifetime](https://www.wired.com/story/vpnsecure-canceled-all-lifetime-subscriptions-claiming-it-didnt-know-about-them/).

Anyway, to solve this problem I took a quick look at [Jellyfin](https://jellyfin.org/) which is a self-hosted alternative to Plex. It looks like it has a lot of the same features as Plex, but I have only played with the music library side so far.

When importing my music library it seems to struggle with multi disc albums and compilations so I had to spend a lot of time fixing the metadata, which to be fair is something I also had to do with Plex. Maybe this is a problem with the way I have organised my music rather than the applications :( But at least a small child can listen to full songs now!

## Self Hosted Note Taking App

I currently use Obsidian for my note taking which generally works well, but it requires a subscription to sync notes between devices (there are workarounds with plugins but these aren't ideal).

This week I installed [memos](https://github.com/usememos/memos) on my home server. The interface is closer to Google Keep, with multiple notes being shown on the screen at once compared to Obsidian's single note view. I am not sure if I will keep it, but it is nice to have a self-hosted alternative and as it's web based I can access it from all my devices without a subscription.

## What's Next?

I am keen to expand my self-hosted applications further, but I need to be careful not to overcomplicate things. I have seen some people running a lot of applications on their home servers and it can get messy quickly.  I don't want to fully replace all my cloud services, but am keen to use technology to make my life easier where possible. 