At the moment, QLC+ is translated in German, Spanish, Catalan, Italian, Japanese, French, Dutch, Portuguese (v4 only), Czech (v4 only), Finnish (v4 only), Polish (v5 only), Russian (v5 only) and Ukrainian (v5 only).<br>
If your language is not supported, please jump to the "**Add a new translation**" paragraph, or contact the developers and request the addition of it.<br>

In both cases (new or existing translation), you'll need to download and install Qt Linguist. It comes with any prebuilt Qt release: https://download.qt.io/official_releases/qt/

### Contribute on an existing translation

* Create an account on GitHub.
* If you're not familiar with GIT, you can download the GitHub official desktop client here: https://desktop.github.com/
* **Fork** qlcplus (guide: https://help.github.com/articles/fork-a-repo) or **sync** your existing tree.
* Open all `xx_XX.ts` files for your language (see below) with Qt Linguist.
* Translate, translate, translate and save.
* Synchronize your changes with GitHub (in GIT words: "commit" and "push"). If you're using the GitHub client, press the "Commit" button (left side of the screen) and then the "Sync" button (upper right corner of the window).
* When you're done, go to your GitHub page and send a **pull request** with your changes to the main QLC+ tree (guide: https://help.github.com/articles/using-pull-requests/).

The following videos might help:<br>
https://www.youtube.com/watch?v=1S_526C8Gkw<br>
https://www.youtube.com/watch?v=NnBb9NTk-To<br>

### Add a new translation

Translation files are spread all over the QLC+ source tree.
Each folder has a `CMakeLists.txt` file. If you open it with a text editor, you will find at some point something like

`set(TS_FILES`

That statement starts the list of already existing translation files.
You need to add a new entry and then run the `translate.sh` tool from the top-level directory of the source code tree.
For example:

```shell
./translate.sh create <ll_CC> ui
./translate.sh create <ll_CC> qmlui
```

If everything goes well, a new file will be created in each folder containing translatable strings.
You are now ready to process the file with QtLinguist, as mentioned above.
