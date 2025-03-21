
<p align="center">
    <br>
    <img src="images/title.png" width="900"/>
    <br>
<a href="https://twitter.com/intent/tweet?text=Wow:&url=https%3A%2F%2Fgithub.com%2Fikergarcia1996%2FEasy-Translate"><img alt="Twitter" src="https://img.shields.io/twitter/url?style=social&url=https%3A%2F%2Fgithub.com%2Fikergarcia1996%2FEasy-Translate"></a>
<a href="https://github.com/ikergarcia1996/Easy-Translate/blob/main/LICENSE.md"><img alt="License" src="https://img.shields.io/github/license/ikergarcia1996/Easy-Translate"></a>
<a href="https://huggingface.co/docs/transformers/index"><img alt="Transformers" src="https://img.shields.io/badge/-%F0%9F%A4%97Transformers%20-grey"></a>
<a href="https://huggingface.co/docs/accelerate/index/"><img alt="Accelerate" src="https://img.shields.io/badge/-%F0%9F%A4%97Accelerate%20-grey"></a>
<a href="https://ikergarcia1996.github.io/Iker-Garcia-Ferrero/"><img alt="Author" src="https://img.shields.io/badge/Author-Iker García Ferrero-ff69b4"></a>

<br>
    <br>
</p>

```
Easy-Translate 是一个通过💥单行命令💥翻译大型文本文件的脚本。该工具旨在为**初学者**提供最简单易用的体验，同时为高级用户保持**无缝衔接**和**高度可定制**的特性。
我们支持几乎所有主流模型，包括 [M2M100](https://arxiv.org/pdf/2010.11125.pdf)、
[NLLB200](https://research.facebook.com/publications/no-language-left-behind/)、
[LLaMA](https://ai.facebook.com/blog/large-language-model-llama-meta-ai/)、
[Bloom](https://bigscience.notion.site/BLOOM-BigScience-176B-Model-ad073ca07cdf479398d5f95d88e218c4) 等更多模型 🥳。
我们还提供了用于[评估翻译结果](#evaluate-translations)的脚本 📋
```

Easy Translate建立在🤗HuggingFace's [Transformers](https://huggingface.co/docs/transformers/index) 和 🤗HuggingFace's [Accelerate](https://huggingface.co/docs/accelerate/index) 仓库.


我们目前支持：
-CPU/多CPU/GPU/多GPU/TPU加速
-BF16/FP16/FP32/8位/4位精度。
-自动批量查找器：忘记CUDA OOM错误。设置初始批量大小，如果不合适，我们将自动调整它。
-多种解码策略：贪婪搜索、波束搜索、Top-K采样、Top-p（核）采样等。有关更多信息，请参阅[解码策略]（#解码采样策略）。
-：新增：在单个GPU中加载大型模型，采用8位/4位量化，并支持在GPU和CPU之间分割模型。有关更多信息，请参阅[加载大型模型]（#加载大型模型）。
-：新增：支持LoRA模型-：new：支持HuggingFace Hub的任何Seq2SeqLM或CausalLM模型。
-：新增：及时支持！有关更多信息，请参阅[提示]（#promining）。
>测试🔌 在线演示：<https://huggingface.co/spaces/Iker/Translate-100-languages>



##支持的语言

有关支持的语言及其ID的表，请参阅[支持的语言表]（Supported_languages.md）。



##支持的型号💥 
EasyTranslate现在支持以下任何Seq2SeqLM（m2m100、nllb200、small100、mbart、MarianMT、T5、FlanT5等）和任何CausalLM（GPT2、LLaMA、Vicuna、Falcon）模型🤗 拥抱脸的枢纽！！
我们仍然建议您使用M2M100或NLLB200以获得最佳结果，但您可以尝试任何其他MT模型，以及提示LLM生成翻译（有关更多详细信息，请参阅[提示部分]（#promining））。
您还可以查看[示例文件夹]（示例），了解如何将EasyTranslate用于不同模型的示例。

### M2M100
**M2M100** 是基于论文[《Beyond English-Centric Multilingual Machine Translation》](https://arxiv.org/pdf/2010.11125.pdf)提出的多语言编码器-解码器模型，首次发布于[此代码库](https://github.com/pytorch/fairseq/tree/master/examples/m2m_100)。
>M2M100 可直接在 100 种语言的 9,900 个方向之间进行翻译。

- **Facebook/m2m100_418M**: <https://huggingface.co/facebook/m2m100_418M>

- **Facebook/m2m100_1.2B**: <https://huggingface.co/facebook/m2m100_1.2B>

- **Facebook/m2m100_12B**: <https://huggingface.co/facebook/m2m100-12B-avg-5-ckpt>

### NLLB200

**No Language Left Behind（NLLB）：**开源模型能够直接在200多种语言之间提供高质量的翻译，包括阿斯图里亚斯语、卢安达语、乌尔都语等低资源语言。它旨在帮助人们在任何地方与任何人交流，无论他们的语言偏好如何。本文对此进行了介绍(https://research.facebook.com/publications/no-language-left-behind/)首次发布于[此](https://github.com/facebookresearch/fairseq/tree/nllb)存储库。
>NLLB可以直接翻译200多种语言中的40000多种。

- **facebook/nllb-moe-54b**: <https://huggingface.co/facebook/nllb-moe-54b> (需要 transformers 4.28.0)

- **facebook/nllb-200-3.3B**: <https://huggingface.co/facebook/nllb-200-3.3B>

- **facebook/nllb-200-1.3B**: <https://huggingface.co/facebook/nllb-200-1.3B>

- **facebook/nllb-200-distilled-1.3B**: <https://huggingface.co/facebook/nllb-200-distilled-1.3B>

- **facebook/nllb-200-distilled-600M**: <https://huggingface.co/facebook/nllb-200-distilled-600M>

###支持的其他MT型号
我们支持 🤗 Hugging Face仓库中的每种MT模型。
如果你发现一个模型不起作用，请为我们打开一个问题来修复它，或者打开一个带有修复的PR。其中包括：
- **Small100**: <https://huggingface.co/alirezamsh/small100>
- **Mbart 多对多 / 多对一**: <https://huggingface.co/facebook/mbart-large-50-many-to-many-mmt>
- **作品 MT**: <https://huggingface.co/Helsinki-NLP/opus-mt-es-en>



## 引文
如果您使用此软件，请引用
````
@inproceedings{garcia-ferrero-etal-2022-model,
    title = "Model and Data Transfer for Cross-Lingual Sequence Labelling in Zero-Resource Settings",
    author = "Garc{\'\i}a-Ferrero, Iker  and
      Agerri, Rodrigo  and
      Rigau, German",
    booktitle = "Findings of the Association for Computational Linguistics: EMNLP 2022",
    month = dec,
    year = "2022",
    address = "Abu Dhabi, United Arab Emirates",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2022.findings-emnlp.478",
    pages = "6403--6416",
}
````

## 要求

```
Pytorch >= 1.10.0 
请参阅: https://pytorch.org/get-started/locally/

Accelerate >= 0.12.0
pip install accelerate

HuggingFace Transformers 
如果你计划使用 NLLB200, 请使用 >= 4.28.0 版本, 因为此版本修复了重大BUG. 
pip install --upgrade transformers

BitsAndBytes (可选, required for 8-bits / 4-bits quantization)
pip install bitsandbytes

PEFT (可选, 加载LoRA型号时需要)
pip install peft
```

## 翻译文件

运行 `python translate.py -h` 获取更多信息.   

# 有关如何运行不同模型的示例，请参阅[示例文件夹]（示例）#
See [the examples folder](examples) for examples of how to run different models. 

#### 使用单个CPU/GPU

```bash
python3 translate.py \
--sentences_path sample_text/en.txt \
--output_path sample_text/en2es.translation.m2m100_1.2B.txt \
--source_lang en \
--target_lang es \
--model_name facebook/m2m100_1.2B
```

#### 使用多个CPU/GPU
#### Multi-GPU

有关更多信息（多节点、TPU、分片模型…），请参阅Accelerate文档：: <https://huggingface.co/docs/accelerate/index>  
您可以使用Accelerate CLI配置Accelerate环境（在终端中运行`Accelerate config`），而不是使用`-multi_gpu和--num_processes`标志。
```bash
# Use 2 GPUs
accelerate launch --multi_gpu --num_processes 2 --num_machines 1 translate.py \
--sentences_path sample_text/en.txt \
--output_path sample_text/en2es.translation.m2m100_1.2B.txt \
--source_lang en \
--target_lang es \
--model_name facebook/m2m100_1.2B
```

####自动批量查找器

我们将自动找到适合您GPU内存的批量大小。默认的初始批大小为128（您可以使用“--starting_batch_size 128”标志进行设置）。如果我们发现内存不足错误，我们将自动减小批大小，直到找到一个可用的批大小。

### 加载大型模型

通过 8-bit 和 4-bit 量化技术，可以在单 GPU 上加载 LLaMA 65B 或 nllb-moe-54b 等超大规模模型，且性能损失极小。
详见 [BitsAndBytes](https://github.com/TimDettmers/bitsandbytes)。使用 `--precision` 参数设置精度为 8 或 4。

```bash
pip install bitsandbytes

python3 translate.py \
--sentences_path sample_text/en.txt \
--output_path sample_text/en2es.translation.nllb200-moe-54B.txt \
--source_lang eng_Latn \
--target_lang spa_Latn \
--model_name facebook/nllb-moe-54b \
--precision 8 \
--force_auto_device_map \
--starting_batch_size 8
```

若量化后的模型仍无法放入 GPU 显存，可设置 `--force_auto_device_map` 参数。
该功能会将模型拆分到多个 GPU 和 CPU 内存中，虽然 CPU 卸载会降低速度，但能运行远超单卡显存容量的大型模型。



###提示

您可以使用LLMs，如LLaMA、Vicuna、GPT2、FlanT5等，而不是翻译模型。这些模型需要
定义任务的提示。您可以在输入文件中已有提示（每句话都包含提示）
或者，您可以使用“--prompt”标志将提示添加到每个句子中。在这种情况下，您需要在提示中包含标记%%SENTENCE%%。
此标记将被要翻译的句子替换。在这种情况下，您不需要指定“--source_lang”和“--target_lang”标志。

```bash
python3 translate.py \
--sentences_path sample_text/en.txt \
--output_path sample_text/en2es.FlanT5.translation.txt \
--model_name google/flan-t5-large \
--prompt "Translate English to Spanish: %%SENTENCE%%" 
``` 


###解码/采样策略

您可以选择要使用的解码/采样策略以及每个输入句子要输出的候选翻译数量。
默认情况下，我们将使用“num_beams”设置为5的beam搜索，并输出最可能的候选翻译。这应该是最好的了
大多数用例的配置。您可以使用以下标志更改此行为：

```bash
--num_beams: Number of beams to use for beam-search decoding (default: 5)
--do_sample: Whether to use sampling instead of beam-search decoding (default: False)
--temperature: Sampling temperature (default: 0.8)
--top_k: Top k sampling (default: 100)
--top_p: Top p sampling (default: 0.75)
--repetition_penalty: Repetition penalty (default: 1.0)
--keep_special_tokens: Whether to keep special tokens (default: False)
--keep_tokenization_spaces: Whether to keep tokenization spaces (default: False)
--num_return_sequences: Number of candidate translations to output for each input sentence (default: 1)
```
请注意，运行`--do_sample`，其中`--num_beams`>1和`8 bits`或`4 bits`量化可能在数值上不稳定并产生错误。


## 评估翻译

要运行评估脚本，您需要安装 [bert_score](https://github.com/Tiiiger/bert_score): `pip install bert_score` 和 🤗HuggingFace [Evaluate](https://huggingface.co/docs/evaluate) 的模型: `pip install evaluate`.

评估脚本将计算以下指标：

- [SacreBLEU](https://github.com/huggingface/datasets/tree/master/metrics/sacrebleu)
- [BLEU](https://github.com/huggingface/datasets/tree/master/metrics/bleu)
- [ROUGE](https://github.com/huggingface/datasets/tree/master/metrics/rouge)
- [METEOR](https://github.com/huggingface/datasets/tree/master/metrics/meteor)
- [TER](https://github.com/huggingface/datasets/tree/master/metrics/ter)
- [BertScore](https://github.com/huggingface/datasets/tree/master/metrics/bertscore)

运行以下命令以评估翻译：

```bash
python3 eval.py \
--pred_path sample_text/en2es.translation.m2m100_1.2B.txt \
--gold_path sample_text/es.txt 
```

如果要将结果保存到文件中，请使用`--output_path`标志。

有关示例输出，请参阅[sample_text/en2es.m2m100_1.2B.json]（sample_text/en2 es.m2m100_1.2B.json）。

