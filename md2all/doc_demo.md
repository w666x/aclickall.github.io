
```sh
排版demo
```


## 评估数据集概览


#### 数据集效果概览

- 评估模型为qwen-7B，显卡为A6000，显存占用18G

| 评估数据集 | 评估时长 | acc | rouge(action-input)| right-rate(action) | bad-rate(action) | pass@1
|:-|:-|:-|:-|:-|:-|:-
| ceval | 2min  |  60.25 | -|-|-
| mmlu | 30min  |   56.99   | -|-|-
| cmmlu | 13min |  60.26  | -|-|-
| gsm8k | 2.5h  |  50.72  | -|-|-
| plugin   | 1.5h | - | 87.13 | 96.18| 11.56|-
| HumanEval | 32min | -| -| -|-| 24.390 | -


## 评估数据集详解


### humanEval


- 1. 任务介绍
    - HumanEval基准测试在2021年提出，包含164个精心设计的Python编程问题，**这些问题通过一系列测试用例来检验代码LLMs在零样本条件下生成代码的能力。**
    - 数据集用来评估语言理解、算法和简单的数学，有一些可与简单的软件面试问题相媲美。
    

- 2. 数据demo

```python
import pandas as pd
print("this is a test")
```


### 常用评价详解


#### BLEU

- 1. 指标介绍
    - **即统计同时出现在completion（模型推理）和groud truth/gold standard（标准答案）中的n元词的个数，最后把匹配到的n元词的数目除以completion（模型推理）的单词数目，得到评测结果。**
    - 1. **一般n=2，即比较1个词、2个词**来计算
    - 2. 提出取模型completion（模型推理）N-gram的出现次数和groud truth中N-gram最大出现次数中的最小值的算法
    - 3. 针对completion长度比groud truth要短的情况，就需要一个惩罚的机制去控制，即BP啦


- 2. 优点
    - 方便、快速，结果比较接近人类评分


```python
import pandas as pd
print("this is a test")
```


- 3. 缺点
    - 1、不考虑语言表达（语法）上的准确性；
    - 2、测评精度会受常用词的干扰；
    - 3、短译句的测评精度有时会较高；
    - 4、没有考虑同义词或相似表达的情况，可能会导致合理翻译被否定；