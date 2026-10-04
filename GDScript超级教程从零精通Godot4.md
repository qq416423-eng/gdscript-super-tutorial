# GDScript 超级教程：从零结构化精通 Godot 4 脚本语言

> **本书定位**：一本自包含、无废话、超精细的 GDScript（Godot 4.x）语言教程。
> **适合人群**：从未写过代码的纯新手 ～ 想系统补齐语法的中级开发者。
> **阅读方式**：从头按顺序读是"学习"，跳章节查是"参考"。两种用法都支持。
> **本书约定**：
> - 所有代码都在 Godot 4.x（含 4.3）验证过语法；
> - `# →` 开头的注释表示"这行执行后的结果"；
> - 每个知识点至少配 3 个例子：入门例、实战例、陷阱例；
> - 大量"模块模板"可以直接抄走改造。

---

## 全书总目录

### 第一卷 · 编程地基

- 第 1 章：编程到底是怎么回事（结构化思维养成）
- 第 2 章：环境、工具与代码规范

### 第二卷 · 语言核心（语法逐个击破）

- 第 3 章：变量与常量——数据的盒子
- 第 4 章：数据类型大全——盒子里能装什么
- 第 5 章：运算符大全——数据怎么被加工
- 第 6 章：流程控制——程序的岔路与循环
- 第 7 章：函数——代码的积木与螺丝
- 第 8 章：数组（Array）完全教程
- 第 9 章：字典（Dictionary）完全教程
- 第 10 章：类型化数组与 Packed 系列性能专题
- 第 11 章：字符串（String）完全教程
- 第 12 章：枚举与常量组织术

### 第三卷 · 面向对象

- 第 13 章：类的基础——图纸与实物
- 第 14 章：继承深入——站在巨人肩膀上
- 第 15 章：静态成员与工具类设计
- 第 16 章：内部类、引用语义与值语义
- 第 17 章：构造函数与对象的一生
- 第 18 章：注解大全（@export 家族等 20+ 种）

### 第四卷 · 引擎交互

- 第 19 章：节点与场景树深入
- 第 20 章：生命周期函数全解
- 第 21 章：信号深入——观察者模式实战
- 第 22 章：节点引用的所有姿势
- 第 23 章：资源系统（Resource / load / preload）
- 第 24 章：输入系统
- 第 25 章：数学与向量专题
- 第 26 章：Tween 补间动画完全教程
- 第 27 章：await、协程与异步编程
- 第 28 章：文件、JSON 与配置
- 第 29 章：错误处理与调试技巧
- 第 30 章：性能优化意识

### 第五卷 · 模块模板库（30+ 即插即用模板）

- 第 31 章：基础模板（血量/伤害/背包/存档/事件总线...）
- 第 32 章：行为模板（状态机/AI/巡逻/弹幕/波次...）
- 第 33 章：体验模板（屏幕震动/伤害数字/音频/设置...）
- 第 34 章：架构模板（单例/对象池/命令模式/数据驱动...）

### 第六卷 · 收尾

- 第 35 章：综合小项目——把一切串起来
- 第 36 章：完整语法速查表
- 第 37 章：报错词典（40+ 条）
- 第 38 章：Godot 3 → 4 迁移对照
- 附录 A：术语表
- 附录 B：学习路线图
- 附录 C：全书索引（章节导航）
- 附录 D：把知识用到真实项目上（基础篇）
- 附录 E：纯手机学习方案（逐章对照表）

---
---

# 第一卷 · 编程地基

# 第 1 章：编程到底是怎么回事

## 1.1 三个世界：人脑、代码、机器

写程序的人常常忘记一件重要的事：**代码不是写给机器看的，是写给人看的**。机器最终执行的是编译后的二进制，它根本不在乎你的代码美不美。代码真正的读者是——三个月后的你自己、你的同伴、以及接手你项目的倒霉蛋。

所以学编程其实是学两件事：

1. **把想法拆成机器能执行的步骤**（这是"结构化思维"）；
2. **用一门语言把这些步骤写清楚**（这是"语法"）。

本书第二~四卷解决 2，本卷先解决 1。

## 1.2 程序 = 数据 + 对数据的操作

所有程序，从计算器到 3A 大作，剥开来看只有两样东西：

```
数据（名词）：血量 100、名字"勇者"、背包里 3 瓶药水、屏幕上一个坐标
操作（动词）：扣血 30、改名字、喝掉一瓶药、把坐标向右移 10 像素
```

编程语言的全部设计，本质上都是在回答两个问题：

- **怎么装数据？** → 变量、类型、数组、字典、对象（第 3~4 章、第 8~9 章、第 13 章）
- **怎么描述操作？** → 运算符、控制流、函数（第 5~7 章）

先记住这个骨架，后面每学一个语法点，你都问自己一句："这是在帮我**装数据**，还是帮我**描述操作**？"知识就不会散。

## 1.3 结构化思维三件套：顺序、分支、循环

任何复杂逻辑都能用三种基本结构拼出来。这不是比喻，是被数学证明过的定理（结构化程序定理）。

### 顺序：从上到下一步步来

```
步骤1：打开背包
步骤2：找到红药水
步骤3：喝下
步骤4：血量 +50
```

### 分支：遇到岔路选一条

```
如果 血量 < 30%：
    喝药
否则：
    继续砍怪
```

### 循环：重复同样的事

```
对 背包里的每一件物品：
    如果 是药水：
        喝掉
```

99% 的游戏逻辑都是这三样的嵌套组合。举个真实游戏逻辑（装备评分系统）：

```
总评 = 0                        ← 顺序
对 装备的每条属性：              ← 循环
    如果 属性是攻击力：          ← 分支
        总评 += 攻击力 × 2
    否则 如果 属性是防御力：
        总评 += 防御力 × 1.5
    否则：
        总评 += 属性值
```

**新手训练法**：以后玩任何游戏，试着用"顺序/分支/循环"三件套口述它的某个功能（比如"拾取物品"是怎么工作的）。能口述清楚，你就能写出来。

## 1.4 把大问题拆小：函数思维

给你一个任务："做一把会发光的剑"。直接写代码会无从下手。结构化思维是这样拆的：

```
做发光剑
├── 造剑的模型（显示图片）
├── 给剑加光效（周期性改变透明度）
│     ├── 每帧让透明度在 0.6~1.0 之间波动
│     └── 用三角函数算波动值
├── 挥剑时播放音效
└── 命中敌人时造成伤害
      ├── 计算距离够不够近
      ├── 计算伤害（攻击力 − 防御力，最低为 1）
      └── 敌人血量减少 + 播放受击动画
```

每个 `├──` 就是未来代码里的一个**函数**。大任务 → 小任务 → 更小任务，直到每个小任务"一句话能说清怎么做"为止。这就是第 7 章函数、第 13 章类的思想源头。

## 1.5 状态：记住"现在怎么样了"

游戏和普通软件最大的区别：游戏是**有状态**的。状态 = 程序记住的、会随时间变化的数据。

```
勇者的状态：
  位置 = (100, 200)
  血量 = 78 / 100
  当前动作 = "挥剑中"
  挥剑第几帧 = 3
```

游戏每秒 60 次（60 帧）地问自己："状态现在是什么？该按状态做什么？状态要怎么变？"这个循环叫**游戏循环（game loop）**：

```
每一帧：
    读取输入          （玩家按了什么键？）
    更新状态          （按输入和规则改变数据）
    渲染画面          （把状态画到屏幕上）
```

你以后写的 `_process(delta)`（第 20 章）就是把自己挂进这个循环。理解"一切皆状态"，很多困惑会消失：为什么角色会"卡住"？因为某个状态没被正确更新。为什么存档能读回进度？因为状态被完整写入文件又读回来了（第 28 章）。

## 1.6 命名：编程界的半壁江山

数据要装进"盒子"，盒子要贴"标签"。标签起得好，代码读起来像英语；起得差，三个月后连自己都看不懂。

**好名字的标准：看名字就知道装的是什么、做什么用。**

| 烂名字 | 好名字 | 为什么 |
|---|---|---|
| `a` | `attack_power` | a 是什么？谁都猜不到 |
| `flag` | `is_alive` | flag 太泛；is_ 前缀还暗示了"是/否" |
| `temp` | `damage_after_armor` | temp 只说明"临时的"，没说明内容 |
| `data1` `data2` | `enemy_data` `player_data` | 数字编号是命名懒惰 |
| `hp2` | `hp_max` | 2 是什么意思？max 一目了然 |
| `doIt()` | `play_hit_animation()` | do it 做什么 it？ |

**命名的几条军规**：

1. 变量/属性：名词或名词短语 —— `speed`、`enemy_count`、`inventory_list`
2. 函数/方法：动词开头 —— `take_damage()`、`spawn_enemy()`、`get_score()`
3. 返回真假的函数：`is_` / `has_` / `can_` 开头 —— `is_dead()`、`has_item()`
4. 临时循环变量可以短：`for i in 10` 的 `i` 是全世界公认的"循环计数"
5. 常量全大写：`MAX_SPEED = 500.0`
6. 私有成员加下划线：`_internal_cache`（表示"外部别碰"）
7. **别怕名字长**：`enemy_spawn_interval_seconds` 远好过 `esi`。代码是写给人看的。

## 1.7 读代码的能力：比写代码更先学会

初学者 70% 的时间其实在读代码（教程的、别人的、引擎的），读不懂就写不出。训练法：

1. **一行一行读，读出声**。`hp -= damage` 念作"血量 减去 伤害，再赋值回血量"。慢，但前期值得。
2. **手指当指针**，指着当前行，别跳。跳读是熟手特权。
3. **在脑内"运行"**：拿张纸，左边写变量名，每执行一行就更新变量值。这个技能叫"人肉调试"，是编程水平的分水岭。
4. **先看结构再看细节**：先扫 `func` 关键词知道有哪几个函数，再挑一个感兴趣的深入。
5. **看不懂就抄下来改**：把别人的代码抄一遍、改几个数字、猜运行结果、验证。错配修正，进步飞快。

## 1.8 本章小结

- 程序 = 数据 + 操作；语法只解决"怎么装数据、怎么描述操作"两件事
- 顺序、分支、循环是全部逻辑的三块积木
- 大问题层层拆小，每个小任务对应一个函数
- 游戏的本质是"每帧更新状态"
- 命名是代码可读性的半壁江山
- 读代码先于写代码，人肉运行是核心训练

## 1.9 自测（先别看答案）

1. 用"顺序+分支+循环"口述：游戏里"捡金币"的全过程。
2. 把"Boss 每 3 秒召唤 4 只小怪，小怪出生后冲向玩家"拆解成小任务树。
3. 给以下数据起好名字：记录玩家死了几次的数字、存放所有敌人对象的容器、判断任务是否完成的真假值、计算两敌人距离的函数。

> 参考答案：
> 1. 顺序：玩家移动→每帧检测玩家与金币距离→(分支)距离小于20像素→金币消失→金币数+1→播放音效→(循环)对场上每枚金币重复检测。
> 2. 召唤Boss：定时器到3秒(循环)→随机取4个出生点(循环4次)→每个出生点造一只小怪→给小怪设定目标为玩家→小怪每帧朝玩家移动。
> 3. `player_death_count`、`enemies_list`、`is_quest_completed`、`get_distance_between()`。

---

# 第 2 章：环境、工具与代码规范

## 2.1 你可以在哪里写 GDScript

| 场景 | 工具 | 说明 |
|---|---|---|
| 电脑正统开发 | Godot 编辑器内置脚本编辑器 | 语法高亮、自动补全、报错跳转，首选 |
| 电脑轻量编辑 | VS Code + godot-tools 插件 | 熟悉 VS Code 的人用 |
| 手机（APK 改包） | MT管理器 / 其他文本编辑器 | 纯文本编辑，无补全无高亮，本书部分读者场景 |
| 网页练习 | 官方 "GDScript app"（浏览器学语法） | 不装任何东西 |

**本书代码全部可"纸上运行"**——即使手边没有 Godot，拿纸笔做"人肉运行"也能完成 90% 的练习。

## 2.2 创建你的第一个脚本（电脑版流程）

1. 打开 Godot，新建任意项目；
2. 场景里建一个 `Node2D`；
3. 右键节点 → 附加脚本 → 命名 `my_first.gd` → 创建；
4. 看到这个骨架：

```gdscript
extends Node2D

# 在这里写代码
```

`extends Node2D` 表示"我这个脚本将作为 Node2D 的一种"（继承，第 14 章详讲）。现在只需要知道：**每个 gd 文件第一行通常都是 extends 某个类**。

5. 按 F5（或运行场景按钮）运行，底部输出面板能看到 print 的内容。

## 2.3 文件、类名与目录：gd 文件的组织

```
my_project/
├── project.godot           项目配置
├── scenes/                 场景文件(.tscn)一般放这
│   └── player.tscn
├── scripts/                脚本一般放这（纯个人习惯，不是强制）
│   ├── player.gd
│   └── enemy.gd
└── assets/                 图片音频等资源
```

规则：
- 一个 .gd 文件 = 一个类（第 13 章展开）；
- 文件名小写+下划线：`enemy_base.gd` ✔，`EnemyBase.gd` 也可以但不推荐混用风格；
- 文件内部第一行写 `class_name EnemyBase` 后，全项目任何地方都能直接用 `EnemyBase` 这个名字（第 13 章）。

## 2.4 代码规范（前 10 条最重要的）

语法是"法律"，规范是"道德"。法律保证能跑，道德保证别人愿意读。

1. **缩进**：GDScript 用缩进表达代码块（同 Python）。**官方推荐 Tab**。一个文件内绝不混用 Tab 和空格——这是新手崩溃率第一的错误。
2. **一行一句**：不要 `var a = 1; var b = 2`。分号能写但没人写。
3. **空行分段**：函数之间空 1~2 行；函数内逻辑段落之间空 1 行。
4. **行宽**：尽量不超过 100 字符（手机上更短些好读）。太长用 `\` 续行（第 6 章演示）。
5. **运算符两侧留空格**：`hp - 30` ✔，`hp-30` 能跑但难读。括号内侧不留：`func test(a, b)`。
6. **逗号后留空格**：`[1, 2, 3]` ✔ `[1,2,3]` 一般。
7. **命名风格统一**：变量用 snake_case（全小写+下划线），常量全大写，类名用 PascalCase（大驼峰）。**Godot 4 生态几乎全是这套**。
8. **注释写"为什么"，不写"是什么"**：`hp -= 30 # 扣血` 是废话；`hp -= 30 # 火伤无视护甲，走直伤通道` 是好注释。
9. **数字不要魔法化**：`if hp < 30` 里的 30 是啥？写成 `const LOW_HP_WARNING = 30` 然后用名字。
10. **改别人的代码，遵循别人的风格**：接手一个 Tab 缩进的项目，别把新代码写成空格缩进。

## 2.5 缩进为什么如此重要（原理篇）

大多数语言（C/Java/JS）用花括号 `{ }` 划定代码块，缩进只是装饰。GDScript 把缩进**升级成了语法**：

```gdscript
func attack():
	print("第一刀")      # 缩进 1 级 → 属于 attack 函数
	print("第二刀")      # 同级 → 还是 attack 的
print("结束了")          # 顶格 → 不属于 attack！函数定义到此为止
```

看一个靠缩进改变含义的例子：

```gdscript
# 版本A：奖励只给活着的
if is_alive:
	give_reward()
	level_up()

# 版本B：死了也给升级（可能是bug！）
if is_alive:
	give_reward()
level_up()
```

两段代码只差一个缩进，行为完全不同。**读代码时缩进就是"这句话归谁管"的全部真相。**

Tab 和空格的战争：1 个 Tab 显示出来可能等于 4 个空格的宽度，但对机器来说它们是完全不同的两个字符。文件里同时出现"Tab 的行"和"空格的行"，引擎解析时代码块归属就乱了，报错往往莫名其妙（比如 `Unindent does not match any outer indentation level`）。所以：**打开一个文件先看行首是什么，新加的行保持一致**。

## 2.6 保存、运行与热重载的日常习惯

- 写 10 行，测一次。别写 200 行再运行——报错一堆，定位困难；
- Godot 修改脚本保存后，正在运行的场景里常会**热重载**（部分对象状态会重置，属正常现象）；
- 养成随手 Ctrl+S 的习惯（编辑器偶尔会崩，相信老开发者的眼泪）。

## 2.7 本章小结

- 环境：电脑首选 Godot 编辑器；手机 MT管理器也可（纯文本）；
- 文件即类，snake_case 命名，目录自由但统一；
- 缩进是语法：Tab 官方推荐，一个文件绝不混用；
- 十条规范的核心：代码是写给人看的；
- 小步快跑：10 行一测。

## 2.8 自测

1. 下面代码哪里有问题？
```gdscript
func test():
    print("a")
	print("b")
```
（答案：第 2 行是 4 空格缩进、第 3 行是 Tab——混用了。且第 2 行缩进级别比第 3 行浅，块归属混乱。统一即可。）

2. `var HP_MAX = 100`、`var MaxHp = 100`、`const MAX_HP = 100`、`var max_hp = 100` 四个名字，哪个最适合"最大血量常量"？为什么？
（答案：`const MAX_HP = 100`。它是常量（不该变的量），且常量用全大写是通行规范。前两个把常量写成了变量；第四个语法没错但如果它是常量就违反全大写习惯。）

3. 注释 `speed = 200 # 设置速度` 有什么问题？
（答案：只重复了代码"是什么"，没解释"为什么 200"。好注释如：`speed = 200 # 冲刺速度设为基础移速2倍，保证能穿过3格宽的火墙`。）


---

# 第二卷 · 语言核心（语法逐个击破）

# 第 3 章：变量与常量——数据的盒子

## 3.1 变量：程序的记忆

上一章说过：程序 = 数据 + 操作。**变量就是"数据存放处"**。没有变量，程序就是健忘症患者：

```gdscript
print(100 - 30)     # 能算出 70，但结果立刻被丢弃，谁也记不住
```

```gdscript
var hp = 100        # 开一个记忆格，命名为 hp，存入 100
hp = hp - 30        # 取出 hp（100），减 30，结果 70 放回 hp
print(hp)           # → 70 —— 记住的结果随时可用
```

**变量 = 命名 + 存储单元**。名字是给人看的地址，存储单元是机器存放值的地方。

## 3.2 声明变量的四种姿势

```gdscript
# 姿势一：最简声明（动态类型）
var count = 5

# 姿势二：显式类型标注
var count: int = 5

# 姿势三：类型推断（:=）
var count := 5          # 编译器看右边是 5，推断 count 为 int

# 姿势四：先声明后赋值
var count: int          # 此刻 count 默认为 0（int 的默认值）
count = 5
```

四种都能跑，怎么选？**给初学者的直接建议：优先用 `:=`（姿势三）**。理由：

1. 比姿势一安全——以后不小心给它赋错类型的东西（比如字符串），当场报错，而不是留到运行时出灵异 bug；
2. 比姿势二省字——类型自动推断，不用重复写；
3. Godot 官方代码规范同款推荐。

什么时候必须用姿势二（显式标注）？——**先声明后赋值**（暂时不知道值，但想先占位）：

```gdscript
var target: Node2D                 # 先声明（此刻是 null）
# ...稍后根据情况赋值...
target = get_tree().get_first_node_in_group("enemy")
```

## 3.3 赋值的本质：= 不是"等于"

数学里 `a = a + 1` 是荒谬的（一个数怎么会等于自己加一？）。程序里它是天经地义——**`=` 是赋值箭头**，永远读作"把右边的计算结果，塞进左边的盒子"：

```gdscript
var a = 10
a = a + 1        # 右边先算：a+1 → 11；再把 11 塞回 a。此后 a 是 11
```

执行顺序铁律：**永远先算右边，再赋给左边。** 看透这个，下面这些就都好懂了：

```gdscript
var x = 5
x = x * 2        # x → 10
x = x * 2        # x → 20
x = x - 7        # x → 13
```

再狠一点，变量可以参与自己的下落：

```gdscript
var hp = 100
var damage = 30
var armor = 10
hp = hp - max(damage - armor, 1)     # 先算右边：30-10=20，和1取大=20；hp → 80
```

## 3.4 变量的命名规则（法律）与风格（道德）

**法律（违反直接报错）**：

1. 只能用：字母（含中文但不推荐）、数字、下划线 `_`；
2. 不能以数字开头：`1hp` ✘，`hp1` ✔，`hp_1` ✔；
3. 不能用保留字：`var`、`func`、`if`、`class`、`return` 等 30 多个词；
4. 区分大小写：`hp`、`Hp`、`HP` 是三个不同的变量。

```gdscript
var player_name = "小明"     # ✔
var player2 = "小红"          # ✔
var 2player = "小刚"          # ✘ 报错：数字开头
var player-name = "小李"      # ✘ 报错：横杠不合法（会被当成减法！）
var var = 5                   # ✘ 报错：保留字
```

注意 `player-name` 这种错最阴险——在有的语言里合法，初学者带习惯过来，GDScript 里 `player - name` 是个减法表达式，报错还看不太懂。

**风格（不违反但会挨骂）**：

```gdscript
# 推荐
var enemy_count = 10           # snake_case，全小写
var is_boss_dead = false

# 不推荐（能跑，但违背 GDScript 生态习惯）
var EnemyCount = 10            # PascalCase 留给类名
var enemyCount = 10            # 小驼峰是 JS/Java 的习惯
var ENEMY_COUNT = 10           # 全大写留给常量
```

## 3.5 变量的作用域：名字的势力范围

变量不是声明了就处处可用。**作用域 = 这个名字在哪个范围内"活着"**。三种层级：

```gdscript
extends Node

var score = 0                    # 【成员变量/全局于本脚本】整个类里都能用

func add_score(points: int):
	var bonus = 10               # 【局部变量】只在 add_score 函数内活着
	score = score + points + bonus
	print(bonus)                 # ✔ 函数内可用

func show():
	print(score)                # ✔ 成员变量随处可用
	print(bonus)                # ✘ 报错！bonus 不认识——它死在了 add_score 里

func other():
	var score = 999             # ⚠️ 陷阱：这里又声明了一个"局部 score"，
	print(score)                # 打印 999 —— 局部变量暂时遮蔽了同名成员变量！
```

**遮蔽（shadowing）**：局部变量与成员变量同名时，函数内部用的是局部的那份，成员变量纹丝不动。上面 `other()` 里 `score = 999` 改的是自己的局部盒子，全局 score 还是原值。这种写法是 bug 温床——**同名遮蔽能免则免**。

再看一个新手高频翻车现场：

```gdscript
func bad_example():
	if true:
		var msg = "你好"         # 在 if 块里声明的变量
	print(msg)                  # ✘ 报错！msg 的作用域只是那个 if 块
```

块级作用域：`if`/`for`/`while` 块里声明的变量，出了块就消失。要在块外使用，先在外面声明：

```gdscript
func good_example():
	var msg = ""                # 在函数层声明
	if true:
		msg = "你好"             # 在块里只赋值，不重新声明
	print(msg)                  # ✔ "你好"
```

**记忆口诀：变量在哪一层"出生"，就活到那一层的"右花括号"（GDScript 里是回到原缩进级）为止。**

## 3.6 常量：一次定型，永不更改

```gdscript
const MAX_HP = 100
const GRAVITY = 980.0
const GAME_NAME = "勇者传说"
const RESPAWN_TIME := 3.0       # 常量同样可用 := 推断
```

`const` 与 `var` 唯一区别：**只允许赋值一次（声明时）**，之后再赋值直接报错：

```gdscript
const MAX_HP = 100
MAX_HP = 200                    # ✘ 报错：不能修改常量
```

**为什么要发明常量？数值又不会自己跑掉。** 三个理由：

1. **防御手滑**：某个"不该变的值"（π、重力、最大血量）被未来某行代码误改，是极常见的 bug。const 把这种可能直接扼杀；
2. **一改全改**：重力 980 出现在 17 个地方，想调难度改成 1200，要改 17 处，漏一处就穿帮。写成常量只改 1 处；
3. **自带说明书**：`velocity.y += 980 * delta`（980 是啥？）vs `velocity.y += GRAVITY * delta`（哦，重力）。

**const 的高级用法（先混个眼熟）**：

```gdscript
# 常量可以由表达式计算（编译期就能算出结果的都行）
const HALF_HP = MAX_HP / 2                  # 引用另一个常量
const DASH_SPEED = BASE_SPEED * 2.0
const ENEMY_UIDS = ["slime_01", "bat_03"]   # 数组/字典也能做常量内容

# 但不能引用"运行时才知道"的值
# const RAND = randi()                      # ✘ 报错：randi() 要运行时才算
```

⚠️ 一个深度陷阱：const 数组/字典**内容仍然可改**（const 锁的是"盒子指向哪"，不锁"盒子里的东西"）：

```gdscript
const LIST = [1, 2, 3]
LIST.append(4)      # ✔ 居然合法！
LIST = [9, 9, 9]    # ✘ 报错（这才被禁止）
```

想彻底锁死内容，没有语言级手段，靠自觉（把常量数组当只读看待）。读代码时要知道这层微妙。

## 3.7 变量的默认值：不赋值时里面是什么

每种类型都有"出厂默认值"：

```gdscript
var a: int          # 0
var b: float        # 0.0
var c: String       # ""
var d: bool         # false
var e: Vector2      # (0, 0)
var f: Array        # []（空数组）
var g: Dictionary   # {}（空字典）
var h: Node2D       # null（对象类型默认都是 null）
```

这解释了两个常见现象：

现象一：忘了初始化，程序不报错但行为怪：

```gdscript
var total: int
for i in 10:
	total += i          # total 从默认值 0 开始累加，碰巧没问题
print(total)            # 45
```

如果默认值不是 0（比如 float 的 0.0 参与整数运算、null 被拿去调用方法），就会炸。所以**好习惯：声明时就给有意义的初值**。

现象二：null 一切对象类型的默认值，也是新手报错之王：

```gdscript
var target: Node2D     # 此刻 target == null
target.position        # ✘ 运行时崩：Invalid call. Directory or file does not exist / null instance
```

null 上的任何操作都崩。守卫姿势（第 6、7 章还会反复出现）：

```gdscript
if target != null:
	target.position = Vector2.ZERO
# 或更严谨（对象可能"已被销毁"但引用还在）：
if target != null and is_instance_valid(target):
	target.position = Vector2.ZERO
```

## 3.8 多变量声明与解构赋值

GDScript 支持一行声明多个变量（用逗号），以及"解构"（把一组值拆进多个变量）：

```gdscript
# 一行多变量
var a = 1, b = 2, c = 3           # ✔ 合法，但可读性一般，不建议滥用

# 数组解构
var pos = [100, 200]
var x = pos[0]                     # 传统取法
var x2, y2 = pos                   # 解构：x2=100, y2=200 —— 注意元素不够时是 null

# 经典用途：向量拆分量
var v = Vector2(3, 7)
var vx, vy = v                     # vx=3, vy=7
```

解构在"函数返回多个值"场景非常好用（第 7 章）：

```gdscript
func get_min_max(arr: Array) -> Array:
	return [arr.min(), arr.max()]

var lo, hi = get_min_max([4, 9, 1, 7])    # lo=1, hi=9
```

## 3.9 变量赋值的行为差异：值类型 vs 引用类型（重要！）

先看两个实验：

**实验一（数字，怎么拷贝都安全）**：

```gdscript
var a = 10
var b = a          # 把 a 的值复制给 b
b = 99
print(a)           # → 10（a 毫发无伤）
```

**实验二（数组，"复制"的是钥匙）**：

```gdscript
var list_a = [1, 2, 3]
var list_b = list_a        # ⚠️ 这不是复制内容！
list_b.append(4)
print(list_a)              # → [1, 2, 3, 4]  a 也变了！！
```

为什么？因为 GDScript 的数据分两大类：

| 类别 | 包括 | 赋值时发生什么 |
|---|---|---|
| **值类型** | int、float、bool、String、Vector2、Color、Rect2...（基础类型） | **复制内容**。改新变量，旧变量不受影响 |
| **引用类型** | Array、Dictionary、所有对象/节点 | **复制"地址"**。两个名字指向同一份数据，改谁都是改它 |

生活化理解：
- 值类型像**复印件**：把你的笔记复印给别人，别人在复印件上乱画，你的原件没事；
- 引用类型像**同一间房的备用钥匙**：你配了把钥匙给室友，室友把房间搞乱，你开门看到的也是乱房间。

**怎么真正复制一份引用类型的数据？** 用 `duplicate()`：

```gdscript
var list_a = [1, 2, 3]
var list_b = list_a.duplicate()     # 真·深拷贝
list_b.append(4)
print(list_a)                        # → [1, 2, 3]  a 安全了

var dict_a = {"hp": 100}
var dict_b = dict_a.duplicate()      # 字典同理
# 嵌套结构要深拷贝：
var deep = complex_data.duplicate(true)   # true = 连里面的子数组/子字典一起拷
```

这个知识点在函数传参时还会坑一次（第 7 章详解），此处先扎根印象。

## 3.10 成员变量 vs 局部变量：什么时候用哪个

**判断流程**（背下来）：

```
这个数据需要在"当前这次函数调用"之外还存在吗？
├── 不需要（算完就没用）→ 局部变量 var
└── 需要（要被别的函数用/跨帧保留）→ 成员变量
```

例：玩家受伤闪红。

```gdscript
# 闪红只需要在受击函数里临时算 → 局部
func take_damage(amount: int):
	var final_damage = max(amount - defense, 1)   # 局部：算完就用完
	hp -= final_damage
	flash_red()                                   # 触发别的函数
	flash_time = 0.2                              # flash_time 是成员变量！
	#                                          因为闪红要持续好几帧，
	#                                          _process 里每帧都在消耗它
```

```gdscript
var flash_time: float = 0.0        # 成员变量：跨帧存在的状态

func _process(delta):
	if flash_time > 0.0:
		flash_time -= delta        # 每帧倒计时
		modulate = Color(1, 0.5, 0.5)
	else:
		modulate = Color.WHITE
```

**成员变量 = 对象的"长期记忆"；局部变量 = 函数的"草稿纸"。** 草稿纸乱点没事，长期记忆要精心管理（命名、初值、注释）。

## 3.11 完整小案例：把本章知识串起来

需求：实现一个简单的"连击计数器"——攻击时连击+1，2 秒不打就连击清零。

```gdscript
extends Node

# ---- 成员变量区（对象的长期记忆）----
var combo_count: int = 0               # 当前连击数
var combo_timer: float = 0.0           # 连击倒计时（剩余秒数）
const COMBO_RESET_TIME := 2.0          # 常量：多久没攻击就清零

func _process(delta: float) -> void:
	# 每帧：连击计时倒计时
	if combo_timer > 0.0:
		combo_timer -= delta           # 引用成员变量，无需 var
		if combo_timer <= 0.0:         # 计时耗尽
			reset_combo()

func attack() -> void:
	combo_count += 1                   # 连击+1
	combo_timer = COMBO_RESET_TIME     # 重置计时（用常量，见3.6）
	print("连击 x", combo_count)       # 阶段性成果：局部计算
	var is_big_combo = combo_count >= 10   # 局部变量：算完即弃
	if is_big_combo:
		print("大爆发！伤害加成 50%")

func reset_combo() -> void:
	print("连击中断，最终：", combo_count)
	combo_count = 0                    # 清零（成员变量，跨函数修改）
```

用到本章全部知识点：成员/局部/常量三种变量、赋值、作用域、默认值、命名规范。逐行读一遍，确保每行都能说出"为什么"。

## 3.12 常见错误清单

| 错误代码 | 报错/现象 | 原因 |
|---|---|---|
| `hp = 100`（没写 var） | 报错/意外创建 | 函数内必须 var；类内成员变量可以不写 var（Godot 4.3+ 新特性，但建议都写） |
| `var 1st_place = ...` | 语法错误 | 名字数字开头 |
| `var my-var = ...` | 语法错误 | 横杠当减法 |
| `const X = 1; X = 2` | 常量被赋值 | const 只能赋一次 |
| if 块里 var，块外用 | Identifier not found | 块级作用域 |
| `var b = a_array` 后改 b，a 也变 | 灵异现象 | 引用类型赋值是共享，不是复制 |
| 忘记初始化的 float 参与 int 运算 | 类型不匹配警告 | 0.0 与 0 不同类型 |

## 3.13 练习

1. 指出下面代码 3 个问题：
```gdscript
func calc():
	var total
	for i in 5:
		total = total + i
	print(total)
```
（答案：① total 声明了但没初值，默认 null，null+i 直接崩；② total 应在循环外声明一次、在循环里累加是可行的，但更糟的写法是放循环里；③ 若想累加，正确写法是 `var total := 0`。）

2. 只用变量和赋值（不用 if），交换 a、b 两个变量的值。
```gdscript
var a = 5
var b = 9
var temp = a
a = b
b = temp
# 或 GDScript 特色一行流：
# a, b = b, a
```

3. 预测输出：
```gdscript
var x = 10
func test():
	var x = 20
	x = x + 5
	print(x)      # A 处
func test2():
	print(x)      # B 处
```
（答案：A 处 25（局部变量）；B 处 10（成员变量）。）

4. 下面代码输出什么？为什么？
```gdscript
var arr1 = [1, 2]
var arr2 = arr1
arr2.append(3)
print(arr1 == arr2)
print(arr1.size())
```
（答案：true 和 3。arr2 和 arr1 是同一份数据（引用），append 之后两个名字看到同样的 [1,2,3]。）

---

# 第 4 章：数据类型大全——盒子里能装什么

## 4.1 类型系统鸟瞰

GDScript 是"渐进类型"语言：你可以完全不写类型（像 Python），也可以处处写类型（像 Java），还能混着来。类型的价值：

1. **提前抓错**：`var hp: int = 100` 之后 `hp = "满血"` → 编辑器立刻红线；
2. **自动补全**：写出 `var sprite: Sprite2D = ...` 后，`sprite.` 会弹出全部可用属性方法；
3. **文档效果**：`func heal(amount: int) -> void` 一眼看清进出。

本章把**每一种基础类型**过一遍，每个类型配：说明、声明方式、常用操作、典型陷阱。

## 4.2 int：整数

没有小数点的数，可正可负。用于：血量、金币、关卡、计数。

```gdscript
var hp := 100
var gold := -50                # 负数
var big := 9223372036854775807 # int 上限（64位），日常用不到顶
print(hp / 3)                  # → 33  ⚠️ 整数除法砍小数（第 5 章详解）
print(hp % 3)                  # → 1   取余
```

int 的边界常识：64 位整数范围 ±9.2×10^18。做游戏永远够用，但**连乘注意溢出**：`pow(2, 63)` 之类的表达式结果会绕回负数（和所有语言一样）。

## 4.3 float：浮点数（小数）

```gdscript
var speed := 250.0             # 带 .0 就是 float
var gravity := 980.0
var half := 0.5
var sci := 1.5e3               # 科学计数法 → 1500.0
```

**必知：浮点数有误差！** 计算机用二进制存小数，0.1 这种数存不精确：

```gdscript
print(0.1 + 0.2)                    # → 0.30000000000000004（不是0.3！）
print(0.1 + 0.2 == 0.3)             # → false ！！
print(is_equal_approx(0.1 + 0.2, 0.3))  # → true  ✔ 用这个比较
```

三条浮点军规：

```gdscript
# 军规一：判等用 is_equal_approx，别用 ==
if is_equal_approx(a, b): ...

# 军规二：判"≥"边界也用 approx 版
if is_zero_approx(x - 10.0): ...

# 军规三：显示给玩家前四舍五入
print("%.2f" % 3.14159)             # → 3.14
print(round(2.5))                    # → 3.0（注意返回还是float）
print(int(round(2.5)))               # → 3（要整数需再转）
```

典型翻车：做移动判定 `if position.x == target_x`，因为浮点误差永远差 0.0001，条件永不成立，角色卡死在目标前。**凡涉及 float 的相等判断，一律 is_equal_approx 或改用范围判断。**

## 4.4 int 与 float 的混算规则

```gdscript
print(5 / 2)          # → 2      int / int   = int（砍小数！）
print(5.0 / 2)        # → 2.5    float 参与 = float
print(5 / 2.0)        # → 2.5
print(int(5) / 2)     # → 2      转成int没用，还是int÷int
print(float(5) / 2)   # → 2.5    要先转float
print(7 % 2)          # → 1      整数取余
print(7.5 % 2)        # → 1.5    float 也能取余
```

**int→float 自动升格**：`var x := 5 + 0.0`，x 是 5.0（float）。**float→int 必须显式转**，且转法有讲究：

```gdscript
var f := 3.7
print(int(f))          # → 3    直接砍掉小数（不四舍五入！）
print(round(f))        # → 4.0  四舍五入，但结果是float
print(int(round(f)))   # → 4    四舍五入取整的完整姿势
print(floor(3.9))      # → 3.0  向下取整
print(ceil(3.1))       # → 4.0  向上取整
print(floori(3.9))     # → 3    向下取整直接给int（4.x推荐）
print(roundi(3.7))     # → 4    四舍五入直接给int
print(ceili(3.1))      # → 4
```

记忆：**i 结尾的取整函数（roundi/floori/ceili）直接返回 int**，最省心。

## 4.5 String：字符串

任意文本，双引号或单引号包裹（推荐双引号统一风格）：

```gdscript
var name := "勇者"
var msg := '你好'
var empty := ""
```

字符串是**值类型**（3.9 节），赋值即复制，改新不改旧——这点与数组相反，很多人搞混。超长字符串、拼接、格式化、全部 40+ 方法在第 11 章专题精讲。这里只给 3 个最常见的：

```gdscript
var s := "Hello"
print(s.length())       # 5        长度
print(s + " World")     # Hello World  拼接
print(str(42))          # "42"     万物转字符串
```

## 4.6 bool：真假

只有两个值：`true` / `false`。是所有"判断"的燃料：

```gdscript
var is_dead := false
var has_key := true

if is_dead:
	print("游戏结束")
if not has_key:
	print("门打不开")
```

**truthy 概念**：GDScript 里不是所有语言都允许 `if 1:`。GDScript 严格——if 后面必须是 bool 或能转成 bool 的比较表达式：

```gdscript
var hp := 100
if hp:                  # ⚠️ 合法！非零数字转 true，零转 false（但别这么写）
	print("还活着")
# 等价于 if hp != 0:  ——永远写明确版本
```

显式转换：

```gdscript
print(bool(1))          # true
print(bool(0))          # false
print(bool(""))         # false（空串）
print(bool("文字"))      # true
print(bool([]))         # false（空数组）
print(bool([1]))        # true
```

## 4.7 null：什么都没有

null 不是类型，是**任何对象类型都可能取的特殊值**，表示"没有对象"：

```gdscript
var target: Node2D = null     # 明确"还没有目标"
var data = null               # 未指定类型时，null 本身也是一种状态

if target == null:
	print("目标丢失")
```

null 的正确用途：
1. **占位**：稍后才会有值的变量，先置 null；
2. **表示"无"**：武器槽空着、没有目标、查询无结果；
3. **函数返回失败**：`load("不存在的路径")` 返回 null。

null 的头号大罪：**null 上的操作必崩**：

```gdscript
var t = null
t.position          # 💥 崩
t.free()            # 💥 崩
```

防御 null 的三种姿势：

```gdscript
# 姿势一：用前判空
if t != null:
	t.position = Vector2.ZERO

# 姿势二：判空+验活（对象可能已 queue_free）
if t != null and is_instance_valid(t):
	t.position = Vector2.ZERO

# 姿势三：合并运算符（Godot 4.3+），null 时用右边的兜底值
var speed = config.get("speed", 500.0)    # 字典get自带兜底
```

判空顺序很重要：`if t != null and t.hp > 0` ✔（左边false就短路，右边不执行）；`if t.hp > 0 and t != null` 💥（先碰t.hp就崩）。**and 把"便宜的、保命的"条件放左边**——这就是第 5 章要讲的"短路求值"。

## 4.8 Vector2：二维向量（2D 游戏的血液）

一个 Vector2 打包了两个 float（x 和 y），表示**坐标、方向、速度、偏移、尺寸**：

```gdscript
var pos := Vector2(100, 200)      # 点：x=100, y=200
var vel := Vector2(0, -50)        # 速度：向上每秒50像素
var size := Vector2(32, 64)       # 尺寸：宽32高64

# 分量访问
print(pos.x)                      # 100.0
print(pos.y)                      # 200.0

# 预置常量
Vector2.ZERO                      # (0, 0)
Vector2.ONE                       # (1, 1)
Vector2.RIGHT                     # (1, 0)  屏幕右方
Vector2.LEFT                      # (-1, 0)
Vector2.UP                        # (0, -1) 屏幕上方（y轴向下！）
Vector2.DOWN                      # (0, 1)
Vector2.INF                       # (inf, inf) 无穷

# 四则运算（逐分量）
var a := Vector2(1, 2)
var b := Vector2(10, 20)
print(a + b)          # (11.0, 22.0)
print(a - b)          # (-9.0, -18.0)
print(a * 3)          # (3.0, 6.0)     向量×数：整体放大
print(a * b)          # (10.0, 40.0)   向量×向量：逐分量相乘
print(a / 2)          # (0.5, 1.0)
```

**⚠️ 屏幕坐标 y 轴向下！** 这是 2D 图形界的祖传约定（源自电视扫描线）。`Vector2(0, 100)` 在屏幕**下方**。"往上跳"要给 y 负值。第一次做游戏的人 100% 在这里晕一次，现在晕比以后晕好。

**方向与长度（核心 API）**：

```gdscript
var v := Vector2(3, 4)

v.length()             # 5.0    长度（勾股：√(9+16)）
v.length_squared()     # 25.0   长度的平方（省开方，比较距离用，性能优化常见）
v.normalized()         # (0.6, 0.8)  单位化：方向不变，长度变1
v.direction_to(w)      # 从v指向w的单位向量
v.distance_to(w)       # 两点距离
v.distance_squared_to(w) # 距离的平方
v.angle()              # 与x轴正方向的夹角（弧度）
v.rotated(0.5)         # 旋转0.5弧度后的新向量
v.dot(w)               # 点积（判断同向/夹角，AI视野常用）
v.cross(w)             # 叉积（2D返回float，判断左右侧）
v.limit_length(500.0)  # 长度超500就截到500
v.move_toward(target, step)  # 朝target挪step距离（追击移动的核心！）
```

实战三连：

```gdscript
# ① 匀速追击敌人（每帧调用）
position = position.move_toward(enemy.position, speed * delta)

# ② 朝目标方向发射子弹
var dir = (target_pos - global_position).normalized()
bullet.velocity = dir * 800.0

# ③ 判断敌人在自己面前还是背后（AI视野）
var to_enemy = (enemy.position - position).normalized()
if facing_dir.dot(to_enemy) > 0.5:      # 点积>0.5≈夹角小于60°
	see_enemy()
```

## 4.9 Vector2i / Vector3 / Vector3i / Vector4（家族速览）

```gdscript
# Vector2i：整数版二维（网格坐标、瓦片地图最爱）
var cell := Vector2i(3, 7)
print(cell.x)          # 3（int，不是float）

# Vector3：三维（3D位置/速度）
var p3 := Vector3(1, 2, 3)
print(p3.y)            # 2.0
Vector3.ZERO / UP / FORWARD / BACK

# Vector3i：整数三维
var block := Vector3i(0, 5, 12)

# Vector4：四维（shader颜色、数学特殊场景）
var v4 := Vector4(1, 1, 1, 1)
```

2D 游戏主要和 Vector2/Vector2i 打交道；Vector2i 用于"格子"（棋盘、背包格、瓦片），它的分量是 int，做格子运算不会有浮点误差，且能直接当字典键：

```gdscript
var tile_data := {}                    # 字典键用Vector2i
tile_data[Vector2i(2, 3)] = "草地"
tile_data[Vector2i(4, 1)] = "石头"
print(tile_data[Vector2i(2, 3)])       # 草地
```

## 4.10 Color：颜色

四个 0~1 的分量：红、绿、蓝、透明度(alpha)：

```gdscript
var red := Color(1, 0, 0)
var white := Color(1, 1, 1)              # 全1=白，全0=黑
var half := Color(1, 1, 1, 0.5)          # 半透明白
var gold := Color(1.0, 0.84, 0.0)        # 金
var by_name := Color.RED                 # 预置常量
var by_hex := Color("#ff8800")           # 十六进制（设计师给色值用这个）
var by_hex_a := Color("#ff880088")       # 8位=带透明度

# 分量
print(red.r)          # 1.0
print(half.a)         # 0.5

# 常用操作
var dark := Color(0.5, 0.5, 0.5)
print(dark.lightened(0.3))      # 提亮30%
print(dark.darkened(0.3))       # 压暗30%
print(red.lerp(blue, 0.5))      # 红到蓝的中点色（渐变动画核心！）

# to_html() 反向：颜色转十六进制字符串
print(gold.to_html(false))      # "ffd700"
```

**游戏实战**：受伤闪红 `modulate = Color(1, 0.3, 0.3)`；无敌闪烁 `modulate.a = 0.5`；毒发变绿 `modulate = Color(0.6, 1, 0.6)`；血条渐变 `bar.color = Color.RED.lerp(Color.GREEN, hp_ratio)`。

## 4.11 Rect2：矩形区域

一个位置 + 一个尺寸，描述矩形（框选、判定区、图片裁剪区）：

```gdscript
var rect := Rect2(0, 0, 100, 50)      # 从(0,0)起，宽100高50
var rect2 := Rect2(Vector2(10, 10), Vector2(80, 30))   # 等价写法

rect.position         # (0, 0)
rect.size             # (100, 50)
rect.end              # (100, 50) 右下角点

# 核心方法
rect.has_point(Vector2(50, 25))        # true 点是否在矩形内
rect.intersects(other_rect)            # 两矩形是否相交（碰撞检测）
rect.encloses(other_rect)              # 是否完全包住另一个
rect.grow(10)                          # 四边外扩10像素的新矩形
rect.abs()                             # 负尺寸转正
```

**精灵表抠图**（游戏特效/帧动画的核心用法）：

```gdscript
$Sprite2D.region_enabled = true
$Sprite2D.region_rect = Rect2(64, 128, 64, 64)   # 只显示大图的这块64x64区域
```

**简单矩形碰撞**（无需物理引擎）：

```gdscript
var hitbox := Rect2(position - size / 2, size)
if hitbox.intersects(enemy.hitbox):
	print("撞到了！")
```

## 4.12 Callable：函数的"值"

GDScript 里**函数本身也能装进变量**传递。装着函数的值叫 Callable（可调用体）：

```gdscript
# 创建
var f = take_damage                  # 注意：没有括号！加括号是"调用"，不加是"引用"
var g = func(x): return x * 2        # lambda 也是 Callable

# 调用
f.call(30)                           # call() 执行它
g.call(21)                           # → 42

# 也有便捷直接调用（4.x）：
f.call(30)                           # 标准姿势
```

Callable 的三大用途（后面章节反复出现）：

```gdscript
# 用途一：信号连接（第 21 章）——把函数交给事件系统
button.pressed.connect(on_button)     # 递的是函数本身

# 用途二：延时回调（Tween/Timer）
tween.tween_callback(play_sound)      # 动画到点时执行

# 用途三：策略模式——把"怎么做"当参数传
func apply_to_all(items: Array, action: Callable):
	for item in items:
		action.call(item)

apply_to_all(enemies, func(e): e.stun())
apply_to_all(items, func(i): i.price *= 0.5)
```

Callable 自省方法（调试利器）：

```gdscript
var c = my_func
c.is_valid()          # 是否可调用
c.get_object()        # 绑定的对象
c.get_method()        # 函数名字符串
```

## 4.13 类型转换大全（cast 速查表）

```gdscript
# 数字之间
int(3.9)              # 3     （砍小数）
float(3)              # 3.0
int("42")             # 42
float("3.5")          # 3.5

# 万物 → 字符串
str(42)               # "42"
str(3.5)              # "3.5"
str(true)             # "true"
str([1,2])            # "[1, 2]"
str(Vector2(3,4))     # "(3.0, 4.0)"

# 字符串 → 数字
"42".to_int()         # 42
"3.5".to_float()      # 3.5
int("abc")            # 0（转不动给0，不报错！）
int("12abc")          # 12（能转多少转多少）

# bool
bool(1)               # true
bool("")              # false

# 对象向下转型（父类→子类）
var node: Node = get_child(0)
var sprite := node as Sprite2D     # 是Sprite2D就转，不是就null（安全转）
var sprite2: Sprite2D = node       # 不是Sprite2D会报错（强转）
```

`as` vs 直接标注：`as` 转不动给 null（配合判空最安全），直接标注转不动报错。**读 API 返回 Node 的东西时，`as` + 判空是黄金组合**：

```gdscript
var s := get_node_or_null("Icon") as Sprite2D
if s != null:
	s.modulate = Color.RED
```

## 4.14 类型标注的进阶规则

```gdscript
# 基础
var a: int = 5
var b := 5.0                # 推断为float

# 推断的陷阱：推断成"字面量最窄类型"
var c := 5                  # int —— 之后 c = 5.0 会报错！
var d := 5.0                # float
# 想让数字变量未来能装小数，初始化时就写 5.0

# 参数与返回值（第 7 章展开）
func heal(amount: int) -> void: ...
func get_pos() -> Vector2: ...

# 类型化容器（第 10 章展开）
var enemies: Array[Node2D] = []
var scores: Dictionary = {}    # 字典暂不支持值类型参数

# 特殊返回类型
# -> void        不返回
# -> Variant     任何类型都行（等于不标注，但表达"故意不标"）
```

什么时候**不标**类型？
- lambda 内部临时量（标了反而啰嗦）；
- 真正动态的数据（从 JSON 读来的混合结构）；
- 快速试验代码。生产代码建议全标——报错越早，bug 越便宜。

## 4.15 本章知识地图

```
GDScript 数据类型
├── 基础值类型（赋值=复制）
│   ├── int          整数（/会砍小数！）
│   ├── float        小数（有误差，判等用is_equal_approx）
│   ├── bool         true/false（if 后面放这个）
│   ├── String       文本（专题见第11章）
│   ├── Vector2/2i   2D坐标方向（y向下！）
│   ├── Vector3/3i/4 3D与四维
│   ├── Color        RGBA各0~1
│   ├── Rect2        矩形（抠图/碰撞）
│   └── Callable     函数的值（信号/回调/策略）
├── 引用类型（赋值=共享）
│   ├── Array        数组（第8章）
│   ├── Dictionary   字典（第9章）
│   └── 所有对象/节点（第13、19章）
└── 特殊值
    └── null         "没有对象"——判空是保命技能
```

## 4.16 练习

1. 判断输出：
```gdscript
print(7 / 2)
print(7 % 2)
print(7.0 / 2)
print(int(7.9))
print(roundi(7.5))
```
（答案：3、1、3.5、7、8）

2. 只用本章知识写：把速度向量 (300, 400) 变成方向和速率两个值。
```gdscript
var v := Vector2(300, 400)
var speed := v.length()              # 500
var dir := v.normalized()            # (0.6, 0.8)
```

3. `Color("#ff0000")` 和 `Color(1, 0, 0)` 什么关系？`Color(1,1,1,0)` 的 a=0 意味着？
（答案：同一个红色（红通道255/255=1.0）；完全透明，显示上不可见但仍在渲染。）

4. 下面的判等哪里危险？怎么改？
```gdscript
if node.position.x == 100.0:
	print("到达")
```
（答案：浮点误差可能让 x 是 99.99999 或 100.00001，永远不等。改成 is_equal_approx(node.position.x, 100.0) 或 absf(node.position.x - 100.0) < 0.5。）

5. `var data = load("res://icon.svg")` 之后直接 `data.width` 安全吗？
（答案：不安全。load 失败返回 null，null.width 崩溃。先判 `if data != null:`。）


# 第 5 章：运算符大全——数据怎么被加工

运算符是语法的"动词"，连接数据产生新数据。本章按功能分 8 组，每组都配：语法表、语义、例子、陷阱。

## 5.1 算术运算符：加减乘除余

| 运算符 | 名字 | 例子 | 结果 |
|---|---|---|---|
| `+` | 加 | `5 + 2` | `7` |
| `-` | 减 | `5 - 2` | `3` |
| `*` | 乘 | `5 * 2` | `10` |
| `/` | 除 | `5 / 2` | `2`（int！见下） |
| `%` | 取余 | `5 % 2` | `1` |
| `**`（4.4+） | 幂 | `5 ** 2` | `25` |
| `-x` | 取负 | `-x` | 符号翻转 |
| `unary +` | 正号 | `+x` | 原样（几乎不用） |

**头号陷阱：整数除法**。int / int = int，小数**直接砍掉**（向零取整，不是四舍五入）：

```gdscript
print(10 / 3)         # 3     不是 3.333
print(7 / 2)          # 3     不是 3.5
print(-7 / 2)         # -3    向零取整（-3.5 → -3）
print(5 / 0)          # 💥 报错崩溃！除零是运行时错误
print(5.0 / 0.0)      # inf（float除零给无穷，不崩但多半是bug）
```

任何一边是 float，就走小数除法：

```gdscript
print(10 / 3.0)       # 3.3333332538604736
print(10.0 / 3)       # 同上
print(float(10) / 3)  # 同上
```

**取余 % 的妙用**（游戏开发天天用）：

```gdscript
# 妙用一：循环取值（不超过范围地循环）
var frame = total_frame % 8          # 0~7 循环，永不出界

# 妙用二：判断整除/奇偶
if year % 4 == 0: ...                # 被4整除
if hp % 2 == 1: print("奇数血")       # 奇偶判断

# 妙用三：限制随机数范围
var dice = randi() % 6               # 0~5（randi()给大整数，%6砍到0~5）

# 妙用四：格子坐标
var col = index % 10                 # 10列的表格：列号
var row = index / 10                 # 行号（整除）
```

⚠️ 负数取余的符号：GDScript 的 % 结果符号**跟随被除数**（同 C 语言）：

```gdscript
print(-7 % 3)         # -1
print(7 % -3)         # 1
```

要"总是正的余数"用 `wrapi()` 或 `posmod()`：

```gdscript
print(posmod(-7, 3))  # 2  （数学意义上的模）
print(wrapi(-1, 0, 8)) # 7  （-1在0~8循环里是7，做循环索引超好用）
```

## 5.2 复合赋值运算符：偷懒但可读

```gdscript
var hp := 100

hp += 30        # 等价 hp = hp + 30   → 130
hp -= 50        # 等价 hp = hp - 50   → 80
hp *= 2         # 等价 hp = hp * 2    → 160
hp /= 4         # 等价 hp = hp / 4    → 40（注意int除法！160/4=40没问题）
hp %= 7         # 等价 hp = hp % 7    → 5

# 字符串也能 +=
var log := "事件:"
log += "玩家受伤"     # → "事件:玩家受伤"
# 数组没有 +=（用append），但可以：
var arr := [1]
arr += [2, 3]        # → [1, 2, 3]（拼接语义）
```

**GDScript 没有 `++` 和 `--`**！C/Java 的 `i++` 在这里直接语法错误。自增写：

```gdscript
count += 1          # 标准姿势
count = count + 1   # 啰嗦版
```

## 5.3 比较运算符：生产 bool

| 运算符 | 含义 | 例子 | 结果 |
|---|---|---|---|
| `==` | 等于 | `5 == 5` | `true` |
| `!=` | 不等于 | `5 != 3` | `true` |
| `<` | 小于 | `3 < 5` | `true` |
| `>` | 大于 | `3 > 5` | `false` |
| `<=` | 小于等于 | `5 <= 5` | `true` |
| `>=` | 大于等于 | `4 >= 5` | `false` |

**`==` 与 `=` 的生死之别**（新手第一坑）：

```gdscript
var hp := 100
if hp == 0: ...       # ✔ 判断hp是否为0
if hp = 0: ...        # ✘ 语法错误（GDScript会拦住，有的语言静默变bug）
```

技巧：比较写"常量在左"可防手滑（`if 0 == hp:`），不过 GDScript 编辑器会报错，正常写法即可。

**浮点判等**（第 4 章讲过，再强调）：

```gdscript
0.1 + 0.2 == 0.3              # false！！
is_equal_approx(0.1 + 0.2, 0.3)  # true ✔
```

**字符串比较**：按字典序逐字符比较（Unicode 码点）：

```gdscript
"abc" == "abc"        # true
"a" < "b"             # true
"Z" < "a"             # true（大写Z码点90 < 小写a码点97）
"10" < "9"            # true！！字符串比较按位："1" < "9"
10 < 9                # false（数字比大小就正常了）
```

⚠️ "10" < "9" 是字符串比较的经典陷阱——排序数字时如果装在 String 里比，顺序会乱。**数字比较前务必转回 int/float**。

**null 判断**：

```gdscript
var t = null
t == null             # true
t != null             # false
# 判对象是否存在，惯例顺序：
if t == null: return
```

## 5.4 逻辑运算符：组合判断

| 运算符 | 别名 | 读作 | 规则 |
|---|---|---|---|
| `and` | `&&` | 且 | 两边都真才真 |
| `or` | `||` | 或 | 一边真就真 |
| `not` | `!` | 非 | 真假翻转 |

```gdscript
var hp := 50
var has_key := true

hp > 30 and has_key        # true   血够且有钥匙
hp < 30 or has_key         # true   血不够 或 有钥匙
not has_key                # false
hp > 0 and not has_key     # false
```

**短路求值（short-circuit）——本节最重要**：

- `and`：左边是 false，右边**看都不看**（结果已注定 false）
- `or`：左边是 true，右边**看都不看**（结果已注定 true）

这不是优化细节，是**保命机制**：

```gdscript
# 危险版：如果 target 是 null，访问 target.hp 当场崩溃
if target != null and target.hp > 0: ...    # ✔ 安全：左边false就短路，右边不执行
if target.hp > 0 and target != null: ...    # 💥 先执行 target.hp → 崩

# 实战三连（顺序就是安全设计）：
if node != null and is_instance_valid(node) and node.visible:
	# ① 不为空 → ② 对象还活着 → ③ 才敢碰它的属性
	...
```

军规：**and 链里，"可能崩"的检查放左边，"需要前面成立才有意义"的放右边。**

**真值表**（背到条件反射）：

| A | B | A and B | A or B |
|---|---|---|---|
| 真 | 真 | 真 | 真 |
| 真 | 假 | 假 | 真 |
| 假 | 真 | 假 | 真 |
| 假 | 假 | 假 | 假 |

逻辑运算返回的一定是 bool：

```gdscript
print(true and false)     # false
print(not true)           # false
print(5 > 3 and 2 > 1)    # true（先算比较，再算逻辑）
```

运算优先级：`not` > `and` > `or`。拿不准就加括号，括号不要钱：

```gdscript
# 意图：活着 且 (有钥匙 或 有斧头)
if is_alive and (has_key or has_axe): ...    # ✔ 括号明确
if is_alive and has_key or has_axe: ...      # ✘ 实际是 (活着且有钥匙) 或 有斧头 —— 逻辑变了！
```

## 5.5 成员运算符 in：在里面吗

```gdscript
# 数组：是否包含元素
var fruits := ["苹果", "香蕉"]
print("苹果" in fruits)         # true
print("西瓜" in fruits)         # false
print(not ("西瓜" in fruits))   # true

# 字符串：是否包含子串
print("god" in "godot")         # true
print("dot" in "godot")         # true

# 字典：是否包含键（注意：是键，不是值！）
var d := {"hp": 100, "mp": 50}
print("hp" in d)                # true
print(100 in d)                 # false！100是值不是键

# 遍历语法（第 6 章）：in 还有"逐个取出"的含义
for item in fruits: ...
```

in 的判等用的是 `==`，所以**浮点元素判存在**同样有误差坑（极少遇到，知道即可）。

## 5.6 类型运算符 is：是这个类型吗

```gdscript
var node = $Sprite2D

if node is Sprite2D:
	print("是精灵")
if node is Node2D:
	print("也是Node2D（父类）——is 认父子关系")   # 会打印

# 常见实战：遍历孩子，只处理某类节点
for child in get_children():
	if child is CollisionShape2D:
		child.disabled = true        # 只对碰撞形状操作
```

**is 认继承链**：`Sprite2D` 继承自 `Node2D` 继承自 `CanvasItem` 继承自 `Node`。所以 `sprite is Node` 也是 true。判断"是不是人类"用最具体的类，判断"是不是生物"用父类——取决于你要做什么级别的操作。

## 5.7 三元运算符：一行迷你 if

```gdscript
# 格式：真值 if 条件 else 假值
var label = "已死" if hp <= 0 else "存活"

# 等价于四行：
# var label
# if hp <= 0:
#     label = "已死"
# else:
#     label = "存活"
```

嵌套（可读性陡降，最多一层）：

```gdscript
var grade = "S" if score >= 90 else ("A" if score >= 80 else "B")
```

适用判断：**只是"二选一取值"**。如果分支里要执行多条语句、或有副作用（改状态），老实写 if/else。

实战例子：

```gdscript
# 移动方向（按住左右键给±1，否则0）
var dir_x = 1 if Input.is_action_pressed("right") else (-1 if Input.is_action_pressed("left") else 0)

# 数值钳制前的边界显示
text = "MAX" if hp == max_hp else str(hp)
```

## 5.8 位运算符（进阶，可选掌握）

把整数当作 64 个 0/1 的开关来操作。日常开发 80% 用不上，但**读引擎源码、做权限/状态标志位时会遇到**：

| 运算符 | 名字 | 例子 | 说明 |
|---|---|---|---|
| `&` | 按位与 | `12 & 10` → `8` | 两位都1才1 |
| `\|` | 按位或 | `12 \| 10` → `14` | 一位1就1 |
| `^` | 按位异或 | `12 ^ 10` → `6` | 不同才1 |
| `~` | 按位非 | `~12` → `-13` | 0/1全翻转 |
| `<<` | 左移 | `3 << 2` → `12` | 二进制左移=×2^n |
| `>>` | 右移 | `12 >> 2` → `3` | ÷2^n |

**经典用法：标志位（flags）**——一个 int 存多个开关：

```gdscript
# 定义：每个开关占一个二进制位
const FLAG_NONE := 0
const FLAG_INVINCIBLE := 1          # 二进制 0001
const FLAG_POISONED := 2            # 0010
const FLAG_SLOWED := 4              # 0100
const FLAG_STUNNED := 8             # 1000

var status := 0

# 打开开关（或上它）
status = status | FLAG_POISONED     # → 2

# 同时开多个
status = status | FLAG_STUNNED | FLAG_SLOWED   # → 14 (1110)

# 查开关（与上它，非零=开着）
print(status & FLAG_POISONED)       # 2（非0 → 中毒中）
print(status & FLAG_INVINCIBLE)     # 0（无敌没开）

# 关开关（与上"非它"）
status = status & ~FLAG_POISONED    # 关掉中毒

# 判断完整状态
if status & FLAG_STUNNED:
	skip_turn()
```

位运算的优势：一个变量装 N 个开关，存储省、比较快、`@export_flags` 注解直接支持（第 18 章）。劣势：可读性差，必须配好常量名。

## 5.9 运算符优先级总表（高→低）

```
1.  ()  括号（永远最优先）
2.  x.y  f()  x[i]  成员访问/函数调用/下标
3.  unary -  not  ~  一元运算
4.  *  /  %  乘除余
5.  +  -  加减
6.  <<  >>  位移
7.  &  按位与
8.  ^  异或
9.  |  按位或
10. <  >  <=  >=  比较
11. ==  !=  判等
12. in  is
13. and
14. or
15. 三元 if-else
16. =  +=  -=  ...  赋值（最低）
```

**实用主义建议**：这张表不用背。规则只有一条——**拿不准就加括号**。括号免费，bug 昂贵。唯一必须刻进 DNA 的：`and` 优先于 `or`，赋值永远最后。

## 5.10 字符串运算补充

```gdscript
# + 拼接（两边必须都是String）
"你好" + "世界"          # "你好世界"
"数量:" + str(5)         # "数量:5"
"数量:" + 5              # 💥 报错：String + int 非法

# * 重复
"ab" * 3                 # "ababab"
"-" * 20                 # "--------------------"（画分隔线）

# 比较：见5.3（字典序陷阱）

# % 格式化（详见第11章）
"血量 %d/%d" % [78, 100]   # "血量 78/100"
```

## 5.11 组合实战：伤害计算公式（完整例子）

把本章运算符串成一个真实系统。需求：伤害 = 攻击力 × 暴击倍率(若暴击) − 防御，最低 1 点；若目标无敌则 0；命中率判定。

```gdscript
extends Node

# ---- 可调参数 ----
const CRIT_MULTIPLIER := 2.0
const MIN_DAMAGE := 1

func calculate_damage(atk: int, def: int, crit_chance: float, target: Node) -> int:
	# ① 无敌判定（成员运算+逻辑）
	if target.is_invincible:
		return 0

	# ② 命中判定（随机+比较）
	if randf() > 0.9:                    # 10% 挥空
		return 0

	# ③ 暴击判定（随机+三元）
	var is_crit := randf() < crit_chance
	var raw := float(atk) * (CRIT_MULTIPLIER if is_crit else 1.0)

	# ④ 防御减免 + 保底（算术+max）
	var dmg := maxi(int(raw) - def, MIN_DAMAGE)

	# ⑤ 调试输出（格式化）
	print("造成 %d 伤害%s" % [dmg, "（暴击！）" if is_crit else ""])
	return dmg

func _ready():
	var d = calculate_damage(100, 30, 0.25, self)
	print("最终伤害: ", d)
```

逐块对照本章知识点：`randf() > 0.9`（比较+逻辑短路）、`if is_crit` 三元取倍率、`maxi(…, MIN_DAMAGE)` 保底、`% 格式化`嵌套三元输出。**每行都能说出用了哪个运算符，本章才算过关。**

## 5.12 练习

1. 判断输出：
```gdscript
print(9 / 2)
print(9 % 2)
print(9.0 / 2)
print(2 ** 10)
print("5" == 5)
print(not (3 > 1))
```
（答案：4、1、4.5、1024、false、false）

2. 一行代码：随机 1~100，如果小于 30 打印 "暴击" 否则打印 "普通"。
（答案：`print("暴击" if randi_range(1, 100) < 30 else "普通")`）

3. 修复 bug（两处）：
```gdscript
if player.hp = 0 and player.has_revive_item:
	player.revive()
```
（答案：`= `应为 `==`；若 player 可能为 null，需 `player != null and ...` 前置。）

4. 用位运算实现：一个 int 变量 `unlock`，表示 4 个宝箱（第0~3位）是否开过。写出"开第2个宝箱"和"查询第3个宝箱是否已开"两行。
（答案：`unlock = unlock | (1 << 2)`；`if unlock & (1 << 3): print("已开")`）

5. 不用 if，一行把 hp 限制到 0~max_hp。
（答案：`hp = clampi(hp, 0, max_hp)`）

---

# 第 6 章：流程控制——程序的岔路与循环

程序默认从上往下逐行跑（顺序结构）。本章的三类语句让程序能"拐弯"和"重复"：

```
if / elif / else     拐弯：走哪条路
match                多岔路口：一个值对应多个可能
for / while          重复：把事情做 N 遍
break / continue     循环内的紧急出口
```

## 6.1 if / elif / else：三分支入门

```gdscript
var hp := 35

if hp <= 0:
	print("死亡")
elif hp < 30:
	print("重伤！喝药！")
elif hp < 60:
	print("半血，注意走位")
else:
	print("状态良好")
```

执行流程解剖：

```
       hp <= 0 ?
      /        \
    true      false → hp < 30 ?
   (打印死亡)   /        \
             true      false → hp < 60 ?
           (重伤)      /        \
                     true      false
                   (半血)     (良好)
```

**自上而下逐条检查，命中一条就进它的分支，后面的全部跳过**。所以条件顺序是设计：

- 上例若把 `hp < 60` 放最前，hp=35 会先命中它，永远到不了"重伤"分支；
- **范围判断：从小到大（或从大到小）排**，让窄条件在前、宽条件在后。

语法细节（全是新手雷区）：

```gdscript
if hp <= 0:          # ① 条件后必须有冒号 :
	print("x")       # ② 分支代码必须缩进一级（Tab）
elif hp < 30:        # ③ elif = else if 缩写，0~n 个
	print("y")
else:                # ④ else 0~1 个，兜底
	print("z")
```

常见错误形态：

```gdscript
if hp <= 0            # ✘ 缺冒号
	print("死")

if hp <= 0:
print("死")           # ✘ 分支没缩进（print顶格了，if没有自己的身体）

if hp <= 0:
	print("死")
	print("复活")      # ✔ 两行都缩进 → 都属于if
```

## 6.2 if 的五种常用形态

**形态一：单分支（只关心真）**

```gdscript
if enemy_count == 0:
	print("关卡完成")
```

**形态二：双分支**

```gdscript
if is_night:
	spawn_ghosts()
else:
	spawn_slimes()
```

**形态三：多级范围（elif 链）**——6.1 的例子。

**形态四：嵌套（分支里再分支）**

```gdscript
if is_alive:
	if has_weapon:
		attack()
	else:
		flee()
else:
	play_death_animation()
```

**形态五：早退守卫（游戏开发最常用风格）**

把"不满足条件就先走人"放函数最前面，主逻辑不缩进：

```gdscript
func try_pickup(item) -> bool:
	if item == null:              # 守卫1：物品无效
		return false
	if not item.can_pickup:       # 守卫2：不可拾取
		return false
	if inventory.is_full():       # 守卫3：背包满
		show_msg("背包已满")
		return false

	# ---- 主逻辑：到这里说明全部前置通过 ----
	inventory.add(item)
	item.queue_free()
	return true
```

对比"不早退"写法（四层嵌套）：

```gdscript
func try_pickup(item):
	if item != null:
		if item.can_pickup:
			if not inventory.is_full():
				inventory.add(item)
				item.queue_free()
			else:
				show_msg("背包已满")
```

**守卫风格把嵌套拍平，主逻辑一目了然。这是专业代码的标志性风格。**

## 6.3 match：多路分发

一个值有很多种可能取值、每种取值对应不同处理——if/elif 链写起来啰嗦，match 专为这场景而生：

```gdscript
var state := "idle"

match state:
	"idle":
		print("站立待机")
		play_anim("idle")
	"run":
		print("奔跑")
		play_anim("run")
	"attack", "skill":            # ← 多值共享分支：逗号隔开
		print("战斗中")
	"_":
		print("未知状态:", state)   # ← _ 是默认分支（都没中时走这）
```

语法规则：

1. `match 值:` 后换行；
2. 每个分支以**模式:** 开头，缩进一级；
3. 分支内写多条语句随便；
4. **不需要 break**！一个分支执行完自动结束整个 match（跟 C 的 switch 不同，不会有穿透 bug）；
5. `_` 是万能兜底（同 else），习惯放最后。

**match 的模式匹配能力**（比 switch 强大）：

```gdscript
# 模式一：常量
match x:
	0: print("零")
	1: print("一")

# 模式二：多常量
match key:
	KEY_UP, KEY_W:
		move_up()

# 模式三：区间判断（用表达式当模式）
match hp:
	var v when v <= 0:            # when 守卫（4.x）
		die()
	var v when v < 30:
		warn_low_hp()
	_:
		normal()

# 模式四：数组结构
match command:
	["move", var x, var y]:       # 拆出元素
		move_to(x, y)
	["attack", var target_id]:
		attack(target_id)
	_:
		print("未知指令")

# 模式五：字典结构
match config:
	{"type": "heal", "amount": var n}:
		heal(n)
	{"type": "damage", "amount": var n}:
		take_damage(n)
```

**match vs if/elif 怎么选**：

| 场景 | 用什么 |
|---|---|
| 一个变量对多个**离散值** | match |
| 复杂/不同的条件表达式 | if/elif |
| 范围判断 | if/elif（或 match+when） |
| 想要"漏了哪种情况"兜底提醒 | match 的 `_` |

实战案例——游戏指令解析器：

```gdscript
func handle_command(cmd: String, args: Array) -> void:
	match cmd:
		"/heal":
			hp = max_hp
			send_msg("已回满血")
		"/give":
			if args.size() >= 2:
				give_item(args[0], int(args[1]))
			else:
				send_msg("用法: /give 物品 数量")
		"/tp":
			if args.size() >= 2:
				position = Vector2(float(args[0]), float(args[1]))
		"/help":
			send_msg("可用: /heal /give /tp")
		_:
			send_msg("未知指令: " + cmd)
```

## 6.4 for：最常用的循环

### 形态一：数字循环（Godot 特色）

```gdscript
for i in 5:
	print(i)
# 输出：
# 0
# 1
# 2
# 3
# 4
```

`for i in 5` = 循环 5 次，i 依次取 0、1、2、3、4（**从 0 开始，不含 5**）。

### 形态二：range 三件套

```gdscript
for i in range(5):           # 0 1 2 3 4        （同上）
for i in range(2, 5):        # 2 3 4            （含头不含尾）
for i in range(0, 10, 3):    # 0 3 6 9          （步长3）
for i in range(5, 0, -1):    # 5 4 3 2 1        （倒数！步长-1）
for i in range(10, 0, -2):   # 10 8 6 4 2
```

倒计时就用 range(5, 0, -1)——从 5 数到 1，"开打！"。

### 形态三：遍历数组

```gdscript
var weapons := ["剑", "弓", "杖"]

for w in weapons:             # w 依次是每个元素
	print("装备了:", w)

# 需要下标时：
for i in weapons.size():      # i = 0,1,2
	print(i, "号位:", weapons[i])

# 或同时要下标和元素：
for i in weapons.size():
	var w = weapons[i]
	print(i, w)
```

### 形态四：遍历字典

```gdscript
var stats := {"atk": 50, "def": 30, "spd": 12}

for key in stats:             # key 依次是每个键
	print(key, "=", stats[key])
# atk = 50
# def = 30
# spd = 12

for key in stats.keys():      # 显式取键数组（同上）
	...
for value in stats.values():  # 只要值
	...
```

⚠️ 字典遍历顺序：GDScript 的 Dictionary **按插入顺序**遍历（4.x 保证），不是乱序也不是排序。

### 形态五：遍历字符串

```gdscript
for ch in "abc":
	print(ch)          # a / b / c 逐字符
```

### 形态六：遍历节点孩子（引擎场景）

```gdscript
for child in get_children():        # 我的全部子节点
	print(child.name)

for node in get_tree().get_nodes_in_group("enemies"):   # 某分组的全部节点
	node.queue_free()
```

### 嵌套 for：表格、棋盘、全组合

```gdscript
# 九九乘法表
for i in range(1, 10):
	var row := ""
	for j in range(1, 10):
		row += "%d×%d=%2d " % [j, i, i * j]
	print(row)

# 网格生成（俄罗斯方块场地 10×20）
for y in 20:
	for x in 10:
		var cell := Vector2i(x, y)
		grid[cell] = 0

# 全组合（两两配对）
for i in enemies.size():
	for j in range(i + 1, enemies.size()):
		if enemies[i].distance_to(enemies[j]) < 32:
			print("发生碰撞")
```

嵌套次数 = 循环次数相乘：`20×10 = 200` 次；`100 个敌人两两配对 = 100×99/2 = 4950` 次。**嵌套循环的性能直觉要养成**（第 30 章）。

## 6.5 while：条件循环

```gdscript
var hp := 100
var turn := 0
while hp > 0:              # 条件为真就一直转
	hp -= 30
	turn += 1
	print("第", turn, "回合，剩", hp, "血")
# 输出3轮后 hp=-60 退出
```

for 与 while 的分工：

| | for | while |
|---|---|---|
| 循环次数 | **已知**（N 次/每个元素） | **未知**（看条件） |
| 典型场景 | 遍历数组、重复N次 | 等待某条件、游戏主循环、重试 |
| 死循环风险 | 几乎没有（次数有界） | **高**（条件永远真） |

**死循环警示**：

```gdscript
var i := 0
while i < 5:
	print(i)          # 💥 忘了 i += 1，i 永远是 0，游戏卡死！
```

卡死症状：编辑器无响应/游戏画面冻结。**写 while 时先写好"让条件变假的那一行"**（i += 1、hp -= 30），再填循环体。

while 的合法用途示范：

```gdscript
# 用途一：重试直到成功
var data = null
var tries := 0
while data == null and tries < 3:      # 最多试3次
	data = try_connect()
	tries += 1

# 用途二：逐层向上找父节点
var node := self
while node != null and not node is BattleScene:
	node = node.get_parent()
# 出来时 node 要么是null（到顶了没找到）要么是BattleScene

# 用途三：消耗型循环（花光资源为止）
while gold >= 100 and hp < max_hp:
	gold -= 100
	hp = mini(hp + 20, max_hp)         # 买药回血直到钱不够或血满
```

## 6.6 break 与 continue：循环的出口

```gdscript
# continue：跳过本轮剩余，直接下一轮
for i in 10:
	if i % 2 == 0:          # 偶数跳过
		continue
	print(i)                # 只打印 1 3 5 7 9

# break：直接砸开循环，不再回头
for i in 10:
	if i == 5:
		break               # 碰到5就停
	print(i)                # 0 1 2 3 4

# 实战：找第一个满足条件的（找到就走）
func find_first_dead(soldiers: Array):
	for s in soldiers:
		if s.hp <= 0:
			return s        # return 也能"砸开"循环并带值离场！
	return null             # 全找完没有
```

⚠️ break 只砸**最内层**循环：

```gdscript
for i in 3:
	for j in 3:
		if j == 1:
			break           # 只结束内层j循环，i继续
		print(i, j)
# 输出: 0 0 / 1 0 / 2 0
```

想"一次砸穿两层"？用**标志变量**或把内层抽成函数：

```gdscript
# 方案A：标志变量
var found := false
for i in 3:
	for j in 3:
		if grid[i][j] == target:
			found = true
			break
	if found:
		break

# 方案B：抽函数（更优雅）
func find_in_grid():
	for i in 3:
		for j in 3:
			if grid[i][j] == target:
				return Vector2i(i, j)   # return 砸穿一切
	return Vector2i(-1, -1)
```

## 6.7 循环经典算法模板（背下来受益终身）

**模板一：累计求和**

```gdscript
var total := 0
for n in [10, 20, 30, 40]:
	total += n                # → 100
```

**模板二：找最大/最小**

```gdscript
var nums := [7, 2, 9, 4]
var biggest := nums[0]           # 用第一个当起点
for n in nums:
	if n > biggest:
		biggest = n
print(biggest)                    # 9
# 引擎自带：nums.max() / nums.min()，但逻辑要会手写
```

**模板三：计数**

```gdscript
var count := 0
for s in soldiers:
	if s.team == 1:
		count += 1
print("敌军数量:", count)
```

**模板四：过滤（筛选出新数组）**

```gdscript
var alive := []
for s in soldiers:
	if s.hp > 0:
		alive.append(s)
# 引擎一行流：alive = soldiers.filter(func(s): return s.hp > 0)
```

**模板五：映射（每个元素变形）**

```gdscript
var names := []
for e in enemies:
	names.append(e.display_name)
# 一行流：names = enemies.map(func(e): return e.display_name)
```

**模板六：查找（返回第一个命中）**

```gdscript
var result = null
for s in shop_items:
	if s.price <= my_gold:
		result = s
		break                    # 找到就走
```

**模板七：冒泡排序（理解排序思想）**

```gdscript
var arr := [5, 2, 9, 1, 7]
for i in arr.size():
	for j in arr.size() - 1 - i:
		if arr[j] > arr[j + 1]:
			var t = arr[j]
			arr[j] = arr[j + 1]
			arr[j + 1] = t
print(arr)                        # [1, 2, 5, 7, 9]
# 实际开发直接 arr.sort()，但要懂原理
```

**模板八：反转**

```gdscript
var src := [1, 2, 3]
var rev := []
for i in range(src.size() - 1, -1, -1):    # 从最后下标倒数到0
	rev.append(src[i])
print(rev)                          # [3, 2, 1]
# 自带：src.reverse() 原地反转
```

## 6.8 循环 + 状态：一帧内的小游戏逻辑

把流程控制揉进状态管理，一个"回合制战斗"函数：

```gdscript
func auto_battle(hero: Dictionary, monster: Dictionary) -> String:
	var round := 1
	while hero.hp > 0 and monster.hp > 0:          # 谁死了停
		print("--- 第 %d 回合 ---" % round)

		# 英雄行动
		var hero_dmg := maxi(hero.atk - monster.def, 1)
		monster.hp -= hero_dmg
		print("%s 对 %s 造成 %d 伤害" % [hero.name, monster.name, hero_dmg])

		if monster.hp <= 0:                        # 怪死了提前结束本轮
			break

		# 怪物行动
		var m_dmg := maxi(monster.atk - hero.def, 1)
		hero.hp -= m_dmg
		print("%s 对 %s 造成 %d 伤害" % [monster.name, hero.name, m_dmg])

		round += 1

	# 战斗结束判定（三元+match组合）
	return "%s 获胜！" % hero.name if hero.hp > 0 else "%s 获胜！" % monster.name

# 调用
var result = auto_battle(
	{"name": "勇者", "hp": 100, "atk": 30, "def": 5},
	{"name": "史莱姆", "hp": 60, "atk": 12, "def": 2}
)
print(result)
```

这段 40 行代码用到了：while（未知回合数）、break（怪死后跳过英雄挨打）、maxi（保底伤害）、格式化输出、三元（胜负判定）。**能独立写出这个，流程控制毕业。**

## 6.9 常见错误清单

| 错误 | 现象 | 修复 |
|---|---|---|
| `if hp = 0:` | 语法错误 | `==` |
| if 后忘冒号 | Expected ":" | 补 `:` |
| 分支不缩进 | Unexpected indent 报错方向混乱 | 分支体缩进一级 |
| `for i in range(1, 5)` 以为是 1~5 | 少跑一次 | 含头不含尾：1~4 |
| while 忘记改变条件 | 游戏卡死 | 循环体里必须推进条件 |
| 循环里修改正在遍历的数组 | 跳元素/崩溃 | 遍历副本 `for x in arr.duplicate()` |
| for 循环变量当成员变量用 | 出了循环不存在 | 变量作用域（第 3 章） |
| 遍历时删除元素 | 跳过元素 | 倒序遍历或收集后统一删 |

**"遍历时删除"展开**（高频翻车）：

```gdscript
# 想删掉所有死掉的敌人 —— 错误示范：
for e in enemies:
	if e.hp <= 0:
		enemies.erase(e)         # 💥 删除导致数组移位，下一个元素被跳过

# 正确姿势一：倒序遍历（删除不影响前面的下标）
for i in range(enemies.size() - 1, -1, -1):
	if enemies[i].hp <= 0:
		enemies.remove_at(i)

# 正确姿势二：先收集，后统一删
var to_remove := enemies.filter(func(e): return e.hp <= 0)
for e in to_remove:
	enemies.erase(e)

# 正确姿势三（节点场景）：filter 留下活着的
enemies = enemies.filter(func(e): return e.hp > 0)
```

## 6.10 练习

1. 打印 1~100 所有 3 和 5 的公倍数（15 的倍数）。
```gdscript
for i in range(15, 101, 15):
	print(i)
# 或判断式：
for i in range(1, 101):
	if i % 3 == 0 and i % 5 == 0:
		print(i)
```

2. 用 while 计算 2 的多少次方首次超过 1000。
```gdscript
var p := 1
var n := 0
while p <= 1000:
	p *= 2
	n += 1
print(n)      # 10（2^10=1024）
```

3. FizzBuzz（面试名题）：1~100，3 的倍数打 Fizz，5 的倍数打 Buzz，公倍数打 FizzBuzz。
```gdscript
for i in range(1, 101):
	if i % 15 == 0:
		print("FizzBuzz")
	elif i % 3 == 0:
		print("Fizz")
	elif i % 5 == 0:
		print("Buzz")
	else:
		print(i)
```

4. 用 match 改写：
```gdscript
if cmd == "start": start_game()
elif cmd == "stop": stop_game()
elif cmd == "pause" or cmd == "freeze": pause_game()
else: print("unknown")
```
```gdscript
match cmd:
	"start": start_game()
	"stop": stop_game()
	"pause", "freeze": pause_game()
	_: print("unknown")
```

5. 读程序题：输出什么？
```gdscript
var s := 0
for i in 5:
	if i == 2:
		continue
	if i == 4:
		break
	s += i
print(s)
```
（答案：s = 0+1+3 = 4。i=2 被 continue 跳过没加；i=4 直接 break。）


# 第 7 章：函数——代码的积木与螺丝

函数是**把一段逻辑打包、起名、复用**的机制。没有函数，所有代码挤在一起像一锅粥；有了函数，代码变成乐高积木。本章从零讲到深，包括：定义、参数（默认/类型/可变参数）、返回值、lambda、递归、闭包、回调、函数式三件套（map/filter/reduce）。

## 7.1 为什么需要函数：三个理由

**理由一：复用（DRY 原则：Don't Repeat Yourself）**

```gdscript
# 没有函数：同样的逻辑抄5遍
hp_1 = hp_1 - 30 if hp_1 > 30 else 0
hp_2 = hp_2 - 30 if hp_2 > 30 else 0
hp_3 = hp_3 - 30 if hp_3 > 30 else 0
# 想改保底规则？改5处，漏一处出bug

# 有函数：逻辑写1处，到处调用
func take_damage(hp: int, dmg: int) -> int:
	return maxi(hp - dmg, 0)

hp_1 = take_damage(hp_1, 30)
hp_2 = take_damage(hp_2, 30)
hp_3 = take_damage(hp_3, 30)
```

**理由二：抽象——起个好名字，读代码不用读实现**

```gdscript
# 直接读这行，秒懂意图，不必关心内部3行怎么算的
spawn_boss("dragon", Vector2(500, 200))
```

**理由三：测试与排错的最小单元**——问题定位到某个函数，范围就缩到几行。

## 7.2 函数解剖学

```gdscript
func  calculate_damage(  atk: int,  def: int,  is_crit: bool  )  ->  int  :
 │           │             │         │          │           │      │    │
 │           │             │         │          │           │      │    └ ⑦冒号
 │           │             │         │          │           │      └ ⑥返回类型
 │           │             │         │          │           └ ⑤箭头
 │           │             │         │          └ ④参数3（bool型）
 │           │             │         └ ③参数2（int型）
 │           │             └ ②参数1（int型）
 │           └ ①函数名（动词开头）
 └ ⓪关键字
	return maxi(atk * (2 if is_crit else 1) - def, 1)     # 函数体（缩进）
```

命名铁律：**动词开头**。`get_xxx`（取）、`set_xxx`（设）、`is_xxx`/`has_xxx`/`can_xxx`（问真假）、`play_xxx`（播放）、`spawn_xxx`（生成）、`calc_xxx`（计算）、`apply_xxx`（应用）、`on_xxx`（事件响应）。

## 7.3 定义与调用

```gdscript
# 定义（此刻不会执行，只是"登记"）
func greet() -> void:
	print("你好！")

func add(a: int, b: int) -> int:
	return a + b

# 调用（此刻才执行）
greet()                    # 打印"你好！"
var sum := add(3, 5)       # sum = 8
```

**定义 ≠ 执行**：函数体在调用时才运行。理解这点，下面不奇怪：

```gdscript
func _ready():
	print("A")
	my_func()               # A之后才进入函数
	print("C")

func my_func():
	print("B")
# 输出：A → B → C（调用点"跳进去"，执行完"跳回来"）
```

## 7.4 参数：往函数里递材料

### 按位置传参（基础）

```gdscript
func introduce(name: String, level: int, job: String) -> void:
	print("我是%s，%d级%s" % [name, level, job])

introduce("勇者", 15, "战士")      # 我是勇者，15级战士
```

参数按**顺序**对应：第一个实参 → 第一个形参。顺序错了就乱：

```gdscript
introduce(15, "勇者", "战士")     # 类型不匹配，报错拦住（好处：标注了类型）
```

### 默认参数：可选材料

```gdscript
func fire_bullet(speed: float, count: int = 1, spread: float = 0.0) -> void:
	for i in count:
		var angle := (i - (count - 1) / 2.0) * spread
		print("发射子弹 速度%.0f 角度%.1f" % [speed, angle])

fire_bullet(800.0)                    # 1发，不散开
fire_bullet(800.0, 3)                 # 3发
fire_bullet(800.0, 5, 0.3)            # 5发，扇形散开
```

规则：**默认参数必须排在普通参数后面**：

```gdscript
func bad(a: int = 1, b: int): ...     # ✘ 报错：默认参数后不能有必选参数
func good(a: int, b: int = 1): ...    # ✔
```

### 按名字传参（关键字参数）

调用时指定参数名，**顺序随意、可跳过中间的默认参数**：

```gdscript
fire_bullet(600.0, spread=0.5)                       # 跳过count
fire_bullet(count=7, speed=900.0, spread=0.15)       # 顺序随意
```

引擎 API 全支持这种调用，源码里大量出现，见到别慌。

### 可变参数：...要多少给多少

`...` 前缀让一个参数吞掉所有剩余实参，打包成数组：

```gdscript
func sum_all(first: int, ...rest) -> int:
	var total := first
	for n in rest:               # rest 是 Array
		total += n
	return total

print(sum_all(1))                     # 1
print(sum_all(1, 2, 3))               # 6
print(sum_all(1, 2, 3, 4, 5))         # 15

# 实战：日志函数
func log_msg(prefix: String, ...parts) -> void:
	var line := prefix + ": "
	for p in parts:
		line += str(p) + " "
	print(line)

log_msg("战斗", "勇者", "对", "史莱姆", "造成", 25, "伤害")
# 战斗: 勇者 对 史莱姆 造成 25 伤害
```

## 7.5 返回值：函数交货

### return 的两个作用

```gdscript
func check_hp(hp: int) -> String:
	# 作用一：交货（把结果送出函数）
	if hp <= 0:
		return "死亡"          # 作用二：立刻离场（后面代码不执行）
	if hp < 30:
		return "重伤"
	return "正常"               # 函数末尾必须保证有路能return（有返回类型的）
```

**return 即终点**：执行到 return，函数当场结束，无论后面还有多少行：

```gdscript
func find_item(items: Array, uid: String):
	for item in items:
		if item.uid == uid:
			return item        # 找到立刻交货离场，不再遍历
	return null                # 遍历完没找到 → null
```

### void：不交货的函数

```gdscript
func play_sound(name: String) -> void:      # -> void 表示无返回值
	Audio.play(name)
	# 不写return，函数跑完自然结束
	# 写裸 return 也行：提前离场用
```

### 返回多个值的三种方案

GDScript 函数只能 return 一个值，但有变通：

```gdscript
# 方案一：返回数组，调用侧解构
func get_min_max(arr: Array) -> Array:
	return [arr.min(), arr.max()]
var lo, hi = get_min_max([4, 9, 1])          # lo=1, hi=9

# 方案二：返回字典（带名字，更可读）
func calc_attack(atk: int, def: int) -> Dictionary:
	return {"damage": maxi(atk - def, 1), "is_lethal": atk - def >= 100}
var r = calc_attack(120, 20)
print(r.damage, r.is_lethal)

# 方案三：返回 Vector2（正好两个数字时）
func get_dir_and_dist(a: Vector2, b: Vector2) -> Vector2:
	return Vector2(...)   # 凑合，但语义不清晰，不推荐
```

### 早期返回（Early Return）+ 守卫：专业风格

把所有"不干了"的条件堆在函数开头，主逻辑不缩进：

```gdscript
func equip_weapon(weapon) -> bool:
	# ---- 守卫区：任何一条不满足，立刻退出 ----
	if weapon == null:
		return false
	if not weapon.is_equippable:
		return false
	if level < weapon.required_level:
		show_msg("等级不足")
		return false
	if gold < weapon.price:
		show_msg("金币不足")
		return false

	# ---- 主逻辑：0 缩进，清爽 ----
	gold -= weapon.price
	current_weapon = weapon
	weapon.equipped.emit()
	return true
```

## 7.6 引用陷阱：函数参数是值还是引用

第 3 章讲过值/引用类型。传参时同样适用，这是**新手必踩的坑**：

**基础类型参数：改了也白改（值拷贝）**

```gdscript
func try_heal(hp: int) -> void:
	hp += 50                    # 改的是"复印件"

var my_hp := 100
try_heal(my_hp)
print(my_hp)                    # 100！没变！
```

想在函数里改外面的 int/float？**用返回值**：

```gdscript
func heal(hp: int, amount: int) -> int:
	return hp + amount

my_hp = heal(my_hp, 50)         # 150 ✔
```

**数组/字典/对象参数：真的会改（共享同一份）**

```gdscript
func add_item(bag: Array, item) -> void:
	bag.append(item)             # 改的是"原件"（传进来的是钥匙）

var my_bag := []
add_item(my_bag, "药水")
print(my_bag)                   # ["药水"] 真的进去了！
```

这既是坑（不小心改了调用方的数据）也是宝（想改时就利用它）：

```gdscript
# 利用引用特性：排序别人的数组（函数内sort，外面也生效）
func sort_by_price(items: Array) -> void:
	items.sort_custom(func(a, b): return a.price < b.price)

# 防御性拷贝：不想被改，就传副本
sort_by_price(my_items.duplicate())      # 内部怎么折腾，原件不动
```

**对象参数**（节点等）永远是引用：

```gdscript
func kill_target(t) -> void:
	t.queue_free()              # 真的销毁外面的那个节点

kill_target(enemy_node)          # enemy_node 被销毁（外部引用还在但对象已死！）
```

## 7.7 静态函数 static：不用实例的函数

普通函数要先有对象才能调（`enemy.attack()`——谁的attack？）。static 函数挂在**类本身**上（`MyUtils.clamp_xxx()`——工具，不需要"谁"）：

```gdscript
# math_helper.gd
class_name MathHelper

static func clamp_hp(hp: int, max_hp: int) -> int:
	return clampi(hp, 0, max_hp)

static func rand_sign() -> int:
	return 1 if randf() > 0.5 else -1
```

任何脚本里直接：

```gdscript
var h := MathHelper.clamp_hp(150, 100)      # → 100
var dir := MathHelper.rand_sign()
```

**static 函数内不能用 self / 成员变量**（它不属于任何实例）：

```gdscript
var base_speed := 100.0

static func bad() -> void:
	print(base_speed)        # ✘ 报错：静态环境访问实例成员
```

什么时候用 static：**纯函数**（只依赖参数、不依赖对象状态的工具：数学、格式化、转换）。游戏源码里的 `CommonUtils`、`StringUtils` 等工具类全是 static 设计。

## 7.8 lambda：匿名小函数

不配拥有名字的**一次性函数**，语法 `func(参数): 表达式` 或多行版：

```gdscript
# 单行lambda
var double := func(x): return x * 2
print(double.call(21))                # 42（用 .call() 执行）

# 多行lambda
var greeter := func(name):
	var msg := "你好, " + name
	print(msg)
greeter.call("勇者")
```

**lambda 的主战场是"当参数传"**——把"怎么做"递给另一个函数：

```gdscript
# 战场1：按钮点击（最常见的用法）
$Button.pressed.connect(func(): start_game())

# 战场2：数组过滤/映射
var adults = people.filter(func(p): return p.age >= 18)
var names = people.map(func(p): return p.name)

# 战场3：延时执行
get_tree().create_timer(1.0).timeout.connect(
	func(): print("1秒后执行")
)

# 战场4：Tween回调
tween.tween_callback(func(): sprite.visible = false)
```

**lambda 捕获外部变量（closure 闭包）**：

```gdscript
func make_counter() -> Callable:
	var count := 0                        # 这个变量被lambda"记住"了
	return func():
		count += 1
		return count

var counter := make_counter()
print(counter.call())     # 1
print(counter.call())     # 2
print(counter.call())     # 3  —— count 活在闭包里，跨调用保持
```

闭包陷阱——**循环变量捕获**：

```gdscript
# 意图：3个按钮，点击分别打印0/1/2
for i in 3:
	var btn := Button.new()
	btn.text = "按钮%d" % i
	btn.pressed.connect(func(): print(i))       # 💥 三个按钮都打印 3！
	# 原因：lambda 捕获的是"变量i本身"，点击时i早已变成3
	add_child(btn)

# 修复：用 bind 把当前值"冻结"进回调
for i in 3:
	var btn := Button.new()
	btn.pressed.connect((func(n): print(n)).bind(i))   # ✔ 各打印各的
	add_child(btn)
```

**bind 是"循环 + lambda"组合的标准解药**：`.bind(值)` 把值快照绑进函数，不再受变量后续变化影响。

## 7.9 递归：函数调用自己

```gdscript
# 经典：阶乘 5! = 5×4×3×2×1
func factorial(n: int) -> int:
	if n <= 1:
		return 1                        # ① 基线条件（出口！必须有）
	return n * factorial(n - 1)         # ② 递推（自己调自己，规模变小）

print(factorial(5))                     # 120
```

执行轨迹（脑内模拟）：

```
factorial(5)
= 5 * factorial(4)
= 5 * (4 * factorial(3))
= 5 * (4 * (3 * factorial(2)))
= 5 * (4 * (3 * (2 * factorial(1))))
= 5 * (4 * (3 * (2 * 1)))        ← 基线触发，开始"回程"
= 120
```

**递归两要素**：①基线（什么时候停）；②递推（问题怎么变小）。缺基线 = 无限递归 = 栈溢出崩溃。

游戏里的实用递归——**遍历树形结构**（场景树、UI树、技能树）：

```gdscript
# 统计某节点家族的全部子孙数
func count_descendants(node: Node) -> int:
	var total := 0
	for child in node.get_children():        # 树的天然结构适配递归
		total += 1 + count_descendants(child)   # 孩子自己 + 孩子的子孙
	return total

# 递归找节点
func find_node_by_name(root: Node, target: String) -> Node:
	if root.name == target:
		return root
	for child in root.get_children():
		var found = find_node_by_name(child, target)
		if found != null:
			return found
	return null

# 斐波那契（数学经典，性能反面教材——重复计算指数爆炸）
func fib(n: int) -> int:
	if n <= 1:
		return n
	return fib(n - 1) + fib(n - 2)
# fib(30) 已经过百万次调用，游戏内别用；改循环版
func fib_iter(n: int) -> int:
	var a := 0
	var b := 1
	for i in n:
		a, b = b, a + b
	return a
```

**实用建议**：游戏开发 95% 的循环用 for/while；递归留给**树/嵌套结构**。深度不可控的递归有栈溢出风险（Godot 默认递归深度有限制）。

## 7.10 函数式三件套：map / filter / reduce

把"对集合的循环操作"压缩成一行。熟练后代码量和错误率双降。

### filter：筛选

```gdscript
var nums := [1, 8, 3, 9, 2, 7]

# 只要大于5的
var big = nums.filter(func(n): return n > 5)
print(big)          # [8, 9, 7]

# 只要活的敌人
var alive = enemies.filter(func(e): return e.hp > 0)

# 排除空字符串
var valid = lines.filter(func(l): return l.strip_edges() != "")
```

### map：变形（每个元素加工）

```gdscript
var nums := [1, 2, 3, 4]

var doubled = nums.map(func(n): return n * 2)         # [2, 4, 6, 8]
var texts = nums.map(func(n): return "第%d名" % n)      # ["第1名", ...]
var areas = rects.map(func(r): return r.size.x * r.size.y)
```

### reduce：聚合（滚雪球成一个值）

```gdscript
var nums := [10, 20, 30]

# 求和（初始值0，逐个累加）
var total = nums.reduce(func(acc, n): return acc + n, 0)       # 60

# 求最大（初始值=第一个元素）
var max_v = nums.reduce(func(acc, n): return acc if acc > n else n, nums[0])

# 拼接
var words := ["hello", "world"]
var sentence = words.reduce(func(a, w): return a + " " + w, "")   # " hello world"
```

### 链式组合（威力全开）

```gdscript
# 需求：活的敌人 → 按血量排序 → 取名字 → 拼成句子
var report = enemies\
	.filter(func(e): return e.hp > 0)\
	.sort_custom(func(a, b): return a.hp < b.hp)\
	.map(func(e): return "%s(%d血)" % [e.name, e.hp])\
	.reduce(func(a, s): return a + "、", "") \
	+ " 生存中"
```

（注意：`sort_custom` 是原地排序返回 void，链式中要先 sort 再 filter，此处示意链式思想，实际写法按需拆行。）

## 7.11 方法（Method）：挂在对象上的函数

**方法 = 类里面的函数**。语法完全同函数，只是它属于某个对象，调用要点名：

```gdscript
# 定义（写在类里）
extends CharacterBody2D

var hp := 100

func take_damage(amount: int) -> void:     # 这是"方法"
	hp -= amount                           # 方法内可直接用自己的成员变量
	if hp <= 0:
		die()
```

```gdscript
# 调用（要点对象的名）
var hero = load("res://hero.tscn").instantiate()
hero.take_damage(30)          # 谁的take_damage？hero的！

# 自己内部调用自己，可以不点名
func attacked():
	take_damage(10)           # 等价 self.take_damage(10)
```

**self 关键字**：指"我自己这个对象"。多数时候可省，但**参数名与成员变量同名时必须用**：

```gdscript
var speed := 100.0

func set_speed(speed: float) -> void:     # 参数speed遮蔽了成员speed
	self.speed = speed                     # self.speed=成员，speed=参数
```

## 7.12 函数设计规范（专业分水岭）

1. **一个函数只做一件事**（单一职责）：
```gdscript
# ✘ 坏：又算伤害又扣血又播放特效又写日志
func attack(target): ...

# ✔ 好：拆开，各司其职
func calc_damage(target) -> int: ...
func apply_damage(target, dmg) -> void: ...
func play_hit_fx(target) -> void: ...
```

2. **函数不超过一屏（~30行）**：超了就问自己"是不是在做两件事"。

3. **参数别超过 4 个**：超了考虑打包成字典/对象，或拆函数。

4. **避免副作用爆炸**：纯函数（只进参数、只出返回值、不改外界）最好测最好懂。改外界（播放音效、动别的对象）的方法要命名明显（`apply_`、`spawn_`、`trigger_`）。

5. **bool 参数是设计坏味道**：
```gdscript
# ✘ 调用处看不懂true啥意思
move(true)

# ✔ 枚举/命名参数
move(MoveMode.RUN)
# 或拆成两个函数
run() / walk()
```

6. **先写调用处，再写实现**（设计驱动）：想象"这个功能我希望怎么调用它最爽"，按那个样子定义签名，再填实现。

## 7.13 综合模板：一个完整的战斗函数库

```gdscript
class_name BattleUtils
# 通用战斗公式库：全部static纯函数，任何脚本可直接调

const CRIT_MULT := 2.0
const MIN_DMG := 1

# 物理伤害：攻击-防御，保底1，可暴击
static func calc_physical(atk: int, def: int, crit: bool = false) -> int:
	var raw := float(atk) * (CRIT_MULT if crit else 1.0)
	return maxi(int(raw) - def, MIN_DMG)

# 命中判定：基础命中 - 目标闪避
static func is_hit(hit_rate: float, dodge: float) -> bool:
	return randf() < clampf(hit_rate - dodge, 0.05, 1.0)

# 暴击判定
static func is_crit(crit_chance: float) -> bool:
	return randf() < crit_chance

# 全流程一击：返回完整结算结果
static func resolve_hit(atk: int, def: int, hit_r: float, dodge: float, crit_r: float) -> Dictionary:
	if not is_hit(hit_r, dodge):
		return {"hit": false, "crit": false, "damage": 0}

	var crit := is_crit(crit_r)
	return {
		"hit": true,
		"crit": crit,
		"damage": calc_physical(atk, def, crit),
	}

# 经验分配：等级差惩罚曲线
static func exp_reward(base: int, hero_lv: int, enemy_lv: int) -> int:
	var diff := hero_lv - enemy_lv
	if diff >= 5:
		return 0                        # 碾压没经验
	return maxi(int(base * pow(0.8, diff)), 1)

# 距离判定（比物理引擎便宜的圆形碰撞）
static func in_range(a_pos: Vector2, b_pos: Vector2, radius: float) -> bool:
	return a_pos.distance_squared_to(b_pos) <= radius * radius
```

调用侧（体验设计的好处）：

```gdscript
var result = BattleUtils.resolve_hit(hero_atk, enemy_def, 0.9, 0.1, 0.25)
if result.hit:
	enemy.hp -= result.damage
	if result.crit:
		FxManager.show_crit_text(enemy.position, result.damage)
```

## 7.14 练习

1. 写函数 `is_leap_year(year: int) -> bool`：闰年=能被4整除且不被100整除，或能被400整除。
```gdscript
func is_leap_year(year: int) -> bool:
	return (year % 4 == 0 and year % 100 != 0) or year % 400 == 0
```

2. 写函数 `format_time(seconds: int) -> String`：把 3661 变 "01:01:01"。
```gdscript
func format_time(seconds: int) -> String:
	var h := seconds / 3600
	var m := (seconds % 3600) / 60
	var s := seconds % 60
	return "%02d:%02d:%02d" % [h, m, s]
```

3. 用 reduce 一行求 `[3, 5, 2, 8]` 的乘积。
```gdscript
var p = [3, 5, 2, 8].reduce(func(a, n): return a * n, 1)   # 240
```

4. 指出 bug：
```gdscript
func level_up(level: int) -> int:
	level += 1
func _ready():
	var lv := 1
	level_up(lv)
	print(lv)
```
（答案：打印1。int 是值类型，函数内改的是副本。修复：`lv = level_up(lv)`。）

5. 写递归函数 `power(base: int, exp: int) -> int`（不用 `**`）。
```gdscript
func power(base: int, exp: int) -> int:
	if exp == 0:
		return 1
	return base * power(base, exp - 1)
```

6. 用 filter+map 一行流：从 `["apple", "fig", "banana"]` 取长度≥5的词的全大写。
```gdscript
var r = ["apple", "fig", "banana"].filter(func(w): return w.length() >= 5).map(func(w): return w.to_upper())
# ["APPLE", "BANANA"]
```


# 第 8 章：数组（Array）完全教程

数组是**有序的容器**：一个名字管一串数据。游戏里"背包、敌人列表、技能栏、对话选项"全是数组。本章覆盖 Array 全部常用方法（40+个），每个配例子与陷阱。

## 8.1 创建数组的所有方式

```gdscript
# 方式一：字面量（最常用）
var empty := []
var nums := [1, 2, 3]
var mixed := [1, "文字", true, null]         # 允许混装（但混装容易埋雷）
var nested := [[1, 2], [3, 4]]                # 嵌套：数组套数组

# 方式二：Array.new()
var a := Array.new()                          # 等价 []

# 方式三：指定大小并填充
var zeros := []
zeros.resize(5)                               # [null, null, null, null, null]
var cells := []
cells.resize(10)
for i in cells.size():                        # 填默认值要自己循环
	cells[i] = 0

# 方式四：从其他数据构造
var from_str := "a,b,c".split(",")            # ["a", "b", "c"]
var from_range := range(5)                    # [0, 1, 2, 3, 4]
var from_dict := {"x": 1}.keys()              # ["x"]

# 方式五：重复填充
var repeat_arr := []
repeat_arr.resize(3)
repeat_arr.fill(9)                            # [9, 9, 9]
```

**元素与下标（index）**——第 1 个元素下标是 **0**：

```gdscript
var fruits := ["苹果", "香蕉", "橙子"]
#  下标：       0       1       2

print(fruits[0])            # 苹果
print(fruits[2])            # 橙子
print(fruits.size())        # 3
print(fruits[fruits.size() - 1])    # 橙子（最后一个元素的通用写法）
print(fruits[-1])           # 橙子（负下标=从后往前数！-1最后,-2倒数第二）
```

**负下标**是实用特性：`arr[-1]` 取末尾，不用写 `arr[arr.size()-1]`。

**越界 = 崩溃**：

```gdscript
print(fruits[3])            # 💥 Invalid get index '3'（只有0~2）
print(fruits[99])           # 💥 同上
```

安全取值姿势（处理"可能为空"的数组）：

```gdscript
if idx >= 0 and idx < arr.size():
	print(arr[idx])

# 或先判空
if not arr.is_empty():
	print(arr[0])
```

## 8.2 增：添加元素

```gdscript
var bag := ["剑"]

bag.append("盾")              # 尾部加 → ["剑", "盾"]
bag.push_back("弓")           # 同append（栈术语）
bag.push_front("头盔")        # 头部加 → ["头盔", "剑", "盾", "弓"]

bag.append_array(["药", "卷轴"])   # 一次拼接一串
# → ["头盔", "剑", "盾", "弓", "药", "卷轴"]

bag.insert(1, "护符")         # 在下标1处插入（原1及以后后移）
# → ["头盔", "护符", "剑", "盾", "弓", "药", "卷轴"]
```

**insert 的性能提示**：往头部/中部插入，后面元素全部要搬家（O(n)）。高频操作的队列结构，考虑用 `Array` 尾部操作（O(1)）或专用结构。

## 8.3 删：移除元素

```gdscript
var bag := ["剑", "盾", "弓", "药", "盾"]

bag.remove_at(0)              # 按下标删 → ["盾", "弓", "药", "盾"]
bag.erase("盾")               # 按值删（只删第一个匹配）→ ["弓", "药", "盾"]
                              # ⚠️ erase("盾")删的是第一个"盾"
bag.pop_back()                # 删末尾并【返回】它 → 返回"盾"，数组变["弓", "药"]
bag.pop_front()               # 删头部并【返回】它 → 返回"弓"，数组变["药"]
bag.clear()                   # 清空 → []
```

**remove_at vs erase**：

| 方法 | 参数 | 没找到时 |
|---|---|---|
| `remove_at(i)` | **下标** | 越界→崩溃 |
| `erase(v)` | **值** | 静默无事 |

新手常混："想删第2个"用 remove_at(1)（下标！）；"想删'弓'"用 erase("弓")。

**遍历时删除的坑**（第 6 章讲过原则，这里给数组完整解法）：

```gdscript
# 需求：删除所有"药"
var items := ["剑", "药", "弓", "药", "药"]

# ✘ 错误：边遍历边erase，删除引起移位，相邻元素被跳过
for item in items:
	if item == "药":
		items.erase(item)

# ✔ 正确一：倒序遍历删除（删除不影响已遍历过的下标）
for i in range(items.size() - 1, -1, -1):
	if items[i] == "药":
		items.remove_at(i)

# ✔ 正确二：filter 一行流（推荐！）
items = items.filter(func(x): return x != "药")
```

## 8.4 查：搜索与判断

```gdscript
var nums := [10, 20, 30, 20]

nums.has(20)                  # true   是否包含
nums.count(20)                # 2      出现次数
nums.find(20)                 # 1      第一个匹配的下标（没有→-1）
nums.find(20, 2)              # 3      从下标2起找
nums.rfind(20)                # 3      从后往前找
nums.min()                    # 10     最小值
nums.max()                    # 30     最大值

# 自定义查找（对象/字典）
var enemies := [{"name": "史莱姆", "hp": 20}, {"name": "蝙蝠", "hp": 15}]
var idx := enemies.find_custom(func(e): return e.hp < 18)
# → 1（第一个hp<18的下标）

# 判空
nums.is_empty()               # false
```

**find 返回 -1 的经典处理**：

```gdscript
var i := inventory.find("钥匙")
if i != -1:                   # 找到了
	print("钥匙在第", i, "格")
	inventory.remove_at(i)     # 顺便用掉它
else:
	print("没有钥匙")
```

## 8.5 改：排序与乱序

```gdscript
var nums := [3, 1, 4, 1, 5, 9, 2, 6]

nums.sort()                   # 升序原地排 → [1, 1, 2, 3, 4, 5, 6, 9]
nums.reverse()                # 原地翻转
nums.shuffle()                # 随机打乱（洗牌）

var sorted = nums.duplicate().sort()  # ⚠️ 错误示范！sort返回void
# 想"排副本不动原件"：
var copy = nums.duplicate()
copy.sort()                   # ✔ 两步

# 自定义排序：sort_custom（递给一个"比较函数"）
var players := [
	{"name": "A", "score": 80},
	{"name": "B", "score": 95},
	{"name": "C", "score": 60},
]
# 按分数从高到低：
players.sort_custom(func(a, b): return a.score > b.score)
# B(95), A(80), C(60)
# 规则：比较函数返回 true 表示"a 应排在 b 前面"

# 多级排序：先按分数降序，同分按名字升序
players.sort_custom(func(a, b):
	if a.score != b.score:
		return a.score > b.score
	return a.name < b.name
)
```

**排序稳定性**：sort_custom 是稳定排序（相等元素保持原相对顺序）。对"同分保持先来后到"的需求天然友好。

**乱序的正确姿势**：shuffle() 是均匀洗牌。别用"随机交换两次"之类的自制算法（分布不均）。

**排序对象数组的模板**（背下来）：

```gdscript
# 按数值字段降序
items.sort_custom(func(a, b): return a.price > b.price)
# 按数值字段升序
items.sort_custom(func(a, b): return a.price < b.price)
# 按字符串字段升序
items.sort_custom(func(a, b): return a.name < b.name)
# 按距离升序（离某点近的在前）
var me := global_position
enemies.sort_custom(func(a, b):
	return a.global_position.distance_squared_to(me) \
		< b.global_position.distance_squared_to(me)
)
```

## 8.6 切片与拼接

```gdscript
var nums := [0, 1, 2, 3, 4, 5]

nums.slice(1, 4)              # [1, 2, 3]   下标1~3（含头不含尾）
nums.slice(2)                 # [2, 3, 4, 5] 从2到末尾
nums.slice(0, -2)             # [0, 1, 2, 3] 去掉最后两个
nums.slice(-2)                # [4, 5]       最后两个
nums.slice(0, 6, 2)           # [0, 2, 4]    步长2

# 数组合并
var a := [1, 2]
var b := [3, 4]
a.append_array(b)             # a → [1, 2, 3, 4]（b不变）
var c := a + b                # 新数组 = [1,2,3,4] + [3,4] → [1,2,3,4,3,4]

# 转字符串
print(nums)                   # [0, 1, 2, 3, 4, 5]
",".join(["a", "b", "c"])     # "a,b,c"（字符串方法，把数组连成串）
```

**slice 不修改原数组**（返回新数组）；sort/reverse/shuffle 是**原地修改**。这个区别记牢。

## 8.7 数组的高级操作

### any / all：存在性判断

```gdscript
var scores := [60, 45, 80, 30]

scores.any(func(s): return s >= 80)    # true  有任何一个≥80？
scores.all(func(s): return s >= 60)    # false 全部≥60？（45和30拖后腿）

# 实战：全员死亡判定
var game_over := soldiers.all(func(s): return s.hp <= 0)
# 有敌人进入警报范围
var alert := enemies.any(func(e): return e.distance_to(player) < 100)
```

### filter / map / reduce（第 7 章讲过，数组视角复习）

```gdscript
var inventory := [
	{"name": "剑", "type": "weapon", "price": 100},
	{"name": "苹果", "type": "food", "price": 5},
	{"name": "弓", "type": "weapon", "price": 80},
]

# 找出所有武器
var weapons = inventory.filter(func(i): return i.type == "weapon")
# 全部打折30%
var discounted = inventory.map(func(i):
	return {"name": i.name, "type": i.type, "price": int(i.price * 0.7)}
)
# 背包总价值
var total = inventory.reduce(func(acc, i): return acc + i.price, 0)   # 185
```

## 8.8 二维数组：表格与网格

数组元素可以是数组 → 二维表（棋盘、地图、背包格）：

```gdscript
# 创建 3行×4列 的棋盘（全0）
var grid: Array = []
for y in 3:
	var row := []
	row.resize(4)
	row.fill(0)
	grid.append(row)
# grid = [[0,0,0,0], [0,0,0,0], [0,0,0,0]]

# 读写：grid[行][列]
grid[1][2] = 5                     # 第2行第3列放5
print(grid[1][2])                  # 5

# 遍历（y=行号, x=列号）
for y in grid.size():
	for x in grid[y].size():
		if grid[y][x] == 5:
			print("找到5在", y, "行", x, "列")
```

**二维数组的引用陷阱**：

```gdscript
# ✘ 经典错误：想造5行全0，结果5行是【同一行】
var bad: Array = []
var row := [0, 0, 0]
for i in 5:
	bad.append(row)              # 5次append的是同一个row的引用！
bad[0][0] = 9
print(bad[3][0])                  # 9 💥 全部一起变了！

# ✔ 正确：每行新建
var good: Array = []
for i in 5:
	good.append([0, 0, 0])        # 每次都造新数组
```

**俄罗斯方块/三消类游戏的地形表示**（实战模板）：

```gdscript
const W := 10
const H := 20
var board: Array = []              # board[y][x]: 0空 1~7方块色

func _ready() -> void:
	for y in H:
		var row := []
		row.resize(W)
		row.fill(0)
		board.append(row)

# 消除满行（三消/俄罗斯方块核心）
func clear_full_rows() -> int:
	var cleared := 0
	for y in range(board.size() - 1, -1, -1):        # 倒序！删行不影响上方下标
		if board[y].all(func(cell): return cell != 0): # 整行非0=满
			board.remove_at(y)                         # 删掉这行
			var new_row := []
			new_row.resize(W)
			new_row.fill(0)
			board.push_front(new_row)                   # 顶上补空行
			cleared += 1
	return cleared

# 落子判定
func can_place(shape: Array, at: Vector2i) -> bool:
	for sy in shape.size():
		for sx in shape[sy].size():
			if shape[sy][sx] == 0:
				continue
			var gx := at.x + sx
			var gy := at.y + sy
			if gx < 0 or gx >= W or gy < 0 or gy >= H:
				return false                      # 出界
			if board[gy][gx] != 0:
				return false                      # 已占用
	return true
```

## 8.9 数组当栈/队列用

```gdscript
# 栈（Stack）：后进先出 LIFO —— 弹夹、撤销操作、返回上一菜单
var stack: Array = []
stack.push_back("主菜单")          # 进栈
stack.push_back("设置页")          # 进栈
stack.push_back("音量页")          # 进栈
var current = stack.pop_back()     # 出栈→"音量页"（最后进的先出）
# 实战：返回键 = pop当前页，再pop出上一页显示

# 队列（Queue）：先进先出 FIFO —— 排队、消息、回合顺序
var queue: Array = []
queue.push_back("玩家A")           # 排队
queue.push_back("玩家B")
var next = queue.pop_front()       # →"玩家A"（先来的先走）
```

| 结构 | 进 | 出 | 用途 |
|---|---|---|---|
| 栈 | push_back | pop_back | 撤销、菜单返回、深度搜索 |
| 队列 | push_back | pop_front | 排队、消息、广度搜索 |

⚠️ pop_front 是 O(n)（全员前移）。**高频大队列**用引擎专用类型（第 10 章）。

## 8.10 数组与类型

### 类型化数组（4.x 推荐）

```gdscript
var scores: Array[int] = [1, 2, 3]
scores.append(4)                # ✔
scores.append("四")             # ✘ 编辑器报错：类型不符

var enemies: Array[Node2D] = []
var points: Array[Vector2] = [Vector2.ZERO]

# 好处：①装错当场报错 ②取出来自动补全类型 ③性能略优
```

### 数组内容的类型混装风险

```gdscript
var chaos := [1, "a", true]
var x = chaos[0] + 1            # 哪行报错？运行时才知道chaos[0]是int才能加
```

混装不是非法，但**取出来用之前必须心里有数**。数据来自 JSON/文件时尤其注意（第 28 章）。

## 8.11 数组性能意识（先立观念，细节第 30 章）

| 操作 | 复杂度 | 说明 |
|---|---|---|
| `arr[i]` 读/写 | O(1) | 飞快 |
| append / pop_back | O(1) | 飞快 |
| push_front / pop_front / insert / remove_at | O(n) | 搬家，慢 |
| find / has / erase(值) | O(n) | 逐个找，慢 |
| sort | O(n log n) | 还行 |

**大数组的粗略直觉**：1000 元素的 find 每帧跑一次毫无压力；100 万元素就要换思路（字典/分块/缓存）。

## 8.12 实战模板集

**模板一：背包系统**

```gdscript
var inventory: Array = []          # 每格: {"uid": "potion", "count": 3}

func add_item(uid: String, count: int = 1) -> void:
	# 先找同款（可叠加）
	for slot in inventory:
		if slot.uid == uid:
			slot.count += count
			return
	# 没同款，新开一格
	inventory.append({"uid": uid, "count": count})

func remove_item(uid: String, count: int = 1) -> bool:
	for i in inventory.size():
		if inventory[i].uid == uid:
			if inventory[i].count < count:
				return false                      # 不够扣
			inventory[i].count -= count
			if inventory[i].count == 0:
				inventory.remove_at(i)             # 扣光删格
			return true
	return false                                  # 没这东西

func has_item(uid: String, count: int = 1) -> bool:
	return inventory.any(func(s): return s.uid == uid and s.count >= count)
```

**模板二：最近目标查找（AI 核心）**

```gdscript
func find_nearest_target(from_pos: Vector2, targets: Array) -> Node2D:
	var nearest: Node2D = null
	var nearest_d := INF                             # 无穷大当起点
	for t in targets:
		if t == null or not is_instance_valid(t):
			continue                                  # 死了/无效跳过
		var d := from_pos.distance_squared_to(t.global_position)  # 平方省开方
		if d < nearest_d:
			nearest_d = d
			nearest = t
	return nearest
```

**模板三：波次生成器**

```gdscript
var waves := [
	{"count": 3, "type": "slime", "interval": 1.0},
	{"count": 5, "type": "bat",   "interval": 0.8},
	{"count": 8, "type": "goblin","interval": 0.5},
]
var wave_idx := 0

func start_wave() -> void:
	if wave_idx >= waves.size():
		print("全部波次结束")
		return
	var w = waves[wave_idx]
	for i in w.count:
		await get_tree().create_timer(w.interval * i).timeout   # 间隔生成
		spawn_enemy(w.type)
	wave_idx += 1
```

**模板四：洗牌发牌**

```gdscript
var deck := ["A♠", "2♠", "K♥", "Q♦"]
deck.shuffle()                       # 洗
var hand := []
for i in 2:
	hand.append(deck.pop_back())     # 发两张（从牌堆顶）
print(hand, "牌堆剩", deck.size())
```

**模板五：历史记录/滚动日志**

```gdscript
var log_lines: Array[String] = []
const MAX_LOG := 5

func push_log(line: String) -> void:
	log_lines.append(line)
	if log_lines.size() > MAX_LOG:
		log_lines.pop_front()            # 超长删最旧
	refresh_ui()
```

## 8.13 常见错误清单

| 错误 | 现象 | 修复 |
|---|---|---|
| `arr[3]`（长度3） | Invalid get index 崩溃 | 下标0~size-1；先判size |
| 边遍历边 erase | 跳元素 | 倒序/filter |
| `var sorted = arr.sort()` | sorted 是 null！ | sort 原地排序返回 void |
| append 了"引用"想复制 | 改一处全变 | `.duplicate()` |
| 二维数组 append 同一 row | 行联动 | 每行新建 `[]` |
| erase 以为删下标 | 实际按值删 | 下标用 remove_at(i) |
| find 没找到当 0 用 | 元素0/空串误命中 | 先判 `!= -1` |
| 空数组取 min/max | null | 先判 is_empty |

## 8.14 练习

1. 不看文档实现：统计数组 `[3,7,3,2,7,7,1]` 中 7 出现的次数（两种方法：循环累加 / count()）。
```gdscript
# 法1
var c := 0
for n in arr:
	if n == 7: c += 1
# 法2
var c2 := arr.count(7)
```

2. 一行流：`[1,2,3,4,5,6]` 取偶数的平方。
```gdscript
var r = [1,2,3,4,5,6].filter(func(n): return n % 2 == 0).map(func(n): return n * n)
# [4, 16, 36]
```

3. 实现 `second_largest(arr)` 返回第二大值（不排序原数组）。
```gdscript
func second_largest(arr: Array) -> int:
	var copy = arr.duplicate()
	copy.sort()
	return copy[copy.size() - 2]
```

4. 数组 A=[1,2,3]、B=[2,3,4]，求交集、并集。
```gdscript
var a := [1,2,3]
var b := [2,3,4]
var inter = a.filter(func(x): return x in b)        # [2,3]
var union = a.duplicate()
for x in b:
	if not x in union:
		union.append(x)                              # [1,2,3,4]
```

5. 读程序：输出什么？
```gdscript
var s := []
s.append(1)
s.append(2)
s.push_front(0)
s.pop_back()
s.insert(1, 9)
print(s)
```
（答案：[0, 9, 1]。逐步：[1]→[1,2]→[0,1,2]→[0,1]→[0,9,1]）


# 第 9 章：字典（Dictionary）完全教程

数组靠"第几个"找数据，字典靠"**名字（键）**"找数据。游戏配置表、角色属性、物品数据、存档结构全是字典。掌握字典 = 掌握游戏数据的世界语。

## 9.1 创建字典

```gdscript
# 方式一：字面量（最常用）
var empty := {}
var hero := {
	"name": "勇者",
	"level": 10,
	"hp": 100,
	"is_alive": true,
}

# 方式二：键不加引号的简写（仅当键是合法标识符）
var hero2 := {
	name = "勇者",              # 等价 "name": "勇者"
	level = 10,
	hp = 100,
}

# 方式三：Dictionary.new()
var d := Dictionary.new()
```

两种键写法完全等价，**团队里统一一种**即可（引擎源码多用带引号版）。

**键值对**：`"name"` 是键（key），`"勇者"` 是值（value）。键是"查询用的名字"，值是"查到的内容"。

## 9.2 读写：四种姿势

```gdscript
var hero := {"name": "勇者", "hp": 100}

# 姿势一：方括号（基础）
print(hero["name"])             # 勇者
hero["hp"] = 80                 # 改
hero["mp"] = 50                 # 键不存在？→ 直接创建！
print(hero)                     # {name:勇者, hp:80, mp:50}

# 姿势二：点语法（键是合法标识符时）
print(hero.name)                # 勇者（等价 hero["name"]）
hero.hp = 60
hero.stamina = 100              # 也能创建新键

# 姿势三：get（安全！不存在不崩，给默认值）
print(hero.get("attack", 0))    # 0（没有attack键，返回默认值）
print(hero.get("hp", 0))        # 60（有，返回真值）

# 姿势四：方括号读不存在的键 → 💥 崩溃！
print(hero["attack"])           # Invalid get index 'attack'
```

**姿势三 get 是字典世界的安全带**。什么时候用哪个：

| 场景 | 姿势 |
|---|---|
| 键 100% 存在（自己刚写的字面量） | `[键]` 或 `.` 随意 |
| 键可能不存在（外部数据/JSON/玩家输入） | **必须 get(键, 默认值)** |
| 想知道键在不在再决定动作 | `has(键)` |

```gdscript
# 外部数据处理的黄金姿势
var config := {"volume": 0.8, "fullscreen": true}
var music_vol := config.get("volume", 0.5)          # 没有→0.5兜底
var lang := config.get("language", "zh")             # 没有→中文兜底
```

## 9.3 键的类型：什么都能当键

```gdscript
var d := {}

d["字符串键"] = 1                # String 键（99%的场景）
d[42] = 2                       # int 键
d[Vector2i(3, 5)] = "草地"       # Vector2i 键（网格/瓦片地图神器！）
d[true] = 3                     # bool 键（基本没用）
d[Vector2(1.5, 2.5)] = 4        # ⚠️ float向量当键有精度风险，不推荐
```

**Vector2i 当键 = 网格游戏的正确姿势**：

```gdscript
var tiles := {}
tiles[Vector2i(0, 0)] = "草地"
tiles[Vector2i(1, 0)] = "石头"
tiles[Vector2i(1, 1)] = "水"

# 查询任意格子
func tile_at(x: int, y: int) -> String:
	return tiles.get(Vector2i(x, y), "虚空")
```

⚠️ **数组不能当键**（引用类型，每次比较都是新地址）。嵌套结构要"数组键"时，转成字符串：`d[str([1,2])]`（不优雅但偶尔救命）。

## 9.4 删除与清空

```gdscript
var bag := {"药水": 3, "卷轴": 1, "金币": 99}

bag.erase("卷轴")               # 删除指定键（不存在也没事）
bag.clear()                     # 清空 → {}

# erase 不存在 vs 方括号读不存在：
bag.erase("不存在")             # ✔ 静默成功（没东西可删而已）
var x = bag["不存在"]           # 💥 崩溃
```

## 9.5 查询：has / keys / values / size

```gdscript
var hero := {"name": "勇者", "hp": 100, "mp": 30}

hero.has("hp")                  # true   有这个键吗
hero.has("attack")              # false
"mp" in hero                    # true   in 等价 has（更顺手）

hero.keys()                     # ["name", "hp", "mp"]   全部键（数组）
hero.values()                   # ["勇者", 100, 30]       全部值
hero.size()                     # 3                      键值对数量
hero.is_empty()                 # false
```

**has 的典型用法**——"有则改，无则建"：

```gdscript
# 统计词频（经典算法）
var counts := {}
for word in ["苹果", "香蕉", "苹果", "苹果", "香蕉"]:
	if counts.has(word):
		counts[word] += 1        # 见过：+1
	else:
		counts[word] = 1         # 没见过：建档
print(counts)                    # {苹果:3, 香蕉:2}

# 更简洁的等价写法（get默认值）
for word in words:
	counts[word] = counts.get(word, 0) + 1
```

## 9.6 遍历字典

```gdscript
var stats := {"atk": 50, "def": 30, "spd": 12}

# 方式一：遍历键（最常用）
for key in stats:
	print(key, " = ", stats[key])
# atk = 50 / def = 30 / spd = 12
# （4.x 保证按插入顺序遍历）

# 方式二：只要键
for k in stats.keys(): ...

# 方式三：只要值
for v in stats.values():
	print(v)                    # 50 / 30 / 12

# 方式四：键值同时要
for k in stats:
	var v = stats[k]
	...
```

**遍历时删除的坑**（同数组）：

```gdscript
# ✘ 遍历时erase → 部分元素被跳过
for k in stats:
	if stats[k] < 20:
		stats.erase(k)

# ✔ 先收集要删的键，遍历完统一删
var to_delete := stats.keys().filter(func(k): return stats[k] < 20)
for k in to_delete:
	stats.erase(k)
```

## 9.7 嵌套字典：游戏数据的真实形状

字典的值可以是任何东西——**包括另一个字典或数组**。真实游戏数据都是套娃结构：

```gdscript
# 武器数据表（大字典：uid → 属性字典）
const WEAPONS := {
	"sword_001": {
		"name": "铁剑",
		"atk": 20,
		"price": 100,
		"type": "sword",
	},
	"bow_001": {
		"name": "短弓",
		"atk": 15,
		"price": 120,
		"type": "bow",
	},
}

# 玩家存档（字典套数组套字典）
const SAVE_TEMPLATE := {
	"player": {
		"name": "勇者",
		"level": 1,
		"pos": {"x": 100.0, "y": 200.0},
	},
	"inventory": [
		{"uid": "potion_hp", "count": 3},
		{"uid": "sword_001", "count": 1},
	],
	"quests_done": ["q_intro", "q_first_blood"],
	"playtime": 3600.0,
}
```

**读嵌套 = 层层方括号**：

```gdscript
print(WEAPONS["sword_001"]["name"])        # 铁剑
print(WEAPONS["bow_001"]["atk"])           # 15

var save = SAVE_TEMPLATE.duplicate(true)
print(save["player"]["pos"]["x"])          # 100.0
print(save["inventory"][0]["uid"])         # potion_hp
#                          ↑数组下标 ↑字典键 ↑再一层键
```

**改嵌套 = 同样层层**：

```gdscript
save["player"]["level"] = 2                 # 改层级值
save["inventory"][0]["count"] -= 1          # 用掉一瓶药
save["quests_done"].append("q_tutorial")    # 数组方法照用
```

**安全读嵌套 = get 层层兜底**：

```gdscript
# ✘ 危险：任何一层缺失都崩
var x = save["player2"]["pos"]["x"]         # 💥 没有player2键

# ✔ get 链式兜底（每层都给默认{}）
var x2 = save.get("player2", {}).get("pos", {}).get("x", 0.0)     # 0.0

# ✔ 或先判
if save.has("player2") and save["player2"].has("pos"):
	var x3 = save["player2"]["pos"]["x"]
```

**get 链式兜底是处理 JSON/存档/网络数据的肌肉记忆**，源码里到处都是。

## 9.8 字典的合并与比较

```gdscript
var a := {"hp": 100, "mp": 50}
var b := {"mp": 60, "atk": 30}

# 合并（merge）：b的内容覆盖进a
a.merge(b, true)                # 第二参数true=覆盖同名键
# a → {"hp":100, "mp":60, "atk":30}
# a.merge(b, false) 则保留a原值：mp仍是50

# 比较相等：键值全等才相等（不分顺序）
var c := {"hp": 100, "mp": 50}
print(a == c)                    # true（== 深度比较，与数组不同对象比较不同！）
```

**merge 实战**——配置分层（默认配置 + 用户配置覆盖）：

```gdscript
const DEFAULT_SETTINGS := {
	"volume_master": 1.0,
	"volume_music": 0.8,
	"language": "zh",
	"fullscreen": false,
}

func load_settings() -> Dictionary:
	var settings = DEFAULT_SETTINGS.duplicate()      # 从默认开始
	var user := read_user_settings()                  # 用户存过的
	settings.merge(user, true)                        # 用户的覆盖默认
	return settings
# 效果：老版本新增的设置项自动有默认值，用户的个性化全保留
```

## 9.9 深拷贝与引用陷阱

字典是引用类型（第 3 章）：

```gdscript
var a := {"hp": 100}
var b := a                      # 共享同一份！
b["hp"] = 50
print(a["hp"])                   # 50 💥 a也被改了

# 真拷贝
var c = a.duplicate()            # 浅拷贝：顶层新造，嵌套的子字典/数组仍共享
var d = a.duplicate(true)        # 深拷贝：连子层全部新造
```

**浅拷贝 vs 深拷贝**：

```gdscript
var save := {
	"hp": 100,
	"bag": ["药", "剑"],          # 值是数组（引用类型）
}

var shallow = save.duplicate()    # 浅
shallow["bag"].append("弓")       # 改的是共享的数组
print(save["bag"])                # [药, 剑, 弓] 💥 原档也被塞进弓了

var deep = save.duplicate(true)   # 深
deep["bag"].append("盾")
print(save["bag"])                # [药, 剑] ✔ 原档安全
```

**存档、模板、配置的复制一律 `duplicate(true)`**。

## 9.10 字典 vs 数组：选型指南

| 需求 | 用什么 |
|---|---|
| 有序列表、顺序重要（队伍顺序、对话序列） | 数组 |
| 按名字查（uid→数据、键位→功能） | 字典 |
| 需要快速判断"存在与否"（缓存、去过的地方） | 字典（has 是 O(1)） |
| 会频繁按下标增删尾部 | 数组 |
| 表示"一个东西的各项属性"（一把武器/一个存档） | 字典 |
| 表示"很多同类东西的集合" | 数组（元素常是字典） |

**组合拳**（真实世界）：

```gdscript
# 数组+字典：所有敌人的列表
var enemies := [
	{"name": "史莱姆", "hp": 20, "pos": Vector2(100, 200)},
	{"name": "蝙蝠",   "hp": 15, "pos": Vector2(300, 150)},
]
# 字典+数组：按类型归类的敌人
var enemies_by_type := {
	"slime": [slime1, slime2],
	"bat":   [bat1],
}
# 字典+字典：uid → 完整数据
var weapon_db := {"sword_001": {...}, "bow_001": {...}}
```

## 9.11 实战模板集

**模板一：数据驱动设计（游戏配置表的标准形）**

```gdscript
class_name EnemyDB
# 所有敌人的数据表：策划改这里，程序不用动

const ENEMIES := {
	"slime": {
		"name": "史莱姆",
		"hp": 20, "atk": 5, "def": 0,
		"speed": 40.0,
		"exp": 10, "gold": 5,
		"color": Color(0.3, 0.9, 0.4),
	},
	"bat": {
		"name": "蝙蝠",
		"hp": 12, "atk": 8, "def": 0,
		"speed": 90.0,
		"exp": 15, "gold": 8,
		"color": Color(0.5, 0.3, 0.7),
	},
}

static func get_enemy(uid: String) -> Dictionary:
	return ENEMIES.get(uid, {})

static func get_stat(uid: String, stat: String, default_val = null):
	return ENEMIES.get(uid, {}).get(stat, default_val)

static func all_uids() -> Array:
	return ENEMIES.keys()
```

**模板二：键位映射（输入配置）**

```gdscript
var keybinds := {
	"up":    KEY_W,
	"down":  KEY_S,
	"left":  KEY_A,
	"right": KEY_D,
}

func get_action(key: Key) -> String:
	for action in keybinds:
		if keybinds[action] == key:
			return action
	return "none"
```

**模板三：冷却管理器（技能CD）**

```gdscript
var cooldowns := {}                     # 技能名 → 剩余秒数

func try_use_skill(skill: String, cd: float) -> bool:
	if cooldowns.get(skill, 0.0) > 0.0:
		return false                     # 还在冷却
	cooldowns[skill] = cd                # 重置CD
	return true

func tick(delta: float) -> void:        # 每帧调用
	for skill in cooldowns:
		cooldowns[skill] = maxf(cooldowns[skill] - delta, 0.0)
```

**模板四：缓存（加载过的资源不再加载）**

```gdscript
var _cache := {}                        # 路径 → 已加载的Texture

func get_texture(path: String) -> Texture2D:
	if _cache.has(path):
		return _cache[path]              # 缓存命中，直接给
	var tex = load(path)
	if tex != null:
		_cache[path] = tex               # 存入缓存
	return tex
```

**模板五：状态机状态表（行为驱动）**

```gdscript
# 把"每种状态干什么"全写进字典（数据驱动AI的雏形）
var states := {
	"idle": {
		"anim": "idle",
		"next": ["patrol", "chase"],
		"duration": 2.0,
	},
	"patrol": {
		"anim": "walk",
		"next": ["idle", "chase"],
		"duration": 5.0,
	},
	"chase": {
		"anim": "run",
		"next": ["attack"],
		"duration": 0.0,
	},
}

func enter_state(name: String) -> void:
	var s = states.get(name)
	if s == null:
		return
	play_anim(s.anim)
	if s.duration > 0.0:
		await get_tree().create_timer(s.duration).timeout
		var next = s.next.pick_random()
		enter_state(next)
```

**模板六：多语言文本表**

```gdscript
const TEXTS := {
	"zh": {
		"start": "开始游戏",
		"quit": "退出",
		"hello": "你好，%s！",
	},
	"en": {
		"start": "Start Game",
		"quit": "Quit",
		"hello": "Hello, %s!",
	},
}
var lang := "zh"

func tr_text(key: String, ...args) -> String:
	var s = TEXTS.get(lang, {}).get(key, key)      # 找不到就显示键名（好排错）
	return s % args if args.size() > 0 else s

tr_text("hello", "勇者")      # 你好，勇者！
```

## 9.12 常见错误清单

| 错误 | 现象 | 修复 |
|---|---|---|
| `d["不存在"]` 读 | 崩溃 Invalid get index | 用 `d.get(键, 默认值)` |
| 键名打错（"Hp" vs "hp"） | 永远取不到/意外新建 | 键名全小写统一习惯；用常量当键 |
| 混用 `.hp` 和 `["hp"]` 写新键 | 都行，但"点语法"不能用于非法标识符键（"hp-1"） | 复杂键一律方括号 |
| 直接 `=` 给外部字典想复制 | 引用共享，改了原件 | `.duplicate(true)` |
| 遍历时 erase | 跳键 | 先收集 keys 再删 |
| 值是数组被"顺便"改了 | 浅拷贝坑 | deep duplicate |
| 拿 float/Vector2 当键 | 精度不一致查不到 | 用 int/Vector2i/String 当键 |

## 9.13 练习

1. 建学生字典 `{"name": "小明", "scores": [90, 85, 78]}`，求平均分。
```gdscript
var stu := {"name": "小明", "scores": [90, 85, 78]}
var avg = stu["scores"].reduce(func(a, s): return a + s, 0) / float(stu["scores"].size())
```

2. 两字典相加（键相同值相加，不同则保留）：`{"a":1,"b":2}` + `{"b":3,"c":4}` → `{"a":1,"b":5,"c":4}`。
```gdscript
func merge_add(d1: Dictionary, d2: Dictionary) -> Dictionary:
	var r = d1.duplicate()
	for k in d2:
		r[k] = r.get(k, 0) + d2[k]
	return r
```

3. 数组转字典：`["apple", "banana", "apple"]` → `{"apple": 2, "banana": 1}`。
```gdscript
func count_words(arr: Array) -> Dictionary:
	var d := {}
	for w in arr:
		d[w] = d.get(w, 0) + 1
	return d
```

4. 从嵌套字典 `save["player"]["bag"]["gold"]` 安全取金币（可能缺任何一层），默认 0。
```gdscript
var gold = save.get("player", {}).get("bag", {}).get("gold", 0)
```

5. 读程序：输出什么？
```gdscript
var d := {"x": 1}
d["y"] = d.get("x", 0) + d.get("z", 10)
d.erase("x")
print(d, d.size())
```
（答案：{y: 11} 1。y = 1 + 10 = 11；删除x后只剩y。）

---

# 第 10 章：类型化数组与 Packed 系列性能专题

## 10.1 类型化数组 Array[T]（4.x 重要特性）

给数组声明"只能装某种类型"：

```gdscript
var scores: Array[int] = [1, 2, 3]
var names: Array[String] = ["a", "b"]
var enemies: Array[Node2D] = []
var points: Array[Vector2] = [Vector2.ZERO, Vector2.ONE]
var tables: Array[Dictionary] = []          # 字典数组（游戏数据表常用）
```

**三大好处**：

```gdscript
# ①装错当场报错（而不是留到运行时炸）
var hp_list: Array[int] = []
hp_list.append(100)          # ✔
hp_list.append("一百")        # ✘ 编辑器红线 + 运行报错

# ②取出来类型确定，自动补全可用
var first: int = hp_list[0]
print(first + 1)              # 编辑器知道first是int

# ③性能：内存连续、省类型检查
```

**注意**：类型化数组间的赋值兼容性：

```gdscript
var typed: Array[int] = [1, 2]
var untyped: Array = typed            # ✔ 类型化→非类型化 OK
var back: Array[int] = untyped        # ✘ 非类型化→类型化 直接赋不行
var back2: Array[int] = untyped.duplicate()   # 复制后可以（逐元素验证）
```

## 10.2 Packed 系列：引擎的高性能数组

普通 Array 万物皆可装（灵活但每元素带类型信息开销）。Packed 系列是**单一类型的紧凑数组**，内存省、批量读写快：

| 类型 | 装什么 |
|---|---|
| `PackedInt32Array` / `PackedInt64Array` | 整数 |
| `PackedFloat32Array` / `PackedFloat64Array` | 小数 |
| `PackedStringArray` | 字符串 |
| `PackedVector2Array` | Vector2（路径点、多边形顶点！） |
| `PackedVector3Array` | Vector3 |
| `PackedColorArray` | Color（调色板） |
| `PackedByteArray` | 字节（文件/网络数据） |

```gdscript
var names := PackedStringArray(["A", "B", "C"])
var path := PackedVector2Array([Vector2(0, 0), Vector2(100, 0), Vector2(100, 100)])

names.append("D")               # 用法与Array基本一致
print(names[0])                 # A
print(names.size())             # 4
```

**什么时候用 Packed**：
- 数量大（几千~百万）且类型单一：路径点、顶点缓冲、音频采样；
- 与引擎 API 交界处（很多 API 直接收发 Packed 类型）；
- 日常几十上百个元素，普通 Array 完全够，别为性能焦虑。

## 10.3 性能基准直觉（数量级感受）

同一操作在普通 Array vs Packed 上的差异（示意量级，实际因硬件而异）：

```
10万元素遍历求和：
  Array           ~8ms
  PackedInt32Array ~2ms     （快约4倍）

100万元素：
  Array           ~80ms（掉帧！）
  PackedInt32Array ~20ms（勉强1帧内）
```

**结论**：日常规模无感，百万级才必须换。先写清楚，再谈快。

## 10.4 练习

1. 声明一个只能装 Vector2 的数组，加入三个点。
```gdscript
var pts: Array[Vector2] = []
pts.append(Vector2(0, 0))
pts.append(Vector2(1, 1))
pts.append(Vector2(2, 4))
```

2. 什么时候你会把 `Array` 换成 `PackedVector2Array`？
（答：存大量路径点/多边形顶点（数千以上）且只做批量读写时；或调用需要该类型的引擎API时。）

3. `var a: Array[int] = [1,2]` 和 `var b := [1,2]`，b 能直接赋给 a 吗？
（答：不能直接赋。b 是普通 Array（虽然内容恰好是int），转类型化需 `b.duplicate()` 或逐个 append。`:=` 推断 [1,2] 为普通 Array，不是 Array[int]。）


# 第 11 章：字符串（String）完全教程

字符串无处不在：UI文本、资源路径、存档、日志、网络消息。本章覆盖 String 全部常用方法（40+）、格式化输出、转义字符、以及实战模板。

## 11.1 基础：声明与拼接

```gdscript
var s1 := "双引号"
var s2 := '单引号'            # 两者等价，团队统一即可
var empty := ""
var multi := """
多行字符串
第二行
"""                            # 三引号跨行

# 拼接方式一：+ 号（两边必须是String）
var greeting := "你好, " + "世界"
var with_num := "等级 " + str(10)       # 数字先转str
# "等级 " + 10     # ✘ 报错！

# 拼接方式二：print 的多参数（自动空格连接）
print("血量", 78, "魔法", 30)            # 血量78魔法30

# 拼接方式三：% 格式化（下节详讲，最推荐）
var msg := "血量 %d / %d" % [78, 100]
```

## 11.2 格式化输出：% 占位符大全

`%` 格式化 = 模板填空。模板里 `%X` 是坑，`%` 后面给数据填：

```gdscript
# 基础用法
var s1 := "我是%s" % "勇者"                     # 我是勇者
var s2 := "血量 %d" % 78                        # 血量 78
var s3 := "血量 %d / %d" % [78, 100]            # 多个值用数组

# 占位符类型
%d      整数            "%d" % 42            → "42"
%f      小数            "%f" % 3.14          → "3.140000"
%.Nf    保留N位小数      "%.2f" % 3.14159    → "3.14"
%s      万能(转字符串)   "%s" % [1,"a"]      → "[1, a]"
%%      百分号本身       "100%%" % []        → "100%"
%5d     宽度补齐        "[%5d]" % 42        → "[   42]"
%05d    补零            "%05d" % 42         → "00042"
%-5d    左对齐          "[%-5d]" % 42       → "[42   ]"
%x      十六进制        "%x" % 255          → "ff"
%c      单字符          "%c" % 65           → "A"（ASCII码65是A）
```

**实战示例**：

```gdscript
# 伤害飘字
func damage_text(dmg: int, crit: bool) -> String:
	return "%s%d" % ["暴击 " if crit else "", dmg]

# 百分比显示（×100自己算）
func hp_ratio_text(cur: int, max_v: int) -> String:
	return "%.0f%%" % (float(cur) / max_v * 100.0)      # "78%"

# 表格对齐（对齐日志神器）
print("%-10s %5d %8.2f" % ["苹果", 3, 12.5])            # 苹果            3    12.50
print("%-10s %5d %8.2f" % ["香蕉蛋糕", 12, 108.0])       # 香蕉蛋糕       12   108.00

# 千位分隔（没有直接占位符，format_number辅助）
"%s" % format_number(1234567)    # 自定义函数加分隔符 "1,234,567"
```

**format_number 模板**：

```gdscript
func format_number(n: int) -> String:
	var s := str(n)
	var result := ""
	var count := 0
	for i in range(s.length() - 1, -1, -1):
		result = s[i] + result
		count += 1
		if count % 3 == 0 and i > 0:
			result = "," + result
	return result
```

## 11.3 转义字符：特殊字符的写法

```gdscript
var s1 := "第一行\n第二行"            # \n 换行
var s2 := "姓名:\t勇者"               # \t 制表符（对齐用）
var s3 := "他说:\"你好\""              # \" 引号内的引号
var s4 := "路径:C\\Users\\test"       # \\ 反斜杠本身
var s5 := "Unicode:\u4f60\u597d"      # \uXXXX → "你好"
```

| 转义 | 含义 |
|---|---|
| `\n` | 换行 |
| `\t` | Tab |
| `\"` | 双引号 |
| `\'` | 单引号 |
| `\\` | 反斜杠 |
| `\uXXXX` | Unicode字符 |

**Windows 路径必须双反斜杠**（单 `\` 被当转义）。Godot 内部路径统一用正斜杠 `/`，省心。

## 11.4 查询类方法

```gdscript
var s := "Hello Godot"

s.length()                    # 11      字符数（"你好"长度是2！中文字符算1个）
s.is_empty()                  # false
s.begins_with("Hell")         # true    以...开头
s.ends_with("dot")            # true    以...结尾
s.contains("lo G")            # true    包含子串
s.find("o")                   # 4       第一次出现的下标（无→-1）
s.find("o", 5)                # 7       从下标5起找
s.rfind("o")                  # 9       从后往前找
s.count("o")                  # 3       出现次数
s.get_slice(" ", 1)           # "Godot" 按" "切片取第1段
```

**find 的 -1 检查**（高频写法）：

```gdscript
var i := filename.find(".png")
if i != -1:
	var name_no_ext := filename.substr(0, i)      # 截掉扩展名
```

**中文与 length**：`"你好".length()` 是 **2**（字符数），不是 6（字节数）。GDScript 的 String 内部 UTF-32，一个汉字就是一个字符，遍历/截取不会劈成半个字。放心用。

## 11.5 变形类方法

```gdscript
var s := "  Hello World  "

s.to_upper()                  # "  HELLO WORLD  "
s.to_lower()                  # "  hello world  "
s.strip_edges()               # "Hello World"        去两端空白（含\n\t）
s.strip_edges(true, false)    # 只去左端
s.capitalize()                # "hello world" → "Hello World" 每词首字母大写
s.to_camel_case()             # "hello_world" → "helloWorld"
s.to_pascal_case()            # "hello_world" → "HelloWorld"
s.to_snake_case()             # "HelloWorld" → "hello_world"
s.trim_prefix("Hello ")       # "World"      有这前缀就去掉
s.trim_suffix(" World")       # "Hello"      有这后缀就去掉
```

**trim_prefix/suffix 是路径/格式处理的利器**：

```gdscript
var p := "res://assets/icon.png"
var rel := p.trim_prefix("res://")           # "assets/icon.png"
var p2 := "user://save_01.json"
var num := p2.trim_prefix("user://save_").trim_suffix(".json")   # "01"
```

## 11.6 切分与重组

```gdscript
# split：字符串 → 数组
var csv := "剑,盾,弓,药"
var items := csv.split(",")          # ["剑", "盾", "弓", "药"]
var items2 := csv.split(",", false, 2)   # 最多切2段 → ["剑", "盾,弓,药"]

# 特殊：split空串会把每个字符切开
"a,b".split("")                     # 不常用，知道即可

# join：数组 → 字符串（split的逆操作）
var words := ["Hello", "World"]
" ".join(words)                     # "Hello World"
",".join(["1", "2", "3"])           # "1,2,3"
"-".join(["2026", "01", "15"])      # "2026-01-15"

# substr：按下标截取
var s := "HelloGodot"
s.substr(0, 5)                      # "Hello"  从0起取5个字符
s.substr(5)                         # "Godot"  从5起到结尾
s.substr(-5)                        # "Godot"  负数=从尾部数
```

**split + join 实战**：

```gdscript
# 路径拆解
var path := "res://resource/weapon/sword.png"
var parts := path.split("/")        # ["res:", "", "resource", "weapon", "sword.png"]
var filename := parts[-1]           # sword.png
var folder := "/".join(parts.slice(0, parts.size() - 1))   # res://resource/weapon

# CSV一行 → 属性字典
func parse_csv_line(line: String) -> Dictionary:
	var cols := line.split(",")
	return {"name": cols[0], "hp": cols[1].to_int(), "atk": cols[2].to_int()}
# "史莱姆,20,5" → {name:史莱姆, hp:20, atk:5}
```

## 11.7 替换

```gdscript
var s := "你是个好人，但我们的勇士是另一个人"

s.replace("好人", "勇士")           # "你是个勇士，但我们的勇士是另一个人"（全换）
s.replacen("GOOD", "bad")          # 忽略大小写替换

# 路径规范化实战
var win_path := "C:\\game\\assets\\icon.png"
var uni_path := win_path.replace("\\", "/")   # "C:/game/assets/icon.png"
```

## 11.8 转换

```gdscript
# 字符串 → 数字
"42".to_int()                      # 42
"3.14".to_float()                  # 3.14
"42abc".to_int()                   # 42（能转多少转多少）
"abc".to_int()                     # 0（转不动给0，不报错！）
"  42  ".to_int()                  # 42（自动去两端空白）

# 数字 → 字符串
str(42)                            # "42"
str(3.14)                          # "3.14"
str(true)                          # "true"
str([1,2])                         # "[1, 2]"
str(Vector2(1,2))                  # "(1.0, 2.0)"

# 进制转换
"ff".hex_to_int()                  # 255
(255).to_int() 保持原样；str("%x" % 255)  # "ff"（格式化路线）

# 类型判断
"123".is_valid_int()               # true（能不能转int）
"3.14".is_valid_float()            # true
"12.5".is_valid_int()              # false（小数不是整数）
```

**is_valid 系列是"解析用户输入"的安全网**：

```gdscript
# 玩家在输入框打了字，要转数字
var text := input_field.text
if text.is_valid_int():
	var n := text.to_int()
	print("输入了:", n)
else:
	print("请输入整数！")
```

## 11.9 字符串比较与排序

```gdscript
"a" == "a"                         # true（内容比较）
"a" < "b"                          # true（字典序）
"A" < "a"                          # true（大写码点在前）
"abc" < "abd"                      # true（逐位比较）
"10" < "9"                         # true ！！字符串陷阱："1"<"9"
```

**⚠️ 数字排序前必须转回数字**：

```gdscript
var strs := ["10", "9", "2"]
strs.sort()                        # ["10", "2", "9"] 字典序，乱！
var nums := strs.map(func(s): return s.to_int())
nums.sort()                        # [2, 9, 10] ✔
```

忽略大小写比较：

```gdscript
func equals_ignore_case(a: String, b: String) -> bool:
	return a.to_lower() == b.to_lower()
```

## 11.10 字符遍历与字符码

```gdscript
var s := "ABC"

for ch in s:                       # 遍历字符
	print(ch)                       # A / B / C

# 字符 ↔ 编码
"a".unicode_at(0)                  # 97（字符→码）
String.chr(97)                     # "a"（码→字符）

# 实战：凯撒密码（字母移位加密）
func caesar(text: String, shift: int) -> String:
	var result := ""
	for ch in text:
		var c := ch.unicode_at(0)
		if c >= 97 and c <= 122:            # 小写字母区间
			c = 97 + (c - 97 + shift) % 26  # 环绕移位
		result += String.chr(c)
	return result

print(caesar("hello", 3))          # khoor
```

## 11.11 路径处理专题（游戏开发高频）

Godot 路径三前缀：

```
res://    项目内资源（打包进游戏，只读）
user://   用户数据（存档、设置；可写；各平台自动映射）
绝对路径   /sdcard/... 或 C:/...（少用，跨平台坑）
```

```gdscript
# 常用路径操作（String方法直接可用）
var p := "res://assets/weapon/sword.png"

p.get_file()                       # "sword.png"      文件名
p.get_basename()                   # "res://assets/weapon/sword"  去扩展名
p.get_extension()                  # "png"            扩展名
p.get_base_dir()                   # "res://assets/weapon"  所在目录
p.is_absolute_path()               # true

# 拼接（推荐手动 + "/" 或路径函数）
var dir := "res://assets"
var full := dir + "/" + "icon.png"     # res://assets/icon.png

# 判断资源类型
p.ends_with(".png")                # 图片？
p.ends_with(".ogg")                # 音频？
p.contains("weapon")               # 在武器目录？
p.begins_with("res://")            # 项目内资源？
```

**路径处理模板**：

```gdscript
# 遍历目录加载所有PNG（配合DirAccess，第28章详讲）
func load_all_textures(dir_path: String) -> Dictionary:
	var result := {}
	var dir := DirAccess.open(dir_path)
	if dir == null:
		return result
	dir.list_dir_begin()
	var file := dir.get_next()
	while file != "":
		if file.ends_with(".png"):
			result[file.get_basename()] = load(dir_path + "/" + file)
		file = dir.get_next()
	dir.list_dir_end()
	return result
# load_all_textures("res://assets/icons") → {"icon_sword": Texture2D, ...}
```

## 11.12 正则表达式 RegEx（进阶选学）

复杂文本模式匹配（验证邮箱、提取数字、解析聊天命令）：

```gdscript
var regex := RegEx.new()

# 匹配数字
regex.compile("\\d+")              # \d=数字（gd里要双反斜杠）
var m := regex.search("伤害: 250点")
if m:
	print(m.get_string())          # "250"

# 验证邮箱
var email_re := RegEx.new()
email_re.compile("^[\\w.]+@[\\w.]+\\.[a-z]{2,}$")
print(email_re.search("a@b.com") != null)      # true
print(email_re.search("垃圾") != null)          # false

# 捕获组：提取命令参数
var cmd_re := RegEx.new()
cmd_re.compile("^/(\\w+)\\s+(.+)$")          # /命令 参数
var cm := cmd_re.search("/give 剑 3")
if cm:
	print(cm.get_string(1))       # "give"（第1组）
	print(cm.get_string(2))       # "剑 3"

# 全局替换
var re := RegEx.new()
re.compile("\\s+")                 # 任意空白
print(re.sub("a   b \t c", " "))  # "a b c"（多空白压成单空格）
```

正则速查（够用版）：

```
\d  数字    \w  字母数字下划线   \s  空白
.   任意字符   *  0~n次   +  1~n次   ?  0~1次
^   开头    $   结尾    [abc] abc任一   [0-9] 区间
( ) 捕获组   |  或     {2,5} 2~5次
```

## 11.13 实战模板集

**模板一：富文本损伤飘字构造器**

```gdscript
func build_damage_text(dmg: int, tags: Array) -> String:
	# tags: ["crit", "fire", "miss"] 任意组合
	var color := "white"
	var prefix := ""
	if "crit" in tags:
		color = "yellow"
		prefix = "会心! "
	elif "fire" in tags:
		color = "orange"
		prefix = "灼烧 "
	if "miss" in tags:
		return "[color=gray]MISS[/color]"
	return "[color=%s]%s%d[/color]" % [color, prefix, dmg]
```

**模板二：字符串补零（关卡/编号显示）**

```gdscript
"%03d" % 7          # "007"
"第 %02d 关" % 12    # "第 12 关"
```

**模板三：耗时格式化**

```gdscript
func format_duration(seconds: float) -> String:
	var s := int(seconds)
	var h := s / 3600
	var m := (s % 3600) / 60
	var sec := s % 60
	if h > 0:
		return "%d:%02d:%02d" % [h, m, sec]
	return "%02d:%02d" % [m, sec]
# 754秒 → "12:34"   3661秒 → "1:01:01"
```

**模板四：文字进度条**

```gdscript
func text_bar(cur: int, max_v: int, width: int = 10) -> String:
	var filled := int(float(cur) / max_v * width) if max_v > 0 else 0
	filled = clampi(filled, 0, width)
	return "[" + "█".repeat(filled) + "░".repeat(width - filled) + "]"
# text_bar(7, 10, 10) → "[███████░░░]"
```

**模板五：聊天命令解析器**

```gdscript
func parse_command(raw: String) -> Dictionary:
	raw = raw.strip_edges()
	if not raw.begins_with("/"):
		return {"is_cmd": false}
	var parts := raw.substr(1).split(" ", false)   # 去掉/，按空格切
	if parts.is_empty():
		return {"is_cmd": false}
	return {
		"is_cmd": true,
		"cmd": parts[0].to_lower(),
		"args": parts.slice(1),                     # 剩余全部当参数
	}
# "/GIVE sword 3" → {is_cmd:true, cmd:"give", args:["sword","3"]}
```

**模板六：模板字符串引擎（简易文案系统）**

```gdscript
const TEMPLATE_MAP := {
	"$player": func(): return GameState.player_name,
	"$time":   func(): return Time.get_time_string_from_system(),
	"$gold":   func(): return str(GameState.gold),
}

func render(text: String) -> String:
	var result := text
	for key in TEMPLATE_MAP:
		if result.contains(key):
			result = result.replace(key, str(TEMPLATE_MAP[key].call()))
	return result
# render("欢迎 $player ！你有 $gold 金币") → "欢迎 勇者！你有 150 金币"
```

## 11.14 常见错误清单

| 错误 | 现象 | 修复 |
|---|---|---|
| `"值" + 5` | 报错 String+int | str(5) 转换 |
| 中文按字节截取劈成乱码 | 不会！GDScript按字符 | 放心用substr |
| 忘记 to_int 拿字符串比较大小 | "10"<"9" | 先转数字 |
| 路径用单反斜杠 | \U等被当转义 | 统一 / 或双\\ |
| to_int 失败拿0当真值 | 静默bug | 先 is_valid_int 判断 |
| split 后没检查段数 | 越界崩溃 | `if parts.size() >= n` |
| 格式化 % 数量不匹配 | 运行报错 | % 后数组元素数 = 占位符数 |
| 大小写敏感比较失败 | "OK"≠"ok" | to_lower() 后比 |

## 11.15 练习

1. 把 `"hello world"` 变 "Hello World"（每个词首字母大写）。
```gdscript
print("hello world".capitalize())       # Hello World
```

2. 一行代码：`"file_2026_01_15.png"` 提取出 `"2026-01-15"`。
```gdscript
var p = "file_2026_01_15.png".get_basename()   # file_2026_01_15
var date = "-".join(p.split("_").slice(1))     # 2026-01-15
```

3. 统计一段文字里 "godot"（忽略大小写）出现次数。
```gdscript
var text := "Godot is fun. I love godot! godot godot."
print(text.to_lower().count("godot"))           # 4
```

4. 写函数 `is_palindrome(s)`：判断字符串是否回文（正读反读一样，忽略大小写与空格）。
```gdscript
func is_palindrome(s: String) -> bool:
	var clean := s.to_lower().replace(" ", "")
	return clean == clean.reverse()
# Godot 4.x String 有 reverse()方法
```

5. 输出什么？
```gdscript
print("%.1f%%" % 66.7)
print("%s有%d个" % ["苹果", 3])
print("ab" * 2)
print("hello"[1])
```
（答案：66.7%、苹果有3个、abab、e）


# 第 12 章：枚举与常量组织术

游戏里有大量"固定选项"：职业{战士,法师,射手}、稀有度{普通,精良,传说}、状态{待机,移动,攻击}。枚举（enum）就是给这类"一组相关常量"起家族名的机制。

## 12.1 为什么需要枚举：魔法数字之灾

**没有枚举的世界**：

```gdscript
# 1=战士 2=法师 3=射手（写在某张纸巾上）
if job == 1:
	attack()
elif job == 2:
	cast_spell()

# 三个月后：1是什么？2是什么？新同事看代码像在解密
# 更糟：手滑写成 job == 4（不存在的职业），没有任何报错，运行静默出错
```

**有枚举的世界**：

```gdscript
enum Job { WARRIOR, MAGE, ARCHER }

if job == Job.WARRIOR:
	attack()
elif job == Job.MAGE:
	cast_spell()
# 人人可读；job == Job.ARCHER 有自动补全；写错立刻可见
```

## 12.2 枚举的定义与本质

```gdscript
# 定义一：匿名枚举（常量直接散在本文件）
enum { STATE_IDLE, STATE_RUN, STATE_ATTACK }
# 本质等价于：
# const STATE_IDLE = 0
# const STATE_RUN = 1
# const STATE_ATTACK = 2

# 定义二：命名枚举（成组管理，推荐）
enum State { IDLE, RUN, ATTACK }
# 使用时带家族名：State.IDLE

# 定义三：指定数值
enum Rarity {
	COMMON = 0,
	FINE = 1,
	EXCELLENT = 2,        # 不写则自动 = 前一个+1
	GOD = 4,              # 想跳号也行
}

# 定义四：从非0开始 / 负数
enum Tile { EMPTY = -1, GRASS = 0, WATER = 1, WALL = 2 }
```

**本质**：枚举成员就是**int 常量**。下面两行完全等价：

```gdscript
enum State { IDLE, RUN }
print(State.IDLE)         # 0
print(State.RUN)          # 1
print(typeof(State.IDLE)) # TYPE_INT —— 就是int！
```

正因为是 int，枚举才能放进数组、字典、match、网络传输。

## 12.3 枚举与字典的互相转换（实战必备）

**枚举 → 名字字符串**（调试显示神器）：

```gdscript
enum State { IDLE, RUN, ATTACK }
var state := State.RUN

State.keys()                        # ["IDLE", "RUN", "ATTACK"]（成员名数组）
State.keys()[state]                 # "RUN" —— 用值反查名字！

func state_name(s: int) -> String:
	return State.keys()[s] if s >= 0 and s < State.keys().size() else "???"

print(state_name(state))            # RUN
# 调试时"当前状态: RUN"比"当前状态: 1"友好一万倍
```

**枚举 → 显示文本**（给玩家看的）：

```gdscript
const STATE_TEXT := {
	State.IDLE: "待机",
	State.RUN: "奔跑",
	State.ATTACK: "攻击",
}
func state_text(s: int) -> String:
	return STATE_TEXT.get(s, "未知")
```

**字符串 → 枚举**（从存档/配置恢复）：

```gdscript
var saved := "RUN"                          # 存档里存的字符串
var idx := State.keys().find(saved)         # 1
if idx != -1:
	state = idx                              # 恢复成 State.RUN
```

## 12.4 枚举 + match：状态机黄金搭档

```gdscript
enum State { IDLE, PATROL, CHASE, ATTACK, HURT, DEAD }
var state: int = State.IDLE

func _process(delta: float) -> void:
	match state:
		State.IDLE:
			if enemy_nearby():
				change_state(State.CHASE)
		State.PATROL:
			move_along_path()
			if enemy_nearby():
				change_state(State.CHASE)
			elif patrol_done():
				change_state(State.IDLE)
		State.CHASE:
			chase_target()
			if in_attack_range():
				change_state(State.ATTACK)
			elif not enemy_nearby():
				change_state(State.PATROL)
		State.ATTACK:
			if attack_cooldown <= 0.0:
				perform_attack()
				attack_cooldown = 1.0
			if target_hp <= 0:
				change_state(State.IDLE)
		State.HURT:
			hurt_timer -= delta
			if hurt_timer <= 0.0:
				change_state(State.IDLE)
		State.DEAD:
			pass                            # 什么都不做
		_:
			change_state(State.IDLE)         # 未知状态回安全态

func change_state(new_state: int) -> void:
	if state == new_state:
		return
	state = new_state
	print("状态: ", State.keys()[state])     # 日志友好
```

## 12.5 常量组织术：把配置集中管理

小项目随手写 const 无妨；项目长大后，**常量要按"主题"分文件集中**——这就是"数据与逻辑分离"的起点：

```gdscript
# game_constants.gd —— 全游戏数值中心
class_name GameConstants

# ---- 战斗数值 ----
const MAX_HP := 9999
const BASE_CRIT := 0.05
const CRIT_MULT := 2.0
const MIN_DAMAGE := 1

# ---- 移动 ----
const PLAYER_SPEED := 300.0
const DASH_SPEED := 900.0
const DASH_TIME := 0.2
const GRAVITY := 1200.0

# ---- 经济 ----
const START_GOLD := 100
const SHOP_MARKUP := 1.3            # 商店加价30%

# ---- 层级（渲染顺序）----
const Z_WORLD := 0
const Z_PLAYER := 10
const Z_FX := 50
const Z_UI := 100
```

使用（任何脚本）：

```gdscript
speed = GameConstants.PLAYER_SPEED
sprite.z_index = GameConstants.Z_FX
```

**好处**：数值调平衡只开一个文件；"魔法数字"全灭；新成员找数值有唯一入口。

## 12.6 分组导出：@export 的枚举支持（预览，详见18章）

```gdscript
# 在检查器里显示下拉选择框
enum WeaponType { SWORD, BOW, STAFF }

@export var weapon_type: WeaponType = WeaponType.SWORD
@export var rarity: int = 0              # 无类型注解版
```

编辑器里直接下拉选枚举，策划改配置不用碰代码。

## 12.7 完整模板：稀有度系统（枚举驱动）

```gdscript
class_name RaritySystem

enum Rarity {
	COMMON,        # 0 白
	FINE,          # 1 绿
	EXCELLENT,     # 2 蓝
	EPIC,          # 3 紫
	GOD,           # 4 金
}

# 每档配置：颜色、名字、掉落权重、属性倍率
const CONFIG := {
	Rarity.COMMON:    {"name": "普通", "color": Color.WHITE,  "weight": 50, "mult": 1.0},
	Rarity.FINE:      {"name": "精良", "color": Color.GREEN,  "weight": 30, "mult": 1.2},
	Rarity.EXCELLENT: {"name": "稀有", "color": Color.CORNFLOWER_BLUE, "weight": 13, "mult": 1.5},
	Rarity.EPIC:      {"name": "史诗", "color": Color.MEDIUM_ORCHID, "weight": 6, "mult": 2.0},
	Rarity.GOD:       {"name": "神品", "color": Color.GOLD,   "weight": 1, "mult": 3.0},
}

static func get_name(r: int) -> String:
	return CONFIG.get(r, {}).get("name", "??")

static func get_color(r: int) -> Color:
	return CONFIG.get(r, {}).get("color", Color.WHITE)

static func get_mult(r: int) -> float:
	return CONFIG.get(r, {}).get("mult", 1.0)

# 按权重随机掉落（weighted random）
static func roll_rarity(luck: float = 0.0) -> int:
	var total := 0
	for r in CONFIG:
		var w: int = CONFIG[r].weight
		if r >= Rarity.EPIC:
			w = int(w * luck)              # 幸运值只加成高级掉落
		total += maxi(w, 0)
	var roll := randi_range(1, total)
	var acc := 0
	for r in CONFIG:
		var w: int = CONFIG[r].weight
		if r >= Rarity.EPIC:
			w = int(w * luck)
		acc += maxi(w, 0)
		if roll <= acc:
			return r
	return Rarity.COMMON
```

使用效果：

```gdscript
var r := RaritySystem.roll_rarity()
print("掉落[%s]品质装备，属性倍率%.1f" % [RaritySystem.get_name(r), RaritySystem.get_mult(r)])
item_label.modulate = RaritySystem.get_color(r)
```

## 12.8 练习

1. 定义方向枚举 `{UP, RIGHT, DOWN, LEFT}`，写函数返回对应 Vector2。
```gdscript
enum Dir { UP, RIGHT, DOWN, LEFT }
const DIR_VEC := {
	Dir.UP: Vector2.UP, Dir.RIGHT: Vector2.RIGHT,
	Dir.DOWN: Vector2.DOWN, Dir.LEFT: Vector2.LEFT,
}
func dir_vec(d: int) -> Vector2:
	return DIR_VEC.get(d, Vector2.ZERO)
```

2. `enum E { A = 5, B, C = 2, D }`，B 和 D 分别是几？
（答案：B=6（跟随A+1），D=3（跟随C+1）。）

3. 写函数：任意枚举值 → 打印"当前状态：XXX"。
```gdscript
func debug_state(s: int, enum_class) -> void:
	print("当前状态：", enum_class.keys()[s])
# 调用：debug_state(State.RUN, State)
```

---
---

# 第三卷 · 面向对象

# 第 13 章：类的基础——图纸与实物

## 13.1 类是什么：从"一堆变量和函数"到"一种东西"

假设要管理 3 个敌人，用目前所学的"散装写法"：

```gdscript
# 敌人1的数据（散落在各处的变量）
var e1_hp := 100
var e1_atk := 10
var e1_pos := Vector2(0, 0)
# 敌人2...
var e2_hp := 100
var e2_atk := 12
var e2_pos := Vector2(100, 0)
# 敌人3...复制粘贴到吐血
# 每个行为都要写三遍：e1_take_damage() e2_take_damage() ...
```

**类（class）= 把"数据"和"行为"打包成一种自定义类型**：

```gdscript
# 定义"敌人"这种东西（图纸）
class_name Enemy
extends Node2D

var hp := 100              # 这种东西有什么数据
var atk := 10
var enemy_name := "史莱姆"

func take_damage(amount: int) -> void:      # 这种东西会什么行为
	hp -= amount
	if hp <= 0:
		die()

func die() -> void:
	print(enemy_name, " 死亡")
```

```gdscript
# 按图纸造实物（实例化）
var e1 := Enemy.new()       # 造一个
e1.enemy_name = "史莱姆A"
e1.take_damage(30)

var e2 := Enemy.new()       # 再造一个，互不干扰
e2.enemy_name = "史莱姆B"
e2.hp = 150
```

术语对照：

| 术语 | 含义 | 类比 |
|---|---|---|
| 类 class | 类型定义（图纸） | "狗"这个物种概念 |
| 实例 instance | 按图纸造的对象 | 你家那条具体的狗 |
| 实例化 instantiate | 造对象的过程 | 生育 |
| 成员变量/属性 | 类里的变量 | 每条狗自己的体重 |
| 方法 method | 类里的函数 | 狗会"叫" |
| 成员访问 | `obj.x` / `obj.f()` | 这条狗的体重 / 让这条狗叫 |

## 13.2 GDScript 的类：文件即类

GDScript 里**一个 .gd 文件 = 一个类**。三种存在形态：

**形态一：独立文件 + class_name（全局可见，推荐）**

```gdscript
# enemy.gd
class_name Enemy
extends CharacterBody2D
# ...内容
```

之后**任何**脚本里 `Enemy.new()` 都能用。

**形态二：独立文件、无 class_name（按路径引用）**

```gdscript
# enemy.gd（没有class_name行）
extends CharacterBody2D
```

```gdscript
# 别的文件要用它：
const Enemy = preload("res://enemy.gd")     # 按路径"引进来"
var e := Enemy.new()
```

**形态三：内部类（一个文件里的迷你类）**

```gdscript
# main.gd
extends Node

class HitResult:                            # 声明在文件内
	var damage := 0
	var is_crit := false

func attack() -> HitResult:
	var r := HitResult.new()                # 内部类同样 .new()
	r.damage = 50
	r.is_crit = true
	return r
```

内部类适合"只为本文件服务的小数据结构"（结果打包、临时配置）。

## 13.3 extends：这个类"是什么"

每个类的第一行几乎都是 `extends X`，声明**继承**自哪个类（下一章细讲继承，这里先建立直觉）：

```gdscript
extends Node                    # 我是一种节点（逻辑挂载点）
extends Node2D                  # 我是一种2D节点（有position/rotation）
extends CharacterBody2D         # 我是一种物理角色（会移动/碰撞）
extends Sprite2D                # 我是一种图片节点
extends Button                  # 我是一种按钮
extends Resource                # 我是一种可保存/加载的数据资源
extends RefCounted              # 我是一种轻量纯数据对象（没有节点开销）
```

**选 extends 谁 = 决定"生下来会什么"**：

- 纯数据打包（不需要出现在场景里）→ `RefCounted`（最轻）
- 需要挂进场景树、参与帧循环 → `Node` / `Node2D`
- 需要显示图片 → `Sprite2D`
- 需要物理移动 → `CharacterBody2D`
- 可序列化的数据资源 → `Resource`

不写 extends 时默认继承 `RefCounted`。

## 13.4 成员变量：对象的出厂设置

```gdscript
class_name Enemy
extends RefCounted

var hp := 100                          # 带初值：每个实例出生就100血
var atk: int                           # 不带初值：默认0
var enemy_name := "无名"
var drops: Array[String] = []          # 类型化成员
```

**每个实例一份**——这是类的核心规则：

```gdscript
var a := Enemy.new()
var b := Enemy.new()
a.hp = 50
print(b.hp)                # 100 —— b的hp与a的无关！
```

## 13.5 方法：对象的行为

```gdscript
class_name Enemy
extends RefCounted

var hp := 100
var enemy_name := "史莱姆"

# 方法内直接用自己的成员（不用任何前缀）
func take_damage(amount: int) -> void:
	hp -= amount
	print(enemy_name, " 受击，剩", hp, "血")
	if hp <= 0:
		die()

func die() -> void:
	print(enemy_name, " 被消灭")
```

方法调用其他方法同样直接喊名：`die()`（等价 `self.die()`）。

**self**：指"当前这个实例"。通常省略，两个场景必须写：

```gdscript
var speed := 100.0

# 场景一：参数名遮蔽成员名
func set_speed(speed: float) -> void:
	self.speed = speed          # 左边成员，右边参数

# 场景二：需要把"自己"传给别人
func register():
	EnemyManager.add(self)      # 把我这个对象递出去
```

## 13.6 实例化与销毁的完整流程

```gdscript
extends Node

var enemies: Array[Enemy] = []

func spawn_enemy() -> void:
	var e := Enemy.new()            # ① 造
	e.enemy_name = "哥布林"          # ② 配（配置属性）
	e.hp = 80
	enemies.append(e)               # ③ 收（纳入管理）

func kill_all() -> void:
	for e in enemies:
		e.hp = 0
	enemies.clear()                  # 数组清空
	# RefCounted对象没有引用后自动回收（下一章详解）
```

## 13.7 类的静态视角与实例视角

类有两面：

```gdscript
class_name Enemy
extends RefCounted

# ---- 实例面：每个对象各一份 ----
var hp := 100
func take_damage(n: int) -> void: ...

# ---- 类面：全体共享 ----
static var total_count := 0                # 类变量
static func spawn(name: String) -> Enemy:  # 类方法
	total_count += 1
	var e := Enemy.new()
	e.enemy_name = name
	return e
```

```gdscript
# 类面：用类名直接访问，不需要实例
print(Enemy.total_count)               # 0
var goblin = Enemy.spawn("哥布林")      # 通过类方法造对象
print(Enemy.total_count)               # 1

# 实例面：用对象访问
goblin.take_damage(20)
print(goblin.hp)                        # 80
```

## 13.8 综合示例：第一个完整的类

需求：计时器类，支持倒计时、暂停、完成回调。

```gdscript
# game_timer.gd
class_name GameTimer
extends RefCounted

# ---- 配置（实例变量）----
var duration: float = 1.0
var one_shot: bool = true
var autostart: bool = false

# ---- 运行状态 ----
var time_left: float = 0.0
var is_running := false
var is_paused := false

# ---- 回调 ----
var on_timeout: Callable                 # 到点要执行的函数

func _init(p_duration: float = 1.0) -> void:     # 构造（17章详讲）
	duration = p_duration
	if autostart:
		start()

func start(p_duration: float = -1.0) -> void:
	if p_duration > 0.0:
		duration = p_duration
	time_left = duration
	is_running = true
	is_paused = false

func pause() -> void:
	if is_running:
		is_paused = true

func resume() -> void:
	is_paused = false

func stop() -> void:
	is_running = false
	time_left = 0.0

# 每帧推进（由外部驱动，因为RefCounted没有_process）
func tick(delta: float) -> void:
	if not is_running or is_paused:
		return
	time_left -= delta
	if time_left <= 0.0:
		time_left = 0.0
		is_running = false
		if one_shot:
			stop()
		else:
			start()                     # 循环模式重新开始
		if on_timeout.is_valid():
			on_timeout.call()
```

```gdscript
# 使用方（挂在Node上驱动）
extends Node

var respawn_timer: GameTimer
var combo_timer: GameTimer

func _ready() -> void:
	respawn_timer = GameTimer.new(3.0)
	respawn_timer.on_timeout = func(): print("敌人重生！")

	combo_timer = GameTimer.new()
	combo_timer.start(2.0)

func _process(delta: float) -> void:
	respawn_timer.tick(delta)           # 驱动所有计时器
	combo_timer.tick(delta)
```

不到 60 行实现了一个通用工具类——**这就是面向对象的复利**：写一次，全项目到处 `new`。

## 13.9 练习

1. 定义 `PlayerStats` 类（extends RefCounted）：hp/mp/atk/def 四个成员 + `is_alive()` 方法。
```gdscript
class_name PlayerStats
extends RefCounted

var hp := 100
var mp := 50
var atk := 10
var def := 5

func is_alive() -> bool:
	return hp > 0
```

2. 造两个 PlayerStats 实例，把 A 的 hp 改 50，B 的 hp 是多少？为什么？
（答案：100。每个实例的成员变量独立，互不影响。）

3. 在类里定义 `static var instance_count := 0`，构造时+1（提示：_init），实例化三个后值是多少？
```gdscript
static var instance_count := 0
func _init():
	instance_count += 1
# 三个实例后 = 3（全体共享这一个变量）
```

---

# 第 14 章：继承深入——站在巨人肩膀上

## 14.1 继承的直觉：is-a 关系

**继承（inheritance）表达"is a（是一种）"关系**：

```
CharacterBody2D（引擎内置：能物理移动的东西）
    └── Player（玩家：是一种能物理移动的东西 + 跳跃能力）
    └── Enemy（敌人：是一种能物理移动的东西 + AI）
          └── FlyingEnemy（飞行敌人：是一种敌人 + 无视重力）
```

```gdscript
# player.gd
class_name Player
extends CharacterBody2D        # Player 是一种 CharacterBody2D

func jump():
	velocity.y = -400.0
```

继承带来两件事：

1. **白得全部本领**：Player 一行不写就拥有 position、velocity、move_and_slide() 等 CharacterBody2D 的几百个属性方法；
2. **可以重写与扩展**：加自己的 jump()，或改掉父类某方法的实现。

## 14.2 extends 的三种目标

```gdscript
# ① 继承引擎类（最常见）
extends CharacterBody2D

# ② 继承自定义类（多级继承链）
class_name FlyingEnemy
extends Enemy                  # 继承自己项目的Enemy类

# ③ 继承"某个文件"（无class_name时用路径）
extends "res://enemies/base_enemy.gd"
```

## 14.3 方法重写（override）与 super

子类**重新定义**父类的同名方法 = 重写：

```gdscript
# base_enemy.gd
class_name Enemy
extends CharacterBody2D

func die() -> void:
	print("敌人倒下")
	queue_free()

func attack() -> void:
	print("普通攻击")
```

```gdscript
# boss.gd
class_name Boss
extends Enemy

# 重写：完全替换父类行为
func die() -> void:
	print("Boss死亡，掉落神装！")     # 不调用super → 父类的die不执行
	# 注意：这里故意不 queue_free，Boss要留尸体播放死亡动画
	drop_loot()
	play_death_animation()

# 追加式重写：先跑父类原版，再干自己的
func attack() -> void:
	super()                          # ← 执行父类Enemy.attack()（"普通攻击"）
	print("附加震屏效果")             # 我的花活
	shake_camera()
```

**super 三种形态**：

```gdscript
# ① super()：调父类的【同名同参】方法
func attack():
	super()

# ② super.method()：调父类的【指定】方法
func my_wrapper():
	super.attack()                   # 即使本方法不叫attack也能调父类attack
	super.die()

# ③ super.method(args)：带参数
func take_damage(amount: int, type: String):
	super(amount, type)              # 原样转发参数
	# 或 super.take_damage(amount, type)
```

**什么时候用 super**：想"保留父类行为+加料"时。忘记 super = 父类行为丢失（bug 高发地）。重写方法时**先问自己：父类原版要不要保留？**

## 14.4 继承链与成员的可见性

```gdscript
class_name A extends RefCounted
	var a_var := 1
	func a_func(): ...

class_name B extends A
	var b_var := 2
	func b_func(): ...

class_name C extends B
	func c_func():
		print(a_var)          # ✔ 爷爷的成员也能用（继承是传递的）
		print(b_var)          # ✔ 爸爸的
		a_func()              # ✔
		b_func()              # ✔
```

**子类能用父类的一切，父类对子类一无所知**。

## 14.5 is 与多态

**is 检查认整条继承链**：

```gdscript
var boss := Boss.new()

boss is Boss                 # true
boss is Enemy                # true（Boss是一种Enemy）
boss is CharacterBody2D      # true（一路都是）
boss is Node                 # true
boss is RefCounted           # true（万物曾祖）
boss is Player               # false（兄弟不算）
```

**多态（polymorphism）**：同一个调用，不同子类表现不同：

```gdscript
# 父类定义"规范"
class_name Shape extends RefCounted
	func area() -> float:
		return 0.0

class_name Circle extends Shape
	var radius := 10.0
	func area() -> float:              # 各自重写area
		return PI * radius * radius

class_name Rect extends Shape
	var w := 4.0
	var h := 5.0
	func area() -> float:
		return w * h
```

```gdscript
# 使用方完全不管具体类型，统一当Shape调
var shapes: Array[Shape] = [Circle.new(), Rect.new()]
for s in shapes:
	print(s.area())        # 圆打印314.16，矩形打印20 —— 各按各的实现
```

**多态的价值**：调用方代码零修改即可支持新形状。加个 Triangle？继承 Shape 实现 area，数组里塞进去就行——**"对扩展开放，对修改关闭"**。

实战中最常见的多态：重写引擎方法。

```gdscript
extends Node

func _ready() -> void: ...        # 重写Node的_ready（引擎会调）
func _process(delta: float) -> void: ...   # 重写_process
```

你在**重写引擎的类**——这就是天天在用的继承。

## 14.6 何时不该用继承：组合优于继承

继承是强关系（永久绑定）。滥用会产生脆弱的继承塔。**"has-a（有一个）"关系用组合**：

```gdscript
# ✘ 坏设计：为了"能攻击"而继承
class Sword extends Enemy            # 剑不是敌人！！is-a不成立

# ✔ 好设计：组合——玩家【有一个】武器
class_name Weapon extends RefCounted
	var atk := 10
	func swing(): ...

class_name Player extends CharacterBody2D
	var weapon: Weapon = null         # 组合：持有
	func attack():
		if weapon != null:
			weapon.swing()
```

**判断口诀**：
- "X 是一种 Y" → 继承（Enemy 是一种 CharacterBody2D）
- "X 有一个 Y" → 组合（Player 有一个 Weapon）

## 14.7 练习

1. `class_name Cat extends Animal`，`Animal extends Node`。`Cat.new() is Node` 是？
（答案：true。is 认整条链。）

2. 子类重写 `func save(): ...` 时想先执行父类的保存逻辑，第一行写什么？
（答案：`super()`。）

3. "汽车"和"引擎"应该用继承还是组合？"电动汽车"和"汽车"呢？
（答案：汽车 has 引擎 → 组合；电动汽车 is 汽车 → 继承。）

4. 多态示例中，若新增 `Triangle extends Shape`，`shapes` 数组的遍历代码要改吗？
（答案：不用。这就是多态的开闭价值。）


# 第 15 章：静态成员与工具类设计

## 15.1 static 全家福

`static` 关键字让成员**属于类本身**而非某个实例：

```gdscript
class_name GameData
extends RefCounted

# 静态变量：全体共享一份
static var high_score := 0
static var instance_count := 0

# 静态常量：数据表的最佳载体
const MAX_LEVEL := 99

# 静态方法：不造对象直接调
static func is_high_score(score: int) -> bool:
	return score > high_score

# 构造里也能碰静态
func _init():
	instance_count += 1
```

```gdscript
# 使用：全程用类名，一次都不用new
GameData.high_score = 1000
print(GameData.is_high_score(500))       # false
```

## 15.2 static 方法的限制

静态方法里**不能用实例成员和 self**：

```gdscript
class_name Bad
extends RefCounted
var hp := 100                    # 实例成员
static func broken():
	print(hp)                    # ✘ 报错：静态环境访问不到实例的hp
	print(self)                  # ✘ 报错：没有self
```

反过来，**实例方法里可以随便用静态成员**：

```gdscript
static var config := {}
func load_cfg():
	config = read_file()          # ✔ 实例方法碰静态变量没问题
```

## 15.3 static var 的经典应用模式

**模式一：全局共享状态（游戏状态中心）**

```gdscript
class_name GameState
extends RefCounted

static var player_name := "勇者"
static var gold := 0
static var current_level := 1
static var playtime := 0.0

static func add_gold(amount: int) -> void:
	gold = maxi(gold + amount, 0)
	static_save_gold()                     # 静态方法里也能调静态方法

static func static_save_gold() -> void:
	print("存档金币:", gold)
```

任何脚本里 `GameState.gold += 100`，全游戏同步。

**模式二：资源缓存（加载一次，全局复用）**

```gdscript
class_name TextureCache
extends RefCounted

static var _cache := {}                     # 路径→纹理

static func get_texture(path: String) -> Texture2D:
	if _cache.has(path):
		return _cache[path]                 # 命中：直接返回
	var tex = load(path)
	if tex != null:
		_cache[path] = tex
	return tex

static func clear() -> void:
	_cache.clear()                          # 换场景时可清缓存省内存
```

**模式三：实例计数**

```gdscript
class_name Enemy
static var alive_count := 0
static var total_spawned := 0

func _init():
	total_spawned += 1
	alive_count += 1

func die():
	alive_count -= 1
	# 界面显示 "存活: 8" 直接读 Enemy.alive_count
```

## 15.4 工具类设计模板（static 的主场）

**纯工具类**：全是 static 方法 + 无状态（或只有 static 状态），永远不 new。

```gdscript
class_name MathX
extends RefCounted

# 范围映射：把一个区间的值按比例映射到另一区间
# 例：把 0~100 的血量 映射到 0~1 的进度条比例
static func remap(value: float, from_min: float, from_max: float,
		to_min: float, to_max: float) -> float:
	if is_equal_approx(from_min, from_max):
		return to_min
	var t := (value - from_min) / (from_max - from_min)
	return lerpf(to_min, to_max, t)

# 数值便捷钳制
static func clamp01(v: float) -> float:
	return clampf(v, 0.0, 1.0)

# 概率工具
static func chance(p: float) -> bool:
	return randf() < p

# 随机取两个数
static func rand_range_i(a: int, b: int) -> int:
	return randi_range(a, b)

# 带权随机选择（游戏掉落核心算法）
static func weighted_pick(options: Array) -> Variant:
	# options: [{"value": xxx, "weight": 10}, ...]
	var total := 0
	for opt in options:
		total += maxi(opt.weight, 0)
	if total <= 0:
		return null
	var roll := randi_range(1, total)
	var acc := 0
	for opt in options:
		acc += maxi(opt.weight, 0)
		if roll <= acc:
			return opt.value
	return options[-1].value
```

```gdscript
# 使用
var ratio := MathX.remap(hp, 0, 100, 0, 1)     # 血量→进度条
if MathX.chance(0.25):                          # 25%概率
	critical_hit()
var drop = MathX.weighted_pick([
	{"value": "金币", "weight": 60},
	{"value": "药水", "weight": 30},
	{"value": "神装", "weight": 1},
])
```

## 15.5 引擎自带的静态工厂（认脸）

很多引擎类提供了 static 构造方法，见名知义：

```gdscript
Image.create(w, h, false, Image.FORMAT_RGBA8)        # 造空白图像
ImageTexture.create_from_image(img)                  # 图像→纹理
Vector2.from_angle(0.5)                              # 角度→单位向量
Color.from_hsv(0.5, 0.8, 0.9)                        # HSV颜色
Label.new() / Sprite2D.new()                         # 节点构造
```

自己设计类时，遇到"几种不同的创建方式"，也可以用 static 工厂：

```gdscript
class_name Enemy
var uid := ""
var hp := 100

static func from_dict(data: Dictionary) -> Enemy:
	var e := Enemy.new()
	e.uid = data.get("uid", "")
	e.hp = data.get("hp", 100)
	return e

static func boss_version(base_uid: String) -> Enemy:
	var e := Enemy.new()
	e.uid = base_uid + "_boss"
	e.hp = 10000
	return e
```

## 15.6 单例模式与 Autoload（预告）

"全游戏只有一份、随处可访问"的对象叫单例（Singleton）。Godot 有官方机制 **Autoload**（项目设置里注册），注册后类名全局可用且始终存在。这是静态类的加强版——**有生命周期（_ready/_process）、能挂信号、能当节点**。第 19、34 章实战展开。

## 15.7 练习

1. 写工具类 `StrX`：static 方法 `pad_center(s, width)` 居中补空格。
```gdscript
class_name StrX
static func pad_center(s: String, width: int) -> String:
	if s.length() >= width:
		return s
	var left := (width - s.length()) / 2
	return " ".repeat(left) + s + " ".repeat(width - s.length() - left)
# pad_center("ab", 6) → "  ab  "
```

2. static 方法里能用 `static var` 吗？能用 `var`（实例变量）吗？
（答案：能用 static var；不能用实例 var。）

3. 设计一个 `AudioCache`：`static func get_sound(name)` 保证每个音效只 load 一次。
```gdscript
class_name AudioCache
static var _cache := {}
static func get_sound(name: String) -> AudioStream:
	if not _cache.has(name):
		_cache[name] = load("res://audio/%s.ogg" % name)
	return _cache[name]
```

---

# 第 16 章：内部类、引用语义与值语义

## 16.1 内部类（class 嵌套）

一个 gd 文件里，主类之外可声明若干**内部类**：

```gdscript
# battle_report.gd
class_name BattleReport
extends RefCounted

# 内部类：只为BattleReport服务的小结构
class Round:
	var round_no := 0
	var events: Array[String] = []
	func add_event(e: String) -> void:
		events.append("回合%d: %s" % [round_no, e])

class Summary:
	var total_damage := 0
	var winner := ""
```

```gdscript
# 使用：类型名要带主类前缀
var r := BattleReport.Round.new()
r.round_no = 1
r.add_event("勇者攻击")
var s := BattleReport.Summary.new()
```

**何时用内部类**：数据结构只跟这个文件强相关、不值得单独开文件（结果打包、配置项、临时节点）。**何时不用**：结构会被多处引用——单独建文件+class_name 更清晰。

## 16.2 引用语义 vs 值语义（第 3 章深化，本章面向对象）

GDScript 数据分两族：

| 族 | 成员 | 赋值/传参行为 |
|---|---|---|
| 值类型 | int/float/bool/String/Vector2/Color/Rect2 | 复制内容，改新不换旧 |
| 引用类型 | Array/Dictionary/**所有类实例与节点** | 复制"地址"，改一个全变 |

**类实例永远是引用**——用对象做实验：

```gdscript
class_name Enemy
extends RefCounted
var hp := 100

var a := Enemy.new()
var b = a                  # b和a指向同一个敌人！
b.hp = 50
print(a.hp)                # 50 💥
print(a == b)              # true（同一个对象）
```

**函数传对象也是引用**（第 7 章讲过，从类视角再看）：

```gdscript
func heal(target: Enemy, amount: int) -> void:
	target.hp += amount             # 真的改到外面的对象

var e := Enemy.new()
heal(e, 30)
print(e.hp)                        # 130 ✔（这次是想要的效果）
```

## 16.3 引用相等 vs 内容相等

```gdscript
var a := Enemy.new()
var b := Enemy.new()
var c = a

a == b          # false —— 两个不同的对象（即使所有属性一样）
a == c          # true  —— 同一个对象
```

对象比较 `==` 问的是"**是不是同一个**"，不是"长得像不像"。字典/数组恰好相反：`==` 是深度内容比较（引擎特例）。

**自实现内容比较**：给自己的类写 `equals` 方法：

```gdscript
class_name Point
var x := 0.0
var y := 0.0

func equals(other: Point) -> bool:
	return x == other.x and y == other.y
```

## 16.4 引用与生命周期：谁在 keeping alive

**RefCounted（默认）：引用计数自动回收**

```gdscript
var e := Enemy.new()          # 引用计数=1
var f = e                     # =2
f = null                      # =1
e = null                      # =0 → 对象自动销毁，无需手动
```

**Node：由场景树管理（不归引用计数）**

```gdscript
var n := Node.new()
n = null                      # ⚠️ 对象不会消失（场景树还持有着？不——没add_child的话也不会自动删）
# 正确销毁节点：
n.free()                      # 立即销毁
n.queue_free()                # 帧末安全销毁（推荐）
```

节点泄漏是新手项目变卡的主因：`Sprite2D.new()` 了一堆忘了 free。**节点三律**：
1. 造了要挂（add_child）或明确说明用途；
2. 不要了要 queue_free；
3. 拿别人节点引用前先 is_instance_valid。

## 16.5 练习

1. `var a := [1]; var b = a; b.append(2)`，a 现在是？`var c := Vector2(1,1); var d = c; d.x = 9`，c.x 是？
（答案：a=[1,2]（数组引用共享）；c.x=1（Vector2值拷贝）。）

2. 为什么 `queue_free()` 优于 `free()`？
（答案：free 立即销毁，本帧后续代码若还碰它就崩；queue_free 推迟到帧末，当前帧安全。）

3. 内部类 `Round` 在外部文件怎么实例化？
（答案：`BattleReport.Round.new()`，带主类前缀。）

---

# 第 17 章：构造函数与对象的一生

## 17.1 _init：出生时执行

`_init` 是**构造函数**——`new()` 的瞬间自动执行：

```gdscript
class_name Enemy
extends RefCounted

var hp: int
var uid: String

func _init(p_uid: String = "slime", p_hp: int = 100) -> void:
	uid = p_uid
	hp = p_hp
	print(uid, " 出生")
```

```gdscript
var a := Enemy.new()                    # slime 出生（用默认参）
var b := Enemy.new("bat", 60)           # bat 出生
var c := Enemy.new("boss")              # boss 出生（hp默认100）
```

**命名习惯**：构造参数加 `p_` 前缀（p=param），避免与成员名冲突。也可用 self 风格：

```gdscript
func _init(uid: String = "slime", hp: int = 100) -> void:
	self.uid = uid                     # self.区分类成员与参数
	self.hp = hp
```

## 17.2 构造链：super 的时机

子类**默认自动调用**父类 `_init()`。父类构造带参数时，子类必须显式传：

```gdscript
class_name Entity
extends RefCounted
var name := ""

func _init(p_name: String) -> void:
	name = p_name

class_name Boss extends Entity
var phase := 1

func _init(p_name: String, p_phase: int) -> void:
	super(p_name)                      # ← 必须先给父类构造喂参数
	phase = p_phase
```

```gdscript
var b := Boss.new("龙王", 2)
print(b.name, b.phase)                  # 龙王 2
```

**顺序铁律**：父类构造先于子类构造执行（先有地基再盖楼）。

## 17.3 Node 的一生：_init → _enter_tree → _ready → ... → _exit_tree

Node 对象的完整生命周期（20 章函数详解）：

```
ClassName.new()
    ↓
_init()                 出生：分配内存（此时不在场景树！不能get_parent）
    ↓ add_child() 
_enter_tree()           进入场景树：有父有根了
    ↓ 所有子节点就位
_ready()                就绪：孩子齐全，初始化圣地（只调一次）
    ↓
_process/_physics_process   每帧循环（若定义）
_input/_unhandled_input     输入响应（若定义）
    ↓
_exit_tree()            离开树：清理引用、断信号
    ↓
queue_free()/free()     销毁
NOTIFICATION_PREDELETE  临终通知
```

**_init 与 _ready 的分工**（新手常混）：

| | _init | _ready |
|---|---|---|
| 时机 | new 的瞬间 | 进树且孩子就绪后 |
| 能用父节点/孩子？ | ✘ 都不行 | ✔ 都行 |
| 执行次数 | 每次 new | 一次 |
| 适合干什么 | 设置成员初值 | 抓节点引用、连信号、加载资源 |

```gdscript
extends Node2D

var config := {}                         # 纯数据：_init搞定
func _init(p_config: Dictionary = {}) -> void:
	config = p_config

@onready var sprite := $Sprite2D         # 孩子引用：必须等_ready
func _ready() -> void:
	sprite.modulate = Color.RED           # 现在碰孩子才安全
```

## 17.4 工厂模式：控制对象的诞生

构造函数不够灵活时（多种创建路径、创建时要做检查），用**静态工厂**：

```gdscript
class_name Character
extends RefCounted

var name := ""
var cls := ""
var hp := 100

# 私有构造（约定：不直接new）
func _init(p_name: String, p_cls: String, p_hp: int) -> void:
	name = p_name
	cls = p_cls
	hp = p_hp

# ---- 工厂方法们：每种创建需求一个入口 ----
static func create_warrior(p_name: String) -> Character:
	return Character.new(p_name, "warrior", 150)

static func create_mage(p_name: String) -> Character:
	return Character.new(p_name, "mage", 80)

static func from_dict(d: Dictionary) -> Character:
	return Character.new(
		d.get("name", "无名"),
		d.get("cls", "warrior"),
		d.get("hp", 100),
	)

static func random_enemy() -> Character:
	var names := ["史莱姆", "蝙蝠", "骷髅"]
	return Character.new(names.pick_random(), "enemy", randi_range(20, 60))
```

```gdscript
var hero = Character.create_warrior("兰斯洛特")
var foe = Character.random_enemy()
var loaded = Character.from_dict(save_data)
```

工厂的好处：调用处读起来像自然语言；创建逻辑集中可测；隐藏构造细节。

## 17.5 对象池（重对象的复生术）

频繁 new/free（子弹、粒子）会加重 GC/内存压力。**对象池**：造一批循环用（34 章完整模板，这里看生命周期视角）：

```gdscript
class_name BulletPool
extends RefCounted

var _pool: Array = []            # 待命区
var _active: Array = []          # 使用中

func acquire() -> Bullet:
	var b: Bullet
	if _pool.is_empty():
		b = Bullet.new()          # 池空才造新的
	else:
		b = _pool.pop_back()      # 复用旧的
		b.revive()                # 复位状态（重获新生）
	_active.append(b)
	return b

func release(b: Bullet) -> void:  # "死"了不销毁，回池待命
	_active.erase(b)
	b.sleep()
	_pool.push_back(b)
```

## 17.6 练习

1. `_init` 里能 `get_parent()` 吗？`_ready` 里呢？
（答案：不能/能。_init 时还没进树；_ready 时已在树且孩子就绪。）

2. 子类 `_init` 要先做什么（当父类构造带参）？
（答案：`super(参数)` 显式调用父类构造并传参。）

3. 设计 `ScoreEntry` 类：`_init(player_name, score)`，配 `from_list` 静态工厂把 `[[名,分],...]` 转成对象数组。
```gdscript
class_name ScoreEntry
extends RefCounted
var player_name := ""
var score := 0

func _init(p_name: String = "", p_score: int = 0) -> void:
	player_name = p_name
	score = p_score

static func from_list(list: Array) -> Array:
	var result := []
	for pair in list:
		result.append(ScoreEntry.new(pair[0], pair[1]))
	return result
```

---

# 第 18 章：注解大全——@开头的魔法

注解（Annotation）是挂在声明前的编译期指令，`@` 开头。本章按用途分组介绍全部常用注解。

## 18.1 @export 家族（检查器可视化，共 15+ 种）

`@export` 让变量出现在编辑器**检查器**面板——策划不用碰代码就能调数值：

```gdscript
@export var speed := 300.0                  # 基础版：滑条/输入框
@export var enemy_name := "史莱姆"
@export var is_boss := false
@export_range(0, 100, 1) var hp := 100      # 限定范围与步长
@export_range(0.0, 1.0, 0.01) var volume := 0.8
@export_range(1, 10, 1, "or_greater") var level := 1   # 允许超上限
@export_range(-360, 360, 0.1, "radians") var angle := 0.0  # 显示度数存弧度
@export_file var dialog_path: String        # 文件选择器
@export_file("*.png") var icon_path: String # 过滤扩展名
@export_dir var save_folder: String         # 目录选择器
@export_global_file("*.json") var config: String  # 全局路径
@export_node_path("Sprite2D") var sprite_path: NodePath  # 场景内选节点
@export_multiline var tooltip_text := ""    # 多行文本框
@export_placeholder("请输入...") var code: String  # 占位提示（值不会保存）
@export var color := Color.WHITE            # 颜色选择器
@export var texture: Texture2D              # 资源拖放槽
@export var drops: Array[String] = []       # 数组编辑器
@export_flags("fire", "ice", "poison") var elements := 0   # 勾选框组（位标志）
@export_enum("普通", "精良", "史诗") var rarity := 0        # 下拉枚举（返回int索引）
@export_enum("A:1", "B:2") var mode := 1    # "显示名:值"形式
```

**分组与分类**（检查器太长时）：

```gdscript
@export_group("战斗属性")           # 分组标题
@export var atk := 10
@export var def := 5
@export var crit := 0.1

@export_group("移动")
@export_subgroup("基础")            # 子分组
@export var speed := 300.0
@export_subgroup("冲刺")
@export var dash_speed := 900.0

@export_category("高级设置")        # 大分区（带分隔线）
@export var debug_mode := false
```

**@export_storage**：值会存进场景文件但**不显示**在检查器（程序内部配置）：

```gdscript
@export_storage var internal_id := ""     # 保存但不给策划看
```

**@export_custom**：自定义属性提示（极少用，知道存在即可）。

## 18.2 @onready：进树时初始化

```gdscript
@onready var sprite: Sprite2D = $Sprite2D
@onready var anim := $AnimationPlayer
@onready var hp_bar := $UI/HPBar
```

等价于在 _ready 里赋值，但更短更集中。**所有"抓自己孩子引用"都该用 @onready**——比手写在 _ready 里少写一个函数。

注意执行顺序：@onready 全部在 _ready 之前按声明顺序执行：

```gdscript
@onready var a := $A                    # 先执行
@onready var b := get_node("B")         # 再执行
func _ready():
	print(a, b)                          # 都已就绪
```

## 18.3 @tool：编辑器里也运行

普通脚本只在游戏运行时执行；`@tool` 让脚本**在编辑器里就跑**（看到实时预览）：

```gdscript
@tool
extends Node2D

@export var radius := 50.0:
	set(v):                             # 值一变就重绘
		radius = v
		queue_redraw()

func _draw() -> void:                  # 画一个圈预览
	draw_circle(Vector2.ZERO, radius, Color.RED)
```

⚠️ @tool 危险提醒：编辑器里代码也在跑，`print`/存文件/访问"游戏状态"会污染编辑器。**@tool 脚本里凡涉及游戏逻辑要判断 `Engine.is_editor_hint()`**：

```gdscript
@tool
extends Node2D

func _process(delta):
	if Engine.is_editor_hint():
		return                       # 编辑器环境不跑游戏逻辑
	move(delta)
```

## 18.4 @rpc：网络同步（多人游戏用）

```gdscript
@rpc("any_peer", "call_local", "reliable")
func sync_position(pos: Vector2) -> void:
	position = pos
```

参数组合：authority范围 / 本地是否也执行 / 可靠性。单机开发用不到，多人必学。

## 18.5 @warning_ignore：屏蔽特定警告

```gdscript
@warning_ignore("unused_parameter")
func _process(delta: float) -> void:      # delta没用到，屏蔽"未使用参数"警告
	update_visuals()
```

常用警告名：`unused_parameter`、`unused_variable`、`shadowed_variable`、`integer_division`、`unsafe_property_access`。**能改代码消警告就别屏蔽**，屏蔽是最后手段。

## 18.6 @abstract（4.4+）与 @warning_restore

```gdscript
# @abstract：声明"子类必须实现"
@abstract
class_name BaseEnemy extends CharacterBody2D

@abstract func unique_attack() -> void    # 子类不实现会报错

# @warning_restore：屏蔽警告后恢复
@warning_ignore("unused_parameter")
func a(x): ...
@warning_restore("unused_parameter")       # 之后的恢复警告
```

## 18.7 @static_load / @static_unload（4.4+，了解）

控制静态成员的加载卸载时机，内存敏感场景使用。入门阶段跳过。

## 18.8 注解速查总表

| 注解 | 作用 | 章节 |
|---|---|---|
| `@export` 系列 | 变量进检查器 | 18.1 |
| `@export_group/subgroup/category` | 检查器分组 | 18.1 |
| `@onready` | 就绪时初始化 | 18.2 |
| `@tool` | 编辑器内运行 | 18.3 |
| `@rpc` | 网络远程调用 | 18.4 |
| `@warning_ignore` | 屏蔽警告 | 18.5 |
| `@abstract` | 抽象声明(4.4+) | 18.6 |
| `@rpc` 多参形式 | 详细网络配置 | 18.4 |
| `@export_custom` | 自定义提示 | 18.1 |

## 18.9 属性的 set/get（与注解配合的进阶写法）

变量可以定义"存取钩子"——赋值/读取时自动执行代码：

```gdscript
# set/get 完整形态
var hp := 100:
	set(value):                       # 赋值时执行
		hp = clampi(value, 0, max_hp)
		hp_changed.emit(hp)
	get:
		return hp
```

```gdscript
# 常用简化：set里调更新
@export var speed := 300.0:
	set(v):
		speed = v
		if Engine.is_editor_hint():
			queue_redraw()

# 只读属性（get没有set）
var display_name: String:
	get:
		return "%s Lv.%d" % [name, level]

# 背景字段模式（避免set里递归自己）
var _hp := 100
var hp: int:
	set(v):
		_hp = clampi(v, 0, max_hp)
	get:
		return _hp
```

**⚠️ set 里给自己赋值会无限递归吗？** GDScript 有保护：set 内 `hp = v` 会直接写底层存储，不再触发 set。但复杂逻辑仍推荐 `_hp` 背景字段模式，最直白安全。

## 18.10 练习

1. 让"最大血量"在检查器里限制 1~9999、步长 1，怎么写？
```gdscript
@export_range(1, 9999, 1) var max_hp := 100
```

2. `@onready var label := $Label` 放在类顶部，与在 _ready 里 `label = $Label` 等价吗？
（答案：等价。@onready 本质就是把赋值推迟到 _ready 前。）

3. @tool 脚本里防止游戏逻辑污染编辑器的标准写法？
```gdscript
func _process(delta):
	if Engine.is_editor_hint():
		return
	# 游戏逻辑...
```

4. 写一个 `speed` 变量：赋值时打印变化日志。
```gdscript
var speed := 300.0:
	set(v):
		print("速度 %.1f → %.1f" % [speed, v])
		speed = v
```


---
---

# 第四卷 · 引擎交互

# 第 19 章：节点与场景树深入

## 19.1 一切皆节点

Godot 的世界观极简：**游戏 = 一棵节点树**。节点（Node）是最小积木，每种节点有一技之长：

```
Node                     万物之祖：能进树、能有孩子、能收通知
├── Node2D               有位置/旋转/缩放的2D节点（CanvasItem→Node2D链）
│   ├── Sprite2D         显示一张图
│   ├── AnimatedSprite2D 显示帧动画
│   ├── CharacterBody2D  可编程物理体（主角标配）
│   ├── RigidBody2D      真实物理体（受重力/碰撞）
│   ├── StaticBody2D     静止碰撞体（墙/地）
│   ├── Area2D           触发区域（判定进入/离开）
│   ├── Camera2D         摄像机
│   ├── TileMapLayer     瓦片地图
│   └── Path2D/PathFollow2D  路径（巡逻辑用）
├── Control              UI之祖（有布局属性）
│   ├── Button           按钮
│   ├── Label            文本
│   ├── TextureRect      图片框
│   ├── ProgressBar      进度条
│   └── Panel/Container  容器与面板
├── Timer                定时器
├── AudioStreamPlayer    音频播放器
└── AnimationPlayer      动画控制器
```

**看一眼节点类型名，就知道它干嘛**——名字是直白的英文。

## 19.2 场景树：节点的家谱

运行中的游戏结构：

```
/root (Window)
├── MyGame (Node)               ← 你项目的主场景
│   ├── World (Node2D)
│   │   ├── Player (CharacterBody2D)
│   │   │   ├── Sprite (Sprite2D)
│   │   │   └── Collision (CollisionShape2D)
│   │   ├── Enemy1 (CharacterBody2D)
│   │   └── Enemy2 (CharacterBody2D)
│   └── UI (Control)
│       ├── HPBar (ProgressBar)
│       └── ScoreLabel (Label)
└── Autoload单例们...            ← 常驻后台（GameState等）
```

**父子关系的含义**：

1. **组织**：树是天然的管理结构（"消灭所有敌人"=遍历World的孩子们）；
2. **继承变换**（2D下）：孩子 position/rotation/scale 相对父亲。父亲动，全家动；
3. **传播**：信号、通知、输入沿树传播；
4. **存亡与共**（部分）：父亲 free 时，全部孩子一起销毁。

**相对坐标实验**：

```gdscript
# World 在 (100, 0)，Player是World的孩子，position=(50, 0)
# → Player在屏幕上的位置 = 100 + 50 = 150 (global_position)
print(player.global_position)        # (150, 0)
print(player.position)               # (50, 0) 相对父亲的"本地坐标"
```

## 19.3 场景（Scene）：可复用的子树

**场景（.tscn文件）= 存在硬盘上的一棵子树**。做成场景 → 反复实例化：

```
enemy.tscn（图纸场景）
└── Enemy (CharacterBody2D)
    ├── Sprite
    └── Collision

main.tscn（主场景）
└── World
    ├── Enemy (enemy.tscn的实例)   ← 同一图纸造的三份
    ├── Enemy2 (又是实例)
    └── Enemy3 (又是实例)
```

代码实例化场景：

```gdscript
const ENEMY_SCENE := preload("res://enemy.tscn")   # 编译期加载图纸

func spawn_enemy(pos: Vector2) -> void:
	var e := ENEMY_SCENE.instantiate()              # 照图纸造
	e.position = pos
	$World.add_child(e)                             # 挂进树才开始运行
```

**三步走：load图纸 → instantiate → add_child**。

## 19.4 add_child 的细节

```gdscript
# 基本用法
add_child(node)                        # 挂到我下面（成为我最小的孩子）

# 挂到指定位置（影响绘制顺序/遍历顺序）
add_child(node)                        # 默认加到末尾（最上层）
$World.move_child(node, 0)             # 挪到第0位（最底层）

# 挂别人家
get_tree().root.add_child(ui_node)     # 挂根（常驻UI）
GlobalNode.battle_scene.add_child(fx)  # 挂到某单例场景
```

**⚠️ add_child 时机**：_init 里不能 add_child（自己还没进树）。要挂孩子等 _enter_tree 之后（_ready 最稳）。

## 19.5 遍历与查找节点

```gdscript
# 我的直接孩子们
for child in get_children():
	print(child.name)

# 含自己的全后代
for node in find_children("*", "Node2D"):   # 按模式+类型找
	print(node)

# 分组：批量管理的正道
add_to_group("enemies")                    # 入组
for e in get_tree().get_nodes_in_group("enemies"):
	e.queue_free()                          # 全体点名
get_tree().call_group("enemies", "take_damage", 10)   # 直接给全组发指令！

# 父亲与根
get_parent()
get_tree().root                            # /root

# 沿树向上找（找"我属于哪个战场"）
func find_owner_node() -> Node:
	var node := self
	while node != null:
		if node.is_in_group("battle_field"):
			return node
		node = node.get_parent()
	return null
```

## 19.6 节点常用属性速查（Node2D）

```gdscript
position            本地坐标(Vector2)（相对父）
global_position     世界坐标
rotation            旋转（弧度！）
rotation_degrees    旋转（度数，人话版）
scale               缩放 (Vector2)
z_index             渲染层级（同级中越大越靠上）
z_as_relative       层级是否累加父亲
modulate            染色/透明(Color)
visible             显隐
name                名字(String)
get_index()         在父亲那里的排行
```

```gdscript
# 节点常用方法
move_child(child, idx)      调整孩子顺序
get_path()                  拿自己的绝对路径
is_inside_tree()            是否已在树中
add_to_group(g)/is_in_group(g)/remove_from_group(g)
set_process(bool)           开关_process
duplicate()                 克隆整个节点（含孩子）
replace_by(node)            被顶替
```

## 19.7 场景切换与暂停

```gdscript
# 换场景（把当前主场景整个换掉）
get_tree().change_scene_to_file("res://levels/level2.tscn")
get_tree().change_scene_to_packed(preloaded_scene)

# ⚠️ change_scene是延迟执行的（帧末才换）
get_tree().change_scene_to_file("res://dead.tscn")
print("这行还是旧场景在跑")

# 暂停（整树暂停）
get_tree().paused = true                 # 全树_process/_physics_process停
get_tree().paused = false

# 暂停中的例外（暂停菜单自己要能响应）
pause_mode = Node.PROCESS_MODE_ALWAYS    # 我不受暂停影响
# 4.x写法：process_mode = Node.PROCESS_MODE_ALWAYS
```

**暂停模式**（process_mode）：

```
PROCESS_MODE_INHERIT      跟随父亲（默认）
PROCESS_MODE_PAUSABLE     受暂停控制
PROCESS_MODE_WHEN_PAUSED  只在暂停时运行（暂停菜单！）
PROCESS_MODE_ALWAYS       永不暂停（系统级UI）
PROCESS_MODE_DISABLED     永不运行
```

## 19.8 信号版节点操作速查（排错必备）

```gdscript
child_entered_tree(child)     我有了新孩子
child_exiting_tree(child)     我要失去孩子了
renamed()                     我改名了
tree_entered()                我进树了
tree_exited()                 我出树了
tree_exiting()                我正要出树（还能干活）
ready()                       我就绪了（= _ready() 的信号版）
```

---

# 第 20 章：生命周期函数全解

引擎在特定时机**自动调用**你的特定名字函数——它们是游戏运行的"心跳"。全部记住名字与时机。

## 20.1 总表

| 函数 | 时机 | 用途 |
|---|---|---|
| `_init()` | new() 瞬间 | 设置初值 |
| `_enter_tree()` | 进入场景树 | 早期初始化（少用） |
| `_ready()` | 进树+孩子就绪，仅一次 | **主初始化** |
| `_process(delta)` | 每渲染帧 | 视觉更新、计时 |
| `_physics_process(delta)` | 每物理帧(默认60) | 移动、物理 |
| `_input(event)` | 每个输入事件 | 全局输入 |
| `_shortcut_input(event)` | 快捷键 | 少用 |
| `_unhandled_input(event)` | 未被UI消费的输入 | 游戏操作 |
| `_unhandled_key_input(event)` | 同上键盘版 | 少用 |
| `_exit_tree()` | 离开场景树 | 清理 |
| `_notification(what)` | 各种系统通知 | 底层通知总线 |

## 20.2 _ready：唯一初始化圣地

```gdscript
func _ready() -> void:
	# 在这里：
	# ① 抓孩子引用（其实用@onready更好）
	# ② 连接信号
	$Button.pressed.connect(_on_start)
	# ③ 读取配置/存档
	load_settings()
	# ④ 初始状态
	hp = max_hp
	print("我准备好了，孩子共", get_child_count(), "个")
```

**_ready 顺序**：孩子的 _ready 先于父亲（父亲等所有孩子就绪才 ready）。所以"在父脚本 _ready 里访问孩子属性"是安全的。

## 20.3 _process 与 delta

每帧调用（默认60帧/秒，跟着显示器走）：

```gdscript
func _process(delta: float) -> void:
	# delta = 距上一帧的秒数（60帧时≈0.0167）
	rotating_icon.rotation += 2.0 * delta       # 每秒转2弧度
	# ⚠️ 不乘delta：好手机转得飞快，差手机爬行
```

**delta 为什么必须乘**——数学直觉：

```
60帧设备：每帧跑 1/60 秒 → 每帧转 2×(1/60) → 一秒共 60次×2/60 = 2弧度 ✔
144帧设备：每帧跑 1/144 秒 → 每帧转 2×(1/144) → 一秒共 144次×2/144 = 2弧度 ✔
不乘delta：144帧设备一秒转 144×2 = 288弧度 💥（每秒46圈！）
```

**_process 适用**：视觉（旋转、UI刷新、计时倒计）、轻量逻辑。
**不适合**：物理运动（用 _physics_process）、重计算（卡帧）。

按需开关（省性能）：

```gdscript
set_process(false)          # 关掉我的_process
set_process(true)           # 要用时再开
```

## 20.4 _physics_process：物理的心跳

固定频率（默认60/秒，项目设置可改），与渲染帧率无关：

```gdscript
func _physics_process(delta: float) -> void:
	# 移动/碰撞检测放这里（帧率无关、物理稳定）
	velocity.x = direction * speed
	move_and_slide()
```

**两兄弟对比**：

| | _process | _physics_process |
|---|---|---|
| 频率 | 渲染帧率（可变） | 固定（默认60） |
| delta | 实际帧间隔 | 恒定 1/60 |
| 放什么 | 视觉、UI、计时 | move_and_slide、RayCast、施力 |

**混用陷阱**：物理体在 _process 里改位置 → 和物理引擎"打架"（抖动/穿墙）。**CharacterBody2D 的移动一律 _physics_process**。

## 20.5 输入四件套

```gdscript
# _input：所有输入的第一站（连UI的都来）
func _input(event: InputEvent) -> void:
	if event is InputEventMouseButton and event.pressed:
		print("鼠标按下于", event.position)

# _unhandled_input：UI消费完剩下的（游戏操作放这）
func _unhandled_input(event: InputEvent) -> void:
	if event.is_action_pressed("attack"):
		attack()

# 键盘专用版
func _unhandled_key_input(event: InputEvent) -> void:
	if event.pressed and event.keycode == KEY_ESCAPE:
		toggle_pause_menu()
```

**event 的类型判断与字段**：

```gdscript
func _unhandled_input(event: InputEvent) -> void:
	if event is InputEventKey:
		print("键:", event.keycode, "按下:", event.pressed)
	elif event is InputEventMouseButton:
		print("鼠标键:", event.button_index, "位置:", event.global_position)
		if event.double_click:
			print("双击！")
	elif event is InputEventMouseMotion:
		print("移动:", event.relative)        # 相对位移（视角控制用）
	elif event is InputEventJoypadMotion:
		print("手柄轴:", event.axis, "值:", event.axis_value)
```

**动作（Action）优先于裸按键**：项目设置→输入映射 里定义 "jump"=空格/W/手柄A，代码只问动作名——跨设备天然支持（24章展开）。

## 20.6 _exit_tree 与清理职责

```gdscript
func _exit_tree() -> void:
	# 我被移出场景树（可能是场景切换、可能是free前）
	disconnect_all_signals()         # 断开我连的信号
	EventBus.player_died.disconnect(_on_died)
	timer_queue.clear()
	print("我下树了")
```

**清理清单**（谁连接谁断开；谁new谁free）：

```gdscript
extends Node
var bullet_pool: Array[Node] = []
var spawned_timer: Timer

func _ready():
	spawned_timer = Timer.new()           # 我造的
	add_child(spawned_timer)              # 挂我下面（我死它也死，自动清理✔）
	EventBus.score_changed.connect(_on_score)   # 我连的

func _exit_tree():
	EventBus.score_changed.disconnect(_on_score)  # 我要亲手断
```

## 20.7 _notification：底层通知总线

```gdscript
func _notification(what: int) -> void:
	match what:
		NOTIFICATION_READY:
			pass                        # 同_ready
		NOTIFICATION_EXIT_TREE:
			pass                        # 同_exit_tree
		NOTIFICATION_PAUSED:
			print("游戏暂停了")
		NOTIFICATION_UNPAUSED:
			print("游戏恢复了")
		NOTIFICATION_WM_CLOSE_REQUEST:
			save_before_quit()           # 玩家点窗口X（电脑版）
		NOTIFICATION_APPLICATION_PAUSED: # 手机切后台
			save_game()                  # 防杀进程丢档
```

**手机存档黄金时机**：`NOTIFICATION_APPLICATION_PAUSED`（切后台立刻存）。

## 20.8 帧循环全景图

```
每一帧（60Hz示意）：
┌────────────────────────────────────┐
│ 1. 输入事件 → _input → UI → _unhandled_input │
│ 2. _process(delta)  ← 所有节点按树序        │
│ 3. 物理步（若累计够1/60秒）                  │
│    → _physics_process(delta)               │
│    → 物理计算/碰撞                          │
│ 4. 场景树延迟操作（queue_free在这里执行）    │
│ 5. 渲染画面                                 │
└────────────────────────────────────┘
```

**单帧内的顺序保证**（重要直觉）：
- 父节点 _process 先于孩子（树序）；
- _process 全部跑完才轮到渲染 → "在_process里改位置，同帧渲染就生效"；
- queue_free 的对象活到本帧末 → "free后同帧仍可安全访问？不！is_instance_valid才可靠"。

## 20.9 练习

1. 把"每秒+1分"放 _process 里怎么写（用delta）？
```gdscript
var score := 0
var acc := 0.0
func _process(delta: float) -> void:
	acc += delta
	if acc >= 1.0:
		acc -= 1.0
		score += 1
```

2. 为什么移动代码不放 _process？
（答案：物理帧率固定、渲染帧率可变；物理体在渲染帧动会和物理引擎失步，造成抖动/穿墙。放 _physics_process。）

3. 玩家点X关闭窗口，哪个通知拦住并存档？
（答案：NOTIFICATION_WM_CLOSE_REQUEST（电脑）；手机切后台用 NOTIFICATION_APPLICATION_PAUSED。）

---

# 第 21 章：信号深入——观察者模式实战

## 21.1 信号解决什么问题

**没有信号的耦合地狱**：

```gdscript
# 玩家受伤了，要：UI掉血、屏幕闪红、音效、成就计数、AI仇恨……
class Player:
	func take_damage(n):
		hp -= n
		# 只能在Player里认识所有下游：
		get_node("/root/Main/UI").update_hp(hp)          # 认识UI
		get_node("/root/Main/Camera").shake()            # 认识相机
		get_node("/root/Main/Audio").play("hurt")        # 认识音频
		get_node("/root/Main/Achievements").count()      # 认识成就
		# 新需求=改Player源码=越改越烂
```

**信号 = 对象广播事件，不认识任何听众**：

```gdscript
class_name Player
signal damaged(amount: int, new_hp: int)        # 我只负责广播

func take_damage(n: int) -> void:
	hp -= n
	damaged.emit(n, hp)                         # 对天喊一嗓子，谁听见谁处理
```

```gdscript
# 各听众自己接线（互不相识，也都不认识Player内部）
player.damaged.connect(func(n, hp): ui.update_hp(hp))
player.damaged.connect(func(n, hp): camera.shake(0.2))
player.damaged.connect(func(n, hp): audio.play("hurt"))
# 新需求：加一行connect，Player一个字不改 ✔
```

**这就是观察者模式**：广播者（被观察者）只管喊，观察者们各自响应。**解耦**——两个模块协作却不互相依赖。

## 21.2 内置信号大全（高频30个）

```gdscript
# ---- 按钮/控件 ----
Button.pressed                       按下
Button.button_down / button_up       按住/松开瞬间
Button.toggled(pressed: bool)        开关型按钮变化
LineEdit.text_changed(new_text)      文本框内容变
LineEdit.text_submitted(text)        按回车
CheckBox.toggled(on)                 勾选变化
Slider.value_changed(v)              滑条变化

# ---- 节点生命 ----
Node.ready                           就绪
Node.tree_entered / tree_exited      进/出树
Node.child_entered_tree(node)        来了新孩子

# ---- 碰撞（Area2D）----
Area2D.body_entered(body: Node2D)    有物体进入我
Area2D.body_exited(body)             物体离开我
Area2D.area_entered(area)            另一个Area碰到我

# ---- 物理 ----
RigidBody2D.body_entered(body)       碰撞发生
CharacterBody2D 无内置碰撞信号（用move_and_slide后检查get_slide_collision）

# ---- 动画/计时 ----
Timer.timeout                        到点
AnimationPlayer.animation_finished(anim_name)   动画播完
Tween.finished                       补间完成
AudioStreamPlayer.finished           音效播完

# ---- 窗口 ----
get_tree().node_added(node)          全树任何节点诞生
get_viewport().size_changed()        窗口尺寸变
```

## 21.3 connect 的全部姿势

```gdscript
# 姿势一：连到方法（标准）
button.pressed.connect(_on_start_pressed)

# 姿势二：连到lambda（一行小事）
button.pressed.connect(func(): get_tree().quit())

# 姿势三：带额外参数（bind）
button.pressed.connect(_on_slot_clicked.bind(slot_index))
# 调用时：_on_slot_clicked(slot_index) —— bind的参数接在后面

# 姿势四：信号自带参数+bind追加
# item_selected(index) 信号 + bind("inventory") → _on_selected(index, "inventory")

# 姿势五：一次性连接（响一次自动断）
tween.finished.connect(_on_done, CONNECT_ONE_SHOT)

# 姿势六：挂起时自动断（对象销毁防悬空，4.x默认行为）
# CONNECT_REFERENCE_COUNTED 默认；手动管理用 CONNECT_PERSIST

# 检查与断开
signal.is_connected(callable)        已连接吗
signal.disconnect(callable)          断开
signal.get_connections()             全部连接列表
```

**重复连接坑**：

```gdscript
# 连两次 → 喊一次执行两次！
button.pressed.connect(_on_x)
button.pressed.connect(_on_x)
# 防御写法：
if not button.pressed.is_connected(_on_x):
	button.pressed.connect(_on_x)
```

## 21.4 自定义信号

```gdscript
class_name Player
extends CharacterBody2D

# 声明（可带类型标注的参数）
signal health_changed(new_hp: int, max_hp: int)
signal died
signal item_equipped(item: Dictionary)
signal leveled_up(new_level: int)          # 4.x可带默认参数

# 发射（emit）
func take_damage(n: int) -> void:
	hp -= n
	health_changed.emit(hp, max_hp)         # 带参广播
	if hp <= 0:
		died.emit()                          # 无参广播
```

**声明/发射/接收的参数必须对齐**：

```gdscript
# 接收方函数签名 = 信号参数（可少接尾部的，不能多）
func _on_health_changed(new_hp: int, max_hp: int) -> void:
	hp_bar.value = float(new_hp) / max_hp
```

## 21.5 await：把信号变成"时间点"

```gdscript
# 等信号（当前函数暂停，其他照跑）
func slow_death_sequence() -> void:
	sprite.play("die")
	await died_animation.animation_finished      # 等动画播完
	await get_tree().create_timer(1.0).timeout    # 再等1秒
	queue_free()                                   # 才消失

# 等任意信号（一步到位）
await get_tree().create_timer(2.0).timeout        # 等待2秒的极简写法
```

await 的本质：**把"回调风格"改写成"顺序风格"**。异步逻辑读起来像同步，可读性飞跃。

## 21.6 信号总线（EventBus）模式

**问题**：深层节点想通知另一个深层节点（玩家死亡 → 藏在5层下的GameOverUI），中间节点被迫层层转发。

**解法**：一个全局信号集线器（Autoload单例）：

```gdscript
# event_bus.gd —— 注册为Autoload，名 EventBus
extends Node

signal player_died
signal player_hp_changed(hp: int, max: int)
signal score_changed(new_score: int)
signal level_completed(level_id: int)
signal item_picked(item: Dictionary)
signal boss_spawned(boss_name: String)
signal game_saved
```

```gdscript
# 任何地方广播（不认识任何听众）
EventBus.player_died.emit()

# 任何地方收听（不认识任何广播者）
func _ready():
	EventBus.player_died.connect(_on_player_died)
	EventBus.score_changed.connect(func(s): label.text = str(s))
```

**EventBus 使用规范**（团队协作约定）：
1. 信号集中在 event_bus.gd 一处声明（好找好查）；
2. 命名"主语_动作过去式"：`player_died`、`item_picked`；
3. 广播只带**事实数据**（发生了什么），不带"指令"（该干什么）；
4. 跨模块通信用 EventBus；节点内部（父直接调子）直接调方法更简单，别过度信号化。

## 21.7 信号 vs 直接调用：选型

| 场景 | 用什么 |
|---|---|
| 一对一、上下级、同步执行 | 直接调用 `child.do_x()` |
| 一对多、广播事件 | 信号 |
| 跨模块、深层通信 | EventBus |
| "等某事发生再继续" | await 信号 |
| UI响应游戏数据 | 信号（或set/get钩子） |

**直觉**：喊"发生了什么"用信号；命令"你去干什么"用方法调用。

## 21.8 完整实战：血条系统（信号驱动UI）

```gdscript
# player.gd
class_name Player
extends CharacterBody2D

signal health_changed(hp: int, max_hp: int)
signal died

@export var max_hp := 100
var hp: int

func _ready() -> void:
	hp = max_hp
	health_changed.emit(hp, max_hp)      # 初始也广播一次（UI首刷）

func take_damage(amount: int) -> void:
	if hp <= 0:
		return                            # 死人不挨打
	hp = maxi(hp - amount, 0)
	health_changed.emit(hp, max_hp)
	if hp == 0:
		died.emit()

func heal(amount: int) -> void:
	if hp <= 0:
		return
	hp = mini(hp + amount, max_hp)
	health_changed.emit(hp, max_hp)
```

```gdscript
# hp_bar.gd —— 挂在UI上
extends ProgressBar

func _ready() -> void:
	EventBus.player_hp_changed.connect(_on_hp)

func _on_hp(hp: int, max_hp: int) -> void:
	value = float(hp) / max_hp * 100.0
	# 血量低变红
	self_modulate = Color.RED if hp < max_hp * 0.3 else Color.WHITE
```

```gdscript
# game_over_ui.gd
extends CanvasLayer

func _ready() -> void:
	EventBus.player_died.connect(show_game_over)
	# EventBus.player_hp_changed 也被血条用——多播的威力

func show_game_over() -> void:
	$Label.text = "游戏结束"
	self.visible = true
	get_tree().paused = true
```

Player 完全不知道 UI 的存在；UI 也只听 EventBus——**加新 UI（伤害飘字、低血警告音）零侵入**。

## 21.9 练习

1. 信号 `hit(target, damage, is_crit)`，写接收函数。
```gdscript
func _on_hit(target, damage: int, is_crit: bool) -> void: ...
```

2. 按钮按下要传"槽位号3"给处理器，connect 怎么写？
```gdscript
button.pressed.connect(_on_click.bind(3))
func _on_click(slot: int) -> void: ...
```

3. 为什么要 EventBus？直接全局单例调方法不行吗？
（答案：能但不优雅。信号是"广播事实"，监听方可选可增减、时序解耦；直接调用是"点对点命令"，广播者必须认识每个接收者。EventBus让双向都不相识。）

---

# 第 22 章：节点引用的所有姿势

"拿到那个节点"是日常操作的一半。全部姿势与取舍：

```gdscript
# ---- 姿势一：$ 语法糖（最常用）----
@onready var sprite := $Sprite2D          # 我的孩子"Sprite2D"
@onready var bar := $UI/HPBar             # 孙子：路径用/连

# ---- 姿势二：get_node ----
get_node("Sprite2D")                       # 等价$
get_node("UI/HPBar")
get_node("../Enemy")                       # 兄弟：先上再下
get_node("/root/Main/World")               # 绝对路径（从根）

# ---- 姿势三：安全版 ----
get_node_or_null("Sprite2D")               # 没有返回null，不崩
$Sprite2D                                  # 没有→直接崩！

# ---- 姿势四：unique name（%语法，场景里勾"作为唯一名称"）----
%HPBar                                     # 场景内直达，无视层级（UI最爱）

# ---- 姿势五：按类找 ----
get_tree().get_first_node_in_group("player")
find_child("HPBar", true, false)           # 按名找后代

# ---- 姿势六：从场景文件 ----
const PRELOADED := preload("res://ui/panel.tscn")
var panel = PRELOADED.instantiate()
```

**选择策略**：

| 场景 | 推荐姿势 |
|---|---|
| 自己的孩子/孙子 | `@onready var x := $路径` |
| 可能不存在的节点 | `get_node_or_null` + 判空 |
| 场景里唯一的UI | `%名称`（unique name） |
| 跨树的全局玩家 | 分组 `get_first_node_in_group("player")` |
| 兄弟/父级 | `get_parent()` / `get_node("../x")` |

**⚠️ 路径的脆弱性**：`$UI/HPBar` 写死了层级——场景里改个名、挪个层，代码崩。**少用深路径；常用引用集中@onready声明；跨模块用分组/信号/单例**。

**null 防御三连**（引用外部节点的标准开头）：

```gdscript
var target := get_tree().get_first_node_in_group("enemy") as Node2D
if target == null:
	return                              # 没目标，不干了
if not is_instance_valid(target):
	return                              # 目标死了，不干了
if not is_inside_tree():
	return                              # 自己都要没了
# —— 安全，开始干活 ——
look_at(target.global_position)
```

---
---

# 第四卷 · 引擎交互（续）

# 第 23 章：资源系统（Resource / load / preload）

> **本章目标**：理解 Godot"一切皆资源"的世界观；彻底吃透 `load()` / `preload()` 的区别与陷阱；
> 学会用自定义 Resource + `.tres` 文件做"数据驱动设计"（改数值零改代码）；
> 掌握资源共享语义这个新手最大暗坑；会用异步加载做加载屏；建立规范的资源目录习惯。

---

## 23.1 什么是资源：Godot 用一个类统一抽象一切资产

### 23.1.1 为什么需要"资源"这个概念

回忆一下第 13~17 章的面向对象：`class_name` 是图纸，`new()` 出来的是对象。
那么问题来了——**游戏里的"资产"呢**？

- 一张 `player.png` 贴图；
- 一段 `hit.wav` 音效；
- 一个 `enemy.tscn` 场景；
- 一款 `font.ttf` 字体；
- 一份你自己发明的"武器数值表"。

这些东西有 3 个共同点：

1. **它们在硬盘上有文件**（而不是代码里凭空 `new` 出来的）；
2. **它们会被很多地方共用**（100 个敌人共用一张贴图，没理由存 100 份）；
3. **它们需要被编辑器认识**（在 Inspector 面板里拖拽、编辑、保存）。

如果每种资产各搞一套加载/保存/共享机制，工程会碎成一片。Godot 的解法非常优雅：

> **把"一切资产"抽象成一个统一的基类：`Resource`（资源）。**

```
Object                      万物之祖
└── RefCounted              引用计数（自动内存管理）
    └── Resource            ★ 一切资产的统一抽象
        ├── Texture2D       贴图（.png/.jpg/.webp 导入后）
        │   └── ...
        ├── AudioStream     音频（.wav/.ogg/.mp3 导入后）
        │   └── AudioStreamWAV / AudioStreamOggVorbis ...
        ├── Font            字体（.ttf/.otf 导入后）
        │   └── FontFile / SystemFont
        ├── PackedScene     场景（.tscn/.scn）★ 场景也是资源！
        ├── Script          脚本（.gd）
        ├── Gradient        渐变
        ├── Curve           曲线
        ├── Shape2D / Shape3D  物理形状
        ├── Animation       动画数据
        ├── Theme           UI 主题
        ├── BitMap / Mesh / Material ...
        └── ItemData        ← 你自己 class_name Xxx extends Resource 的自定义资源
```

一句话总结：**在 Godot 里，"资源" = 存在硬盘上、可被共享、可在编辑器里编辑的数据对象。**

### 23.1.2 资源 vs 普通对象：一张表看清区别

`Resource` 和普通 `RefCounted` 对象都是对象，但"身份"完全不同：

| 对比维度 | 普通 RefCounted/Node 对象 | Resource 资源 |
|---|---|---|
| 出生方式 | 代码里 `new()` / `instantiate()` | 从文件 `load()` / `preload()`，或 `Resource.new()` |
| 存在形式 | 只在内存里 | 硬盘上有对应文件（`.png` `.tres` `.tscn`...） |
| 身份标识 | 没有路径概念 | 有 `resource_path`（唯一"身份证号"） |
| 共享性 | `new()` 两次 = 两个独立对象 | 同一路径 `load()` 两次 = **同一个对象**（23.7 细讲） |
| 编辑器可见性 | 不可见 | Inspector 可查看/编辑，可拖进 `@export` 槽位 |
| 序列化 | 需要自己写存档逻辑 | 天然支持：改属性 → `ResourceSaver.save()` 存回文件 |
| 生命周期 | 引用计数归零即销毁 | 被引用着就活着；有缓存（见 23.9） |
| 典型成员 | 业务逻辑、状态 | **纯数据** + 少量方法 |
| 例子 | `Player.new()`、`Enemy` 节点 | 一张贴图、一份武器数值表 |

### 23.1.3 入门例：第一次"摸"资源

```gdscript
extends Node

func _ready() -> void:
	# load() 把硬盘上的贴图文件读成一个 Texture2D 对象
	var tex: Texture2D = load("res://icon.svg")

	print(tex)                  # → Texture2D 对象（如 "Texture2D#[...]..."）
	print(tex.get_width())      # → 128（icon.svg 的宽度）
	print(tex.resource_path)    # → res://icon.svg（它的"身份证号"）

	# 资源也有属性、也可以改（改的是内存里这份，见 23.7 的坑）
	print(tex.resource_name)    # → ""（默认没名字，可以在编辑器里起）
```

### 23.1.4 实战例：三个敌人共用一张贴图

```gdscript
extends Node2D

func _ready() -> void:
	for i in 3:
		var s := Sprite2D.new()
		s.texture = load("res://assets/art/enemy.png")  # 三次 load，同一份纹理
		s.position = Vector2(100 + i * 80, 100)
		add_child(s)

	# 验证共享：三个 Sprite 用的是同一个对象
	var sprites := get_children()
	print(sprites[0].texture == sprites[1].texture)  # → true（这就是共享）
```

### 23.1.5 陷阱例：把资源当节点用

**错误写法**：

```gdscript
var tex := load("res://player.png")
add_child(tex)          # → 报错！tex 不是 Node
tex.position = Vector2(50, 0)   # → 报错！Texture2D 没有 position
```

**后果**：`Invalid call. Nonexistent function 'add_child' in base 'Texture2D'`。
资源是**数据**，不是**树上的活物**。数据不会动、不参与生命周期，它只负责"被谁引用"。

**修正**：资源放进"载体"节点里用——

```gdscript
var sprite := Sprite2D.new()   # 节点：载体（有位置、能进树）
sprite.texture = load("res://player.png")  # 资源：数据（被载体引用）
add_child(sprite)
sprite.position = Vector2(50, 0)           # 移动的是节点，不是资源
```

### 23.1.6 什么时候别用资源

- **运行时会频繁变化的游戏状态**（血量、坐标、金币数）：这是 Node/普通对象 + 变量的活儿。资源天生是"配置/资产"，把会话状态塞进资源会让缓存和共享语义把你咬得体无完肤（23.7）；
- **体积极小的临时数据**（一个坐标、一个颜色）：直接用 `Vector2`、`Color` 这类值类型，别为 2 个数字建一个 `.tres` 文件。

---

## 23.2 load() 与 preload()：一对双胞胎，性格迥异

### 23.2.1 为什么有两种加载方式

游戏加载资产有两个截然不同的时机：

1. **写代码的时候就确定了要用哪个文件**（主角贴图、主场景）——最好**进游戏前就准备好**，别等到用的时候才读硬盘；
2. **运行时才知道路径**（玩家选择了哪个皮肤、MOD 目录里有啥、关卡编辑器动态拼路径）——只能**运行时再加载**。

于是 Godot 提供了对应的两个函数：

| 特性 | `preload(path)` | `load(path)` |
|---|---|---|
| 求值时机 | **编译期**（脚本被解析时） | **运行期**（这行代码执行时） |
| 参数要求 | **必须是常量字符串字面量** | 任意运行时拼出来的 String |
| 能否放进 `const` | ✅ 可以（它本身就是常量表达式） | ❌ 不行（函数调用不是常量） |
| 加载失败 | **脚本直接编译报错**，游戏根本跑不起来 | 运行时报错/返回 null（可用 `exists()` 预判） |
| 启动开销 | 把加载成本提前到启动时（资源会随脚本常驻） | 首次调用那一刻才付成本 |
| 典型用法 | `const SCENE := preload("...")` | `load(path_from_save)` |

```gdscript
# preload：编译期，路径必须是写死的字符串
const ENEMY_SCENE: PackedScene = preload("res://scenes/enemy.tscn")
const ICON: Texture2D = preload("res://icon.svg")

# load：运行期，路径可以是变量、可以是拼出来的
func load_skin(skin_name: String) -> Texture2D:
	return load("res://skins/%s.png" % skin_name)
```

### 23.2.2 入门例：各自的最简用法

```gdscript
extends Node

const BULLET := preload("res://scenes/bullet.tscn")  # 编译期加载，常量

func fire() -> void:
	var b := BULLET.instantiate()    # 随取随用，零等待

func load_level(n: int) -> void:
	# 关卡编号运行时才知道（甚至可能存档里读来的）→ 只能 load
	var path := "res://levels/level_%02d.tscn" % n    # → "res://levels/level_03.tscn"
	var scene: PackedScene = load(path)
	add_child(scene.instantiate())
```

### 23.2.3 实战例：一个类里两种都用对

```gdscript
class_name WeaponSpawner
extends Node

# ① 已知且必用 → preload 成常量
const BASE_WEAPON := preload("res://data/weapons/sword_iron.tres")

# ② 玩家运行时才决定 → load
@export var weapon_folder: String = "res://data/weapons/"

func get_weapon(id: String) -> Resource:
	var path := weapon_folder + id + ".tres"
	if not ResourceLoader.exists(path):
		push_warning("武器不存在：%s，回退默认武器" % path)
		return BASE_WEAPON
	return load(path)
```

### 23.2.4 陷阱 1：条件加载 / 动态路径写成 preload

**错误写法**：

```gdscript
func load_texture_by_name(n: String) -> Texture2D:
	return preload("res://art/" + n + ".png")   # → 编译报错！
```

**后果**：`Preload` 的参数**必须是纯字符串字面量常量**，任何拼接、变量、格式化都会报：

```
Parse Error: Expected a constant string as the argument of preload().
```

这个报错会在你保存脚本的那一刻出现，游戏根本进不去——某种意义上是好事：**preload 逼你把错误提前暴露**。

**修正**：路径运行时才确定 → 改用 `load`，并加存在性检查：

```gdscript
func load_texture_by_name(n: String) -> Texture2D:
	var path := "res://art/" + n + ".png"
	if not ResourceLoader.exists(path):     # 先探路再加载（23.9）
		push_error("找不到贴图：" + path)
		return null
	return load(path)
```

顺带一提：有些"看起来像条件加载"的场景，其实可以改造成 preload——

```gdscript
# 错误思路：运行时用 if 挑 preload
func get_bg(kind: String) -> Texture2D:
	if kind == "forest":
		return preload("res://art/forest.png")
	else:
		return preload("res://art/desert.png")

# 这种写法能编译（每个分支都是字面量），但两张图都会被提前加载！
# 若种类多、图大，白白吃掉启动时间——见陷阱 2。
```

### 23.2.5 陷阱 2：preload 拖慢启动时间

**错误写法**（大杂烩脚本）：

```gdscript
# global_utils.gd —— 一个被所有场景引用的"工具箱"
extends Node

# 为了"方便"，把十张大图全 preload 进来……
const ART_1 := preload("res://art/huge_1.png")
const ART_2 := preload("res://art/huge_2.png")
const ART_3 := preload("res://art/huge_3.png")
const SCENE_A := preload("res://scenes/scene_a.tscn")   # 场景会连带它引用的所有资源！
const SCENE_B := preload("res://scenes/scene_b.tscn")
```

**后果**：

- 该脚本一被加载（比如它挂在 Autoload 上），**所有这些资源连同场景的依赖链全部进内存**；
- 玩家点开游戏 → 黑屏干等 10 秒 → 差评；
- 更隐蔽的是 `preload("...tscn")`：**场景会把它引用的贴图、音效、子场景一起拖进来**，一张 preload 牵出一整棵依赖树。

**修正原则**：

1. `preload` 只给**必然使用、且希望零等待**的常驻资源（主角贴图、常用子弹）；
2. 大资源、未必用的资源 → `load` + 按需调用，或干脆 `load_threaded_*` 异步（23.9）；
3. 工具类脚本里**永远不要**"为了方便"囤 preload。

### 23.2.6 陷阱 3：路径拼错

**错误写法**：

```gdscript
var a = load("res://Art/Enemy.png")     # 大写 A —— Windows 上能跑，导出到手机/黑屏报错！
var b = load("res://art/enemy.PNG")     # 扩展名大小写随手写
var c = preload("res://art/enemy.png ") # 末尾多了个空格
var d = load("res://art\\enemy.png")    # 反斜杠（Windows 习惯）
var e = load("art/enemy.png")            # 忘了 res:// 前缀（相对路径含义不同，见 23.3）
```

**后果分两种**：

- `preload` 拼错：**编译期立刻报错**，逼你修——体验好；
- `load` 拼错：**运行时**才炸，控制台输出 `Error: Couldn't load file`，返回值是 `null`。如果后面直接 `null.xxx`，就是一连串崩溃。

**修正**：

1. 用 `ResourceLoader.exists()` 先检查（23.9）；
2. **路径永远全小写**（Godot 官方建议资源文件名用 `snake_case`）；
3. 永远用 `res://` 开头的绝对路径，别玩相对路径花活；
4. 路径集中定义为常量，别在十处手打：

```gdscript
# paths.gd —— 集中管理路径，拼错只错一处
class_name Paths

const ART := "res://art/"
const WEAPONS := "res://data/weapons/"

static func weapon(id: String) -> String:
	return WEAPONS + id + ".tres"
```

### 23.2.7 什么时候别用哪个

- **别滥用 preload**：大文件、条件资源、未必用到的资源；
- **别滥用 load**：那种全项目必然用的小资源（主场景、图标），写成 `load` 意味着每次执行都做一次字符串路径解析 + 缓存查找（好在有缓存不会重复读盘，但语义上 preload 更能表达"这是常量"的意图）；
- **经验法则**：写代码时路径已经能写死 → `preload`；路径里有变量 → `load` + `exists()` 检查。

---

## 23.3 资源路径详解：res:// 与 user://

### 23.3.1 为什么要有两个"根"

游戏里的文件分两种身份，安全要求完全相反：

| 身份 | 你打包进游戏的内容 | 玩家机器上产生的数据 |
|---|---|---|
| 例子 | 贴图、场景、脚本、音效 | 存档、设置、截图、日志 |
| 能否修改 | ❌ 只读（打进包里） | ✅ 随便读写 |
| 路径前缀 | `res://` | `user://` |
| Windows 实际位置 | 项目根目录（导出后在包内） | `%APPDATA%\Godot\app_userdata\游戏名\` |
| Linux 实际位置 | 同上 | `~/.local/share/godot/app_userdata/游戏名/` |
| macOS 实际位置 | 同上 | `~/Library/Application Support/Godot/app_userdata/游戏名/` |

```gdscript
# res://：项目根目录
var tex := load("res://assets/art/player.png")

# user://：玩家的可写目录（存档标配，第 28 章细讲）
var save_path := "user://save_01.json"
	var f := FileAccess.open(save_path, FileAccess.WRITE)
	f.store_string("hello")
	f.close()

# 拿到 user:// 的真实物理路径（调试用）
print(ProjectSettings.globalize_path("user://"))  # → "C:/Users/你/AppData/.../游戏名/"
```

### 23.3.2 相对路径：能玩，但别玩

`load("art/enemy.png")` 这种不带协议前缀的"相对路径"，相对的是**当前脚本文件**所在目录：

```gdscript
# 本脚本位于 res://scripts/player/player.gd
# 同目录结构：
# res://scripts/player/player.gd
# res://scripts/player/art/enemy.png   ← 假设有这么个文件

var t = load("art/enemy.png")          # 相对路径 → res://scripts/player/art/enemy.png
var t2 = load("res://scripts/player/art/enemy.png")  # 等价的绝对路径
```

**强烈建议**：除非写"给别人用的插件/素材包"（相对路径对包内资源有意义），**自己项目里一律写 `res://` 绝对路径**。理由：

1. 脚本一旦移动目录，相对路径全部静默失效；
2. 代码评审时一眼看不出文件在哪。

### 23.3.3 常见资源扩展名速查表

在文件系统面板（FileSystem Dock）里，你会看到两类文件：

| 扩展名 | 是什么 | 用什么加载 |
|---|---|---|
| `.png` `.jpg` `.webp` `.svg` | 源贴图（导入后生成 `.ctex` 缓存） | `load()` → `Texture2D` |
| `.wav` `.ogg` `.mp3` | 音频源 | `load()` → `AudioStream`（wav → `AudioStreamWAV`，ogg → `AudioStreamOggVorbis`...） |
| `.ttf` `.otf` `.woff` | 字体源 | `load()` → `FontFile`（以 `Font` 使用） |
| `.glb` `.gltf` | 3D 模型 | `load()` → `PackedScene`/`GLTFState` |
| `.obj` | 3D 模型（简单格式） | `load()` → `Mesh` |
| `.res` | **二进制资源**（Godot 专有，体积小加载快） | `load()` |
| `.tres` | **文本资源**（人能读能改，Godot 专有） | `load()` |
| `.tscn` | **文本场景**（人能读的"场景图纸"） | `load()` → `PackedScene`，再 `.instantiate()` |
| `.scn` | 二进制场景 | 同上 |
| `.gd` | GDScript 脚本 | `load()` → `GDScript`（可 `.new()` 出对象） |
| `.json` `.txt` `.csv` | **纯数据文件，不是 Resource！** | `FileAccess` 手动读（第 28 章） |
| `.cfg` | Godot ConfigFile | `ConfigFile.load_file()` |

**关键区分**：`.tres` / `.tscn` / `.res` 是"资源"，能直接 `load()` 成对象；
`.json` / `.txt` / `.csv` 是"普通文件"，**不是**资源系统的一员，要走 `FileAccess`。

`.tres` 长什么样？（用文本编辑器打开一个）：

```ini
[gd_resource type="Resource" script_class="ItemData" load_steps=2 format=3]

[ext_resource type="Script" path="res://scripts/data/item_data.gd" id="1"]

[resource]
script = ExtResource("1")
item_name = "铁剑"
attack = 12
price = 100
```

它就是一份"属性清单"——`load()` 的工作就是照着这份清单，new 一个对象、把属性填进去。
**这就是 23.5 自定义资源的全部秘密：你定义类，Godot 负责把属性写成清单、再从清单还原对象。**

### 23.3.4 大小写陷阱（跨平台杀手）

- Windows 文件系统（NTFS）**不区分大小写**：`res://Art/Enemy.png` 能加载；
- 导出后的目标平台（Linux/Android/macOS/iOS/Web）**区分大小写**：同一行代码直接失败。

**现象**："在我电脑上明明是好的！"——这是新手玩家电脑 vs 开发者 Windows 机器的经典事故。

**修正**：所有文件名、文件夹名一律 `snake_case` 全小写；在 **项目设置 → 高阶 → 文件系统 → 确保**里可以用 Godot 4 的文件系统一致性检查；发布前在 Linux 上跑一遍冒烟测试。

### 23.3.5 陷阱例：把 user:// 当 res:// 用

**错误写法**：

```gdscript
# 想给玩家"上传自定义头像"功能
var avatar := load("res://screenshots/my_avatar.png")  # → res:// 是只读的！
```

**后果**：编辑器里也许碰巧能"看起来工作"（因为项目目录本来就可写），**导出后必炸**——导出包里的 `res://` 是只读的，玩家产生的文件必须放 `user://`。

**修正**：

```gdscript
# 玩家产生的文件 → user://
func load_player_avatar() -> Texture2D:
	var path := "user://avatars/my_avatar.png"
	if not FileAccess.file_exists(path):
		return null
	return load(path)    # load 同样适用于 user:// 路径！
```

---

## 23.4 Resource 类核心 API

`Resource` 作为所有资产的基类，自身提供了一批通用 API。这 5 个你迟早全用上。

### 23.4.1 速查表

| API | 类型 | 作用 |
|---|---|---|
| `resource_path` | 属性（String） | 资源的唯一路径"身份证号"，如 `res://a.tres`；代码 new 出来的资源是 `""` |
| `resource_name` | 属性（String） | 给人看的名字，编辑器/调试器里显示；不影响加载逻辑 |
| `resource_local_to_scene` | 属性（bool） | 为 true 时，该资源在"场景每次实例化"时都会复制一份独立副本 |
| `duplicate(copy: bool = false)` | 方法 | 复制资源；`copy=false` 浅拷贝，`copy=true` 连内部引用的子资源一起拷 |
| `take_over_path(path: String)` | 方法 | 给"无名"资源指派路径，并**顶替**缓存里该路径原有的资源 |

### 23.4.2 resource_path 与 resource_name

```gdscript
extends Node

func _ready() -> void:
	var tex := load("res://icon.svg")
	print(tex.resource_path)   # → "res://icon.svg"（从文件加载的资源自带身份证）

	var r := Gradient.new()     # 代码 new 的资源：没有身份证
	print(r.resource_path)     # → ""
	r.resource_name = "我的渐变"  # 起个名字（纯展示用）
	print(r.resource_name)     # → "我的渐变"
```

**用途**：

- `resource_path` 常用于调试（"这个资源到底是从哪来的？"）和把已加载资源存回原文件；
- `resource_name` 常用于给编辑器面板、`print` 输出加可读标签。

### 23.4.3 入门例：duplicate() 的两种深度

```gdscript
extends Node

func _ready() -> void:
	var orig := load("res://data/weapons/sword_iron.tres")

	var shallow: Resource = orig.duplicate()      # 浅拷贝（默认）
	var deep: Resource = orig.duplicate(true)      # 深拷贝
```

两者区别在"**资源里套资源**"时爆发。假设 `sword_iron.tres` 内部引用了一个 `icon.png`：

```
浅拷贝 duplicate()            深拷贝 duplicate(true)
┌─────────────┐               ┌─────────────┐
│ 副本(新)     │               │ 副本(新)     │
│  icon ────┐ │               │  icon ─────┐ │
└───────────┼─┘               └────────────┼─┘
            ↓                              ↓
      ┌──────────┐                   ┌──────────┐
      │ 原icon(共享)│                  │ 新icon(独立)│
      └──────────┘                   └──────────┘
```

- **浅拷贝**：副本的 `icon` 字段**还指着原来那份**。改原 icon，副本跟着变；
- **深拷贝**：把 icon 也复制一份，彻底独立。

**经验法则**：想"改了不影响别人"→ `duplicate(true)`；只想复制顶层字段、愿意共享子资源 → `duplicate()`。

### 23.4.4 实战例：武器数值模板改造——同一把刀，三把属性

```gdscript
extends Node

const SWORD := preload("res://data/weapons/sword_iron.tres")

func make_weapon_variants() -> Array:
	# 策划想要"铁剑+1/+2/+3"三件套，不想做三个 .tres
	var variants: Array[Resource] = []
	for i in 3:
		var w: Resource = SWORD.duplicate(true)   # 深拷贝，免得改到原版
		w.attack = SWORD.attack + (i + 1) * 3      # 假设字段 attack 存在
		w.item_name = "铁剑+%d" % (i + 1)
		variants.append(w)
	print(variants[0].attack)  # → 15（假设原版 12）
	print(SWORD.attack)        # → 12（原版没被动过 ✅）
	return variants
```

### 23.4.5 take_over_path()：运行时"调包"

`take_over_path` 做三件事：① 给资源绑定路径；② 把资源缓存里该路径原本的资源**顶掉**；③ 此后所有人 `load()` 这个路径，拿到的都是你的"新货"。

**经典用法——皮肤热替换**：

```gdscript
extends Node

func swap_player_skin(new_tex: Texture2D) -> void:
	# 让 new_tex 冒充 "res://art/player.png"
	new_tex.take_over_path("res://art/player.png")
	# 之后任何代码再 load 这个路径，都得到 new_tex
	var t := load("res://art/player.png")
	print(t == new_tex)   # → true 调包成功
```

### 23.4.6 陷阱例：take_over_path 的全局影响

**错误写法**：

```gdscript
func apply_pixel_art_filter(tex: Texture2D) -> void:
	tex.take_over_path(tex.resource_path)  # ??? 自己顶自己，看似无害
	# ... 一些修改
```

**后果**：`take_over_path` 是**全局操作**，影响所有后续 `load`。如果这里传入的是个副本，原本全项目共享的那份资源从此被替换，"只想改这一个 Sprite 的贴图"变成"全项目贴图都被改"，而且不可撤销。

**修正**：只在确实想要"全项目替换"时用它（换皮肤、MOD）；只改局部 → 用 `duplicate` 再把副本赋给目标：

```gdscript
func tint_one_sprite(sprite: Sprite2D, color: Color) -> void:
	var tex := sprite.texture.duplicate() as Texture2D
	# ... 对 tex 做修改（只影响这个副本）
	sprite.texture = tex
```

### 23.4.7 local_to_scene：场景局部资源

默认情况下，场景 `.tscn` 里引用的资源**全局共享**。勾选 `resource_local_to_scene`（或代码设置 `resource_local_to_scene = true`）后，**每实例化一次场景，该资源都会自动复制一份独立副本**。

```
                  ┌─ enemy.tscn 实例 A ──→ [血条贴图(独立副本A)]
enemy.tscn ───────┤
(内含血条贴图)     └─ enemy.tscn 实例 B ──→ [血条(独立副本B)]

勾选前：两个实例 ────────→ 共享同一份 [血条贴图]
```

**什么时候用**：场景里有个资源需要"每个实例各自改"（比如每个敌人自己的 `Curve` 巡逻曲线、自己染色的渐变）。这比每次手动 `duplicate` 省心。

```gdscript
extends CharacterBody2D

func _ready() -> void:
	# 前提：在编辑器里把 patrol_curve 勾上 Local to Scene
	# 这样每个敌人实例拿到的都是自己的曲线，互不干扰
	$PathFollower.curve = patrol_curve
	patrol_curve.add_point(Vector2(100, 0))  # 只影响本实例
```

---

## 23.5 自定义资源（重点）：把你的游戏数据变成"官方资产"

**这是本章最重要的一节**。学会它，你的游戏架构会上一个台阶。

### 23.5.1 为什么需要自定义资源

先看一个没有资源的痛案例。策划说："给游戏加 5 把武器。" 你写：

```gdscript
# ❌ 硬编码地狱
var weapon_names := ["木剑", "铁剑", "钢剑", "银剑", "圣剑"]
var weapon_attacks := [5, 12, 25, 40, 99]
var weapon_prices := [10, 100, 500, 2000, 10000]
var weapon_sprites := [preload(...), preload(...), ...]  # 还要同步维护 5 个数组！
```

四宗罪：

1. **加第 6 把武器 = 改 5 处代码**，漏改一处就错位（第 3 把的价格配到第 4 把头上）；
2. **策划不会写代码**，每调一个数值都要程序员动手；
3. **无法在编辑器里可视化编辑**，对着裸数组人肉核对；
4. **数据和行为搅在一起**，武器逻辑被数值绑架。

**自定义资源 + `.tres` 文件**把这一切变成：

- 数值存在独立文件里（`sword_iron.tres`），**策划在 Inspector 里点开就改**；
- 加武器 = 复制一个 `.tres` 文件改几个数，**代码零改动**；
- 数值和类型有编辑器保障（`@export_range(0, 100)` 拖不到 101）。

### 23.5.2 第一步：写一个"数据类"

```gdscript
# res://scripts/data/item_data.gd
class_name ItemData
extends Resource          # ★ 关键：继承 Resource，而不是 RefCounted/Node

enum Category { WEAPON, ARMOR, CONSUMABLE }

@export var item_name: String = "无名物品"        # 显示名
@export var icon: Texture2D                       # 图标（可以直接拖贴图进来！）
@export_category("数值")
@export_range(0, 999) var attack: int = 0         # 攻击力
@export_range(0, 99999) var price: int = 0         # 价格
@export var category: Category = Category.WEAPON
@export var description: String = ""              # 多行文本

## 计算含税售价（资源里也可以有方法，不只放数据）
func get_taxed_price(tax_rate: float = 0.1) -> int:
	return int(price * (1.0 + tax_rate))

func is_affordable(coins: int) -> bool:
	return coins >= price
```

**逐行拆解关键点**：

| 关键 | 作用 |
|---|---|
| `extends Resource` | 让它成为资源家族一员：可保存、可加载、可共享、可在 Inspector 编辑 |
| `class_name ItemData` | 全局注册类名：编辑器"新建资源"列表里会出现它（★ 必须有） |
| `@export` | 字段暴露到 Inspector——**这就是"自定义资源能在编辑器里编辑"的全部原理**（第 18 章注解全家桶在资源上同样生效） |
| `@export_range` / `@export_category` | 数值约束与分组，编辑体验直逼官方节点 |
| 枚举 + `@export` | Inspector 里自动变成下拉框 |
| `icon: Texture2D` | **资源套资源**：`ItemData` 里可以引用贴图、音效、甚至另一个 `ItemData`（合成配方） |

### 23.5.3 第二步：在编辑器里"新建资源 → 保存为 .tres"

完整点击流程（一步不落）：

```
① 打开"文件系统"面板（FileSystem / 文件系统）
② 右键你想要的文件夹（如 res://data/items/）
   → 选择"新建" → "新建资源..."（Create New Resource / 新建资源）
③ 弹出一个巨大的类型搜索框 → 输入 "ItemData"
   → 出现你的类（带你项目的图标样式）→ 双击它
④ 编辑器中央出现一个空 ItemData 的 Inspector（属性面板）
⑤ 填属性：item_name = "铁剑"，attack = 12，price = 100，
   icon 槽位直接把 player.png 从文件系统面板拖进去
⑥ 保存：点左上角"文件"菜单 → "保存"（或 Ctrl+S）
   → 选路径 res://data/items/sword_iron.tres → 保存
⑦ 完成！文件系统里出现 sword_iron.tres，图标是个"资源箱"
```

**ASCII 全流程图**：

```
脚本(item_data.gd)          编辑器                      硬盘
┌───────────────────┐   ┌────────────────────┐   ┌──────────────────────┐
│ class_name ItemData│→ │ 新建资源 → ItemData │→ │ sword_iron.tres      │
│ extends Resource   │   │ Inspector 里填属性  │   │ (清单式文本文件)      │
│ @export var ...    │   │ Ctrl+S 保存         │   │ 谁要谁 load          │
└───────────────────┘   └────────────────────┘   └──────────────────────┘
        图纸                    填数据                    存档成品
```

### 23.5.4 第三步：在 Inspector 里编辑（含引用别的资源）

`.tres` 保存后，**双击它**即可重新打开编辑。三种典型操作：

**操作 A：编辑普通字段**——直接点数值输入框改（`@export_range` 会强制范围）。

**操作 B：引用另一个资源**——`icon` 槽从"文件系统"面板把 `sword.png` 拖进去。

**操作 C：嵌入子资源（不存成单独文件）**——某些槽位（如 Gradient、Curve）点击可以"新建内嵌资源"，它会**内嵌**在 `.tres` 文件里而不是独立成文件：

```ini
# 一个带内嵌 Gradient 的 .tres 长这样：
[gd_resource type="Resource" script_class="ItemData" load_steps=3 format=3]

[sub_resource type="Gradient" id="Gradient_1"]
colors = PackedColorArray(1, 0, 0, 1, 1, 1, 0, 1)

[resource]
item_name = "彩虹剑"
glow/sub_resource = SubResource("Gradient_1")   ← 内嵌：存在同一个文件里
```

内嵌 vs 外置怎么选：**只有这一份资源用 → 内嵌；多处复用 → 存成单独文件再引用**。

### 23.5.5 第四步：在代码里加载使用

```gdscript
extends Node

const IRON_SWORD := preload("res://data/items/sword_iron.tres")

func _ready() -> void:
	print(IRON_SWORD.item_name)              # → 铁剑
	print(IRON_SWORD.attack)                 # → 12
	print(IRON_SWORD.get_taxed_price())      # → 110
	print(IRON_SWORD.is_affordable(99))      # → false（99 < 100）
```

### 23.5.6 第五步：让别的脚本用 @export 引用它

自定义资源最强的姿势——**拖进槽位，写代码时点补全，全程无字符串路径**：

```gdscript
class_name ShopSlot
extends Control

@export var item: ItemData        # ← Inspector 里出现一个 ItemData 槽

@onready var name_label: Label = $NameLabel
@onready var icon_rect: TextureRect = $IconRect

func _ready() -> void:
	# @export 变量被赋值发生在 _ready 之前，这里直接用
	name_label.text = "%s（%d 金）" % [item.item_name, item.price]
	icon_rect.texture = item.icon
```

在编辑器里把 `sword_iron.tres` 拖到 `ShopSlot` 节点的 `item` 槽——完事。
**代码里全程不知道文件路径存在**：想换商品？换个 `.tres` 拖进去就行。

### 23.5.7 实战例：完整背包数据（含资源数组）

```gdscript
# res://scripts/data/inventory_data.gd
class_name InventoryData
extends Resource

@export var items: Array[ItemData] = []      # 类型化数组（第 10 章）：只能装 ItemData
@export var max_slots: int = 20

func total_weight() -> int:
	var sum := 0
	for i in items:
		sum += i.price    # 假设用价格近似重量，纯演示
	return sum

func add(item: ItemData) -> bool:
	if items.size() >= max_slots:
		return false
	items.append(item)
	return true
```

在编辑器里建一个 `starter_inventory.tres`（类型 InventoryData），Inspector 的 items 数组里
点"添加元素"→ 每个槽又能拖 `.tres` 进去——**资源套资源，一层层拖出来整个初始背包配置**。

### 23.5.8 入门例：代码直接 new 一个资源

不经过文件，纯代码也能创建（比如程序化生成的临时数据）：

```gdscript
extends Node

func _ready() -> void:
	var apple := ItemData.new()     # 资源也是类，new 出来没问题
	apple.item_name = "苹果"
	apple.attack = 0
	apple.price = 5
	apple.category = ItemData.Category.CONSUMABLE
	print(apple.get_taxed_price(0.5))   # → 7（5 * 1.5 取整）

	# 还能反向保存成文件（23.6 会讲用途）
	var err := ResourceSaver.save(apple, "res://data/items/apple.tres")
	print(err == OK)   # → true（编辑器环境下保存成功）
```

### 23.5.9 陷阱例：忘写 class_name / 忘写 extends Resource

**错误写法 A：没写 class_name**

```gdscript
# item_data.gd
extends Resource
@export var item_name: String     # 没有 class_name ItemData
```

后果：编辑器"新建资源"列表里**搜不到这个类**，没法可视化建 `.tres`。
只能走野路子：先建一个空 Resource 再手动绑脚本——多两步且容易漏绑。
修正：**想用编辑器建资源的类，必须挂 `class_name`**。

**错误写法 B：没写 extends Resource**

```gdscript
# item_data.gd
class_name ItemData
extends RefCounted          # ← 不是 Resource 家族
@export var item_name: String
```

后果：这个类是普通对象，无法保存为 `.tres`、`@export` 槽拖不进去、`load()` 不认识它。
修正：`extends Resource` 是入场券。

**错误写法 C：在 Resource 里写 @onready**

```gdscript
class_name BadData
extends Resource
@onready var label = $NameLabel   # → 报错
```

后果：`Resource` **不是节点**，不在场景树里、没有孩子、没有 `_ready()` 时序（虽然资源
有自己的 `_init()` 构造）。`@onready` / `$路径` / `get_node()` 全是节点的世界。
修正：资源只放数据 + 纯计算方法；要碰节点，让外部节点来读资源。

### 23.5.10 什么时候别用自定义资源

- **一次性临时数据**：`var cfg := {"speed": 100}` 一个字典就够，别为 2 个字段建类 + `.tres`；
- **需要每帧变化的重度状态**（见 23.1.6）；
- **需要多态行为的复杂 AI**：资源放数据，行为放节点/状态机，别把整套 AI 逻辑塞进 Resource。

---

## 23.6 数据驱动设计：改数值零改代码

### 23.6.1 什么是数据驱动

> **数据驱动设计**：把"游戏数值/配置"从代码里抽出来，放进资源文件；代码只写**通用的玩法规则**，不写任何具体数值。

对比：

```
【代码驱动（每把武器都是特例）】            【数据驱动（代码只写一次）】
if weapon_name == "铁剑":                  # 砍一刀
	damage = 12                             func hit(target):
elif weapon_name == "钢剑":                    target.take_damage(w.damage)
	damage = 25                             # 武器数值？去 .tres 里看
elif weapon_name == "银剑":
	damage = 40
	# 加第 6 把武器 = 再写一个 elif...
```

**收益清单**：

1. 策划/美术自助调参，程序员专注玩法；
2. 平衡性测试（"铁剑攻击 ×10"试试手感）改文件即可，秒级迭代；
3. 换皮/做 DLC/出 MOD = 换一套 `.tres` 目录；
4. 数值有版本管理（`.tres` 是文本文件，git diff 直接看改了哪几行）。

### 23.6.2 完整模板：WeaponData（武器）

```gdscript
# res://scripts/data/weapon_data.gd
# 武器数据模板：自包含、可直接抄走改造
class_name WeaponData
extends Resource

## —— 基础信息 ——
@export var weapon_name: String = ""
@export var icon: Texture2D

## —— 战斗数值 ——
@export_category("战斗")
@export_range(0.1, 10.0, 0.1) var attack: float = 1.0     # 单发伤害
@export_range(0.05, 5.0, 0.05) var cooldown: float = 0.5   # 攻击间隔（秒）
@export_range(0, 1000) var ammo_capacity: int = 0         # 弹匣容量（0=近战/无限）
@export_range(1, 50) var pellets_per_shot: int = 1        # 一次射几发（霰弹枪）
@export_range(0.0, 1.0) var spread: float = 0.0           # 散布角度（弧度）
@export_range(0.0, 1000.0) var bullet_speed: float = 600.0

## —— 表现资源 ——
@export_category("表现")
@export var bullet_scene: PackedScene      # 子弹场景（资源套场景！）
@export var sound_fire: AudioStream       # 开火音效
@export var muzzle_flash: Texture2D       # 枪口火光

## —— 派生数值：方法而非重复存储 ——
## DPS = 单发伤害 × 每秒发数 × 单次弹丸数
func get_dps() -> float:
	var shots_per_sec := 1.0 / cooldown
	return attack * shots_per_sec * pellets_per_shot

## 开火间隔是否结束（把计时也交给数据的使用者传入）
func is_ready(last_fire_time: float, now: float) -> bool:
	return now - last_fire_time >= cooldown
```

**三个 `.tres` 示例**（在编辑器里建三个 WeaponData 资源照抄数值即可）：

| 文件名 | weapon_name | attack | cooldown | pellets | 效果定位 |
|---|---|---|---|---|---|
| `pistol.tres` | 手枪 | 10 | 0.4 | 1 | 稳定可靠 |
| `shotgun.tres` | 霰弹枪 | 6 | 0.9 | 8 | 近战爆发（DPS≈53） |
| `sniper.tres` | 狙击枪 | 120 | 1.8 | 1 | 一枪一个 |

**配套射手组件（消费数据的一方）**：

```gdscript
# res://scripts/player/weapon_component.gd
class_name WeaponComponent
extends Node
## 通用武器组件：只认 WeaponData，不认识任何具体武器名

signal fired

@export var weapon: WeaponData:               # ← 换武器 = 换一个 .tres 拖进来
	set(v):
		weapon = v
		if v != null and is_inside_tree():
			_apply_weapon()

var _last_fire_time: float = -INF

@onready var player: CharacterBody2D = get_parent()

func _unhandled_input(event: InputEvent) -> void:
	if event.is_action_pressed("fire"):
		try_fire()

func try_fire() -> void:
	var now := Time.get_ticks_msec() / 1000.0
	if weapon == null or not weapon.is_ready(_last_fire_time, now):
		return                                    # 数据说没冷却好，就不开火
	_last_fire_time = now
	_shoot()

func _shoot() -> void:
	# 数值全从资源读——代码里没有一个魔法数字
	for i in weapon.pellets_per_shot:
		var b := weapon.bullet_scene.instantiate()
		var angle := (player.rotation - weapon.spread / 2.0
				+ weapon.spread * float(i) / max(weapon.pellets_per_shot - 1, 1))
		b.rotation = angle
		b.speed = weapon.bullet_speed
		b.damage = weapon.attack
		b.global_position = player.global_position
		get_tree().current_scene.add_child(b)
	fired.emit()
	print("%s 开火！DPS=%.1f" % [weapon.weapon_name, weapon.get_dps()])
	# → "霰弹枪 开火！DPS=53.3"
```

### 23.6.3 完整模板：EnemyData（敌人）

```gdscript
# res://scripts/data/enemy_data.gd
class_name EnemyData
extends Resource

## —— 外观 ——
@export var enemy_name: String = "小怪"
@export var scene: PackedScene            # 敌人场景（23.8 会大量用）

## —— 数值 ——
@export_category("数值")
@export_range(1, 9999) var max_hp: int = 10
@export_range(0.0, 999.0) var speed: float = 100.0
@export_range(0.0, 999.0) var contact_damage: float = 1.0
@export_range(0.0, 999.0, 0.1) var detection_range: float = 200.0

## —— 掉落 ——
@export_category("掉落")
@export var loot_table: Array[DropEntry] = []     # 每项 {item, weight}

## 掉落命中一次随机
func roll_loot() -> Array[ItemData]:
	var results: Array[ItemData] = []
	for entry in loot_table:
		if randf() <= entry.chance:
			results.append(entry.item)
	return results

## 满血生成
func make_hp() -> int:
	return max_hp
```

**掉落条目：资源套资源再套资源**——

```gdscript
# res://scripts/data/drop_entry.gd
class_name DropEntry
extends Resource

@export var item: ItemData          # 掉什么（又是一个自定义资源！）
@export_range(0.0, 1.0) var chance: float = 0.5    # 掉落概率
@export_range(1, 10) var amount: int = 1            # 掉几个
```

### 23.6.4 陷阱例：在共享资源里存运行时状态

**错误写法**：

```gdscript
class_name EnemyData
extends Resource
@export var max_hp: int = 10
var current_hp: int = 10          # ← 运行时状态混进了数据资源！
```

```gdscript
func _ready() -> void:
	var data := load("res://data/enemies/slime.tres")
	data.current_hp -= 3          # 两只史莱姆共用一个 data
```

**后果**：所有加载 `slime.tres` 的史莱姆**共享同一份 `current_hp`**——你打 A 一拳，
B 也掉血；A 死了，全地图史莱姆一起暴毙。这是 23.7 大陷阱的预演。

**修正（数据驱动的铁律）**：

```
Resource（.tres）    → 只存"不变的配置"：max_hp、速度、掉落表
Node（敌人场景实例）  → 才存"运行时状态"：current_hp、当前目标
```

```gdscript
# enemy.gd —— 节点持有状态，资源只提供配置
class_name Enemy
extends CharacterBody2D

@export var data: EnemyData          # 配置：共享，无所谓
var current_hp: int                  # 状态：每个敌人各一份 ✅

func _ready() -> void:
	current_hp = data.max_hp         # 出生时从配置读初值
```

### 23.6.5 数据驱动的边界（什么时候别用）

- **强行为差异**：如果"武器"之间的区别不是数值而是机制（激光枪要蓄力、弓箭要拉弦），
  纯数据驱动会逼你在 WeaponData 里堆一堆 `is_charge_weapon` / `is_arrow` 标志位——
  此时更适合**类继承**（`ChargeWeapon extends WeaponData` 重写方法）；
- **冷启动的小游戏**：3 把武器的 game jam 作品，建 3 个类的成本 > 直接写常量；
- **数值高频变化**：见上，运行时状态去节点里待着。

---

## 23.7 资源的引用语义与共享（新手最大的坑）

### 23.7.1 为什么这里有大坑

回顾第 16 章"引用语义"：`RefCounted` 对象存在"盒子在栈上、东西在堆上"的两层结构，
赋值只是**复制盒子里那张地址条**。`Resource` 继承自 `RefCounted`，天然是引用语义。

但资源还有一个普通对象没有的狠角色：**全局缓存（ResourceCache）**。
`load()` 拿到路径后先查缓存——**同一路径永远返回同一个对象**：

```
                    ┌────────────────────────────────────┐
load("res://a.png") │  ResourceCache（全局缓存区）        │
        ┌────────→  │  "res://a.png" → [Texture2D 对象]   │ ← 第一次：读盘 + 建对象 + 存缓存
        │           └────────────────────────────────────┘
load("res://a.png") │
        └────────→  同一个对象（第二次：缓存命中，秒回）   │
```

**收益**：100 个敌人 `load` 同一张贴图，内存里只有一份，快且省。
**代价**：**你以为拿了"复印件"，其实拿到的是"原件"**——改一处，处处变。

### 23.7.2 入门例：亲眼验证共享

```gdscript
extends Node

func _ready() -> void:
	var a := load("res://icon.svg")
	var b := load("res://icon.svg")
	var c := load("res://icon.svg")

	print(a == b)         # → true（三个变量装的是同一个对象）
	print(a == c)         # → true
	print(a.get_instance_id() == b.get_instance_id())  # → true（实例ID都一样）

	# preload 也走同一个缓存
	var d := preload("res://icon.svg")
	print(a == d)         # → true（preload/load 共享同一份）
```

### 23.7.3 陷阱例（本章头号坑）：改一个，全体变

**错误写法**：想在游戏里实现"敌人被打了闪红"：

```gdscript
# enemy.gd
extends CharacterBody2D

func on_hit() -> void:
	# 想给贴图染个红色……
	var mat := $Sprite2D.material
	mat.set_shader_parameter("tint", Color.RED)   # ❌ 假设 material 是共享的
```

更直白的纯数据版本：

```gdscript
extends Node

const SLIME := preload("res://data/enemies/slime.tres")

func _ready() -> void:
	var e1 := SLIME            # 第一只史莱姆
	var e2 := load("res://data/enemies/slime.tres")   # 第二只史莱姆"自己加载"的

	e1.max_hp = 1              # 策划想测试"1滴血史莱姆"
	print(e2.max_hp)           # → 1 ！！！第二只也变 1 血了

	# 更恐怖的：连 .tres 文件本体都在内存里被改了
	# 如果此时有人在编辑器里 Ctrl+S，或者你调用了 ResourceSaver.save……
	# 文件里的默认值就永久变成 1 了！
```

**后果链**（这个坑的三层杀伤）：

1. **同屏全部实体联动**：改 A 的"配置"，B/C/D 全变（它们 `==` 同一个对象）；
2. **跨系统污染**：商店 UI 加载同一 `.tres` 显示数据 → 玩家打了一个怪，商店里的价格跟着变；
3. **意外写盘**：在共享资源上改 `@export` 字段后若被保存（编辑器运行中修改 + 某些保存路径），
   **配置文件本体被改**——这不是 bug，这是策划事故。

**为什么会中招**：代码里 `var e2 := load(...)` 看起来是"新拿了一份"，
人类直觉把 `load` 理解成"复制文件"，Godot 的语义是"按路径找对象，找到了就给你同一个"。

### 23.7.4 修正方案一：duplicate(true) 深拷贝

要"每个怪一份独立配置"→ 显式复制：

```gdscript
extends Node

const SLIME := preload("res://data/enemies/slime.tres")

func _ready() -> void:
	var e1: Resource = SLIME.duplicate(true)   # 深拷贝1
	var e2: Resource = SLIME.duplicate(true)   # 深拷贝2

	e1.max_hp = 1
	print(e1.max_hp)   # → 1
	print(e2.max_hp)   # → 10（原件的默认值，没被牵连 ✅）
	print(SLIME.max_hp)  # → 10（配置原件完好 ✅）
```

### 23.7.5 修正方案二：状态放节点（治本）

上一节 23.6.4 的铁律才是根治：**资源 = 只读配置；状态 = 节点变量**。
"1 血史莱姆"的正确姿势是给 `Enemy` 节点加 `@export var hp_override: int = 0`，
或者干脆复制一份 `slime_weak.tres`——**配置不同 = 不同的文件**，而不是"同一个文件的不同状态"。

### 23.7.6 共享 vs 复制：决策速查表

| 你想要的是…… | 用什么 |
|---|---|
| 全项目用同一份数据，改就一起改（贴图、音效、只读配置） | 直接 `load`/`preload`，**享受共享** |
| 同一场景的多个实例各有各的某个子资源 | `resource_local_to_scene = true` |
| 运行时改配置且不影响别人（临时数值调整） | `duplicate(true)` 深拷贝 |
| 每个实体自己的运行时状态（血量、 buff） | 别放资源！放节点变量 |
| 替换全项目某路径的资源（皮肤/MOD） | `take_over_path()` |

### 23.7.7 实战例：把"共享陷阱"变成"共享优势"

共享不总是坑，用对了就是**全局数据总线**。比如全局玩家的"货币"：

```gdscript
# game_config.gd —— 单例配置（配合第 34 章的 Autoload 更佳）
class_name GameConfig
extends Resource

@export var master_volume: float = 0.8
@export var language: String = "zh"

static var _cfg: GameConfig

static func get_config() -> GameConfig:
	if _cfg == null:
		if ResourceLoader.exists("user://settings.tres"):
			_cfg = load("user://settings.tres")     # 读玩家保存过的
		else:
			_cfg = load("res://data/default_config.tres")
	return _cfg
```

```gdscript
# settings_menu.gd
func _on_volume_slider_changed(value: float) -> void:
	GameConfig.get_config().master_volume = value    # 改共享对象

# audio_manager.gd
func apply_volume() -> void:
	AudioServer.set_bus_volume_db(0,
		linear_to_db(GameConfig.get_config().master_volume))  # 读到的一定是最新的
```

所有系统拿到的都是**同一个对象**——A 处改、B 处读，天然同步，连信号都省了。
（注意：这个模式要求大家都明确知道"这是共享的"——把这条潜规则写在类的注释里。）

---

## 23.8 场景也是资源：PackedScene + instantiate()

### 23.8.1 概念打通：.tscn 的真实身份

第 19 章说过"场景 = 一棵存起来的子树"。现在用资源视角再看一遍：

> **`.tscn` 文件本质是一个 `PackedScene` 资源——它是"打包好的一棵节点树"，是 Resource 的子类。**

```
Resource
└── PackedScene        ← 场景文件的本体
    内含：节点结构清单 + 各节点属性 + 引用的其他资源（贴图/脚本/子场景）
```

所以对场景能做的所有"资源操作"都成立：

```gdscript
var s: PackedScene = load("res://scenes/enemy.tscn")   # 加载"图纸"
print(s.resource_path)                                  # → res://scenes/enemy.tscn
print(s is Resource)                                     # → true（场景就是资源）
var copy := s.duplicate(true)                            # 复制图纸
```

`load` 场景拿到的是**图纸（PackedScene）**，不是活节点。要"照图纸造实物"用 `instantiate()`：

```
PackedScene（图纸，可复用）  --instantiate()-->  Node（活节点，可进树）
     load 一次                    ✦ 每次调用造一个新的
```

### 23.8.2 入门例：三行经典组合拳

```gdscript
extends Node

const ENEMY := preload("res://scenes/enemy.tscn")   # ① 编译期拿图纸

func _ready() -> void:
	var e := ENEMY.instantiate()     # ② 造一只（此时它还不在场景树里）
	add_child(e)                     # ③ 挂进树（挂上才进 _ready() 流程）
	e.position = Vector2(100, 50)    # ④ 属性随便改（这是本实例独有的）
```

**顺序很重要**：`instantiate()` 之后的节点**必须 add_child 才会执行它的 `_ready()`**；
而挂树之前先改属性，可以避免 `_ready` 里读到默认值——按需选择顺序。

### 23.8.3 实战例：封装一个 spawn 工具函数（模板）

手写三步组合拳十次就很烦了，而且**忘了 add_child 的节点会变成"孤儿节点"**（引擎会警告）。
封装一个 Spawner 单例（Autoload），从此一个函数生成一切：

```gdscript
# res://autoload/spawner.gd
# 通用生成器：挂到项目设置的 Autoload 里使用
class_name Spawner
extends Node

## —— 内置缓存：同一场景只 load 一次 ——
static var _cache: Dictionary = {}

static func get_scene(path: String) -> PackedScene:
	if not _cache.has(path):
		if not ResourceLoader.exists(path):
			push_error("场景不存在: " + path)
			return null
		_cache[path] = load(path)
	return _cache[path]

## 核心 API：在指定父节点下生成一个场景实例
## 返回生成出来的节点（失败返回 null）
static func spawn(path: String, parent: Node = null,
		xform: Transform2D = Transform2D.IDENTITY) -> Node:
	var scene := get_scene(path)
	if scene == null:
		return null
	var node := scene.instantiate()

	# 2D 节点应用变换；非 2D 节点忽略
	if node is Node2D:
		(node as Node2D).global_transform = xform

	if parent == null:
		parent = (Engine.get_main_loop() as SceneTree).current_scene
	if parent == null:
		push_error("没有可用的父节点，且当前场景为空")
		node.queue_free()     # 别留孤儿！
		return null
	parent.add_child(node)
	return node

## 便捷版：直接给坐标（2D 最常用）
static func spawn_at(path: String, pos: Vector2, parent: Node = null) -> Node2D:
	var node := spawn(path, parent, Transform2D(0.0, pos))
	return node as Node2D

## 便捷版：生成后延迟 N 秒自动销毁（子弹/特效标配）
static func spawn_temp(path: String, lifetime: float, parent: Node = null) -> Node:
	var node := spawn(path, parent)
	if node != null:
		var t := node.get_tree().create_timer(lifetime)
		t.timeout.connect(node.queue_free)
	return node
```

**使用示例**：

```gdscript
extends Node2D

func _ready() -> void:
	# 原地生成一只敌人
	Spawner.spawn_at("res://scenes/enemy.tscn", Vector2(200, 100))

	# 生成一发只活 2 秒的子弹
	Spawner.spawn_temp("res://scenes/bullet.tscn", 2.0)

	# 生成到指定父节点下
	Spawner.spawn("res://scenes/fx/explosion.tscn", $Effects)
```

### 23.8.4 陷阱例：拿 PackedScene 当节点用

**错误写法**：

```gdscript
const ENEMY := preload("res://scenes/enemy.tscn")

func _ready() -> void:
	add_child(ENEMY)             # ❌ 把"图纸"塞进树
	ENEMY.position = Vector2(50, 0)   # ❌ 图纸没有 position
	ENEMY.take_damage()          # ❌ 图纸没有你的自定义方法
```

**后果**：`Cannot add child of type PackedScene`（或隐式转换报错）。
图纸不是实物——就像你不能住进建筑效果图里。

**修正**：

```gdscript
func _ready() -> void:
	var enemy := ENEMY.instantiate()      # ✅ 先造实例
	add_child(enemy)
	(enemy as Node2D).position = Vector2(50, 0)
```

### 23.8.5 陷阱例：instantiate() 了却忘了 add_child

**错误写法**：

```gdscript
func spawn_bullet() -> void:
	var b := BULLET.instantiate()
	b.global_position = muzzle.global_position
	# ... 忘了 add_child(b) —— 或者提前 return 了
	if not can_fire:
		return          # ← b 已经 instantiate 但没挂树，泄漏为"孤儿"
```

**后果**：控制台反复出现 `Parent node is busy setting up children`不一定会出现，
但**一定会出现** `STATUS ORPHAN` 类泄漏警告（在调试器 → 监视里能看到 Orphan 节点数上涨）。

**修正**：先判断再 instantiate；或者写个"生成失败即销毁"的守卫（上面 Spawner 模板里已内置）：

```gdscript
func spawn_bullet() -> void:
	if not can_fire:
		return                          # ✅ 判断在前
	var b := BULLET.instantiate()
	b.global_position = muzzle.global_position
	get_tree().current_scene.add_child(b)
```

### 23.8.6 场景与资源的关系图（串起全章）

```
                       res://enemy.tscn
                              │ load / preload
                              ▼
                    ┌── PackedScene（Resource 的一种）
                    │        │ .instantiate()
                    │        ▼
                    │   Node（活节点）──── add_child ──→ 场景树
                    │        │
                    │        ▼ 引用
                    │   ┌── Texture2D（贴图，共享的 Resource）
                    │   ├── AudioStream（音效，共享）
                    │   └── EnemyData（你的 .tres，共享 + 可编辑）
                    └── 上面所有东西都在"缓存"里按路径唯一化
```

---

## 23.9 ResourceLoader 进阶：exists() 与异步加载

### 23.9.1 为什么需要 ResourceLoader 这个"管家"

`load()` / `preload()` 是"糖"，底层干活的其实是 **`ResourceLoader` 单例**。
直接用它，你能拿到糖给不了的能力：

| 能力 | 对应 API |
|---|---|
| 加载前探路（避免运行时报错） | `ResourceLoader.exists(path)` |
| **异步加载**（加载大资源不卡帧） | `load_threaded_request()` + `load_threaded_get()` |
| 查询异步进度 | `load_threaded_get_status()` |
| 取消异步加载 | `load_threaded_cancel()` |
| 列出目录下的资源 | `ResourceLoader.get_recognized_extensions_for_type()` 等辅助 API |

### 23.9.2 exists()：先探路再加载

**为什么需要**：`load` 一个不存在的路径会报错并返回 `null`，后续代码连锁崩溃。
MOD 加载、存档读取、玩家自定义内容——这些"路径不可信"的场景必须先探路：

```gdscript
extends Node

func safe_load(path: String) -> Resource:
	if not ResourceLoader.exists(path):
		push_warning("资源不存在：%s" % path)
		return null
	return load(path)

func _ready() -> void:
	print(ResourceLoader.exists("res://icon.svg"))   # → true
	print(ResourceLoader.exists("res://不存在.png"))    # → false（不报错！）
	var tex := safe_load("res://不存在.png")          # → 打印警告，tex = null
	print(tex)                                        # → null
```

还能指定类型检查：`exists(path, "Texture2D")`——路径存在但**不是贴图**时返回 `false`。

### 23.9.3 同步加载的卡顿问题（异步的动机）

```
玩家点击"进入第 3 关"
        │
        ▼ load("level_3.tscn")   ← 同步加载
┌───────────────────────────────────┐
│ 主线程停摆 800ms                  │  ← 屏幕冻结！玩家以为死机
│ （读盘 + 解析 + 建对象 + 子资源...） │
└───────────────────────────────────┘
        │
        ▼ 恢复运行
```

**异步加载**把"读盘+解析"丢到后台线程，主线程继续跑（渲染动画、转圈圈），
好了再"瞬间取货"。Godot 4 的异步接口是"下单-取货"两段式：

```gdscript
# ① 下单（后台线程开始加载，立即返回，不阻塞）
ResourceLoader.load_threaded_request("res://levels/level_3.tscn")

# ② 取货（若后台还没加载完，这一句会阻塞等待——所以要配轮询/进度查询）
var scene: PackedScene = ResourceLoader.load_threaded_get("res://levels/level_3.tscn")
```

### 23.9.4 实战模板：异步加载屏（Loading Screen，可直接抄）

思路：主场景之外挂一个"加载屏场景"，用它加载下一关，边加载边显示进度。

**场景结构**（`loading_screen.tscn`）：

```
LoadingScreen (Control)  ← 全屏，脚本如下
├── ColorRect            背景（盖住上一关）
├── ProgressBar          进度条（fill 模式）
└── TipsLabel (Label)     "加载中……小贴士：按住 Shift 可以冲刺"
```

**完整脚本**：

```gdscript
# res://scenes/ui/loading_screen.gd
# 通用异步加载屏：把本场景实例化并 add_child 到 /root 即可触发加载
class_name LoadingScreen
extends Control

## 要加载的场景路径（外部设置后再 start）
@export var target_path: String = ""
@export var tips: Array[String] = ["加载中……", "喝口水，马上就好", "小提示：空格是跳跃"]

var _progress: Array = []          # load_threaded_get_status 要求传入的数组（输出参数）
@onready var bar: ProgressBar = $ProgressBar
@onready var tip_label: Label = $TipsLabel

func _ready() -> void:
	process_mode = Node.PROCESS_MODE_ALWAYS      # 即使暂停也继续加载
	tip_label.text = tips[randi() % tips.size()]
	if target_path != "":
		start_load(target_path)

## 开始异步加载
func start_load(path: String) -> void:
	assert(ResourceLoader.exists(path), "目标场景不存在: " + path)
	target_path = path
	# ① 下单（use_sub_threads=true：多个子资源也并行加载，快）
	var err := ResourceLoader.load_threaded_request(path, "PackedScene", true)
	if err != OK:
		push_error("异步加载请求失败: %s" % path)
		_finish()
		return
	set_process(true)

func _process(_delta: float) -> void:
	# ② 每帧查询进度
	var status := ResourceLoader.load_threaded_get_status(target_path, _progress)
	# status 有 4 种：
	#   THREAD_LOAD_INVALID_REQUEST  无效请求
	#   THREAD_LOAD_IN_PROGRESS      加载中
	#   THREAD_LOAD_LOADED           完成（数据已就绪）
	#   THREAD_LOAD_FAILED           失败
	match status:
		ResourceLoader.THREAD_LOAD_LOADED:
			_finish()
		ResourceLoader.THREAD_LOAD_FAILED:
			push_error("加载失败: " + target_path)
			_finish()
		_:
			# _progress[0] ∈ [0.0, 1.0]（行内进度）
			bar.value = _progress[0] * 100.0

## ③ 取货并切换场景
func _finish() -> void:
	set_process(false)
	var scene: PackedScene = ResourceLoader.load_threaded_get(target_path)
	queue_free()                              # 先收起加载屏
	get_tree().change_scene_to_packed(scene)  # 官方切场景 API
```

**使用方式**：

```gdscript
# 在主菜单的"开始游戏"按钮回调里：
func _on_start_pressed() -> void:
	var ls := preload("res://scenes/ui/loading_screen.tscn").instantiate()
	ls.target_path = "res://levels/level_1.tscn"
	get_tree().root.add_child(ls)      # 加载屏盖上来，开始后台加载
	# 当前场景不用动，change_scene_to_packed 会自动清理
```

**注意三个坑**：

1. `load_threaded_request` 必须传**子线程加载模式参数**——Godot 4.2 起签名是
   `(path, type_hint, use_sub_threads, cache_mode)`；`use_sub_threads=true` 才能并行加载子资源；
2. **不要在取货前用同步 `load()` 加载同一路径**（两者会打架，可能死等）；
3. 加载中不要 `free` 发起请求的节点（用 `queue_free` 让它走完本帧流程）。

### 23.9.5 进度条为什么一直 0%？

**陷阱例**：

```gdscript
var status = ResourceLoader.load_threaded_get_status(path, progress)
print(progress[0])   # → 一直 0.1、0.1、0.1…… 最后直接 1
```

**原因**：`progress` 数组的第一格是**行内进度**——当场景只有"一个大依赖"（比如一张超大贴图）时，
引擎没法细分进度，只会在 0.1 附近躺平，加载完瞬间跳 1。这是**正常现象**，不是 bug。
对策：进度条 UI 上用"缓动假进度"（先自己涨到 90%，真实完成后补到 100%）——业界标配的小把戏。

### 23.9.6 什么时候别用异步

- 小资源（几 KB 的 `.tres`、单张贴图）：异步的开销（线程、轮询、代码复杂度）远大于收益；
- 需要严格时序的加载（"必须先有 A 才能建 B"）：异步会放大竞态问题；
- **经验法则**：同步加载超过 0.2 秒（肉眼可感知）的资源才值得上异步；关卡场景、大图集、长音频是典型候选。

---

## 23.10 资源组织最佳实践：目录结构与命名规范

### 23.10.1 为什么这件事重要（越早做越省命）

第 10 个 `.png` 出现时，"全扔 assets 目录"还能活；第 200 个文件、3 个程序员、
两次重构之后——乱目录直接吃掉你的开发时间：找不到文件、路径改到手抽筋、
重名文件覆盖、导入设置失控。**目录结构是项目的地基**。

### 23.10.2 两种主流目录方案

**方案 A：按"资源类型"分（小项目友好）**

```
res://
├── assets/                ← 美术/音频素材（按类型）
│   ├── art/
│   │   ├── characters/
│   │   └── tiles/
│   ├── audio/
│   │   ├── sfx/
│   │   └── music/
│   └── fonts/
├── data/                  ← 自定义资源 .tres（23.5/23.6 的家）
│   ├── items/
│   ├── weapons/
│   └── enemies/
├── scenes/                ← .tscn 场景
│   ├── player/
│   ├── enemies/
│   └── ui/
├── scripts/               ← .gd 脚本
│   ├── data/              ← Resource 数据类（item_data.gd 等）
│   ├── player/
│   └── ui/
└── autoload/              ← 单例（GameConfig、Spawner...）
```

**方案 B：按"游戏功能"分（大项目/DLC 友好）**

```
res://
├── core/                  ← 引擎级公共（工具、单例、全局配置）
├── player/
│   ├── player.tscn
│   ├── player.gd
│   ├── weapon_component.gd
│   └── art/               ← 只被玩家用的素材就放玩家目录里
├── enemies/
│   ├── scenes/
│   ├── scripts/
│   └── data/
└── ui/
    ├── menus/
    └── hud/
```

**怎么选**：

| 场景 | 推荐 |
|---|---|
| 独立小游戏 / Game Jam | 方案 A（直观、好找） |
| 多人协作 / 会拆 MOD 的中型项目 | 方案 B（功能自治，删一个文件夹 = 删一个系统） |
| 素材高度复用（一套 UI 贴图到处用） | 公共素材仍集中放 `assets/`，方案 B 里只放专属素材 |

### 23.10.3 命名规范速查表

| 对象 | 规范 | 示例 |
|---|---|---|
| 文件夹 | `snake_case`，全小写 | `enemy_boss/` ✅ `EnemyBoss/` ❌ |
| 贴图/音频源文件 | `snake_case`，含语义 | `player_idle.png`、`sfx_jump.wav` |
| 脚本文件 | 与类名对应的 `snake_case` | 类 `ItemData` → 文件 `item_data.gd` |
| `.tres` 资源 | `snake_case`，"主语_属性" | `sword_iron.tres`、`slime.tres` |
| `.tscn` 场景 | `snake_case`，一般可省后缀 | `main_menu.tscn` |
| 类名 | `PascalCase` | `WeaponComponent` |
| 函数/变量 | `snake_case` | `try_fire()` |
| 信号 | `snake_case`，过去式动词 | `died`、`weapon_changed` |

**三条硬纪律**：

1. **全小写**（大小写跨平台陷阱，23.3.4）；
2. **不用空格、不用中文**做文件名（部分工具链/git 跨平台会出幺蛾子，中文内容写在资源字段里没问题）；
3. **别叫 `new_final_v2_真的最后一版.png`**——用 git 管版本，文件名管内容。

### 23.10.4 陷阱例：乱目录的连锁惨案

**事故现场**（真实新手项目节选）：

```
res://
├── 新建文件夹/          ← 里面有什么？没人知道
├── 新建文件夹 (2)/
├── art/PNG/IMG_2024.png
├── art/PNG/IMG_2025.png
├── scripts/data/ItemData.gd      ← 大写I！Linux 导出后 preload 挂掉
├── aaa.tscn
└── 未命名.tres
```

**连锁后果**：

- `preload("res://scripts/data/ItemData.gd")` → Windows 正常，**安卓白屏**；
- 想换主角贴图 → 在 300 个文件里肉眼搜索哪张是主角；
- `aaa.tscn` 是啥？删了又不敢，留着又烦。

**修正**：哪怕项目已经乱了，现在花 20 分钟做三件事——统一小写、语义重命名、
归位目录。Godot 移动文件会自动修复引用（在编辑器内拖动文件，不要在系统文件管理器里移动！后者会把所有引用搞断）。

### 23.10.5 入门例：给现有项目建立资源习惯（清单）

```
□ 新建 data/ 目录，把所有"数值配置"类（ItemData/WeaponData/EnemyData）脚本放进去
□ 新建 data/ 下的子目录（items/weapons/enemies），对应类型的 .tres 放进去
□ .tres 文件名 = 内容可读（sword_iron.tres 而非 weapon_001.tres）
□ 单一职责：一个 .gd 文件一个类；一个 .tres 文件一份配置
□ 导入设置不乱改（.import 文件让 git 忽略，团队间导入设置靠 .import 提交同步）
```

### 23.10.6 什么时候可以不守规范

- 原型/实验代码（`test_1.gd` 随便，反正要扔）；
- 第三方插件目录（`addons/` 里的规范由插件作者定，别动）；
- 抄教程时先跑通再整理——**但整理必须真发生**，"回头再改"通常意味着永不。

---

## 本章小结

1. **Resource 是 Godot 对"一切资产"的统一抽象**：贴图、音频、字体、场景、脚本、
   自定义数据，全是 `Resource` 的子类——学一套 API，通吃所有资产类型。
2. **资源 vs 普通对象**：资源有路径身份证（`resource_path`）、可序列化到硬盘、
   被编辑器认识、同路径全局共享；普通对象 `new` 多少次就是多少个。
3. **`preload` 是编译期、`load` 是运行期**：preload 参数必须是字符串字面量，
   可进 `const`，失败在编译期报错；load 接受任意运行时字符串。
4. **preload 三大陷阱**：条件/拼接路径不能 preload（编译报错）；
   滥用 preload 拖慢启动（场景 preload 会连依赖树一起进内存）；
   路径拼错（preload 编译期炸 / load 运行期炸）。
5. **`res://` 只读、`user://` 可写**：打包资产用 res，玩家产生的数据（存档/设置/截图）用 user。
   相对路径相对"当前脚本"，自己项目一律用 `res://` 绝对路径。
6. **`.tres` 是文本资源、`.tscn` 是文本场景**，人能直接读改；`.json/.txt` 不是资源，走 `FileAccess`。
7. **核心 API 五件套**：`resource_path`（身份证）、`resource_name`（昵称）、
   `local_to_scene`（每实例一份副本）、`duplicate(true)`（深拷贝）、`take_over_path`（全局调包）。
8. **自定义资源三部曲**：`class_name Xxx extends Resource` 写数据类 →
   编辑器"新建资源"选类填属性 → Ctrl+S 存成 `.tres`。`@export` 是 Inspector 可编辑的全部原理。
9. **数据驱动铁律**：资源存"不变的配置"，节点存"运行时状态"——
   `max_hp` 放 `.tres`，`current_hp` 放节点；把状态塞进共享资源 = 全实体联动事故。
10. **同一路径 = 同一个对象**：`load` 两次拿到的是**同一个**，改一处处处变；
    想要独立副本就 `duplicate(true)`，想要每实例独立就 `local_to_scene`。
11. **场景（PackedScene）也是资源**：`load` 拿图纸，`instantiate()` 造实物，
    `add_child` 进活树——三步曲缺一不可，漏掉 add_child 就是孤儿节点。
12. **`ResourceLoader.exists()` 是运行时加载的安全带**；大资源用
    `load_threaded_request` + `load_threaded_get_status` + `load_threaded_get`
    做异步加载屏，进度数组第一格只反映粗粒度进度，"假进度缓动"是 UI 标配。
13. **目录与命名是工程地基**：文件/文件夹全小写 `snake_case`；方案 A 按类型分、
    方案 B 按功能分；在编辑器里移动文件让 Godot 自动修引用，别去系统资源管理器里拖。
14. **资源共享是把双刃剑**：理解它、声明它、然后要么享受它（全局配置总线），
    要么用 duplicate/节点状态绕开它——最怕的是"不知道自己在共享"。

---
---

# 第 24 章：输入系统

> **本章目标**：建立 Godot 输入系统的完整心智模型（InputMap 动作 → Input 轮询 → 事件回调三层）；
> 分清 `_input` 回调链的优先级顺序；掌握键盘/鼠标/手柄/触摸四类事件对象；
> 抄走两个实战模板（玩家自定义改键系统、PlayerInput 输入组件）；排掉输入系统的经典地雷。

---

## 24.1 输入三条通道总览：你到底该用哪个

### 24.1.1 为什么有三条通道

"玩家按了键盘"这件事，在游戏代码里有三种截然不同的处理姿势：

```
                          ┌──────────────────────────────┐
   硬件事件（OS）  ───→    │  Godot 引擎                  │
   键盘/鼠标/手柄/触摸      │  ① 打包成 InputEvent 对象     │
                          │  ② 对照 InputMap 翻译成"动作" │
                          │  ③ 更新 Input 单例的查询缓存  │
                          └──────────────────────────────┘
                                 ↓              ↓              ↓
                     【通道一】_input 系列回调   【通道二】Input 单例轮询
                     （事件驱动，抢第一手）      （每帧主动问，最常用）
                                 ↑
                     【通道零】InputMap 动作定义
                     （把"按键"翻译成"意图"，前两条通道的基石）
```

| 通道 | 形态 | 典型代码 | 适合做什么 |
|---|---|---|---|
| **① InputMap + 动作**（推荐） | 把物理按键绑定成"动作名" | `Input.is_action_pressed("jump")` | 99% 的游戏输入：跳跃/攻击/移动 |
| **② Input 单例轮询** | 每帧问"现在啥状态" | `Input.get_vector(...)`、`Input.is_key_pressed(...)` | 帧内持续状态：移动、瞄准 |
| **③ `_input` 系列回调** | 事件来了喊你 | `func _input(event):` | 稀疏事件：打字、截图键、调试快捷键 |

### 24.1.2 三者关系：层层翻译

```
玩家按下 键盘上的 "W"（物理按键）
        │
        ▼ InputMap 里定义了：动作 "move_up" ← 绑定 W 和 手柄十字键上
        │
   "move_up" 被按下 ←——————————————— ① 的价值：物理输入 → 逻辑意图
        │
        ├──→ ② Input.is_action_pressed("move_up")  你在 _process 里轮询
        └──→ ③ _unhandled_input(event)              你在回调里处理
```

**为什么强烈推荐"动作"而不是直接问按键**：

1. **改键免费**：把 W 换成方向键上？在 InputMap 里拖一下，代码零改动；
2. **多设备免费**：同一个动作绑键盘 + 手柄 + 触摸，玩家换设备代码无感；
3. **本地化免费**：不同键盘布局（QWERTY/AZERTY…）下逻辑不炸。

### 24.1.3 入门例：三条通道各写一次

```gdscript
extends Node

func _process(delta: float) -> void:
	# 通道②：轮询（每帧问）
	if Input.is_action_pressed("move_right"):
		position.x += 200.0 * delta

func _input(event: InputEvent) -> void:
	# 通道③：回调（有事件才来）
	if event.is_action_pressed("pause"):
		get_tree().paused = not get_tree().paused
```

而通道①（InputMap）本身在**项目设置 → 输入映射**里定义，见 24.2。

### 24.1.4 陷阱例：轮询用在"一次性事件"上

**错误写法**：

```gdscript
func _process(delta: float) -> void:
	if Input.is_action_just_pressed("fire"):
		shoot()
	if Input.is_action_just_pressed("fire"):
		play_empty_sound()     # 想在没子弹时补一句"咔哒"
```

**后果**：两个 `just_pressed` 判断在同帧都为 true 的话没问题，但新手常把它写进
**多个脚本**里各查一次——动作不同帧序、逻辑重复触发……这类"每帧轮询一次性事件"的代码
在**低帧率下丢输入**（两帧之间连按两次 = 只识别一次，见 24.3 帧序陷阱）。

**修正**：一次性事件用回调（`_unhandled_input` + `is_action_pressed(event)`），
或者保证"一个动作的逻辑只在一处查询"；连续状态才用轮询。

### 24.1.5 选择速查（背下来）

```
要做什么？                                → 用什么
────────────────────────────────────────────────────────
跳跃/开火/交互（一次性 + 改键需求）        → InputMap + is_action_just_pressed
移动/瞄准/长按蓄力（连续状态）            → InputMap + is_action_pressed / get_vector
手柄摇杆模拟量                            → Input.get_vector() / is_action_strength
打字输入（文本框）                        → LineEdit/TextEdit（内部处理）或 _input 里读 unicode
键盘任意键（截屏 F12、调试 F1）           → _input / _unhandled_key_input
鼠标精确交互（拖 UI、画笔）               → _gui_input / _input 里读 motion
```

---

## 24.2 InputMap 与动作：把按键翻译成意图

### 24.2.1 编辑器里定义动作（一次操作，终身受益）

路径：**项目设置（Project Settings）→ 输入映射（Input Map）→ 添加新动作（Add New Action）**

```
动作名（Action）: jump
    └── 事件列表:
         ├── Key  (物理) Space          ← 键盘空格
         ├── JoypadButton  A             ← 手柄A键
         └── JoypadMotion  Axis 1 (y-, 上推)  ← 左摇杆上推
Dead Zone（死区）: 0.5                  ← 摇杆防漂移（24.7 细讲）
```

建议的起步动作表（直接抄）：

| 动作名 | 建议绑定 | 用途 |
|---|---|---|
| `move_left/right/up/down` | A/D/W/S 或 方向键 | 4 向移动 |
| `move` | WASD/方向键（用 get_vector 时单独用） | 摇杆式移动 |
| `jump` | Space / 手柄A | 跳跃 |
| `fire` | 鼠标左键 / 手柄X | 攻击 |
| `interact` | E / 手柄B | 交互 |
| `dash` | Shift / 手柄RB | 冲刺 |
| `pause` | Esc / 手柄Start | 暂停 |

### 24.2.2 入门例：代码查询动作

```gdscript
extends Node2D

@export var speed: float = 300.0

func _process(delta: float) -> void:
	# get_vector：四方向动作 → 一个归一化二维向量（键盘也能用！）
	var dir := Input.get_vector("move_left", "move_right", "move_up", "move_down")
	position += dir * speed * delta        # 斜向也不会超速（自动归一化）

	if Input.is_action_just_pressed("jump"):
		print("跳！")       # 本帧刚按下
	if Input.is_action_just_released("jump"):
		print("松开")      # 本帧刚松开
```

### 24.2.3 用代码动态注册动作（完整模板）

**为什么需要**：动作是死的，需求是活的——

1. **运行时改键**（24.9 的主角）；
2. **MOD/外设**接入未知的动作；
3. **自动化测试**：代码模拟按键（`Input.action_press`）跑 CI。

完整模板（动态创建 `dash` 动作 + 绑定两个键）：

```gdscript
extends Node

func _ready() -> void:
	ensure_action("dash", [KEY_SHIFT, KEY_X])      # 动作不存在就创建并绑定

## 通用工具：确保动作存在且绑定指定按键
func ensure_action(action: String, keys: Array) -> void:
	# ① 动作不存在 → 创建（默认死区 0.5）
	if not InputMap.has_action(action):
		InputMap.add_action(action, 0.5)

	# ② 收集该动作现有的按键，避免重复绑定
	var existing := {}
	for ev in InputMap.action_get_events(action):
		if ev is InputEventKey:
			existing[(ev as InputEventKey).keycode] = true

	# ③ 逐个绑定新键
	for key in keys:
		if existing.has(key):
			continue                        # 已绑定，跳过
		var ev := InputEventKey.new()
		ev.keycode = key                    # 用 keycode 绑定
		InputMap.action_add_event(action, ev)

	# ④ 验证
	print(InputMap.has_action("dash"))            # → true
	print(InputMap.action_get_events("dash").size())  # → 2
```

**InputMap 核心 API 速查**：

| API | 作用 |
|---|---|
| `InputMap.add_action(name, deadzone)` | 新建动作（可带死区） |
| `InputMap.erase_action(name)` | 删除动作 |
| `InputMap.has_action(name)` | 动作是否存在 |
| `InputMap.action_add_event(name, event)` | 给动作加一个绑定 |
| `InputMap.action_erase_event(name, event)` | 移除一个绑定 |
| `InputMap.action_erase_events(name)` | 清空所有绑定 |
| `InputMap.action_get_events(name)` → Array[InputEvent] | 列出动作的所有绑定 |
| `InputMap.action_set_dead_zone(name, dz)` | 设置死区 |
| `InputMap.load_from_project_settings()` | 恢复成项目设置里的初始定义（改键"恢复默认"功能） |

### 24.2.4 陷阱例：改键忘了保存/没做"恢复默认"

**错误写法**：

```gdscript
# 改键界面：玩家选好新键
InputMap.action_erase_events("fire")
InputMap.action_add_event("fire", new_event)
# 就完了？游戏重启后，改键全丢！
```

**后果**：`InputMap` 的修改**只存在于内存**——项目设置里的默认表不会自动更新，
重启后玩家的改键消失（或者反过来：你把默认表改了，导致所有玩家跟着变）。

**修正**：改键必须持久化。简单方案存 `user://` 的 ConfigFile（完整实现见 24.9）：

```gdscript
const BINDINGS_PATH := "user://bindings.cfg"

func save_bindings() -> void:
	var cfg := ConfigFile.new()
	for action in ["fire", "jump", "dash"]:
		var events: Array[InputEvent] = []
		for ev in InputMap.action_get_events(action):
			events.append(event_to_text(ev))        # 自定义序列化（24.9 给完整实现）
		cfg.set_value("bindings", action, events)
	cfg.save(BINDINGS_PATH)

func load_bindings() -> void:
	# 启动时读回并应用（详见 24.9 完整模板）
	pass
```

另一个隐藏福利：`InputMap.load_from_project_settings()` 一行代码实现"恢复默认按键"。

### 24.2.5 什么时候别用 InputMap

- **需要"任何键"语义**（"按任意键继续"）：直接用 `_input` 收下一个事件即可，别注册 100 个动作；
- **纯 UI 键盘导航**：Control 节点的焦点系统已经内置方向键支持；
- **文本输入**：交给 LineEdit，别自己解析。

---

## 24.3 轮询 API 详解：pressed / just_pressed / just_released 三兄弟

### 24.3.1 三兄弟对照表（本章核心之一）

先讲"为什么有三个"：游戏输入的本质是两种问题——"**现在是什么状态**"和"**刚刚发生了什么变化**"。
一次按键 = 状态翻转两次（松→按下、按下→松开），"just"系列捕获的就是翻转的那一帧。

| API | 什么时候返回 true | 连续按住 5 帧时的表现 | 典型用途 |
|---|---|---|---|
| `is_action_pressed(a)` | 只要按着 | T T T T T | 移动、蓄力 |
| `is_action_just_pressed(a)` | **只有"从松到按"的那 1 帧** | T F F F F | 跳跃、开火 |
| `is_action_just_released(a)` | **只有"从按到松"的那 1 帧** | F F F F T | 松手取消/抛出 |

ASCII 时间轴（玩家在第 2 帧按下、第 6 帧松开）：

```
帧号:        1    2    3    4    5    6    7
物理状态:    松   按   按   按   按   松   松
is_action_pressed:     F    T    T    T    T    T    F
is_action_just_pressed: F    T    F    F    F    F    F      ← 只有第 2 帧！
is_action_just_released: F    F    F    F    F    T    F      ← 只有第 6 帧！
```

### 24.3.2 入门例：三种用法一次看完

```gdscript
extends Node2D

@export var speed := 300.0
var charge := 0.0

func _process(delta: float) -> void:
	# 按住：连续移动
	if Input.is_action_pressed("move_right"):
		position.x += speed * delta

	# 刚按：单次跳跃
	if Input.is_action_just_pressed("jump"):
		velocity.y = -400.0

	# 刚松：把蓄力值打出去
	if Input.is_action_pressed("fire"):
		charge += delta * 100.0              # 按住蓄力
	if Input.is_action_just_released("fire"):
		shoot(charge)                         # 松手发射，力度=蓄力
		charge = 0.0
```

### 24.3.3 帧序陷阱（重要）："just"只活一帧

**陷阱 A：在多帧频率的代码里查 just**

**错误写法**：

```gdscript
func _physics_process(delta: float) -> void:
	# 物理帧 60Hz，渲染帧 144Hz —— 两套频率！
	if Input.is_action_just_pressed("jump"):
		jump()
```

**后果**：`just_pressed` 的有效期绑定的是**当前帧（process 帧）**。物理帧和渲染帧不同步时，
144Hz 渲染 + 60Hz 物理下，有的 process 帧里"刚按下"标志已经被消费/覆盖，
**约 60% 的跳跃输入会被物理帧错过**——表现就是"按了跳有时没反应"。

**修正（两种选一）**：

```gdscript
# 修正 1：把一次性事件放到 _process / 输入回调里处理
func _process(_delta: float) -> void:
	if Input.is_action_just_pressed("jump"):
		request_jump()         # 只置一个标志
func _physics_process(delta: float) -> void:
	if _jump_requested:
		jump()
		_jump_requested = false

# 修正 2：自己记录上一帧状态（永不丢）
var _jump_held_prev := false
func _physics_process(_delta: float) -> void:
	var held := Input.is_action_pressed("jump")
	if held and not _jump_held_prev:
		jump()                # 用"边沿检测"替代 just_pressed
	_jump_held_prev = held
```

**陷阱 B：把 just_pressed 写进多个脚本重复消费**

```gdscript
# player.gd
func _process(_d): 
	if Input.is_action_just_pressed("interact"): interact_with_world()

# ui_manager.gd
func _process(_d): 
	if Input.is_action_just_pressed("interact"): close_dialog()   # ❌ 同一帧两处都触发
```

**后果**：一次按键，两个系统同时响应（既跟 NPC 说话又关了对话框）。
**修正**：一次性动作集中在一处判断，其余地方用信号广播结果（第 21 章）。

### 24.3.4 is_action_strength：模拟量（摇杆强度）

键盘是 0/1 的开关，摇杆是 0.0~1.0 的滑动条。`is_action_strength` 读的就是这个"力度"：

```gdscript
extends Node2D

@export var max_speed := 300.0

func _process(delta: float) -> void:
	# 摇杆轻推 = 慢速；推到底 = 全速（键盘玩家恒为 1.0）
	var strength := Input.get_action_strength("move_right") - Input.get_action_strength("move_left")
	position.x += strength * max_speed * delta

	print(Input.get_action_strength("fire"))   # 摇杆轻按 → 0.3 左右；按死 → 1.0；键盘 → 0 或 1
```

**注意**：`is_action_pressed` 在模拟量上有个隐藏行为——**只有超过死区（deadzone）才算"按下"**。
死区默认 0.5，可以在 InputMap 里调（24.7 讲为什么要死区）。

### 24.3.5 get_vector：四向合一（移动的终极姿势）

```gdscript
extends CharacterBody2D

@export var speed := 400.0

func _physics_process(_delta: float) -> void:
	# 参数顺序：负X、正X、负Y、正Y（左右上下）
	var dir := Input.get_vector("move_left", "move_right", "move_up", "move_down")
	velocity = dir * speed
	move_and_slide()

	# get_vector 的三大优点：
	# ① 键盘斜按（右+上）自动归一化 → (0.707, -0.707)，速度恒定
	# ② 摇杆直接返回模拟量方向
	# ③ 没输入时自动归零（含死区处理）
```

**陷阱例**：手写四方向不归一化：

```gdscript
# ❌ 斜向速度 = √2 × speed，比直线快 41%！
var dir := Vector2(
	Input.get_action_strength("move_right") - Input.get_action_strength("move_left"),
	Input.get_action_strength("move_down") - Input.get_action_strength("move_up")
)
velocity = dir * speed
```

**修正**：`dir = dir.normalized()`，或者直接用 `Input.get_vector()`（内部处理好了）。

---

## 24.4 事件回调链：_input → _gui_input → _shortcut_input → _unhandled_input

### 24.4.1 为什么有 5 条回调

一个输入事件到达引擎后，如果**谁都能处理**，就会乱套：点在 UI 上的鼠标既触发了按钮、
又让角色走了一步。Godot 的解法是**有序流水线 + "消费即停"**：

```
InputEvent 到达
      │
      ▼ ①_input（最先，什么都能看到：包括 UI 的输入）
      │      └─ 调用 viewport.set_input_as_handled() ？→ 是则终止
      ▼ ②_Viewport 的 GUI 处理（Control 节点的 _gui_input）
      │      └─ Control.accept_event() ？→ 是则终止
      ▼ ③_shortcut_input（全局快捷键，如菜单加速键）
      │      └─ set_input_as_handled ？→ 是则终止
      ▼ ④_unhandled_key_input（只收键盘，3D 编辑器习惯遗留，轻量）
      │      └─ set_input_as_handled ？→ 是则终止
      ▼ ⑤_unhandled_input（最后，游戏世界输入的主场）
      │      └─ set_input_as_handled ？→ 是则终止
      ▼ 丢弃（没人要）
```

**核心规则**：

1. **顺序固定**：`_input` > GUI > `_shortcut_input` > `_unhandled_key_input` > `_unhandled_input`；
2. **谁处理谁喊停**：喊停（handled）之后，后面的环节全部收不到——这就是"拦截"；
3. **`_unhandled_` 前缀的含义**："前面没人要的才轮到我"——**这正是游戏输入的黄金位置**。

### 24.4.2 各回调适合干什么（分工表）

| 回调 | 看得到什么 | 推荐用途 | 不推荐 |
|---|---|---|---|
| `_input` | 一切事件（最早） | 截图键、调试快捷键、录音原始流 | 游戏常规操作（会和 UI 打架） |
| `_gui_input` | 到达本 Control 的 GUI 事件 | 自定义按钮/拖拽 UI/画笔 | 游戏世界输入 |
| `_shortcut_input` | 未被处理的事件 | 全局快捷键（Ctrl+S 等菜单加速键） | 移动/攻击 |
| `_unhandled_key_input` | 未被处理的纯键盘 | 纯键盘的快捷操作 | 其他设备输入 |
| `_unhandled_input` | 前面没人要的一切 | **游戏世界的标准入口** | UI 相关 |

### 24.4.3 accept_event() 与 set_input_as_handled()

**两个"喊停"API 的区别**（新手常混）：

| API | 谁能用 | 效果 |
|---|---|---|
| `accept_event()` | **Control 节点**在 `_gui_input` 里调 | 标记本 GUI 事件已处理，阻止后续 GUI 父子传播 + 不再下传到 unhandled |
| `viewport.set_input_as_handled()` | 任何节点（`_input`/`_shortcut_input`/`_unhandled_input` 里） | 全局标记"此事件已被消费"，流水线当场终止 |
| `get_viewport().set_input_as_handled()` | 同上（标准写法） | 同上 |

### 24.4.4 入门例：体验顺序

```gdscript
extends Node

func _input(event: InputEvent) -> void:
	print("_input 收到: ", event)                    # ① 最先

func _shortcut_input(event: InputEvent) -> void:
	print("_shortcut_input 收到: ", event)            # ③

func _unhandled_key_input(event: InputEvent) -> void:
	print("_unhandled_key_input 收到: ", event)       # ④ 只有键盘

func _unhandled_input(event: InputEvent) -> void:
	print("_unhandled_input 收到: ", event)          # ⑤ 最后
```

点击鼠标一次，输出顺序：

```
_input 收到: InputEventMouseButton...
_shortcut_input 收到: InputEventMouseButton...
_unhandled_input 收到: InputEventMouseButton...
```

### 24.4.5 实战例：_input 拦截截图键，_unhandled_input 做游戏操作

```gdscript
extends Node

func _input(event: InputEvent) -> void:
	# F12 截图：无论玩家正在打字还是点菜单，都要响应 → _input（最优先）
	if event is InputEventKey and event.pressed and not event.echo:
		if (event as InputEventKey).keycode == KEY_F12:
			take_screenshot()
			get_viewport().set_input_as_handled()     # 拦截，别让它继续流

func _unhandled_input(event: InputEvent) -> void:
	# 游戏内攻击：如果玩家点在 UI 上，就不该攻击 → unhandled（等 UI 放行）
	if event.is_action_pressed("fire"):
		player.try_attack()
```

**对比出来的设计感**：截图要"抢"，攻击要"让"——两个需求用两个回调精准表达。

### 24.4.6 陷阱例：在 _input 里处理游戏操作（和 UI 打架）

**错误写法**：

```gdscript
# player.gd
func _input(event: InputEvent) -> void:
	if event.is_action_pressed("fire"):
		shoot()        # ❌ 玩家点"暂停按钮"时，角色也会开火！
```

**后果**：玩家点 UI 按钮 → `_input` **先于** GUI 收到这次点击 → 角色朝 UI 方向开火。
弹出的确认框上每按一次"确定"，后台就开一枪。

**修正**：游戏世界输入放 `_unhandled_input`——UI 消费掉的事件到不了这里：

```gdscript
func _unhandled_input(event: InputEvent) -> void:
	if event.is_action_pressed("fire"):
		shoot()        # ✅ 点 UI 时不会触发
```

**陷阱变体**：在 `_input` 里弹 UI：

```gdscript
func _input(event: InputEvent) -> void:
	if event.is_action_pressed("inventory"):
		toggle_inventory()     # ❌ 本帧后续的鼠标点击还会流进游戏世界
```

**后果**：打开背包的**同一帧**，玩家的这次点击还会继续在流水线里跑，
可能又点中地面的敌人触发攻击。**修正**：`_input` 里处理完就 `set_input_as_handled()`，
或者搬到 `_unhandled_input`。

---

## 24.5 键盘事件：InputEventKey 全解

### 24.5.1 事件对象解剖

每次按键，`_input` 回调里收到的就是一个 `InputEventKey`：

```gdscript
extends Node

func _input(event: InputEvent) -> void:
	if event is InputEventKey:
		var k := event as InputEventKey
		print("keycode       = ", k.keycode)         # 逻辑键码（当前布局下的字符键）
		print("physical      = ", k.physical_keycode) # 物理键码（键盘上"那个位置"）
		print("pressed       = ", k.pressed)          # true=按下 / false=松开
		print("echo          = ", k.echo)             # true=按住不放产生的"重复事件"
		print("unicode       = ", k.unicode)           # 按出的字符码（考虑Shift/大写/输入法）
		print("ctrl/shift/alt= ", k.ctrl_pressed, k.shift_pressed, k.alt_pressed)
		print("组合判定      = ", k.get_modifiers_mask() == KEY_MASK_CTRL)
```

按下 `A` 一次的输出：

```
keycode       = 65 (KEY_A)     physical      = 65 (KEY_A)
pressed       = true            echo          = false
unicode       = 97（字符 'a'）
```

### 24.5.2 physical_keycode vs keycode（改键与多布局的关键）

**为什么有两个键码**：世界上不止一种键盘布局。

```
QWERTY（美式）:   Q W E R T ...
AZERTY（法式）:   A Z E R T ...   ← 同样的"位置"，标签不同
```

| 属性 | 含义 | 同一个物理键在 QWERTY vs AZERTY 上 |
|---|---|---|
| `keycode`（逻辑码） | **按布局翻译后的"字符键"** | QWERTY 的 Q → `KEY_Q`；AZERTY 的同一位置 → `KEY_A` |
| `physical_keycode`（物理码） | **只看"键在键盘哪个位置"** | 两个布局下都是 `KEY_Q`（位置码） |

**选哪个？**

| 需求 | 用哪个 |
|---|---|
| **游戏按键 / 改键系统**（WASD 移动） | `physical_keycode`——**所有布局下位置一致**，法式玩家照样用"左上区域"移动 |
| 打字/文本类快捷（Ctrl+C 复制语义） | `keycode`——尊重布局，玩家按标签操作 |
| 修饰键组合（Ctrl/Shift/Alt） | 物理码（Ctrl 在哪都一样） |

**改键系统必须用 physical**：玩家在 AZERTY 键盘上按"QWERTY 的 W 位置"（他键盘上写着 Z），
如果存成 `keycode`（KEY_Z），到 QWERTY 布局的电脑上读档，就变成按 Z 键了——灾难。

### 24.5.3 入门例：组合键检测

```gdscript
extends Node

func _unhandled_key_input(event: InputEvent) -> void:
	var k := event as InputEventKey
	if k == null or not k.pressed or k.echo:
		return
	# Ctrl + Shift + R 重载配置
	if k.physical_keycode == KEY_R and k.ctrl_pressed and k.shift_pressed:
		print("重载配置！")
	# Ctrl + S 拦截（防误触发引擎的"保存场景"调试快捷键）
	if k.physical_keycode == KEY_S and k.ctrl_pressed:
		get_viewport().set_input_as_handled()
```

### 24.5.4 实战例：带修饰键筛选的快捷键分发器（模板）

```gdscript
# res://scripts/core/hotkey_manager.gd
# 简易快捷键管理：注册"物理键+修饰键"→回调，可直接扩展进你的项目
class_name HotkeyManager
extends Node

## 注册表：组合键字符串 → Callable
## 组合键格式："ctrl+shift+r"（小写；支持 ctrl/shift/alt/meta 前缀）
var _bindings: Dictionary = {}

func _ready() -> void:
	# 用法示例：注册几个全局快捷键
	register("ctrl+shift+r", _on_reload_config)
	register("ctrl+d", _on_toggle_debug)
	register("f1", _on_help)      # 无修饰键直接写键名

func register(combo: String, callback: Callable) -> void:
	_bindings[combo.to_lower()] = callback

func _unhandled_key_input(event: InputEvent) -> void:
	var k := event as InputEventKey
	if k == null or not k.pressed or k.echo:
		return
	var combo := _event_to_combo(k)
	if _bindings.has(combo):
		_bindings[combo].call()
		get_viewport().set_input_as_handled()     # 吃掉它，别漏到游戏世界

func _event_to_combo(k: InputEventKey) -> String:
	var parts: Array[String] = []
	if k.ctrl_pressed:  parts.append("ctrl")
	if k.alt_pressed:   parts.append("alt")
	if k.shift_pressed: parts.append("shift")
	if k.meta_pressed:  parts.append("meta")
	parts.append(OS.get_keycode_string(k.physical_keycode).to_lower())
	return "+".join(parts)

func _on_reload_config() -> void:  print("配置已重载")
func _on_toggle_debug() -> void:   print("调试界面开关")
func _on_help() -> void:           print("帮助面板开关")
```

### 24.5.5 echo：按住不放的"重复事件"

操作系统有"按键重复率"：按住 A，系统会连续发 `按下A` 事件（就像打字时的 aaaaa）。
这些重复事件被打上了 `echo = true` 的标记：

```gdscript
extends Node

func _input(event: InputEvent) -> void:
	var k := event as InputEventKey
	if k == null: return
	if k.pressed and not k.echo:
		print("真正的第一次按下")       # 只出现一次
	if k.pressed and k.echo:
		print("系统重复事件（按住不放）")  # 持续按住时刷屏
```

**什么时候要过滤 echo**：几乎所有"按下触发一次"的逻辑（跳跃、攻击、快捷键）都必须
`not event.echo`，否则按住跳跃键 = 原地疯狂蹦。**例外**：打字类场景（聊天框）反而欢迎 echo。

### 24.5.6 unicode：拿到"玩家真正想打的字符"

`unicode` 是考虑了 Shift/大写锁定/输入法之后的**字符码**，最适合文本场景：

```gdscript
extends Node

var typed := ""

func _input(event: InputEvent) -> void:
	var k := event as InputEventKey
	if k == null or not k.pressed or k.echo:
		return
	# 想收集玩家打出的字符（含大小写、Shift 符号）→ 用 unicode
	if k.unicode > 0:
		var ch := String.chr(k.unicode)
		typed += ch
		print(typed)         # 打 "G", "o" → "G" → "Go"
```

**陷阱例**：用 keycode 拼字符：

```gdscript
# ❌ 想实现"打字"效果
var ch = OS.get_keycode_string(k.keycode)   # "A"（永远大写！Shift符号也对不上）
# 玩家打 a 得到 "A"，打 Shift+1 在美式键盘想要 "!" 得到 "1"
```

**修正**：文本用 `k.unicode`；UI 打字请直接用 `LineEdit`（内部处理了输入法/删除/光标一切）。

### 24.5.7 键盘事件常见陷阱三连

**陷阱 1：忘了过滤 echo**（见 24.5.5）→ 按住 = 连发。

**陷阱 2：`_input` 里判断 keycode 但玩家是非英文布局**：

```gdscript
# ❌ 玩家用 AZERTY：按标签"Q"想退出，物理位置其实是 QWERTY 的 A
if event.keycode == KEY_Q: quit()
```

**修正**：游戏操作用 `physical_keycode`；或者干脆走 InputMap 动作（引擎已帮你选对了语义）。

**陷阱 3：按下与松开判断漏了 `pressed`**：

```gdscript
# ❌ 只判断了键码，没判断方向 → 松开的那次也触发！
if event is InputEventKey and (event as InputEventKey).keycode == KEY_SPACE:
	jump()
```

**后果**：按一下跳一次，松一下**又**跳一次（一次按键 = 两次跳跃）。
**修正**：`if k.pressed and not k.echo:`。

---

## 24.6 鼠标：点击、滚轮、移动、模式

### 24.6.1 事件对象解剖

鼠标相关的事件有三兄弟：

| 事件类 | 何时产生 | 关键字段 |
|---|---|---|
| `InputEventMouseButton` | 按下/松开/滚轮 | `button_index`、`pressed`、`double_click` |
| `InputEventMouseMotion` | 鼠标移动 | `relative`（相对位移）、`position`、`velocity` |
| `InputEventScreenTouch/Drag` | 触摸（24.8） | `index`（第几根手指）、`position` |

`button_index` 常用值速查（`MOUSE_BUTTON_*` 常量）：

```
MOUSE_BUTTON_LEFT     = 1    左键（最常用）
MOUSE_BUTTON_RIGHT    = 2    右键
MOUSE_BUTTON_MIDDLE   = 3    中键
MOUSE_BUTTON_WHEEL_UP = 4    滚轮上
MOUSE_BUTTON_WHEEL_DOWN = 5  滚轮下
MOUSE_BUTTON_XBUTTON1/2 = 8/9 侧键
```

**注意**：滚轮事件是 `pressed = true` 的"瞬发事件"（滚一下来一条，没有持续按住），且**没有配对的松开事件**。

### 24.6.2 入门例：识别点击/滚轮/双击

```gdscript
extends Node

func _unhandled_input(event: InputEvent) -> void:
	if event is InputEventMouseButton:
		var mb := event as InputEventMouseButton
		match mb.button_index:
			MOUSE_BUTTON_LEFT:
				if mb.double_click:
					print("双击！")
				elif mb.pressed:
					print("左键按下 @", mb.position)
				else:
					print("左键松开")
			MOUSE_BUTTON_WHEEL_UP:
				print("放大（滚轮上，一次一格）")
			MOUSE_BUTTON_WHEEL_DOWN:
				print("缩小")
```

### 24.6.3 InputEventMouseMotion：relative 与 position

```gdscript
extends Node

func _input(event: InputEvent) -> void:
	if event is InputEventMouseMotion:
		var mm := event as InputEventMouseMotion
		# position：这一帧鼠标在视口里的绝对坐标
		# relative：这一帧鼠标移动了多少（相对上一帧）
		print(mm.position, " 位移=", mm.relative)

		# 经典用法：右键拖动平移镜头（Figma/编辑器手感）
		if mm.button_mask & MOUSE_BUTTON_MASK_RIGHT:
			camera.position -= mm.relative * camera.zoom
```

`relative` 是"相机视角"游戏（第一人称/俯视射击瞄准）的命脉——**鼠标被捕获时
（见 24.6.5），`position` 不再有意义，`relative` 才是你唯一的信息来源**。

### 24.6.4 get_global_mouse_position 与坐标换算

```gdscript
extends Node2D

func _process(_delta: float) -> void:
	# 屏幕坐标系（视口左上角为原点，像素）
	var screen_pos := get_viewport().get_mouse_position()

	# 世界坐标系（被相机移动/缩放影响后的"游戏世界"坐标）
	var world_pos := get_global_mouse_position()

	# 两者换算：
	var world_pos2 := get_canvas_transform().affine_inverse() * screen_pos
	print(world_pos.distance_to(world_pos2))   # → 0（两种算法等价）

	print(screen_pos)    # → (640, 360) 玩家屏幕中间
	print(world_pos)      # → 随相机位置变化的真实世界坐标
```

**为什么有两套**：UI 用屏幕坐标（按钮永远在屏幕右上角），游戏世界用世界坐标
（"鼠标指向哪个敌人"）。**在 CharacterBody2D/Node2D 脚本里，默认该用 `get_global_mouse_position()`**。

**陷阱例**：用鼠标坐标做瞄准却不换算：

```gdscript
# ❌ 相机一动，射击方向全偏
var dir = (get_viewport().get_mouse_position() - global_position).normalized()
```

**修正**：

```gdscript
var dir = (get_global_mouse_position() - global_position).normalized()   # ✅ 世界坐标互减
```

### 24.6.5 鼠标模式：可见/隐藏/捕获

| 模式 | 常量 | 表现 | 典型游戏 |
|---|---|---|---|
| 可见 | `MOUSE_MODE_VISIBLE` | 正常鼠标 | 策略/RPG |
| 隐藏 | `MOUSE_MODE_HIDDEN` | 看不见但能点 | 看视频/演出 |
| 捕获 | `MOUSE_MODE_CAPTURED` | 鼠标锁在窗口中央，`relative` 驱动视角 | 第一人称/俯视射击 |
| 冲突区域 | `MOUSE_MODE_CONFINED` | 鼠标被困在窗口内但可见 | 窗口化 RTS |
| 隐藏+困住 | `MOUSE_MODE_CONFINED_HIDDEN` | 困住且隐藏 | 手柄为主+键鼠彩蛋 |

```gdscript
extends Node

func _ready() -> void:
	Input.mouse_mode = Input.MOUSE_MODE_CAPTURED

func _unhandled_input(event: InputEvent) -> void:
	# Esc 释放鼠标（暂停/开菜单时必备体验！）
	if event.is_action_pressed("pause"):
		toggle_mouse()

func toggle_mouse() -> void:
	Input.mouse_mode = (Input.MOUSE_MODE_VISIBLE
		if Input.mouse_mode == Input.MOUSE_MODE_CAPTURED
		else Input.MOUSE_MODE_CAPTURED)

	# 捕获期间读鼠标位置无意义（被锁中央），只读 relative：
	if event is InputEventMouseMotion:
		var mm := event as InputEventMouseMotion
		rotate_camera(mm.relative)
```

**陷阱例**：捕获模式忘了给玩家"逃生出口"：

```gdscript
# ❌ 进游戏就捕获鼠标，没绑定任何恢复方式
func _ready() -> void:
	Input.mouse_mode = Input.MOUSE_MODE_CAPTURED
```

**后果**：alt+Tab 玩家会抓狂；游戏崩溃时鼠标可能永远消失（下次启动引擎会恢复，
但玩家已经被劝退了）。**修正**：永远绑一个 Esc 处理（上面的 `toggle_mouse`），
并在暂停菜单打开时切回 `VISIBLE`。

---

## 24.7 手柄：按钮、摇杆、死区、震动、连接事件

### 24.7.1 事件对象解剖

| 事件类 | 说明 | 关键字段 |
|---|---|---|
| `InputEventJoypadButton` | 手柄按键 | `button_index`（JOY_BUTTON_*）、`pressed`、`pressure` |
| `InputEventJoypadMotion` | 摇杆/扳机模拟量 | `axis`（JOY_AXIS_LEFT_X 等）、`axis_value`（-1.0~1.0） |

轴与按钮速查（标准 Xbox 布局）：

```
摇杆轴（axis_value ∈ [-1,1]）               按钮（button_index）
JOY_AXIS_LEFT_X   左摇杆左右                  JOY_BUTTON_A / B / X / Y
JOY_AXIS_LEFT_Y   左摇杆上下                  JOY_BUTTON_LEFT_SHOULDER  LB
JOY_AXIS_RIGHT_X  右摇杆左右                  JOY_BUTTON_RIGHT_SHOULDER RB
JOY_AXIS_RIGHT_Y  右摇杆上下                  JOY_BUTTON_LEFT_STICK  左摇杆按下
JOY_AXIS_TRIGGER_LEFT  左扳机(0~1)             JOY_BUTTON_RIGHT_STICK 右摇杆按下
JOY_AXIS_TRIGGER_RIGHT 右扳机(0~1)             JOY_BUTTON_START / BACK
```

### 24.7.2 入门例：读摇杆原始值

```gdscript
extends Node

func _process(_delta: float) -> void:
	var lx := Input.get_axis("move_left", "move_right")      # 动作方式（推荐）
	# 或者直接读原始轴（调试/特殊用途）
	var raw_lx := Input.get_joy_axis(0, JOY_AXIS_LEFT_X)    # 0号手柄的左摇杆X
	print(raw_lx)   # → 摇杆静止时约 -0.02~0.05（漂移！），推到最左 = -1.0
```

**注意打印结果暴露的天机**：静止时摇杆不是 0——**硬件漂移**。这就是死区存在的原因。

### 24.7.3 死区处理模板（重要）

**问题**：摇杆静止时输出 ±0.05 左右的漂移；角色会"自己慢慢漂移"。
**死区**：小于某个阈值的输入一律视为 0。

```
原始摇杆值:   -1.0 ... -0.05 ... 0 ... 0.05 ... 1.0
                     ↑漂移区↑          ↑漂移区↑
死区处理（阈值0.2）: 全归零            全归零   线性放大 → 保持推满时=1.0
```

**方案一：InputMap 死区（配置层解决，推荐）**

动作的 Dead Zone 属性就是干这个的：`get_vector()`、`is_action_strength()` 自动应用死区。
简单情况把动作死区设 0.2 即可，**不用写代码**。

**方案二：代码死区（模板，精确控制手感）**

```gdscript
# res://scripts/core/joypad_utils.gd
# 摇杆工具：带死区的读取，支持"简单截断"与"径向缩放"两种策略
class_name JoypadUtils

## 策略A：简单截断——阈值内归零，阈值外原样
static func deadzone_simple(value: float, dz: float = 0.2) -> float:
	return 0.0 if absf(value) < dz else value

## 策略B：径向缩放（推荐）——阈值内归零，阈值外重新映射到 [0,1]
## 好处：摇杆在死区边界不会"跳变"，推满仍是 1.0，中间过渡平滑
static func deadzone_radial(value: float, dz: float = 0.2) -> float:
	var mag := absf(value)
	if mag < dz:
		return 0.0
	return signf(value) * (mag - dz) / (1.0 - dz)

## 完整摇杆向量版：向量整体考虑长度（比按轴处理更平滑）
static func apply_deadzone(vec: Vector2, dz: float = 0.2) -> Vector2:
	var mag := vec.length()
	if mag < dz:
		return Vector2.ZERO
	var scaled := (mag - dz) / (1.0 - dz)          # 新长度 ∈ [0,1]
	return vec / mag * scaled

## 演示：
static func demo() -> void:
	print(apply_deadzone(Vector2(0.1, 0.05)))   # → (0, 0)   漂移被吃掉
	print(apply_deadzone(Vector2(0.6, 0.0)))    # → (0.5, 0) 边缘平滑缩放
	print(apply_deadzone(Vector2(1.0, 0.0)))     # → (1, 0)   推满保持
```

**使用**：

```gdscript
extends CharacterBody2D

@export var speed := 400.0

func _physics_process(_delta: float) -> void:
	var raw := Input.get_vector("move_left", "move_right", "move_up", "move_down")
	# 如果觉得 InputMap 的死区不够细腻 → 套一层自己的
	velocity = JoypadUtils.apply_deadzone(raw, 0.25) * speed
	move_and_slide()
```

### 24.7.4 扳机震动：start_joypad_rumble

```gdscript
extends Node

func player_got_hit() -> void:
	# 参数：手柄序号、弱震强度(0~1)、强震强度(0~1)、持续秒数
	Input.start_joypad_rumble(0, 0.3, 0.8, 0.15)   # 中弹：短促一麻

func boss_roar() -> void:
	Input.start_joypad_rumble(0, 1.0, 1.0, 1.2)     # Boss 咆哮：长震

func _notification(what: int) -> void:
	# 注意：切窗口失焦时震动不会自动停，必要时手动清零
	if what == NOTIFICATION_APPLICATION_FOCUS_OUT:
		Input.stop_joypad_rumble(0)                # 玩家切走就别震了，礼貌
```

**陷阱例**：高频触发震动导致手柄"抽搐"：

```gdscript
# ❌ 每颗子弹命中都 start_joypad_rumble(0, 1, 1, 0.5)
# 机枪 10 发/秒 → 震动指令互相打断，手感稀碎
```

**修正**：按"事件强度分级 + 节流"设计：小命中不震、大事件才震；
或者用 `Input.get_joy_axis` 阶梯化。**触觉是稀缺资源，省着用**。

### 24.7.5 手柄连接/断开信号

手柄是热插拔的（玩家随时可能拔线/蓝牙断连），**支持手柄的游戏必须处理这两个信号**：

```gdscript
extends Node

func _ready() -> void:
	# Godot 4：Input 单例的信号
	Input.joy_connection_changed.connect(_on_joy_changed)

func _on_joy_changed(device: int, connected: bool) -> void:
	if connected:
		# 手柄名：Input.get_joy_name(device)
		print("手柄接入 #%d: %s" % [device, Input.get_joy_name(device)])
		print("当前手柄数：", Input.get_connected_joypads().size())   # → 1
		show_toast("已连接手柄，布局自动切换")
	else:
		print("手柄断开 #%d" % device)
		if Input.get_connected_joypads().is_empty():
			show_toast("手柄已断开，切换回键鼠操作")

func show_toast(msg: String) -> void:
	print("UI提示：", msg)
```

**配套设计**（做手柄支持时抄这三条）：

1. **UI 随设备切换**：最后输入设备是手柄 → 按钮提示显示 "A"；是键鼠 → 显示 "E"；
   实现方式：`_input` 里检查 `event is InputEventJoypadButton/Motion` 更新一个 `last_device` 变量；
2. **断连自动暂停**：手柄断了进暂停菜单（玩家手柄没电了还站着挨打，体验灾难）；
3. **UI 焦点切换**：手柄接入时把 UI 焦点交给第一个按钮（`grab_focus()`）。

---

## 24.8 触摸：InputEventScreenTouch / ScreenDrag

### 24.8.1 事件对象解剖

移动端（安卓/iOS）和 Windows 触屏会产生触摸事件：

| 事件类 | 何时产生 | 关键字段 |
|---|---|---|
| `InputEventScreenTouch` | 手指按下/抬起 | `index`（第几根手指，0=第一根）、`position`、`pressed` |
| `InputEventScreenDrag` | 手指在屏上移动 | `index`、`position`、`relative`（位移）、`velocity` |

**与鼠标事件的本质区别**：**多点**——`index` 告诉你是哪根手指，五根手指五个事件流。

> 小知识：项目设置里 `pointing_devices/emulate_mouse_from_touch` 默认开启——
> 触摸会**同时**模拟鼠标事件。做移动游戏时建议关掉模拟或统一只用触摸事件，避免双响应。

### 24.8.2 入门例：打印每一次触摸

```gdscript
extends Node

func _input(event: InputEvent) -> void:
	if event is InputEventScreenTouch:
		var t := event as InputEventScreenTouch
		print("手指#%d %s @%s" % [t.index, "按下" if t.pressed else "抬起", t.position])
		# 单指点击屏幕左下 → 手指#0 按下 @(120, 640)

	if event is InputEventScreenDrag:
		var d := event as InputEventScreenDrag
		print("手指#%d 拖动 → %s (本次位移 %s)" % [d.index, d.position, d.relative])
```

### 24.8.3 实战模板：单指拖拽（画笔/拖动面板手感）

```gdscript
# res://scripts/ui/drag_handler.gd
# 单指拖拽处理器：挂在 Control 上，实现"手指按到哪、节点跟到哪"
# 触摸、鼠标双兼容（桌面调试 + 手机真机都不误事）
class_name DragHandler
extends Control

signal drag_started
signal drag_ended

@export var target: Control              # 要拖动的节点（不填就拖自己）
var _dragging := false
var _offset := Vector2.ZERO              # 按下点相对节点左上角的偏移

@onready var _target: Control = target if target != null else self

func _ready() -> void:
	custom_minimum_size = Vector2(100, 100)   # 保证有可点区域（示例用）

func _input(event: InputEvent) -> void:
	# —— 触摸：单指（index==0）——
	if event is InputEventScreenTouch and (event as InputEventScreenTouch).index == 0:
		var t := event as InputEventScreenTouch
		if t.pressed and _hit(t.position):
			_begin_drag(t.position)
		elif not t.pressed and _dragging:
			_end_drag()

	# —— 触摸移动 ——
	if event is InputEventScreenDrag and _dragging:
		if (event as InputEventScreenDrag).index == 0:
			_move_to((event as InputEventScreenDrag).position)

	# —— 鼠标兼容（桌面调试）——
	if event is InputEventMouseButton:
		var mb := event as InputEventMouseButton
		if mb.button_index == MOUSE_BUTTON_LEFT:
			if mb.pressed and _hit(mb.position):
				_begin_drag(mb.position)
			elif not mb.pressed and _dragging:
				_end_drag()
	if event is InputEventMouseMotion and _dragging:
		_move_to((event as InputEventMouseMotion).position)

func _hit(screen_pos: Vector2) -> bool:
	# 把屏幕坐标转成"本节点局部坐标"再判断边界
	var local := _target.make_input_local(
		InputEventMouseButton.new()) # 占位（make_input_local 只用 transform）
	var rect := Rect2(_target.global_position, _target.size * _target.scale)
	return rect.has_point(screen_pos)

func _begin_drag(pos: Vector2) -> void:
	_dragging = true
	_offset = pos - _target.global_position    # 记住"抓取点"，避免拖动时节点跳到指尖左上角
	drag_started.emit()

func _move_to(pos: Vector2) -> void:
	_target.global_position = pos - _offset    # 减去偏移 = 节点跟着手指平滑走

func _end_drag() -> void:
	_dragging = false
	drag_ended.emit()
```

**要点**（照抄时的检查清单）：

- **记录 `_offset`**：不记录的话，手指按下的一瞬间节点"瞬移"到指尖位置（左上角对齐），非常廉价；
- **`index == 0`**：单指逻辑要过滤"第二根手指"（放大手势会乱入）；
- **桌面调试兼容**：同一套逻辑里同时处理 `ScreenTouch/Drag` 与 `MouseButton/Motion`，
  才能在编辑器里测、在手机上跑。

### 24.8.4 双指缩放手势（进阶预告）

多点触控的看家本领——两根手指，读 `index` 区分、算两点距离变化：

```gdscript
extends Node2D

var _touches: Dictionary = {}       # index → position
var _start_dist := 0.0

func _input(event: InputEvent) -> void:
	if event is InputEventScreenTouch:
		var t := event as InputEventScreenTouch
		if t.pressed:
			_touches[t.index] = t.position
		else:
			_touches.erase(t.index)
		# 恰好两根手指时记录初始间距
		_start_dist = dist() if _touches.size() == 2 else 0.0

	if event is InputEventScreenDrag:
		var d := event as InputEventScreenDrag
		if _touches.has(d.index):
			_touches[d.index] = d.position
		if _touches.size() == 2 and _start_dist > 0.0:
			# 两指间距变大 → 放大；变小 → 缩小
			$Camera2D.zoom *= dist() / _start_dist
			_start_dist = dist()

func dist() -> float:
	var arr := _touches.values()
	return (arr[0] as Vector2).distance_to(arr[1] as Vector2)
```

**陷阱例**：忽略 `index` 直接用最后一次触摸：

```gdscript
# ❌ 两根手指操作时，抬起的"另一根"触发错误的拖动
if event is InputEventScreenDrag:
	move_panel((event as InputEventScreenDrag).position)
```

**后果**：双指操作时两个 Drag 流交叉，面板瞬移乱跳。
**修正**：永远先用 `index` 把"关心的那根手指"筛出来。

---

## 24.9 实战模板 A：玩家自定义改键系统（完整可直接抄）

### 24.9.1 需求拆解

一个合格的改键系统 = 5 块能力：

```
① 列表展示动作名 + 当前绑定键（"跳跃 —— 空格"）
② 点击某行 → 进入"监听状态"（"请按新按键……"，Esc 取消）
③ 玩家按下一个键 → 捕获该键
④ 冲突检测：这键是不是已经被别的动作占了？占用了怎么办？
⑤ 保存到 user:// + 启动时加载；一键"恢复默认"
```

### 24.9.2 完整类：RebindManager（核心逻辑，与 UI 无关）

```gdscript
# res://scripts/core/rebind_manager.gd
# 改键管理核心：负责捕获、冲突检测、持久化。UI 层只管展示与调用。
class_name RebindManager
extends Node

signal rebinding_started(action: String)      # 开始监听（UI 显示"请按键…"）
signal rebinding_finished(action: String, ok: bool)  # 结束（ok=成功/取消）
signal conflict_detected(action: String, other_action: String)  # 发现冲突

const SAVE_PATH := "user://bindings.cfg"
const SECTION := "bindings"

## 允许玩家改键的动作白名单（也是 UI 列表的数据源）
## 写成 {动作名: 显示名}，展示给玩家的用中文，逻辑里只用英文动作名
@export var rebindable_actions: Dictionary = {
	"jump": "跳跃",
	"fire": "攻击",
	"dash": "冲刺",
	"interact": "交互",
	"pause": "暂停",
}

var _listening_action: String = ""           # 空串 = 不在监听状态
var _default_snapshot: Dictionary = {}        # 默认绑定快照（供"恢复默认"）

func _ready() -> void:
	# ① 记住引擎默认（项目设置里的）绑定 —— 注意深拷贝事件对象
	for action in rebindable_actions:
		_default_snapshot[action] = InputMap.action_get_events(action).duplicate()
	load_bindings()

# —————————————————————— 监听流程 ——————————————————————

## UI 点击某行时调用：开始监听该动作的新按键
func start_listening(action: String) -> void:
	assert(rebindable_actions.has(action), "动作不在可改键白名单: " + action)
	_listening_action = action
	rebinding_started.emit(action)

func _unhandled_key_input(event: InputEvent) -> void:
	_process_catch(event)

func _unhandled_input(event: InputEvent) -> void:
	# 鼠标/手柄键也支持改绑
	_process_catch(event)

func _process_catch(event: InputEvent) -> void:
	if _listening_action == "":
		return
	var key := event as InputEventKey
	var mouse := event as InputEventMouseButton

	# —— 取消：Esc ——
	if key != null and key.pressed and key.physical_keycode == KEY_ESCAPE:
		_finish(false)
		get_viewport().set_input_as_handled()
		return

	# —— 只在"按下"时捕获，忽略 echo 和松开 ——
	if key != null and key.pressed and not key.echo:
		_apply_new_event(key, _make_key_event(key))
	elif mouse != null and mouse.pressed and mouse.button_index != MOUSE_BUTTON_WHEEL_UP \
			and mouse.button_index != MOUSE_BUTTON_WHEEL_DOWN:
		# 滚轮不适合做绑定（一滚就中），排除
		_apply_new_event(mouse, _make_mouse_event(mouse))

## 把原始事件转成"干净的新绑定事件"（只留关键字段）
func _make_key_event(src: InputEventKey) -> InputEventKey:
	var ev := InputEventKey.new()
	ev.physical_keycode = src.physical_keycode     # ★ 物理键码！见 24.5.2
	return ev

func _make_mouse_event(src: InputEventMouseButton) -> InputEventMouseButton:
	var ev := InputEventMouseButton.new()
	ev.button_index = src.button_index
	return ev

# —————————————————————— 冲突检测 + 应用 ——————————————————————

func _apply_new_event(raw_event: InputEvent, new_event: InputEvent) -> void:
	var action := _listening_action

	# ① 冲突检测：新键是否被其他动作占用
	var holder := find_action_with_event(new_event, action)
	if holder != "":
		# 策略选择：A. 抢过来（把旧动作的该绑定删除） B. 拒绝并提示
		# 本模板采用"抢过来"，冲突信号给 UI 弹提示
		InputMap.action_erase_event(holder, new_event)
		conflict_detected.emit(holder, action)

	# ② 替换本动作的"第一个键盘/鼠标绑定"（保留手柄绑定不动！）
	_replace_first_km_binding(action, new_event)

	_finish(true)
	get_viewport().set_input_as_handled()      # 别让这次按键漏到游戏世界

func _replace_first_km_binding(action: String, new_event: InputEvent) -> void:
	var evs := InputMap.action_get_events(action)
	for ev in evs:
		# 找到第一个键盘/鼠标绑定并替换（手柄绑定保留）
		if ev is InputEventKey or ev is InputEventMouseButton:
			InputMap.action_erase_event(action, ev)
			break
	InputMap.action_add_event(action, new_event)

func _finish(ok: bool) -> void:
	var a := _listening_action
	_listening_action = ""
	rebinding_finished.emit(a, ok)
	if ok:
		save_bindings()

## 全局搜索：哪个动作绑了 ev？（排除 skip 动作自身）
func find_action_with_event(ev: InputEvent, skip: String = "") -> String:
	for action in InputMap.get_actions():
		var a := action as String
		if a.begins_with("ui_") or a == skip:      # 内置 ui_* 动作不参与玩家冲突
			continue
		if not rebindable_actions.has(a) and a != skip:
			continue
		if InputMap.action_has_event(a, ev):
			return a
	return ""

# —————————————————————— 持久化 ——————————————————————

func save_bindings() -> void:
	var cfg := ConfigFile.new()
	for action in rebindable_actions:
		var texts: Array[String] = []
		for ev in InputMap.action_get_events(action):
			texts.append(event_to_text(ev))
		cfg.set_value(SECTION, action, texts)
	var err := cfg.save(SAVE_PATH)
	if err != OK:
		push_error("改键保存失败: %s" % err)

func load_bindings() -> void:
	if not FileAccess.file_exists(SAVE_PATH):
		return                                   # 首次游玩：用默认绑定
	var cfg := ConfigFile.new()
	if cfg.load(SAVE_PATH) != OK:
		push_warning("改键文件损坏，使用默认绑定")
		return
	for action in rebindable_actions:
		if not cfg.has_section_key(SECTION, action):
			continue
		InputMap.action_erase_events(action)     # 清空后按存档重建
		for text in cfg.get_value(SECTION, action):
			var ev := text_to_event(text)
			if ev != null:
				InputMap.action_add_event(action, ev)

func reset_to_default() -> void:
	# "恢复默认"：把启动时的快照贴回去 + 删存档
	for action in rebindable_actions:
		InputMap.action_erase_events(action)
		for ev in _default_snapshot[action]:
			InputMap.action_add_event(action, ev.duplicate())  # 再拷一份，防共享篡改
	DirAccess.remove_absolute(ProjectSettings.globalize_path(SAVE_PATH))
	save_bindings()                              # 存一份"干净的默认"（可选）

# —————————————————————— 序列化（事件 ↔ 文本） ——————————————————————

## 存储格式自设计："key:K_xxx" / "mouse:M_n" / "joyb:JB_n" / "joyaxis:JAX_n±"
func event_to_text(ev: InputEvent) -> String:
	if ev is InputEventKey:
		return "key:%d" % (ev as InputEventKey).physical_keycode
	if ev is InputEventMouseButton:
		return "mouse:%d" % (ev as InputEventMouseButton).button_index
	if ev is InputEventJoypadButton:
		return "joyb:%d" % (ev as InputEventJoypadButton).button_index
	if ev is InputEventJoypadMotion:
		var m := ev as InputEventJoypadMotion
		return "joyaxis:%d,%s" % [m.axis, ("+" if m.axis_value >= 0 else "-")]
	return ""

func text_to_event(text: String) -> InputEvent:
	var parts := text.split(":")
	if parts.size() != 2:
		return null
	match parts[0]:
		"key":
			var ev := InputEventKey.new()
			ev.physical_keycode = int(parts[1]) as Key
			return ev
		"mouse":
			var ev := InputEventMouseButton.new()
			ev.button_index = int(parts[1]) as MouseButton
			return ev
		"joyb":
			var ev := InputEventJoypadButton.new()
			ev.button_index = int(parts[1]) as JoyButton
			return ev
		"joyaxis":
			var bits := parts[1].split(",")
			var ev := InputEventJoypadMotion.new()
			ev.axis = int(bits[0]) as JoyAxis
			ev.axis_value = 1.0 if bits[1] == "+" else -1.0
			return ev
	return null
```

### 24.9.3 搭一个最简 UI（ItemContainer + 每行一个按钮）

```gdscript
# rebind_ui.gd —— 挂在改键界面的面板上（VBoxContainer 里动态生成行）
extends VBoxContainer

const ROW := preload("res://scenes/ui/rebind_row.tscn")   # 每行：[动作名Label][当前键Button]

func _ready() -> void:
	var mgr := get_node("/root/RebindManager")              # 假设挂了 Autoload
	for action in mgr.rebindable_actions:
		var row := ROW.instantiate()
		row.get_node("ActionLabel").text = mgr.rebindable_actions[action]
		var btn: Button = row.get_node("KeyButton")
		btn.text = describe_binding(action)
		btn.pressed.connect(_on_rebind_pressed.bind(action, btn))
		add_child(row)

	mgr.rebinding_started.connect(_on_listening)
	mgr.rebinding_finished.connect(func(_a, _ok): refresh_all())
	mgr.conflict_detected.connect(func(other, mine):
		print("提示：%s 的按键被 %s 占用，已自动转移" % [
			mgr.rebindable_actions[other], mgr.rebindable_actions[mine]]))

func _on_rebind_pressed(action: String, btn: Button) -> void:
	btn.text = "请按新按键…（Esc 取消）"
	get_node("/root/RebindManager").start_listening(action)

func _on_listening(_action: String) -> void:
	pass   # 需要时禁用其他 UI/播放音效

func refresh_all() -> void:
	var mgr := get_node("/root/RebindManager")
	for row in get_children():
		var action: String = row.get_meta("action")
		row.get_node("KeyButton").text = describe_binding(action)

func describe_binding(action: String) -> String:
	var mgr := get_node("/root/RebindManager")
	var evs := InputMap.action_get_events(action)
	if evs.is_empty():
		return "未绑定"
	var e: InputEvent = evs[0]
	if e is InputEventKey:
		return OS.get_keycode_string((e as InputEventKey).physical_keycode)
	if e is InputEventMouseButton:
		return "鼠标%d" % (e as InputEventMouseButton).button_index
	return "手柄键"
```

（记得在行节点创建时 `row.set_meta("action", action)`——或者改用 `@export String action`，任选。）

### 24.9.4 改键系统的三个设计决策（抄走前想清楚）

| 决策点 | 选项 A | 选项 B | 建议 |
|---|---|---|---|
| 冲突处理 | 新键抢过来（占用者失去该键） | 拒绝并提示 | 单人游戏选 A（爽快），有对战/重要映射选 B |
| 键/柄分开 | 改键只影响键盘鼠标绑定，手柄单独页 | 一个绑定槽全局替换 | 分开！键鼠玩家改键不该把手柄弄坏 |
| 允许的键 | 所有键 | 白名单（排除 Esc/系统键） | 白名单 + 显式排除滚轮 |

### 24.9.5 陷阱例：改键时被游戏世界"顺带"响应

**错误写法**：在 `_input` 里捕获新键且不喊停：

```gdscript
func _input(event: InputEvent) -> void:
	if _listening and event is InputEventKey:
		apply_binding(event)     # ❌ 没有 set_input_as_handled
```

**后果**：玩家把"跳跃"改成 J，**这一下 J 同时让角色跳了一下**（改键界面背后角色还在动）。

**修正**：捕获成功/取消后都调用 `get_viewport().set_input_as_handled()`（模板里已内置）；
更稳妥的做法是改键界面打开时暂停游戏（`get_tree().paused = true` + 界面 `PROCESS_MODE_ALWAYS`）。

---

## 24.10 实战模板 B：PlayerInput 输入组件（完整类）

### 24.10.1 为什么要"输入组件"

**问题现场**：输入查询代码散落在玩家脚本的每个角落——

```gdscript
# player.gd（散装输入，问题多多）
func _physics_process(delta):
	if Input.is_action_just_pressed("jump"): ...
	var dir = Input.get_vector(...)
	if Input.is_action_pressed("dash") and Input.is_action_just_pressed("fire"): ...
	# 以上代码会重复出现在：状态机的每个状态里、动画脚本里、特效脚本里……
```

四宗罪：

1. **查询重复**：同一动作在 5 处各查一次，"只触发一次"逻辑被破坏；
2. **手柄/键鼠特判遍布**：想加"手柄提示图标"要改 20 处；
3. **无法替换输入源**：想做"回放系统"（录像重放）、"AI 托管"、单元测试——
   全项目 `Input.is_xxx` 直查意味着根本没法伪造输入；
4. **输入缓冲/长按判定没有统一实现**：每个动作各自手写计时。

**解法**：把"读输入"收拢成一个**组件**（第 19 章组件思想），玩家代码只问组件要结论：

```
┌──────────────────────┐     查询接口      ┌─────────────────────┐
│ Player.gd            │ ◄──────────────  │ PlayerInput.gd      │
│ 只关心"跳不跳、往哪走" │                  │ 负责读硬件/动作/缓冲  │
└──────────────────────┘                  └─────────────────────┘
        ↑ 想换成 AI 输入/录像回放？换一个同接口组件即可，Player 一行不改
```

### 24.10.2 完整类：PlayerInput（可直接抄）

```gdscript
# res://scripts/player/player_input.gd
# 玩家输入组件：统一查询接口 + 键盘/手柄自适应 + 跳跃缓冲
# 用法：挂为 Player 的子节点，Player 里 @onready var input: PlayerInput = $PlayerInput
class_name PlayerInput
extends Node

# ———————————————————— 配置 ————————————————————

## 跳跃缓冲窗口（秒）：起跳前一点点按了跳，落地后仍会起跳
@export var jump_buffer_time: float = 0.12
## 土狼时间（秒）：走出平台边缘后仍允许跳跃的宽限
@export var coyote_time: float = 0.10
## 攻击"刚好按住也算按"的窗口（秒）：连打体验
@export var attack_buffer_time: float = 0.18

# ———————————————————— 查询缓存（每帧刷新一次） ————————————————————

var move: Vector2 = Vector2.ZERO          # 移动向量（已归一化、含摇杆模拟量）
var move_raw: Vector2 = Vector2.ZERO      # 未做处理的原始移动向量
var jump_held := false                     # 跳跃键是否按住
var jump_pressed := false                  # 跳跃键本帧刚按下
var attack_held := false
var dash_held := false

var last_device: StringName = &"keyboard"  # 最近输入设备（UI 图标切换用）
var is_gamepad := false                    # 当前是否用手柄玩

# ———————————————————— 输入缓冲 ————————————————————

var _jump_buffer_left := 0.0               # 跳跃缓冲剩余时间
var _coyote_left := 0.0                    # 土狼时间剩余
var _attack_buffer_left := 0.0            # 攻击缓冲剩余
var _was_grounded := false
var _jump_queued := false                  # 玩家明确"想吃"这记跳跃前，先排队

@export var is_grounded: bool = false      # 由外部（玩家物理）每帧写入：着地与否

func _ready() -> void:
	# 让组件可在暂停时禁用（跟随默认即可）；预留：process_mode = PROCESS_MODE_PAUSABLE
	set_process(true)

func _process(delta: float) -> void:
	_process(delta) # 防止子类重写漏调（其实不需要，删）
# 注意：上面这行是示例常见笔误，正确实现如下——见 _update()

func _physics_process(_delta: float) -> void:
	_update(_delta)

# ———————————————————— 核心：每帧刷新输入快照 ————————————————————

func _update(delta: float) -> void:
	# ① 移动（键盘 = 数字量，手柄 = 模拟量，get_vector 一次搞定两种）
	move_raw = Input.get_vector("move_left", "move_right", "move_up", "move_down")
	# 死区微调（摇杆漂移场景可开）
	move = JoypadUtils.apply_deadzone(move_raw, 0.15)

	# ② 状态查询
	jump_held = Input.is_action_pressed("jump")
	jump_pressed = Input.is_action_just_pressed("jump")
	attack_held = Input.is_action_pressed("fire")
	dash_held = Input.is_action_pressed("dash")

	# ③ 输入缓冲倒计时
	_jump_buffer_left = maxf(_jump_buffer_left - delta, 0.0)
	_coyote_left = maxf(_coyote_left - delta, 0.0)
	_attack_buffer_left = maxf(_attack_buffer_left - delta, 0.0)

	# ④ 跳跃缓冲：刚按下 → 记一段"有效窗口"
	if jump_pressed:
		_jump_buffer_left = jump_buffer_time

	# ⑤ 土狼时间：上一帧在地面、这一帧离地 → 送一段宽限
	if _was_grounded and not is_grounded:
		_coyote_left = coyote_time
	_was_grounded = is_grounded

	# ⑥ 攻击缓冲
	if Input.is_action_just_pressed("fire"):
		_attack_buffer_left = attack_buffer_time

# ———————————————————— 对外接口：玩家代码只调这些 ————————————————————

## "现在能跳吗？" = 缓冲里有跳跃 且 （在地面 或 土狼时间内）
func consume_jump() -> bool:
	if _jump_buffer_left > 0.0 and (is_grounded or _coyote_left > 0.0):
		_jump_buffer_left = 0.0        # 吃掉缓冲，防止一次按键跳两次
		_coyote_left = 0.0
		return true
	return false

## "有攻击输入排队吗？"（缓冲内一次消费）
func consume_attack() -> bool:
	if _attack_buffer_left > 0.0:
		_attack_buffer_left = 0.0
		return true
	return false

## 蓄力比例示例：0~1（可给冲刺蓄力/蓄力攻击用）
func charge_ratio(hold_action: String, max_time: float) -> float:
	if not Input.is_action_pressed(hold_action):
		return 0.0
	return clampf(Input.get_action_strength(hold_action) * _held_time(hold_action) / max_time, 0.0, 1.0)

var _charge_clock := 0.0
func _held_time(action: String) -> float:
	# 简化实现：按住时长累加（真实项目可做成通用多动作计时器）
	if Input.is_action_pressed(action):
		_charge_clock += get_process_delta_time()
	else:
		_charge_clock = 0.0
	return _charge_clock

# ———————————————————— 设备识别 ————————————————————

func _input(event: InputEvent) -> void:
	# 只做"记录最近设备"这一件事，不消费事件
	if event is InputEventJoypadButton or event is InputEventJoypadMotion:
		last_device = &"gamepad"
		is_gamepad = true
	elif event is InputEventKey or event is InputEventMouseButton \
			or event is InputEventMouseMotion:
		last_device = &"keyboard"
		is_gamepad = false

## UI 提示用：给出某动作当前设备的按键描述
func describe(action: String) -> String:
	for ev in InputMap.action_get_events(action):
		if is_gamepad and (ev is InputEventJoypadButton or ev is InputEventJoypadMotion):
			return "手柄 " + _joy_name(ev)
		if not is_gamepad and ev is InputEventKey:
			return OS.get_keycode_string((ev as InputEventKey).physical_keycode)
	return action

func _joy_name(ev: InputEvent) -> String:
	if ev is InputEventJoypadButton:
		return "按键%d" % (ev as InputEventJoypadButton).button_index
	var m := ev as InputEventJoypadMotion
	return "轴%d%s" % [m.axis, "+" if m.axis_value >= 0 else "-"]
```

### 24.10.3 玩家脚本怎么用（对照示例）

```gdscript
# player.gd —— 干净得发光的玩家核心逻辑
class_name Player
extends CharacterBody2D

@export var move_speed: float = 320.0
@export var jump_speed: float = -420.0

@onready var input: PlayerInput = $PlayerInput

func _physics_process(_delta: float) -> void:
	# ① 把物理结果喂回输入组件（土狼时间依赖它）
	input.is_grounded = is_on_floor()

	# ② 移动
	velocity.x = input.move.x * move_speed

	# ③ 跳跃：所有"缓冲/土狼"复杂度都被 consume_jump() 吃掉了
	if input.consume_jump():
		velocity.y = jump_speed
		$AnimationPlayer.play("jump")

	# ④ 攻击：连打窗口内点击都算数
	if input.consume_attack():
		weapon.try_fire()

	move_and_slide()
```

**体验对比**（这个模板真正值钱的地方）：

| 场景 | 没有缓冲 | 有缓冲（本模板） |
|---|---|---|
| 落地前 0.1 秒按跳 | 无反应（按早了） | 落地瞬间自动起跳 ✅ |
| 走出平台后 0.1 秒按跳 | 无反应（已离地） | 土狼时间内照跳 ✅ |
| 连打攻击键 | 掐不准节奏就丢输入 | 0.18 秒窗口内全算 ✅ |

这三个"小宽容"就是"这游戏手感真好"和"这游戏手感真硬"的区别。

### 24.10.4 陷阱例：把输入缓冲做进状态机每个状态

**错误写法**：

```gdscript
# state_jump.gd
var jump_buffer_timer := 0.0
func _process(d): jump_buffer_timer -= d ...

# state_fall.gd
var jump_buffer_timer := 0.0        # 又一份！
# state_idle.gd
var jump_buffer_timer := 0.0        # 又又一份！
```

**后果**：3 份缓冲计时器各自为政，切状态时缓冲丢失/重复；调一个参数改三处。
**修正**：缓冲属于"输入"，收拢在 PlayerInput 一个地方；状态机只管"要不要消费它"。

---

## 24.11 陷阱大全：输入系统排雷清单

### 24.11.1 陷阱 1：动作没注册就查询

**错误写法**：

```gdscript
func _process(_d: float) -> void:
	if Input.is_action_just_pressed("atack"):    # 拼错了！attack → atack
		shoot()
```

**后果**：控制台每次执行刷一条
`The InputMap action "atack" doesn't exist.`——**但游戏不崩溃**！
新手不看输出面板的话，现象就是"按了没反应"，对着按键本身排查一晚上。

**修正**：

1. **常看输出面板**（Output/调试器），这类警告一眼可见；
2. 动作名统一收拢为常量/枚举，杜绝手拼字符串：

```gdscript
class_name Actions
const JUMP := &"jump"        # StringName 更快且不可拼错
const FIRE := &"fire"

# 使用：Input.is_action_just_pressed(Actions.JUMP)
```

3. 或者启动时自检（推荐大项目）：

```gdscript
func _ready() -> void:
	for a in ["jump", "fire", "dash", "move_left", "move_right", "move_up", "move_down"]:
		assert(InputMap.has_action(a), "InputMap 缺动作: " + a)
```

### 24.11.2 陷阱 2：_input 里直接改 UI 状态

**错误写法**：

```gdscript
# ui_hud.gd
func _input(event: InputEvent) -> void:
	if event.is_action_pressed("pause"):
		$PauseMenu.visible = true          # ❌ 弹菜单，但没拦事件、没暂停游戏
```

**三重后果**：

1. 本帧事件继续流动 → 弹出菜单的这次 Esc 又被"关闭菜单"逻辑收到（菜单闪一下就没了）；
2. 没喊停 → 同帧其他系统（比如"Esc 打开地图"）也响应；
3. 菜单弹出来但游戏还在跑 → 菜单点"继续"之前，角色在背后被小怪围殴。

**修正**：

```gdscript
func _unhandled_input(event: InputEvent) -> void:
	if event.is_action_pressed("pause"):
		$PauseMenu.visible = true
		get_tree().paused = true                    # 暂停游戏
		get_viewport().set_input_as_handled()        # 吃掉事件
```

（菜单自身记得 `process_mode = PROCESS_MODE_ALWAYS`，否则暂停时菜单也点了没反应——这是本陷阱的"续集陷阱"。）

### 24.11.3 陷阱 3：set_input_as_handled 与 accept_event 混用

**错误写法**：

```gdscript
# 挂在 Control（自定义按钮）上
func _gui_input(event: InputEvent) -> void:
	if event.is_action_pressed("confirm"):
		do_confirm()
		get_viewport().set_input_as_handled()   # ❌ 用错对象：这里该用 accept_event()
```

**后果**：`_gui_input` 期间事件还没走到"全局处理"阶段，此时调全局的
`set_input_as_handled` 时机不对；GUI 事件的父子传播（冒泡）也没被拦住——
父容器还以为没人处理这个点击，又触发选择框。

**修正（一张表记牢）**：

| 你在哪个回调里 | 用哪个喊停 |
|---|---|
| `_gui_input`（Control 上） | `accept_event()` |
| `_input` / `_shortcut_input` / `_unhandled_input` | `get_viewport().set_input_as_handled()` |

### 24.11.4 陷阱 4：物理帧里查 just 系列（复习 24.3.3）

`_physics_process` 里查 `is_action_just_pressed`，在高刷屏幕 + 低物理频率下丢输入。
修正：回调里置标志 / 边沿检测 / 输入组件（24.10 已内置正确姿势）。

### 24.11.5 陷阱 5：`process_mode` 与暂停中的输入

**错误写法**：暂停菜单打开了，点"继续"没反应——

**原因**：`get_tree().paused = true` 后，默认 `PROCESS_MODE_INHERIT` 的所有节点
**停止接收 `_process` / `_input` / 物理回调**——包括你的菜单。

**修正**：菜单（和一切"暂停时还要工作"的节点）显式设置：

```gdscript
$PauseMenu.process_mode = Node.PROCESS_MODE_ALWAYS
```

### 24.11.6 陷阱 6：多点触摸忘过滤 index（复习 24.8.4）

单指逻辑必须 `index == 0`；双指手势要按 index 分流。触摸事件"每根手指一条流"，
混流 = UI 乱跳。

### 24.11.7 陷阱 7：改键系统存了 keycode（复习 24.5.2）

存 `keycode` → 换键盘布局的机器上读档，绑定全错位；存 `physical_keycode` 才是正解。
同理 `InputEventKey` 新建绑定事件时也别忘了设的是 physical。

### 24.11.8 陷阱 8：滚轮事件当"按住"用

**错误写法**：

```gdscript
# 想做"按住滚轮拖动"
if Input.is_action_pressed("zoom"):   # ❌ 绑的是滚轮
	continuous_zoom()
```

**后果**：滚轮是**瞬发事件**（滚一格来一条，没有按住状态、没有松开事件），
`is_action_pressed` 表现成"滚一下触发一帧"——不是持续状态。
**修正**：滚轮做离散缩放（每格一档）；持续缩放用按住键（Ctrl+/Q/E）或摇杆轴。

### 24.11.9 陷阱 9：手柄震动忘了停

`start_joypad_rumble(duration)` 的 duration 之外还有切窗口、失焦、暂停等场景不会自动停震。
**修正**：在 `NOTIFICATION_APPLICATION_FOCUS_OUT`、暂停、手柄断连三处调 `stop_joypad_rumble`。

### 24.11.10 陷阱 10：_input 里做重活

`_input` 一帧可能被调用**几十次**（鼠标移动流、按住不放的 echo 流），
把昂贵的逻辑放这里 = 帧率灾难：

```gdscript
# ❌ 每次鼠标移动都做一次全场景射线检测
func _input(event):
	if event is InputEventMouseMotion:
		pick_target_under_mouse()    # 一帧60次调用，每次遍历200个节点
```

**修正**：`_input` 里只**记录**（存下坐标），`_process` 里做**一次**处理：

```gdscript
var _mouse_dirty := false
var _mouse_pos := Vector2.ZERO

func _input(event: InputEvent) -> void:
	if event is InputEventMouseMotion:
		_mouse_pos = (event as InputEventMouseMotion).position
		_mouse_dirty = true

func _process(_delta: float) -> void:
	if _mouse_dirty:
		pick_target_under_mouse()   # 一帧最多一次
		_mouse_dirty = false
```

### 24.11.11 排雷清单（发布前过一遍）

```
□ 项目里所有 is_action_* 查询的动作名，启动时 assert 自检存在
□ "一次性事件"没有散落在多个脚本重复消费
□ just 系列查询不在 _physics_process 里裸查
□ UI 打开时：paused 正确 + 菜单 PROCESS_MODE_ALWAYS + 事件被 handled
□ 捕获鼠标模式有 Esc 逃生出口
□ 手柄断连会暂停/提示；UI 图标随最近设备切换
□ 触摸逻辑过滤了 index；桌面调试有鼠标兼容路径
□ 改键保存用 physical_keycode；有"恢复默认"
□ _input 里没有重活（只记录，_process 处理）
□ 滚轮没被当持续键使用；echo 已在所有按下判断里过滤
```

---

## 本章小结

1. **输入系统三层**：InputMap（按键→意图的翻译层）→ Input 单例（每帧轮询）→
   `_input` 系列回调（事件驱动）。常规游戏输入首选 **InputMap 动作**。
2. **动作（Action）是解耦的关键**：改键、多设备、多布局三大问题被它一次性解决；
   代码里应写 `is_action_pressed("jump")` 而不是 `keycode == KEY_SPACE`。
3. **动作可代码注册**：`InputMap.add_action` + `action_add_event`，
   改键系统、MOD、自动化测试都靠它；改完记得持久化到 `user://`。
4. **三兄弟语义**：`is_action_pressed`（按住期间恒真）、`just_pressed`（仅翻转那一帧）、
   `just_released`（仅松开那一帧）——用错就是把单次事件做成连发或丢事件。
5. **帧序陷阱**：`just_*` 只在一帧内有效；物理帧 + 高刷新率下会漏检。
   方案：回调置标志、自做边沿检测、或收拢进输入组件。
6. **回调链顺序**：`_input` → GUI(`_gui_input`) → `_shortcut_input` →
   `_unhandled_key_input` → `_unhandled_input`，谁处理谁喊停；
   游戏世界输入放 `_unhandled_input`，抢秒级全局键才用 `_input`。
7. **两个喊停 API**：Control 的 `_gui_input` 里用 `accept_event()`；
   其他回调用 `get_viewport().set_input_as_handled()`——用错时机拦不住事件。
8. **键盘双键码**：游戏操作/改键存 `physical_keycode`（跨布局稳定），
   文本/复制类语义用 `keycode`；打字收字符用 `unicode`；按下判断必须 `pressed and not echo`。
9. **鼠标**：`InputEventMouseButton`（含滚轮瞬发、双击 `double_click`）、
   `MouseMotion.relative` 是捕获模式唯一可靠信息；世界坐标瞄准用 `get_global_mouse_position()`；
   捕获模式必须留 Esc 出口。
10. **手柄**：摇杆有硬件漂移 → 必须死区（InputMap 死区或 `apply_deadzone` 径向缩放模板）；
    震动要分级节流并在失焦/断连时 `stop_joypad_rumble`；热插拔接
    `Input.joy_connection_changed`。
11. **触摸**：`ScreenTouch/ScreenDrag` 靠 `index` 区分手指；单指逻辑过滤 index==0，
    双指手势按 index 分流；桌面调试写鼠标兼容路径。
12. **改键系统五件套**：监听捕获（physical_keycode）→ 冲突检测（跨动作搜占用）→
    替换绑定（键鼠/手柄分开）→ 序列化存 user:// → 恢复默认（启动快照或
    `load_from_project_settings`）。
13. **PlayerInput 组件的价值**：统一查询入口、集中输入缓冲（跳跃缓冲/土狼时间/攻击窗口）、
    记录最近设备；玩家代码只消费 `consume_jump()` 这类"结论"，AI/回放可整体替换输入源。
14. **十个经典陷阱**：动作名拼错（不崩溃只刷警告→常量+启动自检）、_input 改 UI 不喊停、
    handled/accept 用错对象、物理帧查 just、暂停忘 PROCESS_MODE_ALWAYS、
    触摸混流、改键存逻辑键码、滚轮当持续键、震动忘停、_input 里做重活。
15. **心智口诀**：**"翻译用 InputMap，状态用轮询，事件用回调；UI 先吃，游戏后吃；
    单次只问一次，缓冲给宽容。"**——背下这句，输入系统九成的设计题都有了答案。







---

# 第 25 章：数学与向量专题

> **本章目标**：把"游戏开发必须用到的数学"一次性讲透。
> 你不需要成为数学家——但你必须看懂"位置、移动、旋转、碰撞、瞄准"背后的那几行公式。
> 读完本章，你会拥有一个可以随手抄走的 `MathUtils` 工具类，覆盖游戏中 90% 的数学需求。

---

## 25.1 为什么游戏离不开数学

### 25.1.1 先破除恐惧：你需要的数学远比想象中少

很多新手一听"数学"就头皮发麻，脑海里浮现出微积分、线性代数的厚书。先给你吃颗定心丸：

> **游戏里 90% 的场景，只用到了"向量的加减乘除"和"勾股定理"。**

真的。你每天在游戏里做的这些事情，背后都是同一小撮数学：

| 你想做的事 | 背后的数学 | 本章对应小节 |
| --- | --- | --- |
| 角色朝前走 | 位置 += 方向 × 速度 × 时间 | 25.2 / 25.8 |
| 斜向移动不能更快 | 单位向量（归一化） | 25.4 |
| 判断敌人是否在视野内 | 点积 dot | 25.5 |
| 判断敌人在左还是右 | 叉积 cross | 25.6 |
| 角色朝鼠标瞄准 | 角度 + 旋转 | 25.7 |
| 相机平滑跟随 | 线性插值 lerp | 25.8 |
| 子弹反弹 | 向量反射 reflect | 25.3 |
| 花瓣弹幕排列 | 正弦/余弦 + 黄金角 | 25.12 |

看到了吗？**没有一行的数学难到需要天赋。** 它们都只是"把几何关系写成代码"。

### 25.1.2 一维数轴：一切概念的起点

先回忆最朴素的东西——**数轴**。一个数字，代表"在一条线上的位置"：

```
负数区                    原点                     正数区
──┼────┼────┼────┼────┼────┼────┼────┼────┼────┼──▶
 -5   -4   -3   -2   -1    0    1    2    3    4    5
                          ↑
                       "我在 0 点上"
```

如果玩家在 `3`，敌人在 `-2`，你怎么算"距离"？很简单：

```
距离 = |3 - (-2)| = |5| = 5
         ↑ 用绝对值消掉方向只留长度
```

如果玩家要"朝敌人移动"，你还需要**方向**：

```
方向 = 敌人 - 玩家 = -2 - 3 = -5   （负数 = 往左）
```

**注意这个关键区别**：`-5` 同时告诉你"多远"（长度 5）和"往哪"（往左）。这种"带方向的量"就是**向量**的雏形。一维的叫"带符号标量"，二维的叫 `Vector2`，三维的叫 `Vector3`。

### 25.1.3 从一维到二维：坐标平面

一维只有一条线。二维加上第二条线（通常是垂直的 y 轴），就有了平面：

```
        y
        ▲
        │
   3    │
        │
   2    │
        │
   1    │
        │
────────┼─────────▶  x
  -1 0  1   2   3
        │
  -1    │
        │
```

平面上每个点用一对数字 `(x, y)` 表示，例如：

- `(3, 2)` 表示"向右 3，向上 2"；
- `(-1, -1)` 表示"向左 1，向下 1"（在 Godot 屏幕坐标里 y 向下越大）。

**Godot 的屏幕坐标有个重要特点：y 轴向下为正！**

```
        (0,0) ──────────▶ x 增大（向右）
          │
          │   屏幕坐标系
          │   y 增大方向 = 向下
          ▼
          y
```

这一点新手极易踩坑：**"向上飞"是 `y` 变小，"向下掉"是 `y` 变大**。记住它，后面所有例子都默认这套坐标系。

### 25.1.4 本章只讲"够用的数学"

本章不会讲：微分、积分、矩阵证明、特征值……这些你在 GUI 游戏里几乎用不到。

本章会讲：向量、点积、叉积、角度、插值、随机数、正弦余弦。学完你就能实现"移动、瞄准、转向、跟随、弹幕、抖动"。**够用，就是最好的标准。**

---

## 25.2 Vector2 从零开始

### 25.2.1 什么是 Vector2

`Vector2` 是 Godot 内置的**二维向量**类型。你可以把它理解成"一对打包好的数字 `(x, y)`"，它有两个身份：

1. **位置（Position）**：表示平面上一个点，如玩家在 `(100, 200)`；
2. **方向 + 长度（Displacement）**：表示"从 A 到 B 的位移"，如"向右 3，向上 4"。

同一个类型，两种用法。区分它们靠上下文：描述"在哪"就是点，描述"往哪走/走多远"就是向量。

### 25.2.2 构造 Vector2

```gdscript
# 入门例：最基础的构造
var a := Vector2(3, 4)        # 用 x=3, y=4 构造
var b := Vector2.ZERO         # 常量：零向量 (0, 0)
var c := Vector2.ONE          # 常量：单位向量 (1, 1)
var d := Vector2.LEFT         # 常量：(-1, 0) 左
var e := Vector2.RIGHT        # 常量：(1, 0)  右
var f := Vector2.UP           # 常量：(0, -1) 上（注意是负数！）
var g := Vector2.DOWN         # 常量：(0, 1)  下

# 只给一个数：两个分量都等于它
var h := Vector2(5, 5)
var i := Vector2(5)           # 注意：Godot 4 的 Vector2 不支持单参数构造！
                               # 想两个分量相同要写 Vector2(5, 5)
```

> ⚠️ **神坑**：`Vector2(5)` 在 Godot 4 里**不存在**。如果你想要 `(5, 5)`，必须老老实实写 `Vector2(5, 5)`。
> 而 `Vector2.ONE * 5` 才是 `(5, 5)` 的常用简写。

```gdscript
# 实战例：把节点的位置读成向量
@onready var player: Node2D = $Player
var pos: Vector2 = player.position       # 直接拿到 (x, y)
var screen_size: Vector2 = get_viewport_rect().size
var center: Vector2 = screen_size / 2.0  # ★ 向量支持整体除法：每个分量都除以 2
print(center)  # → 假设屏幕 1152x648，则 (576, 324)
```

```gdscript
# 陷阱例：误以为 Vector2 是引用类型
var p := Vector2(1, 1)
var q := p            # ★ Vector2 是"值类型"，q 是 p 的副本，不是别名
q.x = 999
print(p)              # → (1, 1)   p 没有变！
print(q)              # → (999, 1)

# 后果：你以为改了 p，其实没改。
# 修正：要么用 p.x = ... 直接改，要么 q = q 运算后重新赋值给 p。
```

### 25.2.3 取值与改值：x / y

```gdscript
var v := Vector2(3, 4)
print(v.x)      # → 3.0
print(v.y)      # → 4.0

v.x = 10        # 就地修改单个分量（v 是值类型，这样改是安全的）
print(v)        # → (10, 4)

# 也可以当成数组按索引访问（0 是 x，1 是 y）——但可读性差，不推荐
print(v[0], v[1])  # → 10 4
```

### 25.2.4 长度：勾股定理图解

现在来到最重要的概念：**向量有多长**。

仍以 `v = (3, 4)` 为例。把它画成一个直角三角形：

```
        y
        ▲
        │
   4    ● (3,4)
        │╲
        │  ╲  这条斜边就是向量长度 length
   3    │    ╲
        │      ╲
   2    │        ╲
        │          ╲
   1    │            ╲
        │              ╲
────────┼───┼───┼───┼───╲──▶ x
        0   1   2   3
              水平 3
```

两条直角边分别是 `3` 和 `4`（x 分量和 y 分量）。根据**勾股定理**：

```
length² = 3² + 4² = 9 + 16 = 25
length  = √25 = 5
```

写成代码：

```gdscript
print(Vector2(3, 4).length())        # → 5.0
print(Vector2(3, 4).length_squared()) # → 25.0
```

就这么简单！**向量的长度 = 两个分量平方和的平方根。**

```gdscript
# 实战例：判断玩家是否进入敌人的"警戒半径"
var to_player: Vector2 = player.global_position - enemy.global_position
if to_player.length() < 200.0:
    enemy.start_chase()

# 陷阱例：每帧大量调用 length() 造成无谓的开销
```

### 25.2.5 length_squared：省掉一次开方

`length()` 内部要做一次**开方**（`sqrt`），开方比乘法慢。如果只是想**比较长度大小**（不关心具体数值），可以比较**长度的平方**：

```gdscript
# 慢：开方两次
if a.length() < b.length():
    ...

# 快：只比较平方，结果一样（因为正数开方是单调递增的）
if a.length_squared() < b.length_squared():
    ...

# 与常数的比较也要平方过来
# 想判断 length() < 200，等价于 length_squared() < 200*200
if to_player.length_squared() < 200.0 * 200.0:
    enemy.start_chase()
```

> **什么时候别用 length_squared**：当你需要真实的距离数值（比如用来算速度比例、显示到 UI）时，还是得用 `length()`。省开方只适用于"纯比较"。

### 25.2.6 加减法的几何意义（ASCII 图示）

**向量加法 = 首尾相接**：

```
     A(2,1)          B(1,2)
  起点→────┐         起点→──┐
          │                │
          └──▶ A          └──▶ B

把 B 的尾巴接到 A 的头上：
                 A+B = (3, 3)

        y
        ▲
   3    │           ●(3,3)
        │         ╱
   2    │       ╱   ← B 的箭头
        │     ╱
   1    │   ●(2,1)   ← A 的箭头终点
        │ ╱
────────┼───────────▶ x
        1   2   3
```

代码上就是**分量分别相加**，Godot 已经帮你重载好了运算符：

```gdscript
var a := Vector2(2, 1)
var b := Vector2(1, 2)
print(a + b)   # → (3, 3)
print(a - b)   # → (1, -1)
print(-a)      # → (-2, -1)  取反 = 反向
```

**向量减法 = 从被减数指向减数（得到相对方向）**：

```
target - position = "从 position 指向 target"

        target(5,3)
           ●
          ╱
        ╱   ← 这个箭头就是 target - position
      ╱
    ● position(1,1)

print(Vector2(5,3) - Vector2(1,1))  # → (4, 2)  指向右上
```

这就是游戏里最常用的一招：**想知道"从我这到目标该怎么走"，就用 `目标 - 自己`**。

```gdscript
# 实战例：每帧朝目标移动
func _process(delta: float) -> void:
    var direction := target.global_position - global_position  # 从自己指向目标
    global_position += direction.normalized() * speed * delta
```

```gdscript
# 陷阱例：把加法当减法，方向反了
var dir := global_position - target.global_position  # ✗ 这是"从目标指向我"，跑反了！
global_position += dir.normalized() * speed * delta  # 后果：越跑离目标越远
# 修正：交换顺序 → target.global_position - global_position
```

### 25.2.7 数乘缩放：改变长度不改变方向

**向量 × 一个普通数字（标量）= 每个分量都乘这个数**：

```gdscript
var v := Vector2(3, 4)
print(v * 2)     # → (6, 8)    长度从 5 变成 10（方向不变）
print(v * 0.5)   # → (1.5, 2)  长度变成 2.5
print(v * -1)    # → (-3, -4)  长度不变，方向反转
print(2 * v)     # → (6, 8)    数字在前也行（乘法和数字顺序无关）

# 除法同理
print(v / 2)     # → (1.5, 2)
```

几何意义：

```
v * 2 更长了           v * 0.5 更短了        v * -1 掉头
    ╱                    ╱                    ●
  ╱                   ╱                    ╱
 ╱  长度 10         ●  长度 2.5          ╱  指向相反
●                  ╱                   ●（原点是尾巴）
```

```gdscript
# 实战例：用数乘做速度
var velocity := Vector2(1, 0)        # 朝右、长度为 1 的方向
var speed := 300.0                   # 每秒 300 像素
position += velocity * speed * delta # 每秒走 300 像素，向右
```

---

## 25.3 向量常用方法大全

下面是最常用方法的**速查表**。先扫一遍有个印象，后面小节会挑重点深入。

| 方法 | 作用 | 示例（执行结果） | 备注 |
| --- | --- | --- | --- |
| `length()` | 求长度（模） | `Vector2(3,4).length()` → `5.0` | 内部有开方，稍慢 |
| `length_squared()` | 长度的平方 | `Vector2(3,4).length_squared()` → `25.0` | 纯比较时用它更快 |
| `normalized()` | 归一化，返回长度 1 的方向向量 | `Vector2(3,4).normalized()` → `(0.6, 0.8)` | 零向量调用返回 `(0,0)` |
| `normalize()` | 就地归一化（原地修改自身） | `v.normalize()` | 会改动 `v`，注意值类型 |
| `is_normalized()` | 是否已是单位向量 | `Vector2(1,0).is_normalized()` → `true` | 浮点近似判断 |
| `distance_to(other)` | 到另一个点的距离 | `Vector2(0,0).distance_to(Vector2(3,4))` → `5.0` | = `(other-self).length()` |
| `distance_squared_to(other)` | 距离的平方 | `Vector2(0,0).distance_squared_to(Vector2(3,4))` → `25.0` | 比较距离时用 |
| `direction_to(other)` | 指向另一个点的单位向量 | `Vector2(0,0).direction_to(Vector2(3,4))` → `(0.6, 0.8)` | = `(other-self).normalized()` |
| `dot(other)` | 点积（判断同向/垂直/反向） | `Vector2(1,0).dot(Vector2(1,0))` → `1.0` | 详见 25.5 |
| `cross(other)` | 二维叉积（判断左右） | `Vector2(1,0).cross(Vector2(0,1))` → `1.0` | 返回单个标量，详见 25.6 |
| `angle()` | 与 x 轴正方向的夹角（弧度） | `Vector2(0,1).angle()` → `1.5708`（=π/2） | 屏幕 y 向下，正角是顺时针 |
| `angle_to(other)` | 到另一个向量的夹角（弧度） | `Vector2(1,0).angle_to(Vector2(0,1))` → `1.5708` | 有正负，逆时针为正 |
| `angle_to_point(other)` | 从自身位置看另一个点的角度 | `pos.angle_to_point(mouse_pos)` | 常用于瞄准 |
| `get_angle_to(other)` | 相对旋转量（供 rotation 用） | `node.get_angle_to(target)` | = `angle_to_point - global_rotation` |
| `lerp(to, weight)` | 线性插值到目标 | `Vector2(0,0).lerp(Vector2(10,0), 0.5)` → `(5,0)` | weight 0~1 |
| `slerp(to, weight)` | 球面/角度插值 | `v.slerp(target, 0.5)` | 沿弧线插值，保持长度 |
| `move_toward(to, delta)` | 以固定步长朝目标移动 | `Vector2(0,0).move_toward(Vector2(10,0), 2)` → `(2,0)` | 不会越过目标 |
| `bounce(normal)` | 沿法线反弹 | `Vector2(1,-1).bounce(Vector2(0,1))` → `(1,1)` | 相当于 `reflect(-...)`，详见下 |
| `reflect(normal)` | 关于法线反射 | `Vector2(1,-1).reflect(Vector2(0,1))` → `(1,1)` | 注意参数是法线 |
| `slide(normal)` | 沿表面滑动（去掉法线分量） | `Vector2(1,-1).slide(Vector2(0,1))` → `(1,0)` | 消除进入墙内的分量 |
| `rotated(angle)` | 旋转后的新向量（不改自身） | `Vector2(1,0).rotated(PI/2)` → `(0,1)` | 弧度制 |
| `posmod(mod)` | 分量取正余数 | `Vector2(-1,-2).posmod(3)` → `(2,1)` | 结果始终非负 |
| `clamp(min, max)` | 分量夹取到区间 | `Vector2(-5,9).clamp(Vector2(0,0),Vector2(5,5))` → `(0,5)` | 分向量各自夹取 |
| `snapped(step)` | 分量吸附到步长网格 | `Vector2(2.7,3.2).snapped(Vector2(1,1))` → `(3.0,3.0)` | 做格子对齐 |
| `is_equal_approx(other)` | 近似相等（浮点安全比较） | `Vector2(0.1+0.2,0).is_equal_approx(Vector2(0.3,0))` → `true` | 别用 `==` 比较浮点 |
| `is_zero_approx()` | 是否近似零向量 | `Vector2(0.0000001,0).is_zero_approx()` → `true` | 判断零向量用它 |
| `abs()` | 各分量取绝对值 | `Vector2(-3,4).abs()` → `(3,4)` | |
| `sign()` | 各分量取符号（-1/0/1） | `Vector2(-3,4).sign()` → `(-1,1)` | |
| `floor()` / `ceil()` / `round()` | 各分量取整 | `Vector2(1.7,2.3).round()` → `(2.0,2.0)` | |
| `orthogonal()` | 返回一个垂直向量 | `Vector2(1,0).orthogonal()` → `(0,1)` | 旋转 90°，长度不变 |
| `max_axis_index()` | 哪个分量最大（0=x,1=y） | `Vector2(1,5).max_axis_index()` → `1` | 取主轴方向 |
| `min_axis_index()` | 哪个分量最小 | `Vector2(1,5).min_axis_index()` → `0` | |

> 表中所有方法，`Vector2` 和 `Vector3` **名字完全一样**（`cross` 在 3D 下返回 `Vector3` 而非标量）。学会一套，两处通用。

下面挑几个"光看表看不懂"的深入讲。

### 25.3.1 move_toward：不会越过的靠近

```gdscript
# 入门例
var p := Vector2(0, 0)
p = p.move_toward(Vector2(10, 0), 3)  # 朝目标一次最多走 3
print(p)  # → (3, 0)

# 再走两次
p = p.move_toward(Vector2(10, 0), 3)  # → (6, 0)
p = p.move_toward(Vector2(10, 0), 3)  # → (9, 0)
p = p.move_toward(Vector2(10, 0), 3)  # → (10, 0)  到达后停住，不会冲过头
p = p.move_toward(Vector2(10, 0), 3)  # → (10, 0)  仍然停住

# 实战例：让节点以恒定速度追目标，且不会抖动
func _process(delta: float) -> void:
    global_position = global_position.move_toward(
        target.global_position, speed * delta
    )
```

```gdscript
# 陷阱例：用 move_toward 的"步长"时忘了乘 delta，速度随帧率变化
global_position = global_position.move_toward(target.global_position, speed)  # ✗
# 后果：120Hz 屏幕上移动速度是 60Hz 的两倍！
# 修正：步长 = 速度(像素/秒) * delta(秒)
global_position = global_position.move_toward(target.global_position, speed * delta)
```

### 25.3.2 clamp / snapped：把数值限制在合理范围

```gdscript
# 入门例：把玩家限制在地图边界内
var pos := Vector2(1200, -50)
pos = pos.clamp(Vector2.ZERO, Vector2(1152, 648))
print(pos)  # → (1152, 0)  右边界和下边界各被夹住

# 实战例：让物体吸附到 32 像素的格子（做塔防/战棋）
var snapped_pos := pos.snapped(Vector2(32, 32))
print(snapped_pos)  # → 各分量吸附到最近的 32 的倍数
```

### 25.3.3 rotate 家族：orthogonal / rotated

```gdscript
# orthogonal()：逆时针旋转 90°，得到垂直向量，长度不变
print(Vector2(1, 0).orthogonal())   # → (0, 1)
print(Vector2(3, 4).orthogonal())   # → (-4, 3)，长度仍是 5

# rotated(angle)：按任意角度旋转（弧度制）
print(Vector2(1, 0).rotated(PI / 2))   # → (0, 1)   逆时针 90°
print(Vector2(1, 0).rotated(PI))       # → (-1, 0)  转 180°
print(Vector2(1, 0).rotated(-PI / 2))  # → (0, -1)  y 是负的 = 屏幕上方
```

> ⚠️ **屏幕坐标的"逆时针"直觉要反过来看**：因为 y 轴向下，数学上的"逆时针"在屏幕上看起来可能是"顺时针"。遇到方向不对，先怀疑 y 轴方向。

---

## 25.4 单位向量与 normalized 的深入

### 25.4.1 为什么要归一化：斜向移动更快的经典陷阱

先说结论：**如果你直接用"方向向量 × 速度"来移动，而没有先把方向变成单位长度，斜向移动会更快。**

看数字。假设速度是 1 像素/帧：

```
只按右 (1, 0)：长度 = √(1²+0²) = 1        → 每帧走 1
只按下 (0, 1)：长度 = √(0²+1²) = 1        → 每帧走 1

同时按右+下 (1, 1)：长度 = √(1²+1²) = √2 ≈ 1.414
   → 每帧走 1.414！比只能走 1 的单方向快了 41%！
```

几何上很好理解：对角线是正方形的斜边，总是比边更长。

```
   (0,0)───────▶(1,0)  长度 1
     │
     │
     ▼
   (0,1)  长度 1

   同时按：
   (0,0)───────▶
     │╲
     │  ╲  这条斜边长 √2 ≈ 1.414
     │    ╲
     ▼──────▶(1,1)
```

**修正方法：先归一化，让方向向量的长度变成 1，再乘速度。**

```gdscript
# 入门例：看归一化的效果
print(Vector2(1, 1).length())             # → 1.4142135...
print(Vector2(1, 1).normalized())         # → (0.70710678, 0.70710678)
print(Vector2(1, 1).normalized().length())# → 1.0   ★ 长度永远是 1
```

`normalized()` 做的事就是"每个分量除以当前长度"：

```
(1, 1) / 1.414 = (0.707, 0.707)
0.707² + 0.707² = 0.5 + 0.5 = 1   ✓
```

### 25.4.2 正确的斜向移动写法

```gdscript
# 实战例：8 方向移动，保证斜向速度与直向一致
func _physics_process(delta: float) -> void:
    var input_dir := Input.get_vector("left", "right", "up", "down")
    # ★ Input.get_vector 已经帮你归一化了！(1,1) 会变成 (0.707, 0.707)
    velocity = input_dir * speed
    move_and_slide()
```

如果你手动收集方向，就要自己归一化：

```gdscript
func _physics_process(delta: float) -> void:
    var dir := Vector2.ZERO
    if Input.is_action_pressed("right"): dir.x += 1
    if Input.is_action_pressed("left"):  dir.x -= 1
    if Input.is_action_pressed("down"):  dir.y += 1
    if Input.is_action_pressed("up"):    dir.y -= 1

    # ★ 关键：不能省略这一句
    dir = dir.normalized()

    velocity = dir * speed
    move_and_slide()
```

```gdscript
# 陷阱例：忘记归一化
var dir := Vector2.ZERO
if Input.is_action_pressed("right"): dir.x += 1
if Input.is_action_pressed("down"):  dir.y += 1
velocity = dir * speed   # ✗ 斜向时 dir=(1,1)，速度变成 speed*1.414
# 后果：玩家斜着走比直着走快 41%，速通玩家立刻发现并利用。
# 修正：velocity = dir.normalized() * speed
```

### 25.4.3 零向量归一化陷阱

**零向量 `(0,0)` 没有方向可言，它的长度是 0。** 除以 0 在数学上是未定义的，Godot 的处理是：

```gdscript
print(Vector2.ZERO.normalized())  # → (0, 0)  Godot 不报错，直接返回零向量
```

看起来很方便，但**危险**在于：你以为拿到的是个"方向"，结果是个零向量，乘以速度后移动量还是 0，角色就**卡住不动了**。

```gdscript
# 陷阱例：目标是自己时，direction_to 返回零向量
func _process(delta: float) -> void:
    var dir := target.global_position - global_position
    # 如果 target 和自己位置重合，dir = (0,0)
    velocity = dir.normalized() * speed   # (0,0)*speed = (0,0)，角色不动
    # 若做旋转，还会因为角度未定义出现诡异表现

    # 修正：先判断是否近似为零
    if dir.is_zero_approx():
        return  # 已经重合，不处理
    velocity = dir.normalized() * speed
```

```gdscript
# 实战例：安全的归一化辅助函数
func safe_normalize(v: Vector2, fallback: Vector2 = Vector2.ZERO) -> Vector2:
    if v.is_zero_approx():
        return fallback
    return v.normalized()
```

> **记忆口诀**：**"归一化前先想清楚——如果它可能是零，就要兜底。"**

---

## 25.5 点积（dot）直觉详解

### 25.5.1 点积的定义与算法

点积（dot product）把**两个向量**变成一个**数字**：

```
a · b = a.x * b.x + a.y * b.y
```

```gdscript
print(Vector2(1, 0).dot(Vector2(1, 0)))   # → 1*1 + 0*0 = 1.0
print(Vector2(1, 0).dot(Vector2(0, 1)))   # → 1*0 + 0*1 = 0.0
print(Vector2(1, 0).dot(Vector2(-1, 0)))  # → 1*-1 + 0*0 = -1.0
```

### 25.5.2 三个关键切面：同向 / 垂直 / 反向

当两个向量都是**单位向量**时，点积结果有极其直观的含义：

```
cos(夹角) = a · b   （a、b 都是单位向量时）

夹角 0°  （完全同向）：  dot =  1
夹角 60°：              dot =  0.5
夹角 90°（垂直）：       dot =  0
夹角 120°：             dot = -0.5
夹角 180°（完全反向）：  dot = -1
```

图示：

```
同向            垂直            反向
  →→            →               →   ←
dot =  1        ↑              dot = -1
                dot = 0
```

**判断表**（单位向量）：

| dot 值 | 含义 |
| --- | --- |
| `dot > 0` | 两向量夹角小于 90°，大致同向 |
| `dot == 0` | 垂直（正交），互不"投影" |
| `dot < 0` | 夹角大于 90°，大致反向 |
| `dot ≈ 1` | 几乎完全同方向 |
| `dot ≈ -1` | 几乎完全反方向 |

### 25.5.3 余弦关系：完整的点积公式

一般（非单位）向量的点积公式是：

```
a · b = |a| * |b| * cos(θ)
```

所以：

```
cos(θ) = (a · b) / (|a| * |b|)
```

如果你把 `a`、`b` 都归一化，分母就变成 1，于是 `cos(θ) = a · b`。**这就是为什么"判断方向关系时要先归一化"。**

### 25.5.4 实战：敌人是否在玩家视野内

这是点积最经典的应用。玩家朝某方向看，视野是左右各 45°（总 90°）。要判断敌人是否在视野里：

```gdscript
# 模块模板：视野锥判定
@onready var player: Node2D = $"../Player"

@export var view_distance: float = 300.0   # 视野半径（像素）
@export var view_half_angle_deg: float = 45.0  # 半视野角（度）

func can_see_player() -> bool:
    var to_player: Vector2 = player.global_position - global_position

    # 1) 距离判定：太远就看不见
    if to_player.length() > view_distance:
        return false

    # 2) 角度判定：用点积代替昂贵的反三角函数
    var forward: Vector2 = Vector2.RIGHT.rotated(global_rotation)  # 自己的朝向
    var cos_limit: float = cos(deg_to_rad(view_half_angle_deg))

    # to_player 方向与 forward 方向的点积（都归一化后）
    var d: float = forward.dot(to_player.normalized())
    # d >= cos(45°) ≈ 0.707 说明夹角在 45° 以内
    return d >= cos_limit
```

用 ASCII 画出来：

```
               视野半径 300
        ╭───────────────────╮
      ╱  视野半角 45°          ╲
    ╱     ↑                      ╲
   │      │forward                │
   │       ●──▶                  │   ← 玩家在中心，朝右看
    ╲      │                    ╱
      ╲    │45°              ╱
        ╰────┼─────────────╯
             ● 敌人
      若敌人在这个扇形内 → dot ≥ cos(45°) → 看得见
```

```gdscript
# 陷阱例：忘了归一化 to_player 就 dot
var d := forward.dot(to_player)   # ✗ to_player 没归一化，结果被距离放大了
# 后果：远处敌人不管在不在视野内，dot 都可能很大或很小，判定完全乱套。
# 修正：forward.dot(to_player.normalized())
```

> **为什么用 dot 而不用角度**：`angle_to` 内部要算 `acos`，比几次乘法慢得多。**"能不能看见"这类频繁判定，用 dot 更高效。**

---

## 25.6 叉积（cross）直觉详解

### 25.6.1 二维叉积是什么

在二维里，`a.cross(b)` 返回**一个数字**（不是向量）：

```
a.cross(b) = a.x * b.y - a.y * b.x
```

```gdscript
print(Vector2(1, 0).cross(Vector2(0, 1)))   # → 1*1 - 0*0 = 1.0
print(Vector2(0, 1).cross(Vector2(1, 0)))   # → 0*0 - 1*1 = -1.0
print(Vector2(1, 0).cross(Vector2(1, 0)))   # → 0.0  （平行）
```

### 25.6.2 判断目标在左还是右

在屏幕坐标系（y 向下）下，**叉积的符号告诉你"另一个向量在你的哪一侧"**：

```
a.cross(b) > 0  →  b 在 a 的顺时针方向（屏幕上通常表现为"右侧"）
a.cross(b) < 0  →  b 在 a 的逆时针方向（"左侧"）
a.cross(b) = 0  →  a 与 b 共线（同向或反向）
```

图示（a 朝屏幕右方）：

```
        b 在上方(a 的逆时针)
             ●
             ↑
   a →  ●─────
   （你在中心朝右看）
             ↓
             ●
        b 在下方(a 的顺时针)

a.cross(b_上) < 0
a.cross(b_下) > 0
```

```gdscript
# 入门例
var forward := Vector2.RIGHT
var enemy1 := Vector2(1, -1).normalized()   # 右上方
var enemy2 := Vector2(1, 1).normalized()    # 右下方

print(forward.cross(enemy1))  # → 负数（约 -0.707）
print(forward.cross(enemy2))  # → 正数（约 0.707）
```

### 25.6.3 实战：NPC 朝目标平滑转身

叉积的符号 = 该往哪个方向转；`angle_to_point` = 该转多少。结合起来就是"平滑转身"：

```gdscript
# 模块模板：NPC 平滑转向目标（每帧调用）
@export var turn_speed: float = 5.0   # 弧度/秒

func turn_toward(target_pos: Vector2, delta: float) -> void:
    var to_target: Vector2 = target_pos - global_position
    if to_target.is_zero_approx():
        return  # 与目标重合，方向未定义

    var target_angle: float = to_target.angle()          # 目标朝向（弧度）
    # ★ lerp_angle 自动选择最短转向路径，跨越 ±π 也不会绕远
    global_rotation = lerp_angle(global_rotation, target_angle, turn_speed * delta)
```

如果你要**显式用叉积**决定转向方向（比如手动控制转向速率）：

```gdscript
# 模块模板：用叉积 + 固定角速度转身（不会瞬间转头）
@export var turn_rate: float = 3.0   # 弧度/秒

func turn_with_cross(target_pos: Vector2, delta: float) -> void:
    var forward := Vector2.RIGHT.rotated(global_rotation)
    var to_target := (target_pos - global_position).normalized()

    var side: float = forward.cross(to_target)   # >0 顺时针，<0 逆时针
    var diff: float = forward.angle_to(to_target)  # 还需要转多少（带符号）

    # 每次最多转 turn_rate * delta，且不越过
    var step: float = min(abs(diff), turn_rate * delta) * sign(diff)
    global_rotation += step
```

```gdscript
# 陷阱例：直接用 atan2 算角度然后硬赋值，转向会突然跳到另一侧
global_rotation = (target_pos - global_position).angle()  # ✗ 瞬间完成，像开了挂
# 后果：NPC 毫无"转身"过程，视觉生硬；跨越 -π/π 边界时可能反向猛转一整圈。
# 修正：用 lerp_angle 或限制每帧角速度（上面的模板）。
```

---

## 25.7 角度系统

### 25.7.1 弧度 vs 角度

电脑内部一律用**弧度（radian）**，人习惯用**角度（degree）**。换算关系：

```
180° = π 弧度 ≈ 3.14159 弧度
1°   ≈ 0.01745 弧度
1 弧度 ≈ 57.2958°
```

```
     90°
      ↑
      │
180° ─┼─ 0° / 360°
      │
      ↓
     270°
```

```gdscript
print(rad_to_deg(PI))         # → 180.0
print(deg_to_rad(180))        # → 3.14159...
print(rad_to_deg(PI / 2))     # → 90.0
print(deg_to_rad(90))         # → 1.5708
```

| 场景 | 用什么单位 | 转换函数 |
| --- | --- | --- |
| `rotation` 属性 | 弧度 | 界面输入用度，存前转弧度 |
| `sin/cos` 参数 | 弧度 | |
| Inspector 里 `@export` 的角度 | 建议用度，内部再转 | `deg_to_rad()` |
| UI 显示给玩家 | 度 | `rad_to_deg()` |

### 25.7.2 *_angle 家族细节

```gdscript
var v := Vector2(1, 1)
print(v.angle())          # → 0.7854 (45°)，与 x 轴正方向夹角
print(rad_to_deg(v.angle()))  # → 45.0

# angle_to：a 到 b 的有符号夹角
print(Vector2(1,0).angle_to(Vector2(0,1)))   # → 1.5708 (90°)
print(Vector2(0,1).angle_to(Vector2(1,0)))   # → -1.5708 (-90°)

# angle_to_point：从自身位置看某点的角度（常用于瞄准）
var player_pos := Vector2(100, 100)
var mouse_pos := Vector2(200, 100)
print(rad_to_deg(player_pos.angle_to_point(mouse_pos)))  # → 0.0（正右方）

# get_angle_to：节点朝向与目标的差（Node2D 方法，考虑 global_rotation）
player.rotation += player.get_angle_to(mouse_pos)
```

### 25.7.3 wrapf：把角度折回 -π~π

角度转多了会变成 5π、-7π 之类。`wrapf` 把它折回一个区间：

```gdscript
print(wrapf(3 * PI, -PI, PI))   # → PI（3π 折回 π）
print(wrapf(5.5, 0, 3))         # → 2.5
print(wrapf(-1.0, 0, 3))        # → 2.0
```

对比表格：

| 函数 | 作用 |
| --- | --- |
| `wrapf(value, min, max)` | 浮点折返到 `[min, max)` |
| `wrapi(value, min, max)` | 整数折返 |
| `fposmod(a, b)` | 浮点正余数，结果落在 `[0, b)` |
| `fmod(a, b)` | 浮点余数（符号跟被除数，可能为负） |

### 25.7.4 rotation 与 position 的关系

`rotation` 只管**朝向**，`position` 只管**位置**，两者独立。想让"朝向"影响"移动"，你得手动把方向向量旋转：

```gdscript
# 模块模板：朝"自己面向的前方"移动（像坦克）
func _physics_process(delta: float) -> void:
    global_rotation += turn_input * turn_speed * delta          # 先转向
    var forward := Vector2.RIGHT.rotated(global_rotation)        # 前方单位向量
    global_position += forward * move_speed * delta              # 再前进
```

> 注意：`Vector2.RIGHT` 是"角色在 rotation=0 时的前方"。所以前进方向 = `RIGHT` 旋转了 `rotation` 之后的向量。

### 25.7.5 完整模板：朝鼠标瞄准并开火

```gdscript
# 模块模板：PlayerAim.gd —— 朝鼠标瞄准，点击开火
extends Node2D
class_name PlayerAim

@export var bullet_scene: PackedScene
@export var fire_interval: float = 0.15     # 开火间隔（秒）

var _cooldown: float = 0.0

func _process(delta: float) -> void:
    _cooldown = maxf(_cooldown - delta, 0.0)

    # 1) 拿到鼠标在全局坐标下的位置
    var mouse_pos := get_global_mouse_position()

    # 2) 让枪口朝向鼠标：直接设置 rotation（弧度）
    rotation = (mouse_pos - global_position).angle()

    # 3) 按住鼠标左键且冷却结束 → 开火
    if Input.is_action_pressed("fire") and _cooldown <= 0.0:
        _fire()

func _fire() -> void:
    _cooldown = fire_interval

    var bullet := bullet_scene.instantiate()
    # 子弹从枪口（自己前方 20 像素处）生成
    var muzzle := global_position + Vector2.RIGHT.rotated(rotation) * 20.0
    bullet.global_position = muzzle
    bullet.global_rotation = rotation               # 子弹也朝向同一方向
    get_tree().current_scene.add_child(bullet)
```

```gdscript
# 陷阱例：用鼠标的屏幕坐标直接算角度，忽略了相机
rotation = get_viewport().get_mouse_position().angle()  # ✗ 相机移动后就错位
# 后果：相机一旦滚动，准星和鼠标对不上。
# 修正：用 get_global_mouse_position()（Node2D/CanvasItem 提供）
rotation = get_global_mouse_position().angle()
```

---

## 25.8 lerp 家族深入

### 25.8.1 lerp：线性插值

```gdscript
print(lerp(0.0, 100.0, 0.0))    # → 0.0    还没开始
print(lerp(0.0, 100.0, 0.5))    # → 50.0   走了一半
print(lerp(0.0, 100.0, 1.0))    # → 100.0  完全到达
print(lerp(0.0, 100.0, 0.25))   # → 25.0

# 向量也有 lerp
print(Vector2(0, 0).lerp(Vector2(100, 50), 0.5))  # → (50, 25)
```

公式：`结果 = a + (b - a) * weight`。`weight` 是 0~1 的比例。

```
a=0 ●──────────────────────────● b=100
    0    25    50    75   100
         ↑weight=0.25 等
```

### 25.8.2 lerp_angle：角度插值过 ±π

普通 `lerp` 用在角度上会出事：从 `170°` 插值到 `-170°`，普通 lerp 会**绕一大圈**（340° 的路），而实际只需走 20°。

```gdscript
# 普通 lerp：绕远路
print(rad_to_deg(lerp(deg_to_rad(170), deg_to_rad(-170), 0.5)))  # → 0.0（绕了 180°！）

# lerp_angle：走最短路径
print(rad_to_deg(lerp_angle(deg_to_rad(170), deg_to_rad(-170), 0.5)))  # → 180.0 附近
```

```
普通 lerp:  170° ──▶ 0° ──▶ -170°   （绕了半圈）
lerp_angle: 170° ──▶ 180°/=180° ──▶ -170°  （只走 20°）
```

**规则：只要插值对象是角度/rotation，永远用 `lerp_angle`，不用 `lerp`。**

### 25.8.3 inverse_lerp / remap / smoothstep

```gdscript
# inverse_lerp：lerp 的逆运算，"value 在 [a,b] 里占百分之几"
print(inverse_lerp(0.0, 100.0, 25.0))   # → 0.25
print(inverse_lerp(0.0, 100.0, 50.0))   # → 0.5

# remap：把一个区间的值映射到另一个区间
print(remap(50.0, 0.0, 100.0, 0.0, 1.0))    # → 0.5
print(remap(75.0, 0.0, 100.0, 0.0, 10.0))   # → 7.5
# 实战：血条比例、把血量映射到颜色亮度

# smoothstep：平滑过渡（首尾速度慢、中间快，S 形曲线）
print(smoothstep(0.0, 1.0, 0.5))   # → 0.5
print(smoothstep(0.0, 1.0, 0.1))   # → 0.028  （比线性 0.1 更小，起步更缓）
print(smoothstep(0.0, 1.0, 0.9))   # → 0.972  （更接近 1，收尾更缓）
```

```
smoothstep 曲线（S 形）          线性 lerp（直线）
1 ┤         ╭──                 1 ┤         ╱
  │      ╱                       │       ╱
0 ┤──╯                          0 ┤ ╱
  0            1                 0          1
  起步、收尾更柔和                匀速
```

### 25.8.4 帧率无关的指数平滑（重要！）

**问题**：很多教程教你每帧 `lerp(current, target, 0.1)` 来做平滑跟随。这有个致命缺陷——**帧率不独立**。

```gdscript
# 陷阱例：帧率不独立的平滑
func _process(delta: float) -> void:
    position = position.lerp(target.position, 0.1)  # ✗ 每秒算多少次取决于帧率
```

为什么错？假设每秒 lerp 一次拿到的"剩余距离"是 0.9 倍，那 60Hz 一秒内 lerp 60 次，剩余 = `0.9^60 ≈ 0.0018`；而 120Hz 一秒内 lerp 120 次，剩余 = `0.9^120 ≈ 0.0000036`。**高刷屏上跟随明显更快**。

**正确做法：用基于时间的指数衰减。**

```gdscript
# 模块模板：帧率无关的指数平滑
@export var follow_speed: float = 5.0   # 越大跟得越紧

func _process(delta: float) -> void:
    # ★ 核心公式：把"每帧固定比例"换成"基于 delta 的比例"
    var weight: float = 1.0 - exp(-follow_speed * delta)
    position = position.lerp(target.position, weight)
```

**推导直觉**：连续时间的指数衰减解是 `剩余比例 = exp(-speed * t)`。那么在 `delta` 秒内，走过的比例就是 `1 - exp(-speed * delta)`。这样无论 60Hz 还是 144Hz，经过相同真实时间，剩余距离都一样。

两种写法对比表：

| 写法 | 帧率独立？ | 说明 |
| --- | --- | --- |
| `lerp(a, b, 0.1)` | ❌ | 高帧率更快，低帧率更慢 |
| `lerp(a, b, 1 - exp(-k * delta))` | ✅ | 与帧率无关，`k` 越大越快 |
| `a.move_toward(b, speed * delta)` | ✅ | 恒定速度（非指数），也会停住 |

```gdscript
# 陷阱例：把 delta 当成权重直接塞进 lerp
position = position.lerp(target.position, delta)  # ✗ delta≈0.016，几乎不动
# 后果：60Hz 时每秒靠近比例约 1-(1-0.016)^60 ≈ 62%，且帧率一变速度就变。
# 修正：用 1 - exp(-speed * delta)，walk_speed 控制手感。
```

---

## 25.9 Transform2D 初探

### 25.9.1 位置 / 旋转 / 缩放 如何组成变换

一个 `Node2D` 对外有三个直观属性：`position`、`rotation`、`scale`。它们其实被打包进一个 `Transform2D`。你可以把变换理解成"**本地坐标系到父坐标系的换算规则**"。

```
局部坐标 (0,0) 在这个节点的"原点"
    ↓ 应用 position 平移
    ↓ 应用 rotation 旋转
    ↓ 应用 scale 缩放
得到父坐标系下的位置
```

`Transform2D` 里通常关心：

| 属性 | 含义 |
| --- | --- |
| `origin` | 变换的位置部分（相当于 position） |
| `x` | 本地 x 轴方向与缩放（rotation=0, scale=1 时是 `(1,0)`） |
| `y` | 本地 y 轴方向与缩放（rotation=0, scale=1 时是 `(0,1)`） |
| `get_rotation()` | 从变换里提取旋转角 |
| `get_scale()` | 提取缩放 |
| `get_origin()` | 提取位置 |

### 25.9.2 局部坐标 vs 全局坐标

- **局部坐标（local）**：相对自己父节点/自己的坐标系；
- **全局坐标（global）**：相对整个场景根（世界原点）。

```
世界原点 (0,0)
   │
   └── 容器节点 position=(100,100)
          │
          └── 子节点 position=(20,20)   ← 这是局部坐标
                它在世界里的位置 = (120,120)  ← 这是全局坐标
```

### 25.9.3 to_local / to_global 转换模板

```gdscript
# 子节点世界坐标换算：把子节点的全局位置，转成"我自己坐标系下的位置"
var child_world_pos: Vector2 = child.global_position
var local_to_me: Vector2 = to_local(child_world_pos)     # 世界 → 我的局部
print(local_to_me)   # 相对于我的偏移，已包含我的旋转和缩放

# 反过来：把"我局部坐标里的一个点"转成世界坐标
var world_pos: Vector2 = to_global(Vector2(20, 0))       # 我的局部 → 世界

# Node2D 层面还有现成的：
child.global_position            # 直接读写世界坐标
child.global_rotation
global_transform                  # 读取/设置整个变换
```

```gdscript
# 模块模板：判断鼠标是否点在我这个旋转过的矩形内
func is_mouse_over() -> bool:
    var mouse_world := get_global_mouse_position()
    var mouse_local := to_local(mouse_world)     # ★ 转到本地坐标后再判断
    # 本地坐标下矩形永远轴对齐，判定简单
    var rect := Rect2(-32, -32, 64, 64)          # 以自己为中心 64x64
    return rect.has_point(mouse_local)
```

```gdscript
# 陷阱例：用全局坐标直接和"本地矩形"比较
return Rect2(Vector2(0,0), Vector2(64,64)).has_point(get_global_mouse_position())  # ✗
# 后果：节点一移动/旋转，判定区域就跑到世界原点去了，完全错位。
# 修正：先 to_local(get_global_mouse_position()) 再做本地判定。
```

> **口诀**：**"跨坐标系比较前，先统一到同一个坐标系。"**

---

## 25.10 Vector3 与 3D 简明

### 25.10.1 Vector3 与 Vector2 的对比

`Vector3` 就是多了一个 `z` 维度。方法几乎同名。

| 项目 | Vector2 | Vector3 |
| --- | --- | --- |
| 分量 | `x, y` | `x, y, z` |
| 构造 | `Vector2(1, 2)` | `Vector3(1, 2, 3)` |
| 常量 | `ZERO / ONE / UP / DOWN / LEFT / RIGHT` | 追加 `FORWARD(0,0,-1) / BACK(0,0,1)` |
| 长度 | `length()` | 同名 |
| 归一化 | `normalized()` | 同名 |
| 点积 | `dot()` → float | `dot()` → float |
| 叉积 | `cross()` → float（标量） | `cross()` → **Vector3**（垂直两向量的向量） |
| 距离 | `distance_to()` | 同名 |
| 角度 | `angle()` / `angle_to()` | `angle_to()`（返回弧度） |
| 插值 | `lerp()` / `slerp()` | 同名 |
| 屏幕坐标 | y 向下为正 | y 向上为正 |

**关键区别一：3D 里 y 向上为正**（和 2D 屏幕坐标系相反！），"向上飞"是 y 变大。

**关键区别二：3D 的 `cross` 返回向量**，方向遵循**右手定则**：

```
   y
   │   z 指向屏幕外（朝向观察者）
   │ ╱
   │╱
   └──────── x
   右手：x 叉 y = z
```

```gdscript
# 3D 叉积例子
print(Vector3.RIGHT.cross(Vector3.UP))   # → (0, 0, -1)  Godot 里 FORWARD 是 -z
```

### 25.10.2 3D 常用基础

```gdscript
# 入门例
var a := Vector3(1, 2, 3)
print(a.length())                 # → √14 ≈ 3.7417
print(a.normalized())             # → (0.267, 0.534, 0.801)
print(Vector3(0,1,0).dot(Vector3(1,0,0)))  # → 0.0

# 实战例：3D 里让敌人朝玩家移动（在水平面上）
func _physics_process(delta: float) -> void:
    var to_player: Vector3 = player.global_position - global_position
    to_player.y = 0.0                              # 只在水平面移动，忽略高度差
    if to_player.length() > 1.0:
        var dir := to_player.normalized()
        global_position += dir * speed * delta
```

```gdscript
# 实战例：3D 朝向目标（用 look_at，内部帮你算好旋转）
look_at(target.global_position, Vector3.UP)   # ★ Node3D 方法
```

```gdscript
# 陷阱例：把 2D 的 y 向下习惯带到 3D
position.y += 1  # 以为在"下移"，其实在 3D 里是向上！
# 后果：角色浮空、掉落方向反了。
# 修正：3D 里向下是 position.y -= 1，或统一用 gravity 向量处理。
```

> 3D 够用就行：会构造、会加减、会用 `normalized/dot/length/look_at`，就能应付绝大多数移动、指向、距离需求。

---

## 25.11 随机数专题

### 25.11.1 全局随机函数

```gdscript
print(randf())            # → 0.0 ~ 1.0 之间的浮点（含 0，不含 1）
print(randf_range(5, 10)) # → 5.0 ~ 10.0 之间的浮点
print(randi())            # → 0 ~ 2^32-1 的无符号随机整数
print(randi_range(1, 6))  # → 1 ~ 6 之间的整数（模拟骰子，两端都包含）
print(randfn(0.0, 1.0))   # → 正态分布：均值 0，标准差 1（钟形曲线）
```

正态分布 `randfn` 图示：

```
         ▁▄███▄▁          
     ▁▄█████████▄▁
   ▄███████████████▄
 ───────────────────────▶
 -3σ  -1σ  μ  +1σ  +3σ
      大多数值落在 μ±2σ 附近
```

**实战选择**：伤害浮动一般用 `randf_range`（均匀）；掉落物的稀有度分布更像 `randfn`（大量普通、极少极品）。

### 25.11.2 randomize() 与 seed

Godot 启动时默认种子是**固定的**（每次运行随机结果相同）。要让每次运行都不一样，必须调用 `randomize()`：

```gdscript
func _ready() -> void:
    randomize()   # ★ 用当前时间等作为种子，让每次运行结果不同
    print(randi_range(1, 100))
```

`seed()` 则用来**固定**随机序列，方便复现问题：

```gdscript
func _ready() -> void:
    seed(12345)   # 固定种子 → 每次运行随机结果一模一样（便于调试）
    print(randi_range(1, 100))   # 每次都得到同一个数
```

| 需求 | 做法 |
| --- | --- |
| 每次玩都不同 | `randomize()` |
| 复现某个 bug 的随机场景 | `seed(固定值)` |
| 多套互不干扰的随机 | 用多个 `RandomNumberGenerator` 实例 |

### 25.11.3 RandomNumberGenerator 类（独立种子实例）

全局 `randi()` 用的是"全局状态"，多处使用会互相影响。想"各玩各的"，就自己 `new` 一个实例：

```gdscript
# 模块模板：独立的随机数生成器
var rng := RandomNumberGenerator.new()

func _ready() -> void:
    rng.randomize()                       # 或 rng.seed = 在一个固定值
    print(rng.randi_range(1, 6))
    print(rng.randf_range(0.0, 1.0))
    print(rng.randfn(0.0, 1.0))
    # 实例方法名与全局一致：randi / randf / randi_range / randf_range / randfn / randf_weighted...
```

**为什么用实例**：地图生成、战斗掉落、音效变调各用各的种子，互不干扰，还方便单独复现。

### 25.11.4 加权随机模板（weighted_pick）

需求：普通怪 70%、精英 25%、Boss 5%。做法是"把区间首尾相接"：

```
概率区间（总宽 1.0）
[0────────0.70][0.70────0.95][0.95──1.0]
   普通 70%        精英 25%      Boss 5%
```

```gdscript
# 模块模板：加权随机（class_name 可直接抄走）
class_name WeightedPicker
extends RefCounted

# items 与 weights 一一对应
static func pick(items: Array, weights: Array, rng: RandomNumberGenerator = null) -> Variant:
    assert(items.size() == weights.size(), "items 和 weights 数量必须一致")
    var total: float = 0.0
    for w in weights:
        total += float(w)

    var r: float = (rng if rng else _default_rng()).randf() * total
    var acc: float = 0.0
    for i in items.size():
        acc += float(weights[i])
        if r < acc:
            return items[i]
    return items.back()   # 浮点误差兜底

static var _rng: RandomNumberGenerator
static func _default_rng() -> RandomNumberGenerator:
    if _rng == null:
        _rng = RandomNumberGenerator.new()
        _rng.randomize()
    return _rng
```

```gdscript
# 使用
var loot := WeightedPicker.pick(
    ["普通", "精英", "Boss"],
    [70, 25, 5]
)
print(loot)  # → 大概率是 "普通"
```

### 25.11.5 shuffle 洗牌 与 不重复抽牌（bag 模式）

```gdscript
# 入门例：洗牌
var deck := [1, 2, 3, 4, 5, 6]
deck.shuffle()          # ★ 原地打乱
print(deck)             # → 打乱后的顺序，如 [4, 1, 6, 2, 5, 3]
```

"洗牌后依次抽"能保证一轮内不重复，但一轮抽完才重洗，会让稀有牌出得集中。**bag 模式**（抽牌袋）更常用于"不重复随机"：

```gdscript
# 模块模板：抽牌袋（洗好的牌抽完前不重复）
class_name RandomBag
extends RefCounted

var _pool: Array = []
var _bag: Array = []

func _init(pool: Array) -> void:
    _pool = pool.duplicate()
    _bag = pool.duplicate()
    _bag.shuffle()

func draw() -> Variant:
    if _bag.is_empty():
        _bag = _pool.duplicate()   # 抽完重装
        _bag.shuffle()
    return _bag.pop_back()         # 从末尾抽一张
```

```gdscript
# 使用：俄罗斯方块式随机，保证每个方块都会轮到
var bag := RandomBag.new(["I", "O", "T", "S", "Z", "J", "L"])
for i in 7:
    print(bag.draw())   # → 7 次抽完所有方块，互不重复
```

---

## 25.12 实用数学工具箱

本节每个工具都按"**现象 → 公式 → 模板**"三段式讲。

### 25.12.1 平滑跟随相机

**现象**：相机硬邦邦地钉在玩家身上，画面抖、没有重量感。
**公式**：帧率无关的指数平滑 `weight = 1 - exp(-speed * delta)`。

```gdscript
# 模块模板：SmoothCamera2D.gd
extends Camera2D
class_name SmoothCamera2D

@export var target_path: NodePath
@export var follow_speed: float = 6.0   # 越大跟得越紧

@onready var target: Node2D = get_node(target_path)

func _process(delta: float) -> void:
    if target == null:
        return
    var weight := 1.0 - exp(-follow_speed * delta)
    global_position = global_position.lerp(target.global_position, weight)
```

### 25.12.2 阻尼 / 弹性运动

**现象**：角色停下时"急刹"，不够自然。
**公式**：对速度做指数衰减，位置 += 速度 × delta。

```gdscript
# 模块模板：带阻尼的移动
@export var accel: float = 1200.0     # 加速度
@export var damping: float = 8.0      # 阻尼系数
var vel := Vector2.ZERO

func _physics_process(delta: float) -> void:
    var input_dir := Input.get_vector("left", "right", "up", "down")
    vel += input_dir * accel * delta               # 施加推力
    vel = vel.lerp(Vector2.ZERO, 1.0 - exp(-damping * delta))  # 阻尼拉回 0
    global_position += vel * delta
```

**弹性（弹簧）**：让相机带一点"滞后回弹"：

```gdscript
# 模块模板：弹簧跟随（二阶阻尼）
@export var stiffness: float = 60.0    # 弹簧刚度
@export var damping_ratio: float = 12.0
var _vel := Vector2.ZERO

func spring_to(target: Vector2, delta: float) -> void:
    var force := (target - global_position) * stiffness      # 胡克定律
    force -= _vel * damping_ratio                            # 阻尼力
    _vel += force * delta
    global_position += _vel * delta
```

### 25.12.3 正弦波漂浮与呼吸动画

**现象**：道具上下浮动、UI 呼吸缩放。
**公式**：`offset = sin(时间 * 频率) * 幅度`。

```gdscript
# 模块模板：漂浮道具
@export var amplitude: float = 8.0     # 幅度（像素）
@export var frequency: float = 2.0     # 频率（越快越抖）
var _t: float = 0.0
var _base_y: float

func _ready() -> void:
    _base_y = position.y

func _process(delta: float) -> void:
    _t += delta
    position.y = _base_y + sin(_t * frequency) * amplitude

# 呼吸缩放（同一招，用在 scale 上）
func breathe(delta: float) -> void:
    _t += delta
    var s := 1.0 + sin(_t * 3.0) * 0.05
    scale = Vector2(s, s)
```

```
sin 波形
 1 ┤    ╭─╮         ╭─╮
   │  ╱    ╲      ╱    ╲
 0 ┼─╯      ╰────╯      ╰──▶ 时间
   │
-1 ┤
  周期 T = 2π / 频率
```

### 25.12.4 屏幕震动

**现象**：受击、爆炸时相机抖动。
**公式**：随机方向 + 随时间衰减的幅度。

```gdscript
# 模块模板：屏幕震动（配合 Camera2D）
extends Camera2D
class_name ShakyCamera

var _shake: float = 0.0          # 当前震动强度
@export var decay: float = 8.0   # 衰减速度

func shake(amount: float) -> void:
    _shake = maxf(_shake, amount)   # 取较大者，连续受击不叠加爆炸

func _process(delta: float) -> void:
    if _shake > 0.01:
        _shake = maxf(_shake - decay * delta * _shake, 0.0)  # 指数衰减
        var offset := Vector2(
            randf_range(-1.0, 1.0),
            randf_range(-1.0, 1.0)
        ).normalized() * _shake
        offset = offset.round()      # 取整避免画面撕裂
        offset_pos = offset          # Camera2D 的局部偏移属性
    else:
        _shake = 0.0
        offset_pos = Vector2.ZERO
```

### 25.12.5 圆周运动与环绕

**现象**：卫星护卫绕玩家转、敌人做圆周巡逻。
**公式**：`x = 中心.x + 半径 * cos(角)`, `y = 中心.y + 半径 * sin(角)`。

```gdscript
# 模块模板：绕中心旋转的护卫
@export var center_path: NodePath
@export var radius: float = 60.0
@export var angular_speed: float = 2.0   # 弧度/秒
@export var phase: float = 0.0           # 初始相位（多护卫错开）

@onready var center: Node2D = get_node(center_path)
var _angle: float = 0.0

func _process(delta: float) -> void:
    _angle += angular_speed * delta
    var a := _angle + phase
    global_position = center.global_position + Vector2(cos(a), sin(a)) * radius
```

```
        ┌─ 半径 r ─┐
        ●──────────●
       ╱  中心       ╲
      │    (cx,cy)     │
       ╲              ╱
        ●──────────●
   pos = 中心 + (cos a, sin a) * r
```

**多个护卫均匀分布**：给每个护卫设 `phase = i * TAU / count`（`TAU = 2π`）。

### 25.12.6 菲波那契 / 黄金角散布（花瓣弹幕排列）

**现象**：子弹、花瓣、粒子从一个点均匀散开，不重叠不扎堆。
**公式**：黄金角 `≈ 137.507°`，第 i 个点：`angle = i * 黄金角`，`radius = 间距 * sqrt(i)`。

```gdscript
# 模块模板：黄金角均匀散布（向日葵种子排列）
class_name GoldenSpread
extends RefCounted

const GOLDEN_ANGLE := 2.399963229728653   # 弧度，≈137.507°

# count 个点的偏移量数组
static func spread(count: int, spacing: float = 30.0) -> Array[Vector2]:
    var out: Array[Vector2] = []
    for i in count:
        var angle := i * GOLDEN_ANGLE
        var radius := spacing * sqrt(float(i))
        out.append(Vector2(cos(angle), sin(angle)) * radius)
    return out
```

```gdscript
# 使用：生成花瓣状排列的子弹
var offsets := GoldenSpread.spread(16, 24.0)
for off in offsets:
    spawn_bullet(global_position + off)
```

```
黄金角散布效果（越往外越稀疏但不留空）
        ●   ●
     ●    ●    ●
        ●   ●
     ●    ●    ●
        ●   ●
   ● 环绕但不扎堆，像向日葵种子
```

> **为什么是黄金角**：它是最"无理"的角度比例，反复旋转时点几乎不会重合，因此分布最均匀，最适合做弹幕、粒子初始位置。

---

## 25.13 本章综合模板：MathUtils 静态工具类

下面是把本章所有常用工具**汇聚一处**的静态类，直接抄进你的项目就能用。

```gdscript
# MathUtils.gd —— 游戏数学工具箱（Godot 4.x）
# 用法：MathUtils.xxx(...)
class_name MathUtils
extends RefCounted

const TAU := 2.0 * PI                       # 整圆弧度
const GOLDEN_ANGLE := 2.399963229728653     # 黄金角（弧度）

# ---------- 向量基础 ----------

# 安全归一化：零向量时返回 fallback，避免"卡死"
static func safe_normalize(v: Vector2, fallback: Vector2 = Vector2.ZERO) -> Vector2:
    return fallback if v.is_zero_approx() else v.normalized()

# 从 a 指向 b 的单位方向向量
static func dir(a: Vector2, b: Vector2) -> Vector2:
    return safe_normalize(b - a)

# 是否在指定半径内（用平方比较，省开方）
static func within_range(a: Vector2, b: Vector2, radius: float) -> bool:
    return a.distance_squared_to(b) <= radius * radius

# ---------- 视野 / 角度 ----------

# 目标是否在"朝向 fwd、半角 half_angle_rad、距离 max_dist"的视野锥内
static func in_cone(origin: Vector2, fwd: Vector2, target: Vector2,
        half_angle_rad: float, max_dist: float) -> bool:
    var to_target := target - origin
    if to_target.length_squared() > max_dist * max_dist:
        return false
    var d := safe_normalize(fwd).dot(safe_normalize(to_target))
    return d >= cos(half_angle_rad)

# 目标在左侧还是右侧：-1 左, 0 正前/后, 1 右
static func side_of(fwd: Vector2, target_dir: Vector2) -> int:
    var c := fwd.cross(target_dir)
    if absf(c) < 0.001:
        return 0
    return 1 if c > 0.0 else -1

# ---------- 插值 / 平滑 ----------

# 帧率无关的指数平滑权重（配 lerp 用）
static func smooth_weight(speed: float, delta: float) -> float:
    return 1.0 - exp(-speed * delta)

# 帧率无关的平滑跟随
static func exp_smooth(from: Vector2, to: Vector2, speed: float, delta: float) -> Vector2:
    return from.lerp(to, smooth_weight(speed, delta))

# 平滑旋转（自动走最短角路径）
static func smooth_angle(from_rad: float, to_rad: float, speed: float, delta: float) -> float:
    return lerp_angle(from_rad, to_rad, smooth_weight(speed, delta))

# 把 [a,b] 区间内的 v 重新映射到 [c,d]
static func remap_clamped(v: float, a: float, b: float, c: float, d: float) -> float:
    return c + (d - c) * clampf(inverse_lerp(a, b, v), 0.0, 1.0)

# ---------- 运动模式 ----------

# 圆周位置
static func orbit(center: Vector2, radius: float, angle_rad: float) -> Vector2:
    return center + Vector2(cos(angle_rad), sin(angle_rad)) * radius

# 正弦漂浮偏移（返回给 position 用）
static func bob(time: float, amplitude: float, frequency: float) -> Vector2:
    return Vector2(0.0, sin(time * frequency) * amplitude)

# 黄金角散布（弹幕/粒子初始位置）
static func golden_spread(count: int, spacing: float = 30.0) -> Array[Vector2]:
    var out: Array[Vector2] = []
    for i in count:
        var a := i * GOLDEN_ANGLE
        out.append(Vector2(cos(a), sin(a)) * (spacing * sqrt(float(i))))
    return out

# ---------- 随机工具 ----------

# 加权随机：items 与 weights 一一对应
static func weighted_pick(items: Array, weights: Array,
        rng: RandomNumberGenerator = null) -> Variant:
    var total := 0.0
    for w in weights:
        total += float(w)
    var r := (rng if rng != null else _default_rng()).randf() * total
    var acc := 0.0
    for i in items.size():
        acc += float(weights[i])
        if r < acc:
            return items[i]
    return items.back()

# 随机单位方向（2D）
static func random_dir2(rng: RandomNumberGenerator = null) -> Vector2:
    var a := (rng if rng != null else _default_rng()).randf() * TAU
    return Vector2(cos(a), sin(a))

static var _rng: RandomNumberGenerator
static func _default_rng() -> RandomNumberGenerator:
    if _rng == null:
        _rng = RandomNumberGenerator.new()
        _rng.randomize()
    return _rng
```

```gdscript
# 使用示例：一个会追人、会转身、带视野判定的敌人
extends CharacterBody2D

@export var speed: float = 120.0
@export var turn_speed: float = 6.0
@export var view_dist: float = 320.0

@onready var player: Node2D = get_tree().get_first_node_in_group("player")

func _physics_process(delta: float) -> void:
    if player == null:
        return

    # 1) 视野判定：面朝方向 ±45° 内、距离 320 内才追
    var fwd := Vector2.RIGHT.rotated(rotation)
    var can_see := MathUtils.in_cone(
        global_position, fwd, player.global_position,
        deg_to_rad(45.0), view_dist
    )

    if can_see:
        # 2) 平滑转身朝向玩家
        rotation = MathUtils.smooth_angle(
            rotation,
            (player.global_position - global_position).angle(),
            turn_speed, delta
        )
        # 3) 朝前移动
        velocity = Vector2.RIGHT.rotated(rotation) * speed
    else:
        velocity = velocity.move_toward(Vector2.ZERO, speed * delta * 4.0)

    move_and_slide()
```

---

## 本章小结

1. **游戏里 90% 的数学只有向量加减乘除 + 勾股定理**，不需要高等数学，别被"数学"两个字吓退。
2. **`Vector2` 是值类型**：赋值会复制，`a = b` 之后改 `b` 不影响 `a`；统一用 `目标 - 自己` 得到"指向目标"的方向。
3. **向量长度就是勾股定理**：`length()` 会开方，纯比较大小时用 `length_squared()` 省掉开方。
4. **移动前必须归一化**：否则斜向 `(1,1)` 长度是 `√2 ≈ 1.414`，斜着走比直着快 41%，这是经典陷阱。
5. **零向量归一化要兜底**：`Vector2.ZERO.normalized()` 返回 `(0,0)`，不加判断会导致角色卡死，用 `is_zero_approx()` 防御。
6. **点积 `dot` 判断方向关系**：单位向量下 `>=0` 大致同向、`=0` 垂直、`<0` 大致反向；视野锥判定用它，比算角度更高效。
7. **叉积 `cross`（2D 返回标量）判断左右**：正负号表示目标在顺时针/逆时针一侧，配合角度可实现平滑转身。
8. **角度一律用弧度**：`rad_to_deg`/`deg_to_rad` 换算；角度插值永远用 `lerp_angle` 而不是 `lerp`，否则会绕远路。
9. **`position` 和 `rotation` 相互独立**：想让朝向影响移动，必须手动 `Vector2.RIGHT.rotated(rotation)` 得到前方向量。
10. **每帧 `lerp(a, b, 0.1)` 帧率不独立**：正确写法是 `lerp(a, b, 1 - exp(-speed * delta))`，高刷屏和 60Hz 表现一致。
11. **坐标系要统一**：比较坐标前先 `to_local` / `to_global` 转换到同一坐标系；2D 屏幕 y 向下为正，3D 世界 y 向上为正，两者相反。
12. **`Vector3` 就是多一维的 `Vector2`**：方法同名，`cross` 在 3D 返回向量并遵循右手定则，`look_at` 可一步朝向目标。
13. **随机要分清用途**：每次玩都不同用 `randomize()`，复现问题用固定 `seed()`，多套互不干扰用独立的 `RandomNumberGenerator` 实例。
14. **加权随机的本质是"概率区间首尾相接"**，抽牌袋（bag）模式能保证一轮内不重复，比纯随机更公平。
15. **常用运动模式都有公式**：圆周 `cos/sin` 参数方程、正弦漂浮、指数阻尼、黄金角散布——`MathUtils` 已把它们全部封装，随取随用。
---

# 第 26 章：Tween 补间动画完全教程

> 如果说 `AnimationPlayer` 是"手绘动画师"，那么 `Tween` 就是"会算插值的程序化动画师"。你只需要告诉它"这个属性从现在的值，在 0.4 秒内变成目标值"，剩下每帧的中间值它全替你算。UI 弹出、按钮悬停、受伤闪红、伤害数字飘字、摄像机震动、道具旋转上升……这些"看一眼就知道怎么动"的小动画，用 Tween 写只需要几行，而且改起来极其方便。
>
> ⚠️ **重要前提**：Godot 4 的 Tween 与 Godot 3 **完全是两个东西**。Godot 3 那套 `Tween` 节点 + `interpolate_property()` + `start()` 的写法在 Godot 4 里已经被彻底移除。本书只讲 **Godot 4.x 新语法**，凡是看到 "Node 类型的 Tween"、"Tween 节点"、"interpolate_property"，请一律当成过时资料。

---

## 26.1 什么是补间动画（Tween）

### 26.1.1 从"插值"这个词说起

"补间"（Tween，来自 in-between）原本是传统动画行业的术语：原画师只画关键帧（起点、终点），中间那些过渡帧由助手补上。计算机接管这份工作后，你只要给出**起点、终点、持续时间**，引擎就能在每一帧算出一个中间值。

假设你要让一个 UI 面板从屏幕外滑入：

| 你要告诉引擎的 | 具体内容 |
| --- | --- |
| 动谁 | 面板节点 |
| 动哪个属性 | `position` |
| 从哪开始 | 当前的 `position`（屏幕外，比如 `(-300, 0)`） |
| 到哪结束 | 目标值 `(0, 0)` |
| 用多久 | `0.4` 秒 |
| 用什么节奏 | 先快后慢（缓出） |

这就是一条完整的需求描述。用 Tween 写出来：

```gdscript
# 入门例：让面板从左侧滑入
func slide_in(panel: Control) -> void:
	var tween := panel.create_tween()          # 创建一条补间
	tween.tween_property(panel, "position", Vector2.ZERO, 0.4) \
		.set_trans(Tween.TRANS_CUBIC)          # 速度曲线：立方
		.set_ease(Tween.EASE_OUT)              # 缓动方向：缓出
	# → 0.4 秒内，panel.position 从当前值平滑过渡到 (0, 0)
```

### 26.1.2 为什么不让引擎"一帧到位"？

如果直接把 `panel.position = Vector2.ZERO`，那就叫"瞬移"——第 N 帧还在屏幕外，第 N+1 帧已经在目标位置，中间没有任何过渡。玩家看到的是画面"跳"了一下。补间动画的价值就是**把这个跳跃摊开成很多帧的连续变化**：

```
瞬移（直接赋值）：
帧:   N        N+1
位置: (-300) ─────────► (0)          ← 一帧跨完，视觉上就是"闪现"

补间（Tween，0.4 秒 ≈ 24 帧@60fps）：
帧:   N    N+1   N+2   ...   N+23   N+24
位置: -300  -280  -255  ...    -5     0    ← 每帧挪一点，视觉上是"滑进来"
```

### 26.1.3 自己用 `_process` 手写不行吗？

行，但很啰嗦。手写插值你需要维护"开始时间、起始值、目标值、是否结束"这些状态：

```gdscript
# 陷阱例：手写插值——能跑，但容易出错
var _t := 0.0
var _start := Vector2.ZERO
var _target := Vector2.ZERO
var _animating := false

func start_move() -> void:
	_start = position
	_target = Vector2(100, 0)
	_t = 0.0
	_animating = true

func _process(delta: float) -> void:
	if not _animating:
		return
	_t += delta
	var w := clampf(_t / 0.4, 0.0, 1.0)   # 归一化进度 0→1
	position = _start.lerp(_target, w)
	if w >= 1.0:
		_animating = false
```

**后果**：每个要动的属性都要一套这种样板；多个动画要管理多套状态；要加缓动函数还得自己实现曲线；中途要改目标值、要暂停、要串行接下一段，全是额外工作量。**这正是 Tween 存在的意义**——把上面这一坨浓缩成一行。

### 26.1.4 Tween 适合什么、不适合什么

| 场景 | 推荐 | 原因 |
| --- | --- | --- |
| UI 动效（弹出、滑入、淡入淡出、缩放） | ✅ Tween | 属性明确、时长短、程序化生成 |
| 按钮 hover / press 反馈 | ✅ Tween | 一行搞定，随时可打断 |
| 伤害数字飘字、金币飞向图标 | ✅ Tween | 位置 + 透明度组合，短平快 |
| 摄像机 punch / 震动 | ✅ Tween | 用偏移的衰减补间即可 |
| 属性数值的平滑变化（音量、进度、Shader 参数） | ✅ Tween | `tween_method` 的拿手好戏 |
| 程序化生成的简单序列（连续几段） | ✅ Tween | `await tween.finished` 串起来 |
| 复杂角色骨骼动画 | ❌ 用 AnimationPlayer | 关键帧多、需要美术在编辑器里调 |
| 需要动画混合（走跑切换、上/下半身分离） | ❌ 用 AnimationTree | Tween 不会混合两套动画 |
| 需要精确音频同步的逐帧动画 | ❌ 用 AnimationPlayer | 关键帧可对齐到时间轴 |
| 需要导入外部动画（glTF / FBX） | ❌ 用 AnimationPlayer | 动画数据来自外部资源 |

一句话决策：**"我自己能在代码里一句话说清怎么动"→ Tween；"这是美术做的、要混合、要导入"→ AnimationPlayer / AnimationTree。**（详见 26.12 的完整对比表）

---

## 26.2 创建 Tween 的唯一正确姿势

### 26.2.1 Godot 4 只有一种创建方式

在 Godot 4 里，创建 Tween **只有一个入口**：从某个节点或 SceneTree 上 `create_tween()`。

```gdscript
# ✅ 正确：从节点创建（最常用）
var tween := create_tween()               # 在 Node 脚本里直接调用
# 等价于：get_tree().create_tween().bind_node(self)

# ✅ 正确：从一个具体节点创建（写工具类/静态方法时常用）
var tween2 := some_node.create_tween()

# ✅ 正确：从 SceneTree 创建（要手动绑定节点时）
var tween3 := get_tree().create_tween()
tween3.bind_node(self)                    # 让它跟随 self 的生死
```

```gdscript
# ❌ 错误：Godot 4 已经禁止 new Tween()
var tween := Tween.new()
# → 运行时报错：Tween 不能被直接实例化（Tween cannot be instantiated directly）
```

**为什么禁止？** 因为 Godot 4 的 Tween 不是"独立存在的对象"，而是**由 SceneTree 统一管理、并绑定到某个节点上**的动画控制器。它的生命周期、何时推进、何时销毁，全部由引擎掌控，不允许你绕过 SceneTree 自己造一个。

### 26.2.2 SceneTreeTween 的由来

如果你在网上看到 `SceneTreeTween` 这个词，不用慌，它不是另一套 API。历史上 Godot 4.0 的早期预览版把新 Tween 类命名为 `SceneTreeTween`，正式版发布时改名为 `Tween`。所以：

```
Godot 3：Tween 是一个 Node  →  加到场景树里当节点用
Godot 4：Tween 是一个 RefCounted  →  由 SceneTree 创建并持有，绑定到节点
          （4.0 预览期曾叫 SceneTreeTween，正式版改回 Tween）
```

记住结论：**一个 Tween 实例 = 一条由 SceneTree 托管的补间时间线，它一定归属于某个节点。**

### 26.2.3 tween 与绑定节点的"生死关系"（必考）

这是新手最容易踩的坑，也是 Tween 最优雅的设计之一：

> **Tween 绑定的节点一旦被释放（`queue_free()` 或 `free()`），这条 Tween 会自动失效（`is_valid()` 变 `false`），不会继续报错。**

```gdscript
# 实战例：绑定关系带来的"自动安全"
func spawn_popup() -> void:
	var popup := Label.new()
	add_child(popup)
	var tween := popup.create_tween()                 # 绑定到 popup
	tween.tween_property(popup, "position", popup.position + Vector2(0, -60), 0.6)
	tween.parallel().tween_property(popup, "modulate:a", 0.0, 0.6)
	tween.tween_callback(popup.queue_free)            # 播完销毁自己
	# → popup 被 free 后，这条 tween 自动结束，不会“访问已释放对象”崩溃
```

对比一下：如果你手动给一个**已经 free 掉的节点**写 `tween_property`，那才会报错。所以绑定关系是"保护"而不是"隐患"。26.11 会专门讲"手动绑定了别人的节点"这种反例。

### 26.2.4 入门 / 实战 / 陷阱三连

```gdscript
# 【入门例】最简：让图标转一圈
func spin_icon(icon: TextureRect) -> void:
	var tween := icon.create_tween()
	tween.tween_property(icon, "rotation", TAU, 1.0)   # TAU = 2π
	# → 1 秒内 rotation 从当前值转到一整圈，图标顺时针转一圈

# 【实战例】封装成"通用淡出并销毁"的静态风格工具
func fade_out_and_free(node: CanvasItem, dur := 0.3) -> void:
	var tween := node.create_tween()
	tween.tween_property(node, "modulate:a", 0.0, dur)
	tween.tween_callback(node.queue_free)

# 【陷阱例】沿用 Godot 3 的写法
func wrong_way() -> void:
	var tween := Tween.new()                 # ❌ 直接实例化
	add_child(tween)                         # ❌ Tween 已不是 Node，add_child 也不对
	tween.interpolate_property(self, "position", position, Vector2.ZERO, 1.0)  # ❌ 方法不存在
	tween.start()                            # ❌ 方法不存在
# 后果：三处全报错，游戏直接跑不起来。
# 修正：改用 §26.2.1 的 create_tween() + tween_property()。
```

---

## 26.3 tween_property 详解：属性路径语法全解

`tween_property(对象, 属性路径, 目标值, 时长秒数)` 是 Tween 最核心的方法。它平时接收的是**属性路径字符串**，而不是属性本身——这一点决定了它能做很多花活，也埋了不少坑。

### 26.3.1 属性路径的三种粒度

| 写法 | 含义 | 适用类型 |
| --- | --- | --- |
| `"position"` | 整个属性一起变 | `Vector2` / `Vector3` / `Color` 等 |
| `"position:x"` | 只改 `position` 的 `x` 分量 | `Vector2` / `Vector3` |
| `"position:y"` | 只改 `position` 的 `y` 分量 | `Vector2` / `Vector3` |
| `"modulate:a"` | 只改 `modulate` 的 alpha（透明度） | `Color` |
| `"modulate:r"` / `:g` / `:b` | 只改对应颜色通道 | `Color` |
| `"scale:x"` / `"scale:y"` | 只改缩放的单个轴 | `Vector2` |
| `"material:shader_param/amount"` | 改材质里的 shader 参数 | `ShaderMaterial` |
| `"theme_override_constants/separation"` | 改主题覆盖常量 | `Control` |

```gdscript
# 入门例：三种粒度对比
func demo_paths(c: Control) -> void:
	var tween := c.create_tween()
	tween.tween_property(c, "modulate:a", 0.0, 0.5)            # 只把透明度降到 0
	tween.tween_property(c, "position:x", 300.0, 0.5)          # 只把 x 移过去，y 不动
	tween.tween_property(c, "scale", Vector2(1.2, 1.2), 0.3)   # 整条 scale 一起缩放
```

> ⚠️ **关于 `"scale:xy"`**：网上和某些资料会写 `"scale:xy"` 表示"同时改 x 和 y"。**这在 Godot 4 里并不成立**——`Vector2` 暴露的子属性只有单个的 `x` 和 `y`，没有 `xy` 这个合并子属性。写 `"scale:xy"` 通常**不会报错**（因为路径解析失败时 Tween 会静默跳过），但**动画就是不动**，非常难排查。正确做法：要一起改就写整条 `"scale"`；要单轴改就写 `"scale:x"` / `"scale:y"`。（详见 26.11 陷阱五）

### 26.3.2 目标值类型必须与属性匹配

路径解析没问题，但目标值类型对不上，同样会出问题：

```gdscript
var tween := node.create_tween()
tween.tween_property(node, "position:x", Vector2(100, 0), 0.5)   # ❌ 目标值类型错
# 后果：x 分量期待 float，却给了 Vector2，动画不生效或报类型提示。
```

| 属性路径 | 正确目标值类型 | 错误示例 |
| --- | --- | --- |
| `"position"` | `Vector2` | `100.0` ❌ |
| `"position:x"` | `float` | `Vector2(100,0)` ❌ |
| `"modulate:a"` | `float`（0.0~1.0） | `Color(...)` ❌ |
| `"scale"` | `Vector2` | `2.0` ❌ |

### 26.3.3 from_current()：把起点显式钉在"当前值"

默认情况下，`tween_property` 的**起点就是开始执行那一刻该属性的当前值**。但有时文件里定义的默认值和"开始时的值"不一致，或者你想明确表达"从当下出发"，就可以用 `.from_current()`：

```gdscript
var tween := node.create_tween()
tween.tween_property(node, "position", Vector2(200, 0), 0.5).from_current()
# → 起点 = 出发那一刻 node.position（显式声明，可读性更好）
```

> 提示：`from()` 也可以指定一个固定起点（`from(Vector2(0,0))`），但初学阶段用 `.from_current()` 表达意图即可。

### 26.3.4 as_relative()：相对值——"在当前值基础上加多少"

这是最容易搞混的一对。看表：

| 方法 | 目标值的含义 | 例子 | 结果 |
| --- | --- | --- | --- |
| 默认（不写） | **绝对目标值** | `tween_property(n,"position",Vector2(100,0),1.0)` | 无论现在在哪，最后一定到 `(100,0)` |
| `.as_relative()` | **相对增量** | `tween_property(n,"position",Vector2(100,0),1.0).as_relative()` | 在**当前值**基础上再加 `(100,0)` |

```gdscript
# 实战例：伤害数字上飘 60 像素（相对）
func float_up(label: Label) -> void:
	var tween := label.create_tween()
	tween.tween_property(label, "position", Vector2(0, -60), 0.8).as_relative()
	tween.parallel().tween_property(label, "modulate:a", 0.0, 0.8)
	# → 不管 label 出生在哪个坐标，都往上飘 60 像素并渐隐
	#   如果用绝对值，就得先算出“当前位置 - 60”，麻烦且易错
```

```gdscript
# 陷阱例：把相对值当绝对值用
var tween := node.create_tween()
tween.tween_property(node, "position", Vector2(0, -60), 0.8).as_relative()
# ❌ 你以为它"移到屏幕上方"，实际是"往上挪 60 像素"
# 修正：要绝对定位就删掉 .as_relative()，要绝对坐标就传目标坐标本身。
```

`as_relative()` 对 float 属性同样适用：

```gdscript
tween.tween_property(icon, "rotation", TAU, 1.0).as_relative()
# → 当前角度再转一整圈，而不是"转到 TAU"（两者对同一角度等价，但连续触发时差别巨大）
```

---

## 26.4 序列与并行：Tween 的时间线编排

Tween 内部维护一条**时间线**。默认情况下，你连续调用的 `tween_property` 是**串行**的——一个接一个。

### 26.4.1 默认串行（链式）

```gdscript
func seq_demo(n: Node2D) -> void:
	var tween := n.create_tween()
	tween.tween_property(n, "position", Vector2(100, 0), 0.4)
	tween.tween_property(n, "position", Vector2(100, 100), 0.4)
	tween.tween_property(n, "position", Vector2(0, 100), 0.4)
	# → 先右 0.4s，再下 0.4s，再左 0.4s，总时长 1.2s（像个“L”形路线）
```

ASCII 时间线：

```
时间轴 →  0.0    0.4    0.8    1.2
[右移]    ████████
[下移]           ████████
[左移]                   ████████
          └─ 一个接一个，总时长 = 三段之和 ─┘
```

### 26.4.2 `parallel()`：让"下一个"与"上一个"并行

`parallel()` 的作用是：**让紧跟在它后面的那一个 tweener，与之前那一个同时开始。**

```gdscript
func fade_and_move(n: CanvasItem) -> void:
	var tween := n.create_tween()
	tween.tween_property(n, "position", Vector2(200, 0), 0.5)
	tween.parallel().tween_property(n, "modulate:a", 0.0, 0.5)
	# → 移动与淡出同时进行，总时长仍是 0.5s（不是 1.0s）
```

ASCII 时间线：

```
时间轴 →  0.0        0.5
[position] ████████████
[modulate] ████████████   ← parallel() 让淡出与移动同时开跑
           └─ 总时长 = 0.5s ─┘
```

### 26.4.3 `set_parallel(true)`：整条 Tween 全部并行

如果你想让**后续所有** tweener 都并行，不想一个个写 `parallel()`，就用 `set_parallel(true)`：

```gdscript
func burst(n: CanvasItem) -> void:
	var tween := n.create_tween()
	tween.set_parallel(true)                                   # 之后默认全并行
	tween.tween_property(n, "position", Vector2(80, -80), 0.6)
	tween.tween_property(n, "modulate:a", 0.0, 0.6)
	tween.tween_property(n, "scale", Vector2(1.5, 1.5), 0.6)
	# → 三个属性一起变化
	tween.chain().tween_interval(0.2)                           # chain() 切回串行
	# → 全部结束后，再等 0.2s
```

**`chain()` 的妙用**：在 `set_parallel(true)` 之后，想让某个"之后"的动作重新变回串行，就调用 `chain()`（返回 tween 本身，可继续链式）。这是 26.4 里最实用的技巧之一。

### 26.4.4 并行分支的延迟启动（俗称 "parallel_delayed"）

Godot 4 **没有**一个叫 `parallel_delayed()` 的 API。所谓"并行 + 各自延迟"，标准做法是：`set_parallel(true)` 让它们同时插队，再用每个 tweener 的 `set_delay()` 错开启动时刻。

```gdscript
func staggered_bars(bars: Array[Control]) -> void:
	var tween := create_tween()
	tween.set_parallel(true)
	var i := 0
	for bar in bars:
		tween.tween_property(bar, "scale:x", 1.0, 0.4).set_delay(i * 0.1)
		i += 1
	# → 所有柱子并行，但每根比上一根晚 0.1s 开始（“波浪式”依次展开）
```

ASCII 时间线（3 根柱子，各延迟 0.1s 启动）：

```
时间轴 →   0.0  0.1  0.2  0.3  0.4  0.5  0.6
[柱1]      ████████████
[柱2]           ████████████
[柱3]                ████████████
           └──── set_parallel(true) + set_delay() ────┘
```

### 26.4.5 `tween_interval()`：在时间线里插入"纯等待"

```gdscript
func blink(n: CanvasItem) -> void:
	var tween := n.create_tween()
	tween.tween_property(n, "modulate:a", 0.0, 0.15)
	tween.tween_interval(0.1)                                  # 保持透明 0.1s
	tween.tween_property(n, "modulate:a", 1.0, 0.15)
	# → 透明 → 停一拍 → 恢复
```

**串行 vs 并行 对照总表：**

| 写法 | 效果 | 总时长（上面例子） |
| --- | --- | --- |
| 默认链式 | 串行，一个接一个 | 各段之和 |
| `parallel()` | 让**下一个**与上一个同时 | 取较长者 |
| `set_parallel(true)` | 之后**全部**并行 | 取最长者 |
| `set_parallel(true)` + `chain()` | 并行一段后切回串行 | 分段累加 |
| `tween_interval(t)` | 时间线插入等待 | 累加 t |

---

## 26.5 缓动全解：TRANS × EASE

如果你只会写时长，动画会显得"机械、匀速、像机器人"。真实世界的运动几乎都不匀速：启动要加速、到达要减速、弹回要有回弹。控制这个节奏的就是两个参数：

- `set_trans(Tween.TRANS_XXX)`：**过渡曲线**（用什么形状的数学函数做插值）
- `set_ease(Tween.EASE_XXX)`：**缓动方向**（这条曲线朝哪个方向"偏"）

### 26.5.1 十种 TRANS（过渡曲线）

| 常量 | 名称 | 手感 | 典型用途 |
| --- | --- | --- | --- |
| `Tween.TRANS_LINEAR` | 线性 | 匀速，机械 | 匀速旋转、进度条 |
| `Tween.TRANS_SINE` | 正弦 | 柔和，两头微缓 | UI 淡入淡出（默认推荐） |
| `Tween.TRANS_QUAD` | 二次 | 轻度加减速 | 通用移动 |
| `Tween.TRANS_CUBIC` | 三次 | 明显的加减速 | 面板滑入（常用） |
| `Tween.TRANS_QUART` | 四次 | 更夸张的加减速 | 强对比的入场 |
| `Tween.TRANS_QUINT` | 五次 | 极强加减速 | 强调型动效 |
| `Tween.TRANS_EXPO` | 指数 | 极陡，起步极快/极慢 | 冲刺、快速甩入 |
| `Tween.TRANS_ELASTIC` | 弹性 | 弹簧般来回振荡 | 卡通、夸张弹跳 |
| `Tween.TRANS_BOUNCE` | 弹跳 | 落地反弹 | 掉落物落地 |
| `Tween.TRANS_BACK` | 回拉 | 会"冲过头再回来" | 弹出、overshoot |

### 26.5.2 四种 EASE（缓动方向）

| 常量 | 含义 | 曲线形状（归一化进度） |
| --- | --- | --- |
| `Tween.EASE_IN` | 慢启动 | 开头平缓，结尾陡 |
| `Tween.EASE_OUT` | 慢收尾 | 开头陡，结尾平缓 |
| `Tween.EASE_IN_OUT` | 两头慢、中间快 | S 形 |
| `Tween.EASE_OUT_IN` | 两头快、中间慢 | 反 S 形（少见但可用于循环） |

ASCII 曲线示意（纵轴=已完成的进度，横轴=时间）：

```
EASE_IN（缓入：起步慢）          EASE_OUT（缓出：收尾慢）
进度                           进度
1.0 |            ●             1.0 |  ●
    |           /                  |   \
    |        ,-'                   |    `-._
    |    _,-'                      |        `-.__
0.0 ●───────► 时间            0.0 ●───────────► 时间
    起步慢，越走越快              起步快，越走越慢

EASE_IN_OUT（两头慢，中间快）   EASE_OUT_IN（两头快，中间慢）
进度                           进度
1.0 |        _,-●              1.0 |●--_        _--●
    |    _,-'                    |    `-._  _.-'
    | _,-'                       |        ~~
0.0 ●───────────► 时间        0.0 ●───────────► 时间
    S 形，最“自然”              反 S 形，循环动画偶尔用
```

### 26.5.3 组合效果：同一个 TRANS 配不同 EASE

```gdscript
# 入门例：同一段位移，四种节奏
func four_tempos(n: Node2D) -> void:
	for ease_mode in [Tween.EASE_IN, Tween.EASE_OUT, Tween.EASE_IN_OUT, Tween.EASE_OUT_IN]:
		var tween := n.create_tween()
		tween.tween_property(n, "position", Vector2(300, 0), 1.0) \
			.set_trans(Tween.TRANS_CUBIC).set_ease(ease_mode)
		await tween.finished        # 一段一段播放，感受差别
		n.position = Vector2.ZERO
```

### 26.5.4 游戏常用组合推荐表

| 动效 | 推荐 TRANS | 推荐 EASE | 说明 |
| --- | --- | --- | --- |
| UI 面板滑入 / 弹出 | `TRANS_CUBIC` 或 `TRANS_QUINT` | `EASE_OUT` | 快进慢停，最舒服 |
| UI 面板滑出 / 收起 | `TRANS_CUBIC` | `EASE_IN` | 慢起快走，干脆利落 |
| 淡入 | `TRANS_SINE` | `EASE_OUT` | 柔和、不抢眼 |
| 淡出 | `TRANS_SINE` | `EASE_IN` | 同上 |
| 按钮 hover 放大 | `TRANS_BACK` | `EASE_OUT` | 轻微 overshoot 有"弹性"手感 |
| 弹出 popup（要过冲） | `TRANS_BACK` | `EASE_OUT` | 会冲过头一点再回到位 |
| 卡通弹跳 | `TRANS_ELASTIC` | `EASE_OUT` | 弹性振荡 |
| 掉落物落地 | `TRANS_BOUNCE` | `EASE_OUT` | 真实的落地反弹 |
| 匀速旋转 / 进度条 | `TRANS_LINEAR` | `EASE_IN_OUT` | 线性即可 |
| 摄像机震动衰减 | `TRANS_EXPO` | `EASE_OUT` | 幅度快速衰减 |

```gdscript
# 实战例：使用推荐组合做"面板弹出"
func pop_up(panel: Control) -> void:
	panel.pivot_offset = panel.size * 0.5        # 从中心缩放
	panel.scale = Vector2(0.6, 0.6)
	panel.modulate.a = 0.0
	var tween := panel.create_tween()
	tween.set_parallel(true)
	tween.tween_property(panel, "scale", Vector2.ONE, 0.35) \
		.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)
	tween.tween_property(panel, "modulate:a", 1.0, 0.2) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_OUT)
	# → 缩放带一点过冲，透明度更快到位，整体干净利落
```

### 26.5.5 陷阱例：set_trans / set_ease 的作用范围

**`set_trans()` / `set_ease()` 只影响"它被调用之后创建的那个 tweener"。** 详见 26.11 陷阱一，这里先给个预告：

```gdscript
var tween := n.create_tween()
tween.tween_property(n, "position:x", 100.0, 0.5)    # ① 用的是默认 TRANS + 默认 EASE
tween.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)   # 设置只对 ② 生效
tween.tween_property(n, "position:x", 200.0, 0.5)    # ② 才带 BACK/OUT
# ❌ 常见误解：以为第一条也变成 BACK 了——并没有。
```

---

## 26.6 tween_method：让任意函数每帧被插值调用

有时候你想动的不是一个属性，而是"一段逻辑"：比如进度条的自定义刷新、Shader 参数的汇总计算、每帧根据进度做几何运算。这时候用 `tween_method(可调用对象, 起始值, 结束值, 时长)`。

它的语义是：**在时长内，把从起始值到结束值的插值结果，每帧作为参数调用一次你给的函数。**

```gdscript
# 入门例：把 0→100 的插值结果每帧喂给一个函数
func animate_score(from: int, to: int) -> void:
	var tween := create_tween()
	tween.tween_method(_on_score_changed, from, to, 1.0) \
		.set_trans(Tween.TRANS_QUAD).set_ease(Tween.EASE_OUT)
	# → 1 秒内，每帧调用 _on_score_changed(当前插值整数)

func _on_score_changed(value: int) -> void:
	$ScoreLabel.text = str(value)
```

> ⚠️ 用 `tween_method` 做数值动画时，**参数类型要与函数签名一致**。如果你传 int 起止值，回调收到的就是 int；传 float 则收到 float。

### 26.6.1 实战例 A：自定义进度条（带缓动的填充）

```gdscript
# 实战例：把 ProgressBar 从当前值平滑滚到目标值
func roll_progress(bar: ProgressBar, target: float) -> void:
	var tween := create_tween()
	tween.tween_method(
		func(v: float) -> void: bar.value = v,   # 匿名函数：Lambda
		bar.value,
		target,
		0.6
	).set_trans(Tween.TRANS_CUBIC).set_ease(Tween.EASE_OUT)
```

### 26.6.2 实战例 B：动画 Shader 参数（波浪强度）

```gdscript
# 实战例：动画一个 ShaderMaterial 的 custom 参数
func animate_dissolve(mat: ShaderMaterial) -> void:
	var tween := create_tween()
	tween.tween_method(
		func(v: float) -> void: mat.set_shader_parameter("dissolve", v),
		0.0,
		1.0,
		1.2
	).set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_IN_OUT)
	# → 1.2 秒内 dissolve 从 0 平滑到 1，做出“溶解”效果
```

### 26.6.3 实战例 C：用 Vector 驱动多个值

```gdscript
# 实战例：一次插值同时驱动位置与旋转（比两个 tween_property 更灵活）
func spiral(node: Node2D, turns: float) -> void:
	var tween := create_tween()
	tween.tween_method(
		func(t: float) -> void:
			var angle := t * TAU * turns
			node.position += Vector2(cos(angle), sin(angle)) * 2.0
			node.rotation = angle,
		0.0,
		1.0,
		2.0
	).set_trans(Tween.TRANS_LINEAR)
```

### 26.6.4 陷阱例

```gdscript
# ❌ 错误：直接把函数名写成了"调用结果"
tween.tween_method(_on_score_changed(50), 0, 100, 1.0)
# 后果：参数位置全乱，且 _on_score_changed(50) 立刻执行了一次。
# 修正：传"可调用对象"本身（函数名不加括号，或用 Callable()/匿名函数）。

# ❌ 错误：回调函数签名参数个数不匹配
tween.tween_method(_needs_two_args, 0, 100, 1.0)   # 但 _needs_two_args(a, b) 要两个参数
# 后果：参数不足，运行时报错。
# 修正：让回调只接收一个插值参数，其它数据通过 Lambda 闭包捕获。
```

---

## 26.7 tween_callback 与 tween_interval：按时间线执行动作

`tween_callback(可调用对象)` 在时间线上的"轮到它"时调用一次函数，适合在动画序列里插入副作用（播放音效、切场景、销毁节点）。

```gdscript
# 入门例：动画播完调用一个方法
func flash_then_hide(n: CanvasItem) -> void:
	var tween := n.create_tween()
	tween.tween_property(n, "modulate:a", 0.0, 0.3)
	tween.tween_callback(hide_flash)     # 淡出结束后执行
	# → 0.3s 后自动调用 hide_flash()

func hide_flash() -> void:
	print("淡出完成")
```

### 26.7.1 实战例：替代 Timer 的延迟调用

```gdscript
# 用 Tween 实现"延迟 1 秒后播放音效"（比 Timer 更轻量，且能串进动画序列）
func delayed_sfx(player: AudioStreamPlayer2D, sfx: AudioStream) -> void:
	var tween := create_tween()
	tween.tween_interval(1.0)                       # 等待 1 秒
	tween.tween_callback(func() -> void:
		player.stream = sfx
		player.play()
	)
```

**Tween 延迟调用 vs Timer 对比：**

| 维度 | `tween_interval + tween_callback` | `SceneTreeTimer` / `Timer` 节点 |
| --- | --- | --- |
| 是否可串进动画序列 | ✅ 天然是时间线一环 | ❌ 需要另外拼接 |
| 是否可暂停/调速 | ✅ 随 Tween 一起 `pause()` / `speed_scale` | 需单独处理 |
| 一次性延迟 | ✅ 简洁 | `get_tree().create_timer(t).timeout` 也简洁 |
| 重复周期触发 | 一般 | ✅ `Timer` 更合适 |
| 随节点释放自动取消 | ✅ 绑定节点的 Tween 自动失效 | ❌ 需手动处理 |

**结论**：一次性、且可能和动画编排在一起的延迟 → 用 Tween 的 interval+callback；纯周期循环计时（比如每秒回血）→ 用 `Timer` 或 `SceneTreeTimer`。

### 26.7.2 陷阱例

```gdscript
# ❌ 错误：callback 里捕获了会被释放的节点，却没做校验
tween.tween_callback(dead_node.queue_free)   # dead_node 已经被 free
# 后果：调用已释放对象 → 报错。
# 修正：出栈前用 is_instance_valid 判断，或用 Callable.bind 前先检查。

# ❌ 错误：把 tween_callback 当成“立刻执行”
tween.tween_callback(play_sound)
tween.tween_property(n, "position", Vector2(10, 0), 1.0)
# 误解：以为 play_sound 立刻播。实际它是时间线上第一个动作，
#       会在“轮到它”时（即 tween 开始时）才调用，然后才开始位移。
# 修正：若想立刻执行，直接调用 play_sound() 即可，不要塞进 tween。
```

---

## 26.8 循环与延迟：set_loops / set_delay

### 26.8.1 set_loops(n) 与 set_loops()

```gdscript
func pulse(icon: CanvasItem) -> void:
	var tween := icon.create_tween()
	tween.tween_property(icon, "scale", Vector2(1.2, 1.2), 0.4) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_IN_OUT)
	tween.tween_property(icon, "scale", Vector2.ONE, 0.4) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_IN_OUT)
	tween.set_loops(3)      # 整套动作重复 3 次
	# tween.set_loops()     # 不传参 = 无限循环（小心！见 26.11 陷阱四）
	tween.loop_finished.connect(_on_loop)
	# → 每完成一整轮，触发一次 loop_finished

func _on_loop(loop_count: int) -> void:
	print("已完成第 %d 轮" % loop_count)   # loop_count 从 0 开始计
```

> 注意：`set_loops()` 要放在**最后一个 tweener 之后**调用，才能让整条时间线整体循环；放在中间只会影响后续的分段语义，容易让人误解。（习惯上统一放最后一行。）

### 26.8.2 loop_finished 信号

| 信号 | 触发时机 | 参数 |
| --- | --- | --- |
| `finished` | 整条 Tween 完全结束（若无限循环则永不触发） | 无 |
| `loop_finished` | 每完成一轮循环 | `loop_count: int` |
| `step_finished` | 每完成一个 tweener | `idx: int` |

```gdscript
# 实战例：无限呼吸灯（靠 loop_finished 记数，到 10 次自己停）
func breathing_light(light: CanvasItem) -> void:
	var tween := light.create_tween()
	tween.tween_property(light, "modulate:a", 0.4, 0.8).set_trans(Tween.TRANS_SINE)
	tween.tween_property(light, "modulate:a", 1.0, 0.8).set_trans(Tween.TRANS_SINE)
	tween.set_loops()
	var count := 0
	tween.loop_finished.connect(func(_n: int) -> void:
		count += 1
		if count >= 10:
			tween.kill()           # ← 无限循环必须能自己收手
	)
```

### 26.8.3 set_delay：让某个 tweener 晚点动手

`set_delay(秒)` 是 **Tweener 级别**的方法（写在某个 `tween_property` 后面），含义是"这一段动画在排队轮到自己后，再等 N 秒才开始"。

```gdscript
func staggered_fade(items: Array[CanvasItem]) -> void:
	var tween := create_tween()
	tween.set_parallel(true)
	var i := 0
	for item in items:
		tween.tween_property(item, "modulate:a", 1.0, 0.4).set_delay(i * 0.08)
		i += 1
	# → 一串列表项依次淡入（“瀑布式”入场）
```

### 26.8.4 陷阱例

```gdscript
# ❌ 错误：无限循环的 tween 忘了 kill
func hover_glow(n: CanvasItem) -> void:
	var tween := n.create_tween()
	tween.tween_property(n, "modulate:a", 0.6, 0.6)
	tween.tween_property(n, "modulate:a", 1.0, 0.6)
	tween.set_loops()       # 无限循环……
# 后果：如果这个函数每次 hover 都被调用，会不断创建新的无限 tween，越积越多；
#       一旦节点被 free，大量悬空 tween 会让调试器刷报错。
# 修正：成员变量保存引用，重开前先 kill()；或者不用无限循环，用状态控制。
```

---

## 26.9 暂停与控制：pause / play / stop / kill

Tween 提供了一组"播放控制"方法，理解它们对做"可打断"的 UI 动效至关重要。

| 方法 | 作用 | 是否保留进度 | 能否再 play() |
| --- | --- | --- | --- |
| `pause()` | 暂停（保持当前进度） | ✅ 保留 | ✅ 可以 `play()` 继续 |
| `play()` | 从暂停处继续 | ✅ 从断点继续 | — |
| `stop()` | 停止并**重置进度回开头** | ❌ 回到 0 | ✅ 可以 `play()` 从头再来 |
| `kill()` | 彻底销毁这条 Tween（不可恢复） | ❌ 丢弃 | ❌ 不能再 play() |

```gdscript
# 实战例：可暂停的入场动画
var _tween: Tween

func play_intro(panel: Control) -> void:
	_tween = panel.create_tween()
	_tween.tween_property(panel, "position", Vector2.ZERO, 1.0)

func toggle_pause() -> void:
	if _tween and _tween.is_valid():        # 先确认有效
		if _tween.is_running():
			_tween.pause()
		else:
			_tween.play()
```

### 26.9.1 is_running / is_valid

```gdscript
func check(tween: Tween) -> void:
	print(tween.is_valid())      # → 这条 Tween 是否还活着（未 kill / 绑定节点未释放）
	print(tween.is_running())    # → 是否正在推进（暂停时为 false，结束后也为 false）
```

| 方法 | `true` 的含义 | 注意 |
| --- | --- | --- |
| `is_valid()` | Tween 未被 kill，且绑定节点仍存在 | **调用前先判断它，是最佳防御** |
| `is_running()` | 当前正在推进动画 | 暂停后为 `false`；跑完也为 `false` |

### 26.9.2 speed_scale 与 set_time_scale 的区别

| 名称 | 作用范围 | 用法 |
| --- | --- | --- |
| `Tween.set_speed_scale(v)` | **只影响这一条 Tween** | `tween.set_speed_scale(2.0)` = 2 倍速 |
| `Tween.set_process_mode(mode)` | 只影响这一条 Tween 用哪个循环推进 | `Tween.TWEEN_PROCESS_IDLE` / `TWEEN_PROCESS_PHYSICS` |
| `Engine.time_scale` | **全局**，影响整个游戏 | `Engine.time_scale = 0.5` = 全局慢动作 |

> ⚠️ 澄清一个常见混淆：**Tween 上并没有 `set_time_scale()` 这个方法**。你可能见到的是全局的 `Engine.time_scale`（影响包括物理、动画、计时在内的一切）。要做"只让某条 Tween 变速"，用 `set_speed_scale()`；要做"全局慢动作/子弹时间"，用 `Engine.time_scale`。

```gdscript
# 实战例：子弹时间——只让 UI 动效保持正常速度
func bullet_time() -> void:
	Engine.time_scale = 0.2                      # 全局慢下来
	var ui_tween := ui_panel.create_tween()
	ui_tween.set_speed_scale(5.0)                # UI 这条补偿回正常速度
	ui_tween.tween_property(ui_panel, "modulate:a", 1.0, 1.0)
```

### 26.9.3 陷阱例

```gdscript
# ❌ 错误：每次点击都新建 tween，旧的不停掉 → 属性互相打架
func on_press() -> void:
	var tween := scale.create_tween()
	tween.tween_property(self, "scale", Vector2(0.9, 0.9), 0.1)
# 后果：快速连点会创建多条 tween 同时改 scale，动画抽搐。
# 修正：用成员变量保存，重开前 kill() 旧的。
```

---

## 26.10 Tween 与信号：用 await 把动画写成剧本

Tween 是一个"会发信号的对象"，配合第 27 章的 `await`，你能把一串动画写成**从上读到下的剧本**，而不是靠回调套回调。

### 26.10.1 三个信号各自的含义

```gdscript
tween.finished.connect(...)        # 整条结束（无限循环时永不触发）
tween.loop_finished.connect(...)   # 每轮结束（参数：loop_count）
tween.step_finished.connect(...)   # 每个 tweener 结束（参数：idx，从 0 开始）
```

### 26.10.2 await tween.finished：等动画播完再继续

```gdscript
# 入门例：等一条 tween 播完
func move_and_wait(n: Node2D) -> void:
	var tween := n.create_tween()
	tween.tween_property(n, "position", Vector2(200, 0), 1.0)
	await tween.finished          # ← 挂起，动画播完后从这里继续
	print("移动完成！")            # → 1 秒后打印
```

### 26.10.3 可读性对比：回调 vs await

```gdscript
# 回调风格（嵌套，越写越深，难读）
func intro_callback_style(panel: Control, title: Label) -> void:
	var t1 := panel.create_tween()
	t1.tween_property(panel, "modulate:a", 1.0, 0.5)
	t1.finished.connect(func() -> void:
		var t2 := title.create_tween()
		t2.tween_property(title, "position:y", 100.0, 0.5)
		t2.finished.connect(func() -> void:
			var t3 := create_tween()
			t3.tween_method(func(v: float) -> void: pass, 0.0, 1.0, 0.4)
		)
	)
```

```gdscript
# await 风格（从上到下，一目了然）
func intro_await_style(panel: Control, title: Label) -> void:
	var t1 := panel.create_tween()
	t1.tween_property(panel, "modulate:a", 1.0, 0.5)
	await t1.finished                       # 等背景淡入

	var t2 := title.create_tween()
	t2.tween_property(title, "position:y", 100.0, 0.5)
	await t2.finished                       # 等标题滑下

	var t3 := create_tween()
	t3.tween_property(title, "modulate:a", 1.0, 0.4)
	await t3.finished                       # 等标题淡入

	print("开场结束")                        # 顺序清晰，逻辑像剧本
```

**结论**：能用 await 就别用回调嵌套。回调风格在动画一多时阅读成本呈指数上升，而 await 风格永远是一根直线。

### 26.10.4 await 与无限循环的坑

```gdscript
# ❌ 陷阱：对无限循环的 tween await finished → 永远等不到
var t := node.create_tween()
t.tween_property(node, "modulate:a", 0.5, 1.0)
t.set_loops()            # 无限循环
await t.finished         # ❌ finished 永不触发，协程永久挂起！
# 修正：不要 await 无限循环的 finished；若只想等一轮，用 await t.loop_finished。
```

```gdscript
# ✅ 正确：等“第一轮”结束
var t := node.create_tween()
t.tween_property(node, "modulate:a", 0.5, 1.0).set_trans(Tween.TRANS_SINE)
t.tween_property(node, "modulate:a", 1.0, 1.0).set_trans(Tween.TRANS_SINE)
t.set_loops()
await t.loop_finished     # 等第一轮跑完再继续
t.kill()                  # 别忘了收手
```

---

## 26.11 链式调用陷阱大全（重点排雷区）

这一节把 Tween 最坑人的几个问题逐个拆解。**每个陷阱都按"错误写法 → 后果 → 修正"三步走**。

### 陷阱一：set_trans / set_ease 只影响"它之后创建"的 tweener

```gdscript
# ❌ 错误写法
var tween := n.create_tween()
tween.tween_property(n, "position:x", 100.0, 0.5)     # ① 已创建，用默认曲线
tween.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)
tween.tween_property(n, "position:x", 200.0, 0.5)     # ② 才带 BACK/OUT
```

**后果**：你以为两条都带 BACK 过冲，实际只有第二条有。视觉上前半段"平"，后半段"弹"，很割裂。

**修正**：设置要写在**每个** tweener 之前，或者用"先设置、后创建"的顺序：

```gdscript
# ✅ 正确写法：对每一条单独设置
tween.tween_property(n, "position:x", 100.0, 0.5) \
	.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)
tween.tween_property(n, "position:x", 200.0, 0.5) \
	.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)
```

### 陷阱二：同一节点上同时存在多条 Tween 改同一属性 → 打架

```gdscript
# ❌ 错误写法：按钮按下与悬停各开一条 tween，都改 scale
func on_hover() -> void:
	create_tween().tween_property(button, "scale", Vector2(1.1, 1.1), 0.2)

func on_press() -> void:
	create_tween().tween_property(button, "scale", Vector2(0.9, 0.9), 0.1)
```

**后果**：快速 hover + press，两条 tween 同时写 `scale`，每帧互相覆盖，按钮疯狂抖动。

**修正**：用**成员变量保存单一 tween**，开新动画前先 `kill()` 旧的：

```gdscript
# ✅ 正确写法
var _hover_tween: Tween

func _retarget(target: Vector2, dur: float) -> void:
	if _hover_tween and _hover_tween.is_valid():
		_hover_tween.kill()                     # 掐掉旧的，保证只有一条在改 scale
	_hover_tween = button.create_tween()
	_hover_tween.tween_property(button, "scale", target, dur) \
		.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)

func on_hover() -> void: _retarget(Vector2(1.1, 1.1), 0.2)
func on_press() -> void: _retarget(Vector2(0.9, 0.9), 0.1)
```

### 陷阱三：tween 的"目标节点"被 free 后，tween 报错

```gdscript
# ❌ 错误写法：tween 绑定在 A 上，却去动 B，B 被释放后不处理
var tween := self.create_tween()               # 绑定 self
tween.tween_property(other_node, "position", Vector2.ZERO, 1.0)
# 若 other_node 中途 queue_free()：
# → Tween 仍绑定在 self 上，会继续尝试访问已释放的 other_node → 报错
```

**后果**：控制台刷 "Attempt to call function ... on a previously freed instance" 之类的错误。

**修正**：用 `is_instance_valid()` 防御，或在 tweener 前先检查：

```gdscript
# ✅ 正确写法一：动手前校验
if is_instance_valid(other_node):
	tween.tween_property(other_node, "position", Vector2.ZERO, 1.0)

# ✅ 正确写法二：让 tween 直接绑定到“被动的那个节点”，让它随目标一起失效
var tween := other_node.create_tween()          # 绑定 other_node 自己
tween.tween_property(other_node, "position", Vector2.ZERO, 1.0)
# → other_node 被 free，tween 自动失效，不用担心访问已释放对象
```

> 这就是 26.2.3 说的"生死关系"的价值：**绑定谁、就动谁**，是最省心的防御。

### 陷阱四：无限循环 tween 忘记 kill → 节点释放后刷报错

```gdscript
# ❌ 错误写法：每次 hover 创建一条无限循环 tween，从不管理
func on_hover() -> void:
	var t := create_tween()
	t.tween_property(icon, "modulate:a", 0.6, 0.5)
	t.tween_property(icon, "modulate:a", 1.0, 0.5)
	t.set_loops()                                # 无限
```

**后果**：反复 hover 会累积大量无限 tween（内存与性能都被吃掉）；节点被 free 后，调试器可能持续刷 "Tween target ... freed" 类警告。

**修正**：把无限循环的 tween 存成成员变量；退出/重开前 `kill()`；或改成一进一出由状态驱动。参考 26.8.2 的"呼吸灯自己收手"写法。

### 陷阱五：属性路径打错 → 不报错，但动画完全不生效

```gdscript
# ❌ 错误写法：路径拼错 / 用了不存在的子属性
var tween := n.create_tween()
tween.tween_property(n, "postion", Vector2(100, 0), 0.5)      # 把 position 拼成 postion
tween.tween_property(n, "scale:xy", Vector2(2, 2), 0.5)       # Vector2 没有 xy 子属性
tween.tween_property(n, "position:z", 100.0, 0.5)             # Vector2 没有 z
```

**后果**：**这三行全都不会报错**。Tween 在运行时解析路径失败会**静默跳过**对应动画，于是你盯着屏幕看半天："代码明明跑了，为什么不动？"——这是最难排查的一类问题。

**修正**：

```gdscript
# ✅ 正确写法
tween.tween_property(n, "position", Vector2(100, 0), 0.5)     # 拼写正确
tween.tween_property(n, "scale", Vector2(2, 2), 0.5)          # 整条 scale
tween.tween_property(n, "scale:x", 2.0, 0.5)                  # 或只改单轴
```

**排查口诀**：属性路径"静默失败"时，先把路径换成整条属性（如 `"position"`）验证 tween 确实在跑，再逐步细化到子属性，就能定位是路径写错。

### 陷阱六：忘了"起点的当前值"是什么

```gdscript
# ❌ 错误写法：以为 tween 会从 0 开始，实际是从“当前值”开始
func show_panel(panel: Control) -> void:
	var tween := panel.create_tween()
	tween.tween_property(panel, "modulate:a", 1.0, 0.3)
	# 若 panel.modulate.a 此刻就是 1.0，动画“看起来什么都没发生”
```

**后果**：面板已经是可见状态时，淡入动画等于没播。

**修正**：显式设定初始状态（或使用 `.from(0.0)`）：

```gdscript
panel.modulate.a = 0.0
var tween := panel.create_tween()
tween.tween_property(panel, "modulate:a", 1.0, 0.3)
# 或者：tween.tween_property(panel, "modulate:a", 1.0, 0.3).from(0.0)
```

### 陷阱速查表

| # | 陷阱 | 症状 | 一句话修正 |
| --- | --- | --- | --- |
| 1 | set_trans/ease 作用范围 | 部分动画曲线不对 | 每条 tweener 单独设置 |
| 2 | 多 tween 抢同一属性 | 动画抖动/抽搐 | 存成员变量，重开前 kill() |
| 3 | 目标节点被 free | 控制台刷"freed instance" | is_instance_valid 或绑定到目标本身 |
| 4 | 无限循环忘 kill | 累积 tween、刷警告 | 存引用、及时 kill() |
| 5 | 属性路径写错 | 不报错但不动 | 先验证整条属性，再细化子属性 |
| 6 | 起点=当前值 | 动画"没效果" | 先设初值或用 .from() |

---

## 26.12 Tween vs AnimationPlayer vs AnimationTree：怎么选

| 维度 | Tween | AnimationPlayer | AnimationTree |
| --- | --- | --- | --- |
| 创建方式 | 代码里 `create_tween()` | 编辑器里画关键帧 | 编辑器里配状态机/混合 |
| 适合对象 | 属性、方法、简单序列 | 骨骼、逐帧、音画同步 | 角色动画混合 |
| 动画混合（blend） | ❌ 不支持 | 有限（交叉淡化） | ✅ 核心能力 |
| 导入外部动画 | ❌ | ✅ glTF/FBX | ✅ |
| 打断/重定向 | ✅ 极易（kill 重建） | 一般 | ✅ 状态切换 |
| 程序化生成 | ✅ 极强 | 弱 | 弱 |
| 上手成本 | 低 | 中 | 高 |
| 调试可视化 | 弱（只能看代码） | ✅ 时间轴可视化 | ✅ 状态图可视化 |
| 运行时代码量 | 极少 | 中 | 少（配置多） |

**决策流程图：**

```
这个动画是不是美术/外部资源做的关键帧动画？
   ├─ 是 → 需要混合不同动画吗？
   │         ├─ 是 → AnimationTree
   │         └─ 否 → AnimationPlayer
   └─ 否 → 能在代码里一句话描述它怎么动吗？
             ├─ 能 → Tween ✅
             └─ 不能 → AnimationPlayer（去编辑器画关键帧）
```

再给几个典型判断：

| 需求 | 选择 |
| --- | --- |
| 按钮 hover 放大 | Tween |
| 角色走路/跑步切换 | AnimationTree |
| 攻击动作（美术做的帧动画） | AnimationPlayer |
| 伤害数字飘字 | Tween |
| 角色上下半身分别动画 | AnimationTree |
| 进度条数值滚动 | Tween（tween_method） |
| 摄像机震动 | Tween |
| 导入的 glTF 角色动画 | AnimationPlayer |

---

## 26.13 综合模板库（可直接抄走）

下面 7 个模板全部自包含、注释齐全，建议新建一个工具脚本文件收藏使用。所有模板内部都用 `create_tween()`，绑定在目标节点上，天然安全。

### 模板 A：UI 弹窗弹出动画（overshoot 回弹 + 背景淡入）

```gdscript
class_name PopupAnim
extends RefCounted
## 弹窗动效工具：缩放带 overshoot + 背景遮罩淡入

## 播放弹出动画；mask 为背景遮罩（可为 null），panel 为弹出面板
static func pop_out(panel: Control, mask: Control = null) -> void:
	# 1) 面板：从 0.6 倍缩放弹到 1.0 倍，用 BACK 制造过冲手感
	panel.pivot_offset = panel.size * 0.5          # 以中心为缩放轴心
	panel.scale = Vector2(0.6, 0.6)
	panel.modulate.a = 0.0
	var tween := panel.create_tween()
	tween.set_parallel(true)
	tween.tween_property(panel, "scale", Vector2.ONE, 0.4) \
		.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)
	tween.tween_property(panel, "modulate:a", 1.0, 0.18) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_OUT)
	# 2) 背景遮罩：单独淡入
	if mask:
		mask.modulate.a = 0.0
		var mt := mask.create_tween()
		mt.tween_property(mask, "modulate:a", 1.0, 0.25) \
			.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_OUT)
	# → 面板"啵"地弹出（略微过冲再回位），遮罩同步淡入

## 关闭动画：缩小 + 淡出，结束后自动隐藏
static func pop_in(panel: Control, mask: Control = null) -> void:
	panel.pivot_offset = panel.size * 0.5
	var tween := panel.create_tween()
	tween.set_parallel(true)
	tween.tween_property(panel, "scale", Vector2(0.8, 0.8), 0.2) \
		.set_trans(Tween.TRANS_CUBIC).set_ease(Tween.EASE_IN)
	tween.tween_property(panel, "modulate:a", 0.0, 0.2) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_IN)
	tween.chain().tween_callback(panel.hide)
	if mask:
		var mt := mask.create_tween()
		mt.tween_property(mask, "modulate:a", 0.0, 0.2).set_trans(Tween.TRANS_SINE)
		mt.tween_callback(mask.hide)
```

### 模板 B：按钮 hover / press 反馈

```gdscript
class_name ButtonFX
extends RefCounted
## 按钮动效：hover 放大、press 缩小、离开复原，内部保证只有一条 tween 在改 scale

static var _tweens: Dictionary = {}                # 每个按钮保存自己当前的 tween

## target 传入按钮节点；state 取 "hover" / "press" / "normal"
static func feedback(target: Control, state: String) -> void:
	var key := target.get_instance_id()
	if _tweens.has(key) and is_instance_valid(_tweens[key]) \
			and (_tweens[key] as Tween).is_valid():
		(_tweens[key] as Tween).kill()             # 掐掉旧动画，避免抢属性
	var final_scale := Vector2.ONE
	var dur := 0.12
	match state:
		"hover":  final_scale = Vector2(1.08, 1.08); dur = 0.12
		"press":  final_scale = Vector2(0.94, 0.94); dur = 0.06
		"normal": final_scale = Vector2.ONE;         dur = 0.12
	var tween := target.create_tween()
	tween.tween_property(target, "scale", final_scale, dur) \
		.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)
	_tweens[key] = tween
	# → hover 微微放大、按下微缩、松手复原，手感干脆
```

### 模板 C：受伤闪烁（modulate 红色闪 3 次）

```gdscript
class_name DamageFlash
extends RefCounted
## 受伤闪烁：把角色 modulate 短促染红再复原，重复 3 次

static func flash(sprite: CanvasItem, times: int = 3) -> void:
	var tween := sprite.create_tween()
	for i in times:
		# 染红：overlay 用 modulate 叠加红色（这里直接把整体染红）
		tween.tween_property(sprite, "modulate", Color(1.0, 0.3, 0.3), 0.05)
		# 复原
		tween.tween_property(sprite, "modulate", Color.WHITE, 0.08)
	# → 0.05s 变红、0.08s 复原，重复 3 次（总时长约 0.39s）
	# 如果 sprite 已经被 free，tween 自动失效，不会崩
```

### 模板 D：伤害数字飘字（上飘 + 渐隐，对象池版）

```gdscript
class_name FloatingText
extends RefCounted
## 伤害数字飘字：对象池复用 Label，上飘 + 渐隐 + 回收

static var _pool_name: Array[Label] = []
static var _pool_crit: Array[Label] = []

## 在宿主节点上生成一个飘字；text 显示内容，pos 世界/局部坐标，is_crit 是否暴击
static func spawn(host: Node, text: String, pos: Vector2, is_crit: bool = false) -> void:
	var pool := _pool_crit if is_crit else _pool_name
	var label: Label = pool.pop_back() if pool.size() > 0 else null
	if label == null:                                   # 池空则新建
		label = Label.new()
		label.horizontal_alignment = HORIZONTAL_ALIGNMENT_CENTER
		host.add_child(label)
	label.text = text
	label.position = pos
	label.modulate = Color(1.0, 0.85, 0.2) if is_crit else Color.WHITE
	label.modulate.a = 1.0
	label.visible = true

	var tween := label.create_tween()
	tween.set_parallel(true)
	tween.tween_property(label, "position", Vector2(0, -70), 0.8) \
		.as_relative().set_trans(Tween.TRANS_QUAD).set_ease(Tween.EASE_OUT)
	tween.tween_property(label, "modulate:a", 0.0, 0.8) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_IN)
	tween.chain().tween_callback(func() -> void:
		label.visible = false
		pool.append(label)                              # 回收进池，而不是 free
	)
	# → 数字往上飘 70 像素并渐隐，结束后回收复用（无频繁 new/free）
```

### 模板 E：摄像机 punch / 震动（偏移衰减）

```gdscript
class_name CameraFX
extends RefCounted
## 摄像机震动：用 offset 的快速衰减模拟 punch / 震动

## 一次性 punch：给定方向与强度
static func punch(cam: Camera2D, direction: Vector2, strength: float = 12.0) -> void:
	var tween := cam.create_tween()
	tween.tween_property(cam, "offset", direction.normalized() * strength, 0.06) \
		.set_trans(Tween.TRANS_EXPO).set_ease(Tween.EASE_OUT)
	tween.tween_property(cam, "offset", Vector2.ZERO, 0.25) \
		.set_trans(Tween.TRANS_EXPO).set_ease(Tween.EASE_OUT)
	# → 瞬间被"顶"出去，再迅速弹回原位，幅度快速衰减

## 持续震动：随机方向连续抖动，重复 N 次后归零
static func shake(cam: Camera2D, strength: float = 8.0, times: int = 6) -> void:
	var tween := cam.create_tween()
	for i in times:
		var dir := Vector2(randf_range(-1, 1), randf_range(-1, 1)).normalized()
		# 幅度随次数递减，越震越轻
		var s := strength * (1.0 - float(i) / float(times))
		tween.tween_property(cam, "offset", dir * s, 0.04)
	tween.tween_property(cam, "offset", Vector2.ZERO, 0.08)
	# → 短促的高频抖动，自然衰减到静止
```

### 模板 F：道具拾取动画（旋转 + 上升 + 消失）

```gdscript
class_name PickupFX
extends RefCounted
## 道具拾取：边旋转边上升边缩小最终消失，结束后调用回调（如结算）

## item 为要播放动画的节点；on_done 为可选回调
static func play(item: Node2D, on_done: Callable = Callable()) -> void:
	var tween := item.create_tween()
	tween.set_parallel(true)
	# 旋转两圈（相对旋转，避免受当前角度影响）
	tween.tween_property(item, "rotation", TAU * 2.0, 0.5) \
		.as_relative().set_trans(Tween.TRANS_LINEAR)
	# 上升 80 像素
	tween.tween_property(item, "position", Vector2(0, -80), 0.5) \
		.as_relative().set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)
	# 缩小 + 淡出
	tween.tween_property(item, "scale", Vector2.ZERO, 0.5) \
		.set_trans(Tween.TRANS_CUBIC).set_ease(Tween.EASE_IN)
	if item is CanvasItem:
		tween.tween_property(item, "modulate:a", 0.0, 0.5).set_trans(Tween.TRANS_SINE)
	tween.chain().tween_callback(func() -> void:
		if on_done.is_valid():
			on_done.call()
		item.queue_free()
	)
	# → 道具旋转着飞起、缩小淡出，结束后销毁并触发回调
```

### 模板 G：开场标题动画序列（await 串联的完整片头）

```gdscript
class_name TitleIntro
extends Node
## 开场片头：用 await 串联多段动画，逻辑像剧本一样从上到下
## 用法：把它挂在开场场景的根节点上，编辑器中连好各节点引用

@export var background: ColorRect                 # 全屏背景
@export var title: Label                          # 主标题
@export var subtitle: Label                       # 副标题
@export var press_key: Label                      # “按任意键开始”
@export var start_button: Button                  # 开始按钮

func play_intro() -> void:
	# ① 背景从黑淡入
	background.modulate.a = 0.0
	var t1 := background.create_tween()
	t1.tween_property(background, "modulate:a", 1.0, 0.6) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_OUT)
	await t1.finished                                  # 等背景淡入完成

	# ② 主标题：从上滑下 + 淡入（并行）
	title.modulate.a = 0.0
	title.position.y -= 40.0                            # 初始在偏上位置
	var t2 := title.create_tween()
	t2.set_parallel(true)
	t2.tween_property(title, "position:y", 40.0, 0.5) \
		.as_relative().set_trans(Tween.TRANS_CUBIC).set_ease(Tween.EASE_OUT)
	t2.tween_property(title, "modulate:a", 1.0, 0.5) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_OUT)
	await t2.finished

	# ③ 副标题：淡入（略慢，制造层次）
	subtitle.modulate.a = 0.0
	var t3 := subtitle.create_tween()
	t3.tween_property(subtitle, "modulate:a", 1.0, 0.5) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_OUT)
	await t3.finished

	# ④ 开始按钮：带过冲地弹出
	start_button.pivot_offset = start_button.size * 0.5
	start_button.scale = Vector2(0.5, 0.5)
	start_button.modulate.a = 0.0
	var t4 := start_button.create_tween()
	t4.set_parallel(true)
	t4.tween_property(start_button, "scale", Vector2.ONE, 0.4) \
		.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)
	t4.tween_property(start_button, "modulate:a", 1.0, 0.3) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_OUT)
	await t4.finished

	# ⑤ “按任意键开始”：无限呼吸灯，直到玩家按键
	press_key.modulate.a = 0.3
	var t5 := press_key.create_tween()
	t5.tween_property(press_key, "modulate:a", 1.0, 0.8).set_trans(Tween.TRANS_SINE)
	t5.tween_property(press_key, "modulate:a", 0.3, 0.8).set_trans(Tween.TRANS_SINE)
	t5.set_loops()                                      # 无限循环
	await get_tree().create_timer(1.0).timeout          # 演示用；正式游戏可换成按键信号
	t5.kill()                                           # 别忘了收手
	print("片头播放完成，等待玩家操作")
	# → 背景→标题→副标题→按钮→呼吸提示，一气呵成、从上读到下
```

> **模板 G 的要点**：每一段动画都 `await 它的 finished`，让"等待"这件事在代码里可见；并行部分用 `set_parallel(true)` 压缩成同一段；无限循环的呼吸灯必须能被 `kill()`。这套结构可以直接扩展成完整的开场 → 主菜单 → 进入游戏的流程。

---

## 本章小结

1. **Tween = 插值动画器**：给它起点、终点、时长、节奏，它逐帧算出中间值，把"瞬移"变成"平滑过渡"。
2. **Godot 4 的 Tween 与 Godot 3 完全不同**：旧版的 Tween 节点、`interpolate_property()`、`start()` 全部作废，只认新 API。
3. **唯一正确的创建方式**是 `create_tween()`（Node 或 SceneTree 上调用）；`Tween.new()` 在 4.x 被禁止。
4. **Tween 由 SceneTree 托管、绑定到节点**：绑定节点被释放，Tween 自动失效，这是安全设计而非隐患；`SceneTreeTween` 只是 4.0 预览期的旧名字。
5. **属性路径三粒度**：整条（`"position"`）、单分量（`"position:x"` / `"modulate:a"` / `"scale:x"`）；`"scale:xy"` 并不存在，写了会静默不生效。
6. **绝对值 vs 相对值**：默认是绝对目标值；`.as_relative()` 表示"在当前值基础上加多少"；`.from_current()` 把起点显式钉在当前值。
7. **串行是默认，并行靠 `parallel()` / `set_parallel(true)`**；`chain()` 可在全并行后切回串行；`tween_interval()` 插入纯等待；并行延迟用 `set_parallel(true) + set_delay()` 实现（并没有 `parallel_delayed()` 这个 API）。
8. **缓动 = TRANS × EASE**：10 种 `TRANS_XXX` 决定曲线形状，4 种 `EASE_XXX` 决定方向；UI 常用 CUBIC/QUINT + EASE_OUT，弹跳用 BACK/ELASTIC/BOUNCE。
9. **`set_trans()` / `set_ease()` 只影响其后创建的 tweener**，设置要写在每个目标 tweener 之前。
10. **`tween_method`** 把插值结果每帧喂给一个可调用对象，适合进度条、Shader 参数、自定义几何动画；注意回调签名只接收一个插值参数。
11. **`tween_callback` + `tween_interval`** 是轻量版的延时/序列执行，适合一次性延迟；周期计时仍推荐 `Timer`。
12. **循环与信号**：`set_loops(n)` / `set_loops()`；`finished`（无限循环不触发）、`loop_finished`、`step_finished` 各有用途。
13. **播放控制**：`pause()` 保留进度、`play()` 续播、`stop()` 归零、`kill()` 销毁；`is_valid()` / `is_running()` 是最佳防御。
14. **变速分清两层**：`Tween.set_speed_scale()` 只管这一条；`Engine.time_scale` 才是全局；Tween 上不存在 `set_time_scale()`。
15. **用 `await tween.finished` 把动画写成剧本**：可读性远胜回调嵌套；但别 await 无限循环 tween 的 `finished`，要用 `loop_finished`。
16. **六大陷阱牢记**：set_trans 作用范围、多 tween 抢属性、目标节点被 free、无限循环忘 kill、属性路径静默失败、起点等于当前值导致"没动"。
17. **选型原则**：能在代码里一句话描述的运动用 Tween；美术关键帧用 AnimationPlayer；需要混合/导入的用 AnimationTree。
18. **7 大模板可直接复用**：弹窗弹出、按钮反馈、受伤闪烁、伤害飘字（对象池）、摄像机震动、道具拾取、await 片头序列——它们覆盖了日常 UI 与效果动效的绝大多数需求。

> **下一章预告**：第 27 章我们会深入 `await`、协程与异步编程。你会发现，本章末尾用的 `await tween.finished` 只是一个开始——`await` 能把"等动画、等输入、等加载、等倒计时"这些散落各处的等待，统一成一段从上读到下的优雅代码。
---
# 第 27 章：await、协程与异步编程

> 如果要评选 GDScript 中"最能改变你写代码方式"的一个特性，那一定是 `await`。游戏天然充满"等待"：等动画播完、等玩家按键、等倒计时结束、等关卡加载好……如果没有 `await`，这些逻辑会被拆成一地鸡毛的状态机和回调；有了 `await`，你可以把它们写成一段连贯的、像剧本一样从头读到尾的代码。本章将从"为什么要等"讲到"协程到底发生了什么"，再送你一整套可以直接抄走使用的实用模板，最后用剧情对话系统压轴收尾。

## 27.1 同步 vs 异步：为什么需要"等"

### 27.1.1 从四个真实需求说起

先看一个对照表——下面四件事是几乎所有游戏都会遇到的需求，想一想"纯同步代码"该怎么实现它们：

| 游戏需求 | 我们真正想要的写法 | 硬写同步代码的下场 |
| --- | --- | --- |
| 等开场动画播完，再弹"胜利"界面 | "播动画 → 等它完 → 弹界面" | 在 `_process` 里每帧轮询动画状态，用成员变量记录"进行到哪一步" |
| 对话每行显示完等玩家按键继续 | 一行一行往下读 | 每行接一个回调，回调里再接回调 |
| 等待关卡加载完再进场景 | "加载 → 等好 → 进" | 同步加载，画面全程冻结 |
| 等玩家在 10 秒内做选择 | "等 10 秒或等选择" | 手写状态机 + 计时器 + 信号满天飞 |

你会发现：**"等待"本身不难，难的是在等待期间还要让游戏继续活着**——画面继续渲染、按钮继续响应、动画继续播放。这正是异步编程要解决的问题。

### 27.1.2 主线程：那个绝对不能停的人

Godot 的游戏主循环每一帧干的事情大致如下（ASCII 示意）：

```
        ┌──────────── 一帧（60fps 时约 16.7 毫秒） ────────────┐
        │  ① 收集输入（键盘 / 鼠标 / 触摸）                      │
        │  ② 跑 _process / _physics_process                    │
        │  ③ 处理信号、恢复 await 挂起的协程                      │
        │  ④ 渲染画面，把这一帧画到屏幕上                          │
        └────────────────── 转到下一帧，循环 ──────────────────┘
```

关键结论只有一句：**这套流程是在主线程上一口气跑完的**。如果你在 `②` 里写了一个耗时 3 秒的循环，那么 `④` 就会推迟 3 秒才发生——玩家看到的就是画面定格 3 秒（也就是俗称的"卡死"）。等待时间越长，冻结越久。

### 27.1.3 陷阱例：手写"等待"冻住整个游戏

这是初学者最常写出的"等待"，请把它当成反面教材记住：

```gdscript
# ❌ 错误写法：忙等待（busy-wait）
func naive_wait(seconds: float) -> void:
	var target := Time.get_ticks_msec() + int(seconds * 1000)
	while Time.get_ticks_msec() < target:
		pass  # → 空转占用主线程：画面完全冻结，鼠标点击无效，
              # → Windows 上甚至可能弹出"未响应"
```

**后果**：主循环被这个 `while` 卡住，引擎根本走不到"渲染"那一步。等待 3 秒 = 冻结 3 秒；如果写在 `_ready` 里，玩家连游戏画面都看不到。

**修正**：把"死等"换成"挂起"，把控制权还给引擎：

```gdscript
# ✅ 正确写法：挂起等待
func good_wait(seconds: float) -> void:
	await get_tree().create_timer(seconds).timeout
	# → 等待期间引擎照常渲染、照常处理输入，时间一到自动从这里继续
```

两条代码都是"等待 N 秒"，差别在于：前者把主线程锁死在原地空转，后者把主线程让出来，时间到了再回来。

### 27.1.4 同步 vs 异步：一张对照表

| 维度 | 同步调用 | 异步等待（await） |
| --- | --- | --- |
| 等待期间主线程是否被占用 | 占用（画面冻结） | 不占用（照常渲染） |
| 代码书写顺序 | 从上到下 | **也是从上到下**（这正是 await 的妙处） |
| 阅读心智负担 | 低 | 低（写法像同步，行为是异步） |
| 出错调试难度 | 低 | 稍高（执行顺序不直观，见 27.7） |

最后一条也提醒我们：await 的强大是有代价的。本章 27.7 会专门集中排雷。

## 27.2 await 基础语法

### 27.2.1 什么可以被 await

`await` 后面能跟的东西只有两大类，请记牢：

| 类别 | 例子 | 说明 |
| --- | --- | --- |
| 信号（Signal） | `await timer.timeout`、`await player.died` | 自定义信号、内置信号都行 |
| 含 await 的函数调用（协程调用） | `await fetch_reward()` | 见 27.3，本质是"挂起状态" |

顺带一提：`get_tree().process_frame`、`get_tree().physics_frame`、`get_tree().create_timer(1.0).timeout` 这些常用"可等待物"，其实**都是信号**，属于第一类。

不能被 await 的东西（写了会直接报错）：

```gdscript
await 3                        # ❌ 数字不能等
await "abc"                    # ❌ 字符串不能等
await print("hi")              # ❌ 普通函数（内部没有 await）不能等
await $Timer.wait_time          # ❌ 这是 float 属性，不是信号
```

### 27.2.2 入门例：await 一个信号

```gdscript
extends Node

signal enemy_spawned(enemy_name: String)

func _ready() -> void:
	print("① 准备等敌人生成")
	await enemy_spawned          # 等待自定义信号被 emit
	print("④ 敌人出现了，开始战斗逻辑")

func _on_spawner_tick() -> void:
	print("② 先做点别的事")
	enemy_spawned.emit("史莱姆")   # → ③ 发出信号，_ready 里挂起的代码被唤醒
```

运行输出顺序为 `①②③④`。注意一个重要事实：**await 一个信号并不需要事先 connect**——`await` 本身就完成了"挂起 + 监听"两件事。

### 27.2.3 入门例：await 一个返回协程的函数调用

```gdscript
func fetch_reward() -> int:
	await get_tree().create_timer(1.0).timeout   # 模拟"1 秒后才拿到结果"
	return 100

func _ready() -> void:
	print("② 去领奖励……")
	var gold := await fetch_reward()   # 等协程跑完，拿到返回值
	print(gold)                        # → 100
```

`fetch_reward()` 内部有 `await`，所以它是一个"可挂起的函数"（协程）。在它前面加 `await`，就表示"我要等它彻底跑完，并要它的返回值"。

### 27.2.4 await 的表达式值：信号参数

`await 信号` 是一个**有值的表达式**。这个值就是信号发出来的参数：

```gdscript
extends Node

signal loot_dropped(item_name: String, amount: int)

func _ready() -> void:
	var loot = await loot_dropped
	print(loot)        # → ["红宝石", 3]（多参数时返回数组）
	loot_dropped.emit("红宝石", 3)
```

等等，上面的示例故意写反了顺序——正确顺序应当是先 await 再 emit。同时这里还有一处需要特别注意的知识点：参数个数不同，await 拿到的值也不同：

| 信号参数个数 | `await` 的返回值 |
| --- | --- |
| 0 个 | `null` |
| 1 个 | 那个参数本身 |
| 2 个及以上 | 按顺序装进 `Array` |

单参数的例子（这是实战里最常用的形态）：

```gdscript
# Area2D 内置信号：body_entered(body: Node2D)
func wait_for_body(area: Area2D) -> void:
	var body := await area.body_entered    # 直接拿到那 1 个参数
	print("进来的东西是：", body.name)       # → 进来的东西是：Player
```

多参数的例子（拿到的必须是数组）：

```gdscript
signal gesture_made(kind: String, power: float)

func _ready() -> void:
	var result = await gesture_made
	print(result[0], result[1])   # → 挥手 3.0
	gesture_made.emit("挥手", 3.0)
```

### 27.2.5 陷阱例：await 错了东西

```gdscript
# ❌ 错误：await 了一个"已经求值完"的普通结果
var t := get_tree().create_timer(1.0)
await t                          # → 报错：t 是 SceneTreeTimer 对象，不是信号
```

**后果**：编辑器直接报错 `await only works with signals or coroutines`，脚本无法继续运行。

**修正**：等它的 `.timeout` 信号：

```gdscript
var t := get_tree().create_timer(1.0)
await t.timeout                  # ✅ 等 SceneTreeTimer 的 timeout 信号
```

## 27.3 协程本质剖析

### 27.3.1 一句话说清"协程"

**含 `await` 的函数就是协程**（可挂起的函数）。它和普通函数的唯一区别是：跑到 `await` 那一行时，它会**立刻把控制权交还**，自己原地"挂起"；等到条件满足（信号发出），再从挂起处继续往下跑。

### 27.3.2 动手实验：调用 await 函数，它立刻把控制权还给你

```gdscript
func do_slow() -> void:
	print("② do_slow 开始跑")
	await get_tree().create_timer(1.0).timeout   # 在这里挂起
	print("④ 一秒后恢复，继续跑 do_slow 的后半段")

func _ready() -> void:
	print("① 调用 do_slow")
	do_slow()                     # 注意：这里没有 await！
	print("③ _ready 没有被堵住，立刻执行到这里")
```

输出顺序：

```
① 调用 do_slow
② do_slow 开始跑
③ _ready 没有被堵住，立刻执行到这里
（等待 1 秒）
④ 一秒后恢复，继续跑 do_slow 的后半段
```

### 27.3.3 时序图：一次完整的挂起与恢复

```
 _ready()                do_slow()              引擎主循环 / 信号源
    │                       │                        │
    │  do_slow() ──────────>│                        │
    │                       │ print("②…")            │
    │                       │ 碰到 await               │
    │                       │ 【就地挂起】              │
    │<─── 立刻返回（挂起状态）─┤                        │
    │                       │ （局部变量、执行位置       │
    │ print("③…")           │   全部被引擎悄悄保存）      │
    │ ……继续干别的……          │                        │
    │                       │                        │ 1 秒后 SceneTreeTimer
    │                       │                        │ 发出 timeout 信号
    │                       │<────── 信号唤醒挂起 ──────┤
    │                       │ print("④…")             │
    │                       │ do_slow 正常结束          │
```

请务必记住这张图的三个关键瞬间：

1. **碰到 await：函数就地挂起，调用者立刻拿到控制权**；
2. **挂起期间：函数的局部变量和"执行到哪了"都被完整保存**，引擎替你保管；
3. **信号发出：引擎从挂起点恢复函数**，就像什么都没发生过一样继续跑。

### 27.3.4 挂起状态：类似 GDScriptFunctionState 的东西

在 Godot 3 时代，含 `yield` 的函数被调用时会返回一个 `GDScriptFunctionState` 对象，你可以拿着它稍后手动恢复。Godot 4 把这套机制改造成了 `await` 关键字，挂起状态被**隐式化**了——你一般看不到它，但它一直存在。看这个实验：

```gdscript
func slow() -> int:
	await get_tree().process_frame   # 挂一帧
	return 42

func _ready() -> void:
	var x = slow()       # 不加 await 调用协程
	print(x)             # → 打印出一个"挂起状态"对象，而不是 42
	var y = await slow() # 加 await 调用协程
	print(y)             # → 42
```

不加 `await` 时，你拿到的不是函数返回值，而是那个**挂起状态**（一张"取货凭证"）。这张"凭证"本身就是可等待的：`await` 它，就等于等这个函数跑完、并取回真正的返回值。这个设计非常关键，27.6 的并发模板和 27.7 的陷阱 4 全靠它。

### 27.3.5 什么时候别用

- **每帧都要跑的逻辑**：协程挂起/恢复的开销虽小，但比不上直接写在 `_process` 里。持续性的行为（移动、跟随）老老实实用 `_process`，协程适合"一次性、有先后顺序的流程"。
- **需要外部随时中断的复杂状态**：如果一段逻辑有大量"随时可能被打断"的外部输入（比如复杂战斗状态机），用状态机会比用一长串 await 更可控。
- **在静态函数里小心使用**：`get_tree()` 这类依赖节点实例的东西在静态上下文里不可用，静态协程只能 await 与实例无关的信号。

## 27.4 等待的三种常用方式对比

"我想等一会儿"有三种主流写法，各有最佳适用场景。

### 27.4.1 方式一：SceneTreeTimer（一次性计时器）

```gdscript
# 等待 1 秒
await get_tree().create_timer(1.0).timeout

# 完整参数（了解即可）：
# create_timer(时间, 不受暂停影响=false, 用物理帧计时=false, 忽略time_scale=false)
await get_tree().create_timer(1.0, false, false, true).timeout  # 不受 Engine.time_scale 影响
```

入门例：

```gdscript
func play_intro() -> void:
	print("第 1 句")
	await get_tree().create_timer(2.0).timeout
	print("第 2 句")   # → 2 秒后打印
```

### 27.4.2 方式二：等待信号

```gdscript
# 等玩家死亡信号
await player.died
# 等 Area2D 有东西进来
var body := await $Area2D.body_entered
# 等一帧 / 等一个物理帧
await get_tree().process_frame
await get_tree().physics_frame
```

### 27.4.3 方式三：Timer 节点

```gdscript
# 场景里放一个 Timer 节点：wait_time=5，one_shot 勾上
func start_cooldown() -> void:
	$CooldownTimer.start()
	await $CooldownTimer.timeout
	print("冷却结束，技能可用了")   # → 5 秒后打印
```

### 27.4.4 三种方式对比表

| 维度 | create_timer | await 信号 | Timer 节点 |
| --- | --- | --- | --- |
| 典型用途 | 一次性延时 | 事件驱动（"等某个事发生"） | 周期性 / 需要在检查器配置 |
| 精度 | 帧级（按 delta 累加，约 16ms 误差） | 精确（事件一发生立刻醒） | 帧级 |
| 可见性 | 纯代码，检查器里看不到 | — | 场景树里可见可调，策划也能改 |
| 重复触发 | 每次调用新建一个 | 信号每次 emit 醒一次 | `start()` 即重置，天然适合周期 |
| 暂停处理 | 默认受暂停影响 | 看信号源 | 有 `process_callback`、可受暂停控制 |
| 资源占用 | 每次新建小对象 | 无 | 常驻节点 |

**选择决策树**：

```
需要"等"？
 ├── 只等一次、几秒钟 ────────────────> create_timer
 ├── 在等"某件事发生"（按键/死亡/进入区域）──> await 信号
 ├── 周期性触发 / 想在检查器里配时间 ──────> Timer 节点
 └── 需要毫秒级精度（受击无敌帧等）────────> Time.get_ticks_msec() + _process 手动算
```

**什么时候别用**：不要在每帧逻辑里反复 `create_timer`（等于每帧造垃圾对象）；不要用 Timer 节点做"只等一次"的简单事，那是杀鸡用牛刀。

## 27.5 超时等待模式：等信号，但最多等 N 秒

### 27.5.1 为什么要"超时兜底"

`await player.died` 这种写法有一个隐藏风险：**如果那个信号永远不发生呢？** 玩家直接关掉了敌人节点、动画被设成循环导致结束信号永不发出、网络消息丢失……协程就会**永久挂起**，后续代码一行也不会跑，而且不会有任何报错——这是最难排查的一类 bug。

解法：让"目标信号"和"超时信号"**赛跑**，谁先到就听谁的。

### 27.5.2 模板：wait_for_signal_or_timeout

```gdscript
class_name AsyncUtil
extends Node
## 异步工具箱：超时等待 / 并发收集。把本节点挂进场景树即可使用。

signal _race_finished   # 内部"终点线"信号：任何一方先到，都算冲线

## 等待信号 sig，但最多等待 timeout 秒。
## 返回 true  = 信号先来了
## 返回 false = 超时了（信号至今没来）
func wait_for_signal_or_timeout(sig: Signal, timeout: float) -> bool:
	var arrived := false                        # 目标信号是否到了

	# 选手①：目标信号——一到就把 arrived 置真并冲线
	var on_signal: Callable = func() -> void:
		arrived = true
		_race_finished.emit()

	# 选手②：超时计时器——时间一到也冲线（但不改变 arrived）
	var on_timeout: Callable = func() -> void:
		_race_finished.emit()

	sig.connect(on_signal)
	get_tree().create_timer(timeout).timeout.connect(on_timeout)

	await _race_finished     # 原地等冲线：谁先冲都行

	# 善后：把目标信号的连接断掉，防止影响下一次比赛
	if sig.is_connected(on_signal):
		sig.disconnect(on_signal)
	return arrived
```

工作原理：两个信号都连接到内部信号 `_race_finished` 上。谁先发出，协程就被唤醒一次；后到的那个再发也没关系，因为已经没人等它了。最后根据 `arrived` 标志判断是"真等到"还是"超时"。

### 27.5.3 实战：等待玩家确认，10 秒无操作自动跳过

开场播报（briefing）界面的典型需求：提示"按任意键继续"，但玩家可能挂机，必须 10 秒后自动进入游戏。

```gdscript
extends Control

@onready var async_util: AsyncUtil = $AsyncUtil   # 场景里挂的 AsyncUtil 节点
@onready var start_btn: Button = $StartButton

func show_briefing() -> void:
	start_btn.visible = true
	var ok := await async_util.wait_for_signal_or_timeout(start_btn.pressed, 10.0)
	start_btn.visible = false
	if ok:
		print("玩家确认了，进入新手引导")
	else:
		print("10 秒没动静，自动跳过")   # → 玩家挂机时自动跳过
	# 无论哪条路，流程都会继续往下走，绝不会卡死在这里
	Globals.start_game()
```

### 27.5.4 陷阱例：不带超时的"裸等"

```gdscript
# ❌ 错误：裸等一个"可能永远不会发生"的信号
func bad() -> void:
	await network_client.room_ready   # 网络断了？服务器没开？
	load_main_scene()                 # → 永远不会执行，且没有任何报错
```

**修正**：所有"等外部世界"的 await，一律加超时兜底：

```gdscript
# ✅ 正确：最多等 5 秒
var ok := await async_util.wait_for_signal_or_timeout(network_client.room_ready, 5.0)
if not ok:
	show_error_panel("连接服务器超时，请重试")
	return
load_main_scene()
```

## 27.6 并发协程：同时启动，全部等完

### 27.6.1 为什么需要"并发"

看一个加载场景：三张地图，每张要 2 秒。

```
串行（一个等完再下一个）：
  加载森林 ██████░░░░░░░░░░░░░░  2s
  加载洞穴       ██████░░░░░░░░  4s
  加载城镇             ██████░░  6s   总耗时 6 秒

并发（同时开始，一起等完）：
  加载森林 ██████
  加载洞穴 ██████
  加载城镇 ██████            总耗时 ≈ 2 秒
```

协程天然支持并发：**调用协程函数但不立刻 await**，它就会"开始跑并挂在半路"；你先把三个都启动起来，再逐个"收货"。

### 27.6.2 模板：gather（并发收集）

```gdscript
# 续写在 AsyncUtil 里
## 同时启动多个协程，等它们全部完成，按原顺序返回结果数组。
## 用法：var 结果 := await gather([协程调用1, 协程调用2, ...])
func gather(calls: Array) -> Array:
	var states: Array = []
	# 第一步：逐个"点火"。注意这一步没有 await——
	# 每个调用都会立刻执行到它内部的第一个 await 处并挂起，然后返回挂起状态
	for c in calls:
		states.append(c)

	# 第二步：按顺序"收货"。await 挂起状态 = 等这个协程彻底跑完
	var results: Array = []
	for s in states:
		results.append(await s)
	return results
```

理解要点：`calls` 数组里装的是**函数调用表达式**——放入数组的瞬间它们就已经开始执行（各自跑到第一个 await 挂起）；随后我们按顺序 await 每个挂起状态，把它们的结果收集回来。**先全部启动、再逐个收割**，这就是并发。

### 27.6.3 实战：并行加载三张地图

```gdscript
class_name MapLoader
extends Node

## 异步加载一张地图场景（利用引擎的线程化资源加载）
func load_map(path: String) -> PackedScene:
	ResourceLoader.load_threaded_request(path)   # 向引擎下订单
	while true:
		var progress := []                        # [0.0~1.0] 的加载进度
		var status := ResourceLoader.load_threaded_get_status(path, progress)
		match status:
			ResourceLoader.THREAD_LOAD_LOADED:
				return ResourceLoader.load_threaded_get(path)   # 加载完成，取货
			ResourceLoader.THREAD_LOAD_FAILED:
				push_error("地图加载失败：" + path)
				return null
			_:
				await get_tree().process_frame    # 还没好？等一帧再查（把主线程让出来）

## 加载整章所需的全部地图（并发）
func load_chapter(async: AsyncUtil) -> void:
	var scenes: Array = await async.gather([
		load_map("res://maps/forest.tscn"),   # 点火①
		load_map("res://maps/cave.tscn"),      # 点火②
		load_map("res://maps/town.tscn"),      # 点火③
	])
	print("三张地图全部就绪：", scenes.size())   # → 三张地图全部就绪：3
```

### 27.6.4 陷阱例：以为并发，其实串行

```gdscript
# ❌ 错误：在循环里边 await 边调用
var scenes: Array = []
for path in paths:
	scenes.append(await load_map(path))   # 每次都等上一张加载完才开始下一张
# → 总耗时 = 三张地图耗时之和（伪"并发"）
```

**修正**：用 gather，先启动全部、再统一收割：

```gdscript
# ✅ 正确：gather 先点火、后收货
var scenes: Array = await async_util.gather(paths.map(load_map))
```

另一个反面例子：往 gather 里塞**普通函数**（内部没有 await）也是"伪并发"——它会当场执行完才轮到下一个，不过这种情况结果是对的，只是没有并发收益。

## 27.7 陷阱大全：await 的五个经典坑

await 写起来爽，坑起来也不含糊。下面五个坑按"踩坑频率"排序，请逐个吃透。

### 27.7.1 坑一：await 之后，节点可能已经被 free

```gdscript
# ❌ 错误：等 2 秒后直接访问节点
func delayed_buff(target: Node) -> void:
	await get_tree().create_timer(2.0).timeout
	target.add_to_group("buffed")   # → 若这 2 秒里玩家退出战斗、target 被 free，
	                                # → 这里直接崩溃：attempt to call function on a previously freed instance
```

**后果**：运行时崩溃报错（访问已释放实例）。这是 await 最常见的崩溃来源。

**修正模板**：恢复后第一件事先验货——

```gdscript
# ✅ 正确：挂起恢复后先检查对象是否还活着
func delayed_buff(target: Node) -> void:
	await get_tree().create_timer(2.0).timeout
	if not is_instance_valid(target):    # 对象还在吗？
		return                            # 不在就什么都不做，安静退场
	target.add_to_group("buffed")
```

**建议固化为肌肉记忆**：`await` 之后只要要访问"别的节点"，就先 `is_instance_valid`。另外补充两个相关事实：

- 如果被 free 的是**协程自己所在的节点**（`self`），协程会被引擎直接丢弃——不会崩溃，但后半段代码**永远不会执行**，同样很危险；
- 重要的延时任务不要挂在"随时可能被销毁的场景节点"上，挂到常驻的自动加载单例上更稳。

### 27.7.2 坑二：循环/重复点击里的 await 造成逻辑重叠

需求：点"开始"按钮 → 播放淡出动画 → 切场景。看起来没毛病：

```gdscript
# ❌ 错误：没有防抖的按钮处理
func _on_start_pressed() -> void:
	$AnimationPlayer.play("fade_out")
	await $AnimationPlayer.animation_finished
	get_tree().change_scene_to_file("res://scenes/main.tscn")
	# → 玩家手快连点两下：两个协程同时挂起、先后恢复 → 场景被切换两次，
	# → 报错/黑屏/切回主菜单诡异 bug 随机出现
```

**后果**：每次点击都启动一条独立的协程，多条协程并排跑，逻辑"重叠"了。这类 bug 的典型特征是"偶现、难复现"。

**修正模板：忙碌标志（busy flag）防抖**——

```gdscript
# ✅ 正确：用"忙碌标志"保证同一时刻只有一条协程在跑
var _busy := false

func _on_start_pressed() -> void:
	if _busy:
		return          # 上一轮还没完？本次点击直接忽略
	_busy = true
	$AnimationPlayer.play("fade_out")
	await $AnimationPlayer.animation_finished
	_busy = false
	get_tree().change_scene_to_file("res://scenes/main.tscn")
```

**循环变体**：想在循环里 await 也要想清楚"迭代之间会不会重叠"。下面两种写法结果完全不同：

```gdscript
# 写法 A：每 1 秒生成一个敌人（迭代之间不重叠，直觉正确）
while running:
	spawn_enemy()
	await get_tree().create_timer(1.0).timeout

# 写法 B：三秒后"同时"出 3 个敌人（for 循环里 await create_timer 是各自计时的！）
for i in 3:
	await get_tree().create_timer(3.0).timeout
	spawn_enemy()   # → 3 个敌人在同一帧扎堆出现
```

写法 B 里三次 `create_timer(3.0)` 是在循环每轮新建的计时器——前一轮 await 恢复后下一轮才开始计时，因此敌人是逐个延迟出现的。若你想要的是"三秒后同时刷三个"，应把循环和 await 的顺序调换。**结论：循环里 await，永远先问自己一句"每一轮之间会不会重叠？我希望它们重叠吗？"**

### 27.7.3 坑三：在 _ready 里 await 与场景切换冲突

```gdscript
# ❌ 错误：在临时节点的 _ready 里放长等待
func _ready() -> void:
	await get_tree().create_timer(5.0).timeout
	$IntroPanel.hide()      # → 玩家若在 5 秒内切走了场景：节点没了
	get_tree().change_scene_to_file("res://scenes/menu.tscn")
	# → 更糟：场景可能已经被别处切换过，第二次 change_scene 造成叠加/黑屏
```

**后果**：轻则静默失效（协程随节点被丢弃），重则在错误时机再次切场景。

**修正**：

```gdscript
# ✅ 正确：恢复后先确认"我"还活着、目标节点还在
func _ready() -> void:
	await get_tree().create_timer(5.0).timeout
	if not is_inside_tree():
		return                                # 已经离开场景树，什么都别做
	$IntroPanel.hide()
```

**更稳的思路**：别让"临时场景节点"承担长期流程。开场倒计时这类跨场景逻辑，放到自动加载单例（Autoload）里，由它驱动场景切换，就不会被场景卸载误伤。

### 27.7.4 坑四：拿 await 函数的返回值必须也 await

```gdscript
func roll_reward() -> String:
	await get_tree().create_timer(0.5).timeout
	return "传说武器"

# ❌ 错误：忘了 await，拿到的是"挂起状态"
func bad() -> void:
	var item = roll_reward()
	print(item.substr(0, 2))   # → 运行时报错：挂起状态对象没有 substr 方法
```

**修正**：

```gdscript
# ✅ 正确：await 一起写
func good() -> void:
	var item: String = await roll_reward()
	print(item.substr(0, 2))   # → 传说
```

记忆口诀：**协程函数的返回值，永远跟 await 成对出现**。要么 `await f()` 拿真值，要么 `var state = f()` 之后再 `await state`（gather 正是这么玩的）。

### 27.7.5 坑五：信号没成功发出，await 永久挂起

前面 27.5 已经讲过"超时兜底"，这里集中列出四种"永久挂起"的典型成因与排查：

| 成因 | 例子 | 症状 | 解药 |
| --- | --- | --- | --- |
| 循环动画永远不播完 | 动画循环播放，`await animation_finished` | 协程无声卡死 | 检查循环开关；或加超时 |
| tween 被 kill | `tween.kill()` 后 `await tween.finished` | `finished` 在被杀时**不会发出** | kill 前/后自己发一个"中止信号"，或用超时 |
| 信号源被 free | 等 `$Enemy.died`，但敌人节点被销毁 | 没人能再 emit 了 | `is_instance_valid` + 超时 |
| 拼错信号名 | `await player.dead`（实际叫 died） | 编辑器立刻报错（这类反而好查） | 看报错即可 |

```gdscript
# ❌ 错误：循环动画 + 裸等 = 永久挂起
func play_intro_anim() -> void:
	$AnimationPlayer.play("idle_loop")   # 这个动画是循环的！
	await $AnimationPlayer.animation_finished   # → 永远等不到
	next_step()                          # → 永远不会执行
```

**修正**：要么不播循环动画，要么加超时兜底：

```gdscript
# ✅ 正确：超时兜底
var done := await $AsyncUtil.wait_for_signal_or_timeout(
	$AnimationPlayer.animation_finished, 3.0)
next_step()
```

### 27.7.6 陷阱速查表

| 症状 | 大概率是 | 立即检查 |
| --- | --- | --- |
| 崩溃：freed instance | 坑一 | await 后是否验过 `is_instance_valid` |
| 偶现重复触发/逻辑重叠 | 坑二 | 有没有 busy 标志 |
| 代码"神不知鬼不觉没执行" | 坑三/坑五 | 所在节点是否被 free；信号是否真的会发出 |
| 拿到奇怪对象当值用 | 坑四 | 返回值是不是忘了 await |
| 协程卡住无报错 | 坑五 | 加超时，立刻见分晓 |

## 27.8 await 与 tween/动画结合

### 27.8.1 入门例：await tween.finished

```gdscript
func fade_out(control: Control) -> void:
	var tween := create_tween()
	tween.tween_property(control, "modulate:a", 0.0, 0.5)   # 0.5 秒淡出
	await tween.finished          # 等补间动画自然结束
	control.visible = false
	print("淡出完成")              # → 0.5 秒后打印
```

### 27.8.2 封装函数：等 AnimationPlayer 播完指定的动画

动画播放是"发起后马上返回"的异步操作，天然适合配 await。封装成函数后，调用处一行写完"播+等"：

```gdscript
class_name AnimUtil

## 播放动画并等它播完（带超时兜底，防止循环动画导致永久挂起）
static func play_and_wait(anim_player: AnimationPlayer, anim_name: String,
		timeout: float = 10.0) -> bool:
	if anim_player.has_animation(anim_name) == false:
		push_error("动画不存在：" + anim_name)
		return false
	anim_player.play(anim_name)
	var sig: Signal = anim_player.animation_finished
	# 简单等待（信任动画不循环时用）：
	await sig
	return true
```

实战：技能演出 = 三个动画依序播放，一行一个：

```gdscript
func cast_ult_skill() -> void:
	print("起手式！")
	await AnimUtil.play_and_wait($AnimationPlayer, "cast_raise")
	print("聚气！")
	await AnimUtil.play_and_wait($AnimationPlayer, "cast_charge")
	print("释放！")
	await AnimUtil.play_and_wait($AnimationPlayer, "cast_blast")
	deal_damage_to_all_enemies()
```

### 27.8.3 陷阱例：kill 掉的 tween 不会发 finished

```gdscript
# ❌ 错误：先 kill 再等 finished
var tween := create_tween()
tween.tween_property($Sprite2D, "position", Vector2(500, 0), 3.0)
$SkipButton.pressed.connect(func() -> void: tween.kill())   # 玩家点"跳过"
await tween.finished   # → 玩家一旦点了跳过：tween 被 kill，finished 永远不发出
	                   # → 协程永久挂起，后续演出全部哑火
```

**修正**：kill 与等待二选一，跳过时不要走"等 finished"这条路。可行做法是让"跳过"按钮直接推进流程，或者给等待加超时：

```gdscript
# ✅ 正确：等待方带超时，或让跳过逻辑亲自推进流程
var finished_naturally := await async_util.wait_for_signal_or_timeout(tween.finished, 3.5)
if not finished_naturally:
	print("动画被跳过/中止")   # 走跳过分支，流程继续
```

## 27.9 综合模板：剧情对话系统（压轴大模板）

本章压轴。把前面所有知识——信号参数、忙碌标志、超时、按钮信号等待、逐字打印——揉进一个完整的剧情对话系统 `DialogueRunner`。

### 27.9.1 需求拆解

- **逐字打印**：文字一个字一个字出现（打字机效果），有节奏感；
- **可跳过**：打印过程中按下"跳过键"立刻整行显示完；
- **等继续**：一行打完后，等待玩家按"继续键"（空格/回车）；
- **选项分支**：某些台词带选项，玩家点按钮做选择，并触发对应结果；
- **防重入**：对话播放中再次触发不会叠出两条对话（忙碌标志）；
- **对外信号**：`dialogue_started` / `dialogue_finished`，方便主流程衔接。

### 27.9.2 流程图

```
run(脚本)
  │
  ├── _busy？是 → 直接返回（防重入）
  │
  ├── for 每一行 line ──────┐
  │     ├─ _type_text() 逐字打印            │
  │     │     └─ await create_timer(字间延迟).timeout
  │     │     └─ 期间玩家按跳过键 → _skip_typing=true → 立刻整行显示
  │     ├─ 无选项？──→ _wait_continue() ── 轮询 ui_accept
  │     └─ 有选项？──→ _wait_choice()  ── await _choice_made 信号
  │                        └─ 拿到选项 index → 执行该选项的 action 回调
  │        （循环下一行）    │
  └── dialogue_finished.emit()  → 主流程继续
```

### 27.9.3 完整 DialogueRunner 类

```gdscript
class_name DialogueRunner
extends CanvasLayer
## 剧情对话系统（第 27 章压轴模板）
## 能力：逐字打印 / 跳过打印 / 等待继续 / 选项分支 / 防重入 / 完成信号
## 用法：把本类挂为节点（自动加载单例亦可），调用 run() 传入脚本数组，
##       调用处用 await 拿到"对话结束"的时机，无缝衔接后续剧情。

signal dialogue_started        # 对话开始（可用于隐藏游戏 UI）
signal dialogue_finished       # 对话结束（可用于恢复操作、触发后续剧情）
signal _choice_made(index: int)  # 内部信号：玩家点下了某个选项按钮

const TYPE_DELAY := 0.03          # 逐字间隔（秒）
const NEXT_ACTION := "ui_accept"  # 继续键（空格/回车）
const SKIP_ACTION := "ui_cancel"  # 跳过打印键（Esc）

var _busy := false                # 忙碌标志：防双击/防重入（见 27.7.2）
var _skip_typing := false         # 玩家是否要求跳过逐字打印

var _panel: PanelContainer
var _name_label: Label
var _text_label: Label
var _choice_box: VBoxContainer

func _ready() -> void:
	layer = 100            # 盖在游戏画面之上
	_build_ui()
	visible = false

## ---------- 对外唯一入口 ----------

## 运行一段对话脚本。脚本是一个数组，每个元素是一行：
##   {"name": "村长", "text": "你好呀！",
##    "choices": [{"text": "接受", "action": Callable}, ...]}   # choices 可省略
## 注意：run() 是协程，调用处写 await dialogue.run(...) 可以等它播完。
func run(script: Array) -> void:
	if _busy:
		return               # 已有对话在播，忽略新请求
	_busy = true
	visible = true
	dialogue_started.emit()

	for line in script:
		await _play_line(line)

	visible = false
	dialogue_finished.emit()
	_busy = false

## ---------- 内部：播放一行 ----------

func _play_line(line: Dictionary) -> void:
	_skip_typing = false
	_name_label.text = str(line.get("name", ""))
	_choice_box.visible = false
	await _type_text(str(line.get("text", "")))      # ① 逐字打印（可跳过）

	var choices: Array = line.get("choices", [])
	if choices.is_empty():
		await _wait_continue()                       # ②a 等继续键
	else:
		await _wait_choice(choices)                  # ②b 等玩家选选项

## ---------- 逐字打印（可跳过） ----------

func _type_text(full_text: String) -> void:
	_text_label.text = ""
	for i in full_text.length():
		if _skip_typing:
			break                    # 玩家要求跳过：不再逐字
		_text_label.text += full_text[i]
		await get_tree().create_timer(TYPE_DELAY).timeout   # 字与字之间等一小拍
	_text_label.text = full_text     # 无论跳没跳过，最终整行完整显示

## ---------- 等待"继续" ----------

func _wait_continue() -> void:
	# 逐帧轮询继续键；也可以换成超时自动继续（配合 AsyncUtil，见 27.5）
	while true:
		await get_tree().process_frame
		if Input.is_action_just_pressed(NEXT_ACTION):
			return

## ---------- 选项分支 ----------

func _wait_choice(choices: Array) -> void:
	_choice_box.visible = true
	var buttons: Array[Button] = []
	# 生成选项按钮
	for i in choices.size():
		var btn := Button.new()
		btn.text = str(choices[i].get("text", "……"))
		btn.pressed.connect(_emit_choice.bind(i))   # 点击 → 发内部信号
		_choice_box.add_child(btn)
		buttons.append(btn)

	var picked: int = await _choice_made              # 挂起，直到玩家点按钮

	for b in buttons:
		b.queue_free()                               # 清理按钮

	var action: Callable = choices[picked].get("action", Callable())
	if action.is_valid():
		action.call()                                # 执行选项对应的结果

func _emit_choice(index: int) -> void:
	_choice_made.emit(index)

## ---------- 跳过打印的输入 ----------

func _unhandled_input(event: InputEvent) -> void:
	if _busy and event.is_action_pressed(SKIP_ACTION):
		_skip_typing = true          # _type_text 下一拍检测到后立刻整行显示

## ---------- 极简 UI（正式项目可用场景编辑器搭建后 @export 注入） ----------

func _build_ui() -> void:
	_panel = PanelContainer.new()
	_panel.set_anchors_and_offsets_preset(Control.PRESET_CENTER_BOTTOM)
	_panel.offset_bottom = -40          # 底部留边
	_panel.offset_top = -240
	_panel.custom_minimum_size = Vector2(700, 200)

	var vbox := VBoxContainer.new()
	vbox.add_theme_constant_override("separation", 8)

	_name_label = Label.new()
	_name_label.add_theme_font_size_override("font_size", 22)

	_text_label = Label.new()
	_text_label.autowrap_mode = TextServer.AUTOWRAP_WORD_SMART
	_text_label.custom_minimum_size = Vector2(660, 96)

	_choice_box = VBoxContainer.new()

	vbox.add_child(_name_label)
	vbox.add_child(_text_label)
	vbox.add_child(_choice_box)
	_panel.add_child(vbox)
	add_child(_panel)
```

### 27.9.4 使用示例：NPC 支线剧情

```gdscript
extends Node

@onready var dialogue: DialogueRunner = $DialogueRunner

func talk_to_elder() -> void:
	# 选项的"结果"用 Callable 表达，写成 lambda 最方便
	var accept := func() -> void:
		Globals.quest_state = "accepted"
		print("【系统】任务已接受")
	var refuse := func() -> void:
		Globals.quest_state = "refused"
		print("【系统】玩家拒绝了任务")

	await dialogue.run([
		{"name": "村长", "text": "年轻的冒险者，村子东边的森林又闹怪物了……"},
		{"name": "你",   "text": "这次又是什么怪物？"},
		{"name": "村长", "text": "没人说得清。你……愿意帮我们一次吗？",
			"choices": [
				{"text": "接受委托", "action": accept},
				{"text": "改天再说", "action": refuse},
			]},
	])
	# await 保证对话真正播完才走到这里
	print("对话结束，当前任务状态：", Globals.quest_state)   # → 对话结束，当前任务状态：accepted
```

### 27.9.5 扩展建议

- **自动继续**：把 `_wait_continue` 换成 `await async_util.wait_for_signal_or_timeout(继续信号, 5.0)`，即可实现"挂机 5 秒自动跳行"；
- **打字音效**：在 `_type_text` 的循环里每出一字 `Audio.play("type_click")` 即可；
- **剧情数据外置**：把脚本数组挪到 JSON / CSV 中（正好衔接第 28 章），由程序读取后喂给 `run()`；
- **富文本**：把 `Label` 换成 `RichTextLabel`，即可支持颜色、抖动等效果。

## 本章小结

- 游戏主线程每帧必须完成"输入→逻辑→渲染"，**任何长时间占用主线程的等待都会冻结画面**；
- `await` 的本质是把函数**就地挂起**、立刻归还控制权，等信号到了再从断点恢复，局部变量全程保留；
- 含 `await` 的函数是**协程**：不加 await 调用它得到"挂起状态"，加 await 得到最终返回值；
- `await 信号` 是有值的表达式：**0 参返回 null，1 参返回参数本体，多参返回 Array**；
- await 一个信号**不需要 connect**，await 自带监听；await 数字/字符串/普通函数调用会直接报错；
- 等待三件套：`create_timer`（一次性延时）、`await 信号`（事件驱动）、Timer 节点（周期性、检查器可配置），精度都是帧级；
- 一切"等外部世界"的 await 都要配**超时兜底**：`wait_for_signal_or_timeout` 用两个信号赛跑，谁先到听谁的；
- **并发模板 gather** 的心法是"先全部点火、再按顺序收货"：先把协程调用收集成挂起状态数组，再逐个 await；
- await 之后访问节点前必须 `is_instance_valid` 验货——**等待期间节点可能已被 free**；
- 重复触发类逻辑要加**忙碌标志**防重入，否则连点按钮会让多条协程重叠执行，产生偶现 bug；
- 协程所在节点被 free 时，协程会被静默丢弃——**重要延时流程放到常驻单例上更稳**；
- 拿协程返回值必须成对写 await；被 kill 的 tween 不会发 finished，循环动画永远不发 animation_finished——这俩是"永久挂起"的高发源头；
- 压轴模板 DialogueRunner 展示了协程式流程代码的最终形态：**写起来像剧本，跑起来是异步**。

---

# 第 28 章：文件、JSON 与配置

> 你的游戏总会想"记住"一些东西：玩家的进度、屏幕的亮度、上一次选的语言、放在哪个存档槽。这些东西必须写到磁盘上才能在下次启动时原样找回。本章解决三个问题：**写到哪里**（路径）、**怎么写**（FileAccess 与 JSON）、**写什么**（存档与配置的数据结构设计），最后同样以一套可直接抄用的 SaveManager / SettingsManager 压轴。

## 28.1 三种路径彻底讲清

### 28.1.1 先解决哲学问题：res://、user://、绝对路径

Godot 中引用一个文件路径，只有三种写法，各自的"脾气"完全不同：

| 前缀 | 指向 | 开发时（编辑器里） | 导出后（玩家机器上） |
| --- | --- | --- | --- |
| `res://` | 项目根目录（project.godot 所在处） | 真实文件夹，可读**可写** | 打进 PCK 包，**只读** |
| `user://` | 专为你的游戏准备的可写目录 | 真实可写目录 | 真实可写目录（各平台位置不同） |
| 绝对路径 | 如 `C:/xx`、`/home/xx` | 直接用 | 受平台权限约束，尽量别用 |

两个立刻能得出结论：

1. **读游戏自带资源**用 `res://`：`load("res://sprites/player.png")`；
2. **写任何运行期数据**（存档、设置、日志）用 `user://`。

### 28.1.2 user:// 在各平台的真实位置

`user://` 是个"虚拟目录"，引擎会替你映射到每个平台的规范位置（项目名取自 project.godot 的 `config/name`）：

| 平台 | `user://` 的实际位置 |
| --- | --- |
| Windows | `%APPDATA%\Godot\app_userdata\<项目名>` |
| macOS | `~/Library/Application Support/Godot/app_userdata/<项目名>` |
| Linux | `~/.local/share/godot/app_userdata/<项目名>` |
| Android | 应用私有目录 `/data/data/<包名>/files/` |
| iOS | 应用沙盒的 Documents |
| Web | 浏览器管理的虚拟存储（IndexedDB） |

开发期想快速打开这个目录看文件，可以在代码里打印：

```gdscript
func _ready() -> void:
	print(OS.get_user_data_dir())   # → Windows 上如 C:\Users\你\AppData\Roaming\Godot\app_userdata\我的游戏
```

也可以用 `ProjectSettings.globalize_path("user://")` 把虚拟路径翻译成绝对路径——引擎读写它时自动做这件事，我们一般不用手动翻。

### 28.1.3 陷阱例：开发能写、导出必失败的 res://

```gdscript
# ❌ 错误：往 res:// 写存档
func save_bad(data: Dictionary) -> void:
	var f := FileAccess.open("res://saves/save.json", FileAccess.WRITE)
	if f == null:
		push_error("为什么我一导出就存不了档？")   # → 编辑器里一切正常，导出版必失败
		return
	f.store_string(JSON.stringify(data))
```

**后果**：这是最经典的"在我机器上是好的"。编辑器里 `res://` 是真实目录所以能写；导出后 `res://` 在 PCK 包内，是**只读**的，open 直接失败。

**修正**：运行期一律写 `user://`。确实需要区分开发/发布行为时，可以用特性判断：

```gdscript
# ✅ 正确：运行期写 user://
func save_good(data: Dictionary) -> void:
	var path := "user://save.json"
	var f := FileAccess.open(path, FileAccess.WRITE)
	if f:
		f.store_string(JSON.stringify(data))

# 补充技巧：判断当前是否在编辑器里运行
func is_dev() -> bool:
	return OS.has_feature("editor")   # → 编辑器运行时为 true，导出后为 false
```

## 28.2 FileAccess 完全教程

Godot 4 用 `FileAccess` 类读写文件（注意：**Godot 3 的 `File` 类已不存在，老教程要换算**）。

### 28.2.1 打开文件：open 与模式枚举

```gdscript
var f := FileAccess.open("user://save.json", FileAccess.READ)
```

第二个参数决定"打开后能干什么"，五个常用模式务必分清：

| 模式 | 可读？ | 可写？ | 文件不存在时 | 文件已存在时 |
| --- | --- | --- | --- | --- |
| `FileAccess.READ` | ✓ | ✗ | **打开失败（null）** | 从头读 |
| `FileAccess.WRITE` | ✗ | ✓ | 新建 | **清空重写** |
| `FileAccess.READ_WRITE` | ✓ | ✓ | 新建 | 不清空，指针在开头 |
| `FileAccess.WRITE_READ` | ✓ | ✓ | 新建 | **清空**重写 |
| `FileAccess.APPEND` | ✗ | ✓（只追加） | 新建 | 指针挪到**末尾** |

最容易踩的差别：`WRITE` 会把旧文件**整个抹掉**，`APPEND` 只是往尾部**接着写**，`READ_WRITE` 不动旧内容。

### 28.2.2 防御式检查：open 失败返回 null

`open` 失败时**返回 null 而不抛异常**，不检查就往下用，必然崩溃：

```gdscript
# ❌ 错误：不检查 null
var f := FileAccess.open("user://save.json", FileAccess.READ)
f.get_as_text()   # → 文件不存在时 f 为 null：直接崩溃（nil 上调方法）

# ✅ 正确：防御式检查 + 读出错误码
var f := FileAccess.open("user://save.json", FileAccess.READ)
if f == null:
	var err := FileAccess.get_open_error()   # 静态方法：拿到刚才失败的原因
	push_error("打开失败：%s" % error_string(err))   # → 打开失败：Can't open file（或 File not found 等）
	return
```

`error_string()` 能把错误码翻译成人话，常见的有：`OK`、`File not found`（没这个文件）、`Can't open file`（权限/占用问题）等。

### 28.2.3 读写文本：get_as_text 与 store_string

```gdscript
# ---------- 写文本 ----------
func write_text(path: String, content: String) -> bool:
	var f := FileAccess.open(path, FileAccess.WRITE)   # WRITE：没有就建，有就覆盖
	if f == null:
		return false
	f.store_string("第一行\n")      # 原样写入字符串
	f.store_line("第二行")          # store_line 自动补换行，适合逐行写日志
	f.flush()                       # 把缓冲立即刷进磁盘（重要，见下）
	f.close()                       # 显式关闭
	return true

# ---------- 读文本 ----------
func read_text(path: String) -> String:
	var f := FileAccess.open(path, FileAccess.READ)
	if f == null:
		return ""
	var text := f.get_as_text()    # 一次性读全文
	f.close()
	return text
	# → "第一行\n第二行\n"
```

逐行读也很常用：

```gdscript
while not f.eof_reached():
	var line := f.get_line()     # → 每次返回一行（不含换行符）
	print(line)
```

### 28.2.4 flush 与 close：缓冲区的秘密

`store_string` 写的内容先落在**内存缓冲区**里，引擎稍后才真正落盘。这带来一个隐蔽风险：

```gdscript
# ❌ 陷阱：写了不 flush，程序崩溃后文件是空的
f.store_string("玩家进度：第 8 章")
# ——此时玩家拔电源/游戏崩溃——
# → 磁盘上的文件可能只有半截甚至一个空壳
```

**规则**：写完就怕丢的关键数据，`flush()` 立刻刷盘；写完不再用的文件，`close()` 关闭（顺带刷盘）。

### 28.2.5 "with 风格"：自动关闭的推荐写法

GDScript 没有自带 `with` 语句，但 Godot 4 的 `FileAccess` 是引用计数的：**局部变量离开作用域时文件自动关闭**。利用这一点可以写得很优雅：

```gdscript
# ✅ 推荐：作用域自动关闭（with 风格）
func write_all_text(path: String, content: String) -> bool:
	var f := FileAccess.open(path, FileAccess.WRITE)
	if f == null:
		return false
	f.store_string(content)
	return true
	# 函数返回时 f 离开作用域 → 文件自动关闭，无需显式 close()
```

对一次性小文件，这是最省心的写法；对"写一点、处理一点、再写一点"的长流程，建议保留显式 `close()` 让意图更明显。**两种都合法，团队统一即可。**

### 28.2.6 读写二进制

JSON 适合"人能看懂"的数据；二进制格式更紧凑，而且**类型不丢**。`FileAccess` 提供成对的 `store_x / get_x`：

```gdscript
# ---------- 写二进制 ----------
func save_binary() -> void:
	var f := FileAccess.open("user://data.bin", FileAccess.WRITE)
	f.store_32(1337)          # 按 32 位整数写（4 字节）
	f.store_float(3.14)       # 双精度浮点（8 字节）
	f.store_var({"hp": 100})  # 直接序列化整个 Variant（Dictionary 原样保存）
	f.close()

# ---------- 读二进制：必须与写入顺序完全一致 ----------
func load_binary() -> void:
	var f := FileAccess.open("user://data.bin", FileAccess.READ)
	if f == null:
		return
	var n: int = f.get_32()          # → 1337
	var x: float = f.get_float()     # → 3.14
	var d: Dictionary = f.get_var()  # → {"hp":100}
	f.close()
```

家族成员速查：`store_8/16/32/64`（整数）、`store_float`、`store_double`、`store_string`（无长度头）、`store_pascal_string`（带长度头）、`store_var`（整个 Variant）。

`store_var/get_var` 是"上帝视角"的序列化——数组、字典、Vector2 全都能存。但要注意 `get_var(true)`（允许反序列化对象）是个危险选项：会把存进去的对象重新实例化，遇到来路不明的文件可能执行意外代码。**读自家生成的文件也别开这个选项，除非你清楚代价。**

### 28.2.7 实用静态方法

`FileAccess` 还有几个好用的静态方法（直接用类名调用）：

```gdscript
FileAccess.file_exists("user://save.json")   # → 文件是否存在（true/false）
FileAccess.get_sha256("user://save.json")    # → 文件内容校验和（防篡改/比对，见 28.8）
```

## 28.3 JSON 专题

### 28.3.1 为什么存档爱用 JSON

- **人能直接读**：出 bug 时打开存档文件肉眼就能检查；
- **引擎内置**：`JSON` 单例开箱即用，不需要第三方库；
- **通用**：和服务器、mod 社区、其他工具交换数据都方便。
- **代价**：类型系统很弱，见下面的映射表——坑都长在类型上。

### 28.3.2 JSON.stringify：Variant → JSON 字符串

```gdscript
var data := {
	"name": "骑士",
	"hp": 100,
	"items": ["剑", "盾"],
}
print(JSON.stringify(data))
# → {"hp":100,"items":["剑","盾"],"name":"骑士"}   （紧凑格式，省空间）

print(JSON.stringify(data, "\t"))
# → 带缩进的格式（第二个参数是缩进字符串），人眼可读：
#   {
#       "hp": 100,
#       "items": [
#           "剑",
#           "盾"
#       ],
#       "name": "骑士"
#   }
```

**建议**：给玩家的存档、给 modder 的数据文件用带缩进格式（可读性优先）；网络传输用紧凑格式（体积优先）。

### 28.3.3 JSON.parse_string：JSON 字符串 → Variant

```gdscript
var parsed = JSON.parse_string('{"hp": 100, "name": "骑士"}')
print(parsed["name"])           # → 骑士
print(typeof(parsed["hp"]))     # → TYPE_FLOAT（注意！不是 int，详见 28.8.1）
```

**解析失败时返回 null**（不抛异常）——所以每次解析都必须判空：

```gdscript
# ❌ 错误：不判空直接用
var d = JSON.parse_string(corrupted_text)
print(d["hp"])     # → 文件损坏时 d 为 null，直接崩溃

# ✅ 正确：判空
var d = JSON.parse_string(corrupted_text)
if d == null:
	push_warning("存档解析失败，视为损坏")
	return {}
```

### 28.3.4 类型映射表（重点陷阱都在这张表里）

| GDScript 类型 | JSON 类型 | 写入注意 | 读回注意 |
| --- | --- | --- | --- |
| `int` | number | ✓ 正常写 | **读回变 float**！`100 → 100.0` |
| `float` | number | ✓ 正常写 | ✓ |
| `bool` | bool | ✓ | ✓ |
| `String` | string | ✓ | ✓ |
| `null` | null | ✓ | ✓（但和"解析失败"撞车，见 28.3.5） |
| `Array` | array | ✓（嵌套也行） | ✓ |
| `Dictionary` | object | **键只能是字符串**：数字键 `1` 会被写成 `"1"` | 键一律是 `String` 类型 |
| `Vector2 / Vector2i / Color / Rect2` 等 | ❌ 不直接支持 | 直接 stringify 会变成 `"(12, 34)"` 之类的**文字描述** | 读回只是普通字符串，**还原不出引擎类型** |

引擎类型（Vector2 等）的正确处理是**手动转字典**：

```gdscript
# ---------- Vector2 → JSON ----------
var pos := Vector2(12, 34)
var dict := {"x": pos.x, "y": pos.y}          # ✓ 手动拆成字段
print(JSON.stringify(dict))                    # → {"x":12.0,"y":34.0}

# ---------- JSON → Vector2 ----------
var back = JSON.parse_string('{"x":12.0,"y":34.0}')
var pos_back := Vector2(back["x"], back["y"]) # 手动装回去
print(pos_back)                                # → (12, 34)
```

### 28.3.5 模板：safe_load（防损坏读取）

把"判文件存在 → 判 open → 判解析 → 判类型"四道关卡打包成一个通用函数：

```gdscript
class_name JsonUtil

## 安全地从磁盘读一个 JSON 文件。
## 返回解析好的 Variant；任何一步失败都返回 null。
static func safe_load_json(path: String) -> Variant:
	# 关卡①：文件存在吗？
	if not FileAccess.file_exists(path):
		return null
	# 关卡②：能打开吗？（被占用/权限问题）
	var f := FileAccess.open(path, FileAccess.READ)
	if f == null:
		push_warning("无法打开文件：%s" % path)
		return null
	var raw := f.get_as_text()
	f.close()
	# 关卡③：内容是合法 JSON 吗？
	var parsed = JSON.parse_string(raw)
	if parsed == null:
		push_warning("JSON 已损坏：%s" % path)
		return null
	# 关卡④：是我期望的类型吗？（比如期望是个字典）
	if not (parsed is Dictionary):
		push_warning("JSON 结构不符合预期：%s" % path)
		return null
	return parsed
```

一个边缘细节：如果文件内容恰好是字符串 `null`，`parse_string` 也返回 null，与"解析失败"无法区分。因此**约定存档文件永远保存一个对象 `{}` 或数组 `[]`，不要存裸值**，就没有歧义了。

## 28.4 完整存档系统模板（压轴）

### 28.4.1 设计先行：存档结构长什么样

存档系统的质量几乎完全取决于**数据结构设计**。我们采用"信封 + 信纸"两层结构：

```
user://saves/
├── slot_1.json        ← 存档本体
├── slot_1.json.bak    ← 上一次保存的备份（损坏时救命用）
├── slot_2.json
└── slot_3.json
```

存档文件内部：

```json
{
    "checksum": "a1b2c3d4……",
    "body": {
        "version": 2,
        "timestamp": "2026-10-03 12:00:00",
        "data": {
            "player_name": "骑士",
            "hp": 100,
            "gold": 250,
            "pos": { "x": 12.5, "y": -3.0 },
            "items": ["剑", "盾"]
        }
    }
}
```

三层各司其职：

| 层 | 字段 | 作用 |
| --- | --- | --- |
| 信封 | `checksum` | 校验和：检测损坏与篡改 |
| 信封 | `body` | 完整的存档内容（校验和的计算对象） |
| 信纸 | `version` | 存档格式版本号 → 支撑版本迁移 |
| 信纸 | `timestamp` | 保存时间 → 存档列表显示用 |
| 信纸 | `data` | 游戏真正的进度数据 |

### 28.4.2 完整 SaveManager 类

```gdscript
class_name SaveManager
extends Node
## 完整存档系统（第 28 章压轴模板）
## 能力：多槽位 / 版本迁移 / 校验和防篡改 / 损坏自动回滚备份 / 槽位列表扫描

const SAVE_DIR := "user://saves"
const CURRENT_VERSION := 2
const SLOT_COUNT := 3
const SECRET := "把这里换成你的私钥_别照抄"   # 校验和加盐：防玩家手改存档

func _ready() -> void:
	# 启动时确保存档目录存在（make_dir_recursive：多层也能一次建好）
	DirAccess.make_dir_recursive_absolute(SAVE_DIR)

# ---------------- 路径 ----------------

func slot_path(slot: int) -> String:
	return "%s/slot_%d.json" % [SAVE_DIR, slot]

func backup_path(slot: int) -> String:
	return slot_path(slot) + ".bak"   # 备份就是同目录的 .bak 文件

# ---------------- 保存 ----------------

## 保存到指定槽位。data 是游戏进度字典。返回是否成功。
func save_game(slot: int, data: Dictionary) -> bool:
	# ① 组装"信纸"：版本号 + 时间戳 + 玩家数据
	var body := {
		"version": CURRENT_VERSION,
		"timestamp": Time.get_datetime_string_from_system(),
		"data": data,
	}
	# ② 组装"信封"：校验和 + 信纸
	var wrapper := {
		"checksum": _make_checksum(body),
		"body": body,
	}
	# ③ 覆盖前先备份旧档（损坏回滚全靠它）
	if FileAccess.file_exists(slot_path(slot)):
		var err := DirAccess.copy_absolute(slot_path(slot), backup_path(slot))
		if err != OK:
			push_warning("备份失败：%s" % error_string(err))
	# ④ 真正写盘
	return _write_json(slot_path(slot), wrapper)

func _write_json(path: String, value: Variant) -> bool:
	var f := FileAccess.open(path, FileAccess.WRITE)
	if f == null:
		push_error("存档写入失败：%s" % error_string(FileAccess.get_open_error()))
		return false
	f.store_string(JSON.stringify(value, "\t"))   # 带缩进：方便玩家/开发者排错
	return true   # f 在函数结束时自动关闭（见 28.2.5）

# ---------------- 读取 ----------------

## 从指定槽位读取。失败（含损坏+备份也损坏）返回空字典 {}。
func load_game(slot: int) -> Dictionary:
	# ① 先读主存档
	var wrapper = _load_wrapper(slot_path(slot))

	# ② 主存档读不到？→ 尝试备份
	if wrapper == null:
		wrapper = _load_wrapper(backup_path(slot))
		if wrapper == null:
			return {}    # 主档备份全灭 → 当作新档开始

	# ③ 校验和检查（防损坏 / 防手改）
	var body: Dictionary = wrapper.get("body", {})
	if _make_checksum(body) != wrapper.get("checksum", ""):
		push_warning("槽位 %d 校验和不匹配，尝试备份……" % slot)
		var backup = _load_wrapper(backup_path(slot))
		if backup == null or _make_checksum(backup.get("body", {})) != backup.get("checksum", ""):
			return {}    # 备份也坏了 → 放弃，回退新档
		body = backup["body"]

	# ④ 版本迁移：老存档升级到当前版本
	body = _migrate(body)
	return body.get("data", {})

## 读取并校验一个存档文件的原始结构，失败返回 null
func _load_wrapper(path: String) -> Variant:
	if not FileAccess.file_exists(path):
		return null
	var f := FileAccess.open(path, FileAccess.READ)
	if f == null:
		return null
	var parsed = JSON.parse_string(f.get_as_text())
	f.close()
	if parsed == null or not (parsed is Dictionary):
		return null   # 解析失败 / 不是对象 → 视为损坏
	return parsed

# ---------------- 版本迁移 ----------------

## 老版本存档 → 当前版本。核心思想：缺的字段补默认值，永远向后兼容。
func _migrate(body: Dictionary) -> Dictionary:
	var version := int(body.get("version", 1))
	if version < 2:
		# v1 → v2：v1 存档没有 gold 和 pos 字段，补上默认值
		var data: Dictionary = body.get("data", {})
		if not data.has("gold"):
			data["gold"] = 100        # 老玩家默认送 100 金币
		if not data.has("pos"):
			data["pos"] = {"x": 0, "y": 0}
		body["data"] = data
		body["version"] = CURRENT_VERSION
		# 注意：迁移只发生在内存里，玩家下次 save 时自然写回新版本
	return body

# ---------------- 工具 ----------------

## 生成校验和：内容 + 私钥 一起做 sha256（见 28.8.5）
func _make_checksum(body: Dictionary) -> String:
	return (JSON.stringify(body) + SECRET).sha256()

## 扫描所有槽位，供存档界面显示（用法详见 28.7）
func list_save_slots() -> Array[Dictionary]:
	var out: Array[Dictionary] = []
	for slot in range(1, SLOT_COUNT + 1):
		var info := {"slot": slot, "empty": true, "player_name": "空", "time": ""}
		var wrapper = _load_wrapper(slot_path(slot))
		if wrapper != null:
			var body: Dictionary = wrapper.get("body", {})
			if not body.is_empty():
				info.empty = false
				var data: Dictionary = body.get("data", {})
				info.player_name = str(data.get("player_name", "无名冒险者"))
				info.time = str(body.get("timestamp", ""))
		out.append(info)
	return out
```

### 28.4.3 使用示例

```gdscript
extends Node

var save_manager: SaveManager   # 建议挂成自动加载单例

func demo() -> void:
	# ---- 存档 ----
	save_manager.save_game(1, {
		"player_name": "骑士",
		"hp": 100,
		"gold": 250,
		"pos": {"x": 12.5, "y": -3.0},     # Vector2 必须手动拆字段（见 28.3.4）
		"items": ["剑", "盾"],
	})

	# ---- 读档 ----
	var data := save_manager.load_game(1)
	if data.is_empty():
		print("没有可用存档，开始新游戏")
	else:
		print("欢迎回来，", data["player_name"])   # → 欢迎回来，骑士
		var pos := Vector2(data["pos"]["x"], data["pos"]["y"])   # 装回引擎类型
		print("上次位置：", pos)                      # → 上次位置：(12.5, -3)

	# ---- 存档槽界面 ----
	for info in save_manager.list_save_slots():
		if info.empty:
			print("槽位 %d：<空>" % info.slot)
		else:
			print("槽位 %d：%s  %s" % [info.slot, info.player_name, info.time])
			# → 槽位 1：骑士  2026-10-03 12:00:00
```

### 28.4.4 版本迁移的黄金法则

- **只加不删**：新版本永远只"补默认值"，不要删老字段——你永远不知道还有多少旧档在路上；
- **迁移幂等**：同一个函数跑两遍结果必须一样（我们用 `has()` 判断就是为此）；
- **version 必须从第一天就写**：哪怕 v1 也写上 `"version": 1`，将来才有判断依据。这是新手最容易忽略、一年后最后悔的一条。

## 28.5 ConfigFile 教程：分 section 的 ini

### 28.5.1 为什么设置文件别用 JSON

游戏设置（音量、画质、语言）和存档需求不同：**天生适合分组、需要默认值兜底、希望玩家能手动编辑**。`ConfigFile` 生成的就是经典 ini 格式：

```ini
[audio]
master_volume=0.8

[video]
fullscreen=true
resolution=Vector2i(1280, 720)

[language]
locale="zh_CN"
```

`ConfigFile` 与 JSON 的对比：

| 维度 | JSON | ConfigFile |
| --- | --- | --- |
| 结构 | 任意嵌套 | 按 section（节）平铺分组 |
| 默认值 | 全靠手写 `get()` 兜底 | `get_value()` **原生带默认值参数** |
| 引擎类型（Vector2i、Color） | ✗ 要手动转 | ✓ **直接存取**，不丢类型 |
| 整数会变 float | ✓（大坑） | ✗ 不会 |
| 玩家手改 | 容易改坏（少个逗号就全灭） | ini 容错好，还支持 `#`、`;` 注释 |
| 适用 | 存档、网络传输 | 设置文件 |

### 28.5.2 基本用法

```gdscript
var cfg := ConfigFile.new()

# ---------- 读（不存在就用默认值，不会报错） ----------
cfg.load("user://settings.cfg")          # 文件不存在返回错误码，但不影响后续
var vol: float = cfg.get_value("audio", "master_volume", 0.8)   # 第 3 个参数 = 默认值
print(vol)                                # → 首次运行为 0.8，之后为上次保存的值

# ---------- 写 ----------
cfg.set_value("audio", "master_volume", 0.5)
cfg.set_value("video", "fullscreen", true)
cfg.save("user://settings.cfg")

# ---------- 查询与删除 ----------
print(cfg.has_section("video"))               # → true
print(cfg.has_section_key("video", "fullscreen"))   # → true
cfg.erase_section_key("video", "fullscreen")  # 删单个键
```

`get_value` 的默认值参数是灵魂：**读取处永远写上默认值，就不需要"首运行初始化"这种特殊流程**——文件不存在、键不存在，都会安静地拿到默认值。

## 28.6 设置系统模板：SettingsManager

把音量、窗口模式、分辨率、语言四个设置做成"改了立即生效 + 自动持久化"的完整模块：

```gdscript
class_name SettingsManager
extends Node
## 设置系统模板：音量/窗口模式/分辨率/语言
## 特性：读写统一入口、改完立即生效并保存、首运行自动落默认值

signal settings_changed(key: String, value: Variant)   # UI 可监听它同步显示

const PATH := "user://settings.cfg"
const SECTION := "game"

## 默认值表：唯一事实来源（首运行写盘 / 读取兜底都靠它）
const DEFAULTS := {
	"master_volume": 0.8,            # 主音量（0~1 线性值）
	"window_mode": 0,                # 0=窗口 1=全屏
	"resolution": Vector2i(1280, 720),
	"language": "zh_CN",
}

var _cfg := ConfigFile.new()

func _ready() -> void:
	_load_or_init()
	apply_all()      # 启动时把保存的设置全部应用一遍

# ---------------- 读 ----------------

func get_setting(key: String) -> Variant:
	# 原生默认值兜底：文件不存在 / 键不存在都不会出错
	return _cfg.get_value(SECTION, key, DEFAULTS[key])

# ---------------- 写（立即生效 + 保存） ----------------

func set_setting(key: String, value: Variant) -> void:
	_cfg.set_value(SECTION, key, value)
	_apply_one(key, value)      # 立即生效
	_cfg.save(PATH)             # 立即持久化
	settings_changed.emit(key, value)

# ---------------- 首运行 ----------------

func _load_or_init() -> void:
	if _cfg.load(PATH) != OK:
		# 首次运行：把默认值全部写进文件，玩家从此可以手动编辑它
		for key in DEFAULTS:
			_cfg.set_value(SECTION, key, DEFAULTS[key])
		_cfg.save(PATH)

# ---------------- 应用到引擎 ----------------

func apply_all() -> void:
	for key in DEFAULTS:
		_apply_one(key, get_setting(key))

func _apply_one(key: String, value: Variant) -> void:
	match key:
		"master_volume":
			var idx := AudioServer.get_bus_index("Master")
			AudioServer.set_bus_volume_db(idx, linear_to_db(float(value)))
			AudioServer.set_bus_mute(idx, float(value) <= 0.001)
		"window_mode":
			if int(value) == 1:
				DisplayServer.window_set_mode(DisplayServer.WINDOW_MODE_FULLSCREEN)
			else:
				DisplayServer.window_set_mode(DisplayServer.WINDOW_MODE_WINDOWED)
		"resolution":
			# 分辨率只在窗口模式下生效（全屏由系统接管）
			if int(get_setting("window_mode")) == 0:
				DisplayServer.window_set_size(value)
		"language":
			TranslationServer.set_locale(str(value))
		_:
			push_warning("未知设置项：" + key)
```

使用示例：

```gdscript
extends Control

var settings: SettingsManager   # 建议挂为自动加载单例

func _on_volume_slider_changed(value: float) -> void:
	settings.set_setting("master_volume", value)   # 拖动即生效+保存，无需"确定"按钮

func _on_fullscreen_toggled(pressed: bool) -> void:
	settings.set_setting("window_mode", 1 if pressed else 0)
	# → 窗口立即切换全屏，且下次启动记得住
```

## 28.7 目录操作：DirAccess

### 28.7.1 常用 API 速览

Godot 4 的目录操作由 `DirAccess` 承担（Godot 3 的 `Directory` 类已移除）。最常用的方法分三组：

| 功能 | 写法 | 说明 |
| --- | --- | --- |
| 建目录 | `DirAccess.make_dir_recursive_absolute("user://a/b/c")` | 多层路径一次建齐，已存在也不报错 |
| 目录存在？ | `DirAccess.dir_exists_absolute("user://a")` | 返回 bool |
| 文件存在？ | `DirAccess.file_exists_absolute("user://a/f.json")` | 与 `FileAccess.file_exists` 等效 |
| 复制 | `DirAccess.copy_absolute(from, to)` | 返回错误码（OK 才成功），**不会连子目录** |
| 删除文件 | `DirAccess.remove_absolute("user://a/f.json")` | 只删文件 |
| 打开+遍历 | `DirAccess.open("user://a")` + `list_dir_begin()` | 见下方 |

### 28.7.2 遍历目录：list_dir_begin / get_next / list_dir_end

```gdscript
## 列出某目录下的所有文件名（不含子目录内容）
func list_files(dir_path: String) -> Array[String]:
	var out: Array[String] = []
	var dir := DirAccess.open(dir_path)
	if dir == null:
		push_warning("目录打不开：" + dir_path)
		return out

	dir.list_dir_begin()          # ① 开始遍历
	var fname := dir.get_next()   # ② 每调一次返回一个条目；没有更多时返回 ""
	while fname != "":
		# 过滤两个特殊目录条目（若 list_dir_begin() 用默认参数，它们会出现！）
		if fname == "." or fname == "..":
			fname = dir.get_next()
			continue
		if not dir.current_is_dir():      # 只收文件，跳过子目录
			out.append(fname)
		fname = dir.get_next()            # ③ 取下一个
	dir.list_dir_end()            # ④ 结束遍历（必须调用）
	return out
```

**两个要点**：

1. 默认参数下 `get_next()` 会把 `.`（当前目录）和 `..`（上级目录）也列出来，必须过滤；
2. `list_dir_begin(true, true)` 可以分别跳过这两项与隐藏文件，但为了兼容各平台，教程统一显式过滤，最直观可靠。

### 28.7.3 实战：存档槽位扫描（显示槽位名+时间）

结合 28.4 的存档文件命名规范（`slot_1.json`），扫描目录生成存档界面的槽位列表：

```gdscript
class_name SaveSlotScanner
extends Node

## 扫描存档目录，返回所有有效存档的信息（槽位号 + 玩家名 + 保存时间）
func scan_slots() -> Array[Dictionary]:
	var result: Array[Dictionary] = []
	var dir := DirAccess.open("user://saves")
	if dir == null:
		return result                 # 目录都没有 = 一个存档都没有

	dir.list_dir_begin()
	var fname := dir.get_next()
	while fname != "":
		# 命名规范过滤：slot_数字.json，跳过 .bak 备份
		if fname.begins_with("slot_") and fname.ends_with(".json"):
			var slot := fname.trim_prefix("slot_").trim_suffix(".json").to_int()
			# 复用 SaveManager 的安全读取
			var wrapper = SaveManager._load_wrapper("user://saves/" + fname)
			if wrapper != null:
				var body: Dictionary = wrapper.get("body", {})
				result.append({
					"slot": slot,
					"player_name": str(body.get("data", {}).get("player_name", "?")),
					"time": str(body.get("timestamp", "?")),
				})
		fname = dir.get_next()
	dir.list_dir_end()

	# 按槽位号排序，界面展示更规整
	result.sort_custom(func(a, b): return a.slot < b.slot)
	return result

# 使用效果：
# for s in $Scanner.scan_slots():
#     print("槽位 %d：%s（%s）" % [s.slot, s.player_name, s.time])
# → 槽位 1：骑士（2026-10-03 12:00:00）
# → 槽位 2：法师（2026-10-01 09:30:00）
```

### 28.7.4 陷阱例：复制/删除用错对象

```gdscript
# ❌ 错误：以为 copy 能拷整个文件夹
DirAccess.copy_absolute("user://old_saves", "user://backups")   # → 目录不会被复制，函数对目录无能为力

# ✅ 正确：目录要自己遍历后逐个文件 copy
var dir := DirAccess.open("user://old_saves")
DirAccess.make_dir_recursive_absolute("user://backups")
dir.list_dir_begin()
var fname := dir.get_next()
while fname != "":
	if not dir.current_is_dir():
		DirAccess.copy_absolute("user://old_saves/" + fname, "user://backups/" + fname)
	fname = dir.get_next()
dir.list_dir_end()
```

## 28.8 陷阱大全：文件系统的五个经典坑

### 28.8.1 坑一：JSON 数字全是 float，大整数丢精度

JSON 规范里只有"number"一种数字，解析后统统进 float（64 位双精度）。**53 位以上（约 9×10^15）的整数会丢精度**：

```gdscript
# ❌ 错误：把大整数直接存 JSON
var big_id := 9007199254740993            # 2^53 + 1
var json := JSON.stringify({"player_id": big_id})
var back = JSON.parse_string(json)
print(back["player_id"])                   # → 9007199254740992.0   ——差了 1！而且类型是 float
```

**后果**：用大整数做唯一 ID（比如服务器 uid、道具实例 id）的存档，读回后"对不上号"——这种 bug 隐蔽到令人发指。

**修正**（按场景三选一）：

```gdscript
# ① 大整数存成字符串（通用、可读，最推荐）
JSON.stringify({"player_id": str(big_id)})
# 读回：str(...).to_int()

# ② 明知是小范围数字，读回时立即转 int 并检查
var n := int(data["hp"])     # 小数值安全；若可能很大，改用 ①

# ③ 需要保真所有类型 → 放弃 JSON，用二进制 store_var/get_var（见 28.2.6）
```

**防御性检查模板**（读档后统一走这一道）：

```gdscript
func to_int_safe(v: Variant, fallback: int = 0) -> int:
	match typeof(v):
		TYPE_FLOAT:
			var f := float(v)
			if f != floor(f) or absf(f) > 9007199254740991.0:
				return fallback    # 超出安全整数范围或不是整数：拒绝并兜底
			return int(f)
		TYPE_STRING:
			return String(v).to_int() if String(v).is_valid_int() else fallback
		TYPE_INT:
			return v
		_:
			return fallback
```

### 28.8.2 坑二：路径大小写

```gdscript
# ❌ 陷阱：开发在 Windows 上，怎么写都能跑
load("res://Maps/Forest.TSCN")     # Windows 不区分大小写 → 编辑器里"没问题"
# 导出 PCK 后（PCK 内资源查找是区分大小写的）→ 资源加载失败，黑屏/报错找不到资源
```

**后果**：又一款"在我机器上是好的"——且往往到了测试同学或玩家的机器上才炸。

**修正**：团队约定统一命名风格（推荐 `snake_case` 全小写 + 全小写扩展名），并在 code review 时留意路径拼写；IDE 的重命名功能会同步改引用，尽量用而不是手动改文件名。

### 28.8.3 坑三：忘记 flush/close 丢数据

```gdscript
# ❌ 错误：写日志不收尾
func log_bad(msg: String) -> void:
	var f := FileAccess.open("user://log.txt", FileAccess.APPEND)
	f.store_line(msg)
	# 既不 flush 也不 close，函数也还没返回……
	# → 程序此刻崩溃/断电 → 磁盘上可能只有半行甚至空文件
```

**修正**：三种正确姿势任选其一——

```gdscript
# ① 作用域自动关闭（推荐，见 28.2.5）
func log_good(msg: String) -> void:
	var f := FileAccess.open("user://log.txt", FileAccess.APPEND)
	f.store_line(msg)
	# 函数返回时自动关闭并刷盘

# ② 关键写入后立刻 flush
f.store_line(msg)
f.flush()          # "这条日志我必须保证写上了"

# ③ 长流程持文件：写完记得显式 close()
```

### 28.8.4 坑四：往 res:// 写文件在导出版必失败

完整版已在 28.1.3 讲过，这里把判断标准固化成一张表：

| 想写的内容 | 正确路径 |
| --- | --- |
| 玩家存档 | `user://` |
| 游戏设置 | `user://` |
| 运行日志 | `user://` |
| 截图（`get_viewport().get_texture().get_image().save_png()`） | `user://screenshots/` |
| 随游戏发行的资源 | `res://`（仅作为**输入**读取，永远别写） |

另外提醒：编辑器里 `res://` 能写，导致这类 bug **无法在开发阶段暴露**。可以养成习惯：**凡是代码往磁盘写东西，路径一律以 `user://` 开头**，就没有例外可踩。

### 28.8.5 坑五：存档被玩家改（校验和简单防篡改）

单机游戏存档就是玩家电脑上的文本文件，`记事本`一打开 `gold: 250` 改成 `gold: 999999`。简单有效的防御是**校验和 + 盐**（SaveManager 里已在用，这里解释原理）：

```gdscript
## 保存时：对存档内容 + 私钥 一起做 sha256，把结果一起写进文件
func _make_checksum(body: Dictionary) -> String:
	return (JSON.stringify(body) + SECRET).sha256()

## 读取时：用同样算法重算一遍，对比文件里存的校验和
func is_tampered(wrapper: Dictionary) -> bool:
	var body: Dictionary = wrapper.get("body", {})
	return _make_checksum(body) != wrapper.get("checksum", "")
	# → 不一致：内容被改过（或损坏）→ 拒绝加载 / 回滚备份
```

**原理**：玩家只改数字不改校验和 → 重算对不上 → 被识破；想让校验和也"对上"，就必须知道你的私钥 SECRET。

**诚实的边界**：客户端的一切都可被逆向——把导出的游戏解开、在二进制里翻出 SECRET 并不算难。这套方案能挡住 99% 手痒改存档的休闲玩家，**挡不住有技术的修改者**。真正严肃的经济系统（排行榜、内购、联机数据）必须以服务器为准，客户端只做"体验层"的防篡改。单机游戏用这一招 + 损坏回滚，已经足够体面。

### 28.8.6 陷阱速查表

| 症状 | 大概率是 | 立即检查 |
| --- | --- | --- |
| 大整数 ID 对不上 | 坑一 | 存档里是不是把大整数直接存了 number？改字符串 |
| 导出后资源加载失败 | 坑二 | 路径大小写是否与磁盘实际一致 |
| 崩溃后存档是空的/半截 | 坑三 | 写完是否 flush/close |
| 编辑器正常、导出后存不了档 | 坑四 | 写入路径是否以 `user://` 开头 |
| 玩家金币"莫名其妙"变成天文数字 | 坑五 | 校验和是否生效；核心数据是否上了服务端 |

## 本章小结

- 运行期一切写盘都走 `user://`，**`res://` 在导出后只读**——这是本章最重要的一条纪律；
- `user://` 在各平台映射不同（Windows 在 %APPDATA%，Linux 在 ~/.local/share 等），可用 `OS.get_user_data_dir()` 打开实际位置；
- `FileAccess.open` 失败返回 **null 不抛异常**，每次都要防御式检查，配合 `FileAccess.get_open_error()` + `error_string()` 输出原因；
- 五种打开模式最易混的是：`WRITE` 清空重写、`APPEND` 末尾续写、`READ_WRITE` 不清空；
- `flush()` 立刻落盘、`close()` 关闭并落盘；Godot 4 的引用计数让"局部变量出作用域自动关文件"成为推荐的 with 风格写法；
- 二进制读写 `store_32/get_32/store_var/get_var` **必须按写入顺序读回**；`get_var` 不要开启允许对象反序列化的开关；
- `JSON.stringify(data, "\t")` 带缩进供人阅读；`JSON.parse_string` 失败返回 null，**必须判空**；
- JSON 类型映射三坑：**整数读回变 float（大整数丢精度）**、**字典键只能是字符串**、**Vector2 等引擎类型必须手动拆字段/装回**；
- 存档结构采用"信封+信纸"：`checksum` 校验和包住 `body`，body 里放 `version + timestamp + data`——**version 从第一天就要写**；
- 版本迁移黄金法则：**只加不删、迁移幂等、缺字段补默认值**；
- 损坏三重保险：主档读不到→读备份→备份也坏→新档开局；每次保存前先把旧档复制为 `.bak`；
- 设置文件优先用 `ConfigFile` 而不是 JSON：section 分组、`get_value` 原生默认值、**不丢引擎类型、整数不变 float**、玩家手改容错好；
- `DirAccess` 三板斧：`make_dir_recursive_absolute` 建目录、`copy_absolute/remove_absolute` 拷贝删除、`list_dir_begin/get_next/list_dir_end` 遍历（记得过滤 `.` 和 `..`）；
- 校验和防篡改 = `sha256(内容 + 私钥)`：挡得住休闲玩家，挡不住专业逆向；严肃数据以服务器为准。

---
# 第 29 章：错误处理与调试技巧

> 写代码的人分成两类：一类遇到红色的报错就慌，一类把报错当成"引擎在免费给你指路"。本章的目标，就是把你从前者变成后者。我们要做四件事：**认清错误分几层**、**学会逐词翻译报错**、**掌握打印与断点两套调试手段**、**建立防御性编程与自定义日志的工程习惯**。学完之后，你将拥有一个"报错词典"，并能把它当成工具书反复查阅。

## 29.1 错误的三层分类

### 29.1.1 为什么先分类：不同层，排查方法完全不同

很多新手卡住，不是因为报错太难，而是**用错了排查方法**。比如脚本根本打不开（解析错误），你却在那里打 `print` 调试——当然什么都打不出来。所以我们先建立一张"分类地图"：

| 层级 | 名字 | 典型表现 | 出现时机 | 排查主战场 |
| --- | --- | --- | --- | --- |
| 第一层 | 解析 / 编译期错误 | 脚本打不开、编辑器标红、无法运行 | 保存 / 加载脚本时 | 代码编辑器 + 报错行定位 |
| 第二层 | 运行时错误 | 游戏报错、崩溃、功能中断 | 运行时某一帧 | 输出面板 + 断点 + 调用栈 |
| 第三层 | 逻辑错误 | 不报任何错，但结果不对 | 运行时持续存在 | 断点 + 打印 + 场景树观察 |

记住一句口诀：**一层看编辑器，二层看输出栈，三层靠对比观察。**

### 29.1.2 第一层：解析 / 编译期错误

**特点**：`GDScript` 是"先解析后执行"的语言。当你保存脚本时，引擎会先把它**整体解析成可执行的形式**，一旦发现有语法问题（少括号、缩进乱、写错的符号），整个脚本直接判定为"无法加载"。你甚至会看到场景里的节点后面跟一个小红叉。

**为什么打不开脚本时不要 `print`**：因为脚本根本没进入运行状态，`print` 无从执行。

**排查思路**：
1. 看编辑器底部 / 输出面板给出的**文件名 + 行号**。
2. 报错行不一定就是"根源行"，它常常是"引擎终于看不懂的那一行"——所以**往上多看 2~3 行**。
3. 重点关注缩进（空格 vs Tab）、括号配对、运算符拼写、字符串引号是否闭合。

```gdscript
# ❌ 解析错误：缩进用了 Tab 与空格混排，编辑器直接拒绝加载
func _ready() -> void:
	print("A")
	print("B")   # → 假如此行用了 Tab 而上一行用了 4 个空格，报 "Parse Error: Used space character for indentation instead of tab"
```

### 29.1.3 第二层：运行时错误

**特点**：脚本能加载、能跑，但在某一帧执行到某个语句时炸了。典型如：访问 `null` 的属性、调用不存在的函数、数组越界。这类错误**会打印到输出面板，并且带调用栈**。

**排查思路**：
1. 读报错原文（本章 29.2 教你逐词翻译）。
2. 顺着 **调用栈（Call Stack）** 找到"最先出事"的那一行，而不是最后一行。
3. 用断点 + 监视面板看当时的变量值（29.4）。

```gdscript
# ❌ 运行时错误：player 是 null 时访问 .name
func _ready() -> void:
	var player: Node = null
	print(player.name)   # → 报 "Invalid access to property or key 'name' on a base object of type 'null instance'"
```

### 29.1.4 第三层：逻辑错误

**特点**：**最难的一类**。引擎一声不响，游戏照跑，但"结果不是你要的"。比如：伤害算成了 0、敌人永远追不上玩家、金币加减法反了、坐标偏移 1 像素。

**排查思路**：
1. 先**明确期望值**（我认为这里应该输出 100），再**观察实际值**（输出却是 0）。
2. 在关键路径打 `print_debug`（带走行号），或直接断点。
3. 用**二分法**：把可疑逻辑砍成两半，看错误出现在哪一半，逐步缩小范围。
4. 善用场景树 Remote（29.5）看运行时的真实属性值。

### 29.1.5 三层对照速查

| 你想知道的问题 | 对应层 | 用什么工具 |
| --- | --- | --- |
| 为什么脚本打不开？ | 解析期 | 编辑器报错行 + 缩进检查 |
| 为什么一运行就报红字？ | 运行时 | 输出面板原文 + 调用栈 |
| 为什么不报错但结果不对？ | 逻辑 | 断点 + 打印 + Remote 面板 |
| 为什么每次结果还不一样？ | 逻辑（时序） | 断点 + 条件断点 + 日志时间戳 |

## 29.2 学会读报错

### 29.2.1 一条完整错误信息的结构

Godot 的报错文本看起来很长，其实结构固定，拆开就四块：

```
E 0:00:01.234   res://player/player.gd:18 @ _physics_process():
  Invalid get index 'hp' (on base: 'null instance').
  <C++ Error>    Condition "_p_target" is true.
  <Stack Trace>  player.gd:18 @ _physics_process()
                 scene_main.gd:42 @ _on_timer_timeout()
```

| 片段 | 含义 | 怎么用 |
| --- | --- | --- |
| `E 0:00:01.234` | 错误级别 + 发生时刻（时:分:秒.毫秒） | 定位"第几秒出的事"，配合录像/日志复现 |
| `res://player/player.gd:18` | 脚本路径 + 行号 | 直接双击/点击跳转 |
| `@ _physics_process()` | 出错时正在执行的函数名 | 确认是哪个回调里出的问题 |
| `Invalid get index 'hp' ...` | 错误描述（人话翻译见下） | 核心信息 |
| `<Stack Trace>` | 调用栈：谁调用了谁 | **从上往下**找第一处你的代码 |

### 29.2.2 报错翻译一：Invalid get index 'hp' (on base: 'null instance')

逐词翻译：

| 词 | 含义 |
| --- | --- |
| `Invalid` | 非法的、不允许的 |
| `get index` | 取下标 / 取键（`a.b` 或 `a[b]` 都算） |
| `'hp'` | 你要取的键名 |
| `on base:` | 在什么"底座对象"上取 |
| `'null instance'` | 底座是空对象（`null`） |

**合起来**：你在一个空对象上取 `hp`，引擎说"这对象都没有，哪来的 hp"。

**最小复现**：

```gdscript
extends Node

var enemy: Node = null

func _ready() -> void:
	print(enemy.hp)   # → Invalid get index 'hp' (on base: 'null instance')
```

**修复**：给对象赋值，或加防护：

```gdscript
func _ready() -> void:
	if enemy != null:
		print(enemy.hp)
	# 或
	if is_instance_valid(enemy):
		print(enemy.get("hp"))
```

### 29.2.3 报错翻译二：Invalid call. Expected 2 arguments.

逐词翻译：

| 词 | 含义 |
| --- | --- |
| `Invalid call` | 非法调用 |
| `Expected` | 期望（引擎要求的） |
| `2 arguments` | 2 个参数 |

**合起来**：你调用某个函数，但它要求 2 个参数，你给的数量不对（可能 0 个、1 个或多于 2 个）。

**最小复现**：

```gdscript
extends Node

func add(a: int, b: int) -> int:
	return a + b

func _ready() -> void:
	add(1)   # → Invalid call. Expected 2 arguments.
```

**修复**：补全参数 `add(1, 2)`；或给参数设默认值 `func add(a: int, b: int = 0) -> int`。

### 29.2.4 报错翻译三：Attempt to call function 'take_damage' in base 'null instance'

逐词翻译：

| 词 | 含义 |
| --- | --- |
| `Attempt to call function` | 试图调用函数 |
| `'take_damage'` | 你想调用的函数名 |
| `in base` | 在哪个对象上调用 |
| `'null instance'` | 空对象 |

**合起来**：你对着一个空对象调用了 `take_damage()`。

**最小复现**：

```gdscript
extends Node

var target: Node = null

func _ready() -> void:
	target.take_damage(10)   # → Attempt to call function 'take_damage' in base 'null instance'
```

**修复**：确认 `target` 已赋值且未被 `queue_free`。常见根源是"节点已释放但引用还在"，见 29.7。

### 29.2.5 读报错的通用四步法

1. **定位行号**：报错里第一个 `res://` 行号最重要。
2. **翻译描述**：把英文逐词拆开（本章 29.6 有词典）。
3. **看调用栈**：谁触发了这个函数？是不是时序问题（还没 `_ready` 就被调用）？
4. **构造最小复现**：把这段逻辑单独复制到一个空场景跑一遍，复制不出来说明和别人有关。

## 29.3 打印全家桶对比表

### 29.3.1 为什么打印也分"全家桶"

新手只知道 `print`，其实 Godot 提供了一整套不同用途的输出函数。**选对函数，能省掉一半调试时间**。核心差异有三点：是否带位置信息（文件/行号）、是否带符号链接（可点击跳转）、是否在 release 版保留。

### 29.3.2 回忆一下 print 与 print_rich

```gdscript
extends Node

func _ready() -> void:
	print("普通输出")                                   # → 普通输出
	print_rich("[color=red]红字[/color] [b]加粗[/b]")    # → 输出面板里显示彩色、加粗文本
	print_rich("[url=res://player.gd]点击跳转脚本[/url]") # → 可点击的链接
```

### 29.3.3 print_verbose：只在"详细模式"下出现

```gdscript
extends Node

func _ready() -> void:
	print_verbose("这条只有开启 verbose 时才显示")
	# → 在项目设置里开启 Debug > Settings > Verbose Stdout，或编辑器高级输出时才会打印
```

**用途**：写库/插件的开发者用，普通运行时默认静默，避免刷屏。

### 29.3.4 print_debug：自带文件与行号（强烈推荐）

```gdscript
extends Node

func _ready() -> void:
	var hp := 0
	print_debug("当前 hp =", hp)
	# → player.gd:5 @ _ready(): 当前 hp = 0
```

**为什么推荐**：它自动附上"文件:行号 @ 函数名"，你一眼就知道是哪一行打的，不用手动写 `"第 5 行"`。

### 29.3.5 printerr 与 push_error / push_warning / push_script_error

```gdscript
extends Node

func _ready() -> void:
	printerr("这是写到标准错误流的文本")        # → 输出到 stderr，一般显示为红色
	push_warning("这是一条警告")                # → 输出面板黄色警告，带调用位置
	push_error("这是一条错误")                  # → 输出面板红色错误，带调用位置
	push_script_error("脚本级错误")             # → 以引擎错误格式抛出，会进调用栈
```

| 函数 | 输出级别 | 带位置信息 | 会中断执行吗 | 典型用途 |
| --- | --- | --- | --- | --- |
| `print` | 普通 | 否 | 否 | 临时看变量 |
| `print_rich` | 普通（富文本） | 否 | 否 | 彩色/可点击输出 |
| `print_verbose` | 详细 | 否 | 否 | 库作者的可选日志 |
| `print_debug` | 普通 + 位置 | **是** | 否 | 最常用的调试打印 |
| `printerr` | 错误流 | 否 | 否 | 需要写到 stderr 时 |
| `push_warning` | 警告 | **是** | 否 | 不合预期但可继续 |
| `push_error` | 错误 | **是** | 否 | 明确错误但想继续跑 |
| `push_script_error` | 错误（引擎格式） | **是** | 否 | 需要完整调用栈 |

### 29.3.6 release 版行为差异（重要）

| 行为 | debug 版 | release 版 |
| --- | --- | --- |
| `print` / `printerr` | 输出 | 输出（但控制台通常看不到） |
| `print_debug` | 输出（带位置） | 输出（位置信息可能被剥离） |
| `print_verbose` | 视开关 | 通常静默 |
| `assert` | **生效** | **被整体剥离**（见 29.8） |
| `push_error` / `push_warning` | 进输出面板 | 一般不再显示 |
| 断点调试 | 可用 | **不可用** |

**结论**：不要依赖 `assert` 或 `push_error` 做正式的游戏逻辑判断，它们只是"开发期的脚手架"。

## 29.4 断点调试（超详细步骤）

### 29.4.1 为什么需要断点：print 的天花板

`print` 只能告诉你"某一刻的值"，却没法：
- 暂停整个游戏，让你慢慢看；
- 查看那一刻**所有**变量的值；
- 一步步执行，观察每一步的变化；
- 改一个值再继续。

断点可以。**断点 = 让引擎在某一行停下来，把控制权交给你。**

### 29.4.2 操作步骤（文字版图文）

1. **打开脚本**：在编辑器里双击要调试的 `.gd` 文件，让它进入脚本编辑器。
2. **找到行号槽（gutter）**：代码左侧那条灰色窄栏就是 gutter。
3. **点红点**：在 gutter 上单击目标行，会出现一个**红点**，表示这里打了断点。再次单击可取消。
4. **运行游戏**：按 `F5` 运行项目。当执行流到达断点行时，游戏会**暂停**，编辑器切到"调试"布局。
5. **看四个关键面板**（见 29.4.3）。
6. **单步执行**：用下方工具栏的按钮一步步走。
7. **继续运行**：点"继续（Resume）"或按 `F12`，游戏恢复，直到下一个断点。

### 29.4.3 断点暂停后，屏幕上有四个面板要看

| 面板 | 位置 | 作用 |
| --- | --- | --- |
| 堆栈（Stack Frames） | 左侧 | 显示"谁调用了谁"，从当前函数一路往上 |
| 变量/监视（Variables / Watch） | 中左 | 当前作用域内所有变量、成员变量的值 |
| 场景树（Scene / Remote） | 右侧 | 运行时节点树（见 29.5） |
| 编辑器主区 | 中央 | 高亮当前执行到的那一行 |

### 29.4.4 单步按钮含义

| 按钮 | 名称 | 行为 | 什么时候用 |
| --- | --- | --- | --- |
| ▶ | 继续 Resume | 继续运行到下一个断点 | 确认这一处没问题了 |
| ⤵ | 单步跳过 Step Over | 执行当前行，**不进入**遇到的函数内部 | 快速走过一行（不想看函数内部） |
| ⤓ | 单步进入 Step Into | 执行当前行，**进入**遇到的函数内部 | 想钻进某函数看细节 |
| ⤴ | 单步跳出 Step Out | 把当前函数**一次跑完**，回到调用它的地方 | 函数内部已看清，想出去 |
| ⏹ | 停止 | 终止调试会话 | 结束 |

**记忆技巧**：Over 是"跳过去"，Into 是"钻进去"，Out 是"退出来"。

### 29.4.5 实战例：用断点查"伤害为什么是 0"

```gdscript
extends Node

var attack := 10
var defense := 10

func calculate_damage() -> int:
	var damage := attack - defense          # ← 在这里打断点
	if damage < 0:
		damage = 0
	return damage

func _ready() -> void:
	print("最终伤害：", calculate_damage())  # 期望 5，实际 0
```

在 `var damage := attack - defense` 这一行打断点，运行后暂停，看 `attack = 10`、`defense = 10`——原来牌面上两者相等，减法自然是 0。**这就是逻辑错误的破案方式：不看不知道，一看就明白。**

### 29.4.6 条件断点：只在满足条件时暂停

有时你只想在"第 100 帧"或"hp 为负"时停下。做法：

1. **右键断点**（或右键 gutter 上的红点），弹出菜单。
2. 选择 **Edit Breakpoint（编辑断点）**。
3. 在表达式框里填入条件，例如 `hp <= 0` 或 `frame_count > 100`。
4. 确定后，红点通常带一个小标记，表示"条件断点"。

```gdscript
extends Node

var hp := 100
var frame_count := 0

func _process(_delta: float) -> void:
	frame_count += 1
	hp -= 1
	# 在下一行打断点，条件写 hp == 0
	print("hp =", hp)   # → 只在 hp 归零的那一刻暂停，其余帧不打断
```

**用途**：循环里第 500 次才出的 bug、偶发 bug、性能问题定位。

### 29.4.7 右键断点的其他编辑项

| 菜单项 | 作用 |
| --- | --- |
| Edit Breakpoint | 设条件、启用/禁用 |
| Disable Breakpoint | 暂时关闭（保留红点但不起作用） |
| Remove Breakpoint | 彻底删除 |
| Remove All Breakpoints | 清空全部断点 |

**提示**：调试完记得清空断点，否则下次运行时还会莫名其妙停下来。

## 29.5 Remote 场景树

### 29.5.1 什么是 Remote 场景树

运行游戏时，编辑器侧边栏会出现 **Remote** 标签（和 Local/本地对应）。它展示的是**当前正在运行的游戏里的真实节点树**。Local 是"编辑器里没运行的设计树"，Remote 是"运行时活着的树"。

| 面板 | 内容 | 什么时候看 |
| --- | --- | --- |
| Local | 编辑器中的设计节点树 | 编辑时 |
| Remote | 游戏运行中的节点树、实时属性 | 调试时 |

### 29.5.2 实时查看节点树与搜索节点

1. 运行游戏（`F5`）。
2. 切到 **Remote** 标签。
3. 用面板顶部的**搜索栏**输入节点名，可快速定位（例如搜 `Player`）。
4. 点选某节点，右侧 **Inspector** 会显示它**当前那一刻的真实属性值**——不是设计值，是运行时值。

**典型用途**：确认"我 `get_node` 的路径到底对不对"——在 Remote 里眼睛看一遍路径，比猜强一百倍。

### 29.5.3 实战例：确认节点是否被正确添加到树里

```gdscript
extends Node

func _ready() -> void:
	var bullet := Node2D.new()
	bullet.name = "Bullet"
	# 忘记 add_child 的话……
	# add_child(bullet)
	# → 打开 Remote 面板，发现树里根本没有 Bullet，立刻明白错在哪
```

### 29.5.4 陷阱：Remote 里节点还在，但功能没了

如果节点被 `queue_free` 后（下一帧才真正删除），你短暂还能在 Remote 看到它，但脚本已失效——这会造成"明明在树里却报 null"的困惑。记住：**`queue_free` 是延迟删除**，见 29.7.6。

## 29.6 常见报错词典（16 条）

> 用法：遇到红字，先用 Ctrl+F 在本表里搜关键词，找到"为什么会发生"和"修复方法"。每条格式固定：**报错原文 → 为什么 → 最小复现 → 修复**。

### 29.6.1 Invalid get index 'xxx' (on base: 'null instance')

- **为什么**：在一个 `null` 对象上取属性或键。
- **最小复现**：`var n: Node = null; print(n.hp)`
- **修复**：先判空（`if n != null`）或 `is_instance_valid(n)`；本质是对象没赋值 / 已释放。

### 29.6.2 Attempt to call function 'xxx' in base 'null instance'

- **为什么**：对着 `null` 调函数。
- **最小复现**：`var n: Node = null; n.take_damage(1)`
- **修复**：判空 + 检查 `get_node` 路径是否写对；节点可能还没进树。

### 29.6.3 Invalid call. Expected 2 arguments.

- **为什么**：函数定义要 2 个参数，调用时给错数量。
- **最小复现**：`func f(a, b): pass` 后调 `f(1)`
- **修复**：补齐参数，或给参数加默认值。

### 29.6.4 Cyclic reference（循环引用）

- **为什么**：两个脚本用 `class_name` 互相引用对方类型，解析陷入死循环。
- **最小复现**：`a.gd` 里 `var b: B`，`b.gd` 里 `var a: A`，且都 `class_name`。
- **修复**：把一方改成弱引用（用 `Node` 而非具体类），或用 `@warning_ignore` / 延迟到运行时解析（`load()` 字符串）。

### 29.6.5 Parse error: indentation（缩进错误）

- **为什么**：Tab 与空格混用，或缩进层级不对。
- **最小复现**：同一代码块里一行空格、一行 Tab。
- **修复**：编辑器设置里开启"缩进仅用空格"或统一 Tab，`Ctrl+Shift+F` 格式化（需插件）或手动统一。

### 29.6.6 Variable 'x' is already declared in this scope

- **为什么**：同一作用域内重复声明同名变量。
- **最小复现**：`var x := 1` 后隔几行又 `var x := 2`。
- **修复**：删掉一个，或改名；赋值时直接写 `x = 2`（不加 `var`）。

### 29.6.7 Trying to assign value of type 'String' to a variable of type 'int'

- **为什么**：类型不匹配赋值。
- **最小复现**：`var n: int = "abc"`
- **修复**：转换类型 `int("123")`，或修正变量类型标注。

### 29.6.8 Invalid operands 'String' and 'int' in operator '+'

- **为什么**：不同类型做运算。
- **最小复现**：`"abc" + 1`
- **修复**：`"abc" + str(1)`。

### 29.6.9 The function 'xxx()' isn't declared in the current class

- **为什么**：调用了当前类里不存在的函数（拼写错 / 没继承到 / 未定义）。
- **最小复现**：`func _ready(): take_dmg(1)` 但定义的是 `take_damage`。
- **修复**：核对拼写；确认 `extends` 是否正确；确认函数确实在本类或父类里。

### 29.6.10 Node not found: "xxx"

- **为什么**：`get_node("路径")` 找不到该节点，通常路径写错或节点还没进树。
- **最小复现**：`get_node("Player/Sprite")` 但实际层级是 `Player/Body/Sprite`。
- **修复**：在 Remote 面板核对路径；或改用 `@onready` + `$` 并检查是否同名多节点。

### 29.6.11 Attempt to call function on a previously freed instance

- **为什么**：对象已被释放（`free`/`queue_free`），你还在调它。
- **最小复现**：`n.queue_free()` 后隔帧 `n.do_something()`。
- **修复**：用 `is_instance_valid(n)` 判断后再调；或用信号通知"已销毁"。

### 29.6.12 Nonexistent function 'new()' in base '...'

- **为什么**：把普通脚本当类来 `new()`，但脚本没 `extends RefCounted`/`Node`，或漏了 `class_name`。
- **最小复现**：`MyThing.new()` 但 `MyThing` 未声明为可实例化的类。
- **修复**：加上 `class_name`，并确认它 `extends` 一个可实例化的基类。

### 29.6.13 Cannot instantiate abstract class 'xxx'

- **为什么**：对 `abstract` 类调用 `.new()`。
- **最小复现**：对 `class_name Base extends Node` 且 `@abstract` 的类调 `.new()`。
- **修复**：实例化具体的子类，而不是抽象基类。

### 29.6.14 Signal 'xxx' is connected to nonexistent method

- **为什么**：连接信号时指定的方法不存在（改名 / 删了 / 拼错）。
- **最小复现**：`btn.pressed.connect(_on_click)` 但已把 `_on_click` 改名。
- **修复**：删除连接后重连；或在编辑器里移除失效连接。

### 29.6.15 A class member cannot have the same name as its enclosing class

- **为什么**：成员变量/函数名和类名相同，冲突。
- **最小复现**：`class_name Player` 后又写 `var Player := 1`。
- **修复**：给成员改名，避免与 `class_name` 同名。

### 29.6.16 Invalid access to property or key 'xxx' on a base object of type 'Nil'

- **为什么**：与 29.6.1 同类，另一种格式的"空对象取属性"。
- **最小复现**：`var d: Dictionary = null; print(d["k"])`
- **修复**：初始化字典 `:= {}`，或判空后访问。

## 29.7 防御性编程工具箱

### 29.7.1 什么是防御性编程

**核心思想**：不要假设"对象一定存在""节点一定在树里""方法一定存在"。在动手之前先问一句"它还好吗？"——用几个内置函数做安全检查，让程序不轻易崩。这不等于到处写 `if`，而是**在边界处做检查**（用户输入、跨节点调用、延迟逻辑）。

### 29.7.2 is_instance_valid：对象还活着吗

```gdscript
extends Node

var target: Node = null

func _ready() -> void:
	# 陷阱例：target 可能已被 queue_free，此时用 != null 判断并不可靠
	if is_instance_valid(target):
		target.call("die")
	else:
		print_debug("target 已失效，跳过")   # → 安全兜底
```

**关键点**：`queue_free()` 之后到真正删除之间，引用**仍不是 `null`**，但 `is_instance_valid()` 会立刻返回 `false`。所以**判断"对象是否可用"要用 `is_instance_valid`，而不是 `!= null`**。

### 29.7.3 is_inside_tree：节点在树里吗

```gdscript
extends Node2D

func do_effect() -> void:
	# 陷阱：还没 add_child 就调用，会报 "Condition is_inside_tree() is false"
	if is_inside_tree():
		queue_redraw()
```

**典型场景**：`_init()` 里访问 `get_tree()` 会失败，因为那时还没进树。

### 29.7.4 has_method / is_in_group

```gdscript
extends Node

func try_hit(body: Node) -> void:
	# 实战例：只有对方实现了 take_damage 才调用，避免 "isn't declared" 报错
	if body.has_method("take_damage"):
		body.take_damage(10)

func check_group(node: Node) -> void:
	# → 判断节点是否属于某个分组（常用于"是不是敌人"）
	if node.is_in_group("enemies"):
		print_debug("这是一个敌人")
```

### 29.7.5 get 函数返回 null 的安全链（and 短路）

```gdscript
extends Node

var data: Dictionary = {}

func _ready() -> void:
	# 坏写法：链式取值，中间一层 null 就炸
	# print(data["user"]["name"])
	# 好写法：用 get 提供默认值
	var user: Dictionary = data.get("user", {})
	print(user.get("name", "匿名"))   # → 匿名（缺键也不崩）
```

短路技巧：

```gdscript
extends Node

var player: Node = null

func try_attack() -> void:
	# and 短路：player 为 null 时，后面的 .is_inside_tree() 根本不会执行
	if player != null and player.is_inside_tree():
		print("可以攻击")
```

**原理**：`and` 左边为假，右边**不执行**，天然防崩。

### 29.7.6 @onready 时机

```gdscript
extends Node

@onready var label: Label = $Label   # → 在节点进入树、_ready 之前那一刻赋值

func _ready() -> void:
	label.text = "就绪"   # → 安全：@onready 已保证此时 label 有值
```

**为什么**：如果在成员变量声明处直接 `var label := $Label`，那时节点还没进树，`$Label` 会为 `null`。`@onready` 把赋值推迟到进树后，避免了"时机错误"。

### 29.7.7 free vs queue_free 详解

| 对比项 | `free()` | `queue_free()` |
| --- | --- | --- |
| 执行时机 | **立即**删除 | 本帧结束后（延迟）删除 |
| 能否在信号回调/`_process` 里安全用 | **危险**，可能崩 | 安全 |
| 正在执行该对象自身代码时调用 | 直接崩溃 | 安全 |
| 性能 | 立即释放 | 分散到帧末 |
| 推荐度 | 极少用 | **强烈推荐** |

```gdscript
extends Node

func bad_remove() -> void:
	$Enemy.free()   # ❌ 如果当前正在执行 Enemy 的某个方法，直接崩

func good_remove() -> void:
	$Enemy.queue_free()   # ✅ 安全：等当前逻辑跑完、帧末再删
```

**为什么推荐 `queue_free`**：因为它把"删除"推迟到**所有当前代码执行完**之后，不会在对象还在执行自己代码时把它从脚下抽走。几乎所有"freed instance"报错，都和 `free()` 或在对象自己的回调里删除自己有关。

### 29.7.8 防御性编程速查

| 场景 | 该用的检查 |
| --- | --- |
| 对象可能被释放 | `is_instance_valid(obj)` |
| 节点可能在树外 | `is_inside_tree()` |
| 对方可能有/没有某方法 | `has_method("x")` |
| 判断阵营 | `is_in_group("enemies")` |
| 字典/对象可能缺键 | `.get(key, 默认值)` |
| 空引用链式调用 | `a != null and a.b` 短路 |
| 成员节点引用 | `@onready` |
| 删除节点 | `queue_free()` |

## 29.8 assert 断言

### 29.8.1 什么是断言

`assert(条件)` 表示"我**断言**这个条件一定成立"。如果成立，什么也不发生；如果不成立，就**中断执行并报错**。它用于捕捉"绝对不该发生"的编程失误。

```gdscript
extends Node

func set_hp(value: int) -> void:
	assert(value >= 0, "血量不能为负")   # → 开发期自检
	hp = value
```

### 29.8.2 release 版被剥离（重要）

**`assert` 只在 debug 版生效**。导出 release 版时，引擎会**把 `assert` 整个删掉**。这意味着：

| 行为 | debug 版 | release 版 |
| --- | --- | --- |
| `assert(false)` | 中断 + 报错 | 完全无事发生 |
| 性能开销 | 有（求值） | 零（被删） |

**结论**：`assert` 是"开发期的安全网"，**不能用来做正式的逻辑判断**。如果某条件在正式运行时也必须成立，请写成 `if not 条件: push_error(...)` 或真正的业务处理。

### 29.8.3 好断言 vs 坏断言

```gdscript
extends Node

var inventory: Array = []

# ✅ 好断言：检查"程序员自己的错误"，条件应永远为真
func pop_item() -> void:
	assert(inventory.size() > 0, "理论上不该空着弹物品，说明调用方逻辑有误")
	inventory.pop_back()

# ❌ 坏断言：把玩家输入这种"正常可能发生"的情况当断言
func use_gold(amount: int) -> void:
	assert(amount > 0, "金额必须为正")   # ❌ 玩家真的可能传 0，release 版不检查就漏了
	gold -= amount
```

**好坏判别标准**：断言用于"不可能发生、发生即 bug"的问题；对于"业务上可能发生"的情况，用正常的 `if` + 返回值/错误处理。

## 29.9 自定义日志系统模板

### 29.9.1 为什么要自建日志

`print` 打的日志没有级别、没有时间、没有来源，出问题时像一团乱麻。一个统一的 `Log` 类可以让你：按级别过滤、带时间戳、带调用类名、彩色输出、可选写文件。下面是完整可抄模板。

### 29.9.2 完整模板

```gdscript
# log.gd —— 全局日志工具，建议放在 res://autoload/ 下并注册为 Autoload（名称为 Log）
class_name Log
extends RefCounted

# ============ 日志级别定义 ============
enum Level {
	DEBUG,   # 调试：只在开发期关心
	INFO,    # 信息：正常运行轨迹
	WARN,    # 警告：不合预期但能继续
	ERROR,   # 错误：功能可能已受损
}

# ============ 全局配置（可在运行时修改）============
static var min_level: Level = Level.DEBUG   # 低于此级别的日志不输出
static var to_file: bool = false             # 是否同时写入文件
static var file_path: String = "user://game.log"
static var use_color: bool = true            # 是否使用彩色输出

# 各级别对应的颜色（BBCode）
const _COLORS := {
	Level.DEBUG: "gray",
	Level.INFO: "cyan",
	Level.WARN: "yellow",
	Level.ERROR: "red",
}
const _TAGS := {
	Level.DEBUG: "DEBUG",
	Level.INFO: "INFO ",
	Level.WARN: "WARN ",
	Level.ERROR: "ERROR",
}

# ============ 内部：生成一行日志文本 ============
static func _format(level: Level, msg: String, caller_class: String) -> String:
	var t := Time.get_time_dict_from_system()
	# → 形如 [2026-10-03 14:05:09]
	var stamp := "[%04d-%02d-%02d %02d:%02d:%02d]" % [
		t.year, t.month, t.day, t.hour, t.minute, t.second
	]
	return "%s [%s] [%s] %s" % [stamp, _TAGS[level], caller_class, msg]

# ============ 内部：输出 + 落盘 ============
static func _emit(level: Level, line: String) -> void:
	if use_color:
		print_rich("[color=%s]%s[/color]" % [_COLORS[level], line])
	else:
		print(line)
	if to_file:
		_append_file(line)

static func _append_file(line: String) -> void:
	var f := FileAccess.open(file_path, FileAccess.READ_WRITE)
	if f == null:
		f = FileAccess.open(file_path, FileAccess.WRITE)
	if f == null:
		push_error("Log: 无法打开日志文件 " + file_path)
		return
	f.seek_end()
	f.store_line(line)
	f.close()

# ============ 对外：四个级别 ============
static func debug(msg: String, caller: String = "") -> void:
	if Level.DEBUG < min_level:
		return
	_emit(Level.DEBUG, _format(Level.DEBUG, msg, caller))

static func info(msg: String, caller: String = "") -> void:
	if Level.INFO < min_level:
		return
	_emit(Level.INFO, _format(Level.INFO, msg, caller))

static func warn(msg: String, caller: String = "") -> void:
	if Level.WARN < min_level:
		return
	_emit(Level.WARN, _format(Level.WARN, msg, caller))

static func error(msg: String, caller: String = "") -> void:
	if Level.ERROR < min_level:
		return
	_emit(Level.ERROR, _format(Level.ERROR, msg, caller))
	# 同时推到引擎，方便在编辑器里看到
	push_error("[%s] %s" % [caller, msg])
```

### 29.9.3 使用示例

```gdscript
extends Node

func _ready() -> void:
	Log.info("游戏启动", "Main")
	Log.debug("玩家初始位置 = %s" % global_position, "Main")
	Log.warn("存档文件缺失，将新建存档", "SaveSystem")
	Log.error("资源加载失败：%s" % "res://miss.tscn", "ResourceLoader")

	# → [2026-10-03 14:05:09] [INFO ] [Main] 游戏启动
	# → [2026-10-03 14:05:09] [WARN ] [SaveSystem] 存档文件缺失，将新建存档
```

### 29.9.4 进阶用法

```gdscript
extends Node

func _ready() -> void:
	# 发布前收紧日志：只留 WARN 以上
	Log.min_level = Log.Level.WARN
	# 打开落盘
	Log.to_file = true
	Log.info("这条因级别被过滤，不会输出", "Main")   # → 无输出
	Log.error("这条会输出并写文件", "Main")          # → 输出 + 写入 user://game.log
```

### 29.9.5 陷阱例：print 与 Log 混用导致顺序混乱

同一个逻辑里一会儿 `print`、一会儿 `Log.error`，一个不带时间戳一个带，阅读时很难对齐。**约定**：项目里统一用 `Log`，只在临时调试时用 `print_debug`，调试完删掉。

## 29.10 本章小结

- **错误分三层**：解析/编译期（脚本打不开）、运行时（报红字崩溃）、逻辑（不报错但结果错），三者排查方法完全不同。
- **解析错误看编辑器**：重点是缩进、括号、拼写，报错行往往不是根源行，往上多看几行。
- **运行时错误看输出面板和调用栈**，从调用栈"从上往下"找第一处自己的代码。
- **逻辑错误最难**：先明确期望值，再用打印/断点/Remote 做对比观察，用二分法缩小范围。
- **读报错四步**：定位行号 → 逐词翻译 → 看调用栈 → 构造最小复现。
- **打印全家桶各司其职**：`print_debug` 带位置最常用，`push_error/push_warning` 带位置且分级，`print_verbose` 只在详细模式输出。
- **release 版差异关键**：`assert` 被整体剥离，`push_*` 一般不再显示，断点不可用——不要依赖它们做正式逻辑。
- **断点是 print 的升级版**：能暂停、查看所有变量、单步执行、条件触发。
- **单步口诀**：Over 跳过去、Into 钻进去、Out 退出来。
- **条件断点**用于偶发 bug 与循环深处的 bug（右键 gutter 红点编辑）。
- **Remote 场景树**让你看到运行时真实的节点结构和属性值，是核对节点路径的利器。
- **报错词典要背关键词**：null instance、Expected N arguments、freed instance、Node not found 是绝对高频。
- **防御性检查**：`is_instance_valid`、`is_inside_tree`、`has_method`、`is_in_group`、`.get(key, 默认)`、`and` 短路。
- **`queue_free` 优先于 `free`**：延迟删除避免"删掉正在执行自己的对象"。
- **`@onready` 解决"时机错误"**：成员节点引用应推迟到进树后赋值。
- **`assert` 是开发期自检**：用于"绝不该发生"的 bug，release 版消失，不可当业务判断。
- **自建 `Log` 类**：级别 + 时间戳 + 类名 + 可选落盘 + 彩色，是工程化的第一步。

---

# 第 30 章：性能优化意识

> 性能问题常常很"反直觉"：你以为慢的是渲染，其实是脚本；你以为 `visible = false` 就省了，其实没有。本章不教你"魔法调优"，而是建立一套**性能思维**——先测量、再定位、后优化。你会拿到一张"每帧成本"清单、一个压轴的对象池模板，以及一张 20 组的坏/好写法对照表。

## 30.1 性能思维第一课：先测量再优化

### 30.1.1 不要凭感觉优化

新手最常见的错误是"还没测就优化"：听说对象池快，于是给处处都用上，结果代码复杂了、性能没啥变化，甚至更慢。**性能优化的第一原则：先测量，再定位，最后优化。**

优化口头禅：**"先让它跑对，再让它跑快；不要猜，要测。"**

### 30.1.2 游戏性能的两个指标

| 指标 | 含义 | 单位 | 越大/越小越好 |
| --- | --- | --- | --- |
| FPS | 每秒渲染帧数 | 帧/秒 | 越**大**越好 |
| 单帧耗时 | 渲染一帧花了多少时间 | 毫秒 ms | 越**小**越好 |

二者互为倒数：`单帧耗时(ms) ≈ 1000 / FPS`。

| 目标 FPS | 单帧预算 |
| --- | --- |
| 60 FPS | 16.6 ms |
| 120 FPS | 8.3 ms |
| 30 FPS | 33.3 ms |

**换算口诀**：
- **60 FPS ≈ 16.6 ms/帧**，即"你每一帧只有 16.6 毫秒的时间预算"。
- **120 FPS ≈ 8.3 ms/帧**，翻倍帧率 = 预算减半。

**为什么记 ms 比记 FPS 有用**：因为你的代码耗时是"叠加"的。脚本 5ms + 物理 4ms + 渲染 6ms = 15ms，刚好卡在 60FPS 边缘；任何一处多 2ms 就掉帧。**用毫秒思考，才知道该砍哪里。**

### 30.1.3 实战例：自制帧率读数

```gdscript
extends Label

func _process(_delta: float) -> void:
	# → 直接读引擎统计的 FPS（也是性能监视器显示的值）
	text = "FPS: %d" % Engine.get_frames_per_second()
```

### 30.1.4 陷阱例：用计数器"手算"FPS

```gdscript
extends Node

var frames := 0
var elapsed := 0.0
var fps := 0.0

func _process(delta: float) -> void:
	frames += 1
	elapsed += delta
	if elapsed >= 1.0:
		fps = frames / elapsed   # → 只在整秒更新，数值跳动、不精确
		frames = 0
		elapsed = 0.0
```

**问题**：一秒才刷新一次，且没有考虑帧耗时波动的实时性。**修正**：优先用 `Engine.get_frames_per_second()`，或用滑动平均。手算仅用于学习原理。

## 30.2 Godot 性能去哪了：CPU vs GPU

### 30.2.1 两大阵营

| 阵营 | 负责 | 典型瓶颈 |
| --- | --- | --- |
| CPU | 脚本逻辑、物理、节点管理、AI、路径查找 | `_process`/`_physics_process` 里干了重活 |
| GPU | 绘制画面（顶点、纹理、着色） | 绘制调用太多、填充率过高、特效过重 |

**关键分辨方法**：打开性能监视器（30.9），看 **FPS** 掉的同时 **CPU 时间** 是否也涨。
- 如果是 CPU 涨 → 脚本/物理问题，优化代码。
- 如果 CPU 空闲但 FPS 低 → GPU / 绘制瓶颈，减少绘制调用或特效。

### 30.2.2 常见瓶颈判断表

| 症状 | 可能瓶颈 | 优先排查 |
| --- | --- | --- |
| 节点一多就卡，脚本里干很多事 | CPU（脚本） | `_process` 里的查找、`load`、大循环 |
| 大量子弹/粒子时卡 | CPU（节点管理）或 GPU（绘制） | 对象池 + 批量绘制 |
| 角色脚本一多就掉帧 | CPU（脚本） | 每帧轮询、`get_parent` 调用 |
| 画面复杂时卡，逻辑很简单 | GPU（绘制） | 绘制调用、Shader、分辨率 |
| 物理碰撞体一多就卡 | CPU（物理） | 碰撞层裁剪、用 Area2D 代替遍历 |
| 加载卡顿（不是运行卡） | I/O | 预加载、异步加载 |

### 30.2.3 入门例：区分"逻辑卡"还是"渲染卡"

```gdscript
extends Node

func _ready() -> void:
	print("当前 FPS：", Engine.get_frames_per_second())
	# 在性能监视器里同时观察：
	# → Time > Process：脚本耗时（毫秒）
	# → Raster > Draw Calls：绘制调用次数
	# 哪个高就优化哪个
```

## 30.3 每帧成本意识

### 30.3.1 核心原则：`_process` 是黄金地皮

`_process` 和 `_physics_process` **每帧都会执行**。60FPS 下它们一秒被调用 60 次；100 个节点就是 6000 次/秒。所以里面**每一行代码的成本都被放大 60 倍**。原则：**能在初始化做一次的，绝不放到每帧里。**

### 30.3.2 `_process` 里绝对不要做的事

| 禁止项 | 为什么慢 | 替代方案 |
| --- | --- | --- |
| `load("res://...")` | 同步读盘 + 解析，可能几十毫秒 | `preload()` 或 `_ready` 里加载缓存 |
| `get_node("路径")` 每帧 | 每次都要遍历节点树查找 | `@onready` 缓存到成员变量 |
| 频繁字符串拼接 | String 不可变，每次都新建 | 缓存或用 `StringName`/数组 |
| `new()` 大对象 / `instantiate()` | 分配内存、构造场景开销大 | 预生成 + 对象池（30.4） |
| `find_child` / `get_children` 循环 | 遍历整棵树 | 初始化时建索引/缓存引用 |
| 复杂数学每帧重算 | 浪费 CPU | 缓存结果、增量更新 |
| 大量 `print` | I/O 与字符串格式化开销 | 用日志级别控制或删掉 |

### 30.3.3 对照示例：坏写法 vs 好写法

**坏写法**：

```gdscript
extends Node2D

func _process(_delta: float) -> void:
	# ❌ 每帧都从节点树里重新查找 player
	var player := get_node("/root/Main/Player")
	# ❌ 每帧加载资源（极慢）
	var bullet_scene := load("res://bullet.tscn")
	# ❌ 每帧拼接字符串
	var t := "hp:" + str(player.hp) + " mp:" + str(player.mp)
	$Label.text = t
```

**好写法**：

```gdscript
extends Node2D

# ✅ 引用在初始化时缓存
@onready var player: Node = get_node("/root/Main/Player")
@onready var label: Label = $Label
# ✅ 资源在加载时预加载一次
const BULLET_SCENE := preload("res://bullet.tscn")

func _process(_delta: float) -> void:
	# ✅ 只做必要的更新，字符串用格式化一次性构造
	label.text = "hp:%d mp:%d" % [player.hp, player.mp]
```

**差距说明**：坏写法每帧三次 `get_node`/`load`/字符串拼接，好写法每帧只有一次属性赋值。节点一多，差距是**数量级**的。

### 30.3.4 陷阱例：`_ready` 缓存了引用，但对象被换掉了

```gdscript
extends Node

var cached: Node = null

func _ready() -> void:
	cached = get_node("/root/Main/Enemy")

func _process(_delta: float) -> void:
	# 陷阱：Enemy 被 queue_free 后重建，cached 已失效
	if is_instance_valid(cached):
		cached.tick()
```

**结论**：缓存要配合 `is_instance_valid` 检查，对象重建时记得更新缓存。

## 30.4 对象池模式（压轴模板）

### 30.4.1 为什么需要对象池

射击游戏每帧发射子弹，如果每颗都 `instantiate()` 再 `queue_free()`，等于每秒创建/销毁几十上百个节点。**创建与销毁是昂贵操作**（分配内存、初始化、加入树、触发通知）。对象池的思想是：**预先造好一批，用时"取出"，不用时"归还"，循环使用，永不真正销毁。**

| 对比项 | 每帧 new + free | 对象池 |
| --- | --- | --- |
| 对象创建开销 | 每次都有 | **只在预生成时付一次** |
| GC/内存抖动 | 频繁分配释放 | 稳定 |
| 峰值卡顿 | 大批生成时卡顿 | 平滑 |
| 代码复杂度 | 简单 | 略高 |
| 适用场景 | 低频对象（血包） | 高频对象（子弹、粒子、伤害飘字） |

### 30.4.2 完整模板：BulletPool

```gdscript
# bullet_pool.gd —— 通用对象池（以子弹为例），预生成 + 取用 + 归还 + 自动扩容
class_name BulletPool
extends Node

# 预生成数量与硬上限
@export var initial_size: int = 32
@export var max_size: int = 512

# 要池化的场景（子弹）
@export var bullet_scene: PackedScene

# 容器：所有子弹都挂在这个 Node2D 下，方便统一管理
@onready var container: Node2D = $Container

var _available: Array[Node] = []   # 空闲队列（可复用）
var _in_use: int = 0               # 使用中的数量

func _ready() -> void:
	# 预生成：一口气造好 initial_size 个，全部隐藏、休眠
	for i in initial_size:
		var b := bullet_scene.instantiate()
		b.visible = false
		b.process_mode = Node.PROCESS_MODE_DISABLED   # 不跑 _process，零成本
		container.add_child(b)
		_available.append(b)

# 取用：从池里拿一个，池空则自动扩容
func acquire() -> Node:
	var bullet: Node
	if _available.is_empty():
		if _in_use >= max_size:
			push_warning("BulletPool: 已达上限 %d，无法再取" % max_size)
			return null
		# 自动扩容：池空就再造一个
		bullet = bullet_scene.instantiate()
		container.add_child(bullet)
	else:
		bullet = _available.pop_back()
	# 激活
	bullet.visible = true
	bullet.process_mode = Node.PROCESS_MODE_INHERIT
	_in_use += 1
	return bullet

# 归还：隐藏、休眠，放回空闲队列
func release(bullet: Node) -> void:
	if not is_instance_valid(bullet):
		return
	bullet.visible = false
	bullet.process_mode = Node.PROCESS_MODE_DISABLED
	bullet.global_position = Vector2.ZERO
	_available.append(bullet)
	_in_use -= 1
```

### 30.4.3 调用示例

```gdscript
extends Node2D

@onready var pool: BulletPool = $BulletPool

func _fire(direction: Vector2) -> void:
	var bullet := pool.acquire()
	if bullet == null:
		return
	bullet.global_position = global_position
	bullet.setup(direction)   # 假设子弹脚本有一个 setup 方法

# 子弹脚本内部：命中或超时后归还自己
# extends Area2D
# var pool: BulletPool
# func _on_lifetime_timeout() -> void:
#     pool.release(self)
```

### 30.4.4 陷阱例：归还后状态没重置

```gdscript
# ❌ 归还时忘记重置速度/计时器，下次取出还带着上次的"残影"
func release(bullet: Node) -> void:
	bullet.visible = false
	_available.append(bullet)   # ❌ 没有重置位置、速度、计时器

# ✅ 正确：归还时彻底复位
func release_fixed(bullet: Node) -> void:
	bullet.visible = false
	bullet.process_mode = Node.PROCESS_MODE_DISABLED
	bullet.global_position = Vector2.ZERO
	bullet.velocity = Vector2.ZERO   # 复位速度
	bullet.reset_lifetime()          # 复位计时器
	_available.append(bullet)
```

**教训**：对象池最大的坑是"脏状态"。归还时必须把对象恢复成出厂状态。

### 30.4.5 性能差异说明

假设一次战斗发射 500 颗子弹：
- **new + free**：500 次 `instantiate` + 500 次 `queue_free`，每次都有内存分配/回收、场景实例化、进树通知，容易在开火密集时掉帧。
- **对象池**：`_ready` 时一次性造 32 个，之后 500 次只是"切换可见性和 process_mode"，几乎零分配，帧率平稳。

## 30.5 字符串与容器的性能细节

### 30.5.1 String 是不可变的

GDScript 的 `String` **一旦创建就不能修改**。每次"修改"实际上都是**新建一个字符串**。所以在循环里用 `+=` 拼接，会产生大量中间字符串。

```gdscript
extends Node

func bad() -> void:
	var s := ""
	for i in 1000:
		s += str(i)   # ❌ 每次都新建字符串，1000 次分配，O(n²) 级开销
	print(s.length())

func good() -> void:
	var parts := PackedStringArray()   # ✅ 用数组收集，最后一次性拼接
	for i in 1000:
		parts.append(str(i))
	var s := "".join(parts)            # 一次拼接完成
	print(s.length())
```

| 写法 | 复杂度 | 说明 |
| --- | --- | --- |
| 循环 `s += x` | 近似 O(n²) | 每次都复制整串 |
| `PackedStringArray` + `join` | O(n) | 只复制一次 |

### 30.5.2 PackedStringArray 与 Packed 数组

`PackedStringArray` 是"紧凑字符串数组"，比普通 `Array` 更省内存、更快遍历，因为元素是连续存储的原始类型。

```gdscript
extends Node

func _ready() -> void:
	var arr := PackedStringArray(["a", "b", "c"])
	arr.append("d")                # ✅ 高效的追加
	print(arr.size())              # → 4
	print("".join(arr))            # → abcd

	var ints := PackedInt32Array([1, 2, 3])
	print(ints[0] + ints[1])       # → 3
```

### 30.5.3 数组 append 是"均摊 O(1)"

`Array.append()` 大多数时候是 O(1)，偶尔会触发"扩容并复制"（O(n)），但平均下来仍是均摊 O(1)。所以**正常追加不用担心**，只要别在循环里反复 `insert` 到头部（那是 O(n)）。

| 操作 | 复杂度 | 建议 |
| --- | --- | --- |
| `append` / `push_back` | 均摊 O(1) | 放心用 |
| `pop_back` | O(1) | 放心用 |
| `insert(0, x)` | O(n) | 避免在头部频繁插入 |
| `erase` 中间元素 | O(n) | 大量删除考虑换结构 |

### 30.5.4 字典键查找是 O(1)——善用索引

`Dictionary` 的键查找平均是 O(1)。当你需要"按名字快速找对象"时，用字典建索引，比每次遍历数组强得多。

```gdscript
extends Node

var _enemies_by_name: Dictionary = {}

func _ready() -> void:
	for enemy in get_children():
		_enemies_by_name[enemy.name] = enemy   # ✅ 初始化建索引

func get_enemy(n: String) -> Node:
	return _enemies_by_name.get(n)             # ✅ O(1) 查找

# ❌ 坏写法：每次遍历数组 O(n)
func get_enemy_slow(n: String) -> Node:
	for enemy in get_children():
		if enemy.name == n:
			return enemy
	return null
```

### 30.5.5 陷阱例：把字典当"有序列表"用

```gdscript
extends Node

func _ready() -> void:
	var d := {"b": 1, "a": 2, "c": 3}
	# 陷阱：字典不保证顺序，别靠它做"第几个"的逻辑
	for k in d:
		print(k)   # → 顺序不保证，不要依赖
```

## 30.6 信号 vs 每帧轮询

### 30.6.1 轮询的代价

"每帧主动去问"（轮询）看起来简单，但它**每帧都要执行**，哪怕根本没事发生。而"信号"只在**真正发生变化时**才触发一次——这叫**事件驱动**。

| 对比 | 每帧轮询 | 信号 |
| --- | --- | --- |
| 执行次数 | 每帧（60 次/秒） | 仅变化时 |
| 空闲开销 | 一直有 | 几乎为零 |
| 耦合度 | 需要知道对方层级 | 松耦合 |
| 可读性 | 逻辑分散 | 事件集中 |

### 30.6.2 改造示例：从轮询到信号

**坏写法（每帧问父节点）**：

```gdscript
extends Node

func _process(_delta: float) -> void:
	# ❌ 每帧向上找父节点、访问它的属性
	var game_state := get_parent().get_parent().get("game_state")
	if game_state == "paused":
		pause_anim()
	elif game_state == "playing":
		play_anim()
```

**好写法（信号驱动）**：

```gdscript
extends Node

signal state_changed(new_state: String)

var _current_state := ""

func set_state(new_state: String) -> void:
	if new_state == _current_state:
		return
	_current_state = new_state
	state_changed.emit(new_state)   # ✅ 只在真正变化时发一次

# 动画节点里连接信号，而不是每帧轮询
# func _ready() -> void:
#     game.state_changed.connect(_on_state_changed)
#
# func _on_state_changed(new_state: String) -> void:
#     if new_state == "paused":
#         pause_anim()
#     else:
#         play_anim()
```

### 30.6.3 实战例：血量变化通知

```gdscript
extends Node

signal hp_changed(new_hp: int)

var _hp := 100:
	set(value):
		if value == _hp:
			return
		_hp = value
		hp_changed.emit(_hp)   # ✅ 变化才发信号

func take_damage(dmg: int) -> void:
	_hp -= dmg   # → 自动触发 setter → 发信号
```

### 30.6.4 陷阱例：误以为信号是"免费"的

信号也有开销：连接、断开、发射都要遍历监听者。**信号也不能滥用到每帧发**（比如每帧 emit 一次坐标），那还不如直接赋值。原则：**变化频繁的用直接调用，变化稀疏的用信号。**

## 30.7 节点数量与绘制

### 30.7.1 节点越多越贵

每个节点都有开销：进树/出树通知、属性同步、`_process` 调用（如果启用）、渲染批次。**几百个节点还好，几千个就会明显掉帧**。

| 优化方向 | 做法 |
| --- | --- |
| 合并同类 | 用 `MultiMeshInstance2D` 批量渲染相同图元 |
| 拆分逻辑 | 把多个小节点的逻辑合并进一个大脚本 |
| 关闭不需要的处理 | `set_process(false)` / `set_physics_process(false)` |
| 可见性剔除 | 屏幕外的节点停掉逻辑与绘制 |

### 30.7.2 `visible = false` 不等于"零成本"

**反直觉的重点**：把一个节点 `visible = false`，只是**不绘制**它，但：
- 它的 `_process` / `_physics_process` **仍在执行**；
- 物理体、碰撞检测**可能仍在参与**；
- 它仍占据节点树位置。

**正确做法**：真正不需要时要同时关掉处理：

```gdscript
extends Node2D

func hide_and_sleep() -> void:
	visible = false
	set_process(false)            # ✅ 停掉每帧逻辑
	set_physics_process(false)    # ✅ 停掉物理逻辑

func wake_up() -> void:
	visible = true
	set_process(true)
	set_physics_process(true)
```

### 30.7.3 CanvasItem 的 set_process(false)

任何继承 `CanvasItem` / `Node` 的对象都有 `set_process()`、`set_physics_process()`、`set_process_input()` 等开关。**只在你需要时才让节点参与每帧循环**，是性价比极高的优化。

```gdscript
extends Node

func _ready() -> void:
	# 默认先关闭，等真正需要时再打开
	set_process(false)

func start_tracking() -> void:
	set_process(true)   # ✅ 需要时开

func stop_tracking() -> void:
	set_process(false)  # ✅ 不需要时关
```

### 30.7.4 可见性剔除

Godot 会做可见性剔除（视口外的 `CanvasItem` 不绘制），但**脚本逻辑不会自动停**。所以对于屏幕外的大批实体（远处敌人、粒子）：

```gdscript
extends Node2D

func _on_visible_on_screen_notifier_2d_screen_exited() -> void:
	# → 离开屏幕：关掉逻辑
	set_process(false)
	set_physics_process(false)

func _on_visible_on_screen_notifier_2d_screen_entered() -> void:
	# → 回到屏幕：恢复逻辑
	set_process(true)
	set_physics_process(true)
```

### 30.7.5 陷阱例：粒子系统常驻

```gdscript
extends GPUParticles2D

# ❌ 一直 emitting = true，即使看不见也在算
# ✅ 用完就停，或设 oneshot = true 自动结束
func _ready() -> void:
	emitting = false
	one_shot = true
```

## 30.8 物理检测优化

### 30.8.1 为什么不用"每帧 distance_to 遍历"

新手常写：每帧遍历所有敌人，算和玩家的 `distance_to`，判断是否在攻击范围。这在敌人多时是 **O(n) 每帧**，而且绕过了物理引擎的"空间分区"加速。

```gdscript
extends Node2D

# ❌ 坏写法：每帧遍历所有敌人算距离
func _process(_delta: float) -> void:
	for enemy in get_tree().get_nodes_in_group("enemies"):
		if global_position.distance_to(enemy.global_position) < 100.0:
			attack(enemy)
```

### 30.8.2 用 Area2D 交给物理引擎

**好写法**：给玩家挂一个 `Area2D`（圆形碰撞），引擎内部用空间划分快速筛选附近对象，你只处理"进入/离开"事件：

```gdscript
extends Area2D

func _ready() -> void:
	body_entered.connect(_on_body_entered)
	body_exited.connect(_on_body_exited)

func _on_body_entered(body: Node) -> void:
	# → 只有真正进入范围的敌人才会触发，无需每帧遍历
	if body.is_in_group("enemies"):
		attack(body)

func _on_body_exited(body: Node) -> void:
	if body.is_in_group("enemies"):
		stop_attack(body)
```

| 对比 | 每帧 distance_to | Area2D 信号 |
| --- | --- | --- |
| 复杂度 | O(n) 每帧 | 引擎内部加速 + 事件 |
| 精度控制 | 手动 | 碰撞形状精确定义 |
| 代码量 | 循环 | 两个回调 |
| 推荐度 | 小规模可用 | 中大规模推荐 |

### 30.8.3 碰撞层与掩码分组

`Collision Layer`（我在哪层）与 `Collision Mask`（我检测哪层）可以精确控制"谁和谁检测"，**避免无意义的碰撞计算**。

| 概念 | 含义 | 例子 |
| --- | --- | --- |
| Layer | 我自己属于哪一类 | 玩家=1，敌人=2，子弹=3 |
| Mask | 我要检测哪些类 | 子弹只检测敌人层，不检测其他子弹 |

```gdscript
extends Area2D

func _ready() -> void:
	# → 子弹：只在"敌人"层检测，不检测子弹自己，减少无效计算
	collision_layer = 0            # 子弹本身不属于任何层（不需要被检测）
	collision_mask = 1 << 1        # 只检测第 2 层（敌人）
```

**收益**：碰撞对数量大幅下降，物理 CPU 占用降低。

### 30.8.4 陷阱例：故意关掉了所有掩码导致检测失效

```gdscript
extends Area2D

func _ready() -> void:
	collision_mask = 0   # ❌ 掩码为 0 = 谁也不检测，body_entered 永不触发
```

**结论**：优化掩码时，要保证"该检测的层仍在掩码里"。

## 30.9 工具使用

### 30.9.1 性能监视器面板（Monitor）

运行游戏时，编辑器底部 **Debugger > Monitors** 面板会实时显示各项指标。常用项含义：

| 监视项 | 含义 | 关注点 |
| --- | --- | --- |
| FPS | 当前帧率 | 是否稳定在目标值 |
| Frame Time / Process | 一帧耗时 / 脚本处理耗时(ms) | 脚本是否过重 |
| Physics Process / Physics Time | 物理帧耗时(ms) | 物理是否过重 |
| Draw Calls (Raster) | 绘制调用次数 | GPU 瓶颈信号，越少越好 |
| Objects / Nodes | 节点与对象数量 | 是否异常膨胀 |
| Static Memory / Memory | 内存占用 | 是否泄漏 |
| Video Mem | 显存占用 | 纹理是否过大 |

**读法**：出现掉帧时，先看是 **Process 高**（脚本）、还是 **Physics 高**（物理）、还是 **Draw Calls 多 / Video Mem 高**（绘制），再对症下药。

### 30.9.2 远程 Profiler

在 **Debugger > Profiler** 标签里，可以看到按函数统计的耗时（谁最耗时、调用多少次）。用于精确定位"哪个函数是性能黑洞"。

用法要点：
1. 运行游戏后切到 Profiler。
2. 观察函数列表，按时间排序。
3. 找到占用最高的函数，回到代码优化它。

### 30.9.3 Performance 单例代码读数

```gdscript
extends Node

func _ready() -> void:
	# → 场景里实时读取的性能指标
	print("FPS: ", Performance.get_monitor(Performance.TIME_FPS))
	print("单帧物理耗时(秒): ", Performance.get_monitor(Performance.TIME_PHYSICS_PROCESS))
	print("绘制调用: ", Performance.get_monitor(Performance.RENDER_TOTAL_DRAW_CALLS_IN_FRAME))
	print("对象数: ", Performance.get_monitor(Performance.OBJECT_COUNT))
	print("节点数: ", Performance.get_monitor(Performance.OBJECT_NODE_COUNT))
```

### 30.9.4 自制 FPS 显示模板

```gdscript
# fps_display.gd —— 挂在 CanvasLayer 下的 Label 上，屏幕常驻显示帧率
class_name FPSDisplay
extends Label

@export var refresh_interval: float = 0.5   # 每 0.5 秒刷新一次，避免数字乱跳

var _timer := 0.0

func _ready() -> void:
	# 显示在最上层，且不受场景缩放影响
	set_anchors_preset(Control.PRESET_TOP_LEFT)
	position = Vector2(8, 8)
	z_index = 4096

func _process(delta: float) -> void:
	_timer += delta
	if _timer < refresh_interval:
		return
	_timer = 0.0
	var fps := Engine.get_frames_per_second()
	var frame_ms := 1000.0 / maxf(fps, 1.0)
	# → 例如 "FPS: 60  16.7 ms"
	text = "FPS: %d  %.1f ms" % [fps, frame_ms]
	# 低于 50 帧显示红色警示
	modulate = Color.RED if fps < 50 else Color.WHITE
```

## 30.10 坏写法 vs 好写法速查表（20 组）

| # | 场景 | 坏写法 | 好写法 | 为什么 |
| --- | --- | --- | --- | --- |
| 1 | 获取节点 | 每帧 `get_node("路径")` | `@onready` 缓存引用 | 查找是 O(树深)，缓存后 O(1) |
| 2 | 加载资源 | 每帧 `load()` | `preload()` 或 `_ready` 加载 | 读盘+解析每次几十毫秒 |
| 3 | 子弹生成 | 每帧 `instantiate()` | 对象池取用 | 创建/销毁昂贵，池化零分配 |
| 4 | 子弹销毁 | `free()` | `queue_free()` | `free` 可能删掉正在执行的对象 |
| 5 | 字符串拼接 | 循环 `s += x` | `PackedStringArray` + `join` | String 不可变，`+=` 近 O(n²) |
| 6 | 找敌人 | 每帧遍历数组比对名字 | 字典建索引 `dict[name]` | 字典查找 O(1) vs 遍历 O(n) |
| 7 | 状态变化通知 | 每帧轮询父节点属性 | 信号 `state_changed` | 轮询每帧执行，信号仅变化时 |
| 8 | 距离检测 | 每帧 `distance_to` 遍历 | `Area2D` 的 `body_entered` | 物理引擎有空间加速 |
| 9 | 碰撞裁剪 | 所有层都检测 | 精确设置 layer/mask | 减少无效碰撞对 |
| 10 | 隐藏对象 | 只设 `visible=false` | 同时 `set_process(false)` | 隐藏不阻止 `_process` 运行 |
| 11 | 屏幕外实体 | 一直跑逻辑 | 可见性通知进出开关 | 屏幕外不需计算 |
| 12 | 数组删除 | 循环 `remove_at` 头部 | 用 `pop_back` / 标记后清理 | 头部删除 O(n) |
| 13 | 大量小节点 | 每个单位一个节点 | 合并逻辑 / MultiMesh | 节点本身有固定开销 |
| 14 | 粒子效果 | 常驻 `emitting=true` | `one_shot` 或按需开关 | 常驻持续消耗 |
| 15 | 属性访问 | 每帧 `get_parent().a.b` | 缓存引用到变量 | 链式查找每帧重复 |
| 16 | 类型标注 | 全用 `Variant`（不标注） | 标注 `int`/`float`/类型 | 强类型可优化、更安全 |
| 17 | 临时对象 | 每帧 `new()` 小对象 | 复用成员变量 | 减少分配与 GC 压力 |
| 18 | 调试打印 | 正式版残留大量 `print` | `Log` 分级 + 发布收紧 | 打印有格式化与 I/O 开销 |
| 19 | 定时判断 | 每帧累加 `delta` 判超时 | `Timer` / `create_timer` | 引擎定时器更高效清晰 |
| 20 | 数据读取 | 每帧读大 Array 全量 | 增量更新 / 缓存结果 | 避免每帧全量重算 |

### 30.10.1 使用建议

不要一次全上。**先找出瓶颈（30.1/30.9），再对照本表挑 2~3 条针对性地改，然后重新测量验证**。盲目套用所有条目，只会让代码变复杂而收益不明。

## 30.11 本章小结

- **先测量再优化**：不要凭感觉，用性能监视器和 Profiler 找到真正的瓶颈。
- **两个核心指标**：FPS 与单帧耗时（ms），互为倒数；**60FPS ≈ 16.6ms，120FPS ≈ 8.3ms**。
- **CPU vs GPU**：CPU 管脚本/物理/逻辑，GPU 管绘制；看是 Process 高还是 Draw Calls 多来分辨。
- **`_process` 是黄金地皮**：`load`、`get_node`、字符串拼接、`new`、`find_*` 都不该出现在每帧里。
- **缓存优先**：成员节点引用用 `@onready` 缓存，资源用 `preload`。
- **对象池压轴**：预生成 + 取用 + 归还 + 自动扩容，解决高频对象的创建/销毁开销。
- **对象池最大坑是脏状态**：归还时必须彻底复位位置、速度、计时器。
- **String 不可变**：循环拼接用 `PackedStringArray` + `join`，避免 O(n²)。
- **容器选择**：`append` 均摊 O(1)、头部 `insert` O(n)、字典查找 O(1)（善用索引）。
- **信号优于轮询**：变化稀疏时用信号，变化频繁时用直接调用。
- **节点数量有成本**：合并同类、关闭多余处理、可见性剔除。
- **`visible = false` 不等于零成本**：还要 `set_process(false)` 才是真省。
- **物理检测交给引擎**：用 `Area2D` 信号代替每帧 `distance_to` 遍历。
- **碰撞层掩码分组**：精确的 layer/mask 能大幅减少碰撞对数量。
- **善用工具**：Monitors 看全局、Profiler 找热点、`Performance` 单例做代码读数。
- **自制 FPS 显示**是每个项目的标配，能让你随时看见性能变化。
- **20 组对照表是清单**：找到瓶颈后挑几条改，改完必须重新测量验证。
---

# 第五卷 · 模块模板库（26 个即插即用模板）

# 第 31 章：基础模板（数据与状态类）

> 从本章开始，我们进入**第五卷：模块模板库**。这一卷的写作方式和前面三十章完全不同。前三十章我们像老师带学生，一句一句拆解语法；而这一卷，我们像在逛**超市**——货架上摆着一个又一个"开箱即用的模块"，你缺什么就拿什么，直接复制粘贴到项目里就能跑。
>
> 本章是"货架"的第一排：**数据与状态类模板**。它们负责一个游戏最底层、最枯燥、也最不能出错的部分——血量、伤害、背包、属性、状态机、事件、存档。把这几块打磨好，你后面做任何类型的游戏都能反复复用。

## 31.1 模板使用说明

### 31.1.1 这一卷的模板长什么样

每一个模板，都严格遵循下面这套统一格式，方便你"快速识别、快速抄走"：

| 区块 | 作用 | 你需要关注什么 |
| --- | --- | --- |
| **用途** | 一句话说明它解决什么问题 | 判断自己是否真的需要它 |
| **依赖** | 它需要什么前置条件 | 有没有要设置的 Autoload、有没有要继承的 `class_name` |
| **文件位置建议** | 建议放在 `res://` 下的哪个目录 | 保持项目结构清爽 |
| **完整代码** | 可整段复制的 `gdscript` 代码 | 复制时注意缩进（Tab）别被编辑器改坏 |
| **使用方法** | 从"创建文件"到"跑起来"的步骤 | 按序号一步步做，不要跳步 |
| **可调参数说明** | 表格列出所有可调字段 | 想改行为先看这里 |
| **进阶改造提示** | 怎么把它变成"你自己的" | 想扩展时从这里找方向 |

### 31.1.2 复制模板的四个标准动作

**动作一：建文件、填代码。**
在 Godot 编辑器的文件系统面板里右键新建一个脚本文件（New Script），把语言选成 `GDScript`，然后把模板代码整段粘进去。**注意**：GDScript 用缩进表达层级，粘贴时务必确认缩进没有被浏览器或聊天软件替换成奇怪的字符。如果看到编辑器整段标红，第一件事就是**全选后统一用 Tab 重排缩进**。

**动作二：确认 `class_name` 是否重复。**
很多模板带 `class_name`，例如 `HealthComponent`。`class_name` 是**全局注册**的，全项目不能出现两个同名。如果你项目里已经有同名脚本，就把模板开头的 `class_name` 那行删掉，改用 `preload` 或 `@export` 引用。

**动作三：挂载到场景树。**
凡是写 `extends Node` 的组件，都要作为一个**子节点**挂到"宿主"（比如玩家、敌人）身上。右键宿主节点 → Add Child Node → 搜索 `Node` → 创建 → 把脚本拖到该节点上。**为什么是子节点而不是继承？** 因为子节点式组件（Component Pattern）可以**一个宿主挂多个组件**、可以**单独启停**、可以**跨宿主复用**，比继承更灵活。

**动作四：连线与调用。**
组件之间靠**信号（signal）**通信。宿主脚本里用 `@onready var hp := $Health` 拿到组件，`hp.died.connect(_on_died)` 接线。**记住 Godot 4 的写法**：`connect` 接收的是 `Callable`，所以是 `connect(_on_died)`，而不是 Godot 3 的 `connect("died", self, "_on_died")`。

### 31.1.3 改造模板的通用原则

- **先跑通，再改造**。先把原样代码跑起来，确认能用，再去动它。
- **改"数据"不改"结构"**。优先通过导出变量（`@export`）调整数值，而不是删代码。
- **信号只增不减**。你要加功能，优先"新增信号 + 新增方法"，而不是修改已有信号签名——否则所有接线处都会一起报错。
- **命名统一**。本卷统一用 `take_damage` / `heal` / `current_hp` 这类直观命名，你的扩展也请保持一致。

---

## 31.2 模板 T01：Health 血量组件

### 模板 T01：Health 血量组件

**用途**：给任意角色（玩家、敌人、可破坏物）挂上一个"能受伤、能回血、能死亡"的血量组件，并对外广播血量变化、受伤、死亡等信号。

**依赖**：无。纯 `Node` 组件，不需要任何 Autoload，也不需要前置 `class_name`。

**文件位置建议**：`res://components/health_component.gd`

#### 完整代码

```gdscript
# res://components/health_component.gd
# 血量组件：挂到角色身上作为子节点使用
class_name HealthComponent
extends Node

# ============ 信号 ============
## 当前血量发生变化（包括初始化、受伤、回血、死亡）
signal hp_changed(current_hp: float, max_hp: float)
## 受到伤害（amount 为实际扣的血；info 为附加信息，比如伤害来源、暴击标记）
signal damaged(amount: float, info: Dictionary)
## 恢复血量（amount 为实际回复量）
signal healed(amount: float)
## 死亡（只触发一次）
signal died()

# ============ 可调参数 ============
@export var max_hp: float = 100.0
## 受击后的无敌时间（秒）。设为 0 表示关闭无敌帧。
@export var invincible_time: float = 0.0
## 初始血量比例（1.0 表示满血出生）
@export_range(0.0, 1.0, 0.01) var start_hp_ratio: float = 1.0

# ============ 运行时状态 ============
var current_hp: float = 0.0
var is_invincible: bool = false

var _invincible_timer: float = 0.0
var _dead: bool = false

func _ready() -> void:
	# 为什么在 _ready 里初始化而不是直接赋默认值？
	# 因为导出变量可能在编辑器里被改过，_ready 时才能拿到最终值。
	current_hp = max_hp * clampf(start_hp_ratio, 0.0, 1.0)
	hp_changed.emit(current_hp, max_hp)

func _process(delta: float) -> void:
	# 无敌帧倒计时
	if _invincible_timer > 0.0:
		_invincible_timer = maxf(_invincible_timer - delta, 0.0)
		if is_equal_approx(_invincible_timer, 0.0):
			is_invincible = false

# ---------- 对外接口 ----------
## 受伤。返回实际造成的伤害（被无敌帧或已死亡挡掉时返回 0）
func take_damage(amount: float, info: Dictionary = {}) -> float:
	if _dead or is_invincible or amount <= 0.0:
		return 0.0
	var real_damage := minf(amount, current_hp)
	current_hp = maxf(current_hp - amount, 0.0)
	damaged.emit(real_damage, info)
	hp_changed.emit(current_hp, max_hp)
	if invincible_time > 0.0:
		is_invincible = true
		_invincible_timer = invincible_time
	if current_hp <= 0.0:
		_die()
	return real_damage

## 回血。返回实际回复量（满血时返回 0）
func heal(amount: float) -> float:
	if _dead or amount <= 0.0:
		return 0.0
	var before := current_hp
	current_hp = minf(current_hp + amount, max_hp)
	var real_heal := current_hp - before
	if real_heal > 0.0:
		healed.emit(real_heal)
		hp_changed.emit(current_hp, max_hp)
	return real_heal

## 直接击杀（无视无敌帧）
func kill() -> void:
	if _dead:
		return
	current_hp = 0.0
	hp_changed.emit(current_hp, max_hp)
	_die()

## 复活
func revive(ratio: float = 1.0) -> void:
	_dead = false
	is_invincible = false
	_invincible_timer = 0.0
	current_hp = clampf(max_hp * ratio, 0.0, max_hp)
	hp_changed.emit(current_hp, max_hp)

## 血量百分比（0.0 ~ 1.0），供血条 UI 使用
func get_hp_percent() -> float:
	if max_hp <= 0.0:
		return 0.0
	return current_hp / max_hp

func is_dead() -> bool:
	return _dead

func _die() -> void:
	if _dead:
		return
	_dead = true
	died.emit()
```

#### 使用方法

1. 把上面的文件保存为 `res://components/health_component.gd`。
2. 选中你的角色节点（比如 `Enemy`），右键 → **Add Child Node** → 搜索 `Node` → 创建，命名为 `Health`。
3. 把 `health_component.gd` 拖到这个 `Health` 节点上。
4. 在 Inspector 里调整 `max_hp`（血量）和 `invincible_time`（无敌帧秒数）。
5. 在宿主脚本里取出组件并接线：

```gdscript
extends CharacterBody2D

@onready var health: HealthComponent = $Health

func _ready() -> void:
	health.hp_changed.connect(_on_hp_changed)
	health.died.connect(_on_died)

func _on_hp_changed(current_hp: float, max_hp: float) -> void:
	# 例如驱动血条
	$HpBar.value = health.get_hp_percent() * 100.0

func _on_died() -> void:
	# 播放死亡动画、掉落物品、删除节点……
	queue_free()

# 被攻击时调用
func hurt(amount: float) -> void:
	health.take_damage(amount, {"source": "player", "element": "fire"})
```

6. 让"攻击者"拿到目标的 `HealthComponent` 并调用 `take_damage()`，就完成了一次伤害传递。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `max_hp` | float | 100.0 | 最大血量，同时决定满血值 |
| `invincible_time` | float | 0.0 | 受击后无敌时长（秒）；0 = 关闭无敌帧 |
| `start_hp_ratio` | float | 1.0 | 出生血量比例，1.0 为满血 |
| `current_hp` | float | 运行时 | 当前血量（只读建议） |
| `is_invincible` | bool | 运行时 | 当前是否处于无敌状态 |

#### 进阶改造提示

- **加护盾/护甲层**：在 `take_damage` 开头先扣护盾，护盾扣完再扣血；新增 `shield_changed` 信号。
- **加受击硬直**：在 `damaged` 信号里让动画状态机切换到 `Hurt` 状态，几帧后返回。
- **加伤害数字**：把 `damaged` 信号接到一个飘字节点，在 `info` 里带上伤害数值与是否暴击。
- **加血条组件联动**：单独写一个 `HealthBar` 组件，`_ready` 时自动查找兄弟 `Health` 并接线，实现"拖上去就生效"。
- **为什么不做成 `class_name` 继承 `CharacterBody2D`？** 因为这样敌人/玩家/箱子都能复用同一份血量逻辑，继承会把逻辑绑死在某一类节点上，得不偿失。

---

## 31.3 模板 T02：Damage 伤害计算器

### 模板 T02：Damage 伤害计算器

**用途**：把"伤害该怎么算"这件事从战斗代码里抽出来，用一份独立的数据类 `DamageInfo` 描述一次攻击，再由 `DamageCalculator` 统一结算暴击、抗性减免与穿透。

**依赖**：需要同目录下两个 `class_name`：`DamageInfo`（数据类）与 `DamageCalculator`（计算器）。

**文件位置建议**：`res://combat/damage_info.gd` 与 `res://combat/damage_calculator.gd`

#### 完整代码

先写数据类 `DamageInfo`——它描述"一次攻击长什么样"：

```gdscript
# res://combat/damage_info.gd
# 伤害信息数据类：描述"这一次攻击"的全部属性
class_name DamageInfo
extends Resource

# 基础伤害（未暴击、未减抗前的数值）
@export var base_damage: float = 10.0
# 暴击率 0.0 ~ 1.0
@export_range(0.0, 1.0, 0.01) var crit_chance: float = 0.0
# 暴击倍率（2.0 表示暴击造成双倍伤害）
@export var crit_multiplier: float = 2.0
# 伤害元素类型，用于查抗性表，如 "physical" / "fire" / "ice"
@export var element: String = "physical"
# 穿透：忽略目标抗性的比例，0.0 ~ 1.0
@export_range(0.0, 1.0, 0.01) var penetration: float = 0.0

## 复制一份，方便在传递过程中安全地修改而不影响原对象
## 为什么需要它？因为 Resource 默认是"引用共享"的，直接改会污染调用方的数据。
func clone() -> DamageInfo:
	var d := DamageInfo.new()
	d.base_damage = base_damage
	d.crit_chance = crit_chance
	d.crit_multiplier = crit_multiplier
	d.element = element
	d.penetration = penetration
	return d
```

再写计算器 `DamageCalculator`：

```gdscript
# res://combat/damage_calculator.gd
# 伤害计算器：无状态工具类，全部用静态方法调用
class_name DamageCalculator
extends RefCounted

## 结算一次伤害。
## resistances 形如 {"fire": 0.3, "physical": 0.0}，表示对应元素减伤比例。
## on_number 是可选的"伤害数字回调"，会在结算后把结果字典回传，方便做飘字。
static func calculate(
		info: DamageInfo,
		resistances: Dictionary = {},
		on_number: Callable = Callable()
) -> Dictionary:
	# 1) 暴击判定
	var is_crit := randf() < clampf(info.crit_chance, 0.0, 1.0)
	var raw := info.base_damage
	if is_crit:
		raw *= maxf(info.crit_multiplier, 1.0)

	# 2) 抗性减免（考虑穿透）
	var resist := clampf(float(resistances.get(info.element, 0.0)), 0.0, 1.0)
	# 穿透按比例抵消抗性：穿透 0.5 且抗性 0.4 → 有效抗性 0.2
	var effective_resist := clampf(resist * (1.0 - clampf(info.penetration, 0.0, 1.0)), 0.0, 1.0)
	var final_damage := raw * (1.0 - effective_resist)

	var result := {
		"damage": maxf(final_damage, 0.0),
		"is_crit": is_crit,
		"element": info.element,
		"resist": effective_resist,
	}

	# 3) 回调：把结果交给上层（比如生成伤害数字）
	if on_number.is_valid():
		on_number.call(result)

	return result
```

#### 使用方法

1. 把两个文件分别保存为 `res://combat/damage_info.gd` 和 `res://combat/damage_calculator.gd`。
2. 在攻击逻辑里构造 `DamageInfo`，调用 `DamageCalculator.calculate()`，再把结果喂给目标的 `HealthComponent`：

```gdscript
extends Node2D

func attack(target: Node2D) -> void:
	# 构造这一次攻击的属性
	var info := DamageInfo.new()
	info.base_damage = 25.0
	info.crit_chance = 0.2
	info.crit_multiplier = 2.0
	info.element = "fire"
	info.penetration = 0.3

	# 目标的抗性表（真实项目里通常存在 StatsComponent 中）
	var resistances := {"fire": 0.4, "physical": 0.0}

	# 结算，并传入伤害数字回调
	var result := DamageCalculator.calculate(info, resistances, _spawn_damage_number)

	# 把伤害打到目标血量上
	var hp := target.get_node_or_null("Health")
	if hp is HealthComponent:
		hp.take_damage(result.damage, {"crit": result.is_crit, "element": result.element})

func _spawn_damage_number(result: Dictionary) -> void:
	var text := str(int(result.damage))
	if result.is_crit:
		text += "!"   # 暴击加感叹号
	print("伤害数字：", text)
```

3. 若不需要伤害数字，直接省略第三个参数即可：`DamageCalculator.calculate(info, resistances)`。

#### 可调参数说明

| 参数（DamageInfo） | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `base_damage` | float | 10.0 | 未暴击前的基础伤害 |
| `crit_chance` | float | 0.0 | 暴击概率 0~1 |
| `crit_multiplier` | float | 2.0 | 暴击倍率 |
| `element` | String | "physical" | 元素名，用于查抗性表 |
| `penetration` | float | 0.0 | 忽略抗性的比例 0~1 |
| `resistances`（入参） | Dictionary | {} | 元素 → 减伤比例 |
| `on_number`（入参） | Callable | 空 | 可选伤害数字回调 |

#### 进阶改造提示

- **加"伤害浮动"**：在结算前对 `raw` 乘一个 `randf_range(0.95, 1.05)`，让同一把武器打出不同数字。
- **加"多段伤害"**：把 `DamageInfo` 放进数组，循环结算，适合做连击、持续灼烧。
- **加"防御力公式"**：把 `resistances` 扩展成"防御值 → 减伤曲线"，比如 `damage * 100 / (100 + defense)`。
- **为什么用 `Resource` 而不是普通类？** 因为 `Resource` 可以在 Inspector 里创建和编辑（右键新建资源），策划能直接配置武器伤害，不必改代码。
- **为什么计算器是无状态的静态类？** 因为它只做纯计算，不保存任何状态，天生线程安全、到处可调用。

---

## 31.4 模板 T03：Inventory 背包系统

### 模板 T03：Inventory 背包系统

**用途**：提供"定长格子 + 堆叠"的背包系统，支持增删物品、统计数量、交换与移动格子，并在物品变化或背包满时广播信号。

**依赖**：需要 `ItemStack`（单个格子的数据结构，`class_name`）与 `Inventory`（背包本体）。

**文件位置建议**：`res://systems/item_stack.gd` 与 `res://systems/inventory.gd`

#### 完整代码

先写格子数据结构 `ItemStack`：

```gdscript
# res://systems/item_stack.gd
# 一个格子里的物品堆叠数据
class_name ItemStack
extends Resource

@export var item_id: String = ""
@export var amount: int = 1
# 这一格最多能堆多少个
@export var max_stack: int = 99
# 附加数据（比如武器强化等级、耐久）
@export var extra: Dictionary = {}

func is_empty() -> bool:
	return item_id == "" or amount <= 0

func is_full() -> bool:
	return amount >= max_stack

## 复制一份堆叠数据
func clone() -> ItemStack:
	var s := ItemStack.new()
	s.item_id = item_id
	s.amount = amount
	s.max_stack = max_stack
	s.extra = extra.duplicate(true)
	return s
```

再写背包本体 `Inventory`：

```gdscript
# res://systems/inventory.gd
# 定长格子式背包（含堆叠合并逻辑）
class_name Inventory
extends Node

# ============ 信号 ============
## 成功放入物品
signal item_added(item_id: String, amount: int, slot_index: int)
## 成功取出物品
signal item_removed(item_id: String, amount: int, slot_index: int)
## 背包已满、有物品放不进去
signal inventory_full(item_id: String)
## 某个格子的内容发生了变化（供 UI 刷新单个格子）
signal slot_changed(slot_index: int)
## 背包整体发生变化（供 UI 整体刷新）
signal inventory_changed()

# ============ 可调参数 ============
## 格子总数
@export var capacity: int = 20
## 新物品默认最大堆叠数
@export var default_max_stack: int = 99

# ============ 运行时数据 ============
## 定长数组，空格子为 null。用独立数组而不是字典，是为了对应 UI 的格子索引。
var slots: Array[ItemStack] = []

func _ready() -> void:
	slots.resize(capacity)  # resize 会填充 null

# ---------- 对外接口 ----------
## 放入物品。返回"没能放进去"的剩余数量（0 表示全部放入成功）
func add_item(item_id: String, amount: int = 1, max_stack: int = -1) -> int:
	if amount <= 0:
		return 0
	if max_stack <= 0:
		max_stack = default_max_stack
	var remaining := amount

	# 第一步：优先堆叠到"同种且未满"的已有格子里
	# 为什么先堆叠？避免背包里出现一堆只放了 1 个的同名物品
	for i in slots.size():
		if remaining <= 0:
			break
		var stack := slots[i]
		if stack != null and stack.item_id == item_id and stack.amount < stack.max_stack:
			var space := stack.max_stack - stack.amount
			var put := mini(space, remaining)
			stack.amount += put
			remaining -= put
			item_added.emit(item_id, put, i)
			slot_changed.emit(i)

	# 第二步：再依次放入空格子
	for i in slots.size():
		if remaining <= 0:
			break
		if slots[i] == null:
			var put := mini(max_stack, remaining)
			var stack := ItemStack.new()
			stack.item_id = item_id
			stack.amount = put
			stack.max_stack = max_stack
			slots[i] = stack
			remaining -= put
			item_added.emit(item_id, put, i)
			slot_changed.emit(i)

	# 第三步：容器满则报警
	if remaining > 0:
		inventory_full.emit(item_id)
	else:
		inventory_changed.emit()
	return remaining

## 取出物品。数量不足时返回 false 且不做任何改动
func remove_item(item_id: String, amount: int = 1) -> bool:
	if amount <= 0:
		return true
	if count_item(item_id) < amount:
		return false
	var remaining := amount
	# 从后往前取，尽量保留前面的整齐堆叠
	for i in range(slots.size() - 1, -1, -1):
		if remaining <= 0:
			break
		var stack := slots[i]
		if stack != null and stack.item_id == item_id:
			var take := mini(stack.amount, remaining)
			stack.amount -= take
			remaining -= take
			item_removed.emit(item_id, take, i)
			if stack.amount <= 0:
				slots[i] = null   # 取空后格子置空
			slot_changed.emit(i)
	inventory_changed.emit()
	return true

## 统计某种物品的总数量
func count_item(item_id: String) -> int:
	var total := 0
	for stack in slots:
		if stack != null and stack.item_id == item_id:
			total += stack.amount
	return total

## 是否含有至少 amount 个某物品
func has_item(item_id: String, amount: int = 1) -> bool:
	return count_item(item_id) >= amount

## 交换两个格子（无条件对调，不考虑堆叠）
func swap(a: int, b: int) -> bool:
	if not _valid_index(a) or not _valid_index(b) or a == b:
		return false
	var tmp := slots[a]
	slots[a] = slots[b]
	slots[b] = tmp
	slot_changed.emit(a)
	slot_changed.emit(b)
	inventory_changed.emit()
	return true

## 把 from 格的物品移动到 to 格；同种物品会尝试合并，否则对调
func move_item(from_index: int, to_index: int) -> bool:
	if not _valid_index(from_index) or not _valid_index(to_index) or from_index == to_index:
		return false
	var from_stack := slots[from_index]
	if from_stack == null:
		return false
	var to_stack := slots[to_index]

	if to_stack == null:
		# 目标格子为空，直接搬过去
		slots[to_index] = from_stack
		slots[from_index] = null
	elif to_stack.item_id == from_stack.item_id and to_stack.amount < to_stack.max_stack:
		# 同种物品：合并到目标格子
		var space := to_stack.max_stack - to_stack.amount
		var put := mini(space, from_stack.amount)
		to_stack.amount += put
		from_stack.amount -= put
		if from_stack.amount <= 0:
			slots[from_index] = null
	else:
		# 不同物品：直接交换
		return swap(from_index, to_index)

	slot_changed.emit(from_index)
	slot_changed.emit(to_index)
	inventory_changed.emit()
	return true

## 返回某格内容（可能为 null）
func get_slot(index: int) -> ItemStack:
	if not _valid_index(index):
		return null
	return slots[index]

## 当前已占用的格子数
func used_slot_count() -> int:
	var n := 0
	for stack in slots:
		if stack != null:
			n += 1
	return n

## 是否完全没空位（注意：能堆叠到已有堆的情况不算"满"）
func is_full() -> bool:
	for stack in slots:
		if stack == null:
			return false
	return true

## 清空背包
func clear() -> void:
	for i in slots.size():
		slots[i] = null
		slot_changed.emit(i)
	inventory_changed.emit()

func _valid_index(i: int) -> bool:
	return i >= 0 and i < slots.size()
```

#### 使用方法

1. 保存两个文件到 `res://systems/`。
2. 在玩家节点下新建一个 `Node` 子节点，命名为 `Inventory`，挂上 `inventory.gd`。
3. 在 Inspector 里设置 `capacity`（格子数）。
4. 在玩家脚本里使用：

```gdscript
extends CharacterBody2D

@onready var inventory: Inventory = $Inventory

func _ready() -> void:
	inventory.item_added.connect(_on_item_added)
	inventory.inventory_full.connect(func(id: String): print("背包满了，放不下：", id))
	# 铺格子式的背包 UI 可以直接监听整体变化
	inventory.inventory_changed.connect(_refresh_ui)

func pick_up(item_id: String, amount: int = 1) -> void:
	var leftover := inventory.add_item(item_id, amount)
	if leftover > 0:
		print("有 ", leftover, " 个没捡起来")

func use_potion() -> void:
	# 消耗一个药水
	if inventory.remove_item("potion", 1):
		print("喝下药水")

func _on_item_added(item_id: String, amount: int, slot_index: int) -> void:
	print("放入", item_id, "x", amount, "到第", slot_index, "格")

func _refresh_ui() -> void:
	# 遍历 inventory.slots 刷新每个格子图标与数量
	for i in inventory.slots.size():
		print("格子", i, "：", inventory.slots[i])
```

5. **拖拽整理**：在 UI 里拖拽结束时调用 `inventory.move_item(from, to)`，相同物品会自动合并，不同物品会自动交换。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `capacity` | int | 20 | 背包格子总数 |
| `default_max_stack` | int | 99 | 新物品默认最大堆叠数 |
| `slots` | Array[ItemStack] | 运行时 | 定长格子数组，空格为 null |
| `max_stack`（ItemStack） | int | 99 | 单个物品的最大堆叠数 |
| `extra`（ItemStack） | Dictionary | {} | 物品附加数据 |

#### 进阶改造提示

- **加物品定义表**：新建一个 `ItemData` 资源（图标、名称、最大堆叠、类型），`add_item` 时按 `item_id` 查表拿 `max_stack`，就不用每次手填。
- **加重量上限**：维护一个 `total_weight`，`add_item` 前先算重量是否超限，超了就返回剩余数量。
- **加装备栏**：另开一组固定槽位（武器、头盔……），每个槽位只接受对应类型的物品。
- **为什么空槽用 `null` 而不是空 `ItemStack`？** 因为 `null` 判断最直接（`if slots[i] == null`），而"空对象"还要额外判断 `is_empty()`，容易漏判。
- **为什么堆叠要"先合并、后开新格"？** 这是背包手感的关键：合并能让玩家一眼看到"我有 37 个药水"，而不是散在三个格子里。

---

## 31.5 模板 T04：Stats 属性与 Buff 系统

### 模板 T04：Stats 属性与 Buff 系统

**用途**：用"基础值 + 加成列表 + 最终值"三层结构管理角色属性，支持加法、乘法、覆盖三种修饰，并支持"限时 Buff"到期自动移除。

**依赖**：无。

**文件位置建议**：`res://components/stats_component.gd`

#### 完整代码

```gdscript
# res://components/stats_component.gd
# 属性组件：基础值 + 修饰列表 → 最终值
class_name StatsComponent
extends Node

# ============ 信号 ============
## 某属性的最终值变化（stat_name 为属性名，final_value 为新值）
signal stat_changed(stat_name: String, final_value: float)
## 添加了一个修饰
signal modifier_added(stat_name: String, modifier: Dictionary)
## 移除了一个修饰
signal modifier_removed(stat_name: String, modifier: Dictionary)
## 一个限时 Buff 到期结束
signal buff_expired(stat_name: String, buff_id: String)

# ============ 可调参数 ============
## 基础属性表：属性名 → 基础数值
@export var base_stats: Dictionary = {
	"max_hp": 100.0,
	"attack": 10.0,
	"defense": 5.0,
	"move_speed": 200.0,
}

# ============ 运行时数据 ============
# 属性名 → 修饰数组，每个修饰为 {"type": "add"/"mul"/"override", "value": float, "id": String}
var _modifiers: Dictionary = {}
# 正在计时的限时修饰：[{"stat":..., "modifier":..., "remaining":...}, ...]
var _timed_buffs: Array = []

func _ready() -> void:
	# 初始化时广播一遍，方便 UI 取初始值
	for key in base_stats.keys():
		stat_changed.emit(key, get_stat(key))

func _process(delta: float) -> void:
	# 限时 Buff 倒计时，到期自动移除
	for i in range(_timed_buffs.size() - 1, -1, -1):
		var entry: Dictionary = _timed_buffs[i]
		entry["remaining"] -= delta
		if entry["remaining"] <= 0.0:
			var stat_name: String = entry["stat"]
			var buff_id: String = entry["modifier"]["id"]
			remove_modifier(stat_name, buff_id)
			buff_expired.emit(stat_name, buff_id)
			_timed_buffs.remove_at(i)

# ---------- 修饰管理 ----------
## 添加永久修饰。type 可为 "add"（加法）、"mul"（乘法）、"override"（覆盖）
func add_modifier(stat_name: String, value: float, type: String = "add", id: String = "") -> void:
	if id == "":
		id = "%s_%d" % [stat_name, Time.get_ticks_usec()]
	var mod := {"type": type, "value": value, "id": id}
	if not _modifiers.has(stat_name):
		_modifiers[stat_name] = []
	_modifiers[stat_name].append(mod)
	modifier_added.emit(stat_name, mod)
	stat_changed.emit(stat_name, get_stat(stat_name))

## 添加限时修饰；duration 秒后自动移除
func add_timed_modifier(
		stat_name: String, value: float, type: String,
		duration: float, id: String = ""
) -> void:
	if id == "":
		id = "buff_%d" % Time.get_ticks_usec()
	add_modifier(stat_name, value, type, id)
	# 台账里记录这份限时修饰，方便到期精确移除同 id 的那一条
	_timed_buffs.append({
		"stat": stat_name,
		"modifier": {"id": id},
		"remaining": duration,
	})

## 按 id 移除修饰
func remove_modifier(stat_name: String, id: String) -> bool:
	if not _modifiers.has(stat_name):
		return false
	var arr: Array = _modifiers[stat_name]
	for i in range(arr.size() - 1, -1, -1):
		if arr[i]["id"] == id:
			var removed: Dictionary = arr[i]
			arr.remove_at(i)
			modifier_removed.emit(stat_name, removed)
			stat_changed.emit(stat_name, get_stat(stat_name))
			return true
	return false

## 清空某属性的所有修饰
func clear_modifiers(stat_name: String) -> void:
	_modifiers[stat_name] = []
	stat_changed.emit(stat_name, get_stat(stat_name))

# ---------- 取值 ----------
## 计算某属性的最终值：先累加 add，再乘 mul，最后若有 override 则直接覆盖
## 为什么是这个顺序？因为"覆盖"语义最强，应当拥有最终决定权；
## "乘法"通常表示百分比增益，应当在加法结算之后统一作用。
func get_stat(stat_name: String) -> float:
	var base := float(base_stats.get(stat_name, 0.0))
	var add_sum := 0.0
	var mul_product := 1.0
	var override_value = null

	for mod in _modifiers.get(stat_name, []):
		match mod["type"]:
			"add":
				add_sum += float(mod["value"])
			"mul":
				mul_product *= float(mod["value"])
			"override":
				override_value = float(mod["value"])

	if override_value != null:
		return float(override_value)
	return (base + add_sum) * mul_product

## 便捷读取基础值
func get_base_stat(stat_name: String) -> float:
	return float(base_stats.get(stat_name, 0.0))

## 修改基础值（等级成长时使用）
func set_base_stat(stat_name: String, value: float) -> void:
	base_stats[stat_name] = value
	stat_changed.emit(stat_name, get_stat(stat_name))
```

#### 使用方法

1. 保存文件到 `res://components/stats_component.gd`。
2. 在角色节点下新建 `Node` 子节点 `Stats`，挂上该脚本。
3. 在 Inspector 的 `base_stats` 里按需增删属性行，例如加上 `"crit_chance": 0.1`。
4. 使用示例：

```gdscript
extends CharacterBody2D

@onready var stats: StatsComponent = $Stats

func _ready() -> void:
	print("攻击力基础值：", stats.get_stat("attack"))
	# 装备一把 +15 攻击的剑
	stats.add_modifier("attack", 15.0, "add", "sword_01")
	# 再吃一个 +20% 攻击的药，持续 8 秒
	stats.add_timed_modifier("attack", 1.2, "mul", 8.0, "atk_potion")
	print("当前攻击力：", stats.get_stat("attack"))
	# 监听属性变化，用于刷新 UI
	stats.stat_changed.connect(func(name, val): print(name, " → ", val))

func unequip_sword() -> void:
	stats.remove_modifier("attack", "sword_01")

func apply_slow() -> void:
	# 减速 50%，持续 3 秒（覆盖式，避免与加速叠乘出奇怪数值）
	stats.add_timed_modifier("move_speed", 0.5, "mul", 3.0, "slow")
```

5. 想临时定身，可用覆盖：`stats.add_timed_modifier("move_speed", 0.0, "override", 2.0, "root")`。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `base_stats` | Dictionary | 见代码 | 属性名 → 基础值 |
| `type`（修饰） | String | "add" | `add` 加法 / `mul` 乘法 / `override` 覆盖 |
| `value`（修饰） | float | 必填 | 修饰数值 |
| `id`（修饰） | String | 自动生成 | 修饰唯一标识，用于精确移除 |
| `duration`（限时） | float | 必填 | 持续秒数 |

#### 进阶改造提示

- **加属性上限/下限**：在 `get_stat` 返回前做一次 `clampf`，比如移动速度不低于 0。
- **加来源标记**：把 `id` 换成一个 `{source, key}` 结构，方便"卸下装备时移除该装备的全部修饰"。
- **加"重新计算"信号**：当依赖属性变化时（如 `attack` 依赖 `strength`），用一帧延迟统一重算，避免频繁重算。
- **为什么用字符串做属性名而不是枚举？** 字符串便于策划在 Inspector 里直接填写，也便于存档序列化；枚举虽然更快，但每次加属性都要改代码。
- **为什么把限时 Buff 单列一个台账？** 因为"移除修饰"和"计时到期"是两条独立的路径，混在一起容易导致"移除时漏删计时"或"到期时删错 id"。

---

## 31.6 模板 T05：StateMachine 有限状态机（通用版）

### 模板 T05：StateMachine 有限状态机（通用版）

**用途**：提供一套通用有限状态机，把"当前处于什么状态、状态之间怎么切换"交给引擎管理，你的角色只需为每个状态写一小段行为代码。

**依赖**：需要 `State`（状态基类，`class_name`）与 `StateMachine`（状态机节点，`class_name`）。

**文件位置建议**：`res://fsm/state.gd` 与 `res://fsm/state_machine.gd`

#### 完整代码

状态基类 `State`：

```gdscript
# res://fsm/state.gd
# 状态基类：所有具体状态都继承它
class_name State
extends Node

# 由 StateMachine 在 _ready 时自动注入
var state_machine: StateMachine
# 宿主节点（通常是状态机的父节点），方便状态里直接操作角色
var owner_node: Node

## 进入该状态时调用；msg 可携带切换原因、方向等参数
func enter(_msg: Dictionary = {}) -> void:
	pass

## 离开该状态时调用，用来收尾（停止动画、清零计时等）
func exit() -> void:
	pass

## 每帧调用（对应 _process）
func update(_delta: float) -> void:
	pass

## 每物理帧调用（对应 _physics_process）
func physics_update(_delta: float) -> void:
	pass

## 未处理的输入（对应 _unhandled_input）
func handle_input(_event: InputEvent) -> void:
	pass
```

状态机 `StateMachine`：

```gdscript
# res://fsm/state_machine.gd
# 通用有限状态机：自身作为子节点挂到角色上，其子节点即为各状态
class_name StateMachine
extends Node

# ============ 信号 ============
## 状态发生切换
signal state_changed(from_state: String, to_state: String)

# ============ 可调参数 ============
## 初始状态节点名；留空则使用第一个 State 子节点
@export var initial_state_name: String = ""

# ============ 运行时数据 ============
var current_state: State = null
## 状态历史（记录切换顺序），便于调试与"返回上一状态"
var history: Array[String] = []
## 宿主节点
var owner_node: Node

func _ready() -> void:
	owner_node = get_parent()
	# 给每个 State 子节点注入引用
	for child in get_children():
		if child is State:
			child.state_machine = self
			child.owner_node = owner_node

	# 确定初始状态
	var first: State = null
	if initial_state_name != "":
		first = _find_state(initial_state_name)
	if first == null:
		for child in get_children():
			if child is State:
				first = child
				break
	if first != null:
		current_state = first
		current_state.enter()
		state_changed.emit("", String(first.name))

func _process(delta: float) -> void:
	if current_state != null:
		current_state.update(delta)

func _physics_process(delta: float) -> void:
	if current_state != null:
		current_state.physics_update(delta)

func _unhandled_input(event: InputEvent) -> void:
	if current_state != null:
		current_state.handle_input(event)

# ---------- 对外接口 ----------
## 切换到名为 state_name 的状态；msg 会透传给新状态的 enter()
func change_state(state_name: String, msg: Dictionary = {}) -> void:
	var next := _find_state(state_name)
	if next == null or next == current_state:
		return
	var from_name := ""
	if current_state != null:
		from_name = String(current_state.name)
		current_state.exit()
		history.append(from_name)
	current_state = next
	current_state.enter(msg)
	state_changed.emit(from_name, String(next.name))

## 返回上一个状态（history 为空则不做任何事）
func change_to_previous(msg: Dictionary = {}) -> void:
	if history.is_empty():
		return
	var prev: String = history.pop_back()
	change_state(prev, msg)

## 当前状态名
func get_current_state_name() -> String:
	return "" if current_state == null else String(current_state.name)

func _find_state(state_name: String) -> State:
	# 为什么用遍历子节点比较名字，而不是 get_node(name)？
	# 因为节点名可能含空格，NodePath 需要转义；直接比名字更稳。
	for child in get_children():
		if child is State and String(child.name) == state_name:
			return child
	return null
```

#### 使用方法

1. 保存 `state.gd` 与 `state_machine.gd`。
2. 在玩家节点下新建 `Node` 命名 `StateMachine`，挂上 `state_machine.gd`。
3. 在 `StateMachine` 下新建若干 `Node` 子节点（如 `Idle`、`Move`、`Jump`），每个都挂 `state.gd`（或下面示例的具体状态脚本）。
4. 写一个具体状态示例 `PlayerState`——这里以"待机"和"移动"两个状态为例：

```gdscript
# res://fsm/player/idle_state.gd
extends State

func enter(_msg: Dictionary = {}) -> void:
	# 进入待机：播放动画、把水平速度清零
	var body := owner_node as CharacterBody2D
	body.velocity.x = 0
	$"../../AnimatedSprite2D".play("idle")

func physics_update(delta: float) -> void:
	var body := owner_node as CharacterBody2D
	# 施加重力
	if not body.is_on_floor():
		body.velocity.y += 980.0 * delta
	body.move_and_slide()

func handle_input(event: InputEvent) -> void:
	if Input.is_action_just_pressed("jump"):
		state_machine.change_state("Jump")
```

```gdscript
# res://fsm/player/move_state.gd
extends State

const SPEED := 200.0

func enter(_msg: Dictionary = {}) -> void:
	$"../../AnimatedSprite2D".play("run")

func physics_update(delta: float) -> void:
	var body := owner_node as CharacterBody2D
	var dir := Input.get_axis("move_left", "move_right")
	body.velocity.x = dir * SPEED
	if not body.is_on_floor():
		body.velocity.y += 980.0 * delta
	body.move_and_slide()

func update(_delta: float) -> void:
	# 没有输入时回到待机
	if absf(Input.get_axis("move_left", "move_right")) < 0.01:
		state_machine.change_state("Idle")

func handle_input(event: InputEvent) -> void:
	if Input.is_action_just_pressed("jump"):
		state_machine.change_state("Jump")
```

5. 把玩家本体的 `_physics_process` 交给状态机（或干脆不写逻辑，只保留状态机）。状态机会自动驱动当前状态的 `physics_update`。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `initial_state_name` | String | "" | 初始状态节点名；留空取第一个 State 子节点 |
| `current_state` | State | 运行时 | 当前状态 |
| `history` | Array[String] | 运行时 | 状态切换历史 |
| `owner_node` | Node | 运行时 | 宿主节点，自动注入 |

#### 进阶改造提示

- **加状态超时**：在 `update` 里累加一个计时器，超时后自动切回 `Idle`。
- **加全局转移表**：把"任意状态下按 Esc 都进入 Pause"这类规则写成一张表，统一在 `_unhandled_input` 里处理。
- **加子状态机**：把 `StateMachine` 作为某个状态的子节点，实现"移动状态内部再分走/跑"的层级状态机。
- **为什么 `enter` 收一个 `msg` 字典？** 因为切换往往要传参（比如"跳向左边"），用字典比定义一堆专门方法更灵活，也不会因为加参数而破坏已有调用。
- **为什么不直接用 `_process` 里一堆 `if` 判断？** 状态一多，`if` 会变成"面条式代码"，状态机把每个状态隔离成独立文件，改一个状态不会影响其他状态。

---

## 31.7 模板 T06：EventBus 全局事件总线

### 模板 T06：EventBus 全局事件总线

**用途**：用 Autoload 单例集中定义全局信号，让"发送方"和"接收方"互不认识也能通信，彻底解开节点之间的强耦合。

**依赖**：需要把脚本注册为 **Autoload**，名字建议 `EventBus`。

**文件位置建议**：`res://autoload/event_bus.gd`

#### 完整代码

```gdscript
# res://autoload/event_bus.gd
# 全局事件总线（Autoload 单例）
extends Node
# 注意：这里故意不写 class_name。
# 为什么？因为作为 Autoload 注册后，会自动以节点名（EventBus）全局可见，
# 再写 class_name 会与 Autoload 名冲突，造成"重名"报错。

# ============ 玩家相关 ============
signal player_damaged(amount: float, current_hp: float)
signal player_healed(amount: float)
signal player_died()
signal player_spawned(player: Node2D)

# ============ 战斗相关 ============
signal enemy_killed(enemy: Node2D, drop_item_id: String)
signal score_changed(new_score: int, delta: int)
signal combo_changed(count: int)

# ============ 物品与背包 ============
signal item_picked_up(item_id: String, amount: int)
signal inventory_full_alert(item_id: String)

# ============ 关卡与流程 ============
signal wave_started(wave_index: int, total_waves: int)
signal wave_cleared(wave_index: int)
signal all_waves_cleared()
signal game_started()
signal game_paused(is_paused: bool)
signal game_over(is_win: bool)
```

#### 使用方法

1. 保存文件为 `res://autoload/event_bus.gd`。
2. 打开 **项目 → 项目设置 → Autoload（自动加载）**，把该脚本添加进去，节点名填 `EventBus`。
3. 之后在任何脚本里都能直接用 `EventBus.xxx.emit(...)` 发送、`EventBus.xxx.connect(...)` 监听。
4. 发送方（不知道谁在听）：

```gdscript
# 敌人死亡时
func die() -> void:
	EventBus.enemy_killed.emit(self, "coin")

# 玩家受伤时
func hurt(amount: float) -> void:
	health.take_damage(amount)
	EventBus.player_damaged.emit(amount, health.current_hp)
```

5. 接收方（不知道谁发的）：

```gdscript
# 计分 UI
func _ready() -> void:
	EventBus.enemy_killed.connect(_on_enemy_killed)
	EventBus.score_changed.connect(_on_score_changed)

func _on_enemy_killed(_enemy: Node2D, _drop_item_id: String) -> void:
	var new_score := score + 100
	EventBus.score_changed.emit(new_score, 100)
	score = new_score

func _on_score_changed(new_score: int, _delta: int) -> void:
	$Label.text = "分数：%d" % new_score
```

6. **记得在节点退出时断开**（对常驻单例来说，监听者如果是短期节点，最好在 `_exit_tree` 里 `disconnect`，避免对已释放节点发信号报错）。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| 各 `signal` | signal | 无 | 事件总线本身没有可调参数，全部由你按需增删信号 |

#### 何时该用、何时不该用

这是本模板最重要的部分。事件总线是"双刃剑"，用错了比不用还糟。

**适合用的场景（松耦合、跨层级）：**

| 场景 | 为什么适合 |
| --- | --- |
| 击杀敌人 → 加分并刷新 UI | 敌人与 UI 相隔很远，直接用事件总线最省事 |
| 玩家受伤 → 触发屏幕红闪、音效、震动 | 一个事件要通知多个互不相关的系统 |
| 游戏结束 → 各处清理、暂停、播动画 | 广播式通知，接收方数量不固定 |
| 背包满 → 弹提示 | 逻辑与 UI 分属不同模块 |

**不适合用的场景（强耦合、点对点、高频）：**

| 场景 | 为什么不建议 | 更好的做法 |
| --- | --- | --- |
| 子弹命中敌人 → 结算伤害 | 点对点、每帧可能发生，走总线会难追踪 | 直接拿目标 `HealthComponent` 调用 |
| 状态机内部切换 | 属于同一个对象的内部逻辑 | 直接调用 `state_machine.change_state()` |
| 父子节点之间通信 | 有明确的从属关系 | 用 `@onready` 直连或回调 |
| 每帧发送的高频数据 | 事件总线难以做性能优化 | 直接引用共享数据或信号 |
| 需要返回值/顺序保证的调用 | 信号是"发出去就不管"，没有返回值 | 用普通方法调用 |

一句口诀：**"跨模块、广播式、低频"用总线；"同对象、点对点、高频"走直连。**

#### 进阶改造提示

- **加事件命名规范**：统一用"名词_动词过去式"，如 `enemy_killed`、`wave_cleared`，可读性最好。
- **加调试打印**：临时在 `_ready` 里用一个循环把常用信号接上打印，观察触发顺序。
- **加分类子总线**：项目变大后，可拆成 `CombatBus`、`UIBus` 等多个 Autoload，避免一个文件无限膨胀。
- **注意内存泄漏**：长期存在的监听者若持有被 `queue_free()` 的节点引用，发信号时会报"对象已释放"。断开连接或改用 `is_instance_valid()` 判断。

---

## 31.8 模板 T07：SaveManager 简洁存档

### 模板 T07：SaveManager 简洁存档

**用途**：一个单槽位、纯 JSON 的最简存档管理器，提供 `save_game / load_game / has_save / delete_save` 四个接口，复制即用。

**依赖**：建议注册为 Autoload，名为 `SaveManager`。

**文件位置建议**：`res://autoload/save_manager.gd`

> 说明：第 28 章我们写过功能完整的存档系统（多槽位、版本迁移、自动备份）。这里是它的**精简姊妹版**，面向"我只要一个存档、只想用 JSON 存点进度"的场景。两者不冲突，按需选一。

#### 完整代码

```gdscript
# res://autoload/save_manager.gd
# 简洁存档管理器（Autoload：SaveManager）
extends Node

# 存档路径：user:// 是 Godot 为每个项目分配的"可写"目录，
# 打包成 exe / apk 后依然可读写，是存玩家数据唯一正确的选择。
const SAVE_PATH := "user://save_slot_1.json"

# ============ 信号 ============
signal game_saved()
signal game_loaded()
signal save_deleted()

## 保存：把一个字典序列化成 JSON 写入磁盘。成功返回 true。
func save_game(data: Dictionary) -> bool:
	var file := FileAccess.open(SAVE_PATH, FileAccess.WRITE)
	if file == null:
		# 为什么用 push_error 而不是 print？错误会进调试器，更容易被看见。
		push_error("无法写入存档：%s（错误码 %d）" % [SAVE_PATH, FileAccess.get_open_error()])
		return false
	# "\t" 让 JSON 带上缩进，方便你直接打开文件肉眼检查
	file.store_string(JSON.stringify(data, "\t"))
	file.close()
	game_saved.emit()
	return true

## 读取：返回存档字典；文件不存在或损坏时返回空字典
func load_game() -> Dictionary:
	if not has_save():
		return {}
	var file := FileAccess.open(SAVE_PATH, FileAccess.READ)
	if file == null:
		push_error("无法读取存档：%s" % SAVE_PATH)
		return {}
	var text := file.get_as_text()
	file.close()

	# JSON.parse_string 解析失败会返回 null，务必判类型
	var parsed = JSON.parse_string(text)
	if typeof(parsed) != TYPE_DICTIONARY:
		push_warning("存档内容已损坏，忽略：%s" % SAVE_PATH)
		return {}
	game_loaded.emit()
	return parsed

## 是否存在存档
func has_save() -> bool:
	return FileAccess.file_exists(SAVE_PATH)

## 删除存档。成功返回 true，本就不存在则返回 false。
func delete_save() -> bool:
	if not has_save():
		return false
	# 用 DirAccess.open("user://") 拿到目录再删，比拼绝对路径更稳妥
	var dir := DirAccess.open("user://")
	if dir == null:
		return false
	var err := dir.remove("save_slot_1.json")
	if err != OK:
		push_error("删除存档失败，错误码 %d" % err)
		return false
	save_deleted.emit()
	return true
```

#### 使用方法

1. 保存文件为 `res://autoload/save_manager.gd`。
2. 在 **项目设置 → Autoload** 里添加，名字填 `SaveManager`。
3. 存档（比如暂停菜单里点"保存"）：

```gdscript
func save_now() -> void:
	var data := {
		"version": 1,
		"player": {
			"hp": 76.0,
			"position": [player.global_position.x, player.global_position.y],
			"inventory": ["potion", "potion", "sword"],
		},
		"score": 1520,
		"saved_at": Time.get_datetime_string_from_system(),
	}
	if SaveManager.save_game(data):
		print("保存成功")
```

4. 读档（游戏开始时）：

```gdscript
func _ready() -> void:
	if not SaveManager.has_save():
		return
	var data := SaveManager.load_game()
	if data.is_empty():
		return
	# 注意：JSON 里所有数字都会变成 float，取位置时要自己转回来
	var pos: Array = data["player"]["position"]
	player.global_position = Vector2(float(pos[0]), float(pos[1]))
	player.get_node("Inventory").clear()
	for item_id in data["player"]["inventory"]:
		player.get_node("Inventory").add_item(String(item_id), 1)
```

5. 删除存档：`SaveManager.delete_save()`。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `SAVE_PATH` | const String | "user://save_slot_1.json" | 存档文件路径（改常量即可换位置/槽位） |

#### 进阶改造提示

- **改成多槽位**：把常量换成变量 `var slot := 1`，路径写成 `"user://save_slot_%d.json" % slot`。
- **加"加密"**：可用 `FileAccess.open_encrypted_with_pass()` 代替 `open()`，传入一个密码字符串，适合小体量存档。
- **加"版本号"**：读取时比较 `data.get("version", 1)`，做字段迁移。
- **为什么用 JSON 而不是二进制？** 因为 JSON 是纯文本，出问题能直接打开看，调试成本极低；对绝大多数独立游戏来说，性能完全够用。
- **为什么不存节点路径？** 节点路径在重构场景时极易失效。正确的做法是存"稳定标识"（如物品 id、关卡编号），再用代码映射回节点。

---

## 31.9 本章小结

1. 本卷所有模板都遵循统一格式：**用途 / 依赖 / 文件位置 / 完整代码 / 使用方法 / 可调参数 / 进阶改造**，方便快速抄用。
2. 复制模板的四个标准动作是：**建文件填代码 → 查重 `class_name` → 挂载为子节点 → 接线调用**。
3. T01 血量组件的核心是"接口 + 信号"：`take_damage / heal / kill / revive` 对外，`hp_changed / damaged / died` 对外广播。
4. T01 的无敌帧用"计时器 + 布尔锁"实现，是"受击保护"最通用的做法。
5. T02 把伤害拆成"数据类 `DamageInfo`"与"计算器 `DamageCalculator`"，让结算逻辑与战斗流程解耦，暴击与穿透都在一处集中处理。
6. T02 用 `Callable` 做"伤害数字回调"，避免计算器直接依赖 UI。
7. T03 背包的关键在**堆叠合并顺序**：先填已有堆、再开新格，最后才报"背包满"。
8. T03 的 `move_item` 同时实现了"合并"和"交换"两种语义，适配拖拽整理的常见需求。
9. T04 属性系统采用"基础值 + 修饰列表 + 最终值"三层，`add` → `mul` → `override` 的结算顺序必须写死并注释清楚。
10. T04 的限时 Buff 用独立台账管理，保证"到期移除"和"手动移除"不会互相打架。
11. T05 状态机把每个状态隔离成独立脚本，彻底告别"一坨 `if`"的面条代码；`change_state(name, msg)` 用字典传参，扩展性最好。
12. T05 的状态历史 `history` 支持"返回上一状态"，做命中反馈、受伤打断非常方便。
13. T06 事件总线的价值是"解耦"，但必须克制使用：**跨模块、广播式、低频**才用，**同对象、点对点、高频**走直连。
14. T06 作为 Autoload 时**不要写 `class_name`**，否则会与自动加载名冲突。
15. T07 存档必须写在 `user://` 目录下；JSON 是"可读、易调试"的最优解。
16. T07 读档时要注意 JSON 数字全变 `float`，位置等数据需手动转换类型。
17. 所有组件式模板都遵循同一哲学：**宿主挂组件、组件发信号、宿主做决策**。
18. 判断该不该用某个模板的标准，不是"它酷不酷"，而是"它是否让我的代码更容易改、更容易查"。
19. 模板是起点不是终点：先跑通，再通过 `@export` 调参数，最后才动结构。
20. 这一章的数据与状态模板，是后面行为类模板（AI、刷怪、弹幕）的地基——血量、属性、状态机都会在下一章反复出现。

---

# 第 32 章：行为模板（AI 与逻辑类）

> 上一章的模板管"数据与状态"，这一章的模板管"**行为**"。它们让角色动起来、让关卡有节奏、让战斗有手感。你会看到，第 31 章的 `HealthComponent`、`StatsComponent`、`StateMachine` 在这里被反复引用——这正是"模板库"的意义：**模块之间互相拼装**。

## 32.1 模板 T08：PatrolAI 巡逻 AI

### 模板 T08：PatrolAI 巡逻 AI

**用途**：让敌人在若干路点之间来回/环状巡逻，支持到达判定、停留等待、朝向翻转，并能被击退打断。

**依赖**：无。作为子 `Node` 挂到 `Node2D` 宿主上即可。

**文件位置建议**：`res://ai/patrol_ai.gd`

#### 完整代码

```gdscript
# res://ai/patrol_ai.gd
# 巡逻 AI：在给定路点之间移动
class_name PatrolAI
extends Node

# ============ 信号 ============
## 到达某个路点
signal waypoint_reached(index: int)
## 单程/整轮巡逻结束（loop=false 时才可能触发）
signal patrol_finished()

# ============ 可调参数 ============
## 移动速度（像素/秒）
@export var speed: float = 80.0
## 到达某路点后的停留时间（秒）
@export var wait_time: float = 1.0
## 到达判定距离（小于此距离视为"到达"）
@export var arrive_distance: float = 4.0
## true = 环绕循环；false = 走完往返/停止
@export var loop: bool = true
## 路点数组（世界坐标）。留空则自动在出生点附近生成一条演示路径。
@export var waypoints: Array[Vector2] = []

# ============ 运行时数据 ============
var current_index: int = 0
## 外部可置 false 来暂停巡逻（比如进入追击状态时）
var enabled: bool = true

var _body: Node2D
var _waiting: bool = false
var _wait_timer: float = 0.0
## 击退速度（会被逐帧衰减）
var _knockback: Vector2 = Vector2.ZERO
var _direction: int = 1  # 1 前进，-1 后退（loop=false 时用于往返）

func _ready() -> void:
	_body = get_parent() as Node2D
	# 没有手填路点时生成一条演示路径，保证"拖上去就能看到效果"
	if waypoints.is_empty() and _body != null:
		var p := _body.global_position
		waypoints = [p + Vector2(120, 0), p + Vector2(120, 60), p + Vector2(-40, 60)]

func _physics_process(delta: float) -> void:
	if not enabled or _body == null or waypoints.is_empty():
		return

	# 击退优先：击退期间不执行正常巡逻
	if _knockback.length() > 1.0:
		_body.global_position += _knockback * delta
		_knockback = _knockback.move_toward(Vector2.ZERO, 600.0 * delta)
		return

	# 停留等待
	if _waiting:
		_wait_timer -= delta
		if _wait_timer <= 0.0:
			_waiting = false
			_advance_index()
		return

	# 朝当前路点移动
	var target: Vector2 = waypoints[current_index]
	var to_target := target - _body.global_position
	if to_target.length() <= arrive_distance:
		_body.global_position = target
		waypoint_reached.emit(current_index)
		# 为什么到达后要停留？避免在转角处来回抖动，也给玩家"可预测"的节奏
		_waiting = true
		_wait_timer = wait_time
		return

	var dir := to_target.normalized()
	_body.global_position += dir * speed * delta
	_face(dir.x)

func _advance_index() -> void:
	if loop:
		current_index = (current_index + 1) % waypoints.size()
		return
	# 非循环：走到尽头后反向
	if current_index >= waypoints.size() - 1:
		_direction = -1
	elif current_index <= 0:
		_direction = 1
	current_index += _direction
	if current_index < 0:
		current_index = 0
		patrol_finished.emit()

func _face(dx: float) -> void:
	if absf(dx) < 0.01:
		return
	# 假设贴图默认朝右；向左移动时水平翻转
	_body.scale.x = absf(_body.scale.x) * signf(dx)

## 施加一次击退（会叠加）
func apply_knockback(force: Vector2) -> void:
	_knockback += force

## 强制跳到指定路点
func set_waypoint(index: int) -> void:
	if waypoints.is_empty():
		return
	current_index = clampi(index, 0, waypoints.size() - 1)
	_waiting = false

## 从某点开始巡逻（常用于出生/回归）
func start_from(position_: Vector2) -> void:
	if _body != null:
		_body.global_position = position_
	current_index = 0
	_waiting = false
	_knockback = Vector2.ZERO
```

#### 使用方法

1. 保存为 `res://ai/patrol_ai.gd`。
2. 选中敌人节点，新增 `Node` 子节点，命名 `PatrolAI`，挂上脚本。
3. 在 Inspector 里填 `waypoints`（点小加号，逐个填 `Vector2`）。不填也能跑，会自动生成演示路径。
4. 让敌人的 `HealthComponent` 受伤时调用击退：

```gdscript
extends Node2D

@onready var patrol: PatrolAI = $PatrolAI
@onready var health: HealthComponent = $Health

func _ready() -> void:
	health.damaged.connect(_on_damaged)

func _on_damaged(amount: float, info: Dictionary) -> void:
	# 从伤害来源方向把敌人击退
	var from: Vector2 = info.get("from_position", global_position - Vector2(1, 0))
	var push_dir := (global_position - from).normalized()
	patrol.apply_knockback(push_dir * 400.0)
```

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `speed` | float | 80.0 | 巡逻移动速度 |
| `wait_time` | float | 1.0 | 每个路点停留时间 |
| `arrive_distance` | float | 4.0 | 到达判定距离 |
| `loop` | bool | true | 环绕循环 / 往返 |
| `waypoints` | Array[Vector2] | [] | 路点世界坐标列表 |
| `enabled` | bool | true | 运行时开关 |

#### 进阶改造提示

- **加"看见玩家就停"**：在 `_physics_process` 开头检查同级的 `ChaseAI` 是否锁定了目标，是则直接 `return`。
- **加"地面检测"**：在路点前方投一条射线，检测到悬崖就停住（防止巡逻掉坑）。
- **加"剧情脚本"**：把 `waypoints` 从手工填写换成关卡物体（`Path2D` 或 `Marker2D` 数组）读取。
- **为什么击退要单独处理而不是加到速度里？** 因为巡逻是"位移动画"而非物理速度，把击退叠加进位置更新更简单直接，还能与巡逻逻辑并行不冲突。

---

## 32.2 模板 T09：ChaseAI 追击 AI

### 模板 T09：ChaseAI 追击 AI

**用途**：当玩家进入"侦测范围 + 视野角度"内时锁定并追击，进入攻击距离后停下；丢失目标后回到巡逻。

**依赖**：可选依赖 T08 的 `PatrolAI`（同名子节点）。用第 25 章的**点积**做视野角度判定。

**文件位置建议**：`res://ai/chase_ai.gd`

#### 完整代码

```gdscript
# res://ai/chase_ai.gd
# 追击 AI：侦测 → 追踪 → 攻击距离停下 → 丢失回到巡逻
class_name ChaseAI
extends Node

# ============ 信号 ============
## 发现目标
signal target_spotted(target: Node2D)
## 丢失目标
signal target_lost()
## 进入攻击距离
signal in_attack_range(target: Node2D)

# ============ 可调参数 ============
## 侦测半径
@export var detect_range: float = 220.0
## 丢失半径（应大于侦测半径，形成"迟滞"避免反复切换）
@export var lose_range: float = 320.0
## 视野张角（度）。360 表示全方位感知。
@export var view_angle_deg: float = 120.0
## 追击速度
@export var speed: float = 120.0
## 攻击距离：进入后停下
@export var attack_range: float = 40.0
## 目标所在的分组（玩家记得加入 "player" 分组）
@export var target_group: String = "player"
## 初始朝向（用于视野判定），默认朝右
@export var facing_dir: Vector2 = Vector2.RIGHT
## 是否在丢失目标时自动恢复同级 PatrolAI
@export var resume_patrol: bool = true

# ============ 运行时数据 ============
var target: Node2D = null
var enabled: bool = true

var _body: Node2D
var _patrol: PatrolAI = null
## 上一次是否已发出"进入攻击距离"信号，避免每帧重复发
var _was_in_attack_range: bool = false

func _ready() -> void:
	_body = get_parent() as Node2D
	if resume_patrol and _body != null:
		_patrol = _body.get_node_or_null("PatrolAI") as PatrolAI

func _physics_process(delta: float) -> void:
	if not enabled or _body == null:
		return

	# 没有目标：尝试重新侦测
	if target == null or not is_instance_valid(target):
		_try_acquire_target()
		return

	var to_target := target.global_position - _body.global_position
	var dist := to_target.length()

	# 丢失判定（超出 lose_range）
	if dist > lose_range:
		_lose_target()
		return

	var dir := to_target.normalized()
	facing_dir = dir  # 追击时始终面向目标

	# 攻击距离判定
	var in_range := dist <= attack_range
	if in_range and not _was_in_attack_range:
		in_attack_range.emit(target)
	_was_in_attack_range = in_range

	# 未进入攻击距离就继续追
	if not in_range:
		_body.global_position += dir * speed * delta
		_face(dir.x)

func _try_acquire_target() -> void:
	var best: Node2D = null
	var best_dist := INF
	for node in get_tree().get_nodes_in_group(target_group):
		if not (node is Node2D):
			continue
		var candidate := node as Node2D
		var d := _body.global_position.distance_to(candidate.global_position)
		if d > detect_range:
			continue
		if not _in_view(candidate):
			continue
		if d < best_dist:
			best_dist = d
			best = candidate
	if best != null:
		target = best
		_was_in_attack_range = false
		# 发现目标时暂停巡逻，避免两套逻辑打架
		if _patrol != null:
			_patrol.enabled = false
		target_spotted.emit(best)

## 视野判定：用点积比较"朝向"与"目标方向"的夹角
## 点积 = cos(夹角)。夹角越小点积越接近 1。
func _in_view(candidate: Node2D) -> bool:
	# 360 度视野直接放行
	if view_angle_deg >= 360.0:
		return true
	var to_candidate := (candidate.global_position - _body.global_position).normalized()
	var threshold := cos(deg_to_rad(view_angle_deg * 0.5))
	return facing_dir.normalized().dot(to_candidate) >= threshold

func _lose_target() -> void:
	target = null
	_was_in_attack_range = false
	target_lost.emit()
	if _patrol != null:
		_patrol.enabled = true

func _face(dx: float) -> void:
	if absf(dx) < 0.01:
		return
	_body.scale.x = absf(_body.scale.x) * signf(dx)
```

#### 使用方法

1. 保存为 `res://ai/chase_ai.gd`。
2. 给敌人节点加 `Node` 子节点 `ChaseAI`，挂上脚本。
3. **把玩家的节点加入 `"player"` 分组**：选中玩家 → 节点面板 → Groups → 添加 `player`。这是追击能工作的前提。
4. 在 Inspector 里调 `detect_range`、`view_angle_deg`、`attack_range`。
5. 连接攻击逻辑：

```gdscript
extends Node2D

@onready var chase: ChaseAI = $ChaseAI

func _ready() -> void:
	chase.target_spotted.connect(func(t): print("发现玩家！"))
	chase.in_attack_range.connect(_on_in_range)
	chase.target_lost.connect(func(): print("跟丢了"))

func _on_in_range(t: Node2D) -> void:
	print("进入攻击范围，开始攻击：", t)
	# 这里触发攻击动画 / 生成子弹
```

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `detect_range` | float | 220.0 | 侦测半径 |
| `lose_range` | float | 320.0 | 丢失半径（应大于侦测半径） |
| `view_angle_deg` | float | 120.0 | 视野张角（度），360 为全方位 |
| `speed` | float | 120.0 | 追击速度 |
| `attack_range` | float | 40.0 | 攻击距离，进入后停下 |
| `target_group` | String | "player" | 目标分组名 |
| `facing_dir` | Vector2 | (1,0) | 当前朝向 |
| `resume_patrol` | bool | true | 丢失后恢复巡逻 |

#### 进阶改造提示

- **加"视线遮挡"**：从敌人到玩家发一条 `RayCast2D`，被墙挡住就不算看见。
- **加"警觉状态"**：发现目标后先进入一个短暂的"发现停顿"再追，给玩家反应时间，手感更好。
- **加"绕障"**：用 `NavigationAgent2D` 代替直接位移，走真正的寻路。
- **为什么 `lose_range` 要大于 `detect_range`？** 这是经典的"迟滞"设计。若两者相等，玩家在边界反复进出会导致 AI 每帧在"追/不追"之间抖动，观感极差。
- **为什么用点积而不是 `angle_to()`？** 点积是几次乘加运算，比反三角函数便宜，且能直接与 `cos(半角)` 比较，避免了角度归一化的边界问题。

---

## 32.3 模板 T10：WaveSpawner 波次刷怪器

### 模板 T10：WaveSpawner 波次刷怪器

**用途**：按配置一波一波地刷怪，每波可设数量、间隔、敌人类型、血量倍率，清完自动进入休息，再开始下一波。

**依赖**：可选配合 T01 `HealthComponent`（用于按倍率调整敌人血量）；敌人场景需设为 `PackedScene`。

**文件位置建议**：`res://spawners/wave_spawner.gd`

#### 完整代码

```gdscript
# res://spawners/wave_spawner.gd
# 波次刷怪器
class_name WaveSpawner
extends Node

enum Phase { IDLE, SPAWNING, WAITING_CLEAR, REST }

# ============ 信号 ============
## 一波开始（index 从 0 开始）
signal wave_started(index: int, total: int)
## 本波刷怪进度
signal wave_progress(index: int, spawned: int, total: int)
## 一波清完（最后一只敌人死亡）
signal wave_cleared(index: int)
## 全部波次完成
signal all_waves_cleared()

# ============ 可调参数 ============
## 出生点（Node2D 节点路径数组）；留空则使用刷怪器自身位置
@export var spawn_points: Array[NodePath] = []
## 万用敌人场景（当某波未指定 enemy_scene 时使用）
@export var default_enemy_scene: PackedScene
## 波与波之间的休息时间（秒）
@export var rest_time: float = 5.0
## 是否在场景就绪后自动开始
@export var auto_start: bool = true
## 波次配置数组，每项形如：
## {"count": 5, "interval": 1.0, "enemy_scene": null, "hp_multiplier": 1.0}
@export var waves: Array[Dictionary] = [
	{"count": 5, "interval": 1.0, "enemy_scene": null, "hp_multiplier": 1.0},
	{"count": 8, "interval": 0.8, "enemy_scene": null, "hp_multiplier": 1.25},
	{"count": 12, "interval": 0.6, "enemy_scene": null, "hp_multiplier": 1.5},
]

# ============ 运行时数据 ============
var current_wave: int = -1
## 当前波还活着的敌人
var _alive: Array[Node] = []
var _phase: Phase = Phase.IDLE
var _spawn_timer: float = 0.0
var _rest_timer: float = 0.0
var _spawned_count: int = 0

func _ready() -> void:
	if auto_start:
		# 延后一帧启动，确保场景里其他节点都已 _ready
		call_deferred("start_next_wave")

func _process(delta: float) -> void:
	match _phase:
		Phase.SPAWNING:
			_process_spawning(delta)
		Phase.WAITING_CLEAR:
			if _alive.is_empty():
				_phase = Phase.REST
				wave_cleared.emit(current_wave)
				_rest_timer = rest_time
		Phase.REST:
			_rest_timer -= delta
			if _rest_timer <= 0.0:
				start_next_wave()

# ---------- 对外接口 ----------
## 手动开始下一波
func start_next_wave() -> void:
	current_wave += 1
	if current_wave >= waves.size():
		_phase = Phase.IDLE
		all_waves_cleared.emit()
		return
	_spawned_count = 0
	_spawn_timer = 0.0
	_phase = Phase.SPAWNING
	wave_started.emit(current_wave, waves.size())

## 立即结束当前波并进入休息（例如玩家触发机关）
func force_end_wave() -> void:
	if _phase == Phase.IDLE:
		return
	for enemy in _alive:
		if is_instance_valid(enemy):
			enemy.queue_free()
	_alive.clear()
	_phase = Phase.REST
	wave_cleared.emit(current_wave)
	_rest_timer = rest_time

## 当前波剩余敌人数量
func alive_count() -> int:
	return _alive.size()

func _process_spawning(delta: float) -> void:
	var cfg: Dictionary = waves[current_wave]
	var count := int(cfg.get("count", 5))
	var interval := float(cfg.get("interval", 1.0))

	if _spawned_count >= count:
		# 本波已刷完，等待清场
		if _alive.is_empty():
			_phase = Phase.REST
			wave_cleared.emit(current_wave)
			_rest_timer = rest_time
		else:
			_phase = Phase.WAITING_CLEAR
		return

	_spawn_timer -= delta
	if _spawn_timer > 0.0:
		return
	_spawn_one(cfg)
	_spawned_count += 1
	_spawn_timer = interval
	wave_progress.emit(current_wave, _spawned_count, count)

func _spawn_one(cfg: Dictionary) -> void:
	var scene: PackedScene = cfg.get("enemy_scene", null)
	if scene == null:
		scene = default_enemy_scene
	if scene == null:
		push_warning("WaveSpawner：本波未指定敌人场景，也无法使用默认场景")
		return

	var enemy := scene.instantiate()

	# 按倍率抬高敌人血量：查找其 Health 子节点
	var hp_mul := float(cfg.get("hp_multiplier", 1.0))
	var health := enemy.get_node_or_null("Health")
	if health != null and "max_hp" in health:
		health.max_hp *= hp_mul
		health.current_hp = health.max_hp

	# 先加入场景树，再设置全局位置（未入树时 global_position 不可靠）
	get_parent().add_child(enemy)
	var point := _pick_spawn_point()
	if point != null:
		enemy.global_position = point

	_alive.append(enemy)
	# 用 tree_exited 统一处理"敌人离场"，无论它是被打死还是被移除
	enemy.tree_exited.connect(_on_enemy_removed.bind(enemy))

func _on_enemy_removed(enemy: Node) -> void:
	_alive.erase(enemy)

func _pick_spawn_point() -> Node2D:
	if spawn_points.is_empty():
		return get_parent() as Node2D
	# 随机挑一个出生点
	var path: NodePath = spawn_points[randi() % spawn_points.size()]
	return get_node_or_null(path) as Node2D
```

#### 使用方法

1. 保存为 `res://spawners/wave_spawner.gd`。
2. 在关卡节点下新建 `Node` 命名 `WaveSpawner`，挂上脚本。
3. 在场景里摆几个 `Marker2D` 作为出生点，把它们拖到 `spawn_points` 数组里。
4. 把敌人场景（`.tscn`）拖到 `default_enemy_scene`。
5. 在 Inspector 里编辑 `waves` 数组：每一波点开填 `count / interval / hp_multiplier`；想用不同敌人，给该波单独指定 `enemy_scene`。
6. 监听进度事件：

```gdscript
extends Node2D

@onready var spawner: WaveSpawner = $WaveSpawner

func _ready() -> void:
	spawner.wave_started.connect(func(i, total): print("第 %d/%d 波开始" % [i + 1, total]))
	spawner.wave_progress.connect(func(i, spawned, total): print("本波已刷 %d/%d" % [spawned, total]))
	spawner.wave_cleared.connect(func(i): print("第 %d 波清完，休息中……" % [i + 1]))
	spawner.all_waves_cleared.connect(_on_win)

func _on_win() -> void:
	print("全部波次通过！")
```

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `spawn_points` | Array[NodePath] | [] | 出生点节点路径；留空用刷怪器位置 |
| `default_enemy_scene` | PackedScene | null | 默认敌人场景 |
| `rest_time` | float | 5.0 | 波间休息时间 |
| `auto_start` | bool | true | 是否自动开打 |
| `waves` | Array[Dictionary] | 见代码 | 波次配置列表 |
| `waves[i].count` | int | 5 | 本波敌人数量 |
| `waves[i].interval` | float | 1.0 | 本波刷怪间隔 |
| `waves[i].enemy_scene` | PackedScene | null | 本波专用敌人场景 |
| `waves[i].hp_multiplier` | float | 1.0 | 本波敌人血量倍率 |

#### 进阶改造提示

- **加"精英波"标记**：在配置里加 `"is_boss": true`，触发不同的 UI 提示。
- **加"难度递增曲线"**：不手工写每一波，而是用一个公式动态生成 `waves`，如数量 = `5 + wave * 3`。
- **加"掉落随波次提升"**：在 `enemy_killed` 事件里按 `current_wave` 决定掉落概率。
- **为什么用 `tree_exited` 而不是直接监听敌人的 `died` 信号？** 因为敌人在测试时可能被手动删除、也可能因场景切换离场，`tree_exited` 能覆盖所有"离场"情况，更健壮。
- **为什么刷怪先 `add_child` 再设位置？** 节点不在场景树中时，`global_position` 的基准节点尚未建立，赋值会不稳定；先入树再定位是安全顺序。

---

## 32.4 模板 T11：BulletPattern 弹幕发射器

### 模板 T11：BulletPattern 弹幕发射器

**用途**：提供单发、扇形、环形、螺旋四种弹幕发射模式，支持角度、数量、冷却配置，并附带对象池版本以减少频繁实例化的开销。

**依赖**：需要一个子弹场景（含下面的 `Bullet` 脚本）。使用对象池时子弹需支持"回收复用"。

**文件位置建议**：`res://combat/bullet.gd` 与 `res://combat/bullet_pattern.gd`

#### 完整代码

先写子弹本体 `Bullet`（支持被对象池回收）：

```gdscript
# res://combat/bullet.gd
# 简单子弹：直线飞行，超时或越界后回收
class_name Bullet
extends Area2D

@export var speed: float = 300.0
@export var lifetime: float = 3.0
@export var damage: float = 5.0

## 由发射器赋值
var direction: Vector2 = Vector2.RIGHT
## 归属于哪个对象池（回收时归还）
var pool: Array = []

var _age: float = 0.0

func _physics_process(delta: float) -> void:
	position += direction * speed * delta
	_age += delta
	if _age >= lifetime:
		recycle()

func _ready() -> void:
	area_entered.connect(_on_area_entered)

func _on_area_entered(area: Area2D) -> void:
	var hp := area.get_node_or_null("Health")
	if hp is HealthComponent:
		hp.take_damage(damage, {"element": "physical"})
	recycle()

func recycle() -> void:
	_age = 0.0
	visible = false
	set_physics_process(false)
	if pool != null and not pool.has(self):
		pool.append(self)
```

再写发射器 `BulletPattern`：

```gdscript
# res://combat/bullet_pattern.gd
# 弹幕发射器：单发 / 扇形 / 环形 / 螺旋
class_name BulletPattern
extends Node2D

# ============ 信号 ============
## 完成一次发射
signal fired(mode: String, bullet_count: int)

# ============ 可调参数 ============
## 子弹场景
@export var bullet_scene: PackedScene
## 发射模式：single / fan / circle / spiral
@export_enum("single", "fan", "circle", "spiral") var mode: String = "single"
## 冷却时间（秒）
@export var cooldown: float = 0.5
## 子弹速度（覆盖子弹默认速度）
@export var bullet_speed: float = 300.0
## 子弹伤害
@export var bullet_damage: float = 5.0
## 单次发射的子弹数量（扇形/环形/螺旋使用）
@export var bullet_count: int = 3
## 扇形张角（度）
@export var fan_angle_deg: float = 45.0
## 螺旋每次递增的角度（度）
@export var spiral_step_deg: float = 15.0
## 是否使用对象池
@export var use_pool: bool = true

# ============ 运行时数据 ============
## 外部可设置的瞄准方向（不设置时用自身朝右）
var aim_direction: Vector2 = Vector2.RIGHT
var _cooldown_timer: float = 0.0
var _spiral_angle: float = 0.0
## 对象池：回收来的空闲子弹
var _pool: Array = []

func _process(delta: float) -> void:
	if _cooldown_timer > 0.0:
		_cooldown_timer = maxf(_cooldown_timer - delta, 0.0)

# ---------- 对外接口 ----------
func can_fire() -> bool:
	return _cooldown_timer <= 0.0 and bullet_scene != null

## 发射。direction 为基准方向（不传则用 aim_direction）
func fire(direction: Vector2 = Vector2.ZERO) -> bool:
	if not can_fire():
		return false
	var base_dir := direction
	if base_dir == Vector2.ZERO:
		base_dir = aim_direction
	base_dir = base_dir.normalized()

	var count := _emit_by_mode(base_dir)
	_cooldown_timer = cooldown
	fired.emit(mode, count)
	return true

## 剩余冷却比例（0~1），供 UI 画冷却圈
func cooldown_ratio() -> float:
	if cooldown <= 0.0:
		return 0.0
	return clampf(_cooldown_timer / cooldown, 0.0, 1.0)

func _emit_by_mode(base_dir: Vector2) -> int:
	match mode:
		"single":
			_spawn_bullet(base_dir)
			return 1
		"fan":
			return _emit_fan(base_dir)
		"circle":
			return _emit_circle(base_dir)
		"spiral":
			return _emit_spiral(base_dir)
	return 0

func _emit_fan(base_dir: Vector2) -> int:
	var n := maxi(bullet_count, 1)
	if n == 1:
		_spawn_bullet(base_dir)
		return 1
	var half := deg_to_rad(fan_angle_deg * 0.5)
	# 从 -half 到 +half 均匀铺开
	for i in n:
		var t := float(i) / float(n - 1)   # 0 → 1
		var angle := lerpf(-half, half, t)
		_spawn_bullet(base_dir.rotated(angle))
	return n

func _emit_circle(base_dir: Vector2) -> int:
	var n := maxi(bullet_count, 1)
	var step := TAU / float(n)
	for i in n:
		_spawn_bullet(base_dir.rotated(step * i))
	return n

func _emit_spiral(base_dir: Vector2) -> int:
	var n := maxi(bullet_count, 1)
	var step := deg_to_rad(spiral_step_deg)
	for i in n:
		_spawn_bullet(base_dir.rotated(_spiral_angle + step * i))
	# 每次发射后基准角度推进，形成螺旋
	_spiral_angle = fmod(_spiral_angle + step * n, TAU)
	return n

func _spawn_bullet(dir: Vector2) -> void:
	if bullet_scene == null:
		return
	var bullet: Bullet = _get_bullet_from_pool()
	bullet.global_position = global_position
	bullet.direction = dir.normalized()
	bullet.speed = bullet_speed
	bullet.damage = bullet_damage
	bullet.pool = _pool
	bullet.visible = true
	bullet.set_physics_process(true)

func _get_bullet_from_pool() -> Bullet:
	if use_pool and not _pool.is_empty():
		return _pool.pop_back() as Bullet
	var b := bullet_scene.instantiate() as Bullet
	# 子弹挂到发射器的父节点下，避免跟随发射器一起旋转
	get_parent().add_child(b)
	return b
```

#### 使用方法

1. 保存 `bullet.gd` 与 `bullet_pattern.gd`。
2. 新建一个子弹场景：根节点用 `Area2D`，挂 `bullet.gd`，给它一个 `CollisionShape2D`，可选加一个 `Sprite2D` 作为外观。
3. 在敌人/炮台节点下新建 `Node2D` 命名 `Muzzle`，挂上 `bullet_pattern.gd`，把它拖到炮口位置。
4. 在 Inspector 里把子弹场景拖到 `bullet_scene`，选择 `mode`，调 `cooldown / bullet_count` 等。
5. 开火示例：

```gdscript
extends Node2D

@onready var muzzle: BulletPattern = $Muzzle

func _process(_delta: float) -> void:
	# 正弦扫射：在 -90° 到 +90° 之间来回摆，配合 fan/circle 模式
	var aim := Vector2.RIGHT.rotated(sin(Time.get_ticks_msec() * 0.001))
	muzzle.aim_direction = aim
	muzzle.fire()   # 冷却未到会自动返回 false

func shoot_at_player(player: Node2D) -> void:
	# 朝玩家瞄准发射
	var dir := (player.global_position - muzzle.global_position).normalized()
	muzzle.fire(dir)
```

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `bullet_scene` | PackedScene | null | 子弹场景（必填） |
| `mode` | String | "single" | single / fan / circle / spiral |
| `cooldown` | float | 0.5 | 发射冷却（秒） |
| `bullet_speed` | float | 300.0 | 子弹速度 |
| `bullet_damage` | float | 5.0 | 子弹伤害 |
| `bullet_count` | int | 3 | 扇形/环形/螺旋的子弹数量 |
| `fan_angle_deg` | float | 45.0 | 扇形张角 |
| `spiral_step_deg` | float | 15.0 | 螺旋每次递增角度 |
| `use_pool` | bool | true | 是否使用对象池 |

#### 进阶改造提示

- **加"子弹分组/滤镜"**：用 `collision_layer / collision_mask` 区分我方与敌方子弹，防止误伤。
- **加"追踪弹"**：给 `Bullet` 一个可选的 `homing_target`，每帧把 `direction` 朝目标插值。
- **加"弹幕脚本表"**：把"每 0.5 秒切换一次扇形/环形/螺旋"写成一张时序表，做出真正的弹幕演出。
- **为什么环形要用 `TAU / n` 均分？** 因为 `TAU` 是 2π，除以数量正好得到每颗子弹之间的等角间隔，能保证环形闭合均匀。
- **为什么要做对象池？** 弹幕游戏每秒可能生成上百颗子弹，频繁 `instantiate()` 与 `queue_free()` 会造成明显的帧率波动；对象池把"创建/销毁"变成"隐藏/复用"，是弹幕类游戏的标配。

---

## 32.5 模板 T12：ComboSystem 连击系统

### 模板 T12：ComboSystem 连击系统

**用途**：统计连续命中次数，在连击窗口超时后归零，并按连击数提供伤害加成、评分加成与里程碑特效触发。

**依赖**：无。可作为玩家节点的子组件，也可挂成 Autoload 供全局使用。

**文件位置建议**：`res://systems/combo_system.gd`

#### 完整代码

```gdscript
# res://systems/combo_system.gd
# 连击系统：计数 + 窗口超时归零 + 加成
class_name ComboSystem
extends Node

# ============ 信号 ============
## 连击数变化（count 为当前连击，damage_bonus 为当前伤害加成倍率）
signal combo_increased(count: int, damage_bonus: float)
## 连击归零
signal combo_reset()
## 达到某个里程碑（如 10/25/50 连击）
signal combo_milestone(count: int)

# ============ 可调参数 ============
## 连击窗口：两次命中间隔超过该秒数则连击归零
@export var window_time: float = 2.0
## 每层连击提供的伤害加成（0.05 表示每连击 +5%）
@export var bonus_per_hit: float = 0.05
## 伤害加成上限倍率（3.0 表示最多 3 倍）
@export var max_multiplier: float = 3.0
## 里程碑节点，达到时触发一次特效
@export var milestones: Array[int] = [10, 25, 50, 100]

# ============ 运行时数据 ============
## 当前连击数
var count: int = 0
## 距归零的剩余时间
var _timer: float = 0.0
## 已触发过的里程碑（避免重复触发）
var _fired_milestones: Dictionary = {}

func _process(delta: float) -> void:
	if count <= 0:
		return
	_timer -= delta
	if _timer <= 0.0:
		_reset()

# ---------- 对外接口 ----------
## 命中一次，连击 +1。返回当前的伤害加成倍率，方便调用方直接乘算。
func register_hit() -> float:
	count += 1
	_timer = window_time
	var mult := get_damage_multiplier()
	combo_increased.emit(count, mult)
	_check_milestones()
	return mult

## 当前伤害加成倍率（1.0 表示无加成）
func get_damage_multiplier() -> float:
	var raw := 1.0 + float(count) * bonus_per_hit
	return minf(raw, max_multiplier)

## 连击带来的额外评分（可与基础分相加）
func get_score_bonus(base_score: int) -> int:
	return int(round(float(base_score) * (get_damage_multiplier() - 1.0)))

## 剩余连击时间比例（0~1），供 UI 画一个"连击条"
func window_ratio() -> float:
	if window_time <= 0.0 or count <= 0:
		return 0.0
	return clampf(_timer / window_time, 0.0, 1.0)

## 手动重置
func reset() -> void:
	_reset()

## 手动加长连击窗口（比如打出一记终结技）
func extend_window(extra: float) -> void:
	if count > 0:
		_timer += extra

func _reset() -> void:
	if count == 0:
		return
	count = 0
	_timer = 0.0
	_fired_milestones.clear()
	combo_reset.emit()

func _check_milestones() -> void:
	for m in milestones:
		if count >= m and not _fired_milestones.has(m):
			_fired_milestones[m] = true
			combo_milestone.emit(m)
```

#### 使用方法

1. 保存为 `res://systems/combo_system.gd`。
2. 在玩家节点下新建 `Node` 命名 `ComboSystem`，挂上脚本。
3. 每次命中敌人时调用 `register_hit()`，并把返回值乘到伤害上：

```gdscript
extends CharacterBody2D

@onready var combo: ComboSystem = $ComboSystem

func _ready() -> void:
	combo.combo_increased.connect(_on_combo_increased)
	combo.combo_reset.connect(func(): print("连击断了"))
	combo.combo_milestone.connect(_on_milestone)

func hit_enemy(enemy: Node2D) -> void:
	# 先登记连击，拿到加成倍率
	var mult := combo.register_hit()

	# 构造伤害并按连击加成放大
	var info := DamageInfo.new()
	info.base_damage = 10.0
	var result := DamageCalculator.calculate(info)
	var hp := enemy.get_node_or_null("Health")
	if hp is HealthComponent:
		hp.take_damage(result.damage * mult, {"combo": combo.count})

	# 评分也享受连击加成
	var gained := combo.get_score_bonus(100)
	print("本次得分：", 100 + gained)

func _on_combo_increased(c: int, bonus: float) -> void:
	print("连击 x%d，伤害加成 %.2f 倍" % [c, bonus])

func _on_milestone(c: int) -> void:
	print("达成 %d 连击！播放特效" % c)
	# 这里触发屏幕闪光、音效、飘字等
```

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `window_time` | float | 2.0 | 连击窗口秒数，超时归零 |
| `bonus_per_hit` | float | 0.05 | 每层连击的伤害加成 |
| `max_multiplier` | float | 3.0 | 伤害加成上限倍率 |
| `milestones` | Array[int] | [10,25,50,100] | 里程碑连击数 |
| `count` | int | 运行时 | 当前连击数 |

#### 进阶改造提示

- **加"连击分级"**：按连击数返回 D/C/B/A/S 评级，UI 显示不同颜色。
- **加"连击衰减"**：不用"超时直接归零"，而是每秒缓慢减少 1 点，手感更柔和。
- **加"断连惩罚"**：受到伤害时调用 `reset()`，形成"高风险高回报"的战斗循环。
- **为什么用"窗口 + 超时归零"而不是"永久累加"？** 因为连击的意义在于"鼓励连续进攻"。若无超时，玩家挂机也能攒满连击，奖励失去张力。
- **为什么 `register_hit` 直接返回倍率？** 让调用方一行拿到结果，避免"先登记、再查询"两次调用，减少忘记查询导致的加成失效。

---

## 32.6 模板 T13：TimedAbility 冷却技能系统

### 模板 T13：TimedAbility 冷却技能系统

**用途**：统一管理技能的冷却、消耗与施放条件，提供 `can_cast / cast`、剩余冷却查询（供 UI 画冷却圈）以及"技能就绪"信号。

**依赖**：无（消耗资源时通过 `Callable` 与你的资源系统对接）。

**文件位置建议**：`res://systems/timed_ability.gd`

#### 完整代码

```gdscript
# res://systems/timed_ability.gd
# 冷却技能系统：管理一组技能的冷却、消耗与施放
class_name TimedAbility
extends Node

# ============ 信号 ============
## 成功施放某技能
signal ability_cast(id: String)
## 某技能冷却结束、重新就绪
signal ability_ready(id: String)
## 施放失败（reason 说明原因：cooldown / cost / condition）
signal cast_failed(id: String, reason: String)

# ============ 可调参数 ============
## 技能定义数组，每项形如：
## {"id": "dash", "cooldown": 3.0, "cost": 10.0, "condition": ""}
@export var abilities: Array[Dictionary] = [
	{"id": "dash", "cooldown": 3.0, "cost": 10.0},
	{"id": "fireball", "cooldown": 1.5, "cost": 20.0},
	{"id": "ultimate", "cooldown": 30.0, "cost": 100.0},
]

# ============ 对接资源的回调 ============
## 判断能否支付 cost：签名 func(cost: float) -> bool；留空表示不消耗任何资源
var can_afford: Callable = Callable()
## 实际支付 cost：签名 func(cost: float) -> void
var spend: Callable = Callable()

# ============ 运行时数据 ============
# id → 各技能的运行时状态
var _defs: Dictionary = {}
# id → 剩余冷却秒数
var _remaining: Dictionary = {}
# id → 是否已就绪（用于只发一次 ready 信号）
var _ready_emitted: Dictionary = {}

func _ready() -> void:
	for def in abilities:
		var id: String = def.get("id", "")
		if id == "":
			continue
		_defs[id] = def
		_remaining[id] = 0.0
		_ready_emitted[id] = true

func _process(delta: float) -> void:
	for id in _remaining.keys():
		if _remaining[id] > 0.0:
			_remaining[id] = maxf(_remaining[id] - delta, 0.0)
			if _remaining[id] == 0.0 and not _ready_emitted.get(id, false):
				_ready_emitted[id] = true
				ability_ready.emit(id)

# ---------- 对外接口 ----------
## 能否施放（冷却好了、资源够用）
func can_cast(id: String) -> bool:
	if not _defs.has(id):
		return false
	if _remaining.get(id, 0.0) > 0.0:
		return false
	var cost := float(_defs[id].get("cost", 0.0))
	if cost > 0.0 and can_afford.is_valid() and not can_afford.call(cost):
		return false
	return true

## 尝试施放。成功返回 true，并触发 ability_cast 信号。
func cast(id: String) -> bool:
	if not _defs.has(id):
		cast_failed.emit(id, "unknown")
		return false
	if _remaining.get(id, 0.0) > 0.0:
		cast_failed.emit(id, "cooldown")
		return false

	var cost := float(_defs[id].get("cost", 0.0))
	if cost > 0.0 and can_afford.is_valid() and not can_afford.call(cost):
		cast_failed.emit(id, "cost")
		return false

	# 真正的扣费由外部系统完成，本组件只负责"问一声、然后记账"
	if cost > 0.0 and spend.is_valid():
		spend.call(cost)

	_remaining[id] = float(_defs[id].get("cooldown", 0.0))
	_ready_emitted[id] = false
	ability_cast.emit(id)
	return true

## 剩余冷却秒数
func get_remaining(id: String) -> float:
	return float(_remaining.get(id, 0.0))

## 冷却进度 0~1（0 表示就绪，1 表示刚释放）。供 UI 画冷却圈。
## 为什么用比例而不是剩余秒数？因为不同技能总冷却不同，比例才能统一画图。
func get_cooldown_ratio(id: String) -> float:
	if not _defs.has(id):
		return 0.0
	var total := float(_defs[id].get("cooldown", 0.0))
	if total <= 0.0:
		return 0.0
	return clampf(get_remaining(id) / total, 0.0, 1.0)

func is_ready(id: String) -> bool:
	return _defs.has(id) and get_remaining(id) <= 0.0

## 强制刷新某技能冷却（比如使用道具）
func reset_cooldown(id: String) -> void:
	if not _remaining.has(id):
		return
	_remaining[id] = 0.0
	if not _ready_emitted.get(id, false):
		_ready_emitted[id] = true
		ability_ready.emit(id)

## 减少冷却（比如冷却缩减装备）
func reduce_cooldown(id: String, seconds: float) -> void:
	if not _remaining.has(id):
		return
	_remaining[id] = maxf(_remaining[id] - seconds, 0.0)
```

#### 使用方法

1. 保存为 `res://systems/timed_ability.gd`。
2. 在玩家节点下新建 `Node` 命名 `Abilities`，挂上脚本。
3. 在 Inspector 的 `abilities` 里配置技能表（`id / cooldown / cost`）。
4. 用 T04 的 `StatsComponent` 对接资源消耗：

```gdscript
extends CharacterBody2D

@onready var abilities: TimedAbility = $Abilities
@onready var stats: StatsComponent = $Stats

func _ready() -> void:
	# 用 Stats 里的 "mana" 属性作为技能资源
	abilities.can_afford = func(cost: float) -> bool:
		return stats.get_stat("mana") >= cost
	abilities.spend = func(cost: float) -> void:
		stats.add_modifier("mana", -cost, "add", "ability_cost")

	abilities.ability_cast.connect(_on_cast)
	abilities.ability_ready.connect(func(id): print(id, " 冷却完毕"))

func _unhandled_input(event: InputEvent) -> void:
	if event.is_action_pressed("dash"):
		if abilities.cast("dash"):
			# 真正执行位移
			print("冲刺！")
	if event.is_action_pressed("fireball"):
		abilities.cast("fireball")
```

5. UI 画冷却圈（`TextureProgressBar` 的 `value` 用 `1 - ratio`）：

```gdscript
func _process(_delta: float) -> void:
	$FireballButton.value = (1.0 - abilities.get_cooldown_ratio("fireball")) * 100.0
	$DashButton.disabled = not abilities.is_ready("dash")
```

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `abilities` | Array[Dictionary] | 见代码 | 技能定义表 |
| `abilities[i].id` | String | 必填 | 技能唯一标识 |
| `abilities[i].cooldown` | float | 必填 | 冷却秒数 |
| `abilities[i].cost` | float | 0.0 | 施放消耗 |
| `can_afford` | Callable | 空 | 能否支付：`func(cost) -> bool` |
| `spend` | Callable | 空 | 实际扣费：`func(cost) -> void` |

#### 进阶改造提示

- **加"施放条件"**：在 `can_cast` 里加 `condition` 回调（比如必须在空中、必须有目标），失败时以 `"condition"` 为 reason 发信号。
- **加"充能次数"**：允许技能存储 2 次充能，冷却分别计时。
- **加"冷却缩减属性"**：在设置 `_remaining` 时乘上 `(1 - cdr)`，用 T04 的属性系统统一管理。
- **为什么把"扣费"交给外部 `Callable`？** 因为技能系统不该关心你的资源叫什么（魔法、能量、弹药都可能）。通过回调解耦后，同一个技能组件能接入任意资源系统。
- **为什么就绪要发一次信号，而不是每帧发？** 因为每帧发会让监听方（音效、UI 动画）疯狂重复触发；只在"从冷却转为就绪"的那一刻发一次，才是正确的事件语义。

---

## 32.7 本章小结

1. 行为模板的共同特征是"每帧驱动"：它们大多在 `_physics_process` 里更新位置或状态，因此要特别注意性能与逻辑互斥。
2. T08 巡逻 AI 的三要素是：**路点序列、到达判定、停留等待**，少了任何一个都会显得很"假"。
3. T08 的击退用独立速度向量逐帧衰减实现，能与巡逻逻辑并存而不打架。
4. T09 追击 AI 用"侦测范围 + 视野角度"双重判定，视野判定用**点积**等价于比较夹角余弦，比反三角函数更快更稳。
5. T09 的 `lose_range` 必须大于 `detect_range`，形成"迟滞"，避免边界抖动。
6. T09 在发现目标时暂停巡逻、丢失时恢复巡逻，需要两个 AI 组件之间有明确的开关约定。
7. T10 波次刷怪器的核心是"相位状态机"：`SPAWNING → WAITING_CLEAR → REST`，用相位切换描述整个关卡节奏。
8. T10 在敌人入树后再设置全局位置，并用 `tree_exited` 统计敌人离场，健壮性最好。
9. T11 弹幕发射器支持 single / fan / circle / spiral 四种模式，环形用 `TAU / n` 均分、扇形用 `lerp` 铺开、螺旋用累加角度推进。
10. T11 的对象池把 `instantiate / queue_free` 换成"隐藏 / 复用"，是高频生成场景下的性能关键。
11. T12 连击系统用"窗口 + 超时归零"制造紧张感，并让 `register_hit()` 直接返回伤害倍率，减少调用失误。
12. T12 的里程碑用字典记录"是否已触发"，保证每个里程碑在一次连击周期内只触发一次。
13. T13 技能系统把"冷却记账"与"资源扣费"分离，用 `Callable` 对接任意资源系统，扩展性极强。
14. T13 的"就绪信号只发一次"体现了正确的事件语义：状态**转变**时才发事件，而不是状态**存在**时每帧发。
15. UI 画冷却圈应使用 `get_cooldown_ratio()` 这类 0~1 的比例接口，而不是直接依赖剩余秒数。
16. 组件之间优先用信号通信，但"每帧高频、点对点"的交互（如 AI 控制宿主位移）用直接调用更清晰。
17. 本章模板大量复用了第 31 章的模块：`HealthComponent`、`StatsComponent`、`DamageCalculator`——这正是模块化设计的价值所在。
18. 调参永远优先于改代码：先用 Inspector 把数值调到满意，再考虑是否需要扩展功能。
19. 行为类模块"组合"比"继承"更重要：巡逻 + 追击 + 技能可以拼在同一个敌人身上，各司其职。
20. 至此，第五卷的基础模板库已经搭好骨架。你完全可以把这些模块当作乐高积木，用它们快速拼出一个可玩的原型，再逐步替换成自己打磨过的版本。
---

# 第 33 章：体验模板（手感与反馈类）

> 第 31、32 章我们搭好了"数据与状态"和"行为"两排货架。但从玩家的角度看，游戏好不好玩，往往不取决于"系统对不对"，而取决于"**打起来爽不爽**"。
>
> 这一章就是专门解决"爽不爽"的：屏幕会震、数字会飘、声音会叠、时间会顿、相机会追、画面会闪、设置会被记住。这些东西在专业术语里叫 **Game Feel（游戏手感）** 与 **Feedback（反馈）**。它们不改变任何一条游戏规则，却能让同一套规则产生完全不同的体验。
>
> 一句话总结本章的价值：**规则决定这游戏能不能玩，反馈决定这游戏好不好玩。**

## 33.0 本章模板总览

| 编号 | 模板名 | 解决什么问题 | 是否建议常驻 |
| --- | --- | --- | --- |
| T14 | ScreenShake 屏幕震动 | 打击/爆炸的能量感 | 建议，但要有全局开关 |
| T15 | DamageNumber 伤害飘字 | 让伤害"看得见" | 强烈建议 |
| T16 | AudioManager 音频管理 | 音乐切换、音效重叠、音量分组 | 强烈建议做成 Autoload |
| T17 | HitStop 打击顿帧 | 命中瞬间的"重量感" | 动作类强烈建议 |
| T18 | CameraController 相机控制 | 跟随不晕、有前瞻、有呼吸 | 强烈建议 |
| T19 | ScreenFlash 屏幕闪光 | 受伤/拾取的全屏冲击 | 建议 |
| T20 | SettingsManager 设置持久化 | 玩家关掉游戏后设置还在 | 强烈建议做成 Autoload |

**统一原则**：本章所有模板都遵循一个"反馈三件套"的搭配思路——
1. **视觉**（T14/T15/T18/T19）；
2. **听觉**（T16）；
3. **时间**（T17）。

任何一次"重大事件"（受击、暴击、死亡、拾取），你都应该同时触发**至少两类**反馈。只触发一类，玩家会觉得"软"；三类齐发，就是俗称的"打击感拉满"。

---

## 33.1 模板 T14：ScreenShake 屏幕震动

### 模板 T14：ScreenShake 屏幕震动

**用途**：给相机加一层"可以随时请求短暂抖动"的能力。爆炸、受击、落地、Boss 出场，都调用一句 `shake()` 即可，画面立刻有能量感。

**依赖**：无。直接作为 `Camera2D` 的脚本使用。不需要 Autoload。

**文件位置建议**：`res://scripts/effects/screen_shake.gd`

#### 完整代码

```gdscript
class_name ScreenShake
extends Camera2D

## ============================================================
## 屏幕震动（ScreenShake）
## ------------------------------------------------------------
## 设计要点一：为什么把脚本挂在 Camera2D 上？
##   因为震动本质上就是"让相机不再待在原地"。挂在相机上，
##   谁想震就拿到相机引用调一次 shake()，不需要额外的管理器。
##
## 设计要点二：为什么要维护一个"震动请求列表"？
##   同一帧里可能同时有多个来源请求震动：玩家受击、子弹命中、
##   手雷爆炸。如果只用一个变量保存"当前震动强度"，
##   后一次会直接覆盖前一次，视觉上会"断帧"。
##   所以我们把每次请求都存进数组，最后把它们的偏移量叠加，
##   这样"两个小震动"会自然合成"一个更大的震动"。
##
## 设计要点三：为什么写入 offset 而不是 position？
##   因为 T18 的 CameraController 会写入 global_position（负责跟随），
##   而本模板负责写入 offset（负责抖动）。两者互不打架，
##   可以同时挂在一个相机上：一个管"去哪"，一个管"抖多少"。
## ============================================================

## 总开关。设置界面里加一个"屏幕震动：开/关"的选项，
## 关掉后所有 shake() 调用都会被安静地忽略（而不是报错）。
@export var enabled: bool = true

## 抖动模式：
##   false = 正弦波抖动，画面更顺滑，适合持续性的地震、引擎轰鸣
##   true  = 每帧随机抖动，画面更"脆"，适合短促的打击、枪声
@export var use_random_jitter: bool = false

## 叠加后的最大位移上限（像素）。
## 为什么需要它？因为多个大震动叠加时，位移量会线性增长，
## 不设上限的话画面可能直接飞出可视区域，玩家会"丢失方向感"。
@export var max_total_offset: float = 56.0

## 基准偏移。震动是"叠加"在它上面的。
## 有些游戏想让相机整体偏上一点（给下方留出 UI 空间），
## 就把这里设成 (0, -20) 之类，震动依然会在它附近抖。
var base_offset: Vector2 = Vector2.ZERO

## 正在进行中的震动请求列表。
## 每个元素形如：
## {
##   "time_left": float,   # 剩余时间
##   "duration": float,    # 总时长
##   "amplitude": float,   # 初始最大位移
##   "freq": float,        # 抖动频率
##   "decay": float,       # 衰减指数
##   "seed": float,        # 相位随机种子
## }
var _shakes: Array[Dictionary] = []


func _ready() -> void:
	# 记住编辑器里手调的 offset，作为叠加的基准
	base_offset = offset


## 请求一次震动。
## amplitude 最大位移（像素）：3~6 轻微，8~14 中等，16+ 重击
## duration  持续时间（秒）：0.1~0.2 干脆，0.3~0.5 有余韵
## frequency 抖动频率（次/秒的量级）：20~40 常见
## decay     衰减指数：1.0 线性，2.0 先快后慢（最自然），3.0 更陡
func shake(amplitude: float = 8.0, duration: float = 0.3,
		frequency: float = 28.0, decay: float = 2.0) -> void:
	if not enabled:
		return
	if amplitude <= 0.0 or duration <= 0.0:
		return
	_shakes.append({
		"time_left": duration,
		"duration": duration,
		"amplitude": amplitude,
		"freq": frequency,
		"decay": decay,
		# 随机相位，避免多次震动完全同步导致"机械感"
		"seed": randf() * 1000.0,
	})


## 带方向的定向震动：只朝某个方向抖（例如"被从右边打飞"）。
## 实现上就是在总偏移上再乘一个方向向量。
func shake_dir(direction: Vector2, amplitude: float = 10.0,
		duration: float = 0.25, frequency: float = 30.0) -> void:
	if not enabled or direction == Vector2.ZERO:
		return
	_shakes.append({
		"time_left": duration,
		"duration": duration,
		"amplitude": amplitude,
		"freq": frequency,
		"decay": 2.0,
		"seed": 0.0,
		"dir": direction.normalized(),
	})


## 立刻停止全部震动并复位
func stop_all() -> void:
	_shakes.clear()
	offset = base_offset


## 距离衰减的便捷封装：离相机越远，震动越弱。
## 常用于爆炸——屏幕中间的爆炸强，角落的爆炸弱。
func shake_at(world_position: Vector2, max_distance: float = 600.0,
		amplitude: float = 12.0, duration: float = 0.3) -> void:
	if not enabled:
		return
	var dist := global_position.distance_to(world_position)
	var falloff := clampf(1.0 - dist / max_distance, 0.0, 1.0)
	shake(amplitude * falloff, duration)


func _process(delta: float) -> void:
	if _shakes.is_empty():
		if offset != base_offset:
			offset = base_offset
		return

	var total := Vector2.ZERO

	# 倒序遍历：删除元素时不会打乱后面的索引
	for i in range(_shakes.size() - 1, -1, -1):
		var s: Dictionary = _shakes[i]

		s["time_left"] = float(s["time_left"]) - delta
		var time_left: float = s["time_left"]
		if time_left <= 0.0:
			_shakes.remove_at(i)
			continue

		var duration: float = s["duration"]
		var progress: float = 1.0 - time_left / duration        # 0 → 1
		var falloff: float = pow(1.0 - progress, s["decay"])     # 衰减曲线
		var amp: float = float(s["amplitude"]) * falloff

		var local: Vector2
		if use_random_jitter:
			# 每帧取随机方向：更"炸裂"，但可能显得噪
			local = Vector2(randf_range(-1.0, 1.0), randf_range(-1.0, 1.0)) * amp
		else:
			# 用两条不同频率的正余弦做伪随机轨迹，保证连续、不跳变
			var t: float = duration - time_left
			var phase: float = t * float(s["freq"]) + float(s["seed"])
			local = Vector2(sin(phase), cos(phase * 1.37)) * amp

		# 定向震动：把无方向的抖动投影到指定方向上
		if s.has("dir"):
			local = s["dir"] * absf(local.length())

		total += local

	# 位移限幅
	if total.length() > max_total_offset:
		total = total.normalized() * max_total_offset

	offset = base_offset + total
```

#### 使用方法

1. 在场景里选中你的 `Camera2D` 节点（没有就右键玩家 → Add Child Node → `Camera2D`）。
2. 在属性面板底部找到 **Script** → 点击 **New Script** → 语言选 `GDScript`，路径填 `res://scripts/effects/screen_shake.gd`，把上面的代码整段粘进去保存。
3. 回到编辑器，点右上角 **运行（F5）**，确认没有报错。此时相机应该保持静止（没有震动请求）。
4. 写一个触发脚本，例如挂在玩家身上：

```gdscript
extends CharacterBody2D

@onready var camera: ScreenShake = $Camera2D

func _input(event: InputEvent) -> void:
	# 空格键 = 模拟"被打了一下"
	if event.is_action_pressed("ui_accept"):
		camera.shake(10.0, 0.25, 30.0, 2.0)

	# 回车键 = 模拟"旁边有爆炸"
	if event.is_action_pressed("ui_select"):
		camera.shake_at(global_position + Vector2(200, 0), 600.0, 16.0, 0.4)
```

5. 运行后按空格/回车，观察画面抖动。如果抖动方向感太"飘"，把 `use_random_jitter` 关掉；如果嫌不够猛，把 `amplitude` 提到 16 以上。
6. 在设置界面里加一个 `CheckButton`，把它的 `toggled` 信号连到 `camera.enabled = pressed`，就完成了"屏幕震动开关"。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 | 调参方向 |
| --- | --- | --- | --- | --- |
| `enabled` | `bool` | `true` | 总开关 | 设置界面关掉它 |
| `use_random_jitter` | `bool` | `false` | 随机抖动 / 正弦抖动 | 打击用 `true`，地震用 `false` |
| `max_total_offset` | `float` | `56.0` | 叠加位移上限（像素） | 屏幕小就调小 |
| `base_offset` | `Vector2` | `(0,0)` | 震动叠加的基准偏移 | 常在 `_ready` 自动读取 |
| `amplitude`（入参） | `float` | `8.0` | 最大位移 | 3~6 轻，8~14 中，16+ 重 |
| `duration`（入参） | `float` | `0.3` | 持续秒数 | 0.1 干脆，0.4 有余韵 |
| `frequency`（入参） | `float` | `28.0` | 抖动频率 | 越大越"密" |
| `decay`（入参） | `float` | `2.0` | 衰减指数 | 1 线性，2 自然，3 陡降 |

#### 进阶改造提示

- **做成"冲击波"**：把 `shake_at` 与一个逐渐扩大的 `Sprite2D` 光圈绑定，光圈到哪、震到哪。
- **加优先级**：给每个请求加一个 `priority` 字段，只保留最高优先级的那一个（避免 Boss 大招被小怪受击"盖住"）。
- **用噪声替代正弦**：接一个 `FastNoiseLite` 实例，用 `get_noise_1d(t * freq)` 取值，画面会更"有机"，适合长时间的地震。
- **无头模式兼容**：如果你要做自动化测试，运行时用 `shake()` 之外的路径都会正常，但相机不在场景里时请先 `if camera and camera.enabled:` 判空，避免空引用。
- **别忘了无障碍**：有些玩家对屏幕震动非常敏感（晕动症）。把它做成可调等级（关/弱/中/强）而不是只给一个开关，会显著提升体验。

---

## 33.2 模板 T15：DamageNumber 伤害飘字

### 模板 T15：DamageNumber 伤害飘字

**用途**：在敌人头顶弹出一个数字，向上飘动、逐渐透明。暴击时数字更大、颜色不同。配套一个**对象池**，避免每打一下都 `instantiate()` 造成卡顿。

**依赖**：需要一个 `Label` 场景（下面给出创建步骤），以及一个 `Node2D` 作为对象池的宿主节点。不依赖任何 Autoload。

**文件位置建议**：脚本放在 `res://scripts/effects/damage_number.gd` 与 `res://scripts/effects/damage_number_pool.gd`，场景放在 `res://effects/damage_number.tscn`。

#### 完整代码

**第一部分：单个飘字 `damage_number.gd`**

```gdscript
class_name DamageNumber
extends Label

## ============================================================
## 伤害飘字
## ------------------------------------------------------------
## 设计要点一：为什么继承 Label 而不是 Sprite2D？
##   Label 自带字体、字号、描边、对齐等主题能力，改个 value 就能显示，
##   不需要为每个数字准备贴图，也不需要自己拼字。
##
## 设计要点二：为什么用 Tween 而不是自己写 _process 插值？
##   Tween 由引擎管理，可以并行、可以链式、可以随时 kill()。
##   自己写插值要维护一堆进度变量，且容易和对象池的"复用"打架。
##
## 设计要点三：为什么保留一个 _start_global 记录起点？
##   因为对象池会复用同一个节点：节点被"释放"时可能停在半空中，
##   下次被 acquire 时位置是不确定的。play() 里重新抓一次起点即可。
## ============================================================

## 飘字"生命"总时长（秒）
@export var lifetime: float = 0.8

## 向上飘动的距离（像素）
@export var rise_distance: float = 48.0

## 左右随机散开的范围（像素）。
## 设计原因：连续命中时数字如果全部沿同一条垂线上升，会叠成一坨看不清。
@export var horizontal_spread: float = 22.0

## 三种颜色的语义区分
@export var normal_color: Color = Color(1.0, 1.0, 1.0)
@export var crit_color: Color = Color(1.0, 0.85, 0.2)
@export var heal_color: Color = Color(0.45, 1.0, 0.55)

## 字号
@export var normal_font_size: int = 16
@export var crit_font_size: int = 30

## 描边粗细。描边是"任何背景上都看得清"的关键，别省。
@export var outline_size: int = 5

## Label 的固定尺寸（用于把数字中心对齐到世界坐标）
@export var label_size: Vector2 = Vector2(200, 48)

## 动画结束时通知对象池
signal finished

var _tween: Tween
var _start_global: Vector2 = Vector2.ZERO


func _ready() -> void:
	horizontal_alignment = HORIZONTAL_ALIGNMENT_CENTER
	vertical_alignment = VERTICAL_ALIGNMENT_CENTER
	# 忽略鼠标，否则全屏飘字会挡住按钮点击
	mouse_filter = Control.MOUSE_FILTER_IGNORE
	# 黑色描边 + 主题覆盖，保证在亮色/暗色背景上都能读
	add_theme_color_override("font_outline_color", Color(0, 0, 0, 0.9))
	add_theme_constant_override("outline_size", outline_size)


## 播一次飘字。由对象池在设置好 global_position 之后调用。
## value           要显示的数字
## is_crit         是否暴击（决定字号、颜色、放大回弹）
## color_override  传入非透明颜色时覆盖默认配色（例如治疗用绿字）
func play(value: int, is_crit: bool = false, color_override: Color = Color(0, 0, 0, 0)) -> void:
	text = str(value)

	var use_color := crit_color if is_crit else normal_color
	if color_override.a > 0.0:
		use_color = color_override
	add_theme_color_override("font_color", use_color)
	add_theme_font_size_override("font_size", crit_font_size if is_crit else normal_font_size)

	# 复位视觉状态（因为可能是从对象池里捞出来的"旧节点"）
	modulate.a = 1.0
	size = label_size
	pivot_offset = size * 0.5

	# Label 的 position 指的是"左上角"，而调用方传进来的是"数字中心"。
	# 这里整体挪半个尺寸，让文字中心正好落在世界坐标上。
	var center := global_position
	global_position = center - size * 0.5

	_start_global = global_position
	scale = Vector2.ONE * (1.45 if is_crit else 1.0)

	# 上一轮动画可能还没播完（节点被提前复用），先杀掉
	if _tween and _tween.is_valid():
		_tween.kill()

	var drift := Vector2(
		randf_range(-horizontal_spread, horizontal_spread),
		-rise_distance
	)

	_tween = create_tween()
	_tween.set_parallel(true)   # 位移、透明、缩放三件事同时进行
	_tween.tween_property(self, "global_position", _start_global + drift, lifetime) \
		.set_trans(Tween.TRANS_CUBIC).set_ease(Tween.EASE_OUT)
	_tween.tween_property(self, "modulate:a", 0.0, lifetime) \
		.set_trans(Tween.TRANS_QUAD).set_ease(Tween.EASE_IN)

	if is_crit:
		# 暴击先"炸开"再回弹到正常大小
		_tween.tween_property(self, "scale", Vector2.ONE, 0.22) \
			.set_trans(Tween.TRANS_BACK).set_ease(Tween.EASE_OUT)

	# chain() 让下一步等前面所有并行动画结束
	_tween.chain().tween_callback(_on_animation_done)


func _on_animation_done() -> void:
	finished.emit()
```

**第二部分：对象池 `damage_number_pool.gd`**

```gdscript
class_name DamageNumberPool
extends Node2D

## ============================================================
## 伤害飘字对象池
## ------------------------------------------------------------
## 设计要点一：为什么需要池？
##   战斗中每秒可能产生几十个飘字。每次 instantiate() + free()
##   都会触发内存分配与场景树改动，在低端设备上会造成掉帧尖刺。
##   池化后节点只创建一次，之后只做 show/hide 与 Tween 重置。
##
## 设计要点二：为什么溢出不"等待"，而是"复用最旧的一个"？
##   飘字属于"过期即无用"的纯反馈物，玩家不会因为少了 1 个飘字
##   而损失游戏信息。所以溢出时直接抢最老的那个来用，保证
##   最新、最关键的一次伤害一定能显示出来。
##
## 设计要点三：为什么池是 Node2D？
##   因为我们要把飘字加为它的子节点，从而使用"局部坐标 = 世界坐标"
##   的便利（池默认放在原点）。若池有位移，spawn 里用 global_position
##   也依然正确。
## ============================================================

## 飘字场景（res://effects/damage_number.tscn）
@export var number_scene: PackedScene

## 预热数量：进游戏就造好这么多，避免第一次战斗时才卡一下
@export var initial_size: int = 24

## 池容量上限
@export var max_size: int = 160

## 飘字统一层级（越大越靠前）
@export var z_layer: int = 100

var _free: Array[DamageNumber] = []
var _used: Array[DamageNumber] = []


func _ready() -> void:
	for i in initial_size:
		if _free.size() + _used.size() >= max_size:
			break
		if number_scene == null:
			push_warning("DamageNumberPool: 未设置 number_scene")
			return
		_free.append(_create_number())


func _create_number() -> DamageNumber:
	var n: DamageNumber = number_scene.instantiate()
	n.z_index = z_layer
	# 绑定完成信号。用 bind 把节点本身作为参数传回来，
	# 这样池不需要去猜"是哪个节点结束了"。
	n.finished.connect(_on_number_finished.bind(n))
	add_child(n)
	n.hide()
	return n


## 对外唯一接口：在世界坐标 world_position 处弹出一个数字。
func spawn(world_position: Vector2, value: int,
		is_crit: bool = false, color_override: Color = Color(0, 0, 0, 0)) -> void:
	if number_scene == null:
		return
	var n := _obtain()
	n.global_position = world_position
	n.show()
	_used.append(n)
	n.play(value, is_crit, color_override)


## 取一个可用节点（优先空闲，其次新建，最后抢最旧的）
func _obtain() -> DamageNumber:
	if not _free.is_empty():
		return _free.pop_back()

	if _used.size() + _free.size() < max_size:
		return _create_number()

	# 溢出：直接没收最老的那个（它还在播动画，play() 会 kill 掉旧 Tween）
	return _used.pop_front()


func _on_number_finished(n: DamageNumber) -> void:
	n.hide()
	var idx := _used.find(n)
	if idx != -1:
		_used.remove_at(idx)
	_free.append(n)


## 调试用：输出当前池状态
func debug_stats() -> void:
	print("DamageNumberPool  free=%d  used=%d  total=%d"
		% [_free.size(), _used.size(), _free.size() + _used.size()])
```

#### 使用方法

1. **造飘字场景**：右键 `res://effects/` 文件夹 → **New Scene** → 根节点选 `Label` → 保存为 `damage_number.tscn`。
2. 选中根节点 Label，在属性面板里：**Horizontal Alignment** 设为 `Center`，**Vertical Alignment** 设为 `Center`，**Text** 随便填 `0`（运行时会被覆盖）。再用属性面板右侧的 **Attach Script** 挂上 `damage_number.gd`。
3. **造池节点**：在关卡场景（例如 `Main.tscn`）的根节点下新建一个 `Node2D`，命名为 `DamageNumbers`，把 `damage_number_pool.gd` 挂上去。
4. 在 Inspector 里把 **Number Scene** 拖成刚才的 `damage_number.tscn`（从文件系统面板拖到该属性上）。
5. 在敌人受击逻辑里调用：

```gdscript
extends Node2D

@onready var pool: DamageNumberPool = $DamageNumbers

func _ready() -> void:
	# 预热（可选，也可以让 _ready 自动做）
	pass

func take_hit(damage: int) -> void:
	var is_crit := randf() < 0.25          # 25% 暴击率
	var final_damage := damage * (2 if is_crit else 1)
	pool.spawn(global_position + Vector2(0, -24), final_damage, is_crit)

	# 治疗时用绿色覆盖色
	# pool.spawn(global_position + Vector2(0, -24), 30, false, Color(0.45, 1.0, 0.55))
```

6. 运行，点击/攻击敌人，观察数字。确认：
   - 连续命中时数字左右散开、不重叠成一坨；
   - 暴击数字明显更大、颜色偏金黄、有"炸开回弹"的动感；
   - 长时间战斗后按 `debug_stats()` 看到 `total` 不会突破 `max_size`。

#### 可调参数说明

| 参数 | 所在脚本 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `lifetime` | DamageNumber | `0.8` | 数字存活秒数 |
| `rise_distance` | DamageNumber | `48.0` | 上飘距离（像素） |
| `horizontal_spread` | DamageNumber | `22.0` | 左右散开范围 |
| `normal_color` / `crit_color` / `heal_color` | DamageNumber | 白 / 金 / 绿 | 三种配色 |
| `normal_font_size` / `crit_font_size` | DamageNumber | `16` / `30` | 两种字号 |
| `outline_size` | DamageNumber | `5` | 描边宽度 |
| `label_size` | DamageNumber | `(200,48)` | 固定尺寸，用于居中对齐 |
| `number_scene` | Pool | `null` | 必填，指向飘字场景 |
| `initial_size` | Pool | `24` | 预热数量 |
| `max_size` | Pool | `160` | 池容量上限 |
| `z_layer` | Pool | `100` | 层级 |

#### 进阶改造提示

- **加图标**：把根节点从 `Label` 换成 `HBoxContainer`（里面放一个 `TextureRect` 加一个 `Label`），就能显示"剑 + 数字""火 + 数字"。
- **支持小数**：把 `play` 的 `value` 改成 `float`，用 `"%.1f" % value` 格式化。
- **连击累加**：给池加一个"200ms 内同位置的飘字合并"逻辑，重复命中时不弹新数字，而是让已有数字数值累加并放一个轻微缩放脉冲——这是很多手游的做法。
- **屏幕外剔除**：在 `spawn` 里用 `get_viewport_rect().grow(64).has_point(world_position)` 判断，屏幕外直接不生成，省性能。
- **注意 `Control` 与 `Node2D` 混用的坑**：飘字作为 `Node2D` 的子节点，`z_index` 与 `CanvasItem` 的绘制顺序一致，但如果你之后把池塞进 `CanvasLayer`，坐标系会改变，此时请统一改用 `global_position`（本模板已经这么做了）。

---

## 33.3 模板 T16：AudioManager 音频管理

### 模板 T16：AudioManager 音频管理

**用途**：一个全局音频总管。把声音按总线分成"音乐 / 音效 / UI"三组，分别控音量；音效可重叠播放（走播放器池）；音乐切换时自动淡入淡出。

**依赖**：建议做成 **Autoload**。可选依赖"音频总线布局"（Audio Bus Layout），没有也能跑（会自动回退到 Master）。

**文件位置建议**：`res://autoload/audio_manager.gd`

#### 完整代码

```gdscript
extends Node

## ============================================================
## 音频管理器（Autoload 名称建议：AudioManager）
## ------------------------------------------------------------
## 设计要点一：为什么用"总线（Bus）"而不是给每个音效一个音量变量？
##   总线是引擎级的混音通道，音量控制、静音、效果器（混响/压缩）
##   都在 AudioServer 层面完成，性能几乎为零，而且天然支持
##   "音乐淡出同时音效不受影响"这类需求。
##
## 设计要点二：为什么音乐用两个 AudioStreamPlayer 而不是一个？
##   单播放器切歌必须"先停再播"，中间一定有一段空白，
##   做不到交叉淡入淡出。用 A/B 两个播放器互相接力，
##   一首淡出的同时另一首淡入，听感才连贯。
##
## 设计要点三：为什么音效要用播放器池？
##   同一个音效在 0.1 秒内可能响 5 次（连发武器、连续拾取）。
##   单个 AudioStreamPlayer 播放新声音时会打断上一个，
##   池化后每个都在自己的播放器上响，才能真正"叠加"。
##
## 设计要点四：为什么要做总线回退？
##   本项目可能还没在"音频总线布局"里建 Music/SFX/UI。
##   直接 p.bus = "SFX" 会得到一个无效总线，虽然不崩，
##   但音量控制会全部失效。回退到 Master 至少能听得到声音。
## ============================================================

const BUS_MASTER := "Master"
const BUS_MUSIC := "Music"
const BUS_SFX := "SFX"
const BUS_UI := "UI"

## 音效播放器池大小。12 对于大多数 2D 游戏足够；
## 弹幕游戏建议提到 24~32。
@export var sfx_pool_size: int = 12

## 音乐淡入淡出默认时长
@export var default_fade_time: float = 1.0

# ---- 内部状态 ----
var _music_a: AudioStreamPlayer
var _music_b: AudioStreamPlayer
var _music_active: AudioStreamPlayer
var _music_tween: Tween

var _sfx_players: Array[AudioStreamPlayer] = []
var _sfx_cursor: int = 0

var _ui_player: AudioStreamPlayer

## 记录每个总线的线性音量（0~1），供设置界面读回
var _volumes: Dictionary = {
	BUS_MASTER: 1.0,
	BUS_MUSIC: 1.0,
	BUS_SFX: 1.0,
	BUS_UI: 1.0,
}


func _ready() -> void:
	# 音乐双缓冲
	_music_a = _make_player(BUS_MUSIC)
	_music_b = _make_player(BUS_MUSIC)
	_music_active = _music_a

	# 音效播放器池
	for i in sfx_pool_size:
		_sfx_players.append(_make_player(BUS_SFX))

	# UI 单独一个播放器：UI 音效几乎不会重叠，不需要池
	_ui_player = _make_player(BUS_UI)


func _make_player(bus: String) -> AudioStreamPlayer:
	var p := AudioStreamPlayer.new()
	p.bus = _resolve_bus(bus)
	add_child(p)
	return p


## 总线不存在时回退到 Master，避免"点了没声音还查不出原因"
func _resolve_bus(bus: String) -> String:
	return bus if AudioServer.get_bus_index(bus) != -1 else BUS_MASTER


# ============================================================
# 音效
# ============================================================

## 播放一次音效（可与自身重叠）。
## pitch_random 传入 0.1 表示音高在 ±10% 内随机，
## 这是避免"同一句脚步声听 100 遍变腻"的最低成本技巧。
func play_sfx(stream: AudioStream, volume_db: float = 0.0,
		pitch: float = 1.0, pitch_random: float = 0.0) -> void:
	if stream == null:
		return
	var p := _next_sfx_player()
	p.stream = stream
	p.volume_db = volume_db
	p.pitch_scale = pitch * (1.0 + randf_range(-pitch_random, pitch_random))
	p.play()


## 播放 UI 音效（按钮点击、翻页）。统一走 UI 总线，
## 这样玩家可以在设置里"单独关掉 UI 音效"。
func play_ui(stream: AudioStream, volume_db: float = 0.0) -> void:
	if stream == null:
		return
	_ui_player.stream = stream
	_ui_player.volume_db = volume_db
	_ui_player.play()


## 找到一个可用的播放器：优先空闲，全忙则轮转抢占。
## 注意这里不做"打断最轻"的智能判断——那种策略需要额外记账，
## 对 2D 游戏收益很小，轮转已经足够。
func _next_sfx_player() -> AudioStreamPlayer:
	var count := _sfx_players.size()
	if count == 0:
		# 极端情况：sfx_pool_size 被设成 0，兜底补一个
		_sfx_players.append(_make_player(BUS_SFX))
		count = 1

	for i in count:
		var idx := (_sfx_cursor + i) % count
		var p := _sfx_players[idx]
		if not p.playing:
			_sfx_cursor = (idx + 1) % count
			return p

	var fallback := _sfx_players[_sfx_cursor]
	_sfx_cursor = (_sfx_cursor + 1) % count
	return fallback


# ============================================================
# 音乐
# ============================================================

## 播放背景音乐（带交叉淡入淡出）。
## 如果当前正在播的就是同一首，则什么都不做——
## 这一条很重要：很多人的代码在"进入战斗区域"的 _ready 里调 play_music，
## 结果每次切场景地图 BGM 都被打断重头播，听感极差。
func play_music(stream: AudioStream, fade_time: float = -1.0,
		volume_db: float = 0.0) -> void:
	if stream == null:
		return
	if fade_time < 0.0:
		fade_time = default_fade_time

	if _music_active.playing and _music_active.stream == stream:
		return

	# 挑一个"不是当前活跃"的播放器来接棒
	var incoming := _music_b if _music_active == _music_a else _music_a
	incoming.stream = stream
	incoming.volume_db = -60.0   # 从"几乎听不见"开始
	incoming.play()

	if _music_tween and _music_tween.is_valid():
		_music_tween.kill()

	_music_tween = create_tween()
	_music_tween.set_parallel(true)
	_music_tween.tween_property(incoming, "volume_db", volume_db, fade_time) \
		.set_trans(Tween.TRANS_SINE)

	var outgoing := _music_active
	if outgoing.playing:
		_music_tween.tween_property(outgoing, "volume_db", -60.0, fade_time) \
			.set_trans(Tween.TRANS_SINE)

	# 等所有并行动画结束，再去停掉旧播放器
	_music_tween.chain().tween_callback(_finish_music_switch.bind(incoming, outgoing))

	# 先更新活跃指针，避免淡出期间再次调用 play_music 时选错播放器
	_music_active = incoming


func _finish_music_switch(new_active: AudioStreamPlayer,
		old_active: AudioStreamPlayer) -> void:
	if old_active == new_active:
		return
	if old_active.playing:
		old_active.stop()
	old_active.volume_db = 0.0


## 停止音乐（带淡出）
func stop_music(fade_time: float = 1.0) -> void:
	if not _music_active.playing:
		return
	if _music_tween and _music_tween.is_valid():
		_music_tween.kill()
	var outgoing := _music_active
	_music_tween = create_tween()
	_music_tween.tween_property(outgoing, "volume_db", -60.0, fade_time)
	_music_tween.tween_callback(outgoing.stop)


# ============================================================
# 音量
# ============================================================

## 设置某个总线的线性音量（0.0 ~ 1.0）。
## 说明：linear_to_db(0) 会得到 -inf，所以先夹一个极小值。
func set_bus_volume(bus: String, linear: float) -> void:
	linear = clampf(linear, 0.0, 1.0)
	_volumes[bus] = linear
	var idx := AudioServer.get_bus_index(bus)
	if idx == -1:
		return
	AudioServer.set_bus_mute(idx, linear <= 0.001)
	AudioServer.set_bus_volume_db(idx, linear_to_db(maxf(linear, 0.001)))


func get_bus_volume(bus: String) -> float:
	return float(_volumes.get(bus, 1.0))


# 三个便捷封装，给设置界面直接调用
func set_music_volume(v: float) -> void:
	set_bus_volume(BUS_MUSIC, v)

func set_sfx_volume(v: float) -> void:
	set_bus_volume(BUS_SFX, v)

func set_ui_volume(v: float) -> void:
	set_bus_volume(BUS_UI, v)


## 一次性把所有已记录的音量写回引擎（切换音频设备后调用）
func apply_all_volumes() -> void:
	for bus in _volumes.keys():
		set_bus_volume(bus, float(_volumes[bus]))
```

#### 使用方法

1. **（推荐）创建音频总线**：菜单 **Project → Tools → Audio Bus Layout**（或在底部面板切到 Audio），在 `Master` 下面添加三条总线，分别改名 `Music`、`SFX`、`UI`。保存后会在项目里生成 `default_bus_layout.tres`。**不做这步也能运行**，只是三种音量会一起变化。
2. **注册 Autoload**：菜单 **Project → Project Settings → Autoload**，把 `res://autoload/audio_manager.gd` 添加进去，节点名填 `AudioManager`。注意勾选 **Enable**。
3. **放置音乐文件**：把 `res://audio/bgm_*.ogg`、`res://audio/sfx_*.wav` 准备好。建议在音效文件的导入设置里取消勾选 **Loop**（音效不该循环），BGM 的 `.ogg` 导入面板里勾选 **Loop**。
4. **播放音乐**：

```gdscript
extends Node2D

const BGM_FIELD := preload("res://audio/bgm_field.ogg")
const BGM_BOSS := preload("res://audio/bgm_boss.ogg")
const SFX_HIT := preload("res://audio/sfx_hit.wav")

func _ready() -> void:
	# 进入场景就播，重复进入不会打断（内部有"同一首不重播"判断）
	AudioManager.play_music(BGM_FIELD, 1.5, -6.0)

func _on_boss_appear() -> void:
	AudioManager.play_music(BGM_BOSS, 0.6)

func _on_player_hit() -> void:
	# 每次随机音高 ±10%，避免听腻
	AudioManager.play_sfx(SFX_HIT, 0.0, 1.0, 0.1)
```

5. **音量滑块**：给 `HSlider`（`min_value = 0`，`max_value = 1`，`step = 0.01`）的 `value_changed` 接上：

```gdscript
func _on_music_slider_value_changed(value: float) -> void:
	AudioManager.set_music_volume(value)
```

6. 运行后确认：连开十枪，音效是叠加的而不是互相打断；切 BGM 时没有生硬的断点；把音乐音量拉到 0 时音效仍在响。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `sfx_pool_size` | `int` | `12` | 音效播放器池大小，弹幕游戏建议 24~32 |
| `default_fade_time` | `float` | `1.0` | 音乐默认淡入淡出秒数 |
| `BUS_MASTER/MUSIC/SFX/UI` | `String` | — | 总线名常量，必须与音频布局里一致 |
| `play_sfx(volume_db)` | `float` | `0.0` | 单次音效增益（dB） |
| `play_sfx(pitch_random)` | `float` | `0.0` | 音高随机比例，0.1 = ±10% |
| `play_music(volume_db)` | `float` | `0.0` | 音乐增益（dB） |

#### 进阶改造提示

- **音效限流（voice limiting）**：给 `play_sfx` 加一个"同一帧同一音效最多播 N 次"的计数器，防止机枪一秒触发 200 次爆音。
- **随机音效组**：封装 `play_sfx_random(paths: Array[AudioStream])`，从 3~5 个相似音效里随机取一个，脚步、击打声会自然得多。
- **立体声定位**：把 `AudioStreamPlayer` 换成 `AudioStreamPlayer2D`，并给 `play_sfx` 加一个 `world_position` 参数，音效就会随距离衰减、随左右声道偏移，空间感立刻上一个档次。
- **暂停处理**：`AudioStreamPlayer` 的 `process_mode` 默认跟随树暂停。如果游戏暂停时你想让 BGM 继续（或者相反），在 `_make_player` 里显式设置 `p.process_mode = Node.PROCESS_MODE_ALWAYS`。
- **资源泄漏提醒**：`_sfx_players` 是 Autoload 的成员，`AudioStreamPlayer` 是它的子节点，二者生命周期一致，不会泄漏。**不要**在 `play_sfx` 里每次 `new()` 一个播放器然后忘记 `queue_free()`，那是最常见的音频内存泄漏来源。

---

## 33.4 模板 T17：HitStop 打击顿帧

### 模板 T17：HitStop 打击顿帧

**用途**：命中瞬间把游戏整体时间"踩一脚刹车"（通常 40~100 毫秒），让这一次攻击在玩家感知上"变重"。这是动作游戏最核心的手感技巧之一。

**依赖**：建议做成 **Autoload**，因为它是全局唯一的。

**文件位置建议**：`res://autoload/hit_stop.gd`

#### 完整代码

```gdscript
extends Node

## ============================================================
## 打击顿帧（Autoload 名称建议：HitStop）
## ------------------------------------------------------------
## 设计要点一：为什么用 Engine.time_scale 而不是 get_tree().paused？
##   paused 是"全停"，会连输入、UI、动画一起冻住，且需要到处设
##   process_mode，维护成本极高。time_scale 只缩放"时间流速"，
##   输入依然可读、UI 依然可点，只是世界走得慢。
##
## 设计要点二：为什么必须用 ignore_time_scale = true 的计时器？
##   如果用一个普通的 Timer 或 create_timer(duration, ...) 来恢复时间，
##   当 time_scale = 0 时，那个计时器的倒计时也被冻住了——
##   它会永远不触发，游戏就彻底卡死。
##   Godot 4 的 SceneTree.create_timer 签名是：
##     create_timer(time_sec, process_always = true,
##                  process_in_physics = false, ignore_time_scale = false)
##   我们把最后一个参数设为 true，它就走"真实时间"，
##   不受 time_scale 影响，因此一定能恢复。
##
## 设计要点三：为什么要"计数"而不是直接赋值？
##   一次重击中，剑、火花、顿帧可能各自调一次 freeze()。
##   如果后一次直接覆盖前一次，恢复时就会提前把时间放回去，
##   顿帧时间被"缩短"。用 _active 计数，只有全部到期才恢复。
## ============================================================

## 顿帧期间的时间缩放值。0.0 = 完全静止，0.1 = 极慢动作。
## 实际项目里 0.0 和 0.05 都很常见，0.0 更"硬"。
@export var freeze_scale: float = 0.0

## 是否允许叠加（多次 freeze 会延长总时长）。
## 关闭后，顿帧期间的新请求会被忽略。
@export var allow_stacking: bool = true

## 正在进行的顿帧计数
var _active: int = 0

## 进入顿帧前保存的时间缩放值，用于恢复
var _saved_time_scale: float = 1.0

## 慢动作状态（与顿帧共用时间缩放，但语义不同）
var _slow_active: bool = false
var _slow_saved: float = 1.0


## 触发一次顿帧。
## duration 秒数：0.04~0.06 轻击，0.08~0.12 重击，0.2+ 处决
func freeze(duration: float = 0.08, scale_value: float = -1.0) -> void:
	if duration <= 0.0:
		return
	if scale_value < 0.0:
		scale_value = freeze_scale

	if _active > 0 and not allow_stacking:
		return

	# 只在"从零开始"的那一刻保存原始值，
	# 否则第二次 freeze 会把已经被改小的值当成"原始值"存下来。
	if _active == 0:
		_saved_time_scale = Engine.time_scale
		Engine.time_scale = scale_value

	_active += 1

	# 关键：process_always = true（暂停时也走），
	#       process_in_physics = false，
	#       ignore_time_scale = true（不受 time_scale 影响）
	get_tree().create_timer(duration, true, false, true).timeout.connect(_on_freeze_timeout)


func _on_freeze_timeout() -> void:
	_active -= 1
	if _active > 0:
		return
	_active = 0
	if _slow_active:
		return   # 慢动作接管时间缩放，别抢它的控制权
	Engine.time_scale = _saved_time_scale


## 慢动作（子弹时间）：进入一段时间变慢，结束后自动恢复。
## 与 freeze 的区别：freeze 极短且接近"停"，慢动作较长且"能看清"。
func slow_motion(duration: float, scale_value: float = 0.3) -> void:
	if duration <= 0.0:
		return
	_slow_saved = Engine.time_scale
	_slow_active = true
	Engine.time_scale = scale_value
	get_tree().create_timer(duration, true, false, true).timeout.connect(_on_slow_timeout)


func _on_slow_timeout() -> void:
	_slow_active = false
	if _active > 0:
		return
	Engine.time_scale = _slow_saved


## 强制复位（切场景、游戏结束、读档时调用，防止时间比例卡在异常值）
func reset() -> void:
	_active = 0
	_slow_active = false
	Engine.time_scale = 1.0


func get_is_frozen() -> bool:
	return _active > 0
```

#### 使用方法

1. **注册 Autoload**：**Project → Project Settings → Autoload**，添加 `res://autoload/hit_stop.gd`，节点名填 `HitStop`。
2. **检查物理帧率**：确认 **Project Settings → Physics → Common → Physics Ticks Per Second** 是 60（默认）。顿帧依赖物理帧推进，帧率过低时顿帧会显得不均匀。
3. **在命中处调用**：

```gdscript
extends Node2D

const SFX_HEAVY := preload("res://audio/sfx_heavy_hit.wav")

func deal_damage(target: Node2D, amount: int, is_crit: bool) -> void:
	# 1) 视觉：飘字
	$DamageNumbers.spawn(target.global_position + Vector2(0, -24), amount, is_crit)

	# 2) 听觉
	AudioManager.play_sfx(SFX_HEAVY, -2.0, 1.0, 0.08)

	# 3) 时间：暴击顿得更久
	HitStop.freeze(0.12 if is_crit else 0.06)

	# 4) 镜头
	$Camera2D.shake(14.0 if is_crit else 8.0, 0.2)
```

4. **Boss 死亡时来一发慢动作**：

```gdscript
func _on_boss_died() -> void:
	HitStop.slow_motion(1.5, 0.25)   # 1.5 秒内时间流速降到 25%
	$Camera2D.shake(20.0, 0.6)
```

5. **切场景时务必复位**：

```gdscript
func _exit_tree() -> void:
	HitStop.reset()
```

6. 运行并测试。**必须检查的一件事**：把 `HitStop.freeze(0.1, 0.0)` 写死在一个按键上，连按多次，确认游戏最终一定会恢复（`Engine.time_scale` 回到 1.0），而不是永久卡死。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `freeze_scale` | `float` | `0.0` | 顿帧期间的时间缩放；0 为全停，0.05~0.15 为"微动" |
| `allow_stacking` | `bool` | `true` | 多次顿帧是否叠加时长 |
| `duration`（入参） | `float` | `0.08` | 顿帧秒数 |
| `scale_value`（入参） | `float` | `-1` | 本次顿帧的时间缩放，-1 表示用 `freeze_scale` |
| `slow_motion` 的 `duration` | `float` | — | 慢动作持续秒数 |
| `slow_motion` 的 `scale` | `float` | `0.3` | 慢动作的时间缩放 |

#### 进阶改造提示

- **顿帧时长自动计算**：`freeze(0.04 + damage * 0.002)`，伤害越高顿得越久，手感会随数值成长而升级。
- **只冻敌人不冻玩家**：这需要给玩家节点设 `process_mode = Node.PROCESS_MODE_ALWAYS`，然后调用 `get_tree().paused = true` 而不是 `time_scale`。两条路线各有取舍——`time_scale` 简单通用，`paused` 可控粒度更细。**不要同时用两套机制**，会互相打架。
- **和音频的联动**：顿帧时给 BGM 加一个短暂的音高下滑（`AudioServer.set_bus_effect` + `AudioEffectPitchShift`），打击感会被进一步放大。这是很多主机动作游戏的隐藏技巧。
- **注意 UI 动画**：顿帧会让基于 `_process(delta)` 的 UI 动画也变慢。如果某个 UI 元素（比如血条抖动）希望不受影响，把它的 `process_mode` 设成 `PROCESS_MODE_ALWAYS` 并自己在 `_process` 里用 `delta * Engine.time_scale` 之外的原始时间。
- **`create_timer` 的内存**：`create_timer` 返回的 `SceneTreeTimer` 在超时后自动释放，不需要手动 `free()`。这也是它比"自己 `new` 一个 `Timer` 节点"更省心的原因。

---

## 33.5 模板 T18：CameraController 相机控制

### 模板 T18：CameraController 相机控制

**用途**：相机平滑跟随目标，带"朝移动方向前瞻"的偏移、地图边界限制、以及缓慢的缩放呼吸，让画面既有跟手的反馈又不会晃得人头晕。

**依赖**：无。作为 `Camera2D` 的脚本使用。**注意**：如果同时使用 T14 ScreenShake，请让二者分工——本模板写 `global_position`，T14 写 `offset`，互不冲突。

**文件位置建议**：`res://scripts/camera/camera_controller.gd`

#### 完整代码

```gdscript
class_name CameraController
extends Camera2D

## ============================================================
## 相机控制器
## ------------------------------------------------------------
## 设计要点一：为什么用 lerp(当前, 目标, 1 - exp(-k * delta))？
##   如果直接写 lerp(cur, dst, 0.1)，跟随速度会随帧率变化：
##   60fps 和 120fps 下相机的"跟手感"完全不同。
##   1 - exp(-k * delta) 是这一问题的标准解：它让"每秒收敛比例"
##   与帧率无关，无论多少帧，1 秒后的位置都一样。
##
## 设计要点二：为什么前瞻要用"速度"而不是"朝向"？
##   玩家往右跑时，我们希望画面往右多露出一点。
##   用速度方向做偏移，天然覆盖了"跑、跳、冲刺"等状态；
##   用朝向（例如摇杆方向）则在玩家原地转向时会让画面乱晃。
##
## 设计要点三：为什么前瞻本身也要平滑？
##   如果直接把 velocity.normalized() * distance 赋值给偏移量，
##   玩家急停或反向时，画面会"啪"地弹一下。所以前瞻也做一次
##   帧率无关的平滑（lookahead_speed 比 follow_speed 略小）。
##
## 设计要点四：边界为什么交给 Camera2D 的 limit_* 而不是自己 clamp？
##   引擎自带的 limit 已经处理好"缩放后的可视范围"，
##   并且有 limit_smoothed 可以在碰到边界时软化，自己 clamp 容易
##   在缩放变化时算错。
## ============================================================

## 跟随目标（推荐显式赋值，别只依赖 NodePath 字符串）
@export var target: Node2D

## 跟随速度：越大越跟手，越小越"拖沓"。
## <= 0 表示"硬跟随"（相机直接贴在目标上，适合复古像素游戏）。
@export var follow_speed: float = 8.0

## 前瞻最大距离（像素）：朝移动方向提前露出多少画面
@export var lookahead_distance: float = 64.0

## 前瞻平滑速度
@export var lookahead_speed: float = 3.5

## 呼吸缩放幅度（相对比例）。0.0 关闭。0.015 约为 ±1.5%
@export var zoom_breath_amount: float = 0.015

## 呼吸速度（弧度/秒）
@export var zoom_breath_speed: float = 1.5

## 速度估计的平滑系数（0 表示不平滑，直接差分）
@export var velocity_smoothing: float = 12.0

# ---- 内部状态 ----
var _lookahead: Vector2 = Vector2.ZERO
var _last_target_pos: Vector2 = Vector2.ZERO
var _smoothed_velocity: Vector2 = Vector2.ZERO
var _base_zoom: Vector2 = Vector2.ONE
var _breath_time: float = 0.0
var _has_target: bool = false


func _ready() -> void:
	_base_zoom = zoom
	if target:
		_attach(target)


## 运行时更换跟随目标（例如"过场结束切到新角色"）
func _attach(new_target: Node2D) -> void:
	target = new_target
	global_position = target.global_position
	_last_target_pos = target.global_position
	_smoothed_velocity = Vector2.ZERO
	_lookahead = Vector2.ZERO
	_has_target = true


func set_target(new_target: Node2D) -> void:
	_attach(new_target)


func _process(delta: float) -> void:
	if target == null:
		return
	if not _has_target:
		_attach(target)

	# 1) 用位置差分估计速度（对任何 Node2D 都通用，
	#    不要求目标一定是 CharacterBody2D）
	var instant_velocity := Vector2.ZERO
	if delta > 0.0:
		instant_velocity = (target.global_position - _last_target_pos) / delta
	_last_target_pos = target.global_position

	if velocity_smoothing <= 0.0:
		_smoothed_velocity = instant_velocity
	else:
		var kv := 1.0 - exp(-velocity_smoothing * delta)
		_smoothed_velocity = _smoothed_velocity.lerp(instant_velocity, kv)

	# 2) 前瞻：朝移动方向偏移（速度太小就不偏，避免"静止时抖"）
	var desired_lookahead := Vector2.ZERO
	if _smoothed_velocity.length() > 8.0:
		desired_lookahead = _smoothed_velocity.normalized() * lookahead_distance

	var kl := 1.0 - exp(-lookahead_speed * delta)
	_lookahead = _lookahead.lerp(desired_lookahead, kl)

	# 3) 跟随
	var desired_pos := target.global_position + _lookahead
	if follow_speed <= 0.0:
		global_position = desired_pos
	else:
		var kf := 1.0 - exp(-follow_speed * delta)
		global_position = global_position.lerp(desired_pos, kf)

	# 4) 缩放呼吸
	if zoom_breath_amount > 0.0:
		_breath_time += delta * zoom_breath_speed
		var factor := 1.0 + sin(_breath_time) * zoom_breath_amount
		zoom = _base_zoom * factor


## 设定地图边界。rect 用世界坐标表示。
## Camera2D 的 limit_* 是整数像素，所以这里取整。
func set_bounds(rect: Rect2, smooth: bool = true) -> void:
	limit_left = int(rect.position.x)
	limit_top = int(rect.position.y)
	limit_right = int(rect.position.x + rect.size.x)
	limit_bottom = int(rect.position.y + rect.size.y)
	limit_smoothed = smooth


## 根据一张 TileMap 的已用矩形自动设置边界
func set_bounds_from_rect(used_rect: Rect2, cell_size: Vector2i,
		smooth: bool = true) -> void:
	var r := Rect2(
		Vector2(used_rect.position) * Vector2(cell_size),
		Vector2(used_rect.size) * Vector2(cell_size)
	)
	set_bounds(r, smooth)


## 临时改变呼吸幅度（例如进入 Boss 战，镜头"紧张"起来）
func set_breath_amount(amount: float) -> void:
	zoom_breath_amount = amount


## 平滑改变基础缩放（例如开镜、进 Boss 房拉远）
func tween_zoom_to(new_zoom: Vector2, duration: float = 0.6) -> void:
	var t := create_tween()
	t.tween_property(self, "zoom", new_zoom, duration) \
		.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_IN_OUT)
	t.tween_callback(func() -> void: _base_zoom = new_zoom)
```

#### 使用方法

1. 选中你的 `Camera2D`，**Attach Script** 为 `res://scripts/camera/camera_controller.gd`。
2. **限制边界**：在 Inspector 里展开 **Limit** 分组，手动填 Left/Top/Right/Bottom（世界坐标像素），并勾选 **Limit Smoothed**。或者运行时调用：

```gdscript
@onready var cam: CameraController = $Camera2D

func _ready() -> void:
	cam.set_target($Player)

	# 方式一：手写边界
	cam.set_bounds(Rect2(0, 0, 3200, 1800))

	# 方式二：从 TileMapLayer 自动推导
	# var layer: TileMapLayer = $Ground
	# cam.set_bounds_from_rect(layer.get_used_rect(), layer.tile_set.tile_size)
```

3. **别忘了开启相机**：`Camera2D` 默认是 `Enabled`，但如果场景里有多个相机，只有一个是 active。检查 Inspector 里的 **Enabled** 勾选状态。
4. 调整手感：先设 `follow_speed = 0` 观察"硬跟随"的效果（相机与玩家完全同步），再逐步加到 6~10，感受"跟手"与"稳定"的平衡点。
5. 运行并测试：往一个方向持续移动，画面应该朝移动方向多露出一点；急停时不应该出现画面回弹；跑到地图边缘时相机应该停住，而不是继续带出黑色区域。
6. 若同时使用 T14 ScreenShake，确认震动只影响 `offset`、跟随只影响 `global_position`，两者叠加正常。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 | 推荐区间 |
| --- | --- | --- | --- | --- |
| `target` | `Node2D` | `null` | 跟随目标 | 必填 |
| `follow_speed` | `float` | `8.0` | 跟随收敛速度 | 4~12；0 为硬跟随 |
| `lookahead_distance` | `float` | `64.0` | 前瞻距离（像素） | 32~120 |
| `lookahead_speed` | `float` | `3.5` | 前瞻平滑速度 | 2~6 |
| `zoom_breath_amount` | `float` | `0.015` | 呼吸缩放幅度 | 0（关）~0.03 |
| `zoom_breath_speed` | `float` | `1.5` | 呼吸速度 | 0.8~2.5 |
| `velocity_smoothing` | `float` | `12.0` | 速度估计平滑 | 6~20 |

#### 进阶改造提示

- **死区跟随**：在屏幕中央设一个矩形死区，目标在死区内时相机不动，出了死区才追。像素平台跳跃游戏几乎都这么做，能大幅减少眩晕。
- **多目标取中点**：双人游戏里让 `target` 变成两个玩家的中点，并根据两人距离动态调整 `zoom`。只需改 `_process` 里 `desired_pos` 的计算。
- **事件驱动的高光**：命中 Boss 时 `tween_zoom_to(zoom * 1.15, 0.2)` 再拉回去，配合 T17 顿帧，演出感会很强。
- **像素完美**：像素风游戏请把 `follow_speed` 设为 0（硬跟随），并在 Inspector 里把 **Position Smoothing** 关掉、**Snap 2D Transforms to Pixel** 打开（项目设置里也有全局开关），否则会出现"像素抖动"。
- **注意 `zoom` 的基准值**：`_base_zoom` 是在 `_ready` 时读的。如果你之后用编辑器改了缩放，记得同步改 `_base_zoom`，或者重新调用 `tween_zoom_to`。

---

## 33.6 模板 T19：ScreenFlash 屏幕闪白/闪红

### 模板 T19：ScreenFlash 屏幕闪白/闪红

**用途**：用一层全屏色块做"闪一下"的效果。受伤闪红、拾取闪白、治疗闪绿、中毒闪紫。颜色可配置，透明度用 Tween 渐隐。

**依赖**：无。做成 `CanvasLayer`，全屏 `ColorRect` 在代码里自动创建，不需要在编辑器里手动搭 UI。

**文件位置建议**：`res://scripts/effects/screen_flash.gd`

#### 完整代码

```gdscript
class_name ScreenFlash
extends CanvasLayer

## ============================================================
## 屏幕闪光
## ------------------------------------------------------------
## 设计要点一：为什么用 CanvasLayer 而不是直接放一个 ColorRect？
##   CanvasLayer 是独立绘制层，不受相机移动、缩放影响，
##   天然就是"贴在屏幕上的滤镜"。而普通 Control 会被相机带着走。
##
## 设计要点二：为什么用代码创建 ColorRect 而不是做进场景？
##   这样复制粘贴即可运行，不需要用户去搭 UI 层级。
##   同时避免"每个项目都要新建一个场景"的摩擦成本。
##
## 设计要点三：为什么用 color:a 而不是 modulate:a？
##   modulate:a 会连带影响子节点的整体透明度，将来你若在
##   这一层下加别的东西（例如暗角、噪点），它们会被一起闪到。
##   只改 ColorRect 自己的 color.a 更"干净"。
##
## 设计要点四：为什么每次 flash 都要 kill 上一个 Tween？
##   受伤闪红后 0.05 秒又拾取闪白，如果两个 Tween 同时在跑，
##   它们会争抢 color.a，出现"闪到一半突然变暗"的抽搐。
##   只保留最新一次，观感统一。
## ============================================================

## 这一层的绘制顺序（越大越靠前）。100 基本在所有游戏 UI 之下、
## 在调试信息之上；如果你的血条在 CanvasLayer 120，请把它调到 110。
@export var layer_index: int = 100

## 默认闪白持续时长
@export var default_duration: float = 0.25

## 内部引用
var _rect: ColorRect
var _tween: Tween


func _ready() -> void:
	layer = layer_index

	_rect = ColorRect.new()
	_rect.name = "FlashRect"
	# 铺满整个视口。Control 直接挂在 CanvasLayer 下时，
	# 锚点参照的是视口矩形，所以 PRESET_FULL_RECT 就是全屏。
	_rect.set_anchors_preset(Control.PRESET_FULL_RECT)
	_rect.color = Color(1, 1, 1, 0)   # 完全透明 = 不显示
	# 必须忽略鼠标，否则它会吃掉所有的 UI 点击
	_rect.mouse_filter = Control.MOUSE_FILTER_IGNORE
	add_child(_rect)


## 核心接口：闪一下。
## color       闪光颜色（alpha 会被 peak_alpha 覆盖）
## duration    渐隐时长（秒）
## peak_alpha  起始不透明度 0~1，越大越"刺眼"
func flash(color: Color = Color(1, 1, 1),
		duration: float = -1.0, peak_alpha: float = 0.6) -> void:
	if duration < 0.0:
		duration = default_duration

	color.a = clampf(peak_alpha, 0.0, 1.0)
	_rect.color = color

	if _tween and _tween.is_valid():
		_tween.kill()

	_tween = create_tween()
	_tween.tween_property(_rect, "color:a", 0.0, duration) \
		.set_trans(Tween.TRANS_QUAD).set_ease(Tween.EASE_OUT)


## ---- 常用预设：语义清晰，调用处一看就懂 ----

func flash_damage(intensity: float = 0.6, duration: float = 0.35) -> void:
	flash(Color(1.0, 0.12, 0.12), duration, intensity)


func flash_pickup(intensity: float = 0.45, duration: float = 0.18) -> void:
	flash(Color(1.0, 1.0, 1.0), duration, intensity)


func flash_heal(intensity: float = 0.4, duration: float = 0.5) -> void:
	flash(Color(0.35, 1.0, 0.45), duration, intensity)


func flash_poison(intensity: float = 0.45, duration: float = 0.6) -> void:
	flash(Color(0.55, 0.2, 0.9), duration, intensity)


func flash_stun(intensity: float = 0.5, duration: float = 0.25) -> void:
	flash(Color(1.0, 0.95, 0.3), duration, intensity)


## 立刻清除（切场景、开菜单时调用）
func clear_now() -> void:
	if _tween and _tween.is_valid():
		_tween.kill()
	_rect.color.a = 0.0


## 持续脉动（例如"屏住呼吸"、"毒圈逼近"）。
## 返回的 Tween 由调用方保存，需要时 kill 掉即可。
func start_pulse(color: Color, min_alpha: float = 0.0,
		max_alpha: float = 0.25, half_period: float = 0.6) -> Tween:
	if _tween and _tween.is_valid():
		_tween.kill()
	_rect.color = color
	_tween = create_tween()
	_tween.set_loops()
	_tween.tween_property(_rect, "color:a", max_alpha, half_period)
	_tween.tween_property(_rect, "color:a", min_alpha, half_period)
	return _tween
```

#### 使用方法

1. 把 `screen_flash.gd` 挂到一个 `CanvasLayer` 节点上。放置位置有两种：
   - **只在本关生效**：在关卡场景里加一个 `CanvasLayer` 子节点并挂脚本；
   - **全局生效**：注册成 Autoload（节点名 `ScreenFlash`），任何地方都能调用。
2. **推荐用 Autoload**，因为受伤提示往往需要跨场景调用。
3. 在玩家受伤逻辑里调用：

```gdscript
extends CharacterBody2D

func take_damage(amount: int) -> void:
	ScreenFlash.flash_damage(0.55 if amount > 20 else 0.3)
	AudioManager.play_sfx(preload("res://audio/sfx_player_hurt.wav"))

func pick_up(item: String) -> void:
	ScreenFlash.flash_pickup()

func heal(amount: int) -> void:
	ScreenFlash.flash_heal()
```

4. **中毒状态**：

```gdscript
var _poison_tween: Tween

func start_poison() -> void:
	ScreenFlash.flash_poison(0.4, 0.4)
	_poison_tween = ScreenFlash.start_pulse(Color(0.55, 0.2, 0.9), 0.0, 0.18, 0.7)

func stop_poison() -> void:
	if _poison_tween and _poison_tween.is_valid():
		_poison_tween.kill()
	ScreenFlash.clear_now()
```

5. 运行确认：受伤时屏幕边缘（其实是全屏）闪红然后迅速消失；连按三次受伤，红色不会"叠加成深红"（因为每次都从头开始渐隐，且 `peak_alpha` 固定）。如果你希望"连续受伤越来越红"，把 `peak_alpha` 改成累加值即可（见进阶提示）。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `layer_index` | `int` | `100` | 绘制层级，须高于游戏 UI 之下的层级 |
| `default_duration` | `float` | `0.25` | 未指定时长时的默认渐隐时间 |
| `color`（入参） | `Color` | 白 | 闪光颜色 |
| `duration`（入参） | `float` | `-1` | 渐隐秒数，`-1` 表示用默认值 |
| `peak_alpha`（入参） | `float` | `0.6` | 起始不透明度 |
| `flash_damage` 的 `intensity` | `float` | `0.6` | 红屏强度 |
| `start_pulse` 的 `half_period` | `float` | `0.6` | 脉动半周期（秒） |

#### 进阶改造提示

- **只闪边缘**：用一张"屏幕外框 + 中间透明"的 `TextureRect` 替代纯色 `ColorRect`，做成暗角式受伤提示，比全屏闪红更高级、也更不遮挡画面。
- **累计受伤加深**：维护一个 `_recent_damage` 计数，1 秒内每次受伤 +0.15，闪红强度取 `min(1.0, 0.3 + _recent_damage)`，被连打时会"越闪越红"，压迫感更强。
- **加噪点**：在 `CanvasLayer` 下再放一个 `ColorRect` 并挂 `ShaderMaterial`（写一点点屏幕噪点 shader），能显著提升"受伤"的质感。
- **透明色块的性能**：全屏半透明 `ColorRect` 每帧都要混合一整屏像素，在移动端会有一点开销。如果持续时间长（例如持续脉动），考虑把 `flash_poison` 的 `peak_alpha` 调低，或者改用带 alpha 的 `TextureRect`（同样的混合成本，但可以只覆盖边缘）。
- **别忘了可访问性**：光敏性癫痫患者对高频闪白极度敏感。请给闪光加一个"强度"设置项，并在默认配置里避免高于 3Hz 的闪烁频率（这属于"安全设计"的基本要求）。

---

## 33.7 模板 T20：SettingsManager 设置持久化

### 模板 T20：SettingsManager 设置持久化

**用途**：把玩家的音量、全屏、分辨率、语言等偏好写进 `user://settings.cfg`，下次打开游戏自动读回并**立即生效**。

**依赖**：建议 Autoload。可选：与 T16 AudioManager 协作（存在则调用它，不存在则直接操作 `AudioServer`）。

**文件位置建议**：`res://autoload/settings_manager.gd`

#### 完整代码

```gdscript
extends Node

## ============================================================
## 设置管理器（Autoload 名称建议：Settings）
## ------------------------------------------------------------
## 设计要点一：为什么用 ConfigFile 而不是 JSON？
##   ConfigFile 是引擎自带的 INI 风格读写器，天然支持"分节"，
##   出错时不会抛异常，缺字段就用默认值，非常适合"设置"这种
##   "允许部分缺失"的数据。JSON 还要自己处理解析失败的异常分支。
##
## 设计要点二：为什么用 user:// 而不是 res://？
##   res:// 在导出后的游戏里是只读的（打包进 pck），
##   写进去的设置在真机上会直接失败。user:// 是每个玩家可写的
##   用户目录，是唯一正确的选择。桌面端它位于
##   %APPDATA%/Godot/app_userdata/<项目名>/（Windows）。
##
## 设计要点三：为什么"应用即生效"而不是"点确定才应用"？
##   现代游戏基本都做成即时预览——拖音量滑块立刻能听到变化。
##   所以每个 set_xxx 都同时做两件事：改内存值 + 立刻应用到引擎。
##   保存到磁盘则交给 save()，或者退出时统一保存一次。
##
## 设计要点四：为什么要做成"能独立运行"？
##   本模板不 import AudioManager。如果项目里恰好有它，就用它的
##   总线封装；没有就直接操作 AudioServer。这样模板可以单独抄走，
##   不会因为缺依赖而报错。这就是"弱耦合"。
## ============================================================

const CONFIG_PATH := "user://settings.cfg"

const SEC_GENERAL := "general"
const SEC_AUDIO := "audio"
const SEC_VIDEO := "video"

## 可供选择的分辨率列表（请按你的美术实际比例调整）
const RESOLUTIONS: Array[Vector2i] = [
	Vector2i(1280, 720),
	Vector2i(1600, 900),
	Vector2i(1920, 1080),
	Vector2i(2560, 1440),
]

## 可供选择的语言（需与 TranslationServer 的 locale 名一致）
const LOCALES: Array[String] = ["zh_CN", "en", "ja"]

## 设置变化信号。UI 可以连它做刷新（例如语言切换后重设文本）
signal settings_changed

# ---- 内存中的设置值 ----
var master_volume: float = 1.0
var music_volume: float = 0.8
var sfx_volume: float = 1.0
var ui_volume: float = 1.0

var fullscreen: bool = false
var resolution: Vector2i = Vector2i(1280, 720)
var vsync_enabled: bool = true

var language: String = "zh_CN"

## 防止"读盘时触发的 set_xxx"反过来又写盘，形成递归
var _loading: bool = false


func _ready() -> void:
	load_settings()
	apply_all()
	# 退出程序时自动保存一次，避免玩家忘记点"保存"
	get_tree().auto_accept_quit = true
	# 用一个常驻节点在退出时落盘
	set_process(false)


func _notification(what: int) -> void:
	# 窗口即将关闭：把当前设置写到磁盘
	if what == NOTIFICATION_WM_CLOSE_REQUEST:
		save_settings()


# ============================================================
# 读写
# ============================================================

func load_settings() -> void:
	_loading = true
	var cfg := ConfigFile.new()
	var err := cfg.load(CONFIG_PATH)
	if err != OK:
		# 首次运行：文件不存在很正常，直接用默认值
		_detect_defaults()
		_loading = false
		return

	master_volume = float(cfg.get_value(SEC_AUDIO, "master_volume", master_volume))
	music_volume = float(cfg.get_value(SEC_AUDIO, "music_volume", music_volume))
	sfx_volume = float(cfg.get_value(SEC_AUDIO, "sfx_volume", sfx_volume))
	ui_volume = float(cfg.get_value(SEC_AUDIO, "ui_volume", ui_volume))

	fullscreen = bool(cfg.get_value(SEC_VIDEO, "fullscreen", fullscreen))
	vsync_enabled = bool(cfg.get_value(SEC_VIDEO, "vsync", vsync_enabled))
	var rx := int(cfg.get_value(SEC_VIDEO, "res_x", resolution.x))
	var ry := int(cfg.get_value(SEC_VIDEO, "res_y", resolution.y))
	resolution = Vector2i(rx, ry)

	language = String(cfg.get_value(SEC_GENERAL, "language", language))

	_loading = false


func save_settings() -> void:
	var cfg := ConfigFile.new()

	cfg.set_value(SEC_AUDIO, "master_volume", master_volume)
	cfg.set_value(SEC_AUDIO, "music_volume", music_volume)
	cfg.set_value(SEC_AUDIO, "sfx_volume", sfx_volume)
	cfg.set_value(SEC_AUDIO, "ui_volume", ui_volume)

	cfg.set_value(SEC_VIDEO, "fullscreen", fullscreen)
	cfg.set_value(SEC_VIDEO, "vsync", vsync_enabled)
	cfg.set_value(SEC_VIDEO, "res_x", resolution.x)
	cfg.set_value(SEC_VIDEO, "res_y", resolution.y)

	cfg.set_value(SEC_GENERAL, "language", language)

	var err := cfg.save(CONFIG_PATH)
	if err != OK:
		push_warning("SettingsManager: 保存失败，错误码 %d" % err)


## 首次运行时，用当前窗口状态作为默认值，比硬编码更贴近玩家环境
func _detect_defaults() -> void:
	var size := DisplayServer.window_get_size()
	if size.x > 0 and size.y > 0:
		resolution = size
	fullscreen = DisplayServer.window_get_mode() == DisplayServer.WINDOW_MODE_FULLSCREEN
	var sys_locale := OS.get_locale()
	for loc in LOCALES:
		if sys_locale.begins_with(loc.substr(0, 2)):
			language = loc
			break


# ============================================================
# 立即应用
# ============================================================

func apply_all() -> void:
	_apply_audio()
	_apply_video()
	_apply_language()
	settings_changed.emit()


func _apply_audio() -> void:
	_set_bus_volume("Master", master_volume)
	_set_bus_volume("Music", music_volume)
	_set_bus_volume("SFX", sfx_volume)
	_set_bus_volume("UI", ui_volume)


## 优先委托给 AudioManager（如果项目里有）；否则直接操作 AudioServer。
## 这种"先问一句你会不会，再决定走哪条路"的写法就是鸭子类型，
## 让设置系统与音频系统解耦。
func _set_bus_volume(bus: String, value: float) -> void:
	value = clampf(value, 0.0, 1.0)

	var am := get_node_or_null("/root/AudioManager")
	if am != null and am.has_method("set_bus_volume"):
		am.set_bus_volume(bus, value)
		return

	var idx := AudioServer.get_bus_index(bus)
	if idx == -1:
		return
	AudioServer.set_bus_mute(idx, value <= 0.001)
	AudioServer.set_bus_volume_db(idx, linear_to_db(maxf(value, 0.001)))


func _apply_video() -> void:
	DisplayServer.window_set_vsync_mode(
		DisplayServer.VSYNC_ENABLED if vsync_enabled else DisplayServer.VSYNC_DISABLED
	)

	if fullscreen:
		DisplayServer.window_set_mode(DisplayServer.WINDOW_MODE_FULLSCREEN)
	else:
		DisplayServer.window_set_mode(DisplayServer.WINDOW_MODE_WINDOWED)
		DisplayServer.window_set_size(resolution)
		# 居中，避免切回窗口后跑到屏幕角上
		var screen_size := DisplayServer.screen_get_size()
		var pos := (screen_size - resolution) / 2
		DisplayServer.window_set_position(Vector2i(maxi(pos.x, 0), maxi(pos.y, 0)))


func _apply_language() -> void:
	TranslationServer.set_locale(language)


# ============================================================
# 供 UI 调用的 setter（都是"改值 + 立刻生效"）
# ============================================================

func set_master_volume(v: float) -> void:
	master_volume = clampf(v, 0.0, 1.0)
	_set_bus_volume("Master", master_volume)
	_auto_save()

func set_music_volume(v: float) -> void:
	music_volume = clampf(v, 0.0, 1.0)
	_set_bus_volume("Music", music_volume)
	_auto_save()

func set_sfx_volume(v: float) -> void:
	sfx_volume = clampf(v, 0.0, 1.0)
	_set_bus_volume("SFX", sfx_volume)
	_auto_save()

func set_ui_volume(v: float) -> void:
	ui_volume = clampf(v, 0.0, 1.0)
	_set_bus_volume("UI", ui_volume)
	_auto_save()

func set_fullscreen(on: bool) -> void:
	fullscreen = on
	_apply_video()
	_auto_save()

func set_resolution(res: Vector2i) -> void:
	resolution = res
	if not fullscreen:
		_apply_video()
	_auto_save()

func set_vsync(on: bool) -> void:
	vsync_enabled = on
	_apply_video()
	_auto_save()

func set_language(loc: String) -> void:
	language = loc
	_apply_language()
	settings_changed.emit()
	_auto_save()


## 读盘期间不要写盘，避免"读到一半被自己的写入覆盖"
func _auto_save() -> void:
	if _loading:
		return
	save_settings()


## 恢复出厂设置
func reset_to_defaults() -> void:
	master_volume = 1.0
	music_volume = 0.8
	sfx_volume = 1.0
	ui_volume = 1.0
	fullscreen = false
	resolution = Vector2i(1280, 720)
	vsync_enabled = true
	language = "zh_CN"
	apply_all()
	save_settings()
```

#### 使用方法

1. **注册 Autoload**：**Project → Project Settings → Autoload**，添加 `res://autoload/settings_manager.gd`，节点名填 `Settings`。
   > 注意：不要把它命名为 `Settings` 之外混淆的名字，因为下面 UI 里会固定用 `Settings.` 前缀。
2. **准备翻译**：如果你要用语言切换，需要在项目里配置本地化（**Project Settings → Localization → Translations**），并为 `zh_CN`、`en`、`ja` 各导入一份 `.po` 或 `.csv` 翻译。**不做这步也完全没问题**，`TranslationServer.set_locale` 只是没有对应词条可替换。
3. **搭设置面板**（一个示例场景，根节点 `Control`）：

```gdscript
extends Control

@onready var master_slider: HSlider = %MasterSlider
@onready var music_slider: HSlider = %MusicSlider
@onready var sfx_slider: HSlider = %SfxSlider
@onready var fullscreen_check: CheckButton = %FullscreenCheck
@onready var res_option: OptionButton = %ResOption
@onready var lang_option: OptionButton = %LangOption

func _ready() -> void:
	# 1) 先把当前设置填进控件
	master_slider.value = Settings.master_volume
	music_slider.value = Settings.music_volume
	sfx_slider.value = Settings.sfx_volume
	fullscreen_check.button_pressed = Settings.fullscreen

	res_option.clear()
	for i in Settings.RESOLUTIONS.size():
		var r: Vector2i = Settings.RESOLUTIONS[i]
		res_option.add_item("%d x %d" % [r.x, r.y], i)
		if r == Settings.resolution:
			res_option.select(i)

	lang_option.clear()
	for i in Settings.LOCALES.size():
		lang_option.add_item(Settings.LOCALES[i], i)
		if Settings.LOCALES[i] == Settings.language:
			lang_option.select(i)

	# 2) 再接线
	master_slider.value_changed.connect(Settings.set_master_volume)
	music_slider.value_changed.connect(Settings.set_music_volume)
	sfx_slider.value_changed.connect(Settings.set_sfx_volume)
	fullscreen_check.toggled.connect(Settings.set_fullscreen)
	res_option.item_selected.connect(_on_res_selected)
	lang_option.item_selected.connect(_on_lang_selected)

func _on_res_selected(index: int) -> void:
	Settings.set_resolution(Settings.RESOLUTIONS[index])

func _on_lang_selected(index: int) -> void:
	Settings.set_language(Settings.LOCALES[index])
```

4. 运行游戏，随便拖动音量滑块，然后**完全退出游戏**，再打开，确认滑块位置被记住。
5. 手动确认文件真的生成了：在编辑器里 **Project → Open User Data Folder**，你会看到 `settings.cfg`，内容类似：

```ini
[audio]

master_volume=0.7
music_volume=0.5
sfx_volume=1.0
ui_volume=0.9

[video]

fullscreen=false
vsync=true
res_x=1600
res_y=900

[general]

language="zh_CN"
```

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `CONFIG_PATH` | 常量 | `user://settings.cfg` | 存档位置，不要改成 `res://` |
| `RESOLUTIONS` | 常量数组 | 4 项 | 下拉框可选分辨率，务必按美术比例改 |
| `LOCALES` | 常量数组 | 3 项 | 可选语言，需与翻译词条一致 |
| `master_volume` / `music_volume` / `sfx_volume` / `ui_volume` | `float` | 1.0 / 0.8 / 1.0 / 1.0 | 各总线线性音量 |
| `fullscreen` | `bool` | `false` | 全屏开关 |
| `resolution` | `Vector2i` | `(1280,720)` | 窗口分辨率 |
| `vsync_enabled` | `bool` | `true` | 垂直同步 |
| `language` | `String` | `"zh_CN"` | 语言 locale |

#### 进阶改造提示

- **加"按键重绑定"**：`InputMap` 是可以在运行时改的，把 `action` → `InputEvent` 存成 `ConfigFile` 的一部分即可。`ConfigFile` 支持直接存 `InputEventKey` 对象（引擎会序列化成文本），不需要你自己转字符串。
- **多存档位**：把 `CONFIG_PATH` 改成变量，配合 `user://save_1.cfg`、`user://save_2.cfg` 就能支持多个玩家档案。
- **注册表式的设置项描述**：把"设置名 → 类型 → 默认值 → 应用回调"做成一张表，UI 就能自动生成。这会让新增一个设置项的成本降到"加一行数据"。
- **注意 Web 平台**：在 HTML5 导出里，`user://` 实际映射到浏览器的 IndexedDB，需要页面允许持久化存储；如果玩家清了浏览器数据，设置会丢。这是平台限制，不是代码 bug。
- **分辨率与窗口缩放**：如果你用了 `Project Settings → Display → Window → Stretch` 的 `canvas_items` 模式，`window_set_size` 改变的是窗口大小，游戏内部分辨率仍按 `viewport_width/height` 缩放。这两件事不要混为一谈。

---

## 33.8 本章小结

- **手感是"规则的放大器"**：同样一条"造成 10 点伤害"的规则，加上震动、飘字、音效、顿帧之后，玩家感受到的强度可以差好几倍。
- **反馈要成组出现**：本章的七个模板不是让你全抄，而是让你**每遇到一个重要事件，就从"视觉 / 听觉 / 时间"三类里各挑一个**。T14 的屏幕震动、T15 的伤害飘字、T16 的音频管理、T17 的打击顿帧，是"打击感四件套"。
- **T14 ScreenShake 的关键是"请求列表 + 叠加 + 限幅"**：不要用一个变量保存震动状态，否则多来源震动会互相覆盖；同时一定要给叠加后的位移限幅，防止画面飞出可视区域。
- **T14 写 `offset`，T18 写 `global_position`**：这是两个模板能同时挂在一个相机上的前提。设计模板时主动分配"谁控制哪个属性"，能极大降低组合成本。
- **T15 DamageNumber 必须池化**：飘字是"高频、短命、纯表现"的对象，正是对象池最典型的适用场景。溢出的正确处理不是"等待"，而是"抢最旧的"，因为飘字过期即无用。
- **T16 AudioManager 的三条设计红线**：用**总线**分组、音乐用**双播放器交叉淡入淡出**、音效用**播放器池**实现重叠。任何一条做不到，音频体验都会明显下降。
- **T16 的"同一首 BGM 不重播"判断一定要有**：否则每次切场景都会把背景音乐从头打断一次，这是新手项目里最普遍、也最刺耳的音频 bug。
- **T17 HitStop 的两种实现要分清**：`Engine.time_scale` 只缩放时间流速，简单通用；`get_tree().paused` 是全停，粒度更细但要给节点设 `process_mode`。**二者不要混用**。
- **T17 的恢复计时器必须 `ignore_time_scale = true`**：`create_timer(duration, true, false, true)` 的最后一个参数就是它。忘了它，`time_scale = 0` 时游戏会永久卡死——这是本章最需要反复检查的一处。
- **T18 CameraController 用 `1 - exp(-k * delta)` 做平滑**：这是帧率无关的标准插值写法，直接写 `lerp(a, b, 0.1)` 会让高帧率和高刷新率设备上的手感完全走样。
- **T18 的前瞻要基于"速度"并做二次平滑**：基于速度才能覆盖跑、跳、冲刺；二次平滑才能避免急停时画面弹跳。
- **T19 ScreenFlash 用 `ColorRect` + `color:a` 的 Tween**：`color:a` 只影响自己，`modulate:a` 会连带影响子节点；同时每次 `flash` 都要 `kill` 上一个 Tween，否则两个动画抢同一个属性会抽帧。
- **T19 必须设 `mouse_filter = MOUSE_FILTER_IGNORE`**：全屏色块如果不忽略鼠标，会吃掉整屏的按钮点击，这类问题在新手项目里非常常见且难查。
- **T20 SettingsManager 必须写 `user://`**：`res://` 在导出后只读，写设置会静默失败。这是"编辑器里好好的、一打包就丢设置"的经典原因。
- **T20 的每个 setter 都"改值 + 立即应用"**：现代游戏都做即时预览；同时用 `_loading` 标志防止"读盘触发 setter 又写盘"的递归。
- **弱耦合是模板能"单独抄走"的前提**：T20 不直接 `import` T16，而是用 `get_node_or_null("/root/AudioManager")` 加 `has_method` 的鸭子类型判断，让两个模板既能一起用，也能分开用。
- **无障碍不是可选项**：屏幕震动、全屏闪烁这类强刺激反馈，都要给玩家可关闭或可调弱的开关。这既是道德要求，也已经是行业规范。
- **最后记住一句话**：本章所有模板加起来也就一千多行代码，但它们对"游戏好不好玩"的影响，可能超过你后面写的几千行业务逻辑。**先把反馈做对，再去做内容。**

---

# 第 34 章：架构模板（工程化模式）

> 第 33 章解决的是"玩家爽不爽"。这一章解决的是"**你自己爽不爽**"。
>
> 很多项目不是死于功能做不出来，而是死于**代码互相纠缠**：玩家脚本要引用背包，背包要引用 UI，UI 要引用存档，存档又要引用玩家……改一处，全项目报错。
>
> 本章的六个模板，就是六个"**解耦工具**"。它们不增加任何游戏功能，但它们能让你在项目做到第 100 个文件时，依然敢随手改代码。

## 34.0 为什么需要"架构模板"

先看一个真实场景。假设你要做一个"商店"：

- 玩家点击商品 → 扣钱 → 物品进背包 → 背包 UI 刷新 → 播放音效 → 存档。

如果让玩家脚本直接干这些事，`player.gd` 里会长出这样的代码：

```gdscript
# ❌ 反面教材：什么都自己干
func buy(item_id: String) -> void:
	if money < ItemDatabase.get_price(item_id):
		return
	money -= ItemDatabase.get_price(item_id)
	$"../UI/BackpackUI".add_item(item_id)     # 硬编码路径
	$"../UI/MoneyLabel".text = str(money)     # 直接改别人的 UI
	$"../AudioManager".play(preload("res://sfx/buy.wav"))
	SaveSystem.set_value("money", money)      # 直接写存档
```

这段代码有五个问题：
1. **硬编码节点路径**——节点一改名，全线崩溃；
2. **职责混乱**——玩家类不该管 UI 长什么样；
3. **无法撤销**——买错了只能读档；
4. **无法测试**——想单独跑"购买逻辑"必须先搭好整个 UI；
5. **无法复用**——NPC 想买东西？只能把代码复制一遍。

本章六个模板对应的正是这五个问题的解法：

| 模板 | 解决的问题 | 对应上面的第几个问题 |
| --- | --- | --- |
| T21 ObjectPool | 频繁创建/销毁的性能与 GC 抖动 | 性能层 |
| T22 Singleton | 全局唯一状态放哪 | 全局状态 |
| T23 ServiceLocator | 硬编码节点路径与模块互相引用 | 问题 1、2、5 |
| T24 Command | 无法撤销/重做 | 问题 3 |
| T25 DataTable | 数据散落在代码里 | 问题 2、5 |
| T26 SceneRouter | 场景切换逻辑散落各处 | 问题 1、2 |

**一句话原则**：**架构不是让你写更多代码，而是让你每次改需求时，需要改的文件更少。**

---

## 34.1 模板 T21：ObjectPool 通用对象池

### 模板 T21：ObjectPool 通用对象池

**用途**：一个不挑类型的通用对象池。子弹、特效、伤害飘字、血条、掉落物……只要是"**频繁地创建又销毁、结构完全相同**"的场景，都能塞进来复用。

**依赖**：无。作为独立的 `Node` 挂在场景里，或由代码 `new` 出来。

**文件位置建议**：`res://scripts/core/object_pool.gd`

> **与第 30 章的区别**：第 30 章的 `BulletPool` 是**专用池**——它知道子弹长什么样，能调用 `bullet.setup(dir, damage)`，甚至内置了"飞出屏幕自动回收"。本章的 `ObjectPool` 是**通用池**——它只负责"借出 / 归还 / 扩容 / 溢出"这套生命周期管理，完全不关心对象内部是什么。两者是互补关系：**先用通用池管生命周期，再用专用脚本管业务逻辑**。

#### 完整代码

```gdscript
class_name ObjectPool
extends Node

## ============================================================
## 通用对象池
## ------------------------------------------------------------
## 设计要点一：为什么用"两个数组"而不是一个"状态字典"？
##   _free（空闲）与 _used（借出）两个数组，天然记录了
##   "借出顺序"。溢出策略 RECYCLE_OLDEST 需要"最久未归还"
##   这个语义，用数组的 pop_front() 就能 O(1) 拿到，
##   换成一个 Dictionary 就得自己维护时间戳，得不偿失。
##
## 设计要点二：为什么对象始终留在场景树里，只做 hide/disable？
##   加入/移出场景树（add_child/remove_child）会触发一堆回调，
##   还会打乱节点的处理顺序。而"留在树里 + set_process 关掉"
##   是几乎零成本的操作，且对象的子节点、信号连接、Tween 状态
##   都不会被打断。这是池化性能收益的主要来源。
##
## 设计要点三：为什么要连接 tree_exited 信号？
##   有些对象在业务逻辑里被 queue_free() 了（比如子弹撞墙时
##   调用了自己的 queue_free）。如果我们不监听解树事件，
##   池里就会留下一个"已释放的引用"，下次 acquire 直接
##   触发 "Attempt to call function on a null instance"。
##
## 设计要点四：为什么提供三种溢出策略，而不是写死一种？
##   "溢出时该怎么办"完全取决于业务：
##     子弹打光了应该"抢最旧的"（保证最新的一定能打出去）
##     掉落物过多应该"丢弃新的"（地上的东西不重要）
##     过场演员应该"无限扩容"（绝对不能少）
##   写死一种，这个池就永远只适用一半场景。
##
## 设计要点五：为什么用 has_method 而不是要求继承一个基类？
##   为了让池"零侵入"：任何 PackedScene 都能直接扔进来用，
##   不需要改脚本、不需要继承。你愿意写 pool_on_acquire()
##   就写，不写也有默认行为。这就是鸭子类型。
## ============================================================

## 溢出策略
enum Overflow {
	RECYCLE_OLDEST,   ## 抢占"借出最久"的对象（推荐给子弹、特效）
	DROP,             ## 直接放弃本次请求，acquire() 返回 null
	GROW,             ## 无视上限继续新建（内存换稳定）
}

## 要池化的场景。任何 PackedScene 都行（2D、3D、Control 都支持）。
@export var scene: PackedScene

## 预热数量：进游戏就一次性造好，避免第一次战斗时才卡一下
@export var prewarm_count: int = 12

## 池容量上限（RECYCLE_OLDEST / DROP 策略下生效）
@export var max_size: int = 120

## 溢出策略
@export var overflow: Overflow = Overflow.RECYCLE_OLDEST

## 可选：指定一个容器节点作为所有对象的父节点。
## 留空则对象直接挂在本池下面。好处是把它们统一挂到
## 一个专门的 "Projectiles/" 节点下，场景树更清爽。
@export var container_path: NodePath

## 借出 / 归还时广播，UI 和调试面板可以连它
signal node_acquired(node: Node)
signal node_released(node: Node)

var _free: Array[Node] = []
var _used: Array[Node] = []
var _container: Node = null


func _ready() -> void:
	_container = get_node_or_null(container_path)
	if _container == null:
		_container = self
	prewarm(prewarm_count)


## 预热：提前创建 n 个对象
func prewarm(count: int) -> void:
	if scene == null:
		push_warning("ObjectPool: 未设置 scene，无法预热")
		return
	for i in count:
		if _free.size() + _used.size() >= max_size:
			break
		if overflow != Overflow.GROW and _free.size() >= max_size:
			break
		_free.append(_instantiate())


# ============================================================
# 生命周期
# ============================================================

## 借出一个对象。用完记得 release() 还回来。
## DROP 策略下池满时会返回 null，调用方必须判空。
func acquire() -> Node:
	if scene == null:
		push_warning("ObjectPool: 未设置 scene")
		return null

	var node: Node = null

	if not _free.is_empty():
		node = _free.pop_back()
	elif overflow == Overflow.GROW or _used.size() < max_size:
		node = _instantiate()
	else:
		match overflow:
			Overflow.DROP:
				return null
			_:
				# RECYCLE_OLDEST：没收借出最久的那一个
				if _used.is_empty():
					return null
				node = _used.pop_front()
				_deactivate(node)

	_used.append(node)
	_activate(node)
	node_acquired.emit(node)
	return node


## 归还一个对象。重复归还会被安全忽略。
func release(node: Node) -> void:
	if node == null or not is_instance_valid(node):
		return
	var idx := _used.find(node)
	if idx == -1:
		# 要么不是本池借出的，要么已经归还过了。
		# 不报错，因为"重复归还"在复杂逻辑里很难完全避免。
		return
	_used.remove_at(idx)
	_deactivate(node)
	_free.append(node)
	node_released.emit(node)


## 归还当前所有借出的对象（切场景、重开一局时调用）
func release_all() -> void:
	# 先复制一份，避免在遍历时修改 _used
	for node in _used.duplicate():
		release(node)


## 延迟归还：适合"射出后 2 秒自动回收"这类需求
func release_after(node: Node, delay: float) -> void:
	if node == null or not is_instance_valid(node):
		return
	# 注意：这里用普通计时器即可；如果你希望顿帧时它照常计时，
	# 把 create_timer 的第三个参数（ignore_time_scale）设为 true。
	get_tree().create_timer(delay).timeout.connect(func() -> void:
		if is_instance_valid(node):
			release(node)
	)


## 清空整个池（释放所有对象）。只在确定不再使用时调用。
func clear() -> void:
	for n in _free:
		if is_instance_valid(n):
			n.queue_free()
	for n in _used:
		if is_instance_valid(n):
			n.queue_free()
	_free.clear()
	_used.clear()


# ============================================================
# 内部
# ============================================================

func _instantiate() -> Node:
	var n: Node = scene.instantiate()
	# 监听解树，防止业务代码偷偷 queue_free 之后留下悬空引用
	n.tree_exited.connect(_on_node_tree_exited.bind(n))
	_container.add_child(n)
	_deactivate(n)
	return n


## 停用一个对象：隐藏 + 停止处理 + 通知脚本
func _deactivate(n: Node) -> void:
	if n is CanvasItem:
		(n as CanvasItem).visible = false
	# PROCESS_MODE_DISABLED 会连同它的子孙一起停掉，
	# 包括 _process / _physics_process / input
	n.process_mode = Node.PROCESS_MODE_DISABLED
	if n.has_method("pool_on_release"):
		n.call("pool_on_release")


## 启用一个对象：恢复处理 + 显示 + 通知脚本
func _activate(n: Node) -> void:
	n.process_mode = Node.PROCESS_MODE_INHERIT
	if n is CanvasItem:
		(n as CanvasItem).visible = true
	if n.has_method("pool_on_acquire"):
		n.call("pool_on_acquire")


func _on_node_tree_exited(n: Node) -> void:
	# 对象被外部释放了，从两个数组里摘掉它的引用
	_free.erase(n)
	_used.erase(n)


# ============================================================
# 调试
# ============================================================

func get_free_count() -> int:
	return _free.size()

func get_active_count() -> int:
	return _used.size()

func get_total_count() -> int:
	return _free.size() + _used.size()

func debug_stats() -> String:
	return "[%s] free=%d used=%d total=%d max=%d" % [
		name, _free.size(), _used.size(), get_total_count(), max_size
	]
```

#### 使用方法

1. **写一个可池化的对象脚本**。它**不需要继承任何东西**，只需要两个约定：脚本里如果想收到通知，就实现 `pool_on_acquire()` / `pool_on_release()`。

```gdscript
extends Area2D
## 一个可池化的子弹

@export var speed: float = 800.0
var direction: Vector2 = Vector2.RIGHT
var damage: int = 10
var _life: float = 0.0

## 被借出时调用：重置状态
func pool_on_acquire() -> void:
	_life = 0.0
	rotation = direction.angle()

## 被归还时调用：清理状态
func pool_on_release() -> void:
	direction = Vector2.ZERO
	damage = 0
	position = Vector2.ZERO

## 可选：指定 setup 接口
func setup(dir: Vector2, dmg: int) -> void:
	direction = dir.normalized()
	damage = dmg

func _physics_process(delta: float) -> void:
	position += direction * speed * delta
	_life += delta
	if _life > 2.0:
		# 注意：这里不能 queue_free()，要还回池里！
		# 该由持有池引用的发射器来 release，见下面步骤 4。
		pass
```

2. **做场景**：新建 `Area2D` 场景，加上 `CollisionShape2D` 与 `Sprite2D`，挂上上面的脚本，保存为 `res://projectiles/bullet.tscn`。

3. **在场景里放池**：在 `Main.tscn` 根节点下新建一个 `Node`，命名 `BulletPool`，挂上 `object_pool.gd`。Inspector 里设置：
   - `Scene` → 拖入 `bullet.tscn`
   - `Prewarm Count` = 32
   - `Max Size` = 200
   - `Overflow` = `RECYCLE_OLDEST`
   - `Container Path`（可选）→ 指向一个空的 `Node2D`，让子弹都挂在它下面

4. **发射**：

```gdscript
extends Node2D

@onready var pool: ObjectPool = $BulletPool

func fire(direction: Vector2) -> void:
	var bullet := pool.acquire()
	if bullet == null:
		return          # DROP 策略下可能返回 null，必须判空
	bullet.global_position = $Muzzle.global_position
	bullet.setup(direction, 12)
	# 3 秒后自动回收（池帮你做，子弹脚本里就不用写 queue_free）
	pool.release_after(bullet, 3.0)
```

5. **碰撞回调里的正确写法**（**最容易出错的一步**）：

```gdscript
# 在 bullet.gd 里
func _on_area_entered(area: Area2D) -> void:
	# 不能直接 queue_free()！否则池会留下悬空引用。
	# 正确做法：把"该回收了"这件事交给持有池的发射器。
	if area.has_method("take_damage"):
		area.take_damage(damage)
	# 用一个信号把"我完成了"这件事广播出去，
	# 由 BulletEmitter 接住并调用 pool.release(self)
	finished.emit(self)
```

   更简单也更常见的一种做法是：在 `bullet.gd` 里保存池的引用（发射时赋值），命中后直接 `_pool.release(self)`。

6. 运行验证：
   - 连发 500 发子弹，`debug_stats()` 显示 `total` 稳定在上限附近，不再无限增长；
   - 暂停游戏时借出对象，恢复后对象状态正常（`pool_on_acquire` 重置生效）；
   - 手动在子弹里 `queue_free()` 一发，再继续发射，确认不会报空引用（`tree_exited` 兜底生效）。

#### 可调参数说明

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `scene` | `PackedScene` | `null` | 必填，要池化的场景 |
| `prewarm_count` | `int` | `12` | 预热数量，建议设为"屏幕上同屏最大数量 × 1.5" |
| `max_size` | `int` | `120` | 池容量上限 |
| `overflow` | `Overflow` | `RECYCLE_OLDEST` | 溢出策略：抢占最旧 / 丢弃 / 无限扩容 |
| `container_path` | `NodePath` | 空 | 对象父节点，留空则挂在本池下 |
| `pool_on_acquire()` | 约定方法 | 无 | 被借出时回调，用于重置状态 |
| `pool_on_release()` | 约定方法 | 无 | 被归还时回调，用于清理状态 |
| `acquire()` | 方法 | — | 借出，可能返回 `null` |
| `release(node)` | 方法 | — | 归还，重复归还安全 |
| `release_all()` | 方法 | — | 归还所有借出对象 |
| `clear()` | 方法 | — | 真释放所有对象 |

#### 进阶改造提示

- **加"自动归还寿命"**：给池加一个 `auto_release_time` 导出参数，在 `_activate` 里自动挂一个计时器，到点自动 `release`。这样连 `release_after` 都不用调用方操心。
- **加"统计埋点"**：给 `acquire` 加一个 `_miss_count`（需要新建的次数）计数器，跑几局后打印出来。如果 `miss_count` 一直是 0，说明预热数量够；如果持续增长，说明 `prewarm_count` 该调大。
- **3D 版本**：把 `_deactivate` 里的 `CanvasItem.visible` 判断换成 `Node3D.visible`（`Node3D` 也有 `visible` 属性），其余逻辑完全通用。
- **和 T23 ServiceLocator 配合**：把池注册进服务定位器（`Services.register(&"bullet_pool", pool)`），这样武器脚本就不需要 `get_node("../../BulletPool")` 这种脆弱路径了。
- **注意：不要池化"有独立逻辑状态"的对象**。比如一个有 `Signal` 连到全局、有 Tween 在跑、有唯一 `id` 的 Boss，池化后状态重置会非常麻烦。池化只适用于"结构简单、每次使用都是全新开始"的对象。

---

## 34.2 模板 T22：Singleton 单例模式

### 模板 T22：Singleton 单例模式

**用途**：让某个对象在全局只有一个实例，并且任何脚本都能直接访问它。Godot 里做单例有**两条正道**：**Autoload 单例** 和 **静态变量单例**。本模板把两者都写出来，并给出选择依据。

**依赖**：无。

**文件位置建议**：
- Autoload 方式：`res://autoload/game_state_autoload.gd`
- 静态变量方式：`res://scripts/core/game_state.gd`

#### 完整代码

**方式一：Autoload 单例（推荐给"需要节点能力"的场景）**

```gdscript
extends Node

## ============================================================
## Autoload 单例
## ------------------------------------------------------------
## 注册方式：Project → Project Settings → Autoload
##   Path: res://autoload/game_state_autoload.gd
##   Node Name: GameState
##
## 设计要点一：为什么不给它加 class_name？
##   如果 class_name 也叫 GameState，Godot 会报
##   "Autoload 名称与全局类名冲突"。两者名字必须不同。
##   所以这里不加 class_name，只用 Autoload 名做全局访问。
##
## 设计要点二：为什么 Autoload 能做的事比静态变量多？
##   因为 Autoload 是场景树里的一个真实节点，它拥有：
##     - get_tree()（能开计时器、能切场景、能暂停）
##     - 生命周期回调（_ready/_process/_notification）
##     - 能挂子节点（承载 UI、音频播放器、状态机）
##   静态变量只是一个数据容器，没有这些能力。
## ============================================================

## 全局状态变化时广播（UI 可连它刷新）
signal money_changed(new_value: int)
signal score_changed(new_value: int)
signal state_reset

## 金币
var money: int = 0:
	set(value):
		var v := maxi(value, 0)
		if v == money:
			return
		money = v
		money_changed.emit(money)

## 分数
var score: int = 0:
	set(value):
		if value == score:
			return
		score = value
		score_changed.emit(score)

## 已解锁关卡
var unlocked_levels: Array[int] = [1]

## 当前游戏是否正在进行（用于"暂停菜单"判断）
var is_playing: bool = false


func _ready() -> void:
	# 让本节点在游戏暂停时依然响应（例如暂停菜单要读它）
	process_mode = Node.PROCESS_MODE_ALWAYS


func add_money(amount: int) -> void:
	money += amount


func spend_money(amount: int) -> bool:
	if amount > money:
		return false
	money -= amount
	return true


func unlock_level(index: int) -> void:
	if index not in unlocked_levels:
		unlocked_levels.append(index)


func reset() -> void:
	money = 0
	score = 0
	unlocked_levels = [1]
	is_playing = false
	state_reset.emit()
```

**方式二：静态变量单例（推荐给"纯数据 / 纯工具"的场景）**

```gdscript
class_name GameStats
extends RefCounted

## ============================================================
## 静态变量单例
## ------------------------------------------------------------
## 设计要点一：static var 是 Godot 4.1 才有的特性。
##   它属于"脚本"本身，而不是某个实例。脚本在程序运行期间
##   只有一份，所以 static var 天然就是全局唯一的。
##
## 设计要点二：为什么叫 _instance 而不叫 instance？
##   因为下面还要定义一个 static func instance() 作为访问器。
##   变量名和函数名不能相同，否则解析时冲突。
##
## 设计要点三：为什么用"懒加载 + 访问器"而不是直接暴露 static var？
##   直接暴露意味着任何地方都能 GameStats._instance = null 把它清掉。
##   私有变量 + 访问器（带 null 检查）是更安全的封装。
## ============================================================

## 私有实例
static var _instance: GameStats

## 累积统计
var total_kills: int = 0
var total_deaths: int = 0
var total_playtime: float = 0.0
var best_score: int = 0

## 访问器：第一次调用时自动创建
static func instance() -> GameStats:
	if _instance == null:
		_instance = GameStats.new()
	return _instance


## 需要"每帧累积"的数据，可以自己维护时间。
## 注意：静态单例不在场景树里，没有 _process，
## 所以只能靠外部把 delta 传进来。
static func tick(delta: float) -> void:
	instance().total_playtime += delta


static func shutdown() -> void:
	_instance = null
```

**配套：一个"渲染"静态单例的好用形式——纯工具类**

```gdscript
class_name MathX
extends Object

## 纯静态工具类：不需要实例，全部方法都是 static。
## 这类"单例"其实连 instance 都不需要，直接当命名空间用。

static func approach(current: float, target: float, delta: float) -> float:
	if current < target:
		return minf(current + delta, target)
	return maxf(current - delta, target)


static func remap01(value: float, min_v: float, max_v: float) -> float:
	if is_equal_approx(max_v, min_v):
		return 0.0
	return clampf((value - min_v) / (max_v - min_v), 0.0, 1.0)


static func random_unit_vector() -> Vector2:
	var angle := randf() * TAU
	return Vector2(cos(angle), sin(angle))
```

#### 使用方法

**Autoload 方式：**

1. 把脚本放到 `res://autoload/game_state_autoload.gd`。
2. 打开 **Project → Project Settings → Autoload**。
3. 在 **Path** 里选到该脚本，在 **Node Name** 里填 `GameState`，点 **Add**。
4. 确认 **Enable** 勾选（默认勾选），按 **F5** 运行一次，若 Autoload 有语法错误会立刻弹报错。
5. 任何脚本里直接写：

```gdscript
func _on_coin_picked() -> void:
	GameState.add_money(10)
	AudioManager.play_sfx(preload("res://audio/sfx_coin.wav"))
```

**静态变量方式：**

1. 把脚本放到 `res://scripts/core/game_stats.gd`，**不需要**注册 Autoload。
2. 任何脚本里直接引用：

```gdscript
func _physics_process(delta: float) -> void:
	GameStats.tick(delta)

func _on_enemy_killed() -> void:
	var s := GameStats.instance()
	s.total_kills += 1
	s.best_score = maxi(s.best_score, GameState.score)
```

#### 两种单例的对比与选择

| 维度 | Autoload 单例 | 静态变量单例 |
| --- | --- | --- |
| 本质 | 场景树中的一个节点 | 脚本上的一个全局变量 |
| 能否 `get_tree()` | ✅ 可以 | ❌ 不行 |
| 能否开 `create_timer` | ✅ 可以 | ❌ 不行 |
| 能否有 `_process` | ✅ 可以 | ❌ 不行 |
| 能否挂子节点 | ✅ 可以（能承载播放器、UI） | ❌ 不行 |
| 能否用 `@export` | ✅ 可以（在编辑器里调） | ❌ 不行 |
| 受暂停影响 | 可配置 `process_mode` | 与暂停无关（它不在树里） |
| 初始化时机 | 引擎启动时自动 `_ready` | 第一次访问时懒加载 |
| 场景重载时是否重置 | ❌ 不重置（它是常驻节点） | ❌ 不重置（脚本只有一份） |
| 编辑器里能否看到 | ✅ 在 Remote 树里能检查 | ❌ 完全不可见 |
| 版本要求 | 所有 Godot 4 版本 | Godot 4.1+（`static var`） |
| 适用场景 | 音频、存档、场景路由、全局状态 | 纯数据统计、纯算法工具 |

**选择口诀**：
- **需要节点能力的 → Autoload**（要计时器、要挂子节点、要响应暂停）。
- **只是存点数据 / 提供纯函数的 → 静态变量**（更轻、更"干净"，不需要在 Project Settings 里注册）。

#### 可调参数说明

| 参数 / 方法 | 所属 | 说明 |
| --- | --- | --- |
| `money` / `score` | GameState | 用 setter 做边界校验并自动发信号 |
| `unlocked_levels` | GameState | 已解锁关卡列表 |
| `is_playing` | GameState | 是否在游戏中 |
| `add_money` / `spend_money` | GameState | 加钱 / 花钱（返回是否成功） |
| `reset()` | GameState | 重置所有全局状态 |
| `_instance` | GameStats | 私有静态实例 |
| `instance()` | GameStats | 静态访问器 |
| `tick(delta)` | GameStats | 手动推进时间统计 |
| `shutdown()` | GameStats | 清空静态实例（重开游戏时用） |

#### 进阶改造提示

- **单例的初始化顺序**：Autoload 之间的 `_ready` 顺序由 Project Settings 里的列表顺序决定（**从上到下**依次 `_ready`）。如果 `SaveSystem` 的 `_ready` 里要用 `Settings`，就必须把 `Settings` 排在它上面。**这是新手最容易踩的坑之一。**
- **不要滥用单例**：单例是全局变量，全局变量多了以后，代码会重新陷入"谁都能改我"的混乱。建议**把单例数量控制在 5 个以内**，并且只放"真的全局唯一"的东西。其他模块请用 T23 的服务定位器。
- **避免"隐式依赖"**：在脚本里写 `GameState.money`，会让这个脚本**无法脱离项目单独测试**。如果某个类只是偶尔用一下全局状态，更好的做法是把它**通过参数或 `@export` 传进去**。
- **`static var` 的一个隐藏特性**：`static var` 的生命周期与脚本资源绑定。在编辑器里热重载脚本（修改并保存）时，静态变量的值**可能被重置**。所以不要用它存"必须跨编辑期保持"的数据。
- **用 `Engine.has_singleton` 吗？** `Engine.has_singleton()` 查询的是**引擎原生单例**（如 `Input`、`DisplayServer`），**查不到 Autoload**。要判断某个 Autoload 是否存在，请用 `get_node_or_null("/root/GameState")`。

---

## 34.3 模板 T23：ServiceLocator 服务定位器

### 模板 T23：ServiceLocator 服务定位器

**用途**：一个运行时注册表。模块把自己"注册"进去，其他模块按名字"取用"，从而彻底告别 `get_node("../../UI/HUD")` 这种脆弱路径，也避免把一切都做成 Autoload。

**依赖**：建议做成 Autoload（注册为 `Services`）。

**文件位置建议**：`res://autoload/service_locator.gd`

#### 完整代码

```gdscript
class_name ServiceLocator
extends Node

## ============================================================
## 服务定位器（Autoload 名称建议：Services）
## ------------------------------------------------------------
## 设计要点一：它到底解决了什么问题？
##   对比一下两种写法：
##     ❌ var hud := get_node("../../UI/HUD")
##     ✅ var hud := Services.get_service(&"hud")
##   前者"把代码绑定到了具体的场景树结构上"，节点改名/改层级就崩；
##   后者"把代码绑定到一个逻辑名字上"，场景怎么改都无所谓。
##
## 设计要点二：为什么不把所有东西都做成 Autoload？
##   Autoload 要在 Project Settings 里手工注册，数量一多就难以管理；
##   而且 Autoload 是"永远活着"的，一个只在某关存在的 HUD
##   被做成 Autoload 就是资源浪费。服务定位器让"生命周期由场景决定，
##   访问方式却是全局的"，两个好处兼得。
##
## 设计要点三：为什么用 StringName 做键而不是 String？
##   StringName 是引擎内部的"字符串常量"类型，比较时走指针
##   而不是逐字符比对，字典查找更快，而且书写时用 &"" 有
##   语法高亮，能一眼看出"这是个服务名而不是普通文本"。
##
## 设计要点四：为什么 get_service 失败时返回 null 而不是断言崩溃？
##   游戏里"服务还没注册好就被访问"的情况是真实存在的
##   （例如网络服务延迟就绪）。返回 null + push_error 让调用方
##   自己决定是"跳过这次操作"还是"真的崩"，比强制崩溃更可控。
##
## 设计要点五：为什么监听 tree_exited 自动注销？
##   关卡里的 HUD 节点随场景销毁后，注册表里会留下一个悬空引用。
##   自动注销让注册表始终和现实一致，避免"幽灵服务"。
## ============================================================

## 服务注册表：StringName -> Object
var _registry: Dictionary = {}

## 服务注册 / 注销时广播，调试面板可以连它做可视化
signal service_registered(name: StringName)
signal service_unregistered(name: StringName)


## 注册一个服务。
## name    唯一标识，建议用 &"小写字母加下划线"
## service 任何 Object（Node、Resource、RefCounted 都行）
func register(name: StringName, service: Object) -> void:
	if service == null:
		push_error("Services: 不能注册空服务 '%s'" % name)
		return

	if _registry.has(name):
		push_warning("Services: 服务 '%s' 已被注册，本次将覆盖它" % name)
		# 覆盖前先把旧的监听摘掉，避免误注销
		var old = _registry[name]
		if old is Node and (old as Node).tree_exited.is_connected(_on_service_tree_exited):
			(old as Node).tree_exited.disconnect(_on_service_tree_exited)

	_registry[name] = service

	# 如果服务是个节点，它离开场景树时自动注销
	if service is Node:
		var node := service as Node
		if not node.tree_exited.is_connected(_on_service_tree_exited):
			node.tree_exited.connect(_on_service_tree_exited.bind(name))

	service_registered.emit(name)


## 注销服务
func unregister(name: StringName) -> void:
	if not _registry.has(name):
		return
	_registry.erase(name)
	service_unregistered.emit(name)


## 是否已注册（且引用仍然有效）
func has(name: StringName) -> bool:
	if not _registry.has(name):
		return false
	var svc = _registry[name]
	# 节点可能已经被别的代码释放了，这种情况视为"没有"
	if svc is Object and not is_instance_valid(svc):
		_registry.erase(name)
		return false
	return true


## 取服务。取不到返回 null 并报错（报错是为了让你早点发现拼写错误）。
func get_service(name: StringName) -> Object:
	if not has(name):
		push_error("Services: 找不到服务 '%s'。是否忘记 register()？" % name)
		return null
	return _registry[name]


## 安全版本：取不到就返回 null，不报错。
## 适合"这个服务可有可无"的场景（例如可选的特效模块）。
func get_service_or_null(name: StringName) -> Object:
	if not has(name):
		return null
	return _registry[name]


## 带类型断言的取节点版本，方便链式调用
func get_node_service(name: StringName) -> Node:
	var svc := get_service(name)
	if svc is Node:
		return svc as Node
	if svc != null:
		push_error("Services: 服务 '%s' 不是 Node" % name)
	return null


## 清空注册表（重开一局、回主菜单时调用）
func clear() -> void:
	for name in _registry.keys():
		service_unregistered.emit(name)
	_registry.clear()


## 调试用：列出所有已注册服务
func debug_dump() -> void:
	print("---- Services (%d) ----" % _registry.size())
	for name in _registry.keys():
		var svc = _registry[name]
		var cls_name := "?"
		if svc is Object and is_instance_valid(svc):
			var script := (svc as Object).get_script()
			if script != null:
				cls_name = script.get_global_name()
		print("  %-20s -> %s" % [name, cls_name])


func _on_service_tree_exited(name: StringName) -> void:
	# 节点已经离开场景树，注册表里的引用必须同步清除
	if _registry.has(name):
		_registry.erase(name)
		service_unregistered.emit(name)
```

#### 使用方法

1. **注册 Autoload**：**Project → Project Settings → Autoload**，添加 `res://autoload/service_locator.gd`，节点名填 `Services`。
2. **让模块在自己 `_ready` 时注册自己**：

```gdscript
extends Control
## 玩家 HUD

func _ready() -> void:
	# 把自己注册成服务。节点销毁时会自动注销。
	Services.register(&"hud", self)

func set_hp(current: int, maximum: int) -> void:
	# 具体实现……
	pass

func pop_damage_flash() -> void:
	pass
```

3. **让使用方按名字取用**：

```gdscript
extends CharacterBody2D
## 玩家

func take_damage(amount: int) -> void:
	# 只依赖"逻辑名字"，不依赖场景树结构
	var hud := Services.get_service_or_null(&"hud")
	if hud != null and hud.has_method("set_hp"):
		hud.set_hp(hp, max_hp)

	# 音效服务同理
	var audio := Services.get_service_or_null(&"audio")
	if audio != null and audio.has_method("play_sfx"):
		audio.play_sfx(preload("res://audio/sfx_hurt.wav"))
```

4. **把对象池也注册进去**（配合 T21）：

```gdscript
# 在 BulletPool 所在的场景脚本里
func _ready() -> void:
	Services.register(&"bullet_pool", $BulletPool)

# 武器脚本里
func fire(dir: Vector2) -> void:
	var pool := Services.get_service(&"bullet_pool") as ObjectPool
	var bullet := pool.acquire()
	bullet.global_position = global_position
	bullet.setup(dir, damage)
```

5. **回主菜单时清空**：在根场景的 `_exit_tree()` 里调用 `Services.clear()`，避免跨局残留。
6. 运行并在调试控制台执行 `Services.debug_dump()`，确认服务列表和实际场景一致。

#### 优缺点分析

| 优点 | 说明 |
| --- | --- |
| **解耦路径** | 不依赖节点层级，节点改名/改结构不会崩 |
| **生命周期自由** | 服务可以随场景销毁，不需要做成永久 Autoload |
| **可替换** | 测试时注册一个"假 UI"，就能脱离真实 UI 跑逻辑 |
| **可观测** | 一张注册表 + `debug_dump()`，全局依赖一目了然 |
| **渐进式** | 可以只把"真的到处都要用的东西"注册进去，其余保持原样 |

| 缺点 | 说明 | 缓解办法 |
| --- | --- | --- |
| **隐式依赖** | 看代码看不出它依赖哪些服务 | 在每个脚本顶部的注释里列清依赖的服务名 |
| **运行时才报错** | 名字拼错要到运行时才发现 | 用 `StringName` 常量集中定义服务名，见进阶提示 |
| **顺序问题** | 服务未注册就被访问 | 用 `get_service_or_null` 做容错，或延迟一帧再访问 |
| **全局状态回归** | 用多了又变成"全局变量的另一种写法" | 只注册"模块级"对象，不注册零散数值 |

#### 可调参数说明

| 方法 | 参数 | 返回 | 说明 |
| --- | --- | --- | --- |
| `register(name, service)` | `StringName`, `Object` | `void` | 注册（重复则覆盖并警告） |
| `unregister(name)` | `StringName` | `void` | 注销 |
| `has(name)` | `StringName` | `bool` | 是否可用（含有效性检查） |
| `get_service(name)` | `StringName` | `Object` | 取服务，失败报错返回 `null` |
| `get_service_or_null(name)` | `StringName` | `Object` | 取服务，失败静默返回 `null` |
| `get_node_service(name)` | `StringName` | `Node` | 取节点型服务 |
| `clear()` | — | `void` | 清空全部 |
| `debug_dump()` | — | `void` | 打印全部服务 |

#### 进阶改造提示

- **服务名集中管理**（强烈推荐）：新建 `res://scripts/core/service_names.gd`：

```gdscript
class_name ServiceNames
extends Object

## 所有服务名的唯一来源。改名字只需要改这里。
const HUD := &"hud"
const AUDIO := &"audio"
const BULLET_POOL := &"bullet_pool"
const PLAYER := &"player"
const SAVE := &"save"
```

  之后统一用 `Services.register(ServiceNames.HUD, self)`。这样"名字拼错"从运行时问题变成了**编译期问题**——写错的常量名会直接报"标识符未定义"。

- **接口约定用 `has_method` 兜底**：GDScript 没有接口（interface）语法。要表达"这个服务必须有 `set_hp` 方法"，可以在注册时检查：

```gdscript
func register_checked(name: StringName, service: Object, required: Array[StringName]) -> bool:
	for m in required:
		if not service.has_method(m):
			push_error("Services: 服务 '%s' 缺少必要方法 '%s'" % [name, m])
			return false
	register(name, service)
	return true
```

- **和 T22 的关系**：ServiceLocator 是一种"**动态的、可撤销的** Autoload"，而 Autoload 是"**静态的、永久的**"。经验法则是：**永久存在的东西用 Autoload（音频、存档），随场景存在的东西用服务定位器（HUD、对象池）**。
- **不要用它传数据**：`Services.register(&"score", 100)` 这种"注册一个数值"是误用。服务定位器管的是**对象**，数值请放进 T22 的单例或 T25 的数据表。

---

## 34.4 模板 T24：Command 命令模式

### 模板 T24：Command 命令模式

**用途**：把"一次操作"封装成一个对象，从而获得**撤销 / 重做**能力。适用于回合制战斗、建造游戏、编辑器工具、卡牌游戏、解谜游戏。

**依赖**：无。三个脚本都是纯 `RefCounted`，不需要 Autoload。

**文件位置建议**：`res://scripts/patterns/command.gd`、`command_stack.gd`、`command_group.gd`

> **和引擎自带 `UndoRedo` 的选择**：Godot 核心自带一个 `UndoRedo` 类，它通过 `add_do_method()` / `add_undo_method()` 记录"要调用的方法"，用 `commit_action()` 提交。它的设计目标是**编辑器插件**（撤销一次"移动节点"这种操作）。游戏里我们更想要的是：**每个操作是一个有名字、能自描述、能组成宏**的对象。所以本模板自己实现 Command 模式。**两者不要混用**——如果你做的是编辑器插件，请直接用 `UndoRedo`。

#### 完整代码

**第一部分：命令基类 `command.gd`**

```gdscript
class_name Command
extends RefCounted

## ============================================================
## 命令基类
## ------------------------------------------------------------
## 设计要点一：为什么用 RefCounted 而不是 Node？
##   命令对象只是个"数据 + 两个方法"的轻量载体，不需要
##   进入场景树、不需要 _process、不需要被渲染。
##   RefCounted 的引用计数在没人引用时自动归零并释放，
##   正好符合"命令用完就丢"的生命周期。
##
## 设计要点二：为什么每个命令都建议实现 describe()？
##   因为撤销栈最终是要给玩家看的——"撤销：购买 红药水 x1"。
##   有描述，UI 才好展示；没有描述，撤销按钮只能写"撤销"两个字。
## ============================================================

## 执行。子类必须重写。
func execute() -> void:
	push_error("Command.execute() 未实现：%s" % get_script())

## 撤销。子类必须重写。
func undo() -> void:
	push_error("Command.undo() 未实现：%s" % get_script())

## 人类可读的描述，用于 UI 展示与调试日志
func describe() -> String:
	return "未命名操作"

## 可选：命令执行前的前置检查。
## 返回 false 时，CommandStack 会拒绝执行它。
func can_execute() -> bool:
	return true
```

**第二部分：命令栈 `command_stack.gd`**

```gdscript
class_name CommandStack
extends RefCounted

## ============================================================
## 命令栈（撤销 / 重做）
## ------------------------------------------------------------
## 设计要点一：为什么用"两个栈"而不是"一个列表 + 游标"？
##   两个栈的语义最清晰：undo_stack 顶 = "下一步能撤销的操作"，
##   redo_stack 顶 = "下一步能重做的操作"。所有操作都是 O(1)。
##   用"列表 + 游标"虽然省内存，但每次插入新命令都要清空
##   游标之后的部分，代码里到处都是 len()/slice()，很容易写错。
##
## 设计要点二：为什么执行新命令时要清空 redo_stack？
##   这是撤销栈的标准语义：一旦你在历史中间做了新操作，
##   原来"未来"的那条分支就永远回不去了。
##   所有主流编辑器（含 Godot 自己）都是这个行为。
##
## 设计要点三：为什么要有 max_history？
##   每一条命令都持有对目标对象的引用。如果最大历史是无限的，
##   一场上千回合的对局会把所有历史对象都留在内存里。
##   限制上限后，超出部分从底部丢弃（最老的历史不可撤销）。
##   丢弃时不需要特殊处理，引用计数会自动释放。
## ============================================================

## 历史记录上限
var max_history: int = 128

var _undo_stack: Array[Command] = []
var _redo_stack: Array[Command] = []

## 撤销/重做可用状态变化时广播。UI 应该连它来启停按钮。
signal stack_changed(can_undo: bool, can_redo: bool)


## 执行一条命令并压入历史。
## 返回是否真的执行了（can_execute() 返回 false 时不会执行）。
func execute(cmd: Command) -> bool:
	if cmd == null:
		return false
	if not cmd.can_execute():
		return false

	cmd.execute()
	_undo_stack.append(cmd)
	_redo_stack.clear()

	# 超出上限就从最老的历史开始丢
	while _undo_stack.size() > max_history:
		_undo_stack.pop_front()

	stack_changed.emit(can_undo(), can_redo())
	return true


## 撤销一步
func undo() -> bool:
	if _undo_stack.is_empty():
		return false
	var cmd: Command = _undo_stack.pop_back()
	cmd.undo()
	_redo_stack.append(cmd)
	stack_changed.emit(can_undo(), can_redo())
	return true


## 重做一步
func redo() -> bool:
	if _redo_stack.is_empty():
		return false
	var cmd: Command = _redo_stack.pop_back()
	cmd.execute()
	_undo_stack.append(cmd)
	stack_changed.emit(can_undo(), can_redo())
	return true


func can_undo() -> bool:
	return not _undo_stack.is_empty()


func can_redo() -> bool:
	return not _redo_stack.is_empty()


## 下一步要撤销的操作描述（给 UI 显示"撤销：xxx"）
func peek_undo_description() -> String:
	if _undo_stack.is_empty():
		return ""
	return _undo_stack.back().describe()


func peek_redo_description() -> String:
	if _redo_stack.is_empty():
		return ""
	return _redo_stack.back().describe()


## 清空历史（读档、重开一局时用）
func clear() -> void:
	_undo_stack.clear()
	_redo_stack.clear()
	stack_changed.emit(false, false)


func get_undo_count() -> int:
	return _undo_stack.size()


func get_redo_count() -> int:
	return _redo_stack.size()


## 调试用
func debug_dump() -> void:
	print("CommandStack: undo=%d redo=%d" % [_undo_stack.size(), _redo_stack.size()])
	for i in _undo_stack.size():
		print("  [%d] %s" % [i, _undo_stack[i].describe()])
```

**第三部分：宏命令 `command_group.gd`**

```gdscript
class_name CommandGroup
extends Command

## ============================================================
## 组合命令（宏）
## ------------------------------------------------------------
## 把多条命令打包成"一个原子操作"。
## 例如"使用一张卡牌"实际上包含：扣费用 + 造成伤害 + 抽一张牌。
## 玩家按一次 Ctrl+Z，这三件事应该一起撤销，而不是撤三步。
##
## 关键细节：undo 必须【逆序】执行。
## 若正向是 扣费 → 加道具，逆向就应该是 减道具 → 还钱。
## 顺序错了，中间状态可能出现负数或幽灵物品。
## ============================================================

var _children: Array[Command] = []


func _init(children: Array[Command] = []) -> void:
	_children = children.duplicate()


## 链式添加，方便拼装
func add(cmd: Command) -> CommandGroup:
	if cmd != null:
		_children.append(cmd)
	return self


func can_execute() -> bool:
	for c in _children:
		if not c.can_execute():
			return false
	return true


func execute() -> void:
	for c in _children:
		c.execute()


func undo() -> void:
	# 逆序撤销！
	for i in range(_children.size() - 1, -1, -1):
		_children[i].undo()


func describe() -> String:
	if _children.is_empty():
		return "空操作"
	if _children.size() == 1:
		return _children[0].describe()
	return "%s 等 %d 项操作" % [_children[0].describe(), _children.size()]
```

**第四部分：三个实战命令示例**

```gdscript
# ---------- 示例 1：移动 ----------
class_name MoveCommand
extends Command

var _target: Node2D
var _offset: Vector2

func _init(target: Node2D, offset: Vector2) -> void:
	_target = target
	_offset = offset

func execute() -> void:
	_target.position += _offset

func undo() -> void:
	_target.position -= _offset

func describe() -> String:
	return "移动 %s %s" % [_target.name, _offset]


# ---------- 示例 2：购买（跨两个对象）----------
class_name PurchaseCommand
extends Command

var _wallet: Object        ## 需要 get_money() / set_money() 方法
var _inventory: Object     ## 需要 add_item() / remove_item() 方法
var _item_id: StringName
var _price: int

func _init(wallet: Object, inventory: Object,
		item_id: StringName, price: int) -> void:
	_wallet = wallet
	_inventory = inventory
	_item_id = item_id
	_price = price

func can_execute() -> bool:
	return _wallet.get_money() >= _price

func execute() -> void:
	_wallet.set_money(_wallet.get_money() - _price)
	_inventory.add_item(_item_id, 1)

func undo() -> void:
	_inventory.remove_item(_item_id, 1)
	_wallet.set_money(_wallet.get_money() + _price)

func describe() -> String:
	return "购买 %s（-%d）" % [_item_id, _price]


# ---------- 示例 3：使用道具（带回血）----------
class_name UseItemCommand
extends Command

var _user: Object          ## 需要 get_hp() / set_hp() / remove_item() 方法
var _item_id: StringName
var _heal_amount: int
var _actual_heal: int = 0  ## 因为"溢出治疗量"要记下来才能精确撤销

func _init(user: Object, item_id: StringName, heal_amount: int) -> void:
	_user = user
	_item_id = item_id
	_heal_amount = heal_amount

func can_execute() -> bool:
	return _user.has_item(_item_id)

func execute() -> void:
	_user.remove_item(_item_id, 1)
	var before: int = _user.get_hp()
	_user.set_hp(before + _heal_amount)
	# 关键：记录"实际回了多少血"，而不是理论值。
	# 否则玩家满血吃药后撤销，血量会凭空增长。
	_actual_heal = _user.get_hp() - before

func undo() -> void:
	_user.set_hp(_user.get_hp() - _actual_heal)
	_user.add_item(_item_id, 1)

func describe() -> String:
	return "使用 %s（+%d HP）" % [_item_id, _heal_amount]
```

#### 使用方法

1. 把四个脚本放到 `res://scripts/patterns/` 下（`command.gd`、`command_stack.gd`、`command_group.gd`，示例命令可以放在 `res://scripts/commands/`）。
   > `class_name` 是全局注册的，**一个项目里不能有两个同名脚本**。示例里的 `MoveCommand` 如果你项目里已有同名类，请改名。
2. 在需要撤销能力的系统里持有**一个** `CommandStack`：

```gdscript
extends Node
## 回合制战斗控制器

var history := CommandStack.new()

@onready var wallet: Object = $PlayerWallet
@onready var inventory: Object = $PlayerInventory
@onready var player: Object = $Player

func _ready() -> void:
	history.max_history = 64
	history.stack_changed.connect(_refresh_undo_buttons)
	_refresh_undo_buttons(false, false)

func _unhandled_input(event: InputEvent) -> void:
	if event.is_action_pressed("ui_undo"):      # 需要自己在输入映射里加
		history.undo()
		get_viewport().set_input_as_handled()
	elif event.is_action_pressed("ui_redo"):
		history.redo()
		get_viewport().set_input_as_handled()

func do_buy(item_id: StringName, price: int) -> void:
	var cmd := PurchaseCommand.new(wallet, inventory, item_id, price)
	if not history.execute(cmd):
		# can_execute() 返回 false，说明钱不够
		AudioManager.play_ui(preload("res://audio/sfx_denied.wav"))
		return
	AudioManager.play_ui(preload("res://audio/sfx_buy.wav"))
	print("已购买：", cmd.describe())

func do_use_card() -> void:
	# 宏命令：一次 Ctrl+Z 撤掉全部三件事
	var macro := CommandGroup.new()
	macro.add(PurchaseCommand.new(wallet, inventory, &"potion", 30))
	macro.add(UseItemCommand.new(player, &"potion", 40))
	macro.add(MoveCommand.new($Cursor, Vector2(64, 0)))
	history.execute(macro)

func _refresh_undo_buttons(can_u: bool, can_r: bool) -> void:
	# 这里更新 UI 按钮的 disabled 状态，并显示描述文本
	pass
```

3. 运行，执行几次购买 → 按撤销快捷键 → 观察金币和背包**同时**回滚。
4. 中途执行一次新操作，确认重做栈被清空（"撤销后做新操作，就不能再重做了"）。

#### 可调参数说明

| 参数 / 方法 | 所属 | 说明 |
| --- | --- | --- |
| `max_history` | CommandStack | 历史上限，建议 32~256 |
| `execute(cmd)` | CommandStack | 执行并入栈，返回是否成功 |
| `undo()` / `redo()` | CommandStack | 撤销 / 重做一步 |
| `can_undo()` / `can_redo()` | CommandStack | 是否可撤销 / 可重做 |
| `peek_undo_description()` | CommandStack | 下一撤销项的描述（给 UI 用） |
| `clear()` | CommandStack | 清空历史 |
| `stack_changed` | CommandStack | 状态变化信号，用于刷新按钮 |
| `can_execute()` | Command | 前置检查，返回 false 则不执行 |
| `describe()` | Command | 人类可读描述 |
| `add(cmd)` | CommandGroup | 链式添加子命令 |

#### 进阶改造提示

- **记录"实际发生的变化"而不是"理论值"**：`UseItemCommand` 里的 `_actual_heal` 就是典型例子。凡是"可能被夹紧、被上限截断、被概率影响"的数值（治疗溢出、伤害减免、暴击），**必须在 `execute()` 里把真实结果记下来**，否则 `undo()` 会算错。这是命令模式最容易踩的坑。
- **让命令可序列化**：给命令加 `to_dict()` / `from_dict()`，就能把整套操作历史存进存档，实现"读档后依然能撤销"。
- **网络同步**：命令模式天然适合回合制联机——双方只同步"命令列表"，各自执行，结果必然一致（前提是命令是确定性的，不能依赖 `randf()`）。
- **撤销栈的内存**：命令持有目标对象的引用，只要命令还在栈里，目标对象就不会被释放。所以**清空历史要主动调用 `history.clear()`**，尤其在切场景时。
- **有副作用就别强行撤销**：播放一次音效、弹一次飘字是不可逆的。不要把这类东西放进 `execute()`，否则撤销时你会听到"倒放"的声音。把它们放在**调用方**（执行命令之后），而不是命令内部。

---

## 34.5 模板 T25：DataTable 数据驱动配表

### 模板 T25：DataTable 数据驱动配表

**用途**：把配置数据（物品、技能、敌人、关卡、掉落表）从代码里搬到**数据文件**里，运行时按 `id` 查询。开发期还能直接从 JSON 重载，改数值不用重启游戏。

**依赖**：一个基础 `Resource` 类 `DataRow`（提供统一的 `id` 字段）。`DataTable` 本身是一个 `Node`。

**文件位置建议**：
- `res://scripts/data/data_row.gd`
- `res://scripts/data/item_data.gd`
- `res://scripts/data/data_table.gd`
- 数据文件：`res://data/items/*.tres` 或 `res://data/items.json`

#### 完整代码

**第一部分：统一基类 `data_row.gd`**

```gdscript
class_name DataRow
extends Resource

## ============================================================
## 配置行基类
## ------------------------------------------------------------
## 设计要点一：为什么所有配置都要继承一个共同基类？
##   因为 DataTable 需要"从任意 Resource 里安全地拿到 id"。
##   如果直接对任意 Resource 调用 get("id")，一旦该资源没有
##   id 属性，就会得到 null 或者报错。有了统一基类，
##   一句 `if res is DataRow` 就能安全地做类型过滤。
##
## 设计要点二：为什么用 StringName 存 id 而不是 int？
##   StringName 在代码里可读（&"iron_sword" 比 id=37 清晰），
##   在字典里查找效率也高。数字 id 的优势是省内存，
##   对配置表这种"几百到几千行"的规模完全没有必要。
## ============================================================

## 唯一标识。约定用"小写字母 + 下划线"。
@export var id: StringName = &""

## 排序权重（列表显示时按它排序）
@export var order: int = 0

## 是否弃用（保留数据但不参与游戏逻辑，方便做版本兼容）
@export var deprecated: bool = false
```

**第二部分：具体的物品配置 `item_data.gd`**

```gdscript
class_name ItemData
extends DataRow

## ============================================================
## 物品配置
## ------------------------------------------------------------
## 这是"自定义 Resource 配表"的典型写法：
##   每个字段都是 @export，所以能在 Godot 编辑器的
##   Inspector 里直接可视化编辑，改完存盘即可，不需要写 JSON。
##   同时，图标等资源引用可以直接拖进来，编辑器会保证引用有效。
## ============================================================

@export var display_name: String = ""
@export_multiline var description: String = ""
@export var price: int = 0
@export var max_stack: int = 99

## 资源引用（图标）——这是"用 Resource 配表"相比 JSON 的最大优势：
## JSON 里只能存路径字符串，还得自己 load；这里直接是强引用。
@export var icon: Texture2D

## 使用效果
@export var heal_amount: int = 0
@export var damage_bonus: int = 0

## 标签，用于"按类型筛选"（&"consumable"、&"weapon"、&"quest"）
@export var tags: Array[StringName] = []


## 便捷判断
func has_tag(tag: StringName) -> bool:
	return tag in tags


func is_consumable() -> bool:
	return has_tag(&"consumable")
```

**第三部分：数据表 `data_table.gd`**

```gdscript
class_name DataTable
extends Node

## ============================================================
## 数据表
## ------------------------------------------------------------
## 设计要点一：为什么同时支持 .tres 目录和 JSON 两种来源？
##   .tres（自定义 Resource）适合"策划直接在编辑器里改"，
##     有类型检查、有图标预览、不会手滑写错字段名。
##   JSON 适合"从 Excel/表格工具导出"、"热更新"、
##     "开发期改了立刻重载"。
##   两者并存，用哪条路取决于你的工作流。
##
## 设计要点二：为什么内部是 Dictionary 而不是 Array？
##   因为 99% 的查询是"按 id 取一条"。Dictionary 的键查找是 O(1)，
##   Array 线性扫描是 O(n)。配置表哪怕只有 200 行，
##   战斗中每帧查几次也会变成明显开销。
##
## 设计要点三：为什么要缓存"资源对象"和"字典"两份？
##   代码里常常想写 row["price"]（字典风格，方便通用处理），
##   但也常常想要 res.icon（强类型，方便直接拖资源）。
##   两份数据加上一个转换器，两边都舒服。
## ============================================================

## .tres 配置目录（留空则不使用）
@export var resource_dir: String = ""

## JSON 配置路径（留空则不使用）
@export var json_path: String = ""

## 是否在 _ready 自动加载
@export var auto_load: bool = true

## 开发期热重载按键（设为 0 表示关闭）
@export var debug_reload_key: Key = KEY_F9

## 载入完成信号
signal table_loaded(count: int)

## id(StringName) -> Dictionary
var _rows: Dictionary = {}
## id(StringName) -> DataRow
var _resources: Dictionary = {}


func _ready() -> void:
	if auto_load:
		reload()


func _unhandled_input(event: InputEvent) -> void:
	# 只在调试构建里响应热重载按键，正式版不受影响
	if debug_reload_key == KEY_NONE or not OS.is_debug_build():
		return
	if event is InputEventKey and event.pressed and not event.echo \
			and (event as InputEventKey).keycode == debug_reload_key:
		reload()
		print("DataTable: 已热重载，共 %d 条" % _rows.size())


## 重新读取全部配置
func reload() -> int:
	_rows.clear()
	_resources.clear()

	if not resource_dir.is_empty():
		load_from_dir(resource_dir)
	if not json_path.is_empty():
		# JSON 在目录之后加载，便于"临时覆盖某几行"
		load_from_json(json_path)

	table_loaded.emit(_rows.size())
	return _rows.size()


# ============================================================
# 来源一：.tres 目录
# ============================================================

func load_from_dir(dir_path: String) -> int:
	var da := DirAccess.open(dir_path)
	if da == null:
		push_warning("DataTable: 打不开目录 %s" % dir_path)
		return 0

	var loaded := 0
	# 第一个参数 true = 跳过 . 和 ..，第二个 true = 跳过隐藏文件
	da.list_dir_begin(true, true)
	var file_name := da.get_next()
	while file_name != "":
		if not da.current_is_dir() and file_name.ends_with(".tres"):
			var res := ResourceLoader.load(dir_path.path_join(file_name))
			if res is DataRow and (res as DataRow).id != &"":
				var row := res as DataRow
				_resources[row.id] = row
				_rows[row.id] = _resource_to_dict(row)
				loaded += 1
			elif res != null:
				push_warning("DataTable: %s 不是 DataRow，已跳过" % file_name)
		file_name = da.get_next()
	da.list_dir_end()
	return loaded


## 把 Resource 的脚本变量导成字典
func _resource_to_dict(res: Resource) -> Dictionary:
	var d := {}
	for prop in res.get_property_list():
		# 只导出"用户自定义的脚本变量"，不导出内置属性
		if int(prop["usage"]) & PROPERTY_USAGE_SCRIPT_VARIABLE:
			d[String(prop["name"])] = res.get(prop["name"])
	return d


# ============================================================
# 来源二：JSON
# ============================================================

## 支持两种 JSON 结构：
##   [ {...}, {...} ]                  —— 顶层是数组
##   { "rows": [ {...}, {...} ] }      —— 顶层是对象且含 rows
func load_from_json(path: String) -> int:
	if not FileAccess.file_exists(path):
		push_warning("DataTable: 找不到 JSON 文件 %s" % path)
		return 0

	var text := FileAccess.get_file_as_string(path)
	if text.is_empty():
		push_warning("DataTable: JSON 文件为空 %s" % path)
		return 0

	var parsed = JSON.parse_string(text)
	if parsed == null:
		push_error("DataTable: JSON 解析失败 %s" % path)
		return 0

	var list: Array = []
	if parsed is Array:
		list = parsed
	elif parsed is Dictionary and parsed.has("rows") and parsed["rows"] is Array:
		list = parsed["rows"]
	else:
		push_error("DataTable: JSON 结构不符合预期 %s" % path)
		return 0

	var loaded := 0
	for entry in list:
		if not (entry is Dictionary) or not entry.has("id"):
			continue
		var row: Dictionary = entry
		var id := StringName(str(row["id"]))
		_rows[id] = row
		loaded += 1
	return loaded


# ============================================================
# 查询接口
# ============================================================

## 是否包含某 id
func has_row(id: StringName) -> bool:
	return _rows.has(id)


## 取一条字典（推荐：通用、安全）
func get_row(id: StringName) -> Dictionary:
	if not _rows.has(id):
		push_warning("DataTable: 找不到 id '%s'" % id)
		return {}
	return _rows[id]


## 取一条字典，找不到返回空字典但不报警（适合"可选配置"）
func get_row_or_empty(id: StringName) -> Dictionary:
	return _rows.get(id, {})


## 取强类型资源（适合 .tres 来源）
func get_resource(id: StringName) -> DataRow:
	if not _resources.has(id):
		return null
	return _resources[id]


## 取某字段，带默认值。日常业务里最常用的一个接口。
func get_value(id: StringName, key: String, default_value: Variant = null) -> Variant:
	var row := _rows.get(id, {})
	return row.get(key, default_value)


## 全部 id
func get_all_ids() -> Array:
	return _rows.keys()


## 行数
func count() -> int:
	return _rows.size()


## 按标签筛选（要求该行有 tags 字段且为数组）
func filter_by_tag(tag: StringName) -> Array:
	var out: Array = []
	for id in _rows.keys():
		var row: Dictionary = _rows[id]
		var tags = row.get("tags", [])
		if tags is Array and tag in tags:
			out.append(id)
	return out


## 按字段排序返回 id 列表
func get_ids_sorted_by(key: String) -> Array:
	var ids := _rows.keys()
	ids.sort_custom(func(a, b) -> bool:
		return float(_rows[a].get(key, 0)) < float(_rows[b].get(key, 0))
	)
	return ids


## 调试输出前 n 行
func debug_dump(limit: int = 5) -> void:
	print("---- DataTable: %d 行 ----" % _rows.size())
	var shown := 0
	for id in _rows.keys():
		if shown >= limit:
			break
		print("  ", id, " -> ", _rows[id])
		shown += 1
```

#### 使用方法

1. 把 `data_row.gd`、`item_data.gd`、`data_table.gd` 放到 `res://scripts/data/`。
2. **创建 .tres 配置**（推荐路径）：
   - 在 `res://data/items/` 目录右键 → **New Resource**；
   - 在弹窗里搜索 `ItemData`（因为脚本有 `class_name`，这里能搜到）；
   - 命名保存为 `iron_sword.tres`；
   - 在 Inspector 里填：`Id` = `iron_sword`，`Display Name` = `铁剑`，`Price` = 120，`Damage Bonus` = 8，`Tags` 加一项 `weapon`；
   - 重复上面的步骤创建更多物品。
3. **创建数据表节点**：在 `Main.tscn` 里新建 `Node`，命名 `ItemTable`，挂 `data_table.gd`。Inspector 里：
   - `Resource Dir` = `res://data/items`
   - `Json Path`（可选）= `res://data/items.json`
   - `Debug Reload Key` = `F9`
4. **注册成服务**（配合 T23），方便全局访问：

```gdscript
func _ready() -> void:
	ItemTable.load_from_dir(ItemTable.resource_dir)
	Services.register(&"item_table", ItemTable)
```

5. **业务代码里查询**：

```gdscript
func get_item_price(id: StringName) -> int:
	var table := Services.get_service(&"item_table") as DataTable
	return int(table.get_value(id, "price", 0))

func can_afford(id: StringName, money: int) -> bool:
	return money >= get_item_price(id)

func get_icon(id: StringName) -> Texture2D:
	var table := Services.get_service(&"item_table") as DataTable
	var res := table.get_resource(id)
	if res is ItemData:
		return (res as ItemData).icon
	return null
```

6. **准备一个 JSON 用于开发期热重载**（`res://data/items.json`）：

```json
{
  "rows": [
    {
      "id": "iron_sword",
      "display_name": "铁剑",
      "description": "普通但可靠。",
      "price": 120,
      "damage_bonus": 8,
      "tags": ["weapon"]
    },
    {
      "id": "potion",
      "display_name": "红药水",
      "description": "恢复 40 点生命。",
      "price": 30,
      "max_stack": 20,
      "heal_amount": 40,
      "tags": ["consumable"]
    }
  ]
}
```

7. 运行游戏，按 **F9**（调试构建下）触发重载。改一下 JSON 里的 `price`，再按 F9，打开商店看价格是否立刻变了——**不需要重启游戏**。
8. 用 `ItemTable.debug_dump(10)` 确认加载到的行数和内容。

#### 可调参数说明

| 参数 / 方法 | 所属 | 说明 |
| --- | --- | --- |
| `id` | DataRow | 唯一标识，必填 |
| `order` | DataRow | 排序权重 |
| `deprecated` | DataRow | 是否弃用 |
| `display_name` / `description` / `price` / `max_stack` | ItemData | 展示与数值字段 |
| `icon` | ItemData | 图标资源（强引用） |
| `heal_amount` / `damage_bonus` | ItemData | 效果数值 |
| `tags` | ItemData | 分类标签数组 |
| `resource_dir` | DataTable | .tres 目录 |
| `json_path` | DataTable | JSON 路径 |
| `auto_load` | DataTable | 是否 `_ready` 自动加载 |
| `debug_reload_key` | DataTable | 热重载按键，默认 `F9` |
| `get_value(id, key, default)` | DataTable | 取字段（最常用） |
| `filter_by_tag(tag)` | DataTable | 按标签筛选 |
| `get_ids_sorted_by(key)` | DataTable | 按字段排序 |

#### 进阶改造提示

- **配表校验**：写一个 `validate()` 方法，检查"所有 `id` 唯一""`price` 非负""`max_stack` > 0"，在 `_ready` 里跑一遍并打印错误。**项目越大，这一步越值钱**——它能把"策划填错数据导致游戏崩溃"提前到启动时发现。
- **表间引用**：在 JSON 里用 `"drop_table": "goblin_drops"` 这样的字符串外键，加载后统一做一次"引用完整性检查"。
- **CSV 工作流**：如果策划坚持用 Excel，可以导出 CSV 后用 `FileAccess.get_csv_line()` 读取。字段名从第一行读，后续行按列组装成 Dictionary，然后走和 JSON 一样的路径进入 `_rows`。
- **本地化文本**：不要把"显示名"硬编码在配表里。正确做法是配表里存 `"display_name_key": "ITEM_IRON_SWORD"`，然后用 `tr()` 取值。这样一份配表能支持多语言。
- **热重载的边界**：F9 热重载只在**编辑器里运行时**有效，因为导出后 `res://` 是只读的（在 pck 内部）。**这是特性，不是缺陷**——正式版不应该允许玩家改数值。
- **和存档的关系**：**永远不要在存档里存整行配置数据**，只存 `id` 和数量。读取时用 `id` 去表里查。这样你改数值后，老存档会自动使用新数值——这正是"数据驱动"的核心价值。

---

## 34.6 模板 T26：SceneRouter 场景路由器

### 模板 T26：SceneRouter 场景路由器

**用途**：统一管理场景切换。提供**淡入淡出转场**、**带进度条的异步加载**、**向下一个场景传参**、**返回上一场景**四件套。

**依赖**：建议做成 Autoload（注册为 `Router`）。

**文件位置建议**：`res://autoload/scene_router.gd`

#### 完整代码

```gdscript
extends CanvasLayer

## ============================================================
## 场景路由器（Autoload 名称建议：Router）
## ------------------------------------------------------------
## 设计要点一：为什么继承 CanvasLayer 而不是 Node？
##   因为路由器需要一个"盖在所有内容之上"的遮罩来做淡入淡出。
##   继承 CanvasLayer 后，遮罩天然处于独立绘制层，
##   不会被任何相机的移动或缩放影响。
##
## 设计要点二：为什么用 change_scene_to_packed 而不是 change_scene_to_file？
##   change_scene_to_file 内部会同步加载，加载大场景时画面会卡死。
##   我们先异步加载成 PackedScene，加载完再一次性换掉，
##   卡顿就变成了"遮罩上的进度条"。
##
## 设计要点三：为什么转场必须用 await 而不是回调？
##   转场是典型的"线性时序"逻辑：
##     淡出 → 加载 → 切换 → 淡入
##   用回调要拆成四五个函数，还会跨帧丢状态；
##   用 await 写成一段直线代码，可读性和可维护性都好得多。
##   （如果某个项目的编码规范禁止协程，再改回信号链也不迟。）
##
## 设计要点四：为什么参数要"放在路由器上"而不是"传给新场景构造函数"？
##   因为 Godot 切换场景时会自己实例化新场景，我们无法插手它的
##   构造函数。所以唯一的通道就是"全局中转站"——路由器。
##   新场景在 _ready 里主动来取，取走即清空（take_params），
##   这样能自然防止"上一局的参数泄漏到下一局"。
##
## 设计要点五：为什么 _start_transition 要加 _busy 锁？
##   玩家在淡出动画期间疯狂点按钮，会触发多次切换请求。
##   没有锁的话会出现"加载 A 加载到一半又去加载 B"的竞态，
##   最坏情况是场景树处于半切换状态导致崩溃。
## ============================================================

## 转场开始时广播
signal transition_started(path: String)
## 加载进度变化（0.0 ~ 1.0）。进度条连它。
signal load_progress_changed(ratio: float)
## 转场完全结束（新场景已就绪且遮罩已淡出）
signal transition_finished(path: String)

## 传参数给下一个场景。新场景在 _ready 里调用 take_params() 取走。
var scene_params: Dictionary = {}

## 遮罩颜色
@export var fade_color: Color = Color(0, 0, 0)

var _fade: ColorRect
var _busy: bool = false
var _history: Array[String] = []

var _pending_path: String = ""
var _pending_params: Dictionary = {}
var _pending_fade_in: float = 0.0

var _loading: bool = false
var _load_progress: float = 0.0


func _ready() -> void:
	# 层级设高，保证遮罩盖在所有 UI 之上；想让它盖住某个特定 UI 就调它
	layer = 128
	# 转场期间即使游戏处于暂停状态，也必须继续跑，
	# 否则"从暂停菜单退回主菜单"这类流程会卡住。
	process_mode = Node.PROCESS_MODE_ALWAYS

	_fade = ColorRect.new()
	_fade.name = "FadeRect"
	_fade.set_anchors_preset(Control.PRESET_FULL_RECT)
	_fade.color = Color(fade_color.r, fade_color.g, fade_color.b, 0.0)
	_fade.mouse_filter = Control.MOUSE_FILTER_IGNORE
	_fade.visible = false
	add_child(_fade)


func _process(_delta: float) -> void:
	if not _loading:
		return

	# 第二个参数必须是一个数组，引擎会往它的第 0 项写入进度
	var progress: Array = [0.0]
	var status := ResourceLoader.load_threaded_get_status(_pending_path, progress)
	_load_progress = float(progress[0])
	load_progress_changed.emit(_load_progress)

	match status:
		ResourceLoader.THREAD_LOAD_IN_PROGRESS:
			pass   # 继续等
		ResourceLoader.THREAD_LOAD_LOADED:
			_loading = false
			_finish_transition()
		_:
			# THREAD_LOAD_FAILED / THREAD_LOAD_INVALID_RESOURCE
			push_error("SceneRouter: 加载失败 %s" % _pending_path)
			_loading = false
			_busy = false
			await _fade_to(0.0, 0.2)
			_fade.visible = false


# ============================================================
# 对外接口
# ============================================================

## 切换到目标场景（最简单的用法，全用默认参数）
func goto(path: String) -> void:
	goto_scene(path, {}, 0.3, 0.3)


## 完整版：切换场景
## path      目标场景路径，例如 "res://scenes/level_2.tscn"
## params    要传给新场景的参数（新场景用 take_params() 取）
## fade_out  淡出时长（秒），0 表示不淡出
## fade_in   淡入时长（秒），0 表示不淡入
func goto_scene(path: String, params: Dictionary = {},
		fade_out: float = 0.3, fade_in: float = 0.3) -> void:
	if path.is_empty():
		push_warning("SceneRouter: 空路径，已忽略")
		return
	# 同一个场景重复请求也直接忽略（防止"停在主菜单上点开始"重复加载）
	if path == _current_scene_path() and not _busy:
		return
	_start_transition(path, params, fade_out, fade_in, true)


## 返回上一场景（栈式回退）
func go_back(params: Dictionary = {},
		fade_out: float = 0.3, fade_in: float = 0.3) -> void:
	if _history.is_empty():
		push_warning("SceneRouter: 没有上一场景可返回")
		return
	var prev: String = _history.pop_back()
	# record_history = false：回退时不再把当前场景压栈，
	# 否则"前进一步再后退"会来回横跳。
	_start_transition(prev, params, fade_out, fade_in, false)


## 重启当前场景（"重试本关"）
func reload_current(params: Dictionary = {},
		fade_out: float = 0.25, fade_in: float = 0.25) -> void:
	var cur := _current_scene_path()
	if cur.is_empty():
		push_warning("SceneRouter: 无法确定当前场景路径")
		return
	_start_transition(cur, params, fade_out, fade_in, false)


## 取走参数：取一次就清空，避免参数"漏"到下一个场景
func take_params() -> Dictionary:
	var p := scene_params
	scene_params = {}
	return p


## 看一眼参数但不拿走
func peek_params() -> Dictionary:
	return scene_params


## 是否正在转场（UI 可以用它禁用按钮）
func is_transitioning() -> bool:
	return _busy


## 当前加载进度
func get_load_progress() -> float:
	return _load_progress


func get_history_size() -> int:
	return _history.size()


func clear_history() -> void:
	_history.clear()


# ============================================================
# 内部实现
# ============================================================

## 真正干活的地方。所有 goto 接口都汇聚到这里。
func _start_transition(path: String, params: Dictionary,
		fade_out: float, fade_in: float, record_history: bool) -> void:
	if _busy:
		push_warning("SceneRouter: 正在转场中，本次请求被忽略（%s）" % path)
		return

	_busy = true
	_pending_path = path
	_pending_params = params
	_pending_fade_in = fade_in
	transition_started.emit(path)

	if record_history:
		var cur := _current_scene_path()
		if not cur.is_empty():
			_history.append(cur)

	# 1) 淡出到全屏遮罩
	if fade_out > 0.0:
		_fade.visible = true
		await _fade_to(1.0, fade_out)
	else:
		_fade.color.a = 1.0
		_fade.visible = true

	# 2) 开始异步加载
	_load_progress = 0.0
	var err := ResourceLoader.load_threaded_request(path, "PackedScene")
	if err != OK:
		push_error("SceneRouter: 无法开始加载 %s（错误码 %d）" % [path, err])
		_loading = false
		_busy = false
		await _fade_to(0.0, 0.2)
		_fade.visible = false
		return

	_loading = true
	# 注意：这里不 await，加载进度由 _process 轮询。
	# _process 检测到加载完成后会调用 _finish_transition()。


## 加载完成：真正切换场景，然后淡入
func _finish_transition() -> void:
	var packed: PackedScene = ResourceLoader.load_threaded_get(_pending_path)
	if packed == null:
		push_error("SceneRouter: 加载结果为空 %s（文件可能不是 PackedScene）" % _pending_path)
		_busy = false
		await _fade_to(0.0, 0.2)
		_fade.visible = false
		return

	# 先把参数放好，再切场景——顺序不能反！
	# 因为新场景的 _ready 可能会立刻调用 take_params()。
	scene_params = _pending_params

	var err := get_tree().change_scene_to_packed(packed)
	if err != OK:
		push_error("SceneRouter: 切换场景失败（错误码 %d）" % err)
		_busy = false
		await _fade_to(0.0, 0.2)
		_fade.visible = false
		return

	# 等一帧，让新场景完成 _ready 与首帧布局，
	# 再开始淡入，避免看到"半成品"画面
	await get_tree().process_frame

	var fi := _pending_fade_in
	if fi > 0.0:
		await _fade_to(0.0, fi)
	else:
		_fade.color.a = 0.0

	_fade.visible = false
	_busy = false
	transition_finished.emit(_pending_path)


## 把遮罩透明度渐变到目标值
func _fade_to(target_alpha: float, duration: float) -> void:
	if duration <= 0.0:
		_fade.color.a = target_alpha
		return
	var t := create_tween()
	t.set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_IN_OUT)
	t.tween_property(_fade, "color:a", target_alpha, duration)
	await t.finished


## 取当前场景的资源路径
func _current_scene_path() -> String:
	var cs := get_tree().current_scene
	if cs == null:
		return ""
	return cs.scene_file_path
```

#### 使用方法

1. **准备场景**：确保目标场景都保存为 `.tscn` 文件，例如 `res://scenes/main_menu.tscn`、`res://scenes/level_1.tscn`。
2. **注册 Autoload**：**Project → Project Settings → Autoload**，添加 `res://autoload/scene_router.gd`，节点名填 `Router`。
3. **设置主场景**：**Project Settings → Application → Run → Main Scene** 设为 `res://scenes/main_menu.tscn`。
4. **最简单的切换**（主菜单 → 关卡）：

```gdscript
extends Control
## 主菜单

func _on_start_button_pressed() -> void:
	Router.goto_scene("res://scenes/level_1.tscn")

func _on_settings_button_pressed() -> void:
	Router.goto_scene("res://scenes/settings.tscn", {}, 0.2, 0.2)
```

5. **带参数切换**——发送方：

```gdscript
func _on_level_button_pressed(level_index: int, difficulty: StringName) -> void:
	Router.goto_scene("res://scenes/level_1.tscn", {
		"level_index": level_index,
		"difficulty": difficulty,
		"spawn_point": "entry_a",
		"carry_over_hp": GameState.player_hp,
	}, 0.3, 0.3)
```

   接收方（新场景的根节点脚本）：

```gdscript
extends Node2D
## level_1

@onready var player: CharacterBody2D = $Player

func _ready() -> void:
	var params := Router.take_params()
	if params.is_empty():
		# 直接按 F6 单独运行本场景时，参数是空的。
		# 这时给一套默认值，保证场景能独立调试——这很重要！
		params = {
			"level_index": 1,
			"difficulty": &"normal",
			"spawn_point": "default",
		}

	player.global_position = get_spawn_position(params.get("spawn_point", "default"))

	if params.has("carry_over_hp"):
		GameState.player_hp = int(params["carry_over_hp"])

	print("进入关卡 %d，难度 %s" % [params.get("level_index", 0), params.get("difficulty", &"normal")])
```

6. **返回上一场景**：

```gdscript
func _on_back_button_pressed() -> void:
	Router.go_back({"from": "settings"})
```

7. **带进度条的加载画面**：如果你有专门的加载场景，可以给进度条接上信号：

```gdscript
extends Control
## 加载界面

@onready var bar: ProgressBar = $ProgressBar
@onready var label: Label = $ProgressLabel

func _ready() -> void:
	Router.load_progress_changed.connect(_on_progress)
	Router.transition_finished.connect(_on_finished)

func _on_progress(ratio: float) -> void:
	bar.value = ratio * 100.0
	label.text = "%d%%" % int(ratio * 100.0)
```

   > 对于大多数中小项目，`_load_progress` 会瞬间从 0 跳到 1（场景太小，加载太快）。这很正常，进度条主要是给大型场景准备的。

8. **重试本关**：

```gdscript
func _on_retry_pressed() -> void:
	Router.reload_current()
	# 也可以带上"保留分数"之类的参数：
	# Router.reload_current({"keep_score": true})
```

9. **切场景时清理服务**（配合 T23）：

```gdscript
func _exit_tree() -> void:
	Services.clear()
```

   > 注意：只有在你的 `Services` 确实"随场景存活"时才需要清。如果你把 `Services` 做成了 Autoload 且注册的都是长生命周期对象，则没必要清。

#### 可调参数说明

| 参数 / 方法 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `fade_color` | `Color` | 黑 | 遮罩颜色，可改成白/深蓝做风格化转场 |
| `layer` | `int` | `128` | 遮罩层级，要比所有 UI 高 |
| `goto(path)` | 方法 | — | 最简切换，默认 0.3s 淡入淡出 |
| `goto_scene(path, params, fade_out, fade_in)` | 方法 | `{}`, `0.3`, `0.3` | 完整切换 |
| `go_back(params, fade_out, fade_in)` | 方法 | `{}`, `0.3`, `0.3` | 返回上一场景 |
| `reload_current(params, ...)` | 方法 | `{}` | 重载当前场景 |
| `take_params()` | 方法 | — | 取走并清空参数 |
| `peek_params()` | 方法 | — | 查看但不取走 |
| `is_transitioning()` | 方法 | — | 是否正在转场 |
| `transition_started` | 信号 | — | 转场开始 |
| `load_progress_changed` | 信号 | — | 加载进度 0~1 |
| `transition_finished` | 信号 | — | 转场完成 |

#### 进阶改造提示

- **转场样式多样化**：把 `ColorRect` 换成一个 `TextureRect` 并给它挂 ShaderMaterial，就能做"圆形擦除""百叶窗""溶解"等转场效果。`_fade_to` 里的逻辑只需改成驱动 shader 的 `progress` uniform 即可。
- **给"独立运行"兜底**：`take_params()` 在空字典时回退到默认值这一步非常关键。**每个场景都应该能单独按 F6 运行**，否则你会失去"只调这一个场景"的能力，开发效率会断崖式下跌。
- **加载失败的用户体验**：目前加载失败只是淡回原画面。更好的做法是弹一个提示框"资源加载失败，请重试"，并记录日志。玩家看不懂控制台报错。
- **内存提醒**：`change_scene_to_packed` 会释放旧场景（连同它的所有子节点）。如果你需要"切场景时保留某个对象"（例如背景音乐播放器），请把它做成 Autoload，或调用 `get_tree().root.remove_child(node)` 把它摘出来再挂到别处。
- **同步版本**：如果你的场景小到加载不到 10ms，可以直接用 `get_tree().change_scene_to_file(path)` 加一个纯淡出，省掉异步轮询的一整套状态机。**不要为了"架构完整"而引入不必要的复杂度。**
- **注意信号断开**：`Router` 是 Autoload，常驻不销毁。如果某个场景把自己连到了 `Router.load_progress_changed`，**在 `_exit_tree()` 里一定要断开**，否则场景销毁后信号回调会指向已释放的对象，触发 "Attempt to call function on a previously freed instance"。

---

## 34.7 本章小结

- **架构的目的是"改需求时少改文件"**：本章六个模板都不产生游戏功能，它们唯一的产出是"降低你未来修改代码的成本"。判断一个架构好坏的标准，不是"代码漂亮"，而是"加一个新需求要动几个文件"。
- **T21 ObjectPool 的两个核心选择**：用"数组而不是字典"来天然记录借出顺序；用"留在树里 + 禁用处理"而不是"反复 add_child/remove_child"来获得零成本激活。
- **T21 必须监听 `tree_exited`**：业务代码里难免有人手滑 `queue_free()`，不兜底就会留下悬空引用，这是最典型的"偶发崩溃"来源。
- **T21 的三种溢出策略各有用途**：子弹用 `RECYCLE_OLDEST`（最新的一定能打出去）、掉落物用 `DROP`（少一个无所谓）、过场演员用 `GROW`（绝对不能缺）。
- **T21 与第 30 章 BulletPool 是互补而非替代**：通用池管生命周期，专用池管业务语义。项目里应该**通用池当底座、专用脚本当业务**。
- **T22 的两条正道**：需要 `get_tree()`、需要 `_process`、需要挂子节点的，用 **Autoload**；纯数据、纯函数的，用 **静态变量单例**。
- **T22 的 Autoload 初始化顺序由 Project Settings 的列表决定**：`Settings` 必须排在 `SaveSystem` 前面，否则 `_ready` 里会取不到值。这是最高频的单例翻车原因。
- **T22 的单例别超过 5 个**：单例本质是全局变量，用多了等于把"面条代码"换个形式重新写一遍。
- **T22 的 `Engine.has_singleton()` 查不到 Autoload**：它只查引擎原生单例。判断 Autoload 是否存在要用 `get_node_or_null("/root/名字")`。
- **T23 ServiceLocator 是"可撤销的 Autoload"**：Autoload 永久存在，服务可以随场景销毁。**永久的东西用 Autoload，随场景的东西用服务定位器。**
- **T23 的最佳实践是"服务名集中成常量"**：把字符串拼写错误从"运行时报错"提前到"编辑器报错"，这是投入产出比极高的一步。
- **T23 要监听 `tree_exited` 自动注销**：否则关卡切换后注册表里会留下指向已释放节点的"幽灵服务"。
- **T24 Command 模式解决的是"撤销"这一类需求**：回合制、建造、解谜、卡牌、编辑器工具都用得上。注意 Godot 自带的 `UndoRedo` 是给编辑器插件用的，**游戏里用自己写的 `Command` 更合适**。
- **T24 的头号坑是"记录理论值而不是实际值"**：治疗溢出、伤害减免、上限截断——凡是数值可能被夹紧的地方，都必须在 `execute()` 里记录**真实发生的变化**，否则 `undo()` 会算错账。
- **T24 的 `CommandGroup.undo()` 必须逆序执行**：正向是"扣钱 → 加道具"，逆向就必须是"减道具 → 还钱"。顺序错了中间状态会出现负数。
- **T24 不要把有副作用的东西放进命令里**：播声音、弹飘字是不可逆的，放进 `execute()` 会导致撤销时听到"倒放"。副作用放在调用方。
- **T25 数据驱动的最大价值是"改数值不用改代码"**：而且因为存档只存 `id`，改完数值后**老存档会自动使用新数值**。
- **T25 用自定义 Resource 还是 JSON，取决于工作流**：策划直接编辑 → `.tres`（有类型检查、能拖资源）；Excel 导出 / 热更新 → JSON。两者可以并存，JSON 后加载以覆盖个别行。
- **T25 一定要做启动时校验**：`id` 唯一性、数值非负、外键存在。这一小段代码能把"上线后突然崩溃"提前到"启动时报警"。
- **T25 不要本地化文本硬编码在表里**：存 `display_name_key` 配合 `tr()`，一份数据支持多语言。
- **T26 SceneRouter 用 `change_scene_to_packed` 而不是 `change_scene_to_file`**：先异步加载再一次性替换，把"卡死"变成"进度条"。
- **T26 的参数必须放在路由器上**：因为 Godot 自己实例化新场景，我们无法插手构造函数，全局中转站是唯一通道。而 `take_params()` 的"取走即清空"能防止参数跨局泄漏。
- **T26 的 `_busy` 锁不是可选项**：没有它，玩家连点两次按钮就会触发两次加载，竞态下可能出现半切换状态。
- **T26 的每个场景都必须能"单独按 F6 运行"**：`take_params()` 为空时回退到默认值，是保证调试效率的关键设计。
- **六个模板的组合用法**：`Router` 负责场景、`Services` 负责模块寻址、`ObjectPool` 负责高频对象、`Command` 负责可撤销操作、`DataTable` 负责数值、`GameState` 负责全局状态。**它们组合起来，就是一个可以直接启动新项目的骨架。**
- **最后一句忠告**：**不要一上来就把六个模板全用上。** 先用最笨的方式把玩法做出来，等你真的感觉到"这里改起来好痛"的时候，再回来把对应的模板引进去。**架构是为痛苦准备的解药，不是为炫耀准备的装饰。**
---

# 第六卷 · 收尾（综合项目 / 速查 / 报错 / 迁移）

# 第 35 章：综合小项目——把一切串起来

> 前面 34 章，我们学完了语法、引擎交互、模块模板。但知识如果不串起来用，就只是一堆散落的零件。这一章，我们要从**一个空项目**开始，一步一步做出一个**完整可运行的小游戏**：俯视角生存射击（俗称"割草"）。
>
> 它的乐趣在于：**你只需要移动和瞄准，敌人会自己成波涌来，你唯一要做的就是活下去、变强、拿高分。** 玩法简单，但麻雀虽小五脏俱全——移动、射击、敌人 AI、血量闭环、波次生成、掉落、HUD、存档、设置，一样不少。
>
> 学习本章的正确姿势：**不要复制粘贴就完事**。每读完一步，自己动手敲一遍，并问自己："这一步用到了前面第几章的知识？为什么非这么做不可？" 这样走完，你才真正"通关"了这本书。

## 35.1 项目概览

### 35.1.1 目标玩法

我们要做的游戏，核心循环是这样的：

| 阶段 | 玩家在做什么 | 系统在做什么 |
| --- | --- | --- |
| 准备 | 在开始界面点"开始游戏" | 清空存档中的临时数据，加载主场景 |
| 移动 | 按 WASD 四处跑动、走位拉扯 | 八方向移动、速度归一化、滑步 |
| 射击 | 只用鼠标瞄准，枪自动开火 | 冷却计时、生成子弹、对象池回收 |
| 生存 | 躲避敌人、靠拾取变强 | 敌人成波追击、随时间变强 |
| 反馈 | 看到飘字、屏幕震动、血条变化 | 伤害计算、飘字、震动、音效 |
| 死亡 | 血量归零 | 结算分数、写入最高分、显示结算界面 |
| 重开 | 点"再来一局" | 场景重载，波次与分数归零 |

一句话概括：**"移动 + 自动射击 + 波次敌人 + 掉落成长 + 计分结算"**。

### 35.1.2 完整功能清单

先把"要做什么"列成一张表。**做项目最忌讳一上来就想全，功能清单能帮你把"必须做"和"想做"分开。**

| 编号 | 功能 | 优先级 | 依赖的前置知识 | 关联模板 |
| --- | --- | --- | --- | --- |
| F01 | 玩家八向移动 | 必须 | 第 5、25 章（运算符、向量归一化） | — |
| F02 | 鼠标瞄准旋转 | 必须 | 第 24 章（节点变换） | — |
| F03 | 自动射击（带冷却） | 必须 | 第 12 章（时间）、第 30 章（对象池） | T21 ObjectPool |
| F04 | 子弹飞行与命中 | 必须 | 第 16 章（Area2D）、第 30 章 | — |
| F05 | 敌人追击玩家 | 必须 | 第 25 章（点积、方向） | — |
| F06 | 血量与伤害闭环 | 必须 | 第 31 章（组件） | T01 HealthComponent、T02 伤害计算器 |
| F07 | 伤害飘字 | 强烈建议 | 第 33 章（反馈） | T15 DamageNumber |
| F08 | 受伤闪烁 + 屏幕震动 | 强烈建议 | 第 33 章 | T14 ScreenShake、T19 ScreenFlash |
| F09 | 波次生成 + 难度递增 | 必须 | 第 31 章 | T10 WaveSpawner |
| F10 | 掉落与自动拾取 | 必须 | 第 16 章（Area2D） | — |
| F11 | HUD（血条/分数/波次） | 必须 | 第 21 章（信号解耦） | T05 EventBus |
| F12 | 暂停菜单 | 必须 | 第 13 章（process_mode） | — |
| F13 | 场景流程（开始/游戏/结算） | 必须 | 第 34 章 | T26 SceneRouter |
| F14 | 最高分存档 | 必须 | 第 28 章（文件读写） | T20 SettingsManager |
| F15 | 音量设置 | 建议 | 第 28 章 | T16 AudioManager、T20 |

### 35.1.3 目录结构规划

一个项目乱不乱，很大程度取决于"文件放哪儿"。我们采用最稳妥的分层：

```text
res://
├── project.godot              # 项目设置（Autoload、输入映射都在这里配）
├── autoload/                  # 全局单例（常驻内存，跨场景）
│   ├── event_bus.gd           # 事件总线（T05）：所有跨模块信号的中转站
│   ├── audio_manager.gd       # 音频管理（T16）：BGM/音效/音量分组
│   ├── settings_manager.gd    # 设置持久化（T20）：音量/画质/按键
│   └── scene_router.gd        # 场景路由（T26）：带淡入淡出的场景切换
├── scripts/                   # 各类游戏逻辑脚本（纯 .gd，不含场景）
│   ├── actors/
│   │   ├── player.gd
│   │   ├── enemy.gd
│   │   └── bullet.gd
│   ├── components/
│   │   ├── health_component.gd   # T01：可复用的血量组件
│   │   └── hit_flash.gd          # T19：受伤闪烁
│   ├── systems/
│   │   ├── damage_calculator.gd  # T02：伤害计算器（静态类）
│   │   └── wave_spawner.gd       # T10：波次生成器
│   ├── pickups/
│   │   └── pickup.gd
│   └── ui/
│       ├── hud.gd
│       └── main_menu.gd
├── scenes/                    # 场景文件（.tscn），按角色/界面分类
│   ├── main.tscn              # 主游戏场景（游戏世界容器）
│   ├── actors/
│   │   ├── player.tscn
│   │   ├── enemy.tscn
│   │   └── bullet.tscn
│   ├── pickups/
│   │   └── pickup.tscn
│   └── ui/
│       ├── main_menu.tscn
│       ├── hud.tscn
│       ├── pause_menu.tscn
│       └── game_over.tscn
├── resources/                 # 自定义资源（数据驱动，见第 32 章）
│   ├── enemies/
│   │   └── slime.tres         # 敌人数值表
│   └── waves/
│       └── wave_curve.tres    # 难度曲线
└── assets/                    # 美术与音频原始资源
    ├── sprites/
    └── audio/
```

**为什么要这么分？一句话理由：**

| 目录 | 分类依据 | 理由 |
| --- | --- | --- |
| `autoload/` | 按"生命周期" | 只有常驻全局的东西才放这里，一眼就知道谁是单例 |
| `scripts/` | 按"职责角色" | 逻辑脚本和场景分离，方便版本管理时看 diff |
| `scenes/` | 按"界面/角色" | 场景文件是"装配图"，天然按用途分类 |
| `resources/` | 按"数据" | 数值和代码分开，改数值不用动代码（第 32 章） |
| `assets/` | 按"原始素材" | 美术音频不参与逻辑，单独隔离 |

> **新手最常犯的错**：把所有 `.gd` 和 `.tscn` 都堆在根目录。等文件超过 30 个，你会连"玩家脚本在哪"都要找半天。**目录结构是给未来的自己省时间的。**

---

## 35.2 第 1 步：项目与自动加载配置

### 35.2.1 创建项目

打开 Godot 4.3，新建项目，渲染后端选 **Forward+**（2D 项目其实 Compatibility 也够，但 Forward+ 更通用）。项目名随意，比如 `survivor_demo`。

**为什么一开始就确定渲染后端？** 因为中途切换需要重启编辑器且可能影响材质，早定早省心。

### 35.2.2 注册 Autoload

Autoload 是"常驻内存的全局单例"。本项目用 4 个：

| Autoload 名 | 脚本 | 职责 | 来自模板 |
| --- | --- | --- | --- |
| `EventBus` | `res://autoload/event_bus.gd` | 全局信号中转（跨模块解耦） | T05 |
| `AudioManager` | `res://autoload/audio_manager.gd` | 播放 BGM/音效、音量分组 | T16 |
| `SettingsManager` | `res://autoload/settings_manager.gd` | 读写音量/最高分等设置 | T20 |
| `SceneRouter` | `res://autoload/scene_router.gd` | 带淡入淡出的场景切换 | T26 |

**配置步骤**：菜单 `项目 → 项目设置 → 全局（Autoload）`，在"路径"里选脚本，在"节点名"里填名字，点"添加"。

**顺序要求（重要）**：`SettingsManager` 必须排在 `AudioManager` 前面。因为 `AudioManager._ready()` 里会去读 `SettingsManager` 的音量值，顺序反了会读到空值。这正是第 34 章强调过的"Autoload 初始化顺序由列表决定"。

推荐顺序：

```text
SettingsManager
AudioManager
EventBus
SceneRouter
```

### 35.2.3 输入映射

打开 `项目设置 → 输入映射`，添加以下动作（Action）：

| 动作名 | 绑定按键 | 用途 |
| --- | --- | --- |
| `move_left` | A / 左方向键 | 向左移动 |
| `move_right` | D / 右方向键 | 向右移动 |
| `move_up` | W / 上方向键 | 向上移动 |
| `move_down` | S / 下方向键 | 向下移动 |
| `shoot` | 鼠标左键 | 开火（本项目可设为"按住即自动开火"） |
| `pause` | Esc / P | 暂停/恢复 |

**为什么必须用输入映射而不是直接 `Input.is_key_pressed(KEY_W)`？**

1. **可改键**：玩家想改成方向键？改映射即可，代码一行不动。
2. **语义清晰**：代码里 `Input.is_action_pressed("move_left")` 比 `KEY_A` 更能表达意图，也支持手柄摇杆。
3. **可复用**：一个动作可以绑多个按键/手柄轴。

```gdscript
# 读取输入的正确写法（推荐，向量合成为一行）
var input_dir := Input.get_vector("move_left", "move_right", "move_up", "move_down")
```

`Input.get_vector()` 会自动处理"同时按两个方向"和"手柄死区"，比手写四个 `if` 优雅得多。

### 35.2.4 事件总线脚本（第一个 Autoload）

```gdscript
# res://autoload/event_bus.gd
extends Node
## 事件总线（T05）：所有"跨模块"信号都集中定义在这里。
## 好处：A 模块不需要知道 B 模块的存在，只需往总线发信号。

# ---- 玩家相关 ----
signal player_spawned(player: Node2D)      # 玩家出生，UI/敌人可据此拿引用
signal player_health_changed(cur: int, max_hp: int)  # 血量变化，血条监听
signal player_died                         # 玩家死亡，结算界面监听
signal player_level_changed(level: int)    # 玩家升级（道具累计经验）

# ---- 战斗相关 ----
signal damage_dealt(target: Node, amount: int, is_crit: bool)  # 造成伤害，飘字监听
signal enemy_killed(kill_count: int, score: int)               # 击杀敌人，计分
signal screen_shake_requested(strength: float, duration: float)  # 请求震屏

# ---- 流程相关 ----
signal wave_started(wave_index: int, enemy_count: int)  # 新一波开始
signal wave_cleared(wave_index: int)                    # 本波清空
signal game_over(final_score: int, is_new_record: bool)  # 游戏结束
signal game_paused(is_paused: bool)                     # 暂停状态变化

# ---- 拾取相关 ----
signal pickup_collected(kind: int, value: float)  # 拾到道具
```

> **注意**：EventBus 里**只定义信号，不写业务逻辑**。它可以有极少量辅助函数，但严禁在里面写"游戏规则"。一旦它开始处理逻辑，就会变成谁都想改的"上帝对象"。

---

## 35.3 第 2 步：玩家节点

### 35.3.1 节点结构

在 `scenes/actors/player.tscn` 里搭一个这样的树：

```text
Player (CharacterBody2D)          <- 挂 player.gd
├── Sprite2D                      <- 玩家贴图（枪口朝右，方便旋转对齐）
├── CollisionShape2D              <- 圆形碰撞体，半径约 12px
└── Muzzle (Marker2D)             <- 枪口位置，子节点随父旋转，子弹从这出膛
```

**为什么用 `CharacterBody2D` 而不是 `Area2D`？**

- `Area2D` 只做"侦测重叠/进入离开"，**不会被物理阻挡**，玩家会穿墙、穿怪。
- `CharacterBody2D` 提供 `move_and_slide()`，能自动处理"撞到东西就停下/沿墙滑行"，是俯视角角色的标准选择。

**为什么贴图要"枪口朝右"？** 因为 Godot 的旋转角度 0 弧度对应"向右"。贴图朝右，`rotation = 角度` 才能直接和"瞄准方向"对齐，省掉一个 ±90° 的偏移量。

### 35.3.2 玩家移动脚本

```gdscript
# res://scripts/actors/player.gd
extends CharacterBody2D
class_name Player

# ---- 可调参数（用 @export 可以在检查器里改，见第 24 章注解） ----
@export var move_speed: float = 220.0        # 移动速度（像素/秒）
@export var acceleration: float = 2000.0     # 加速度，值越大越"跟手"
@export var friction: float = 1800.0         # 无输入时的减速度
@export var max_health: int = 100

# ---- 预加载子弹场景（第 30 章对象池会用到） ----
const BULLET_SCENE := preload("res://scenes/actors/bullet.tscn")

@onready var sprite: Sprite2D = $Sprite2D
@onready var muzzle: Marker2D = $Muzzle

var _aim_direction: Vector2 = Vector2.RIGHT   # 当前瞄准方向（单位向量）
var _shoot_cooldown: float = 0.0              # 剩余冷却时间

func _ready() -> void:
	# 通过事件总线广播"我出生了"，UI 和敌人系统据此拿引用
	EventBus.player_spawned.emit(self)

func _physics_process(delta: float) -> void:
	_handle_movement(delta)   # 先处理移动
	_handle_aiming()          # 再处理朝向
	_handle_shooting(delta)   # 最后处理开火

func _handle_movement(delta: float) -> void:
	# 第 5 章：Vector2 支持加减乘除；第 25 章：归一化让斜向不加速
	var input_dir := Input.get_vector("move_left", "move_right", "move_up", "move_down")
	# get_vector 已经保证了最大长度为 1，所以无需再 normalize()
	var target_velocity := input_dir * move_speed

	if input_dir != Vector2.ZERO:
		# move_toward：平滑逼近目标值，避免瞬时变速导致的"瞬移感"
		velocity = velocity.move_toward(target_velocity, acceleration * delta)
	else:
		velocity = velocity.move_toward(Vector2.ZERO, friction * delta)

	move_and_slide()

func _handle_aiming() -> void:
	# get_global_mouse_position 返回鼠标在"世界坐标"中的位置
	var mouse_pos := get_global_mouse_position()
	_aim_direction = (mouse_pos - global_position).normalized()  # 归一化为单位向量
	# 第 24 章：rotation 是弧度制；贴图朝右，所以方向角可直接用 angle()
	sprite.global_rotation = _aim_direction.angle()

func _handle_shooting(delta: float) -> void:
	_shoot_cooldown -= delta
	if _shoot_cooldown > 0.0:
		return
	if Input.is_action_pressed("shoot"):
		_shoot_cooldown = 0.15   # 冷却 0.15 秒，即约 6.7 发/秒
		_fire()

func _fire() -> void:
	# 直接 new 一个子弹；第 35.4 步会换成对象池版本
	var bullet: Node2D = BULLET_SCENE.instantiate()
	bullet.global_position = muzzle.global_position
	bullet.direction = _aim_direction
	get_tree().current_scene.add_child(bullet)
```

**关键知识点回顾：**

| 代码 | 用到第几章 |
| --- | --- |
| `Input.get_vector(...)` | 第 19 章（输入） |
| `move_toward` 平滑逼近 | 第 25 章（向量方法） |
| `normalized()` 归一化 | 第 25 章（向量） |
| `rotation` / `angle()` | 第 24 章（变换） |
| `@export` / `@onready` | 第 24 章（注解） |
| `_physics_process` | 第 12 章（生命周期） |

> **踩坑提醒**：新手常写成 `_process` 里做移动。**凡是和物理/碰撞相关的移动，都该放 `_physics_process`**，因为它以固定频率（默认 60Hz）运行，不会因帧率波动导致穿墙。`_process` 的频率随帧率变化，适合做纯视觉更新（如飘字）。

---

## 35.4 第 3 步：瞄准与射击

### 35.4.1 子弹节点结构

```text
Bullet (Area2D)                   <- 挂 bullet.gd
├── Sprite2D                      <- 子弹贴图
└── CollisionShape2D              <- 小圆形碰撞体
```

**为什么子弹用 `Area2D` 而不是 `CharacterBody2D`？**

子弹不需要"被阻挡后停下并贴墙"，它只需要"碰到敌人时上报并消失"。`Area2D` 的 `area_entered` / `body_entered` 信号正好满足。而且 `Area2D` 不做物理求解，几百发子弹也不掉帧。

### 35.4.2 子弹脚本

```gdscript
# res://scripts/actors/bullet.gd
extends Area2D
class_name Bullet

@export var speed: float = 700.0
@export var damage: int = 10
@export var pierce: int = 0        # 可穿透次数（0 表示命中即消失）
@export var lifetime: float = 1.5  # 最长存活时间，防止飞出屏幕永不回收

var direction: Vector2 = Vector2.RIGHT   # 由开火方在生成时赋值

func _ready() -> void:
	# 连接"进入区域"信号（第 21 章信号）
	area_entered.connect(_on_area_entered)
	# 到点自动回收，避免漏网子弹污染内存
	get_tree().create_timer(lifetime).timeout.connect(_recycle)

func _physics_process(delta: float) -> void:
	global_position += direction * speed * delta   # 每帧按方向平移

func _on_area_entered(area: Area2D) -> void:
	# 约定：敌人的受击区类型是 enemy_hurbox，用 is 判断（第 6 章类型判断）
	if area is Hurtbox:
		var hurtbox := area as Hurtbox
		hurtbox.take_damage(damage, self)
		pierce -= 1
		if pierce < 0:
			_recycle()

func _recycle() -> void:
	queue_free()   # 简化版；第 34 章 T21 会换成"归还对象池"
```

> **约定优于配置**：这里我们约定"敌人的受击区脚本类名是 `Hurtbox`"。用 `class_name Hurtbox` 定义后，`area is Hurtbox` 这种判断既准确又比字符串比较更安全（打错字会编译报错）。

### 35.4.3 引入对象池（第 30 / 34 章）

上面 `_fire()` 每发子弹都 `instantiate()` 再 `queue_free()`，每秒 6-7 发、打 10 分钟就是几千次分配——**垃圾回收压力大、偶发卡顿**。正确做法是用第 34 章 T21 的 **ObjectPool**。

```gdscript
# res://scripts/systems/bullet_pool.gd
extends Node
## 子弹专用池：包一层通用 ObjectPool，提供"取一发子弹"的语义。
## 知识来源：第 30 章（对象池概念）+ 第 34 章 T21（通用实现）。

const POOL_SIZE := 200
var _pool: Array[Node] = []   # 池中备用的子弹（已实例化但未激活）

func _ready() -> void:
	var scene := preload("res://scenes/actors/bullet.tscn")
	for i in POOL_SIZE:
		var b: Node2D = scene.instantiate()
		b.visible = false
		b.set_physics_process(false)   # 未激活的子弹不参与运算
		add_child(b)                   # 常驻在树里，激活时无需再加
		_pool.append(b)

func fire(pos: Vector2, dir: Vector2, dmg: int = 10) -> void:
	if _pool.is_empty():
		return   # 池空则这一发丢失（溢出策略：DROP）
	var b: Node2D = _pool.pop_back()   # 取最后一个：天然按借出顺序回收
	b.visible = true
	b.global_position = pos
	b.direction = dir
	b.damage = dmg
	b.set_physics_process(true)
	AudioManager.play_sfx("shoot")     # 播放开火音效

func recycle(b: Node2D) -> void:
	b.visible = false
	b.set_physics_process(false)
	b.global_position = Vector2(-10000, -10000)  # 移出屏幕，防止误碰撞
	_pool.append(b)
```

然后玩家的 `_fire()` 改成调用池：

```gdscript
func _fire() -> void:
	# 通过组名找到池（也可以在 _ready 里缓存引用，这里演示 get_first_node_in_group）
	var pool := get_tree().get_first_node_in_group("bullet_pool")
	pool.fire(muzzle.global_position, _aim_direction)
```

**对象池的两个核心思想（第 30 / 34 章）：**

1. **用数组而不是字典**：`pop_back()` 天然记录"最近借出的"并能按序回收，简单高效。
2. **留在树里 + 关掉处理**：`add_child` / `remove_child` 本身也有开销，用 `visible = false` + `set_physics_process(false)` 实现"零成本休眠"。

---

## 35.5 第 4 步：敌人

### 35.5.1 敌人节点结构

```text
Enemy (CharacterBody2D)            <- 挂 enemy.gd
├── Sprite2D
├── CollisionShape2D               <- 敌人自身的身体碰撞（用于和玩家碰撞）
├── Hurtbox (Area2D)               <- 受击区，挂 hurtbox.gd，class_name Hurtbox
│   └── CollisionShape2D
├── HealthComponent (Node)         <- T01 血量组件
└── HitFlash (Node)                <- T19 受伤闪烁（用 AnimationPlayer 或着色器）
```

**为什么要单独做一个 `Hurtbox`（受击区），而不是直接用身体的 `CollisionShape2D`？**

- **职责分离**：身体碰撞体负责"物理阻挡"，受击区负责"判定挨打"。两者大小往往不同——比如身体大、受击区略大一点更"好打"。
- **灵活定向**：以后要做"头部弱点 2 倍伤害"，只需在头上再挂一个 Hurtbox 并给它设置倍率，游戏逻辑不用改。
- **类型判断干净**：子弹只需判断 `area is Hurtbox`，不用去猜 `collision_layer` 的位掩码。

### 35.5.2 血量组件（T01）

```gdscript
# res://scripts/components/health_component.gd
extends Node
class_name HealthComponent
## 血量组件（T01）：任何"能挨打的东西"都挂一个，逻辑只写一次。

signal health_changed(cur: int, max_hp: int)
signal damaged(amount: int, source: Node)
signal died

@export var max_health: int = 30
var current_health: int = 0

func _ready() -> void:
	# 允许父节点覆盖初始血量（例如精英怪）
	if max_health <= 0:
		max_health = 1
	current_health = max_health

func take_damage(amount: int, source: Node = null) -> void:
	if current_health <= 0:
		return   # 已经死了，忽略后续伤害（防止重复触发 died）
	current_health -= amount
	current_health = max(current_health, 0)   # 第 36 章：clamp 也可，这里用 max
	damaged.emit(amount, source)
	health_changed.emit(current_health, max_health)
	if current_health == 0:
		died.emit()

func heal(amount: int) -> void:
	current_health = min(current_health + amount, max_health)
	health_changed.emit(current_health, max_health)
```

### 35.5.3 敌人脚本

```gdscript
# res://scripts/actors/enemy.gd
extends CharacterBody2D
class_name Enemy

@export var move_speed: float = 90.0
@export var attack_damage: int = 8
@export var attack_cooldown: float = 1.0
@export var score_value: int = 10
@export var drop_chance: float = 0.25   # 25% 概率掉落道具

@onready var health: HealthComponent = $HealthComponent
@onready var hurtbox: Hurtbox = $Hurtbox
@onready var sprite: Sprite2D = $Sprite2D

var _target: Node2D = null              # 追击目标（玩家）
var _attack_timer: float = 0.0
var _dead := false

func _ready() -> void:
	# 每只敌人单独克隆一份血量组件资源，避免共享 max_health
	health.damaged.connect(_on_damaged)
	health.died.connect(_on_died)
	# 从事件总线拿玩家引用（不硬编码路径）
	var p := get_tree().get_first_node_in_group("player")
	if p != null:
		_target = p

func _physics_process(delta: float) -> void:
	if _dead or _target == null:
		return
	_chase_and_attack(delta)

func _chase_and_attack(delta: float) -> void:
	# 第 25 章：方向 = 目标位置 - 自己位置，再归一化
	var to_target := (_target.global_position - global_position)
	if to_target.length() > 24.0:   # 距离大于 24px 就继续追
		var dir := to_target.normalized()
		velocity = dir * move_speed
	else:
		velocity = Vector2.ZERO
		# 贴身了，按冷却攻击
		_attack_timer -= delta
		if _attack_timer <= 0.0:
			_attack_timer = attack_cooldown
			_attack_player()
	move_and_slide()
	# 面朝玩家（用点积判断玩家在左还是在右，翻转贴图）
	if to_target.x != 0.0:
		sprite.flip_h = to_target.x < 0.0

func _attack_player() -> void:
	if _target.has_method("take_damage"):
		_target.take_damage(attack_damage, self)

func _on_damaged(amount: int, _source: Node) -> void:
	# 受到伤害：闪光 + 震屏 + 飘字（三种反馈一次给足，见第 33 章）
	var hf := get_node_or_null("HitFlash")
	if hf != null and hf.has_method("flash"):
		hf.flash()
	EventBus.screen_shake_requested.emit(3.0, 0.12)
	EventBus.damage_dealt.emit(self, amount, false)

func _on_died() -> void:
	if _dead:
		return
	_dead = true
	# 掉道具（概率）
	if randf() < drop_chance:
		_spawn_pickup()
	# 计分（通过总线广播，由 GameState 累加）
	EventBus.enemy_killed.emit(1, score_value)
	queue_free()

func _spawn_pickup() -> void:
	var scene := preload("res://scenes/pickups/pickup.tscn")
	var pk: Node2D = scene.instantiate()
	pk.global_position = global_position
	pk.kind = randi() % 3   # 0=回血 1=加速 2=加伤害
	get_parent().add_child(pk)
```

### 35.5.4 点积在游戏里的用途（第 25 章）

第 25 章讲过：`a.dot(b) > 0` 表示两向量夹角小于 90°（同向）。这在游戏里用途极广：

| 需求 | 写法 |
| --- | --- |
| 判断玩家是否在敌人"正面" | `facing.dot(to_player_normalized) > 0.0` |
| 判断是否"背后偷袭" | `facing.dot(to_player_normalized) < -0.5` |
| 计算视野锥（约 60° 内） | `facing.dot(to_player) > cos(deg_to_rad(30.0))` |
| 求两向量夹角（弧度） | `a.angle_to(b)` 或 `acos(a.normalized().dot(b.normalized()))` |

---

## 35.6 第 5 步：伤害与血量闭环

### 35.6.1 伤害计算器（T02）

把"基础伤害 → 加成 → 暴击 → 减免 → 保底"这套规则集中到一个静态类里，**任何攻击方都调它，改规则只改一处**。

```gdscript
# res://scripts/systems/damage_calculator.gd
extends RefCounted
class_name DamageCalculator
## 伤害计算器（T02）：纯函数，无状态，方便单元测试。

class Result:
	var final_amount: int
	var is_crit: bool

static func compute(base: int, attacker_bonus: float, crit_chance: float,
		crit_mult: float, target_defense: int) -> Result:
	var r := Result.new()
	var raw := float(base) * (1.0 + attacker_bonus)     # 攻击方加成
	r.is_crit = randf() < crit_chance
	if r.is_crit:
		raw *= crit_mult
	raw = raw * (100.0 / (100.0 + float(target_defense)))  # 减伤公式
	r.final_amount = maxi(int(round(raw)), 1)              # 至少造成 1 点
	return r
```

**为什么用"100/(100+防御)"而不是"直接减防御"？**

- 直接减法在防御高于攻击时会归零甚至为负，战斗直接失衡。
- 除法公式是**渐近函数**：防御越高效收益越低，永远不会减到 0，数值可控。这是业界最常见的减伤公式。

### 35.6.2 伤害飘字（T15）

```gdscript
# res://scripts/ui/damage_number.gd
extends Node2D
## 伤害飘字（T15）：在受击点弹出一个数字，向上飘并淡出。

@export var lifetime: float = 0.7
@export var rise_speed: float = 60.0

var _t: float = 0.0
@onready var label: Label = $Label

func setup(amount: int, is_crit: bool) -> void:
	label.text = str(amount)
	if is_crit:
		label.add_theme_color_override("font_color", Color.GOLD)
		label.add_theme_font_size_override("font_size", 28)
	else:
		label.add_theme_font_size_override("font_size", 18)

func _process(delta: float) -> void:
	_t += delta
	position.y -= rise_speed * delta
	modulate.a = 1.0 - (_t / lifetime)   # 线性淡出
	if _t >= lifetime:
		queue_free()
```

在 EventBus 里加一个转发（也可以让飘字生成器监听 `damage_dealt`）：

```gdscript
# res://scripts/systems/damage_number_spawner.gd
extends Node

func _ready() -> void:
	EventBus.damage_dealt.connect(_on_damage_dealt)

func _on_damage_dealt(target: Node, amount: int, is_crit: bool) -> void:
	if not (target is Node2D):
		return
	var scene := preload("res://scenes/ui/damage_number.tscn")
	var dn: Node2D = scene.instantiate()
	dn.global_position = (target as Node2D).global_position + Vector2(0, -20)
	dn.setup(amount, is_crit)
	get_tree().current_scene.add_child(dn)
```

### 35.6.3 受伤闪烁与屏幕震动（T14 / T19）

```gdscript
# res://scripts/components/hit_flash.gd
extends Node
## 受伤闪烁（T19）：被击中时短暂把角色染成白色。
## 用 ShaderMaterial 的 white_amount 参数实现，比改 modulate 更"亮"。

@onready var sprite: Sprite2D = get_parent().get_node("Sprite2D")
var _timer: float = 0.0

func flash(duration: float = 0.1) -> void:
	_timer = duration
	if sprite.material != null:
		sprite.material.set_shader_parameter("white_amount", 1.0)

func _process(delta: float) -> void:
	if _timer > 0.0:
		_timer -= delta
		if _timer <= 0.0 and sprite.material != null:
			sprite.material.set_shader_parameter("white_amount", 0.0)
```

屏幕震动直接用第 33 章 T14 的 `ScreenShake` 挂在主场景的 `Camera2D` 上，然后监听总线：

```gdscript
# 挂在相机上的 ScreenShake 脚本里加：
func _ready() -> void:
	EventBus.screen_shake_requested.connect(shake)
```

**为什么用 EventBus 转发震屏，而不是每个敌人自己找相机？**

- 敌人不知道相机在哪、叫什么，**零耦合**。
- 相机被销毁或替换，敌人代码不受影响。
- 这就是第 21 章"信号解耦"的直接应用。

---

## 35.7 第 6 步：波次生成

### 35.7.1 敌人管理器 / 波次生成器（T10）

```gdscript
# res://scripts/systems/wave_spawner.gd
extends Node2D
class_name WaveSpawner
## 波次生成器（T10）：按波次在屏幕外生成敌人，难度逐渐递增。

@export var base_enemy_scene: PackedScene
@export var base_count: int = 5          # 第 1 波的敌人数
@export var count_growth: float = 1.15   # 每波数量倍率
@export var hp_growth: float = 1.10      # 每波血量倍率
@export var spawn_radius: float = 420.0  # 生成半径（屏幕外）
@export var wave_interval: float = 1.2   # 波与波之间的间隔

var current_wave: int = 0
var _alive_enemies: int = 0
var _spawning := false

func _ready() -> void:
	EventBus.enemy_killed.connect(_on_enemy_killed)

func start() -> void:
	_spawning = true
	_next_wave()

func stop() -> void:
	_spawning = false   # 只是停止"下一波"的调度，已在场的敌人不受影响

func _next_wave() -> void:
	if not _spawning:
		return
	current_wave += 1
	# 第 36 章：pow 计算指数增长
	var count := int(round(base_count * pow(count_growth, current_wave - 1)))
	var hp_mult := pow(hp_growth, current_wave - 1)
	EventBus.wave_started.emit(current_wave, count)
	_alive_enemies = count
	for i in count:
		_spawn_one(hp_mult)
		await get_tree().create_timer(0.06).timeout   # 逐个生成，视觉上像"涌出来"
	await get_tree().create_timer(wave_interval).timeout
	if _alive_enemies <= 0:
		EventBus.wave_cleared.emit(current_wave)
	_next_wave()

func _spawn_one(hp_mult: float) -> void:
	if base_enemy_scene == null:
		return
	var e: Enemy = base_enemy_scene.instantiate()
	# 在玩家周围的圆周上随机取一点（屏幕外）
	var angle := randf() * TAU
	var pos := get_tree().get_first_node_in_group("player").global_position \
		+ Vector2(cos(angle), sin(angle)) * spawn_radius
	e.global_position = pos
	# 必须先 add_child，_ready() 才会执行，@onready 出来的 health 引用才非 null
	add_child(e)
	# 应用难度倍率：直接覆盖血量组件的值（当前值也要一起改，否则仍是旧上限）
	var scaled_hp := int(round(e.health.max_health * hp_mult))
	e.health.max_health = scaled_hp
	e.health.current_health = scaled_hp
	e.move_speed *= (1.0 + 0.03 * (current_wave - 1))   # 移速也小幅提升

func _on_enemy_killed(_count: int, _score: int) -> void:
	_alive_enemies -= 1
```

### 35.7.2 难度曲线设计

难度不能"线性堆怪"，否则第 20 波会变成幻灯片。经验做法是**缓慢的指数增长 + 数值封顶**：

| 参数 | 第 1 波 | 第 5 波 | 第 10 波 | 第 20 波 | 设计意图 |
| --- | --- | --- | --- | --- | --- |
| 数量（1.15^n） | 5 | 8 | 17 | 68 | 敌人越堆越多，形成"割草"爽感 |
| 血量倍率（1.10^n） | 1.0 | 1.46 | 2.36 | 6.12 | 慢慢变肉，逼玩家堆伤害 |
| 移速加成 | 1.00 | 1.12 | 1.27 | 1.57 | 走位空间逐渐收紧 |
| 生成间隔 | 1.2s | 1.2s | 1.2s | 1.2s | 保持不变，让节奏稳定 |

> **调平衡的黄金法则**：一次只改一个参数，改完立刻玩 3 波感受。**别一次改五个参数，否则你永远不知道是哪一个起了作用。**

---

## 35.8 第 7 步：掉落与拾取

### 35.8.1 拾取物节点

```text
Pickup (Area2D)              <- 挂 pickup.gd
├── Sprite2D
└── CollisionShape2D         <- 稍大的圆形，方便自动吸附
```

```gdscript
# res://scripts/pickups/pickup.gd
extends Area2D
class_name Pickup

enum Kind { HEAL, SPEED, DAMAGE }   # 第 27 章：枚举让代码可读

@export var kind: int = Kind.HEAL
@export var value: float = 20.0
@export var magnet_speed: float = 280.0   # 靠近时的吸附速度

var _target: Node2D = null
var _bob_time: float = 0.0

func _ready() -> void:
	body_entered.connect(_on_body_entered)
	# 根据类型换颜色（实际项目里换贴图）
	match kind:
		Kind.HEAL: $Sprite2D.modulate = Color.SPRING_GREEN
		Kind.SPEED: $Sprite2D.modulate = Color.SKY_BLUE
		Kind.DAMAGE: $Sprite2D.modulate = Color.ORANGE_RED

func _process(delta: float) -> void:
	_bob_time += delta
	$Sprite2D.position.y = sin(_bob_time * 4.0) * 3.0   # 上下浮动，吸引注意
	var p := get_tree().get_first_node_in_group("player")
	if p == null:
		return
	# 玩家在磁吸范围内则飞向玩家
	if global_position.distance_to(p.global_position) < 90.0:
		global_position = global_position.move_toward(p.global_position, magnet_speed * delta)

func _on_body_entered(body: Node2D) -> void:
	if body.is_in_group("player"):
		_collect(body)

func _collect(player: Node2D) -> void:
	match kind:
		Kind.HEAL:
			player.get_node("HealthComponent").heal(int(value))
		Kind.SPEED:
			player.move_speed += value          # 永久小加速
		Kind.DAMAGE:
			player.bullet_damage = player.bullet_damage + int(value)
	EventBus.pickup_collected.emit(kind, value)
	AudioManager.play_sfx("pickup")
	queue_free()
```

**为什么用 `body_entered` 而不是 `area_entered`？**

因为玩家是 `CharacterBody2D`（物理体，属于 `body`），而 `Area2D` 侦测其他 `Area2D` 才用 `area_entered`。**记住这个对应关系，少踩一半物理坑：**

| 侦测对象是什么 | 用哪个信号 |
| --- | --- |
| 另一个 `Area2D`（如子弹的受击区） | `area_entered` / `area_exited` |
| 一个物理体（`CharacterBody2D`/`RigidBody2D`/`StaticBody2D`） | `body_entered` / `body_exited` |

---

## 35.9 第 8 步：UI 与 HUD

### 35.9.1 HUD 节点结构

```text
HUD (CanvasLayer)                 <- 挂 hud.gd，CanvasLayer 保证 UI 不随相机移动
└── MarginContainer
    ├── VBoxContainer（左上）
    │   ├── HealthBar (ProgressBar)
    │   ├── ScoreLabel (Label)
    │   └── WaveLabel (Label)
    └── PauseMenu (Control)       <- 默认隐藏
        ├── ResumeButton
        └── QuitButton
```

**为什么 HUD 要放在 `CanvasLayer` 下？** 因为游戏世界有相机跟随、缩放、震动，如果 HUD 是普通节点，它会跟着抖、跟着缩。`CanvasLayer` 让 UI 保持屏幕坐标系，不受相机影响。

### 35.9.2 HUD 脚本（信号解耦）

```gdscript
# res://scripts/ui/hud.gd
extends CanvasLayer

@onready var health_bar: ProgressBar = $MarginContainer/VBoxContainer/HealthBar
@onready var score_label: Label = $MarginContainer/VBoxContainer/ScoreLabel
@onready var wave_label: Label = $MarginContainer/VBoxContainer/WaveLabel
@onready var pause_menu: Control = $MarginContainer/VBoxContainer/PauseMenu

var _score: int = 0

func _ready() -> void:
	# 全部通过事件总线监听，HUD 不认识任何游戏对象
	EventBus.player_health_changed.connect(_on_health_changed)
	EventBus.enemy_killed.connect(_on_enemy_killed)
	EventBus.wave_started.connect(_on_wave_started)
	EventBus.player_died.connect(_on_player_died)
	pause_menu.visible = false

func _unhandled_input(event: InputEvent) -> void:
	if event.is_action_pressed("pause"):
		_toggle_pause()
		get_viewport().set_input_as_handled()   # 消费掉事件，防止穿透

func _toggle_pause() -> void:
	var paused := not get_tree().paused
	get_tree().paused = paused
	pause_menu.visible = paused
	EventBus.game_paused.emit(paused)

func _on_health_changed(cur: int, max_hp: int) -> void:
	health_bar.max_value = max_hp
	health_bar.value = cur

func _on_enemy_killed(_count: int, score: int) -> void:
	_score += score
	score_label.text = "分数：%d" % _score

func _on_wave_started(wave_index: int, enemy_count: int) -> void:
	wave_label.text = "第 %d 波（%d 只）" % [wave_index, enemy_count]

func _on_player_died() -> void:
	pause_menu.visible = false
```

> **暂停的正确做法**：设置 `get_tree().paused = true` 后，只有 `process_mode` 为 `PROCESS_MODE_WHEN_PAUSED` 或 `PROCESS_MODE_ALWAYS` 的节点还会运行。**UI 要能响应暂停菜单按钮，必须把自己（或其父节点）的 `process_mode` 设为 `ALWAYS`**，否则暂停后连菜单按钮都点不动。这是第 13 章讲过的坑。

---

## 35.10 第 9 步：游戏流程

### 35.10.1 状态机

```gdscript
# res://autoload/game_state.gd（也可做成普通 Autoload）
extends Node
## 全局游戏状态机：管理"当前处于哪个阶段"，并串联流程。

enum State { MENU, PLAYING, PAUSED, GAME_OVER }

var state: State = State.MENU
var score: int = 0
var current_wave: int = 0

func _ready() -> void:
	EventBus.enemy_killed.connect(func(_c, s): score += s)
	EventBus.wave_started.connect(func(w, _n): current_wave = w)
	EventBus.player_died.connect(_on_player_died)

func start_game() -> void:
	score = 0
	current_wave = 0
	state = State.PLAYING
	SceneRouter.goto("res://scenes/main.tscn")   # 走 T26 带淡入淡出

func _on_player_died() -> void:
	state = State.GAME_OVER
	var best: int = SettingsManager.get_best_score()
	var is_record := score > best
	if is_record:
		SettingsManager.set_best_score(score)    # 写入存档
	EventBus.game_over.emit(score, is_record)
	# 稍等 1.2 秒让死亡反馈播完，再切结算界面
	await get_tree().create_timer(1.2).timeout
	SceneRouter.goto("res://scenes/ui/game_over.tscn")
```

### 35.10.2 用 SceneRouter 串联（T26）

```gdscript
# res://autoload/scene_router.gd（T26 的简化版）
extends CanvasLayer

const FADE_TIME := 0.35
var _fade: ColorRect
var _busy := false

func _ready() -> void:
	layer = 100                        # 盖在所有 UI 之上
	_fade = ColorRect.new()
	_fade.color = Color(0, 0, 0, 0)
	_fade.set_anchors_preset(Control.PRESET_FULL_RECT)
	_fade.mouse_filter = Control.MOUSE_FILTER_IGNORE
	add_child(_fade)

func goto(path: String) -> void:
	if _busy:
		return                          # 加锁：防止连点导致半切换
	_busy = true
	_fade.mouse_filter = Control.MOUSE_FILTER_STOP
	var tween := create_tween()
	tween.tween_property(_fade, "color:a", 1.0, FADE_TIME)
	await tween.finished
	# 第 34 章：用 packed 版本，可提前异步加载资源
	get_tree().change_scene_to_file(path)
	await get_tree().process_frame
	var tween2 := create_tween()
	tween2.tween_property(_fade, "color:a", 0.0, FADE_TIME)
	await tween2.finished
	_fade.mouse_filter = Control.MOUSE_FILTER_IGNORE
	_busy = false
```

### 35.10.3 开始界面

```gdscript
# res://scripts/ui/main_menu.gd
extends Control

@onready var best_label: Label = $VBoxContainer/BestLabel

func _ready() -> void:
	best_label.text = "最高分：%d" % SettingsManager.get_best_score()
	$VBoxContainer/StartButton.pressed.connect(_on_start_pressed)
	$VBoxContainer/QuitButton.pressed.connect(func(): get_tree().quit())

func _on_start_pressed() -> void:
	# 这里调用全局状态机的开始逻辑
	var gs := get_node("/root/GameState")
	gs.start_game()
```

**完整流程串起来：**

```text
main_menu.tscn
   │ 点"开始"
   ▼
GameState.start_game() → SceneRouter.goto(main.tscn)
   │
   ▼
main.tscn  _ready() → 启动 WaveSpawner
   │  玩家存活 → 循环：移动/射击/杀敌/拾取/波次
   ▼
玩家血量归零 → EventBus.player_died
   │
   ▼
GameState._on_player_died() → 写最高分 → 等 1.2s → goto(game_over.tscn)
   │
   ▼
game_over.tscn 显示分数与"再来一局"
   │ 点"再来一局"
   └──────────────► 回到 GameState.start_game()
```

---

## 35.11 第 10 步：存档与设置接上

### 35.11.1 SettingsManager（T20 + 第 28 章文件读写）

```gdscript
# res://autoload/settings_manager.gd
extends Node

const SAVE_PATH := "user://settings.cfg"

var master_volume: float = 1.0
var best_score: int = 0

func _ready() -> void:
	load_settings()

func load_settings() -> void:
	# 第 28 章：ConfigFile 比手写 JSON 更适合存"键值型设置"
	var cfg := ConfigFile.new()
	var err := cfg.load(SAVE_PATH)
	if err != OK:
		return   # 首次运行没有存档，用默认值即可
	master_volume = cfg.get_value("audio", "master", 1.0)
	best_score = cfg.get_value("game", "best_score", 0)
	_apply()

func save_settings() -> void:
	var cfg := ConfigFile.new()
	cfg.set_value("audio", "master", master_volume)
	cfg.set_value("game", "best_score", best_score)
	cfg.save(SAVE_PATH)   # user:// 是各平台可写目录，永远不要写 res://

func set_master_volume(v: float) -> void:
	master_volume = clampf(v, 0.0, 1.0)
	_apply()
	save_settings()       # 立即持久化，防止崩溃丢失

func get_best_score() -> int:
	return best_score

func set_best_score(v: int) -> void:
	best_score = v
	save_settings()

func _apply() -> void:
	# 把音量值推给音频总线（Godot 4 用 AudioServer）
	var bus := AudioServer.get_bus_index("Master")
	AudioServer.set_bus_volume_db(bus, linear_to_db(master_volume))
```

**关键点：为什么用 `user://` 而不是 `res://`？**

| 路径 | 能否写 | 说明 |
| --- | --- | --- |
| `res://` | ❌ 只读（导出版） | 是游戏资源目录，打包后不可写 |
| `user://` | ✅ 可写 | 各平台用户数据目录，存档就该放这 |

用 `res://` 存档，在编辑器里能跑，**一导出就崩**——这是新手最经典的翻车点之一。

### 35.11.2 AudioManager 读设置

```gdscript
# res://autoload/audio_manager.gd
extends Node

var _sfx_players: Array[AudioStreamPlayer] = []

func _ready() -> void:
	for i in 8:               # 预建 8 个播放器，交替使用以支持音效重叠
		var p := AudioStreamPlayer.new()
		add_child(p)
		_sfx_players.append(p)
	EventBus.game_paused.connect(func(p): 
		for pl in _sfx_players: pl.stream_paused = p)

func play_sfx(name: String) -> void:
	var path := "res://assets/audio/%s.wav" % name
	if not ResourceLoader.exists(path):
		return                 # 没这个音效就静默跳过，不报错
	var stream: AudioStream = load(path)
	for p in _sfx_players:
		if not p.playing:
			p.stream = stream
			p.play()
			return
	# 全部占用时，抢占第一个（新的优先）
	_sfx_players[0].stream = stream
	_sfx_players[0].play()
```

---

## 35.12 完整代码清单

### 35.12.1 脚本文件总表

| 文件路径 | 职责 | 关键依赖 | 关联章节 |
| --- | --- | --- | --- |
| `autoload/event_bus.gd` | 全局信号定义与中转 | 无 | 第 21 章、T05 |
| `autoload/settings_manager.gd` | 设置与最高分持久化 | ConfigFile | 第 28 章、T20 |
| `autoload/audio_manager.gd` | BGM/音效播放、音量 | SettingsManager | 第 33 章、T16 |
| `autoload/scene_router.gd` | 带淡入淡出切换场景 | Tween | 第 34 章、T26 |
| `autoload/game_state.gd` | 全局状态机与计分 | EventBus、SceneRouter | 第 34 章 |
| `scripts/actors/player.gd` | 玩家移动/瞄准/开火 | Input、EventBus | 第 12/19/24/25 章 |
| `scripts/actors/enemy.gd` | 敌人追击/攻击/死亡 | HealthComponent、Hurtbox | 第 25/31 章 |
| `scripts/actors/bullet.gd` | 子弹飞行与命中 | Hurtbox 类型判断 | 第 16/30 章 |
| `scripts/components/health_component.gd` | 通用血量 | 无 | 第 31 章、T01 |
| `scripts/components/hit_flash.gd` | 受伤闪烁 | ShaderMaterial | 第 33 章、T19 |
| `scripts/components/hurtbox.gd` | 受击判定区 | HealthComponent | 第 16 章 |
| `scripts/systems/damage_calculator.gd` | 伤害公式（静态） | 无 | 第 31 章、T02 |
| `scripts/systems/wave_spawner.gd` | 波次生成与难度 | Enemy 场景 | 第 31 章、T10 |
| `scripts/systems/bullet_pool.gd` | 子弹对象池 | Bullet 场景 | 第 30/34 章、T21 |
| `scripts/systems/damage_number_spawner.gd` | 监听伤害生成飘字 | EventBus | 第 33 章、T15 |
| `scripts/pickups/pickup.gd` | 掉落物与自动拾取 | Area2D | 第 16 章 |
| `scripts/ui/hud.gd` | 血条/分数/波次/暂停 | EventBus | 第 21/13 章 |
| `scripts/ui/main_menu.gd` | 开始界面 | GameState | 第 34 章 |
| `scripts/ui/game_over.gd` | 结算界面 | SettingsManager | 第 28/34 章 |

### 35.12.2 主场景装配脚本

```gdscript
# res://scripts/main.gd —— 挂在 main.tscn 根节点
extends Node2D

@onready var wave_spawner: WaveSpawner = $WaveSpawner
@onready var bullet_pool: Node = $BulletPool

func _ready() -> void:
	# 让玩家出生后再启动波次，避免敌人追着"空气"跑
	EventBus.player_spawned.connect(_on_player_spawned)

func _on_player_spawned(_player: Node2D) -> void:
	await get_tree().create_timer(1.0).timeout   # 给玩家 1 秒喘息
	wave_spawner.start()
```

### 35.12.3 核心脚本一：玩家（完整）

```gdscript
# res://scripts/actors/player.gd
extends CharacterBody2D
class_name Player

signal bullet_damage_changed(value: int)

@export var move_speed: float = 220.0
@export var acceleration: float = 2000.0
@export var friction: float = 1800.0
@export var fire_rate: float = 0.15      # 每 0.15 秒一发
@export var bullet_damage: int = 10:
	set(v):
		bullet_damage = v
		bullet_damage_changed.emit(v)

@onready var sprite: Sprite2D = $Sprite2D
@onready var muzzle: Marker2D = $Muzzle
@onready var health: HealthComponent = $HealthComponent

var _aim_direction: Vector2 = Vector2.RIGHT
var _shoot_cooldown: float = 0.0
var _hurt_invincible: float = 0.0        # 受伤后的短暂无敌

func _ready() -> void:
	add_to_group("player")
	health.health_changed.connect(_on_health_changed)
	health.died.connect(_on_died)
	EventBus.player_spawned.emit(self)
	EventBus.player_health_changed.emit(health.current_health, health.max_health)

func _physics_process(delta: float) -> void:
	_hurt_invincible = maxf(_hurt_invincible - delta, 0.0)
	_handle_movement(delta)
	_handle_aiming()
	_handle_shooting(delta)

func _handle_movement(delta: float) -> void:
	var input_dir := Input.get_vector("move_left", "move_right", "move_up", "move_down")
	if input_dir != Vector2.ZERO:
		velocity = velocity.move_toward(input_dir * move_speed, acceleration * delta)
	else:
		velocity = velocity.move_toward(Vector2.ZERO, friction * delta)
	move_and_slide()

func _handle_aiming() -> void:
	var mouse_pos := get_global_mouse_position()
	_aim_direction = (mouse_pos - global_position).normalized()
	sprite.global_rotation = _aim_direction.angle()

func _handle_shooting(delta: float) -> void:
	_shoot_cooldown -= delta
	if _shoot_cooldown > 0.0 or not Input.is_action_pressed("shoot"):
		return
	_shoot_cooldown = fire_rate
	var pool := get_tree().get_first_node_in_group("bullet_pool")
	if pool != null:
		pool.fire(muzzle.global_position, _aim_direction, bullet_damage)

func take_damage(amount: int, _source: Node = null) -> void:
	if _hurt_invincible > 0.0:
		return
	_hurt_invincible = 0.3               # 0.3 秒无敌，防止被围死
	health.take_damage(amount)
	EventBus.screen_shake_requested.emit(6.0, 0.2)
	var hf := get_node_or_null("HitFlash")
	if hf != null:
		hf.flash()

func _on_health_changed(cur: int, max_hp: int) -> void:
	EventBus.player_health_changed.emit(cur, max_hp)

func _on_died() -> void:
	EventBus.player_died.emit()
	set_physics_process(false)
	set_process(false)
	# 死亡特效：缩小并淡出
	var tw := create_tween()
	tw.set_parallel(true)
	tw.tween_property(sprite, "scale", Vector2.ZERO, 0.4)
	tw.tween_property(sprite, "modulate:a", 0.0, 0.4)
	tw.chain().tween_callback(queue_free)
```

### 35.12.4 核心脚本二：主循环（main.gd 汇总版）

```gdscript
# res://scripts/main.gd
extends Node2D
## 主场景总控：负责在玩家出生后启动波次，并在玩家死亡时停掉一切。

@onready var wave_spawner: WaveSpawner = $WaveSpawner

func _ready() -> void:
	EventBus.player_spawned.connect(_on_player_spawned)
	EventBus.player_died.connect(_on_player_died)

func _on_player_spawned(_player: Node2D) -> void:
	# 用 await 等待 1 秒（第 17 章：协程）
	await get_tree().create_timer(1.0).timeout
	wave_spawner.start()

func _on_player_died() -> void:
	wave_spawner.stop()
	# 清场：把残留敌人和子弹清掉，避免结算时还在动
	for e in get_tree().get_nodes_in_group("enemy"):
		e.queue_free()
```

### 35.12.5 核心脚本三：结算界面

```gdscript
# res://scripts/ui/game_over.gd
extends Control

@onready var score_label: Label = $VBoxContainer/ScoreLabel
@onready var record_label: Label = $VBoxContainer/RecordLabel

func _ready() -> void:
	# 直接读取全局状态（也可通过 SceneRouter 传参，见 T26）
	var gs := get_node("/root/GameState")
	score_label.text = "本局分数：%d" % gs.score
	var best: int = SettingsManager.get_best_score()
	record_label.text = "最高分：%d" % best
	record_label.visible = gs.score >= best and gs.score > 0
	$VBoxContainer/RetryButton.pressed.connect(_on_retry)
	$VBoxContainer/MenuButton.pressed.connect(_on_menu)

func _on_retry() -> void:
	get_node("/root/GameState").start_game()

func _on_menu() -> void:
	SceneRouter.goto("res://scenes/ui/main_menu.tscn")
```

---

## 35.13 本章小结

### 35.13.1 技能清单（对照第 1-34 章逐卷打勾）

| 卷 | 章节范围 | 本项目用到的关键点 | 是否掌握 |
| --- | --- | --- | --- |
| 第一卷 基础语法 | 第 1-6 章 | `var/const`、类型、运算符、`is/as`、`match` | ☐ |
| 第二卷 流程与结构 | 第 7-11 章 | `if/for/while`、函数、参数默认值 | ☐ |
| 第三卷 引擎交互 | 第 12-20 章 | 生命周期、`_physics_process`、输入、Area2D、Timer | ☐ |
| 第四卷 进阶语法 | 第 21-27 章 | 信号、`await`、静态类、`@export`、枚举、向量归一化 | ☐ |
| 第五卷 工程化 | 第 28-30 章 | 文件读写、对象池、数据驱动 | ☐ |
| 第六卷 模板库 | 第 31-34 章 | T01/T02/T05/T10/T14/T15/T19/T20/T21/T26 | ☐ |

### 35.13.2 一句话总结每一步的价值

| 步骤 | 一句话价值 |
| --- | --- |
| 项目与 Autoload | 先定"谁是全局、谁是局部"，后面才不乱 |
| 玩家移动 | `get_vector` + `move_toward` = 跟手且不加速的八向移动 |
| 瞄准与射击 | 鼠标位置转方向向量，冷却控制射速，对象池控制性能 |
| 敌人 | 方向归一化追击，组件化血量，死亡掉落计分 |
| 伤害闭环 | 一处公式、一处动画、一处反馈，规则和表现分离 |
| 波次 | 指数递增 + 封顶，让难度"慢慢变难而不失控" |
| 掉落拾取 | `body_entered` 侦测物理体，磁吸提升手感 |
| HUD | 全部走事件总线，UI 不认识任何游戏对象 |
| 流程 | 状态机 + SceneRouter = 可重入、可扩展的关卡流 |
| 存档设置 | `user://` + ConfigFile，关掉游戏设置还在 |

### 35.13.3 最后的话

你已经做出了一个**结构清晰、可扩展、带完整反馈**的小游戏。它不华丽，但它是一具"能跑起来的骨架"——你可以往里面塞任何你想要的肉：

- 想加武器？照着 `bullet.gd` 加一个新的子弹场景，玩家身上放一个"武器数组"。
- 想加 Boss？给 Enemy 加一个 `is_boss` 标记，波次到第 10 波时生成。
- 想加技能树？把第 32 章数据驱动的那一套搬进来。

**记住：一个能跑的最小版本，永远比一个想得很美的设计文档更有价值。** 先去把游戏跑起来，再去优化它。

---

# 第 36 章：完整语法速查表

> 前 35 章教你怎么"理解和写"，这一章只做一件事：**让你在需要的时候，用最快的速度查到"正确写法"**。
>
> 这一章不需要从头读，它是工具书。你写代码卡壳时翻它、不确定某个方法名时翻它、从 Godot 3 迁移时翻它。**把这一章当成你的"快捷键"**。

## 36.1 使用说明

**这张表怎么用？**

| 场景 | 去哪一节 |
| --- | --- |
| 忘了某个词能不能当变量名 | 36.2 关键字与保留字 |
| 不确定某类型有哪些方法、默认值是多少 | 36.3 数据类型 |
| 分不清 `==` 和 `is`、`and` 和 `&&` | 36.4 运算符 |
| 想找某个字符串处理方法 | 36.5 字符串方法 |
| 数组/字典方法记不全 | 36.6 Array 与 Dictionary |
| 数学函数（`lerp`/`clamp`/`snapped`…） | 36.7 数学函数 |
| 节点生命周期/树操作方法 | 36.8 节点方法 |
| `@export` 的各种变体怎么写 | 36.9 注解全表 |
| 从 Godot 3 代码迁移到 4 | 36.10 迁移对照 |
| 想要"单行能用"的常见配方 | 36.11 常用配方 |

**查表三原则：**
1. **先看签名再看示例**：签名告诉你"参数几个、返回什么"，示例告诉你"怎么用"。
2. **方法名区分原版与副本**：带 `_` 前缀或返回新值的要分清（如 `sort()` 原地 vs `sorted()` 返回新数组）。
3. **Godot 3/4 差异重点看 36.10**：网上大量老教程是 Godot 3 语法，直接抄会报错。

---

## 36.2 关键字与保留字全表

GDScript 的关键字**不能用作变量名、函数名、类名**。下面的表按类别整理，并标注"能否当变量名"。

### 36.2.1 声明类关键字

| 关键字 | 作用 | 一行示例 | 能当变量名？ |
| --- | --- | --- | --- |
| `var` | 声明变量 | `var hp := 100` | 否 |
| `const` | 声明常量（编译期） | `const SPEED := 200.0` | 否 |
| `static` | 静态变量/函数 | `static var counter := 0` | 否 |
| `func` | 声明函数 | `func jump() -> void:` | 否 |
| `class` | 内部类 | `class Inner: pass` | 否 |
| `class_name` | 注册全局类名 | `class_name Player` | 否 |
| `extends` | 继承 | `extends CharacterBody2D` | 否 |
| `signal` | 声明信号 | `signal died` | 否 |
| `enum` | 枚举 | `enum State { IDLE, RUN }` | 否 |
| `breakpoint` | 调试断点 | `breakpoint` | 否 |
| `await` | 协程等待 | `await timer.timeout` | 否 |
| `pass` | 空语句占位 | `func _ready() -> void: pass` | 否 |

### 36.2.2 控制流关键字

| 关键字 | 作用 | 示例 | 能当变量名？ |
| --- | --- | --- | --- |
| `if` | 条件 | `if hp > 0:` | 否 |
| `elif` | 否则如果 | `elif hp == 0:` | 否 |
| `else` | 否则 | `else:` | 否 |
| `for` | 遍历 | `for i in 10:` | 否 |
| `while` | 循环 | `while alive:` | 否 |
| `match` | 模式匹配 | `match state:` | 否 |
| `when` | match 守卫条件 | `1 when hp > 0:` | 否 |
| `break` | 跳出循环 | `break` | 否 |
| `continue` | 跳过本轮 | `continue` | 否 |
| `return` | 返回 | `return value` | 否 |
| `yield` | （Godot 3 遗留）**已废弃** | 用 `await` 替代 | 否 |

### 36.2.3 值/标识关键字

| 关键字 | 作用 | 示例 | 能当变量名？ |
| --- | --- | --- | --- |
| `true` | 布尔真 | `var ok := true` | 否 |
| `false` | 布尔假 | `var done := false` | 否 |
| `null` | 空值 | `var node = null` | 否 |
| `self` | 当前对象 | `return self` | 否 |
| `super` | 父类 | `super._ready()` | 否 |
| `void` | 无返回类型 | `func f() -> void:` | 否 |
| `is` | 类型判断 | `if n is Node2D:` | 否 |
| `as` | 类型转换 | `var n := x as Node2D` | 否 |
| `in` | 包含/遍历 | `if 3 in arr:` | 否 |
| `and` | 逻辑与 | `if a and b:` | 否 |
| `or` | 逻辑或 | `if a or b:` | 否 |
| `not` | 逻辑非 | `if not done:` | 否 |
| `PI` | 圆周率常量 | `rotation = PI` | 否 |
| `TAU` | 2π 常量 | `rotation = TAU` | 否 |
| `INF` | 无穷 | `var x := INF` | 否 |
| `NAN` | 非数字 | `var x := NAN` | 否 |

### 36.2.4 保留但通常可当变量名的"上下文关键字"

以下词**在特定上下文才有特殊含义**，一般可用作变量名，但**强烈不建议**，容易混淆：

| 词 | 特殊含义 | 建议 |
| --- | --- | --- |
| `name` | 节点属性 `name` | 可用但易混淆 |
| `position`、`rotation`、`scale` | Node2D 属性 | 建议加前缀如 `player_pos` |
| `owner` | 节点属性 | 避免 |
| `get`、`set` | 属性的 getter/setter 语法 | 避免 |
| `信号名 on_xxx` | 无保留，但 `on` 不是关键字 | `on_ready` 可当变量名 |
| `preload`、`load` | 内置函数（非关键字） | 可被覆盖，极不建议 |
| `range` | 内置函数 | 可被覆盖，极不建议 |

### 36.2.5 命名规范速记

| 类别 | 规范 | 示例 |
| --- | --- | --- |
| 变量/函数 | 蛇形 `snake_case` | `move_speed`、`take_damage` |
| 常量 | 全大写 `SCREAMING_SNAKE` | `MAX_HEALTH`、`SAVE_PATH` |
| 类名 | 大驼峰 `PascalCase` | `WaveSpawner`、`Player` |
| 信号 | 过去式/事件式 | `died`、`health_changed` |
| 私有成员 | 前缀下划线 | `_aim_direction` |
| 枚举值 | 全大写 | `enum State { IDLE, RUN }` |
| 节点名 | 大驼峰 | `HealthComponent` |

---

## 36.3 数据类型速查表

### 36.3.1 基础类型

| 类型 | 默认值 | 字面量写法 | 常用方法 |
| --- | --- | --- | --- |
| `bool` | `false` | `true` / `false` | `if x:` 直接判断 |
| `int` | `0` | `42`、`0xFF`、`0b1010`、`1_000` | `abs()`、`clampi()`、`signi()` |
| `float` | `0.0` | `3.14`、`1e5`、`0.5` | `roundf()`、`lerpf()`、`snappedf()` |
| `String` | `""` | `"你好"` | `format()`、`split()`、`to_upper()` |
| `StringName` | `&""` | `&"idle"` | `to_string()`、`is_empty()` |
| `NodePath` | `^""` | `^"../Player"` | `get_name()`、`is_empty()` |

### 36.3.2 数学/几何类型

| 类型 | 默认值 | 字面量 | 常用方法 |
| --- | --- | --- | --- |
| `Vector2` | `(0, 0)` | `Vector2(1, 2)`、`Vector2.ONE` | `normalized()`、`dot()`、`lerp()`、`angle()` |
| `Vector2i` | `(0, 0)` | `Vector2i(1, 2)` | `length()`、`clampi()`、`distance_to()` |
| `Vector3` | `(0, 0, 0)` | `Vector3(1, 0, 0)` | `cross()`、`slide()`、`normalized()` |
| `Vector4` | `(0,0,0,0)` | `Vector4(1,0,0,0)` | `dot()`、`normalized()` |
| `Rect2` | `(0,0,0,0)` | `Rect2(0, 0, 32, 32)` | `has_point()`、`intersects()`、`grow()` |
| `Rect2i` | `(0,0,0,0)` | `Rect2i(0, 0, 32, 32)` | `has_point()`、`intersection()` |
| `Transform2D` | 单位阵 | `Transform2D(0, Vector2(1,1))` | `translated()`、`scaled()`、`xform()` |
| `Transform3D` | 单位阵 | — | `basis`、`origin`、`looking_at()` |
| `Basis` | 单位阵 | — | `rotated()`、`slerp()` |
| `Quaternion` | 单位 | `Quaternion(0,0,0,1)` | `slerp()`、`normalized()` |
| `Color` | `(0,0,0,1)` | `Color(1, 0, 0)`、`Color.RED`、`"#ff0000"` | `lerp()`、`darkened()`、`from_hsv()` |
| `Plane` | — | — | `distance_to()`、`project()` |

### 36.3.3 容器类型

| 类型 | 默认值 | 字面量 | 常用方法 |
| --- | --- | --- | --- |
| `Array` | `[]` | `[1, 2, 3]` | `append()`、`map()`、`filter()` |
| `Array[T]` | `[]` | `var a: Array[int] = []` | 类型化数组，会做类型检查 |
| `Dictionary` | `{}` | `{"k": 1}` | `get()`、`keys()`、`has()` |
| `PackedByteArray` | `[]` | `PackedByteArray([1, 2])` | `decode_*()`、`to_int*()` |
| `PackedInt32Array` | `[]` | `PackedInt32Array([1, 2])` | `append()`、`slice()` |
| `PackedFloat32Array` | `[]` | `PackedFloat32Array([1.0])` | `append()`、`sort()` |
| `PackedStringArray` | `[]` | `PackedStringArray(["a"])` | `append()`、`join()` |
| `PackedVector2Array` | `[]` | — | `append()`、`to_byte_array()` |

### 36.3.4 对象/回调类型

| 类型 | 默认值 | 写法 | 说明 |
| --- | --- | --- | --- |
| `Object` | `null` | — | 所有对象的基类 |
| `Node` | `null` | `$Player` | 场景树节点基类 |
| `Node2D` | `null` | — | 2D 变换节点 |
| `Control` | `null` | — | UI 基类 |
| `Resource` | `null` | `preload("...")` | 数据资源基类 |
| `RefCounted` | 自动释放 | — | 引用计数对象（非节点） |
| `Callable` | 空 | `func(): pass`、`obj.method` | 可调用对象，替代 Godot 3 的字符串回调 |
| `Signal` | 空 | `obj.signal_name` | 信号对象，用于 `connect()` |
| `Variant` | `null` | 任意类型 | 动态类型，任何值都能装 |

### 36.3.5 类型转换要点

```gdscript
# 显式转换 vs 隐式转换
var i: int = 3
var f: float = i          # 隐式：int -> float 允许
# var j: int = 3.7        # 会警告/截断，建议显式

var x := float(3)         # 构造函数式转换
var s := str(42)          # 数字转字符串："42"
var n := int("42")        # 字符串转整数：42
var d := float("3.14")    # 字符串转浮点：3.14
var b := bool(1)          # 非零为 true

# as 是"安全向下转换"，失败返回 null
var body := get_node_or_null("X") as CharacterBody2D
if body != null:
    body.move_and_slide()
```

**易错点：`int(3.9)` 得到 `3`（截断，不是四舍五入）！** 要四舍五入用 `roundi(3.9)`。

---

## 36.4 运算符全表

### 36.4.1 算术运算符

| 运算符 | 含义 | 示例 | 结果 |
| --- | --- | --- | --- |
| `+` | 加 / 字符串拼接 / 数组合并 | `[1] + [2]` | `[1, 2]` |
| `-` | 减 | `5 - 2` | `3` |
| `*` | 乘 / 字符串重复 | `"ab" * 3` | `"ababab"` |
| `/` | 除 | `7 / 2` | `3`（整数除） |
| `%` | 取余 | `7 % 2` | `1` |
| `**` | 幂 | `2 ** 3` | `8` |
| `-x` | 取负 | `-3` | `-3` |

> **整数除法陷阱**：`7 / 2` 在 GDScript 里是 `3`，不是 `3.5`。要小数结果必须至少一个操作数是浮点：`7.0 / 2` 得 `3.5`。

### 36.4.2 比较运算符

| 运算符 | 含义 | 示例 | 说明 |
| --- | --- | --- | --- |
| `==` | 相等 | `a == b` | 值比较 |
| `!=` | 不等 | `a != b` | — |
| `<` `>` | 小于/大于 | `a < b` | — |
| `<=` `>=` | 小于等于/大于等于 | `a <= b` | — |
| `is` | 是否属于类型 | `n is Node2D` | 会包含子类 |
| `is not` | 不属于类型 | `n is not Node2D` | — |
| `in` | 是否包含 | `3 in [1,2,3]` | 数组/字典/字符串 |
| `not in` | 不包含 | `4 not in arr` | — |

### 36.4.3 逻辑运算符

| 运算符 | 别名 | 示例 | 注意 |
| --- | --- | --- | --- |
| `and` | `&&`（不推荐） | `a and b` | 短路求值 |
| `or` | `\|\|`（不推荐） | `a or b` | 短路求值 |
| `not` | `!`（不推荐） | `not a` | — |

> GDScript **推荐用英文单词** `and/or/not`，`&&/||/!` 虽能编译但不符合官方风格。

### 36.4.4 位运算符

| 运算符 | 含义 | 示例 | 结果（二进制） |
| --- | --- | --- | --- |
| `&` | 按位与 | `6 & 3` | `2`（110 & 011 = 010） |
| `\|` | 按位或 | `6 \| 3` | `7`（110 \| 011 = 111） |
| `^` | 按位异或 | `6 ^ 3` | `5`（110 ^ 011 = 101） |
| `~` | 按位取反 | `~6` | `-7` |
| `<<` | 左移 | `1 << 3` | `8` |
| `>>` | 右移 | `16 >> 2` | `4` |

### 36.4.5 赋值运算符

| 运算符 | 等价于 | 示例 |
| --- | --- | --- |
| `=` | — | `x = 5` |
| `+=` | `x = x + n` | `x += 1` |
| `-=` | `x = x - n` | `x -= 1` |
| `*=` | `x = x * n` | `x *= 2` |
| `/=` | `x = x / n` | `x /= 2` |
| `%=` | `x = x % n` | `x %= 3` |
| `**=` | `x = x ** n` | `x **= 2` |
| `&=` `\|=` `^=` `<<=` `>>=` | 位运算赋值 | `flags \|= 1` |

### 36.4.6 特殊运算符

| 运算符 | 含义 | 示例 |
| --- | --- | --- |
| `?:` | 三元（行内 if） | `var s = "生" if hp > 0 else "死"` |
| `as` | 类型转换 | `var n = x as Node2D` |
| `is` | 类型检查 | `if x is Node:` |
| `in` | 包含检查 | `if key in dict:` |
| `..` | 范围（仅用于 match 模式） | `match x: 1..5: print("小")` |
| `->` | 返回类型标注 | `func f() -> int:` |
| `:=` | 类型推断赋值 | `var v := Vector2.ZERO` |
| `:` | 类型标注 | `var v: Vector2` |

> **注意**：GDScript 的 `..` **只能用于 `match` 的取值范围模式**，不能像 Python 那样写 `for i in 0..10`。要遍历范围请用 `range()`。

### 36.4.7 运算符优先级（从高到低）

| 优先级 | 运算符 | 结合性 |
| --- | --- | --- |
| 1 | `()` 括号、`[]` 索引、`.` 成员访问 | 左 |
| 2 | `-x` `~` `not` `!`（一元） | 右 |
| 3 | `**` | 右 |
| 4 | `*` `/` `%` | 左 |
| 5 | `+` `-` | 左 |
| 6 | `<<` `>>` | 左 |
| 7 | `&` | 左 |
| 8 | `^` | 左 |
| 9 | `\|` | 左 |
| 10 | `<` `>` `<=` `>=` `is` `in` | 左 |
| 11 | `==` `!=` | 左 |
| 12 | `and` `&&` | 左 |
| 13 | `or` `\|\|` | 左 |
| 14 | `?:` 三元 | 右 |
| 15 | `=` `+=` 等赋值 | 右 |

**易错点**：`a and b or c` 会先算 `a and b` 再 `or c`。**逻辑复杂时务必加括号**，可读性比省字符重要。

---

## 36.5 字符串方法速查

GDScript 的字符串是**不可变**的：下面所有方法若"返回新值"，原字符串都不会被改动。

| 方法 | 用途 | 示例 | 返回 |
| --- | --- | --- | --- |
| `length()` | 字符数 | `"你好".length()` → `2` | int |
| `is_empty()` | 是否空串 | `"".is_empty()` → `true` | bool |
| `contains(s)` | 是否包含子串 | `"abc".contains("b")` → `true` | bool |
| `begins_with(s)` | 是否以开头 | `"file.png".begins_with("file")` | bool |
| `ends_with(s)` | 是否以结尾 | `"a.png".ends_with(".png")` | bool |
| `find(s, from)` | 首次出现位置 | `"abcabc".find("b")` → `1` | int（无则 -1） |
| `rfind(s, from)` | 末次出现位置 | `"abcabc".rfind("b")` → `4` | int |
| `count(s)` | 子串出现次数 | `"aaa".count("a")` → `3` | int |
| `replace(a, b)` | 替换全部 | `"a-b".replace("-", "+")` → `"a+b"` | String |
| `replace_char(a, b)` | 替换字符 | `"a-b".replace_char("-", "+")` | String |
| `substr(from, len)` | 取子串 | `"hello".substr(1, 3)` → `"ell"` | String |
| `left(n)` | 左起 n 个字符 | `"hello".left(2)` → `"he"` | String |
| `right(n)` | 右起 n 个字符 | `"hello".right(2)` → `"lo"` | String |
| `insert(pos, s)` | 指定位置插入 | `"ac".insert(1, "b")` → `"abc"` | String |
| `strip_edges(l, r)` | 去两端空白 | `" x ".strip_edges()` → `"x"` | String |
| `strip_escapes()` | 去转义符 | 处理控制字符 | String |
| `split(delim, allow_empty)` | 分割为数组 | `"a,b".split(",")` → `["a","b"]` | PackedStringArray |
| `join(parts)` | 拼接数组 | `",".join(["a","b"])` → `"a,b"` | String |
| `to_upper()` | 转大写 | `"ab".to_upper()` → `"AB"` | String |
| `to_lower()` | 转小写 | `"AB".to_lower()` → `"ab"` | String |
| `capitalize()` | 首字母大写 | `"hello".capitalize()` → `"Hello"` | String |
| `to_camel_case()` | 转驼峰 | `"hello_world".to_camel_case()` | String |
| `to_pascal_case()` | 转大驼峰 | `"hello_world".to_pascal_case()` | String |
| `to_snake_case()` | 转蛇形 | `"HelloWorld".to_snake_case()` | String |
| `lpad(min, char)` | 左侧补齐 | `"7".lpad(3, "0")` → `"007"` | String |
| `rpad(min, char)` | 右侧补齐 | `"7".rpad(3, ".")` → `"7.."` | String |
| `repeat(n)` | 重复 n 次 | `"ab".repeat(3)` → `"ababab"` | String |
| `reverse()` | 反转 | `"abc".reverse()` → `"cba"` | String |
| `unicode_at(i)` | 第 i 位字符码 | `"A".unicode_at(0)` → `65` | int |
| `chr(code)` | 码转字符（静态） | `String.chr(65)` → `"A"` | String |
| `hash()` | 哈希值 | `"abc".hash()` | int |
| `sha256_text()` | SHA256 摘要 | 用于校验 | String |
| `md5_text()` | MD5 摘要 | 用于校验 | String |
| `to_int()` | 转整数 | `"42".to_int()` → `42` | int |
| `to_float()` | 转浮点 | `"3.14".to_float()` → `3.14` | float |
| `is_valid_int()` | 是否合法整数 | `"42".is_valid_int()` → `true` | bool |
| `is_valid_float()` | 是否合法浮点 | `"3.14".is_valid_float()` → `true` | bool |
| `is_valid_hex_number()` | 是否十六进制 | `"ff".is_valid_hex_number()` | bool |
| `is_absolute_path()` | 是否绝对路径 | `"/root".is_absolute_path()` | bool |
| `format(values)` | 格式化替换 | `"HP:%d".format([5])` → `"HP:5"` | String |
| `%` 运算符 | 格式化（推荐） | `"HP:%d" % 5` → `"HP:5"` | String |

**格式化占位符速查：**

| 占位符 | 含义 | 示例 |
| --- | --- | --- |
| `%s` | 字符串 | `"%s" % 42` → `"42"` |
| `%d` | 整数 | `"%d" % 3.9` → `"3"` |
| `%f` | 浮点 | `"%f" % 1.5` → `"1.500000"` |
| `%.2f` | 保留 2 位 | `"%.2f" % 1.567` → `"1.57"` |
| `%x` | 十六进制 | `"%x" % 255` → `"ff"` |
| `%c` | 字符 | `"%c" % 65` → `"A"` |
| `%%` | 百分号本身 | `"100%%"` → `"100%"` |
| `%05d` | 补零 | `"%05d" % 42` → `"00042"` |
| `%v` | 任意值 | `"%v" % [1,2]` → `"[1, 2]"` |

```gdscript
# 多参数格式化：用数组包裹
print("坐标：(%d, %d)" % [pos.x, pos.y])
```

---

## 36.6 Array 与 Dictionary 方法速查

### 36.6.1 Array 常用方法（30+）

> 标注说明：**原地** = 修改数组自身；**新值** = 返回新数组，原数组不变。

| 方法 | 用途 | 示例 | 原地/新值 |
| --- | --- | --- | --- |
| `append(x)` | 尾部追加 | `a.append(1)` | 原地 |
| `push_back(x)` | 同 append | `a.push_back(2)` | 原地 |
| `push_front(x)` | 头部插入 | `a.push_front(0)` | 原地 |
| `insert(i, x)` | 指定位置插入 | `a.insert(1, 9)` | 原地 |
| `pop_back()` | 弹出尾部 | `var v = a.pop_back()` | 原地 |
| `pop_front()` | 弹出头部 | `var v = a.pop_front()` | 原地 |
| `remove_at(i)` | 删除索引 i | `a.remove_at(0)` | 原地 |
| `erase(x)` | 删除等于 x 的首个元素 | `a.erase(5)` | 原地 |
| `clear()` | 清空 | `a.clear()` | 原地 |
| `size()` | 元素个数 | `a.size()` | 只读 |
| `is_empty()` | 是否为空 | `a.is_empty()` | 只读 |
| `has(x)` | 是否包含 | `a.has(3)` | 只读 |
| `find(x, from)` | 首个索引 | `a.find(3)` | 只读（无则 -1） |
| `rfind(x, from)` | 末个索引 | `a.rfind(3)` | 只读 |
| `count(x)` | 出现次数 | `a.count(3)` | 只读 |
| `front()` | 首元素 | `a.front()` | 只读 |
| `back()` | 末元素 | `a.back()` | 只读 |
| `slice(begin, end, step)` | 切片 | `a.slice(1, 3)` | 新值 |
| `duplicate(deep)` | 复制 | `a.duplicate(true)` | 新值 |
| `sort()` | 升序排序 | `a.sort()` | 原地 |
| `sort_custom(callable)` | 自定义排序 | `a.sort_custom(func(x,y): return x>y)` | 原地 |
| `reverse()` | 反转 | `a.reverse()` | 原地 |
| `shuffle()` | 随机打乱 | `a.shuffle()` | 原地 |
| `pick_random()` | 随机取一个 | `var v = a.pick_random()` | 只读 |
| `bsearch(x, before)` | 二分查找（需已排序） | `a.bsearch(3)` | 只读 |
| `max()` | 最大值 | `a.max()` | 只读 |
| `min()` | 最小值 | `a.min()` | 只读 |
| `sum()` | 求和 | `a.sum()` | 只读 |
| `map(callable)` | 映射 | `a.map(func(x): return x*2)` | 新值 |
| `filter(callable)` | 过滤 | `a.filter(func(x): return x>0)` | 新值 |
| `reduce(callable, init)` | 归约 | `a.reduce(func(acc,x): return acc+x, 0)` | 返回累计值 |
| `any(callable)` | 是否存在满足 | `a.any(func(x): return x>5)` | 只读 |
| `all(callable)` | 是否全部满足 | `a.all(func(x): return x>0)` | 只读 |
| `merge(arr, overwrite)` | 合并 | `a.merge(b, true)` | 原地 |
| `fill(x)` | 全部填充 | `a.fill(0)` | 原地 |
| `resize(n)` | 改变长度 | `a.resize(5)` | 原地 |
| `append_array(arr)` | 批量追加 | `a.append_array(b)` | 原地 |
| `flatten()` | 展平（递归） | `[[1],[2]].flatten()` | 新值 |
| `to_byte_array()` | 转字节数组 | `a.to_byte_array()` | 新值 |

```gdscript
# 函数式三连：map / filter / reduce
var nums := [1, 2, 3, 4, 5]
var doubled := nums.map(func(n): return n * 2)          # [2,4,6,8,10]
var evens := nums.filter(func(n): return n % 2 == 0)    # [2,4]
var total := nums.reduce(func(acc, n): return acc + n, 0)  # 15
```

### 36.6.2 Dictionary 常用方法（30+）

| 方法 | 用途 | 示例 | 说明 |
| --- | --- | --- | --- |
| `dict[key]` | 取值（键不存在报错） | `d["hp"]` | 无则报错 |
| `get(key, default)` | 安全取值 | `d.get("hp", 0)` | 无则返回默认 |
| `set(key, value)` | 设值 | `d.set("hp", 100)` | 原地 |
| `has(key)` | 是否含键 | `d.has("hp")` | 只读 |
| `has_all(keys)` | 是否含全部键 | `d.has_all(["a","b"])` | 只读 |
| `erase(key)` | 删除键 | `d.erase("hp")` | 原地（返回 bool） |
| `clear()` | 清空 | `d.clear()` | 原地 |
| `size()` | 键值对数量 | `d.size()` | 只读 |
| `is_empty()` | 是否为空 | `d.is_empty()` | 只读 |
| `keys()` | 所有键 | `d.keys()` | 新值数组 |
| `values()` | 所有值 | `d.values()` | 新值数组 |
| `duplicate(deep)` | 复制 | `d.duplicate(true)` | 新值 |
| `merge(other, overwrite)` | 合并 | `d.merge(d2, true)` | 原地 |
| `get_or_add(key, default)` | 取或添加 | `d.get_or_add("hp", 0)` | 原地 |
| `hash()` | 哈希 | `d.hash()` | 只读 |
| `is_same_typed(other)` | 类型比较 | — | 只读 |
| `assign(other)` | 整体赋值 | `d.assign(d2)` | 原地（4.x 新） |

```gdscript
# 字典遍历的两种方式
var stats := {"hp": 100, "mp": 50}
for key in stats:
	print(key, " = ", stats[key])       # hp = 100 / mp = 50
for key in stats.keys():
	print(key, stats[key])
for kv in stats:
	print(kv, "=", stats[kv])           # kv 是 key

# 合并 + 默认值模式（配置表常用）
func get_config(user_cfg: Dictionary) -> Dictionary:
	var base := {"volume": 1.0, "fullscreen": false, "lang": "zh"}
	base.merge(user_cfg, true)          # 用户配置覆盖默认值
	return base
```

> **深拷贝提醒**：`duplicate()` 默认是**浅拷贝**。如果数组/字典里还嵌套着数组或字典，必须用 `duplicate(true)` 才是深拷贝，否则改内层会同时影响原对象。这是非常隐蔽的 bug 来源。

### 36.6.3 高频"陷阱"对比

| 易混对 | 区别 |
| --- | --- |
| `sort()` vs `sorted()` | `sort()` 原地修改；`sorted()` 返回新数组（4.x 中 Array 有 `sorted()`） |
| `duplicate()` vs `duplicate(true)` | 浅拷贝 vs 深拷贝 |
| `erase()` vs `remove_at()` | 按值删 vs 按索引删 |
| `d["k"]` vs `d.get("k")` | 键不存在时前者报错、后者返回默认值 |
| `has()` vs `in` | `d.has("k")` 与 `"k" in d` 等价 |

---

## 36.7 常用数学函数表

GDScript 的数学函数是**全局函数**（不是某个类的静态方法），可以分为泛型版（`abs`）、浮点版（`absf`）、整数版（`absi`）。

### 36.7.1 取整与符号

| 函数 | 用途 | 示例 | 结果 |
| --- | --- | --- | --- |
| `abs(x)` / `absf` / `absi` | 绝对值 | `abs(-3)` | `3` |
| `sign(x)` / `signf` / `signi` | 符号 | `sign(-5)` | `-1` |
| `floor(x)` / `floorf` / `floori` | 向下取整 | `floor(1.9)` | `1.0` |
| `ceil(x)` / `ceilf` / `ceili` | 向上取整 | `ceil(1.1)` | `2.0` |
| `round(x)` / `roundf` / `roundi` | 四舍五入 | `round(1.5)` | `2.0` |
| `trunc(x)` / `truncf` / `trunci` | 截断 | `trunc(1.9)` | `1.0` |
| `int(x)` | 转整数（截断） | `int(3.9)` | `3` |

> **`f` 后缀返回 float，`i` 后缀返回 int。** 写代码时明确用哪个，能避免大量隐式转换警告。

### 36.7.2 比较与夹紧

| 函数 | 用途 | 示例 | 结果 |
| --- | --- | --- | --- |
| `min(a, b)` | 最小值 | `min(3, 5)` | `3` |
| `max(a, b)` | 最大值 | `max(3, 5)` | `5` |
| `mini` / `maxi` / `minf` / `maxf` | 类型明确版 | `maxi(3, 5)` | `5` |
| `clamp(x, lo, hi)` | 夹在区间内 | `clamp(12, 0, 10)` | `10` |
| `clampi` / `clampf` | 类型明确版 | `clampi(-1, 0, 10)` | `0` |
| `is_equal_approx(a, b)` | 浮点近似相等 | `is_equal_approx(0.1+0.2, 0.3)` | `true` |
| `is_zero_approx(x)` | 是否近似 0 | `is_zero_approx(1e-8)` | `true` |

> **浮点数千万不要用 `==` 比较**！`0.1 + 0.2 == 0.3` 是 `false`。要用 `is_equal_approx()`。这是所有语言的通病。

### 36.7.3 插值与逼近

| 函数 | 用途 | 示例 | 说明 |
| --- | --- | --- | --- |
| `lerp(a, b, t)` | 线性插值 | `lerp(0, 100, 0.5)` → `50` | t 可为任意值 |
| `lerpf` | 浮点版线性插值 | `lerpf(0.0, 10.0, 0.3)` → `3.0` | — |
| `lerp_angle(a, b, t)` | 角度插值（走最短弧） | `lerp_angle(0, PI, 0.5)` | 避免"绕远路" |
| `inverse_lerp(a, b, v)` | 反插值 | `inverse_lerp(0, 100, 50)` → `0.5` | lerp 的逆运算 |
| `remap(v, a, b, c, d)` | 区间映射 | `remap(5, 0, 10, 0, 100)` → `50` | — |
| `smoothstep(a, b, x)` | 平滑阶跃 | 常用于淡入淡出 | 有缓动 |
| `move_toward(a, b, d)` | 向 b 移动 d | `move_toward(0, 10, 3)` → `3` | 有上限的逼近 |
| `move_toward`（向量版） | 向量逼近 | `v.move_toward(target, step)` | — |
| `snapped(x, step)` | 吸附到步长 | `snapped(7, 4)` → `8` | — |
| `snappedf` / `snappedi` | 浮点/整数版 | `snappedf(2.7, 1.0)` → `3.0` | — |
| `wrap(v, lo, hi)` | 循环环绕 | `wrap(370, 0, 360)` → `10` | 角度常用 |
| `wrapf` / `wrapi` | 类型明确版 | `wrapi(370, 0, 360)` | — |
| `fmod(a, b)` | 浮点取余 | `fmod(-1.5, 1.0)` → `-0.5` | — |
| `fposmod(a, b)` | 结果恒非负的取余 | `fposmod(-1, 3)` → `2` | 循环索引常用 |
| `posmod(a, b)` | 整数版 | `posmod(-1, 3)` | — |
| `step_decimals(x)` | 小数位数 | — | — |

### 36.7.4 幂与对数

| 函数 | 用途 | 示例 | 结果 |
| --- | --- | --- | --- |
| `pow(x, y)` | 幂 | `pow(2, 3)` | `8.0` |
| `sqrt(x)` | 平方根 | `sqrt(16)` | `4.0` |
| `exp(x)` | e 的 x 次幂 | `exp(1)` | `2.718…` |
| `log(x)` | 自然对数 | `log(2.718)` | `≈1.0` |
| `log(x)` 相关 | — | — | — |

### 36.7.5 三角函数与角度

| 函数 | 用途 | 示例 |
| --- | --- | --- |
| `sin(x)` / `cos(x)` / `tan(x)` | 三角（弧度） | `sin(PI/2)` → `1.0` |
| `asin(x)` / `acos(x)` / `atan(x)` | 反三角 | `asin(1.0)` → `PI/2` |
| `atan2(y, x)` | 由坐标求角 | `atan2(1, 1)` → `PI/4` |
| `deg_to_rad(d)` | 角度转弧度 | `deg_to_rad(180)` → `PI` |
| `rad_to_deg(r)` | 弧度转角度 | `rad_to_deg(PI)` → `180` |
| `sinh/cosh/tanh` | 双曲函数 | 少数特效场景用 |

### 36.7.6 随机数

| 函数 | 用途 | 示例 | 结果范围 |
| --- | --- | --- | --- |
| `randi()` | 随机整数 | `randi()` | `0 ~ 2^32-1` |
| `randi_range(a, b)` | 范围内随机整数 | `randi_range(1, 6)` | `1~6`（含端点） |
| `randf()` | 随机浮点 | `randf()` | `0.0 ~ 1.0` |
| `randf_range(a, b)` | 范围内随机浮点 | `randf_range(-1, 1)` | `-1.0 ~ 1.0` |
| `randomize()` | 用系统时间初始化种子 | `randomize()` | 在 `_ready` 里调一次 |
| `rand_from_seed(seed)` | 由种子生成序列 | 用于可复现的随机关卡 | 返回数组 |

```gdscript
# 随机数三件套
func _ready() -> void:
	randomize()                              # 必须！否则每次运行序列相同
	var dice := randi_range(1, 6)            # 骰子
	var angle := randf_range(0.0, TAU)       # 随机角度
	var lucky := randf() < 0.25              # 25% 概率
```

> **`randomize()` 只调一次**：通常放在最顶层的 Autoload 或主场景 `_ready()`。每帧调用不会更"随机"，反而浪费。

---

## 36.8 节点常用方法表

### 36.8.1 生命周期回调

| 回调 | 何时调用 | 典型用途 |
| --- | --- | --- |
| `_init()` | 对象构造（C++ 层） | 初始化纯数据，慎用 `get_node` |
| `_enter_tree()` | 进入场景树 | 注册到组、连接全局信号 |
| `_ready()` | 子节点全部就绪后 | 主要初始化（最常用） |
| `_process(delta)` | 每帧 | 视觉更新、计时 |
| `_physics_process(delta)` | 固定频率（默认 60Hz） | 移动、碰撞 |
| `_input(event)` | 有输入事件时 | 全局输入 |
| `_unhandled_input(event)` | 未被 UI 消费的输入 | 游戏内输入（推荐） |
| `_unhandled_key_input(event)` | 只处理键盘 | — |
| `_notification(what)` | 引擎通知 | 高级用法（如 `NOTIFICATION_WM_CLOSE_REQUEST`） |
| `_exit_tree()` | 离开场景树 | 断开连接、保存状态 |

### 36.8.2 树操作

| 方法 | 用途 | 示例 |
| --- | --- | --- |
| `get_node(path)` | 按路径取节点 | `get_node("Player/Body")` |
| `$path` | `get_node` 语法糖 | `$Player/Body` |
| `get_node_or_null(path)` | 安全取节点 | `get_node_or_null("X")` |
| `find_child(pattern, recursive, owned)` | 按名找子节点 | `find_child("Enemy*")` |
| `get_parent()` | 父节点 | `get_parent().add_child(n)` |
| `get_children()` | 所有直接子节点 | `for c in get_children():` |
| `add_child(node, force_readable)` | 添加子节点 | `add_child(bullet)` |
| `remove_child(node)` | 移除子节点 | `remove_child(n)` |
| `queue_free()` | 延迟安全删除 | `queue_free()` |
| `free()` | 立即删除（危险） | 慎用 |
| `is_inside_tree()` | 是否在树中 | `if is_inside_tree():` |
| `get_tree()` | 场景树 | `get_tree().paused = true` |
| `move_child(node, index)` | 调整顺序 | `move_child(n, 0)` |
| `reparent(new_parent)` | 换父节点（4.x 新） | `reparent(new_parent)` |
| `duplicate(flags)` | 复制节点 | `var c = duplicate()` |
| `owner` | 场景的拥有者 | 保存打包场景时用 |

### 36.8.3 分组（Groups）

| 方法 | 用途 | 示例 |
| --- | --- | --- |
| `add_to_group(name)` | 加入组 | `add_to_group("enemy")` |
| `remove_from_group(name)` | 离开组 | `remove_from_group("enemy")` |
| `is_in_group(name)` | 是否在组 | `if body.is_in_group("player"):` |
| `get_tree().get_nodes_in_group(n)` | 取组内所有节点 | `get_nodes_in_group("enemy")` |
| `get_tree().call_group(g, m, ...)` | 调用组内所有节点方法 | `call_group("enemy", "freeze")` |
| `get_tree().get_first_node_in_group(g)` | 取组内第一个 | `get_first_node_in_group("player")` |
| `get_tree().get_node_count_in_group(g)` | 组内节点数 | — |

### 36.8.4 信号（Signals）

| 方法 | 用途 | 示例 |
| --- | --- | --- |
| `connect(signal, callable)` | 连接信号 | `btn.pressed.connect(_on_press)` |
| `disconnect(signal, callable)` | 断开 | `btn.pressed.disconnect(_on_press)` |
| `is_connected(signal, callable)` | 是否已连 | `if sig.is_connected(cb):` |
| `emit(signal, ...)` | 发出信号（4.x） | `died.emit()` |
| `signal.emit(...)` | 信号对象直接发 | `health_changed.emit(cur, max)` |
| `Callable.bind(...)` | 绑定参数 | `t.timeout.connect(func(): f(1))` |
| `Callable.unbind(n)` | 解绑前缀参数 | — |
| `CONNECT_ONE_SHOT` | 只触发一次 | `connect(cb, CONNECT_ONE_SHOT)` |
| `CONNECT_DEFERRED` | 延迟到帧末 | 避免在物理回调用 |
| `call_deferred(method, ...)` | 延迟调用 | `call_deferred("f")` |
| `has_method(name)` | 是否有方法 | `if n.has_method("take_damage"):` |
| `callv(method, args)` | 用数组传参调用 | `callv("f", [1, 2])` |

### 36.8.5 属性与元数据

| 方法 | 用途 | 示例 |
| --- | --- | --- |
| `set(name, value)` | 按名设属性 | `set("visible", false)` |
| `get(name)` | 按名取属性 | `get("visible")` |
| `set_deferred(name, value)` | 延迟设属性 | `set_deferred("monitoring", false)` |
| `get_property_list()` | 属性列表 | 编辑器/序列化用 |
| `set_meta(name, value)` | 设元数据 | `set_meta("id", 3)` |
| `get_meta(name, default)` | 取元数据 | `get_meta("id", -1)` |
| `has_meta(name)` | 是否有元数据 | — |
| `remove_meta(name)` | 删元数据 | — |
| `get_class()` | 类名 | `get_class()` |

### 36.8.6 节点/处理开关

| 属性/方法 | 用途 | 示例 |
| --- | --- | --- |
| `process_mode` | 处理模式 | `PROCESS_MODE_ALWAYS` 等 |
| `set_process(bool)` | 开关 `_process` | `set_process(false)` |
| `set_physics_process(bool)` | 开关 `_physics_process` | `set_physics_process(false)` |
| `set_process_input(bool)` | 开关 `_input` | — |
| `visible` | 是否可见（CanvasItem） | `visible = false` |
| `modulate` | 颜色调制 | `modulate.a = 0.5` |
| `z_index` | 层级 | `z_index = 10` |
| `paused`（SceneTree） | 全局暂停 | `get_tree().paused = true` |
| `get_tree().quit()` | 退出游戏 | `get_tree().quit()` |
| `get_tree().reload_current_scene()` | 重载当前场景 | 重开一局 |

### 36.8.7 定时与协程

| 方法 | 用途 | 示例 |
| --- | --- | --- |
| `create_timer(t).timeout` | 一次性延时 | `await get_tree().create_timer(1.0).timeout` |
| `Timer` 节点 | 可复用定时器 | `$Timer.start(2.0)` |
| `await` | 等待信号/协程 | `await tween.finished` |
| `await get_tree().process_frame` | 等一帧 | `await get_tree().process_frame` |
| `await get_tree().physics_frame` | 等一个物理帧 | — |

---

## 36.9 注解全表

注解（Annotation）以 `@` 开头，写在声明前一行。Godot 4 大量使用注解替代 Godot 3 的关键字。

### 36.9.1 @export 家族

| 注解 | 作用 | 示例 |
| --- | --- | --- |
| `@export` | 暴露给检查器 | `@export var speed: float = 100.0` |
| `@export_range` | 带范围滑块 | `@export_range(0, 100, 1, "suffix:%") var pct := 50` |
| `@export_enum` | 下拉枚举 | `@export_enum("易", "中", "难") var diff := 1` |
| `@export_enum`（用枚举） | 关联真实 enum | `@export var k: Kind`（有 `enum Kind` 即可） |
| `@export_flags` | 位标志勾选 | `@export_flags("火", "水", "木") var elem := 0` |
| `@export_flags_2d_physics` | 物理层勾选 | `@export_flags_2d_physics var layer := 1` |
| `@export_flags_2d_render` | 渲染层勾选 | — |
| `@export_file("*.png")` | 文件路径选择 | `@export_file("*.png") var tex_path: String` |
| `@export_dir` | 目录选择 | `@export_dir var folder: String` |
| `@export_global_file` | 全局文件 | `@export_global_file var f: String` |
| `@export_multiline` | 多行文本 | `@export_multiline var desc: String` |
| `@export_color_no_alpha` | 颜色（无透明） | `@export_color_no_alpha var c: Color` |
| `@export_node_path("Node2D")` | 节点路径（带类型） | `@export_node_path("Node2D") var target: NodePath` |
| `@export_storage` | 存储但不显示 | 用于内部状态 |
| `@export_custom(hint, hint_string)` | 自定义提示 | 高级用法 |
| `@export_group("名字")` | 分组起 | `@export_group("移动")` |
| `@export_subgroup("子组")` | 子分组 | — |
| `@export_category("类别")` | 大类 | — |
| `@export_placeholder("提示")` | 输入框占位符 | — |

```gdscript
# 综合示例：一个可配置的敌人
class_name EnemyConfig
extends Resource

enum Difficulty { EASY, NORMAL, HARD }

@export_group("基础")
@export var display_name: String = "史莱姆"
@export_range(1, 1000, 1) var max_health: int = 30
@export_range(0.0, 2.0, 0.05) var speed_mult: float = 1.0

@export_group("选项")
@export var difficulty: Difficulty = Difficulty.NORMAL
@export_flags("火", "水", "木") var elements: int = 0
@export_color_no_alpha var tint: Color = Color.WHITE
@export_file("*.png") var icon_path: String = ""
```

### 36.9.2 其他常用注解

| 注解 | 作用 | 示例 |
| --- | --- | --- |
| `@onready` | 延迟到 `_ready` 前初始化 | `@onready var s := $Sprite2D` |
| `@tool` | 编辑器中也运行脚本 | 插件/自定义控件 |
| `@static_unload` | 类不再被引用时卸载静态变量 | 减少内存 |
| `@icon("路径")` | 设置脚本图标 | `@icon("res://icon.svg")` |
| `@warning_ignore("名字")` | 忽略特定警告 | `@warning_ignore("unused_parameter")` |
| `@warning_ignore_start` / `_restore` | 区间忽略警告 | 批量忽略 |
| `@rpc` | 标注远程调用方法 | `@rpc("any_peer") func sync():` |
| `@abstract` | 抽象类（4.5+） | 需确认版本支持 |

```gdscript
# @onready 的时机：等价于 _ready 开头，但更简洁
@onready var label: Label = $UI/Label
# 等价写法：
# var label: Label
# func _ready():
#     label = $UI/Label

# @tool：让脚本在编辑器里也执行（做插件/预览必用）
@tool
extends Node2D
@export var radius: float = 50.0:
	set(v):
		radius = v
		queue_redraw()   # 编辑器里立刻更新
```

### 36.9.3 @rpc 参数速查（多人游戏）

| 参数 | 含义 |
| --- | --- |
| `"any_peer"` | 任何端都能调用 |
| `"authority"` | 只有权威端能调用 |
| `"call_local"` | 本地也执行 |
| `"call_remote"` | 只在远端执行 |
| `"reliable"` | 可靠传输 |
| `"unreliable"` | 不可靠（快） |
| `"unreliable_ordered"` | 不可靠但有顺序 |

```gdscript
@rpc("any_peer", "call_local", "reliable")
func request_shoot(dir: Vector2) -> void:
    # 只有服务器通过时才真正生成子弹
    if not multiplayer.is_server():
        return
    spawn_bullet.rpc(dir)
```

---

## 36.10 Godot 3 → 4 语法迁移对照表

这是全书**最实用的一张表**。网上 90% 的教程、视频、问答仍是 Godot 3 语法，直接抄会大量报错。迁移时对照此表逐行改。

| # | Godot 3 写法 | Godot 4 写法 | 说明 |
| --- | --- | --- | --- |
| 1 | `yield(obj, "signal")` | `await obj.signal` | 协程全面改为 await |
| 2 | `yield()` | `await get_tree().process_frame` | 等一帧 |
| 3 | `onready var x = $N` | `@onready var x = $N` | 关键字变注解 |
| 4 | `export(int) var x` | `@export var x: int` | export 变注解 + 类型标注 |
| 5 | `export(float, 0, 1) var x` | `@export_range(0, 1) var x: float` | 范围变 range 注解 |
| 6 | `export(String, "a", "b") var x` | `@export_enum("a", "b") var x: String` | 枚举下拉 |
| 7 | `export(Texture) var t` | `@export var t: Texture2D` | 类型直接标注 |
| 8 | `export(NodePath) var n` | `@export_node_path var n` 或 `@export var n: Node2D` | 节点引用 |
| 9 | `instance()` | `instantiate()` | PackedScene 实例化 |
| 10 | `connect("x", self, "f")` | `x.connect(f)` 或 `self.x.connect(f)` | 字符串改成 Callable |
| 11 | `disconnect("x", self, "f")` | `x.disconnect(f)` | 同上 |
| 12 | `emit_signal("x", a)` | `x.emit(a)` | 信号发出 |
| 13 | `is_connected("x", self, "f")` | `x.is_connected(f)` | 判断连接 |
| 14 | `PoolStringArray` | `PackedStringArray` | 池类型改名 |
| 15 | `PoolIntArray` | `PackedInt32Array` | 同理 |
| 16 | `PoolRealArray` | `PackedFloat32Array` | 同理 |
| 17 | `PoolColorArray` | `PackedColorArray` | 同理 |
| 18 | `PoolVector2Array` | `PackedVector2Array` | 同理 |
| 19 | `OS.get_ticks_msec()` | `Time.get_ticks_msec()` | 时间统一到 Time 单例 |
| 20 | `OS.get_unix_time()` | `Time.get_unix_time_from_system()` | 系统时间 |
| 21 | `OS.get_datetime()` | `Time.get_datetime_dict_from_system()` | 日期时间 |
| 22 | `KinematicBody2D` | `CharacterBody2D` | 更名 |
| 23 | `KinematicBody` | `CharacterBody3D` | 更名 |
| 24 | `move_and_slide(vel, up)` | `velocity = vel; move_and_slide()` | velocity 变属性，不再传参 |
| 25 | `move_and_slide()` 返回速度 | 无返回值（读 `velocity`） | 返回值语义变化 |
| 26 | `is_on_floor()` | `is_on_floor()`（保留） | 无变化 |
| 27 | `Tween` 节点 | `create_tween()` 返回 Tween | Tween 不再手动加节点 |
| 28 | `$Tween.interpolate_property(...)` | `var t = create_tween(); t.tween_property(...)` | API 改为链式 |
| 29 | `$Tween.start()` | 自动开始（或 `t.play()`） | 无需手动 start |
| 30 | `File` 类 | `FileAccess` 类 | 更名 |
| 31 | `Directory` 类 | `DirAccess` 类 | 更名 |
| 32 | `File.new().open(...)` | `FileAccess.open(path, mode)` | 静态工厂 |
| 33 | `file.close()` | `file.close()` 或自动（配合 `use`） | 保持 |
| 34 | `rand_range(a, b)` | `randf_range(a, b)` | 显式浮点 |
| 35 | `randf()` / `randi()` | 保留 | 无变化 |
| 36 | `deg2rad(d)` | `deg_to_rad(d)` | 改名 |
| 37 | `rad2deg(r)` | `rad_to_deg(r)` | 改名 |
| 38 | `linear2db(x)` | `linear_to_db(x)` | 改名 |
| 39 | `db2linear(x)` | `db_to_linear(x)` | 改名 |
| 40 | `clamp(x, lo, hi)` | `clampf/clampi(clamp)` | 泛型化 |
| 41 | `lerp(a, b, t)` | `lerpf(a, b, t)` | 泛型化 |
| 42 | `Range`/`Rect` 属性 | `Rect2`/`Rect2i` | 统一 |
| 43 | `Vector2(i, j)` 用 int | 显式 `Vector2i` | 类型分离 |
| 44 | `Node.get_node("X")` | 保留 | — |
| 45 | `yield(get_tree().create_timer(1), "timeout")` | `await get_tree().create_timer(1).timeout` | 定时协程 |
| 46 | `State` 枚举不可用 `@export` | 可直接导出 `enum` | 枚举导出增强 |
| 47 | `set_deferred("monitoring", false)` | 保留 | — |
| 48 | `AnimationPlayer.play("x")` | 保留 | — |
| 49 | `get_tree().change_scene("res://x.tscn")` | `change_scene_to_file("res://x.tscn")` | 明确资源 vs 文件 |
| 50 | `preload("x").instance()` | `preload("x").instantiate()` | 见 #9 |
| 51 | `ProjectSettings.get("x")` | 保留 | — |
| 52 | `Input.is_action_just_pressed` | 保留 | — |
| 53 | `AudioServer.set_bus_volume_db` | 保留 | — |
| 54 | `OS.window_size` | `DisplayServer.window_get_size()` | 窗口 API 移到 DisplayServer |
| 55 | `OS.set_window_title()` | `DisplayServer.window_set_title()` | 同上 |
| 56 | `OS.window_fullscreen` | `DisplayServer.window_set_mode()` | 全屏模式枚举 |
| 57 | `VisualServer` 类 | `RenderingServer` 类 | 更名 |
| 58 | `Physics2DServer` | `PhysicsServer2D` | 更名 |
| 59 | `Object.connect` 的 flags 字符串 | `CONNECT_*` 常量 | 枚举化 |
| 60 | `ColorN("red")` | `Color.RED` 或 `Color("red")` | 常量访问 |
| 61 | `str2var()` / `var2str()` | `str_to_var()` / `var_to_str()` | 改名 |
| 62 | `GDScript.new()` 动态 | `GDScript.new()` 保留但更少用 | — |

### 36.10.1 迁移时的三个高频"连锁改动"

**改动一：connect 全家族**

```gdscript
# Godot 3
health.connect("died", self, "_on_died")
# Godot 4（两种等价写法）
health.died.connect(_on_died)
health.connect("died", _on_died)
```

**改动二：移动代码**

```gdscript
# Godot 3
func _physics_process(delta):
	velocity = move_and_slide(velocity, Vector2.UP)
# Godot 4
func _physics_process(delta: float) -> void:
	move_and_slide()   # velocity 是内置属性，直接赋值即可
```

**改动三：export + onready**

```gdscript
# Godot 3
export var speed = 100.0
onready var sprite = $Sprite
# Godot 4
@export var speed: float = 100.0
@onready var sprite: Sprite2D = $Sprite
```

> **迁移建议**：不要"一次性全改"。做法是**先让脚本能加载（编辑器不报语法错），再逐个修运行时报错**。GDScript 的静态检查会很清楚地告诉你哪一行用了旧 API。

---

## 36.11 常用"配方"速查

以下 20 条，都是"几行就能解决"的常见需求，可直接抄用。

**配方 1：动态生成节点并加入场景**

```gdscript
var node := Sprite2D.new()
node.texture = preload("res://icon.svg")
add_child(node)
```

**配方 2：从打包场景实例化**

```gdscript
const ENEMY := preload("res://enemy.tscn")
var e := ENEMY.instantiate()
e.global_position = spawn_pos
get_tree().current_scene.add_child(e)
```

**配方 3：延时执行一段代码**

```gdscript
await get_tree().create_timer(2.0).timeout
print("2 秒后执行")
```

**配方 4：查找节点（安全版）**

```gdscript
var node := get_node_or_null("Player/Body")
if node != null:
	node.visible = false
```

**配方 5：按组查找**

```gdscript
var player := get_tree().get_first_node_in_group("player")
var enemies := get_tree().get_nodes_in_group("enemy")
```

**配方 6：随机取范围值**

```gdscript
randomize()
var dmg := randi_range(5, 15)
var chance := randf_range(0.0, 1.0)
var pick := ["a", "b", "c"].pick_random()
```

**配方 7：范围判定（点是否在圈内）**

```gdscript
if global_position.distance_to(target_pos) < 100.0:
	print("在范围内")
```

**配方 8：格式化字符串（多种写法）**

```gdscript
var hp := 75
print("HP: %d/%d" % [hp, 100])            # 百分号
print("HP: {0}/{1}".format([hp, 100]))    # format
print("HP: %s" % str(hp))                 # str 拼接
```

**配方 9：播放一次音效（无需配置节点）**

```gdscript
func play_sfx(path: String) -> void:
	var p := AudioStreamPlayer.new()
	p.stream = load(path)
	p.finished.connect(p.queue_free)   # 播完自己删除
	add_child(p)
	p.play()
```

**配方 10：切换场景**

```gdscript
get_tree().change_scene_to_file("res://scenes/level2.tscn")
# 或带淡入淡出（见第 35 章 SceneRouter）
```

**配方 11：读写文本文件**

```gdscript
# 写
var f := FileAccess.open("user://save.txt", FileAccess.WRITE)
f.store_string("hello")
f.close()
# 读
if FileAccess.file_exists("user://save.txt"):
	var f2 := FileAccess.open("user://save.txt", FileAccess.READ)
	print(f2.get_as_text())
```

**配方 12：读取 JSON**

```gdscript
var f := FileAccess.open("user://data.json", FileAccess.READ)
var data: Variant = JSON.parse_string(f.get_as_text())
if data is Dictionary:
	print(data["name"])
```

**配方 13：定时器（Timer 节点式）**

```gdscript
$Timer.wait_time = 1.5
$Timer.one_shot = true
$Timer.timeout.connect(func(): print("到点"))
$Timer.start()
```

**配方 14：屏幕震动（简易）**

```gdscript
func shake(camera: Camera2D, duration: float, strength: float) -> void:
	var t := create_tween()
	for i in 8:
		t.tween_property(camera, "offset",
			Vector2(randf_range(-strength, strength),
					randf_range(-strength, strength)), duration / 8.0)
	t.tween_property(camera, "offset", Vector2.ZERO, 0.05)
```

**配方 15：平滑跟随（相机）**

```gdscript
func _process(delta: float) -> void:
	global_position = global_position.lerp(target.global_position, 5.0 * delta)
```

**配方 16：按概率触发**

```gdscript
if randf() < 0.1:   # 10% 概率
	print("触发稀有事件")
```

**配方 17：面朝方向翻转贴图**

```gdscript
sprite.flip_h = (target_pos.x - global_position.x) < 0.0
```

**配方 18：限制在屏幕内**

```gdscript
var vp := get_viewport_rect().size
global_position.x = clampf(global_position.x, 0.0, vp.x)
global_position.y = clampf(global_position.y, 0.0, vp.y)
```

**配方 19：暂停 / 恢复游戏**

```gdscript
get_tree().paused = not get_tree().paused
# 注意：菜单节点要设 process_mode = PROCESS_MODE_WHEN_PAUSED
```

**配方 20：安全重开当前场景**

```gdscript
get_tree().reload_current_scene()
```

**配方 21：把节点移动到另一个父节点**

```gdscript
var node := $SomeChild
var new_parent := get_tree().current_scene
node.reparent(new_parent)   # Godot 4 新增，安全
```

**配方 22：获取场景根节点并添加 UI**

```gdscript
var scene_root := get_tree().current_scene
var ui := preload("res://scenes/ui/popup.tscn").instantiate()
scene_root.add_child(ui)
```

**配方 23：一行连接按钮**

```gdscript
$Button.pressed.connect(func(): print("点击了"))
```

**配方 24：判断敌人是否在玩家前方（点积）**

```gdscript
var to_player := (player.global_position - global_position).normalized()
if facing.dot(to_player) > 0.0:
	print("玩家在我前方")
```

**配方 25：生成不重叠的随机位置（简单重试）**

```gdscript
func random_spawn(center: Vector2, radius: float) -> Vector2:
	for i in 10:
		var p := center + Vector2.from_angle(randf() * TAU) * randf_range(0.0, radius)
		if not _is_blocked(p):
			return p
	return center   # 兜底
```

---

## 36.12 本章小结

- **速查表的用法是"带着问题查"**：不要试图背下来。真正的熟练，是"知道有这么个东西存在，需要时能查得到"。
- **关键字表告诉你"什么不能当变量名"**：`var`、`if`、`class` 等一律不能用；`name`、`position` 等属性能用但强烈不建议。
- **数据类型的关键是"默认值 + 字面量 + 常用方法"三件套**：记住 `Vector2.ZERO`、`""`、`[]`、`{}`、`null` 这五个默认值，能省掉大量判空。
- **运算符最坑的两点**：① 整数除法 `7/2 == 3`；② 浮点不能用 `==` 比较，要用 `is_equal_approx()`。
- **字符串不可变**：所有方法要么返回新串，要么是只读查询，没有"原地修改字符串"这回事。
- **Array 与 Dictionary 要分清"原地 vs 新值"**：`sort()` 改自身，`duplicate()` 产生副本，`duplicate(true)` 才是深拷贝。
- **数学函数的 `f`/`i` 后缀含义固定**：`roundf` 返回 float、`roundi` 返回 int、`round` 是泛型。养成明确写后缀的习惯。
- **节点方法的四条主线**：生命周期（`_ready`/`_process`）、树操作（`add_child`/`queue_free`）、分组（`is_in_group`）、信号（`connect`/`emit`）。
- **注解是 Godot 4 的门面**：`@export` 家族决定了"策划能不能不写代码改数值"，`@onready` 决定了初始化时机，`@rpc` 决定了联网写法。
- **迁移对照表是"救命表"**：看到 `yield`、`onready`（无 @）、`instance()`、`connect("x", self, "f")`、`PoolStringArray`、`KinematicBody2D`，立刻知道要换成什么。
- **配方是"肌肉记忆"**：把这 25 条抄进你自己的代码片段库，写新功能时能直接复用，效率翻倍。
- **最后一句**：**语言只是工具，做出来才作数。** 你把这本书读到这里，已经超过了绝大多数"看了两眼就放弃"的人。现在，去写你自己的游戏吧。

---

> **全书完。**
>
> 从 `var hp = 100` 到能跑起来的小游戏，你已经走完了 GDScript 的完整旅程。愿这些知识，能在你做出下一个作品时，安静地为你所用。
---

# 第 37 章：报错词典

> 到这里，你已经学完了整本教程的语法与工程实践。但真实开发中，**拦住你的往往不是"不会写"，而是"报错看不懂"**。这一章就是你的"翻译官"：把 Godot 4 最常见的报错原文，一条条翻译成人话，并给出复现与修复。
>
> 本章不是让你从头读到尾的（那太痛苦了），而是**当字典用**：遇到红色报错时，复制报错原文，来这一章里 Ctrl+F 搜一下。

## 37.1 使用说明

### 37.1.1 怎么查

本章按"报错发生的时机"分成三大类，你可以据此快速定位到对应小节：

| 报错种类 | 什么时候出现 | 本节 | 典型特征 |
| --- | --- | --- | --- |
| 解析 / 编译期错误（Parse / Compile Error） | 保存脚本的瞬间，编辑器底部"输出"面板立刻变红 | 37.3 | 代码根本跑不起来，游戏无法启动 |
| 运行时错误（Runtime Error） | 游戏运行到某一行代码时才崩 | 37.4 | 代码能启动，跑到某处才报错 |
| 逻辑错误（Silent Bug） | 不报错，但结果不对 | 37.5 | 红字一条没有，行为却莫名其秒 |

**检索方式**：按 `Ctrl+F`（macOS 为 `Cmd+F`），粘贴报错原文里最稳定的一段（一般不含具体变量名），例如搜 `Invalid get index` 而不是搜 `Invalid get index 'health'`。

### 37.1.2 每条包含哪几部分

为了让信息尽量"自解释"，37.3、37.4 的每一条都遵守**四段式（加症状共五段）**：

```
【报错原文】   —— 引擎原文，保留大小写与引号
【典型症状】   —— 你肉眼会看到什么现象（哪个面板、什么时机）
【最小复现代码】—— 能跑出这个错的最短脚本
【原因】       —— 引擎为什么这么报，背后的机制
【修复】       —— 正确代码对照 + 一句话口诀
```

37.5 的逻辑错误因为**不报错**，格式换成三段式：**【现象】→【根因】→【正确写法】**。

> 小贴士：Godot 的报错很多时候**第一条才是根因**，后面的报错是被"连坐"的连锁反应。先解决最上面那条。

---

## 37.2 报错阅读方法论

### 37.2.1 报错四要素

Godot 的报错虽然看起来很长，但信息就四块，认准它们，阅读速度能提升十倍：

| 要素 | 长什么样 | 提示 |
| --- | --- | --- |
| 错误类型 | `Invalid get index` / `Parse Error` / `Cannot call` | 决定你该去 37.3 还是 37.4 查 |
| 位置 (file:line) | `res://player.gd:42` 或 `player.gd:42 @ _ready()` | 精确到行号和函数，直接跳过去 |
| 描述 | 引号里的变量名、类型名 | 引号里的东西就是"案发对象" |
| 调用栈 (Stack trace) | 一长串 `at: xxx (file:line)` | 从**栈顶**往下读，第一行是"死在哪儿" |

Godot 4 的运行时报错典型形态：

```text
E 0:00:01:2345   player.gd:42 @ _process(): Invalid get index 'hp' (on base: 'Nil').
   <C++ 错误> <源码位置>
   <C++ 调用栈: ...>
   <GDScript 调用栈>
          at: _process (res://player.gd:42)
```

- `E` = Error（错误）；`W` = Warning（警告）。
- `0:00:01:2345` 是游戏启动后的相对时间（时:分:秒:毫秒）。
- `player.gd:42 @ _process()` 告诉你：**文件 player.gd 的第 42 行，在 _process 函数里**。

### 37.2.2 从栈顶往下读的规则

调用栈就像"事故现场的照片链"：**最上面一行是真正出错的那行代码**，下面的是"谁调用了它"。

```text
at: player_take_damage (res://combat.gd:88)   ← 实际报错点
at: _on_body_entered (res://bullet.gd:31)     ← 谁触发了它
at: _physics_process (res://bullet.gd:20)     ← 再上一级
```

读法口诀：**先看最上面一行定位"死在哪"，再往下看理解"怎么走到这的"**。

### 37.2.3 判断"报错在哪一层"

| 现象 | 说明 | 排查方向 |
| --- | --- | --- |
| 只在保存脚本时报错，游戏压根没启动 | 解析期问题 | 语法、缩进、标识符拼写 → 37.3 |
| 游戏能跑，进某个场景 / 做某个动作才崩 | 运行期问题 | 空引用、越界、类型不符 → 37.4 |
| 完全不报错，但表现怪 | 逻辑问题 | 归一化、帧率、引用共享 → 37.5 |
| 报错指向 `C++` 源码行、你根本没写 | 引擎内部或插件问题 | 先回退到"你自己脚本栈帧"那一行 |

> 记住一句话：**报错是朋友，不是敌人。** 没有报错的白屏才是最难查的。

---

## 37.3 Parse / 编译期错误

> 这一类错误发生在**你按 Ctrl+S 的瞬间**。它们不需要运行游戏就能发现，属于"最好对付"的一批。

### 37.3.1 Expected end of statement after expression

**【报错原文】**
```text
Parse Error: Expected end of statement after expression.
```

**【典型症状】** 保存脚本时立刻报错，编辑器光标定位到某行，行尾可能有个突兀的字符。

**【最小复现代码】**
```gdscript
var hp = 100 power = 10     # 一行里写了两个赋值，中间没换行/分号
```

**【原因】** 解析器读到 `100` 时认为一条语句结束了，结果后面又冒出 `power`，它不知道这俩是什么关系。GDScript 是"一行一条语句"，除非显式用 `;`。

**【修复】**
```gdscript
# 正确：拆成两行
var hp = 100
var power = 10
# 或者用分号（不推荐养成习惯）
var hp = 100; var power = 10
```
**口诀：一行一语句，别在同一行堆两句赋值。**

### 37.3.2 Parse Error: Indentation error / Unindent doesn't match any outer indentation level

**【报错原文】**
```text
Parse Error: Unindent doesn't match any outer indentation level.
Parse Error: Indentation error.
```

**【典型症状】** 保存即报错，报错行常常是某个 `else`、`elif`、或者函数结尾。代码看起来"明明对齐了"。

**【最小复现代码】**
```gdscript
func test():
    if true:
        print("a")
      print("b")     # 缩进比上一行少了 2 格，但又没退回到 if 外层的 4 格位置
```

**【原因】** GDScript 用**缩进表示代码块层级**（像 Python）。缩进量必须能"对齐到某个外层级别"。上面 `print("b")` 缩进 6 格，而存在的外层级别只有 0 格和 4 格、8 格——6 格"悬空"，引擎不知道它属于哪层。另外，**同一项目里用 Tab 和空格混用**也会触发此错。

**【修复】**
```gdscript
func test():
    if true:
        print("a")   # 8 格
    print("b")       # 退回 4 格，表示"在 if 之外、函数之内"
```
**口诀：缩进只能回到已有层级；Tab 和空格不要混用，本项目统一用 4 个空格或一个 Tab。**

### 37.3.3 Identifier "xxx" not declared in the current scope

**【报错原文】**
```text
Parse Error: Identifier "hp" not declared in the current scope.
```

**【典型症状】** 保存报错，指向某个变量名，通常是你刚想用的名字。

**【最小复现代码】**
```gdscript
func _ready():
    prnt("hello")     # 少打了一个字母 i，写成 prnt
```

**【原因】** 你用的标识符（变量名 / 函数名 / 类名）在当前作用域里"查无此人"。常见诱因：**拼写错误**、**作用域不对**（在 A 函数定义，却在 B 函数用）、**没导入/没 preload**。

**【修复】**
```gdscript
func _ready():
    print("hello")    # 正确拼写

# 作用域示例：变量必须在使用前、同一作用域内声明
var hp := 100
func take_damage(dmg: int) -> void:
    hp -= dmg          # 能用，因为 hp 是成员变量
```
**口诀：先看拼写，再看作用域，最后看有没有 preload。**

### 37.3.4 Variable "xxx" is already declared in this scope

**【报错原文】**
```text
Parse Error: Variable "hp" is already declared in this scope.
```

**【典型症状】** 保存报错，说某变量重复声明。

**【最小复现代码】**
```gdscript
func _ready():
    var hp := 100
    var hp := 200     # 同一个作用域内，hp 定义了两次
```

**【原因】** 同一作用域（同一个函数体 / 同一个类）内不允许两个同名变量。GDScript 不像某些语言会在内层"遮蔽"外层，它会直接报错要求你改名。

**【修复】**
```gdscript
func _ready():
    var hp := 100
    var max_hp := 200   # 换成不同名字
```
**口诀：一个作用域一个名字，重名就改名。**

### 37.3.5 The identifier "xxx" isn't a valid class name

**【报错原文】**
```text
Parse Error: The identifier "Healther" isn't a valid class name.
```

**【典型症状】** 保存报错，指向一个你以为存在的类名。

**【最小复现代码】**
```gdscript
var h := Healther.new()   # 正确类名是 HealthComponent，这里拼错了
```

**【原因】** 你写的类型名/类名不存在或拼错。使用 `class_name` 注册的类、内置类型（`Node`、`Vector2`…）才能直接当类型名。写错一个字母就会报此错。

**【修复】**
```gdscript
# 假设组件脚本顶部有：class_name HealthComponent
var h := HealthComponent.new()
```
**口诀：类名要么是内置的，要么是你用 class_name 注册过的，否则就是拼错了。**

### 37.3.6 Class "xxx" hides a global script class

**【报错原文】**
```text
Parse Error: Class "Enemy" hides a global script class.
```

**【典型症状】** 报错指向 `class_name Enemy` 这一行。

**【最小复现代码】**
```gdscript
# enemy.gd
class_name Enemy
extends CharacterBody2D

# 同一个文件里又定义了一个内部类，名字一样
class Enemy:      # 与全局 class_name 重名
    var x := 1
```

**【原因】** `class_name Enemy` 会把类注册为**全局类**。如果同时项目里（或本文件内）还有一个叫 `Enemy` 的东西，就会冲突。

**【修复】**
```gdscript
class_name Enemy
extends CharacterBody2D

class EnemyStats:      # 内部类换个不冲突的名字
    var hp := 1
```
**口诀：全局 class_name 是唯一名号，别和别的定义撞名。**

### 37.3.7 Cannot find member "xxx" in base "yyy"

**【报错原文】**
```text
Parse Error: Cannot find member "color" in base "Sprite2D".
```

**【典型症状】** 保存报错，指向某属性 / 方法，你确信它应该存在。

**【最小复现代码】**
```gdscript
extends Sprite2D
func _ready():
    self.color = Color.RED    # Sprite2D 没有 color 属性（那是 modulate）
```

**【原因】** 你在某个类型的变量上访问了一个它**没有的成员**。Godot 在编译期就能确定静态类型，所以会直接拦住。原因通常是：**属性名记错**（把 `modulate` 记成 `color`）、**API 在 4.0 改名了**（见 38.3）。

**【修复】**
```gdscript
extends Sprite2D
func _ready():
    modulate = Color.RED      # 正确属性名
```
**口诀：报错说找不到成员，先怀疑名字记错 / 版本改名，去官方文档确认。**

### 37.3.8 Function "xxx" has the same name as a previously declared function

**【报错原文】**
```text
Parse Error: Function "take_damage" has the same name as a previously declared function.
```

**【典型症状】** 保存报错，说函数重名。

**【最小复现代码】**
```gdscript
func take_damage(a: int) -> void: pass
func take_damage(a: int, b: int) -> void: pass    # 同名，但参数不同
```

**【原因】** GDScript **不支持函数重载**（不像 C++/C# 可以同名不同参）。同名函数只能有一个。

**【修复】**
```gdscript
func take_damage(a: int) -> void: pass
func take_damage_with_bonus(a: int, b: int) -> void: pass   # 改名
```
**口诀：GDScript 没有重载，同名函数只能一个，不同功能就起不同名。**

### 37.3.9 Too many arguments for "xxx" call

**【报错原文】**
```text
Parse Error: Too many arguments for "take_damage()" call. Expected at most 1 but received 2.
```

**【典型症状】** 保存报错，指出调用某函数时参数个数不对。

**【最小复现代码】**
```gdscript
func take_damage(amount: int) -> void: pass
func _ready():
    take_damage(10, 20)   # 只接受 1 个参数，却传了 2 个
```

**【原因】** 调用时传的参数个数超过函数定义能接受的最大值。参数多的那个往往是你"多写了一个"。

**【修复】**
```gdscript
take_damage(10)                          # 数量匹配
# 若确实需要两个，就改函数定义：
# func take_damage(amount: int, source: Node = null) -> void: pass
```
**口诀：函数要几个参数就给几个，多了少了都报错。**

### 37.3.10 Static function cannot be virtual / override

**【报错原文】**
```text
Parse Error: Function "foo()" cannot be virtual. Static functions can't be virtual.
Parse Error: The function signature doesn't match the parent. Parent signature is ...
```

**【典型症状】** 报错发生在把 `static` 和虚函数（可被 override 的函数）混用时。

**【最小复现代码】**
```gdscript
extends Node
static func _ready() -> void:   # _ready 是引擎会调用的虚函数，不能是 static
    pass
```

**【原因】** `static`（静态）函数不依赖实例，而 `_ready`、`_process` 这类引擎回调必须绑定到实例。二者冲突。另外，override 父类函数时**参数列表必须完全一致**，否则报签名不匹配。

**【修复】**
```gdscript
extends Node
func _ready() -> void:      # 引擎回调不要 static
    pass

static func helper() -> int:   # 纯工具函数才用 static
    return 1
```
**口诀：引擎回调不 static；覆写父类函数，签名要一模一样。**

### 37.3.11 The class "xxx" cannot be instantiated because it is not a node class / cannot instantiate abstract class

**【报错原文】**
```text
Parse Error: Cannot instantiate abstract class "Shape".
```
或运行时：
```text
Invalid call. Nonexistent function 'new' in base 'GDScript'.
```

**【典型症状】** 想 `SomeClass.new()` 创建实例，却报不能实例化。

**【最小复现代码】**
```gdscript
# 抽象基类
@abstract
class_name Entity
extends Node

# 使用时
var e := Entity.new()    # 抽象类不能直接 new
```

**【原因】** Godot 4.4+ 支持 `@abstract` 标记抽象类，抽象类**只能被继承，不能直接实例化**。此外某些内置类型（如 `Shape`、`Node` 的纯虚基类）也不能直接 `new`。

**【修复】**
```gdscript
class_name Player
extends Entity      # 继承抽象类，实现它要求的抽象方法

func _ready():
    var p := Player.new()   # 实例化具体子类
```
**口诀：抽象类只当"模板"，要 new 就 new 它的具体子类。**

### 37.3.12 Cyclic reference in class inheritance

**【报错原文】**
```text
Parse Error: Cyclic reference in class inheritance.
```

**【典型症状】** 保存报错，且报错文件看起来风马牛不相及。

**【最小复现代码】**
```gdscript
# a.gd
class_name A extends B

# b.gd
class_name B extends A     # B 继承 A，而 A 又继承 B —— 循环了
```

**【原因】** 继承链形成了环：A 是 B 的父类，B 又是 A 的父类，谁也没法"排在前面"。`preload` 互相引用也会触发类似循环。

**【修复】**
```gdscript
# 抽出公共父类 base.gd: class_name Base extends Node
# a.gd: class_name A extends Base
# b.gd: class_name B extends Base
```
**口诀：继承是一棵树，不能成环；两个类互相 preload 也会成环。**

### 37.3.13 Expected ":" after "if" condition

**【报错原文】**
```text
Parse Error: Expected ":" after "if" condition.
```

**【典型症状】** 报错指向 `if` / `elif` / `else` / `for` / `while` / `func` 行的末尾。

**【最小复现代码】**
```gdscript
if hp > 0
    print("alive")     # if 条件后少了冒号
```

**【原因】** GDScript 的复合语句头部（`if/elif/else/for/while/func/class/match`）**必须以冒号结尾**。冒号是块开始的标志。

**【修复】**
```gdscript
if hp > 0:
    print("alive")
```
**口诀：块语句开头一律带冒号，`else` 也带（`else:`）。**

### 37.3.14 更多解析错误速查

| 报错原文 | 一句话原因 | 修复 |
| --- | --- | --- |
| `Expected ")" but found ...` | 括号没配对 | 补全/删除多余括号 |
| `Expected closing "]"` | 数组/索引方括号不配对 | 检查 `[` `]` |
| `Expected indented block after "..."` | `if/for` 后没有缩进块 | 下面补一行缩进的语句或加 `pass` |
| `Unindent to fraction of indentation` | 缩进量非整数层级 | 统一缩进单位 |
| `Expected expression in assignment` | 赋值号右边为空 | 补上右值 |
| `Assignment is not allowed in this context` | 在表达式中写赋值 | 拆成两条语句 |
| `Can't use a void function as a value` | 把无返回值的函数当值用 | 让函数 `return` 一个值 |
| `The argument 1 is not a constant expression` | 该处要求编译期常量 | 换成字面量或常量 |
| `Cannot use a local variable before it is declared` | 变量先用后声明 | 把声明提到前面 |

---

## 37.4 运行时错误

> 这一类错误**游戏能启动**，但跑到某行代码时才崩。它是工程量最大的部分，也是你最常撞见的。核心病因只有两个：**拿到了空（null）**、**类型对不上**。

### 37.4.1 Invalid get index 'xxx' (on base: 'Nil')

**【报错原文】**
```text
Invalid get index 'hp' (on base: 'Nil').
```

**【典型症状】** 游戏运行中突然刷红字，指向某个 `xxx.hp` 之类的读取。

**【最小复现代码】**
```gdscript
var target: Node = null
func _ready():
    print(target.hp)    # target 是 null，还去读它的 hp
```

**【原因】** 你在一个**值为 null** 的变量上用 `[]` 或 `.属性` 取值。常见于：`$Node` 路径写错拿不到节点、信号回调里的参数没传、对象已被 `queue_free`。

**【修复】**
```gdscript
if is_instance_valid(target):
    print(target.hp)

# 或取节点用可选方式
var label := get_node_or_null("HP/Label")
if label:
    label.text = "100"
```
**口诀：访问属性前，先问一句"它是不是 null"；取节点优先 `get_node_or_null`。**

### 37.4.2 Invalid set index 'xxx' (on base: 'Nil')

**【报错原文】**
```text
Invalid set index 'hp' (on base: 'Nil').
```

**【典型症状】** 与上一条对称，报的是**写入**。

**【最小复现代码】**
```gdscript
var target: Node = null
func _ready():
    target.hp = 10     # 往 null 里写属性
```

**【原因】** 试图给一个 null 的基对象设置属性。多半是"我以为它初始化好了，其实还没有"——比如在 `_enter_tree` 就用了 `@onready` 变量（见 37.5.4）。

**【修复】**
```gdscript
func _ready():
    if target:
        target.hp = 10

# 或先确保 target 被赋值：
@onready var target := $Enemy
```
**口诀：写属性前同样先判空；注意 @onready 的赋值时机。**

### 37.4.3 Attempt to call function 'xxx' in base 'null instance' on a null instance

**【报错原文】**
```text
Attempt to call function 'take_damage' in base 'null instance' on a null instance.
```

**【典型症状】** 运行时报错，指向某个方法调用。

**【最小复现代码】**
```gdscript
var bullet: Node = null
func _ready():
    bullet.hit()     # 对 null 调用方法
```

**【原因】** 对一个 null 值调用函数。本质与 37.4.1 相同，只是这次是"调用"。最常见场景：**子弹/敌人已经被 `queue_free()` 回收，但计时器或信号又调了它一次**。

**【修复】**
```gdscript
if is_instance_valid(bullet):
    bullet.hit()

# 更稳的写法：取消对已释放对象的所有引用
func _exit_tree() -> void:
    bullet = null
```
**口诀：调用前判空；对象会死就别留悬空引用。**

### 37.4.4 Invalid call. Nonexistent function 'xxx' in base 'Node (xxx.gd)'

**【报错原文】**
```text
Invalid call. Nonexistent function 'heal' in base 'Node (player.gd)'.
```

**【典型症状】** 运行时报错，说对象上没有这个函数——但你确信写了。

**【最小复现代码】**
```gdscript
# player.gd
extends Node
func heal() -> void: pass

# main.gd
func _ready():
    var p := Node.new()     # 建的是裸 Node，不是 player.gd
    p.heal()                # 裸 Node 没有 heal
```

**【原因】** 调用对象上**不存在**该方法。原因通常是：调用的对象类型不对（拿成了父类/别的脚本）、函数名拼错、脚本没挂上、或该函数是 `static` 却被实例调用。

**【修复】**
```gdscript
func _ready():
    var p: Node = preload("res://player.gd").new()   # 正确实例化脚本
    p.heal()
```
**口诀：报"没有这个函数"，先确认对象到底挂了哪个脚本。**

### 37.4.5 Invalid access to property or key 'xxx' on a base object of type 'Nil'

**【报错原文】**
```text
Invalid access to property or key 'name' on a base object of type 'Nil'.
```

**【典型症状】** 与 37.4.1 类似，但措辞是"access to property or key"。

**【最小复现代码】**
```gdscript
var data: Dictionary = {}
func _ready():
    print(data["level"])     # 字典里没有 level 这个 key，且 data 为 null 时也会这样
```

**【原因】** 两种情况都会：① 基对象是 null；② 用 `[]` 访问字典 / 对象上不存在 `key`。Godot 无法区分"对象为空"和"键不存在"时，会给出这类警告性报错。

**【修复】**
```gdscript
var data: Dictionary = {"hp": 100}
if data.has("level"):
    print(data["level"])
else:
    print("没有 level")

# 或直接给默认值
print(data.get("level", 0))
```
**口诀：读字典前 `has()` 一下，或用 `dict.get(key, 默认值)`。**

### 37.4.6 Node not found: "xxx" (relative to "/root/...")

**【报错原文】**
```text
Node not found: "UI/HealthBar" (relative to "/root/Main").
```

**【典型症状】** 运行时报错，游戏可能黑屏，指向一句 `$` 或 `get_node`。

**【最小复现代码】**
```gdscript
extends Node2D
func _ready():
    var bar := $UI/HealthBar     # 场景里根本没有 UI/HealthBar 这个路径
```

**【原因】** `get_node` / `$` 找不到该路径的节点。原因：**路径写错**、**节点名被改**、**节点还没被加入场景树**（在 `_init` 里取子节点）、**父节点改名导致相对路径失效**。

**【修复】**
```gdscript
func _ready():
    var bar := get_node_or_null("UI/HealthBar")
    if bar == null:
        push_warning("HealthBar 节点没找到，请检查路径与场景结构")
        return

# 更稳：用 @onready，它在进入树后、_ready 前赋值
@onready var bar := $UI/HealthBar
```
**口诀：节点路径大小写敏感；先确认场景里真有这个节点，再确认取的时机。**

### 37.4.7 Condition "!is_inside_tree()" is true

**【报错原文】**
```text
Condition "!is_inside_tree()" is true. Returning: ...
```

**【典型症状】** 运行时报错，常在你手动 `remove_child` 后又操作节点时。

**【最小复现代码】**
```gdscript
func _ready():
    var n := $Child
    remove_child(n)          # 从树上摘下来
    n.global_position = Vector2.ZERO   # 不在树里，全局坐标无从计算
```

**【原因】** 某些操作（全局变换、`get_tree()`、`is_ancestor_of`）**要求节点在场景树内**。节点被 `remove_child` 后 `is_inside_tree()` 为 false，这些操作就会报"条件为真（即不在树里）"。

**【修复】**
```gdscript
func _ready():
    var n := $Child
    remove_child(n)
    n.position = Vector2.ZERO    # 改用局部坐标，不需要在树里
    add_child(n)                 # 或者先加回树再设全局坐标
```
**口诀：全局变换 / get_tree 类操作，节点必须"在树上"。**

### 37.4.8 Attempt to call function 'xxx' on a previously freed instance

**【报错原文】**
```text
Attempt to call function 'set_text' on a previously freed instance.
```

**【典型症状】** 时序性报错：先 `queue_free()`，之后某个延时/信号又调到它。

**【最小复现代码】**
```gdscript
func _ready():
    var lbl := $Label
    lbl.queue_free()
    await get_tree().create_timer(1.0).timeout
    lbl.text = "hi"      # lbl 已经被释放了
```

**【原因】** `queue_free()` 是"请求在本帧末尾销毁"。对象销毁后，引用变为"已释放实例"。之后再摸它就会报此错。对象本身可能已经 `null` 或处于非法状态。

**【修复】**
```gdscript
func _ready():
    var lbl := $Label
    await get_tree().create_timer(1.0).timeout
    if is_instance_valid(lbl):   # 用前再确认
        lbl.text = "hi"
```
**口诀：凡是"跨帧/跨 await"用到的节点，用前一律 `is_instance_valid`。**

### 37.4.9 Cannot change this value when the object is not inside the tree

**【报错原文】**
```text
Cannot change this value when the object is not inside the tree.
```

**【典型症状】** 设置某个属性时被拒绝。

**【最小复现代码】**
```gdscript
func _ready():
    var cam := Camera2D.new()
    cam.enabled = true      # 新节点还没 add_child，某些属性不允许此时改
```

**【原因】** 少数属性（如 Camera2D 的 `enabled`、某些物理属性）**只有在节点进入场景树后才允许修改**。

**【修复】**
```gdscript
func _ready():
    var cam := Camera2D.new()
    add_child(cam)          # 先入树
    cam.enabled = true      # 再设置
```
**口诀：新节点先 add_child，再改那些和场景状态相关的属性。**

### 37.4.10 Signal 'xxx' is already connected to given callable

**【报错原文】**
```text
Signal 'pressed' is already connected to given callable 'Button::_on_pressed' in that object.
```

**【典型症状】** 运行时报错，出现在 `_ready` 里 connect 的地方，尤其在**场景重载或多次实例化**后。

**【最小复现代码】**
```gdscript
func _ready():
    $Button.pressed.connect(_on_pressed)
    $Button.pressed.connect(_on_pressed)   # 同一 callable 连了两次
```

**【原因】** 同一个信号与同一个 callable 只能连一次（4.x 起会报错，3.x 是静默忽略）。多次连接会导致回调执行多次（见 37.5.3）。

**【修复】**
```gdscript
func _ready():
    if not $Button.pressed.is_connected(_on_pressed):
        $Button.pressed.connect(_on_pressed)

# 或改用编辑器连接，脚本里就别再连
# 或在 _exit_tree 里断开
```
**口诀：连接前 `is_connected` 一下，或统一在编辑器/代码二选一。**

### 37.4.11 Too many arguments for "connect" call / Invalid argument type

**【报错原文】**
```text
Invalid call. Nonexistent function 'connect' in base 'Signal'.
Too many arguments for "connect()" call.
```

**【典型症状】** 从 3.x 迁过来的代码，`connect` 立刻崩。

**【最小复现代码】**
```gdscript
# Godot 3 写法，在 4.x 会崩
$Button.connect("pressed", self, "_on_pressed")
```

**【原因】** Godot 4 把信号连接改成了 **Callable** 风格：`signal.connect(callable)`，不再传字符串方法名。旧的 `connect("sig", self, "method")` 无效。

**【修复】**
```gdscript
$Button.pressed.connect(_on_pressed)

# 带参数绑定
$Button.pressed.connect(_on_pressed.bind(42))

# 断开
$Button.pressed.disconnect(_on_pressed)
```
**口诀：4.x 信号一律 `信号.connect(可调用对象)`；字符串方法名写法已废弃。**

### 37.4.12 Invalid operands 'String' and 'int' in operator '+'

**【报错原文】**
```text
Invalid operands 'String' and 'int' in operator '+'.
```

**【典型症状】** 运行时报错，指向一行字符串拼接。

**【最小复现代码】**
```gdscript
func _ready():
    var hp := 100
    print("HP: " + hp)      # String + int 不能直接相加
```

**【原因】** GDScript 是强类型：**字符串只能与字符串拼接**。`+` 在 `String` 与 `int` 之间没有定义。

**【修复】**
```gdscript
func _ready():
    var hp := 100
    print("HP: " + str(hp))     # 转成字符串
    print("HP: %d" % hp)        # 或用格式化
    print("HP: ", hp)           # 或直接逗号多参（print 支持）
```
**口诀：String 拼接前，先把数字 `str()` 一下，或用 `%` 格式化。**

### 37.4.13 Cannot assign a value of type 'String' to variable of type 'int'

**【报错原文】**
```text
Cannot assign a value of type "String" to variable of type "int".
```

**【典型症状】** 保存或运行时报错，类型不符。

**【最小复现代码】**
```gdscript
var hp: int = "100"      # 字符串赋给 int
```

**【原因】** 变量声明了静态类型，赋值时类型不匹配，GDScript 不会自动转换（这与弱类型语言不同）。

**【修复】**
```gdscript
var hp: int = int("100")    # 显式转换
# 或
var hp: int = 100
```
**口诀：声明了类型，就得给对类型；字符串转数字用 `int()` / `float()`。**

### 37.4.14 Trying to assign value of type 'Array' to a variable of type 'int'

**【报错原文】**
```text
Trying to assign value of type "Array" to a variable of type "int".
```

**【典型症状】** 运行时报错，常见于"把一组数当成一个数"。

**【最小复现代码】**
```gdscript
func _ready():
    var hp: int = 0
    var hits := [10, 20, 30]
    hp = hits              # 把整个数组赋给 int
```

**【原因】** 你真的把数组赋给了整数。多半是想求和或取某个元素。

**【修复】**
```gdscript
var hp: int = 0
var hits := [10, 20, 30]
hp = hits[0]              # 取第一个元素
# 或求和
for h in hits:
    hp += h
```
**口诀：报"Array 赋给 int"，八成是忘写下标 `[i]` 或忘循环求和。**

### 37.4.15 get_tree() on a null instance / 必须在场景树内调用

**【报错原文】**
```text
Cannot call method 'get_tree' on a null instance.
```

**【典型症状】** 报错指向 `get_tree()`。

**【最小复现代码】**
```gdscript
extends Node
func _init():
    get_tree().create_timer(1.0)   # _init 时节点还没进树，get_tree() 返回 null
```

**【原因】** `get_tree()` 只有在节点**已加入场景树**后才非空。在 `_init`、`_enter_tree` 早期、或节点已被移除时调用会得到 null。所以要用 `await` 计时器，必须在 `_ready` 之后。

**【修复】**
```gdscript
func _ready():
    await get_tree().create_timer(1.0).timeout
    print("一秒后")

# 非节点（如 Resource）里没有 get_tree，需要别的方式拿 tree
```
**口诀：`get_tree()` 只在入树后可用；想等待就用 `_ready` 里的 `await get_tree().create_timer(...)`。**

### 37.4.16 Index p_index = x is out of bounds (size y)

**【报错原文】**
```text
Index p_index = 5 is out of bounds (size 3).
```

**【典型症状】** 运行时报错，指向数组/字符串下标。

**【最小复现代码】**
```gdscript
var arr := [1, 2, 3]
func _ready():
    print(arr[5])       # 越界，合法下标只有 0..2
```

**【原因】** 数组/`Packed*Array`/字符串的索引从 0 开始，最大合法下标是 `size - 1`。访问 `size` 或负数（除非用 `-1` 反向语义）会越界。

**【修复】**
```gdscript
var arr := [1, 2, 3]
func _ready():
    if arr.size() > 5:
        print(arr[5])
    else:
        print("下标越界，数组只有 %d 个元素" % arr.size())
    print(arr[-1])          # -1 表示最后一个，合法
```
**口诀：下标范围 `0 … size()-1`；访问前先 `.size()` 检查。**

### 37.4.17 Invalid type in function 'xxx' in base 'yyy'

**【报错原文】**
```text
Invalid type in function 'add_child' in base 'Node'. The variable type is 'int'.
```

**【典型症状】** 运行时报错，说参数类型不对。

**【最小复现代码】**
```gdscript
func _ready():
    add_child(42)      # add_child 需要一个 Node，却给了 int
```

**【原因】** 传给函数的实参类型与形参要求不符。

**【修复】**
```gdscript
func _ready():
    var child := Node2D.new()
    add_child(child)   # 传正确的类型
```
**口诀：报"Invalid type in function"，就看那个参数该是什么类型。**

### 37.4.18 Division by zero / Attempt to divide by zero

**【报错原文】**
```text
Division by zero.
```

**【典型症状】** 运行时报错，指向除法或取模表达式。

**【最小复现代码】**
```gdscript
func _ready():
    var count := 0
    var avg := 100 / count      # 除以 0
```

**【原因】** 除数为 0。浮点除法会得到 `inf`/`nan` 并报错；整数除法直接报错。取模 `% 0` 同理。

**【修复】**
```gdscript
func _ready():
    var count := 0
    var avg := 0 if count == 0 else 100 / count
    # 或先判断
    if count != 0:
        avg = 100 / count
```
**口诀：除法/取模前，先确认除数不为 0。**

### 37.4.19 Resource file not found: res://...

**【报错原文】**
```text
Resource file not found: res://assets/player.png.
```

**【典型症状】** 运行或加载时报错，图/音/场景加载失败。

**【最小复现代码】**
```gdscript
var tex := preload("res://assets/playr.png")    # 路径拼错，或文件不在
```

**【原因】** 路径写错、文件被删/移动、导出时没包含、或大小写不符（尤其从 Windows 迁到 Linux）。`preload` 是编译期加载，文件不存在直接报错；`load` 是运行期。

**【修复】**
```gdscript
const TEX := preload("res://assets/player.png")   # 确认路径与大小写

# 更稳的运行时加载：
func load_tex() -> Texture2D:
    if ResourceLoader.exists("res://assets/player.png"):
        return load("res://assets/player.png")
    push_error("贴图缺失")
    return null
```
**口诀：路径大小写敏感；资源缺失就用 `ResourceLoader.exists` 兜底。**

### 37.4.20 Can't load cached file /... 或 Condition "err" is true. Returning: ...

**【报错原文】**
```text
Can't open file: 'user://save.json' (errno: 2).
Condition "err" is true. Returning: ...
```

**【典型症状】** 读写文件时报错，往往发生在存/读档。

**【最小复现代码】**
```gdscript
func _ready():
    var f := FileAccess.open("user://save.json", FileAccess.READ)   # 文件还不存在
    var data := f.get_as_text()      # f 为 null，崩溃
```

**【原因】** 用 `READ` 打开一个不存在的文件，`FileAccess.open` 返回 `null`。`Condition "err" is true. Returning: ...` 是引擎内部的兜底报错——**看到它不要慌，回到你自己脚本的栈帧那一行**。

**【修复】**
```gdscript
func load_save() -> Dictionary:
    if not FileAccess.file_exists("user://save.json"):
        return {}
    var f := FileAccess.open("user://save.json", FileAccess.READ)
    if f == null:
        push_error("打开存档失败：%s" % error_string(FileAccess.get_open_error()))
        return {}
    return JSON.parse_string(f.get_as_text()) as Dictionary
```
**口诀：读文件前 `FileAccess.file_exists`；打开后永远判 `null`。**

### 37.4.21 更多运行时错误速查

| 报错原文 | 一句话原因 | 修复要点 |
| --- | --- | --- |
| `Attempt to open a file...` | 文件打不开 | 检查路径/权限/是否存在 |
| `Parameter "x" is null` | 传了 null 参数 | 传有效值或判空 |
| `Cannot get index of ...` | 类型不支持下标 | 换类型或改访问方式 |
| `Out of memory` | 递归太深/申请过大 | 改迭代、检查无限递归 |
| `Stack overflow` | 无限递归 | 加终止条件 |
| `Invalid assignment of property on base` | 属性不存在 | 核对属性名 |
| `Trying to set value of type ...` | 类型不符 | 显式转类型 |
| `Can't change state while flushing queries` | 物理回调里改动结构 | 用 `call_deferred` 延后 |
| `The node is already in the tree` | 重复 add_child | 先判 `get_parent()` |
| `Can't add child, already has parent` | 节点已有父 | 先 `remove_child` 或 `reparent` |
| `NaN` 相关报错 | 出现非法浮点 | 检查除以 0、开负数根 |

### 37.4.22 "报错在哪一层"的经典例子

```gdscript
# bullet.gd
extends Area2D

func _on_body_entered(body: Node) -> void:
    body.take_damage(10)    # ← 栈顶：如果 body 没有 take_damage，就死在这
```

报错栈可能是：
```text
Invalid call. Nonexistent function 'take_damage' in base 'StaticBody2D'.
at: _on_body_entered (res://bullet.gd:5)   ← 第一行是"死因"
at: ... 引擎物理回调
```

**结论**：不是 Area2D 的错，是"撞上来的 body 恰好是没有该方法的 StaticBody2D"。修复：

```gdscript
func _on_body_entered(body: Node) -> void:
    if body.has_method("take_damage"):
        body.take_damage(10)
```

---

## 37.5 逻辑类"不报错的错"

> 这一类最难查：**没有一条红字**，但游戏行为就是不对。它们的共同点是"隐藏的常识"。记住它们，胜过记住一百条报错。

### 37.5.1 斜向移动比直线快（没归一化）

**【现象】** 按 W 走一格的时间和按 W+D 斜着走一格不一样，斜着明显更快，走位手感飘。

**【根因】** 把 `Vector2(1, 1)` 当方向直接乘速度。它的长度是 `√2 ≈ 1.414`，不是 1，于是斜着走多出 41% 速度。

**【正确写法】**
```gdscript
func _physics_process(delta: float) -> void:
    var dir := Input.get_vector("left", "right", "up", "down")
    # get_vector 已经归一化，长度不超过 1
    velocity = dir * SPEED
    move_and_slide()

# 如果自己算方向，务必 normalized()
var raw := Vector2(input_x, input_y).normalized()
```
**口诀：方向向量要乘速度前，**先 `.normalized()`**。**

### 37.5.2 每帧 lerp 导致帧率不独立

**【现象】** 在高配电脑上平滑，在低配电脑上"瞬移"到位；或反过来，动画速度随帧率变化。

**【根因】** `lerp(a, b, 0.1)` 每帧调用一次，相当于"每帧靠拢 10%"。帧越多靠拢越快，和真实时间无关。

**【正确写法】**
```gdscript
# 错误：帧率相关
modulate.a = lerp(modulate.a, 1.0, 0.1)

# 正确一：用 delta 做指数衰减（与帧率无关）
modulate.a = lerp(modulate.a, 1.0, 1.0 - exp(-10.0 * delta))

# 正确二：确切的"每秒变化量"
modulate.a = move_toward(modulate.a, 1.0, 2.0 * delta)

# 正确三：用 Tween（引擎自动按时间插值）
var t := create_tween()
t.tween_property(self, "modulate:a", 1.0, 0.4)
```
**口诀：任何"每帧变化一点"的插值，都必须乘 `delta` 或用 `Tween`。**

### 37.5.3 信号重复连接导致回调执行多次

**【现象】** 按下按钮，函数执行了 2 次、3 次……次数随场景进出增加；或伤害一次扣了好几点。

**【根因】** 在每次进入场景时都 connect，却没断开；或同一 callable 被连了多次。

**【正确写法】**
```gdscript
func _ready() -> void:
    # 连接前判重
    if not btn.pressed.is_connected(_on_pressed):
        btn.pressed.connect(_on_pressed)

# 或者统一约定：只在编辑器里连，代码里不再连
# 或者在节点离开树时断开
func _exit_tree() -> void:
    if btn and btn.pressed.is_connected(_on_pressed):
        btn.pressed.disconnect(_on_pressed)
```
**口诀：连接之前先 `is_connected`，或"编辑器 / 代码"二选一。**

### 37.5.4 @onready 变量在 _ready 之前的 _enter_tree 里为 null

**【现象】** 在 `_enter_tree()` 里用 `@onready var label := $Label`，报 null 或行为异常。

**【根因】** `@onready` 的赋值时机是**进入树之后、`_ready()` 之前**，具体在 `_enter_tree` **结束时**才生效。所以在 `_enter_tree` 内部访问还是 null。

**【正确写法】**
```gdscript
@onready var label := $Label

func _enter_tree() -> void:
    # 这里 label 还是 null，别用
    pass

func _ready() -> void:
    label.text = "OK"   # 这里才安全
```
**口诀：`@onready` 变量只在 `_ready` 及之后可用，`_enter_tree` 里别碰。**

### 37.5.5 改 Array 时遍历自己导致跳元素

**【现象】** 遍历数组删除元素时，总会漏掉几个，或者越删越乱。

**【根因】** 遍历过程中删除元素，导致后续元素前移，`for` 的下标跟着跳过了刚移过来的那个。

**【正确写法】**
```gdscript
var arr := [1, 2, 3, 4, 5]

# 错误：边遍历边删
for i in arr:
    if i % 2 == 0:
        arr.erase(i)

# 正确一：倒序遍历删除
for i in range(arr.size() - 1, -1, -1):
    if arr[i] % 2 == 0:
        arr.remove_at(i)

# 正确二：先收集再删
var to_remove: Array[int] = []
for i in arr:
    if i % 2 == 0:
        to_remove.append(i)
for i in to_remove:
    arr.erase(i)

# 正确三：用 filter 生成新数组
arr = arr.filter(func(v): return v % 2 != 0)
```
**口诀：边遍历边删数组极其危险，优先倒序删或用 `filter`。**

### 37.5.6 字典 key 用 Vector2 或 Array 导致查不到

**【现象】** `dict[Vector2(1,1)]` 明明存过，再取却取不到。

**【根因】** 字典的 key 要"可哈希且按值比较"。`Array`、`Dictionary` 是**引用类型**，用它们当 key 是比引用；`Vector2` 虽然可哈希，但浮点误差会让两个"看起来一样"的向量不相等。

**【正确写法】**
```gdscript
var grid: Dictionary = {}

# 错误：用 Vector2 当 key，浮点误差会导致查不到
# grid[Vector2(1, 1)] = "wall"

# 正确：转成字符串或整数坐标作为 key
func key_of(cell: Vector2i) -> String:
    return "%d,%d" % [cell.x, cell.y]

grid[key_of(Vector2i(1, 1))] = "wall"
print(grid[key_of(Vector2i(1, 1))])   # "wall"
```
**口诀：字典 key 用"值语义且稳定"的（int/String/Vector2i），别用 Array/Dictionary/浮点向量。**

### 37.5.7 整数除法 5/2 == 2

**【现象】** 算平均数、百分比总是差一点，"50% 的血"变成 0。

**【根因】** GDScript 中两个 `int` 相除，结果仍是 `int`（向下取整），`5 / 2 == 2`。

**【正确写法】**
```gdscript
var a := 5
var b := 2

print(a / b)               # 2（整数除法）
print(float(a) / b)        # 2.5
print(a / float(b))        # 2.5
print(a * 1.0 / b)         # 2.5

# 求百分比
var ratio: float = float(current_hp) / float(max_hp)
```
**口诀：要小数结果，先 `float()` 一次；`/` 两端都是 int 就是整除。**

### 37.5.8 float 精度比较用 == 失效

**【现象】** 两个"应该相等"的浮点数，`==` 却为 false，导致状态判断出错。

**【根因】** 浮点是二进制近似，`0.1 + 0.2 != 0.3`。

**【正确写法】**
```gdscript
var a := 0.1 + 0.2
print(a == 0.3)                       # false
print(is_equal_approx(a, 0.3))        # true

# 或用容差
func approx(a: float, b: float, eps := 0.0001) -> bool:
    return absf(a - b) < eps
```
**口诀：浮点比较别用 `==`，用 `is_equal_approx` 或设容差。**

### 37.5.9 局部变量遮蔽成员变量导致改了没用

**【现象】** 函数里改了 `hp`，外面的成员 `hp` 却没变。

**【根因】** 函数内 `var hp := 0` 重新声明了一个**局部** `hp`，后续操作都作用在局部变量上，成员变量纹丝不动。

**【正确写法】**
```gdscript
var hp := 100          # 成员变量

func damage() -> void:
    hp -= 10           # 直接改成员，不要重新 var hp
    print(hp)

# 如果确实需要局部变量，起不同名字
func calc() -> int:
    var local_hp := hp
    return local_hp
```
**口诀：别用 `var` 重复声明与成员同名的变量，除非你明确知道自己在遮蔽。**

### 37.5.10 load() 同一资源修改互相影响（共享引用）

**【现象】** 改了一个敌人的贴图，结果场上所有敌人都变了；修改一个配置，另一个场景的配置也变了。

**【根因】** `load()` / `preload()` 对同一路径会返回**同一个 Resource 实例**（资源是引用类型，被缓存共享）。直接改它的属性，等于改了"全局那一份"。

**【正确写法】**
```gdscript
var base: Resource = preload("res://enemy.tres")

func make_unique() -> Resource:
    var copy := base.duplicate()      # 拷贝一份再改
    copy.set("hp", 50)
    return copy

# 数组/字典也要注意深拷贝
var a := [1, 2, 3]
var b := a.duplicate()               # 浅拷贝
var c := a.duplicate(true)           # 深拷贝（嵌套也拷）
```
**口诀：要改共享资源，先 `duplicate()`；数组/字典传参传的是引用，别以为传了副本。**

---

## 37.6 报错速查表（一页表格）

> 把这张表贴在显示器旁边。左侧搜"关键词"，中间看一句话原因，右侧跳小节。

| 报错 / 现象关键词 | 一句话原因 | 去哪节 |
| --- | --- | --- |
| `Expected end of statement` | 一行塞了多条语句 | 37.3.1 |
| `Indentation error` / `Unindent` | 缩进不匹配层级 / Tab 空格混用 | 37.3.2 |
| `not declared in the current scope` | 标识符没定义 / 拼错 / 作用域不对 | 37.3.3 |
| `already declared in this scope` | 同作用域变量重名 | 37.3.4 |
| `isn't a valid class name` | 类名不存在或拼错 | 37.3.5 |
| `hides a global script class` | 与全局 class_name 撞名 | 37.3.6 |
| `Cannot find member` | 属性名错 / 版本改名 | 37.3.7 |
| `same name as a previously declared function` | GDScript 无重载 | 37.3.8 |
| `Too many arguments` | 调用参数个数不对 | 37.3.9 |
| `cannot be virtual` | static 与虚函数冲突 / 签名不符 | 37.3.10 |
| `cannot be instantiated` / `abstract` | 抽象类不能直接 new | 37.3.11 |
| `Cyclic reference` | 继承或 preload 成环 | 37.3.12 |
| `Expected ":" after "if"` | 块语句头缺冒号 | 37.3.13 |
| `Invalid get index (on base: 'Nil')` | 对 null 取属性/下标 | 37.4.1 |
| `Invalid set index (on base: 'Nil')` | 对 null 写属性 | 37.4.2 |
| `base 'null instance'` | 对 null 调方法 | 37.4.3 |
| `Nonexistent function` | 对象没这个方法 | 37.4.4 |
| `Invalid access to property or key` | key 不存在 / 对象为空 | 37.4.5 |
| `Node not found` | 节点路径错 / 时机不对 | 37.4.6 |
| `!is_inside_tree()` | 不在树里却做树内操作 | 37.4.7 |
| `previously freed instance` | 用了已 `queue_free` 的对象 | 37.4.8 |
| `not inside the tree` | 属性要求先入树 | 37.4.9 |
| `already connected` | 信号重复连接 | 37.4.10 |
| `Too many arguments for "connect"` | 用了 3.x 连接写法 | 37.4.11 |
| `Invalid operands 'String' and 'int'` | 字符串直接拼数字 | 37.4.12 |
| `Cannot assign a value of type` | 类型不匹配 | 37.4.13 |
| `Trying to assign value of type 'Array'` | 数组赋给了单值 | 37.4.14 |
| `get_tree() ... null instance` | 未入树就取 tree | 37.4.15 |
| `Index ... out of bounds` | 下标越界 | 37.4.16 |
| `Invalid type in function` | 参数类型不对 | 37.4.17 |
| `Division by zero` | 除数为 0 | 37.4.18 |
| `Resource file not found` | 资源路径错/缺失 | 37.4.19 |
| `Can't load cached file` / `Condition "err"` | 文件打开失败（看返回 null） | 37.4.20 |
| 斜向移动更快 | 方向没归一化 | 37.5.1 |
| 帧率影响动画 | 每帧 lerp 没乘 delta | 37.5.2 |
| 回调执行多次 | 信号重复连接 | 37.5.3 |
| `_enter_tree` 里变量为 null | @onready 尚未赋值 | 37.5.4 |
| 遍历删数组跳元素 | 边遍历边删 | 37.5.5 |
| 字典查不到 | key 用了引用类型/浮点向量 | 37.5.6 |
| `5/2 == 2` | 整数除法 | 37.5.7 |
| 浮点 `==` 失效 | 精度误差 | 37.5.8 |
| 改了局部没改成员 | 变量遮蔽 | 37.5.9 |
| 改一个全变 | 资源共享引用 | 37.5.10 |

---

## 37.7 本章小结

- 报错分三类：**解析期**（保存就红）、**运行期**（跑到才红）、**逻辑期**（不红但错）。
- 读报错抓**四要素**：类型、位置 `file:line`、描述、调用栈；**从栈顶读起**，第一行才是死因。
- 解析期错误几乎全是**语法、缩进、拼写、类名**问题，最好办。
- 运行期错误九成是 **null 引用** 和 **类型不符**；口诀是"用前判空、类型对齐"。
- 逻辑错误靠**常识清单**：归一化、`delta`、信号判重、`@onready` 时机、遍历删数组、字典 key、整数除法、浮点比较、变量遮蔽、资源复制。
- 实在查不到，把报错原文粘进本章 37.6 速查表，或直接 `Ctrl+F` 搜 37.3 / 37.4。

> 上一章你做出了完整游戏，这一章你学会了"出了事怎么救"。下一章，我们处理每个 Godot 老兵的必经之路：**把 Godot 3 项目迁移到 Godot 4**。

---
---

# 第 38 章：Godot 3 → 4 迁移对照

> 你可能会问：都学完 37 章了，为什么最后还要讲"老版本"？
>
> 因为现实世界里，**大量的教程、插件、开源项目、你公司的老代码，都还停在 Godot 3.x**。你迟早会拿到一份 3.x 的脚本，需要在 4.x 里跑起来。这一章就是你的"翻译器"和"体检表"。
>
> 更重要的是：**理解 3→4 的差异，等于把前面 37 章的知识重新串了一遍**。你会发现"为什么 4.x 要这么设计"，比单独背 API 有用得多。

## 38.1 迁移前必读：Godot 3 与 4 的根本差异

### 38.1.1 一句话概括：这不是"小版本更新"

Godot 3.x → 4.x 是一次**破坏性大版本升级**（官方叫 "Godot 4.0 is a major rewrite"）。它不像 3.2 → 3.3 那样"下载新引擎、直接打开项目就能跑"。4.x 里：

- 渲染后端从 **GLES3/GLES2** 换成了 **Vulkan**（也提供 GLES3 兼容后端）；
- 脚本语言从 **GDScript 1.0** 升级到 **GDScript 2.0**（大量语法变化）；
- 一大批节点、属性、方法**改了名字**；
- 场景文件格式从 `format=2` 变成 `format=3`。

所以迁移从来不是"改几个 API"，而是"读一遍官方迁移文档 + 逐处翻译 + 手工验证"。

### 38.1.2 三大根本差异

**差异一：渲染与图形（Vulkan）**

| 方面 | Godot 3.x | Godot 4.x |
| --- | --- | --- |
| 主渲染 API | OpenGL ES 3.0 / 2.0 | Vulkan（默认）/ OpenGL ES 3.0 兼容 |
| 2D 光照 | `Light2D`，能力有限 | `Light2D` + `CanvasItem` 阴影大改，支持法线贴图更完整 |
| 材质 | `SpatialMaterial` | `StandardMaterial3D` |
| 全局光照 | `GIProbe` | `VoxelGI` |
| 烘焙光照 | `BakedLightmap` | `LightmapGI` |
| 天空 | `ProceduralSky` | `ProceduralSkyMaterial` 资源 |
| 粒子 | `Particles` / `Particles2D` | `GPUParticles3D` / `GPUParticles2D`、`CPUParticles3D/2D` |

> 一句话：**画面相关的 API，几乎全改过一遍**。这也是为什么"迁移场景/材质"比"迁移脚本"更费劲。

**差异二：GDScript 2.0（语法大改）**

这是本书读者最该关心的。GDScript 2.0 引入了：

- **注解（Annotations）**：`@export`、`@onready`、`@tool`、`@export_range` 等，取代了 3.x 的"特殊关键字"；
- **一等函数 / 可调用对象（Callable）**：`connect()` 直接传方法引用，不再传"对象 + 方法名字符串"；
- **属性（Property）语法**：`set/get` 关键字，取代 `setget`；
- **类型系统强化**：类型标注更普遍，导出变量**默认必须带类型或用属性**；
- **`await` 关键字**：取代 `yield`；
- **函数引用、lambda 表达式**更自然。

**差异三：节点改名（3D 无限适配）**

Godot 3.x 里 2D 和 3D 节点很多是"共用名字"（如 `Sprite`、`RayCast`、`Camera`、`MeshInstance`）。4.x 为了消除歧义，**3D 版统一加 `3D` 后缀，2D 版统一加 `2D` 后缀**：

- `Spatial` → `Node3D`（这是最显著的改名，整棵 3D 场景树的根都换了）；
- `KinematicBody` → `CharacterBody3D`；`KinematicBody2D` → `CharacterBody2D`；
- `Sprite` → `Sprite2D`；`MeshInstance` → `MeshInstance3D`；
- 等等（详见 38.3 全表）。

> 记住这个规律，能帮你不查表猜出一半改名：**看到 3.x 里"没说 2D 也没说 3D"的节点名，先想它到底是几 D，再补后缀。**

### 38.1.3 两种迁移策略

拿到一个 3.x 项目，你有两条路。选错方向会浪费大量时间。

**策略 A：整体升级（"原地翻译"）**

适用场景：项目**体量不大**、逻辑清晰、你不打算重做美术、只想尽快让它跑起来。

做法：用官方转换工具跑一遍 → 修语法错误 → 逐个场景在编辑器里重存 → 手工修 API。优点是"改动量可控、可对照原代码"；缺点是"如果项目依赖大量 3.x 插件，插件本身没升级就白搭"。

**策略 B：重写核心（"推倒重构"）**

适用场景：项目**很大**、或你想顺便重整架构、或依赖的第三方插件没有 4.x 版。

做法：保留美术资源（图片、模型、音频、字体）、保留设计文档，**脚本与场景重写**。优点是"一步到位、架构更干净"；缺点是"前期投入大"。

**怎么选？** 给你一个经验公式：

| 判断维度 | 偏 A（整体升级） | 偏 B（重写核心） |
| --- | --- | --- |
| 项目代码行数 | < 5000 行 | > 20000 行 |
| 场景数量 | < 30 个 | > 100 个 |
| 第三方插件依赖 | 少，且都有 4.x 版 | 多，或已停更 |
| 美术资源比重 | 逻辑为主 | 美术为主 |
| 你的目标 | 先跑起来再说 | 一步到位、长期维护 |

> 本书立场：**新手项目一律选 A**。你现在的项目规模，重写纯属自虐。

---

## 38.2 语法层迁移对照（核心大表）

这一节是本章的"字典"。下表按"从最常遇到到较少遇到"排列。**每一行都是真实存在的差异，不要跳读。**

### 38.2.1 变量、注解与导出

| Godot 3 写法 | Godot 4 写法 | 说明 |
| --- | --- | --- |
| `onready var x = $Y` | `@onready var x = $Y` | `onready` 从关键字变成注解，前面加 `@` |
| `export var hp = 100` | `@export var hp: int = 100` | 导出**必须有类型**，或改用属性 set/get，否则报错 |
| `export(int) var hp = 100` | `@export var hp: int = 100` | 类型提示写法从 `export(类型)` 改为 `@export` + 类型标注 |
| `export(String) var name = ""` | `@export var name: String = ""` | 同上 |
| `export(Array, int) var ids = []` | `@export var ids: Array[int] = []` | 数组导出改为泛型标注 |
| `export(Resource) var res` | `@export var res: Resource` | 资源导出同样用类型 |
| `export(float, 0, 1) var r = 0.5` | `@export_range(0.0, 1.0) var r: float = 0.5` | 范围导出改为 `@export_range` |
| `export(int, "a,b,c") var t = 0` | `@export_enum("a", "b", "c") var t: int = 0` | 下拉枚举导出改为 `@export_enum` |
| `export(File) var f` | `@export_file() var f: String` | 文件导出改为 `@export_file` |
| `export var x = 5` | `@export var x := 5` | 用 `:=` 让引擎类型推断；**仅当能推断出类型才合法** |
| `tool` | `@tool` | 编辑器脚本声明改为注解 |
| `class_name Foo` | `class_name Foo` | 不变（保持原样） |
| `var x = 5`（无类型） | `var x := 5`（推荐） | 4.x 鼓励类型推断，`:=` 表示"推断出静态类型" |

> ⚠️ 关于 `@export var x := 5`：`:=` 会推断成 `int`。如果推断不出来（比如 `@export var x := null`），依然报错。最稳妥的写法永远是**显式类型**：`@export var x: int = 5`。

### 38.2.2 信号、连接与异步

| Godot 3 写法 | Godot 4 写法 | 说明 |
| --- | --- | --- |
| `connect("pressed", self, "_on_pressed")` | `pressed.connect(_on_pressed)` | 推荐用节点信号的 `.connect()` 方法 + Callable |
| `connect("pressed", self, "_on_pressed")` | `connect("pressed", _on_pressed)` | 也可以沿用 `Object.connect`，但第二参换成 Callable |
| `connect("pressed", self, "_on_pressed", [a, b])` | `connect("pressed", _on_pressed.bind(a, b))` | 绑定参数用 `Callable.bind()` |
| `connect("x", self, "m", [], CONNECT_ONESHOT)` | `x.connect(m, CONNECT_ONE_SHOT)` | 常量改名：`CONNECT_ONESHOT` → `CONNECT_ONE_SHOT` |
| `is_connected("x", self, "m")` | `is_connected("x", m)` | 只需"信号名 + Callable" |
| `disconnect("x", self, "m")` | `disconnect("x", m)` | 同上 |
| `emit_signal("hp_changed", hp)` | `hp_changed.emit(hp)` | 推荐新写法；`emit_signal("hp_changed", hp)` 仍可用 |
| `yield(obj, "signal")` | `await obj.signal` | `yield` 关键字被移除，改为 `await` |
| `yield(get_tree().create_timer(1.0), "timeout")` | `await get_tree().create_timer(1.0).timeout` | 等待计时器的典型写法 |
| `yield(get_tree(), "idle_frame")` | `await get_tree().process_frame` | 等待每帧信号的写法 |
| `var c = funcref(self, "foo")` | `var c := foo` 或 `var c := Callable(self, "foo")` | `funcref()` 被 Callable 取代 |

> `in` 关键字在 3 和 4 中行为一致（`for i in range(3)`、`"a" in dict`），无需迁移。

### 38.2.3 数组、字符串与内置类型

| Godot 3 写法 | Godot 4 写法 | 说明 |
| --- | --- | --- |
| `PoolStringArray` | `PackedStringArray` | Pool 类型改名，加 `Packed` 前缀并补位宽 |
| `PoolByteArray` | `PackedByteArray` | 同上 |
| `PoolIntArray` | `PackedInt32Array` | 明确位宽为 32 |
| `PoolRealArray` | `PackedFloat32Array` | 同上 |
| `PoolVector2Array` | `PackedVector2Array` | 同上 |
| `PoolVector3Array` | `PackedVector3Array` | 同上 |
| `PoolColorArray` | `PackedColorArray` | 同上 |
| `Array.empty()` | `Array.is_empty()` | 判断空都改为 `is_empty()` |
| `Dictionary.empty()` | `Dictionary.is_empty()` | 同上 |
| `String.empty()` | `String.is_empty()` | 同上 |
| `arr.invert()` | `arr.reverse()` | 反转数组改名 |
| `arr.subarray(1, 3)` | `arr.slice(1, 3)` | 取子数组改名 |
| `arr.find_last(v)` | `arr.rfind(v)` | 从后查找改名 |
| `str.plus_file("a.txt")` | `str.path_join("a.txt")` | 拼接路径改名 |
| `str.left(3)` / `str.right(3)` | `str.substr(0, 3)` / `str.substr(-3)` | 左右截取被 `substr` 取代 |
| `str.find_last("x")` | `str.rfind("x")` | 同上 |
| `str.empty()` | `str.is_empty()` | 同上 |
| `str.is_valid_integer()` | `str.is_valid_int()` | 改名 |
| `str.to_ascii()` | `str.to_ascii_buffer()` | 返回 `PackedByteArray` |
| `stepify(v, 0.1)` | `snapped(v, 0.1)` | 全局函数改名 |
| `rand_range(1, 5)` | `randf_range(1.0, 5.0)` | 区分整型/浮点：`randf_range` / `randi_range` |
| `deg2rad(x)` / `rad2deg(x)` | `deg_to_rad(x)` / `rad_to_deg(x)` | 三角函数改名 |
| `OS.get_ticks_msec()` | `Time.get_ticks_msec()` | 时间相关从 `OS` 移到 `Time` |
| `OS.get_unix_time()` | `Time.get_unix_time_from_system()` | 同上 |
| `OS.get_datetime()` | `Time.get_datetime_dict_from_system()` | 同上 |
| `OS.window_size` | `DisplayServer.window_get_size()` | 窗口相关从 `OS` 移到 `DisplayServer` |
| `OS.set_window_fullscreen(true)` | `DisplayServer.window_set_mode(DisplayServer.WINDOW_MODE_FULLSCREEN)` | 改为设置"窗口模式" |
| `Engine.editor_hint` | `Engine.is_editor_hint()` | 属性改方法 |

### 38.2.4 面向对象与场景

| Godot 3 写法 | Godot 4 写法 | 说明 |
| --- | --- | --- |
| `scene.instance()` | `scene.instantiate()` | `instance()` 全面改名 `instantiate()` |
| `var x setget set_x, get_x` | `var x: int: set = set_x, get = get_x` | `setget` 关键字废弃，改用属性语法 |
| `var x = 5 setget ,get_x` | `var x := 5: get: return x + 1` | 属性支持内联 get/set 代码块 |
| `.tscn` 中 `format=2` | `.tscn` 中 `format=3` | 场景文件格式版本升级 |
| `preload("res://a.gd")` | `preload("res://a.gd")` | 不变 |
| `ClassDB.instance("Node")` | `ClassDB.instantiate("Node")` | 反射创建也改名 |
| `yield` 关键字 | `await` 关键字 | 关键字替换 |
| `Object.get_meta()` / `set_meta()` | 不变 | 元数据 API 保持 |

### 38.2.5 属性（Property）语法详解

3.x 的 `setget` 是新手最容易迷惑的地方之一，4.x 改成了更接近 Python 的写法。对照如下：

```gdscript
# Godot 3.x
var hp = 100 setget set_hp, get_hp

func set_hp(value):
    hp = clamp(value, 0, max_hp)

func get_hp():
    return hp

# Godot 4.x —— 写法一：命名方法
var hp: int = 100:
    set(value):
        hp = clampi(value, 0, max_hp)
    get:
        return hp
```

如果 setter/getter 逻辑写在同一处，还可以内联：

```gdscript
# Godot 4.x —— 写法二：内联
var hp: int = 100:
    set(value):
        hp = clampi(value, 0, max_hp)
    get:
        return hp

# 只读属性（外部不可写，但可读）
var level: int = 1:
    get:
        return level
```

> 关键规则：**setter/getter 内部给属性自身赋值时，不会再次触发 setter/getter**（否则会无限递归）。这是 4.x 明确的语义。

---

## 38.3 节点与场景迁移：节点类改名全表

下表覆盖最常遇到的节点改名。规律记牢：**3D 补 `3D`，2D 补 `2D`，服务类改名，被合并的节点改成"功能开关"。**

### 38.3.1 3D 节点改名

| Godot 3 节点 | Godot 4 节点 | 说明 |
| --- | --- | --- |
| `Spatial` | `Node3D` | 3D 空间节点的根，改名最具象征性 |
| `KinematicBody` | `CharacterBody3D` | 角色物理体 |
| `RigidBody` | `RigidBody3D` | 刚体 |
| `StaticBody` | `StaticBody3D` | 静态物理体 |
| `Area` | `Area3D` | 触发区 |
| `Camera` | `Camera3D` | 3D 相机 |
| `Light` | `Light3D` | 3D 灯光 |
| `MeshInstance` | `MeshInstance3D` | 网格实例 |
| `MultiMeshInstance` | `MultiMeshInstance3D` | 多网格实例 |
| `RayCast` | `RayCast3D` | 3D 射线 |
| `Position3D` | `Marker3D` | 位置标记 |
| `Skeleton` | `Skeleton3D` | 骨骼 |
| `BoneAttachment` | `BoneAttachment3D` | 骨骼挂点 |
| `Path` | `Path3D` | 3D 路径 |
| `Listener` | `AudioListener3D` | 3D 听觉监听 |
| `ImmediateGeometry` | `ImmediateMesh`（资源） | 从节点变成 Mesh 资源 |
| `ProximityGroup` | 已移除 | 用其他方式实现 |
| `VehicleBody` | `VehicleBody3D` | 载具 |
| `SpringArm` | `SpringArm3D` | 弹簧臂 |
| `VisibilityNotifier` | `VisibleOnScreenNotifier3D` | 可见性通知 |
| `VisibilityEnabler` | `VisibleOnScreenEnabler3D` | 可见性使能 |
| `NavigationMeshInstance` | `NavigationRegion3D` | 导航区域 |
| `Navigation` | `NavigationRegion3D` | 同上 |
| `GIProbe` | `VoxelGI` | 体素全局光照 |
| `BakedLightmap` | `LightmapGI` | 烘焙光照 |
| `ReflectionProbe` | `ReflectionProbe` | 不变 |
| `InterpolatedCamera` | 已移除 | 用脚本/Tween 实现 |

### 38.3.2 2D 节点改名

| Godot 3 节点 | Godot 4 节点 | 说明 |
| --- | --- | --- |
| `Sprite` | `Sprite2D` | 精灵 |
| `KinematicBody2D` | `CharacterBody2D` | 2D 角色物理体 |
| `Position2D` | `Marker2D` | 位置标记 |
| `Particles2D` | `GPUParticles2D` / `CPUParticles2D` | 拆成 GPU / CPU 两种 |
| `Line2D` | `Line2D` | 不变 |
| `YSort` | `Node2D` + `y_sort_enabled` | 节点被移除，改为 Node2D 的属性开关 |
| `VisibilityNotifier2D` | `VisibleOnScreenNotifier2D` | 可见性通知 |
| `VisibilityEnabler2D` | `VisibleOnScreenEnabler2D` | 可见性使能 |
| `Navigation2D` | `NavigationServer2D` + `NavigationRegion2D` | 导航系统重构 |
| `NavigationPolygonInstance` | `NavigationRegion2D` | 导航区域 |
| `Light2D` | `Light2D` | 不变（但属性大改） |
| `CanvasModulate` | `CanvasModulate` | 不变 |
| `Path2D` | `Path2D` | 不变 |
| `TouchScreenButton` | `TouchScreenButton` | 不变 |
| `RemoteTransform2D` | `RemoteTransform2D` | 不变 |

### 38.3.3 服务与单例改名

| Godot 3 | Godot 4 | 说明 |
| --- | --- | --- |
| `ARVRServer` | `XRServer` | VR/AR 统一为 XR |
| `ARVROrigin` | `XROrigin3D` | XR 原点 |
| `ARVRCamera` | `XRCamera3D` | XR 相机 |
| `ARVRController` | `XRController3D` | XR 手柄 |
| `ARVRAnchor` | `XRAnchor3D` | XR 锚点 |
| `ARVRInterface` | `XRInterface` | XR 接口 |
| `VisualServer` | `RenderingServer` | 渲染服务改名 |
| `Physics2DServer` | `PhysicsServer2D` | 物理服务改名 |
| `PhysicsServer` | `PhysicsServer3D` | 物理服务改名 |
| `AudioServer` | `AudioServer` | 不变 |
| `NavigationServer2D` | `NavigationServer2D` | 新增于 4.x |
| `NavigationServer` | `NavigationServer3D` | 改名 |
| `OS`（窗口相关） | `DisplayServer` | 窗口/显示功能拆分到 `DisplayServer` |
| `OS`（时间相关） | `Time` | 时间功能拆分到 `Time` |
| `Engine.editor_hint` | `Engine.is_editor_hint()` | 属性变方法 |

### 38.3.4 资源 / 材质 / 形状改名

| Godot 3 | Godot 4 | 说明 |
| --- | --- | --- |
| `SpatialMaterial` | `StandardMaterial3D` | 标准材质改名 |
| `ParticlesMaterial` | `ParticleProcessMaterial` | 粒子材质改名 |
| `ProceduralSky` | `ProceduralSkyMaterial` | 天空改为"材质资源" |
| `PanoramaSky` | `PanoramaSkyMaterial` | 全景天空改名 |
| `DynamicFont` | `FontFile` | 动态字体合并为 FontFile |
| `DynamicFontData` | `FontFile` | 同上 |
| `BitmapFont` | `FontFile` | 位图字体合并 |
| `BoxShape` | `BoxShape3D` | 形状补 3D 后缀 |
| `SphereShape` | `SphereShape3D` | 同上 |
| `CapsuleShape` | `CapsuleShape3D` | 同上 |
| `CylinderShape` | `CylinderShape3D` | 同上 |
| `ConvexPolygonShape` | `ConvexPolygonShape3D` | 同上 |
| `ConcavePolygonShape` | `ConcavePolygonShape3D` | 同上 |
| `RayShape` | `SeparationRayShape3D` | 射线形状改名 |
| `PlaneShape` | `WorldBoundaryShape3D` | 平面形状改名 |
| `AudioStreamSample` | 仍为 `AudioStreamWAV` | 音频采样改名 |
| `CubeMap` | `Cubemap` | 拼写规范 |
| `GDScriptNativeClass` | `GDScriptNativeClass` | 不变 |

---

## 38.4 属性 / 方法改名对照表

这一节专治"代码能跑，但属性/方法找不到"。这类报错最隐蔽，因为节点名都对，只是属性换了名字。

### 38.4.1 Control / CanvasItem 属性

| Godot 3 | Godot 4 | 说明 |
| --- | --- | --- |
| `rect_position` | `position` | Control 的局部位置 |
| `rect_size` | `size` | Control 的尺寸 |
| `rect_scale` | `scale` | 缩放 |
| `rect_rotation` | `rotation` | 旋转（弧度） |
| `rect_pivot_offset` | `pivot_offset` | 变换中心偏移 |
| `rect_min_size` | `custom_minimum_size` | 最小尺寸，改名很彻底 |
| `rect_clip_content` | `clip_contents` | 裁剪内容 |
| `margin_left` | `offset_left` | 左边距 → 左偏移 |
| `margin_right` | `offset_right` | 右边距 → 右偏移 |
| `margin_top` | `offset_top` | 上边距 → 上偏移 |
| `margin_bottom` | `offset_bottom` | 下边距 → 下偏移 |
| `visible`（CanvasItem） | `visible` | 不变 |
| `anchor_left/top/right/bottom` | 同名 | 不变 |
| `focus_mode` | `focus_mode` | 不变 |
| `mouse_filter` | `mouse_filter` | 不变 |
| `size_flags_horizontal` | `size_flags_horizontal` | 不变 |

### 38.4.2 Control / CanvasItem 方法

| Godot 3 | Godot 4 | 说明 |
| --- | --- | --- |
| `set_anchors_and_margins_preset()` | `set_anchors_and_offsets_preset()` | 预设布局改名 |
| `get_rect()` | `get_rect()` | 不变（`get_rect()` 仍在） |
| `get_global_rect()` | `get_global_rect()` | 不变 |
| `update()`（CanvasItem） | `queue_redraw()` | 请求重绘改名，最常遇到 |
| `_draw()` | `_draw()` | 不变 |
| `raise()`（CanvasItem） | `move_to_front()` | 提层改名 |
| `lower()`（CanvasItem） | `move_to_back()` | 降层改名 |
| `grab_focus()` | `grab_focus()` | 不变 |
| `accept_event()` | `accept_event()` | 不变 |

### 38.4.3 其他常用属性 / 方法

| Godot 3 | Godot 4 | 说明 |
| --- | --- | --- |
| `AnimationPlayer.playback_speed` | `AnimationPlayer.speed_scale` | 播放速度改名 |
| `AnimationPlayer.playback_active` | `AnimationPlayer.active` | 激活状态改名 |
| `AnimationPlayer.current_animation_length` | `AnimationPlayer.current_animation_length` | 保留 |
| `Camera2D.current` | `Camera2D.enabled` | 2D 相机激活开关改名 |
| `Camera3D.current` | `Camera3D.current` | 3D 相机不变 |
| `Node.pause_mode` | `Node.process_mode` | 暂停模式改为处理模式 |
| `PhysicsBody.gravity_scale` | 不变 | 保留 |
| `RigidBody.mode`（`MODE_RIGID` 等） | `freeze` + `freeze_mode` | 刚体模式改为冻结开关 |
| `RigidBody2D.mode` | `RigidBody2D.freeze` | 同上 |
| `Area2D.gravity_vec` | `Area2D.gravity_direction`（方向） | 重力方向改名 |
| `Area2D.gravity` | 同名 | 重力强度保留 |
| `RichTextLabel.add_text()` | `RichTextLabel.append_text()` | 追加文本改名 |
| `RichTextLabel.append_bbcode()` | `RichTextLabel.append_text()` | 合并为 append_text |
| `LineEdit.secret` | `LineEdit.secret` | 不变 |
| `LineEdit.get_text()` | `.text` | 去掉冗余 getter，直接用属性 |
| `TextEdit.text` | `.text` | 保留 |
| `SkeletonIK`（节点） | `SkeletonIK3D` | 改名（也属于 SkeletonModifier3D 家族） |
| `Tween`（节点 `interpolate_property`） | `create_tween()` + `tween_property()` | 整章级别的 API 更换（见下） |
| `SceneTree.change_scene("path")` | `SceneTree.change_scene_to_file("path")` | 切场景改名 |
| `SceneTree.change_scene(packed)` | `SceneTree.change_scene_to_packed(packed)` | 切场景改名 |
| `Node.set_network_master()` | `Node.set_multiplayer_authority()` | 网络权限改名 |
| `Node.get_network_master()` | `Node.get_multiplayer_authority()` | 同上 |
| `Directory.open()` | `DirAccess.open()` | 目录改名（见下） |
| `File.open()` | `FileAccess.open()` | 文件改名（见下） |

### 38.4.4 Tween 迁移详解（重点）

Godot 3 的 `Tween` 是**一个节点**，你要先把它加到场景里，然后：

```gdscript
# Godot 3.x：Tween 是节点
var tween = $Tween
tween.interpolate_property(sprite, "modulate:a", 1.0, 0.0, 0.5,
    Tween.TRANS_SINE, Tween.EASE_OUT)
tween.start()  # 必须手动 start()
```

Godot 4 里 `Tween` 变成了**由 `SceneTree` 创建的对象**，且**自动开始**：

```gdscript
# Godot 4.x：用 create_tween() 创建
var tween := create_tween()
tween.tween_property(sprite, "modulate:a", 0.0, 0.5)\
    .set_trans(Tween.TRANS_SINE).set_ease(Tween.EASE_OUT)
# 不需要 start()，创建即自动播放
```

要点：

1. **不需要起始值**了：`tween_property()` 从"当前值"开始补间到目标值，所以旧代码里那个 `initial` 参数被删掉；
2. **不用手动 `start()`**；
3. `interpolate_method()` → `tween_method()`；
4. `interpolate_callback()` → `tween_callback()`；
5. 过渡/缓动从函数参数变成了**链式调用**：`.set_trans()`、`.set_ease()`、`.set_delay()`；
6. 4.0 里类名一度叫 `SceneTreeTween`，4.1 起统一为 `Tween`，代码里用 `Tween` 即可。

> 顺带一提：4.x 里 `Tween` **不再需要放进场景树**，用完自动销毁（默认 `TWEEN_PROCESS_IDLE`）。但要记得：**一个 `Tween` 对象只能被"消费"一次**，想循环要写循环逻辑或 `set_loops()`。

### 38.4.5 File / Directory 迁移详解

Godot 3：

```gdscript
# Godot 3.x
var f = File.new()
var err = f.open("user://save.dat", File.WRITE)
if err == OK:
    f.store_string("hello")
    f.close()
```

Godot 4 里 `File` 改名 `FileAccess`，而且 `open()` 变成了**静态方法**，失败返回 `null`：

```gdscript
# Godot 4.x
var f := FileAccess.open("user://save.dat", FileAccess.WRITE)
if f != null:
    f.store_string("hello")
    f.close()
```

读文本更简单，直接有静态便捷方法：

```gdscript
# Godot 4.x：一行读整个文件（读不到返回空串）
var text := FileAccess.get_file_as_string("user://save.dat")
```

目录同理：

```gdscript
# Godot 3.x
var d = Directory.new()
d.open("user://saves")
d.list_dir_begin()
var name = d.get_next()
while name != "":
    name = d.get_next()
d.list_dir_end()

# Godot 4.x
var d := DirAccess.open("user://saves")
if d != null:
    d.list_dir_begin()
    var name := d.get_next()
    while name != "":
        name = d.get_next()
    d.list_dir_end()
```

---

## 38.5 信号改动的完整说明

信号是 Godot 3→4 改动最"伤筋动骨"的一块，单独拎出来讲。

### 38.5.1 连接：从"字符串寻址"到"Callable"

Godot 3 的连接依赖"对象 + 方法名字符串"，**写错方法名不会报错，运行时才发现**：

```gdscript
# Godot 3.x
button.connect("pressed", self, "_on_button_pressed")
```

Godot 4 直接传方法引用（Callable），**方法名写错编辑器立刻标红**：

```gdscript
# Godot 4.x
button.pressed.connect(_on_button_pressed)
# 或沿用 Object.connect：
button.connect("pressed", _on_button_pressed)
# 或显式构造 Callable：
button.connect("pressed", Callable(self, "_on_button_pressed"))
```

### 38.5.2 绑定参数：`binds` 数组 → `Callable.bind()`

```gdscript
# Godot 3.x：第四参是参数数组
button.connect("pressed", self, "_on_click", [item_id, item_name])

# Godot 4.x：用 bind() 绑定，按顺序追加到信号参数之后
button.pressed.connect(_on_click.bind(item_id, item_name))
```

### 38.5.3 一次性连接与标志位

```gdscript
# Godot 3.x
timer.connect("timeout", self, "_on_timeout", [], CONNECT_ONESHOT)

# Godot 4.x（常量改名 ONE_SHOT）
timer.timeout.connect(_on_timeout, CONNECT_ONE_SHOT)
```

常用标志对照：

| Godot 3 | Godot 4 | 含义 |
| --- | --- | --- |
| `CONNECT_DEFERRED` | `CONNECT_DEFERRED` | 延迟到空闲帧调用 |
| `CONNECT_ONESHOT` | `CONNECT_ONE_SHOT` | 触发一次后自动断开 |
| `CONNECT_PERSIST` | `CONNECT_PERSIST` | 序列化时保留连接 |
| `CONNECT_REFERENCE_COUNTED` | `CONNECT_REFERENCE_COUNTED` | 引用计数连接 |

### 38.5.4 `is_connected` / `disconnect`

```gdscript
# Godot 3.x
if button.is_connected("pressed", self, "_on_pressed"):
    button.disconnect("pressed", self, "_on_pressed")

# Godot 4.x
if button.pressed.is_connected(_on_pressed):
    button.pressed.disconnect(_on_pressed)
```

### 38.5.5 发射：`emit_signal` → `.emit()`

```gdscript
# Godot 3.x
emit_signal("hp_changed", hp)

# Godot 4.x（推荐，类型安全、可自动补全）
hp_changed.emit(hp)

# Godot 4.x（仍可用，但不推荐，因为信号名是字符串，易写错）
emit_signal("hp_changed", hp)
```

> 在 4.x 里，**自定义信号的 `.emit()` 会做参数数量检查**（参数个数不对会报错），比 3.x 更安全。

### 38.5.6 信号声明可以带类型

4.x 允许在声明信号时给参数加类型，配合静态检查：

```gdscript
signal hp_changed(new_hp: int)
signal died
```

---

## 38.6 常见迁移报错的解决（10+ 条）

下面每条遵循**「报错原文 → 原因 → 改法」**。都是迁移时高频踩坑。

### 1. `Identifier "yield" not declared in the current scope.`

- **原因**：GDScript 2.0 移除了 `yield` 关键字。
- **改法**：把 `yield(obj, "signal")` 改成 `await obj.signal`。

```gdscript
# 旧：yield(get_tree().create_timer(1.0), "timeout")
# 新：
await get_tree().create_timer(1.0).timeout
```

### 2. `Invalid call. Nonexistent function 'instance' in base 'PackedScene'.`

- **原因**：`PackedScene.instance()` 被改名为 `instantiate()`。
- **改法**：全局搜索 `.instance()`，改成 `.instantiate()`（注意别误改 `ClassDB.instance`，它也要改成 `instantiate`）。

### 3. `Invalid call. Nonexistent function 'interpolate_property' in base 'Tween'.`

- **原因**：Godot 4 的 `Tween` 不再是那个有 `interpolate_property` 的节点。
- **改法**：改用 `create_tween()` + `tween_property()`，并删掉 `start()`。

```gdscript
var tween := create_tween()
tween.tween_property(node, "modulate:a", 0.0, 0.3)
```

### 4. `Cannot find property 'rect_position' on base 'Control'.`

- **原因**：`rect_*` 系列属性改名。
- **改法**：`rect_position→position`、`rect_size→size`、`rect_min_size→custom_minimum_size`、`rect_scale→scale`、`rect_pivot_offset→pivot_offset`、`rect_rotation→rotation`。

### 5. `Invalid set index 'rect_size' (on base: 'Control') with value of type 'Vector2'.`

- **原因**：同第 4 条，只是"赋值"场景。
- **改法**：用 `size = ...` 代替 `rect_size = ...`。注意 `size` 是 Control 的属性，赋值合法。

### 6. `Identifier "onready" expects a statement.` / `Parse Error: Unexpected "onready"`

- **原因**：`onready` 不再是关键字，是注解。
- **改法**：改成 `@onready`。

### 7. `Parse Error: Expected expression after "@export".` 或 `Export variables must have a type or a setter.`

- **原因**：`@export var x = 5` 没有类型，引擎无法导出。
- **改法**：写成 `@export var x: int = 5`，或 `@export var x := 5`（能推断出类型），或给它加 set/get。

### 8. `Identifier "PoolStringArray" not declared in the current scope.`

- **原因**：Pool 类型全部改名。
- **改法**：`PoolStringArray→PackedStringArray`、`PoolByteArray→PackedByteArray`、`PoolIntArray→PackedInt32Array`、`PoolRealArray→PackedFloat32Array`、`PoolVector2Array→PackedVector2Array`、`PoolVector3Array→PackedVector3Array`。

### 9. `Invalid call. Nonexistent function 'empty' in base 'Array'.`

- **原因**：`empty()` 改名 `is_empty()`。
- **改法**：数组、字典、字符串统一改成 `.is_empty()`。

### 10. `Invalid call. Nonexistent function 'rand_range' in base 'GDScriptNativeClass'.`

- **原因**：`rand_range` 拆成整型/浮点两个函数。
- **改法**：浮点用 `randf_range(a, b)`，整型用 `randi_range(a, b)`。

### 11. `Invalid call. Nonexistent function 'get_ticks_msec' in base 'OS'.`

- **原因**：时间函数从 `OS` 移到 `Time`。
- **改法**：`OS.get_ticks_msec()→Time.get_ticks_msec()`，`OS.get_unix_time()→Time.get_unix_time_from_system()`。

### 12. `Invalid call. Nonexistent function 'set_window_fullscreen' in base 'OS'.`

- **原因**：窗口函数移到 `DisplayServer`。
- **改法**：

```gdscript
DisplayServer.window_set_mode(DisplayServer.WINDOW_MODE_FULLSCREEN)
# 退出全屏：
DisplayServer.window_set_mode(DisplayServer.WINDOW_MODE_WINDOWED)
# 查询：
var is_full := DisplayServer.window_get_mode() == DisplayServer.WINDOW_MODE_FULLSCREEN
```

### 13. `Invalid get index 'editor_hint' (on base: 'Engine').`

- **原因**：`editor_hint` 从属性改为方法。
- **改法**：`Engine.editor_hint → Engine.is_editor_hint()`。

### 14. 打开项目时提示 `This project was made with Godot 3, its "format" is 2, expected 3.`

- **原因**：`.tscn` / `.tres` 的文件格式版本过旧。
- **改法**：不要手改文本！用官方转换工具（38.7），或**在 Godot 4 编辑器里打开每个场景并 Ctrl+S 重存**，引擎会自动写成 `format=3`。

### 15. `Too few arguments for "move_and_slide()" call. Expected at least 1 but received 0.`（3.x 的写法反过来）

- **原因**：你还在用 3.x 的 `move_and_slide(velocity, Vector2.UP)`。
- **改法**：`CharacterBody2D` 的 `velocity` 是**属性**，先赋值再调用无参 `move_and_slide()`：

```gdscript
velocity = input_dir * speed
move_and_slide()
```

### 16. `Invalid call. Nonexistent function 'playback_speed'...`

- **原因**：`AnimationPlayer` 属性改名。
- **改法**：`playback_speed → speed_scale`。

### 17. `Parse Error: The method "setget" is not declared.`

- **原因**：`setget` 关键字被移除。
- **改法**：改成 4.x 的属性语法（见 38.2.5）。

### 18. `Invalid call. Nonexistent function 'change_scene' in base 'SceneTree'.`

- **原因**：切场景方法改名。
- **改法**：`change_scene("res://x.tscn") → change_scene_to_file("res://x.tscn")`；如果传的是 `PackedScene`，用 `change_scene_to_packed(packed)`。

---

## 38.7 自动迁移工具：能做什么、不能做什么

### 38.7.1 官方转换器

Godot 4 自带了 **3→4 项目转换器**。最可靠的方式是命令行（无界面）：

```bash
# 在 Godot 4 的可执行文件目录下
godot --headless --path /path/to/godot3_project --convert-3to4
```

或者用**项目管理器**：打开 Godot 4 的项目管理器，通过"导入"选择 3.x 的 `project.godot`，部分版本会提供"转换/升级"入口。（不同 4.x 小版本 UI 位置略有差异，以你使用的版本为准。）

> 也可以先用外部社区工具（如 `gdscript-transpiler`、`godot-3-to-4-converter`、`Godot 4 Converter` 等）做一轮批量替换，再用官方转换器兜底。**不要在没备份的项目上直接跑转换器**。

### 38.7.2 转换器**能**改的

- 节点类改名（`Spatial→Node3D`、`KinematicBody2D→CharacterBody2D` 等）；
- 大部分属性/方法改名（`rect_position→position`、`instance→instantiate`）；
- 关键字替换（`onready→@onready`、`export→@export`、`yield→await` 的基础形态）；
- Pool 类型改名；
- `.tscn` / `.tres` 的 `format` 升级。

### 38.7.3 转换器**改不了 / 改不干净**的（必须手工）

- `move_and_slide()` 的参数语义变化（速度变成属性，需要重排逻辑）；
- Tween 的整体重构（节点式 → `create_tween()`）；
- `connect()` 的 Callable 化（尤其带 binds 的复杂连接）；
- `setget` → 属性语法的语义转换；
- 自定义 `class_name` 冲突、循环依赖；
- 3.x 专有插件（没有 4.x 版就无解）；
- Shader 代码（`shader_type`、内置变量名大改）；
- 材质、光照、环境、粒子系统的具体参数；
- 输入映射（`InputMap`）格式变更；
- 物理层/掩码语义微调；
- 动画（`AnimationTree` 节点路径、`NodePath` 变化）。

### 38.7.4 迁移后必须手工检查的 Checklist（12+ 项）

> 打印出来，迁移后逐项打勾。跳过任何一项，都可能埋雷。

- [ ] **1. 备份**：迁移前把项目完整复制一份，用 Git 打 tag（`git tag pre-4-migration`）。
- [ ] **2. 转换器输出**：完整读一遍转换器打印的 warning/error 列表，别只看最后一行。
- [ ] **3. 脚本静态检查**：每个 `.gd` 文件保存一次，确认编辑器底部无红色解析错误。
- [ ] **4. 场景重存**：逐个打开 `.tscn`，确认根节点类型正确、无"missing node"提示，然后 Ctrl+S。
- [ ] **5. 资源重存**：材质、主题、字体、动画等 `.tres` 逐个打开重存，让格式升到 3。
- [ ] **6. 输入映射**：进"项目设置 → 输入映射"，确认所有 action 仍然存在、键位没丢。
- [ ] **7. 信号连接**：运行前检查所有 `connect()` 是否改成 Callable；运行后看"调试器 → 信号"有无断连报错。
- [ ] **8. 物理行为**：`CharacterBody2D/3D` 的手感是否变化（移动、跳跃、贴墙）；刚体的 `freeze` 逻辑是否正确。
- [ ] **9. Tween / 动画**：所有补间动画是否正常播放、不再依赖已删除的 Tween 节点。
- [ ] **10. UI 布局**：所有 Control 的位置/尺寸是否正确（`rect_*` → `size`/`position` 后常出现错位），锚点与容器是否崩坏。
- [ ] **11. Shader 编译**：有自定义 shader 的项目，确认 `shader_type` 与内置变量已更新、无编译报错。
- [ ] **12. 音频**：`AudioStreamSample` 等资源是否正常播放（可能有重新导入）。
- [ ] **13. 存档兼容**：旧存档是否能读、路径是否仍是 `user://`、JSON 结构是否一致。
- [ ] **14. 性能**：用 Profiler 对比迁移前后帧率，确认没有因渲染后端变化而退化。
- [ ] **15. 导出预设**：导出模板、平台设置是否还在（`export_presets.cfg` 常需要重建）。
- [ ] **16. 第三方插件**：所有 `addons/` 下的插件是否已升级到 4.x 版本，失效的先禁用。

---

## 38.8 迁移实战：把一个 3.x 玩家脚本改成 4.x

这是本章的压轴。我们拿一个**典型的 Godot 3.x 2D 平台跳跃玩家脚本**，逐步翻译。请你跟着一步步改，体会"为什么每一处要改"。

### 38.8.1 迁移前：完整的 Godot 3.x 版本

**场景结构（3.x）**：

```text
Player (KinematicBody2D)
├── Sprite (Sprite2D 的 3.x 名字)
└── Hitbox (Area2D)
    └── CollisionShape2D
```

**脚本 `player.gd`（Godot 3.x）**：

```gdscript
# ===== Godot 3.x 版本 =====
extends KinematicBody2D

export(int) var speed = 300
export(int) var jump_force = -450
export(int) var max_hp = 100

var hp = max_hp
var velocity = Vector2.ZERO
var gravity = 900
var is_dead = false

onready var sprite = $Sprite
onready var hitbox = $Hitbox

signal hp_changed(new_hp)
signal died

func _ready():
    hitbox.connect("body_entered", self, "_on_hitbox_body_entered")
    emit_signal("hp_changed", hp)

func _physics_process(delta):
    velocity.y += gravity * delta

    var dir = 0
    if Input.is_action_pressed("ui_right"):
        dir += 1
    if Input.is_action_pressed("ui_left"):
        dir -= 1
    velocity.x = dir * speed

    if Input.is_action_just_pressed("ui_up") and is_on_floor():
        velocity.y = jump_force

    velocity = move_and_slide(velocity, Vector2.UP)

    if velocity.x != 0:
        sprite.flip_h = velocity.x < 0

func take_damage(amount):
    if is_dead:
        return
    hp -= amount
    emit_signal("hp_changed", hp)
    if hp <= 0:
        die()

func die():
    is_dead = true
    emit_signal("died")
    yield(get_tree().create_timer(1.0), "timeout")
    queue_free()

func _on_hitbox_body_entered(body):
    if body.has_method("take_damage"):
        body.take_damage(10)
```

### 38.8.2 逐步改写

**第 1 步：场景根节点类型**

- **改什么**：`extends KinematicBody2D` → `extends CharacterBody2D`。
- **为什么**：Godot 4 里 2D 角色物理体改名。`move_and_slide` 家族、`is_on_floor()` 都搬到了 `CharacterBody2D`。
- **同时**：编辑器里场景根的节点类型也要从 `KinematicBody2D` 换成 `CharacterBody2D`（转换器通常会帮你改）。

```gdscript
extends CharacterBody2D
```

**第 2 步：导出变量加注解与类型**

- **改什么**：`export(int) var speed = 300` → `@export var speed: int = 300`。
- **为什么**：`export(类型)` 语法废弃；4.x 用 `@export` 注解 + 类型标注。三个导出变量都改。

```gdscript
@export var speed: int = 300
@export var jump_force: int = -450
@export var max_hp: int = 100
```

**第 3 步：普通变量加类型（可选但推荐）**

- **改什么**：给 `hp`、`gravity`、`is_dead` 加类型标注。
- **为什么**：4.x 鼓励静态类型，能提前发现类型错误，也不影响性能。

```gdscript
var hp: int = max_hp
var gravity: int = 900
var is_dead: bool = false
```

**第 4 步：`onready` → `@onready`，并修正节点名**

- **改什么**：

```gdscript
@onready var sprite: Sprite2D = $Sprite2D
@onready var hitbox: Area2D = $Hitbox
```

- **为什么**：
  1. `onready` 关键字变成 `@onready` 注解；
  2. `Sprite` 节点在 4.x 里叫 `Sprite2D`，所以 `$Sprite` 要改成 `$Sprite2D`（**别忘了在场景里也重命名节点**）；
  3. 顺手加上类型标注，编辑器能给 `sprite.flip_h` 补全。

**第 5 步：信号声明加类型 + 连接方式改造**

- **改什么**：

```gdscript
signal hp_changed(new_hp: int)
signal died
```

- **为什么**：4.x 信号参数可带类型；`_ready()` 里的连接要改：

```gdscript
func _ready() -> void:
    hitbox.body_entered.connect(_on_hitbox_body_entered)
    hp_changed.emit(hp)
```

- **为什么**：`hitbox.connect("body_entered", self, "_on_hitbox_body_entered")` 里的"对象 + 字符串"三参形式废弃，直接用 `信号.connect(Callable)`；`emit_signal("hp_changed", hp)` 推荐改成 `hp_changed.emit(hp)`。

**第 6 步：物理移动逻辑（最关键的一步）**

- **改什么**：

```gdscript
    velocity.x = dir * speed
    if Input.is_action_just_pressed("ui_up") and is_on_floor():
        velocity.y = jump_force
    move_and_slide()
```

- **为什么**：3.x 的 `move_and_slide(velocity, up_direction)` 里，速度是**参数**、方向是**第二参**；4.x 里 `velocity` 是 `CharacterBody2D` 的**内置属性**，`move_and_slide()` **无参**调用，`up_direction` 变成了节点属性（在检查器里设置，默认 `(0, -1)`）。
- 注意：**`move_and_slide()` 不再有返回值**，它直接更新 `velocity` 属性。所以旧代码里 `velocity = move_and_slide(...)` 会报错——必须改成先赋值 `velocity`，再调用 `move_and_slide()`。

**第 7 步：`yield` → `await`**

- **改什么**：

```gdscript
func die() -> void:
    is_dead = true
    died.emit()
    await get_tree().create_timer(1.0).timeout
    queue_free()
```

- **为什么**：`yield(get_tree().create_timer(1.0), "timeout")` → `await get_tree().create_timer(1.0).timeout`。`await` 是关键字，等待的是"信号"（这里 `timeout` 是 `SceneTreeTimer` 的信号）。

**第 8 步：函数签名加返回类型（推荐）**

- **改什么**：给所有无返回值函数加 `-> void`，参数加类型。
- **为什么**：4.x 风格，静态检查更严，也便于阅读。

```gdscript
func _physics_process(delta: float) -> void:
func take_damage(amount: int) -> void:
func _on_hitbox_body_entered(body: Node2D) -> void:
```

### 38.8.3 迁移后：完整的 Godot 4.x 版本

**场景结构（4.x）**：

```text
Player (CharacterBody2D)
├── Sprite2D
└── Hitbox (Area2D)
    └── CollisionShape2D
```

**脚本 `player.gd`（Godot 4.x）**：

```gdscript
# ===== Godot 4.x 版本 =====
extends CharacterBody2D

@export var speed: int = 300
@export var jump_force: int = -450
@export var max_hp: int = 100

var hp: int = max_hp
var gravity: int = 900
var is_dead: bool = false

signal hp_changed(new_hp: int)
signal died

@onready var sprite: Sprite2D = $Sprite2D
@onready var hitbox: Area2D = $Hitbox

func _ready() -> void:
    hitbox.body_entered.connect(_on_hitbox_body_entered)
    hp_changed.emit(hp)

func _physics_process(delta: float) -> void:
    # 重力（velocity 是 CharacterBody2D 的内置属性）
    velocity.y += gravity * delta

    var dir := 0
    if Input.is_action_pressed("ui_right"):
        dir += 1
    if Input.is_action_pressed("ui_left"):
        dir -= 1
    velocity.x = dir * speed

    if Input.is_action_just_pressed("ui_up") and is_on_floor():
        velocity.y = jump_force

    # 无参调用；速度已在 velocity 属性里
    move_and_slide()

    if velocity.x != 0:
        sprite.flip_h = velocity.x < 0

func take_damage(amount: int) -> void:
    if is_dead:
        return
    hp -= amount
    hp_changed.emit(hp)
    if hp <= 0:
        die()

func die() -> void:
    is_dead = true
    died.emit()
    await get_tree().create_timer(1.0).timeout
    queue_free()

func _on_hitbox_body_entered(body: Node2D) -> void:
    if body.has_method("take_damage"):
        body.take_damage(10)
```

### 38.8.4 迁移前后逐项对照

| 位置 | 3.x | 4.x | 类别 |
| --- | --- | --- | --- |
| 根类型 | `KinematicBody2D` | `CharacterBody2D` | 节点改名 |
| 导出 | `export(int) var speed = 300` | `@export var speed: int = 300` | 注解 + 类型 |
| 引用 | `onready var sprite = $Sprite` | `@onready var sprite: Sprite2D = $Sprite2D` | 注解 + 节点名 |
| 连接 | `hitbox.connect("body_entered", self, "_on_...")` | `hitbox.body_entered.connect(_on_...)` | Callable |
| 发射 | `emit_signal("hp_changed", hp)` | `hp_changed.emit(hp)` | 信号 |
| 移动 | `velocity = move_and_slide(velocity, Vector2.UP)` | `velocity = ...; move_and_slide()` | 物理 API |
| 等待 | `yield(..., "timeout")` | `await ....timeout` | 异步 |
| 类型 | 全无 | 变量/参数/返回值均有 | 风格 |

> 恭喜，一个完整的 3.x 角色脚本迁移完毕。你会发现：**真正"伤筋动骨"的只有第 6 步（物理）和第 7 步（异步）**，其余都是"改名字 + 加 `@`"。这就是为什么要先理解原理，再动手。

---

## 38.9 本章小结

- **Godot 3 → 4 是破坏性升级**：渲染换 Vulkan、脚本升 GDScript 2.0、节点大改名。不要指望"一键迁移"。
- **两大策略**：小项目"整体升级"（转换器 + 手改），大项目"重写核心"（保留美术、重写逻辑）。
- **语法六大变化**：`@export` / `@onready` 注解、Callable 连接、`setget`→属性、`yield`→`await`、Pool→Packed、类型标注普及。
- **节点改名规律**：3D 补 `3D`、2D 补 `2D`、服务类改名、被合并的改成"属性开关"。
- **最容易踩的坑**：`move_and_slide` 的速度变属性、`rect_*` 属性改名、Tween 整体重构、`connect` 的 Callable 化。
- **迁移铁律**：先备份 → 跑转换器 → 读警告 → 逐场景重存 → 按 16 项 checklist 体检 → 手工验证手感。

到这里，你已经把整本书的语法、工程、模板、项目、排错、迁移全部走完了。接下来是五个附录：**术语表**（随时回查概念）、**学习路线图**（怎么把学到的东西排成计划）、**全书索引**（想找哪个知识点翻哪章）、**实战番外**（把知识用到真实项目上，基础篇）、**纯手机学习方案**（只有手机也能学完这本书）。

---

# 附录 A：术语表

> 收录 100+ 个术语，**中英对照 + 一句话解释**，按类别排列。遇到看不懂的词，先来这里查。

## A.1 语言基础类

| 术语（English） | 一句话解释 |
| --- | --- |
| 变量（Variable） | 一块可改名的内存，用来存放会变化的数据。 |
| 常量（Constant） | 用 `const` 声明、程序运行期间不可重新赋值的值。 |
| 作用域（Scope） | 一个名字能被"看见"和使用的范围，如函数内、类内。 |
| 字面量（Literal） | 直接写死在代码里的值，如 `42`、`"hi"`、`true`。 |
| 表达式（Expression） | 能计算出一个值的代码片段，如 `a + b * 2`。 |
| 语句（Statement） | 一条会执行动作的完整指令，如赋值、`if`、函数调用。 |
| 运算符（Operator） | 对操作数做运算的符号，如 `+`、`==`、`&&`（GDScript 用 `and`）。 |
| 操作数（Operand） | 运算符作用的对象，如 `3 + 5` 里的 `3` 和 `5`。 |
| 类型推断（Type Inference） | 由编译器根据初始值猜出变量类型，GDScript 用 `:=`。 |
| 类型标注（Type Annotation） | 显式写明类型，如 `var hp: int = 100`。 |
| 强类型（Strong Typing） | 类型不匹配就报错，不允许悄悄乱转。 |
| 静态类型（Static Typing） | 类型在编译/解析期确定，GDScript 4 支持可选静态类型。 |
| 动态类型（Dynamic Typing） | 类型在运行时才确定，GDScript 默认可动态。 |
| 装箱 / 拆箱（Boxing / Unboxing） | 值类型与对象类型之间来回包装，GDScript 里多体现为 Variant 转换。 |
| 引用类型（Reference Type） | 赋值时只复制"指针"，改一个另一个也变，如 Array/Dictionary/Object。 |
| 值类型（Value Type） | 赋值时复制整份数据，改一个不影响另一个，如 int/Vector2。 |
| 浅拷贝（Shallow Copy） | 只复制一层，内部引用仍共享。 |
| 深拷贝（Deep Copy） | 递归复制所有层级，彼此完全独立（`duplicate(true)`）。 |
| 空值（Null / Nil） | 表示"什么都没有"，访问它的成员会报 `Nil` 错误。 |
| 布尔（bool） | 只有 `true` / `false` 两种值。 |
| 整数（int） | 64 位整数，GDScript 里统一是 `int`。 |
| 浮点数（float） | 小数，GDScript 里统一是 64 位 `float`。 |
| 字符串（String） | 一串文本，不可变（改的是新字符串）。 |
| 数组（Array） | 有序的元素集合，可增删、可混合类型。 |
| 字典（Dictionary） | 键值对集合，用键快速取值。 |
| 枚举（enum） | 给一组整数起名字，如 `{ IDLE, RUN, JUMP }`。 |
| 注释（Comment） | 用 `#` 开头、不参与执行的说明文字。 |
| 转义字符（Escape Sequence） | 字符串里的 `\n`、`\t` 等特殊字符。 |
| 三元表达式（Ternary） | `a if cond else b` 的简写条件取值。 |

## A.2 面向对象类

| 术语（English） | 一句话解释 |
| --- | --- |
| 类（Class） | 描述一类对象的"蓝图"，定义属性与方法。 |
| 对象（Object） | 由类创建出来的具体实例。 |
| 实例（Instance） | 同"对象"，强调"由某类生成的一份"。 |
| 继承（Inheritance） | 子类复用并扩展父类的成员，用 `extends`。 |
| 多态（Polymorphism） | 同一个方法在不同子类里有不同表现。 |
| 封装（Encapsulation） | 把数据与操作打包，外界只通过接口访问。 |
| 重载（Overload） | 同名但参数不同的多个方法（GDScript 不直接支持，需变通）。 |
| 重写（Override） | 子类重新实现父类的方法，如 `_ready()`。 |
| 抽象类（Abstract Class） | 只作基类、不直接实例化的类（GDScript 无 `abstract` 关键字，靠约定）。 |
| 接口（Interface） | 定义"必须实现哪些方法"的契约；GDScript 没有接口，用 `has_method()` 或基类替代。 |
| 内部类（Inner Class） | 定义在另一个类内部的类。 |
| 静态成员（Static Member） | 属于类本身、不属于实例的变量或方法。 |
| 构造函数（Constructor） | 创建对象时执行的初始化函数，GDScript 用 `_init()`。 |
| 析构函数（Destructor） | 对象销毁时执行的清理函数，GDScript 靠 `_notification(NOTIFICATION_PREDELETE)` 或引用计数。 |
| 闭包（Closure） | 能记住并使用定义时外部变量的函数。 |
| Lambda（匿名函数） | 没有名字、可当值传递的函数，GDScript 用 `func():`。 |
| 回调（Callback） | 被"传进去、等事情发生时再调用"的函数。 |
| 委托（Delegate） | 把某项职责转交给另一个对象处理。 |
| 单例（Singleton） | 全局唯一、全局可访问的实例，Godot 里是 Autoload。 |
| 依赖注入（Dependency Injection） | 由外部把依赖塞进对象，而不是对象自己 new。 |
| 服务定位器（Service Locator） | 通过一个"全局注册表"按名字取服务。 |
| 工厂（Factory） | 负责集中创建对象的类/函数，隐藏创建细节。 |
| 对象池（Object Pool） | 预先创建一批对象循环复用，避免频繁创建销毁。 |
| 状态机（State Machine） | 把对象行为拆成"状态 + 转移"，任一时刻只处于一个状态。 |
| 组件（Component） | 把功能拆成可自由拼装的小模块。 |
| 观察者模式（Observer Pattern） | 一个对象状态变了，自动通知所有订阅者；Godot 信号即此模式。 |
| 事件总线（Event Bus） | 全局的信号中转站，用于解耦模块间通信。 |

## A.3 脚本 / 引擎类

| 术语（English） | 一句话解释 |
| --- | --- |
| 脚本（Script） | 附在节点/资源上的代码文件（`.gd`）。 |
| 场景（Scene） | 一棵可复用、可实例化的节点树（`.tscn`）。 |
| 节点（Node） | 场景树里的基本单元，承担某个功能。 |
| 场景树（Scene Tree） | 所有活动节点的树状结构，由 `SceneTree` 管理。 |
| 生命周期（Lifecycle） | 节点从进入树到离开树的一系列回调，如 `_ready`、`_process`。 |
| 帧（Frame） | 一次完整的渲染循环。 |
| 帧率（FPS） | 每秒渲染多少帧。 |
| Delta（帧间隔） | 两帧之间经过的秒数，用于让逻辑与帧率无关。 |
| 物理帧（Physics Tick） | 固定步长的物理计算时刻，`_physics_process` 在此调用。 |
| 插值（Interpolation） | 在两点之间按比例求中间值。 |
| 缓动（Easing） | 让速度有加减速曲线，如 `EASE_IN_OUT`。 |
| 补间（Tween） | 自动在一段时间内平滑改变属性。 |
| 资源（Resource） | 可被多场景共享的数据对象，如材质、纹理、音频。 |
| 打包资源（PackedScene） | 序列化后的场景文件，可 `instantiate()` 出节点。 |
| 导入（Import） | 把外部文件（png/wav/obj）转成引擎内部资源。 |
| 重导出（Reimport） | 源文件变了，重新执行导入流程。 |
| UUID / 哈希（UUID / Hash） | 唯一标识一串数据；`uuid://` 用于稳定引用资源。 |
| 序列化（Serialization） | 把内存对象变成可存储/传输的字节或文本。 |
| 反序列化（Deserialization） | 把存储/传输的数据还原成内存对象。 |
| 元数据（Metadata） | 附加在对象上的额外信息，用 `set_meta`/`get_meta`。 |
| 反射（Reflection） | 运行时查询"这个对象有什么方法/属性"。 |
| 注解（Annotation） | 以 `@` 开头的特殊标记，如 `@export`、`@tool`。 |
| 信号（Signal） | 节点发出的"事情发生了"的通知。 |
| 槽（Slot） | 接收信号并执行的函数（回调）。 |
| 协程（Coroutine） | 可暂停、可恢复执行的函数，用 `await`。 |
| 异步（Async） | 不阻塞主流程、稍后完成的操作。 |

## A.4 渲染 / 图形类

| 术语（English） | 一句话解释 |
| --- | --- |
| 着色器（Shader） | 运行在 GPU 上、决定像素/顶点如何绘制的小程序。 |
| 材质（Material） | 给几何体"贴"上外观的资源配置，如 `StandardMaterial3D`。 |
| 画布（Canvas） | 2D 绘制用的抽象平面，`CanvasItem` 都在画布上。 |
| 视口（Viewport） | 一个"渲染窗口/输出目标"，相机看到的世界渲染到这里。 |
| 相机（Camera） | 决定从哪个视角观察世界。 |
| 光栅化（Rasterization） | 把矢量几何转成一个个像素的过程。 |
| 批处理（Batching） | 把多个绘制合并成一次提交，减少开销。 |
| 绘制调用（Draw Call） | CPU 命令 GPU"画一次"的开销单位，越少越好。 |
| 精灵（Sprite） | 带贴图的 2D 图像节点。 |
| 精灵表（Sprite Sheet） | 把多张图拼在一张图上，减少 I/O。 |
| 图集（Atlas） | 同"精灵表"，也指纹理打包。 |
| 瓦片地图（TileMap） | 用格子拼出关卡的 2D 地图系统。 |
| 粒子（Particles） | 大量小图元组成的特效，如火花、烟雾。 |
| 后处理（Post-processing） | 画面渲染完成后叠加的滤镜效果。 |
| 全局光照（GI） | 模拟光线在场景中多次反弹的照明。 |
| 顶点（Vertex） | 几何体的角点。 |
| 法线（Normal） | 表面朝向，用于光照计算。 |
| 纹理 / 贴图（Texture） | 贴到表面上的图片数据。 |
| 锚点（Anchor） | Control 相对父容器定位的参考点。 |
| 容器（Container） | 自动排列子 Control 的布局节点。 |
| 布局（Layout） | 控件的位置与尺寸安排方式。 |
| 主题（Theme） | 统一管理一组控件外观的资源。 |
| 字体（Font） | 文字渲染所用的字形数据。 |
| DPI | 每英寸点数，影响 UI 在不同屏幕上的缩放。 |
| 渲染后端（Rendering Backend） | 引擎使用的图形 API，如 Vulkan、OpenGL。 |

## A.5 物理 / 游戏开发通用类

| 术语（English） | 一句话解释 |
| --- | --- |
| AABB | 轴对齐包围盒，用于快速碰撞剔除。 |
| 碰撞体（Collider） | 参与碰撞检测的形状，如 `CollisionShape2D`。 |
| 触发区（Trigger Area） | 只检测"进出"、不产生物理反弹的区域（`Area2D/3D`）。 |
| 碰撞层（Collision Layer） | 我"属于"哪些层。 |
| 碰撞掩码（Collision Mask） | 我"检测"哪些层。 |
| 遮罩（Mask） | 用来限定影响范围的图或位掩码。 |
| 刚体（RigidBody） | 完全由物理引擎驱动的物体。 |
| 角色体（CharacterBody） | 由代码控制移动、但仍做碰撞的物体。 |
| 静态体（StaticBody） | 不动的碰撞体，如地面、墙。 |
| 射线检测（Raycast） | 从一点沿方向"射一条线"，检测撞到什么。 |
| 调试器（Debugger） | 运行时查看变量、断点、调用栈的工具。 |
| 断点（Breakpoint） | 让程序执行到某行时暂停，方便观察。 |
| 堆栈（Stack Trace） | 函数调用的层层记录，报错时用来定位源头。 |
| 性能剖析（Profiler） | 统计各函数耗时/内存，找瓶颈。 |
| 内存泄漏（Memory Leak） | 该释放的对象一直没释放，占用越来越多内存。 |
| 悬空引用（Dangling Reference） | 对象已销毁，但还有变量指向它。 |
| 竞态（Race Condition） | 多个操作顺序不确定，导致结果不稳定。 |
| 防抖（Debounce） | 事件触发后等一段时间再执行，期间重复触发则重置。 |
| 节流（Throttle） | 限制某操作在单位时间内最多执行一次。 |
| 手感（Game Feel） | 操作回馈是否"跟手、爽快"的整体感受。 |
| 打击感（Hit Feel） | 攻击命中时的视觉/音效/震动综合反馈。 |
| 顿帧（Hit Stop / Freeze Frame） | 命中瞬间短暂"卡住"画面，增强打击感。 |
| 屏幕震动（Screen Shake） | 相机短促抖动，增强冲击力。 |
| 存档（Save Data） | 保存玩家进度的数据文件。 |
| 配置（Config） | 保存设置的键值数据，如音量、分辨率。 |
| 回调函数（Callback Function） | 见"回调"。 |
| 协程（Coroutine） | 见"协程"。 |
| 帧同步（Frame Sync） | 网络游戏中按帧对齐各端状态。 |
| 对象池（Object Pool） | 见"对象池"。 |
| 本地化（Localization） | 让游戏支持多语言。 |
| 自动加载（Autoload） | 项目启动时自动挂到根节点的全局单例。 |

---

# 附录 B：学习路线图

> 这本书很厚。**别从头到尾硬啃**——下面给你三条路线，照着走效率最高。

## B.1 零基础读者路线（8 周）

假设你完全没写过代码，每周投入 6～8 小时。

| 周 | 读哪些章 | 做什么练习 | 目标 |
| --- | --- | --- | --- |
| 第 1 周 | 第 1～5 章（引擎初识、变量、类型、运算符、流程控制） | 写一个"猜数字"控制台脚本（`print` 输出） | 能读懂并写出简单逻辑 |
| 第 2 周 | 第 6～10 章（函数、数组、字典、字符串、枚举） | 做一个"通讯录"：用数组存名字，用字典存信息，能增删查 | 掌握数据组织方式 |
| 第 3 周 | 第 11～16 章（类、继承、静态、内部类、构造、注解） | 写一个 `Character` 基类 + 两个子类，练习继承与重写 | 理解面向对象 |
| 第 4 周 | 第 17～20 章（节点、生命周期、信号、节点引用） | 做一个会移动的方块，`_process` 里读输入、发自定义信号 | 让脚本"动起来" |
| 第 5 周 | 第 21～24 章（资源、输入、数学向量、Tween） | 用 Tween 做一个按钮淡入淡出、用向量做一个跟随鼠标的小球 | 掌握引擎交互 |
| 第 6 周 | 第 25～29 章（异步、文件 JSON、存档、调试、性能） | 给第 4 周的方块加存档：退出保存位置，启动读回 | 能持久化数据 |
| 第 7 周 | 第 30～34 章（对象池 + 26 个模板选读） | 挑 T08 玩家控制器、T11 血量系统、T15 主菜单 三个模板亲手敲一遍 | 学会用模板搭系统 |
| 第 8 周 | 第 35 章（综合项目）+ 第 36～37 章（速查、报错） | 独立完成第 35 章的完整小项目；遇到报错查第 37 章 | 做出第一个完整作品 |

> 完成后你就能独立做小游戏了。第 38 章和附录可以随时当工具书查。

## B.2 有编程基础读者路线（2～3 周速通）

如果你已经会 Python / JS / C#，可以**跳过纯语法基础**，重点放在"Godot 特有点"。

**可以快速扫过（1 小时/章，看示例即可）**：
- 第 2～6 章：变量、类型、运算符、流程、函数（几乎与主流语言一致，注意 `:=`、`var x: int`、`match` 语法即可）。
- 第 11～15 章：类与继承（注意 GDScript 用 `extends`、`_init`）。

**必须精读（2～4 小时/章，动手敲）**：

| 章节 | 为什么必读 |
| --- | --- |
| 第 17～20 章（节点/生命周期/信号/引用） | Godot 的核心范式，和普通语言菜谱完全不同 |
| 第 21 章（资源） | Godot 资源共享与内存管理的核心 |
| 第 23～25 章（向量/Tween/异步） | 游戏逻辑的日常，`await` 与主流语言差异大 |
| 第 26～27 章（文件 JSON / 存档） | 工程必备 |
| 第 31～34 章（模板） | 直接给你可复用的架构，别重复造轮子 |
| 第 38 章（迁移） | 你手里的老资料十有八九是 3.x 的 |

**建议顺序**：17→18→19→20→21→23→24→25→26→31～34→35→38。

## B.3 各卷难度与前置关系图

```text
┌──────────────────────────────────────────────────┐
│ 第 1 卷 · 语法地基（1-16 章）    难度：★☆☆☆☆     │
│ 变量/类型/流程/函数/容器/OOP     前置：无        │
└─────────────────────────┬────────────────────────┘
                          ▼
┌──────────────────────────────────────────────────┐
│ 第 2 卷 · 引擎交互（17-30 章）   难度：★★★☆☆     │
│ 节点/信号/资源/输入/数学/异步    前置：第1卷     │
└─────────────────────────┬────────────────────────┘
                          ▼
┌──────────────────────────────────────────────────┐
│ 第 3 卷 · 模板库（31-34 章）     难度：★★★☆☆     │
│ 26 个即插即用模板                前置：第2卷     │
├──────────────────────────────────────────────────┤
│ 第 4 卷 · 综合项目（35 章）      难度：★★★★☆     │
│ 一步一步做出完整小游戏           前置：2、3卷    │
├──────────────────────────────────────────────────┤
│ 第 5 卷 · 工具手册（36-37 章）   难度：★★☆☆☆     │
│ 速查表 / 报错词典                前置：全程可用  │
└─────────────────────────┬────────────────────────┘
                          ▼
┌──────────────────────────────────────────────────┐
│ 第 6 卷 · 附录与迁移             难度：★★★☆☆     │
│ Godot 3→4 迁移 + 术语/路线/索引  前置：建议全读  │
└──────────────────────────────────────────────────┘
```

**阅读建议**：
- 第 1 卷是地基，**别跳**（尤其类型系统）。
- 第 2 卷是核心，**必须动手**。
- 第 3 卷是"积木库"，用时现查。
- 第 4 卷是"体检"，检验你是否真学会了。
- 第 5 卷是"字典"，常备。

## B.4 每卷配套练习建议

| 卷 | 检验你是否真学会的"作品" |
| --- | --- |
| 第 1 卷 | 一个纯脚本小工具：命令行"学生成绩管理"（增删改查 + 排序 + 统计） |
| 第 2 卷 | 一个 2D 小场景：能用键盘移动的角色 + 一个会发光/淡出的 UI + 一份可存档的位置数据 |
| 第 3 卷 | 用模板搭一个"可运行的小游戏骨架"：主菜单 → 关卡 → 暂停 → 结算 → 返回菜单 |
| 第 4 卷 | 完整实现第 35 章项目，并**自己加 2 个它没做的功能** |
| 第 5 卷 | 不看答案，用第 36 章速查表默写出 20 个常用 API |
| 第 6 卷 | 找一个 GitHub 上的 Godot 3.x 小项目，完整迁移到 4.x 并跑通 |

## B.5 学完之后往哪走

本书覆盖的是 2D 为主的语法与引擎交互。想继续深入，按下面清单来，**并标注了本书中对应的基础章节**：

| 下一步主题 | 本书提供的基础 | 建议学习顺序 |
| --- | --- | --- |
| **3D 游戏开发** | 第 17 章节点、第 23 章向量（含 Vector3）、第 38.3 的 3D 节点改名 | 先啃 `Node3D`、`Camera3D`、光照、导入模型 |
| **自定义 Shader** | 第 21 章资源、附录 A.4 图形术语 | 学 `shader_type`、顶点/片元、内置变量 |
| **多人联机** | 第 19 章信号、第 25 章异步、第 38.4 的 `multiplayer_authority` | 学 `MultiplayerAPI`、`@rpc`、状态同步 |
| **导出与发布** | 第 26 章文件路径（`user://` 等） | 学导出预设、各平台打包、签名 |
| **编辑器插件 / 工具脚本** | 第 16 章注解（`@tool`）、第 21 章资源 | 学 `EditorPlugin`、`@tool` 脚本、自定义 Inspector |
| **游戏架构进阶** | 第 31～34 章全部模板 | 学 ECS、事件总线、服务定位器深化 |
| **美术与动画管线** | 第 24 章 Tween、第 9 章字符串 | 学 `AnimationTree`、骨骼动画、SpriteFrames |
| **性能优化专项** | 第 29 章性能、第 30 章对象池 | 学多线程、`WorkerThreadPool`、批处理优化 |
| **测试与 CI** | 第 37 章报错、第 26 章文件 | 学 GUT / GdUnit4 单元测试、命令行跑测试 |

> 附：**永远保持一个"在做的项目"**。看教程只是输入，做一个东西才是学习。哪怕它很烂。

---

# 附录 C：全书索引

## C.1 全书章节一览表

| 章号 | 标题 | 一句内容概括 | 所在卷 |
| --- | --- | --- | --- |
| 第 1 章 | 初识 Godot 4 与 GDScript | 安装引擎、认识编辑器、跑通第一个脚本 | 第 1 卷 |
| 第 2 章 | 变量与常量 | `var` / `const` / `@export` 的声明与命名规范 | 第 1 卷 |
| 第 3 章 | 数据类型与类型系统 | int/float/bool/String、类型标注、`:=` 推断 | 第 1 卷 |
| 第 4 章 | 运算符与表达式 | 算术、比较、逻辑、位运算、优先级 | 第 1 卷 |
| 第 5 章 | 流程控制 | `if` / `match` / `for` / `while` / `break` / `continue` | 第 1 卷 |
| 第 6 章 | 函数 | 参数、默认值、返回值、可变参数、静态类型函数 | 第 1 卷 |
| 第 7 章 | 数组 | 增删查改、排序、`Packed*Array`、遍历 | 第 1 卷 |
| 第 8 章 | 字典 | 键值对、嵌套、遍历、排序与合并 | 第 1 卷 |
| 第 9 章 | 字符串 | 拼接、格式化、查找替换、`%` 与 `format` | 第 1 卷 |
| 第 10 章 | 枚举 | `enum` 声明、取值、与字典/数组配合 | 第 1 卷 |
| 第 11 章 | 类与对象 | `class_name`、成员、实例化、`self` | 第 1 卷 |
| 第 12 章 | 继承 | `extends`、重写、`super`、多态 | 第 1 卷 |
| 第 13 章 | 静态成员 | `static var` / `static func` / 常量类成员 | 第 1 卷 |
| 第 14 章 | 内部类 | 嵌套类、命名空间技巧、工具类组织 | 第 1 卷 |
| 第 15 章 | 构造函数与对象初始化 | `_init`、参数传递、`new()` | 第 1 卷 |
| 第 16 章 | 注解与元数据 | `@export` 家族、`@onready`、`@tool`、`@warning_ignore` | 第 1 卷 |
| 第 17 章 | 节点基础 | 节点是什么、节点树、常用节点类型 | 第 2 卷 |
| 第 18 章 | 节点生命周期 | `_enter_tree` / `_ready` / `_process` / `_physics_process` | 第 2 卷 |
| 第 19 章 | 信号（Signal） | 声明、连接、发射、解耦通信 | 第 2 卷 |
| 第 20 章 | 节点引用 | `$` / `get_node` / `@onready` / `unique_name_in_owner` | 第 2 卷 |
| 第 21 章 | 资源（Resource） | 自定义资源、`preload`/`load`、共享与内存 | 第 2 卷 |
| 第 22 章 | 输入处理 | InputMap、`is_action_pressed`、鼠标/触摸 | 第 2 卷 |
| 第 23 章 | 数学与向量 | Vector2/3、插值、角度、随机数 | 第 2 卷 |
| 第 24 章 | Tween 补间动画 | `create_tween`、链式 API、缓动曲线 | 第 2 卷 |
| 第 25 章 | 异步与协程 | `await`、计时器、加载等待 | 第 2 卷 |
| 第 26 章 | 文件、目录与 JSON | `FileAccess` / `DirAccess` / `JSON` | 第 2 卷 |
| 第 27 章 | 存档与配置数据 | `user://`、序列化、`ConfigFile` | 第 2 卷 |
| 第 28 章 | 调试技巧 | 断点、`print` 家族、远程调试器 | 第 2 卷 |
| 第 29 章 | 性能优化 | Profiler、批处理、绘制调用、常见瓶颈 | 第 2 卷 |
| 第 30 章 | 内存与对象池 | 引用计数、`queue_free`、对象池模式 | 第 2 卷 |
| 第 31 章 | 模块模板（一）：基础系统 | T01～T07：管理器、场景切换、输入、计时、存档、设置、音效 | 第 3 卷 |
| 第 32 章 | 模块模板（二）：角色与战斗 | T08～T14：玩家、状态机、血量、AI、武器、拾取 | 第 3 卷 |
| 第 33 章 | 模块模板（三）：UI 与流程 | T15～T20：主菜单、HUD、对话、背包、暂停、关卡选择 | 第 3 卷 |
| 第 34 章 | 模块模板（四）：进阶系统 | T21～T26：相机、特效、震屏顿帧、存档加密、本地化、控制台 | 第 3 卷 |
| 第 35 章 | 综合小项目 | 从零搭建一个完整可玩的小游戏 | 第 4 卷 |
| 第 36 章 | 语法速查表 | 常用语法与 API 的一页纸速查 | 第 5 卷 |
| 第 37 章 | 报错词典 | 报错原文 → 原因 → 修复 的查询手册 | 第 5 卷 |
| 第 38 章 | Godot 3 → 4 迁移对照 | 差异、对照大表、迁移实战、自动工具 | 第 6 卷 |
| 附录 A | 术语表 | 100+ 术语中英对照与一句话解释 | 第 6 卷 |
| 附录 B | 学习路线图 | 零基础 / 有基础 / 进阶路线与练习 | 第 6 卷 |
| 附录 C | 全书索引 | 章节一览 + 关键词反查 + 模板索引 | 第 6 卷 |
| 附录 D | 把知识用到真实项目上（基础篇） | 读目录/常量/状态机/工具类/资源加载 + 第一处修改 + 8 个坑 | 第 6 卷 |
| 附录 E | 纯手机学习方案（逐章对照表） | 38 章「手机可做/需电脑」对照 + 无引擎推演法 + 4.3→4.7 提醒 | 第 6 卷 |

## C.2 按知识点反查索引

> 想找某个知识点，先来这里搜关键词。

| 关键词 | 对应章节 |
| --- | --- |
| 变量声明 | 第 2 章 |
| 常量 / `const` | 第 2、13 章 |
| 类型推断 / `:=` | 第 3 章 |
| 类型标注 | 第 3、6 章 |
| 类型转换 | 第 3 章 |
| 运算符优先级 | 第 4 章 |
| 位运算 | 第 4 章 |
| `if` / `elif` / `else` | 第 5 章 |
| `match` 模式匹配 | 第 5 章 |
| 循环 `for` / `while` | 第 5 章 |
| 函数定义 | 第 6 章 |
| 默认参数 / 可变参数 | 第 6 章 |
| lambda / 匿名函数 | 第 6、16 章 |
| 数组创建 | 第 7 章 |
| 数组排序 | 第 7 章 |
| 数组去重 / 过滤 | 第 7 章 |
| Packed 数组 | 第 7 章 |
| 字典增删查改 | 第 8 章 |
| 字典遍历 | 第 8 章 |
| 字典排序 | 第 8 章 |
| 字符串格式化 | 第 9 章 |
| 字符串查找替换 | 第 9 章 |
| 正则表达式 | 第 9 章 |
| 枚举 enum | 第 10 章 |
| 类 / `class_name` | 第 11 章 |
| 继承 / `extends` | 第 12 章 |
| 重写 / `super` | 第 12 章 |
| 多态 | 第 12 章 |
| 静态变量 / 静态函数 | 第 13 章 |
| 内部类 | 第 14 章 |
| 构造函数 `_init` | 第 15 章 |
| `@export` 导出变量 | 第 16、38 章 |
| `@onready` | 第 16、20、38 章 |
| `@tool` 工具脚本 | 第 16、21 章 |
| `@warning_ignore` | 第 16、37 章 |
| 节点树 | 第 17 章 |
| `_ready` / `_process` | 第 18 章 |
| 生命周期回调 | 第 18 章 |
| 信号声明 | 第 19 章 |
| 信号连接 | 第 19、38 章 |
| 信号发射 `.emit()` | 第 19、38 章 |
| 信号绑定参数 bind | 第 19、38 章 |
| `$` 节点路径 | 第 20 章 |
| `get_node_or_null` | 第 20、37 章 |
| 场景实例化 instantiate | 第 20、38 章 |
| 自定义资源 | 第 21 章 |
| `preload` / `load` | 第 21 章 |
| 资源循环依赖 | 第 21、37 章 |
| InputMap 输入映射 | 第 22、38 章 |
| 鼠标 / 触摸输入 | 第 22 章 |
| Vector2 / Vector3 | 第 23 章 |
| 向量归一化 | 第 23 章 |
| 角度与弧度 | 第 23 章 |
| 随机数 | 第 23、38 章 |
| Tween 补间 | 第 24、38 章 |
| 缓动曲线 easing | 第 24 章 |
| `await` 异步 | 第 25、38 章 |
| 计时器 Timer | 第 25 章 |
| FileAccess 文件读写 | 第 26、38 章 |
| DirAccess 目录 | 第 26、38 章 |
| JSON 解析 | 第 26 章 |
| CSV 读取 | 第 26 章 |
| `user://` 路径 | 第 27 章 |
| ConfigFile 配置 | 第 27 章 |
| 存档系统 | 第 27、34 章（T24） |
| 断点调试 | 第 28 章 |
| print 家族 | 第 28 章 |
| 性能剖析 Profiler | 第 29 章 |
| 绘制调用优化 | 第 29 章 |
| 多线程 | 第 29 章 |
| 引用计数 / 内存 | 第 30 章 |
| 对象池 | 第 30、34 章（T12 相关） |
| `queue_free` | 第 30、37 章 |
| 场景切换 | 第 31 章（T02） |
| 输入封装 | 第 31 章（T03） |
| 冷却 / 计时 | 第 31 章（T04） |
| 音效管理 | 第 31 章（T07） |
| 玩家控制器 | 第 32 章（T08、T09） |
| 状态机 | 第 32 章（T10） |
| 血量 / 伤害 | 第 32 章（T11） |
| 敌人 AI | 第 32 章（T12） |
| 武器 / 子弹 | 第 32 章（T13） |
| 拾取物 / 道具 | 第 32 章（T14） |
| 主菜单 | 第 33 章（T15） |
| HUD / 血条 | 第 33 章（T16） |
| 对话系统 | 第 33 章（T17） |
| 背包系统 | 第 33 章（T18） |
| 暂停菜单 | 第 33 章（T19） |
| 关卡选择 | 第 33 章（T20） |
| 相机跟随 | 第 34 章（T21） |
| 屏幕震动 / 顿帧 | 第 34 章（T23） |
| 本地化 / 多语言 | 第 34 章（T25） |
| 调试控制台 | 第 34 章（T26） |
| 完整项目实战 | 第 35 章 |
| 语法速查 | 第 36 章 |
| 报错查询 | 第 37 章 |
| Godot 3→4 迁移 | 第 38 章 |
| `yield` → `await` | 第 38 章 |
| `instance` → `instantiate` | 第 38 章 |
| `rect_position` → `position` | 第 38 章 |
| `move_and_slide` 变化 | 第 38 章 |
| Tween 迁移 | 第 38、24 章 |
| 术语解释 | 附录 A |
| 学习路线 | 附录 B |
| 读真实项目 / 看懂别人代码 / 做第一处修改 | 附录 D |
| 只有手机怎么学 / 无电脑练习 | 附录 E |

## C.3 26 个模板（T01–T26）索引表

| 模板号 | 名称 | 所在章节 | 一句话用途 |
| --- | --- | --- | --- |
| T01 | 游戏管理器 / 全局单例 | 第 31 章 | 集中管理全局状态与子系统访问入口 |
| T02 | 场景切换器 | 第 31 章 | 带过渡动画的切场景封装 |
| T03 | 输入映射封装 | 第 31 章 | 把 InputMap 操作包装成统一接口 |
| T04 | 计时器 / 冷却管理器 | 第 31 章 | 统一管理技能冷却、定时事件 |
| T05 | 存档系统 | 第 31 章 | 一键保存/读取游戏进度 |
| T06 | 设置菜单 | 第 31 章 | 音量、分辨率、按键设置的 UI 与持久化 |
| T07 | 音效管理器 | 第 31 章 | BGM 切换、SFX 播放与音量控制 |
| T08 | 玩家控制器（2D） | 第 32 章 | 2D 平台/俯视角色移动与跳跃 |
| T09 | 玩家控制器（3D） | 第 32 章 | 3D 角色移动与相机相对转向 |
| T10 | 有限状态机 | 第 32 章 | 用状态模式组织角色行为 |
| T11 | 血量 / 伤害系统 | 第 32 章 | 生命值、受伤、死亡、无敌帧 |
| T12 | 敌人 AI | 第 32 章 | 巡逻、追击、攻击的状态化 AI |
| T13 | 武器 / 子弹 | 第 32 章 | 射击、弹道、冷却、伤害结算 |
| T14 | 拾取物 / 道具 | 第 32 章 | 掉落、拾取、道具效果 |
| T15 | 主菜单 | 第 33 章 | 开始游戏、设置、退出 |
| T16 | HUD / 血条 | 第 33 章 | 血条、分数、倒计时的界面展示 |
| T17 | 对话系统 | 第 33 章 | 对话框、逐字显示、分支选择 |
| T18 | 背包系统 | 第 33 章 | 物品格、堆叠、拖拽整理 |
| T19 | 暂停菜单 | 第 33 章 | 暂停、恢复、返回主菜单 |
| T20 | 关卡选择 | 第 33 章 | 关卡列表、解锁状态、进度显示 |
| T21 | 相机跟随 | 第 34 章 | 平滑跟随、边界限制、死区 |
| T22 | 粒子 / 特效 | 第 34 章 | 爆炸、拖尾、命中特效的封装 |
| T23 | 屏幕震动 / 顿帧 | 第 34 章 | 增强打击感的镜头与时间效果 |
| T24 | 存档加密 | 第 34 章 | 存档简单加密与校验，防手改 |
| T25 | 本地化 | 第 34 章 | 多语言文本切换与资源组织 |
| T26 | 调试控制台 | 第 34 章 | 运行时输入命令、作弊码、查看状态 |

## C.4 全书结束语

写到这里，这本书就真的结束了。

你可能是一路从第 1 章读过来的，也可能是跳着翻到这里的。不管怎样，如果你此刻能对着一个空场景，从容地写下第一个 `extends Node2D`，知道自己在干什么、为什么要这么写——那你已经比刚开始时强太多了。

学编程这件事，最难的不是语法。语法就这么点，翻来覆去。真正难的，是**在一次次报错、一次次"为什么不动"之后，还愿意打开编辑器，再试一次**。这本书能给你的，是地图和工具；路得你自己走。

所以，别把这本书当终点。合上它，去做一个小东西——哪怕只是一个会跳、会掉血、会死掉的小方块。把它做完整，然后做下一个。你会发现，那些曾经觉得晦涩的章节，会在你真正用它们的时候，突然变得清晰。

祝你写出属于自己的游戏。

我们，下一个项目见。

---
---

# 附录 D：把知识用到真实项目上（基础篇）

前面 38 章是在"实验室"里学 GDScript：例子干净、逻辑单一、读完就知道对错。可真正让人卡住的，从来不是语法，而是**第一次打开一个别人写的真实项目**——几千行代码、几十个脚本、目录层层套娃，你"每个关键字都认识"，却"整段看不懂"，更不敢改。

本附录要解决的就是这一步。它不讲新语法，只教你**看懂一个真实商业 Godot 项目、并安全地做小改动**。

为了对所有读者通用，全文不点名任何具体项目，统一用"**某真实项目 / 示例项目**"这种泛化说法；代码是**重写的干净教学版**，命名通用、可直接抄走。

读完之后，你应该能做到三件事：

1. 打开任意一个中等规模的 Godot 项目，**3 分钟内知道该先看哪几个文件**；
2. 看懂它最核心的三块基建——**常量表、状态机、工具类**；
3. 独立做出**第一处安全的小改动**（改数值、加函数、加状态），并且知道怎么自测、怎么避坑。

---

## D.1 为什么要读别人写的项目

### D.1.1 自学者的瓶颈：不是不会写，是不敢改

很多自学者会经历这样一个阶段：

- 语法书看完了，`for`、`match`、`class_name`、信号、`await` 全会；
- 自己从零写个小 demo 也没问题；
- 但一旦面对真实项目，就**只看不写**——"万一改坏了怎么办？"

这个瓶颈的根源不是知识点缺失，而是缺少**"读懂结构"的训练**。从零写代码时，结构是你自己定的；读别人代码时，结构是别人定的，而且往往和课本不一样。你要学的是：**先看懂别人怎么组织代码，再动它。**

### D.1.2 读项目的正确顺序

千万不要一上来就从 `main.gd` 第一行读到最后一行，那必然晕。推荐这个顺序：

| 步骤 | 做什么 | 产出 |
| --- | --- | --- |
| ① 先跑起来 | 用编辑器打开、点运行，看它到底长什么样、能做什么 | 建立"目标感"：知道每个功能对应什么表现 |
| ② 看目录 | 只看目录名，猜每层放什么 | 建立"地图感"：知道东西大概在哪 |
| ③ 顺藤摸瓜 | 挑一个**最小的功能**，从入口一路追到出口 | 建立"路径感"：知道一次操作经过哪些文件 |
| ④ 再动手改 | 从改一个数值开始，逐步加代码 | 建立"掌控感"：从旁观者变成修改者 |

第 ③ 步是核心。"顺藤摸瓜"的意思是：比如你看到他有个"开始游戏"的按钮，就顺着按钮——信号连到哪个函数——那个函数调了哪个管理器——管理器改了什么数据——一路追下去。**追通一条线，胜过通读十个文件。**

具体怎么"顺"？举个例子，假设你要追"点击开始按钮会发生什么"：

```
① 找到按钮所在场景（.tscn），看它连了哪个信号、连到哪个脚本的哪个函数
        │
        ▼
② 打开那个脚本，找到被连的函数（比如 _on_start_pressed）
        │
        ▼
③ 看函数里调了什么：例如 level_manager.start_level(1)
        │
        ▼
④ 打开 LevelManager 脚本，找到 start_level()，看它改了哪些数据、加载了哪些场景
        │
        ▼
⑤ 一路追到最底层（真正改变游戏状态的地方），这条线就通了
```

追的时候用编辑器的"跳转到定义"（通常是 Ctrl/Cmd + 点击函数名），比手翻文件夹快得多。**追通一条线以后，你再去看别的功能，会发现它们用的是同一套骨架，理解速度会指数级提升。**

**小提醒**：一次只追一条线，别中途被旁边的函数带跑。你在某处看到一个"看起来也很重要"的函数时，先记下名字，追完当前这条线再回头。

### D.1.3 心态：真实项目代码通常"不好看"

这是新手最容易受打击的地方，务必提前打预防针。真实商业项目里，你几乎一定会看到：

- **命名不统一**：同一个概念，有的地方叫 `HP`，有的叫 `Hp`，有的叫 `health`；
- **历史遗留**：有注释掉的代码、有写了但没人调用的函数、有 `# TODO`；
- **风格混杂**：有的文件用 Tab 缩进，有的用 4 个空格；有的每行都写类型，有的完全靠推断；
- **超大文件**：一个脚本上千行，一个类管十件事。

**这很正常，不是你水平不够。** 真实项目是为了"按时上线"而写的，不是为了让谁读得舒服。你的任务是**取其骨架、忽略其噪音**，而不是给每一处不统一都打差评。

---

## D.2 快速看懂一个 Godot 项目的目录结构（基础）

### D.2.1 典型商业项目怎么划分

课本里的 demo 往往一个 `main.gd` 走天下。真实项目第一个动作就是**给目录分层**。一个典型、通用的 Godot 项目会把脚本集中放在 `gd/`（或 `scripts/`）下，再按职责分成几层：

| 目录 | 放什么 | 为什么这么分 |
| --- | --- | --- |
| `constant/` | 常量、枚举、全局配置名 | 全局唯一事实来源，改一处全生效 |
| `config/` | 可调数值、关卡参数 | 策划/平衡性调参的地方，和逻辑解耦 |
| `common/` | 公共基类（状态基类、角色基类） | 被大量子类继承，改动影响面大 |
| `util/` | 工具类（全是 `static func`） | 与上下文无关的纯函数，随处调用 |
| `game/` | 真正的玩法逻辑 | 业务代码，分层最细，通常按功能再分子目录 |

一句口诀：**constant 是词典，common 是骨架，util 是工具箱，game 是血肉。**

### D.2.2 一个泛化的目录树

```
res://
├── gd/                        # 所有 GDScript 脚本（纯逻辑）
│   ├── constant/              # 常量与枚举：全局唯一事实来源
│   │   └── game_const.gd
│   ├── config/                # 可调配置：数值、关卡参数
│   │   └── level_config.gd
│   ├── common/                # 公共基类：被大量继承
│   │   ├── state_base.gd      # 状态基类
│   │   └── actor_base.gd      # 角色基类
│   ├── util/                  # 工具类：全是 static func
│   │   ├── game_utils.gd
│   │   └── resource_util.gd
│   └── game/                  # 玩法逻辑，按功能再分
│       ├── actor/             # 角色相关
│       │   ├── actor.gd
│       │   └── status/        # 状态机与各状态
│       │       ├── state_machine_root.gd
│       │       ├── state_idle.gd
│       │       ├── state_move.gd
│       │       └── state_attack.gd
│       └── level/             # 关卡/流程相关
│           └── level_manager.gd
├── scene/                     # 场景文件 .tscn
│   ├── actor.tscn
│   └── level.tscn
├── assets/                    # 美术、音频等原始资源
│   ├── image/
│   └── audio/
└── project.godot              # 工程配置
```

这张图是**通用骨架**，不同项目名字可能不同（`gd` 可能叫 `scripts`，`game` 可能叫 `logic`），但**分层思路几乎一致**。

### D.2.3 "3 分钟上手清单"

拿到一个新项目，按这个顺序翻：

1. **`constant/` 先看**（1 分钟）：把枚举和常量扫一眼，你就知道了这个游戏里有哪些状态、哪些阵营、有哪些关键数值。这是项目的"词典"。
2. **`common/` 再看**（1 分钟）：只看基类里**定义了哪些方法名**，不用看实现。你立刻知道"一个状态要有 enter/action/exit""一个角色有哪些通用能力"。
3. **`util/` 最后看**（1 分钟）：把工具函数的**函数名列表**过一遍。你会知道项目里"常用的杂活"都有现成的，以后不用重复造轮子。

看完这三块，你就已经拿到项目的"地图"了。**具体玩法代码（`game/`）先别急，等你需要追某条线时再进去。**

---

## D.3 读懂"常量与枚举"文件（基础样板）

### D.3.1 为什么大项目要把枚举集中到一个文件

新手习惯"用到哪就写哪"，比如攻击时写 `if status == 3:`。这个 `3` 就是**魔法数字**，问题很大：

- 别人（以及三个月后的你）根本不知道 `3` 是什么；
- 一旦状态顺序变了，所有 `3` 全错；
- 同一个含义散落各处，改起来要全局搜索。

大项目的做法：**所有枚举和常量集中到一个文件**，定义一个全局常量类。这样"状态"有了名字，改一处全生效。

### D.3.2 泛化的常量类样板

```gdscript
# ============================================================
# 文件：gd/constant/game_const.gd
# 全局常量与枚举集中地：所有"魔法数字/魔法字符串"都放这里
# ============================================================
class_name GameConst
extends RefCounted   # 只是容器，不需要挂到场景树，继承 RefCounted 最轻量

# ---------- 1) 角色状态枚举 ----------
enum ActorStatus {
	IDLE,      # 待机
	MOVE,      # 移动
	ATTACK,    # 攻击
	HURT,      # 受击
	STUN,      # 眩晕
}

# ---------- 2) 阵营枚举 ----------
enum Camp {
	PLAYER,    # 我方
	ENEMY,     # 敌方
	NEUTRAL,   # 中立
}

# ---------- 3) 动画名映射（字典充当小型配置表） ----------
# 键是状态枚举，值是"该状态下应该播放的动画名"
const STATUS_ANIMATION := {
	ActorStatus.IDLE: "idle",
	ActorStatus.MOVE: "walk",
	ActorStatus.ATTACK: "attack",
	ActorStatus.HURT: "hurt",
	ActorStatus.STUN: "stun",
}

# ---------- 4) 通用数值 ----------
const MOVE_SPEED := 120.0     # 默认移动速度（像素/秒）
const ENEMY_MAX_HP := 100     # 敌人默认血量

# ---------- 5) 小工具：安全地取动画名 ----------
static func animation_of(status: int) -> String:
	return STATUS_ANIMATION.get(status, "idle")   # 找不到就回退 idle
```

逐段解释：

- `class_name GameConst`：给它一个全局名字。之后任何脚本里都可以直接写 `GameConst.ActorStatus.ATTACK`，**不用 `preload`、不用 `get_node`**。这是本书第 15 章讲的"让类全局可用"。
- `extends RefCounted`：它只是个装常量/函数的容器，不需要生命周期，继承最轻的 `RefCounted` 即可（也可以不写 `extends`，默认就是 RefCounted）。
- `enum ActorStatus { ... }`：枚举本质是给整数取名字。`IDLE` 就是 `0`，`MOVE` 是 `1`，依次加一。以后代码里写 `ActorStatus.MOVE`，比写 `1` 清楚一百倍。
- `const STATUS_ANIMATION := { ... }`：**用字典充当小型配置表**——把"枚举 → 动画名"这种一对一关系塞进字典，用的时候 `STATUS_ANIMATION[status]` 一句取到。
- `animation_of()`：一个 `static func`（静态函数），不依赖实例就能调用：`GameConst.animation_of(ActorStatus.MOVE)`。注意它用了 `.get(status, 默认值)`，找不到时不会报错，而是回退 `"idle"`——这是工程里非常常见的"防御式取值"。

### D.3.3 enum 与字典映射的取舍

| 方案 | 优点 | 缺点 | 适合 |
| --- | --- | --- | --- |
| 纯 enum | 类型明确、代码提示好用 | 不能携带额外数据 | 只需要一个"名字"的场景 |
| enum + 字典 | 可携带映射数据（动画名、伤害值等） | 字典要手工和枚举保持同步 | 枚举需要关联配置时 |
| 纯字典（字符串键） | 最灵活、易外部替换 | 没有拼写检查，易写错 | 数据驱动的配置表 |

经验法则：**状态"有哪些"用 enum；状态"对应什么"用字典。** 两者搭配，各司其职。

### D.3.4 如何安全地新增一个枚举项

假设你要加一个"眩晕 STUN"。枚举本身很简单，在末尾加一项即可。但**真实项目里加枚举有讲究**，因为枚举值是**整数**，而整数可能被写进了存档或网络包：

- **推荐：新项加在末尾**。因为前面的值不变，旧存档不会错位。
- **危险：插在中间**。比如在 `MOVE` 和 `ATTACK` 之间插入，后面的 `ATTACK`、`HURT` 的整数值全部后移，旧存档里"存着 `2` 表示攻击"就会变成别的状态。**这是最常见的存档事故。**
- **必须中间插入时**：给新项**显式赋值**，避免挤动别人：
  ```gdscript
  enum ActorStatus {
  	IDLE,       # 0
  	MOVE,       # 1
  	ATTACK,     # 2
  	HURT,       # 3
  	STUN = 10,  # 显式赋一个不冲突的值，绝不挤动前面的
  }
  ```
- **同步字典**：如果 `STATUS_ANIMATION` 这类映射存在，记得补上新项，否则 `.get()` 只能拿到默认值。
- **存档兼容的终极做法**：存档里**存枚举的字符串名**（如 `"STUN"`）而不是数字，这样顺序怎么变都不怕。代价是稍微啰嗦一点。

---

## D.4 读懂"状态机"架构（基础，重点）

### D.4.1 大白话：为什么角色要用状态机

先看不用状态机的写法，新手最容易写成这样：

```gdscript
# 反例：不推荐
func _physics_process(delta):
	if is_attacking:
		# 攻击逻辑
		pass
	elif is_hurt:
		# 受击逻辑
		pass
	elif is_moving:
		# 移动逻辑
		pass
	else:
		# 待机逻辑
		pass
```

问题：

- 每加一种行为，就要多一个 `elif`，方法越来越长；
- 各种 `is_xxx` 布尔量容易同时为真，出现"边攻击边受击"的矛盾；
- 每个状态的进入/退出逻辑（播哪个动画、清哪个计时器）散在各处，很容易漏。

**状态机的核心思想**：同一时刻，角色**只处于一个状态**。把每种行为写成一个独立的小脚本，角色只在状态之间"切换"。这样：

- 加行为 = 加一个小文件，不改老代码；
- 状态之间互斥，逻辑不会打架；
- 每个状态自己管好"进来做什么、每帧做什么、离开做什么"。

### D.4.2 三层结构

真实项目里的状态机，通用骨架都是三层：

```
┌───────────────────────────────────────────────────┐
│ 第 3 层：StateMachineRoot（总调度，挂在角色下）      │
│  - _status_map：{枚举 -> 状态节点}                   │
│  - _physics_process 每帧调当前状态的 action()        │
│  - change_status(next)：负责切换、并拦截非法切换     │
└────────────────────────┬──────────────────────────┘
                         │ 各状态作为它的子节点
      ┌──────────────┬───┴────────┬──────────────┐
      ▼              ▼            ▼              ▼
   StateIdle     StateMove    StateAttack    StateHurt
   └───────────── 都继承自 StateBase（第 1/2 层）────────┘
   第 1 层：StateBase 定义统一接口 enter/action/exit
   第 2 层：每个状态脚本继承基类，各写各的逻辑
```

- **第 1 层 `StateBase`（基类）**：只定义接口——`enter`、`action`、`exit_status` 等方法名和默认实现。它规定"一个状态必须长什么样"。
- **第 2 层 各状态脚本**：`StateIdle`、`StateMove`……都 `extends StateBase`，各自实现具体逻辑。
- **第 3 层 `StateMachineRoot`（总调度）**：一个字典把"枚举"映射到"状态节点"，每帧只调当前状态的 `action()`。

### D.4.3 几个关键设计点

| 设计 | 作用 | 为什么这么写 |
| --- | --- | --- |
| 字典做"枚举 → 节点"映射 | `change_status` 时 O(1) 找到目标状态 | 比一堆 `if/elif` 找节点更快、更好扩展 |
| `change_status` 的 `exit_status` 返回 bool | 旧状态可以**拦截**离开 | 比如攻击硬直期间不许被切走 |
| `enter_necessary` 与 `enter` 分开 | 一个"能不能进"，一个"进来做什么" | 判断和初始化分离，语义清晰 |
| `owner` / `owner_node` 取父节点 | 状态脚本要操作"角色本体" | 状态自己是子节点，角色本体在上一层 |

### D.4.4 精简可运行版（可直接抄）

下面这套是**重写的干净教学版**，泛化成 Idle / Move / Attack 三状态，可直接跑。它由 5 个文件组成，放在同一场景树下即可。

**文件 1：`state_base.gd`（第 1 层，基类）**

```gdscript
# ============================================================
# 文件：state_base.gd
# 所有状态的基类：定义统一的钩子接口
# ============================================================
class_name StateBase
extends Node

# 状态机的持有者（角色本体），由 StateMachineRoot 在 _ready 里注入
var owner_node: Node


# 进入前判断：返回 true 表示"允许进入"
func enter_necessary(_msg: Dictionary = {}) -> bool:
	return true


# 真正进入后的初始化：赋初值、播动画、连信号
func enter(_msg: Dictionary = {}) -> void:
	pass


# 每帧调用：状态的主要逻辑
func action(_delta: float) -> void:
	pass


# 退出时调用：返回 true 表示"允许切换出去"
func exit_status() -> bool:
	return true


# 返回状态名，供状态机登记与调试
func get_status_name() -> String:
	return "StateBase"
```

**文件 2：`state_machine_root.gd`（第 3 层，总调度）**

```gdscript
# ============================================================
# 文件：state_machine_root.gd
# 状态机总调度：扫描子节点建字典，每帧调当前状态的 action
# ============================================================
class_name StateMachineRoot
extends Node

# 状态枚举：新增状态时在这里加一项
enum Status {
	IDLE,
	MOVE,
	ATTACK,
}

# 枚举 -> 节点名 的对照表（新增状态时同步补一行）
const STATUS_NAMES := {
	Status.IDLE: "StateIdle",
	Status.MOVE: "StateMove",
	Status.ATTACK: "StateAttack",
}

# 角色本体，可在编辑器里拖入；不填就自动取父节点
@export var owner_node: Node

var _current_status: StateBase          # 当前状态脚本实例
var _status_map: Dictionary = {}        # 枚举 -> 状态节点
var _current_key: int = -1              # 当前状态的枚举值

func _ready() -> void:
	# 1) 扫描所有子节点，凡是 StateBase 类型的都登记进字典
	for child in get_children():
		if child is StateBase:
			child.owner_node = owner_node if owner_node != null else get_parent()
			var key := _key_from_name(child.get_status_name())
			if key != -1:
				_status_map[key] = child
	# 2) 默认进入 IDLE
	change_status(Status.IDLE)


func _physics_process(delta: float) -> void:
	if _current_status != null:
		_current_status.action(delta)


# 把状态名翻译成枚举值
func _key_from_name(status_name: String) -> int:
	for key in STATUS_NAMES:
		if STATUS_NAMES[key] == status_name:
			return key
	return -1


# 切换状态：返回 bool 表示是否切换成功
func change_status(next_key: int, msg: Dictionary = {}) -> bool:
	if not _status_map.has(next_key):
		push_warning("状态机：未注册的状态键 %s" % next_key)
		return false
	# 1) 先问旧状态"能不能走"
	if _current_status != null and not _current_status.exit_status():
		return false                      # 旧状态拦截（如攻击硬直中）
	# 2) 再问新状态"能不能进"
	var next_status: StateBase = _status_map[next_key]
	if not next_status.enter_necessary(msg):
		return false
	# 3) 真正切换
	_current_status = next_status
	_current_key = next_key
	_current_status.enter(msg)
	return true


# 外部查询
func get_current_status() -> StateBase:
	return _current_status


func get_current_key() -> int:
	return _current_key
```

**文件 3：`state_idle.gd`（第 2 层，待机）**

```gdscript
class_name StateIdle
extends StateBase

var _timer: float = 0.0

func enter(_msg: Dictionary = {}) -> void:
	_timer = 0.0
	print("[Idle] 进入待机")

func action(delta: float) -> void:
	_timer += delta
	# 待机超过 2 秒，就切去移动
	if _timer > 2.0:
		var machine := get_parent() as StateMachineRoot
		machine.change_status(StateMachineRoot.Status.MOVE)

func exit_status() -> bool:
	return true   # 待机随时可以走

func get_status_name() -> String:
	return "StateIdle"
```

**文件 4：`state_move.gd`（第 2 层，移动）**

```gdscript
class_name StateMove
extends StateBase

var _speed: float = 100.0     # 像素/秒

func enter(_msg: Dictionary = {}) -> void:
	print("[Move] 进入移动")

func action(delta: float) -> void:
	# 让角色本体沿 X 轴平移（owner_node 是 Node2D 才能改 position）
	var body := owner_node as Node2D
	if body != null:
		body.position.x += _speed * delta
		if body.position.x > 300.0:      # 走到位置就切去攻击
			var machine := get_parent() as StateMachineRoot
			machine.change_status(StateMachineRoot.Status.ATTACK)

func exit_status() -> bool:
	return true

func get_status_name() -> String:
	return "StateMove"
```

**文件 5：`state_attack.gd`（第 2 层，攻击）**

```gdscript
class_name StateAttack
extends StateBase

const ATTACK_DURATION := 1.0
var _timer: float = 0.0

func enter(_msg: Dictionary = {}) -> void:
	_timer = 0.0
	print("[Attack] 进入攻击")

func action(delta: float) -> void:
	_timer += delta
	if _timer >= ATTACK_DURATION:
		var machine := get_parent() as StateMachineRoot
		machine.change_status(StateMachineRoot.Status.IDLE)

# 攻击硬直中不许被切走：这就是 exit_status 拦截
func exit_status() -> bool:
	return _timer >= ATTACK_DURATION

func get_status_name() -> String:
	return "StateAttack"
```

### D.4.5 使用说明（怎么挂节点、怎么切状态）

**节点树**（在编辑器里这样搭）：

```
Actor (Node2D)                 # 角色本体
└── StateMachine (Node, 脚本 = state_machine_root.gd)
    ├── StateIdle   (Node, 脚本 = state_idle.gd)
    ├── StateMove   (Node, 脚本 = state_move.gd)
    └── StateAttack (Node, 脚本 = state_attack.gd)
```

要点：

1. **节点名必须和 `STATUS_NAMES` 里的名字一致**（`StateIdle` / `StateMove` / `StateAttack`），否则登记不上；脚本的 `class_name` 也要一致。
2. **谁用 `owner_node`**：状态脚本操作角色本体时用它（例如移动改位置）。它由 `StateMachineRoot` 在 `_ready` 里自动注入父节点。若角色本体不是状态机的直接父节点，就在编辑器的 `owner_node` 属性里手动拖入。
3. **怎么切状态**：任何地方调用 `state_machine.change_status(StateMachineRoot.Status.ATTACK)` 即可。返回值是 `bool`，`false` 表示被拦下了。
4. **每帧只跑当前状态**：`_physics_process` 只会调用当前状态的 `action()`，所以不用担心多个状态同时乱动。

### D.4.6 给现有状态机加一个新状态：5 步流程

假设你要给这套结构加一个"待机升级版"或"眩晕"，标准流程是：

| 步 | 做什么 | 细节 |
| --- | --- | --- |
| 1 | 加枚举 | 在 `Status` 枚举末尾加一项（如 `STUN`），**别插中间** |
| 2 | 新建脚本 | 新建 `state_stun.gd`，写 `class_name StateStun`、`extends StateBase` |
| 3 | 实现三个方法 | 实现 `enter`（初始化+播动画）、`action`（每帧逻辑）、`exit_status`（能否离开） |
| 4 | 加为子节点 | 在场景树里给 `StateMachine` 加一个 `Node` 子节点，改名 `StateStun`，挂上脚本 |
| 5 | 注册进字典 | 在 `STATUS_NAMES` 里加一行 `Status.STUN: "StateStun"` |

五步做完，新状态就接进系统了，**完全不用改其他状态和调度逻辑**——这就是状态机最大的好处。

---

## D.5 读懂"工具类"（静态函数集中营）

### D.5.1 `static func` 与 `class_name` 的组合

真实项目里几乎一定有一个"工具类"，里面**全是 `static func`**：

```gdscript
class_name GameUtils
extends RefCounted

static func add(a: int, b: int) -> int:
	return a + b
```

用法：`GameUtils.add(1, 2)`，**不用 new 一个实例**。配上 `class_name`，它就是全局可用的"工具箱"。

- `static func` 不依赖对象状态，只做"输入 → 计算 → 输出"；
- `class_name` 让类全局可见，任何脚本直接写类名就能用；
- 两者组合 = **随处可用的纯函数**，这是工程里最省事的复用方式。

**读懂工具类 = 读懂项目的"方言词典"**。别人写 `GameUtils.is_hit(a, b, r)`，你若知道它内部在做什么，就能读懂一半玩法代码。

### D.5.2 高频工具函数 + 干净实现

下面是真实项目里**最常出现**的几类工具函数，各给一个干净版本：

```gdscript
class_name GameUtils
extends RefCounted

# 1) 计数器取模：每 interval 次才返回一次 true（用于"每隔 N 帧/次"）
static func is_interval(counter: int, interval: int) -> bool:
	if interval <= 0:
		return false
	return counter % interval == 0

# 2) 范围判定：用平方距离，避免开方，性能更好
static func in_range(a: Node2D, b: Node2D, radius: float) -> bool:
	return a.global_position.distance_squared_to(b.global_position) <= radius * radius

# 3) 数值格式化：把 1234567 变成 "1,234,567"
static func format_number(value: int) -> String:
	var s := str(absi(value))
	var out := ""
	var count := 0
	for i in range(s.length() - 1, -1, -1):
		out = s[i] + out
		count += 1
		if count % 3 == 0 and i > 0:
			out = "," + out
	return ("-" if value < 0 else "") + out

# 4) 随机范围：浮点用 randf_range，整数用 randi_range
static func rand_float(min_v: float, max_v: float) -> float:
	return randf_range(min_v, max_v)

static func rand_int(min_v: int, max_v: int) -> int:
	return randi_range(min_v, max_v)   # 闭区间

# 5) 概率：返回 true 的概率为 probability（0.0 ~ 1.0）
static func chance(probability: float) -> bool:
	return randf() < clampf(probability, 0.0, 1.0)

# 6) 数组查找最近点：返回离 from 最近的 Vector2
static func find_nearest(from: Vector2, points: Array[Vector2]) -> Vector2:
	var best := from
	var best_dist := INF
	for p in points:
		var d := from.distance_squared_to(p)
		if d < best_dist:
			best_dist = d
			best = p
	return best

# 7) UUID 生成：简单唯一串（时间戳 + 随机数）
static func make_uuid() -> String:
	return "%d-%d" % [Time.get_unix_time_from_system(), randi()]
```

几个值得注意的点：

- **`counter % interval == 0`**：真实项目里"每隔 N 次做一次"的标准写法，比维护一堆计时器省事。注意 `interval` 必须大于 0，否则取模会出错，所以前面有防御判断。
- **`distance_squared_to`**：判断"是否在半径内"时，比较**距离的平方**和**半径的平方**即可，省掉一次开方。这是本书讲过的性能小技巧，真实项目高频使用。
- **`clampf`、`absi`**：Godot 4 内置。用内置函数比自己写判断更稳。
- **`Array[Vector2]`**：带类型的数组，编辑器会提示类型。真实项目里越来越常见。

### D.5.3 为什么工具类容易变成"上帝类"

工具类越用越方便，于是**什么都往里塞**，最后变成几百个函数的"上帝类"（God Class）。它在小项目里没问题，但在大项目里会：

- 难查找（几百个函数挤一个文件）；
- 职责混乱（随机数、路径、数值、网络全混在一起）；
- 改动风险高（谁改一下工具函数，可能影响全项目）。

所以读到工具类时，**先按功能分组看函数名**，而不是从头读到尾；如果你要往里加函数，尽量归到对应分组，别让文件继续膨胀。

---

## D.6 读懂"贴图/资源加载"（基础）

### D.6.1 商业项目为什么爱"包装一层加载"

课本里加载资源就一句 `load("res://xxx.png")`。真实项目却常常**再包一层**，写个自己的加载函数。原因有三：

1. **统一入口**：全项目资源都走同一个函数，出问题只查一处；
2. **便于换实现**：哪天要改成异步加载、要加缓存、要加日志，只改这一个函数；
3. **支持外部替换 / MOD**：这是关键——引擎的 `load()` 只认 `res://` 里**导入过的**资源；而游戏上线后，玩家可能想替换贴图。这时就要**直接从源文件读取**，绕过引擎的导入系统。

### D.6.2 一个泛化的资源加载工具函数

```gdscript
class_name ResourceUtil
extends RefCounted

# 加载贴图：优先直读源文件，失败再回退到引擎的 load()
static func load_texture(path: String) -> Texture2D:
	# 分支 1：user:// 或 绝对路径 —— 这类是"外部文件"，用 Image 直读
	if path.begins_with("user://") or path.is_abs_path():
		var image := Image.new()
		var err := image.load(path)
		if err == OK:
			return ImageTexture.create_from_image(image)
		push_warning("直读图片失败，尝试回退：" + path)

	# 分支 2：res:// 内部资源 —— 走引擎的 load()（走导入系统）
	if path.begins_with("res://"):
		var res := load(path)
		if res is Texture2D:
			return res

	push_warning("资源加载失败：" + path)
	return null
```

逐行解释：

- **分支 1 用 `Image.load()`**：`Image` 是"裸图像"，它能直接读磁盘上的源文件（`user://` 存档目录、或系统绝对路径），不经过引擎导入。读进来后用 `ImageTexture.create_from_image()` 转成贴图，才能挂到 `Sprite2D` 上。这正是"支持玩家替换资源"的关键路径。
- **分支 2 用 `load()`**：`res://` 里的资源是引擎**导入过**的（`.import` 产物），必须用 `load()` 拿。
- **`is_abs_path()`**：Godot 4 的 `String` 方法，判断是不是绝对路径（如 `/root/xxx` 或 `C:\xxx`）。
- **失败回退 + `push_warning`**：先试直读，失败再走 `load`，最后兜底返回 `null` 并给一条警告。**工程里一定要有兜底**，不要让一次加载失败就崩掉整个游戏。

### D.6.3 资源替换的基本原理（只讲原理）

为什么有时候"换了贴图却没生效"？核心原因是：

> **源文件 与 引擎导入产物 必须"同一张图"。**

- 引擎的 `load("res://a.png")` 读的其实是 `a.png` 的**导入产物**（在 `.godot/imported/` 里，由 `a.png.import` 记录）；
- 玩家替换的往往是 `a.png` **源文件**本身；
- 如果代码走 `load()`，读到的还是旧的导入产物 → 换了没反应；
- 如果代码走 `Image.load()` 直读源文件 → 立刻生效。

所以"优先直读源文件"的封装，本质是为了**让替换的资源真的被用上**。这里只需要理解这条原理即可，具体文件不必展开。

**一句话记住**：`res://` 正式资源走 `load()`；**可替换/外部资源**走 `Image.load()` 直读。

---

## D.7 安全地做你的第一处修改（基础）

### D.7.1 改前必做三件事

| 事项 | 具体做法 | 为什么 |
| --- | --- | --- |
| 备份 | 先把整个工程复制一份，或确认在 Git 里、能随时还原 | 新手最容易改坏，有备份就不慌 |
| 建立基线 | 改之前先**跑一遍**，确认它现在是正常的 | 否则改完出问题，分不清是原来的还是你改的 |
| 一次一处 | **一次只改一个地方**，改完立刻测 | 多处一起改，出错时无从定位 |

**改一处、测一次**，是新手唯一该有的节奏。

### D.7.2 三个由易到难的小练习

#### 练习 1：改数值（最容易）

- **改哪里**：打开 `gd/constant/game_const.gd`，找到 `MOVE_SPEED := 120.0` 或 `ENEMY_MAX_HP := 100`。
- **怎么改**：把 `120.0` 改成 `300.0`（角色跑得飞快），或把 `ENEMY_MAX_HP` 改成 `30`（敌人变脆）。
- **怎么验证**：运行游戏，观察角色移动速度 / 敌人几刀就死。**效果立竿见影，最能建立信心。**

#### 练习 2：加一个工具函数

- **改哪里**：打开 `gd/util/game_utils.gd`。
- **怎么改**：在类里加一个 static func，例如把两个数取较大值再乘二：
  ```gdscript
  static func double_max(a: int, b: int) -> int:
  	return maxi(a, b) * 2
  ```
- **怎么调用**：在你追踪过的那条玩法线里，找一处合适的地方加一行 `print(GameUtils.double_max(3, 7))`，运行后看看输出是不是 `14`。
- **怎么验证**：函数有输出、程序不报错，就算成功。这一步在训练"我加的东西能跑起来"。

#### 练习 3：加一个新状态（稍难，但最有价值）

- **改哪里**：状态机目录 `gd/game/actor/status/`。
- **怎么改**：按 **D.4.6 的 5 步流程**，给它加一个最简单的"眩晕"或"待机升级"状态：加枚举 → 新建脚本继承 `StateBase` → 实现 `enter/action/exit_status` → 场景树加子节点 → 在 `STATUS_NAMES` 注册。
- **怎么验证**：先在某个状态的 `action` 里临时改一下 `change_status(...)` 切到你新加的状态，运行，看 `print` 有没有打出来、角色表现对不对。验证完再改回去。

### D.7.3 改完怎么自测

- **看报错**：编辑器底部"输出/调试器"会给出错误行号。对着**第 29 章（调试）和第 37 章（报错词典）**排查，报错信息通常已经把"文件 + 行号 + 类型"写清楚了。
- **用 `print`**：在关键位置打日志，确认代码有没有走到、变量的值对不对。新手最有效的武器。
- **用 `push_warning`**：比 `print` 更醒目，会以黄色警告形式出现，适合标记"不该发生但发生了"的情况。
- **加断点**：在编辑器里点行号左侧加断点，运行到那里会暂停，能逐行看变量。适合逻辑复杂、`print` 说不清的时候。

---

## D.8 改项目最容易踩的 8 个坑

| # | 现象 | 原因 | 正确做法 |
| --- | --- | --- | --- |
| 1 | 编辑器里改了资源/数据，**导出版**没变化 | 改的是 `res://` 里的文件，而导出版用的是打包进 exe 的旧副本 | 需要替换的资源走"直读源文件"路径（D.6），或重新导出 |
| 2 | 改了脚本，编辑器里没重新加载 | 编辑器缓存旧脚本 / 需要重载 | 保存后看是否需要"重新加载当前项目"，必要时重启编辑器 |
| 3 | 旧存档读进来状态全乱了 | 枚举**在中间插了一项**，后面的整数全错位 | 新枚举加末尾；必须插中间就显式赋值（D.3.4） |
| 4 | `@onready` 的变量是 `null` | 访问时机太早，节点还没就绪；或节点路径写错 | `@onready` 在 `_ready` 前才赋值，别在 `_init` 里用；确认 `$路径` 正确 |
| 5 | 拿到的父节点不是想要的那个 | `owner`（场景归属）和 `get_parent()`（直接父节点）概念混了 | 要"上层逻辑节点"用 `get_parent()`；要"场景根"用 `owner`，别弄反 |
| 6 | 改了一个角色的贴图，**所有角色都变了** | 资源是**共享引用**，多处指向同一个 `Texture2D` | 需要独立修改时用 `.duplicate()` 复制一份再改 |
| 7 | 老写法直接报错 | 用了 Godot 3 的 `yield(...)` / `instance()` | 换成 Godot 4：`yield` → `await`；`instance()` → `instantiate()`（详见第 38 章） |
| 8 | 缩进报"mixing spaces and tabs" | 同一文件里**空格与 Tab 混用** | 统一只用 Tab 或只用空格；编辑器里开启"显示空白字符"排查 |

逐条补一句：

- 坑 3 和坑 6 是**真实项目里最常造成"玄学 bug"的两个**，务必记住。
- 坑 5：一句话区分——`get_parent()` 是"我的上一层"，`owner` 是"我属于哪个场景"。
- 坑 8 在从别人那里复制代码时特别高发，粘贴完记得对齐缩进。

---

## D.9 附录小结

1. **读项目不是从第一行读到最后一行**，而是"先跑起来 → 看目录 → 顺一条线 → 再动手改"。
2. 真实项目代码"不好看"是常态，**命名不统一、有遗留、风格混杂**都不代表你水平差。
3. 目录分层的通用口诀：**constant 是词典，common 是骨架，util 是工具箱，game 是血肉**。
4. 上手清单：**先看 constant，再看 common，最后看 util**，三分钟拿到项目地图。
5. **常量与枚举集中管理**，是为了消灭魔法数字、改一处全生效；状态"有哪些"用 enum，状态"对应什么"用字典。
6. 新增枚举**优先加在末尾**；必须插中间就**显式赋值**，否则会引发存档错位。
7. **状态机的核心是"同一时刻只处于一个状态"**；三层结构是 `StateBase → 各状态 → StateMachineRoot`。
8. `change_status` 用 `exit_status` 返回 bool 做**切换拦截**；`enter_necessary` 管"能不能进"，`enter` 管"进来做什么"。
9. 给状态机加新状态就 **5 步**：加枚举 → 建脚本 → 实现三方法 → 加子节点 → 注册字典，不必改别的状态。
10. **工具类是项目的"方言词典"**，`static func + class_name` 让它随处可用；但要警惕它膨胀成"上帝类"。
11. 资源加载封装一层是为了**统一入口、便于换实现、支持外部替换**；可替换资源走 `Image.load()` 直读，正式资源走 `load()`。
12. **资源替换原理**：源文件与引擎导入产物必须同图，否则不同加载路径显示不一致。
13. 改代码的纪律：**备份、建立基线、一次一处、改完就测**。
14. 自测三件套：**看报错（第 29/37 章）、`print`/`push_warning`、加断点**。
15. 最容易踩的坑都记住这几条：**枚举中间插项、`@onready` 为 null、`owner` 与 `get_parent` 混用、资源共享引用、Godot 3 老写法、空格与 Tab 混用**。

**最后一句**：读懂真实项目和写代码是两种不同的能力，都需要练。从今天起，找一个小项目，按本附录的顺序读一遍，再做练习 1 的"改数值"——你就已经超过"只会写 demo"的阶段了。---

# 附录 E：纯手机学习方案（逐章对照表）

前面 38 章，加上附录 A 到 D，都是照着"你有台电脑"来写的：打开编辑器、新建项目、敲代码、按运行、看报错。可现实里有很多读者**手里只有一部手机**——可能是学生、可能通勤路上、可能暂时买不起电脑。

这份附录就是专门写给你的。它不灌鸡汤，也不含糊其辞，而是把"手机到底能学到哪一步"讲清楚，再给你一张**38 章逐章对照表**，告诉你每一章能不能用手机练、不能的话怎么换个方式练。

一句话先放这儿：**手机完全可以学完这本书。** 差别只在于——"敲代码验证"的比例会降低，"读代码 + 脑内推演"的比例会提高。这不丢人，反而是一种更扎实的训练方式。往下看你就知道为什么。

---

## E.1 先给结论：手机能学到什么程度

### E.1.1 直接表态

先把最重要的结论说在前面：

- **手机能学完本书全部知识**。语法、类型、信号、生命周期、架构思路，这些都不依赖电脑，只依赖你的脑子。
- **手机能完成"大部分"的运行验证**。官方有 Android 版编辑器，能建项目、写脚本、真跑、真看报错（就是慢一点、累一点）。
- **手机很难舒服地做"大体量工程"**。几十个文件、复杂场景、性能调优，这些确实需要电脑，但它们是本书后期内容，**不影响你先把前面的地基打牢**。

所以："只有手机"不是不可跨越的门槛，只是**换了条路**。

### E.1.2 学习效果分三档

把本书内容按"手机友好度"分成三档，你对号入座就行：

| 档次 | 含义 | 覆盖范围（大致） | 手机怎么完成 |
| --- | --- | --- | --- |
| 第一档 | **手机全功能可完成** | 变量、类型、运算符、流程、函数、数组、字典、字符串、类、枚举等纯逻辑语法 | 用备忘录写代码 + 脑内推演即可（方案 C） |
| 第二档 | **手机可完成约 80%** | 信号、节点引用、生命周期、Tween、await、模板等 | 推演为主，配合 Android 编辑器跑最小例子（方案 A） |
| 第三档 | **建议等有电脑再深做** | 资源系统、文件读写、性能优化、体验调优、架构落地 | 先读懂概念、记笔记，等有条件再动手 |

注意：**第一档就占了本书一半以上的章节**。也就是说，光靠一部手机，你就能把 GDScript 的"语言本体"学明白——而语言本体，才是后面一切的地基。

### E.1.3 一句让你心安的话

请把下面这句话抄在你的备忘录第一行：

> **语法的掌握靠脑内推演，不靠反复运行；运行只负责"验证"，不负责"理解"。**

很多人误以为"跑一遍代码看到结果"就是学懂。其实不是。你按一下运行，屏幕上跳出一串数字，你**依然不知道它是怎么算出来的**——除非你先在脑子里算过一遍。真正的理解发生在"你预测结果"的那一刻；运行只是帮你确认预测对不对。

所以，手机党不是"残缺版学习"，而是**被迫练习了最核心的那项能力：读懂过程，而不是背下结果**。有电脑的人，往往一辈子都没练过这个。

---

## E.2 三种手机方案对比

手机学习法不止一种。市面上可行的是下面三种，各有取舍。

### E.2.1 方案 A：官方 Android 版 Godot 编辑器

这是**唯一能在手机上真正运行代码**的方案。Godot 官方提供了 Android 版编辑器，可以在手机上建项目、写脚本、运行、看报错输出。

- 获取方式：官方下载页有 Android 版 APK（路径形如 `godotengine.org/download/android/`），应用商店里也能搜到；
- 优点：**能真跑**，功能最完整，能看报错；
- 缺点：手机屏幕小、软键盘难敲代码、运行较重；
- 强烈建议：配一套**蓝牙键盘 + 蓝牙鼠标**，体验立刻从"折磨"变成"能用"。

### E.2.2 方案 B：网页版编辑器

浏览器直接打开官方网页版编辑器（地址形如 `editor.godotengine.org`），无需安装。

- 优点：不占手机存储，打开即用；
- 缺点：网页版编辑器需要浏览器支持**"跨域隔离"**（依赖 HTTPS 等安全上下文），而**手机浏览器的兼容性很不稳定**——有的能开、有的白屏；
- 定位：**只适合验证一小段代码片段**，不适合当主力。

### E.2.3 方案 C：纯手机无引擎学习法（本附录重点）

不安装任何东西。用手机自带的**备忘录 / 文本编辑器**敲代码，然后对照书里用 `# →` 标出的结果，做"**脑内推演**"：自己一行行算，算出每步的变量值，最后翻书对答案。

- 优点：**零门槛、零安装、随时随地**，地铁上、排队时都能练；
- 缺点：**看不到真实运行结果**，只能靠推演；
- 但这恰恰是它最大的价值——详见 E.4。

### E.2.4 三方案对比表

| 对比项 | 方案 A：Android 编辑器 | 方案 B：网页版编辑器 | 方案 C：无引擎推演 |
| --- | --- | --- | --- |
| 安装难度 | 中（装 APK/商店下载，占存储） | 低（打开浏览器） | 零（用自带备忘录） |
| 能否运行代码 | ✅ 能真跑 | 不稳定，多数手机难用 | ❌ 不能，靠推演 |
| 适合哪些章节 | 第 19–35 章等需要"看见"的 | 零散小片段验证 | 第 1–18 章等纯语法章节 |
| 缺点 | 屏幕小、重、敲代码慢 | 兼容性差、易白屏 | 无运行反馈 |
| 推荐人群 | 想真做小项目的人 | 偶尔验证片段的人 | 所有手机读者（打底） |

### E.2.5 一句诚实的话

必须说清楚：**GDScript 目前没有官方的在线执行环境**。你可能会搜到一些第三方网页"在线沙箱"，它们大多只能**编辑**代码，并不能**真正执行** GDScript。所以——

> 想在手机上"真跑起来"，只能靠**方案 A（Android 版 Godot 编辑器）**。方案 C 是用来"理解"的，不是用来"运行"的。

这不是坏消息。因为按 E.1 的结论，**理解才是主线，运行只是验证**。你没有运行环境，只是少了验证，没少理解。

---

## E.3 方案 A 详细上手步骤

这一节带你把 Android 版编辑器跑起来，全程文字分步，不需要你翻任何外部教程。

### E.3.1 下载与安装

1. 打开手机浏览器，进入 Godot 官网下载页，找到 **Android 版**；
2. 也可以直接在应用商店搜索"Godot"安装官方版本；
3. 下载 APK 后，按系统提示允许"安装未知来源应用"，完成安装；
4. 安装完成后，桌面会出现 Godot 编辑器图标。

小提示：APK 体积不大，但**首次运行**会解压资源，耐心等几秒。

### E.3.2 首次启动与设置

1. 第一次打开，问你是否允许访问存储——**允许**，编辑器要把项目存在手机里；
2. 进入后你会看到**项目管理器（项目列表）界面**：中间是项目卡片列表，一般有"新建/导入"之类的按钮；
3. 界面语言如果不对，可在设置里切换（认准"Editor Settings → 语言"这一类选项）；
4. 建议第一次就把**字号调大**（见 E.3.5），不然眼睛会累。

### E.3.3 新建项目 → 新建场景 → 新建脚本（触屏顺序）

触屏没有鼠标右键，操作顺序和电脑不同，请按这个顺序走：

```
① 项目管理器 → 点“新建” → 输入项目名、选择存储路径 → 点“创建并编辑”
        │
        ▼
② 进入编辑器 → 左下角找到“文件系统”面板
        │
        ▼
③ 在“场景”面板点“+ / 新建场景” → 选一个根节点（例如 Control 或 Node2D）
        │
        ▼
④ 选中根节点 → 点“附加脚本”图标 → 命名脚本 → 点“创建”
        │
        ▼
⑤ 脚本编辑器打开 → 开始写代码 → 按运行按钮
```

触屏关键点：**"长按" ≈ 电脑右键**，很多菜单藏在长按里。

### E.3.4 怎么运行、怎么看报错

- **运行（电脑上的 F5）**：在编辑器顶部或侧边找**三角形"播放"按钮**，点它即可运行当前场景；
- **看报错**：运行后如果出错，编辑器会弹出**输出/调试面板**，里面就是报错原文。**把它逐字读一遍**，再对照本书**第 37 章报错词典**，绝大多数问题都能自己解决；
- 如果运行没反应，先确认你**有没有保存脚本**，以及**场景根节点是否挂了脚本**。

### E.3.5 手机上写代码的实用技巧

| 技巧 | 做法 | 收益 |
| --- | --- | --- |
| 外接蓝牙键鼠 | 配一套蓝牙键盘 + 鼠标 | 敲代码速度提升数倍 |
| 调大字号 | 设置里把编辑器字体调大 | 保护眼睛，看得清 |
| 代码片段复用 | 把书里的代码复制到剪贴板，或存进备忘录再粘贴 | 少敲、少错 |
| 横屏使用 | 强制横屏 | 一行能看更多字符 |
| 关闭自动更正 | 输入法里关掉"自动更正/联想" | 不被输入法偷偷改错符号 |
| 符号输入板 | 输入法里找编程符号，或用专门的符号键盘 | 括号、下划线、引号不再难敲 |

### E.3.6 第一次在手机上跑起来（最小验证代码）

下面这段代码，**在手机编辑器里新建一个场景、根节点用 `Control`、附上脚本，然后运行**，你立刻能看到成果。这是给自己打气的第一步。

```gdscript
extends Control
## 手机版“第一个能跑的脚本”：
## 在屏幕上打印一行，并让一个 Label 显示出文字。

func _ready() -> void:
    # 第 7 章：函数。_ready 是本脚本的入口，节点就绪后自动调用。
    print("你好，我是在手机上运行 Godot！")  # 打印到输出面板

    # 第 22 章：节点引用。用代码创建一个 Label 并显示文字。
    var label := Label.new()
    label.text = "手机也能跑起来！"
    label.position = Vector2(40, 80)          # 放在屏幕靠上的位置
    label.add_theme_font_size_override("font_size", 40)  # 把字调大
    add_child(label)                          # 把 Label 挂到当前节点下
```

运行后：输出面板会打印一行字，屏幕上会出现一句"手机也能跑起来！"。**恭喜，你已经迈过最难的第一道坎。**

---

## E.4 方案 C：无引擎推演练习法（本附录最重要的方法论）

这一节是整份附录的核心。哪怕你后来有了电脑，这套方法也应该一直用下去。

### E.4.1 什么叫"脑内编译"

编程语言有个特点：**它是可以被"手动执行"的**。

程序员常说"我脑内编译一下这段代码"，意思就是：不用打开任何软件，光看代码，就能在脑子里一步步算出它会做什么。这能力听着玄，其实和你在纸上算"3 × 4 + 1 = 13"是同一回事——只不过变量名变复杂了。

> **脑内编译 = 把代码当算式，一步步在纸上/备忘录里算出来。**

### E.4.2 具体四步法

每道题都按这四步走，形成肌肉记忆：

| 步 | 动作 | 关键 |
| --- | --- | --- |
| ① 抄代码 | 把题目代码一字不差地抄到备忘录 | 抄的过程就是"读入" |
| ② 写预期 | **先别算**，凭直觉写出你觉得的结果 | 制造"预测"，逼大脑参与 |
| ③ 逐行推演 | 一行行走，写出**每一行执行后相关变量的值** | 过程比结果重要 |
| ④ 翻书对答案 | 拿你的推演结果和书里的 `# →` 对答案 | 错的那一步就是没学懂的点 |

第 ③ 步最重要。你要在备忘录里画一张**变量轨迹表**，形如：

```
行号 | 代码              | 变量变化          | 变量当前值
-----+-------------------+-------------------+--------------
1    | var a = 2 + 3 * 4 | 新建 a            | a = 14
2    | var b = a * 2     | 新建 b            | a = 14, b = 28
...
```

**能画出这张表，你就真懂了。**

### E.4.3 十道推演练习题

给每道题准备一张变量轨迹表，自己填，再看答案。题目覆盖：运算符优先级、整数除法、字符串拼接、数组索引与切片、字典取值、for 累加、while 与 break、函数默认参数与返回值、类型转换、引用与值语义。

#### 第 1 题：运算符优先级

```gdscript
var a = 2 + 3 * 4
var b = (2 + 3) * 4
var c = 10 - 4 / 2
var d = 10 % 3 + 1
# 求 a, b, c, d 的值
```

| 行号 | 代码 | 变量变化 | 变量当前值 |
| --- | --- | --- | --- |
| 1 | `var a = 2 + 3 * 4` | 新建 a | a = ？ |
| 2 | `var b = (2 + 3) * 4` | 新建 b | b = ？ |
| 3 | `var c = 10 - 4 / 2` | 新建 c | c = ？ |
| 4 | `var d = 10 % 3 + 1` | 新建 d | d = ？ |

**答案**：`a = 14`（先乘后加，3×4=12，2+12）；`b = 20`（括号优先，5×4）；`c = 8`（先除后减，4/2=2，10-2）；`d = 2`（先取余 10%3=1，再加 1）。

#### 第 2 题：整数除法

```gdscript
print(7 / 2)
print(7 % 2)
print(-7 / 2)
var x = 7.0 / 2.0
print(x)
```

| 行号 | 代码 | 变量变化 | 输出 |
| --- | --- | --- | --- |
| 1 | `print(7 / 2)` | 无 | ？ |
| 2 | `print(7 % 2)` | 无 | ？ |
| 3 | `print(-7 / 2)` | 无 | ？ |
| 4 | `var x = 7.0 / 2.0` | 新建 x | x = ？ |
| 5 | `print(x)` | 无 | ？ |

**答案**：`3`（两个整数相除，结果取整、丢弃小数）；`1`（余数）；`-3`（负数相除向零取整）；`x = 3.5`；输出 `3.5`。关键点：**只要有一个操作数是浮点数，就会做浮点除法。**

#### 第 3 题：字符串拼接

```gdscript
var s1 = "分数" + "：" + str(95)
var s2 = "行%d" % 3
var s3 = "A" + str(1 + 2)
print(s1)
print(s2)
print(s3)
```

| 行号 | 代码 | 变量变化 | 变量当前值 |
| --- | --- | --- | --- |
| 1 | `var s1 = ...` | 新建 s1 | s1 = ？ |
| 2 | `var s2 = "行%d" % 3` | 新建 s2 | s2 = ？ |
| 3 | `var s3 = ...` | 新建 s3 | s3 = ？ |

**答案**：`s1 = "分数：95"`（数字要用 `str()` 转成字符串才能拼）；`s2 = "行3"`（`%d` 占位符填入整数）；`s3 = "A3"`（先算 `1 + 2 = 3`，再转字符串拼接）。

#### 第 4 题：数组索引与切片

```gdscript
var arr = [10, 20, 30, 40, 50]
var a = arr[0]
var b = arr[arr.size() - 1]
var c = arr.slice(1, 3)
print(a, b, c)
```

| 行号 | 代码 | 变量变化 | 变量当前值 |
| --- | --- | --- | --- |
| 1 | `var arr = [...]` | 新建 arr | arr = [10,20,30,40,50] |
| 2 | `var a = arr[0]` | 新建 a | a = ？ |
| 3 | `var b = arr[arr.size() - 1]` | 新建 b | b = ？ |
| 4 | `var c = arr.slice(1, 3)` | 新建 c | c = ？ |

**答案**：`a = 10`（下标从 0 开始）；`b = 50`（`size()-1` 是最后一个下标）；`c = [20, 30]`。切片要点：**`slice(起, 止)` 含起不含止**，所以取下标 1、2，不取 3。

#### 第 5 题：字典取值

```gdscript
var d = {"hp": 100, "mp": 50}
var a = d["hp"]
var b = d.get("lv", 1)
d["hp"] = 80
print(a, b, d["hp"])
print(d.has("mp"))
```

| 行号 | 代码 | 变量变化 | 变量当前值 |
| --- | --- | --- | --- |
| 1 | `var d = {...}` | 新建 d | d = {hp:100, mp:50} |
| 2 | `var a = d["hp"]` | 新建 a | a = ？ |
| 3 | `var b = d.get("lv", 1)` | 新建 b | b = ？ |
| 4 | `d["hp"] = 80` | 改 d | d = {hp:80, mp:50} |

**答案**：`a = 100`；`b = 1`（**键不存在时返回默认值**，这是 `get` 的用处）；`d["hp"] = 80`（被改写）；`d.has("mp")` 输出 `true`。

#### 第 6 题：for 循环累加

```gdscript
var sum = 0
for i in range(1, 5):
    sum += i
print(sum)
```

| 行号 | 代码 | 变量变化 | 变量当前值 |
| --- | --- | --- | --- |
| 1 | `var sum = 0` | 新建 sum | sum = 0 |
| 2 | 第 1 圈 i=1 | sum += 1 | sum = ？ |
| 3 | 第 2 圈 i=2 | sum += 2 | sum = ？ |
| 4 | 第 3 圈 i=3 | sum += 3 | sum = ？ |
| 5 | 第 4 圈 i=4 | sum += 4 | sum = ？ |

**答案**：`sum = 10`（1+2+3+4）。关键点：**`range(1, 5)` 含 1 不含 5**，只循环 1、2、3、4 四次。

#### 第 7 题：while 循环与 break

```gdscript
var n = 0
while true:
    n += 2
    if n >= 6:
        break
print(n)
```

| 圈次 | n 的变化 | 条件 `n >= 6` | 结果 |
| --- | --- | --- | --- |
| 第 1 圈 | n: 0 → 2 | 否 | 继续 |
| 第 2 圈 | n: 2 → 4 | 否 | 继续 |
| 第 3 圈 | n: 4 → ？ | ？ | ？ |

**答案**：`n = 6`。第 3 圈 n 变成 6，条件成立，`break` 跳出循环。关键点：**`break` 会立刻结束整个循环**，循环体后半段和后续圈都不再执行。

#### 第 8 题：函数默认参数与返回值

```gdscript
func add(a: int, b: int = 10) -> int:
    return a + b

print(add(5))
print(add(5, 1))
```

| 行号 | 调用 | 参数 | 返回值 |
| --- | --- | --- | --- |
| 1 | `add(5)` | a=5, b=10（用默认值） | ？ |
| 2 | `add(5, 1)` | a=5, b=1 | ？ |

**答案**：`15`（5 + 默认值 10）；`6`（5 + 1）。关键点：**默认参数不传就用默认值**，传了就用传入值覆盖。

#### 第 9 题：类型转换

```gdscript
var a = int("42")
var b = str(3.9)
var c = float("2.5")
var d = int(3.9)
print(a, b, c, d)
```

| 行号 | 代码 | 变量变化 | 变量当前值 |
| --- | --- | --- | --- |
| 1 | `var a = int("42")` | 新建 a | a = ？ |
| 2 | `var b = str(3.9)` | 新建 b | b = ？ |
| 3 | `var c = float("2.5")` | 新建 c | c = ？ |
| 4 | `var d = int(3.9)` | 新建 d | d = ？ |

**答案**：`a = 42`（字符串转整数）；`b = "3.9"`（浮点转字符串）；`c = 2.5`（字符串转浮点）；`d = 3`。关键点：**`int()` 转浮点数是"截断"，不是四舍五入**，3.9 变 3。

#### 第 10 题：引用与值语义

```gdscript
var a = [1, 2]
var b = a
b.append(3)
print(a)

var x = 1
var y = x
y += 1
print(x)
```

| 行号 | 代码 | 变量变化 | 变量当前值 |
| --- | --- | --- | --- |
| 1 | `var a = [1, 2]` | 新建 a | a = [1,2] |
| 2 | `var b = a` | 新建 b | b = ？ |
| 3 | `b.append(3)` | 改 b | b = ？，a = ？ |
| 4 | `var x = 1` | 新建 x | x = 1 |
| 5 | `var y = x` | 新建 y | y = 1 |
| 6 | `y += 1` | 改 y | y = 2，x = ？ |

**答案**：数组是**引用语义**——`b = a` 只是让 b 指向同一个数组，`b.append(3)` 后打印 `a` 得到 `[1, 2, 3]`；而整数是**值语义**——`y += 1` 只改了 y 自己的副本，打印 `x` 仍是 `1`。关键点：**"赋值后改一个，另一个会不会跟着变"是判断引用/值语义的经典手法。**

### E.4.4 为什么这套练法有效

运行和推演，是两种完全不同的训练：

- **真跑一次**：你只看到**最后结果**。中间过程一笔带过，你甚至可能因为"结果对了"而产生误判——刚巧蒙对也是一种"对"。
- **推演一次**：你写了每一行的变量值。**过程被完整暴露**，任何一步算错都藏不住。你不但知道了结果，还知道了"为什么是这个结果"。

打个比方：运行像看别人做菜端上桌，你只看到成品；推演像自己站在灶台前，每一步火候、每一勺盐都得自己拿主意。**学做菜当然要看成品，但真正学会是在动手那一次。**

---

## E.5 【核心大表】逐章「手机可做 / 需电脑」对照表

下面是全附录最实用的一张表。38 章，一章一行，告诉你能不能练、怎么练。

**三档符号说明：**

- ✅ **手机完全可做**：纯逻辑/语法，用方案 C（备忘录推演）就够；
- 🟡 **手机可做但体验降级**：需要方案 A（Android 编辑器）或"推演代替运行"；
- 🔴 **建议有电脑再深做**：先读懂概念，动手留到有条件时。

| 章 | 标题 | 手机能否练 | 手机替代练法 |
| --- | --- | --- | --- |
| 1 | 编程到底是怎么回事 | ✅ | 备忘录用文字写清"输入→处理→输出"三步，用生活里的例子手动走一遍 |
| 2 | 环境、工具与代码规范 | 🟡 | 以读为主；在 Android 编辑器里熟悉界面、把命名规范抄成备忘录清单 |
| 3 | 变量与常量 | ✅ | 推演：给变量依次赋值，写下每一步的值轨迹表 |
| 4 | 数据类型大全 | ✅ | 推演：为每个字面量标注类型，手画一张"类型对照卡" |
| 5 | 运算符大全 | ✅ | 推演：逐题按优先级手算，重点练整数除法与取余 |
| 6 | 流程控制 | ✅ | 推演：把 if/for/while 逐行走一遍，手画分支走向图 |
| 7 | 函数 | ✅ | 推演：手算参数如何传入、返回值是什么，画一张简易调用栈 |
| 8 | 数组 | ✅ | 用备忘录写代码，自己画数组下标表推演增删结果 |
| 9 | 字典 | ✅ | 手画 key→value 表，推演增、删、改、查四种操作 |
| 10 | 类型化数组与 Packed 系列 | 🟡 | 推演类型约束规则；Packed 的内存细节留到有电脑时再看 |
| 11 | 字符串 | ✅ | 用备忘录推演拼接、格式化（%d/%s）的结果 |
| 12 | 枚举与常量组织术 | ✅ | 手写枚举，推演每个名字对应的整数值与比较结果 |
| 13 | 类的基础 | ✅ | 画"类—实例"关系图，推演某个实例的属性如何变化 |
| 14 | 继承深入 | 🟡 | 手画继承链，推演方法覆盖到底调用的是谁的版本；运行验证可延后 |
| 15 | 静态成员与工具类设计 | ✅ | 推演静态变量在所有实例间共享的那条轨迹 |
| 16 | 内部类、引用语义与值语义 | ✅ | 重点推演"赋值后改一个，另一个变不变"的差异 |
| 17 | 构造函数与对象的一生 | 🟡 | 推演 `_init` 的调用顺序；用 Android 编辑器加 print 观察真实顺序 |
| 18 | 注解大全 | 🟡 | 抄写注解并推演其作用；`@export` 一类可在 Android 编辑器的属性面板里看到 |
| 19 | 节点与场景树深入 | 🟡 | 读节点树图 + 在 Android 编辑器里手动搭一个三节点小场景 |
| 20 | 生命周期函数全解 | 🟡 | 推演 `_ready/_process` 的调用顺序；Android 编辑器里加 print 观察 |
| 21 | 信号深入 | 🟡 | 抄信号模板推演"连接→触发→回调"顺序；Android 编辑器跑最小例子 |
| 22 | 节点引用的所有姿势 | 🟡 | 推演 `@onready`/`get_node` 的路径；Android 编辑器里搭小场景验证路径 |
| 23 | 资源系统 | 🔴 | 先读概念记笔记；在 Android 编辑器里替换一次现成资源即可，自定义资源留到有电脑 |
| 24 | 输入系统 | 🟡 | 手机上用触控/按钮事件替代键盘事件；Android 编辑器里跑最小输入例子 |
| 25 | 数学与向量专题 | ✅ | 备忘录手算向量加减、点乘、归一化，画箭头示意图 |
| 26 | Tween 补间动画 | 🟡 | 抄模板代码，重点推演时间线图（起点→中点→终点），等有电脑再跑 |
| 27 | await 协程与异步 | 🟡 | 推演 `await` 的暂停点与恢复顺序；Android 编辑器里跑计时器例子 |
| 28 | 文件 JSON 与配置 | 🔴 | 先推演 JSON 的结构与层级；真正的文件读写建议有电脑再做 |
| 29 | 错误处理与调试 | 🟡 | 读报错原文并对照第 37 章报错词典；在 Android 编辑器里故意写错看报错 |
| 30 | 性能优化意识 | 🔴 | 先读思路、记下"什么操作贵"；真测帧率、真做优化留到有电脑 |
| 31 | 基础模板 | 🟡 | 抄模板结构并推演数据流；在 Android 编辑器里搭出骨架 |
| 32 | 行为模板 | 🟡 | 推演状态如何流转；在 Android 编辑器里跑一个最小行为 |
| 33 | 体验模板 | 🔴 | 读设计思路记笔记；手感、音画调优这类"要动手感受"的留到有电脑 |
| 34 | 架构模板 | 🔴 | 读架构图记笔记；真搭多系统协作结构建议有电脑再做 |
| 35 | 综合小项目 | 🟡 | 在 Android 编辑器里按步骤搭，或先只做第 1–3 步（可用本附录 E.6 的手机版替代） |
| 36 | 完整语法速查表 | ✅ | 随身翻阅，用备忘录做一张"自己的"子集速查卡 |
| 37 | 报错词典 | ✅ | 遇到报错就查；用备忘录建立"我的报错集"，记录错因与解法 |
| 38 | Godot 3→4 迁移对照 | ✅ | 推演改名规律（3D 补 3D、2D 补 2D、服务类改名），对照表格读 |

### E.5.1 统计与阅读建议

| 档位 | 章数 | 说明 |
| --- | --- | --- |
| ✅ 手机完全可做 | 17 章 | 第 1、3、4、5、6、7、8、9、11、12、13、15、16、25、36、37、38 章 |
| 🟡 手机可做但体验降级 | 16 章 | 第 2、10、14、17、18、19、20、21、22、24、26、27、29、31、32、35 章 |
| 🔴 建议有电脑再深做 | 5 章 | 第 23、28、30、33、34 章 |

读法建议：

1. **先顺着读**。38 章从第 1 章开始，🟡 的章节先用"推演 + 读代码"的方式过一遍，不用卡在"跑不起来"上；
2. **🔴 的 5 章可以先跳过**。它们分别是资源系统、文件 JSON、性能优化、体验模板、架构模板——**跳过它们完全不影响你读后面的内容**，因为后面的章节（如第 35 章项目）里会顺带用到，你到时候"回头看"也行；
3. **等你有电脑了，回头补 🔴**。这 5 章本来就属于"要动手才有意义"的，晚点做反而更顺。

---

## E.6 手机上的最小可跑项目（把第 35 章缩成手机版）

第 35 章原本是个综合小项目，但对纯手机读者来说太重了。这里给你一个**手机上能完整做完的极简版**：一个 Label 显示分数，一个按钮点一下加一分。全程纯代码，不依赖任何图片资源。

### E.6.1 怎么用（Android 编辑器）

1. 新建项目 → 新建场景，根节点选 **`Control`**；
2. 给根节点**附加脚本**，用下面这段代码替换默认内容；
3. 按运行（播放按钮），屏幕上会出现"分数：0"和一个按钮；
4. 点按钮，分数就往上加——**你的第一个作品诞生了。**

### E.6.2 完整代码

```gdscript
extends Control
## 手机版极简项目：一个 Label 显示分数，一个按钮每点一次加一分。
## 用到的知识：
##   第 3 章  变量          —— score
##   第 5 章  运算符        —— 复合赋值 +=
##   第 7 章  函数          —— _add_score / _refresh_label
##   第 11 章 字符串        —— "分数：%d" % score
##   第 18 章 注解          —— @onready（若用场景节点）
##   第 20 章 生命周期      —— _ready
##   第 21 章 信号          —— pressed.connect(...)
##   第 22 章 节点引用      —— 用变量持有 Label / Button

# 变量：分数，从 0 开始（第 3 章）
var score: int = 0

# 节点引用：用带类型的变量持有两个节点（第 22 章）
var score_label: Label
var add_button: Button

# 生命周期：_ready 在节点进入场景树后调用（第 20 章）
func _ready() -> void:
    _build_ui()
    # 信号：把按钮的 pressed 信号连到本脚本的回调函数（第 21 章）
    add_button.pressed.connect(_on_add_button_pressed)
    _refresh_label()

# 搭界面：纯代码创建 Label 和 Button，免去场景搭建
func _build_ui() -> void:
    # 标签：显示分数
    score_label = Label.new()
    score_label.position = Vector2(40, 60)          # 放在屏幕靠上位置
    score_label.add_theme_font_size_override("font_size", 48)  # 把字调大
    add_child(score_label)                          # 挂到当前节点下

    # 按钮：点了加分
    add_button = Button.new()
    add_button.text = "点我加一分"
    add_button.position = Vector2(40, 170)
    add_button.size = Vector2(240, 64)
    add_button.add_theme_font_size_override("font_size", 28)
    add_child(add_button)

# 信号回调：按钮被按下时调用（第 21 章）
func _on_add_button_pressed() -> void:
    _add_score(1)

# 函数：带默认参数，将来想一次加多分，直接传参即可（第 7 章）
func _add_score(amount: int = 1) -> void:
    score += amount            # 复合赋值（第 5 章）
    _refresh_label()

# 函数：把整数拼进字符串，再放进标签显示（第 11 章）
func _refresh_label() -> void:
    score_label.text = "分数：%d" % score
```

### E.6.3 它用到了哪些知识

| 章节 | 知识 | 在本项目里的体现 |
| --- | --- | --- |
| 第 3 章 | 变量 | `var score: int = 0` |
| 第 5 章 | 运算符 | `score += amount` |
| 第 7 章 | 函数与默认参数 | `_add_score(amount: int = 1)` |
| 第 11 章 | 字符串格式化 | `"分数：%d" % score` |
| 第 18 章 | 注解 | 类型注解 `: int` / `-> void` 与 `@onready` 同族 |
| 第 20 章 | 生命周期 | `_ready()` 入口 |
| 第 21 章 | 信号 | `add_button.pressed.connect(...)` |
| 第 22 章 | 节点引用 | 用变量持有 `Label` 与 `Button` |

### E.6.4 给你的一句话

这个项目不到 50 行，却把本书前 22 章最核心的几块知识全串起来了。**你能在手机上把它跑起来，就已经证明："只有手机"拦不住你。** 后面想加功能（比如加个"重置"按钮），照着同样的套路加就行——你已经会了。

---

## E.7 Godot 4.3 → 4.7 差异简短提醒

本书按 **Godot 4.3** 编写，而你手机上下载到的编辑器版本可能更新（比如 4.7）。不用担心，看下面几点就够。

### E.7.1 核心结论

> **GDScript 的语言语法在 4.x 系列内保持稳定。本书 95% 以上的代码，在更新版本上可以直接运行。**

版本升级主要动的是"引擎功能"和"编辑器界面"，不是"语言语法"。你学的是语言，所以稳。

### E.7.2 可能遇到差异的三类情况

| 类别 | 表现 | 你该怎么办 |
| --- | --- | --- |
| ① 后续版本**新增**功能 | 例如某些版本开始支持**类型化字典**（形如 `Dictionary[String, int]`）这类新写法 | **新增不会破坏旧代码**，放心用旧写法，新写法当作加分项 |
| ② 少数节点/属性被更名或调整 | 个别节点类型、属性名在版本间变化 | 遇到报错先去官方文档，按你的版本名称改写 |
| ③ 编辑器界面按钮位置变化 | 按钮挪了地方，但功能都在 | 认功能不认位置，找不到就用"搜索"或翻面板 |

### E.7.3 兜底流程（四步）

遇到"书里能跑、我这报错"的情况，按这四步走：

```
① 看报错原文          —— 先逐字读完，别凭感觉猜
        │
        ▼
② 查第 37 章报错词典  —— 本书专门为此写的一章
        │
        ▼
③ 查所用版本的官方文档 —— “以你实际安装的版本为准”
        │
        ▼
④ 用第 38 章迁移思路  —— 按改名规律自己推断：
                          3D 相关补 3D、2D 相关补 2D、
                          服务类做了改名（旧名→新名）
```

### E.7.4 一句明确的话

> **一切以你实际安装版本的官方文档为准。** 本书不追求覆盖每个小版本的细节，也不在这里硬编"某版本对应某 API 改动清单"——因为那样很容易出错。**不确定的，就不写；需要精确信息时，查你那个版本的文档。**

---

## E.8 附录小结

把这份附录的要点归拢成一张清单，方便你随时回看：

1. **手机能学完这本书**。差别只在"敲代码验证"变少、"读代码 + 推演"变多，这不是缺陷，是另一种训练。
2. **学习效果分三档**：手机全功能可完成（✅）、可完成约 80%（🟡）、建议有电脑再深做（🔴）。
3. **记住那句心安的话**：语法的掌握靠脑内推演，不靠反复运行；运行只验证，不负责理解。
4. **三种方案各有用途**：A 能真跑（Android 编辑器，配蓝牙键鼠）、B 只适合小片段（网页版不稳定）、C 是主线（无引擎推演）。
5. **诚实地讲**：GDScript 没有官方在线执行环境，想真跑只能用方案 A。
6. **方案 A 的关键操作**：安装 → 项目管理器新建项目 → 新建场景选根节点 → 附加脚本 → 点播放运行 → 看输出面板报错。
7. **手机写代码的技巧**：蓝牙键鼠、调大字号、横屏、关自动更正、善用剪贴板复用书中代码。
8. **推演四步法**：①抄代码 ②先写预期 ③逐行推演写变量轨迹表 ④翻书对答案。第 ③ 步最重要。
9. **十道推演练习题**覆盖：运算符优先级、整数除法、字符串拼接、数组索引与切片、字典取值、for 累加、while 与 break、函数默认参数、类型转换、引用与值语义。
10. **推演为什么有效**：真跑只看结果，推演看懂过程；蒙对也是对，推演藏不住错。
11. **逐章对照表**已给出 38 章的手机可做程度，**17 章 ✅、16 章 🟡、5 章 🔴**。
12. **🔴 的 5 章可以先跳过**（资源系统、文件 JSON、性能优化、体验模板、架构模板），不影响你读后面的章节，等有电脑再回来补。
13. **E.6 的手机版极简项目**（Label + 按钮加分，不到 50 行）能在手机上真跑，是你"第一个作品"，也是你信心的来源。
14. **版本差异不用怕**：GDScript 语法在 4.x 稳定，书中 95% 以上代码可直接跑；遇到差异按"看报错→查第 37 章→查官方文档→用第 38 章迁移思路"四步走。
15. **心态最重要**：手机会慢一点、累一点，但它不会拦住你。决定你能不能学会 GDScript 的，从来不是设备，而是**你愿不愿意每天推演几行代码**。

最后送你一句：

> **设备决定你的速度，推演决定你的深度。手机不是借口，是另一种开始。**

—— 附录 E 完 ——