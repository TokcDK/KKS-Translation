# Koikatsu Sunshine Translations

English translation project for Koikatsu Sunshine

The translations are applied while the game is running and do not require replacing or modifying any game files.

***NOTE: README is not (yet) accurate beyond this point***

## Prerequisites

- [BepInEx 5.4.x+](https://github.com/BepInEx/BepInEx/releases/)
- [BepisPlugins for KKS](https://github.com/bbepis/BepisPlugins/releases)
- [XUnity.AutoTranslator](https://github.com/bbepis/XUnity.AutoTranslator)

[//]: # "- [KKS_TextResourceRedirector](https://github.com/IllusionMods/TranslationTools#textresourceredirector) (required for most resources)"
[//]: # "- [KKS_Subtitles](https://github.com/IllusionMods/KK_Plugins#subtitles) (required to see subtitles)"
[//]: # "- [KKS_TranslationHelper](https://gebo1.github.io/GeBoPlugins/src/TranslationHelper/) (Optional, but recommended)"
[//]: # "- [KKS_TranslationCacheCleaner](https://gebo1.github.io/GeBoPlugins/src/TranslationCacheCleaner/) (optional, but recommended)"

## Installation

1. Ensure you have the prerequisites installed.
2. Go to the [releases page](https://github.com/IllusionMods/KoikatsuStoryTranslation/releases) and download the latest version. Alternatively, advanced users can get the latest beta translations by clicking on the "Clone or download" button above. If you are a translator, read the sections below to see how to contribute to the translations.
3. Extract the zip and place the BepInEx folder inside your game folder (where the file game executable is).

## Contribution

There are over 175,000 unique lines of text that need translation and any help is appreciated. Regardless of your translation skill and Japanese knowledge you can still help with translations. Even if you have no experience, you can help by proofreading or using machine translation services such as Google Translate or DeepL (recommended). In the case of machine translations, clean up the translation using sanity and a little logic.

Translation done purely by machines must be kept in the designated files (`zz_machineTranslation.txt` files within `RedirectedResources`). These should be considered placeholders until manual translations are available (those should go into `translation.txt`). The goal is to have everything, manually translated.

- `Text` - Normal text replacements and modifications.
- `Texture` - Image replacements.

### Basic operation and structure

Each translation line follows the pattern:

```
original text=translated text
```

Example:

```
悟飯=Food
```

Lines beginning with `//` are considered comments, i.e., they are not considered in the translation.

The translations are all inside the `Bepinex\Translation\en` folder. They are then split into the following directories:
- `RedirectedResources` - Replaces the texts embedded in the game files. These translations are loaded only when the game needs the corresponding file, so it is preferable to use this directory instead of the `Text` directory because of its accuracy and performance. This directory mimics the structure of the game, placing a folder for each resource file (such as the ".unity3d" files).
- `Text` - Generic translations that are loaded when the game opens. All texts that are not translated in `RedirectedResources` are checked into this directory. If there is no translation, then the original untranslated text is displayed in the game, Google Translator is called, the translated text is written to `_AutoGeneratedTranslations.txt` and only then the translation is displayed in the game. The text in this folder can be handled with regular expressions (Regex), resized, and separated by game scene instead of being separated by files. This directory is often used in user interfaces (UI) because of these features.
- `Text\Localizations` - Strings under this folder were dumped via TextDump. Translations can be added for missing entries, but new entries should not be added or merging future dumps will become difficult.
- `Texture` - Contains the translated version of game images. The game images are translated using image editing software. If available the source files (`.psd`, `.xcf`, etc.) files can be found in the project's `Image Source Files` folder.

Coordinate with other translators on the [Koikatsu Discord](https://discord.gg/urDt8CK) #lingual-studies channel. To avoid translation conflicts please ask if anyone is working on a file. If you have any questions about the quality of your translations, ask for advice on the server.

### How to add or improve translations

- If you want to make a simple edit simply open the file in question and click edit. After you are done editing, commit the changes and start a pull request.
- If you have more translations to submit [fork the repository](https://help.github.com/articles/fork-a-repo/). This will make a copy of the original project in your account. Upload your changes to the fork into your account, and then [send a pull request](https://help.github.com/articles/about-pull-requests/) to the original project. Your pull request will be reviewed and accepted after a quality check. Again, avoid raw machine translations. Proper capitalization, punctuation, and spelling is a must.

## Text Translations

Texts that are not translated in `RedirectedResources` use the `Text` directory. In this directory the first translation found for a given text is used every time that this same text is found. But sometimes the same word can have different meanings depending on where you are in the game, in this case you can use the "scope level" feature to tell which translation should be used in that part of the game.

### Scope Levels

To use scope levels, use the following structure:

```
#set level xxx
text=translation
text2=translation2
#unset level xxx
```

Where "xxx" represents the number of the desired scope level. Below is a table containing the known scope levels and their locations:

#### Known Scope Levels

| Level | Description             |
|------:|-------------------------|
| -1    | Global                  |
|  1    | Global Extended         |
|  3    | Chara Maker             |
|  4    | Main Menu               |
|  6    | Main Game UI            |
|  8    | H-Scenes Menus          |
|  9    | H-Scenes Location       |
| 11    | Free H Menu             |
| 14    | ADV Dialogues           |
| 15    | Chara Uploader          |
| 16    | Chara Downloader        |


##  Resource Translations

The folder `RedirectedResources` is the main translation directory for the game, so it gets special treatment.

Inside each folder there is a file named `translation.txt`, this is the file where the translations should go. In some folders there is also the file `zz_machineTranslation.txt` which is where machine translations go, that usually have a lower quality.

Every `translation.txt` file has the raw Japanese text that needs translations. Each one starts commented out (`//` at the begining) so it will not be loaded. For your text to display correctly in game, put the translation on the right side of the equal sign and remove the `//` at the start of the line. Do not edit the Japanese text or the translation will not work. Example:

Before:

```
//Tシャツ=
```

After:

```
Tシャツ=T-shirt
```

If `zz_machineTranslation.txt` files are present only lines that are not translated by `translation.txt` will be used. If the file `translation.txt` has been fully translated, the file `zz_machineTranslation.txt` can be deleted. The goal of this translation project is that none of the `zz_machineTranslation.txt` files remain.

The `assets` folder inside of `Bepinex\Translation\en\RedirectedResources` can be compressed into a .zip archive to be read by the game (simply right-click on the assets folder and then compress to .zip). Uncompressed files under `assets` are also still loaded. The game has to be restarted in order to see updated translations.


The plugin [TextResourceRedirector](https://github.com/IllusionMods/TranslationTools#textresourceredirector) is required for these translations. Always keep it updated. (not ready yet, you early adopter!)

### Structure of the "RedirectedResources" directory

Table with the localization of the translations for each part of the game:

| Folder                                  | Description               |
|-----------------------------------------|---------------------------|

[//]: # "| `action/list/event`                     | Event titles              |"
[//]: # "| `adv`                                   | main game dialogs         |"
[//]: # "| `communication`                         | main game dialogs         |"
[//]: # "| `custom/customscenelist`                | Maker Pose Text           |"
[//]: # "| `etcetra/list/nickname`                 | Call Names                |"
[//]: # "| `h/list/*/animationinfo_*`              | Positions (game versions) |"
[//]: # "| `h/list/*/hpointtoggle`                 | Positions (game versions) |"
[//]: # "| `h/list/*/personality_voice*`           | H Subtitles               |"
[//]: # "| `list/characustom`                      | Maker stuff               |"
[//]: # "| `list/characustom/*/cha_sample_voice_*` | Personality names         |"
[//]: # "| `list/random_name`                      | Random names              |"
[//]: # "| `map/list/mapinfo`                      | Map names                 |"
[//]: # "| `studio/info`                           | Studio stuff              |"


#### Personalities

##### Character Personalities

| ID | Name       | Eng Name           | Source                            |
|:--:|:-----------|:-------------------|:----------------------------------|
| 00 | セクシー系お姉さま  | Sexy               |                                   |
| 01 | お嬢様        | Ojousama           |                                   |
| 02 | タカビー       | Snobby             |                                   |
| 03 | 小悪魔っ子      | Kouhai             |                                   |
| 04 | ミステリアス     | Mysterious         |                                   |
| 05 | 電波         | Weirdo             |                                   |
| 06 | 大和撫子       | Yamamoto Nadeshiko |                                   |
| 07 | ボーイッシュ     | Tomboy             |                                   |
| 08 | 純粋無垢な子供    | Pure               |                                   |
| 09 | アホの子       | Simple             |                                   |
| 10 | 邪気眼        | Delusional         |                                   |
| 11 | 母性的お姉さん    | Motherly           |                                   |
| 12 | 姉御肌        | Big Sisterly       |                                   |
| 13 | コギャル       | Gyaru              |                                   |
| 14 | 不良少女       | Delinquent         |                                   |
| 15 | 野生的        | Wild               |                                   |
| 16 | 意識高いクールな女性 | Wannabe            |                                   |
| 17 | ひねくれ       | Reluctant          |                                   |
| 18 | 不幸少女       | Jinxed             |                                   |
| 19 | 文学少女       | Bookish            |                                   |
| 20 | モジモジ       | Timid              |                                   |
| 21 | 正統派ヒロイン    | Typical Schoolgirl |                                   |
| 22 | ミーハー       | Trendy             |                                   |
| 23 | オタク女子      | Otaku              |                                   |
| 24 | ヤンデレ       | Yandere            |                                   |
| 25 | ダル         | Lazy               |                                   |
| 26 | 無口         | Quiet              |                                   |
| 27 | 意地っ張り      | Stubborn           |                                   |
| 28 | ロリばばあ      | Old-Fashioned      |                                   |
| 29 | 素直クール      | Humble             |                                   |
| 30 | 気さく        | Friendly           |                                   |
| 31 | 勝ち気        | Willful            |                                   |
| 32 | 誠実         | Honest             |                                   |
| 33 | 艶やか        | Glamorous          |                                   |
| 34 | 帰国子女       | Returnee           |                                   |
| 35 | 方言娘        | Slangy             |                                   |
| 36 | Sッ気        | Sadistic           |                                   |
| 37 | 無感情        | Emotionless        |                                   |
| 38 | 几帳面        | Perfectionist      |                                   |

##### NPC Personalities


| ID  | Name    | Eng Name        |
|:---:|:--------|:----------------|

[//]: # "| -1  | リナ・ロベール | Lina Roberts    |"
[//]: # "| -2  | 橋本麗奈    | Hashimoto Reina |"
[//]: # "| -4  | 櫻井野乃花   | Sakurai Nonoka  |"
[//]: # "| -5  | 姫川舞     | Himekawa Mai    |"
[//]: # "| -8  | 柊このみ    | Hiiragi Konomi  |"
[//]: # "| -9  | 結城桜     | Yuuki Sakura    |"
[//]: # "| -10 | 水瀬亜依    | Minase Ai       |"



#### Personality Asset Locations

| Type                   | Location (replace `##` with ID from table above) |
|------------------------|--------------------------------------------------|

[//]: # "| Dialog (adv)           | `adv/scenario/c##/*`                             |"
[//]: # "| Dialog (communication) | `communication/info_*/*_##`                      |"
[//]: # "| Call Names             | `etcetra/list/nickname/*/c##`                      |"
[//]: # "| H Lines                | `h/list/*/personality_voice_c##_*`               |"

NPC Personalities only have entries under Dialog (adv) and H Lines.

### Specialized translation lines

There are some specialized resources handled by the resource redirection that require some additional handling.

#### Format strings

Format strings have replacements in them processed by [`String.Format`](https://docs.microsoft.com/en-us/dotnet/api/system.string.format?view=netframework-4.6#Starting).  The sections that are replaced by the game engine will look like `{0}`, `{1}`, `{2}`, etc.  Usually they are a character name or the name of some item.  The same replacements found in the original string should exist in the translated string.

Example:
```
{0}と仲がいいと思ってるわ=I think I'm good friends with {0}.
```

#### ADV Choices

Because these strings are encoded into a larger entry in the resource files they require special handling by TextResourceRedirector to ensure the text that should no be replaced remains untouched, while allowing the displayed text to be translated. These lines will start with `CHOICE:` followed by the text that needs to be translated.  On the right side of the `=` you need only include the translated text without the `CHOICE:` prefix.

Example:

```
CHOICE:受け取る=Accept
```

#### Optional Prefixes

There are a number of assets that support the use of optional prefixing to get a more exact match. This allows for more specific translations in cases where multiple assets might match the same replacement code.  Matching for these assets will first try the prefixed match, then fall back to the standard un-prefixed match.  Given the following translation file:

```
PREFIX1:こんにちは=Hi!
こんにちは=Hello.
```

Trying to match `こんにちは` for an asset using `PREFIX1` would return `Hi!`, where an asset using `PREFIX2` would fall back to `Hello.`.

Some prefixes can be combined with numbers, which limit them to matching specific table rows or columns.

| asset location                         | prefix       | Notes                                                             |
|----------------------------------------|--------------|-------------------------------------------------------------------|

[//]: # "| `adv/scenario/`                        | `CHOICE:`    |                                                                   |"
[//]: # "| `communication/*/optiondisplayitems_*` | `OPTION[x]:` | `x` will be an integer representing a question ID                 |"
[//]: # "| `etcetra/list/nickname`                | `SPECIAL:`   |                                                                   |"
[//]: # "| `list/random_name`                     | `NAME[x]:`   | `x` is the column (1-2 surname, 3-4 female given, 5-6 male given) |"



## Tools

[//]: # "- [TranslationSync](https://github.com/IllusionMods/TranslationTools#translationsync) is a plugin for formatting and copy/pasting translations between files when there are duplicate entries."
- [Release Tool](https://github.com/SpockBauru/TranslationTools_Illusion#releasetool) - Tool that cleans up the translation files to remove any unnecessary untranslated parts (in this repo).
- [Yomichan](https://foosoft.net/projects/yomichan/) - This browser plugin allows you to see the definition of Japanese words by putting your mouse over them in the browser and pressing shift.
- Dictionaries:
  - https://jisho.org/
  - http://www.romajidesu.com/

## Status

TBD
