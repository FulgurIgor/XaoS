# Instructions on internationalization

XaoS has transitioned from gettext to Qt for i18n.

The .ts files can be edited using Qt Linguist. See the
[Qt Linguist manual](https://doc.qt.io/qt-5/qtlinguist-index.html) for more information.

Run the following command from the XaoS top level directory to update the
.ts files with changes from the source code:

```
lupdate -tr-function-alias QT_TRANSLATE_NOOP=TR XaoS.pro
```

The function alias is very important so XaoS can find the TR macros used
by XaoS.

To add a new translation, edit i18n.pri and add a file named 
$$PWD/XaoS_LL.ts to the TRANSLATIONS list.  Replace LL with the two
letter ISO 639-1 code for the new language. Save the pri file and
rerun the lupdate command above to create the .ts file.

The i18n.pri contains commands to automatically generate the binary .qm
files from the .ts files each time XaoS is built, but the .qm files can
also be manually updated by running the following command from the top
level directory:

```
lrelease XaoS.pro
```

Finally, add an entry for the new language in the file XaoS.qrc
in the top level directory. This makes sure that the .qm file will be
used by the executable (actually, the .qm file is linked against
the executable).

After compilation you can try out a translation by setting the shell variable LANGUAGE
to the two letter language code. For example, on a Linux system

```
qmake && make && LANGUAGE=sv bin/xaos
```

will start the application in Swedish.