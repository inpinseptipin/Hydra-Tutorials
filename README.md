# Hydra-Tutorials
Tutorials on using Hydra video synth [Sandbox](https://hydra.ojack.xyz/?sketch_id=mahalia_3)

## Tools Required for Audio Reactive Visuals
For MacOS : [Blackhole](https://existential.audio/blackhole/)

For Windows : [VB-Audio](https://vb-audio.com/Cable/)

**Browser :** Google Chrome (Best Results)

## Setting up Blackhole
In Audio MIDI settings, set Input to Blackhole2ch
In Audio MIDI settings, create a Multioutput device and select "Mac Output Speakers/Mac Mini Speakers" and Blackhole 2ch (Order Matters).

![blackhole-flow](https://github.com/inpinseptipin/Hydra-Tutorials/blob/master/Blackhole_Loopback.png)


## Hydra Basic Components
### Visual Oscillator (osc)
1. Showcase a basic visual oscillator
```javascript
osc().out()
```
[Sandbox : Basic Osc](https://hydra.ojack.xyz/?code=b3NjKCkub3V0KCk%3D "@embed")

