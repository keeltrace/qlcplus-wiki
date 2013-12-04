* MIDI SysEx: pull request #189 merged on November 14th. Now we should add some new valuable presets. For example a "BCF2000 Standard MIDI", so if you manually set it to "Logic" it will automatically switch to a mode usable with QLC+

* RGB Matrix image: add a simple internal editor to easily create images "on the fly" and export them (to BMP? PNG?)

* Refine pull request #185 https://github.com/mcallegari/qlcplus/pull/185, considering the 4 cases identified by Jano:

  1. one dimmer channel per head, no rgb: PAR can
  2. one dimmer channel per head, rgb: LED PAR/LED moving head
  3. one dimmer per more heads, each head has own RGB: LED BAR
  4. no dimmer, only rgb: simple LED PAR

* Improve Function Wizard. There's a lot of space for more automatic creation of functions/widgets.
  To name a few:
  * Pan/Tilt movement should be translated into: degrees presets (0°, 90°, 180°, etc), EFX presets (diagonal, eight, lissajoux, etc), XY pad widgets
  * RGB/CMY-capable fixtures can ge grouped and some preset RGB matrices can be added
  * when users select more than one functionality for the same group of fixtures, it would be cool to compact them into multipage VC frames, instead of separate VC frames like it is right now
  * improve widgets positioning. Right now it always assume the virtual console is empty
  * add click & go sliders for macros like gobos, color wheels, shutters, etc

*  Continue the idea of Stefan of adding a submaster to VC frames https://github.com/stefanriemens/qlcplus/commit/8ad9c07a4cb6604668477bbdcf798a41d92b05ac

* Control RGB matrices attributes through VC sliders. The first idea is to have 2 attributes available:
  * intensity
  * step position. In this way it would be possibile to connect a VC audio trigger, or to manually control the position of a matrix

* Proper functions stack - see [this post](https://sourceforge.net/p/qlcplus/discussion/general/thread/106cdbce/#9f32). Basically - LTP functions do not have default, they stay at last value (as their name says :) ). Sometimes it's not convenient.

* Folders:
   * Folders are not saved properly!!!
   * Add "Add new folder" to context menu
   * Add "Move to new folder" to context menu

* Multipage:
   * Fix pasting widgets
   * Add "Move to page X" to context menu