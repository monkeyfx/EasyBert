# EasyBert
基于Pytorch的Bert应用，包括命名实体识别、情感分析、文本分类以及文本相似度等(后续更新其他方向相关模块)，并有相关数据与深度训练优化方式api。各个子项目大都为开源工作，本项目仅做相应处理以及提供一个已训练的预测接口，方便需求者进行快速的使用。本项目仅作为学习与研究使用，若存在侵权行为，请原作者务必联系我进行协商处理。



# 使用示例

1. 使用前需下载相应的已训练模型，并导入相应位置

   模型下载地址：

2. 在此目录下各以需求名命名的文件中提供相应的使用演示，本阶段所训练的模型效果可以满足相应任务的基本需求。

3. 现阶段通过各任务接口的时间相对慢，大都是在模型加载阶段。若想提升相应的速度，请使用者在接受相应精度损失的前提下更换AlBert进行相应任务的重新预训练。

# 依赖项

## 环境依赖

```
python >= 3.7 Pytorch >= 1.14 transformers >= 2.8.0
注：作者实验环境，其他环境未测试
```

## 硬件依赖

1. 预测与使用在普通cpu机器上既可以运行
2. 重新训练任务需要在GPU机器上进行，当内存不够用时，推荐减少batch_size而不是max_sequence_len，对精度影响较小

# 使用说明

- 注：各个模块的文本输入方式均为List，具体形式请参照文件。

## 情感分析 Sentiment.py

原始训练数据：该部分原数据因项目原因不提供，如需重新训练可更换其他开源数据集.

```python
test = ['#你好2020#新年第一天元气满满的早起出门买早饭结果高估了自己抗冻能力回家成功冻发烧（大概是想告诉我2020要量力而行）然鹅这并不影响后续计划一出门立马生龙活虎新年和新??更配哦??看了误杀吃了大餐就让新的一年一直这样美滋滋下去吧??',
'大宝又感冒鼻塞咳嗽了，还有发烧。队友加班几天不回。感觉自己的情绪在家已然是随时引爆的状态。情绪一上来，容易对孩子说出自己都想不到的话来……2020年，真的要学会控制情绪，管理好家人健康。这是今年最大的目标。?',
'还要去输两天液，这天也太容易感冒发烧了，一定要多喝热水啊?',
'我太难了别人怎么发烧都没事就我一检查甲型流感?',
'果然是要病一场的喽回来第三天开始感冒今儿还发烧了喉咙眼睛都难受的一匹怎么样能不经意让我的毕设导师看到这条微博并给我放一天假呢?']
predict(test)

'''结果：
text:#你好2020#新年第一天元气满满的早起出门买早饭结果高估了自己抗冻能力回家成功冻发烧（大概是想告诉我2020要量力而行）然鹅这并不影响后续计划一出门立马生龙活虎新年和新??更配哦??看了误杀吃了大餐就让新的一年一直这样美滋滋下去吧??
label:中性
text:大宝又感冒鼻塞咳嗽了，还有发烧。队友加班几天不回。感觉自己的情绪在家已然是随时引爆的状态。情绪一上来，容易对孩子说出自己都想不到的话来……2020年，真的要学会控制情绪，管理好家人健康。这是今年最大的目标。?
label:消极
text:还要去输两天液，这天也太容易感冒发烧了，一定要多喝热水啊?
label:中性
text:我太难了别人怎么发烧都没事就我一检查甲型流感?
label:消极
text:果然是要病一场的喽回来第三天开始感冒今儿还发烧了喉咙眼睛都难受的一匹怎么样能不经意让我的毕设导师看到这条微博并给我放一天假呢?
label:消极
'''
```

## 文本分类  TextClassifier.py

```python
结果：
text:国考28日网上查报名序号查询后务必牢记报名参加2011年国家公务员的考生，如果您已通过资格审查，那么请于10月28日8：00后，登录考录专题网站查询自己的“关键数字”——报名序号。国家公务员局等部门提醒：报名序号是报考人员报名确认和下载打印准考证等事项的重要依据和关键字，请务必牢记。此外，由于年龄在35周岁以上、40周岁以下的应届毕业硕士研究生和博士研究生(非在职)，不通过网络进行报名，所以，这类人报名须直接与要报考的招录机关联系，通过电话传真或发送电子邮件等方式报名。
label:教育
text:高品质低价格东芝L315双核本3999元作者：徐彬【北京行情】2月20日东芝SatelliteL300(参数图片文章评论)采用14.1英寸WXGA宽屏幕设计，配备了IntelPentiumDual-CoreT2390双核处理器(1.86GHz主频/1MB二级缓存/533MHz前端总线)、IntelGM965芯片组、1GBDDR2内存、120GB硬盘、DVD刻录光驱和IntelGMAX3100集成显卡。目前，它的经销商报价为3999元。
label:科技
text:国安少帅曾两度出山救危局他已托起京师一代才俊新浪体育讯随着联赛中的连续不胜，卫冕冠军北京国安的队员心里到了崩溃的边缘，俱乐部董事会连夜开会做出了更换主教练洪元硕的决定。而接替洪元硕的，正是上赛季在李章洙下课风波中同样下课的国安俱乐部副总魏克兴。生于1963年的魏克兴球员时代并没有特别辉煌的履历，但也绝对称得上特别：15岁在北京青年队获青年联赛最佳射手，22岁进入国家队，著名的5-19一战中，他是国家队的替补队员。
label:体育
text:汤盈盈撞人心情未平复眼泛泪光拒谈悔意(附图)新浪娱乐讯汤盈盈日前醉驾撞车伤人被捕，原本要彩排《欢乐满东华2008》的她因而缺席，直至昨日(12月2日)，盈盈继续要与王君馨、马赛、胡定欣等彩排，大批记者在电视城守候，她足足迟了约1小时才到场。全身黑衣打扮的盈盈，神情落寞、木无表情，回答记者问题时更眼泛泪光。盈盈因为迟到，向记者说声“不好意思”后便急步入场，其助手坦言盈盈没什么可以讲。后来在《欢乐满东华2008》监制何小慧陪同下，盈盈接受简短访问，她小声地说：“多谢大家关心，交给警方处理了，不方便讲，
label:娱乐
text:甲醇期货今日挂牌上市继上半年焦炭、铅期货上市后，酝酿已久的甲醇期货将在今日正式挂牌交易。基准价均为3050元／吨继上半年焦炭、铅期货上市后，酝酿已久的甲醇期货将在今日正式挂牌交易。郑州商品交易所（郑商所）昨日公布首批甲醇期货8合约的上市挂牌基准价，均为3050元／吨。据此推算，买卖一手甲醇合约至少需要12200元。业内人士认为，作为国际市场上的首个甲醇期货品种，其今日挂牌后可能会因炒新资金追捧而出现冲高走势，脉冲式行情过后可能有所回落，不过，投资者在上市初期应关注期现价差异常带来的无风险套利交易机会。
label:财经

```

## 命名实体识别 NER.py

```python
text=["四川敦煌学”。近年来，丹棱县等地一些不知名的石窟迎来了海内外的游客，他们随身携带着胡文和的著作。",
      "尼日利亚海军发言人当天在阿布贾向尼日利亚通讯社证实了这一消息。",
      "单看这张彩票，税前总奖金为5063992元。本张票面缩水后阿森纳的结果全部为0，斯图加特全部为1，",
      "你会和星级厨师一道先从巴塞罗那市中心兰布拉大道的laboqueria市场的开始挑选食材，",
      "波特与凤凰社》的率队下更加红火。乘着7月的上升气流，《发胶》、《辛普森一家》、《谍影憧憧ⅲ》"]
pos_predict(text)


'''
结果：
{'text': '四川敦煌学”。近年来，丹棱县等地一些不知名的石窟迎来了海内外的游客，他们随身携带着胡文和的著作。', 
'label': {'organization': {'四川敦煌学': [[0, 4]]}, 'address': {'丹棱县': [[11, 13]]}, 'name': {'胡文和': [[41, 43]]}}}
{'text': '尼日利亚海军发言人当天在阿布贾向尼日利亚通讯社证实了这一消息。', 
'label': {'government': {'尼日利亚海军': [[0, 5]]}, 'address': {'阿布贾': [[12, 14]]}, 'company': {'尼日利亚通讯社': [[16, 22]]}}}
{'text': '单看这张彩票，税前总奖金为5063992元。本张票面缩水后阿森纳的结果全部为0，斯图加特全部为1，', 
'label': {'organization': {'阿森纳': [[29, 31]], '斯图加特': [[40, 43]]}}}
{'text': '你会和星级厨师一道先从巴塞罗那市中心兰布拉大道的laboqueria市场的开始挑选食材，', 'label': {'position': {'厨师': [[5, 6]]}, 'address': {'巴塞罗那市中心兰布拉大道的': [[11, 23]], 'laboqueria市场': [[24, 35]]}}}
{'text': '波特与凤凰社》的率队下更加红火。乘着7月的上升气流，《发胶》、《辛普森一家》、《谍影憧憧ⅲ》', 
'label': {'movie': {'波特与凤凰社》': [[0, 6]], '《发胶》': [[26, 29]], '《辛普森一家》': [[31, 37]], '《谍影憧憧ⅲ》': [[39, 45]]}}}
'''
```



## 文本相似度 TextMatch.py

```python
text = [['谁有狂三这张高清的', '这张高清图，谁有'],
		['英雄联盟什么英雄最好', '英雄联盟最好英雄是什么'],
		['这是什么意思，被蹭网吗', '我也是醉了，这是什么意思'],
		['现在有什么动画片好看呢？', '现在有什么好看的动画片吗？'],
		['请问晶达电子厂现在的工资待遇怎么样要求有哪些', '三星电子厂工资待遇怎么样啊']]
result = main(text)

'''
结果：
    ========== Predict Result ==========
    ['谁有狂三这张高清的', '这张高清图，谁有', '相似']
    ['英雄联盟什么英雄最好', '英雄联盟最好英雄是什么', '不相似']
    ['这是什么意思，被蹭网吗', '我也是醉了，这是什么意思', '不相似']
    ['现在有什么动画片好看呢？', '现在有什么好看的动画片吗？', '不相似']
    ['请问晶达电子厂现在的工资待遇怎么样要求有哪些', '三星电子厂工资待遇怎么样啊', '相似']
'''
```

## 文本增强

1. EDA
2. 回译

注：暂时没有提供接口进行集成，已写好相关功能主函数及附带使用例子，若需可自行调。

## 训练优化

1. EMA 指数滑动平均
2. FGM 对抗训练api
3. PGD 对抗训练api

相关源代码已有优秀开源，本项目借鉴训练时部分加入相关训练优化trcik，部分保持原始代码复现格式，若需相关训练优化功能，相关代码及使用方式已给出，按需使用。

```python
# 权重滑动平均，对最近的数据给予更高的权重
uasge：
# 初始化
ema = EMA(model, 0.999)
ema.register()

# 训练过程中，更新完参数后，同步update shadow weights
def train():
    optimizer.step()
    ema.update()

    # eval前，apply shadow weights；
    # eval之后（保存模型后），恢复原来模型的参数
    def evaluate():
        ema.apply_shadow()
        # evaluate
        ema.restore()
```



# 后续工作

1. 关系抽取，此部分实验作者正在进行检测。
2. 文本翻译



# 资料参考

致谢！

[https://github.com/lonePatient/BERT-NER-Pytorch](https://github.com/lonePatient/BERT-NER-Pytorch)

https://github.com/649453932/Bert-Chinese-Text-Classification-Pytorch

https://github.com/zhaogaofeng611/TextMatch

https://github.com/yongzhuo/nlp_xiaojiang

[https://fyubang.com/2019/10/15/adversarial-train/](https://fyubang.com/2019/10/15/adversarial-train/)

[https://zhuanlan.zhihu.com/p/68748778](https://zhuanlan.zhihu.com/p/68748778)