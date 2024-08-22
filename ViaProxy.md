# Custom Skins with ViaProxy

How to use ViaProxy 3.3.4 + CustomSkinLoader to see player skins in Minecraft Java.

1. Download ViaProxy 3.3.4-Snapshot from Jenkins: https://ci.viaversion.com/view/All/job/ViaProxy/.
2. Install the attached Java mod to your Java Minecraft mods directory. This is effectively a fork of CustomSkinLoader (https://github.com/xfl03/MCCustomSkinLoader) but I've modified it to work with ViaProxy.
3. Configure Minecraft Java to show the debug log. This is under the launcher Settings in the bottom left and make sure "Open Output Log when Minecraft Java Edition Starts"
4. Paste the following JSON text to your `.minecraft/CustomSkinLoader` directory (create the directory as it doesn't exist).

```
{
  "version": "14.20.2",
  "buildNumber": 0,
  "loadlist": [
    {
      "name": "LocalSkin",
      "type": "Legacy",
      "checkPNG": false,
      "skin": "LocalSkin/skins/{USERNAME}.png",
      "model": "auto",
      "cape": "LocalSkin/capes/{USERNAME}.png",
      "elytra": "LocalSkin/elytras/{USERNAME}.png"
    }
  ],
  "enableDynamicSkull": true,
  "enableTransparentSkin": true,
  "forceLoadAllTextures": true,
  "enableCape": true,
  "threadPoolSize": 8,
  "enableLogStdOut": true,
  "cacheExpiry": 30,
  "forceUpdateSkull": true,
  "enableLocalProfileCache": true,
  "enableCacheAutoClean": true,
  "forceDisableCache": true
}
```

Along with the following sub directories

CustomSkinLoader\
 LocalSkin\
 skins\
 capes\
 elytra\

5. Launch Minecraft Java with a _separate_ account, and isolate your camera account, as the skin loading is based on render distance.
6. The debug log you'll see a debug line that looks similar as follows:

```
22:19:00.274
net.minecraft.class_2983
§b§3§§4§í§Å§¬§ô
[STDOUT]: [2024-08-21 22:19:00] [§b§3§§4§í§Å§¬§ô/INFO] [CustomSkinLoader Core]: Loading §b§3§§4§í§Å§¬§ô's profile (958042090ddb90878318fca1bda9c61)
```

In this instance: `958042090ddb90878318fca1bda9c61` is the ID of your camera account. 6. Launch Minecraft Bedrock, then move your main account within render distance of your camera account.
Once you get in render distance, you'll see another log entry saying "Loading <random text> Profile (<ID>)". This is the id you'll need to identify your skin.

```
22:19:00.274
net.minecraft.class_2983
§b§3§§4§í§Å§¬§ô
[STDOUT]: [2024-08-21 22:19:00] [§b§3§§4§í§Å§¬§ô/INFO] [CustomSkinLoader Core]: Loading §b§3§§4§í§Å§¬§ô's profile (791fbaa80573a56fb8690f35ce1f0957)
```

7. Quit Java, then move a copy of your skin to `CustomSkinLoader\LocalSkin\skins\<id>.png`.

As an Example, for my main account, this would be:

```
CustomSkinLoader\LocalSkin\skins\791fbaa80573a56fb8690f35ce1f0957.png
```

8. Relaunch Java and you should see your main player skinned. Note 3D skins, and the outer texture layer may not load correct. No idea why
