
<!-- README.md is generated from README.Rmd. Please edit that file -->

## Installation

``` r
devtools::install_github("clauswilke/ungeviz")
```

## Bootstrapping

This is a very simple adaptation of the example developed by [Claus O.
Wilke](https://github.com/clauswilke/ungeviz).

``` r
library(tidyverse)
library(ungeviz)
library(gganimate)

data(BlueJays, package = "Stat2Data")
bs <- BlueJays %>% ungeviz::bootstrap(20) %>% add_count(BirdID)
ggplot(BlueJays, aes(BillLength, Head, color = KnownSex)) +
  geom_smooth(method = "lm", color = NA) +
  geom_point(alpha = 0.3) +
  geom_point(data = bs, aes(group = .draw, size=n)) +
  geom_smooth(data = bs, method = "lm", fullrange = TRUE, se = FALSE) +
  facet_wrap(~KnownSex, scales = "free_x") +
  scale_color_manual(values = c(F = "#D55E00", M = "#0072B2"), guide = "none") +
  theme_bw() +
  transition_states(.draw, 1, 1) + 
  enter_fade() + 
  exit_fade()
```

![](man/figures/README-bootstrap_animate-1.gif)<!-- -->

![](figures/bootstrap_example.gif)<!-- -->
