# PyTorch_CoSENT

## 简介

比Sentence-BERT更有效的句向量方案，复现苏神提出的[CoSENT](https://github.com/bojone/CoSENT)，模型细节可以参考苏神的文章：https://kexue.fm/archives/8847

**数据下载**

* ATEC、BQ、LCQMC和PAWSX：https://github.com/bojone/BERT-whitening/tree/main/chn
* CHIP-STS（平安医疗科技疾病问答迁移学习）：https://tianchi.aliyun.com/dataset/dataDetail?dataId=95414


## 环境

```
pip install ark-nlp
pip install pandas
```

## 使用说明

项目目录按以下格式设置

```shell
│
├── data                                    # 数据文件夹
│   ├── source_datasets                     
│   ├── task_datasets           
│   └── output_datasets                           
│
├── checkpoint                              # 存放训练好的模型
│   ├── ...           
│   └── ...                                      
│
└── code                                    # 代码
```
下载数据并解压到`data/source_datasets`中，运行`code`文件夹中的`.ipynb`文件，最终提交文件会生成在`data/output_datasets`

## 参数设置

代码参数设置如下：

```
句子截断长度：64（PAWSX数据集截断长度为128）
batch_size：32
epochs：5
```


## 效果

使用spearman系数作为测评指标，ATEC、BQ、LCQMC和PAWSX使用test集进行测试实验，CHIP-STS则使用验证集

| | ATEC | BQ | LCQMC | PAWSX | CHIP-STS |
| :-: | :-: | :-: | :-: | :-: | :-: |
| BERT+CoSENT（ark-nlp） | 49.80 | 72.46 | 79.00 | 59.17 |  76.22 |
| BERT+CoSENT（bert4keras） | 49.74 | 72.38 | 78.69 | 60.00 |  |
| Sentence-BERT（bert4keras）| 46.36 | 70.36 | 78.72 | 46.86 |   |

PS：上表ark-nlp展示的是5轮里最好的结果，由于没有深入了解bert4keras，所以设置参数可能还是存在差异，因此对比仅供参考

针对CHIP-STS测试数据集，选择阈值为0.6生成结果进行提交，结果如下：

| | Precision | Recall | Macro-F1|
| :-: | :-: | :-: | :-:|
| BERT+CoSENT| 82.89 | 81.528	 | 81.688	|
| BERT句子对分类 | 84.331 | 83.799 | 83.924| 


## Acknowledge

  感谢苏神无私的分享