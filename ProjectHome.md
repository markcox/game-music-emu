**IMPORTANT NOTE**: Google Code is shutting down code hosting services this year. Accordingly, this library is [moving to BitBucket](https://bitbucket.org/mpyne/game-music-emu) so that it remains available. It will continued to be maintained (though perhaps not actively feature-developed, unless more knowledgeable devs become available).

# Introduction #

game-music-emu is a collection of video game music file emulators that
support the following formats and systems:

| AY       | ZX Spectrum/Amstrad CPC |
|:---------|:------------------------|
| GBS      | Nintendo Game Boy |
| GYM      | Sega Genesis/Mega Drive |
| HES      | NEC TurboGrafx-16/PC Engine |
| KSS      | MSX Home Computer/other Z80 systems (doesn't support FM sound) |
| NSF/NSFE | Nintendo NES/Famicom (with VRC 6, Namco 106, and FME-7 sound) |
| SAP      | Atari systems using POKEY sound chip |
| SPC      | Super Nintendo/Super Famicom |
| VGM/VGZ  | Sega Master System/Mark III, Sega Genesis/Mega Drive,BBC Micro |

Features:
  * Can be used in C and C++ code
  * High emphasis has been placed on making the library very easy to use
  * One set of common functions work with all emulators the same way
  * Several code examples, including music player using SDL
  * Portable code for use on any system with modern or older C++ compilers
  * Adjustable output sample rate using quality band-limited resampling
  * Uniform access to text information fields and track timing information
  * End-of-track fading and automatic look ahead silence detection
  * Treble/bass and stereo echo for AY/GBS/HES/KSS/NSF/NSFE/SAP/VGM
  * Tempo can be adjusted and individual voices can be muted while playing
  * Can read music data from file, memory, or custom reader function/class
  * Can access track information without having to load into full emulator
  * M3U track listing support for multi-track formats
  * Modular design allows elimination of unneeded emulators/features

This library has been used in game music players for Windows, Linux on
several architectures, Mac OS, MorphOS, Xbox, PlayStation Portable,
GP2X, and Nintendo DS.