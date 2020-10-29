# hakase
Cycle System Based Time Management Tool for *nix Systems

# how to setup
* clone repo
* run hakase-helper
* edit the config in the script in your ~/hakase folder
* add alias for hakase to .*shrc file

# commands
* hakase = opens working file (~/hakase/working.hake) in editor
* hakase copy = copies working file to archive with $DATE.hake as filename
* hakase copy WHATEVER = copies working file to archive with $WHATEVER.hake as filename
* hakase fresh = overwrites working file with template (reset for a new day)
* hakase load WHATEVER = overwrites working file with the WHATEVER or WHATEVER.hake file from the archive
* hakase how are ya doing today = gives a polite error message

# issues
* it's just terrible

# goals
* add hakase rank to order todo lists
* make hakase-helper do path stuff
* break out config into file
