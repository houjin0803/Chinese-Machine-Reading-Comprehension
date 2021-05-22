# Data

本文件是面向反恐安全领域的中文抽取式和生成式机器阅读理解数据集，其中dev.json是测试数据集、train.json是训练数据集。

## dev.json/train.json

### 数据结构

![反恐安全数据集结构](F:\postgraduate\MRC\code\Chinese-Machine-Comprehension\cmrc2018\data\反恐安全数据集结构.png)

### 字段含义

测试数据集中的各个字段的含义如下表所示：

| 字段         | 含义                                               |
| ------------ | -------------------------------------------------- |
| version      | 数据集的版本号                                     |
| data         | 数据集中所有数据                                   |
| paragraphs   | 数据集中的具体数据，包括文本id、文本内容、问答对等 |
| id           | 每条文本的id后者每个问题的id                       |
| context      | 文本内容                                           |
| qas          | 包含问答对的对象                                   |
| question     | 问题                                               |
| answers      | 包含答案和答案起始位置的对象                       |
| text         | 问题所对应的答案                                   |
| answer_start | 答案的起始位置                                     |
| GTquestion   | 生成式问题                                         |
| GTanswer     | 生成式答案                                         |
| title        | 每条文本所对应的标题                               |

