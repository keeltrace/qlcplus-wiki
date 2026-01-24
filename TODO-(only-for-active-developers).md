* RGB Matrix:
  * add a simple internal editor to easily create images "on the fly" and export them (to BMP? PNG?)

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

* store speed dials state in function editors

* store order in Function Selection

* store expanded channels in channel groups editor


* QXF format:
   * sort Channels in Head
   * drop Head if only one head is present

# Small improvements

* allow multiple startup functions
* allow feedback for artnet/e1.31 (useful for remote control over artnet)
* allow patching multiple outputs (implemented in QLC+5)