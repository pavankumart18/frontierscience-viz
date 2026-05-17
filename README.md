# FrontierScience — a data story

An intuitive data visualization plus narrative for OpenAI's FrontierScience
evaluation (paper: [arXiv 2601.21165](https://arxiv.org/abs/2601.21165);
dataset: [openai/frontierscience on HF](https://huggingface.co/datasets/openai/frontierscience)).

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

The visualization walks through this in 7 sections, all driven by the
released 160-problem gold set.

## How to view

Just open `index.html` in any modern browser. The dataset is embedded inline
(no network needed at view-time, no build step).

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

- `index.html` — the deliverable; self-contained, ~600&nbsp;kB
- `data/olympiad_test.jsonl` — 100 Olympiad problems
- `data/research_test.jsonl` — 60 Research problems
- `data.json` — the merged + rubric-parsed payload that gets embedded
- `Task.md` — the original task spec

## Methodology notes

- All charts on the page that derive from the **dataset** (subject mix,
  answer-length distribution, rubric anatomy) are computed live from the
  released JSONL files at page load.
- Charts that derive from the **paper** (GPT-5.2 scores, reasoning-effort
  endpoints, head-to-head) only show numbers quoted verbatim in the paper
  text. Bars whose heights I could only estimate by eyeballing Figure 6 are
  intentionally omitted rather than fabricated.
- Sources for every claim are linked at the bottom of `index.html`.
