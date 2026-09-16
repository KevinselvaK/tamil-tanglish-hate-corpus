# A Tamil–Tanglish Corpus for Implicit and Explicit Hate Speech Detection

A four-level annotated corpus of code-mixed Tamil–English (**Tanglish**) and Tamil social-media
comments, labelled for hate typology, **implicit vs. explicit** expression, target, language, and
intensity. This repository accompanies the survey paper:

> Kevin Selva K and Thilagavathy R. (2026). *From Explicit to Implicit Hate Speech Detection in
> Low-Resource and Code-Mixed Languages: A Systematic Survey of Methods, Datasets, and Adaptation
> Strategies, with Emphasis on Dravidian Languages.* ACM Transactions on Asian and Low-Resource
> Language Information Processing (submitted).

It releases a **100-comment sample** of the corpus, including the ten examples shown in **Table 1**
of the paper (flagged by the `in_table1` column), so that readers can inspect the annotation scheme
against real data.

---

## ⚠️ Content warning

This dataset contains **real, unmodified social-media comments** that include caste-based slurs,
sexual profanity, gendered abuse, and political hostility. The text is reproduced verbatim, without
masking, because it is the object of scientific study. It is distributed **solely for research on
hate-speech detection and content moderation**. It does not reflect the views of the authors, and it
must not be used to harass, profile, or target any individual or community.

---

## Overview

| | |
|---|---|
| **Languages** | Tamil (native script) and Tanglish (Tamil–English code-mixing, incl. Romanised Tamil) |
| **Source** | Public YouTube comment threads (Tamil political and caste-related discourse) |
| **Domains** | `caste`, `political` |
| **Full annotated set** | 6,999 comments (3,499 caste + 3,500 political); target size ≈ 15,000 |
| **This release** | 100-comment sample (`data/sample_100.csv`) |
| **Annotators** | Multiple independent annotators; disagreements resolved by adjudication |
| **Tool** | Label Studio |

**What makes this corpus different.** Existing Dravidian datasets overwhelmingly label *explicit*
offensive language. To our knowledge this is the first Tamil/Tanglish resource to annotate the
**implicit vs. explicit** dimension as a first-class category, alongside a fine-grained target and
intensity scheme.

---

## Repository structure

```
.
├── data/
│   └── sample_100.csv          # 100 annotated comments (incl. the 10 paper Table 1 examples)
├── annotation_schema.md        # codebook: label definitions and decision rules
├── CITATION.cff                # machine-readable citation
├── LICENSE                     # CC BY 4.0
└── README.md
```

---

## Data format

`data/sample_100.csv` (UTF-8). Each row is one comment. The five annotation dimensions are given
**per annotator** (`annotator1_*`, `annotator2_*`) and as an **adjudicated gold label** (`gold_*`).
Where the two annotators disagreed on a dimension, the gold field is marked `REVIEW`. Dimensions that
do not apply to non-hateful comments are left empty.

| Column | Description |
|---|---|
| `id` | Sample identifier (`CAS-###` caste, `POL-###` political) |
| `comment_id` | Original YouTube comment ID (provenance) |
| `domain` | `caste` or `political` |
| `text` | The comment, verbatim |
| `annotator1_hate`, `annotator2_hate` | Level 1 — hate typology |
| `annotator1_type`, `annotator2_type` | Level 2 — Implicit / Explicit |
| `annotator1_target`, `annotator2_target` | Level 3 — target of hate |
| `annotator1_language`, `annotator2_language` | Level 4 — language/script |
| `annotator1_intensity`, `annotator2_intensity` | Level 5 — intensity |
| `gold_hate` … `gold_intensity` | Adjudicated label per dimension (`REVIEW` if annotators disagreed) |
| `agreement` | `unanimous` if the annotators matched on every applicable dimension, else `review` |
| `in_table1` | `True` for the ten comments reproduced in Table 1 of the paper |

---

## Label definitions

**Level 1 — Hate typology.** `Non-Hate` · `Hate` · `Hate with Offensive` · `Offensive` ·
`Cannot decide`.

**Level 2 — Implicit / Explicit** *(applies only when the comment is `Hate`, `Hate with Offensive`,
or `Offensive`).* `Explicit` = hostility carried by an overt slur or direct attack; `Implicit` =
hostility carried through coded, indirect, or figurative language that requires world knowledge to
recover.

**Level 3 — Target.** `Caste` · `Political` · `Sexist` · `Religion` · `Ambiguous` (target group not
identifiable from the comment alone).

**Level 4 — Language.** `Tamil` (native script) · `Romanized` (Tamil in Latin script) · `Code-Mixed`
(Tamil + English) · `English`.

**Level 5 — Intensity.** `Low` · `Medium` · `High`.

See [`annotation_schema.md`](annotation_schema.md) for the full codebook and boundary rules.

---

## Annotation and reliability

Comments were labelled independently by multiple annotators in Label Studio; each annotator saw the
raw comment and applied the four-level scheme without consulting the others. Disagreements were
resolved by adjudication to produce the gold label.

Inter-annotator agreement was computed on the **full annotated set (N = 6,999)** using
**Krippendorff's α** (nominal for Levels 1–4, ordinal for intensity):

| Dimension | Krippendorff α | Interpretation |
|---|---:|---|
| Binary hate (hateful/offensive vs. non-hate) | **0.946** | almost perfect |
| Hate typology (5-class) | 0.886 | strong |
| Implicit vs. Explicit | **0.810** | reliable |
| Target of hate | 0.926 | almost perfect |
| Language | 0.952 | almost perfect |
| Intensity (ordinal) | 0.530 | **low — see limitations** |

The implicit/explicit distinction — the novel dimension of this corpus — clears the conventional
α ≥ 0.80 reliability threshold.

---

## Known limitations

- **Intensity reliability is low** (α = 0.530). Intensity labels are released for completeness but
  should be treated as **low-confidence**; they are the subject of ongoing guideline revision.
- **Sample, not the full corpus.** This repository releases 100 items for inspection and
  reproducibility of Table 1. The complete corpus is under preparation.
- **Sparse categories.** The `Religion` target is very rare in the current data and is not yet
  adequately represented.
- **Platform terms.** Comments were collected from YouTube; redistribution of raw text is subject to
  the platform's Terms of Service. This small research sample is shared under fair-use / research
  provisions; users intending large-scale reuse should re-collect via the provided `comment_id`s.

---

## Ethics and responsible use

Only publicly available comments were collected; no private or account-level data is included.
Author identities and @-mentions are not part of the released fields. The study is being conducted
under institutional ethics review (SRMIST Institutional Ethics Committee); a consent waiver was
sought for the use of public social-media data. By using this dataset you agree to use it only for
research or educational purposes and not to attempt to re-identify, target, or harm any individual
or group.

---

## Citation

If you use this corpus, please cite the accompanying paper (see [`CITATION.cff`](CITATION.cff)):

```bibtex
@article{selva2026implicit,
  title   = {From Explicit to Implicit Hate Speech Detection in Low-Resource and Code-Mixed
             Languages: A Systematic Survey of Methods, Datasets, and Adaptation Strategies,
             with Emphasis on Dravidian Languages},
  author  = {Selva K, Kevin and Thilagavathy R.},
  journal = {ACM Transactions on Asian and Low-Resource Language Information Processing},
  year    = {2026}
}
```

---

## License

Released under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license — see
[`LICENSE`](LICENSE). You may share and adapt the data with attribution. *(If you prefer to bar
commercial reuse of this hate-speech data, switch to CC BY-NC 4.0.)*


