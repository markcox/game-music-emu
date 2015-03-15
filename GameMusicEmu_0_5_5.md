# Introduction #

Hi, I'm Michael Pyne, the "guest packager" for the 0.5.5 release.  A couple of months ago I asked blargg for help in "libifying" game-music-emu.  So, he added me an account and told me to get busy. ;)  This release is the result.

# No, seriously, what? #

Several months ago I submitted a patch to the [GStreamer](http://gstreamer.freedesktop.org/) developers to use game-music-emu for the gst-spc plugin.  See GNOME [bug 576800](http://bugzilla.gnome.org/show_bug.cgi?id=576800).  This plugin is used to allow playback of the SNES SPC700-format sound, and had previously used an older, x86-only library.  Not the end of the world, but game-music-emu was better and more portable (hence, my patch).

The GStreamer guys naturally didn't like how I had basically submitted game-music-emu's SPC code with some makefile tweaks, and preferred to simply have a library to link against.  But game-music-emu has no build system to make a library.  It was around this point I asked blargg and recommended [CMake](http://www.cmake.org/), since it's what we use on [KDE](http://www.kde.org/).

The CMake support has been added for some time now but I've only now gotten around to polishing it up and making a release.  Next is to re-do the patch for gstreamer.

# Building #

You'll need at least CMake version 2.6.

Then you'll need to do something like this (these are Linux/UNIX instructions.  Although CMake should work on Mac OS X and Windows I don't have those systems available to test, and you can always still build it yourself like you could before :P):

```
$ tar xjvf game-music-emu-0.5.5.tbz2
$ cd game-music-emu-0.5.5
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

There are two cases to consider if you're a developer:

  1. Detecting available emulators at compile time.  This can be done using the installed gme/gme\_types.h header file.  It is defined in the source code as gme/gme\_types.h.in and filled in by CMake.
  1. Detecting available emulators at run time.  Call the gme\_type\_list() function defined in gme/gme.h to return a NULL-terminated list of available types at runtime.

# Testing #

To test the library, you can use the included very simple GUI player application (requires [SDL](http://www.libsdl.org/)) in the player/ directory.  It is not built by default, but you can cd to the game-music-emu/build/player directory and run make from there _after_ you've already run CMake.

From there just run `./player /path/to/file` on any supported file type.

# Contact #

If you have issues building you can contact Michael Pyne at mpyne at kde org.  I a bit about emulation but absolutely nothing about the actual internals of how any of the emulator cores operate so you'll still need to ask blargg or someone else if you have troubles with the actual operation of the emulators.