# Sleuthing Failed Tagging

1. go through the `failed-tagging` folder for each _Show Folder_ there to try to determine what the cause is most likely as to why it failed

## Files

on tagging failure, try to determine:

1. if the # of files matches the # of songs in the setlist 
2. what the small tracks are (small audio files which are substantially smaller than the other audio files)

### often the discrepancy in the number of songs in the Setlist vs the # of tracks (files) are due to:

1. small tracks present but no corresponding label in the Setlist
2. label in the Setlist but no corresponding small track

#### Labels of these Small Tracks

small track labels are usually worded something like:

1. crowd
2. tuning
3. banter
4. some other description of a joke, statement, announcement, etc.
5. encore break
6. break
7. or something else describing what is not an actual song

#### `Encore Break`

an `Encore Break` in a setlist should **always** be renamed to `Break` in the `show.txt`. This is because `Encore` is a keyword used to determine the start of an `Encore`

if there is no indication of the start of an `Encore` like no `Encore` or `E:`, etc. preceeding the `Encore Break` line.. then `Encore Break` should be written as 2 lines `E:` and then `Break`... if it there is such an indication then just write `Break` on a line after the `Encore`, `E:` or whatever that indicates an `Encore` segment has been started

## Reading the Filenames and Existing Tags

### Filenames

Sometimes the song names might be on the filenames themselves. That should greatly help the Sleuthing.

### Existing Tags in the Files

Also, there may be existing tags already on the Audio Tracks. So it is possible to read these using Tag Reading Tools. 

Usually Tagging should fail before _Show Tagger_ modifies any tags, but occasionally it might start tagging and then fail due to not being able to read a file.

So if the Tag of the Existing file exactly matches the name in our `show.txt`, it might be that _Show Taggers_ tagged that file already. 

#### Command Line Tag Reading Tools on Our System

1. Kid3: `D:\PortableApps\Audio\Tagging\kid3-3.9.1-win32-x64\kid3-cli.exe`
2. 