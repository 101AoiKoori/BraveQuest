## RPG 核心系统

1. **运动与战斗一体化系统**
    
    - 第三人称移动（走、跑、跳）
        
    - 基础攻击（轻攻击、重攻击）
        
    - 简单敌人 AI（追击、攻击、受击死亡）
        
2. **人物与成长系统（简化版）**
    
    - 基础属性（生命值、攻击力）
        
    - 升级或经验条（只需 1-2 个成长维度）
        
3. **装备与物品系统（简化版）**
    
    - 背包界面（只存放基础武器或药品）
        
    - 武器切换、简单道具（回血药）
        
4. **任务系统（线性）**
    
    - 主线任务流程（例如：找到 NPC → 打败敌人 → 进入关卡）
        
    - 简单触发机制（对话触发战斗/关卡进入）
        
5. **UI 系统**
    
    - 血条 / 经验条
        
    - 简单任务提示
        

---

## 游戏结构基础

1. **地图与关卡**
    
    - 1 个小型开放区域（村庄 + 野外）
        
    - 1 个地下城或副本关卡
        
2. **关卡设计**
    
    - 基础敌人分布
        
    - 最终 Boss 战
        
3. **概念与叙事**
    
    - 简单世界观设定（村庄受到威胁 → 玩家冒险 → 战胜敌人）
        
    - 最少 2-3 个关键剧情节点（开头任务、中期转折、最终对决）
        

---

## 总体结构图

|类别|内容|
|---|---|
|核心系统|运动+战斗、人物成长、装备道具、任务系统、UI|
|游戏结构|1 村庄+野外区域、1 地下城、Boss 战、简单剧情|

---

## 一、项目文件夹结构说明

打开UE5项目后，在"内容浏览器"里能看到所有文件夹，我们统一按下面的规则整理：

```
Content（这是根目录，所有东西都放这里面）
│
├─ Core/                【核心框架 - 技术组专用】
│   ├─ GameModes/       → 游戏模式文件
│   ├─ Controllers/     → 玩家控制器
│   └─ GameInstance/    → 全局数据管理
│
├─ Characters/          【角色相关】
│   ├─ Player/          → 玩家的模型、动画、材质
│   └─ Enemies/         → 敌人、Boss的模型、动画、材质
│
├─ Systems/             【游戏系统 - 技术组专用】
│   ├─ Combat/          → 战斗系统
│   ├─ Inventory/       → 背包装备
│   ├─ Quest/           → 任务系统
│   └─ AI/              → 敌人AI
│
├─ Levels/              【地图文件】
│   ├─ Village/         → 村庄地图
│   ├─ Wilderness/      → 野外地图
│   └─ Dungeon/         → 地下城地图
│
├─ UI/                  【所有界面】
│   ├─ Core/            → HUD、血条等核心UI
│   ├─ Menus/           → 主菜单、暂停菜单
│   └─ Gameplay/        → 任务提示、对话框
│
├─ Props/               【场景物品】
│   ├─ Weapons/         → 武器模型（剑、弓等）
│   ├─ Items/           → 道具模型（药水瓶、宝箱等）
│   └─ Environment/     → 环境装饰（树、石头、房子）
│
├─ FX/                  【特效】
│   ├─ Particles/       → 粒子特效（火焰、烟雾等）
│   └─ Materials/       → 特效用的材质
│
└─ Audio/               【音频文件】
    ├─ BGM/             → 背景音乐
    └─ SFX/             → 音效（脚步声、攻击音效）
```

---

## 二、文件命名规则

### 美术资源命名

#### 1. 角色模型
格式：`SM_角色名称_部位`（SM表示Static Mesh静态模型）

**示例：**
- `SM_Player_Body` - 玩家身体
- `SM_Enemy_Goblin` - 哥布林敌人
- `SM_Boss_Dragon` - Boss龙

#### 2. 动画文件
格式：`ANIM_角色_动作名`

**示例：**
- `ANIM_Player_Idle` - 玩家待机
- `ANIM_Player_Attack` - 玩家攻击
- `ANIM_Enemy_Walk` - 敌人行走
- `ANIM_Boss_Roar` - Boss咆哮

#### 3. 武器道具
格式：`SM_类型_名称`

**示例：**
- `SM_Weapon_Sword` - 剑
- `SM_Weapon_Bow` - 弓
- `SM_Item_Potion` - 药水瓶
- `SM_Prop_Chest` - 宝箱

#### 4. 环境物件
格式：`SM_Env_名称`

**示例：**
- `SM_Env_Tree_Oak` - 橡树
- `SM_Env_Rock_Large` - 大石头
- `SM_Env_House_Village` - 村庄房子

---

### 音频文件命名

#### 1. 背景音乐
格式：`BGM_场景名称`

**示例：**
- `BGM_Village` - 村庄音乐
- `BGM_Battle` - 战斗音乐
- `BGM_BossFight` - Boss战音乐

#### 2. 音效
格式：`SFX_类型_名称`

**示例：**
- `SFX_Player_Footstep` - 脚步声
- `SFX_Attack_Sword` - 剑攻击音效
- `SFX_UI_Click` - UI点击音效
- `SFX_Enemy_Hit` - 敌人受伤音效

---

### UI界面命名

格式：`UI_界面名称` 或 `Icon_图标名称`

**示例：**
- `UI_MainMenu` - 主菜单界面
- `UI_HealthBar` - 血条
- `UI_Inventory` - 背包界面
- `Icon_Sword` - 剑的图标
- `Icon_Potion` - 药水图标

---

### ✨ 特效命名

格式：`FX_效果名称` 或 `P_效果名称`（P代表Particle粒子）

**示例：**
- `FX_SwordSlash` - 剑光特效
- `P_HealEffect` - 治疗特效
- `P_Explosion` - 爆炸特效
- `FX_LevelUp` - 升级特效

---