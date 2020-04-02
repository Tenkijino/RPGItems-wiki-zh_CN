# 技能列表

技能是实现道具功能性的核心机制。

技能是按照顺序执行的，并且只在有对应触发时才会执行。

以下是各个技能的通用参数:

- `cooldown` 在下次可以使用前的冷却时间（单位：Ticks）
- `cost` 每次使用时消耗的耐久值
- `condition` 用来触发技能的条件
- `trigger` 技能的触发

以下是用来修改一个道具技能的命令:

/rpgitem power [operation] [item] [params]

可使用的Operations:

- `add` 增加一个技能
- `remove` 移除一个指定技能
- `list` 列出所有技能
- `prop` 列出一个指定技能的详细参数或是使用额外参数修改技能。
- `reorder` 调整一个技能到新的顺序位，这个功能会影响到技能的执行逻辑。

示例：

```
/rpgitem power add mysword rpgitems:beam cost:1 damage:10 ttl:20 triggers:LEFT_CLICK speed:16 particle:CRIT_MAGIC length:24
```

## 范围效果（AOE）

对范围内的目标释放药水效果。

- `amplifier` 效果倍率
- `duration` 效果持续时间
- `range` 范围半径
- `selfapplication` 效果是否会应用给自己
- `name` 效果名字，详见：https://hub.spigotmc.org/javadocs/spigot/org/bukkit/potion/PotionEffectType.html

## 范围命令（AOECommand）

对范围内的目标执行命令

- `type` 目标种类，可以是：
  - `entity`
  - `player`
  - `mobs`
- `r` 目标范围
- `rm` 最小范围
- `facing` 角度范围，可以由0至180度
- `c` 目标数量
- `mustsee` 在你与目标之间是否不得有方块阻拦
- `command` 执行的命令
- `permission` 指令命令所需要的权限节点

## 范围伤害（AOEDamage）

对范围内的目标造成伤害。

- `range` 目标范围
- `minrange` 最小范围
- `angle` 角度范围, 可以由0至180度
- `count` 会被攻击的目标数量
- `incluePlayers` (typo) 是否包含玩家
- `selfapplication` 是否包含自身
- `mustsee` 在你与目标之间是否不得有方块阻拦
- `damage` 造成的伤害量，独立于于道具属性的伤害
- `delay` 造成伤害前的延时（单位：Ticks）
- `selectAfterDelay` 当延时（delay）不为0时，将此参数设置为false可以使得目标脱离范围时仍然受到伤害
- `firingRange`
- `firingLocation` 确定技能生效位置, 可以是自身`SELF`或是目标`TARGET`
- `castOff` 当技能生效位置`firingLocation`是目标`TARGET`且延时（delay）不为0时,设置此参数为`true`可以在延时前设定范围中心

## 空中处决（Airborne）

在飞行时增加伤害

## 箭矢（Arrow）

发射箭矢，不推荐使用。请使用弹射物`Projectile`。

## 配件（Attachment）

用于触发其他道具的ATTACHMENT触发。

## 吸引（Attract）

吸引范围内的目标

- `radius` 范围半径
- `maxSpeed` 吸引实体的最大速度
- `duration` 吸引实体的持续时间
- `attractingTickCost` 使用技能时每Tick所消耗的耐久
- `attractingEntityTickCost` 使用时每个实体每Tick所消耗的耐久
- `attractPlayer` 是否会吸引玩家
- `firingLocation` 技能生效位置, 可以是自身`SELF`或是目标`TARGET`
- `firingRange`

## 粒子束（Beam）

发射由粒子组成的光束. 这是到目前为止RPGItems中最为复杂也是最为强大的技能。

- `length` 粒子束长度
- `ttl` 粒子存在时间（单位Ticks）
- `particle` 粒子种类：https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Particle.html
- `mode` 可以设置为`BEAM`(1Tick内运行)或是`PROJECTILE`(在多Ticks内运行)
- `pierce` 可以穿透的目标数量
- `ignoreWall` 粒子束飞行途中是否无视完整方块,默认为`true`
- `damage` 粒子束的伤害量,此参数独立于道具参数的伤害设置
- `speed` 粒子束飞行速度（单位：方块/s）
- `offsetX` 粒子生成X轴范围
- `offsetY` 粒子生成Y轴范围
- `offsetZ` 粒子生成Z轴范围
- `particleSpeed` 粒子速度参数
- `particleDensity` 在一个方块空间内生成的粒子量
- `cone` 从自身发射粒子束的离散角度
- `homing` 追踪半径
- `homingAngle` 从自身到目标之间的追踪角度
- `homingRange` 从自身到目标之间的追踪方块距离
- `homingMode` 追踪模式，可以是以下类型：
  - `ONE_TARGET` 追踪单一目标
  - `MULTI_TARGET` 在上一次击中后更换目标
  - `MOUSE_TRACK` 追踪距离光标指向位置最近的目标
- `homingTarget` 追踪目标类型，可以是`MOBS` / `ENTITY` / `PLAYER`
- `ticksBeforeHoming` 追踪前的等待时间（单位：Ticks）
- `beamAmount` 单次运行时发射的粒子束数量
- `burstCount` 单次触发时发射的粒子束波数
- `burstInterval` 下一波发射前的等待时间（单位：Ticks）
- `bounce` 粒子束会在完整方块上弹射的次数,需要将`ignoreWall`设置为`false`
- `hitSelfWhenBounced` 粒子束弹射后是否能击中自己
- `gravity` 粒子束重力，可以设置为负数（粒子束可以逆而上天）
- `extraData` 红石粒子`REDSTONE`的颜色参数,格式为`r,g,b,size`。示例：extraData:\`51,204,255,0.35\` 青色粒子束。
- `speedBias` 使用表达式来控制粒子束速度。示例：`4+x*10*t` 其中x为粒子束已飞行路程，t为飞行时间。
- `behavior` 控制粒子束行为
- `initialRotation`
- `firingLocation` 发射位置，可以是自己`SELF`或是目标`TARGET`
- `effectOnly` 仅作为视觉效果，不会触发任何HIT事件
- `firingR` 极坐标参数
- `firingTheta` 极坐标参数
- `firingPhi` 极坐标参数
- `firingRange`
- `castOff`

## 取消箭矢（CancelBowArrow）

取消弓的箭矢，不会造成任何箭矢的消耗也不会发射任何箭矢。常用于使用了其他技能的弓道具。

## 勇气绝杀（Charge）

奔跑时增加伤害。

- `percentage` 伤害增加的百分比量
- `speedPercentage` 根据速度增加伤害增加的百分比量。
- `setBaseDamage` 是否设为基础伤害（伤害增益可叠加）, 不然将会使用道具属性中的伤害量
- `cap` 最大伤害上限

## 命令（Command）

使用时执行命令。

- `command` 执行的命令. 当命令中包含空格时请使用\`符号。示例：command:\`minecraft:give {player} stone\`
- `display` 在lore中显示的展示名
- `permission` 执行命令所需要的命令节点

可在命令中使用的变量：

- `{player}` 玩家名
- `{player.x}` 玩家的X轴坐标
- `{player.y}` 玩家的Y轴坐标
- `{player.z}` 玩家的Z轴坐标
- `{player.yaw}` 玩家的yaw坐标
- `{player.pitch}` 玩家的pitch

## 击中命令（CommandHit）

在击中时执行命令。

- `command` 执行的命令。
- `permission` 执行命令需要的命令节点
- `minDamage` 触发技能所需要的最低伤害

命令中可以使用的变量：

- `{entity}` 目标名
- `{entity.uuid}` 目标的UUID
- `{entity.x}` 目标的X轴坐标
- `{entity.y}` 目标的Y轴坐标
- `{entity.z}` 目标的Z轴坐标
- `{entity.yaw}` 目标的yaw坐标
- `{entity.pitch}` 目标的pitch

## 消耗（Consume）

使用时消耗道具。

## 击中消耗（ConsumeHit）

击中时消耗道具。

## 暴击伤害（CriticalHit）

造成暴击伤害。

- `chance` 暴击概率，N%
- `backstabchance` 背刺概率，N%
- `factor` 暴击伤害倍率
- `backstabFactor` 背刺伤害倍率
- `setBaseDamage` 是否设为基础伤害（伤害增益可叠加）, 不然将会使用道具属性中的伤害量

## 死亡命令（DeathCommand）

在击杀目标时几率性执行指令。

## 弹反（Deflect）

将飞来的弹射物弹反回去。

## 延时命令（DelayedCommand）

在延时后执行命令。

## 空（Dummy）

空技能虽然不会做任何事情但是它提供了许多可以帮助您理清技能运行逻辑的通用选项。

- `checkDurabilityBound` 触发前检查物品的耐久上下界，一旦耐久超出上下界空技能将不会被触发。
- `costByEnchantment`
- `doEnchReduceCost` 类似于耐久附魔 ，可以降低道具耐久消耗(几率性不消耗耐久)
- `enchCostPercentage` 每一附魔等级可以减少耐久消耗的几率
- `enchantmentType` 附魔名字，可以像`minecraft:unbreaking`
- `costbyDamage` 根据伤害消耗耐久值
- `cooldownKey` 当有多个空技能时,设定一个唯一的string字符串来让冷却时间互相独立
- `successResult` 在空技能成功执行后的动作，默认值为`OK`，用于继续执行下一个技能
- `costResult` Action after cost. Defaults to `COST` which deals the cost and continue with next power. Set to `ABORT` to break and abort the whole process, `OK` to ignore the cost and continue with next power.
- `cooldownResult` Action after cooldown. Defaults to `COOLDOWN` which break execution of dummy but continue with next power. Set `ABORT` to break and abort the whole process, `OK` to ignore cooldown and continue with next power.
- `showCDwarning` 如果你不希望显示任何冷却信息，将它设置为`false`
- `globalCooldown` 设置全体的冷却时间

**使用空技能来禁用冷却信息的显示并统一控制技能冷却时间与耐久消耗**

You should already acknowledge that RPGitems execute powers based on trigger, like `RIGHT_CLICK` or `LEFT_CLICK` and activate power one by one in a pitfall. So if you have an item with a list of powers like:

1. PowerProjectile, trigger `LEFT_CLICK`
2. PowerBeam, trigger `RIGHT_CLICK`
3. PowerSound, trigger `RIGHT_CLICK`
4. PowerParticle, trigger `LEFT_CLICK`

When you do left click, only 1 and 4 will be activated. The item firstly shoot a projectile and then play a particle, but in a single tick.

Now if you want to cost 1 durability on each left click use, with 20 ticks cooldown and do not wish to show the duplicated cooldown message, you can add PowerDummy at first place, and set `cooldown:20 cooldownKey:left cooldownResult:ABORT cost:1 showCDWarning:false triggers:LEFT_CLICK`. You should also set PowerProjectile and PowerParticle's `cost` and `cooldown` to 0, indicating you do not need them and only using PowerDummy to control everything.

RPGitem will first check PowerDummy, and if it's in cooldown then abort the whole execution process, which means projectile and particle powers will not be activated. If it's not cooling down and all conditions (if any) are met, cost 1 then continue with power execution (fire a projectile and play particle).

Similarly, if you set `costResult` to `ABORT`, when the item durability less than its lower bound, the power execution will be aborted.

Please note dummy power options is effective only with correct trigger. If you set dummy with `RIGHT_CLICK` trigger, it will not affect any power with triggers other than `RIGHT_CLICK`.

## 经济（Economy）

消耗或给予使用者金钱。

## 附魔攻击（EnchantedHit）

让附魔来增强伤害量。

- `mode` Can be `ADDITION` or `MULTIPLICATION`
- `amountPerLevel` Boost percentage per enchant level, 1 = 100%
- `enchantmentType` See https://hub.spigotmc.org/javadocs/spigot/org/bukkit/enchantments/Enchantment.html
- `setBaseDamage` Set to true to use dynamic damage as base, otherwise use damage property in item config

## 动态伤害（EvalDamage）

使用表达式来计算基础伤害。

## 爆炸（Explosion）

在使用区产生一个爆炸。

## 火焰（Fire）

发射火焰来点燃目标。

## 火焰弹（Fireball）

发射火焰弹，不推荐使用.建议使用弹射物技能`Projectile`。

## 火焰附加（Flame）

点燃被击中的目标。

## 食物（Food）

回复饥饿值。

## 力场护盾（ForceField）

生成一个护盾来保护自己。

## 鬼手（Glove）

抓住实体并将它扔出去。

## 枪斗术（Gunfu）

使弹射物追踪目标。

## 爆头（Headshot）

击中目标头部造成额外伤害。

## 冰（Ice）

发射冰块并形成一个冰牢。

## 击飞（Knockup）

将目标击飞。

## 生命窃取（Lifesteal）

在击中时回复自身生命值。

## 唤雷（Lightning）

生成闪电造成雷击。

## 乘骑（Mount）

可以骑在实体上。

## 取消无敌时间（NoImmutableTick）

无视无敌时间。

## 粒子屏障（ParticleBarrier）

将受到的攻击转化为粒子效果。

## 粒子效果（Particle）

在使用或击中时生成粒子。

## 佩戴粒子效果（ParticleTick）

在持有或穿戴时生成粒子。

## 效果命中（PotionHit）

在击中时赋予状态效果。

## 自身状态效果（PotionSelf）

赋予使用者状态效果。

## 佩戴状态效果（PotionTick）

在持有或穿戴时赋予状态效果。

## 弹射物（Projectile）

发射弹射物，弹射物的参数有多种选项。

- `isCone` if the projectile fires in a cone. Defaults to `false`
- `gravity` if the projectile affected by gravity. Defaults to `true`
- `range` cone angle from your direction
- `amount` amount of projectile in a single run
- `speed` projectile flying speed
- `burstCount` how many projectiles will be fired
- `burstInterval` ticks between next burst run
- `setFireballDirection` fireball will not float if set to `true`
- `yield` may cause explosion, defaults to `false`
- `isIncendiary` may cause fire, defaults to `false`
- `projectileType` type of projectile, can be
  - `arrow`
  - `snowball`
  - `fireball`
  - `smallfireball`
  - `llamaspit`
  - `shulkerbullet`
  - `dragonfireball`
  - `trident`
  - `skull`
- `suppressArrow` Cancels arrow when firing from bow, but arrow will still be consumed
- `applyForce` apply bow force for arrow and fireball, affects speed
- `firingLocation` Can be `SELF` or `TARGET`
- `firingR` Polar coordinates parameter
- `firingTheta` Polar coordinates parameter
- `firingPhi` Polar coordinates parameter
- `firingRange`
- `castOff`

## 蓝瓜头（Pumpkin）

攻击僵尸或者骷髅时给他们戴上南瓜头。

## 彩虹（Rainbow）

发射各种颜色的羊毛。

## 真实伤害（RealDamage）

造成无视护甲的真实伤害。

## 修复（Repair）

Consume material to restore (or cost) durability.

- `durability` Durability restored (or cost) per each repair material
- `display` Message displayed in lore
- `material` Repair material. Can be `HAND` to use item hold in mainhand.
- `isSneak` Require sneak to trigger
- `mode` Can be `DEFAULT`, `ALLOW_OVER` and `ALWAYS`
- `allowBreak` defaults to `true`
- `abortOnSuccess` abort and break execution after successfully triggered (repaired)
- `abortOnFailure` abort and break execution after failed to repair (e.g., no material)
- `customMessage` Message to display in chat
- `amount` Maximum material amount to consume in each trigger
- `showFailMsg` Show repair failed message or not. Default to `true`

## 拯救（Rescue）

受到过量伤害或者血量即将低于指定值时拯救玩家，比不死图腾更好！

## 裂地冲击（Rumble）

在地面上生成一个冲击波将目标击飞。

## 计分板（Scoreboard）

修改玩家的计分板标签或数值。

## 潜影弹（Shulkerbullet）

发射追踪目标的潜影弹。

## 钩爪（Skyhook）

发射钩爪用于钩住指定方块。

## 声音（Sound）

在使用或击中实体时播放声音。

## 定身（Stuck）

使目标无法移动或是传送。

## TNT大炮（TNTCannon）

发送TNT。

## 传送（Teleport）

传送一段距离。

## 投掷（Throw）

投掷实体。

## 药箭（TippedArrow）

发射带有药水效果的箭矢，不推荐使用。请使用弹射物`Projectile`与命中效果`PotionHit`技能。

## 火把（Torch）

投掷一些火把来照亮一片区域。

## 传送信标（Translocator）

投掷一个传送信标并传送到信标所在地。
