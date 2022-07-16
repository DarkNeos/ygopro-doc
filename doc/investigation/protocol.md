# ygopro-core协议解析

## ENUMS

对局的各个阶段PHSAE：
|code|phase|gui_phase|
|---|---|---|
|0x01|DRAW|0|
|0x02|STANDBY|1|
|0x04|MAIN1|2|
|0x08|BATTLE_START|3|
|0x10|BATTLE_STEP|3|
|0x20|DAMAGE|3|
|0x40|DAMAGE_CAL|3|
|0x80|BATTLE|3|
|0x100|MAIN2|4|
|0x200|END|5|

场上位置LOCATION：
TODO

## MSG_RETRY
有出错，对局重开。

## MSG_START
|字段|位数|含义|
|---|---|---|
|playertype|8|-|
|life1|32|玩家一的初始生命值|
|life2|32|玩家二的初始生命值|
|decksize1|16|玩家一的卡组数量|
|extrasize1|16|玩家一的额外卡组数量|
|decksize2|16|玩家二的卡组数量|
|extrasize2|16|玩家二的额外卡组数量|

## MSG_HINT
|字段|位数|含义|
|---|---|---|
|command|8|-|
|player|8|-|
|data|32|-|

根据`command`的值，进行以下操作：
- 5: `player`指定的玩家有提示；
- 9: `player`以外的玩家和观战者有提示；
- 10: 所有玩家和观战者均有提示。

## MSG_NEW_TURN
操作玩家转换。

|字段|位数|含义|
|---|---|---|
|player|8|下一个操作的玩家编号|

## MSG_WIN
玩家胜利。

|字段|位数|含义|
|---|---|---|
|player|8|胜利的玩家编号|
|type|8|胜利的原因类型？|

## MSG_NEW_PHASE
新的阶段。

|字段|位数|含义|
|---|---|---|
|phase|16|阶段编号|
|gui_phase|16|todo|


## MSG_DRAW
TODO：具体含义。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|卡的数量|
|card0|32|卡的编号|
|card1|32|todo|
|---|||

`card`的数量由`count`指定，每张`card`为32位。

## MSG_SHUFFLE_DECK
卡组洗牌。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|

## MSG_SHUFFLE_HAND
手卡洗牌？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|todo|
|code0|32|todo|
|code1|32|todo|
|---|||

`code`的数量由`count`指定，每个`code`占32位。

## MSG_SHUFFLE_EXTRA
额外卡组洗牌？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|todo|
|code0|32|todo|
|code1|32|todo|
|---|||

`code`的数量由`count`指定，每个`code`占32位。

## MSG_CHAINING
连锁中。

|字段|位数|含义|
|---|---|---|
|id|32|连锁id?|
|pc.player|8|玩家编号|
|pc.location|8|产生连锁卡位置的编号|
|pc.index|8|todo|
|subs|8|todo|
|c.player|8|todo|
|c.location|8|todo|
|c.index|8|todo|
|desc|32|todo|
|ct|8|todo|

## MSG_CHAINED
连锁完毕？

|字段|位数|含义|
|---|---|---|
|chain_link|8|todo|

## MSG_CHAIN_SOLVING
处理连锁中？

|字段|位数|含义|
|---|---|---|
|chain_link|8|todo|

## MSG_CHAIN_SOLVED
连锁处理完成？

|字段|位数|含义|
|---|---|---|
|ct|8|todo|

## MSG_CHAIN_NEGATED
连锁否定？

|字段|位数|含义|
|---|---|---|
|chain_link|8|todo|

## MSG_CHAIN_DISABLED
连锁无效？

|字段|位数|含义|
|---|---|---|
|chain_link|8|todo|
