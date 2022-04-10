---
layout: post
title: Design of a coaxial power combiner with low-impedance inputs and increased isolation.
permalink: /posts/coax-combiner-low-Z-isolation.html
last_modified_at: 2022-04-02 12-59
---

Hadrien Theveneau, Christophe Gaquière, Romain Lenglet, Matthieu Werquin, Jean-Christophe Joly, and Stéphane Tortel

<p class="begin-note" markdown="1">This post is a mix between an unpublished long article, an article published in IEEE MWCL[^theveneau2017spatial], and further additions. Original articles by the authors in front of this post, revisions by the first author.</p>

<summary>
This article describes the design, fabrication and measurement of a 2.5&#8239;Ω, 8-way, 1&#8239;&ndash;&#8239;6&#8239;GHz spatial power combiner using an absorbing material to increase the isolation. Insertion losses are lower than 1.8&#8239;dB in the 1&#8239;&ndash;&#8239;6&#8239;GHz band, except for a few peaks. Isolation is at least 10&#8239;dB for 45° input pairs and better than -15&#8239;dB for other pairs. This is the first power combiner to provide wide bandwidth, high isolation, and low input impedances at the same time.
</summary>

## Introduction

More and more applications need to generate very high power pulsed microwave signals, in the order of tens of kilowatts: radars, EM warfare, and so on. These powers are traditionally generated with hyperfrequency tubes: magnetrons, klystrons, TWT, and so on. However, these techniques can have several major drawbacks: poor reliability, short lifespan, fragility, complex waveforms generation difficult and difficult power supplies.

Gallium nitride (GaN) transistors can provide a solution to these problems. However, the output power of a single transistor unit is insufficient for such applications. Efficient power combining schemes must be used to provide needed output power.

However, current solutions have limitations. Spatium<sup>&reg;</sup> power combiners[^jia2003broadband]<sup>,</sup>[^jia2003broadband2] confine the amplifiers inside the structure, which makes thermal cooling difficult. Combiners using probes in linear waveguides[^li2008planar], coaxial waveguides[^deVilliers2008design]<sup>,</sup>[^song2009planar], or radial waveguides[^song2008broadband] have low losses but their bandwidth is lower than 50&#8239;% and are not practical for lower frequencies like 1&#8239;GHz. These solutions also lack isolation between the inputs, which can lead to instability and failure propagation problems. Waveguide combiners[^chu2015isolated] have low losses and isolate their inputs, but they also have bandwidth limitations, and are bulky for lower frequencies. All of the previously mentioned solutions have high-impedance inputs (50&#8239;Ω), difficult to match on the low impedances (≈&#8239;2.5&#8239;Ω) of GaN power transistors on large bandwidths

In this article, an innovative spatial power combiner with high bandwidth, isolation between its inputs and low input impedance is designed, manufactured, and measured. [Section I](#sec-even-odd-modes-analysis) presents a theoretical analysis of the lack of isolation of traditional power combiners, [section II](#sec-CAD-overview) presents the general architecture of this new combiner, [section III](#sec-equivalent-schematics) presents equivalents schematics in even and odd modes, [section IV](#sec-impedance-preadaptation) shows the structure of impedance prematching used to have low-impedances inputs, [section V](#sec-transition-calculation) gives the complete procedure to calculate the shape of the impedance transition, and [section VI](#sec-EM-simulation-results) discusses measurement and simulation results.

<!-- Section removed from IEEE MWCL article -->

## I. Even and odd modes analysis of power combiners {#sec-even-odd-modes-analysis}

We will show in this section that the lack of isolation of power combiners without an isolation mechanism is linked to the reflection of the odd modes.

Fig.&#8239;1. <!--~\ref{fig:sch:general-even-odd}--> shows the even and odd mode excitations of a power combiner without isolation mechanism. In the even mode, the power of the inputs goes to the output. If the impedance matching is correct, no output is reflected to the inputs and they don't see each other. However, in symmetrical odd modes, due to symmetry, the output is connected to a virtual ground. The input waves are totally reflected. This reflection is the cause of the lack of isolation between the inputs. To provide isolation between the inputs, we need to find a way to absorb this reflection. Similar analysis is done in \[[^yau1986new]\]  and \[[^nagai1977nway]\] for combiners using several discrete resistors.

<figure>
  <img class="dark-mode-invert" src="{{ '/posts/coax-combiner-low-Z-isolation/general-even-odd-v3.svg' | relative_url }}" title="General even and odd mode excitations of a power combiner.">
  <figcaption>Fig.&#8239;1. General even and odd mode excitations of a power combiner.</figcaption>
</figure>

<!-- Could be removed if short version needed -->
Mathematically, for a combiner with rotational symmetry, the input modes matrix is given by:

<latexmath>
  M = \begin{pmatrix}
    \; 1      & 1                        & 1                     & \dots                         & 1                                       \\
    \; 1      & e^{\frac{j 2 \pi}{N}}    & e^{\frac{j 4 \pi}{N}} & \dots                         & e^{\frac{j 2 (N - 1) \pi}{N}}           \\
    \; 1      & e^{\frac{j 4 \pi}{N}}    & e^{\frac{j 8 \pi}{N}} & \dots                         & e^{\frac{j 4 (N - 1) \pi}{N}}           \\
    \; \vdots & \vdots                   & \vdots                & \ddots                        & \vdots                                  \\
    \; 1      & e^{\frac{j 2 (N - 1) \pi}{N}}                    & e^{\frac{j 4 (N - 1) \pi}{N}} & \dots & e^{\frac{j 2 (N - 1)^2 \pi}{N}} \\
  \end{pmatrix}
</latexmath>

where N is the number of inputs. The first column is the normal combining mode, the even mode, while the other columns are the odd modes.

For example, for 2 and 4 inputs, M is given by:
<latexmath>
  M_2 = \begin{pmatrix}
    \; 1 & \phantom{-}1 \\
    \; 1 & -1           \\
  \end{pmatrix}
  \qquad
  M_4 = \begin{pmatrix}
    \; 1 & \phantom{-}1 & \phantom{-}1 & \phantom{-}1 \\
    \; 1 & \phantom{-}j & -j & -1                     \\
    \; 1 & -1 & -1            & \phantom{-}1          \\
    \; 1 & -j & \phantom{-}j  & -1                    \\
  \end{pmatrix}
</latexmath>

The inverse of M is given by:
<latexmath>
  M^{-1} = \begin{pmatrix}
    \; 1   & 1                              & 1                              & \dots  & 1                                   \\
    \; 1   & e^{\frac{- j 2 \pi}{N}}        & e^{\frac{- j 4 \pi}{N}}        & \dots  & e^{\frac{- j 2 (N - 1) \pi}{N}}     \\
    \; 1   & e^{\frac{- j 4 \pi}{N}}        & e^{\frac{- j 8 \pi}{N}}        & \dots  & e^{\frac{- j 4 (N - 1) \pi}{N}}     \\
    \vdots & \vdots                         & \vdots                         & \ddots & \vdots                              \\
    \; 1   & e^{\frac{-j 2 (N - 1) \pi}{N}} & e^{\frac{-j 4 (N - 1) \pi}{N}} & \dots  & e^{\frac{-j 2 (N - 1)^2 \pi}{N}} \; \\
  \end{pmatrix}
</latexmath>

By splitting the input excitation in even and odd modes, the isolation can be calculated as following :

<latexmath>
  S_{l,k} = \sum_{m = 1}^{N}{\frac{1}{N} e^{\frac{j 2 (l - 1) (m - 1) \pi}{N}} \Gamma_m e^{\frac{- j 2 (k - 1) \pi}{N}}}, \qquad l \neq k
</latexmath>

where <asciimath>Gamma_m</asciimath> is the reflexion coefficient for the odd mode number m. This equation shows that, when the odd mode matching gets better, the isolation also does. It should be noted that this equation has the same rotational symmetry than the power combiner.

## II. Overview of the combiner {#sec-CAD-overview}

<!-- Note : "Standard" was added to avoid "Fig 2. 50 Ω" which doesn't look like good. -->
The mechanical layout of the power combiner is presented in Fig.&#8239;2. <!-- ~\ref{fig-power-combiner-CAD} --> and Fig.&#8239;3. Standard 50&#8239;Ω connectors are present for measurement purposes, but this combiner is designed for 2.5&#8239;Ω inputs. These connectors will be eventually replaced by amplifier modules with low impedance outputs.

<figure>
  <img src="{{ '/posts/coax-combiner-low-Z-isolation/CAD-annotations-single-col-with-png.svg' | relative_url }}" title="CAD model of the power combiner. The 50&#8239;Ω SMA input connectors used for the measurements will be replaced by 2.5&#8239;Ω amplifier modules to reach high output powers.">
  <figcaption>Fig.&#8239;2. CAD model of the power combiner. The 50&#8239;Ω SMA input connectors used for the measurements will be replaced by 2.5&#8239;Ω amplifier modules to reach high output powers.</figcaption>
</figure>

<figure>
  <img src="{{ '/posts/coax-combiner-low-Z-isolation/CAD-zoom-1-v2-with-png.svg' | relative_url }}" title="Details of the entrance of the combining section.">
  <figcaption>Fig.&#8239;3. Details of the entrance of the combining section.</figcaption>
</figure>

Impedance prematching networks raise the input impedance from 2.5&#8239;Ω to 50&#8239;Ω. This provides a sufficiently high impedance at the start of the combining section to avoid short distances between the inner part of this section and the outer part. Without the prematching, this distance would be on the order of 120&#8239;µm, which is very difficult to manufacture. With the prematching, this distance is between 0.8 and 1.9 mm, which is much easier to manufacture.

The actual combining[^footnote1] begins after the prematching. The first part of the combiner is a coaxial structure containing several copper lines around an absorber material. This provides isolation between the inputs by adding some loss mechanism for the odd modes. Without this, the odd modes would be reflected back to the inputs, and this would cause the poor isolation found in lossless combiners. This absorber is similar to the resistor in Wilkinson combiners[^microwaves101wilkinson]<sup>,</sup>[^cohn1968broadband]<sup>,</sup>[^wilkinson1960divider]<sup>,</sup>[^yau1986new], but its distributed operation provides an higher bandwidth.

Inside the absorber, there is a metal core connected to the body of the combiner. This provides a return path for the heat generated into the combiner. This metal core increases insersion losses of the combiner, particularly in the low frequency range, but this effect is low. Without this return path, the combiner would not be able to sustain high powers. Additionally, this structure allows mechanical sustaining.

The shape of the combining section is precisely calculated to ensure impedance matching between the inputs and the output. This calculation will be described in [section V](#sec-transition-calculation)

At the exit of the combining section, there is one transition between air and PEHD, and one transition in diameter. No impedance matching is performed in these transitions: they have no electric function and are purely mechanical. The PEHD is here to ensure the positioning of the core inside the coaxial structure. The output coaxial connector alone would be insufficient to provide enough mechanical strength. Both transitions were optimized in separate EM simulations.

A CAD of the combiner with the power amplifier modules is shown in Fig.&#8239;4. <!-- ~\ref{fig-power-combiner-CAD-with-modules} --> A dummy circuit is shown in the figure to make mechanical CAD easier. Special care was taken with the cooling of the modules because the average lifespan of a GaN transistor is divided by 2 for each 6~°C increase in temperature. Unlike Spatium<sup>&reg;</sup> power combiners[^jia2003broadband]<sup>,</sup>[^jia2003broadband2], where the power amplifiers MMICs are trapped inside the structure, the transistors are mounted on the outer part and thus can be more easily cooled. The overall structure is contained in a 333&times;322&times;286&times;mm<sup>3</sup> volume.

<figure>
  <img src="{{ '/posts/coax-combiner-low-Z-isolation/CAD-with-modules.png' | relative_url }}" style="width:50%;" title="CAD of the combiner with power amplifier modules. Special care is given to the air cooling.">
  <figcaption>Fig.&#8239;4. CAD of the combiner with power amplifier modules. Special care is given to the air cooling.</figcaption>
</figure>

## III. Equivalent schematics in even and odd modes {#sec-equivalent-schematics}


The simplest method to analyse this power combiner is to use two separate schematics for the even mode and the odd modes, as shown in Fig.~\ref{fig-sch-even-odd-combiner}.

The prematching section behaves in exactly the same way in the even and the odd modes. Its equivalent schematic is a transmission line of continuously variable impedance. Its structure will be detailed in Fig.&#8239;7. <!--~\ref{sec-impedance-preadaptation}-->

<!--
% See this: http://texblog.net/latex-archive/graphics/includegraphics-top-align/
\begin{figure}
\myfloatalign
\subfloat[]{ %
    \begin{minipage}[t]{0.40\columnwidth}%
        \vspace{0pt}%
        \includegraphics[width=\columnwidth]{mode-1-field.png}%
    \end{minipage}%
    \label{fig-plt-even-mode}}%
\qquad%
\subfloat[]{ %
    \begin{minipage}[t]{0.40\columnwidth}%
        \vspace{0pt}%
        \includegraphics[width=\columnwidth]{mode-2-field.png}%
    \end{minipage}%
    \label{fig-plt-mode-2}}\\%
\subfloat[]{ %
    \begin{minipage}[b]{0.40\columnwidth}%
        \vspace{0pt}%
        \includegraphics[width=\columnwidth]{mode-3-field.png}%
    \end{minipage}%
    \label{fig-plt-mode-3}}%
\qquad%
\subfloat{ %
    \begin{minipage}[b]{0.40\columnwidth}%
    \centering%
    \begin{tikzpicture}%
        \node[anchor=south west,inner sep=0] (image) at (0,0) {\includegraphics[width=0.2cm]{modes-scale-colors.png}};%
        \begin{scope}[x={(image.south east)},y={(image.north west)}]%
            \draw (0,0)       -- (0,1) -- (1,1) -- (1,0) -- cycle;%
            \draw (0.0,0)     -- (-0.5,0)     node[left] {\scriptsize  1\,000};%
            \draw (0.0,0.091) -- (-0.5,0.091) node[left] {\scriptsize  3\,044};%
            \draw (0.0,0.180) -- (-0.5,0.180) node[left] {\scriptsize  5\,564};%
            \draw (0.0,0.271) -- (-0.5,0.271) node[left] {\scriptsize  8\,670};%
            \draw (0.0,0.361) -- (-0.5,0.361) node[left] {\scriptsize  12\,500};%
            \draw (0.0,0.453) -- (-0.5,0.453) node[left] {\scriptsize  17\,222};%
            \draw (0.0,0.543) -- (-0.5,0.543) node[left] {\scriptsize  23\,043};%
            \draw (0.0,0.635) -- (-0.5,0.635) node[left] {\scriptsize  30\,219};%
            \draw (0.0,0.724) -- (-0.5,0.724) node[left] {\scriptsize  39\,067};%
            \draw (0.0,0.816) -- (-0.5,0.816) node[left] {\scriptsize  49\,974};%
            \draw (0.0,0.905) -- (-0.5,0.905) node[left] {\scriptsize  63\,421};%
            \draw (0.0,1)     -- (-0.5,1)     node[left] {\scriptsize  80\,000};%
            \draw (0.5,1.02) node[above] {V\cdot m\textsuperscript{-1} (log)};%
        \end{scope}%
    \end{tikzpicture}%
    \end{minipage}}%
\caption{\added{Electric field of propagation modes in point A of the combiner: even mode (a) and two odd modes (b) and (c). The inner core is removed to simplify the calculation, see \cite{theveneau2017amplificateurs} for more details.}\removed{ Electric field in a simplified model of the first part of the combiner without inner metal core, in the even mode (a) and in the first two odd modes (b) and (c) excitations.}}
\label{fig-plt-even-odd-modes}
\end{figure}
-->

<figure>
  <table>
    <tbody>
      <tr>
        <td>
          <img src="{{ '/posts/coax-combiner-low-Z-isolation/even-odd-modes-mode-1-field.png' | relative_url }}" title="Even mode." alt="Even mode.">
        </td>
        <td>
          <img src="{{ '/posts/coax-combiner-low-Z-isolation/even-odd-modes-mode-2-field.png' | relative_url }}" title="Odd mode 1." alt="Odd mode 1.">
        </td>
      </tr>
      <tr>
        <td>
          <img src="{{ '/posts/coax-combiner-low-Z-isolation/even-odd-modes-mode-3-field.png' | relative_url }}" title="Odd mode 2." alt="Odd mode 2.">
        </td>
        <td>
          <img src="{{ '/posts/coax-combiner-low-Z-isolation/even-odd-modes-scale-colors.svg' | relative_url }}" style="height:200px;" title="Color scale." alt="Color scale.">
        </td>
      </tr>
    </tbody>
  </table>
  <figcaption>Fig.&#8239;5. Electric field of propagation modes in point A of the combiner: even mode (a) and two odd modes (b) and (c). The inner core is removed to simplify the calculation, see <span markdown="1">\[[^theveneau2017amplificateurs]\]</span> for more details.</figcaption>
</figure>

In the even mode, as shown in Fig.&#8239;5a<!--~\ref{fig-plt-even-mode}-->, the strips have the same potential and almost no field goes into the absorber. The lines have low losses and the even mode is transmitted from point A to point B. The rest of the combiner, made with a full metal core, completes the impedance transformation, which was started in the prematch section. The heat spreader behaves approximately like a shunt inductor. This mode is the normal combing mode.

In contrast, in the odd modes, as shown in Fig.&#8239;5b<!--\ref{fig-plt-mode-2}--> and Fig.&#8239;5c<!--\ref{fig-plt-mode-3}-->, the strips do not have the same potential and lots of electric field goes into the absorber. The lines have high losses and the odd modes are highly attenuated from point A to point B.

In the odd modes, due to symmetry, point B behaves like a virtual ground. The heat spreader can be removed from the odd modes' equivalent schematic because it is connected to the virtual ground. Without the absorber, the odd mode would be reflected towards the inputs. This reflection would cause a lack of isolation. With the absorber, the reflection of the odd modes is strongly attenuated, which increases isolation between the inputs. This absorber has the same function as the resistor in Wilkinson combiners[^microwaves101wilkinson]<sup>,</sup>[^cohn1968broadband]<sup>,</sup>[^wilkinson1960divider]<sup>,</sup>[^yau1986new], but its distributed operation provides higher bandwidths.

<figure>
  <img src="{{ '/posts/coax-combiner-low-Z-isolation/combiner-even-odd-v12-with-png-web.svg' | relative_url }}"  style="width:100%;" title="Equivalent schematic of the power combiner in the even mode and in the odd modes." alt="Equivalent schematic of the power combiner in the even mode and in the odd modes.">
  <figcaption>Fig.&#8239;6. Equivalent schematic of the power combiner in the even mode and in the odd modes.</figcaption>
</figure>
<!-- \label{fig-sch-even-odd-combiner} -->

## IV. Impedance prematch {#sec-impedance-preadaptation}

<figure>
  <img src="{{ '/posts/coax-combiner-low-Z-isolation/preadaptation-2D-3D-v3-web.svg' | relative_url }}" style="width:100%;" title="Section of the impedance prematch structure (not to scale) and 3D view." alt="Section of the impedance prematch structure (not to scale) and 3D view.">
  <figcaption>Fig.&#8239;7. Section of the impedance prematch structure (not to scale) and 3D view.</figcaption>
</figure>
<!-- \label{fig-preadaptation-2D} -->

This combiner has an impedance preadaptation from 2.5&#8239;Ω to 50&#8239;Ω to make the manufacturing easier. This adaptation cannot be performed with a microstrip line on substrate with constant thickness. The 2.5&#8239;Ω low impedance side has a limited width because, otherwise, higher order modes would propagate. Using high-k substrates is not a solution because they would reduce the maximal width relative to the propagation of higher order modes. This forces the use of a thin substrate. However, a thin substrate forces the use of a narrow strip on the 50&#8239;Ω high impedance side, limiting the power handling and increasing the losses.

We need some way to change the thickness of the substrate. Using multiple substrates can be difficult for the manufacturing. A continuous variation of the thickness of the substrate would be difficult to manufacture. This is why we use a defective ground plane[^arbabi2006increase]<sup>,</sup>[^boutejdar2008miniaturized]<sup>,</sup>[^schlieter2009designing]<sup>,</sup>[^lim2013defected]. Fig.&#8239;7. <!--\ref{fig-preadaptation-2D}--> shows the structure of the impedance preadaptation. The ground plane is progressively opened to increase the "effective substrate height". The ground plane is opened before the strip width is reduced to have minimal losses. Impedance in function of dimensions is computed using the mode solver of CST Microwave Studio<sup>&reg;</sup>.

## V. Calculation of impedance transition {#sec-transition-calculation}

After the manufacturing of this combiner, the author learned that instead of a Klopfenstein transform followed by a postprocessing to remove the discontinuities, an Hecken transform should have been used instead. Hence, the first section presents what was done and the seconde section presents what should have been done instead.

### V.I. Current calculation with Klopfenstein

A Klopfenstein impedance transition[^pozar2012microwave]<sup>,</sup>[^klopfenstein1956transmission]<sup>,</sup>[^collin1956optimum]<sup>,</sup>[^kajfez1973correction]<sup>,</sup>[^microwaves101klopfenstein]<sup>,</sup>[^ning2013spatial] is used for this power combiner. The impedance preadaptation and the combining sections together make a single Klopfenstein impedance transition. Putting two Klopfenstein transitions in series would have been easier to calculate, but this would have increased the length and the losses of the overall structure.

The preadaptation section is the 2.5&#8239;Ω to 50&#8239;Ω part of a Klopfenstein transition going from 2.5&#8239;Ω to 8&times;50=400&#8239;Ω. The combining section is the 50/8=6.25&#8239;Ω to 50&#8239;Ω part of a 2.5/8=0.31&#8239;Ω to 50&#8239;Ω Klopfenstein transition. Both transitions are identical besides a multiplication of the impedance by 8, the number of the lines. This is because, in the prematching section, the impedance is the impedance of a single line, while in the combining section the impedance is the common-mode impedance of all the lines in parallel. Klopfenstein transitions are much discussed in literature[^pozar2012microwave]<sup>,</sup>[^klopfenstein1956transmission]<sup>,</sup>[^collin1956optimum]<sup>,</sup>[^kajfez1973correction]<sup>,</sup>[^microwaves101klopfenstein]<sup>,</sup>[^ning2013spatial], but some points deserve special attention. The following procedure is used for the calculation:

1) Impedances Z(y) are calculated in function of the normalized position y in range [-1;1] using standard formulas for Klopfenstein transitions[^pozar2012microwave]<sup>,</sup>[^pozar2012microwave]<sup>,</sup>[^klopfenstein1956transmission]<sup>,</sup>[^collin1956optimum]<sup>,</sup>[^kajfez1973correction]<sup>,</sup>[^microwaves101klopfenstein]<sup>,</sup>[^ning2013spatial].

2) An affine transformation was performed on <asciimath>ln(Z_0)</asciimath> to remove start and end discontinuities.

3) The electrical length of the transition, <asciimath>theta_min</asciimath> is calculated. Usual formulas[^pozar2012microwave]<sup>,</sup>[^klopfenstein1956transmission]<sup>,</sup>[^collin1956optimum]<sup>,</sup>[^kajfez1973correction]<sup>,</sup>[^microwaves101klopfenstein] in literature are no longer valid because the small-reflection hypothesis[^pozar2012microwave]<sup>,</sup>[^klopfenstein1956transmission] is not valid outside the passband due to the high impedance transformation ratio. This ratio is 160 for this combiner, while it is only 32 in Spatium<sup>&reg;</sup> power combiners and 1.5 in original Klopfenstein paper.

<!-- <asciimath> at beginning of a paragraph not recognized as inline, force <p>. -->
<p><asciimath>theta_min</asciimath> is calculated by a numerical search of the smallest <asciimath>theta</asciimath> such as <asciimath>rho(theta) < rho_max</asciimath>, where <asciimath>rho(theta)</asciimath> is calculated by numerical integration for y from 1 to -1 of the following differential equation:</p>

<latexmath>
  \begin{equation*}
    \frac{\mathrm{d}\rho}{\mathrm{d}y} = j \cdot \Theta \cdot \rho - \frac{1}{2} \cdot \left(1 - \rho\right) \cdot \frac{\mathrm{d}\ln\left(Z_0\right)}{\mathrm{d}y}
  \end{equation*}
</latexmath>

4) The calculated impedances <asciimath>Z_0(y)</asciimath> are cut from 2.5&#8239;Ω (0.31&#8239;Ω) to 50&#8239;Ω (0.63&#8239;Ω) for the prematching and from 50&#8239;Ω (0.63&#8239;Ω) to 400&#8239;Ω (50&#8239;Ω) for the remaining of the combiner.

5) A table of the <asciimath>Z_0</asciimath> and <asciimath>K_{eff}</asciimath> in function of the transverse dimensions is calculated by EM simulation. The transverse dimensions is the ground plane opening for the first part of the preadaptation section, the microstrip line width for its second part, and the inner part diameter for the coaxial part. CST Microwave Studio<sup>&reg;</sup> is used for this calculation.

6) Profile transverse dimensions are calculated from <asciimath>Z_0(y)</asciimath> by numerical interpolation of the table calculated in step 6. Effective}dielectric constant <asciimath>K_{eff}</asciimath>, which depends on the profile dimensions, is calculated in the same step.

7) Position z is calculated from <asciimath>K_{eff}(y)</asciimath> with:
{% comment %}
  <asciimath>
    z = int_{y=-1}^{1} (Theta_min c)/(4 pi f_min sqrt(K_eff(y)))
  </asciimath>
{% endcomment %}
<latexmath>
  z= \int\limits_{y=-1}^{1}{\frac{\Theta_\text{min} \cdot c}{4 \cdot \pi \cdot f_\text{min} \cdot \sqrt{K_\text{eff}(y)}} \cdot \mathrm{d}y} \label{eqn-z}
</latexmath>
by numerical integration. Fig.&#8239;8. <!-- ~\ref{fig-Klopfenstein} --> shows the variation of the different parameters of the transition.

8) The number of points is reduced from 2001 to fewer than 20 points using an iterative end-point fit algorithm. This simple step is very important. Without this step, the mesher would not be able to mesh the structure for numerical simulation. This also helps manufacturing a lot.

<figure>
  <img class="dark-mode-invert" src="{{ '/posts/coax-combiner-low-Z-isolation/Klopfenstein.svg' | relative_url }}" style="width:100%;" title="Impedance Z0, effective dielectric constant Keff, and profiles of both impedance preadaptation and coaxial sections. They make a single Klopfenstein transition." alt="Impedance Z0, effective dielectric constant Keff, and profiles of both impedance preadaptation and coaxial sections. They make a single Klopfenstein transition.">
  <figcaption>Fig.&#8239;8. Impedance Z<sub>0</sub>, effective dielectric constant K<sub>eff</sub>, and profiles of both impedance preadaptation and coaxial sections. They make a single Klopfenstein transition.</figcaption>
</figure>
<!-- \label{fig-Klopfensteinr} -->

### V.I. Correct calculation with Hecken method

Instread of a modified Klopfenstein transition, the calculation method can be updates to use an Hecken transition. For this, at step 1, <asciimath>Z(y)</asciimath> should be calculated using the Hecken method. <!-- FIXME: add references. -->

## VI. Simulation and measurement results {#sec-EM-simulation-results}

To validate the performance of the design before manufacturing, we perform a global electromagnetic simulation. The model includes the initial microstrip lines, the impedance prematching, the combiner itself and the final diameter reduction. SMA input connectors are not considered in this simulation because they are used for measurements only and should be removed for use with 2.5&#8239;Ω power amplifier modules. Their effect is removed from the measurement results. The output connector is also not considered because its effect is low compared to the other losses.

Separate CAD models are used for the mechanical manufacturing and the electromagnetic simulation. The use of two separate models is mandatory because the electromagnetic model and mechanical model have different requirements. For example, the screws must be included in the mechanical model, but they are ignored in the electromagnetic model.

The simulation is performed with CST Microwave Studio<sup>&reg;</sup>. We use the frequency domain solver with tetrahedral meshing, automatic meshing and meshing adaptation. This simulation and meshing method are used because they allow both small and large features to be considered in the same simulation. The smallest features are present in the input microstrip lines, made on 127&#8239;µm substrate, and largest are present at the end of the combining, whose diameter is 30&#8239;mm.

Measurements of this power combiner are very difficult because the inputs are wide microtrip lines with low-impedances. Neither commercial connectors nor measurement instruments can directly connect to such inputs. For the measurements, we manufactured and measured a test version with standard 50&#8239;Ω SMA female connectors as inputs.

This test version is measured with a standard 50&#8239;Ω vector network analyser. The measurement setup is shown in Fig.&#8239;9. <!--\ref{fig-measurement-setup-2}--> It is made two ports at a time with the remaining ports loaded with matched 50&#8239;Ω loads. The N to SMA transition at the 50&#8239;Ω output is simply ignored. A Python script using scikit-rf library is used to combine the multiple Touchstone 2-port files into a single 9-port file. The &&S_{i,j}&& coefficients measured several times, e.g. &&S_{1,1}&&, are averaged between all measurements. De-embedding and impedance renormalization are performed with Keysight Advanced Design System.

<figure>
  <img src="{{ '/posts/coax-combiner-low-Z-isolation/measurement-2.jpg' | relative_url }}" style="width:100%;" title="Measurement setup." alt="Measurement setup.">
  <figcaption>Fig.&#8239;9. Measurement setup.</figcaption>
</figure>
<!-- \label{fig-measurement-setup-2} -->

The transitions from the 50&#8239;Ω SMA coaxial connectors to the 2.5&#8239;Ω wide microstrip lines, present in the test version of the combiner, need to be desembedded. This desembedding is done using the simulated EM model of the transition shown in Fig.&#8239;10. <!--\ref{fig-input-transition}-->

<!-- TODO: add comments. -->

<figure>
  <img src="{{ '/posts/coax-combiner-low-Z-isolation/input-transition.png' | relative_url }}" style="width:50%;" title="3D EM model of the input transition from standard 50 Ω SMA connector to 2.5 Ω wide microstrip line." alt="3D EM model of the input transition from standard 50 Ω SMA connector to 2.5 Ω wide microstrip line.">
  <figcaption>Fig.&#8239;10. 3D EM model of the input transition from standard 50&#8239;Ω SMA connector to 2.5&#8239;Ω wide microstrip line.</figcaption>
</figure>
<!-- \label{fig-measurement-setup-2} -->

Measurement results after desembedding and impedance renormalization are shown in Fig.&#8239;11, <!--\ref{fig-transmission}--> Fig.&#8239;11, <!--\ref{fig-transmission-detail}--> Fig.&#8239;12, <!--~\ref{fig-phase}--> and Fig.&#8239;13, <!--\ref{fig-isolation}--> along with the simulation results. Combining losses (Fig.&#8239;11) <!--\ref{fig-transmission}--> are lower than 1.8&#8239;dB on a 1&#8239;--&#8239;6&#8239;GHz band, except a few peaks. These peaks are due to mechanical tolerances in the start of the combining section, where minimal distance between parts is only 0.8&#8239;mm, and can be removed by a redesign of this combiner, by increasing this small dimension. This figure is good because it includes the impedance preadaptation from 2.5&#8239;Ω. RMS phase error of the inputs (Fig.&#8239;12) <!--\ref{fig-phase}--> is lower than 15° on the full band. These two parameters, insertion loss and RMS phase error, are very promising for power combining.

<figure>
  <img class="dark-mode-invert" src="{{ '/posts/coax-combiner-low-Z-isolation/transmission.svg' | relative_url }}" title="Insertion losses and output matching of power combiner." alt="Insertion losses and output matching of power combiner.">
  <figcaption>Fig.&#8239;11. Insertion losses and output matching of power combiner.</figcaption>
</figure>
<!-- fig-transmission -->

The worst case isolation between inputs is at least 10&#8239;dB for inputs close to each other (45° pair) and at least 15&#8239;dB for other pairs. This isolation enables instability problems to be avoided, and enables the propagation of a failure from a device to another one to be avoided. If a power amplifier module fails, the system can be operated at a reduced power with the other power modules, compared to TWTA-based solutions.

<figure>
  <!-- TODO: Alignment bug in table version, fallback to compound version. -->
  <!--
    <table>
      <tbody>
        <tr>
          <td rowspan="2">
            <span style="writing-mode: vertical-lr;transform: rotate(180deg);">
              Transmission between inputs and output (dB)
            </span>
          </td>
          <td>
            <img src="{{ '/posts/coax-combiner-low-Z-isolation/transmission-detail-plot-1.svg' | relative_url }}">
          </td>
          <td>
            <img src="{{ '/posts/coax-combiner-low-Z-isolation/transmission-detail-plot-2.svg' | relative_url }}">
          </td>
        </tr>
        <tr>
          <td>
            <img src="{{ '/posts/coax-combiner-low-Z-isolation/transmission-detail-plot-3.svg' | relative_url }}">
          </td>
          <td>
            <img src="{{ '/posts/coax-combiner-low-Z-isolation/transmission-detail-plot-4.svg' | relative_url }}">
          </td>
        </tr>
        <tr>
          <td>
          </td>
          <td colspan="2" style="text-align:center;">
            Frequency (GHz)
          </td>
          </td>
        </tr>
      </tbody>
    </table>
  -->
  <img class="dark-mode-invert" src="{{ '/posts/coax-combiner-low-Z-isolation/transmission-detail-plot.svg' | relative_url }}" title="Details of inputs transmissions." alt="Details of inputs transmissions.">
  <figcaption>Fig.&#8239;12. Details of inputs transmissions.</figcaption>
</figure>
<!-- \label{fig-transmission-detail} -->

<figure>
  <img class="dark-mode-invert" class="dark-mode-invert" src="{{ '/posts/coax-combiner-low-Z-isolation/phase-details.svg' | relative_url }}" title="Inputs phase errors and RMS phase error." alt="Inputs phase errors and RMS phase error.">
  <figcaption>Fig.&#8239;13. Inputs phase errors and RMS phase error.</figcaption>
</figure>
<!-- \label{fig-phase-details} -->

<figure>
  <img class="dark-mode-invert" src="{{ '/posts/coax-combiner-low-Z-isolation/isolation.svg' | relative_url }}" title="Measured and simulated isolations." alt="Measured and simulated isolations.">
  <figcaption>Fig.&#8239;14. Measured and simulated isolations.</figcaption>
</figure>
<!-- \label{fig-isolation} -->

Power handling of this combiner is difficult to measure, because the spatial distribution of thermal losses is not the same in splitting and combining modes, and the inputs cannot be directly connected to standard coaxial 50&#8239;Ω amplifiers. The power handling is estimated by an electro-thermal simulation. Fig.&#8239;15a.<!--\ref{fig-thermal}a--> shows the temperature of the device for a combined input power of 500&#8239;W CW at 1&#8239;GHz. This frequency is the worst case for thermal effects. Output power is 330&#8239;W CW and maximal temperature is 225&#8239;°C in the absorber. The current version uses an MF124 absorber, able to withstand a maximum temperature of 180&#8239;°C, which gives a maximal output power of 260&#8239;W at 1&#8239;GHz. This power can be easily increased to 380&#8239;W using a MF500-124 absorber, withstanding 260~&#8239;°C.

<figure>
  <img src="{{ '/posts/coax-combiner-low-Z-isolation/thermal-all-v3-with-png.svg' | relative_url }}">
  <figcaption>Fig.&#8239;15. Electro-thermal simulation of the combiner in combining mode (big picture) and when one amplifier is turned off (small picture).</figcaption>
</figure>
<!-- \label{fig-thermal} -->

Fig.&#8239;15b. <!--\ref{fig-thermal}b--> shows the temperature of the device when the top input is turned off. Maximal temperature is 259&#8239;°C in the absorber.

Table&#8239;1.<!--\ref{tab-state-art-1}--> shows comparison with related power combiners. It is the only one which has low impedance inputs. Insertion losses are high, but such high losses are due to the combination of the high impedance transformation ratio and the low lower frequency.

<figure class="text-table">
  <table>
    <thead>
      <tr><td>    BW                </td><td>     N     </td><td>Z<sub>in</sub></td><td>    IL        </td><td>   Isolations                   </td><td>                   Refs                                                              </td></tr>
      <tr><td>    [GHz]             </td><td>           </td><td>              </td><td>    [dB]      </td><td>   [dB]                         </td><td>                                                                                     </td></tr>
    </thead>
    <tbody>
      <tr><td><em> 1    -  6   </em></td><td><em> 8</em></td><td><em>  2.5</em></td><td><em>1.7 </em></td><td><em>11.5 20.1 18.9 17.2     </em></td><td>               <em>This work                                                  </em>  </td></tr>
      <tr><td>     2    -  8        </td><td>     8     </td><td>     50       </td><td>    0.4      </td><td>     9.5 17.0 16.3 12.7          </td><td><span markdown="1">[^ghanadi2012radial]                                       </span></td></tr>
      <tr><td>     2    - 17        </td><td>     8     </td><td>     50       </td><td>    1        </td><td>     9.5 17.0 16.3 12.7          </td><td><span markdown="1">[^ghanadi2012radial]                                       </span></td></tr>
      <tr><td>     7.6  - 10.4      </td><td>    12     </td><td>     50       </td><td>    1        </td><td>             -                   </td><td><span markdown="1">[^cohn1979broadband]<sup>,</sup>[^schellenberg1978combiner]</span></td></tr>
      <tr><td>     5    - 20        </td><td>    64     </td><td>     50       </td><td>    1.5      </td><td>             -                   </td><td><span markdown="1">[^alexianan1997broadband]                                  </span></td></tr>
      <tr><td>     6    - 18        </td><td>    20     </td><td>     50       </td><td>    0.97     </td><td>             -                   </td><td><span markdown="1">[^ning2013spatial]                                         </span></td></tr>
      <tr><td>     2    - 16        </td><td>    32     </td><td>     50       </td><td>    1.2      </td><td>             -                   </td><td><span markdown="1">[^jia2000multioctave]                                      </span></td></tr>
      <tr><td>     0.52 -  1.86     </td><td>     8     </td><td>     50       </td><td>    0.2      </td><td>             -                   </td><td><span markdown="1">[^amjadi2012design]                                        </span></td></tr>
      <tr><td>    12.1  - 15.7      </td><td>     8     </td><td>     50       </td><td>    0.17     </td><td>     7.0 12.0 11.0  7.0          </td><td><span markdown="1">[^shan2011suspended]                                       </span></td></tr>
      <tr><td>     8    - 18        </td><td>     8     </td><td>     50       </td><td>    0.5      </td><td>     9.0  7.2 10.2 11.0          </td><td><span markdown="1">[^song2007broadband]<sup>,</sup>[^song2008broadband]       </span></td></tr>
      <tr><td>    28    - 36        </td><td>    20     </td><td>    377       </td><td>    1.0      </td><td>    12.0 15.0 17.0 18.0          </td><td><span markdown="1">[^chu2015isolated]                                         </span></td></tr>
      <tr><td>    11.5  - 16        </td><td>     8     </td><td>     50       </td><td>    0.5      </td><td>     9.0 14.6 22.6 16.3 14.6     </td><td><span markdown="1">[^chu2015isolated]                                         </span></td></tr>
    </tbody>
  </table>
  <figcaption>Table 1. Comparison with related combiners.</figcaption>
</figure>

## Conclusion

A 1&#8239;--&#8239;6&#8239;GHz spatial power combiner with 2.5&#8239;Ω low-impedance inputs and increased isolation had been designed, manufactured and measured. Total losses, including impedance prematch, are lower than 1.8&#8239;dB, except on a few peaks. These peaks are due to mechanical tolerances and can be removed by increasing some critical dimensions.

This new power combiner is very promising for high power (kW) combining in a wide frequency range. Thanks to the low insertion losses, the impedance pre-matching, the ability to evacuate calories of the active devices, and the isolation between the inputs.

This design is the subject of the European patent "Spatial power combiner" number EP3171451A1.

## Acknowledgments

The authors would like to thank Sylvie Lepilliet of the IEMN for her precious help during the measurements, Pierre Bruguière of the CEA for reviewing, CST for its cooperation, Steve Huettner and Terry Cisco of Microwaves101 for good advice, and Steve Arscott of the IEMN for help with English language.

[^theveneau2017spatial]: <cite>Hadrien Theveneau, Christophe Gaquière, Romain Lenglet, Matthieu Werquin, Jean-Christophe Joly and Stéphane Tortel, <span class="article-title">Spatial Power Combiner With Low-Impedance Inputs and Increased Isolation</span>, in <span class="article-journal">IEEE Microwave and Wireless Components Letters</span>, vol. 27, no. 11, pp. 956-958, <time>Nov. 2017</time>, doi: 10.1109/LMWC.2017.2750100.</cite>

[^theveneau2017amplificateurs]: theveneau2017amplificateurs

[^jia2003broadband]: jia2003broadband

[^jia2003broadband2]: jia2003broadband2

[^li2008planar]: li2008planar

[^deVilliers2008design]: deVilliers2008design

[^song2009planar]: song2009planar

[^song2008broadband]: song2008broadband

[^chu2015isolated]: chu2015isolated

[^yau1986new]:yau1986new

[^nagai1977nway]: nagai1977nway

[^footnote1]: In this article, we use the term "combiner" loosely for both the complete system, including the impedance prematching, and the mere combining part, without prematching.

[^microwaves101wilkinson]:microwaves101wilkinson

[^cohn1968broadband]:cohn1968broadband

[^wilkinson1960divider]:wilkinson1960divider

[^arbabi2006increase]: arbabi2006increase

[^boutejdar2008miniaturized]: boutejdar2008miniaturized

[^schlieter2009designing]: schlieter2009designing

[^lim2013defected]: lim2013defected

[^pozar2012microwave]: pozar2012microwave

[^klopfenstein1956transmission]: klopfenstein1956transmission

[^collin1956optimum]: collin1956optimum

[^kajfez1973correction]: kajfez1973correction

[^microwaves101klopfenstein]: microwaves101klopfenstein

[^ning2013spatial]: ning2013spatial

[^ning2013spatial]: ning2013spatial

[^ghanadi2012radial]: ghanadi2012radial

[^cohn1979broadband]: cohn1979broadband

[^schellenberg1978combiner]: schellenberg1978combiner

[^alexianan1997broadband]: alexianan1997broadband

[^jia2000multioctave]: jia2000multioctave

[^amjadi2012design]: amjadi2012design

[^shan2011suspended]: shan2011suspended

[^song2007broadband]: song2007broadband
