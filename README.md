# 🌻 Mini PVZ — C++ 项目开发计划

> 用 C++ 从零制作一个简易版《植物大战僵尸》。
>
> **核心目标：通过一个真正能玩的小游戏，掌握类、对象、指针、函数、继承、多态、vector 和基础游戏开发。**

---

# 📌 1. 项目信息

| 项目     | 内容                                          |
| -------- | --------------------------------------------- |
| 项目名称 | Mini PVZ                                      |
| 编程语言 | C++                                           |
| 图形库   | SFML                                          |
| 类型     | 2D 塔防小游戏                                 |
| 地图     | 5 行 × 9 列                                   |
| 当前版本 | V0.1                                          |
| 最终目标 | 做出一个可以鼠标种植物、自动打僵尸的 Mini PVZ |

---

# 🎯 2. 我要通过这个项目学什么？

## C++ 基础

- 类 `class`
- 对象 `object`
- 函数
- 构造函数
- `private`
- `public`
- `protected`
- 指针
- 引用
- `nullptr`
- 数组
- 二维数组
- `vector`

## 面向对象

- 继承
- 虚函数 `virtual`
- `override`
- 多态

## 内存管理

前期学习：

```cpp
new
delete
```

后期学习：

```cpp
unique_ptr
```

## 项目结构

学习：

```text
.h
.cpp
#include
```

## 游戏开发

学习：

- Game Loop
- Position
- Movement
- Collision
- Input
- Render
- Delta Time
- Texture
- Sprite
- Animation
- Sound

---

# 🎮 3. 最终游戏大概是什么样？

游戏地图为：

**5 行 × 9 列**

例如：

```text
          1   2   3   4   5   6   7   8   9

Row 1     .   .   .   P   .   .   Z   .   .
Row 2     .   S   .   .   P   .   Z   .   .
Row 3     .   .   .   P   .   .   .   Z   .
Row 4     .   S   .   .   .   P   Z   .   .
Row 5     .   .   .   .   .   .   .   .   .
```

符号：

```text
P = Peashooter = 豌豆射手
S = Sunflower  = 向日葵
W = WallNut    = 坚果
Z = Zombie     = 僵尸
• = Bullet     = 豌豆子弹
. = Empty      = 空地
```

注意：

这个地图只是用来帮助理解游戏画面。

真正写程序时：

**植物和僵尸不会使用完全相同的数据结构。**

原因：

```text
植物：

🌱

固定在格子里
```

而：

```text
僵尸：

        🧟
       ←
      ←
     ←
    ←

会不断移动
```

因此：

植物适合：

```cpp
Plant* grid[5][9];
```

僵尸适合：

```cpp
vector<Zombie*> zombies;
```

子弹适合：

```cpp
vector<Bullet*> bullets;
```

---

# 🧟 4. 游戏基本规则

游戏开始：

```text
Sun = 100
```

玩家可以使用 Sun 种植植物。

例如：

```text
Sunflower   = 50 Sun
Peashooter  = 100 Sun
WallNut     = 50 Sun
```

游戏流程：

```text
玩家种植物
     ↓
Zombie 从右侧出现
     ↓
Zombie 向左移动
     ↓
Peashooter 发现同一行有 Zombie
     ↓
发射 Bullet
     ↓
Bullet 向右移动
     ↓
Bullet 击中 Zombie
     ↓
Zombie 扣 HP
```

如果：

```text
Zombie HP <= 0
```

则：

```text
Zombie 死亡
```

如果 Zombie 碰到植物：

```text
Zombie
   ↓
Plant
   ↓
停止移动
   ↓
攻击 Plant
```

如果：

```text
Plant HP <= 0
```

则植物死亡。

Zombie 继续向左移动。

如果 Zombie 到达地图最左侧：

```text
GAME OVER
```

如果消灭全部 Zombie：

```text
YOU WIN
```

---

# 🛠️ 5. 使用的软件

## 编程

推荐：

### Visual Studio

主要负责：

```text
写 C++
编译
Debug
运行游戏
```

也可以使用：

- VS Code
- CLion

---

# 🖼️ 6. 游戏 UI

使用：

## SFML

SFML 是 C++ 的 2D 多媒体库。

它负责：

- 创建窗口
- 绘制图形
- 显示 PNG
- 显示文字
- 鼠标输入
- 键盘输入
- 音效
- 音乐
- Sprite
- Texture

最终我们可以从：

```text
P -----> Z
```

变成真正的：

```text
🌱  • • • • • →  🧟
```

---

# 🎨 7. 角色绘图

如果想自己画角色：

## Krita

适合：

- Peashooter
- Sunflower
- WallNut
- Zombie
- 草坪
- UI
- 卡片
- 背景

---

如果想做像素风：

## Aseprite

适合：

- Pixel Art
- Sprite
- Sprite Sheet
- Animation

---

# ⚠️ 8. 第一版不要急着画角色

开发初期：

```text
Peashooter = 绿色圆形

Sunflower = 黄色圆形

WallNut = 棕色矩形

Zombie = 灰色矩形

Bullet = 绿色小圆
```

原因：

我们的开发顺序应该是：

```text
能运行
   ↓
逻辑正确
   ↓
结构正确
   ↓
加入 UI
   ↓
加入图片
   ↓
加入动画
   ↓
加入声音
   ↓
最后美化
```

不要：

```text
代码写了 30 行

Zombie 画了三天
```

---

# 🧱 9. 游戏主要的类

预计需要：

```text
Game

Plant
├── Peashooter
├── Sunflower
└── WallNut

Zombie

Bullet

Lawn
```

以后还可以增加：

```text
Zombie
├── NormalZombie
├── ConeZombie
└── BucketZombie
```

---

# 🌱 10. Plant

所有植物的基础类：

```cpp
class Plant
{
protected:

    int hp;
    int cost;

    int row;
    int column;

public:

    Plant(int hp, int cost);

    virtual void update();

    void takeDamage(int damage);

    bool isDead();
};
```

Plant 本身代表：

```text
所有植物共同拥有的东西
```

例如：

```text
HP
价格
位置
受伤
死亡
```

---

# 🌱 11. Peashooter

继承：

```cpp
class Peashooter : public Plant
{
    // ...
};
```

主要属性：

```text
HP
Cost
Damage
Attack Speed
Position
```

主要功能：

```cpp
shoot();
```

工作流程：

```text
Peashooter
     ↓
检查这一行有没有 Zombie
     ↓
有
     ↓
创建 Bullet
     ↓
Bullet 向右移动
```

---

# 🌻 12. Sunflower

继承：

```cpp
class Sunflower : public Plant
{
    // ...
};
```

功能：

```cpp
produceSun();
```

例如：

```text
每隔一段时间

Sun += 25
```

---

# 🥜 13. WallNut

继承：

```cpp
class WallNut : public Plant
{
    // ...
};
```

特点：

```text
HP 很高

不会攻击

不会生产 Sun
```

主要用途：

```text
🧟 → → → 🥜

Zombie 被挡住
```

---

# 🧟 14. Zombie

基础属性：

```text
HP
Attack
Speed
X
Y
```

主要函数：

```cpp
move();

attackPlant();

takeDamage();

isDead();
```

行为：

```text
没有植物
    ↓
向左移动
    ↓
发现植物
    ↓
停止
    ↓
攻击植物
    ↓
植物死亡
    ↓
继续移动
```

---

# 🟢 15. Bullet

Bullet 属性：

```text
X
Y
Speed
Damage
```

主要函数：

```cpp
move();

getDamage();
```

游戏中可能同时存在很多 Bullet。

因此：

```cpp
vector<Bullet*> bullets;
```

例如：

```text
Peashooter

🌱 ---- • ---- • ---- • ----> 🧟
```

每颗 `•` 都可以理解成一个 Bullet 对象。

---

# 🗺️ 16. Lawn

草坪：

```text
5 × 9
```

植物固定在格子中。

所以：

```cpp
Plant* grid[5][9];
```

例如：

```text
          1   2   3   4   5   6   7   8   9

Row 1     .   .   P   .   .   .   .   .   .
Row 2     .   S   .   .   .   .   .   .   .
Row 3     .   .   .   P   .   .   .   .   .
Row 4     .   W   .   .   .   .   .   .   .
Row 5     .   .   .   .   .   .   .   .   .
```

空格：

```cpp
nullptr
```

有植物：

```cpp
Plant*
```

主要函数：

```cpp
placePlant();

removePlant();

getPlant();

showMap();
```

---

# 🧠 17. 为什么使用 Plant*？

因为：

```cpp
Plant* plant;
```

可以指向：

```cpp
new Peashooter();
```

也可以指向：

```cpp
new Sunflower();
```

也可以：

```cpp
new WallNut();
```

所以：

```text
Plant*

   ├──→ Peashooter
   │
   ├──→ Sunflower
   │
   └──→ WallNut
```

这就是以后学习：

**继承 + 指针 + 多态**

的重要地方。

---

# 🎮 18. Game

`Game` 是整个游戏的大管理者。

负责：

```text
Sun

Lawn

Plants

Zombies

Bullets

Input

Collision

Game State
```

大概会有：

```cpp
class Game
{
private:

    int sun;

    Lawn lawn;

    vector<Zombie*> zombies;

    vector<Bullet*> bullets;

public:

    void run();

    void handleInput();

    void update();

    void checkCollision();

    void render();
};
```

---

# 🔄 19. Game Loop

游戏运行以后会不断循环：

```cpp
while (gameRunning)
{
    handleInput();

    update();

    checkCollision();

    render();
}
```

可以理解为：

```text
INPUT
  ↓
UPDATE
  ↓
COLLISION
  ↓
RENDER
  ↓
INPUT
  ↓
UPDATE
  ↓
...
```

这就是：

# Game Loop

---

# 🚀 20. 开发路线

整个项目分阶段完成。

不要一次全部写完。

---

# 🟢 V0.1 — Peashooter VS Zombie

## 当前任务

暂时：

```text
不做地图
不做 SFML
不做 UI
不做动画
不做 Bullet
```

只创建：

```text
Peashooter

Zombie
```

实现：

```text
Peashooter
     │
     │ attack
     ▼
  Zombie
```

运行效果：

```text
Zombie HP: 100

Peashooter attacks!

Damage: 20

Zombie HP: 80


Peashooter attacks!

Damage: 20

Zombie HP: 60


Peashooter attacks!

Damage: 20

Zombie HP: 40


Peashooter attacks!

Damage: 20

Zombie HP: 20


Peashooter attacks!

Damage: 20

Zombie HP: 0

Zombie died!
```

学习：

```text
class
object
constructor
function
private
public
```

完成：

- [ ] 创建 `Peashooter` 类
- [ ] 创建 `Zombie` 类
- [ ] Peashooter 有 Attack
- [ ] Zombie 有 HP
- [ ] Zombie 可以 `takeDamage()`
- [ ] Zombie 可以 `isDead()`

---

# 🟢 V0.2 — Lawn

加入：

```text
5 × 9
```

草坪。

学习：

```text
二维数组

指针

nullptr
```

实现：

```cpp
Plant* grid[5][9];
```

完成：

- [ ] 创建 5×9 Lawn
- [ ] 可以显示 Lawn
- [ ] 可以指定 Row
- [ ] 可以指定 Column
- [ ] 可以放植物
- [ ] 可以删除植物

---

# 🟡 V0.3 — Plant 继承系统

加入：

```text
Plant
├── Peashooter
├── Sunflower
└── WallNut
```

学习：

```text
Inheritance

virtual

override

Polymorphism
```

完成：

- [ ] 创建 Plant
- [ ] Peashooter 继承 Plant
- [ ] Sunflower 继承 Plant
- [ ] WallNut 继承 Plant
- [ ] 使用 `Plant*`

---

# 🟡 V0.4 — Bullet

创建：

```text
Bullet
```

流程：

```text
Peashooter
     ↓
   shoot()
     ↓
创建 Bullet
     ↓
Bullet Move
     ↓
Hit Zombie
```

学习：

```text
Pointer

vector

new

delete

Object Lifetime
```

完成：

- [ ] 创建 Bullet
- [ ] Bullet 可以移动
- [ ] Peashooter 可以生成 Bullet
- [ ] Bullet 可以击中 Zombie
- [ ] Zombie 扣 HP
- [ ] Bullet 击中后消失

---

# 🟡 V0.5 — Zombie Movement

Zombie 开始真正移动：

```text
START

                           🧟
                            ↓
                    🧟
                     ↓
             🧟
              ↓
       🌱   🧟
```

如果碰到 Plant：

```text
🧟 + 🌱
   ↓
停止移动
   ↓
攻击 Plant
```

完成：

- [ ] Zombie 可以生成
- [ ] Zombie 可以移动
- [ ] Zombie 可以检测 Plant
- [ ] Zombie 可以攻击 Plant
- [ ] Zombie 可以死亡

---

# 🟠 V0.6 — Sun System

玩家拥有：

```cpp
int sun;
```

例如：

```text
START

Sun = 100
```

植物价格：

```text
Sunflower   = 50

Peashooter  = 100

WallNut     = 50
```

Sunflower：

```text
每隔一段时间

Sun += 25
```

完成：

- [ ] 添加 Sun
- [ ] 种植物消耗 Sun
- [ ] Sun 不够不能种
- [ ] Sunflower 生产 Sun

---

# 🟠 V0.7 — Game Loop

创建：

```text
Game
```

让整个游戏自动运行：

```text
Plants Update

Zombie Update

Bullet Update

Collision

Remove Dead Objects
```

完成：

- [ ] Game 管理 Lawn
- [ ] Game 管理 Zombie
- [ ] Game 管理 Bullet
- [ ] 自动 Update
- [ ] 自动 Collision

---

# 🔵 V0.8 — SFML

到这里再加入：

# SFML

创建真正的游戏窗口。

最开始甚至不需要图片。

使用：

```text
绿色圆形 = Peashooter

黄色圆形 = Sunflower

棕色矩形 = WallNut

灰色矩形 = Zombie

绿色小圆 = Bullet
```

完成：

- [ ] 创建 Window
- [ ] 绘制 Lawn
- [ ] 绘制 Plant
- [ ] 绘制 Zombie
- [ ] 绘制 Bullet
- [ ] 显示 Sun

---

# 🖱️ V0.9 — Mouse UI

植物卡：

```text
┌──────────────┐
│ Peashooter   │
│    ☀ 100     │
└──────────────┘

┌──────────────┐
│ Sunflower    │
│    ☀ 50      │
└──────────────┘

┌──────────────┐
│ WallNut      │
│    ☀ 50      │
└──────────────┘
```

操作：

```text
点击植物卡
      ↓
选择植物
      ↓
点击 Lawn
      ↓
计算 Row / Column
      ↓
检查是否有植物
      ↓
检查 Sun
      ↓
创建 Plant
```

例如：

```cpp
int column = mouseX / cellWidth;

int row = mouseY / cellHeight;
```

完成：

- [ ] 鼠标点击
- [ ] 选择 Plant
- [ ] 点击 Lawn
- [ ] 计算 Row
- [ ] 计算 Column
- [ ] 种植 Plant

---

# 🏆 V1.0 — Playable Mini PVZ

V1.0 最终要求：

- [ ] 打开游戏窗口
- [ ] 显示 5×9 Lawn
- [ ] 显示 Sun
- [ ] 鼠标选择植物
- [ ] 鼠标种植物
- [ ] 种植物消耗 Sun
- [ ] Sunflower 生产 Sun
- [ ] Zombie 从右边生成
- [ ] Zombie 向左移动
- [ ] Peashooter 检测 Zombie
- [ ] Peashooter 发射 Bullet
- [ ] Bullet 向右移动
- [ ] Bullet 击中 Zombie
- [ ] Zombie 扣 HP
- [ ] Zombie 死亡
- [ ] Zombie 攻击 Plant
- [ ] Plant 死亡
- [ ] Zombie 到达左边则失败
- [ ] 消灭全部 Zombie 则胜利

全部完成：

# 🎉 MINI PVZ V1.0 COMPLETE

---

# 🎨 V1.1 — Texture

游戏逻辑完成以后，再替换素材。

项目资源：

```text
assets/
│
├── plants/
│   ├── peashooter.png
│   ├── sunflower.png
│   └── wallnut.png
│
├── zombies/
│   └── zombie.png
│
├── bullets/
│   └── pea.png
│
└── ui/
    ├── lawn.png
    └── cards.png
```

---

# 🎞️ V1.2 — Animation

Peashooter：

```text
Idle

Shoot
```

Sunflower：

```text
Idle

Produce Sun
```

Zombie：

```text
Walk

Eat

Death
```

动画：

```text
Frame 1
   ↓
Frame 2
   ↓
Frame 3
   ↓
Frame 4
   ↓
Frame 1
   ↓
...
```

---

# 🔊 V1.3 — Sound

加入：

```text
shoot.wav

plant.wav

zombie.wav

zombie_die.wav

background_music.ogg
```

---

# 📁 21. 项目文件结构

## 刚开始

只需要：

```text
MiniPVZ/
│
└── main.cpp
```

不要刚开始就创建十几个 `.cpp`。

---

## 项目变大以后

再拆：

```text
MiniPVZ/
│
├── main.cpp
│
├── Plant.h
├── Plant.cpp
│
├── Zombie.h
├── Zombie.cpp
│
├── Bullet.h
└── Bullet.cpp
```

---

## 最终

```text
MiniPVZ/
│
├── main.cpp
│
├── Game.h
├── Game.cpp
│
├── Plant.h
├── Plant.cpp
│
├── Peashooter.h
├── Peashooter.cpp
│
├── Sunflower.h
├── Sunflower.cpp
│
├── WallNut.h
├── WallNut.cpp
│
├── Zombie.h
├── Zombie.cpp
│
├── Bullet.h
├── Bullet.cpp
│
├── Lawn.h
├── Lawn.cpp
│
└── assets/
    │
    ├── plants/
    ├── zombies/
    ├── bullets/
    ├── ui/
    ├── sounds/
    └── music/
```

---

# ❓ 22. 有这么多 `.cpp`，到底运行哪个？

不是：

```text
运行 Plant.cpp

或者

运行 Zombie.cpp
```

而是所有 `.cpp` 一起组成一个程序：

```text
main.cpp ─────────┐
                  │
Plant.cpp ────────┤
                  │
Zombie.cpp ───────┼──────→ MiniPVZ.exe
                  │
Bullet.cpp ───────┤
                  │
Game.cpp ─────────┘
```

最终运行：

```text
MiniPVZ.exe
```

程序入口：

```cpp
int main()
{
    // 游戏从这里开始
}
```

所以：

> **`.cpp` 是程序的一部分，`main()` 是程序入口。**

---

# 🚫 23. V1.0 暂时不要做

为了防止项目越来越大：

- ❌ 十几种植物
- ❌ 十几种 Zombie
- ❌ 商店
- ❌ 完整 PVZ 关卡
- ❌ 联机
- ❌ 账号
- ❌ 3D
- ❌ Unreal Engine
- ❌ Unity
- ❌ 复杂存档
- ❌ 特别复杂的动画

---

# ✅ 24. V1.0 只做这些

## Plants

```text
Peashooter

Sunflower

WallNut
```

## Zombie

```text
Normal Zombie
```

## Bullet

```text
Pea
```

## Map

```text
5 × 9 Lawn
```

够了。

---

# 📚 25. 完成后应该掌握的 C++

## 基础

```cpp
class

object

function

constructor

private

public

protected
```

## 指针

```cpp
Plant*

Zombie*

Bullet*

nullptr

new

delete
```

## STL

```cpp
vector
```

## 面向对象

```text
Inheritance

Virtual Function

Override

Polymorphism
```

## 项目

```text
.h

.cpp

#include
```

## 游戏开发

```text
Game Loop

Delta Time

Position

Movement

Collision

Input

Render

Sprite

Texture

Animation

Sound
```

---

# 🗺️ 26. 项目路线图

```text
V0.1
Peashooter VS Zombie
        │
        ▼
V0.2
5×9 Lawn
        │
        ▼
V0.3
Plant 继承系统
        │
        ▼
V0.4
Bullet
        │
        ▼
V0.5
Zombie Movement
        │
        ▼
V0.6
Sun System
        │
        ▼
V0.7
Game Loop
        │
        ▼
V0.8
SFML
        │
        ▼
V0.9
Mouse UI
        │
        ▼
V1.0
Playable Mini PVZ
        │
        ▼
V1.1
Texture
        │
        ▼
V1.2
Animation
        │
        ▼
V1.3
Sound
        │
        ▼
V2.0
More Plants & Zombies
```

---

# ⭐ 27. 最重要的原则

> ## 先让它能玩，再让它好看。

不要一开始追求：

```text
“我要做得和真正 PVZ 一样。”
```

而是：

```text
第一步：

P ----attack----> Z
```

然后：

```text
第二步：

🌱 ---- • ----> 🧟
```

然后：

```text
第三步：

加入地图
```

然后：

```text
第四步：

加入窗口
```

最后才是：

```text
图片

动画

音效

UI 美化
```

---
