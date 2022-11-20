---
title: "Mouse Boost"
date: 2020-07-06T14:02:31+05:30
draft: false
toc: false
images:
tags:
  - mac
  - mouse
  - tweaks
---

I'm lazy and I hate non productive work. Why move the mouse a whole inch, if half is enough? Why click forcefully when I can just tap?!

One of the main reason that I love Macbooks is the Trackpad. Nothing in else in the world currently matches that absolute marvel!
But there are a few things I tweak from the factory settings.

We are using the defaults command to change the settings rather than System Preferences. Take a look at [Pawel Grzybek&#39;s post](https://pawelgrzybek.com/change-macos-user-preferences-via-command-line/) to learn more.

## Speed

I like my mouse to be snappy. Not the 100% setting that macOS supports, faster.

```bash
defaults write -g com.apple.mouse.scaling -float 7.0
defaults write -g com.apple.trackpad.scaling -float 7.0
```

This speeds it up enough from the default 3.0

## Tap to click

The force touch trackpad is great, but I just don't like pressing down to click when I can just tap.

```bash
defaults write com.apple.AppleMultitouchTrackpad Clicking -bool true
defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad Clicking -bool true
```

## Three finger drag

I've already established the dislike to clicking. So, this helps to select/drag with just three fingers.

```bash
defaults write com.apple.AppleMultitouchTrackpad TrackpadThreeFingerDrag -bool true
defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadThreeFingerDrag -bool true

defaults write com.apple.AppleMultitouchTrackpad Dragging -bool false
defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad Dragging -bool false
```
