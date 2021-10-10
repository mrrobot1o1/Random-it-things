# Random-it-things

## Disbale Windows Defender in LTSC 2019

1. Go to __Settings -> Apps -> Startup__ and disable Windows Security notification icon

2. Open gpedit.msc and go to:

    - __Computer Configuration -> Administrative Templates -> Windows Components -> Windows Defender Antivirus.__ Open the Turn off Windows Defender Antivirus policy and set it as Enabled.

    - __Computer Configuration -> Administrative Templates -> Windows Components -> Windows Defender Application Guard.__ Open the Turn on Windows Defender Application Guard in Enterprise Mode policy, set it as Enabled and set it's data value to 0.

    - __Computer Configuration -> Administrative Templates -> Windows Components -> Windows Defender SmartScreen -> Explorer.__ Open the two policies there and set them both to Disabled.

    - __Computer Configuration -> Administrative Templates -> Windows Components -> Windows Defender SmartScreen -> Microsoft Edge.__ Open the first policy there and set it to Disabled.

3. Open regedit and go to:

- **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SecurityHealthService**. Open the registry entry called Start and set it's data value to 4.

4. Reboot Windows and Defender will be gone forever!



## Wrong Login Screen Resolution (LightDM)

```sh
sudo gedit /usr/share/X11/xorg.conf.d/52-myres.conf
```
then in the file:
```
Section "Monitor"
    Identifier "VGA1"
    Option "PreferredMode" "1152x864"
EndSection
```
Save and exit. The values were obtained from command xrandr -q. VGA1 is the name of my connector and 1152x864 is the name of the resolution.



## Some Text Formattings

```sh
cat programs.txt | sed 's/https\?:\/\///; /Seaching for Bug/d'
cat programs.txt | sed 's/https\?:\/\///' | awk '!/Seaching for Bug/' > targtest.txt
cat programs.txt | sed 's/https\?:\/\///; /Seaching for Bug/d; /Disclosour-Search/d; s/^www.//g' | awk -F\/ '{print $1}'
cat domains_list.txt | sed  '/Seaching for Bug Bounty/d; /[*]/d; /Fuck Something/d; s/https\?:\/\///; s/^www.//g' | awk -F\/ '{print $1}'
```
## Only keep passwords that are 8 to 63 characters in length
```sh
sudo grep -x '.\{8,63\}' rockyou.txt > wparockyou.txt       
wc -l wparockyou.txt
```
## GET CIDR IPs from json
```sh
jq '.Information[] | ."CIDR Range"' mxtest.json  | tr -d \"
```
## GET ASN
```sh
ipinfo 17.253.144.10 | jq .org | tr -d \" | awk '{print $1}'
```
## Delete old commites

```sh
git rev-list HEAD --count
git checkout --orphan backup
git rev-list HEAD --count
git add -A
git commit -am "Removed All old commits"
git branch -D master
git branch -m master
git push -f origin master
```
## Set Github Remove Origin 
```sh
git remote set-url origin git@github.com:mrrobot1o1/cheetsheets.git
```
## Change recent commite massage
```sh
git commit --amend -m "Initial commit"
```

## PDF Password Remove
```sh
qpdf --password=@Hide01 --decypt Sec542.pdf Sec542-1.pdf

OR

pdftops -upw @Hide01 Sec542.pdf nopassword.pdf
```


## Remove all empty line

### sed

```sh
sed '/^[[:space:]]*$/d'
sed '/^\s*$/d'
sed '/^$/d'
sed -n '/^\s*$/!p'
```
### grep

```sh
grep .
grep -v '^$'
grep -v '^\s*$'
grep -v '^[[:space:]]*$'
```
### awk

```sh
awk /./
awk 'NF'
awk 'length'
awk '/^[ \t]*$/ {next;} {print}'
awk '!/^[ \t]*$/'
```

## Install Neovim

## Dep
```sh
sudo apt-get install gettext libtool libtool-bin autoconf automake cmake g++ pkg-config unzip build-essential
```
===> Download compile
```sh
cd $(mktemp -d)
git clone https://github.com/neovim/neovim --depth 1
cd neovim
sudo make CMAKE_BUILD_TYPE=Release install
cd ..
sudo rm -r neovim
```

https://sharedby.blomp.com/pFmWz5



## Disbale Touchpad  Linux
```sh
xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 0
```
## Enable Touchpad
```sh
xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1
```

## Open Gmail with mail to Similar to MAILTO:]

https://mail.google.com/mail/u/0/?fs=1&to=test@test.com&tf=cm


https://mail.google.com/mail/?view=cm&fs=1&tf=1&to=target@email.com


## Custom PS1
```sh
export PS1="\[\e[1;32m\]john@ubuntu:\[\e[0;32m\]\w\[\e[0;35m\]$(gitPrompt)\[\e[0;32m\]▶\[\e[0;37m\]"
```
