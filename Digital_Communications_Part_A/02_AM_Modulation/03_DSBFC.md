---
tags:
  - am_modulation
---
# DSBFC
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
maxLevel: 0 # Include headings up to the speficied level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---
## Double Sideband Full Carrier

![[types_dsbfc_map.png]]

Including a carrier on your modulated signal will be beneficial for the receiver to detect, synchronize and demodulate the transmitted signal properly.

We can augment the DSBSC and add the carrier to the modulated signal.

## Block Diagram

![[design_icon.png]]
![[DSBFC_block_diagram.png]]

## Lab Bench

![[lab_icon.png]]

Using the lab equipment, I connect the output of the previous DSBSC to input 1 of the adder $(g)$ and the carrier $c(t)$ to input 2 of the adder $(G)$, where $g$ and $G$ are knob gains that control how much of the signal passes to the adder respectively.

#### Carrier and Baseband Signals

- Orange Line: baseband signal $m(t)$
- Blue Line: carrier signal $c(t)$

**Time Domain Waveforms**
![[dsbsc_carrier_baseband_time.png]]

![[dsbsc_carrier_baseband_time_zoom.png]]

**Frequency Spectrum**
![[dsbsc_carrier_baseband_spectrum.png]]

> [!attention] 
> Since we have the ability to control how much of the signals we add together, we are going to tinker with the knobs and learn different modulated output signals.

#### Tinker Signal 1

- $c(t)$ gain $G = 0$
- $m(t)$ gain $g=2\times A_m$, to compensate the multiplication factor k = 1/2.
- Orange Line: baseband signal $m(t)$
- Blue Line: modulation output $s^{`}(t)$

**Time Domain Waveform**
![[dsbfc_modulation_baseband_time.png]]

**Frequency Spectrum**
![[dsbfc_modulation_spectrum.png]]

> [!note] 
>- No surprises here. We have the same output as the DSBSC.
>- No carrier on the spectrum and the two sidebands at $w_c\pm w_m$
>- I have the scale on the y-axis up to 5V so we can compare different spectrums later.

If I move the $m(t)$ gain knob $g$ up and down, all I am doing is increasing and decreasing the amplitude of the modulated signal both in time and frequency domain.

![[dsbfc_time_signal_1.gif]]

![[dsbfc_spectrum_signal_1.gif]]

#### Tinker Signal 2

- Orange Line: baseband signal $m(t)$
- Blue Line: modulation output $s^{`}(t)$
- Keep $m(t)$ gain $g$ the same.
- Vary $c(t)$ gain $G$ from 0 until the upper envelope of $s^`(t)$ looks more or less like the diagram below
![[am_envelope_diagram.png|500]]

**Time Domain Waveform**
![[dsbfc_time_signal_2.gif]]

**Frequency Spectrum**
![[dsbfc_spectrum_signal_2.gif]]

> [!note] 
>- Fun stuff happening now 🙂
>- As I increase the gain, the carrier starts showing up on the spectrum.
>- $s^`(t)$ is initially weird but at the end before the animation stops, we can see $m(t)$ on the upper envelope of $s^`(t)$

Let me shift $m(t)$ to the top of $s^`(t)$ so we can visualize the upper envelope of $s^`(t)$ being shaped by $m(t)$.

![[dsbfc_time_signal_1_shift.gif]]

#### Tinker Signal 3

- Orange Line: baseband signal $m(t)$
- Blue Line: modulation output $s^{`}(t)$
- Keep $m(t)$ gain $g$ the same.
- Vary $c(t)$ gain $G$ from previous tinker signal 2 to maximum gain.

**Time Domain Waveform**
![[dsbfc_time_signal_3.gif]]

**Frequency Spectrum**
![[dsbfc_spectrum_signal_3.gif]]

> [!note] 
>- From this point on we don't lose the upper or lower envelope of the modulated signal.
>- Increasing $G$ all it does is to increase the signal strength of $c(t)$

## Quick Note

there is a mathematical way to know which of these 3 tinker signals, or any other signal in between your modulated signal will be.

The method is called **modulation index**, it is a ratio that describes the amount of change in amplitude present in AM waveforms. Based on that ratio, signals can be adjusted accordingly so we can recover the signal at the receiver properly.

I am not covering it here so this chapter doesn't get too extensive. Check the modulation index chapter for more details about it.

## Time Domain Analysis

![[theory_icon.png]]

- Baseband: $m(t)=A_m.cos(\omega_m)$
- Carrier: $c(t)=A_c.cos(\omega_c)$

The modulation output $s^`(t)$ is the following:
$$s^`(t)=[1+m(t)].c(t)=A_c.cos(\omega_c)+A_c.A_m.cos(\omega_m).cos(\omega_c)$$
We can use Desmos (or similar mathematical toolboxes) to validate the mathematical expressions.

![[play_icon.png]] [Desmos Link](https://www.desmos.com/calculator/mym9rsbh0x)
![[dsbfc_desmos_animation.gif]]

## Frequency Domain Analysis

Now it is time to verify the spectrum domain starting from the time domain equation.
$$s^`(t)=[1+m(t)].c(t)=\textcolor{red}{A_c.cos(\omega_c)} + \textcolor{blue}{A_c.A_m.cos(\omega_m).cos(\omega_c)}$$
If you understood and followed the frequency domain analysis of the DSBSC, you recognize that the $\textcolor{blue}{blue}$ part of $s^`(t)$ is equal to the DSBSC modulated signal $s(t)$.
We know the Fourier result of that already:
$$S(\omega)=\frac{A_c.A_m.\pi}{2} \left[ \textcolor{magenta}{\delta(\omega-\omega_m-\omega_c)} + \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) + \textcolor{magenta}{\delta(\omega+\omega_m-\omega_c)}\right]$$
The $\textcolor{red}{red}$ part of $s^`(t)$ has a simple transform pair:
$$cos(\omega_0)\to \mathcal{F} \to \pi \left[ \delta(\omega-\omega_0) + \delta(\omega+\omega_0)\right]$$
The final result:
$$S^`(\omega)=A_c.\pi \left[ \textcolor{magenta}{\delta(\omega -\omega_0)} + \delta(\omega+\omega_0)\right] + S(\omega)$$

## Frequency Spectrum

Waveforms software only shows the positive side of the spectrum. With that in mind we can eliminate the frequencies that are negative from $s^`(\omega)$ ($\textcolor{magenta}{\text{coefficients in purple}}$) and rewrite the equation as:
$$S^`(\omega)=A_c.\pi [\delta(\omega+\omega_0)]+\frac{A_c.A_m.\pi}{2} \left[ \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) \right]$$

> [!note] 
> If we sketch $S^`(\omega)$ we get the spectrum below, which complies with what we observed.
> - Full carrier on the modulated signal
> - Two sidebands at frequencies $\omega_c \pm \omega_m$ 

![[fourier_spectrum_icon.png]] **Spectrum**
![[dsbfc_modulation_spectrum_math.png]]
> [!info] 
> If you are confirming the magnitudes on the spectrum:
> - Don't forget that the hardware multiplier that I am using divides the output by k = 1/2
> - To accommodate this, I need to divide my spectrum by two
> - $\pi$ gets cancelled out by Waveforms software FFT visualization

## Alternative Design

You can find in literature an alternative block diagram that produces the same output as the DSBFC described previously.

Instead of adding the carrier to the DSBSC modulated signal, we add a DC component to the baseband signal $\longrightarrow [V_c + m(t)]\longrightarrow$ before multiplying it with $c(t)$.

## Block Diagram 2

![[design_icon.png]]
![[DSBFC_AM_block_diagram.png]]

For this case, it is assumed that $c(t)=cos(\omega_c)$ and $m(t)=A_m.cos(\omega_m)$

The modulation output $s(t)$ is the following:
$$s(t)=[V_c+m(t)].c(t)=A_c.cos(\omega_c)+A_m.cos(\omega_m).cos(\omega_c)$$
where $V_c$  ends up to be the amplitude of the carrier $A_c$

If we factor out $A_c$ and $cos(\omega_c)$ we get the following equation:
$$s(t)=\left[1+\frac{A_m}{A_c}.cos(\omega_m)\right]A_c.cos(\omega_c)$$
and making $\frac{A_m}{A_c}=m_a$ we get:
$$s(t)=\left[1+m_a.cos(\omega_m)\right]A_c.cos(\omega_c)$$
where $m_a$ is called modulation index.

> [!note] 
> As mentioned on the Quick Note, I will cover modulation index on a different chapter. 

> [!attention] 
>  That assumption of $c(t)=cos(\omega_c)$ instead of $c(t)=A_c.cos(\omega_c)$ can be confusing to accept. We have been using $c(t)$ with $A_c$ and all of a sudden we drop that $A_c$ 🤔
>  
>  However, there is a another subtle hidden assumption that we can uncover with the explanation below that will helps us digest $c(t)=cos(\omega_c)$

Let's use the expression that we used during the DSBFC simulation using Desmos.

Desmos equation: 
$$s(t)=G.c(t)+g.k.m(t).c(t)=[1+\frac{g}{G}k.m(t)].G.c(t)$$
$$s(t)=[1+\frac{g}{G}k.A_m.cos(\omega_m)].G.A_c.cos(\omega_c)$$

We can remove $k$ because that is a constant due to the hardware that I am using to test these equations. On that same hardware the modules responsible to generate $m(t)$ and $c(t)$ don't have a way to change the amplitudes $A_m$ and $A_c$ , which makes them a constant too.

For simplicity, if we set $A_m=A_c=1$ (it could be any other constant, as long as we make $A_m=A_c$) we get the following:
$$s(t)=[1+\frac{g}{G}.cos(\omega_m)]G.cos(\omega_c)$$
which $g$ and $G$ end up to control the amplitude of $m(t)$ and $c(t)$ accordingly.
$$s(t)=[1+\frac{A_m}{A_c}.cos(\omega_m)]A_c.cos(\omega_c)$$
> [!note] 
> - This alternative block diagram assumes that $m(t)$ and $c(t)$ have equals magnitudes from the modules that are generating these signals.
> - Later we can manipulate those magnitudes according to the modulation index $m_a$

## Summary

- In DSBFC the carrier signal is present on the AM modulated signal.

- It is less power efficient method compared with DSBSC because we need to transmit the carrier and the sidebands. 

- For the modulated signal to be similar to tinker signal 2 and 3, the magnitude of the carrier is significantly higher that the sidebands which in turn will require more power to transmit.

- On the other hand, because there is a carrier, the receiver side or demodulator will be able to synchronize with the carrier easily.

## References
