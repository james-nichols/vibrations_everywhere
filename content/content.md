---
languageName: "English"
title: "Vibrations Everywhere - The Maths of Waves"
description: "Fourier transforms are a tool used in a whole bunch of different things. This is a explanation of what a Fourier transform does, and some different ways it can be useful."
outFileName: "index.html"
---

Many things in our world can be thought of as a bunch of waves put together. We're going to have a look at sound and images and how to break them up in to waves of different frequencies.

We're going to leave the mathematics and equations out of it for now. We will look at that more in the second half.

# Sound is waves of pressure

Waves of pressure travel through the air. Everything you hear is a pressure wave that reached your ear. Things that vibrate, like loudspeakers, create pressure waves.
<div class="img-component-container">
<img src="img/acoustics-piston-wave-animation.gif" width="500"/>
</div>
The pressure waves radiate outwards from a sound source, for example this bell.
<div class="img-component-container">
<img src="img/acoustics-sound-propagation-2d.png" width="500"/>
</div>
In today's session we are going to think about sound as the graph of the pressure value over time. (i.e. we think of the pressure as a mathematical _function_ against time)
<div class="img-component-container">
<img src="img/acoustics-time-domain-waveform.png" width="500"/>
</div>
Lets listen to a simple example of a sound wave given by the function animated below. It's a squiggly line that repeats forever (at least notionally). We say that this function is _periodic_.
<canvas id="combo-sine-wave" class="sketch" width=500 height=300></canvas>
<button id="together-button" class="button">Play Full Wave</button>

# Breaking up sound in to fundamental frequencies

The squiggly pattern above here can be split up into two fundamental waves of different frequency. When we add up the two we get back the original wave.

<canvas id="combo-sine-wave-split" class="sketch" width=500 height=500></canvas>

We can listen to each of those freqencies by themselves. You can hear how the original sound is indeed a mix of these two frequencies.

<button id="split-button-1" class="button">Play High Frequency</button>

<button id="split-button-2" class="button">Play Low Frequency</button>

### What are these _"fundamental waves"?_ 

They are _sinusoids_, as in the sine and cosine functions that you might remember from trigonometry.
<div class="img-component-container">
<img src="img/sinusoidal.png" width="400"/>
</div>
Sinusoids are considered the most basic wave as many physical systems oscillate in a sinusoidal manner, e.g. 
 - a spring with a weight attached to it
 - a pendulum

There is also mathematically deep theory justifying the choice of sinusoids.

# The Fourier transform

The _Fourier transform_ is the method to take any signal or function and decompose it in to the appropriate amount of sine and cosine waves of every frequency.

It's a bit like guessing the recipe of a fruit juice or _smoothie_ - how much orange juice, mango juice, and ginger went in to this drink? 
<div class="img-component-container">
<img src="img/vicuschka_shutterstock.webp" width="500"/>
</div>

The Fourier transform is a way for us to take the combined wave, and get each of the composite sine and cosine waves back out. 

Our ears naturally do some sort of Fourier transform: we don’t hear that squiggly line, but we hear the different frequencies of the sine waves that make up the sound.

Being able to split them up on a computer can give us an understanding of what a person actually hears. We can understand how high or low a sound is, or figure out what note it is.

# Another example

We can also use this process on waves that don't look like they're made of sine waves.

Let's take a look at this one. It’s called a square wave.

<canvas id="square-wave" class="sketch" width=500 height=300></canvas>

It might not look like it, but it also can be split up into sine waves.

<canvas id="square-wave-split" class="sketch" width=500 height=500></canvas>

We need a lot of them this time – technically an infinite amount to perfectly represent it. As we add up more and more sine waves the pattern gets closer and closer to the square wave we started with.

<canvas id="square-wave-build-up" class="sketch" width=500 height=500></canvas>
<input id="square-wave-build-up-slider" type="range" min="0" max="1" value="0" step="any" >

<button id="square-wave-button" class="button">Play Wave</button>

*Drag the slider above to play with how many sine waves there are.*

Some intersting things to note:

 - The first few sine waves are the ones that make the biggest difference. 
 - With the slider halfway, we have the general shape of the wave, but it's all wiggly. We need the rest of the small ones to make the wigglyness flatten out.
 - When you listen to the wave, you'll hear the sound get lower, because we're removing the higher frequencies.

This process works like that for any repeating line. Give it a go, try drawing your own!

<div class="multi-container">
<div class="sketch" >
    <canvas id="wave-draw" class="sketch-child" width=500 height=300></canvas>
    <p id="wave-draw-instruction" class="instruction wave-instruction">Draw here!</p>
</div>
<canvas id="wave-draw-split" class="sketch" width=500 height=500></canvas>
</div>
<input id="wave-draw-slider" type="range" min="0" max="1" value="1" step="any">
<button id="wave-draw-button" class="button">Play Wave</button>

*Move the slider to see how as we add more sine waves, it gets closer and closer to your drawing*

_By using a Fourier transform, we can get the important parts of a sound, and only store those to end up with something that's pretty close to the original sound._ 

# Sound on a computer

Normally on a computer we store a sound as a series of numbers, each representing the signal intensity at a regular time point.

<canvas id="wave-samples" class="sketch" width=500 height=500></canvas>

However, we can also _store the Fourier transform_ of a sound and perfectly reconstruct the sound from it. _A bit like storing the recipe for a smoothie and being able to make it any time._

What if we can compress the sound by ignoring the smaller frequencies? Our end result won't be the same, but it'll sound pretty similar.

<canvas id="wave-frequencies" class="sketch" width=500 height=500></canvas>

This is essentially what MP3s do, except they're more clever about which frequencies they keep and which ones they throw away.

# Images and waves

Did you know Fourier transforms can also be used on images? We use it all the time, because that's how JPEGs work! 

Now we're dealing with images, we need so we need 2-dimensional sinusoidal waves. 
Instead of a wave that's a line, we now have images with black and white sections.

No matter what image we have, we must be able add up a bunch of these sine waves to get back to our original image.

_Let's start with black-and-white images for now._

### We need some horizontal wave images

<img id="img-y-component" src="img/components-4-0.png" class="sketch sketch-small">

### Along with some vertical wave images.

<img id="img-x-component" src="img/components-0-4.png" class="sketch sketch-small">

By themselves, just horizontal and vertical images aren't enough to represent the types of images we get...

### We also need some extra ones that you get by multiplying the two together.

<div class="multi-container">
<img id="img-mult-x-component" src="img/components-0-4.png" class="sketch sketch-mult">
<div class="maths">×</div>
<img id="img-mult-y-component" src="img/components-4-0.png" class="sketch sketch-mult">
<div class="maths">=</div>
<img id="img-x-y-component" src="img/components-4-4.png" class="sketch sketch-mult">
</div>

For an 8x8 image, here are all the images we need.

<div class="img-component-container">
    <img src="img/components-0-0.png" class="img-component">
    <img src="img/components-0-1.png" class="img-component">
    <img src="img/components-0-2.png" class="img-component">
    <img src="img/components-0-3.png" class="img-component">
    <img src="img/components-0-4.png" class="img-component">
    <img src="img/components-0-5.png" class="img-component">
    <img src="img/components-0-6.png" class="img-component">
    <img src="img/components-0-7.png" class="img-component">
    <img src="img/components-1-0.png" class="img-component">
    <img src="img/components-1-1.png" class="img-component">
    <img src="img/components-1-2.png" class="img-component">
    <img src="img/components-1-3.png" class="img-component">
    <img src="img/components-1-4.png" class="img-component">
    <img src="img/components-1-5.png" class="img-component">
    <img src="img/components-1-6.png" class="img-component">
    <img src="img/components-1-7.png" class="img-component">
    <img src="img/components-2-0.png" class="img-component">
    <img src="img/components-2-1.png" class="img-component">
    <img src="img/components-2-2.png" class="img-component">
    <img src="img/components-2-3.png" class="img-component">
    <img src="img/components-2-4.png" class="img-component">
    <img src="img/components-2-5.png" class="img-component">
    <img src="img/components-2-6.png" class="img-component">
    <img src="img/components-2-7.png" class="img-component">
    <img src="img/components-3-0.png" class="img-component">
    <img src="img/components-3-1.png" class="img-component">
    <img src="img/components-3-2.png" class="img-component">
    <img src="img/components-3-3.png" class="img-component">
    <img src="img/components-3-4.png" class="img-component">
    <img src="img/components-3-5.png" class="img-component">
    <img src="img/components-3-6.png" class="img-component">
    <img src="img/components-3-7.png" class="img-component">
    <img src="img/components-4-0.png" class="img-component">
    <img src="img/components-4-1.png" class="img-component">
    <img src="img/components-4-2.png" class="img-component">
    <img src="img/components-4-3.png" class="img-component">
    <img src="img/components-4-4.png" class="img-component">
    <img src="img/components-4-5.png" class="img-component">
    <img src="img/components-4-6.png" class="img-component">
    <img src="img/components-4-7.png" class="img-component">
    <img src="img/components-5-0.png" class="img-component">
    <img src="img/components-5-1.png" class="img-component">
    <img src="img/components-5-2.png" class="img-component">
    <img src="img/components-5-3.png" class="img-component">
    <img src="img/components-5-4.png" class="img-component">
    <img src="img/components-5-5.png" class="img-component">
    <img src="img/components-5-6.png" class="img-component">
    <img src="img/components-5-7.png" class="img-component">
    <img src="img/components-6-0.png" class="img-component">
    <img src="img/components-6-1.png" class="img-component">
    <img src="img/components-6-2.png" class="img-component">
    <img src="img/components-6-3.png" class="img-component">
    <img src="img/components-6-4.png" class="img-component">
    <img src="img/components-6-5.png" class="img-component">
    <img src="img/components-6-6.png" class="img-component">
    <img src="img/components-6-7.png" class="img-component">
    <img src="img/components-7-0.png" class="img-component">
    <img src="img/components-7-1.png" class="img-component">
    <img src="img/components-7-2.png" class="img-component">
    <img src="img/components-7-3.png" class="img-component">
    <img src="img/components-7-4.png" class="img-component">
    <img src="img/components-7-5.png" class="img-component">
    <img src="img/components-7-6.png" class="img-component">
    <img src="img/components-7-7.png" class="img-component">
</div>

If we take these images, adjust their contrast to the right amount, and then add them up we can create any image.

Let's start with this letter 'A'. It's pretty small, but we need it to be small otherwise we'll end up with too many other images.

<img src="img/a.png" class="sketch sketch-letter">

As we add more and more of these images, we end up with something that becomes closer and closer to the actual image. But I think you'll see the pattern here, as we get a reasonable approximation with just a few of them.

<div class="hidden-preload">
    <img src="img/img-buildup-0-0.png">
    <img src="img/img-buildup-0-1.png">
    <img src="img/img-buildup-0-2.png">
    <img src="img/img-buildup-0-3.png">
    <img src="img/img-buildup-0-4.png">
    <img src="img/img-buildup-0-5.png">
    <img src="img/img-buildup-0-6.png">
    <img src="img/img-buildup-0-7.png">
    <img src="img/img-buildup-1-0.png">
    <img src="img/img-buildup-1-1.png">
    <img src="img/img-buildup-1-2.png">
    <img src="img/img-buildup-1-3.png">
    <img src="img/img-buildup-1-4.png">
    <img src="img/img-buildup-1-5.png">
    <img src="img/img-buildup-1-6.png">
    <img src="img/img-buildup-1-7.png">
    <img src="img/img-buildup-2-0.png">
    <img src="img/img-buildup-2-1.png">
    <img src="img/img-buildup-2-2.png">
    <img src="img/img-buildup-2-3.png">
    <img src="img/img-buildup-2-4.png">
    <img src="img/img-buildup-2-5.png">
    <img src="img/img-buildup-2-6.png">
    <img src="img/img-buildup-2-7.png">
    <img src="img/img-buildup-3-0.png">
    <img src="img/img-buildup-3-1.png">
    <img src="img/img-buildup-3-2.png">
    <img src="img/img-buildup-3-3.png">
    <img src="img/img-buildup-3-4.png">
    <img src="img/img-buildup-3-5.png">
    <img src="img/img-buildup-3-6.png">
    <img src="img/img-buildup-3-7.png">
    <img src="img/img-buildup-4-0.png">
    <img src="img/img-buildup-4-1.png">
    <img src="img/img-buildup-4-2.png">
    <img src="img/img-buildup-4-3.png">
    <img src="img/img-buildup-4-4.png">
    <img src="img/img-buildup-4-5.png">
    <img src="img/img-buildup-4-6.png">
    <img src="img/img-buildup-4-7.png">
    <img src="img/img-buildup-5-0.png">
    <img src="img/img-buildup-5-1.png">
    <img src="img/img-buildup-5-2.png">
    <img src="img/img-buildup-5-3.png">
    <img src="img/img-buildup-5-4.png">
    <img src="img/img-buildup-5-5.png">
    <img src="img/img-buildup-5-6.png">
    <img src="img/img-buildup-5-7.png">
    <img src="img/img-buildup-6-0.png">
    <img src="img/img-buildup-6-1.png">
    <img src="img/img-buildup-6-2.png">
    <img src="img/img-buildup-6-3.png">
    <img src="img/img-buildup-6-4.png">
    <img src="img/img-buildup-6-5.png">
    <img src="img/img-buildup-6-6.png">
    <img src="img/img-buildup-6-7.png">
    <img src="img/img-buildup-7-0.png">
    <img src="img/img-buildup-7-1.png">
    <img src="img/img-buildup-7-2.png">
    <img src="img/img-buildup-7-3.png">
    <img src="img/img-buildup-7-4.png">
    <img src="img/img-buildup-7-5.png">
    <img src="img/img-buildup-7-6.png">
    <img src="img/img-buildup-7-7.png">
</div>
<div id="letter-buildup" class="multi-container">
<img id="letter-buildup-letter" src="img/img-buildup-0-0.png" class="sketch sketch-letter">
<div id="letter-buildup-components" class="img-component-container">
    <img src="img/img-components-0-0.png" class="img-component">
    <img src="img/img-components-0-1.png" class="img-component">
    <img src="img/img-components-0-2.png" class="img-component">
    <img src="img/img-components-0-3.png" class="img-component">
    <img src="img/img-components-0-4.png" class="img-component">
    <img src="img/img-components-0-5.png" class="img-component">
    <img src="img/img-components-0-6.png" class="img-component">
    <img src="img/img-components-0-7.png" class="img-component">
    <img src="img/img-components-1-0.png" class="img-component">
    <img src="img/img-components-1-1.png" class="img-component">
    <img src="img/img-components-1-2.png" class="img-component">
    <img src="img/img-components-1-3.png" class="img-component">
    <img src="img/img-components-1-4.png" class="img-component">
    <img src="img/img-components-1-5.png" class="img-component">
    <img src="img/img-components-1-6.png" class="img-component">
    <img src="img/img-components-1-7.png" class="img-component">
    <img src="img/img-components-2-0.png" class="img-component">
    <img src="img/img-components-2-1.png" class="img-component">
    <img src="img/img-components-2-2.png" class="img-component">
    <img src="img/img-components-2-3.png" class="img-component">
    <img src="img/img-components-2-4.png" class="img-component">
    <img src="img/img-components-2-5.png" class="img-component">
    <img src="img/img-components-2-6.png" class="img-component">
    <img src="img/img-components-2-7.png" class="img-component">
    <img src="img/img-components-3-0.png" class="img-component">
    <img src="img/img-components-3-1.png" class="img-component">
    <img src="img/img-components-3-2.png" class="img-component">
    <img src="img/img-components-3-3.png" class="img-component">
    <img src="img/img-components-3-4.png" class="img-component">
    <img src="img/img-components-3-5.png" class="img-component">
    <img src="img/img-components-3-6.png" class="img-component">
    <img src="img/img-components-3-7.png" class="img-component">
    <img src="img/img-components-4-0.png" class="img-component">
    <img src="img/img-components-4-1.png" class="img-component">
    <img src="img/img-components-4-2.png" class="img-component">
    <img src="img/img-components-4-3.png" class="img-component">
    <img src="img/img-components-4-4.png" class="img-component">
    <img src="img/img-components-4-5.png" class="img-component">
    <img src="img/img-components-4-6.png" class="img-component">
    <img src="img/img-components-4-7.png" class="img-component">
    <img src="img/img-components-5-0.png" class="img-component">
    <img src="img/img-components-5-1.png" class="img-component">
    <img src="img/img-components-5-2.png" class="img-component">
    <img src="img/img-components-5-3.png" class="img-component">
    <img src="img/img-components-5-4.png" class="img-component">
    <img src="img/img-components-5-5.png" class="img-component">
    <img src="img/img-components-5-6.png" class="img-component">
    <img src="img/img-components-5-7.png" class="img-component">
    <img src="img/img-components-6-0.png" class="img-component">
    <img src="img/img-components-6-1.png" class="img-component">
    <img src="img/img-components-6-2.png" class="img-component">
    <img src="img/img-components-6-3.png" class="img-component">
    <img src="img/img-components-6-4.png" class="img-component">
    <img src="img/img-components-6-5.png" class="img-component">
    <img src="img/img-components-6-6.png" class="img-component">
    <img src="img/img-components-6-7.png" class="img-component">
    <img src="img/img-components-7-0.png" class="img-component">
    <img src="img/img-components-7-1.png" class="img-component">
    <img src="img/img-components-7-2.png" class="img-component">
    <img src="img/img-components-7-3.png" class="img-component">
    <img src="img/img-components-7-4.png" class="img-component">
    <img src="img/img-components-7-5.png" class="img-component">
    <img src="img/img-components-7-6.png" class="img-component">
    <img src="img/img-components-7-7.png" class="img-component">
</div>
</div>

# JPEG compression

In JPEG the image gets broken up into 8x8 chunks, and we take the Fourier transform of each chunk. The number of frequencies that we use for each chunk determines the quality of the JPEG.

Here's a real JPEG image, zoomed in so we can see the details. When we play with the quality levels we can see this process happen.

<div id="jpeg-example" class="sketch">
    <img src="img/cat.png" class="sketch-child clear-pixels">
</div>

## Conclusion

Recap:

- Fourier transforms are things that let us take something and split it up into its frequencies.
- The frequencies tell us about some fundamental properties of the data we have
- And can compress data by only storing the important frequencies

This is just scratching the surface. The Fourier transform is an extremely powerful tool, and is used in a lot of fields including _circuit design, mobile phone signals, magnetic resonance imaging (MRI), and quantum physics_.

## Questions for the curious

I skipped most of the math stuff here, but if you're interested in the underlying principles of how it works, here are some questions you can use to guide your research:

- How do you mathematically represent a Fourier transform?
- What's the difference between a continuous time Fourier transform and a discrete time Fourier transform?
- How do you computationally do a Fourier transform?
- How do you do a Fourier transform of a whole song? (Rather than just a single note.)

## Further 'reading'

To learn more, some really good resources you can check out are:

[An Interactive Guide To The Fourier Transform](https://betterexplained.com/articles/an-interactive-guide-to-the-fourier-transform/)
A great article that digs more into the mathematics of what happens.

[But what is the Fourier Transform? A visual introduction.](https://www.youtube.com/watch?v=spUNpyF58BY)
A great Youtube video by 3Blue1Brown, also explaining the maths of Fourier transforms from an audio perspective.

[Fourier transform (Wikipedia)](https://en.wikipedia.org/wiki/Fourier_transform)
And of course, the Wikipedia article is pretty good too.

