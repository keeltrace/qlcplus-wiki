### Interfacing to Mixxx via MIDI (Linux)

This tutorial explains how to drive QLC+ via MIDI from Mixxx. [Mixxx](http://www.mixxx.org/) is an open source DJ application, running on Windows, Mac OSX and Linux. The light effects are geared to a disco setup and we will use the beat detection of Mixxx to drive light effects synchronized with music.

The instructions were tested on Linux, but Windows or MacOS should be similar.

## Prepare and configure Mixxx

We need Mixxx to send information about the music via MIDI to QLC+. For this capability we need a plugin script in Mixxx which sends the information as MIDI events.

* Install Mixx, I used version 1.11
* Install the 'MIDI_for_light' script from this (<A HREF="http://mixxx.org/forums/viewtopic.php?f=7&t=4732">Mixxx forum thread</A>)
The script files (xms + js) must be installed in /usr/share/mixxx/controllers.
* Run Mixxx in developer mode with the command 'mixxx --developer'.
This is necessary because Mixxx hides the 'Midi Through' interface but we need it.
* Start Mixxx, go to 'Options - Preferences - Controllers', select 'Midi Through', enable it and load the Preset 'MIDI for light' from the list.
<P>This will enable the sending of Midi events. You can now run a midi monitor, like 'kmidimon', connect it to the 'Midi Through' device and look at the all the events. Be careful, Mixxx sends 40 events 25 times per second. It to my kmdimon only a minute or two to hang because of overload.


## Configure QLC+

Now we have Mixxx sending us lots of interesting data and want QLC+ to do something with it.

* Install QLC+, I used version 4.8.2
* Define your fixtures and functions as usual
* In the 'Inputs/Outputs' panel, select the 'MIDI Through' device as input
* Select the MIDI Through device and click on plugin configuration <IMG SRC="http://qlcplus.sourceforge.net/docs/gfx/configure.png"> and configure the 'Midi Through' device. Then:
    * Set the 'Midi' Channel to 1
    * Set the 'Mode' to 'Note Velocity'
    * Leave the 'Init Message' on 'None'
    * Push EXIT button.
* In the Profile tab of the 'Inputs/Outputs' screen, add a new Input Profile. I called it 'Mixxx' and model 'MIDI'.<BR>
Here we need to add a Channel for each MIDI message we expect from Mixxx. The list of Midi messages is documented in the file 'VU-Meter_Info.txt' you got with the Mixxx plugin script.
    * First we add a channel for the BPM info (not documented in the file).<BR>
Add a channel, name it 'BPM', Type is 'Button', Midi channel is '1', Message is 'Note On/Off', Parameter is 101.
    * Then we add all channels with the volume information<BR>
Add a channel, name it 'Volume - absolute', Type is 'Slider', Midi channel is '1', Message is 'Note On/Off', Parameter is 101.
    * Repeat this for all channels you find interesting<BR>
The relative volume channels can give interesting light effects, the absolute volume is less interesting

* Now go to your Virtual Console and start using the MIDI signals. Here two examples:
    * Configure the BPM to advance a cue list on each beat<BR>
In your Cue list, in the 'Next Cue' tab, click on 'Choose', expand the 'Mixxx MIDI' line and pick BPM from the list. Your cue list will now advance with the beat of the music, as determined by the Mixxx beat detection.
    * Make a lamp light up with the Volume of the music (VU meter)<BR>
Configure a Slider, on the 'General' tab, under 'External input' click on 'Choose' and select a channel of your choosing, for example 'Volume absolute'. The selected Fixture will now light up with the volume of the music, like a giant VU meter.

