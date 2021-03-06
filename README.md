# react-gambatte

This package is a port of Gambatte for WebAssembly. Original README below.
The emulator runs completely in the users' browsers; no backend needed. Please
note that the license is GPLv2 (due to Gambatte), this may limit your usage of
this library.

## Usage

```bash
npm install react-gambatte --save
```

See stories/index.stories.js for an example of usage.

### Props

|     Prop     |                  Description                    | Default |
|:-------------|:-----------------------------------------------:|--------:|
| paused       | Whether the emulator should run                 |   false |
| samplerate   | Audio sample rate                               |   44100 |
| bufferLength | Length of audio buffer                          |     512 |
| buttons      | Set of currently pressed buttons                |         |
| romData      | Uint8Array of binary ROM data                   |         |
| volume       | Audio volume, between 0.0 and 1.0               |     1.0 |
| width        | Width of the screen, inserted to CSS            |   160px |
| onError      | Called when an error has occurred               |         |
| onTitle      | Called when a game has been successfully loaded |         |

Due to the blitting being driven by the audio callback (yes I know that's
weird), lowering 'bufferLength' lowers __both__ input lag and audio lag at the
expense of extra CPU use. Typically, you get buttons from KeyboardController.

## Building

For building the WebAssembly part, you need the [Meson build system](http://mesonbuild.com/)
and [Emscripten](https://github.com/kripken/emscripten).
Ensure that the [Emscripten binaries are in PATH.](https://kripken.github.io/emscripten-site/docs/getting_started/downloads.html#updating-the-sdk)

```bash
$ npm install
$ npm run build
```

## Testing

After building the WebAssembly part, you can try it out using Storybook.

```bash
$ npm run storybook
```

# Gambatte README

```
--------------------------------------------------------------------------------
--------------------------------------------------------------------------------
Copyright (C) 2007 by sinamas <sinamas at users.sourceforge.net>

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License version 2 as
published by the Free Software Foundation.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License version 2 for more details.

You should have received a copy of the GNU General Public License
version 2 along with this program; if not, write to the
Free Software Foundation, Inc.,
51 Franklin St, Fifth Floor, Boston, MA  02110-1301, USA
--------------------------------------------------------------------------------
--------------------------------------------------------------------------------

About
--------------------------------------------------------------------------------
Gambatte is a portable, open-source Game Boy Color emulator.

The core emulation code is contained in a separate library backend
(libgambatte) written in platform-independent C++. There is currently a Qt GUI
frontend (gambatte_qt), and a simplistic command-line interface SDL frontend
(gambatte_sdl).

The Qt frontend has been ported to Windows, Mac OS X, and Linux/BSD/Unix-like
OSes with audio/video engines utilizing native APIs on these platforms.

The SDL frontend should be usable on all platforms with a working SDL port. It
should also be quite trivial to create new (simple) frontends (note that the
library API should in no way be considered stable).

Usage
--------------------------------------------------------------------------------
You will have to supply Gambatte with a ROM image file of the GB/GBC
program/game you would like to run/play, either as a command line argument, or
through the File->Open... menu in gambatte_qt.

gambatte_sdl keyboard commands:
TAB    - fast-forward
Ctrl-f - toggle full screen
Ctrl-r - reset
F5     - save state
F6     - previous state slot
F7     - next state slot
F8     - load state
0 to 9 - select state slot 0 to 9

Default key mapping:
Up:     Up
Down:   Down
Left:   Left
Right:  Right
A:      D
B:      C
Start:  Return
Select: Shift

Compiling
--------------------------------------------------------------------------------
Building Gambatte from source code can be done by executing the
build_<qt/sdl>.sh scripts for the qt/sdl frontends respectively, or by issueing
the correct build command (either 'scons' or 'qmake && make') in the top-level
subdirectories (libgambatte will have to be built first). The clean.sh script
can be executed to remove all generated files after a compile (including
binaries).

Requirements for building libgambatte:
- A decent C++ compiler (like g++ in the GNU Compiler Collection).
- SCons.
- optionally zlib

Requirements for building gambatte_sdl:
- A decent C++ compiler (like g++ in the GNU Compiler Collection).
- SDL headers and library.
- SCons.
(- libgambatte.)

Requirements for building gambatte_qt:
- A decent C++ compiler (like g++ in the GNU Compiler Collection).
- Qt4 (Core, GUI, OpenGL) headers and library.
- Qmake and make (GNU Make should work).
- Platform-specific requirements:
  * MS Windows:
    - Win32 API headers and libraries.
    - DirectSound and DirectDraw7 headers and libraries.
    - Direct3D9 headers
  * Linux/BSD/UNIX-like OSes:
    - POSIX/UNIX headers (unistd.h, fcntl.h, sys/ioctl.h, sys/time.h, sys/shm.h).
    - Open Sound System header (sys/soundcard.h).
    - X11 Xlib, XVideo, XRandR and XShm headers and libraries.
    - Alsa headers and library (Linux only).
  * Max OS X:
    - Recent Mac OS X SDK (Panther Xcode/SDK should work)
(- libgambatte.)

Installing after a compile simply amounts to copying the generated binary
(either gambatte_qt/bin/gambatte_qt<.exe> or gambatte_sdl/gambatte_sdl<.exe>)
to wherever you'd like to keep it.

Thanks
--------------------------------------------------------------------------------
Derek Liauw Kie Fa (Kreed)
Gilles Vollant
Jeff Frohwein
Jonathan Gevaryahu (Lord Nightmare)
kOOPa
Marat Fayzullin
Martin Korth (nocash)
Maxim Stepin (MaxSt)
Nach
Pan of Anthrox
Pascal Felber
Paul Robson
SDL
Shay Green (blargg)
The OpenGL Extension Wrangler Library

--------------------------------------------------------------------------------
Game Boy and Game Boy Color are registered trademarks of
Nintendo of America Inc.
Gambatte is not affiliated with or endorsed by any of the companies mentioned.
```
