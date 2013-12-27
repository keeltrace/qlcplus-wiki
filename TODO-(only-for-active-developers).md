* MIDI SysEx: pull request #189 merged on November 14th. Now we should add some new valuable presets. For example a "BCF2000 Standard MIDI", so the device can be perfectly usable with QLC+

* RGB Matrix:
  * add a simple internal editor to easily create images "on the fly" and export them (to BMP? PNG?)
  * check if master dimmer control works in every case

* Improve Function Wizard. There's a lot of space for more automatic creation of functions/widgets.
  To name a few:
  * Pan/Tilt movement should be translated into: degrees presets (0°, 90°, 180°, etc), EFX presets (diagonal, eight, lissajoux, etc), XY pad widgets
  * RGB/CMY-capable fixtures can ge grouped and some preset RGB matrices can be added
  * when users select more than one functionality for the same group of fixtures, it would be cool to compact them into multipage VC frames, instead of separate VC frames like it is right now
  * improve widgets positioning. Right now it always assume the virtual console is empty

*  VC Slider submaster. Implemented on 08/12/2013. Think of which options are worth to be added to the configuration page (custom list of widgets?)

* Add RGB matrices attributes:
  * step position. In this way it would be possibile to connect a VC audio trigger, or to manually control the position of a matrix

* Proper functions stack - see [this post](https://sourceforge.net/p/qlcplus/discussion/general/thread/106cdbce/#9f32). Basically - LTP functions do not have default, they stay at last value (as their name says :) ). Sometimes it's not convenient.

* Folders:
   * Add "Move to new folder" to context menu
   * add rename to context menu

* Add support for ENTTEC Mk2 MIDI input/output

* Add support for FX5 USB adapter. Creator not responding to emails. Might abandon this.

* Add support for ArtNet and E1.31 unicast transmission. This might be tricky as plugins know nothing about fixtures !

* add button to show speed dials for EFX; store the setting

* store current tab in EFX editor
* store order in Function Selection
* add cue list to audio triggers widgets ([discussion](https://sourceforge.net/p/qlcplus/discussion/general/thread/b46ac525))

* store expanded channels in channel groups editor
* apply to all fixtures - only to fixtures with the same mode
* EFX: Line 2 that goes in one direction only

* fixture/project saving: check saving ints/doubles for locale safety (for e.g. Slovak locale
  the numbers are not loaded/saved properly). Fix: replace QString::toDouble() with QLocale::c().toDouble(QString)
  and QLocale::c().toString(double)