At the moment, QLC+ is translated in German, Spanish, Catalan, Italian, Portuguese, Japanese, French, Dutch and Czech.<br>
If your language is not supported, please jump to the "**Add a new translation**" paragraph, or contact the developers and request the addition of it.<br>

### Contribute on an existing translation

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

### Add a new translation

Translation files are spread all over the QLC+ source tree. See below for a complete list of where you can find them.
Each folder has a .pro file. If you open it with a text editor, you will find at some point something like

`TRANSLATIONS += dirname_xx_YY.ts`

That is the statement that indicates the translation file name and the language code to consider.
You need to add a new entry and then run the 'lupdate' tool on the modified .pro file. You can find 'lupdate' within any official Qt release.
For example:

`lupdate src.pro`

If everything goes well, a new file will be created in the folder where you modified the .pro file.
You are now ready to process the file with QtLinguist, as mentioned above.

### Translation files

This is the list of files that needs to be translated for a full QLC+ translation:


| Translation file  | .pro name  | Strings (more or less) |
|---|---|---|
| `fixtureeditor/fixtureeditor_xx_YY.ts` | fixtureeditor.pro | 193 |
| `launcher/launcher_xx_YY.ts` | launcher.pro | 2 |
| `plugins/artnet/ArtNet_xx_YY.ts` | src.pro | 33 |
| `plugins/dmx4linux/DMX4Linux_xx_YY.ts` | dmx4linux.pro | 1 |
| `plugins/dmxusb/src/DMX_USB_xx_YY.ts` | src.pro | 29 |
| `plugins/E1.31/E131_xx_YY.ts` | E1.31.pro | 24 |
| `plugins/enttecwing/src/ENTTEC_Wing_xx_YY.ts` | src.pro | 8 |
| `plugins/hid/HID_xx_YY.ts` | hid.pro | 9 |
| `plugins/midi/src/MIDI_xx_YY.ts` | src.pro | 35 |
| `plugins/ola/OLA_xx_YY.ts` | ola.pro | 6 |
| `plugins/osc/OSC_xx_YY.ts` | osc.pro | 18 |
| `plugins/peperoni/Peperoni_xx_YY.ts` | peperoni.pro | 16 |
| `plugins/spi/SPI_xx_YY.ts` | spi.pro | 7 |
| `plugins/udmx/src/uDMX_xx_YY.ts` | src.pro | 10 |
| `plugins/velleman/src/Velleman_xx_YY.ts` | src.pro | 1 |
| `qmlui/qlcplus_xx_YY.ts` | qmlui.pro | 792 |
| `ui/src/qlcplus_xx_YY.ts` | src.pro | 1455 |
| `webaccess/webaccess_xx_YY.ts` | src.pro | 64 |

