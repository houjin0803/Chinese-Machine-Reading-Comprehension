# Chinese-Machine-Comprehension

本项目是测试抽取式和文摘生成式机器阅读理解模型及Anti-terrorism-security数据集。

## 模型

### CMRC-Bert 模型

文件夹cmrc2018是CMRC-Bert模型的源代码，使用此模型来测试Anti-terrorism-security数据集。CMRC-Bert模型的运行环境配置以及项目启动请参考子文件夹baseline中的README文件。

### 自动文摘生成模型

文件夹Extractable-automatic-Text-master是自动文摘生成模型的源代码，使用此模型来测试Anti-terrorism-security数据集。自动文摘生成模型的运行环境配置以及项目启动请参考其目录下的README文件。

## 数据集

### Anti-terrorism-security数据集

Anti-terrorism-security数据集放在data文件夹下，其数据格式是参照SQuAD数据集的格式，使用transform封装的BERT fine-tunning，参考 [Fine-tuning on SQuAD](https://huggingface.co/transformers/examples.html#fine-tuning-on-squad)。你可以通过以下方式快速加载数据集：

```
from Chinese-Machine-Comprehension/data import load_dataset
dataset = load_dataset('data')
```

## 依赖要求

这里没有什么特殊的依赖需求，除了' TensorFlow==1.12 '。也可以使用其他版本的TensorFlow(未测试)。

该代码基于“run_squad.py”的官方BERT实现。

详情请查看：https://github.com/google-research/bert/blob/master/run_squad.py

## CMRC2018模型使用方法

### step1：下载BERT weights

- [Chinese (base)](https://storage.googleapis.com/bert_models/2018_11_03/chinese_L-12_H-768_A-12.zip)
- [Multi-lingual (base)](https://storage.googleapis.com/bert_models/2018_11_23/multi_cased_L-12_H-768_A-12.zip)

### step 2：设置环境变量

- `$PATH_TO_BERT`：BERT weights的路径
- `$DATA_DIR`：数据集的路径
- `$MODEL_DIR`：模型的输出路径

### step3：模型的训练

通过以上步骤的设置之后，可以使用以下脚本进行训练。

```
python run_cmrc2018_drcd_baseline.py \
	--vocab_file=${PATH_TO_BERT}/multi_cased_L-12_H-768_A-12/vocab.txt \
	--bert_config_file=${PATH_TO_BERT}/multi_cased_L-12_H-768_A-12/bert_config.json \
	--init_checkpoint=${PATH_TO_BERT}/multi_cased_L-12_H-768_A-12/bert_model.ckpt \
	--do_train=True \
	--train_file=${DATA_DIR}/cmrc2018_train.json \
	--do_predict=True \
	--predict_file=${DATA_DIR}/cmrc2018_dev.json \
	--train_batch_size=32 \
	--num_train_epochs=2 \
	--max_seq_length=512 \
	--doc_stride=128 \
	--learning_rate=3e-5 \
	--save_checkpoints_steps=1000 \
	--output_dir=${MODEL_DIR} \
	--do_lower_case=False \
	--use_tpu=False
```

### step4：评估

我们使用CMRC2018官方的评估脚本来进行评估。请将模型预测生成的dev_predictions.json文件放在data文件夹中，执行以下命令：

`cd data`
`python cmrc2018_evaluate.py dev.json dev_predictions.json`

## 实验结果
F1为76.286%，EM为50.980%。
## 联系我们
如果你遇到问题，请通过github提交你的问题。
