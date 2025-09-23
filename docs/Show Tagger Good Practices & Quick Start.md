# Show Tagging Good Practices (2022.06.01 by ycomp)

These are various tips for tagging and related.

## Supported File Formats

1. `FLAC`
2. `MP3`
3. `MP4` / `M4A` / `AAC` (_same thing, different name. If `M4A` is mentioned it applies to all these extensions_). This format is quirky, see the manual for notes on using `mp3Tag` to save files before and after tagging just to ensure no fields go missing.
4. `OGG` (_no cover art can be added_)
5. `WMA`

see the manual for any peculiarities of tagging these formats. `FLAC` doesn't really have any.

## `Show.txt`

### Quick Start ( _for creating `Show.txt`_ )

How it works is you either modify an existing _Show Info Text File_ that comes with a Show you have acquired, or you create your own from Scratch (for example paste a Setlist from a site into a Text file and mark it up for processing by **Show Tagger**)

- a **Switch** is my term for these _Command Words_ e.g. `COMMENT`

#### Editing `Show.txt` in Nutshell

1. Write the `Artist` on the **1st line**, e.g. `Grateful Dead`
   - `GD` will be expanded to `Grateful Dead` (for more about supported _Artist Acrynyms_ and how you can define your own, see `[artists]` in the INI)
2. Write the `Album` on the **2nd line** e.g. `1971-08-06 Hollywood Palladium - Hollywood, CA [Matrix:Chappell]`
3. _IF_ there is any junk on on the line before songs write `IGNORE` somewhere above the songs e.g. `IGNORE-` to ignore the `-` and everything preceeding it. You can also write e.g. `IGNORE3` to remove the first 3 characters or even `IGNORE/regex/` for a complicated one (_not entirely sure this is ever necessary as usually specifying a character or # of digits will handle the job, however there is an example included_)
4. use `RTRIM` for any junk after the song name to ignore e.g. `RTRIM(` will cleanup times after written on the line after a song e.g. `El Paso (04:15)` becomes `El Paso`. The problem is if they don't have any character that they all begin with. In that case use a _Regex_ e.g.
   - `RTRIM/\d{1,2}:\d{2}/` for something like `Jack Straw 06:32`
   - `RTRIM/\d{2}:\d{2}/` for something like `Jack Straw 6:32`
5. Mark Comments (_blocks of text we want to write to the Comment Tag_) or Junk (_blocks of text we want to skip_). You can obviously just delete text instead of marking it as `JUNK`, your call.. whatever works for you. **see description of `COMMENT` tagging below**
6. Add one of `SOUNDCHECK`, `SET`, `FILLER`, `CD`, `DISC` before the appropriate list of songs, e.g. `SET 2`
   - These are pretty flexible (e.g. `SET IV` or `3rd Set` or `Set One` work), for more details see the manual.
   - `SET` and `CD`/`DISC` paradigms are like oil and water, they don't mix. Don't worry, if you do **Show Tagger** will inform you.
   - **Encores** are handled a bit differently
     1. `ENCORE` works on the line before the appropriate Songs
     2. but you can also have `E:`, `E2:`, `Encore:`, `(Encore)` and other variations in the _Song Title_, once again see the manual for more info.
     3. `FILLER` works like an `ENCORE`, it will keep increasing the _Disc Count Tag_ each time it is encountered (_so that filler comes after the main songs in the Music Player_). It also can be included in a _Song Title_, e.g. `Jack Straw 4/1/91 (filler)`
     4. `SOUNDCHECK` writes as a _DiscNo 0_ Tag, so that it will appear before _Set 1 Songs_ in the _Music Player_        
   - If it is a _One Set_ show, you don't need to add any of those Switches.

### Tips

1. Use **Batch Tagging** (i.e. **Show Taggers**). It's really great to prepare a bunch of shows for tagging and then let **Show Taggers** do its thing. It will even play sounds on success or failure of the Batch Tagging process.
2. _Never Tag originals of the Audio Files_. Well I do it all the time, but it is up to you.. i.e. don't blame me if anything happens. By "originals" I mean that I downloaded.. obviously if you have been editing the show audio files yourself, only ever tag a copy.
3. Place cover art files in the `Show.txt` folder and name them appopriately so that they are recognized by **Show Tagger** (see manual)
4. If you are modifying a text file that came with the torrent, don't delete it. Keep the original, _again it's up to you..._
5. Refresh your Music Library with your Music Player (_if necessary_) after taggging a show. I mean you don't need to do it after each _Show Tag_ but if you wonder why you still see the old tags, that is the reason.
6. _Ensure that your `Album` names are unique_. You don't want to have a collision because 2 difference sources have the same `Album` name e.g. 2 shows with `Album` of `1971-04-29 Fillmore West, SF` will give you twice as many files listed for the Show (`Album`) in programs like **MuiscBee**. Do something like this to solve the problem: `1971-04-29 Fillmore West, SF [SBD:Smith]` and `1971-04-29 Fillmore West, SF [AUD:Unknown]`
7. Don't worry about Acronyms... the _Acronym Buster_ will hopefully expand them for you. You can always add more to the INI. Acronyms **must** be uppercase.
8. set `commentsTags` in `[tags]` in the INI if you want Comments to be written to (Unsynced) Lyrics (as well or only there).
9. **Show Taggers** can even _move the Tagged Show Folders_ into folders named after `Artist`, `Album`, `Artist` & `Album` or the Date Parsed from the `Album` tags, or just _sucess_ or _failure_ folders you name yourself (e.g. `tagged` or `failed`)
10. Recognized _Song Acronyms_ will be expanded. You can also define your own. See `[acronyms]` in `Show Tagger.ini`

### **! WARNING !**

_now that I have your attention_, currently you have to take care if you customize (_edit_) `Show Tagger.ini`. The problem is that a new install will overwrite it. I eventually will figure out a good solution for this, but for now the burden is on you. The problem is that new versions could have new entries and these are required for the running of the program. Therefore, 

- When **Show Tagger Setup** is run, it will make a backup copy in the same folder. However if you the Setup again, it will back up the current INI again, overwriting the old backup.. so you will have lost your INI.
  
  1. Therefore it is highly suggested to keep a copy of the INI after you edit it somewhere else. 
  
  2. **AFTER** you have run **Show Tagger Setup** and have a fresh new copy of the latest INI, your challenge is then to merge your changes (i.e. your old INI) with the new one. If you know how to do this, then props to you. Otherwise, you will need some merge/diff software so you can compare differences and select the ones to merge into the new file. For example you might have added a bunch of acronyms, so you would to merge those with the list of them in the new INI. It's really easy once you get the hang of it. 
     
     - I recommened **Visual Studio Code** if you have that installed (_you open a folder, right click the first file - select it for merge, then choose the next file and right click and comare it with selected_)
     - I also recommend **WinMerge** it is small and free and works well and that is its entire purpose, so it is a good tool. Just choose one of these, you don't need both.
     - there are probably sites you can do this stuff online on also without installing software, but I haven't investigated.
  
  3. When these things are no longer required, these instructions will be removed from here and the manual, as well as it will be written in the change log (_which is currently in the manual but might be moved to a separate txt file eventually_)
     
     #### This applies to all the programs
1. **Show Tagger** & **Show Taggers** - file: `Show Tagger.ini`
2. **Files Launcher** - file: `Files Launcher.ini`

### Tags that that are benefical to include

### Tags that are created by **Show Tagger**

These tags are created by **Show Tagger** and can be used if you have a _configurable Music Player_ (e.g. [MusicBee](http://www.getmusicbee.com) ). For **MusicBee** check out the _included Screenshots_

- _Standard_ means it is a fairly standard tag, recognized by most decent players.
- _Custom_ means these are not official tags or anything like it, but the information is there 
- _Recognized_ means that it is recognized by some players, and sometimes found somewhere in the UI. 

| Tag             | Type       | Description                                                                                                                                                                                               | Created by...                                                                                      |
| --------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `COMMENT`       | Standard   | `COMMENT` (or `~!@`) can be used as blocks, i.e. once to start a block and once to end it, or simply once to gather everything after it into the Comment Tag (_with some exceptions, as mentioned below_) | `COMMENT` (or `~!@`) Switch                                                                        |
| `YEAR`          | Standard   | If you have your `Album` starting with a 4 digit Year then it will be automatically parsed                                                                                                                | `YEAR` Switch or parsed from the `Album`                                                           |
| `COMPOSER`      | Standard   | Recommended for the Taper or Source Person                                                                                                                                                                | `COMPOSER` or `+` Switch                                                                           |
| `CONDUCTOR`     | Standard   | Recommended for the Releaser or Remasterer                                                                                                                                                                | `CONDUCTOR` or `~` Switch                                                                          |
| `KEYWORDS`      | Recognized | Specify _your own_ **keywords**, I like to use `new` and `listen`                                                                                                                                         | `KEYWORDS` or `KW` Switch                                                                          |
| `ENCORE`        | Custom     | The Encore #                                                                                                                                                                                              | _Automagically_                                                                                    |
| `SET`           | Custom     | The _Set Description_ e.g. `Set II` or `Encore 3`                                                                                                                                                         | _Automagically_                                                                                    |
| `Original Year` | Standard   |                                                                                                                                                                                                           | The _Original Year_, I like to use this to specify the _Year of the Recording/Remastering Release_ |
| QUALITY         | Custom     | Describes the quality of the recording                                                                                                                                                                    | `QUALITY` Switch                                                                                   |
| _Your Own_      | Custom     | Create _your own Custom Tag_, see the manual                                                                                                                                                              | _You_                                                                                              |
| _**More Tags**_ |            | _See the **manual** and `[defaults]` in `Show Tagger.ini`_                                                                                                                                                |                                                                                                    |

### Mark Comments _in-place_

While you can use `COMMENT` at the end of the `Show.txt` file to include everything (except _useless lines_ and the _stop line_, both configurable in the `INI`), and there are a plethora of examples included with __Show Tagger__ that do it just so.

However, that is simply because those __Examples__ were created before the ability to mark `COMMENT`s (and `JUNK`) _in-place_ was added.

#### Example of _in-place_ tagging in `Show.txt`

**NOTE:** `~!@` is an alias for `COMMENT`, it does the same thing. It is just _way faster to type..._ (`JUNK` also has one - `#$%`)

```
Grateful Dead
1973-11-25 Feyline Field - Tempe, AZ [SBD:Miller]
OYEAR 2020
IGNORE-
~!@
Recording Info:
SBD > Reel Master > Dat (44.1k)

Transfer Info:
Dat (Tascam DA-40) > Tascam DA-3000 > Adobe Audition 2020 > Samplitude Pro X5 Suite > FLAC
(3 Discs Audio / 1 DVD FLAC)

All Transfers and Mastering by Charlie Miller
charliemiller87@earthlink.net
November 8, 2020

Notes:
-- This is an upgrade to my previous source (shnid=113007)
-- Thanks to Joe B. Jones for the pitch correction settings
~!@
Set 1:
01 - Tuning
02 - Promised Land
03 - Sugaree
04 - Beat It On Down The Line
05 - Don't Ease Me In
06 - Black Throated Wind
07 - Tennessee Jed
08 - Mexicali Blues
09 - China Cat Sunflower >
10 - I Know You Rider
11 - Big River
12 - Row Jimmy
13 - Me And My Uncle
14 - Brown Eyed Women
15 - Playing In The Band

Set 2:
16 - Around And Around
17 - Eyes Of The World >
18 - Weather Report Suite 
19 - Casey Jones
20 - Sugar Magnolia >
21 - Goin' Down The Road Feeling Bad >
22 - One More Saturday Night

Encore:
23 - Tuning
24 - And We Bid You Good Night


SHNTOOL OUTPUT:
    length     expanded size    cdr  WAVE problems  fmt   ratio  filename
     0:24.37        4320668 B   ---   --   ---xx   flac  0.4143  01 Tuning.flac
     3:23.10       35832764 B   ---   --   ---xx   flac  0.5606  02 Promised Land.flac
     8:10.13       86466620 B   ---   --   ---xx   flac  0.5127  03 Sugaree.flac
     4:11.01       44278796 B   ---   --   ---xx   flac  0.5391  04 Beat It On Down The Line.flac
     5:13.30       55283804 B   ---   --   ---xx   flac  0.5291  05 Don't Ease Me In.flac
     7:35.74       80436092 B   ---   --   ---xx   flac  0.5127  06 Black Throated Wind.flac
     8:04.59       85516412 B   ---   --   ---xx   flac  0.5359  07 Tennessee Jed.flac
     4:46.57       50584508 B   ---   --   ---xx   flac  0.5326  08 Mexicali Blues.flac
     8:08.64       86233772 B   ---   --   ---xx   flac  0.5651  09 China Cat Sunflower.flac
     7:19.59       77578412 B   ---   --   ---xx   flac  0.5077  10 I Know You Rider.flac
     6:06.41       64658876 B   ---   --   ---xx   flac  0.5338  11 Big River.flac
    10:20.42      109466828 B   ---   --   ---xx   flac  0.4951  12 Row Jimmy.flac
     3:47.51       40162796 B   ---   --   ---xx   flac  0.5278  13 Me And My Uncle.flac
     6:41.58       70872860 B   ---   --   ---xx   flac  0.4950  14 Brown Eyed Women.flac
    17:08.72      181508588 B   ---   --   ---xx   flac  0.5620  15 Playing In The Band.flac
     5:36.09       59291612 B   ---   --   ---xx   flac  0.5537  16 Around And Around.flac
    15:32.25      164463644 B   ---   --   ---xx   flac  0.5632  17 Eyes Of The World.flac
    15:50.42      167678828 B   ---   --   ---xx   flac  0.5311  18 Weather Report Suite.flac
     9:14.66       97880876 B   ---   --   ---xx   flac  0.5153  19 Casey Jones.flac
     9:12.42       97471628 B   ---   --   ---xx   flac  0.5678  20 Sugar Magnolia.flac
     8:34.53       90794300 B   ---   --   ---xx   flac  0.5595  21 Goin' Down The Road Feeling Bad.flac
     4:50.11       51181916 B   ---   --   ---xx   flac  0.5589  22 One More Saturday Night.flac
     1:32.12       16257068 B   ---   --   ---xx   flac  0.5098  23 Tuning.flac
     3:23.01       35811596 B   ---   --   ---xx   flac  0.5622  24 And We Bid You Good Night.flac
   175:10.29     1854033264 B                            0.5375  (24 files)
```

# Some Notes about **Show Tagger**

## Miscellaneous

1. Tagging will abort on _`Show.txt` Syntax Errors_ almost always before a single file is tagged. There are one or two cases where it can't.

## **Show Tagger** vs **Show Taggers**

- use **Show Tagger** for Single Show Tagging and use **Show Taggers** for Batch Show Tagging
- but **Show Taggers** can also be used for _tagging a Single Show_ as well

### Some Differences

1. **Show Tagger** will not move Show Folders on _success_ or _failure_, **Show Taggers** can depending on the INI `[move]` configuration
2. **Show Tagger** can launch whatever MP3 Tagging program or Music Player you configure, even different ones for different audio formats, after tagging is complete.
3. **Show Taggers** can only launch [Mp3Tag](http://www.mp3tag.de) because it adds each Show Folder to **MP3 Tag** after each Show is tagged. Other taggers/players _don't have this capability_.

#### **Send To** ( Right Click in Windows Explorer -> Send To )

1. Both can use _Send To_ to initiate tagging of a _Show Folder_
2. **Show Tagger** can use _Send To_ to initiate tagging of a _Show Folder_, _by sending a file from that folder_ to **Show Tagger**
3. **Show Taggers** can use _Send To_ to initiate tagging of _Multiple Selected Show Folders_
4. **Show Taggers** can use _Send To_ to initiate tagging of _All Show Folders within the Selected Folder_ that is sent to **Show Taggers** (Folders not containing a `Show.txt` will be skipped)
