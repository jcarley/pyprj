I have a setup location on my machine where I put my projects.  In that
projects folder I have several areas that projects get grouped into.  I like to
tab complete to find my projects.  I only know how to make this work in the zsh
shell.


The follow lines should go into your .zshrc file, or into a file sourced by your .zshrc file.
```
function myprojects() {
  if [ -z "$1" ]; then
    cd ${HOME}/Projects/
  else
    cd $1
  fi
}

function _myprojects() {
  local completions
  completions="$(<path to python script>/pyprj)"
  reply=( "${(ps:\n:)completions}" )
}
compctl -K _myprojects myprojects
```

Then in a terminal window type myprojects <TAB>, and you'll get a listing of all your projects that
have a .git directory.
