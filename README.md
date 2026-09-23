# Wing Mait

A companion app for WARDOGS that watches your screen and calls out what's happening, in a cast of seven radio voices.

Wing Mait sits alongside WARDOGS, reads what's visible on your game window, and speaks callouts out loud so you can keep your eyes on the fight. This repository hosts our release binaries and notes; the source stays in a private repository.

## What it does

- Watches the visible WARDOGS window and calls out contacts, downed teammates, objectives and more
- Seven selectable character voices, each with their own delivery
- Fixed or Follow minimap orientation, with measured bearing and distance callouts
- A mortar calculator and map panel with a firing solution on screen; the spoken fire solution (grid, bearing, elevation in mils) switches on with the military comms voice bank in the next update
- Runtime radio comms treatment per voice: Clear, or Radio with wandering signal quality, static and dropouts
- A compact on-screen device with rubber-keycap sounds and a "Say again" menu item to replay the last callout

## Download

- Latest release: [github.com/BAIS1C/wingmait-releases/releases/latest](https://github.com/BAIS1C/wingmait-releases/releases/latest)
- Or from the site: [wingmait.xyz/download](https://wingmait.xyz/download/)

## Requirements

- Windows 10 or 11, 64-bit
- WARDOGS running in a 16:9 window, anywhere from 1080p to 4K
- Minimap set to either fixed north-up or follow, matching what you tell Wing Mait in setup (see the guide below)
- An audio output device

## Getting started

Full setup walkthrough: [wingmait.xyz/guides/getting-started](https://wingmait.xyz/guides/getting-started/)

The short version: install, launch WARDOGS, launch Wing Mait, tell it whether your minimap is fixed or follows you, pick a character voice, and arm it.

## How it works, and what it doesn't do

Wing Mait reads pixels from your visible WARDOGS window using standard Windows screen-capture APIs (Windows Graphics Capture, with a GDI fallback). That's the entire input.

It does not inject into WARDOGS, read its process memory, hook its renderer, modify any game files, or send input of any kind. OBS is never required; it's only useful if you want to run WARDOGS through an OBS scene for streaming, which is unrelated to how Wing Mait watches your screen.

The only thing that leaves your machine is your licence key check against our licensing provider. Nothing about your gameplay, your screen, or your voice selections is sent anywhere.

Because this is observation-only, we can't and don't claim it's certified against any anti-cheat policy. We built it to only ever read what's already visible on your screen, and we think that's the right way to build a tool like this, but that's a design choice, not a guarantee about how WARDOGS' anti-cheat will treat it now or in the future.

## Beta status and known limits

This is a beta. Some things to know going in:

- The installer is unsigned, so Windows SmartScreen will flag it (see below); this is expected for now, not a sign something's wrong
- Multi-resolution support (1080p through 4K) is new and has had the most testing at native 4K; other resolutions and DPI settings, HDR, multi-monitor setups and less common audio devices haven't all been through the same testing yet
- The spoken mortar fire solution stays silent until the military comms voice bank ships in the next update
- We haven't tested every GPU, every Windows configuration, or every WARDOGS setting combination

**Coming soon:**

- Live mortar callouts read straight from your in-game map: mark a target and your Mait reads back grid, bearing and elevation.
- Voice callouts in more languages.

## Windows SmartScreen

Because this beta build isn't code-signed yet, Windows will likely show a SmartScreen warning when you run the installer. Click **More info**, then **Run anyway**. We know this is a bit of friction and we're working toward a signed release.

To confirm the file you downloaded is the one we published, check its SHA-256 hash against the value listed on the release page before you run it.

## Licensing

Wing Mait's source code is proprietary and stays private. This repository exists to host public release binaries, changelogs and release notes only, not source.

## Support

Questions, bug reports or feedback: reach us through [wingmait.xyz](https://wingmait.xyz/). We read everything that comes in.
