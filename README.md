# ASF-S Hard Freezing

Continual learning with hard freezing. A single network learns a sequence of tasks, one after another. After each task, we keep the units that matter most for it, freeze them so that later tasks cannot overwrite them, and free the rest for the next task. Which units count as "most important" is the research question: we compare the Principal Gradient Importance (PGI) score from Artificial Structure Function Search (ASF-S), which ranks units by how they shape the output layer's Artificial Functional Connectivity (AFC), with simple scores such as weight magnitude. PackNet, the best-known method of this kind, uses weight magnitude.

Part of **NeuroPulse**, a final-year research project on structure-function-aware pruning for continual learning. Project site: https://neuropulse-co.github.io · Organisation: https://github.com/NeuroPulse-Co

**Workstream:** W3, Continual learning: hard freezing. It builds on the filter scorers in [AFC-Prune](https://github.com/NeuroPulse-Co/AFC-Prune) (W2), and on what we learned in [ASF-S](https://github.com/NeuroPulse-Co/ASF-S) (W1).

## Where this stands

There are no studies yet. In the project plan, the first ones are:

1. **A continual-learning harness with PackNet reproduced** on Split-MNIST and Split-CIFAR-10 (5 tasks of 2 classes). Every later comparison depends on this baseline being right.
2. **Hard freezing with a pluggable scorer**: PGI, L1, Taylor and random, at equal capacity per task, over 5 seeds.

Our pruning results so far shape what we expect. In single-task pruning, corrected PGI beats random choice but loses to simple scores (see AFC-Prune S1). So the main question here is whether functional connectivity helps *continual* learning in ways that single-task pruning does not show. We will report the answer either way.

We measure each method by four things:
- average accuracy over all tasks
- how much of the network each task uses
- how much retraining each task needs
- forward transfer, meaning how much earlier tasks help with later ones

Backward transfer measures forgetting. We report it too, but it is zero by construction when units are frozen.

## Studies

| Study | Question | Status | Owner |
|---|---|---|---|
| — | none yet; propose one with the *Study proposal* issue form | | |

## How to run

```bash
uv run tools/record.py new <study-id> --workstream W3 --owner "Your Name"   # start a study
uv run tools/record.py run <study-id> --tag <tag> --seed 42 -- <command>      # a recorded run
```

## How we keep records

We follow the [NeuroPulse record standard](https://github.com/NeuroPulse-Co/.github/blob/main/standards/RECORDS.md). Each study in `studies/<id>/` has a `study.yaml`, a `LOG.md` and one `runs/<run-id>/run.yaml` per run, and `showcase/` holds the curated pages that the project website publishes. Write the success criterion in `study.yaml` **before** the first run, so that it counts as pre-registered. `uv run tools/record.py check` validates everything, and it also runs in CI.
