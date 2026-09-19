# es-mx-locale-nlu-adaptation

Evaluating dialectal robustness of assistant NLU from es-ES to es-MX, using Amazon's MASSIVE dataset.

> Not affiliated with or endorsed by Amazon. MASSIVE is distributed under CC BY 4.0. 
> See [Attribution](#attribution) below.

## Why this project

Amazon's [MASSIVE](https://huggingface.co/datasets/AmazonScience/massive) dataset is the closest public analogue to 
virtual-assistant NLU work: 1M+ utterances across 52 languages, annotated for intent classification and slot filling. 
Its Spanish locale is `es-ES` (Peninsular), there is no `es-MX`.

This project adapts a Peninsular-trained assistant NLU model to Mexican Spanish, diagnoses where  it breaks, and 
(time permitting) tests whether the gap can be closed without new labeled data.

## Results

*(TBD — filled in as milestones complete)*

| Question | Answer |
|---|---|
| Does an es-ES-trained intent classifier degrade on Mexican Spanish input? | — |
| Which linguistic categories drive the degradation? | — |
| Can the gap be closed with data augmentation alone? | — |

## Milestones

| # | Milestone | Status | Deliverable if stopped here |
|---|---|---|---|
| M1a | Taxonomy of es-ES / es-MX divergence + sampling protocol | ⬜ Not started | Standalone taxonomy document |
| M0 | Fine-tune XLM-R on MASSIVE es-ES for intent classification (3 seeds) | ⬜ Not started | Trained model + variance-aware baseline metrics |
| M1b | Paired es-MX eval set (~200 pairs + ~100 null-edit controls) | ⬜ Not started | First public es-MX eval set for MASSIVE |
| M2 | Evaluate es-ES model on MX eval set. Degradation by category + tokenization analysis | ⬜ Not started | Headline finding |
| M3 | *(stretch)* Mitigate with lexicon substitution + filtered LLM paraphrases, retrain, re-evaluate | ⬜ Not started | Before/after table |

## Method

1. **Taxonomy** - four categories of es-ES/es-MX divergence: lexical substitution, morphosyntactic, idiom/regional 
expression, English code-switching.
2. **Paired design** - each source utterance gets an MX-localized version. A subset of non-divergent items serve as 
null-edit controls, isolating dialectal effect from editing-style effect.
3. **Evaluation** - macro-F1 primary, accuracy secondary. Paired significance testing. Degradation reported per 
category with confidence intervals.
4. **(Stretch) Mitigation** - lexicon-substitution augmentation + quality-filtered LLM paraphrases, retrain, re-evaluate.

## Repo structure

```
├── data/           # eval set + taxonomy (own license/attribution file — see below)
├── notebooks/       # M0 training, M2 evaluation, M3 mitigation
├── src/              # tokenization, data loading, eval scripts
└── README.md
```

## Attribution

This project uses Amazon's [MASSIVE](https://huggingface.co/datasets/AmazonScience/massive)
dataset (CC BY 4.0). Citation:

```
@misc{fitzgerald2022massive,
  title={MASSIVE: A 1M-Example Multilingual Natural Language Understanding Dataset
         with 51 Typologically-Diverse Languages},
  author={Jack FitzGerald and Christopher Hench and Charith Peris and Scott Mackie
          and Kay Rottmann and Ana Sanchez and Aaron Nash and Liam Urbach
          and Vishesh Kakarala and Richa Singh and Swetha Ranganath and Laurie Crist
          and Misha Britan and Wouter Leeuwis and Gokhan Tur and Prem Natarajan},
  year={2022},
  eprint={2204.08582},
  archivePrefix={arXiv},
  primaryClass={cs.CL}
}
```

Any derived eval set released from `data/` carries its own attribution notice and license
file, since it inherits CC BY 4.0 obligations independent of this repo's MIT license.