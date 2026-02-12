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


# Hydra Basic Components
---
## Sources
### Visual Oscillator (osc)

**Function Prototype : osc(frequency,sync,color_offset)**

- Frequency : Instances of a particular color in a single frame [0,100]
- Sync : Refresh rate in seconds [0,Screen Refresh Rate]
- Color offset : Range of colors that would be shown. [0,1]

1. Displays a basic visual oscillator
```javascript
osc().out()
```
[Sandbox : Basic Osc](https://hydra.ojack.xyz/?code=b3NjKCkub3V0KCk%3D "@embed")

2. Oscillator operating at a frequency = 2, Sync = 1, Color_Offset = 100
```javascript
osc(2,1,100).out()
```
[Sandbox : Oscv2](https://hydra.ojack.xyz/?code=b3NjKDIlMkMxJTJDMTAwKS5vdXQoKQ%3D%3D "@embed")

### Exercise
1. osc(1,5,255).out()
2. osc(2,1,2).out()

---

### Solid Color | solid(r,g,b,a=1)

1. Displays a red solid color
```javascript
solid(1,0,0,1).out()
```

[Sandbox : Red Solid Color](https://hydra.ojack.xyz/?code=c29saWQoMSUyQzAlMkMwJTJDMSkub3V0KCklMEE%3D "@embed")

2. Displays two solid color blocks and render them in individual blocks
```javascript
solid(1,0,0,1).out(o0)
solid(0,1,0,1).out(o1)
render()
```
[Sandbox : Displays two solid color blocks](https://hydra.ojack.xyz/?code=c29saWQoMSUyQzAlMkMwJTJDMSkub3V0KG8wKSUwQXNvbGlkKDAlMkMxJTJDMCUyQzEpLm91dChvMSklMEFyZW5kZXIoKQ%3D%3D "@embed")

---
### Noise | noise(scale,offset) | Perlin Noise  
- scale: Blobs of noise that would be rendered [0,10]
- offset: Refresh rate for the noise (In Seconds)
1. Displays a noise blob
```javascript
noise(1,0).out()
```

[Sandbox : static noise frame](https://hydra.ojack.xyz/?code=bm9pc2UoMSUyQzApLm91dCgp "@embed")

2. Displays Noise in Motion
```javascript
noise(5,1).out()
render()
```
[Sandbox : Noise in Motion](https://hydra.ojack.xyz/?code=bm9pc2UoNSUyQzEpLm91dCgp "@embed")

---
# Audio Reactivity
Audio Reactivity in Hydra can be enabled by using object "a". 

## Common Functions
### setBins(int numberOfBins) | Range [1,12]
This sets the number of FFT bins for analysis.
### setSmooth(float smoothFactor) | Range [0,1]
This sets the FFT refresh rate, 0 : Highest refresh rate, 1: Slowest Refresh Rate
### setCutoff(float cutoffFactor) | Range [0,40]
Minimum threshold value in an fft bin. Values less than the threshold are disregarded for reactivity.
### setScale(float scaleAmount) | Range [0,40]
Sets the FFT Bin Scale

### Code Example for Setting up Audio Reactivity

```javascript
a.setBins(4)
a.setSmooth(0.7)
a.setCutoff(6)
a.setScale(16)
a.show()
```

### Basic Audio Reactive Visualizer using noise
```javascript
a.setBins(4)
a.setSmooth(0.7)
a.setCutoff(6)
a.setScale(16)

noise(()=>(a.fft[1]*255),0,1).rotate(()=>(a.fft[2]*32)).out()
a.show()
```
### Override an existing Sketch with Audio Reactivity
```javascript
a.setBins(4)
a.setSmooth(0.7)
a.setCutoff(6)
a.setScale(16)
osc(6, 0, 0.8)
  .color(1.14, 0.6,.80)
  .rotate(0.92, 0.3)
  .pixelate(20, 10)
  .mult(osc(40, 0.03).thresh(0.4).rotate(0, -0.02))
  .modulateRotate(osc(20, 0).thresh(0.3, 0.6), () => 0.1 + a.fft[1] )
  .out(o0)
```



```
