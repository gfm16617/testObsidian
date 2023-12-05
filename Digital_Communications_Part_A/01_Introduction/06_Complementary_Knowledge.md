# Complementary Knowledge
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
maxLevel: 0 # Include headings up to the speficied level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```
---
## Antenna Resonance

Before explaining resonance, I am going to introduce briefly the concept of maximum power transfer. It requires a bit of circuit knowledge but I will do my best to keep things simple. No equations will be involved here, just simple circuit simulation to understand the concept.

Consider the circuit below with a DC voltage supply and two resistors connected in series. This is the typical circuit example that is used to show what value of RL should be picked in order to have maximum power transfer.

The graph is showing the power transfer to RL over time by varying RL from 3.9 $\ohm$ to 150k$\ohm$. Notice on how we get a maximum value of power when RL = 1k$\ohm$ 🤔

![[play_icon.png]] [Falstad Simulation Link](https://tinyurl.com/ynreotxc)
<iframe src="https://tinyurl.com/ynreotxc" width="500" height="500" style="border: 1px solid #ccc" frameborder=0></iframe>

![[simple_resistive_circuit_power_example.gif]]

That is exactly what the maximum power transfer theorem or "Jacobi's law" states:

> [!quote] 
>  To obtain maximum external power from a power source with internal resistance, the resistance of **the load must equal the resistance of the source** as viewed from its output terminals.
>  - Mortiz von Jacobi (1840)

And it even works if the source is an AC signal.

![[play_icon.png]] [Falstad Simulation Link](https://tinyurl.com/yofyyxbd)
![[simple_resistive_circuit_ac_example.gif]]

The math to validate this statement is outside the scope of this article. But feel free to explore it further [(Support Link)](https://en.wikipedia.org/wiki/Maximum_power_transfer_theorem).

Another small experiment that we need to be familiar with is the LC circuit, which consist on connecting an capacitor and inductor with each other.

![[LC_circuit_noPower.png|400]]

> [!info] 
>  Remember this, resistors dissipate energy, capacitors and inductors store energy. Capacitors store energy in terms of electric fields, and inductors store energy in terms of magnetic fields.

If you charge this system with an initial energy, and remove the power supply from the circuit, you will observe the capacitor and inductor exchanging energies back and forth.

![[play_icon.png]] [Falstad Simulation Link](https://tinyurl.com/yvpzt93e)
![[LC_Simulation.gif]]

The simulation above is an ideal simulation where resistors are not present in the circuit. In reality this oscillation will die over time because there are either parasitic resistances or resistors that are part of the circuit.

![[RLC_simulation.gif]]
[Falstad Simulation Link](https://tinyurl.com/yvacejvc)

Now let's play with this RLC circuit a little bit more and let's connect an AC input voltage in the system and keep the switch close all the time. I am also going to connect a ammeter that monitors the current from that voltage source.

![[RLC_AC_source_notrunning.png]]

Let's vary the input frequency from 10Hz to 80Hz and observer the current that the AC source delivers to the RLC circuit (yellow trace plot).

![[play_icon.png]] [Falstad Simulation Link](https://tinyurl.com/yktz3n4x)
![[RLC_resonance_example_1.gif]]

Notice that around 40.8Hz the current is around 2.5mA (minimum value).

> [!important] 
>  Voila you just observed resonance 🤯

> [!quote] 
>  Resonance is a phenomenon that occurs when an object or system is subjected to an external force or vibration that matches its natural frequency.

In our case we subjected the RLC circuit to external vibrations and at around 40.8Hz we notice that the current delivered by the AC source was minimum indicating that we matched the natural frequency of the RLC circuit.

The resonance frequency equation of an RLC circuit is the following:
$$f_r=\frac{1}{2\pi \sqrt{L.C}}$$
If we plug the values of our parameters in this equation we get an $f_r=41Hz$, pretty close to what we observed 🙂

Another observation that we can make is, since the current that we are measuring is minimum at resonance, that suggests that the RLC circuit at resonance has a high output impedance.

To validate this argument, if we connect a load resistance (RL) in parallel with the RLC circuit, we can see RL dictating the current in the circuit.

![[play_icon.png]] [Falstad Simulation Circuit](https://tinyurl.com/yo2qdsaq)
![[RLC_resonance_with_load.gif]]

> [!note] 
>  At resonance the impedance of the RLC circuit is completely resistance.

Going back to the antenna, we can derive a circuit model like the one below.

**Missing Circuit**

## References

https://control.com/textbook/ac-electricity/antennas/
https://control.com/textbook/ac-electricity/transmission-lines/
