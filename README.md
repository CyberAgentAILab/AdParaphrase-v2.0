# AdParaphrase v2.0

This repository contains data for our paper "AdParaphrase v2.0: Generating Attractive Ad Texts Using a Preference-Annotated Paraphrase Dataset" (ACL2025 Findings).

## Overview

AdParaphrase v2.0 is a dataset for ad text paraphrasing, containing human preference data, to enable the analysis of the linguistic factors and to support the development of methods for generating attractive ad texts. Compared with [AdParaphrase v1.0](https://github.com/CyberAgentAILab/AdParaphrase), this dataset is 20 times larger, comprising 16,460 ad text paraphrase pairs, each annotated with preference data from ten evaluators, thereby enabling a more comprehensive and reliable analysis.

- **Paper:** [AdParaphrase v2.0: Generating Attractive Ad Texts Using a Preference-Annotated Paraphrase Dataset](https://arxiv.org/abs/2505.20826)
  - 🆕 Our paper has been accepted to [ACL2025](https://2025.aclweb.org/).
- **Languages**: All ad texts in AdParaphrase are in Japanese.
- **Availability**: Our dataset is available on [Github](https://github.com/CyberAgentAILab/AdParaphrase-v2.0) and [HuggingFace Datasets](https://huggingface.co/datasets/cyberagent/AdParaphrase-v2.0).

## Dataset Structure

This repository contains two types of datasets: `main` and `pt`.

**`main` dataset:**
- Purpose: Analyzing linguistic features influencing human preferences.
- Structure: Pairs of ad texts (`ad1`, `ad2`) with paraphrase and preference annotations.
- See Sections 2 and 3 of the paper for details.

**`pt` (preference tuning) dataset:**
- Purpose: Ad text generation experiments using preference tuning.
- Structure: Triplets (`x`, `y_1`, `y_2`) where `x` is a source ad, and `y_1`, `y_2` are paraphrases with comparative human preference labels.
- Enables direct preference optimization.
- See Section 5.2.1 of the paper for details.


**`main` dataset fields**

The dataset is stored in [data/adparaphrase_v2_main.csv](data/adparaphrase_v2_main.csv).

| Column                  | Type | Description                                                                                                                                                     |
| ----------------------- | ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                    | int  | Index of ad text pair.                                                                                                                                          |
| `ad1`                   | str  | `ad1` is the source ad text for paraphrase candidate generation, which is originally from the CAMERA dataset.                                                   |
| `ad2`                   | str  | `ad2` is a generated ad text by LLMs or crowdworkers based on `ad1`. See `source_ad2` for details.                                                              |
| `source_ad1`            | str  | Source of `ad1`. This indicates the identifier of the ad text included in the CAMERA dataset. The naming convention is as follows: camera\_{split}\_{asset_id}. |
| `source_ad2`            | str  | Source of `ad2`. This can be a model (`swallow8b`, `swallow70b`, `calm7b`, `calm22b`, or `human`) that generated `ad2` from `ad1`.                              |
| `count.paraphrase`      | int  | Number of judges who labeled an ad text pair (`ad1`, `ad2`) as paraphrases in paraphrase identification.                                                        |
| `count.nonparaphrase`   | int  | Number of judges who labeled an ad text pair (`ad1`, `ad2`) as non-paraphrases in paraphrase identification.                                                    |
| `count.preference_ad1`  | int  | Number of judges who preferred `ad1` over `ad2`.                                                                                                                |
| `count.preference_ad2`  | int  | Number of judges who preferred `ad2` over `ad1`.                                                                                                                |
| `count.preference_skip` | int  | Number of judges who skipped an ad text pair (`ad1`, `ad2`) in attractiveness evaluation.                                                                       |

**Note**: Because we performed human preference judgments on paraphrased ad text pairs, nonparaphrased pairs do not contain the results of preference judgments. Specifically, we set `count.preference_{skip,ad1,ad2}` to 0 when a majority of judges (three or more judges out of five judges) labeled ad text pairs as nonparaphrases.

**`pt` dataset fields**

The dataset is stored in [data/adparaphrase_v2_pt.csv](data/adparaphrase_v2_pt.csv).

| Column                  | Type | Description                                                                                                                                                          |
| ----------------------- | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                    | int  | Index of ad text pair.                                                                                                                                               |
| `input_ad`              | str  | `input_ad` is the source ad text for paraphrase generation, which is originally from the CAMERA dataset.                                                             |
| `generated_ad1`         | str  | `generated_ad1` is a generated ad text by LLMs or crowdworkers based on `input_ad`. See `model_ad1` for details.                                                     |
| `generated_ad2`         | str  | `generated_ad2` is a generated ad text by LLMs or crowdworkers based on `input_ad`. See `model_ad2` for details.                                                     |
| `count.preference_ad1`  | int  | Number of judges who preferred `generated_ad1` over `generated_ad2`.                                                                                                 |
| `count.preference_ad2`  | int  | Number of judges who preferred `generated_ad2` over `generated_ad1`.                                                                                                 |
| `count.preference_skip` | int  | Number of judges who skipped an ad text pair (`generated_ad1`, `generated_ad2`) in attractiveness evaluation.                                                        |
| `source_input_ad`       | str  | Source of `input_ad`. This indicates the identifier of the ad text included in the CAMERA dataset. The naming convention is as follows: camera\_{split}\_{asset_id}. |
| `model_ad1`             | str  | A model that generated `generated_ad1` from `input_ad`. (e.g., `swallow8b`, `swallow70b`, `calm7b`, `calm22b`, or `human`)                                           |
| `model_ad2`             | str  | A model that generated `generated_ad2` from `input_ad`. (e.g., `swallow8b`, `swallow70b`, `calm7b`, `calm22b`, or `human`)                                           |
| `split`                 | str  | Data split (train, valid, or test).                                                                                                                                  |

## Citation

If you use AdParaphrase v2.0, please cite our paper:

```bibtex
@misc{murakami2025adparaphrase,
    title="{A}d{P}araphrase v2.0: Generating Attractive Ad Texts Using a Preference-Annotated Paraphrase Dataset",
    author = "Murakami, Soichiro  and
      Zhang, Peinan  and
      Kamigaito, Hidetaka  and
      Takamura, Hiroya  and
      Okumura, Manabu",
    booktitle = "Findings of the Association for Computational Linguistics: ACL 2025",
    month = july,
    year="2025",
    address = "Vienna, Austria",
    publisher = "Association for Computational Linguistics",
    abstract="Identifying factors that make ad text attractive is essential for advertising success. This study proposes AdParaphrase v2.0, a dataset for ad text paraphrasing, containing human preference data, to enable the analysis of the linguistic factors and to support the development of methods for generating attractive ad texts. Compared with v1.0, this dataset is 20 times larger, comprising 16,460 ad text paraphrase pairs, each annotated with preference data from ten evaluators, thereby enabling a more comprehensive and reliable analysis. Through the experiments, we identified multiple linguistic features of engaging ad texts that were not observed in v1.0 and explored various methods for generating attractive ad texts. Furthermore, our analysis demonstrated the relationships between human preference and ad performance, and highlighted the potential of reference-free metrics based on large language models for evaluating ad text attractiveness. The dataset is publicly available at: https://github.com/CyberAgentAILab/AdParaphrase-v2.0."
}
```

## References

AdParaphrase v2.0 is built upon the following two datasets, [AdParaphrase v1.0](https://aclanthology.org/2025.findings-naacl.78/) and [CAMERA](https://aclanthology.org/2024.acl-long.54/):

```bibtex
# AdParaphrase-v1.0
@inproceedings{murakami-etal-2025-adparaphrase,
    title = "{A}d{P}araphrase: Paraphrase Dataset for Analyzing Linguistic Features toward Generating Attractive Ad Texts",
    author = "Murakami, Soichiro  and
      Zhang, Peinan  and
      Kamigaito, Hidetaka  and
      Takamura, Hiroya  and
      Okumura, Manabu",
    editor = "Chiruzzo, Luis  and
      Ritter, Alan  and
      Wang, Lu",
    booktitle = "Findings of the Association for Computational Linguistics: NAACL 2025",
    month = apr,
    year = "2025",
    address = "Albuquerque, New Mexico",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2025.findings-naacl.78/",
    pages = "1426--1439",
    ISBN = "979-8-89176-195-7",
    abstract = "Effective linguistic choices that attract potential customers play crucial roles in advertising success. This study aims to explore the linguistic features of ad texts that influence human preferences. Although the creation of attractive ad texts is an active area of research, progress in understanding the specific linguistic features that affect attractiveness is hindered by several obstacles. First, human preferences are complex and influenced by multiple factors, including their content, such as brand names, and their linguistic styles, making analysis challenging. Second, publicly available ad text datasets that include human preferences are lacking, such as ad performance metrics and human feedback, which reflect people`s interests. To address these problems, we present AdParaphrase, a paraphrase dataset that contains human preferences for pairs of ad texts that are semantically equivalent but differ in terms of wording and style. This dataset allows for preference analysis that focuses on the differences in linguistic features. Our analysis revealed that ad texts preferred by human judges have higher fluency, longer length, more nouns, and use of bracket symbols. Furthermore, we demonstrate that an ad text-generation model that considers these findings significantly improves the attractiveness of a given text. The dataset is publicly available at: https://github.com/CyberAgentAILab/AdParaphrase."
}

# CAMERA
@inproceedings{mita-etal-2024-striking,
    title = "Striking Gold in Advertising: Standardization and Exploration of Ad Text Generation",
    author = "Mita, Masato  and
      Murakami, Soichiro  and
      Kato, Akihiko  and
      Zhang, Peinan",
    editor = "Ku, Lun-Wei  and
      Martins, Andre  and
      Srikumar, Vivek",
    booktitle = "Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics (Volume 1: Long Papers)",
    month = aug,
    year = "2024",
    address = "Bangkok, Thailand",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2024.acl-long.54/",
    doi = "10.18653/v1/2024.acl-long.54",
    pages = "955--972",
    abstract = "In response to the limitations of manual ad creation, significant research has been conducted in the field of automatic ad text generation (ATG). However, the lack of comprehensive benchmarks and well-defined problem sets has made comparing different methods challenging. To tackle these challenges, we standardize the task of ATG and propose a first benchmark dataset, CAMERA, carefully designed and enabling the utilization of multi-modal information and facilitating industry-wise evaluations. Our extensive experiments with a variety of nine baselines, from classical methods to state-of-the-art models including large language models (LLMs), show the current state and the remaining challenges. We also explore how existing metrics in ATG and an LLM-based evaluator align with human evaluations."
}
```

## License

<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><span property="dct:title">AdParaphrase v2.0</span> is licensed under <a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-NC-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>


© 2025 [CyberAgent AI Lab](https://research.cyberagent.ai/)