---
layout: post
title:  Regtest MathJax
date: 2022-03-22
sitemap: false
---
<script>
MathJax = { loader: {load: ['input/asciimath', 'output/chtml', 'ui/menu']} };
</script>
<script type="text/javascript" id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/startup.js">
</script>

<p class="begin-note">
Lorem ipsum dolor sit amet, consectetur adipiscing elit. (<a href="https://en.wikipedia.org/wiki/Lorem_ipsum">https://en.wikipedia.org/wiki/Lorem_ipsum</a>) Sed non risus. Suspendisse lectus tortor, dignissim sit amet, adipiscing nec, ultricies sed, dolor.
</p>

Cras elementum ultrices diam. Maecenas ligula massa, varius a, semper congue, euismod non, mi. Proin porttitor, orci nec nonummy molestie, enim est eleifend mi, non fermentum diam nisl sit amet erat.

<p class="has-mjx-container" markdown="0">
`[[b_1],[a_1]] = T \ [[a_2],[b_2]]`
</p>

Duis semper. Duis arcu massa, scelerisque vitae, consequat in, pretium a, enim. Pellentesque congue. Ut in risus volutpat libero pharetra tempor. Cras vestibulum bibendum augue. Praesent egestas leo in pede. Praesent blandit odio eu enim.

<p class="has-mjx-container" markdown="0">
`T = T_1 \ T_2 \ cdots \ T_N`
</p>

Pellentesque sed dui ut augue blandit sodales. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Aliquam nibh. Mauris ac mauris sed pede pellentesque fermentum. Maecenas adipiscing ante non diam sodales hendrerit.

<div markdown="1" align="center">

| <span markdown="0">`T_(11) = S_(12) - (S_(11)S_(22))/(S_(21))`</span>  | <span markdown="0">`S_(11) = T_(12)/T_(22)`</span>                    |
| <span markdown="0">`T_(12) = S_(11)/S_(21)`</span>                     | <span markdown="0">`S_(21) = 1/T_(22)`</span>                         |
| <span markdown="0">`T_(21) = - S_(22)/S_(21)`</span>                   | <span markdown="0">`S_(12) = T_(11) - (T_(12)T_(21))/(T_(22))`</span> |
| <span markdown="0">`T_(22) = 1/S_(21)`</span>                          | <span markdown="0">`S_(22) = - T_(21)/T_(22)`</span>                  |

</div>

Ut velit mauris, egestas sed, gravida nec, ornare ut, mi. Aenean ut orci vel massa suscipit pulvinar. Nulla sollicitudin. Fusce varius, ligula non tempus aliquam, nunc turpis ullamcorper nibh, in tempus sapien eros vitae ligula.
