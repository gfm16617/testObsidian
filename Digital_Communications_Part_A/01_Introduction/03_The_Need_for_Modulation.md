---
comments: |-
  improve the antenna section using the Digikey article that simplifies the basics of antennas 
  https://www.digikey.com/en/blog/beyond-wires-antennas-evolve-and-adapt
  https://www.digikey.com/en/blog/the-reasons-for-50-ohm-and-75-ohm-transmission-lines
  https://learn.sparkfun.com/tutorials/rfm69hcw-hookup-guide/the-antenna
---
# The Need for Modulation
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
maxLevel: 0 # Include headings up to the speficied level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---
## Fundamental Forces

There are four fundamental forces at work in the universe: the strong force, the weak force, the electromagnetic force, and the gravitational force.

![[4_fundamental_forces.png]]

They work over different ranges and different strengths.

> [!note] 
> Gravity < Weak Force < Electromagnetic Force < Strong Force 

The electromagnetic force is responsible for generating visible light, as well as radiation in other wavebands not detectable by human eye. As electrons and protons fly around bumping into each other in a light source, the electromagnetic force produces photons of all wavelengths (waves with certain lengths) across the electromagnetic spectrum.

![[electromagnetic_spectrum.png]]

Slow, randomly moving charged particles create radio, infrared, optical and ultraviolet photons with wavelengths, respectively, from meters to microns to thousands of nanometers to hundreds of nanometers. Fast moving particles may create X-rays or Gamma-rays.

## Wavelength

The period (seconds) of a waveform is the time between two adjacent peaks of a waveform and it is considered one oscillation of the waveform.  If we count how many oscillations happen per second we get frequency (Hz).

$$f(Hz)=\frac{1}{T(s)}$$

![[frequency_vs_period.png|360]]

Wavelength (meters) is the physical distance between those two adjacent peaks of the waveform.

![[frequency_vs_wavelength 1.png]]

Notice how the two graphs have frequency in common but the first graph shows the time (seconds) that the wave takes to propagate versus the second graph that shows how far (meters) the wave propagated.

In air, we can say that all frequencies must travel at nearly the same speed, the speed of light. With that we can adjust the relationship between frequency ($f$) and wavelength ($\lambda$) with the following equation:
$$f=\frac{c}{\lambda}$$
- $c$  is the speed of light and it is equal to 299 792 458 m / s. In the calculations for this text, for convenience we will approximate this value to $3\text{x}10^{8} m/s$

If we write the equation in terms of wavelength:
$$\lambda=\frac{c}{f}$$

![[images/frequency_vs_wavelength.png]]

> [!info] 
>  
The higher the frequency, the smaller is the physical length of the waveform.

Why is the wavelength important? Let's keep exploring more concepts.

## Antenna Size

In general an antenna is a metallic device (as a rod or wire) that radiates or receives electromagnetic waves. It is the structure between free-space and a guiding device. 

![[antenna_receiver_transmitter_v2.png]]

- A receiving antenna is responsible to convert electromagnetic waves into an electrical energy signal
- A transmitting antenna is responsible to convert an electrical signal signal into electromagnetic waves

The study of antennas just by itself is an interesting endeavor, but let's keep things simple for now. When building antennas we need to pay attention to the following parameters:

![[antenna_parameters.png]]

All these parameters are somehow interconnected which makes it harder to decouple the parameters and study them independently of each other. However, we can focus on some of those relationships to understand how the wavelength is connected to the physical parameters of an antenna.

Antennas can have different shapes and different shapes will radiate or receive electromagnetic waves differently. 

![[types_of_antennas_1.png]]

We can group antennas based on how we built them.

![[types_of_antennas.png]]

> [!note] 
> I am going to focus on one type of antennas for now so we can understand how the wavelength is related with an antenna. 

A common type of antennas found in buildings, ships, cars, and/or space crafts is the **dipole** wire antenna.

![[dipole_antenna_plane_altimeter.png]]

Typically is construct with two metallic wires configured as a T shaped geometry.

![[dipole_antenna_schematic.png]]

Frequently used shapes of a dipole antenna.

![[dipole_antenna_different_shapes.png]]

You can also find a combination of different types of antennas. The picture below shows a "Rabbit-ears" dipole antenna with a small loop antenna.

![[rabbit_ears_antenna.png]]

If we apply a varying voltage source at the terminals of the antenna, the charges inside the metallic antenna will oscillate at the same frequency as the voltage source. Those oscillations will create an electric field that is radiated by the antenna.

![[voltage_source_applied_antenna.png]]

The radiation pattern of a dipole antenna looks like the picture below. 
We will see briefly what size of antenna do we pick for optimal transmission. 

![[animated_charges_tx.gif]]

Remember that an electromagnetic wave is composed by an electrical and magnetic field that are orthogonal (perpendicular) to each other.

![[electromagnetic_wave.png]]

It is common to show only the electric field on antennas radiation patterns. 
The picture below shows the electric field radiation pattern of a dipole antenna vs an isotropic radiation pattern.

![[radiation_pattern_transmitting_antenna.png]]

> [!info] 
> The isotropic radiation is there as a reference radiation pattern. Isotropic antennas are the ideal case of a transmitting antenna. It represents a point source that radiates in all directions equally. Unfortunately, such antenna doesn't exist but we can use it to compute the gains of practical antennas.

If we orient the receiving dipole antenna in away that the electric field vector is aligned with the metallic wires, we polarized the antenna. Polarization could be horizontal, vertical or hybrid. What it is important is that the polarization (or antenna orientation) should be the same at both ends of a communication link.

![[antenna_polarisation.png]]

Now we have this electric field travelling through air until it encounters a receiving antenna.

![[animated_rx_antenna.gif]]

Remember that antennas are normally metallic, and metals are good conductors. When the electric field passes through the antenna, it moves the charges inside the metal according to the way that the electric field is oscillating. The oscillating charges inside the antenna will generate a varying voltage signal at the terminals of the antenna. 

![[animated_charges_inside_antenna.gif]]

> [!note] 
> For a perfect reception and transmission, the size of the antenna should be half of the wavelength. 
> 
> $L=\frac{\lambda}{2}$

![[antenna_length_vs_wavelength.png]]

An interesting fact that happens to an antenna made out of a thin linear conductor that has a length twice the free-space wavelength ($\lambda=2L$) is that it enters the antenna fundamental resonance.

> [!help] 
>  If you don't know what resonance is, don't panic. Check the "Complementary Knowledge" section.

The most common antenna size that you will see is the $L=\frac{\lambda}{2}$, however you can adjust the antenna size according to your required or desired directive gain parameter.

![[gain_of_dipole_antennas.png]]

## Antenna Gain

Another interesting relationship is between antenna gain and antenna effective area, that is described by the following equation:

$$G_r=\frac{\text{radiation intensity to a given polarization}}{\text{total radiation intensity of an isotropic antenna}}$$

The gain will be determined by the amount of radiation that the antenna is receiving for a given orientation (horizontal or vertical polarization) divided by the ideal radiation intensity of an isotropic antenna.

![[antenna_gain_effective_area.png]]

![[some_antenna_structures_and_directive_gain.png]]

You will commonly find the equation below that calculates the antenna gain considering how much area of the antenna is inside a radiation sphere that is capturing the signal.
$$G_r=\frac{(4\pi A_{eff})}{\lambda^2}=(4\pi A_{eff})\left(\frac{f}{c}\right)^2$$
where $G_r$ is the receiver antenna gain, $A_{eff}$ is the effective area (intersection plan) within an isotropic radiation sphere pattern, and $\lambda$ is the wavelength of your signal.

Notice that if we decrease the wavelength of our signal (or increase the frequency of our signal), $G_r$ will increase.

> [!note] 
>  Higher frequency signals will have higher antenna gains

## Putting all Together

Let's say that we want to transmit voice over radio. The human hear can perceive frequencies between 20Hz to 20kHz. However, most of the energy in a human voice takes effect around 250Hz.  

![[audio_bands_table.png]]

![[audio_bands_spectrum.png]]

Consider that we want to transmit the narrow band of audio sounds $f_c=3.4KHz$
For that we will need an antenna with a length $L$ equal to:

$$L=\frac{\lambda}{2}=\frac{c}{2f}=\frac{3\times10^8}{2\times3.4\times10^3}=44117\;(meters)$$

What ? 😱

Another example. Now consider we want to capture an electromagnetic wave at $f_c=433MHz$.

> [!info] 
>  433 MHz is a commonly used frequency band for all types of equipment that requires little power, such as garage door openers, headphones, baby phones and remote controllers.

We will need an antenna with a length $L$ equal to:
$$L=\frac{\lambda}{2}=\frac{c}{2f}=\frac{3\times10^8}{2\times433\times10^6}=0.346\;(meters)$$

Way more feasible to build than the first example.

## Summary

We just saw that it is virtually impossible to send low frequency electromagnetic waveforms with an antenna. The size of the antennas to transmit and receive the signal would be impractically large.

> [!info] 
> However, if we somehow increase the frequency of our signals, the antenna size becomes practical to build. 

Modulation comes to the rescue and we will see what does modulation mean in the next chapter.

There are a couple more reasons why modulation is needed. At this point, I don't think it is visible how the statements below are valid, but I am going to write them down anyway to highlight that modulation brings other benefits.

> [!info] 
>  - Modulation makes the designing and processing of signal in Tx and Rx devices much more convenient and simple.
>  - Modulation allows frequency division multiplexing (FDM) for simultaneous transmission of many information signals over a common channel having much wider bandwidth.

We will validate these statements in later chapters.

## Additional References

- Hyperphysics Website [(Light and Vision Section)](http://hyperphysics.phy-astr.gsu.edu/hbase/ligcon.html#c1)
- The Standard Model [(Cern Article)](https://home.cern/science/physics/standard-model#:~:text=There%20are%20four%20fundamental%20forces,force%2C%20and%20the%20gravitational%20force.)
- The Electromagnetic Spectrum [(NASA Article)](https://imagine.gsfc.nasa.gov/science/toolbox/emspectrum1.html#:~:text=The%20electromagnetic%20(EM)%20spectrum%20is,two%20types%20of%20electromagnetic%20radiation.)
- Hubblesite [(Article)](https://hubblesite.org/contents/articles/the-electromagnetic-spectrum)
- Common Antenna Terms [(Article)](https://www.mvg-world.com/en/manual/antenna-measurement-101/a-guide-to-common-antenna-terms)
- Antennas Types and Parameters [(Circuit Design Article)](https://www.cdt21.com/design_guide/antenna-types-and-parameters/)
- How does an Antenna Work? (Lesics channel) [(YouTube Video)](https://youtu.be/ZaXm6wau-jc?si=TAvYjEU7y_Uq5zoW)
- Understanding Electromagnetic Radiation (Lesics channel) [(YouTube Video)](https://youtu.be/FWCN_uI5ygY?si=TSlagrsy8g_U9JhD)
- Antennas, the mmWave Advantage [(Article)](https://www.microwavejournal.com/articles/print/18072-antennas--the-mmwave-advantage)
- Antenna Theory Propagation [(YouTube Video)](https://youtu.be/-F7KYLO4Bkg?si=91Dj-ZTU757fHvBg)

