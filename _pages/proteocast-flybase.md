---
layout: page
title: ProteoCast for FlyBase
permalink: /tools/proteocast-flybase/
description: Missense-variant predictions right on FlyBase pages. A browser extension for Chrome, Chromium-based browsers and Firefox.
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
    <video class="img-fluid rounded z-depth-1" autoplay muted loop playsinline controls preload="metadata"
           poster="{{ '/assets/img/tools/proteocast-flybase/demo-poster.jpg' | relative_url }}"
           aria-label="Demo of ProteoCast for FlyBase on the Naprt gene and Naprt[E147V] allele pages">
      <source src="{{ '/assets/video/proteocast-flybase-demo.mp4' | relative_url }}" type="video/mp4">
    </video>
  </div>
</div>
<div class="caption">
  ProteoCast for FlyBase in 20 seconds: the panel on the <i>Naprt</i> gene page, selecting a stretch of the
  protein, the substitutions at one residue, classifying G202R, and the <i>Naprt</i><sup>E147V</sup> allele page.
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

ProteoCast for FlyBase works in Chrome, Edge, Brave and other Chromium-based browsers, and in Firefox 140 or later.

<p><a class="btn btn-primary" href="https://chromewebstore.google.com/detail/proteocast-for-flybase/pdkdmicjkpiamojmcfgbcajcnifccokl" target="_blank" rel="noopener">Add to Chrome — Chrome Web Store</a></p>

- **Chrome Web Store:** [ProteoCast for FlyBase](https://chromewebstore.google.com/detail/proteocast-for-flybase/pdkdmicjkpiamojmcfgbcajcnifccokl): one click, updates automatically.
  Edge and Brave users can install it from the same page (Edge first asks to allow extensions from other stores).
- **Firefox:** version 0.3.1 is under review at Firefox Add-ons; the link will appear here once it is published.
- **Source code:** [github.com/MichaelRera/proteocast-flybase](https://github.com/MichaelRera/proteocast-flybase)
  (open source, GPL-3.0, coded with Claude Code; bug reports and suggestions welcome as GitHub issues).

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
