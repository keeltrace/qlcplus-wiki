* merge pull request #189 https://github.com/mcallegari/qlcplus/pull/189 <br>
  Check the UI usability, code stability and cross-platform consistency

* merge pull request #191 https://github.com/mcallegari/qlcplus/pull/191 <br>
  Check "average user" accessibility to this functionality. The easier, the better

* Refine pull request #185 https://github.com/mcallegari/qlcplus/pull/185, considering the 4th cases identified by Jano:

  1. one dimmer channel per head, no rgb: PAR can
  2. one dimmer channel per head, rgb: LED PAR/LED moving head
  3. one dimmer per more heads, each head has own RGB: LED BAR
  4. no dimmer, only rgb: simple LED PAR

* Improve Function Wizard. There's a lot of space for more automatic creation of functions/widgets.
  To name a few:
  * Pan/Tilt movement should be translated into: degrees presets (0°, 90°, 180°, etc), EFX presets (diagonal, eight, lissajoux, etc), XY pad widgets
  * RGB/CMY-capable fixtures can ge grouped and some preset RGB matrices can be added
  * when users select more than one functionality for the same group of fixtures, it would be cool to compact them into multipage VC frames, instead of separate VC frames like it is right now