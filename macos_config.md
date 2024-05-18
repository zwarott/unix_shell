# :computer: MacOS Configuration and Tips


## :woman_technologist: Create a custom login message
```
sudo defaults write /Library/Preferences/com.apple.loginwindow LoginwindowText "Text you want to have as LOgin Message."
```


## :house: Get IP adress
```
ifconfig en0 | grep inet | awk '{ print $2 }'
```


## :toilet: Flush DNS cache
After pass sudo password DNS cache will be flushed
```
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```

## :key: Set ID Touch as a sudo password
:one: **Step 1**: After passing sudo password DNS cache will be flushed   
:two: **Step 2**
```
sudo nano /etc/pam.d/sudo
```
:three: **Step 3**: Write sudo password   
:four: **Step 4**
```
auth sufficient pam_tid.so
```
:five: **Step 5**: Press `Ctrl + X`, press `Y` and press `Enter` to save.


## :skull: Kill actively running computer processes
Shut down Preview as a running computer processes
```
killall Preview
```


## :information_desk_person: Change a device's name
Local Hostname
```
sudo scutil --set LocalHostName Zwarotts MacBook Pro; killall -HUP mDNSResponder
```


## :signal_strength: Get password of connected Wi-Fi network
After pass this command, enter admin username and password and you get this password. In double quotes is Wi-Fi name. 
```
security find-generic-password -wa "Wifi name"
```


## :arrow_double_up: Check MacOS update
```
softwareupdate -l
```


## :mag: Finder settings
### Allow quitting
Allow quitting via `⌘ + Q`; doing so will also hide desktop icons
```
defaults write com.apple.finder QuitMenuItem -bool true; killall Finder
```
### Show path bar
Show path bar
```
defaults write com.apple.finder ShowPathbar -bool true; killall Finder
```
Do not show path bar
```
defaults write com.apple.finder ShowPathbar -bool false; killall Finder
```


## :gear: Able/Disable some functions 
### Disable auto-correct
```
defaults write NSGlobalDomain NSAutomaticSpellingCorrectionEnabled -bool false
```


## :sparkler: Screenshot setup
### Set up screenshots format
Set up `jpg` `png` `tiff` format
```
defaults write com.apple.screencapture type jpg; killall SystemUIServer
```
### Set up screenshots name
```
defaults write com.apple.screencapture name ""; killall SystemUIServer
```
### Set up screenshots destionation folder
```
defaults write com.apple.screencapture location ~/Documents; killall SystemUIServer
```
### Disable shadow in screenshots
```
defaults write com.apple.screencapture disable-shadow -bool true; killall SystemUIServer
```


## :coffee: Keep your Mac awake + Uptime
### Keep your Mac awake using caffeinate
If you need to prevent your Mac from going to sleep — say, you're running an extensive task, or recording your screen
```
caffeinate
```
Exit this node after 1000 seconds
```
caffeinate -t 1000
```
If you don't want to rely on being the one to end your poor Mac's suffering, you can also create a set a number of seconds before your Mac sleeps
```
caffeinate -u -t 5400
```
### How long has my Mac been running?
```
uptime
```


## :speaker: Make your Mac speak
This command is self explanatory, you can trigger the native text-to-voice function by writing a word/sentence followed by ‘say’.
```
say "sometext"
```
