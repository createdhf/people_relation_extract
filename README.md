&emsp;&emsp;运行该项目的模型训练和模型预测脚本需要准备BERT中文版的模型数据，下载网址为：[https://github.com/google-research/bert/blob/master/multilingual.md](https://github.com/google-research/bert/blob/master/multilingual.md) 。

&emsp;&emsp;利用笔者自己收集的2826个样本，对人物关系抽取进行尝试。人物关系共分为14类，如下：

```json
{
  "unknown": 0,
  "夫妻": 1,
  "父母": 2,
  "兄弟姐妹": 3,
  "上下级": 4,
  "师生": 5,
  "好友": 6,
  "同学": 7,
  "合作": 8,
  "同人": 9,
  "情侣": 10,
  "祖孙": 11,
  "同门": 12,
  "亲戚": 13
}
```

&emsp;&emsp;人物关系类别频数分布条形图如下：

![](https://github.com/percent4/people_relation_extract/blob/master/data/bar_chart.png)

&emsp;&emsp;模型结构： BERT + 双向GRU + Attention + FC 

![](https://github.com/percent4/people_relation_extract/blob/master/model.png)

&emsp;&emsp;模型训练效果：

![](https://github.com/percent4/people_relation_extract/blob/master/loss_acc.png)

```
# 训练集(train), loss: 0.0211, acc: 0.9956
# 最终测试集(test),  loss: 1.0226, acc: 0.7858
# 测试集上效果最好的,  loss: 0.8052, acc: 0.8106
```

&emsp;&emsp;模型预测：

```
原文: 润生#润叶#不过，他对润生的姐姐润叶倒怀有一种亲切的感情。
预测人物关系: 兄弟姐妹
原文: 孙玉厚#兰花#脑子里把前后村庄未嫁的女子一个个想过去，最后选定了双水村孙玉厚的大女子兰花。
预测人物关系: 父母
原文: 金波#田福堂#每天来回二十里路，与他一块上学的金波和大队书记田福堂的儿子润生都有自行车，只有他是两条腿走路。
预测人物关系: unknown
原文: 润生#田福堂#每天来回二十里路，与他一块上学的金波和大队书记田福堂的儿子润生都有自行车，只有他是两条腿走路。
预测人物关系: 父母
原文: 周山#李自成#周山原是李自成亲手提拔的将领，闯王对他十分信任，叫他担任中军。
预测人物关系: 上下级
原文: 高桂英#李自成#高桂英是李自成的结发妻子，今年才三十岁。
预测人物关系: 夫妻
原文: 罗斯福#特德#果然，此后罗斯福的政治旅程与长他24岁的特德叔叔如出一辙——纽约州议员、助理海军部长、纽约州州长以至美国总统。
预测人物关系: 亲戚
原文: 詹姆斯#克利夫兰#詹姆斯担任了该公司的经理，作为一名民主党人，他曾资助过克利夫兰的再度竞选，两人私交不错。
预测人物关系: 上下级
原文: 高剑父#关山月#高剑父是关山月在艺术道路上非常重要的导师，同时关山月也是最能够贯彻高剑父“折中中西”理念的得意门生。
预测人物关系: 师生
原文: 唐怡莹#唐石霞#唐怡莹，姓他他拉氏，名为他他拉·怡莹，又名唐石霞，隶属于满洲镶红旗。
预测人物关系: 同人
```

&emsp;&emsp;参考博文：

[https://www.cnblogs.com/jclian91/p/12328570.html](https://www.cnblogs.com/jclian91/p/12328570.html)