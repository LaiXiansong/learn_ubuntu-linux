# How to control ubuntu PC
this is a file telling how to control ubuntu PC (windows)
## first method: vnc
### 1 search PC ip
    ifconfig   
find you ubuntu PC ip. (eg. 219.223.182.20)
### 2 open vnc server
    sudo apt install tightvncserver   
    sudo apt install x11vnc   
two vnc server are alternative, but recomend tightvnc. Then:   
    
    vncserver
open server
### 3 set password
when openning vnc server, you need to set password.(eg.300018)   
you can also set a watch-only password.(eg.214726)
### 4 download vnc viewer(windows)
download vnc viewer in another pc, and then input the ip of ubuntu PC.   
### 5 remove encryption
if you receive a X and are told to select a weaker level of encryption, try:   
    
    gesettings set org.gnome.Vino require-encryption false
