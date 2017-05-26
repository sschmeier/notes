# Note taking on command line

## Setup
Put this into .bashrc, etc. but change directory accordingly where you want to save your notes:

```bash
NOTESDIR=~/projects/github/notes
n() {
    $EDITOR $NOTESDIR/"$*".txt
}
nf() {
    ls -1c $NOTESDIR/*.txt | grep "$*" | xargs -I pattern basename pattern | sed s/.txt//g | sort
}
nls() {
    for filename in $NOTESDIR/*.txt; do echo -n "$(stat -c%y -- $filename 2> /dev/null) | "; echo $(basename $filename); done
}
nlst() {
    for filename in $NOTESDIR/*.txt; do echo -n "$(stat -c%y -- $filename 2> /dev/null) | "; echo $(basename $filename); done | sort -r | head -10
}
nv() {
    cat $NOTESDIR/"$*".txt
}
nrm() {
    rm $NOTESDIR/"$*".txt
}
nmd() {
    pandoc $NOTESDIR/"$*".txt | lynx -stdin
}
ngit() {
    cd $NOTESDIR; git st; cd - > /dev/null
}
ngitu() {
    cd $NOTESDIR; git pull; cd - > /dev/null
}
ngitc() {
    cd $NOTESDIR; git add *.txt; git commit; git push; cd - > /dev/null
}
ng() {
     egrep -i "$*" ~/projects/gitlab/notes/*.txt
}
```


## Usage

```bash
# create / edit a note for storing vim commands I never seem to remember
n vim

# List all notes by name
nls

# List all notes by last time modified
nlst

# Look for a note by name
nf vim

# Quick look into note content => cat
nv vim

# find all notes with text in note
ng bla
```

## Table of commands

| WHAT                         | CMD       |
| ---------------------------- |:--------- |
| OPEN NOTE                    | n NOTE    |
| FIND NOTE                    | nf [NOTE] |
| LIST NOTES BY NAME           | nls       |
| LIST NOTES BY LAST MODIFIED  | nlst      |
| FIND TEXT IN NOTE            | ng TEXT   |
| QUICK VIEW NOTE              | nv NOTE   |
| RENDER NOTE IN LYNX          | nmd NOTE  |
| REMOVE NOTE                  | nrm NOTE  |
| GIT: SHOW CHANGED NOTES      | ngit      |
| GIT: UPDATE NOTES            | ngitu     |
| GIT: ADD, COMMIT, PUSH NOTES | ngitc     |