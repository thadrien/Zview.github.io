---
layout: post
title:  Regtest MathJax
date: 2022-03-22
sitemap: false
---
{%- include mathjax-asciimath.html %}

Inline math test: &&T = T_1 \ T_2 \ cdots \ T_N&&.

Block math test 1:

<asciimath>
  [[b_1],[a_1]] = T \ [[a_2],[b_2]]
</asciimath>

Bloc math test 2:

<asciimath>
  {: (  T_(11) = S_(12) - (S_(11)S_(22))/(S_(21))  ,  S_(11) = T_(12)/T_(22)                     ),
     (  T_(12) = S_(11)/S_(21)                     ,  S_(21) = 1/T_(22)                          ),
     (  T_(21) = - S_(22)/S_(21)                   ,  S_(12) = T_(11) - (T_(12)T_(21))/(T_(22))  ),
     (  T_(22) = 1/S_(21)                          ,  S_(22) = - T_(21)/T_(22)                   ) :}
</asciimath>

End of math tests.
