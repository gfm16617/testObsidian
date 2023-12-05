# Fourier Analysis
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
maxLevel: 0 # Include headings up to the speficied level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---

Fourier analysis is the study of the way general functions may be represented or approximated by sums of simpler trigonometric functions. There are so many flavors under this Fourier analysis that it becomes confusing to understand which one to use.

## Fourier Types

A signal can be either continuous or discrete, and it can be either periodic or aperiodic. The combination of these two features generates the four categories illustrated below.

![[fourier_analysis_categories.png]]
## Fourier Series

A good portion of engineering topics (e.g., analog circuits, power, electromagnetics, signals and systems, engineering mathematics, digital communications), rely on **Fourier Series** as a tool to study the problems that are present in those domains.

Briefly, Fourier Series deals with periodic signals that can be written as an infinite sum of harmonically related sinusoids.

![[play_icon.png]] [Geogebra Link](https://www.geogebra.org/m/aenhzjpz)
![[geogebra_fourier_series.gif]]

The confusion with Fourier Series, relies on the fact that there are 3 common forms to represent this infinite sum of sinusoids: trigonometric, phasor, and exponential form; depending on which problem in engineering you are trying to solve.

- Analog Circuits and Power Electronics typically use the phasor (Amplitude/Phase) representation.
- Signals and Systems, Electromagnetics, and Engineering Mathematics typically use the complex exponential.

![[fougier_series_forms.png]]

## Fourier Series Spectrum

Using the Amplitude/Phase or Complex Exponential Fourier Series representation, we can create the Fourier spectrum of a signal. The Fourier spectrum indicates the relative amplitudes (or magnitudes) and phases of the sinusoids that are required to synthesize that signal. It is also known as discrete frequency spectrum. 

![[play_icon.png]] [MatLab Link](https://dspfirst.gatech.edu/matlab/)
![[fourier_series_matlab_gui.gif]]

> [!info] 
>  The magnitude spectrum will always have positive magnitudes.

What if the signal is aperiodic? 🤔

## Fourier Transform

The Fourier series is a perfectly suitable construct for representing periodic functions, but what about nonperiodic (or aperiodic) functions? This is where Fourier Transform comes in place to answer this question.

Fourier  Transform is the mathematical operation for converting a signal (periodic or aperiodic) from time domain into it's frequency domain. It is derived from the complex exponential Fourier Series representation and it has the following expression:
$$F(\omega)=\mathcal{F}[f(t)]=\int_{-\infty}^{\infty}f(t)e^{-j\omega t}dt$$
The inverse Fourier Transform converts a frequency domain signal to its time domain representation.
$$f(t)=\mathcal{F}^{-1}[F(\omega)]=\frac{1}{2\pi}\int_{-\infty}^{\infty}F(\omega)e^{j\omega t}d\omega$$
We may also use the symbolic form:
$$f(t) \longleftrightarrow  F(\omega)$$

For Digital Communications topics, the Fourier Transform is normally used. However, it is rarely applied by definition. Instead, tables with the most common Fourier Transform pairs and properties are used.

**Fourier Transform Pairs**
![[fourier_transform_pairs.png]]

**Fourier Transform Properties**
![[fourier_transform_properties.png]]

## Fourier Transform Spectrum

The Fourier spectrum is identical to the spectrum presented during the Fourier Series. The main difference relies on a continuous spectrum instead of a discrete spectrum.

![[fourier_series_vs_transform_spectrum.png]]

> [!info] 
>  The Fourier Transform calculates the frequency components present in a signal, while the spectrum visually represents these components, often showing their amplitude, phase or power distribution across different frequencies.
>  
>  The amplitude (or magnitude) spectrum will always have positive values, while the Fourier Transform will have signed real and imaginary numbers.

## Fourier Transform Pairs and Properties

The most common used Fourier Transform pairs in digital communications are:

![[fourier_transform_pairs_most_common.png]]

There is a small detail that is important to emphasize and redraw on the Fourier Transform pairs 8 and 9 figures, the y-axis changes according if it is a real or imaginary number.

The $cos(\omega_0t)$ pair:

![[fourier_transform_pair_cos.png]]
The $sin(\omega_0t)$ pair:

![[fourier_transform_pair_sin.png]]
This is going to be important later to understand more advance concepts (e.g.: Hilbert Transform).

The most common used Fourier Transform properties in digital communications are:

![[fourier_transform_properties_most_common.png]]

## Sources of Confusion

#### Carrier and Baseband Signals

In digital communication literature, you will commonly find the carrier $c(t)=cos(\omega_c)$ and the baseband signal $m(t)=cos(\omega_m)$. However, sometimes some resources use $c(t)=sin(\omega_c)$ and $m(t)=sin(\omega_m)$ or a combination of these signals.

> [!note] 
> For simplicity I am going to set the amplitudes of $c(t)$ and $m(t)$ equal to 1

Which sinusoidal waveform should I use for the carrier and baseband, sin or cos? 🤔

To answer this question, it is important to be aware of a couple of concepts:
- the difference between Fourier Transform and Spectrum
- and are we working with real or complex numbers.

I will try to answer this question with some examples and then summarize the results at the end.

#### Example 1

Let's start by analyzing the most common representation and multiply those two signals together:
- $c(t)=cos(\omega_c)$
- $m(t)=cos(\omega_m)$
- $s(t)=m(t).c(t)=cos(\omega_m).cos(\omega_c)$

There are two ways to approach this multiplication:
1. Apply a trigonometric identity and then apply a Fourier Transform pair
	- the trigonometric identity can be used to represent all cases
	![[trig_product_identity.png]]
2. Apply the modulation Fourier Transform property and then apply a Fourier Transform pair.

I am going to use option 1 but the math will yield the same results if we use option 2.

Apply the trigonometric identity to $s(t)$:
$$cos(\alpha).cos(\beta)=\frac{cos(\alpha+\beta)+cos(\alpha-\beta)}{2}$$
$$s(t)=\frac{1}{2}\left[ cos(\omega_m+\omega_c) + cos(\omega_m-\omega_c) \right]$$
Then apply the Fourier Transform pair to $s(t)$:
$$cos(\omega_0)\to \mathcal{F} \to \pi \left[ \delta(\omega-\omega_0) + \delta(\omega+\omega_0)\right]$$
$$S(\omega)=\frac{1}{2}.\pi \left[ \textcolor{magenta}{\delta(\omega-\omega_m-\omega_c)} + \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) + \textcolor{magenta}{\delta(\omega+\omega_m-\omega_c)}\right]$$

![[fourier_transform_icon.png]] **Fourier Transform Plot**
![[cos_cos_fourier_transform.png]]

![[fourier_spectrum_icon.png]] **Fourier Transform Magnitude Spectrum**
![[cos_cos_fourier_spectrum.png]]

> [!note] 
>  - Notice on how the Fourier Transform Plot has a real number on the y-axis
>  - And the magnitude spectrum has positive magnitudes on the y-axis
>  - For now these two plots are identical but we will see shortly the difference between them.

#### Example 2

Now I will change the baseband signal to a sin waveform:
- $c(t)=cos(\omega_c)$
- $m(t)=sin(\omega_m)$
- $s(t)=m(t).c(t)=sin(\omega_m).cos(\omega_c)$

Apply the trigonometric identity to $s(t)$:
$$sin(\alpha).cos(\beta)=\frac{sin(\alpha+\beta)+sin(\alpha-\beta)}{2}$$
$$s(t)=\frac{1}{2}\left[ sin(\omega_m+\omega_c) + sin(\omega_m-\omega_c) \right]$$
Then apply the Fourier Transform pair to $s(t)$:
$$sin(\omega_0)\to \mathcal{F} \to j\pi \left[ \delta(\omega+\omega_0) - \delta(\omega-\omega_0)\right]$$
$$S(\omega)=\frac{1}{2}.j\pi \left[ \delta(\omega+\omega_m+\omega_c) \textcolor{magenta}{- \delta(\omega-\omega_m-\omega_c)} + \textcolor{magenta}{\delta(\omega+\omega_m-\omega_c)} - \delta(\omega-\omega_m+\omega_c)\right]$$

![[fourier_transform_icon.png]] **Fourier Transform Plot**
![[sin_cos_fourier_spectrum.png]]

![[fourier_spectrum_icon.png]] **Fourier Transform Magnitude Spectrum**
![[cos_cos_fourier_spectrum.png]]

> [!note] 
>  - Notice on how the Fourier Transform Plot has an imaginary number on the y-axis
>  - and the magnitude spectrum has positive magnitudes on the y-axis 
>  - The spectrum of Example 2 is the same has Example 1 spectrum.

#### Example 3

Now I will change the carrier and baseband signal to sin waveforms:
- $c(t)=sin(\omega_c)$
- $m(t)=sin(\omega_m)$
- $s(t)=m(t).c(t)=sin(\omega_m).sin(\omega_c)$

Apply the trigonometric identity to $s(t)$:
$$sin(\alpha).sin(\beta)=\frac{cos(\alpha-\beta)-cos(\alpha+\beta)}{2}$$
$$s(t)=\frac{1}{2}\left[ cos(\omega_m-\omega_c) - cos(\omega_m+\omega_c) \right]$$
Then apply the Fourier Transform pair to $s(t)$:
$$cos(\omega_0)\to \mathcal{F} \to \pi \left[ \delta(\omega-\omega_0) + \delta(\omega+\omega_0)\right]$$
$$S(\omega)=\frac{1}{2}.\pi \left[ \delta(\omega-\omega_m+\omega_c) + \textcolor{magenta}{\delta(\omega+\omega_m-\omega_c)} \textcolor{magenta}{- \delta(\omega-\omega_m-\omega_c)} - \delta(\omega+\omega_m+\omega_c)\right]$$

![[fourier_transform_icon.png]] **Fourier Transform Plot**
![[sin_sin_fourier_spectrum.png]]

![[fourier_spectrum_icon.png]] **Fourier Transform Magnitude Spectrum**
![[cos_cos_fourier_spectrum.png]]

> [!note] 
>  - Notice on how the Fourier Transform Plot has a real number on the y-axis
>  - And the magnitude spectrum has positive magnitudes on the y-axis
>  - The spectrum of Example 3 is the same has Example 1 and 2 spectrums.

## Summary

- The spectrums are the same independently what type of sinusoidal waveform we used for the carrier or baseband signals.

- This is why for analog modulations you can find different sinusoidal waveforms for the carrier and baseband and the spectrum results are the same. 

- However, for digital modulations or for some transforms used in analog modulations (e.g.: Hilbert Transform), quadrature information (or complex signals) is necessary and at this point the Fourier Transform plots can be a useful visualization tool to use.

## References

- Educational MatLab GUIs [(MatLab GUIs)](https://dspfirst.gatech.edu/matlab/)

