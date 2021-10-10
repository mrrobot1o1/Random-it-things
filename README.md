

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



