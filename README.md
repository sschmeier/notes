# Note taking on the command line

Simple and quick note taking on the CLI. Uses git to store notes to remote.
Can be integrated with Dropbox and e.g. [nvALT](http://brettterpstra.com/projects/nvalt).


## Setup
Put this into .bashrc, etc. but change directory accordingly where you want to save your notes:

```bash
NOTESDIR=~/Dropbox/Notes
n() {
    $EDITOR $NOTESDIR/"$*".txt
}
nn() {
    cat $NOTESDIR/"$*".txt
}
n.help() {
    cat $NOTESDIR/notes.txt
}
n.s() {
    ls -1c $NOTESDIR/*.txt | xargs -I pattern basename pattern | grep "$*" | sed s/.txt//g | sort
}
n.grep() {
     egrep -i "$*" $NOTESDIR/*.txt
}
n.ls() {
    for filename in $NOTESDIR/*.txt; do echo -n "$(stat -c%y -- $filename 2> /dev/null) | "; echo $(basename $filename); done
}
n.lst() {
    for filename in $NOTESDIR/*.txt; do echo -n "$(stat -c%y -- $filename 2> /dev/null) | "; echo $(basename $filename); done | sort -r | head -10
}
n.rm() {
    rm $NOTESDIR/"$*".txt
}
n.md() {
    pandoc $NOTESDIR/"$*".txt | lynx -stdin
}
```


## Usage

```bash
# create / edit a note for storing vim commands I never seem to remember
n vim

# List all notes by name
n.ls

# List all notes by last time modified
n.lst

# Look for a note by name
n.s vim

# Quick look into note content => cat
nn vim

# find all notes with text in note
n.grep bla
```

## Table of commands

| WHAT                          | CMD           |
| ----------------------------  |:------------- |
| OPEN NOTE                     | n NOTE        |
| QUICK VIEW NOTE               | nn NOTE       |
| FIND NOTE                     | ns. [NOTE] |
| LIST NOTES BY NAME (ALL)      | n.ls          |
| LIST NOTES LAST MODIFIED (10) | n.lst         |
| FIND TEXT IN NOTE (egrep)     | n.grep TEXT   |
| RENDER NOTE IN LYNX           | n.md NOTE     |
| REMOVE NOTE                   | n.rm NOTE     |
