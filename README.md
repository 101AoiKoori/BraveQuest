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


---

## 一、UE5 项目文件结构建议

约定：所有内容放在 `Content/` 下，使用模块化的 **文件夹 + 前缀** 管理。

```
Content/
│
├─ Core/                       // 核心框架
│   ├─ GameModes/              // 游戏模式、规则
│   ├─ Player/                 // 玩家控制器、角色蓝图
│   └─ UI/                     // 全局UI（HUD、血条、经验条）
│
├─ Characters/                 // 所有角色相关
│   ├─ Player/                 // 玩家角色、动画蓝图
│   └─ Enemies/                // 敌人、Boss
│
├─ Systems/                    // 系统模块
│   ├─ Combat/                 // 战斗系统
│   ├─ Inventory/              // 简化背包、装备
│   ├─ Quest/                  // 任务触发器、任务数据
│   └─ AI/                     // AI 控制器、行为树
│
├─ Levels/                     // 地图与关卡
│   ├─ Village/                // 村庄（起点）
│   ├─ Wilderness/             // 野外
│   └─ Dungeon/                // 地下城/Boss关
│
├─ UI/                         // 界面
│   ├─ Widgets/                // 小组件（血条、任务提示）
│   └─ Screens/                // 全屏界面（主菜单、结算）
│
├─ Props/                      // 道具与物件
│   ├─ Weapons/                // 武器
│   └─ Items/                  // 药品、任务物品
│
├─ FX/                         // 特效资源
│   ├─ Particles/
│   └─ Materials/
│
└─ Audio/                      // 声音资源
    ├─ BGM/
    └─ SFX/
```

---

## 二、蓝图命名规则

采用 **前缀 + 功能 + 名称** 的统一规则，方便区分类型。

### 1. 蓝图前缀

| 类型                   | 前缀   | 示例                              |
| -------------------- | ---- | ------------------------------- |
| 角色 (Character)       | BP_  | BP_PlayerCharacter, BP_Boss     |
| 动画蓝图 (AnimBlueprint) | ABP_ | ABP_Player, ABP_Enemy           |
| 控制器 (Controller)     | PC_  | PC_Player, PC_EnemyAI           |
| 游戏模式 (GameMode)      | GM_  | GM_Main                         |
| 游戏实例 (GameInstance)  | GI_  | GI_Project                      |
| HUD / UI             | UI_  | UI_HUD, UI_QuestTracker         |
| 小组件 (Widget)         | WBP_ | WBP_HealthBar, WBP_Inventory    |
| 行为树 (Behavior Tree)  | BT_  | BT_EnemyMelee                   |
| 黑板 (Blackboard)      | BB_  | BB_EnemyMelee                   |
| 道具 (Item)            | BP_  | BP_Weapon_Sword, BP_Item_Potion |
| 任务 (Quest)           | Q_   | Q_MainVillage, Q_DungeonBoss    |
| 特效 (Particle)        | P_   | P_SwordSlash, P_Heal            |

### 2. 命名规则说明

- **玩家角色**：`BP_PlayerCharacter`
    
- **敌人**：`BP_Enemy_Goblin`, `BP_Boss_Dragon`
    
- **AI 控制器**：`PC_EnemyMelee`
    
- **UI 界面**：`UI_HUD`, `WBP_QuestLog`
    
- **任务**：`Q_MainVillageDefense`, `Q_DungeonClear`
    
- **关卡**：`LV_Village`, `LV_DungeonBoss`