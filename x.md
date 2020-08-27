
2020-08-27 10:45:30

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
(base) xuehp@haomeiya001:/home/xuehp/git/wiki2bio$ conda create -name wiki2bio python=2.7 
```

注意：
这个使用的是`infobox-to-biography`，见作者的数据演示，不是表格生成文本。和我们实际上需要的不太完全一致。
