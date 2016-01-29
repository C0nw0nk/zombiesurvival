# Garry's Mod Zombie Survival

This zombie survival version is my edited version of jetboom's what just fixes trolling issues and other annoyances for server owners.

Version number as stated inside Jetboom's LICENSE file : `"VERSION Xx420xX3, 19 January 2015"`

This is the latest version of Zombie Survival that was released of Jteboom's GitHUB, There are no other changes that will be different than the ones listed below.


#Fixes and added Features :

##Fixes :

Fixed glitched weapon / ammo pickups.

Fixed building of Flesh Creeper nests.

Fixed Zombie Vision.

Anti Bunny Hopping fix. (When player touches ground take away and divide their velocity by two (in half).)

Fixed humans not being able to phase out of props they are stuck in or ontop of.

Fire rates spamming reload or clicking extremely fast allows you to fire faster than intended. (With external programs such as autohotkey and pistols you could unload a entire clip in less than a second.)

Blaster shotgun fire rate glitching.

Boomstick fire rate glitching.

Sweeper shotgun fire rate glitching.

Annabelle rifle fire rate glitching.

Battle Axe pistol fire rate.

Deagle pistol fire rate.

Eraser pistol fire rate.

Glock pistol fire rate.

Magnum fire rate.

Medic Gun fire rate.

Owens pistol fire rate.

Peashooter pistol fire rate.

Redeemers fire rate.

Waraxe pistol fire rate.

Pulse pistol (z9000) fire rate.

##Additions :

Added health bar to Arsenal Crate.

Added health bar to Resupply Box.

Added name and health bar to Spotlamp.

During intermission display to living zombies who will be next boss.

Added JetBoom's HitBox fix. https://github.com/C0nw0nk/zombiesurvival/pull/1/files

For more additional features see my external hook's.

https://github.com/C0nw0nk/Garrys-Mod-Zombie-Survival

##Removed :

Removed the draw written inside Resupply box that says "ur a faget".

# How to install :

Install the addon to the `"/garrysmod/gamemodes/"` folder.

The path to should look like this : `"/garrysmod/gamemodes/zombiesurvival/"`

# How to use :

For those who intend on running public game servers you must also add to your servers command line the following.

`+gamemode zombiesurvival`

In full your command line should be similar to this.

`srcds.exe -console -game garrysmod +gamemode zombiesurvival +map zs_map_name`

# Secure your Server :

Nobody likes playing with cheaters so in order to prevent the cheating and hacking that revolves highly around the ZS game mode you should apply / consider running the following.

A Anti-Cheat : https://scriptfodder.com/scripts/view/460

To your servers command line add the following.

`+sv_pure 1` This will allow clients to only use models and files the server provides them with nothing modified or custom they have put into their folders. Because of the moronic confusion going on over the sv_pure command if you have custom models, sounds etc server side for the client to download and use then yes those will still work fine. Its a whitelist for server sided files if it does not exist on the server then the client is not allowed to use it simple.
In a nut shell sv_pure 1 enforces only what is in the models sounds etc server folders for the client to be able to use. If the client has extra files that do not match with the server they can't use them. (Prevents wallhacks etc.)

Should look like this : `srcds.exe -console -game garrysmod +gamemode zombiesurvival +sv_pure 1`

Disable clients from executing client side lua files : `+sv_allowcslua 0`

Should look like this : `srcds.exe -console -game garrysmod +gamemode zombiesurvival +sv_allowcslua 0`

Merge both the commands above your command line should be similar to this : `srcds.exe -console -game garrysmod +gamemode zombiesurvival +sv_pure 1 +sv_allowcslua 0`

Disable RCON weak RCON passwords or people guessing / bruteforcing or even dictionary attacking as well as other methods are a key flaw in servers you should disable RCON to not allow anyone to execute server sided commands via their client ingame console.

Setting the password to empty will disable RCON `rcon_password ""`

Prevent Clients uploading custom files to the server `sv_allowupload 0` there have been 0 day exploits in the past to do with players uploading files to the server with the following setting `sv_allowupload 0` will ensure that if these problems return we won't see them again. (The only downside effect this has is players can not upload or use/place their sprays ingame.)

An Admin addon to moderate and punish players my recommendation is ULX because it is the most popular and reliable as well as updated and maintained : http://ulyssesmod.net/downloads.php

Prevent players bypassing bans using Steam's family sharing features or throwing their money at Garry to buy the game over and over to troll your server : https://github.com/C0nw0nk/Garrys-Mod-Family-Sharing

# Secure Your Fast Downloads (FastDL sv_downloadurl) :

Nobody likes content scrappers, leechers nor people who hotlink of your servers fast download path consuming your money / bandwidth so here is the soloution.

##### Apache (.htaccess) :
```
# Check the user agent is Half Life 2.
SetEnvIfNoCase User-Agent "^Half-Life 2$" is_hl2
# Take into consideration blank / empty referers that are set to none.
SetEnvIf Referer "^$" valid_ref

# First server.
SetEnvIfNoCase Referer "^hl2:\/\/1\.2\.3\.4:27015$" valid_ref
# Second server.
SetEnvIfNoCase Referer "^hl2:\/\/1\.2\.3\.4:27016$" valid_ref

<RequireAll>
        Require env is_hl2
        Require env valid_ref
</RequireAll>

# Disable the directory indexing so we do not display to everyone the contents of the folder.
Options -Indexes
```

##### Nginx (location config) :
```
location /download-path/ {
  set $allowthis 0;
  # Check the user agent is Half Life 2.
  if ($http_user_agent != "Half-Life 2") {
    return 444;
  }
  # Take into consideration blank / empty referers that are set to none.
  if ($http_referer = "^$") {
    set $allowthis 1;
  }
  
  # First Server.
  if ($http_referer = "hl2://1.2.3.4:27015") {
    set $allowthis 1;
  }
  # Second Server.
  if ($http_referer = "hl2://1.2.3.4:27016") {
    set $allowthis 1;
  }

  if ($allowthis = 0) {
    return 444;
  }
  
  # Disable the directory indexing in nginx this is off by default but just to be sure we set it here.
  autoindex off;
}
```
