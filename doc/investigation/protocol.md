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

POSITION:

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

## MSG_CARD_SELECTED
卡片被选择？

|字段|位数|含义|
|player|8|玩家编号|
|count|8|todo|

## MSG_RANDOM_SELECTED

|字段|位数|含义|
|player|8|玩家编号|
|count|8|todo|
|selections|8 x 4 x count|todo|

## MSG_BECOME_TARGET
|字段|位数|含义|
|count|8|todo|
|selections|8 x 4 x count|todo|

## MSG_PAY_LPCOST
支付生命值？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|lp|32|需要支付的生命值数值？|
|multiplier|8?|todo|

## MSG_DAMAGE
收到伤害？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|lp|32|收到的伤害数值？|
|multiplier|8?|todo|

## MSG_RECOVER
回复生命值？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|lp|32|回复的数值？|
|multiplier|8?|todo|

## MSG_LPUPDATE
更新生命值？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|lp|32|todo|
|multiplier|8?|todo|

## MSG_SUMMONING
召唤。

|字段|位数|含义|
|---|---|---|
|id|32|卡的id?|
|player|8|玩家编号|
|location|8|召唤的位置编号|
|index|8|todo|
|position|8|todo|

## MSG_EQUIP
装备？

|字段|位数|含义|
|---|---|---|
|c1|8|todo|
|l1|8|todo|
|s1|8|todo|
|padding?|8|todo|
|c2|8|todo|
|l2|8|todo|
|s2|8|todo|
|padding?|8|todo|

## MSG_UNEQUIP

|字段|位数|含义|
|---|---|---|
|c1|8|todo|
|l1|8|todo|
|s1|8|todo|
|padding?|8|todo|
|c2|8|todo|
|l2|8|todo|
|s2|8|todo|
|pending?|8|todo|

## MSG_CARD_TARGET

|字段|位数|含义|
|---|---|---|
|c1|8|todo|
|l1|8|todo|
|s1|8|todo|
|padding?|8|todo|
|c2|8|todo|
|l2|8|todo|
|s2|8|todo|
|padding?|8|todo|

## MSG_CANCEL_TARGET

|字段|位数|含义|
|---|---|---|
|c1|8|todo|
|l1|8|todo|
|s1|8|todo|
|padding?|8|todo|
|c2|8|todo|
|l2|8|todo|
|s2|8|todo|
|padding?|8|todo|

## MSG_ADD_COUNTER

|字段|位数|含义|
|---|---|---|
|type|16|todo|
|player|8|玩家编号|
|location|8|位置编号|
|index|8|todo|
|count|8|todo|

## MSG_REMOVE_COUNTER

|字段|位数|含义|
|---|---|---|
|type|16|todo|
|player|8|玩家编号|
|location|8|位置编号|
|index|8|todo|
|count|8|todo|

## MSG_ATTACK
攻击。

|字段|位数|含义|
|---|---|---|
|attacker.player|8|攻击方的玩家编号|
|attacker.location|8|攻击方的位置编号|
|attacker.index|8|todo|
|padding?|8|todo|
|defender.player|8|防御方的玩家编号|
|defender.location|8|防御方的位置编号|
|defender.index|8|todo|
|padding?|8|todo|

## MSG_BATTLE
战斗。

|字段|位数|含义|
|---|---|---|
|ca|8|todo|
|la|8|todo|
|sa|8|todo|
|padding?|8|todo|
|aatk|32|todo|
|adef|32|todo|
|da|8|todo|
|cd|8|todo|
|ld|8|todo|
|sd|8|todo|
|padding|8|todo|
|datk|32|todo|
|ddef|32|todo|
|dd|8|todo|

## MSG_MISSED_EFFECT

|字段|位数|含义|
|---|---|---|
|padding|8|todo|
|id|32|todo|

## MSG_TOSS_DICE

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|todo|
|results|8 x count|todo|

## MSG_ROCK_PAPER_SCISSORS

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|

## MSG_HAND_RES

|字段|位数|含义|
|---|---|---|
|res|8|猜拳结果？|

## MSG_TOSS_COIN

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|todo|
|results|8 x count|todo|

## MSG_ANNOUNCE_RACE
宣言种族？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|announce_count|8|todo|
|avaliable|32|todo|
|options|todo|todo|

## MSG_ANNOUNCE_CARD
宣言卡名？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|declarable_type|32|todo|

## MSG_ANNOUNCE_NUMBER
宣言一个数字？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|announce_count|8|todo|
|values|32 x announce_count|todo|

## MSG_ANNOUNCE_CARD_FILTER

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|todo|
|opcodes|32 x count|todo|

## MSG_CARD_HINT

|字段|位数|含义|
|---|---|---|
|controller|8|todo|
|location|8|todo|
|sequence|8|todo|
|padding|8|todo|
|chtype|8|todo|
|value|32|todo|

## MSG_PLAYER_HINT

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|chtype|8|todo|
|value|32|todo|

## MSG_MATCH_KILL

|字段|位数|含义|
|---|---|---|
|match_kill|32|todo|

## MSG_SELECT_IDLECMD

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|summonable_cards|todo|todo|
|spsummonable_cards|todo|todo|
|repositionable_cards|todo|todo|
|msetable_cards|todo|todo|
|ssetable_cards|todo|todo|
|activatable_cards|todo|todo|
|enableBattlePhase|8|todo|
|enableBatlePhase|8|todo|
|shufflecount|8|todo|

## MSG_MOVE

|字段|位数|含义|
|---|---|---|
|id|32|todo|
|previousController|8|todo|
|pl(previousLocation)|8|todo|
|previousIndex|8|todo|
|overlayindex|8|todo|
|currentController|8|todo|
|cl(currentLocation)|8|todo|
|currentIndex|8|todo|
|currentPosition|8|todo|
|r(reason)|32|todo|
