# 🔥 Language Interpretability Tool (LIT)

语言可解释性工具（LIT）是一种可视的，交互式的
用于NLP模型的模型理解工具。

LIT旨在回答以下问题：
* **哪种示例**在我的模型上效果不佳？
* **为什么我的模型做出此预测？**该预测可以归因于对抗行为还是训练集中的不良先验？
* **如果我更改文本样式，动词时态或代词性别之类的内容，我的模型是否会表现一致**？

![Example of LIT UI](docs/images/figure-1.png)

LIT通过基于浏览器的UI支持各种调试工作流。
功能包括：

* **Local explanations** 通过显着图，注意力和丰富的模型预测可视化。
* **Aggregate analysis**，包括自定义指标，切片和binning以及嵌入空间的可视化。
* **Counterfactual generation**, 通过编辑或生成器插件来真实生成，以动态创建和评估新示例。
* **Side-by-side mode**, 比较两个或多个模型，或一对示例中的一个模型。
* **Highly extensible**到新模型类型，包括分类，回归，跨度标签，seq2seq和语言建模。 开箱即用地支持multi-head 模型和多种输入特征。
* **与框架无关**，与TensorFlow，PyTorch等兼容。

有关更广泛的概述，请查看[our paper](https://arxiv.org/abs/2008.05122) 和[user guide](docs/user_guide.md)。

## Documentation
*   [User Guide](docs/user_guide.md)
*   [Developer Guide](docs/development.md)
*   [FAQ](docs/faq.md)

## Download and Installation

下载repo并设置Python环境：

```sh
git clone https://github.com/PAIR-code/lit.git ~/lit

# Set up Python environment
cd ~/lit
conda env create -f environment.yml
conda activate lit-nlp
conda install cudnn cupti  # optional, for GPU support
conda install -c pytorch pytorch  # optional, for PyTorch

# Build the frontend
cd ~/lit/lit_nlp/client
yarn && yarn build
```

## Running LIT

### Quick-start: sentiment classifier

```sh
cd ~/lit
python -m lit_nlp.examples.quickstart_sst_demo --port=5432
```

这将在[Stanford Sentiment Treebank](https://nlp.stanford.edu/sentiment/treebank.html)上微调[BERT-tiny](https://arxiv.org/abs/1908.08962)模型， 
在GPU上的时间应该少于5分钟。 训练完成后，在开发集上启动LIT服务； http://localhost:5432作为用户界面。


### Quick start: language modeling

要探索预训练的语言模型（BERT或GPT-2）的预测，请运行：

```sh
cd ~/lit
python -m lit_nlp.examples.pretrained_lm_demo --models=bert-base-uncased \
  --port=5432
```

And navigate to http://localhost:5432 for the UI.

### More Examples

See ../lit_nlp/examples. Run similarly to the above:

```sh
cd ~/lit
python -m lit_nlp.examples.<example_name> --port=5432 [optional --args]
```

## User Guide

要了解LIT的功能， check out the [user guide](docs/user_guide.md), or
watch this [short video](https://www.youtube.com/watch?v=j0OfBWFUqIE).

## 添加自己的模型或数据

您可以通过创建自定义`demo.py`启动器来轻松地使用自己的模型运行LIT，
类似于../lit_nlp/examples。 基础的步骤是：

*   Write a data loader which follows the
    [`Dataset` API](docs/python_api.md#datasets)
*   Write a model wrapper which follows the [`Model` API](docs/python_api.md#models)
*   Pass models, datasets, and any additional
    [components](docs/python_api.md#interpretation-components) to the LIT server class

有关完整的演练， see
[adding models and data](docs/python_api.md#adding-models-and-data).

## 用新组件扩展LIT

LIT易于在前端或后端使用新的可解释性组件，生成器等进行扩展。 见
[developer guide](docs/development.md) to get started.

## Citing LIT

If you use LIT as part of your work, please cite:

```
@misc{tenney2020language,
    title={The Language Interpretability Tool: Extensible, Interactive Visualizations and Analysis for NLP Models},
    author={Ian Tenney and James Wexler and Jasmijn Bastings and Tolga Bolukbasi and Andy Coenen and Sebastian Gehrmann and Ellen Jiang and Mahima Pushkarna and Carey Radebaugh and Emily Reif and Ann Yuan},
    year={2020},
    eprint={2008.05122},
    archivePrefix={arXiv},
    primaryClass={cs.CL}
}
```

## Disclaimer

This is not an official Google product.
