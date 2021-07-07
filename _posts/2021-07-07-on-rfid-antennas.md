---
layout: post
title:  Why RFID antennas should be called neither RFID nor antennas ?
---

Today I'm working on the framework of my new website, and I needed some first page to start. I had already some topics to discuss, but they would need some time to prepare something and I wanted something rather quick to start.

Nice topics would include:

* Why a power amplifier on large signal conditions has not only a different impedance than on small signal conditions, but in fact has TWO output impedances.

* Which formula should you use in your Excel spreadsheet to calculate microstrip line impedances.

* Why the filters of Miss X seem to not suffer from the dielectric constant variations of PCB substrates. Hint: the dielectric constant has several values, more to come on this.

But all these topics need time, simulations, and so on. For a starter, I need something quick before I adjust the settings and before I resume the other ideas.

Fortunately, a nice example just felt from the sky.

A friend of mine told me that he was looking for an "expert antenna engineer" to design RFID antennas, but he was not sure he searches well, because the last antenna expert he interview told him that he had designed hundreds of antennad, but never an rfid antenna. Never. Nada.

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
