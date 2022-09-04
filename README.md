# 谁是卧底

> 适用于 [Mirai](https://github.com/mamoe/mirai) 的谁是卧底小游戏插件

### [Github Project](https://github.com/Mitr-yuzr/WhoIsSpy)
### [Release](https://github.com/Mitr-yuzr/WhoIsSpy/releases/tag/1.0)
### [MiraiForum](https://mirai.mamoe.net/topic/1580/whoisspy-%E8%B0%81%E6%98%AF%E5%8D%A7%E5%BA%95%E5%B0%8F%E6%B8%B8%E6%88%8F%E6%8F%92%E4%BB%B6)

## 说明

本插件目的是为了**方便发词条、流程控制、统计投票与判断输赢**，具体游戏内容仍需玩家自己进行和维护。  

进行游戏最少需要四名玩家，不需要权限和调用命令，请注意设置的命令不要重复或是与其他插件重复。  

添加词库请自行在`\data\net.reincarnatey.spy\SpyData.yml`中追加。  

## 使用方法

### 使用前

请确保`SpyData.yml`词库内存在词条，否则无法正常开始游戏。  

可下载 [Release](https://github.com/Mitr-yuzr/WhoIsSpy/releases/tag/1.0) 中附带的`data.zip`(从网络中收集的约500个词的词库)，并将其解压到mcl根目录下。

### 游戏规则

> 标准模式下，每个玩家会拿到自己的词条，其中卧底的词条与其他人的不一样！每个玩家需要轮流描述自己的词，描述不能重复，若出现自己的词则直接判输。之后进行投票选出卧底。票数最多的玩家将会被淘汰。一直重复下去，直到卧底被淘汰或卧底的人数占剩余玩家总数大于等于三分之一。

### 胜利目标

> 普通玩家: 将所有卧底淘汰  
> 卧底: 存活到最后    
> 白板: 存活到最后  

### 创建游戏

在聊天内发送`创建谁是卧底`即可，接下来进入准备流程。  

也可发送`谁是卧底规则`查看游戏规则。

### 准备流程

发送`加入`即可加入游戏中，可发送`当前玩家`可查看已加入的玩家。  

发送`模式 编号`可以切换至对应的模式

> 默认为标准模式，可通过"模式 1/2/3"切换至其他模式  
> 1.标准模式: 仅有1个卧底  
> 2.多卧底模式: 适用于人较多的情况，四分之一玩家为卧底  
> 3.随机白板模式: 将随机一部分玩家为白板(不超过四分之一)
> 
> 特殊模式: 所有玩家均为白板。可输入114514切换至该模式，也会随机强制进入该模式(不提醒)。可通过设置配置项的specialModeOdds来修改概率，概率为0时为不启用该模式。

当 玩家人数 ≥ 4 时，可发送`开始`以开始游戏。

### 词条分发

将会自动私聊每一位玩家发送该玩家的词条 (若为白板则无词条内容，但是会发送私聊提醒)。  
为避免收不到消息的特殊情况，推荐所有玩家开始游戏前先添加好友。

### 描述阶段

未被淘汰的每名玩家需要轮流用一句话描述自己的词语。  

插件只会记录是否所有人都发言过了，需要玩家自觉按序描述，不推荐该阶段进行交流。  
如果描述中包含有该玩家的词语，则会直接判为违反规则并**立即结束游戏**。  

当剩余所有玩家都描述后，由其中一名玩家发送`结束`以结束描述阶段。

### 投票阶段

未被淘汰的每名玩家需要发送`投票 编号`进行投票。

该阶段可进行交流分析和推理。  
淘汰的玩家不可投票，玩家不可投给淘汰的玩家，玩家可以投给自己，当玩家投给编号0时表示弃票。  

最后获得票数最多的被淘汰，平票时不淘汰，剩余玩家回到描述阶段继续进行游戏，直到满足游戏结束条件。

> 剩余3名玩家、卧底被淘汰、卧底人数大于等于剩余玩家总数的三分之一

### 游戏结束

结束时会公开普通词条与卧底词条，并公开所有参与玩家的身份。  
之后可再次通过`创建谁是卧底`重新开始游戏。

## 插件配置

位于`\config\net.reincarnatey.spy\SpyConfig.yml`

```yaml
# 创建触发器
createTriggers: 
  - 创建谁是卧底
# 加入触发器
joinTriggers: 
  - 加入
  - 加入谁是卧底
# 当前玩家触发器
showTriggers: 
  - 当前玩家
  - 玩家列表
# 切换模式触发器
modeTriggers: 
  - 模式
  - 切换模式
# 开始触发器
startTriggers: 
  - 开
  - 开始
  - go
# 描述结束触发器
nextTriggers: 
  - 结束
# 投票触发器
voteTriggers: 
  - 投票
  - vote
  - 投
# 强制结束触发器
stopTriggers: 
  - 结束谁是卧底
# 规则触发器
ruleTriggers: 
  - 谁是卧底规则
# 创建消息
createMessage: "创建成功~\n请输入\"加入\"加入游戏！\n人数大于三人后可输入\"开始\"开始游戏！"
# 重复创建消息
alreadyCreateMessage: "游戏已存在！当前玩家{num}人，可\n请输入\"加入\"加入游戏！输入\"谁是卧底规则\"查看规则，\n人数大于三人后可输入\"开始\"开始游戏！"
# 加入消息
joinMessage: "加入成功~\n当前玩家{num}人"
# 重复加入消息
alreadyJoinMessage: "你已经加入过了！\n当前玩家{num}人"
# 游戏进行中消息
inGamingMessage: 游戏正在进行中！
# 当前玩家消息
showMessage: '当前玩家: {player_list}'
# 词条消息
wordMessage: '你的词条: {word}'
# 白板消息
whiteMessage: 你的词条——欸？！你没有词条呢，多观察一下他人的发言并模仿吧！
# 强制结束消息
stopMessage: 游戏已结束！
# 模式提醒消息
modeMessage: "默认为标准模式，可通过\"模式 1/2/3\"切换至其他模式\n1.标准模式: 仅有1个卧底\n2.多卧底模式: 适用于人较多的情况，四分之一玩家为卧底\n3.随机白板模式: 将随机一部分玩家为白板(不超过四分之一)"
# 切换模式消息
switchModeMessage: '已切换至{mode}！'
# 模式不存在消息
noModeMessage: 该模式不存在！
# 特殊模式消息
specialModeMessage: 游戏模式好像变得奇怪了！
# 卧底胜利消息
spyWinMessage: 游戏结束啦！卧底获得胜利！
# 卧底失败消息
spyLostMessage: 游戏结束啦！卧底输了！
# 特殊模式结束消息
specialModeEndMessage: 游戏结束啦！本轮没有玩家获胜，因为本轮为【特殊模式】，全部玩家都是白板！
# 不知道谁赢消息
normalEndMessage: "游戏结束啦！以下玩家获得胜利:\n{win_list}"
# 描述阶段消息
descriptionMessage: "描述阶段！请按照以下顺序轮流用一句话描述自己的词语（但不可以包含自己的词语），所有人均描述完毕后发送\"{nextTriggers}\"进入下一阶段。\n{player_list}"
# 投票消息
voteMessage: "投票阶段！请输入\"投票 编号\"进行投票，所有人均描述完毕后自动进入下一回合。\n0. 弃票\n{player_list}"
# 规则
rule: 标准模式下，每个玩家会拿到自己的词条，其中卧底的词条与其他人的不一样！每个玩家需要轮流描述自己的词，描述不能重复，若出现自己的词则直接判输。之后进行投票选出卧底。票数最多的玩家将会被淘汰。一直重复下去，直到卧底被淘汰或卧底的人数占剩余玩家总数大于等于三分之一。
# 强制进入特殊模式(不通知)的概率，可填0-100，对应0%-100%的概率，为0时就是禁用特殊模式 。特殊模式: 所有玩家均为白板，只剩下3名玩家时结束。该模式也可通过"切换模式 114514"进入。
specialModeOdds: 5
```

## 声明

本开源插件仅为个人使用而编写，遵循`Apache Licence2.0`开源协议，发布至 [MiraiForum](https://mirai.mamoe.net/) ，禁止用于任何违法法律法规、社区规定、网站规则的行为，若出现问题本人概不负责。

## qwq
本项目开源，需要功能建议自行修改并编译  
如果有bug的话可以回复或者提issue