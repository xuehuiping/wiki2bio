
2020-08-27 10:45:30

## 基本信息
北京大学 liutianyu

>Liu, T., Wang, K., Sha, L., Chang, B., & Sui, Z. (2018). Table-to-text generation by structure-aware seq2seq learning. 32nd AAAI Conference on Artificial Intelligence, AAAI 2018, 4881–4888.

>/Users/huihui/git/all_papers/E-文本生成/1711.09724.pdf

原始仓库：
https://github.com/tyliupku/wiki2bio

我用的仓库：http://git.yonyou.com/ai/wiki2bio.git

>使用数据集：WIKIBIO

>数据下载：https://pan.baidu.com/s/1c324Vs8

环境要求：`python2 + GPU + tf 1.0.0`，大约需要`36~48`小时

```
(wiki2bio) huihui@192 wiki2bio % pip install -r requirements.txt

(wiki2bio) huihui@192 wiki2bio % python preprocess.py 

extracting token, field type and position info from original data ...
extract finished in 552.693 seconds
spliting test and valid summaries for ROUGE evaluation ...
split finished in 74.528 seconds
turning words and field types to ids ...
idlization finished in 172.965 seconds
check done
````

1号机器准备数据，放入gpu机器运行
```
xuehp@haomeiya001:~$ source ~/anaconda3/bin/activate 
(base) xuehp@haomeiya001:/home/xuehp/git/wiki2bio$ conda create --name wiki2bio python=2.7 
conda activate wiki2bio

cd git/wiki2bio/
source ~/anaconda3/bin/activate 
conda activate wiki2bio
```

注意：
- 这个使用的是`infobox-to-biography`，见作者的数据演示，不是表格生成文本。和我们实际上需要的不太完全一致。
- 1号机器环境准备好了。没开始训练。
- https://wiki.yonyou.com/pages/viewpage.action?pageId=159379681

## 测试1
降低参数训练：
```
Successfully installed nltk-3.3
(wiki2bio) huihui@192 wiki2bio % python Main.py       
15 177

W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.1 instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
Reading datasets ...
['1278', '4886', '15', '10', '242', '2032', '3', '1413', '4', '339', '2235', '1136', '9', '575', '8', '4886', '3', '12', '4886', '2235', '2116', '13', '4', '10', '4717', '8', '3', '2235', '6']
['2528', '3', '3', '12', '22', '77', '174', '4', '565', '13', '15', '10', '46', '137', '39', '159', '51', '6']
['1530', '422', '1063', '8', '4089', '12', '34', '43', '21', '3', '1063', '13', '14', '5', '11511', '1530', '8', '4089', '9', '4348', '8', '5', '1022', '8', '369', '666', '12', '3', '29', '3', '13', '6']
Reading datasets comsumes 127.993 seconds
field-gated encoder LSTM
field gated encoder used
dual attention mechanism used
#######################################################
load = 0
fgate_encoder = True
emb_size = 40
pos_size = 5
field_size = 50
target_vocab = 20003
decoder_pos = True
field = False
epoch = 50
field_vocab = 1480
encoder_pos = True
hidden_size = 50
source_vocab = 20003
learning_rate = 0.0003
batch_size = 32
report = 5000
dual_attention = True
limits = 0
position_vocab = 31
mode = train
position = False
dir = processed_data
#######################################################
 [>............................................. 13/5000 .............................................]  Step: 3s703ms | Tot: 3m24s            
运行3小时
 [============================================= 5000/5000 ===========================================>]  Step: 2s370ms | Tot: 3h3m                          
1 : loss = 12852.603, time = 10935.289 ........ 1/5000 ...............................................]  Step: 1s726ms | Tot: 0ms                           

这只是一个epoch，运行完需要3*5000小时。
降低为50，再次训练
```


## 测试2

再次降低。hidden_size=5，epoch=50
```

(wiki2bio) xuehp@haomeiya001:/home/xuehp/git/wiki2bio$ python Main.py 
45 156

W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE3 instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.1 instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use SSE4.2 instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX2 instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use AVX512F instructions, but these are available on your machine and could speed up CPU computations.
W tensorflow/core/platform/cpu_feature_guard.cc:45] The TensorFlow library wasn't compiled to use FMA instructions, but these are available on your machine and could speed up CPU computations.
Reading datasets ...
['1278', '4886', '15', '10', '242', '2032', '3', '1413', '4', '339', '2235', '1136', '9', '575', '8', '4886', '3', '12', '4886', '2235', '2116', '13', '4', '10', '4717', '8', '3', '2235', '6']
['2528', '3', '3', '12', '22', '77', '174', '4', '565', '13', '15', '10', '46', '137', '39', '159', '51', '6']
['1530', '422', '1063', '8', '4089', '12', '34', '43', '21', '3', '1063', '13', '14', '5', '11511', '1530', '8', '4089', '9', '4348', '8', '5', '1022', '8', '369', '666', '12', '3', '29', '3', '13', '6']
Reading datasets comsumes 72.506 seconds
field-gated encoder LSTM
field gated encoder used
dual attention mechanism used
#######################################################
load = 0
fgate_encoder = True
emb_size = 40
pos_size = 5
field_size = 50
target_vocab = 20003
decoder_pos = True
field = False
epoch = 50
field_vocab = 1480
encoder_pos = True
hidden_size = 5
source_vocab = 20003
learning_rate = 0.0003
batch_size = 32
report = 50
dual_attention = True
limits = 0
position_vocab = 31
mode = train
position = False
dir = processed_data
#######################################################
 [============================================= 37/50 ====================>...........................]  Step: 1s210ms | Tot: 2m10s 
 [============================================= 50/50 ==============================================>.]  Step: 2s | Tot: 2m30s                              
1 : loss = 241.201, time = 78.159 ............. 1/50 .................................................]  Step: 1s712ms | Tot: 0ms 

```