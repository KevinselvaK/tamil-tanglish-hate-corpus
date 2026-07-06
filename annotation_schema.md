# Annotation Schema (Codebook)

Each comment is annotated along **five levels**. Levels 2, 3, and 5 apply **only** when Level 1 marks
the comment as hateful or offensive (`Hate`, `Hate with Offensive`, or `Offensive`); for `Non-Hate`
and `Cannot decide` they are left empty.

---

## Level 1 — Hate typology

| Label | Definition |
|---|---|
| `Non-Hate` | No hostility toward a person or group; neutral, supportive, or merely critical of ideas. |
| `Hate` | Expresses hatred, dehumanisation, or calls for harm against a person or group based on a protected or social attribute. |
| `Hate with Offensive` | Hateful content that additionally uses profanity or vulgarity. |
| `Offensive` | Vulgar, insulting, or abusive language that is not tied to hatred of a group (e.g., a personal insult, generic profanity). |
| `Cannot decide` | Meaning is genuinely indeterminate (missing context, unclear referent, ambiguous sarcasm). |

> Decision rule: distinguish **group-directed hatred** (`Hate`) from **general abuse/vulgarity**
> (`Offensive`). If both hatred and profanity are present, use `Hate with Offensive`.

## Level 2 — Implicit vs. Explicit *(hate/offensive only)*

| Label | Definition |
|---|---|
| `Explicit` | Hostility is on the surface — an overt slur, direct attack, or unambiguous insult. |
| `Implicit` | Hostility is coded, indirect, sarcastic, or figurative and requires world/cultural knowledge to recover (e.g., dog-whistles, coded caste references, stereotype framing, delegitimisation). |

> Decision rule: if removing world knowledge still leaves the hostility legible, it is `Explicit`;
> if the surface form looks innocuous or non-hostile without cultural context, it is `Implicit`.

## Level 3 — Target of hate *(hate/offensive only)*

| Label | Definition |
|---|---|
| `Caste` | Targets a caste or caste-based community. |
| `Political` | Targets a political party, ideology, leader, or supporters. |
| `Sexist` | Targets a person/group on the basis of gender or uses gendered/sexual degradation. |
| `Religion` | Targets a religious group or identity. |
| `Ambiguous` | Clearly hostile, but the targeted group cannot be identified from the comment alone. |

## Level 4 — Language / script

| Label | Definition |
|---|---|
| `Tamil` | Written in native Tamil script. |
| `Romanized` | Tamil written in the Latin alphabet. |
| `Code-Mixed` | Mixes Tamil and English within the comment. |
| `English` | Predominantly English. |

## Level 5 — Intensity *(hate/offensive only)*

| Label | Definition |
|---|---|
| `Low` | Mild; dismissive or lightly insulting. |
| `Medium` | Clearly hostile or abusive. |
| `High` | Severe; strong slurs, dehumanisation, or calls for harm. |

> **Note on reliability:** intensity is the least reliable dimension in the current data
> (Krippendorff α = 0.53) and is being revised with anchored examples. Treat intensity labels as
> low-confidence.

---

## Adjudication

Comments were labelled independently. For each dimension, the **gold** label is the value both
annotators agreed on; where they disagreed, the gold field is marked `REVIEW` and resolved by an
adjudicator in the full corpus. The `agreement` column records whether a comment was `unanimous`
across all applicable dimensions.

## Worked examples (from `data/sample_100.csv`)

- **Explicit / Caste:** an overt caste slur combined with profanity → `Hate with Offensive`,
  `Explicit`, `Caste`.
- **Implicit / Caste:** "it's only the charity *we* gave that keeps them going" → coded assertion of
  caste superiority with no slur → `Hate`, `Implicit`, `Caste`.
- **Implicit / Political:** "party X is just party Y's B-team" → delegitimisation through framing →
  `Hate`/`Offensive`, `Implicit`, `Political`.
