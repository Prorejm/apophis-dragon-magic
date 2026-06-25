# Monline 冒险游戏 — 故事设计大纲

> 来源：Monline Wiki + 游戏源文本 + XML

## 核心概念

- **主角**：被吸入Monline世界的普通玩家（The Player）
- **反派**：Robin — 白色连帽斗篷、红色宝石项圈、迷恋变身、Monline世界的创造者
- **目标**：收集6颗圣球（Orbs），击败Robin，逃离Monline
- **核心机制**：每个错误选择都可能导致Bad End（转化为怪物娘）

---

## 角色阵容

### 可玩角色（按加入顺序）
1. **玩家（The Player）** — 主角，开始旅程
2. **PXE** — Forest Zone中的向导/系统实体，提供角色信息
3. **Mark** — Forest Zone，灰白头发，红色头巾，穿盔甲，喜欢泡菜。Forest Zone组队→Coastal Zone合作获得Orb of the Waves → 击败Sea Bishop后分头行动找其他Orbs
4. **Kim** — 海绿色头发，红色眼睛，善良聪明但脾气火爆，有点天真。**Desolate Zone入口加入**（杀死伏击玩家的僵尸），Mansion任务中成为可玩角色，一起去Desert Zone
5. **Aralu** — 金色头发，正义斗士，半吸血鬼。**Demon Zone**加入（对抗母亲Draculara）
6. **Dominic** — 棕色头发，蓝色眼睛。**Desert Zone**遇到（正在召集人手围攻金字塔），背叛玩家想获得法老力量→法老被驱逐→他留下女性化状态加入
7. **Fera** — Mythic Zone任务线

### NPC
- **Percy** — 蓝绿色帽子研究员，研究变身，在所有地带出现提供信息
- **Morgan** — 利己主义玩家，反复出现的反派/第二主角
- **Mara** — Mansion中的强化敌人，自认弱小
- **Robin** — 最终Boss

---

## 六区域故事流程

### 1. Forest Zone（森林地带）— 教程区
**关键地点**：Caste City, Forest, Breachwood, Hive, Hornet Cave, Minoh Ranch
**敌人**：Arachne, Blue Slime, Giant Frog, Holstaurus, Honey Bee, Hornet, Owl Mage
**故事线**：
- 玩家在Forest Zone醒来
- 遇到PXE（向导实体，提供信息）
- 遇到Mark（第一个同伴）
- 学习基本操作
- 探索分支：蜂巢（Hive），米诺牧场（Minoh Ranch），布雷奇伍德（Breachwood）
- 注意：本区域**没有Orb**，暗示未来需要返回
- 通过Branchwood前往Coastal Zone
- 12个Bad Ends

### 2. Coastal Zone（海岸地带）— 获取第一颗圣球
**关键地点**：Eurum City, Eurus Sea, Budan
**关键敌人**：Mermaid, Siren, Sea Bishop, Charybdis, Scylla, Kraken
**故事线**：
- 玩家+Mark组队进入
- Ritual Quest：获取Orb of the Waves（2种方式：以人类形态或以美人鱼形态完成）
- 挑战Sea Bishop
- Nereid Quest在Budan结束
- Mark和玩家胜利后**分头行动**（Mark向西，玩家向东，寻找剩余Orbs）
- 23个Bad Ends

### 3. Demon Zone（恶魔地带）— 最复杂区域
**关键地点**：Castle, Elysium Church, Elysium Coven, Dead Forest, Dark Cave, Elysium City
**故事线**：
- 复杂区域，有4个强制任务
- Castle Quest（城堡任务）
- Elysium Church（教堂任务）
- Elysium Coven（女巫集会任务）
- Succubus Quest（魅魔任务）
- 遇到**Aralu**（半吸血鬼，正义斗士，对抗母亲Draculara和魅魔妹妹）
- 击败Draculara后Aralu分道扬镳
- 38个Bad Ends

### 4. Desolate Zone（荒芜地带）— Kim加入
**关键地点**：Streets, Hospital, Mall, Mansion, Old Church, Police Station, Warehouse, Strip Club, Subway, North Pole
**敌方主题**：僵尸、狼人、机器人、魅魔化Kim
**故事线**：
- **Kim在入口加入**（杀死伏击玩家的僵尸）
- 寻找僵尸爆发的源头
- Mansion任务（遇到Mara和Morgan）
- Mad Scientist（疯狂科学家）
- Werewolf Quest（狼人任务）
- Kimccubus事件（Kim被魅魔化）
- Kim在Mansion中成为可玩角色
- 一起前往Desert Zone
- 84个Bad Ends

### 5. Desert Zone（沙漠地带）— Dominic加入/背叛
**关键地点**：Desert Expanse, Desert Town, Pyramid, Desert Underground, Volcanic Cavern, Djeso
**故事线**：
- 玩家+Kim进入Desert Zone
- 遇到**Dominic**（正在召集人手围攻金字塔）
- Dominic背叛：为获得法老Farinet的力量背叛玩家
- 击败Dominic→法老被驱逐→Dominic留下女性化状态
- Dominic在剩余部分加入队伍
- Pyramid Quest（金字塔任务）
- Curse Quest（诅咒任务）
- 41个Bad Ends

### 6. Mythic Zone（神话地带）— 最终章
**关键地点**：Shrine, Princess Quest（包含Maid, Goblin, Mystic Woods East, Deserted Cliffs子任务）, Fera Quest, Fairy Quest
**故事线**：
- 最终区域
- Princess Quest（公主任务）— 包含Maid Quest, Goblin Quest等子任务
- Fera Quest
- Fairy Quest
- 面对Robin
- 最终结局：True Ending？还是Bad End？
- 收集所有Orbs → 获得太阳神权杖 → 击败Robin → 返回现实

---

## 核心设计原则

1. **每一步都有转化风险** — 每个选择都可能通向Bad End
2. **腐化值系统** — 累积腐化影响选项可用性和结局
3. **物品系统** — 武器、护甲、消耗品、关键物品
4. **同伴系统** — Mark/Kim/Aralu/Dominic依次加入
5. **圣球收集** — 分散在各大区域，最终对抗Robin
6. **XML文本** — TFState转化描述用于Bad End叙事
7. **JSON源文本** — 用于随机遭遇和环境描述
8. **每个区域都有对应敌人和Bad Ends**

---

## 参考文件
- Wiki角色页：Robin(反派)、Mark(同伴1)、Kim(同伴2)、Aralu(同伴3)、Dominic(同伴4)
- Wiki区域页：Forest/Coastal/Demon/Desolate/Desert/Mythic
- Wiki任务页：各区域主线和支线任务
- 中文XML：TFState转化文本
- 游戏JSON：源叙事文本
