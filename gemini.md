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

1. any _Show Folder_ which contains an Early and/or Late Show, should be moved into a folder of the parent folder called "Early Late Shows"
2. other than that, they should not be processed. No `show.txt` created for them.

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
