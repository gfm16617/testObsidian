---
tags:
  - am_modulation
---
# SSB
---
## Single Sideband

![[types_ssb_map.png]]

Comparing the two communications systems from the previous chapters, DSBSC offers considerable power savings over DSBFC because the carrier is not transmitted.

However, both systems generate and transmit two sidebands around the carrier and so they have the same bandwidth as each other.

As far as the transmission of information is concerned using amplitude modulation the transmission of one sideband is necessary. This means that no information will be lost by suppressing the carrier and one of the two sidebands of AM signal. 

This is essential SSB transmission, a form of amplitude modulation in which the carrier is fully suppressed and one of the sidebands (lower or upper) is also suppressed.

In transmitting only one sideband, SSB requires only half the bandwidth of DSBSC and DSBFC which is a significant advantage.

Essentially you can find at least 3 different ways to generate SSB signals:
- Selective filtering
- Phasing method
- Weaver's method

Which one should you pick? 🤔

I believe the answer to this question boils down to, what hardware do you available, and the cost and complexity of each solution.

We are going to explore these 3 methods (no preference on the order) with the goal to familiarize the reader with them.
