# 英语消消乐 / ENGLISH MATCH!

像素风连连看学单词游戏：点两张相同图标即消除，消时弹出单词卡并朗读英文。

- 线上地址：https://sisyphe2620.github.io/Sophia-English-Match/
- 导出日期：2026-11-22
- 导出源：本地最新副本 `~/workspace/goals/goal-6/files/xiang-su-lian-lian-kan/index.html`
  （不是 artifact 导出。artifact 停在第 31 批 1548 词 / 200 关，直接用它会丢第 201 关。）

## 本版规模（已核对）

| 项目 | 数量 |
|---|---|
| 单词总数 | 1556 |
| 主线关卡 | 201 关 |
| 分区 | 17 区 |
| 区关合计 | 237 关 |
| 雪碧图 | 33 张（sheet-00 ~ sheet-32） |
| index.html | 1.3 MB，40515 行，md5 `61da4c88c5b3a2d64ebe8dec88d0883e` |
| 词表 | `docs/wordlist-1556.json`，1556 条 |

第 1 关 8 种 × 3 对，其余每关 12 种 × 2 对。6×8 棋盘一屏，浅色美术。

## 第 32 批（最新，已在线上）

8 个运算词，全进学习书房，主线第 201 关：

- 符号组（裸符号大字）：PLUS（加号）、MINUS（减号）、TIMES（乘号）、DIVIDED BY（除号）
- 动词组（小算式场景）：ADD（加）、SUBTRACT（减）、MULTIPLY（乘）、DIVIDE（除）
- 卡片上单词后括注词性，朗读与设置列表仍用裸词。

扩充只做牛津 3000 的名词，运算词是亲口点的例外。批 31 之后牛津名词缺口约剩 747 个，见 `docs/oxford-noun-gap-2026-11-10.json`。

## 17 区（自上而下）

智慧星空 wisdom、 人际磨坊 social、品格小院 character、情感花园 emotion、
工具工坊 tools、人物职业 people、成长小径 growth、学习书房 study、
城市街区 city、交通工具 transport、自然天地 nature、运动游乐 sport、
身体健康 health、穿搭衣橱 clothes、动植物乐园 animals、美食厨房 food、家园小屋 home。

地图 17 区全开放无锁，学完打金星。

## 玩法与设置

- 点两张相同图标消除（无路径规则），消时弹单词卡并朗读。
- 难度三档在「新开一局」时选：A1 / A2–B1 / B2（按牛津 3000 与剑桥 EVP / CEFR 分级）。
- 设置弹窗（右上角齿轮）：
  - 单词筛选：屏蔽 / 恢复、搜索、一键屏蔽满 5 级，全局生效；
  - 每关配比：全生词／生词 2/3＋熟词 1/3／一半一半／生词 1/3＋熟词 2/3（生词＝≤3 级、熟词＝4–5 级）。
- 记忆排词：艾宾浩斯＋莱特纳轻量版，词分 0–5 级，间隔下一关 / 明天 / 3 天 / 7 天 / 14 天，5 级后 30 天抽查；每关复习词优先＋8 新词；进度存浏览器 localStorage。
- 加载页是珊瑚色进度条（「大脑点亮」2026-11-18 被否决，已回滚）。

## 文件结构

```
english-match/
  index.html                 游戏本体（唯一入口，直接打开或部署）
  assets/
    icons/
      sheet-00.webp ~ sheet-32.webp   33 张雪碧图（图标都在这里）
      *.png                            单张图标源图（约 1000 张）
    zones/                   17 区图片
    map-bg.webp / map-kid.webp / slogan.webp / start-boy.webp / start-title.webp
    fly2/                    开场小图
  docs/
    wordlist-1556.json       1556 词全表（en / zh / key）
    map-zones.json           17 区词表与分区
    map-plan-2026-11-09.md   地图规划
    batch25~31-note-*.md     各批扩充记录
    abstract-noun-candidates-2026-11-09.md
    transport-audit-note-2026-11-11.md
    oxford-noun-gap-2026-11-10.json
    游戏记忆-2026-11-22.md   本聊天记忆快照
  README.md                  本文件
```

注意：`index.html` 必须和 `assets/` 放在同一目录层级下才能正常显示图标，只发单个 `index.html` 玩不了。

## 本地打开

直接双击 `index.html`，或在文件夹里起一个静态服务再用手机浏览器打开，例如：

```bash
cd english-match
python3 -m http.server 8000
# 手机浏览器打开 http://电脑IP:8000/
```

## 部署到 GitHub Pages

1. 新建一个公开仓库，把 `english-match/` 里的全部内容传到仓库根目录（`index.html` 必须在根目录）。
2. 仓库 Settings → Pages → Branch 选 main → Save。
3. 地址就是 `https://用户名.github.io/仓库名/`。
4. 改完后用 `curl` 验一下线上 `index.html` 的字节数和 md5，和本地一致才算推上去了；不要用 jsDelivr / statically 发 HTML 页（它们会按 text/plain 返回，页面只显示源码、跑不起来）。

## 图标铁律（改图前必读）

- SPRITE_POS 共 1556 条；**18–23 号是 1920 坐标，绝不反向换算**；SHEET_SIZE 18–32 全是 [1920, 960]。
- 图标渲染是 drawImage 按 SPRITE_POS 框原生尺寸裁切、不缩放。
- 修图标准做法：alpha ≥ 32 裁可见 → 等比放大到约占框 95% → 清空整格 → 居中贴回；改后用 alpha 逐像素 diff 确认只动了目标格；SPRITE_POS 一般不改。
- 图标每批 50 个先审图、认可后再换进游戏，按批拼雪碧图分批下载。

## 已修好的图标（均已上线）

- 2026-11-19 修 8 个：SWIMSUIT、LOTION、TEAPOT、BATH TUB 放大居中；RAFT、SPEEDBOAT、FERRY 垂直居中；PERFUME 放大居中（sheet-12 新 md5 `9b59667003ecb7c8c0e131321a1bdb39`）。
- 抽屉、吸管已换成他选的 A 款（抽屉单个斜侧拉开；吸管只要吸管、不要水杯，A 弯吸管）。
- **FAIRY 已结案：他确认说的是 Ferry 不是 Fairy，Ferry 已修好，不要再提修 Fairy。**

## 已被否掉的词（勿用）

SAGE、HOE、宝石类、HOOK、CANTEEN、ECLIPSE、BARN OWL、NOUGAT、乐器类、婚礼类、钓鱼类、PINATA、NOISEMAKER、STREAMER、GONDOLA、BEAVER、BADGER、SAUCEPAN、批 20 原版整组。war / death / violence 待他定。

## 待办 / 未决（不要催，等他开口）

- 选错配对的错误音效（进行中）。
- sheet-5 喇叭 / 方向盘 / 排气管三格修好上线、6 个开局图标四角非全透明，均待他手机确认。
- 分区胜利音乐问题疑为缓存或 iOS 时序（音乐已移到彩带前）。
- 2026-11-07 他提过：消消乐也要跟塔防一样有统计玩次数的功能。
