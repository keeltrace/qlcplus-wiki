At the moment, QLC+ is translated in German, Spanish, Catalan, Italian, Portuguese, Japanese, French, Dutch and Czech.<br>
If your language is not supported, please contact the developers and request the addition of it.<br>
Otherwise here's a quick guide to contribute on an existing translation:<br>

* download and install Qt Linguist. It comes with any prebuilt Qt release:
https://download.qt.io/official_releases/qt/

* create an account on GitHub
* if you're not familiar with GIT, you can download the GitHub official desktop client here:
https://desktop.github.com/
 
* **fork** qlcplus (guide: https://help.github.com/articles/fork-a-repo) or **sync** your existing tree
* open all the xx_XX.ts file for your language (see list below) with Qt Linguist
* translate, translate, translate, save
* synchronize your changes with GitHub (in GIT words "commit" and "push"). If you're using the GitHub client, press the "Commit" button (left side of the screen) and then the "Sync" button (upper right corner of the window)
* when you're done, go to your GitHub page and send a **pull request** with your changes to the main QLC+ tree
(guide: https://help.github.com/articles/using-pull-requests/)

The following videos might help:<br>
https://www.youtube.com/watch?v=1S_526C8Gkw<br>
https://www.youtube.com/watch?v=NnBb9NTk-To<br>

### Translation files

This is the list of files that needs to be translated for a full QLC+ translation:

* fixtureeditor/fixtureeditor_xx_XX.ts
* launcher/launcher_xx_XX.ts
* plugins/artnet/ArtNet_xx_XX.ts
* plugins/dmx4linux/DMX4Linux_xx_XX.ts
* plugins/dmxusb/src/DMX_USB_xx_XX.ts
* plugins/E1.31/E131_xx_XX.ts
* plugins/enttecwing/src/ENTTEC_Wing_xx_XX.ts
* plugins/hid/HID_xx_XX.ts
* plugins/midi/MIDI_xx_XX.ts
* plugins/ola/OLA_xx_XX.ts
* plugins/osc/OSC_xx_XX.ts
* plugins/peperoni/Peperoni_xx_XX.ts
* plugins/spi/SPI_xx_XX.ts
* plugins/udmx/src/uDMX_xx_XX.ts
* plugins/velleman/src/Velleman_xx_XX.ts
* qmlui/qlcplus_xx_XX.ts
* ui/src/qlcplus_xx_XX.ts
* webaccess/webaccess_xx_XX.ts

