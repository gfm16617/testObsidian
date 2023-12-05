---
tags:
  - am_modulation
---
# SSB - Phasing Method
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
maxLevel: 0 # Include headings up to the speficied level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---

![[types_phasing_map.png]]

Another way of generating SSB is called phasing method. This uses a technique called phase discrimination to cancel out one of the sidebands at the generation stage (instead of filtering it out afterwards).

## Block Diagram

![[design_icon.png]]
![[ssb_phasing_method_block_diagram.png]]

The phasing method uses complex IQ processing to resolve the superposition of lower and upper sidebands at audio frequencies. 

The complex mixer creates an I and Q component by splitting the signal into two DSBSC mixers that are modulated by a sine and cosine local oscillator (e.g. implemented by a phase shift of 90°). An Hilbert transformer shifts the Q component by 90° before entering the DSBSC mixer. The I and Q component are then added together to form the SSB signal.

I think just by looking at the block diagram, it is not too intuitive on how we cancel one of the sidebands by using complex numbers, but let's build this block diagram first, see it working and then validate the answer mathematically.

## Lab Bench

![[lab_icon.png]]

#### Probe 1 - Baseband Quadrature Generation

We first start by generating a quadrature baseband signal by shifting $m(t)$ by $90^o$

- Orange Line: baseband signal $m(t)$
- Blue Line: quadrature signal $m^`(t)$

![[ssb_phasing_method_block_diagram_probe1.png]]

**Time Domain Waveforms**
![[ssb_phasing_time_probe1.gif]]

#### Probe 2 - IQ DSBSC Generation

Second, we generate two DSBSC signals in quadrature to each other by multiplying with the respective carrier. 

- Orange Line: DSBSC signal $s_1(t)$
- Blue Line: DSBSC signal $s_2(t)$

![[ssb_phasing_method_block_diagram_probe2.png]]

**Time Domain Waveforms**
![[ssb_phasing_time_probe2.png]]

> [!note] 
>  Notice on how we have two DSBSC signals with a modulation index $m_a=1$ in quadrature.

**Frequency Domain Spectrum**

- Orange Line: DSBSC signal $S_1(\omega)$
- Blue Line: DSBSC signal $S_2(\omega)$

![[ssb_phasing_spectrum_probe2.gif]]

> [!note] 
> Looking at the spectrum we see that both DSBSC signals have the same sidebands, which makes sense because the spectrum makes all magnitudes positive.
> 
> However, if I was able to plot the Fourier Transform, I would see the DSBSC $S_2(\omega)$ sidebands slightly different than what we see here.

If we plot the Fourier Transform, we get the following graphs:

![[ssb_phasing_fourier_probe2.png]]

#### Probe 3 - SSB Phasing Generation

On the last step, we can see the final result by probing $s(t)$ and confirm that one of the sidebands will cancel out and the other sideband will become the double in magnitude.

The cool part with this last step is that we can validate the Fourier Transform graphs 🙂

![[ssb_phasing_method_block_diagram_probe3.png]]

**Frequency Domain Spectrum**

- Orange Line: DSBSC signal $S_1(\omega)$
- Blue Line: DSBSC signal $S_2(\omega)$

![[ssb_phasing_spectrum_probe3.png]]

The cool part about this is, if I play around with the phase shifter that generates the $m^`(t)$ signal that goes into the second DSBSC, we can choose which sideband we want to cancel out.

![[ssb_phasing_animation_probe3.gif]]

Or we could subtract the signals instead of adding to reverse the sidebands result.

## Time Domain Analysis

![[theory_icon.png]]

- Baseband: $m(t)=A_m.cos(\omega_m)$
- Carrier: $c(t)=A_c.cos(\omega_c)$

The good news about the theory is that we covered pretty much all of it already, we just need to formalize it.

#### Probe 1 - Baseband Quadrature Generation

Generate a quadrature baseband signal by shifting $m(t)$ by $90^o \longrightarrow A_m.cos(\omega_m - 90^o)$ 
$$m^`(t)=A_m.sin(\omega_m)$$
#### Probe 2 - IQ DSBSC Generation

Generate two DSBSC signals in quadrature to each other by multiplying with the respective carrier. 
$$s_1(t)=m(t).c(t)=A_m.A_c.cos(\omega_m).cos(\omega_c)$$
Quadrature carrier $c^`(t)=A_c.cos(\omega_c - 90^o)=A_c.sin(\omega_c)$
$$s_2(t)=m^`(t).c^`(t)=A_m.A_c.sin(\omega_m).sin(\omega_c)$$
#### Probe 3 - SSB Phasing Generation

Last step, add or subtract $s_1(t)$ with $s_2(t)$ to get the SSB $s(t)$

**Addition**
$$s(t)=s_1(t)+s_2(t)=A_m.A_c.[cos(\omega_m).cos(\omega_c)+ sin(\omega_m).sin(\omega_c)]$$
**Subtraction**
$$s(t)=s_1(t)-s_2(t)=A_m.A_c.[cos(\omega_m).cos(\omega_c)- sin(\omega_m).sin(\omega_c)]$$

## Frequency Domain Analysis

To make our life easier and this process a bit faster we can use the knowledge from the DSBSC section and from the Fourier Analysis Support Knowledge section.

#### Addition
$$S(\omega)=\frac{A_c.A_m.\pi}{2} [ \textcolor{magenta}{\delta(\omega-\omega_m-\omega_c)} + \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) + \textcolor{magenta}{\delta(\omega+\omega_m-\omega_c)} $$
$$ + \delta(\omega-\omega_m+\omega_c) + \textcolor{magenta}{\delta(\omega+\omega_m-\omega_c)} \textcolor{magenta}{- \delta(\omega-\omega_m-\omega_c)} - \delta(\omega+\omega_m+\omega_c)]$$

Recall that we can eliminate the frequencies that are negative from $S(\omega)$ ($\textcolor{magenta}{\text{coefficients in purple}}$):
$$S(\omega)=\frac{A_c.A_m.\pi}{2} [ \delta(\omega-\omega_m+\omega_c) + \delta(\omega+\omega_m+\omega_c) + \delta(\omega-\omega_m+\omega_c) - \delta(\omega+\omega_m+\omega_c)]$$
$$S(\omega)=\frac{A_c.A_m.\pi}{2} [ 2.\delta(\omega-\omega_m+\omega_c)]=A_c.A_m.\pi .[ \delta(\omega-\omega_m+\omega_c)]$$
#### Subtraction
$$S(\omega)=A_c.A_m.\pi .[ \delta(\omega+\omega_m+\omega_c)]$$

![[ssb_phasing_theory.png]]

## Summary

- We get easier suppression results using the phasing method compared with the filtering method.

## References

