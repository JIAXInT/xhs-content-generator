# 小红书内容生成器 (Xiaohongshu Content Generator)

> 基于飞书多维表格数据分析，生成小红书风格干货教程内容

## 🎯 核心特性

- **Multi-Agent 架构**：5个专业Agent流水线
- **ai_prompt 防翻译**：英文描述画面 + 中文引号 + DO NOT TRANSLATE
- **智能 IP 出现**：该出现时出现，不该出现时不出现
- **10张卡片矩阵**：cover→knowledge→list→tutorial→comparison→schedule
- **去AI味文案**：口语化/个人经历/吐槽互动
- **5维度质量审核**

## 📁 目录结构

```
├── SKILL.md                    # 主技能文件
├── README.md                   # 本说明
├── LICENSE                     # MIT
├── ip-characters/
│   ├── xiaoran.md              # 小燃角色卡（扁平矢量·硬核）
│   └── tiege.md                # 铁哥角色卡（动漫卡通·亲切）
├── references/
│   └── orchestrator-guide.md   # Orchestrator集成指南
└── examples/
    └── sample_cards_smart_ip.json  # 示例卡片（智能IP版）
```

## 🎨 ai_prompt 格式

```
A 2D flat vector illustration of a fitness infographic, Xiaohongshu style, 3:4 aspect ratio.
[英文描述画面布局、人物、背景、配色]

[CRITICAL INSTRUCTION FOR TEXT RENDERING]
Render the following text EXACTLY as provided in Chinese characters. DO NOT translate to English.
- Main Title: "中文标题"
- Bottom banner: "中文金句"
```

## 👤 IP 智能出现规则

| 卡片类型 | 是否有IP | 原因 |
|----------|---------|------|
| cover 封面 | ✅ | 展示形象 |
| knowledge 知识 | ❌ | 数据为主 |
| list 步骤 | ❌ | 清单为主 |
| tutorial 动作 | ✅ | 展示姿势 |
| comparison 对比 | ✅ | 展示对错 |
| schedule 计划 | ❌ | 表格为主 |

## 📝 版本历史

### v4.1 (2026-04-12) - 智能IP版
- IP智能出现规则：该出现时出现，不该出现时不出现
- 封面/动作/对比有IP，知识/步骤/计划无IP

### v4.0 (2026-04-12) - 最终格式
- 英文描述+中文引号+DO NOT TRANSLATE
- 知识文字80-85%，IP仅10-15%

### v3.0 (2026-04-12) - Multi-Agent
- 5个专业Agent流水线
- 10张卡片矩阵
- 参考 xhs-yunying 工作流

### v2.2 (2026-04-12) - Lovart架构
- 角色设定、行为准则、任务分级

### v1.0 (2026-04-11) - 初始版本

## 📄 License

MIT
