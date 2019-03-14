# Software Guides

All of the pre-installed software is configured to use the shared Jack backend, so all of it should work right out of the box without a need to tweak the settings. If you install some new software, make sure to configure it to use Jack in its audio settings.

Below are some quick tutorials demonstrating the basic use of the included software.

It could be interesting to keep `patchage` running in the background, to see a visualization of the current Jack backend state and the interconnections between the software and hardware.

## Audacity
![](https://d2mxuefqeaa7sj.cloudfront.net/s_0673996173D822520B2E86E1EB274A16952B49EDCFECF96A4B6F28FA05AFBC2E_1552549688006_image.png)


[Audacity](https://www.audacityteam.org/) is a multi-track wave recorder / editor tool. It is pretty simple to use, after launching it, just click the Record button and it will record the input ports that are available to the Jack backend. After you’re done recording, hit the Stop button, and then the Play button to listen to what was recorded.

Audacity behaves in a bit of an unusual way in the Jack-compatible software world, as it creates its Jack ports only for the duration the playback or recording is happening. That makes it a bit difficult to do custom routing in `patchage`. See [Audacity’s Wiki](https://wiki.audacityteam.org/wiki/Linux_Issues#JACK) for more details on its Jack integration.

## Patchage
![](https://d2mxuefqeaa7sj.cloudfront.net/s_0673996173D822520B2E86E1EB274A16952B49EDCFECF96A4B6F28FA05AFBC2E_1552550823771_image.png)


[Patchage](https://drobilla.net/software/patchage) is a tool to visualize and modify the state of Jack and ALSA MIDI applications. The green colors indicate Audio signal ports and interconnections, red ones indicate JACK MIDI ports and interconnections (in practice not used much, as same capability is provided by ALSA MIDI) and the purple ones indicate the ALSA MIDI ports and interconnections.

The above screenshot shows how the Jack state looks like with Pure Data launched - the Pisound’s input stream is connected to Pure Data’s input, and Pure Data’s output is connected to Pisound’s output. The MIDI routings show that hardware inputs are connected to Pure Data and `pisound-ctl` and Pure Data’s MIDI output is connected to the hardware outputs.

Using this tool you may cut the undesired connections and make new ones.

## Pianoteq Standard Trial
![](https://d2mxuefqeaa7sj.cloudfront.net/s_0673996173D822520B2E86E1EB274A16952B49EDCFECF96A4B6F28FA05AFBC2E_1552551825461_image.png)


[Pianoteq](https://www.pianoteq.com/) is a virtual instrument that reproduces acoustic sounds and playability of a real instrument by physically modeling the selected instrument. This is a trial version of the software, it has some limitations such as disabled keys, and it stops playing after some time.

Simply start the program, hook up a MIDI keyboard via USB or DIN-5 input port, and play around. Or if you don’t have a keyboard available, you can still play with your mouse using the keyboard at the bottom, or play a MIDI track using the top bar.

It is available as an LV2 plugin too, so it can be used in LV2 host software.

## Pure Data
![](https://d2mxuefqeaa7sj.cloudfront.net/s_0673996173D822520B2E86E1EB274A16952B49EDCFECF96A4B6F28FA05AFBC2E_1552554588336_image.png)


[Pure Data](http://puredata.info/) is a visual programming language for multimedia.

The OS image comes bundled with a couple of example patches. Let’s give one of them a try - launch Pure Data, and open this file:

`/usr/local/puredata-patches/GarageBeat/0_START.pd`

It is a rhythmic generative patch, you may then try playing around with the controls in the UI.

Check out the [Pisound App](https://blokas.io/pisound/docs/Pisound-App/) too which has an integration with Pure Data patches, it can be used to switch between patches and control its parameters using your phone and allows integrating [MIDI mappable controls](https://community.blokas.io/t/pure-data-patch-with-parameters-in-the-pisound-app/622).


## Sonic Pi
![](https://d2mxuefqeaa7sj.cloudfront.net/s_0673996173D822520B2E86E1EB274A16952B49EDCFECF96A4B6F28FA05AFBC2E_1552555255575_image.png)


[Sonic Pi](https://sonic-pi.net) is The Live Coding Music Synth for Everyone.

Let’s build a very simple synth - paste the following code into the code area:


    use_synth :prophet
    
    live_loop :midi_piano do
      use_real_time
      note, velocity = sync "/midi/*/*/*/note_on"
      synth :prophet, note: note, amp: velocity / 127.0
    end

Click the ‘Run’ button, hook up a MIDI keyboard, and play!

Check out the Examples section at the bottom area for more stuff to try out!

## SuperCollider
![](https://d2mxuefqeaa7sj.cloudfront.net/s_0673996173D822520B2E86E1EB274A16952B49EDCFECF96A4B6F28FA05AFBC2E_1552555847712_image.png)


[SuperCollider](https://supercollider.github.io/) is a platform for audio synthesis and algorithmic composition. A lot of neat, tweet sized, examples can be found on the internet, like the one below by [@joshpar](https://twitter.com/joshpar/status/100417407021092864).  To run it, paste the contents into the code area, then do `Server→Boot Server`, then `Language→Evaluate File`.


    play{a=SinOsc.ar(LFNoise0.ar(10).range(100,1e4),0,0.05)*Decay.kr(Dust.kr(1));GVerb.ar(a*LFNoise1.ar(40),299,400,0.2,0.5,50,0,0.2,0.9)}
## TouchOSC2MIDI

[TouchOSC2MIDI](https://github.com/velolala/touchosc2midi) is a background process that translates [TouchOSC](https://hexler.net/software/touchosc) compatible App interactions on your mobile device to MIDI messages on the PatchboxOS.

To use it, PatchboxOS must be connected to a local network or act as a WiFi hotspot. Your portable device must be connected to the same network. Open the TouchOSC app settings, and enter the IP of PatchboxOS device into ‘TouchOSC Bridge’ setting. If your network configuration permits it, the PatchboxOS may be auto-detected within the settings.

After the IP is set up, you may use the app to control audio software just as if you were using a MIDI controller.
