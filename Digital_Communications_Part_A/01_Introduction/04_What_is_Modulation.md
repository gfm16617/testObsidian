# Introduction
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
maxLevel: 0 # Include headings up to the speficied level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---

I finish the ["The Need for Modulation"]() chapter stating that we need to increase the frequency of our signals, otherwise the antenna size can become impractical to build. 

Modulation is going to be the mechanism to solve that issue and it is the scope of this chapter.

> [!important] 
>  - Remember that the information or signals that we are trying to send are analog, continuous in time, no abrupt changes.
 
![[Diagram_PartA_analog_comms_modulation.png]]

## What is Modulation?

> [!info] 
> Modulation is defined as the process of changing one or more characteristics of the high-frequency carrier signal in proportion with the instantaneous value of the analog information (or digital data) signal.
> 
> - The low-frequency information signal is superimposed over a hight-frequency carrier signal in the process of modulation
> - Modulation translates a low-frequency signal to the pass band of communication channel
> - The analog information signal is also called baseband signal

Ok, there is some information to digest here. Let's plug some visuals.

If we have a high frequency signal, called carrier signal - $c(t)$, we can change 3 parameters in that carrier signal, the amplitude, the frequency and the phase.

Those changes are dictated by an analog information signal or baseband signal.

![[math_pure_carrier.png]]
Later during the math section $c(t)$ will also be expressed in the following way:
$$c(t)=A_c.cos(\omega_c)$$
For simplicity:
- $t$ and $\phi_0$ will be omitted
- $2\pi f_c=\omega_c$

## Types of Analog Modulation Map
![[types_modulation_analog.png]]

## Simulation
![[design_icon.png]]

> [!info] 
>  For all the simulations below, the baseband signal is me using the mouse and controlling the respective parameter in an analog way (or continuous way), no abrupt changes.

Changing the amplitude of the carrier -> Amplitude Modulation
![[carrier_demo_amplitude_change.gif]]

Changing the frequency of the carrier -> Frequency Modulation
![[carrier_demo_frequency_change.gif]]

Changing the phase of the carrier -> Phase Modulation
![[carrier_demo_phase_change.gif]]

![[play_icon.png]] [Falstad Simulation Link](https://tinyurl.com/yvvzbret)
<iframe src="https://tinyurl.com/yvvzbret" width="600" height="600" style="border: 1px solid #ccc" frameborder=0></iframe>

> [!note] 
> **Some observations:**
> - The **amplitude** and **frequency** **changes** on the carrier are **obvious** has I change the baseband signal manually.
> - The **phase changes** are **not** that **obvious** and hard to track.
> - That suggests that changing the phase will not be that useful when the baseband signal is an analog signal.

## Lab Bench

![[lab_icon.png]]
Connecting a function generator to an oscilloscope, we can observe the same simulated results. 
In this case I am connection the Digilent Analog Discovery 2 function generator with a coaxial cable directly to the oscilloscope channel 1.

![[carrier_demo_discovery_connections.png|600]]

On the Waveforms software, I can see the amplitude and frequency changing as I move the sliders accordingly. For the phase, the changes are not visible because of the oscilloscope trigger that it will always sync to the trigger voltage level threshold.

![[carrier_demos_digilent_test.gif]]

## Theory

![[theory_icon.png]]

So what is the math for all of this? 🤔

> [!note] 
> - Consider our analog information or baseband signal or message as $m(t)$
> - $m(t)$ frequency will be much smaller than the carrier's frequency $c(t)$
> - Remember it is the carrier frequency with the baseband signal that we send to the antenna.

## Amplitude Modulation

The amplitude $(A_c)$ of the carrier signal $c(t)$ is varied in proportion to the instantaneous value of the baseband signal $m(t)$.

- Baseband: $m(t)=A_m.cos(\omega_m)$
- Carrier: $c(t)=A_c.cos(\omega_c)$

The simplest form of amplitude modulation (DSBSC) will have the following $s(t)$:
$$A_c=m(t)=A_m.cos(\omega_m)$$
$$s(t)=m(t).c(t)=A_m.cos(\omega_m).cos(\omega_c)$$
> [!info] 
>  In the next section we will explore variations of this amplitude modulation.

## Frequency Modulation

The frequency $(f_c)$ of the carrier signal $c(t)$ is varied in proportion to the instantaneous value of the baseband signal $m(t)$.

- Analog information signal or message: $m(t)=A_m.cos(\omega_m)$
- Carrier: $c(t)=A_c.cos(2\pi f_ct+\phi_i)$

For frequency modulation $s(t)$ will be the following:
$$\phi_i=2\pi k_f\times \int_{}^{}m(t) dt$$
where $k_f$ is called frequency sensitivity factor.
$$s(t)=A_c.cos \left( 2\pi f_ct+2\pi k_f\times \int_{}^{}m(t) dt \right)$$
> [!info] 
>  A decidedly unpleasant looking equation 🤯, but we will cover it in detail later. 

## Phase Modulation

The phase angle $(\phi_0)$ of the carrier signal $c(t)$ is varied in proportion to the instantaneous value of the baseband signal $m(t)$.

- Analog information signal or message: $m(t)=A_m.cos(\omega_m)$
- Carrier: $c(t)=A_c.cos(2\pi f_c t+\phi_i)$

For analog phase modulation $s(t)$ will be the following:
$$\phi_i=k_p\times m(t)$$
where $k_p$ is called phase sensitivity factor.
$$s(t)=A_c.cos(2\pi f_ct+k_p.m(t))$$
> [!info] 
>  $m(t)$ is barely used as an analog signal but this equation will be useful and important when the baseband signal becomes digital.

## References
