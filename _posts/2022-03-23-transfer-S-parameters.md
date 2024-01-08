---
layout: post
title: Transfer S parameters.
permalink: /posts/transfer-S-parameters.html
last_modified_at: 2023-02-08 04:16
---

<p>
Last edition: 2024-01-08 04:16.
</p>
<p class="begin-note">This content was originally published on Microwaves 101 (<a href="https://www.microwaves101.com/encyclopedias/transfer-s-parameters">https://www.microwaves101.com/encyclopedias/transfer-s-parameters</a>). Many thanks to Steve for hosting the original version. Have a look on his website for more interesting content.
</p>

## Principle

{% comment %}
Manually included to set size, class and alt. Zoomed for better rendering.
{% endcomment %}
<img class="dark-mode-invert" src="{{ '/posts/transfer-S-parameters/S-parameters.svg' | relative_url }}" alt="S-parameters matrix of generalized two-port network with characteristic impedance Z0" style="min-width:50%;">

Transfer S parameters are a convenient way to express S parameters in a way that allows to easily cascade blocks. They have the same principle as ABCD parameters: they express all relevant input quantities in function of all relevant output quantities, contrary to normal S parameters which express all scattered waves in function of all incident waves, and are messy when cascading blocks. They are sometimes more convenient than ABCD parameters, because they work with wave quantities instead of voltages and current, which are very difficult to measure at high frequencies.

It is very counter-intuitive, but expressing input in function of output and not the inverse allows to deal with unilateral blocks, what the other convention doesn’t allow. They are most often defined in the following way:

<asciimath>
  [[b_1],[a_1]] = T \ [[a_2],[b_2]]
</asciimath>

Be careful! Another convention exists, with a and b inverted. Some people even express output in function of the input. So, pay attention  to the used convention when reading calculations from other people!

With the definition used in this page, the transfer parameter matrix of a chain of elements can be calculated as follows:

<asciimath>
  T = T_1 \ T_2 \ cdots \ T_N
</asciimath>

And, be careful, this is the inverse order as one expects. Yes, matrix multiplication is very convenient but sometimes crazy!

The following formulas can be used to pass from regular to transfer S parameter:

<asciimath>
  {: (  T_(11) = S_(12) - (S_(11)S_(22))/(S_(21))  ,  S_(11) = T_(12)/T_(22)                     ),
     (  T_(12) = S_(11)/S_(21)                     ,  S_(21) = 1/T_(22)                          ),
     (  T_(21) = - S_(22)/S_(21)                   ,  S_(12) = T_(11) - (T_(12)T_(21))/(T_(22))  ),
     (  T_(22) = 1/S_(21)                          ,  S_(22) = - T_(21)/T_(22)                   ) :}
</asciimath>

## Applications

### Calculation of characteristic impedance from S parameters

Suppose one wants to measure or simulate the characteristic impedance of something similar to a transmission line. This can be for example a 75&#8239;Ω coax cable or a via structure on HFSS. The characteristic impedance can be calculated form its measured or simulated S parameters references to 50&#8239;Ω.

Suppose also that the structure is "symmetric enough" to have the same characteristic impedance on each side (see <a href="https://en.wikipedia.org/wiki/Image_impedance">https://en.wikipedia.org/wiki/Image_impedance</a>)...

Transfer S parameters can be very convenient for this. Expressing the characteristic impedance as a reflection coefficient from 50&#8239;Ω, and recalling that by definition its invariant through the system, the following can be written:

<asciimath>
  [[b_1],[a_1]] = [[T_11,T_12],[T_21,T_12]] \ [[a_2],[b_2]]
</asciimath>

<asciimath>
  Gamma = b_1 / a_1 = (T_11 Gamma b_2 + T_12 b_2)/(T_21 Gamma b_2 + T_12 b_2) = (T_11 Gamma + T_12)/(T_21 Gamma + T_12)
</asciimath>

Rearranging:

<asciimath>
  Gamma (T_21 Gamma + T_12) = (T_11 Gamma + T_12)
</asciimath>

<asciimath>
  T_21 Gamma^2 + (T_12 - T_11) Gamma - T_12 = 0
</asciimath>

{% comment %}
Substituting for S parameters:

<asciimath>
  - S_(22)/S_(21) Gamma^2 + (S_(11)/S_(21) - (S_(12) - (S_(11)S_(22))/(S_(21)))) Gamma - (S_(11)/S_(21)) = 0
</asciimath>

<asciimath>
  - S_(22) Gamma^2 + (S_(11) - S_(12)S_(21) + S_(11)S_(22)) Gamma - S_(11) = 0
</asciimath>

Which can be solved by the usual methods:

<asciimath>
 Delta = (S_(11) - S_(12)S_(21) + S_(11)S_(22))^2 - 4*S_(22)*S_(11)
</asciimath>

<asciimath>
 Gamma = ((S_(11) - S_(12)S_(21) + S_(11)S_(22)) +- sqrt((S_(11) - S_(12)S_(21) + S_(11)S_(22))^2 - 4*S_(22)*S_(11)))/(2*S_(22))
</asciimath>
{% endcomment %}

Solving by the usual methods:
<asciimath>
  Delta = (T_(12)-T_(11))^2+4*T_(21)*T_(12)
</asciimath>
<asciimath>
  Gamma = (T_(11) - T_(12) +- sqrt((T_(12)-T_(11))^2+4*T_(21)*T_(12)))/(2*T_(21))
</asciimath>

So, the procedure, which can be conveniently put in a spreadsheet, can be outlined as follows:

1. Convert S parameters to T parameters using the previous formulas or scikit-rf (<a href="https://scikit-rf.readthedocs.io/en/latest/api/generated/skrf.network.s2t.html">https://scikit-rf.readthedocs.io/en/latest/api/generated/skrf.network.s2t.html</a>)

2. Calculate the <asciimath>Gamma</asciimath> of the characteristic impedance references to 5&#8239;Ω.

3. From the <asciimath>Gamma</asciimath>, calculate the characteristic impedance.
