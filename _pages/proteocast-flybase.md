---
layout: page
title: ProteoCast for FlyBase
permalink: /tools/proteocast-flybase/
description: Missense-variant predictions right on FlyBase pages. A browser extension for Chrome and Chromium-based browsers.
nav: false
---

<p>
  Reading a FlyBase page and wondering whether a mutation matters? <b>ProteoCast for FlyBase</b> adds the
  <a href="https://proteocast.ijm.fr/">ProteoCast</a> predictions of missense-variant effects to FlyBase
  report pages, so you can judge a <i>Drosophila melanogaster</i> amino-acid change without leaving the page
  you are reading.
</p>

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/tools/proteocast-flybase/context-gene-page.jpg' | relative_url }}"
         alt="The ProteoCast panel at the top of the FlyBase gene report for Naprt" loading="lazy">
  </div>
</div>
<div class="caption">
  The ProteoCast panel at the top of a FlyBase gene report (here <i>Naprt</i>).
</div>

## What it shows

On FlyBase **protein** (FBpp), **gene** (FBgn) and **allele** (FBal) pages, a panel at the top of the report gives:

- **Mutational sensitivity along the protein.** Each residue is coloured by how many of its 19 possible
  substitutions ProteoCast predicts to be impactful, with the protein domains underneath and the positions
  where the evolutionary alignment is too thin to be confident shown in grey.
- **A one-line variant classifier.** Type `G202R` or `Gly202Arg` and get *impactful*, *mild* or *neutral*,
  with a check that the reference residue matches the isoform you are looking at.
- **Every substitution at a glance.** In the colour-coded sequence, hovering a residue shows its 19
  substitutions coloured by predicted class.
- **All isoforms** of a gene, from a menu.
- **The effect of an allele.** On an allele page, the allele's amino-acid replacement is classified and
  marked on the protein; alleles that are not missense changes get a short note.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/tools/proteocast-flybase/variant-box.jpg' | relative_url }}"
         alt="Variant box classifying Gly202Arg in Naprt-PA as impactful" loading="lazy">
  </div>
</div>
<div class="caption">
  Classifying a variant: G202R in Naprt-PA is predicted impactful (all 19 substitutions at this glycine are).
</div>

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/tools/proteocast-flybase/allele-hover.jpg' | relative_url }}"
         alt="Allele page for Naprt[E147V], with the colour-coded sequence and the substitutions at residue 147" loading="lazy">
  </div>
</div>
<div class="caption">
  An allele page, <i>Naprt</i><sup>E147V</sup> (CRISPR allele from Abakarova et al., 2026): the change is classified
  and marked on the track; hovering residue 147 in the sequence shows all its substitutions.
</div>

## Where the predictions come from

ProteoCast classifies every possible missense variant of a protein from its evolutionary history, built on
the GEMME model, and identifies sensitive residues, including in disordered regions. The extension shows the
proteome-wide predictions for *D. melanogaster* (FlyBase release 6.44 proteome), which cover about 99% of fly
proteins; the panel says so when a protein has none. Predictions are served from the ProteoCast server at the
Institut Jacques Monod; sequences, isoforms and domains come from FlyBase's public API.

For a protein that is not in FlyBase, or for any other organism, use the
[ProteoCast web server](https://proteocast.ijm.fr/) directly.

## Install

ProteoCast for FlyBase works in Chrome, Edge, Brave and other Chromium-based browsers.

- **Chrome Web Store:** coming soon.
- **Test version:** <a href="mailto:michael.rera@cnrs.fr?subject=ProteoCast%20for%20FlyBase">e-mail me</a>
  and I will send it with installation instructions.
- **Source code:** [github.com/MichaelRera/proteocast-flybase](https://github.com/MichaelRera/proteocast-flybase)
  (open source, GPL-3.0; bug reports and suggestions welcome as GitHub issues).

## Privacy

The extension reads only the FlyBase page you are on (the identifier in its address and, on allele pages, the
amino-acid replacement). It asks FlyBase's public API and the ProteoCast server for public data identified by
that FlyBase ID, and nothing else. No analytics, no tracking, nothing collected.

## How to cite

If ProteoCast predictions help your work, please cite:

> Abakarova M, Freiberger MI, Liehrmann A, Rera M, Laine E. Proteome-wide prediction of the functional impact of
> missense variants with ProteoCast. *Nature Communications* **17**, 3813 (2026).
> [doi:10.1038/s41467-026-72140-1](https://doi.org/10.1038/s41467-026-72140-1)

and, for the web server:

> Abakarova M, *et al.* ProteoCast: a web server to predict, validate, and interpret missense variant effects.
> *Journal of Molecular Biology* (2026). [doi:10.1016/j.jmb.2026.169657](https://doi.org/10.1016/j.jmb.2026.169657)

ProteoCast for FlyBase is an independent tool and is not affiliated with FlyBase.
