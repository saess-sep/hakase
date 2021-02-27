# hakase
Hakase is a command line based time management system based on TIM? Limoncelli's "Cycle System" from *Time Management for System Administrators*.  It's made for macOS and Linux systems, but will also work on Windows using WSL.  The system works by passing formatted text files to an editor of your choice and then saving them to a sorted directory.  Hakase is written as a POSIX complaint shell script, and runs with `#!/bin/sh` by default.

## quick-start
To start using Hakase, clone the git repo and run the hakase-helper script.  This will place the script and a basic directory structure into your Home folder. 
* You can then run the hakase script from that folder (`~/hakase/hakase`). 
* It will use the GNU Nano editor by default and open the default template.hake file.  You can mark your to-do items, meetings, and notes as you'd like.  
* When you're done for the day you can save and close the file with `Control+O` to save and `Control+X` to exit. 
* To archive the day, run the Hakase script with the copy argument (`./hakase copy`).  
* To load a fresh day, run the Hakase script with the fresh argument (`./hakase fresh`).  

That should be enough to get you started, but you can read on to learn more about how Hakase works.

## setup

Hakase has a config file which has all of the options that are easily changed, but you can always edit the script as well.  

The config file is read from the script as Shell variables using the `source` command, so everything needs to be in the proper format.  This means `Variable=Options`, with no spaces.  Single and double quotes, as well as back ticks are respected and interpreted normally.  Be smart.

The options are as follows:
### program options
* Editor - Editor controls what editor Hakase will open files with.  The default is GNU Nano, but you can use whatever you'd like, even a GUI editor.  You can also set it to the $EDITOR environment variable, if you'd like to be set globally.
* EditorSettings - The arguments you'd like to run your editor with.  The default is no arguments, but you can add whatever arguments you'd like.
* DateFormat - The format is same as the POSIX date command.  The default is `+%y-%m-%d` which will output `21-02-25` on February 25, 2021.  This is used to name files in the archive as well as printed at the top of each file.  See the man page for the Date command on your system for more details.

### directory options
* WorkingDirectory - The working directory is where the Hakase script and config file are located.  By default, this is `$HOME/hakase`.  Also, by default this is where your WorkingFile and TemplateFile are stored as well.
* ArchiveDirectory - The archive directory is where your files are stored when you're done with them.  You can refer back to them for record keeping or alibies.  By default, the archive directory is saved inside the WorkingDirectory (`$HOME/hakase/archive`).  Also, by default this is where your SaveFile is stored.
* NetworkDirectory - The network directory is an optional variable.  You can set it if you have a network path that isn't always available, but where you'd like to save files to.  First, hakase saves to the ArchiveDirectory and then tries to save the same file and name to the network directory, but won't get too upset if it fails to save.

### file options
* WorkingFile - The working file is the current days file.  When you run `hakase` with no arguments, it opens the working file.
* TemplateFile - The template file is the template that each new day is based on.  The default is in the root of the WorkingDirectory.  You can edit the file this points at to add recurring meetings to your daily routine.
* SaveFile - The save file is a backup of your most recent working file.  It prevents accidental moving files about with `hakase copy` and `hakase load`.  The default in the root of the ArchiveDirectory.

## commands
You can run Hakase with no arguments to open the working file in the your chosen editor.  However, there are many fun and exciting options you can use to do things other than open Nano.
* `hakase` - opens the WorkingFile in the Editor with the EditorOptions.
* `hakase copy` - copies the current WorkingFile to the ArchiveDirectory with the name of "`date $DateFormat`.hake", and tries to copy to the NetworkDirectory as well (but doesn't worry too much if that fails).
    * `hakase copy NAME` - copy the current WorkingFile to the ArchiveDirectory with the name of "NAME.hake", and tries to copy to the NetworkDirectory as well (but doesn't worry too much if that fails).
    * `hakase copy /PATH/TO/FILE` - copy the current WorkingFile to the "PATH/TO/" directory with the name of "FILE.hake".  This option does **not** try to copy to the NetworkDirectory.
* `hakase load` - this actually give an error message, you need another argument after load.
    * `hakase load FILE` - overwrites WorkingFile with the file named "FILE.hake" or "FILE" **in that order** from the ArchiveDirectory or whatever your current directory is **in that order**.  If none of those are real files or you don't have access to them, you'll get an error.  The priority works as follows:
        1. ArchiveDirectory/FILE.hake 
        2. ArchiveDirectory/FILE
        3. CurrentDirectory/FILE.hake
        4. CurrentDirectory/FILE
        5. Error
    * `hakase load PATH/TO/FILE` - overwrites the WorkingFile with the file named "FILE.hake" or "FILE" (in that order) located at "PATH/TO" (the relative path) or "/PATH/TO" (the absolute path) **in that order**.  If none of those are real files or you don't have access to them, you'll get an error.  The priority is as follows:
        1. PATH/TO/FILE.hake
        2. PATH/TO/FILE
        3. /PATH/TO/FILE.hake
        4. /PATH/TO/FILE
        5. Error
* `hakase fresh` - overwrites the WorkingFile with the TemplateFile.

## current status
Currently, Hakase is being written as an exercise in "building to specification".  The readme on the Dev branch in no way reflects the current reality of the script, just how it *should* be *eventually*.  The Main branch has all the good "production ready" documentation (there are not enough quotes in the world for "production ready").  I'll update this section as things are fixed and "brought up to code".

## goals
Some nice to have things I have no plans to implement, in no particular order:
* Automatic importation from a calendar (Outlook, Gmail, etc).
* Rewriting as a GUI application so non-weirdos can use it
    * This but also a mobile app
* Automatic importation of to-do items from the previous day (during the fresh command most likely) based on their status.
* Ability to assign a priority or importance to the individual tasks, then sort them


## okay but what's up with the name?
"Hakase" is the Japanese word for "Professor". However, in this case, it's a reference to *Nichijou: My Ordinary Life*.  The character named "Hakase" frequently exclaims the name of "Nano", another character.  My original cycle-system document was "hakase" and was invoked with the command `nano hakase`, with me saying (out loud)

**~NANOOOOOO!~**