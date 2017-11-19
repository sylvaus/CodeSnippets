# CodeSnippets

Just a repository with code snippets for Python, C++, Installation.

## Ubuntu Setup
`sudo apt-get install build-essential git git-cola meld python python3 python-pip python3-pip python-dev python3-dev yakuake unity-tweak-tool numix-gtk-theme numix-icon-theme-circle nmap geany`

## Ubuntu Laptop Battery life improvement
`sudo apt-get install tlp indicator-cpufreq`

## History Search (Ubuntu terminal)
Add the following to the .bashrc:
```
if [[ $- == *i* ]]
then
    bind '"\e[A": history-search-backward'
    bind '"\e[B": history-search-forward'
fi
```
