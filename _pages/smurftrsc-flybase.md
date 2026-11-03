---
layout: page
title: SmurfTrsc for FlyBase
permalink: /tools/smurftrsc-flybase/
description: Smurf vs non-Smurf gene expression right on FlyBase pages. A browser extension for Chrome and Chromium-based browsers (Firefox version under review).
nav: false
---

<p>
  Reading a FlyBase page and wondering how the gene behaves as flies age? <b>SmurfTrsc for FlyBase</b> shows its
  expression in the whole-body transcriptome of Smurf and non-Smurf <i>Drosophila melanogaster</i>
  (<a href="https://doi.org/10.1111/acel.13946">Zane et al., 2023</a>) directly on FlyBase report pages, so you
  can tell a change tied to the Smurf phase from a change with age without leaving the page you are reading.
</p>

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    <video class="img-fluid rounded z-depth-1" autoplay muted loop playsinline controls preload="metadata"
           poster="{{ '/assets/img/tools/smurftrsc-flybase/demo-poster.jpg' | relative_url }}"
           aria-label="Demo of SmurfTrsc for FlyBase on the Thor and Gclc gene pages">
      <source src="{{ '/assets/video/smurftrsc-flybase-demo.mp4' | relative_url }}" type="video/mp4">
    </video>
  </div>
</div>
<div class="caption">
  SmurfTrsc for FlyBase in under 30 seconds: <i>Thor</i>, flat with age but higher in Smurfs; the samples one by
  one, the age contrasts and the table of values; then <i>Gclc</i>, reached through FlyBase's Jump to Gene box.
</div>

## What it shows

On FlyBase **gene** (FBgn), **protein** (FBpp), **transcript** (FBtr) and **allele** (FBal) pages, a panel at the
top of the report gives, for the gene:

- **A one-line verdict.** Up, down or no change in Smurfs, with the log2 fold change and adjusted p, and the
  paper's category: Smurf gene, old non-Smurf gene, or both.
- **All 32 samples.** A strip plot by age (20, 30 and 40 days) and Smurf status, with group means. Hover a
  sample for its details, or open the table of all values.
- **Smurf status and age, side by side.** The paper's three DESeq2 contrasts: Smurfs vs non-Smurfs, and 40 vs
  20 days within each status.
- **The rest of the paper's results for the gene**, where it has them: longevity candidates, the linear model
  on expression, progressive change in non-Smurfs, proteomics, GenAge lifespan effects and the Human Ageing
  Atlas ortholog.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/tools/smurftrsc-flybase/gene-page.jpg' | relative_url }}"
         alt="SmurfTrsc panel on the Thor gene page: non-Smurfs low and Smurfs high at every age" loading="lazy">
  </div>
</div>
<div class="caption">
  <i>Thor</i> (4E-BP): low in non-Smurfs and high in Smurfs at 20, 30 and 40 days, with no change with age within
  either group. The two phases of ageing, in one gene.
</div>

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/tools/smurftrsc-flybase/sample-table.jpg' | relative_url }}"
         alt="SmurfTrsc panel on the Gclc gene page, with one sample hovered and the table of sample values open" loading="lazy">
  </div>
</div>
<div class="caption">
  <i>Gclc</i>: up in Smurfs and also in old non-Smurfs. Hovering a sample gives its age and the time since its
  Smurf transition; the table lists all 32 values.
</div>

## Where the data come from

The panel shows the published results of Zane et al. (2023): whole-body RNA-seq of mated <i>Drs</i>-GFP females,
Smurf and non-Smurf, at 20, 30 and 40 days, analysed with DESeq2 (significant at adjusted p ≤ 0.05, as in the
paper). Genes are matched to the current FlyBase release; genes renamed or merged since the paper's annotation
are flagged in the panel. The data come from the paper's repository,
[SmurfsTrsc](https://github.com/MichaelRera/SmurfsTrsc), and ship inside the extension.

It works alongside [ProteoCast for FlyBase]({{ '/tools/proteocast-flybase/' | relative_url }}): with both installed,
the two panels sit one above the other.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/tools/smurftrsc-flybase/with-proteocast.jpg' | relative_url }}"
         alt="The Thor-PA protein page with the ProteoCast panel above the SmurfTrsc panel" loading="lazy">
  </div>
</div>
<div class="caption">
  A protein page, Thor-PA, with both extensions: ProteoCast's mutational sensitivity, then the gene's Smurf
  transcriptome.
</div>

## Install

SmurfTrsc for FlyBase works in Chrome, Edge, Brave and other Chromium-based browsers. A Firefox version is under
review at Firefox Add-ons.

<p><a class="btn btn-primary" href="https://chromewebstore.google.com/detail/smurftrsc-for-flybase/edlhmihcnmdcgmaaidgcpgolidinnkjp" target="_blank" rel="noopener">Add to Chrome — Chrome Web Store</a></p>

- **Chrome Web Store:** [SmurfTrsc for FlyBase](https://chromewebstore.google.com/detail/smurftrsc-for-flybase/edlhmihcnmdcgmaaidgcpgolidinnkjp): one click, updates automatically.
  Edge and Brave users can install it from the same page (Edge first asks to allow extensions from other stores).
- **Firefox Add-ons:** under review.
- **Source code:** [github.com/MichaelRera/smurftrsc-flybase](https://github.com/MichaelRera/smurftrsc-flybase)
  (open source, GPL-3.0, coded with Claude Code; bug reports and suggestions welcome as GitHub issues).

## Privacy

The extension reads only the FlyBase page you are on (the identifier in its address and, on allele pages, the
associated gene). The data ship inside it: it makes no network requests at all. No analytics, no tracking,
nothing collected.

## How to cite

If these data help your work, please cite:

> Zane F, Bouzid H, Sosa Marmol S, Brazane M, Besse S, Molina JL, Cansell C, Aprahamian F, Durand S, Ayache J,
> Antoniewski C, Todd N, Carré C, Rera M. Smurfness-based two-phase model of ageing helps deconvolve the ageing
> transcriptional signature. *Aging Cell* **22**(11), e13946 (2023).
> [doi:10.1111/acel.13946](https://doi.org/10.1111/acel.13946)

SmurfTrsc for FlyBase is an independent tool and is not affiliated with FlyBase.
