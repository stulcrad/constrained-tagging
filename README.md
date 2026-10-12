# Constrained Tagging for Span Labeling

Anonymous code artifact accompanying the submission *Constrained Tagging for
Span Labeling*.

Span labeling with decoder-only LLMs, where the output must be a **verbatim**
substring of the input and the label set is **dynamic**. The constrained
decoding scheme makes non-verbatim output impossible by construction, needs no
task-specific training, and is evaluated unchanged across six span-labeling
tasks.

## Layout

```
src/utils/          core library: byte-level token trie and the logits processors
scripts/<Dataset>/  one evaluation entry point per dataset and per approach
scripts/analysis/   table generation and experiment auditing
slurm/              the job scripts the experiments were run with
analysis/           paired bootstrap tool (not used for the reported results)
Notebooks/          exploratory notebooks, including the two-phase derivation
Experiment_results_publication/
                    per-run aggregate metrics (CSV), one directory per
                    dataset and approach
Experiment_results_publication_full/
                    the same for the full UniversalNER test sets (no cap),
                    used for the comparison with published results
```

## What is not included

* **Datasets.** Not redistributed: CoNLL-2003 carries Reuters terms, and
  several UniversalNER treebanks and MultiGEC languages are individually
  restricted. The loaders in `scripts/data/` fetch them from their original
  sources.
* **Per-example predictions.** The full prediction JSONL is ~3.4 GB and
  exceeds what this hosting supports. The aggregate CSVs that every reported
  table is computed from are included in full.

## Reproducing

```bash
pip install -r requirements.txt
python scripts/NER/evaluationNER_cons_gen.py --model <hf-id> --batch-size 16
```

Paths in the SLURM scripts are written as `/path/to/...` and need pointing at
a local checkout.
