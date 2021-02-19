# hakase
Cycle System Based Time Management Tool for *nix Systems

# how to setup
* clone repo
* run `hakase-helper`
* edit the `hakase.config` and `template.hake` in your ~/hakase folder to your preferences
* add alias for hakase to .zshrc or .bashrc file

# commands
* `hakase` = opens working file (~/hakase/working.hake) in editor
* `hakase copy` = copies working file to archive with $DATE.hake as filename
* `hakase copy WHATEVER` = copies working file to archive with $WHATEVER.hake as filename
* `hakase fresh` = overwrites working file with template and adds date to the top of working (reset for a new day)
* `hakase load WHATEVER` = overwrites working file with the WHATEVER or WHATEVER.hake file from the archive
* `hakase how are ya doing today` = gives a polite error message

# config items
* `editor` whatever your preferred editor is (default is gnu nano)
* `editorSettings` arguments for your editor **including** the `-` (default is `""`)
* `location` where you'll be storing the hakase script (default is `$HOME/hakase`)
* `archive` where you'll be storing the individual day files (default is `$location/days`)
* `working` where your working file is stored and what it's named (default `$location/working.hake`)
* `template` where your template file is stored and what it's named (default `$location/template.hake`)
* `save` where your backup file is stored and what it's named (default `$archive/save.hake`)
* `dateFormat` what format you'd like the files to be named with (default is POSIX date command using backticks, specifically     `` `date +%y-%m-%d` ``)

# issues
* hakase helper is fragile and dangerous

# goals
* add carryover functionality to `hakase fresh`
* make hakase-helper do path stuff