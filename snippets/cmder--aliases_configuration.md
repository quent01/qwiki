;= @echo off
;= rem Call DOSKEY and use this file as the macrofile
;= %SystemRoot%\system32\doskey /listsize=1000 /macrofile=%0%
;= rem In batch mode, jump to the end of the file
;= goto:eof
;= Add aliases below here
;= -----------------------------------------------------
;=
;=   $$$$$$\  $$\      $$\ $$$$$$$\    $$$$$$$$\ $$$$$$$\  
;=  $$  __$$\ $$$\    $$$ |$$  __$$\   $$  _____|$$  __$$\ 
;=  $$ /  \__|$$$$\  $$$$ |$$ |   $$\  $$ |      $$ |  $$ |
;=  $$ |      $$\$$\$$ $$ |$$ |    $$\ $$$$$\    $$$$$$$  |
;=  $$ |      $$ \$$$  $$ |$$ |   $$ / $$  __|   $$  __$$< 
;=  $$ |  $$\ $$ |\$  /$$ |$$ |  $$ /  $$ |      $$ |  $$ |
;=  \$$$$$$  |$$ | \_/ $$ |$$$$$$$ /   $$$$$$$$\ $$ |  $$ |
;=   \______/ \__|     \__|\______/    \________|\__|  \__|
;= 
;= -----------------------------------------------------

;= ------------------------------------------------
;= PATH SHORTCUT
;= ------------------------------------------------
$go     = cd /d E:\_GO\
$host   = cd /d C:\Windows\System32\drivers\etc
$home   = cd /d C:\Users\Quentin

$dev    = cd /d "E:"
$tiz    = cd /d "E:\_TIZ\"
$site   = cd /d "E:\_SITES\public\"

$drupal = cd /d "E:\_SITES\public\_DRUPAL\"
$wp     = cd /d "E:\_SITES\public\_WORDPRESS\"


;= ------------------------------------------------
;= LINUX COMMAND
;= ------------------------------------------------
e. = explorer .
find = %CMDER_ROOT%\vendor\git-for-windows\usr\bin\find.exe $*

gbranch = git branch -vv
glog    = git log --oneline --all --graph --decorate --color $*
gstatus = git status -s
gi      = git init
gpom    = git pull origin master
gpos    = git pull origin stage
gb      = git branch $*
gnewfeature = git reset --hard HEAD && git checkout master && git pull origin master && git checkout -b $1

l  = ls -al
ls=ls --show-control-chars -F --color $*

pwd   = cd
clear = cls

npm-ls = npm ls --global --depth=0
grep   = grep --color=auto

history=cat "%CMDER_ROOT%\config\.history"
unalias=alias /d $1
vi=vim $*
cmderr=cd /d "%CMDER_ROOT%"

;= ------- SHOW MY IP ADRESS ----------------------
myip = curl https://ipecho.net/plain

;= ------- VAGRANT --------------------------------
vup          = vagrant up
vhalt        = vagrant halt
vssh         = vagrant ssh
vprovision   = vagrant provision
vdestroy     = vagrant destroy


;= ------------------------------------------------
;= ALIASES FOR DIFFICULT TO REMEMBER COMMAND
;= ------------------------------------------------
npmlist = npm list -g --depth=0
weather = wego
weather2 = curl "http://wttr.in/strasbourg"

;= ------------------------------------------------
;= LAUNCH PROGRAMM LIKE A NINJA
;= ------------------------------------------------
chrome      = "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" $*
evernote    = "C:\Program Files (x86)\Evernote\Evernote\Evernote.exe"
firefox     = "C:\Program Files (x86)\Firefox Developer Edition\firefox.exe" $*
heidisql    = "C:\Program Files\HeidiSQL\heidisql.exe"
illustrator = "C:\Program Files (x86)\Adobe\Adobe Illustrator CS5.1\Support Files\Contents\Windows\Illustrator.exe"
photoshop   = "C:\Program Files (x86)\Adobe\Adobe Photoshop CS5.1\Photoshop.exe"
potato      = "C:\Users\Quentin\AppData\Roaming\CouchPotato\application\CouchPotato.exe"
spotify     = "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" open.spotify.com
sublime     = "C:\Program Files\Sublime Text 3\sublime_text.exe"
qbtorrent   = "C:\Program Files (x86)\qBittorrent\qbittorrent.exe" 
wmplayer    = "C:\Program Files (x86)\Windows Media Player\wmplayer.exe"