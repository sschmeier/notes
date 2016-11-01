# Note taking on command line

## Setup
Put this into .bashrc, etc. but change directory accordingly where you want to save your notes:

```bash
n() {
    $EDITOR ~/projects/github/notes/"$*".txt
}
nls() {
    ls -1c ~/projects/github/notes/*.txt | grep "$*"
}
nv() {
    cat ~/projects/github/notes/"$*".txt
}
nrm() {
    rm ~/projects/github/notes/"$*".txt
}
```


## Usage

```bash
# create a note for storing vim commands I never seem to remember
n vim

# Look for a note by name
nls vim

# Quick look into note content
nv vim
```
