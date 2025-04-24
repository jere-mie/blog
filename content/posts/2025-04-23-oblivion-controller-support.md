---
title: How to Actually Enable Controller Support in The Elder Scrolls Oblivion (Original)
date: 2025-04-23
draft: false
author: Jeremie Bornais
--- 

With the new Oblivion remaster now released, I'm sure there are others like me who want to re-experience the game but don't want to spend the money for the remaster, or don't have the hardware to properly run it. Moreover, I'm sure there are others like me who grew up playing games on consoles and don't like keyboard+mouse controls. If you're one of these people, this article is for you.

## FYI

Before I get into the specifics of how to enable controller support, I thought it'd be prudent to give a bit of a heads up. This process involves modding Oblivion, something I have very little experience doing. I tinkered around with Skyrim years ago but never really got into the modding scene. For me, whenever I started adding mods to the game I played them for a bit before getting disinterested. I'm sure there are great mods out there that add lots of new content to the game, but this isn't something I'm interested in.

Further, there are certainly many others who are much more knowledgeable about modding than me (you may even be one of them). What I'm sharing is my experience modding Oblivion from the perspective of someone who knows very little about modding. Your mileage may vary.

## Initial Attempt

I really don't like mod managers, so my first attempt at adding controller support to Oblivion aimed to do so without using one. Theoretically, this should be possible. All a mod manager really does is handle the downloading and placement of the mod files in the Oblivion directory on your PC.

So, I found [this tutorial](https://youtu.be/9jDMRpQcZOs) and followed it exactly (or so I believe). The result - nothing. As far as I could tell, the mods were not being loaded when I ran Oblivion. As I said before, however, your mileage may vary. If you're like me and don't like using mod managers I encourage you to try this method. All I ask is if you do get it working, consider reaching out and letting me know if you did anything different from the video, as I would still love to eventually dump my mod manager.

If you don't want to watch the video, the steps are essentially:

- Download Oblivion from Steam and run it at least once
- Download [OBSE](https://obse.silverlock.org/) and extract the contents directly in your Oblivion folder
- Download [NorthernUI](https://www.nexusmods.com/oblivion/mods/48577) (manual) and extract the contents to the `Data` folder within the Oblivion folder
- Download [SkyBSA](https://www.nexusmods.com/oblivion/mods/49568) (manual) and do the same

Note: You'll need a nexusmods account to download these.
Note2: Your Oblivion folder is likely in `C:\Program Files (x86)\Steam\steamapps\common\Oblivion` (I manually typed that out so it's probably slighyly wrong)

## What Actually Worked for Me

Ok so what actually worked for me? After fiddling around with several different tutorials and trying to get this working without a mod manager, I finally tried [this tutorial](https://www.youtube.com/watch?v=0zgp_x8293Q) which uses the [Vortex Mod Manager](https://www.nexusmods.com/about/vortex).

The steps are essentially:

- Download Oblivion from Steam and run it at least once
- Download and install [Vortex Mod Manager](https://www.nexusmods.com/about/vortex) (requires nexusmods account)
- Download [NorthernUI](https://www.nexusmods.com/oblivion/mods/48577) (via the `Vortex` button) and it'll be automatically installed
- Do the same with [SkyBSA](https://www.nexusmods.com/oblivion/mods/49568)
- At some point during the installation of the above two mods you'll get a notification in the top right of Vortex saying you'll need to install OBSE. Simply click on the notification and follow the relevant steps
- After that, simply start up Oblivion from Vortex (click the play button in the top left) and you'll be all set! It's important you start up Oblivion from within Vortex. For some reason, if you start it from Steam it doesn't work properly

### Additional Mods

Some other mods I installed for quality of life improvements:

- [EngineBugFixes](https://www.nexusmods.com/oblivion/mods/47085)
- [Unofficial Oblivion Patch - UOP](https://www.nexusmods.com/oblivion/mods/5296)
