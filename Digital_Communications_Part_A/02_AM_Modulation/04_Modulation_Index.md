---
tags:
  - am_modulation
---
# Modulation Index
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
maxLevel: 0 # Include headings up to the speficied level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---
## Analytical Approach
![[theory_icon.png]]

Modulation index $(m_a)$ is the ratio of the maximum amplitude of the modulating signal $(A_m)$ and the maximum amplitude of the carrier signal $(A_c)$ and defines the quality of the AM signal transmitted.
$$m_a=\frac{A_m}{A_c}$$

It is also known as depth of modulation, coefficient of modulation, degree of modulation, modulation factor, or amplitude sensitivity. It describes the amount of change in amplitude present in AM waveform.

It can also be viewed on the oscilloscope as the ratio between amplitudes $P$ and $Q$ 
$$m_a=\frac{P-Q}{P+Q}$$

![[modulation_index_graph.png]]

> [!note] 
> **Example**
> $P$ calculation:
> - $P_{max}=4V$
> - $P_{min}=-4V$
> - $P=P_{max}-P_{min}=8V$
> 
> $Q$ calculation:
>  - $Q_{upper}=2V$
>  - $Q_{lower}=-2V$
>  - $Q=Q_{upper}-Q_{lower}=4V$
>    
> Final Result
> $m_a=\frac{P-Q}{P+Q}=\frac{8-4}{8+4}=1/3$
> $m_a<1$

When the amplitude modulation index, $m_a$ is greater than one, the AM signal is said to be overmodulated.

An overmodulated signal on the oscilloscope looks like this:

![[overmodulation_graph_example.png]]

> [!note]
> **Example**
> $P$ calculation:
> - $P_{max}=4V$
> - $P_{min}=-4V$
> - $P=P_{max}-P_{min}=8V$
> 
> $Q$ calculation:
> Notice on how the upper and lower envelopes are swapped for overmodulated signals
>  - $Q_{upper}=2V$
>  - $Q_{lower}=-2V$
>  - $Q=Q_{lower}-Q_{upper}=-4V$
>    
> Final Result
> $m_a=\frac{P-Q}{P+Q}=\frac{8-(-4)}{8-4}=$ 3
> $m_a>1$

The two methods of modulation index described above are based on an analytical approach and are easy to use when $m(t)$ is a periodic signal. However, when using non period signals such as speech, observing the modulated signal on the oscilloscope can be a challenge.

There are a couple of other methods that can help visualize the modulation index.

![[modulation_index_methods.png]]

## Trapezoidal Pattern

The trapezoidal pattern is a quite useful tool to measure modulation characteristics, such as, modulation index, percent modulation, coefficient of modulation, and modulation symmetry for signal that are non periodic.

It is simply an XY oscilloscope rendering, with the x axis equal to $m(t)$ and the y axis equal to $s(t)$.

![[trapezoidal_test_setup_block_diagram.png]]

## DSBSC Example

#### Example for $(m_a=1)$

**XY Scope**
![[dsbsc_ma_1_trapezoid.png]]

**Time Domain - DC Component**
![[dsbsc_ma_1_time.png]]

## DSBFC Examples

#### Example for $(m_a=1)$

**XY Scope**
![[dsbfc_ma_1_trapezoid.png]]

**Time Domain - DC Component**
![[dsbfc_ma_1_time.png]]

#### Example for $(m_a<1)$

**XY Scope**
![[dsbfc_ma_less_1_trapezoid.png]]

**Time Domain - DC Component**
![[dsbfc_ma_less_1_time.png]]

#### Example for $(m_a>1)$ (Overmodulated)

**XY Scope**
![[dsbfc_ma_great_1_trapezoid.png]]

**Time Domain - DC Component**
![[dsbfc_ma_great_1_time.png]]

## Audio Examples

The hardware was wired has an DSBFC modulation. Then I connected the phone audio output to $m(t)$ and played some songs and radio stations from the phone.

To see the effect of overmodulation, in this case, it was easier to move the DC component of $m(t)$ to displace the baseband signal accordingly.

**Radio Station Example**
![[dsbfc_radio_playing.gif]]

**Techno Song Playing**
![[dsbfc_techno_playing.gif]]

Notice that we can observe when overmodulation happens:
- by looking at the trapezoid pattern and match with the pattern when $m_a>1$
- and by looking at the spectrum and seeing the carrier frequency magnitude reduce significantly to the point that the sidebands magnitudes start being more prevalent. 

**Modulation Index $m_a>1$ (Overmodulation)**
![[dsbfc_audio_ma_great_1.png]]

**Modulation Index $m_a<1$**
![[dsbfc_audio_ma_less_1.png]]

**Modulation Index $m_a=1$**
![[dsbfc_audio_ma_1.png]]

## References

