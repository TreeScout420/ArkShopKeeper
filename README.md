[README.txt](https://github.com/user-attachments/files/28431596/README.txt)
ArkShop Keeper - Public Self-Hosted Release
============================================

ArkShop Keeper is a self-hosted Discord bot for ArkShop on Ark: Survival Ascended servers.

This release is designed to run as a Windows .exe.


What it can do
--------------
- Add normal shop items with autocomplete
- Add blueprint items with quality/rating options
- Add dinos with autocomplete
- Build item packs
- Build mixed item/dino kits
- Save to one ArkShop config, a selected copy list, or every configured config
- Find shop entries by key/description
- Remove shop entries or kits by exact key
- Reload ArkShop by RCON
- Update bundled item and creature blueprint lists
- Check GitHub for update notifications


Important
---------
This is not an invite-only public Discord bot.

ArkShop Keeper must run on a machine that can access your ArkShop config.json files and can reach your ARK server RCON ports.

Do not share your real settings.json publicly. It contains your Discord bot token and RCON password.


Recommended Release Folder Layout
---------------------------------
Your public EXE release folder should look like this:

ArkShopKeeper/
  ArkShopKeeper.exe
  settings.json
  settings-commented.json
  README.txt
  arkids_scraper_2.0.py
  data/
    ark_items_blueprints.json
    ark_creatures_blueprints.json
    ark_items_scrape_failures.json
    ark_creatures_scrape_failures.json
    beacon_engrams_from_arkids.json
    beacon_creatures_from_arkids.json
    combined_engrams_blueprints.json
    combined_creatures_blueprints.json

The data folder is important. It contains the item and creature blueprint lists used for autocomplete and shop entries.

/shoplist update also uses this data folder. It updates the ArkIDs files and rebuilds the combined autocomplete files.


Do Not Include
--------------
Do not include these in the public release folder:

__pycache__/
*.pyc
your private settings.json
old ShopKeeperBob named files
duplicate ark_items/ark_creatures JSON files outside the data folder


First-Time Setup
----------------
1. Extract the ArkShopKeeper folder somewhere safe.

   Example:
   C:\ArkShopKeeper\

2. Open settings.json in Notepad or another text editor.

3. Fill in your Discord bot information:

   discord_token:
   Your Discord bot token from the Discord Developer Portal.

   guild_id:
   Your Discord server ID.

   admin_channel_id:
   The Discord channel ID where ArkShop Keeper commands are allowed.

4. Fill in your ArkShop config targets:

   default_config:
   The config target used when you do not choose a target in Discord.

   copy_to_these_configs:
   A custom group of configs used by target:copylist.

   arkshop_configs:
   The named ArkShop config.json files the bot can edit.

5. Fill in RCON:

   rcon.host:
   Usually 127.0.0.1 if the bot runs on the same machine as the ARK servers.

   rcon.password:
   Your ARK server RCON password.

   rcon.maps:
   Map names and RCON ports used by /reloadshop.

6. Optional: Fill in GitHub update settings:

   updates.enabled:
   true or false.

   updates.current_version:
   The version of the local EXE/package.

   updates.notify_on_startup:
   If true, ArkShop Keeper checks for updates when it starts.

   updates.github_repo:
   Your GitHub repo in OWNER/REPO format.

   Example:
   TreeScout420/ArkShopKeeper

   latest_release_api_url:
   Leave blank unless you want to manually override the GitHub API URL.

   update_url:
   Leave blank unless you want to use a custom raw JSON update file instead of GitHub Releases.

7. Save settings.json.

8. Double-click ArkShopKeeper.exe.

9. Watch the console window. You should see the bot log in and sync slash commands.

10. In Discord, test:

   /configs
   /sellitem
   /adddino
   /findentry
   /removeentry
   /reloadshop
   /checkupdates


Example settings.json
---------------------
Use your own values. Do not copy this exactly unless the IDs and paths are yours.

{
  "discord_token": "PASTE_YOUR_BOT_TOKEN_HERE",
  "guild_id": 123456789012345678,
  "admin_channel_id": 123456789012345678,

  "default_config": "default",

  "copy_to_these_configs": [
    "default",
    "island",
    "center",
    "rag"
  ],

  "arkshop_configs": {
    "default": "C:/Desktop/ArkShop_Test_Config/config.json",
    "island": "C:/Path/To/Island/ArkShop/config.json",
    "center": "C:/Path/To/Center/ArkShop/config.json",
    "rag": "C:/Path/To/Ragnarok/ArkShop/config.json",
    "val": "C:/Path/To/Valguero/ArkShop/config.json",
    "lostcolony": "C:/Path/To/LostColony/ArkShop/config.json",
    "astraeos": "C:/Path/To/Astraeos/ArkShop/config.json",
    "genesis": "C:/Path/To/Genesis/ArkShop/config.json"
  },

  "updates": {
    "enabled": true,
    "current_version": "1.0.0",
    "notify_on_startup": true,
    "github_repo": "OWNER/ArkShopKeeper",
    "latest_release_api_url": "",
    "update_url": ""
  },

  "rcon": {
    "host": "127.0.0.1",
    "password": "PASTE_RCON_PASSWORD_HERE",
    "maps": {
      "island": {
        "name": "The Island",
        "port": 27032
      },
      "scorched": {
        "name": "Scorched Earth",
        "port": 27034
      },
      "aberration": {
        "name": "Aberration",
        "port": 27033
      },
      "extinction": {
        "name": "Extinction",
        "port": 27030
      },
      "center": {
        "name": "The Center",
        "port": 27020
      },
      "rag": {
        "name": "Ragnarok",
        "port": 27036
      },
      "val": {
        "name": "Valguero",
        "port": 27038
      },
      "astraeos": {
        "name": "Astraeos",
        "port": 27037
      },
      "lostcolony": {
        "name": "Lost Colony",
        "port": 27035
      },
      "genesis": {
        "name": "Genesis",
        "port": 27039
      }
    }
  }
}


Config Targets
--------------
ArkShop Keeper can write to one config, your copy list, or every configured config.

default_config
  This decides which config is used when you do not choose a target in Discord.

copy_to_these_configs
  This is a custom group of config targets.
  Use target:copylist to write to these configs.

arkshop_configs
  These are the config.json paths ArkShop Keeper can edit.
  The left side is the target name you use in Discord.
  The right side is the real config.json file path.

Target examples:

target:default
  Writes to whatever default_config points to.

target:island
  Writes only to island.

target:copylist
  Writes to every target listed in copy_to_these_configs.

target:all
  Writes to every target listed inside arkshop_configs.


Recommended Safe Workflow
-------------------------
Use one test/default config first.

Example:

/sellitem item:Stone price:1 amount:1 quality:0 target:default
/findentry search:stone target:default
/removeentry key:stone target:default

Once you know it works, use:

target:copylist

or:

target:all

Do not use target:all unless you really want every configured config changed.


Commands
--------
/configs
  Shows configured ArkShop config targets and whether the paths exist.

/sellitem
  Adds a normal item/resource/artifact to ArkShop.

/addbp
  Adds an actual blueprint item with quality/rating options.

/adddino
  Adds a dino to ArkShop.

/pack start
  Starts a pack builder session.

/pack additem
  Adds an item to the current pack.

/pack adddino
  Adds a dino to the current pack.

/pack preview
  Shows the current pack before saving.

/pack save
  Saves the current pack to the selected target.

/pack cancel
  Cancels the current pack builder session.

/findentry
  Searches ShopItems and Kits by key or description.

/removeentry
  Removes an exact key from ShopItems or Kits.

/reloadshop
  Sends arkshop.reload to the selected map through RCON.

/shoplist update
  Updates the local item and creature blueprint lists.

/checkupdates
  Checks GitHub for a newer ArkShop Keeper release.


Item, Blueprint, and Dino Notes
-------------------------------
Normal items are saved under ShopItems.

Single dinos are saved under ShopItems.

Packs that contain only items can be saved as ShopItems.

Mixed item/dino packs should be saved as Kits.

If a pack is saved as a Kit, use the kit amount/default amount option to control how many are available.


Finding and Removing Mistakes
-----------------------------
Use /findentry before removing anything.

Example:

/findentry search:tek target:copylist

Then remove by exact key:

/removeentry key:tek_triceratops_random target:copylist

/removeentry checks both ShopItems and Kits.


Reloading ArkShop
-----------------
After editing a config, use:

/reloadshop

Choose the map/server to reload.

RCON reload only reloads the selected server's ArkShop plugin. It does not decide which config file was edited. Config editing is controlled by the target option on the add/remove/save commands.


Blueprint List Updates
----------------------
/shoplist update updates the local data files used for autocomplete and shop entry creation.

It uses:

data/ark_items_blueprints.json
data/ark_creatures_blueprints.json

and rebuilds:

data/beacon_engrams_from_arkids.json
data/beacon_creatures_from_arkids.json
data/combined_engrams_blueprints.json
data/combined_creatures_blueprints.json

If the data folder is missing, autocomplete and add commands may fail.


GitHub Update Notifications
---------------------------
ArkShop Keeper can check GitHub Releases for newer versions.

In settings.json:

"updates": {
  "enabled": true,
  "current_version": "1.0.0",
  "notify_on_startup": true,
  "github_repo": "OWNER/ArkShopKeeper",
  "latest_release_api_url": "",
  "update_url": ""
}

For normal GitHub Releases, only set:

github_repo

Example:

"github_repo": "TreeScout420/ArkShopKeeper"

Leave these blank:

"latest_release_api_url": ""
"update_url": ""

When you publish a release on GitHub, tag it like:

v1.0.0
v1.0.1
v1.0.2

The local current_version is compared against the latest GitHub release tag.

If the GitHub release tag is newer, ArkShop Keeper will notify the admin channel on startup if notify_on_startup is true.

You can manually check with:

/checkupdates


Building the EXE from Source
----------------------------
If you are building from source, install requirements first:

py -m pip install -r requirements.txt

Then build:

py -m PyInstaller --onedir --name ArkShopKeeper ArkShopKeeper.py

The finished EXE folder will be:

dist\ArkShopKeeper\

Copy these into dist\ArkShopKeeper\ before sharing:

settings.json
settings-commented.json
README.txt
arkids_scraper_2.0.py
data\


Public Release Packaging
------------------------
For a public release, package the finished folder like this:

ArkShopKeeper/
  ArkShopKeeper.exe
  settings.json
  settings-commented.json
  README.txt
  arkids_scraper_2.0.py
  data/

Do not package your private settings.json.

The public settings.json should contain placeholders only.


Troubleshooting
---------------
Bot opens and closes immediately:
  Run ArkShopKeeper.exe from Command Prompt so you can read the error.

Slash commands do not appear:
  Restart the bot and wait for slash command sync.
  Make sure guild_id is correct.
  Make sure the bot is invited to the server with application.commands permission.

Commands say wrong channel:
  Make sure admin_channel_id is the Discord channel where you are using commands.

Item/dino autocomplete is empty:
  Make sure the data folder exists.
  Make sure combined_engrams_blueprints.json and combined_creatures_blueprints.json exist.
  Run /shoplist update.

Add command says it worked but you do not see it:
  Use /findentry to confirm which config target contains the entry.
  Make sure you are looking at the same config path shown by /configs.
  Close and reopen your text editor if it had the config file open before the bot edited it.

Remove did not remove anything:
  Use /findentry first.
  /removeentry requires the exact key, not the display name.

RCON reload fails:
  Check rcon.host, rcon.password, and the selected map port.
  Make sure RCON is enabled on the ARK server.
  Make sure the server is online.

Update check fails:
  Make sure github_repo is in OWNER/REPO format.
  Make sure the GitHub repo has at least one release.
  Make sure the release tag looks like v1.0.0 or 1.0.0.


Versioning
----------
For the first public release:

APP_VERSION in ArkShopKeeper.py:
1.0.0

settings.json current_version:
1.0.0

GitHub release tag:
v1.0.0

For the next release, update all three to match the new version.

Example:

APP_VERSION:
1.0.1

settings.json current_version:
1.0.1

GitHub release tag:
v1.0.1


Security
--------
Never share:
- Real Discord bot token
- Real RCON password
- Private server paths if you do not want them public
- MySQL credentials from ArkShop config files

Always use a placeholder settings.json for public releases.


Credits / Support
-----------------
ArkShop Keeper is a self-hosted helper tool for ArkShop server admins.

Use it carefully. Always test on a backup or test config before pushing changes to live servers.
