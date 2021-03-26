# FreeSpace2-French-Translations

Project to translate FreeSpace 2 mods to French language.
The mods translated here can be found on the community website http://www.hard-light.net/.

## How to test the existing translations?

First install the mod with Knossos (https://fsnebula.org/knossos/).
Set the game in French language with the Knossos settings.
Install the mod you want to test.
Then browse the mod files and copy the translation files in the mod folder, keeping the same file tree.

For example for the mod Between the Ashes, copy the 'Between-The-Ashes\1.5.6\data' folder and its content to: %Knossos location%\FS2\BtA-1.5.6 after having installed the mod Between the Ashes

From here you are ready to run your tests.

## How to create my own translations for other mods?

If you want to create your own translations, you may want to check the following points in order to avoid waste of time.

### Languages with non-ascii characters

In case you want to translate to a language using non-ascii characters (accents, etc) like French for example, you need to check if the mod supports unicode.

From version 19.0 of the SCP engine, there is an official unicode mode, which can be enabled on mods running with this version or above. To enable it, browse the mod files and find the file 'game_settings.tbl'. Most of the time this file is included in a .vp file so you will have to extract it with the tools provided by the community.
Inside this file, you need to change/add the following line under '#GAME SETTINGS' section: 

```
$Unicode mode: True
```

Once the unicode mode is enabled, simply run the mod and check if there is no error. If there are errors, then the mod is not compatible and you will have to ask help from the authors of the mod.

If the mod uses a version prior to 19.0, then you will need to change the fonts used by the mod, and hope it doesn't break the mod.

#### Alternative to Unicode mode

If the Unicode mode is not possible for whatever reason, there is a possibility to copy the beheavior of the fsport mod translations. This mod uses specific fonts for languages with special characters, without using Unicde mode. So you can copy these fonts to the mod you want to translate, but in this case your strings.tbl and tstrings.tbl files need to use the "Western (Windows 1252)" encoding, otherwise the special characters won't show up!

### Where are located the files to be translated?

The files containing strings to be translated depend on the mod.

All texts visible in the game (menus, missions, etc) are stored in different files using the following pattern:
XSTR("the text to be translated", unique integer)

```
XSTR("Return to base", 2275)
```

The unique integer can be used to be translated in a separate translation file.

There are initially 2 translation files:
- strings.tbl (https://wiki.hard-light.net/index.php/Strings.tbl)
- tstrings.tbl (https://wiki.hard-light.net/index.php/Tstrings.tbl)

If these files are not present or don't contain all strings present in the mod, then it means the mod is not ready for translation, and you should contact the authors of the mod before going further.

In these files you will find different sections, matching different languages:

```
#default
2275, "Return to base"
...
END

#French
2275, "Retourner à la base"
...
END
```

default is the English language. If the other languages are not present in the file, you can add it yourself, and the SCP engine will recognize it. It means that all strings located in that section will be used depending on the language set in Knossos launcher.

strings.tbl and tstrings.tbl can be extended (https://wiki.hard-light.net/index.php/Modular_Tables) with other files using the following pattern:
- for strings.tbl => xxxxx-lcl.tbm
- for tstrings.tbl => xxxxx-tlc.tbm

The author of the mod could have created some files extending the original translation files. It is the case for the mod Between The Ashes for example, with the following files which contain translation strings:

```
xstr_bta1_bonus-tlc.tbm
xstr_bta1_coop-tlc.tbm
xstr_bta1_d-tlc.tbm
xstr_bta1_m-tlc.tbm
xstr_bta1_single-tlc.tbm
```

#### How do the extended files are managed by the game engine?

The SCP engine prioritizes the extended files over the original files, and different extended files are prioritized per alphabetical order, which means that if the same string (identified with the same integer) is present on xstr_bta1_d-tlc.tbm, xstr_bta1_m-tlc.tbm and tstrings.tbl, then only the string in xstr_bta1_d-tlc.tbm will be taken into account.

### How to avoid interfering with future mod changes?

A good thing to do is to create your own extended files to be sure it won't interfere with future mod versions. For my translations I copy original translation files and prefix them with 'fr-', and I keep into these files only the #French section, instead of adding a #French section in the original mod files.

Then I make all my translations in these new files. The SCP engine will automatically treat them as soon as I add them in the mod folder, in the condition I follow the naming rules described above.
