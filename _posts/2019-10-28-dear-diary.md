---
layout: post
title: Setting up Git on Chromebook
---

## HELLO!

So you've bought a Chromebook because you thought it was cool, and now you've discovered you can't do _half_ the things you didn't realise you needed to do. Never fear! Most of these things can be achieved using a Chromebook, if you know where to look.

The Chromebook does have a terminal built in (crosh - hit ```ctrl``` + ```alt``` + ```T``` to access it), but it's not very good. Chromebooks are designed to obfuscate any file shenanigans from the user, so you can't actually go all Indiand Jones on your machine from crosh.

>Enter Termux

Termux is actually designed as an Android app, which means it's designed for people who are so terminal-obsessed that they want it on their phone. Jeez. Anyway, if you've got a relatively new Chromebook (your model was released in or since 2017), you can install Android apps. Head to the [Termux website](https://termux.com/) and download the app from the Play store.

From here you can hack away or guess at how to set things up, or follow [this idiot-proof guide](https://pedronveloso.com/proper-git-client-android/) like I did.

Keep in mind that this is installed and functions in the **Android** part of your machine - which is a black box inside the Chromium. This means if you download files on your Chromebook, they go into your Chrome OS downloads folder, _not_ the Android download folder. So literally you can't access any files you put on your machine in the conventional way. You have access to:
* files you grab through the terminal (such as cloning a git repository), and
* the files associated with any other Android apps you've installed on the machine. There's probably a way to hack this to your advantage, such as perhaps downloading the Android version of Chrome, and downloading web assets through that browser. I haven't tried this but it sounds dumb enough to work.
