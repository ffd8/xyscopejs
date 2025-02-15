# XYscope.js
v 0.4.2  
cc [teddavis.org](https://teddavis.org) 2025

p5.js library to render graphics on analog vector displays.  

XYscope.js converts the coordinates of primative shapes (point, line, rect, ellipse, vertex, box, sphere, torus, text...) to audio waveforms (oscillators with custom wavetables) which are sent to an analog display in XY-mode, revealing their vector graphic forms. This library began as [XYscope](https://teddavis.org/xyscope) for Processing in 2017 and has now been ported to p5.js and built from the ground up with the aim of live-coding oscilloscopes from your web browser in [P5LIVE](https://p5live.org)! Vector graphics shine on a vector display and now we can view (and hear) our generative works like never before!

[teddavis.org/xyscopejs](https://www.teddavis.org/xyscopejs)  
[github.com/ffd8/xyscopejs](https://github.com/ffd8/xyscopejs)

## Table of Contents
- [Getting Started](#getting-started)
- [Demos](#demos)
- [Audio Interfaces](#audio-interfaces)
- [Vector Displays](#vector-displays)
- [Additive Synthesis](#additive-synthesis)
- [References](#references)
- [Extras ](#extras)

## Getting Started
### Install
Download and include locally, or via [CDN](https://cdn.jsdelivr.net/gh/ffd8/xyscopejs@0.4.2/xyscope.js):  
`<script src="https://cdn.jsdelivr.net/gh/ffd8/xyscopejs@0.4.2/xyscope.js"></script>` 

For live-coding in [P5LIVE](https://p5live.org), include it in the libs array:  
`let libs = ['https://cdn.jsdelivr.net/gh/ffd8/xyscopejs@0.4.2/xyscope.js']`

### Setup
Here's a basic template to start live-coding within P5LIVE + XYscope.js.  
Essentially, add `xy.` and draw between `clearWaves()` and `buildWaves()`!

```js
let libs = ['https://cdn.jsdelivr.net/gh/ffd8/xyscopejs@0.4.2/xyscope.js', 'includes/libs/xyscope.js']
let xy // XYscope.js instance

function setup() {
	createCanvas(windowWidth, windowHeight)

	xy = new XYscope(this) // set instance
	xy.canvas() // resize canvas/scope to full height, centered

	// xy2 = new XYscope(this, xy.outXY) // optional dup for additive-synth
}

function draw() {
	clear()
	xy.drawXY() // draw virtual scope
	
	xy.clearWaves() // clear shapes buffer (like clear/background)
	
	xy.circle(width/2, height/2, 100) // add to shapes buffer
	
	xy.buildWaves() // build waves from shapes buffer
}

function mousePressed() {
	xy.resume() // user click required for sound in browser
}
```

## Demos
- quick start: [P5LIVE](https://p5live.org/?code=LyogCiAgWFlzY29wZS5qcyDigJMgcXVpY2sgc3RhcnQgCiAgY2MgdGVkZGF2aXMub3JnIDIwMjUKICAKICBKdXN0IGEgcXVpY2sgZGVtbyB0byBnZXQgeW91IHVwIGFuZCBydW5uaW5nLgogIEludGVuZGVkIGZvciBsaXZlLWNvZGluZyB1c2luZyBwNWxpdmUub3JnCiAgVmlzaXQgdGVkZGF2aXMub3JnL3h5c2NvcGVqcyBmb3IgcmVmZXJlbmNlcwogICovCgovLyBmb3IgUDVMSVZFIHVzYWdlCmxldCBsaWJzID0gWydodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvZ2gvZmZkOC94eXNjb3BlanNAMC40LjIveHlzY29wZS5qcycsICdpbmNsdWRlcy9saWJzL3h5c2NvcGUuanMnXQpsZXQgeHkKCmZ1bmN0aW9uIHNldHVwKCkgewoJY3JlYXRlQ2FudmFzKDUxMiwgNTEyKQoJeHkgPSBuZXcgWFlzY29wZSh0aGlzKSAvLyBpbml0IFhZc2NvcGUuanMKCXh5LmNhbnZhcygpIC8vIHJlc2l6ZSBjYW52YXMgdG8gaGVpZ2h0CgkvLyBiYWNrZ3JvdW5kKDEyMCkKCXdpbmRvd1Jlc2l6ZWQgPSBudWxsCn0KCmZ1bmN0aW9uIGRyYXcoKSB7CgliYWNrZ3JvdW5kKDApCgl4eS5kcmF3WFkoKSAvLyBkcmF3IHNjb3BlCgkvLyB4eS5kcmF3QWxsKCkgLy8gZHJhdyBzY29wZSArIGRlYnVnCgkKCW5vRmlsbCgpCglzdHJva2UoMjU1KQoJeHkuZHJhd1NoYXBlcygxKSAvLyB0b2dnbGUgb2ZmIHdpdGggMAoKCXh5LmZyZXEoMSkgLy8gYWRqdXN0IGZyZXEsIGRlZmF1bHQgaXMgNTAKCQoJeHkuY2xlYXJXYXZlcygpIC8vIGNsZWFyIHdhdmVzICsgc2hhcGVzIGJ1ZmZlcgoJeHkuY2lyY2xlKHdpZHRoLzIsIGhlaWdodC8yLCBmcmFtZUNvdW50JWhlaWdodCkgLy8gYWRkIHRvIGJ1ZmZlcgogICAgeHkucmVjdChmcmFtZUNvdW50JXdpZHRoLCBoZWlnaHQvMiwgMTAwKQoJCgl4eS5idWlsZFdhdmVzKCkgLy8gYnVpbGQgd2F2ZXMgYW5kIG91dHB1dCBhdWRpbwp9) / [p5.js Editor](https://editor.p5js.org/ffd8/sketches/zueGSQI-T)  
- _more coming sooooon... first getting this out there!_

## Audio Interfaces
When connecting to an actual oscilloscope,  you'll need a Digital to Analog Converter (DAC) to send your stereo audio signal to the XY-mode of a given display. Here's a few options based on price:

#### < $5  
At the very least you can use your computer's headphone jack with an [`1/8" to RCA`](https://duckduckgo.com/?q=1%2F8%22+to+RCA&t=h_&iax=images&ia=images) cable. However you'll soon want to get a [DC-Coupled](https://www.expert-sleepers.co.uk/siwacompatibility.html) audio interface for a cleaner and more stable visual (not wobbling/centering constantly). 

#### < $20  
For workshops I like to use some variant of the 48Khz [Delock 61645](https://www.delock.com/produkt/61645/merkmale.html) or 96Khz [Delock 63926](https://www.delock.com/produkt/63926/merkmale.html) – you'll find the same chip under many different brands and casings. For modern laptops, there's also a very compact 96Khz [Delock USB-C](https://www.delock.com/produkt/66304/merkmale.html) version.

#### > $150+  
Many of us in the community found the [MOTU Ultralite Mk3 Hybrid](https://motu.com/products/motuaudio/ultralite-mk3) (or newer versions) to be an ideal audio interface. Price varies from used to new. It offers, 10-channels of DC-Coupled 196Khz output, which is useful to drive multiple oscilloscopes or RGB lasers (X, Y, R, G, B).

### Select DAC
_XYscope.js can only use the browser/system selected audio interface – however multi-channel support will soon be added for customizing which channels are used for multiple diplays or RGB lasers._

## Vector Displays
Now we need a vector display to see our glowing output!

### Virtual
[XXY](https://dood.al/oscilloscope/) virtual oscilloscope rendering by Neil Thapen is built into XYscope.js! Activate it by simply adding `xy.drawXY()` to your code. See [rendering](#rendering) references below for complete options and customization.

### Analog Oscilloscope
This is what we really want! They have a Cathode-ray Tube (CRT) that is the magic behind this obsession. You'll find them for ~$50 used on auction websites – be sure it has 2-channels (z-axis input is a bonus) and that they show images of a sharp working beam. You'll need a few [`RCA to BNC`](https://duckduckgo.com/?q=RCA+to+BNC&t=h_&iar=images&iax=images&ia=images) adaptors to interface with it. Have fun playing with all the knobs to put it into `XY Mode` so that the 2-channels drive the beam X/Y (Horizontal/Vertical).

### X-Y Monitor
Similar to an analog oscilloscope, but usually has a larger display and reduced controls for X-Y (+Z) input, leaving away many of the features on an oscilloscope we won't use. They're more rare, expensive, but great if you stumble upon one. Don't confuse these with a 'vector monitor' which is used for calibrating TV broadcast and won't draw X-Y coordinates.

### Vectrex
A vector-graphics video game system of the 1980s, these amazing 9" displays can be [very carefully modified](https://users.sussex.ac.uk/~ad207/adweb/assets/vectrexminijackinputmod2014.pdf) (**CAREFUL - at own risk**) to override (on-demand) the videogame control of the monitor's XYZ inputs. It's ideal to use [switching jacks](https://www.youtube.com/watch?v=q3sKZA2r7qk) so videogames still works when cables are unplugged. You'll also want to apply the [SPOT KILLER MOD](https://www.facebook.com/groups/vectorsynthesis/posts/832237263652516/), but BE SURE to apply an appropriately high-voltage rated switch, so it can be toggled on and off.

_XYscope.js vectrex specific support is pending... it works, just not yet aspect ratio aware._

### Laser
Once you want something bigger than most screens, you'll want to move to an RGB Laser. They're BIG and BRIGHT, but also much slower and more dangerous! It's slower because it mechanically moves galvos/mirrors for the X-Y and dangerous, because, LASERS! Nevertheless, they can be controlled via the ILDA analog input, for which I've developed an easy to build [dac_ilda adaptor](https://github.com/ffd8/dac_ilda). To control a laser, you'll need a DAC (sound card) with a minimum of 5-channels, for sending `X, Y, R, G, B` signals. 

_ILDA RGB Laser specific support is pending... working on multi-channel support next._

## Additive Synthesis
Something very unique to this workflow is sending multiple audio signals to the oscilloscope, which interfer and modulate one another. As these waves combine, their amplitude and frequency determine ones influence on other waves. Key is having different frequencies and amplitudes to modulate off one another. The lower the frequency, the more it will push other waves around. The lower the amp, the less influence it has on the additive waveform. We can easily patch multiple instances of XYscope.js into the same audio output, thus creating endless surprises as the waves interact. 

```js
let libs = ['https://cdn.jsdelivr.net/gh/ffd8/xyscopejs@0.4.2/xyscope.js', 'includes/libs/xyscope.js']
let xy // XYscope.js instance

function setup() {
	createCanvas(windowWidth, windowHeight)

	xy = new XYscope(this) // set instance
	xy.canvas() // resize canvas/scope to full height, centered

	xy2 = new XYscope(this, xy.outXY) // patch xy2 onto xy's audio out
}

function draw() {
	xy.drawXY() // draw virtual scope

	xy.clearWaves() // clear shapes buffer
	xy.freq(50) // 50 is default hz of XYscope instance
	xy.circle(width/2, height/2, 100) // add to shapes buffer
	xy.buildWaves() // build waves from shapes buffer
	
	xy2.clearWaves() // clear 2nd buffer
	xy2.amp(.5) // experiment with amp/loudness of additive signal
	xy2.freq(25.1) // some relationship to 1st xy freq value
	// xy2.freq(225.1) // experiment with much higher freqs too!
	xy2.circle(width/2, height/2, 100) // add to 2nd buffer
	xy2.buildWaves() // build waves of 2nd buffer
}

function mousePressed() {
	xy.resume() // user click enables sound in browser
}
```

Additional tips:

- No need to stop at just 2, add as many as needed!  
- Ratio between freqs is crucial, diff of +/- .1 animates things. 
- Really low frequencies animate shapes over that path.  
- Really high frequencies display shape made of 2nd shape.
- Play with position of 2nd shape, from center to corners.

## References
XYscope.js is a class, so after an instance has been defined to a variable, we'll use that prefix in front of every function listed below (scoped), ie: `xy.ellipse()`. This enables us to have multiple XYscope.js instances running parallel, which will reveal wild and crazy audio/visuals.  
All examples below use `xy` as the instance prefix.

[Initialize XYscope](#initialize-xyscope)

[Waves](#waves)
  * [clearWaves()](#clearwaves())
  * [buildWaves()](#buildwaves())
  * [setWaves()](#setwaves())
  * [smooth()](#smooth())
  * [noSmooth()](#nosmooth())
  * [limitPath()](#limitpath())

[Primitive Shapes](#primitive-shapes)
  * [point()](#point())
  * [line()](#line())
  * [square()](#square())
  * [rect()](#rect())
  * [ellipseDetail()](#ellipsedetail())
  * [circle()](#circle())
  * [ellipse()](#ellipse())
  * [complex shape](#complex-shape)
  * [lissajous()](#lissajous())
  * [box()](#box())
  * [sphere()](#sphere())
  * [ellipsoid()](#ellipsoid())
  * [torus()](#torus())

[Text](#text)
  * [loadFont()](#loadfont())
  * [text()](#text())
  * [textPaths()](#textpaths())
  * [textSize()](#textsize())
  * [textLeading()](#textleading())
  * [textAlign()](#textalign())
  * [textWidth()](#textwidth())

[Modulation](#modulation)
  * [freq()](#freq())
  * [amp()](#amp())
  * [highpass()](#highpass())
  * [lowpass()](#lowpass())

[Sequencer](#sequencer)
  * [Settings](#settings)
  * [Patterns](#patterns)
  * [Events](#events)

[Vectrex](#vectrex)

[Laser](#laser)

[Rendering](#rendering)
  * [Virtual Scope](#virtual-scope)
  * [Debug views](#debug-views)

[Camera](#camera)
  * [camSetup()](#camSetup())
  * [camDisplay()](#camDisplay())
  
---

### Initialize XYscope
```js
xy = new XYscope(this) // 'this' passes current instance of p5.js
xy.canvas() // optionally resize p5.js + XXY to full height, centered

xy2 = new XYscope(this, xy.outXY) //optional 2nd instance for additive-synth
```
---
### Waves
#### clearWaves()
Clears the wavetable of previous shapes, place near top of `draw()`.

```js
xy.clearWaves() // clear previous wavetables
```

#### buildWaves()
Builds X and Y wavetables from buffer of added shapes. Place after you've drawn all shapes.

```js
xy.buildWaves() // send shapes to wavetables/audio
```

#### setWaves()
If you prefer, simply provide your own X and Y arrays of values between -1.0 to 1.0 for custom wavetables.

```js
tempX = new Array(128) // blank array
tempY = new Array(128) // blank array
for(let i = 0; i < tempX.length; i++) {
	tempX[i] = noise(frameCount * .001 + i * .02) * 2 - 1 // pack it
	tempY[i] = noise(frameCount * .0013 + i * .022) * 2 - 1 // pack it
}

xy.setWaves(tempX, tempY) // set XY wavetables to custom x, y arrays
```

#### smooth()
Interpolates (adds) points between each coordinate for smooth lines (on by default).

```js
xy.smooth() // smooth lines, default is 1
xy.smooth(newGap) // set custom gap size between points
```

#### noSmooth()
Only draw exact coordinates of shapes, thus a `rect()` is shown as 4 points.

```js
xy.noSmooth() // only draw coordinate points
```

#### limitPath()
Prevent coordinates outside of canvas from being drawn (creates a wall/box of lines if not activated). Useful if scaling drawing/model beyond the size of canvas.

```js
xy.limitPath() // uses width, height of canvas as border to limit path
xy.limitPath(newLimit) // set inner border (px) amount
xy.limitPath(-1) // disables limitPath
```

---
### Primitive Shapes
Most primitives from p5.js have been ported, so you simply need to add `xy.` in front of them! They can also be used without parameters, for quickly testing.  

#### point()
Draw a single point.

```js
xy.point() // defaults to random width/height
xy.point(x, y)
xy.point(x, y, z)
```

#### line()
Draw a line between two coordinates, in 2D or 3D space.

```js
xy.line() // defaults to random width/height
xy.line(x1, y1, x2, y2)
xy.line(x1, y1, z1, x2, y2, z2)
```
#### square()
Draw a rectangle with same width and height.

```js
rectMode(CENTER) // default CORNER, use CENTER to draw center out

xy.square() // defaults to (0, 0, 100)
xy.square(x, y, w)
```
#### rect()
Draw a rectangle with custom width and height.

```js
rectMode(CENTER) // default CORNER, use CENTER to draw center out

xy.rect() // defaults to (0, 0, 100)
xy.rect(x, y, w) // uses w for h
xy.rect(x, y, w, h)
```

#### ellipseDetail()
Global value for number of facades used for `circle()` and `ellipse()`.

```js
xy.ellipseDetail() // get current facets of ellipse
xy.ellipseDetail(newVal) // set new count of facets, default 50
```

#### circle()
Draw a circle with same width and height.

```js
xy.circle() // defaults to (0, 0, 100)
xy.circle(x, y, w)
xy.circle(x, y, w, numPoints) // numPoints overrides ellipseDetail
```

#### ellipse()
Draw a circle with custom width and height.

```js
xy.ellipse() // defaults to (0, 0, 100)
xy.ellipse(x, y, w) // uses w for h
xy.ellipse(x, y, w, h)
xy.ellipse(x, y, w, h, numPoints) // numPoints overrides ellipseDetail
```

#### triangle()
Draw a triangle with custom coordinates.

```js
xy.triangle() // defaults to 100px, positioned at 0,0
xy.triangle(x1, y1, x2, y2, x3, y3) // set 3-coordinates
```

#### complex shape
Draw a complex form using multiple vertices.
 
```js
xy.beginShape()

xy.vertex() // defaults to random width/height
xy.vertex(x, y)
xy.vertex(x, y, z) // 3D coordinate space
// ...

xy.endShape()
xy.endShape(CLOSE) // closes form
```

#### lissajous()
Draw a [lissajous curve](https://en.wikipedia.org/wiki/Lissajous_curve), which depends on a certain ratio between A and B.

```js
xy.lissajous() // defaults to infinity symbol
xy.lissajous(x, y, radius, ratioA, ratioB, phase) // uses ellipseDetail
xy.lissajous(x, y, radius, ratioA, ratioB, phase, numPoints) override ellipseDetail
```

#### box()
Draw a 3D cube, optionally set the width, height, depth.

```js
xy.box() // defaults to (100)
xy.box(w) // uses w for h and d
xy.box(w, h) // uses w for d
xy.box(w, h, d)
```

#### sphere()
Draw a sphere, optionally set detailX/Y (mesh vertices) and toggle the rendering of latitude and longitude lines as a object passed in any parameter from 2 onward ie. `{lat:false, long:true}`.

```js
xy.sphere()
xy.sphere(radius)
xy.sphere(radius, opts) // {lat:0, long:1}
xy.sphere(radius, detailX) // default 24
xy.sphere(radius, detailX, detailY) // default 24, 16
xy.sphere(radius, detailX, detailY, opts) // {lat:0, long:1}
```
#### ellipsoid()
Draw an ellipsoid with optional custom radius in X/Y/Z dimensions, and toggle the rendering of latitude and longitude lines as a object passed in any parameter from 4 onward ie. `{lat:false, long:true}`.

```js
xy.ellipsoid()
xy.ellipsoid(rx, ry, rz)
xy.ellipsoid(rx, ry, rz, opts) // {lat:0, long:1}
xy.ellipsoid(rx, ry, rz, detailX) // default 24
xy.ellipsoid(rx, ry, rz, detailX, detailY) // default 24, 16
xy.ellipsoid(rx, ry, rz, detailX, detailY, opts) // toggle {lat:0, long:1}
```

#### torus()
Draw a tube shape with optional custom radius, tubeRadius, detail X/Y and toggle the rendering of latitude and longitude lines as a object passed in any parameter from 3 onward ie. `{lat:false, long:true}`.

```js
xy.torus()
xy.torus(radius, tubeRadius)
xy.torus(radius, tubeRadius, opts) // {lat:0, long:1}
xy.torus(radius, tubeRadius, detailX) // default 24
xy.torus(radius, tubeRadius, detailX, detailY) // default 24, 16
xy.torus(radius, tubeRadius, detailX, detailY, opts) // {lat:0, long:1}
```

---
### Text
XYscope.js has built in text rendering for [Hershey fonts](https://en.wikipedia.org/wiki/Hershey_fonts).

#### loadFont()
`hersey_futural` is embedded, you can load others from the [hershey fonts set](https://github.com/kamalmostafa/hershey-fonts).

```js
xy.loadFont("path_to_font")
xy.loadFont('https://cdn.jsdelivr.net/gh/kamalmostafa/hershey-fonts/hershey-fonts/cursive.jhf')
```

#### text()
Draw text.

```js
xy.text() // defaults to ("XYscope", 0, 0)
xy.text("string", x, y)
xy.text("hello\nworld", x, y) // use '\n' for multi-line text

xy.text(`hello
world`, x, y) // or use `` (literals) for multi-line text
```

#### textPaths()
Get coordinates of Hershey text for manipulating type!  
Returns an 2D array of coordinates: `chars[ coords[] ]`

```js
let textPath = xy.textPaths("XYscope", x, y)

for(let char of textPath) {
	xy.beginShape()
	for(let c of char) {
		xy.vertex(c.x, c.y)
	}
	xy.endShape()
}
```

#### textSize()
Get or set the text size.

```js
xy.textSize() // get current textSize
xy.textSize(newSize) // set new textSize
```

#### textLeading()
Get or set the text leading.

```js
xy.textLeading() // get current textLeading
xy.textLeading(newSize) // set new textLeading
```

#### textAlign()
Set the text alignment on horizontal and optionally vertical axis.

```js
xy.textAlign(hAlign) // Horz: LEFT (default) / CENTER / RIGHT
xy.textAlign(hAlign, vAlign) // Vert options: TOP / CENTER / BOTTOM
```

#### textWidth()
Get the width in pixels of a text string for positioning or drawing around.

```js
xy.textWidth("string") // get width (px) of text
```

---

### Modulation
#### freq()
Frequency of oscillators, used to adjust the speed of the beam, adjust it's musical or sonic qualities and very important for additive-synthesis.

```js
// get
xy.freq() // returns object (.x, .y) of freqs
xy.freq().x   // returns frequency of x oscillator 

// set
xy.freq(freqXY)  // set both X/Y levels, default is 50.0 
xy.freq(freqX, freqY) // set x, y to separate frequencies  
```

#### amp()
Amplitude of oscillators, used to adjust how loud a given oscillator is. Can be very quite, or amplified beyond normal range for distortion.

```js
// get
xy.amp()   // returns object (.x, .y) of amps
xy.amp().x // returns amplitude of x oscillator

// set
xy.amp(ampXY) // set both X/Y levels, default is 1.0 
xy.amp(ampX, ampY) // set x, y to separate amplitudes 
```

#### highpass()
A very experimental [high-pass filter](https://en.wikipedia.org/wiki/High-pass_filter) has been implemented.

```js
xy.highpass(freq) // set cutoff for high-pass filter 
```

#### lowpass()
A very experimental [low-pass filter](https://en.wikipedia.org/wiki/Low-pass_filter) has been implemented.

```js
xy.lowpass(freq) // set cutoff for low-pass filter 
```

---
### Sequencer
There's a built-in step sequencer for XYscope.js! It allows you to algorithmicly code patterns that are then played back, setting the frequency of your XY oscillators to those notes aka let's make music! This sequencer will soon be released separately as a library, since it can be used to trigger anything – but was designed for XYscope performances.

The sequencer is already activated on each XYscope instance, and is given the variable scope of `seq`, ie use `xy.seq` when changing settings. Be sure to disable `xy.freq()`, as the two would compete for setting frequency.

#### Settings
We can adjust a few settings for our sequences

```js
xy.seq.bpm() // get bpm
xy.seq.bpm(120) // set bpm

xy.seq.octave() // get default octave for notes, default 3
xy.seq.octave(2) // set custom default octave, ie 1 - 7

xy.seq.duration() // set step/rest duration length, default 8 as in 1/8
xy.seq.duration(dur) // set step/rest duration length, ie 1 – 64

xy.seq.start() // start sequencer
// xy.seq.stop() // stop sequencer

xy.seq.loop = true // default on, set to false for single sequence

xy.mute = false // toggle to silence  
```

#### Patterns
There's a special notation for adjusting duration, octave, repeats, alternates that is inspired by [Strudel](https://strudel.cc/functions/intro/):

##### Notes
- `xy.seq.pattern('c')`// plays C in default octave (3)
- `xy.seq.pattern('C')`// plays C in default octave (3)
- `xy.seq.pattern('c d e f g a b c4')`// C Major scale

##### Rests
- `xy.seq.pattern('a')`// repeated note 
- `xy.seq.pattern('a ')`// repeated note, rest
- `xy.seq.pattern('a  ')`// repeated note, double rest 
- `xy.seq.pattern('a--')`// repeated note, double rest  (can use ' ' or '-')
- `xy.seq.pattern('a 32r d 16r f 4r')`// use `#r` for custom rest length

##### Notes + Rests
- `xy.seq.pattern('a c')`// sequence of notes, no rests
- `xy.seq.pattern('a c ')`// sequence of notes, rest only at end
- `xy.seq.pattern('a  c ')`// sequence of notes, rest after each
- `xy.seq.pattern('a- c-')`// rest after each, more clear

##### Sharps + Flats
- `xy.seq.pattern('a# cb')`// use `#` for sharp, `b` for flat

##### Octave + Duration
- `xy.seq.pattern('a2 ')`// set custom octave with number after note value
- `xy.seq.pattern('4a ')`// set custom duration with first value, here 1/4
- `xy.seq.pattern('2a3 ')`// set custom octave and duration
- `xy.seq.pattern('2a3*3 ')`// with `*3` makes a triplet, `*1` is default

##### Alternates
- `xy.seq.pattern('a c:d:e:f')`// use `:` for alternates to walk thru
- `xy.seq.pattern('a c;d;e;f')`// use `;` for alternates randomly selected
- `xy.seq.pattern('a:a2 d;8d4*4')`// 1st has `:` walk, 2nd has `;` random
- `xy.seq.pattern('A;C;D;E;G')`// random walk A minor pentatonic scale
- `xy.seq.pattern('a:a2- f:f:e:e:d:d:d:d*3-')`// go wild!

##### Melodies
A small collection of tunes and their patterns.

```js
// close encounters of 3rd kind
xy.seq.pattern('4A3 4B3 4G3-- 4G2-- 2D3 2r 4A2 4B2 4G2-- 4G1-- 2D2 2r')

// more soon...
```

#### Events
You can also trigger events whenever a new note is played or ended, ie draw a shape or change values on each note.

```js
xy.seq.onStep((step) => {
	// do something on each step
	circle(random(width), random(height), 50)
})

xy.seq.onStepEnded((step) => {
	// do something when step finished
})

```

---
### Vectrex

_pending..._

---
### Laser

_pending..._

---
### Rendering
#### Virtual Scope
A virtual scope is embedded via [XXY](https://dood.al/oscilloscope/) by Neil Thapen! It offers a very impressive synthesis of glow and tracing artifacts similar to a real oscilloscope, but of course is match for the real thing. Nevertheless, there's plenty of options to adjust when rendering on screen.


```js
xy.drawXY() // launch fullscreen with GUI
xy.drawXY({gui:0}) // hide GUI

// default options
var xyOptions = {			// shorthand
	toggle:1,
	gui:1,
	grid:0,
	fullscreen: 1, 			// 'fs'
	opacity:0.75, 			// 'o'
	thickness:0.01, 		// 't'
	hue:120, 				// 'h'
	gain:0.1, 				// 'g'
	intensity:-.0, 			// 'i'
	persistence:-1 			// 'p'
}
xy.drawXY(xyOptions) // set any number of options above

xy.drawXY({gui:0, fs:1, o:.75, t:.01, h:120, g:.1, i:.0, p:-1}) // shorthand

```
For further experiments, the XXY canvas is available as `xy.scope`.

#### Debug views
Beyond the virtual scope, there's plenty of interesting debug views to check out, from monitoring the waveform (wavetable) used for the oscillators, to the wave itself with time flowing through it. 

```js
xy.drawWaveform() // draw as oscillator waveform frozen
xy.drawWaveform(strokeWeight) // draw waveform frozen and set strokeWeight

xy.drawWave() // draw oscillator wave with time flowing 
xy.drawWave(strokeWeight, color) // oscillator wave, set strokeWeight + color 

xy.drawAll() // displays both above plus drawXY()


xy.drawShapes() // primatives also render in p5.js, not just as audio
xy.drawShapes(toggle) // default true (1), set to false (0) to hide
```

### Camera
Since XYscope.js is intended for live-coding analog vector displays, it's important to easily view that real screen behind your code. For this, we can render an external webcam, which will re-scan your display. Normally with p5.js you'd need a small chunk of code to load and adjust the camera in your sketch, but this takes care of that all in the backend! While it's intended for capturing your oscilloscope or similar monitor, it's also just a fun and weird way to play with the camera!

#### cam()
This should be added within the `draw()`, as it acts as both a setup and render of the camera, along with options to be changed on the fly. This can be instantly added as a short code, or see options for customizing further.

```js
xy.cam() // BAM, you have a CAM!

// default options
var camOptions = {			// shorthand
	orientation: 'height', 	// 'o', fit to 'height' or 'width'
	// scale: 1, 			// 's', set custom scale (overrides orientation)
	horizontal: 1, 			// 'h', 0 - 1, for adjusting aspect ratio issues
	vertical: 1, 			// 'v', 0 - 1, for adjusting aspect ratio issues
	rotation:0, 			// 'r', rotate based on degrees
	toggle:1,				// 't', toggle cam display
}
xy.cam(camOptions)

xy.cam({o:1, h:1, v:1, r:0}) // shorthand
xy.cam({s:3, h:1, v:1, r:0}) // shorthand

```
For further experiments, the camera image is available as `xy.capture`.

## Extras 
### Contributing
Found a bug, missing feature, and/or created a project with XYscope.js?  
Let me know! Create an [issue on GitHub](https://github.com/ffd8/xyscopejs/issues).

### License

This project is licensed under the GNU GPLv3 License - see [LICENSE.md](https://github.com/ffd8/xyscopejs/blob/main/license.txt) for details.

### Shoutouts

* [Stefanie Bräuer](https://stefaniebraeuer.ch/), feeding the obsession with crucial theory + context.
* [Just Van Rossum](http://dailydrawbot.tumblr.com), the enlightening conversation on my X-Y attempts baaack in 2017.
* [Neil Thapen](https://dood.al/oscilloscope/), that amazing virtual oscilloscope rendering.