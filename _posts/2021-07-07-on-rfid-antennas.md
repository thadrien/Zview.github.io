---
layout: post
title:  Why RFID antennas should be called neither RFID nor antennas ?
---

A friend of mine told me that he was looking for an "expert antenna engineer" to design RFID antennas, but he was not sure he searches well, because the last antenna expert he interview told him that he had designed hundreds of antennas, but never an rfid antenna. Never. Nada.

He tried to search on antenna books some information on rfid antenna to orient his search. He was quickly disappointed. He opened the excellent "Electromagnetic Waves and Antennas" [https://www.ece.rutgers.edu/~orfanidi/ewa/](https://www.ece.rutgers.edu/~orfanidi/ewa/) from Orfanidis, and search for RFID and NFC. Nothing! Same thing with "Antenna Theory: Analysis and Design" from Balanis. This starts bad.

The *coup de grâce* comes from [Antenna Theory](https://www.antenna-theory.com/definitions/nfc-antenna.php):

<cite>
Therefore, NFC antennas are not really antennas, in that no one cares about typical antenna parameters, such as the radiation pattern or the antenna gain
</cite>

Here we go! Now, time for more explanations.

## What are antennas ?

That's probably the best question to ask to an antenna expect if you want to be sure that not only he knows his stuff but that he will also be able to explain to you the job you pay him for in terms you are able to understand.

Most science magazines would tell that an antenna is something which "converts a current to a wave". Nothing can be more misleading! First, between the conductors who carry a current, there is already a wave. Second, antennas can also be fed by metallic waveguides, who are not well described by their currents, or by dielectric waveguides, who have NO conduction current at all. Third, it does not explain how the wave emitted or received by an antenna is different from the wave in a cable.

A much better definition would be: "an antenna is a device which converts a guided wave to or from a freely propagating wave".

The wave in the wire which connects a transmitter to an antenna is guided by the wire. Same thing for a metallic or a dielectric waveguide. For the output wave, freely propagating is a very important point: an antenna emits a wave even if there is nothing and just the free space in front of it. In this case, the emitted wave will simply travel during eternity until it meets something. The antenna emits equally well whether there is or not an antenna in front of it.

It's actually a difficulty to measure antenna: to make measurements of an antenna. On the one side, we must put the measured antenna in an enclosure to avoid both disturbance from outside transmitters and to disturb outside receivers. On the other side, the antenna must not see the enclosure walls and only something which look like free space. Metallic enclosures reflect waves and look like a mirror from the antenna point of view. Therefore it must be covered by special materials absorbing electromagnetic waves in order to look like free space.

Something important for the remaining of this article is that the field in the near vicinity of the antenna does not depend whether there is an antenna or nothing far before the antenna.

## What are transformers ?

Transformers are a device made from two coupled coils. In transformers used for power supplies, the coupling is made as strong as possible. The details on the various ways to ensure strong coupling are outside of the scope of this article. When a voltage is applied to the first coil, some current flow in it, just enough to produce a magnetic field which would in turn induce in the coil a voltage equal to the applied voltage, as well as a voltage in the second coil. When nothing is connected to the second coil, no current flows into it. When something is connected to the second coil, it draws a current which changes the magnetic field.
