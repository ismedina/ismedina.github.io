---
layout: post
date: 2025-10-03 00:00:00-0400
inline: false
title: New dataset - <i>High-resolution global and European climatic dataset for the definition of climatic zones for Photovoltaics</i>
related_posts: false
tags: pv
---

Based on my work on photovoltaic (PV) science at the European Commission's Joint Research Center, I am pleased to publish together with Ana M. Martínez [a dataset of high-resolution global and European PV data](https://data.jrc.ec.europa.eu/dataset/71142004-19c2-4827-bfa3-16d640528e5a). This dataset includes average global data on optimal tilt, yearly in-plane irradiance, module performance ratio and other PV performance parameters of interest at a spatial resolution of 0.1º (increased to 0.05º in the European region). The dataset features a novel PV performance parameter of interest, namely the <i>irradiance-weighted module temperature</i>, which proves extremely useful to characterize the PV performance losses due to high operating module temperature. Finally, going beyond discrete parameters, we also provide distributions of the daily irradiance and daily PV+storage self-sufficiency, at the same high spatial resolution, encoded in finely chosen quantiles. All quantities have been extracted using [PVGIS 5.3](https://re.jrc.ec.europa.eu/pvg_tools/en/), which leverages the ERA5 and SARAH3 climatic datasets.

These datasets were assembled with the primary objective of performing a <i>data-driven climatic classification for PV purposes</i>, adaptable both to a discrete set of scalar parameters, as well as to probability distributions of climatic variables. The methodology and results are outlined in a corresponding journal paper, which is still under revision, but the code to reproduce the analysis is already available at [this Github repository](https://github.com/ismedina/climatic-zones-pv).
