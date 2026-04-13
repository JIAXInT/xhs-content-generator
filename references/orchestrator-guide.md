# Orchestrator 集成指南

## Hermes 作为 Orchestrator

就像 Lovart 的 Coco 是前台，Hermes 是你的内容工作室的 Orchestrator（调度者）。

**Hermes 的职责**：
1. 接收用户请求
2. 判断任务复杂度
3. 选择合适的 skill 处理
4. 协调多个 skill 协作
5. 交付最终结果

**Handoff 流程**：
```
用户请求 → Hermes (Orchestrator)
    ↓
判断任务类型
    ↓
选择 skill
    ├─ xiaohongshu-content-generator (内容生成)
    ├─ feishu-bitable (数据分析)
    ├─ de-ai-content (去AI味)
    └─ 其他 skill...
    ↓
执行任务
    ↓
返回结果给用户
```

## 与其他 Skill 的协作

| 场景 | 主 Skill | 辅助 Skill | 协作方式 |
|------|----------|------------|----------|
| 内容生成 | xiaohongshu-content-generator | feishu-bitable | 读取数据 → 生成内容 |
| 去AI味 | de-ai-content | xiaohongshu-content-generator | 生成内容 → 去AI味处理 |
| 批量生成 | xiaohongshu-content-generator | cronjob | 定时触发 → 批量生成 |
| 数据分析 | feishu-bitable | xiaohongshu-content-generator | 分析数据 → 推荐选题 |

## 最佳实践

1. **单一职责**：每个 skill 专注一个领域
2. **清晰接口**：skill 之间通过明确的输入/输出协作
3. **优雅降级**：一个 skill 失败不影响整个流程
4. **用户透明**：用户不需要知道内部调用了哪些 skill
5. **结果验证**：每个 skill 输出后进行验证

## 示例：完整内容生成流程

```
用户："帮我生成一篇关于三分化训练的小红书内容"

Hermes (Orchestrator):
1. 判断：这是中等复杂度任务
2. 加载 skill：xiaohongshu-content-generator
3. 执行流程：
   a. 调用 feishu-bitable 读取数据
   b. 分析数据，推荐选题
   c. 等待用户确认
   d. 生成标题、正文、8张卡片
   e. 调用 de-ai-content 去AI味
   f. 创建飞书文档
4. 返回：文档链接 + 内容预览

用户看到的：
"让我想想~ [Handoff到内容生成]
 基于你的数据，推荐选题：三分化训练全指南
 确认后我帮你生成完整内容~"
```
