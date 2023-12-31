<a href="https://www.open.mp"><img src="/screenshots/open-mp-logo.png?raw=true" width="128" height="128" align="left"></a>
<h1>open.mp Server Installation</h1>
<a href="https://www.open.mp">Open Multiplayer</a> server installation tutorial!
<br><br>

**This tutorial is for those who want to transfer their gamemode from SA:MP server to open.mp server.**

> [!NOTE] 
> *If you are using the FCNPC plugin, please stop for now because this plugin does not work for open.mp currently.*

## Steps

- [Step 1](#step-1)
- [Step 2](#step-2)
- [Step 3](#step-3)
- [Step 4](#step-4)
- [Step 5](#step-5)
- [Step 6](#step-6)
- [Step 7](#step-7)
- [Step 8](#step-8)
- [Step 9](#step-9)
- [Step 10](#step-10)
- [Step 11](#step-11)
- [Step 12](#step-12)

## Step 1

Download the latest version of open.mp server files from https://github.com/openmultiplayer/open.mp/releases

<kbd>![](/screenshots/Screenshot%20(1).png)</kbd>

- `open.mp-win-x86.zip` **Windows** Server
- `open.mp-linux-x86.tar.gz` **Linux** Server
- `open.mp-linux-x86-dynssl.tar.gz` **Linux** Server (Dynamic SSL)

## Step 2

Extract the `.zip` or `.tar.gz` archive contents on your disk

<kbd>![](/screenshots/Screenshot%20(3).png)</kbd>

## Step 3

Create these folders in the **Server** directory:
- filterscripts
- gamemodes
- plugins
- scriptfiles
  
<kbd>![](/screenshots/Screenshot%20(4).png)</kbd>

## Step 4

Put your gamemode `.pwn` file in the **gamemodes** folder

## Step 5

Put required includes (e.g. `sscanf2.inc`, `streamer.inc`) in the **qawno/include** folder

> [!NOTE]
> If you are using the YSI-4 includes in your game mode, update to [YSI-5.x](https://github.com/pawn-lang/YSI-Includes/releases)

## Step 6

Put required plugins (e.g. `sscanf.dll`, `streamer.dll`) in the **plugins** folder

*______________________________________________________________________*

> [!IMPORTANT] 
> If you use the following plugins in table, you must put a version of the plugin that is compatible with omp!
> 
> Put the following plugins in the **../components** folder, not in the **../plugins** folder!

| Plugin            | OMP                                                                          |
|-------------------|------------------------------------------------------------------------------|
| Pawn.CMD          | https://github.com/katursis/Pawn.CMD/releases/tag/3.4.0-omp                  |
| Pawn.RakNet       | https://github.com/katursis/Pawn.RakNet/releases/tag/1.6.0-omp               |
| sampvoice         | https://github.com/AmyrAhmady/sampvoice/releases/tag/v3.1.5-omp              |
| discord-connector | https://github.com/maddinat0r/samp-discord-connector/releases/tag/v0.3.6-pre |
| SKY               | Use Pawn.RakNet instead                                                      |
| YSF               | You don't need YSF because open.mp already declared most of the same natives |
| FCNPC             | Currently not supported                                                      |

## Step 7

Open the qawno IDE program located at **Server/qawno/qawno.exe**

<kbd>![](/screenshots/Screenshot%20(5).png)</kbd>

## Step 8

Press **CTRL + O** then go to the **../gamemodes** folder and open your gamemode `.pwn` file

## Step 9

Find 
```pawn
#include <a_samp>
```
replace with
```pawn
#include <open.mp>
```
then press **F5** to compile.

> [!NOTE]
> If you are get error or warning, See [Compiler errors and warnings](#compiler-errors-and-warnings)

## Step 10

Open **config.json** file with Notepad or other IDEs

<kbd>![](/screenshots/Screenshot%20(9).png)</kbd>

## Step 11

Edit **config.json**

<kbd>![](/screenshots/Screenshot%20(11).png)</kbd>

Find
```json
"main_scripts": [
    "test 1"
],
```
replace with
```json
"main_scripts": [
    "your_gamemode_amx_file_name"
],
```

*______________________________________________________________________*

Find
```json
"legacy_plugins": [],
```
Specify required plugins
```json
"legacy_plugins": [
    "crashdetect",
    "mysql",
    "sscanf",
    "streamer",
    "PawnPlus",
    "pawn-memory"
],
```

*______________________________________________________________________*

Find
```json
"side_scripts": []
```
Specify your filterscripts
```json
"side_scripts": [
    "filterscripts/file_name"
]
```

Press **CTRL + S** to save changes.

## Step 12

Run the server

- **Windows**

Open the `omp-server.exe` program

<kbd>![](/screenshots/Screenshot%20(10).png)</kbd>

- **Linux**

```bash
./omp-server
```

## Compiler errors and warnings
- **warning 213: tag mismatch: expected tag "?", but found none ("_")**:

For example:

```pawn
TogglePlayerControllable(playerid, 1);
// ->
TogglePlayerControllable(playerid, true);
```

```pawn
TextDrawFont(textid, 1);
// ->
TextDrawFont(textid, TEXT_DRAW_FONT_1);
```


```pawn
GivePlayerWeapon(playerid, 4, 1);
// ->
GivePlayerWeapon(playerid, WEAPON_KNIFE, 1);
```

But you can ignore it for now:

```pawn
#define NO_TAGS
#include <open.mp>

// If the warning still occurs
// Use #pragma warning disable 213
```

*______________________________________________________________________*

- **warning 234: function is deprecated (symbol "TextDrawColor") Use `TextDrawColour**

Press **CTRL + F** in qawno and replace all `TextDrawColor` to `TextDrawColour`

<kbd>![](/screenshots/Screenshot%20(7).png)</kbd>

> [!NOTE]
> There are many other deprecated functions, you just need to replace them with the new function name.

*______________________________________________________________________*

- **warning 234: function is deprecated (symbol "GetPlayerPoolSize") This function is fundamentally broken.**
- **warning 234: function is deprecated (symbol "GetVehiclePoolSize") This function is fundamentally broken.**
- **warning 234: function is deprecated (symbol "GetActorPoolSize") This function is fundamentally broken.**

Replace `GetPlayerPoolSize()` with `MAX_PLAYERS`

Replace `GetVehiclePoolSize()` with `MAX_VEHICLES`

Replace `GetActorPoolSize()` with `MAX_ACTORS`

*______________________________________________________________________*

- **warning 234: function is deprecated (symbol "SHA256_PassHash") Use BCrypt for hashing passwords**

Use the [samp-bcrypt](https://github.com/Sreyas-Sreelal/samp-bcrypt) plugin for hashing passwords

*______________________________________________________________________*

- **warning 214: possibly a "const" array argument was intended: "?"**
- **warning 239: literal array/string passed to a non-const parameter**

For example:

```pawn
public MyFunction(string[])
// ->
public MyFunction(const string[])
```

*______________________________________________________________________*

- **error 025: function heading differs from prototype**

For example:

```pawn
public OnPlayerDeath(playerid, killerid, reason)
// ->
public OnPlayerDeath(playerid, killerid, WEAPON:reason)
```

```pawn
public OnPlayerEditAttachedObject(playerid, response, index, modelid, boneid, Float:fOffsetX, Float:fOffsetY, Float:fOffsetZ, Float:fRotX, Float:fRotY, Float:fRotZ, Float:fScaleX, Float:fScaleY, Float:fScaleZ)
// ->
public OnPlayerEditAttachedObject(playerid, EDIT_RESPONSE:response, index, modelid, boneid, Float:fOffsetX, Float:fOffsetY, Float:fOffsetZ, Float:fRotX, Float:fRotY, Float:fRotZ, Float:fScaleX, Float:fScaleY, Float:fScaleZ)
```

*______________________________________________________________________*

> [!NOTE]
> There is also an upgrade tool that attempts to find old untagged and const-incorrect code and upgrade it.
>
> https://github.com/openmultiplayer/upgrade
>
>  Already included in `/qawno/upgrader` folder.

## Useful documents
If you are completely new to Pawn programming: [readme-beginner](https://github.com/openmultiplayer/omp-stdlib/blob/master/documentation/readme-beginner.md)

If you are an intermediate at Pawn programming: [readme-intermediate](https://github.com/openmultiplayer/omp-stdlib/blob/master/documentation/readme-intermediate.md)

If you are an expert at Pawn programming: [readme-expert](https://github.com/openmultiplayer/omp-stdlib/blob/master/documentation/readme-expert.md)

## Help
If you still have issues running the server, please join the [official open.mp Discord server](https://discord.gg/samp)

https://discord.gg/samp

Ask at [#openmp-support](https://discord.com/channels/231799104731217931/966398440051445790)
