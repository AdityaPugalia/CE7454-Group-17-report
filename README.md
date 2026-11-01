# CE7454 Group 17 — project report (CVPR format)

Four-page report in the official [CVPR author-kit](https://github.com/cvpr-org/author-kit) format (CVPR2027-v1 `cvpr.sty`). This folder is self-contained so it can live in its own Git repository and be synced with Overleaf.

```
main.tex          document skeleton, title, authors
preamble.tex      extra packages and macros (\path, \derma, \pneu, \deit, \TODO)
sec/              one file per section: abstract, intro, related, method, experiments, discussion
fig/              figures copied from reports/stage*/ in the code repo
main.bib          references (ieeenat_fullname style)
cvpr.sty, ieeenat_fullname.bst   author-kit files, do not edit
.github/workflows/latex-build.yml   builds main.pdf on every push (active once this is its own repo)
```

## Compile

Overleaf: pdfLaTeX (default). Locally:

```bash
latexmk -pdf main.tex        # or: pdflatex main && bibtex main && pdflatex main && pdflatex main
```

Page limit is 4 pages excluding references. `\TODO{...}` marks open items in red; silence them for the final version by uncommenting the two `\renewcommand` lines in `preamble.tex`. Switch to `\usepackage[review]{cvpr}` in `main.tex` for an anonymous, line-numbered copy.

## Keeping this folder in its own GitHub repo (for Overleaf)

Overleaf's GitHub import takes a whole repository with `main.tex` at its root, so this folder is published as a separate repo with `git subtree` from the code repo root:

```bash
# once: create an empty repo on GitHub, e.g. CE7454-Group-17-report, then
git remote add report-repo git@github.com:<you>/CE7454-Group-17-report.git

# push the report/ folder (and its history) to that repo's main branch
git subtree push --prefix=report report-repo main

# pull edits made in Overleaf (after "Sync → GitHub" there) back into the code repo
git subtree pull --prefix=report report-repo main --squash
```

In Overleaf: New Project → Import from GitHub → pick the report repo. GitHub sync is an Overleaf premium / institutional feature; if it is unavailable, zip this folder and upload it instead.

## Open items

- [ ] Author list in `main.tex`
- [ ] Fine-tuning grid results (Table `tab:ftgrid`) from `outputs/finetune/*/*/seed_*/training_summary.json`
- [ ] Full vs LoRA recovery (Table `tab:recovery`) from `outputs/pruning_study/summary.md`
- [ ] Verify locked-test reduced accuracies against `reports/stage4/comparisons.json`
- [ ] Complete the `byun2026adaptive` bibliography entry
- [ ] Trim to 4 pages, then enable `microtype`
