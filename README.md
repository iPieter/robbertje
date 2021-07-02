<p align="center"> 
    <img src="images/robbertje_logo_with_name.png" alt="RobBERTje: A collection of distilled Dutch BERT-based models" width="75%">
 </p>

# About RobBERTje
RobBERTje is a collection of distilled models based on [RobBERT](http://github.com/iPieter/robbert). There are multiple models with different sizes and different training settings, which you can choose for your use-case.

We are also continuously working on releasing better-performing models, so watch this page for updates.

# News
- **July 2, 2021**: Publicly released 4 RobBERTje models.
- **May 12, 2021**: RobBERTje was accepted at [CLIN31](https://www.clin31.ugent.be) for an oral presentation!

# The models
| Model        | Description | Parameters | Training size | Huggingface id                                                                     |
|--------------|-------------|------------------|-------------------|------------------------------------------------------------------------------------|
| Non-shuffled | Trained on the non-shuffled variant of the oscar corpus, without any operations to preserve this order during training and distillation.            | 74 M             | 1 GB              | [DTAI-KULeuven/robbertje-1-gb-non-shuffled](https://huggingface.co/DTAI-KULeuven/) |
| Shuffled     | Trained on the publicly available and shuffled OSCAR corpus.            | 74 M             | 1 GB              | [DTAI-KULeuven/robbertje-1-gb-shuffled](https://huggingface.co/DTAI-KULeuven/)     |
| Merged (p=0.5)       | Same as the non-shuffled variant, but sequential sentences of the same document are merged with a probability of 50%.           | 74 M             | 1 GB              | [DTAI-KULeuven/robbertje-1-gb-merged](https://huggingface.co/DTAI-KULeuven/)       |
| BORT         | A smaller version with 8 attention heads instead of 12 and 4 layers instead of 6 (and 12 for RobBERT).            | 46 M             | 1 GB              | [DTAI-KULeuven/robbertje-1-gb-bort](https://huggingface.co/DTAI-KULeuven/)         |

# Recreating our experiments

## Distillation
The distillation procedure uses our own [distillation library](https://github.com/iPieter/universal-distillation). This library uses [Pytorch Lightning](https://www.pytorchlightning.ai) under the hood, so it should automatically be set up to use all the available GPUs or TPUs without any issues. If you encounter any problems with the distillation library, please open an [issue in that repo](https://github.com/iPieter/universal-distillation/issues).

### Getting the data
You can download the shuffled and non-shuffled version of the OSCAR corpus [here](https://oscar-corpus.com). At the time of training (early 2021), the dataset was available in sharded tars. The last shard is used as a held-out evaluation set, irregardless of training set size. We specified the training set size, which is obtained with `head -c <size>`. 



## Fine-tuning