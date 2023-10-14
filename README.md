# open.mp Server Installation

[Open Multi Player](https://www.open.mp) server installation tutorial!

**This tutorial is for those who want to convert their gamemode from SA:MP server to open.mp server**

*Note: If you are using the FCNPC plugin, please stop for now because this plugin does not work for open.mp at the moment.*

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

Download latest open.mp server files from https://github.com/openmultiplayer/open.mp/releases

<kbd>![](/screenshots/Screenshot%20(1).png)</kbd>

- `open.mp-win-x86.zip` **Windows** Server
- `open.mp-linux-x86.tar.gz` **Linux** Server

## Step 2

Extract the `.zip` or `.tar.gz` file contents on your disk

<kbd>![](/screenshots/Screenshot%20(3).png)</kbd>

## Step 3

Create these folders in the **Server** folder:
- filterscripts
- gamemodes
- plugins
- scriptfiles
  
<kbd>![](/screenshots/Screenshot%20(4).png)</kbd>

## Step 4

Put your gamemode `.pwn` file in the **gamemodes** folder

## Step 5

Put required includes (e.g. `sscanf2.inc`, `streamer.inc`) in the **qawno/include** folder

## Step 6

Put required plugins (e.g. `sscanf2.dll`, `streamer.dll`) in the **plugins** folder

*______________________________________________________________________*

**Important Note:** If you use the following plugins in table, you must put a version of the plugin that is compatible with omp!

**Important Note:** Put the following plugins in the **components** folder, not in the **plugins** folder!

| Plugin  | OMP |
| ------ | --- |
| Pawn.CMD  | https://github.com/katursis/Pawn.CMD/releases/tag/3.4.0-omp |
| Pawn.RakNet  | https://github.com/katursis/Pawn.RakNet/releases/tag/1.6.0-omp |
| sampvoice  | https://github.com/AmyrAhmady/sampvoice/releases/tag/v3.1.5-omp |
| SKY  | Use Pawn.RakNet instead |
| YSF  | You don't need YSF because open.mp already declared most of the same natives |

## Step 7

Open qawno IDE program located in **Server/qawno/qawno.exe**

<kbd>![](/screenshots/Screenshot%20(5).png)</kbd>

## Step 8

Press **CTRL + O** then open your gamemode `.pwn` file in the **/gamemodes** folder

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

If you are get error or warning, See [Compiler errors and warnings](#compiler-errors-and-warnings)

## Step 10

Open **config.json** file with Notepad or other IDEs

## Step 11

Edit **config.json**

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
"side_scripts": [],
```
Specify your filterscripts
```json
"side_scripts": [
    "filterscripts/file_name"
],
```

## Step 12

Run the server

**Windows**

Open `omp-server.exe`

**Linux**

```bash
./omp-server
```

## Compiler errors and warnings
- **warning 213: tag mismatch: expected tag "?", but found none ("_")**:

You can ignore it for now with:
```pawn
#define NO_TAGS
#include <open.mp>

// If the warning still occurs
// Use #pragma warning disable 213
```

*______________________________________________________________________*

- **warning 234: function is deprecated (symbol "TextDrawColor") Use `TextDrawColour**

Press **CTRL + F** in qawno and replace all `TextDrawColor` to `TextDrawColour`

*______________________________________________________________________*

- **warning 214: possibly a "const" array argument was intended: "?"**
- **warning 239: literal array/string passed to a non-const parameter**

e.g.
```pawn
public MyFunction(string[])
```
->
```pawn
public MyFunction(const string[])
```

*______________________________________________________________________*

- **error 025: function heading differs from prototype**

e.g.
```pawn
public OnVehicleMod(playerid, vehicleid, componentid)

public OnVehiclePaintjob(playerid, vehicleid, paintjobid)
```
->
```pawn
public OnVehicleMod(playerid, vehicleid, component)

public OnVehiclePaintjob(playerid, vehicleid, paintjob)
```
