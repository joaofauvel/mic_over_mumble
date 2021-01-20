# Voice over Mumble

Use Android device as your PC's microphone, using Mumble + [Mumla](https://f-droid.org/en/packages/se.lublin.mumla/). Or use microphone of one PC on other PC.

Linux-only script, but steps can be replicated on other systems (e.g. using VoiceMeeter).

This is the lowest latency I've ever achieved (sounds almost like local loopback, theoretically 7ms WiFi delay + 2x 10ms codec delay = 27 ms).

Alternatives: [WO Mic](https://wolicheng.com/womic/wo_mic_linux.html), [pulseaudio-virtualmic](https://github.com/MatthiasCoppens/pulseaudio-virtualmic).

## Installation

Install Mumble (desktop client) + uMurmur (server) + [Mumla](https://f-droid.org/en/packages/se.lublin.mumla/) (Android client). Set all 3 programs to use best quality and minimal latency. Set mobile client to always streaming.

To install Mumble + uMurmur on Arch, you can use:

```bash
sudo pacman -S mumble umurmur
sudo systemctl stop umurmur.service
sudo systemctl disable umurmur.service
```

Autodiscovery is disabled. Manually add a server on Mumla or another computer by entering the host ip address and any username.

Copy `mic_over_mumble` anywhere - it will use `~/.mic_over_Mumble` as configuration directory. Don't forget to make it executable (`chmod +x mic_over_mumble`).

Run `mic_over_mumble`. It will start the server on LAN, then start Mumble (if asked for nickname, enter anything other than SuperUser). Then connect your mobile device to the LAN server manually.

Then, set up your programs to use either "Monitor_of_Mumble" or "VirtualMic" as input device (they are linked). E.g. in OBS:

![Screenshot of OBS configuration](obs_screenshot.png)

If for some reason the script messes up your audio config, you can use `pulseaudio -k` to reload PA.
