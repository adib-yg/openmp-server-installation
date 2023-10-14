# open-mp-server-setup
A comprehensive [open.mp](https://www.open.mp) server installation tutorial

**This tutorial is for those who want to convert their gamemode from SA:MP server to open.mp server**

- [Step 1](#step-1)
- [Step 2](#step-2)
- [Step 3](#step-3)
- [Step 4](#step-4)
- [Step 5](#step-5)

## Step 1
Download latest open.mp server version from https://github.com/openmultiplayer/open.mp/releases

<kbd>![](/screenshots/Screenshot%20(1).png)</kbd>

- `open.mp-win-x86.zip` **Windows** Server
- `open.mp-linux-x86.tar.gz` **Linux** Server

## Step 2
Extract the `.zip` or `tar.gz` file contents on your disk

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

**Important Note:** if you use these plugins, you must put the omp version of the plugin!

| Plugin  | OMP |
| ------ | --- |
| Pawn.CMD  | https://github.com/katursis/Pawn.CMD/releases/tag/3.4.0-omp |
| Pawn.RakNet  | https://github.com/katursis/Pawn.RakNet/releases/tag/1.6.0-omp |
| sampvoice  | https://github.com/AmyrAhmady/sampvoice/releases/tag/v3.1.5-omp |

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
and replace with
```pawn
#include <open.mp>
```
