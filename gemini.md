## instructions about Show Tagging

main program: docs/Show Tagger.au3
docs: docs/Show Tagger.txt [make sure you read and understand this document!]
also: docs/Show Tagger Good Practices & Quick Start.md [you should also read and understand this]
before & after: docs/Before & After
Show Taggers EXE: C:\Users\misha\AppData\Roaming\Show Tagger\Show Taggers.exe

try hard to read file you can't find like source code and manuals, in docs subfolder... they are crucial for your understanding of how to tag things properly      

# MP3 Show Tagger Project: Show Tagger & Show Taggers AutoIt programs

1. read Show Tagger Good Practices & Quick Start.md manual
2. see the example show.txt files in the project. unfortunately these only show the final edits.. not the original info text files about the show that we manually edited.. but it is useful for you to see some examples, so that is why I mention this
3. view before and after examples from the following folders.. the before is a text file and could have any name, also there might be other files that for example are just hashes... we are looking for the text file with the venue, date of the show, setlist, possibly other comments.. and then you can look at the show.txt which is the version of that text file edited in a way to be processable by Show Tagger in order to tag the music files.
4. the music files might be m4a, or mp3, or FLAC, etc... but usually all the music files or the majority are of the same format
5. never use the term "Encore Break", even if it appears in the setlist of the original txt file.. the presence of "Encore" confuses Show Tagger because it thinks that it should start a new Encore... when "Encore Break" means a break.. usually.. well you figure it out.. we need Encore to indicate that it is an Encore Set now.. but Encore followed by Encore Break on the next line is bad and should be written as Encore followed by Break... but if there is only one line with Encore in it and it says Encore Break then that means it should be written as Encore (or E:)
6. remember that the Album field should be in the format YYYY-MM-DD Venue [source]

## Before and After Examples (in these folders)

1. there should be plenty folders (Grateful Dead Shows) for this folder, that contain show.txt (note: not all of them do.. and maybe some don't have the original text file the show.txt is based on.. so look for ones that have show.txt as well as the original text info file with the setlist and other characteristics mentioned earlier), in the Before & After folder
2. look at as many as you like but there are probably hundreds of examples in there.. you don't need to look at them all

## tips

1. in the COMMENT section use spacing between paragraphs when it would be appropriate
2. don't forget to include the OYEAR instruction under the album line, as long as you can detect what it should be. the OYEAR signifies the year of release of this source/version of the show. Usually it is written somewhere in the comments by the person releasing it. e.g. Charlie S. 1/2/06 would be OYEAR2006
3. There are no `ARTIST` or `ALBUM` commands! do not use them. Artist is deduced from the first line of the show.txt and Album from the second line (both lines required)
4. Do not put `:`after a command like `OYEAR` (i.e. not `OYEAR:`).. `COMMENT` not `COMMENT:`
5. `COMMENT` should be used AFTER the Setlist
6. There is no `SETLIST` command... if there is no setlist mentioned or specified in the original txt file then it should be written as `Set1` before the songs

### Missing Text Files with Setlists

1. if there is no `txt` file or there is not `txt` file with a setlist in it.. (e.g. it might be just checksums), then move it to a folder called `missing txt`

### Early / Late Shows

1. _Early_ (also known as _Matinee_ and _Late Shows_ are common for _Jerry Garcia Band_ shows.
2. Usually _Show Folders_ contain just a _Single Show_, but sometimes they contain any combination of _Early_ and _Late Shows_
3. e.g. just _Early_, just _Late_ or both _Early & Late Shows_

#### `ALBUM` line 
`ALBUM` line that contains the date should write the date as such for Early, Late or Early and Late Shows
1. Early: YYYY-MM-DDa (e.g. 1980-01-02a)
2. Late: YYYY-MM-DDb (e.g. 1980-01-02b)
3. Early & Late: YYYY-MM-DDab (e.g. 1980-01-02ab)

#### Sets

##### when both _Early_ and _Late Shows_ are in the same _Show Folder_

1. they have the same `show.txt`
2. _Early Show_ is essentially to be treated as the _1st Set_ usually and _Late Show_ as the _2nd Set_
3. so write in `show.txt` `Set 1 (Early Show)` for _Early Show_ and `Set 2 (Late Show)` for _Late Show_

##### Example

```
Set 1 (Early Show)
Song a
Song b

E: (Early Show Encore, optional)
Song c

Set 2 (Late Show)
Song d
Song e

E: (Late Show Encore, optional)
Song f
```

_just remember to have all the tracks in the correct, alphabetical order_

#### File Locations of Early and Late Shows

1. _Early_ and _Late_ shows might be all in the _Show Folder_ as a bunch of tracks
2. but they might also be in subfolders of the _Show Folder_, for more about that see the section on _Show Folder Sub Folders_

### Artist Names

#### Standardized List of Artist Names to use

if the band's name is listed, use this standardized form of the name e.g. if _Merle Saunders & Jerry Garcia_ is encountered, use _Garcia & Saunders_

| Standardize Artist Name for Tagging | Known Short Forms | Known Other Versions                 |                                  |
|-------------------------------------|-------------------|--------------------------------------|----------------------------------|
| Van Morrison                        | VM                | Van The Man                          |                                  |
| Grateful Dead                       | GD                | The Grateful Dead                    |                                  |
| Garcia & Grisman                    | GG                |                                      |                                  |
| Garcia & Saunders                   | GS                |                                      |                                  |
| Garcia & Kahn                       | GK                |                                      |                                  |
| Garcia & Wales                      | GW                |                                      |                                  |
| Jerrry Garcia                       | JG                |                                      | This is when he is solo acoustic |
| Jerry Garcia Band                   | JGB               |                                      |                                  |
| John Mayer                          | JM                |                                      |                                  |
| John Mayer Trio                     |                   |                                      |                                  |
| Legion of Mary                      | LOM               |                                      |                                  |
| Reconstruction                      |                   |                                      |                                  |

### Album Venue and City Information

1. don't forget to the include the City and State (or if not the USA, then City and Country) - after the Venue (and before the Source `[]` brackets

### Sources

#### Source & Origin

1. after the venue, the source should be written in the format `[Source | Origin]`
2. the `Source` should be something like `FM`, `Pre-FM`, `SBD`, `AUD`, `FOB` (Front of Board.. it is an audience recording from in front of the soundboard)
3. the `Origin` can be one or more things or people but should be concise and in order of closesness to original source to closeness to release.
4. if there is a long string of people involved, the most important ones to include in the `Origin` is the Taper and the final person who released it. The `COMMENT` section anyhow should have more detailed information like the full `Source` recording chain and all the people involved.

##### Examples

1. `[SBD | Miller]` is a Soundboard Recording released by Charlie Miller
2. `[AUD | Beyer | Unknown` is an audience recording on Beyer mics but futher information is unknown `[AUD | Beyer | Unknown | Clugston` might mean all that but that it was released by Scott Clugston
3. `[FOB | Menkes | Smith | Baker]` might mean FOB recording by Bob Menkes that was released by Smith but then that recording was edited for pitch correction and re-released by Baker

### UltraMatrix

- if an _Ultramatrix_ recording then try to include the source of the _UltraMatrix_, if mentioned. Usually this is `Healy` or `Pearson`
- usually _Charlie Miller_ releases them, regardless of the source. So if it is a _Charlie Miller_ release then `Miller` is often included sometimes after.

#### Examples
1. `UltraMatrix SBD | Miller`
2. `UltraMatrix SBD | Healy | Miller`
3. `UltraMatrix SBD | Pearson | Miller`

### Partial Recordings

1. when the recording is a _Partial Recording_ then the Set information should be listed before the `Source` in this compact way `[Sets; Source | Origin]` 
2. if `Sets; ` is not present it means that it is a complete recording
3. `II; ` means that Set II (Complete) is present but I is missing
4. `Ip,II: ` means partial set I, full Set II

#### Examples

1. `[Ip; FOB | Menkes | Andrew F.]` this means FOB recorded by Bob Menkes, released by Andrew F and is only a _Set I Partial recording_ 
2. `[Ip,IIp; AUD | Jim Vita]` would mean _partial Set I and partial Set II_ Audience recording by Jim Vita

### Songs

1. if the songs are numbered in the original txt file and there is a song with multiple lines but only the first line is numbered, then those lines should be compressed into one line. e.g. 8. A >\n B>\n >C should be A>B>C *(because they are **all the same track**)*
2. if a song is split up over multiple lines and either has multiple different track numbers OR there are no track numbers for any of the songs, then DON'T put them all on the same line *(because they are **all separate tracks**)*   
3. DON'T remove the _segue_ or _cuts_ markers in the _Song Title_, keep them in `show.txt`. e.g. `->`, `>`, `//`, etc. these aren't all the possible symbols used, just some examples. These are useful for the listener to see.

#### Examples

##### Same Track

> d2t03 - Scarlet Begonias>
>         Fire On The Mountain>
>         Good Lovin'

##### Separate Tracks

###### Example 1

> d2t03 - Scarlet Begonias>
> d2t04 - Fire On The Mountain>
> d2t05 - Good Lovin'

###### Example 2

> Scarlet Begonias>
> Fire On The Mountain>
> Good Lovin'

## Show Folder Sub Folders

1. Usually tracks in _Show Folders_ are in the _Show Folder_ as all tracks in the same folder.
2. _Show Tagger_ only supports tracks that are _all in the same folder_
3. Therefore, if tracks are split up in multiple _subfolders_ then they must be moved into the parent (_Show Folder_) before tagging with _Show Taggers_
4. The problem is that often they have the same filenames e.g. `\disc1\track1.mp3`, `disc2\track1.mp3`
5. so these files with the same filenames need to be renamed before tagging
6. and they must be renamed in order.. e.g. `disc1_track1.mp3`, `disc1_track2.mp3`, `disc2_track1.mp3` is good.. all in alphabetical order
7. Early and Late Show example: `early/track1.m4a`, `late/track1.m4a` -> `early_track1.m4a`, `late_track1.m4a`... this is fine because `early_` comes before `late_` alphabetically

## MELD

1. when meld is used for comparisons, don't wait for meld o terminate.. open it with the files to compare.. then open the next comparison, etc. so we can have multiple comparisons open.. one for each show folder being processed.
2. after MELD closes, monitor the changes that were made (if any) to the show.txt - the user may have edited it in MELD... and then take these into consideration when writing future show.txt, if it makes sense why the user did that.. so that the user doesn't have to make such or similar changes again manually in the future
3. MELD should only be opened after all `show.txt` files have been created for all Show Folders within the folder we are processing. They should be opened in **parallel **so that the user can read/edit them all at once. ***Do not wait ***for one instance of Meld to close before the next is opened.

## Processing

Processing is done on a bunch of "show folders", which are the subfolders of the folder that is being processed.

Processing should be done each step in batch... i.e. first step for all show folders to process, then 2nd step for all show folders to process, etc.

Processing means to do the following:

1. create a `show.txt` file based off of the appropriate text file (the one with the setlist) in the folder, for all show folders

2. open Meld to compare the original text file and the created `show.txt`file *(ask for user confirmation to proceed first)*

3. once all Meld instances are closed, ask user for confirmation to tag the show folders using the Show Taggers program

4. once user gives confirmation, then use Show Taggers on the Folder than contains the show folders

### What you should NEVER do

1. NEVER start processing any show folders which exist outside of the folder the user instructed you to process.. show folders which are subfolders or nested within the folder to process is ok, anything outside of it is not
2. NEVER respect `.gitignore`, that is used just for `git` management of the markdown files that another tool uses

### Monitoring User Changes

1. monitor the changes the user made (if any) to the `show.txt` file

2. try to understand why the user did this (especially according to how it relates to the `Show Tagger.txt` manual)

3. try to follow similar style of editing in future generation of `show.txt`

## Wait for further instructions

1. wait to be told what folders to process to begin processing it as per instructions in the "Processing" section above

## Failed Tagging

read `failed-tagging.md` for Instructions on how to _Sleuth_ the reasons the Tagging Failed on a _Show Folder_ 

usually failed tagging ends up moved into a `failed-tagging` folder and successfully tagged shows get moved into a `tagged` folder, by _Show Taggers_
