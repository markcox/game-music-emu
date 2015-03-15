# Introduction #

Hi, I'm Michael Pyne, still the "guest packager", now for the 0.6.0 release, which contains the accumulation of many changes since my first 0.5.5 release nearly 3 years ago.

# Changes #

You can look at the SVN repository on the [Google Code website](https://code.google.com/p/game-music-emu/source/list) to see the changes in this release (all changes from [r16](https://code.google.com/p/game-music-emu/source/detail?r=16) through [r43](https://code.google.com/p/game-music-emu/source/detail?r=43)), or consult changes.txt within the [source code release](https://game-music-emu.googlecode.com/files/game-music-emu-0.6.0.tar.bz2).

In short however, there are:

**Bugfixes to GBS emulation.** Minor code fixes, including support for systems with a single-precision `double` type.
**A new snes\_spc code import for improved SPC support.** A new API call `gme_enable_accuracy` to allow for choosing between accurate and fast code paths for supported music emulation cores (right now only SPC is supported).
**Build system improvements, including multilib fixes, Cygwin support, and pkg-config support.**

# Building #

You'll need at least [CMake](http://cmake.org/) version 2.6.

Then you'll need to do something like this (these are Linux/UNIX instructions.  Although CMake should work on Mac OS X and Windows I don't have those systems available to test, and you can always still build it yourself like you could before :P):

```
$ tar xjvf game-music-emu-0.6.0.tar.bz2
$ cd game-music-emu-0.6.0
$ mkdir build
$ cd build
$ cmake ../ -DCMAKE_INSTALL_PREFIX=/usr/local _See below for more options_
$ make && sudo make install
```


---


  * The `cmake ../` part is to run CMake, passing the parent directory (../) as the source directory.
  * -D for CMake begins a definition, so `-DCMAKE_INSTALL_PREFIX=/usr/local` sets the CMAKE\_INSTALL\_PREFIX (where CMake installs to) to `/usr/local`.  You can change this to be anywhere you'd like to install game-music-emu.
  * Compiling in only certain game music emulators is supported.  By default, all available types are compiled in.  You can remove a type by passing `-DUSE_GME_`_type_`=FALSE` on the command line when running CMake.  Make sure to pass more than one if you have more than one type to remove.  The valid options are listed below:

# Emulator types #

| Emulator type | CMake option |
|:--------------|:-------------|
| Spectrum ZX   | -DUSE\_GME\_AY=0 |
| Game Boy      | -DUSE\_GME\_GBS=0 |
| Sega Genesis  | -DUSE\_GME\_GYM=0 |
| NEC PC Engine / TurboGrafx-16 | -DUSE\_GME\_HES=0 |
| MSX / Other Z80 | -DUSE\_GME\_KSS=0 |
| NES |        -DUSE\_GME\_NSF=0 |
| NES Extended support | -DUSE\_GME\_NSFE=0 |
| Atari SAP | -DUSE\_GME\_SAP=0 |
| SNES      | -DUSE\_GME\_SPC=0 |
| Sega VGM/VGZ | -DUSE\_GME\_VGM=0 |

Note that some emulator code is shared.  For instance the audio processing code used by Spectrum ZX happened to also be used by PC Engine, so if you select PC Engine and disable Spectrum ZX, you may notice a bit of code still being used, but this is not an error.

# Detecting conditionally compiled emulators #

If you're a developer using libgme the only public API is the one defined in gme/gme.h

This API includes a `gme_type_list()` function, which you must call at runtime. It returns a NULL-terminated list of available types (alternately, you can simply try to play a file and allow libgme to fail if it doesn't support it).

# Testing #

To test the library, you can use the included very simple GUI player application (requires [SDL](http://www.libsdl.org/)) in the player/ directory.  It is not built by default, but you can cd to the game-music-emu/build/player directory and run make from there _after_ you've already run CMake.

From there just run `./player /path/to/file` on any supported file type.

# Contact #

If you have issues building you can contact Michael Pyne at mpyne at kde org.  I know a bit about emulation but absolutely nothing about the actual internals of how any of the emulator cores operate, so you'll still need to ask blargg or someone else if you have troubles with the actual operation of the emulators.