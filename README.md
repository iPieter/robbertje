<p align="center"> 
    <img src="images/robbertje_logo_with_name.png" alt="RobBERTje: A collection of distilled Dutch BERT-based models" width="75%">
 </p>

# About RobBERTje
RobBERTje is a collection of distilled models based on [RobBERT](http://github.com/iPieter/robbert). There are multiple models with different sizes and different training settings, which you can choose for your use-case.

We are also continuously working on releasing better-performing models, so watch this page for updates.

# News
- **February 21, 2022**: Our paper about RobBERTje has been published in [volume 11 of CLIN journal](https://www.clinjournal.org/clinj/article/view/131)!
- **July 2, 2021**: Publicly released 4 RobBERTje models.
- **May 12, 2021**: RobBERTje was accepted at [CLIN31](https://www.clin31.ugent.be) for an oral presentation!

# The models
| Model        | Description | Parameters | Training size | Huggingface id                                                                     |
|--------------|-------------|------------------|-------------------|------------------------------------------------------------------------------------|
| Non-shuffled | Trained on the non-shuffled variant of the oscar corpus, without any operations to preserve this order during training and distillation.            | 74 M             | 1 GB              | [DTAI-KULeuven/robbertje-1-gb-non-shuffled](https://huggingface.co/DTAI-KULeuven/robbertje-1-gb-non-shuffled) |
| Shuffled     | Trained on the publicly available and shuffled OSCAR corpus.            | 74 M             | 1 GB              | [DTAI-KULeuven/robbertje-1-gb-shuffled](https://huggingface.co/DTAI-KULeuven/robbertje-1-gb-shuffled)     |
| Merged (p=0.5)       | Same as the non-shuffled variant, but sequential sentences of the same document are merged with a probability of 50%.           | 74 M             | 1 GB              | [DTAI-KULeuven/robbertje-1-gb-merged](https://huggingface.co/DTAI-KULeuven/robbertje-1-gb-merged)       |
| BORT         | A smaller version with 8 attention heads instead of 12 and 4 layers instead of 6 (and 12 for RobBERT).            | 46 M             | 1 GB              | [DTAI-KULeuven/robbertje-1-gb-bort](https://huggingface.co/DTAI-KULeuven/robbertje-1-gb-bort)         |

# Results

## Intrinsic results
We calculated the _pseudo perplexity_ (PPPL) from [cite](), which is a built-in metric in our distillation library. This metric gives an indication of how well the model captures the input distribution.
| Model             | PPPL      |
|-------------------|-----------|
| RobBERT (teacher) | 7.76      |
| Non-shuffled      | 12.95     |
| Shuffled          | 18.74     |
| Merged (p=0.5)    | 17.10     |
| BORT              | 26.44     |

## Extrinsic results
We also evaluated our models on sereral downstream tasks, just like the teacher model RobBERT. Since that evaluation, a [Dutch NLI task named SICK-NL](https://arxiv.org/abs/2101.05716) was also released and we evaluated our models with it as well. 

| Model            | DBRD      | DIE-DAT   | NER       | POS       |SICK-NL   |
|------------------|-----------|-----------|-----------|-----------|----------|
| RobBERT (teacher)|94.4       | 99.2      |89.1       |96.4       | 84.2     |
| Non-shuffled     |90.2       | 98.4      |82.9       |95.5       | 83.4     |
| Shuffled         |92.5       | 98.2      |82.7       |95.6       | 83.4     |
| Merged (p=0.5)   |92.9       | 96.5      |81.8       |95.2       | 82.8     |
| BORT             |89.6       | 92.2      |79.7       |94.3       | 81.0     |


# Recreating our experiments

## Distillation
The distillation procedure uses our own [distillation library](https://github.com/iPieter/universal-distillation). This library uses [Pytorch Lightning](https://www.pytorchlightning.ai) under the hood, so it should automatically be set up to use all the available GPUs or TPUs without any issues. If you encounter any problems with the distillation library, please open an [issue in that repo](https://github.com/iPieter/universal-distillation/issues).

### Getting the data
You can download the shuffled and non-shuffled version of the OSCAR corpus [here](https://oscar-corpus.com). At the time of training (early 2021), the dataset was available in sharded tars. The last shard is used as a held-out evaluation set, irregardless of training set size. We specified the training set size, which is obtained with `head -c <size>`. 



## Fine-tuning
