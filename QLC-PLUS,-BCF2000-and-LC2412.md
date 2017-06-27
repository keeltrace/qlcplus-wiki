***

THIS HOWTO WAS INTEGRATED TO [ONLINE HELP](http://www.qlcplus.org/docs/tutorial-bcf-lc2412.html), AND IS KEPT HERE SO THAT OLD LINKS WORK.
PLEASE REFER TO ONLINE HELP FOR CURRENT VERSION.

***

This is small howto to setup QLC+ remote control with Behringer [LC2412](http://www.behringer.com/EN/Products/LC2412.aspx) connected through [BCF2000](http://www.behringer.com/EN/Products/BCF2000.aspx). Everything said here is also valid for [BCR2000](http://www.behringer.com/EN/Products/BCR2000.aspx).

With this setup (BCF2000 + LC2412) we get:
* 8 motorized faders
* 8 turn encoders
* 30 non-motorized faders
* lots of buttons

That makes a pretty nice console and a much less clicks with mouse :)

Now the steps:

1. Connect MIDI cable from LC2412 MIDI out to MIDI IN on BCF2000. Connect USB cable from BCF2000 to the computer.
1. Set BCF2000 to U-2 mode
   * Press and hold EDIT and then push STORE. 
   * Release both buttons. 
   * Turn the leftmost encoder until it shows u-2.
   * Push EXIT button.
1. Start QLC+
1. In the INPUT/OUTPUTs tab:
   * For one universe, choose BCF2000 MIDI 1 port; check both "input" and "feedback", and select BCF2000 profile
   * For another universe, choose BCF2000 MIDI 2 port; check "input" only - LC2412 does not have feedback capability. Choose LC2412 profile.
1. Now you can choose from knobs, faders and buttons of either device for your VC controls.
 
Enjoy!