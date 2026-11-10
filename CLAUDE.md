# michaelrera.github.io

Personal academic site for Michael Rera (UTELife / CNRS), built on the
[al-folio](https://github.com/alshedivat/al-folio) Jekyll theme and served by GitHub Pages.

## How this repo is wired

- Two remotes: `origin` = this site, `upstream` = `alshedivat/al-folio`.
  **`gh` defaults to `upstream`** — always pass `-R MichaelRera/michaelrera.github.io`
  or you will be reading al-folio's activity, not ours.
- Pages does **not** serve `master`. A "Deploy site" Action builds `master` into the
  `gh-pages` branch, then a second job ("pages build and deployment") publishes it.
  Expect ~2 minutes from push to live; it has taken as long as 13 minutes.
  A push that "didn't work" is almost always just this lag.
- `master` has a branch-protection rule saying changes must go via PR, but it does not
  actually block the owner's pushes. Direct pushes to `master` succeed.

## Content lives here

| Path | What |
|---|---|
| `_bibliography/papers.bib` | Publication list, rendered by jekyll-scholar. `selected=true` promotes an entry to the front page. |
| `_news/` | Short dated announcements on the about page |
| `_pages/` | about, publications, cv, teaching, projects, meeting_org, talks |
| `_projects/` | Project cards |
| `_posts/` | Blog |
| `_data/cv.yml`, `_data/coauthors.yml` | CV content and author-name display |
| `assets/img/`, `assets/pdf/` | Images and PDFs |

Everything else is stock al-folio.

## Maintaining the publication list

`papers.bib` is checked against ORCID `0000-0002-6574-6511`, Europe PMC, Crossref and
HAL (`authFullName_s:"Michael Rera"`). All four are queryable from the shell with `curl`
and need no auth. Watch for:

- entries still carrying **preprint** metadata after the paper was published
  (stale title, `publisher={Cold Spring Harbor Laboratory}`, missing volume/pages);
- **wrong DOIs** — verify every DOI against `api.crossref.org/works/<doi>` and confirm
  Rera is actually in the author list. One entry had a DOI belonging to a different paper;
- **duplicate keys and duplicate works** — the file has had both, and jekyll-scholar
  renders duplicates twice rather than erroring;
- preprint + published versions of the same work are sometimes intentionally kept both.
  Ask before removing one.

Validate before committing — this is the same parser jekyll-scholar uses:

```bash
ruby -e 'require "bibtex"; b=BibTeX.open("_bibliography/papers.bib"); puts b.entries.count'
```

Prefer `https://doi.org/<doi>` for `url` fields; publisher deep links rot and often
return 403 to any checker.

---

# Upgrade from al-folio v0.6.0 to v1.x

**Status: local trial completed successfully — clean build. Nothing committed to this repo yet.**
Trial tree: `<scratchpad>/af-trial` (throwaway; rebuild from scratch any time).

## Why this is safer than it looks

Fork is based on **v0.6.0 (July 2022)**; upstream is **v1.2**, 857 commits ahead.
But there are **zero framework modifications** — nothing in `_layouts`, `_sass`,
`_plugins`, `assets/js` or `assets/css` was ever touched. The 82 changed files are
content, `_config.yml`, and three one-line `_includes` tweaks, all three now obsolete
(upstream dropped polyfill.io after the 2024 compromise; Bluesky is natively supported).

## The big structural change

**v1.x ships the framework as gems**, not as files in the repo:
`al_folio_core`, `al_folio_cv`, `al_folio_distill`, `al_folio_bootstrap_compat`,
`al_img_tools`, `al_folio_upgrade`. The repo drops to ~226 files and holds only content
and config. Includes were renamed `.html` → `.liquid` and now live inside the core gem.

Consequence: **after this migration, future al-folio upgrades are `bundle update`**, not
another four-year merge. That is the main prize here.

## Do NOT rebase the 411 commits onto upstream

Replaying 411 commits against a tree 857 commits ahead produces repeated
"deleted by us / modified by them" conflicts on the same files, because early commits edit
demo files upstream has since renamed or deleted. For content only the final state matters.
Copy the final content onto a fresh framework instead; preserve history by committing the
swap on top, not by rewriting.

## Local build (verified working)

Docker is **not** usable here: the user is not in the `docker` group and sudo needs a
password. Use system Ruby instead — 3.0.2 works fine:

```bash
cd <trial-dir>
export BUNDLE_PATH=vendor/bundle
bundle install          # 118 gems, succeeds on ruby 3.0.2
bundle exec jekyll build   # ~14s
bundle exec jekyll serve --port 8080
```

Errors hide under a huge stack trace — filter with
`| grep -vE "^\s+from |Imagemagick|Terser" | tail -20`.

## Content changes the trial proved necessary

1. **`{% include X.html %}` → `.liquid`** — 33 references across 5 files
   (`_pages/projects.md`, `_projects/{miceS,6_project,exemple_project}.md`,
   `_posts/2015-05-15-images.md`). `figure.liquid` accepts a superset of the old params,
   so a plain rename is enough.
2. **All 10 `_posts` are al-folio demo content** — every one added by an upstream commit,
   none by Michael, and the blog is not in the nav. Deleting them also removes the
   `{% mermaid %}` tag error (v1.x uses ```mermaid fences). `_projects/6_project.md` is
   likewise upstream demo. `_projects/exemple_project.md` **is Michael's**, kept
   deliberately as a template — do not delete it.
3. **`_pages/about.md` front matter**:
   - `profile.address:` → `profile.more_info:`
   - `image_cicular:` → `image_circular:` (the old key was a typo and silently did nothing)
   - `news: true` → an `announcements:` block (`enabled`/`scrollable`/`limit`)
   - `social: true` unchanged
4. **Socials moved to `_data/socials.yml`** and key names are exact — a wrong key falls
   into the plugin's custom-social branch and crashes with
   `undefined method 'split' for nil`. Correct keys:
   `email`, `github_username`, `scholar_userid`, `orcid_id`, **`research_gate_profile`**
   (not `researchgate_profile`), `mastodon_username`, `bluesky_url`.
   - `mastodon_username` uses the template `https://%s`, so the value must be
     `drosophila.social/@Michael__Rera`, not `user@server`.
   - `rss_icon` hides by **omitting the line**, not by setting `false`.
   - `hal_id` is supported and worth adding — Michael has a HAL profile.
5. **`_config.yml`**: upstream ships `baseurl: /al-folio` — **must be blanked**, or every
   asset URL gets an `/al-folio/` prefix. Google Analytics is now nested under
   `analytics: google:`.
6. **Remove upstream's demo `external_sources`** (medium.com, Google Blog) or two foreign
   posts appear in the blog.

## Still to do

- **`_data/cv.yml` needs conversion.** Schema changed completely: old format was a list of
  sections (`type: map` / `time_table`); v1.x expects `cv_format: rendercv` or
  `jsonresume` with a structured `cv:` root. The trial still carries upstream's Einstein
  placeholder. This is the one genuine piece of manual content work.
- Decide whether to keep a blog at all (currently unlinked, demo-only).
- Review the v1.2 appearance — it differs meaningfully from v0.6. A look decision, not breakage.

## Trial results

Clean build, exit 0, ~14s. Verified: 40/40 bibliography entries render, 7 selected papers
on the front page, all 15 news items, nav correct
(about / publications / blog / projects / cv / talks / meeting_organization / outreach),
all 7 social icons with correct URLs, no `/al-folio/` leakage, address block renders.

## Verifying a deploy actually landed

```bash
R=MichaelRera/michaelrera.github.io
git ls-remote origin master          # did the push land
gh run list -R $R --limit 5          # both jobs: "Deploy site", then "pages build and deployment"
curl -s https://michaelrera.github.io/publications/ | grep -c "<some new string>"
```

---

# Tools section (published 2026-10-23)

`_pages/tools.md` (nav_order 2) and `_pages/proteocast-flybase.md` (`/tools/proteocast-flybase/`), images in
`assets/img/tools/proteocast-flybase/`. Chrome Web Store link added 2026-10-24 (item pdkdmicjkpiamojmcfgbcajcnifccokl).
Local build works: `BUNDLE_PATH=vendor/bundle bundle exec jekyll serve --destination <outside the repo>`.
SmurfTrsc for FlyBase added 2026-11-02: `_pages/smurftrsc-flybase.md` (`/tools/smurftrsc-flybase/`), card in `tools.md`,
images in `assets/img/tools/smurftrsc-flybase/`, video `assets/video/smurftrsc-flybase-demo.mp4`. Links to the Chrome Web Store
(item edlhmihcnmdcgmaaidgcpgolidinnkjp) and, since 2026-11-10, Firefox Add-ons (`smurftrsc-for-flybase`) in both places.

## CI: Ruby version pin

`deploy.yml` asks setup-ruby for `ruby-version: "3.3"`, not an exact patch release. `ubuntu-latest`
moved to Ubuntu 26.04 from 2026-10-19, and that image ships only the latest patch of each Ruby series:
an exact pin such as `"3.3.5"` fails at "Setup Ruby" with "Unavailable version" (it broke the SFBVie
deploy on 2026-11-06; fixed here pre-emptively the same day). Pushing workflow changes needs the `gh`
token's `workflow` scope (`gh auth refresh -h github.com -s workflow`).
