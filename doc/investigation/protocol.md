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

|code|location|
|---|---|
|0x0|NONEXISTANT|
|0x01|DECK|
|0x02|HAND|
|0x04|MONSTERZONE|
|0x08|SPELLZONE|
|0x10|GRAVE|
|0x16|MONSTERZONE|
|0x20|BANISHED|
|0x40|EXTRA|
|0x80|OVERLAY|
|0xc0|EXTRA|
|0x100|FZONE|
|0x200|PZONE|

POSITION:
|code|position|
|---|---|
|0x1|FaceUpAttack|
|0x2|FaceDownAttack|
|0x4|FaceUpDefence|
|0x5|FaceUp|
|0xA|FaceDown|
|0x3|Attack|
|0xC|Defence|

RACE:
TODO

RPS:
TODO

CARD_ATTRIBUTES:
TODO

CARD_TYPES:
TODO

COMPLEX_TYPES:
TODO

## MSG_RETRY
有出错，对局重开。

## MSG_START
|字段|位数|含义|
|---|---|---|
|playertype|8|用于判断是否先功或者观战者|
|(master_rule)|8|大师规则(旧版本？)|
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

|command|含义|
|---|---|
|1|todo|
|2|todo|
|3|todo|
|4|效果选择|
|5|todo|
|6|种族选择|
|7|属性选择|
|8|todo|
|9|数字选择|
|10|todo|
|11|区域选择|

`data`在不同的`command`的语境下有不同的含义。
|data表示的type|构成|
|---|---|
|卡|高28位为卡的id，低4位是卡效果内容的index|
|种族|todo|
|属性|todo|
|数字|data即为数字|
|区域|todo|

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
|type|8|胜利的原因类型|

`player`=2时为平局。

## MSG_NEW_PHASE
新的阶段。

|字段|位数|含义|
|---|---|---|
|phase|16|阶段编号|


## MSG_DRAW
抽卡？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|抽卡的数量？|
|card0|32|卡的编号|
|card1|32|卡的编号|
|---|||

`card`的数量由`count`指定，每张`card`为32位。

## MSG_SHUFFLE_DECK
卡组洗牌。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|

## MSG_SHUFFLE_HAND
手卡洗牌。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|todo|
|code0|32|todo|
|code1|32|todo|
|---|||

`code`的数量由`count`指定，每个`code`占32位。

## MSG_SHUFFLE_EXTRA
额外卡组洗牌。

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
|player|8|玩家编号|
|location|8|产生连锁卡位置的编号|
|sequence|8|连锁序列？|
|position|8|表示状态编号|

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
|id|8|连锁链中卡片的index|

## MSG_CHAIN_NEGATED
连锁否定？

|字段|位数|含义|
|---|---|---|
|chain_link|8|todo|

## MSG_CHAIN_DISABLED
连锁无效？

|字段|位数|含义|
|---|---|---|
|id|8|连锁链中被无效卡片的index|

## MSG_CARD_SELECTED
卡片被选择？

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|todo|

## MSG_RANDOM_SELECTED

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|todo|
|selections|8 x 4 x count|todo|

## MSG_BECOME_TARGET
|字段|位数|含义|
|---|---|---|
|count|8|todo|
|selections|8 x 4 x count|被选择的对象|

## MSG_PAY_LPCOST
支付生命值。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|lp|32|需要支付的生命值数值|

## MSG_DAMAGE
玩家收到伤害。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|lp|32|收到的伤害数值|

## MSG_RECOVER
玩家生命值回复。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|lp|32|回复的数值|

## MSG_LPUPDATE
更新生命值。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|lp|32|更新后的生命值数值|

## MSG_SUMMONING
召唤。

|字段|位数|含义|
|---|---|---|
|code|32|卡的code|
|player|8|玩家编号|
|location|8|召唤的位置编号|
|sequence|8|todo|

## MSG_EQUIP
装备？

|字段|位数|含义|
|---|---|---|
|from.player|8|玩家编号|
|from.location|8|位置编号|
|from.sequence|8|todo|
|from.position|8|表示状态编号|
|to.player|8|玩家编号|
|to.location|8|位置编号|
|to.sequence|8|todo|
|to.position|8|表示状态编号|

## MSG_UNEQUIP

|字段|位数|含义|
|---|---|---|
|from.player|8|玩家编号|
|from.location|8|位置编号|
|from.sequence|8|todo|
|from.position|8|表示状态编号|
|to.player|8|玩家编号|
|to.location|8|位置编号|
|to.sequence|8|todo|
|to.position|8|表示状态编号|

## MSG_CARD_TARGET

|字段|位数|含义|
|---|---|---|
端上好像不管？

## MSG_CANCEL_TARGET

|字段|位数|含义|
|---|---|---|
端上好像不管？

## MSG_ADD_COUNTER
增加指示物。

|字段|位数|含义|
|---|---|---|
|type|16|指示物类型？|
|player|8|玩家编号|
|location|8|位置编号|
|sequence|8|todo|
|count|16|增加指示物的数量|

## MSG_REMOVE_COUNTER
减少指示物。

|字段|位数|含义|
|---|---|---|
|type|16|指示物类型？|
|player|8|玩家编号|
|location|8|位置编号|
|index|8|todo|
|count|8|减少指示物的数量|

## MSG_ATTACK
攻击。

|字段|位数|含义|
|---|---|---|
|attacker.player|8|攻击方的玩家编号|
|attacker.location|8|攻击方的位置编号|
|attacker.sequence|8|todo|
|attacker.position|8|攻击方的表示状态编号|
|defender.player|8|防御方的玩家编号|
|defender.location|8|防御方的位置编号|
|defender.sequence|8|todo|
|defender.position|8|防御方的表示状态编号|

## MSG_BATTLE
战斗。

|字段|位数|含义|
|---|---|---|
|attacker.player|8|攻击方的玩家编号|
|attacker.location|8|攻击方的位置编号|
|attacker.sequence|8|todo|
|attacker.position|8|攻击方的表示状态编号|
|aatk|32|攻击方在战斗阶段的攻击力|
|adef|32|攻击方在战斗阶段的防御力|
|padding|8|todo|
|defender.player|8|防御方的玩家编号|
|defender.location|8|防御方的位置编号|
|defender.sequence|8|todo|
|defender.position|8|防御方的表示状态编号|
|datk|32|防御方在战斗阶段的攻击力|
|ddef|32|防御方在战斗阶段的攻击力|
|padding|8|todo|

## MSG_MISSED_EFFECT
失去时点。

|字段|位数|含义|
|---|---|---|
|padding|32|todo|
|code|32|卡的编号?|

## MSG_TOSS_DICE
抛骰子。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|抛骰子次数|
|results|8 x count|骰子结果|

## MSG_ROCK_PAPER_SCISSORS
展示剪刀石头布。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|

## MSG_HAND_RES
猜拳结果。

|字段|位数|含义|
|---|---|---|
|res|8|猜拳结果|

## MSG_TOSS_COIN
抛硬币。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|抛硬币次数|
|results|8 x count|抛硬币结果|

## MSG_ANNOUNCE_RACE
宣言种族。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|announce_count|8|宣言的个数|
|avaliable|32|todo|

## MSG_ANNOUNCE_CARD
宣言卡名。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|宣言的个数|
|search_code|32 x count|todo|

## MSG_ANNOUNCE_NUMBER
宣言数字。

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|announce_count|8|宣言的个数|
|values|32 x announce_count|todo|

## MSG_ANNOUNCE_CARD_FILTER

|字段|位数|含义|
|---|---|---|
|player|8|玩家编号|
|count|8|宣言的个数|
|opcodes|32 x count|todo|

## MSG_CARD_HINT

|字段|位数|含义|
|---|---|---|
|card.player|8|玩家编号|
|card.location|8|位置编号|
|card.sequence|8|todo|
|card.position|8|表示状态编号|
|chtype|8|类型|
|value|32|todo|

|chtype|含义|
|---|---|
|1|数字记录|
|2|卡片记录|
|3|种族记录|
|4|属性记录|
|5|数字记录|
|6|todo|
|7|todo|

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
|summonable.count|8|能通常召唤的数量|
|summonable.card{code, player, location, sequence}|(32 + 8 x 3) x count|能通常召唤的卡|
|spsummonable.count|8|能特殊召唤的数量|
|spsummonable.card{code, player, location, sequence}|(32 + 8 x 3) x count|能特殊召唤的卡|
|position.count|8|能改变表示形式的数量|
|position.card{code, player, location, sequence}|(32 + 8 x 3) x count|能改变表示形式的卡|
|front_placeable.count|8|能前场放置数量|
|front_placeable.card{code, player, location, sequence}|(32 + 8 x 3) x count|能前场放置的卡|
|back_placeable.count|8|能后场放置数量|
|back_placeable.card{code, player, location, sequence}|(32 + 8 x 3) x count|能后场放置的卡|
|effect.count|8|能发动效果数量|
|effect.card{code, player, location, sequence, descP}|(32 + 8 x 3) x count|能后场放置的卡|
|bp|8|能进入战斗阶段|
|ep2|8|能结束回合|
|shuffle|8|能洗切手牌|

## MSG_MOVE

|字段|位数|含义|
|---|---|---|
|code|32|移动卡的code|
|from.player|8|原始玩家编号|
|from.location|8|原始位置编号|
|from.sequence|8|todo|
|from.position|8|原始表示状态|
|to.player|8|当前玩家编号|
|to.location|8|当前位置编号|
|to.sequence|8|todo|
|tp.position|8|当前表示状态|
|reason|32|todo|