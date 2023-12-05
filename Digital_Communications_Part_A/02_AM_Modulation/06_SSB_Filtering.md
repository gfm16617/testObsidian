---
tags:
  - am_modulation
---
# SSB - Selective Filtering
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
maxLevel: 0 # Include headings up to the speficied level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---

![[types_filtering_map.png]]

Recall the DSBSC spectrum.

![[fourier_spectrum_icon.png]] **DSBSC Spectrum**
![[dsbsc_modulation_spectrum_math.png]]

The most obvious method of sideband removal is to apply bandpass filter after the DSBSC modulation. This is simple in conception, yet requires a far-from-simple filter for its execution.

![[fourier_spectrum_icon.png]] **Spectrums**
![[ssb_bandpass_spectrum_example.png]]

The two sidebands are close together in frequency that requires specialized filters with steep roll off frequencies and they can be expensive or hard to build.

## Block Diagram

![[design_icon.png]]
![[ssb_filtering_method_block_diagram.png|500]]

## Lab Bench

![[lab_icon.png]]
Using the lab equipment, I connect an analog carrier signal $c(t)$ initially at 100 kHz to input 1 of a multiplication module, and an analog baseband signal $m(t)$ at 13 kHz to input 2 on that same multiplication module.

> [!note] 
> - Unfortunately, I am not able to control the cut off frequencies of the bandpass filter. 
> - That is the reason why I am using an $m(t)$ of 13kHz instead of 2kHz, so we can visualize the bandpass filter remove either the LSB or USB without affecting the baseband signal.

#### Carrier and Baseband Signals

- Blue Line: baseband signal $m(t)$
- Orange Line: carrier signal $c(t)$

**Time Domain Waveforms**
![[ssb_filtering_carrier_baseband_time.png]]

**Frequency Spectrum**
![[ssb_filtering_carrier_baseband_spectrum.png]]

#### Bandpass Filter

The bandpass filter that has the following frequency response:
- Spectrum start frequency: 1kHz
- Spectrum stop frequency: 1MHz
- At around 80kHz and 130kHz the signal attenuates by -20dBs

**BPF Frequency Response**
![[bpf_frequency_response.png]]

> [!attention] 
> Since we have the ability to control the frequency of the carrier and the frequency of the baseband signal, we are going to tinker with those knobs and implement the SSB modulator.
> 
> In a real radio, we would adjust the cut off frequencies of the bandpass filter accordingly.

#### Tinker Signal 1

- Move the carrier frequency in order to filter out the LSB and keep the USB in the transmitted signal.
- Blue Line: baseband signal $m(t)$
- Orange Line: modulation output $s(t)$

**Frequency Spectrum**
![[ssb_usb_spectrum_animation.gif]]

#### Tinker Signal 2

- Move the carrier frequency in order to filter out the USB and keep the LSB in the transmitted signal.
- Blue Line: baseband signal $m(t)$
- Orange Line: modulation output $s(t)$

**Frequency Spectrum**
![[ssb_lsb_spectrum_animation.gif]]

#### Tinker Signal 3

- I know that I didn't cover demodulation yet, however I am going to show the recovered signal so we can validate the reception of the transmitted SSB signal.
- I will be moving the carrier up and down showing that we can recover the baseband signal with the modulated signal changing between DSBSC, USB, and LSB modulation.
- Blue Line: recovered baseband signal $m(t)$ at 13kHz
- Orange Line: modulation output $s(t)$

**Frequency Spectrum**
![[ssb_demodulation_spectrum.gif]]

#### Bandpass Filter Roll Off Frequencies Challenge

- For this last experiment, I started by adjusting $m(t)$ around 1kHz.
- Then move the carrier around to generate an USB and an LSB modulated signal.
- Hopefully it is clear to see the challenges with designing a bandpass filter when the bandwidth of the baseband signal is small.
- Blue Line: recovered baseband signal $m(t)$ at around 1kHz
- Orange Line: modulation output $s(t)$

**Frequency Spectrum**
![[ssb_roll_off_frequency_spectrum_challenge.gif]]

## Time Domain Analysis

![[theory_icon.png]]

- Baseband: $m(t)=A_m.cos(\omega_m)$
- Carrier: $c(t)=A_c.cos(\omega_c)$

We can split the theory into two parts: the output result of the DSBSC module and then the output of the BPF module

#### DSBSC Output

The DSBSC modulation output is:
$$s^`(t)=m(t).c(t)=A_c.A_m.cos(\omega_m).cos(\omega_c)$$
#### BPF Output

Then BPF module output is performing what is called a convolution $(* \longrightarrow symbol)$ between the input signal $s^`(t)$ and the bandpass filter response $h(t)$:
$$s(t)=s^`(t)*h(t)$$
How does $h(t)$ look like? 🤔

To make the answer easier to understand, let's continue to the frequency domain analysis and through that process we will arrive to an answer to this question.

## Frequency Domain Analysis

#### DSBSC Output

The Fourier Transform of the DSBSC modulation output is:
$$S^`(\omega)=\frac{A_c.A_m.\pi}{2} \left[ \textcolor{magenta}{\delta(\omega-\omega_m-\omega_c)} + \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) + \textcolor{magenta}{\delta(\omega+\omega_m-\omega_c)}\right]$$

Recall that the frequency spectrum eliminates the frequencies that are negative from $S^`(\omega)$ ($\textcolor{magenta}{\text{coefficients in purple}}$) and makes all magnitudes positive:
$$S^`(\omega)=\frac{A_c.A_m.\pi}{2} \left[ \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) \right]$$
![[fourier_spectrum_icon.png]] **Spectrum**
![[dsbsc_modulation_spectrum_math.png]]
#### BPF Output

The shape of a bandpass filter in the frequency domain can be approximated to a rectangular shape that has the following Fourier Transform representation:
$$H(\omega)=rect(\omega)= 
\begin{cases}
A \; \; if \; \; \omega_1 < \left| \omega \right| < \omega_2 \\ 
otherwise \; \; 0
\end{cases}$$
![[fourier_spectrum_icon.png]] **Spectrums**
![[ssb_bandpass_spectrum_example.png]]

Knowing this information we can apply the inverse Fourier Transform to $H(\omega)$ and obtain $h(t)$:
$$h(t)=\frac{1}{2\pi}.sinc\left( \frac{t}{2} \right)$$
![[rect_sync_freq_time_fourier.png]]

$h(t)$ is the famous **Sinc** function.

> [!note] 
>  This is the answer to the question raised during the Time Domain analysis section.

#### Multiplication in the Frequency Domain

At this point we know that in the time domain we are doing the convolution of the DSBSC modulated signal $s^`(t)$ with the sinc function $h(t)$:
$$s(t)=s^`(t)*h(t)=s^`(t)*\frac{1}{2\pi}.sinc\left( \frac{t}{2} \right)$$
This is a bit overwhelming to compute 😐, however according to the Fourier Transform property:
$$f_1(t)*f_2(t) \longleftrightarrow F_1(\omega).F_2(\omega)$$
A convolution in the time domain, translate to a multiplication in the frequency domain. This is way easier to compute 🙂

All we are doing in the frequency domain is multiplying $S^`(\omega)$ with $H(\omega)$.
$$S(\omega)=\frac{A_c.A_m.\pi}{2} \left[ \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) \right].rect(\omega)$$
As you are probably already guessing, only the diracs $\delta(\omega)$ that are inside the boundaries of $rect(\omega)$ will pass, otherwise $S(\omega)=0$

## Summary

- Due to the transmission of only one sideband with suppressed carrier, much less transmitted power is necessary to produce the same quality signal in the receiver.

- Building bandpass filters with steep roll off frequencies can be a challenge, specially when the two sidebands are close to each other.

- We didn't cover demodulation yet, but any modulation technique that suppresses the carrier at transmission will make the receiver system more complex because the receiver will require a carrier recovery and synchronization circuit. 

## References

- Understanding the 'Phasing Method' of Single Sideband Demodulation[(Article)](https://www.dsprelated.com/showarticle/176.php)
