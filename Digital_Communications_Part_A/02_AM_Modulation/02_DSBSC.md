---
tags:
  - am_modulation
---
# DSBSC
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
maxLevel: 0 # Include headings up to the speficied level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---
## Double Sideband Suppressed Carrier

![[types_dsbsc_map.png]]

The first type of AM modulation is the most simple one, but probably one the most used one 🙂

> [!important] 
> Make sure that you fully understand the DSBSC. 
> - The other types of AM modulation built from this one
> - Later, during the digital modulation techniques (Part B of this course), a lot of the knowledge from the DSBSC will be useful to understand digital modulations concepts.

## Block Diagram

![[design_icon.png]]
![[DSBSC_block_diagram.png]]
## Lab Bench

![[lab_icon.png]]

Using the lab equipment, I connect an analog carrier signal $c(t)$ at 100 kHz to input 1 of a multiplication module, and an analog baseband signal $m(t)$ at 2 kHz to input 2 on that same multiplication module.

#### Carrier and Baseband Signals

- Orange Line: baseband signal $m(t)$
- Blue Line: carrier signal $c(t)$
 
**Time Domain Waveform**
![[dsbsc_carrier_baseband_time.png]]

![[dsbsc_carrier_baseband_time_zoom.png]]

**Frequency Spectrum**
![[dsbsc_carrier_baseband_spectrum.png]]


#### Modulated Signal

- Orange Line: baseband signal $m(t)$
- Blue Line: modulation output $s(t)$

**Time Domain Waveform**
![[dsbsc_modulation_baseband_time.png]]

![[dsbsc_modulation_baseband_time_zoom.png]]

> [!note] 
> - We can see the amplitude of the carrier $c(t)$ being modulated by the baseband signal $m(t)$ generating the modulation output $s(t)$.
> - We see the envelope of the carrier changing accordingly

> [!important] 
> There is a small thing that we need to know about the hardware multiplication module that I am using:
> - The output of the multiplication module is equal to $k.X(t).Y(t)$, with k approximately equal to 1/2.
> - That is why we don't see the maximum amplitude of the modulation output signal (in the time domain) equal to $A_c.A_m$ but rather $\frac{A_c.A_m}{2}$.
> - That k factor is 1/2 so that, with standard level inputs, later stages of the BiSKIT are not overloaded.

**Frequency Spectrum**
![[dsbsc_modulation_spectrum.png]]

![[dsbsc_modulation_spectrum_zoom.png]]

> [!note] 
>- We can observe that the modulated signal (in blue) contains two sidebands around the suppressed carrier $c(t)$.
>- Those sidebands are at frequencies $\omega_c \pm \omega_m$

## Time Domain Analysis

![[theory_icon.png]]

- Baseband: $m(t)=A_m.cos(\omega_m)$
- Carrier: $c(t)=A_c.cos(\omega_c)$

The modulation output $s(t)$ is the following:
$$s(t)=m(t).c(t)=A_c.A_m.cos(\omega_m).cos(\omega_c)$$
We can use Desmos (or similar mathematical toolboxes) to validate the mathematical expressions.

![[play_icon.png]] [Desmos Link](https://www.desmos.com/calculator/shjnvkjvl2)
![[dsbsc_desmos_animation.gif]]

> [!important] 
> In order to match the results from the Lab section, we need to adjust the modulation output by 1/2, which is the k factor present on the hardware multiplication module.
> - The theoretical equation doesn't reflect that but the equation on Desmos does.

## Frequency Domain Analysis

Now it is time to verify the spectrum domain starting from the time domain equation.
$$s(t)=m(t).c(t)=A_c.A_m.cos(\omega_m).cos(\omega_c)$$
There are two ways to get the spectrum, and they give the same answer.

#### Option 1

We apply the following trigonometric identity to $s(t)$:
$$cos(\alpha).cos(\beta)=\frac{cos(\alpha+\beta)+cos(\alpha-\beta)}{2}$$
$$s(t)=\frac{A_c.A_m}{2}\left[ cos(\omega_m+\omega_c) + cos(\omega_m-\omega_c) \right]$$
And then apply the following Fourier Transform pair:
$$cos(\omega_0)\to \mathcal{F} \to \pi \left[ \delta(\omega-\omega_0) + \delta(\omega+\omega_0)\right]$$
$$S(\omega)=\frac{A_c.A_m.\pi}{2} \left[ \textcolor{magenta}{\delta(\omega-\omega_m-\omega_c)} + \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) + \textcolor{magenta}{\delta(\omega+\omega_m-\omega_c)}\right]$$

#### Option 2

We apply directly the modulation Fourier Transform property:
$$cos(\omega_0).f(t)\to \mathcal{F} \to \frac{1}{2}\left[ F(\omega-\omega_0) + F(\omega+\omega_0)\right]$$
- where the carrier $c(t)$ is the modulator $cos(\omega_0)=cos(\omega_c)$
- and $f(t)$ is the baseband signal $cos(\omega_m)$
$$S(\omega)=\frac{A_m.A_c}{2} \left[ F(\omega-\omega_c) + F(\omega+\omega_c) \right]$$
Since $F(\omega_m)$ is the following Fourier Transform pair:
$$F(\omega_m)=\pi \left[ \delta(\omega-\omega_m) + \delta(\omega+\omega_m)\right] \to \mathcal{F}^{-1} \to cos(\omega_m) $$
We get to the same result as option 1:
$$S(\omega)=\frac{A_c.A_m.\pi}{2} \left[ \textcolor{magenta}{\delta(\omega-\omega_m-\omega_c)} + \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) + \textcolor{magenta}{\delta(\omega+\omega_m-\omega_c)}\right]$$

## Frequency Spectrum

Waveforms software only shows the positive side of the spectrum. With that in mind we can eliminate the frequencies that are negative from $s(\omega)$ ($\textcolor{magenta}{\text{coefficients in purple}}$) and rewrite the equation as:
$$S(\omega)=\frac{A_c.A_m.\pi}{2} \left[ \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) \right]$$
> [!note] 
> If we sketch $s(\omega)$ we get the spectrum below, which complies with what we observed.
> - Suppressed carrier on the modulated signal
> - Two sidebands at frequencies $\omega_c \pm \omega_m$ 

![[fourier_spectrum_icon.png]] **Spectrum**
![[dsbsc_modulation_spectrum_math.png]]
However, the magnitudes from the graph above are not equal to what we observed in the lab bench spectrum:
$$\frac{A_m.A_c.\pi}{2}=\frac{2\times2\times\pi}{2}=2\pi\neq1$$

> [!info] 
> A couple more things to get the spectrum magnitude correct:
> - Don't forget to divide $\frac{A_m.A_c}{2}$ by 1/2 due to the k factor of the hardware multiplication module.
> - We don't need to worry about the $\pi$ value because on the Waveforms software, if we compute the FFT using the [Vpeak](https://digilent.com/reference/software/waveforms/waveforms-3/reference-manual?redirect=1#magnitude1) which is relative to 1V amplitude sine wave, $\pi$ cancels out.
> ![[waveforms_vpeak_parameter.png]]

With these adjustments, the magnitudes are now the same.
$$\frac{\left( \frac{A_m.A_c}{2} \right)}{2}=\frac{2\times2}{4}=1$$

## Summary

- In DSBSC the carrier signal is completely suppressed from the AM signal. 

- The two sidebands contain complete contents of the modulating signal.

- It is a power efficient method compared with other AM types.

- One disadvantage of using DSBSC is that the resultant envelope is not a faithful representation of the modulating signal. This is more noticeable when complex waveforms such as speech are used.
- Because there is no carrier, the receiver side or demodulator will have a harder time synchronizing with the carrier.

- DSBSC AM is not often used in analog communication systems. However, it forms the basis for generating another AM type signal, the single-sideband suppressed-carrier (SSBSC), or just single-sideband (SSB) signals.

## References

- Leakage and Window Types (Hanning, Flattop, Uniform) [(YouTube Video)](https://youtu.be/fC49T3-LelE?si=qhT7MHWa0oeVnsbB)
- Window Types: Hanning, Flattop, Uniform, Tukey, and Exponential [(Article)](https://community.sw.siemens.com/s/article/window-types-hanning-flattop-uniform-tukey-and-exponential)
- Anti-Aliasing Filter [(YouTube Video)](https://youtu.be/aDS-Au5m0E8?si=dkDFVJGqTDAy4Hou)
