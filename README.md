# FrontierScience — a data story

Two views on OpenAI's FrontierScience evaluation (paper: [arXiv 2601.21165](https://arxiv.org/abs/2601.21165);
dataset: [openai/frontierscience on HF](https://huggingface.co/datasets/openai/frontierscience)):

1. **A single-slide stakeholder view** placing FrontierScience inside the broader
   AI-vs-human-researcher landscape (GPQA, HLE, FrontierMath, SWE-bench, IMO,
   Codeforces, ARC-AGI, RadLE, METR, AlphaFold). **This is the landing page (`index.html`).**
2. **A 9-section narrative deep dive** into the paper itself (`data_story.html`).

## What's the story?

GPT-5.2 scores **77%** on FrontierScience-Olympiad but **25%** on
FrontierScience-Research — a 52-point gap *for the same model*.

The released dataset shows you exactly why. The two splits aren't asking
different questions; they're applying different graders:

- **Olympiad** (100 problems): grade the final expression. Median answer
  length: 57 characters. "U = CT".
- **Research** (60 problems): grade the work, with a 10-point rubric
  containing 7-18 sub-criteria per problem. Median answer length: 2,248
  characters.

That's the paper. The stakeholder slide goes one level up: FrontierScience-Research
isn't an isolated 25% — it's part of a pattern. AI has crossed superhuman on
closed-form benchmarks (GPQA 93%, IMO gold, Codeforces 2727 Elo, SWE-bench 94%)
while still trailing humans on open-ended research work
(FrontierMath Tier 4: 6%, HLE: 45% vs human 90%, ARC-AGI-3: <1% vs 100%).

## How to view

Open `index.html` in any modern browser. You'll land on the stakeholder
slide; footer links take you to the methodology page and the full data
story. Everything is self-contained — no network needed at view-time, no
build step.

```
# Windows
start index.html

# macOS
open index.html

# or any platform: drag the file onto your browser
```

If you want to re-derive the embedded data:

```bash
python -c "import urllib.request as u; base='https://huggingface.co/datasets/openai/frontierscience/resolve/main/'; \
[u.urlretrieve(base+f,'data/'+f.replace('/','_')) for f in ['olympiad/test.jsonl','research/test.jsonl']]"
```

## What's in this folder

| File | Purpose |
|---|---|
| `index.html` | **Landing page.** Single-slide, presentation-ready view of where AI stands vs human researchers across 14 capabilities. Overlapping bar chart, sorted by AI score. Fits one screen, no scrolling. |
| `frontier_ai_vs_humans_about.html` | Companion explainer for the slide: design rationale, full data table with sources for every bar, methodology, honest caveats, who it's useful for. |
| `data_story.html` | The original 9-section data story walking through the FrontierScience paper; self-contained, ~600 kB. Top nav links back to the slide and the about page. |
| `data/olympiad_test.jsonl` | 100 Olympiad problems (raw HF dataset). |
| `data/research_test.jsonl` | 60 Research problems (raw HF dataset). |
| `data.json` | Merged + rubric-parsed payload that gets embedded into `data_story.html`. |
| `paper.txt` | Extracted text of the FrontierScience paper for reference. |
| `Task.md` | Original task spec. |

## Navigation between pages

All three pages cross-link:

- **Slide → about & data story**: footer of `index.html`.
- **Data story → slide & about**: sticky top nav in `data_story.html`.
- **About → slide & data story**: nav buttons at the top and bottom of `frontier_ai_vs_humans_about.html`.

## Methodology notes

**On `index.html` (the stakeholder slide)**

- **AI scores** are taken from the top frontier model on each benchmark as
  of May 2026, quoted verbatim from public leaderboards or papers
  (GPT-5.2 Pro on GPQA, Gemini 3.1 Pro on HLE, Claude Mythos on SWE-bench,
  DeepMind/OpenAI on IMO 2025, OpenAI o3 on Codeforces, etc.).
- **Human scores** are either (a) published expert baselines where they
  exist (GPQA expert ≈65%, HLE expert ≈90%, RadLE radiologists 83%) or
  (b) order-of-magnitude normalizations on a 0–100 scale for structural
  attributes like speed, scale, and cost. The
  FrontierScience paper itself notes (§4) that no formal human baseline
  was run; we're upfront about that in the about page.
- Every bar's source is cited in the tooltip and in the full data table on
  `frontier_ai_vs_humans_about.html`.
- Bars are clickable — each one opens its source in a new tab.

**On `data_story.html` (the FrontierScience paper deep dive)**

- All charts on the page that derive from the **dataset** (subject mix,
  answer-length distribution, rubric anatomy) are computed live from the
  released JSONL files at page load.
- Charts that derive from the **paper** (GPT-5.2 scores, reasoning-effort
  endpoints, head-to-head) only show numbers quoted verbatim in the paper
  text. Bars whose heights I could only estimate by eyeballing Figure 6 are
  intentionally omitted rather than fabricated.
- Sources for every claim are linked at the bottom of `data_story.html`.

## Key data sources for the stakeholder slide

- [FrontierScience paper (arXiv)](https://arxiv.org/abs/2601.21165)
- [Humanity's Last Exam (CAIS)](https://agi.safe.ai/) — 8% → 44.7% in 16 months
- [FrontierMath (Epoch AI)](https://epoch.ai/frontiermath) — Tier 4 at 6.3% best
- [SWE-bench Verified](https://www.swebench.com/verified.html)
- [METR Time Horizons](https://metr.org/time-horizons/) — 4.3-month doubling
- [ARC Prize](https://arcprize.org/) — ARC-AGI-3 <1% AI / 100% human
- [AlphaFold: Five Years of Impact (DeepMind)](https://deepmind.google/blog/alphafold-five-years-of-impact/)
- [Codeforces o3 announcement](https://codeforces.com/blog/entry/133874)
- [Radiology Last Exam (RadLE) preprint](https://arxiv.org/pdf/2509.25559)
- [Sakana AI Scientist evaluation](https://arxiv.org/abs/2502.14297)
