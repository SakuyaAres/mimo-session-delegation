# mimo-session-delegation

MiMo Desktop 跨会话委派协作技能。通过身份体系（规划 / 主管 / 实施）+ 统一登记表协调机制，将复杂任务拆解到多个会话并行或串行执行，保持主对话上下文干净。

## 特性

- **身份体系**：总控入口 / 规划 / 主管 / 实施，流水线可选子集，灵活适配不同复杂度的任务
- **拷问式规划**：集成 grilling 技能（可选），逐题对齐需求后产出实施计划；未安装时降级为内置 Question 式拷问
- **登记表协调**：统一登记表 + 交互日志 + 裁决台账 + 落盘文档，文件系统为唯一真源，不依赖消息链路
- **裁决台账**：主管裁定标「勿重开」落档 rulings.md，下游任务书裁决带入区逐项引用，决策债汇聚点一次清零
- **全自动推进模式**：opt-in 六款机制——授权横幅双通道 / 免目视放行（回执核验制）/ cron 定时巡检 / 活性探针阶梯 / 裁决台账 / 计划变更确认；附录带实战模板
- **跳数安全**：全异步解耦 + 落盘中转，从根本上规避 MiMo Desktop 会话投递的跳数限制
- **串行/并行**：默认串行，用户明确要求才并行，支持任务范围确认
- **任务清单**：主管委派前自动创建 task 任务清单，用户在侧边面板实时目视进度
- **回报保障**：回执落盘为实施完成判据（登记表由主管巡检合并）；登记表回执空位巡检兜底
- **项目接力**：跨会话半成品交接，写交接文档 + 确认接手 + 源会话收尾

## 安装

将 `SKILL.md` 和 `locales/` 复制到 MiMo Desktop 的技能目录：

```
# Windows
%USERPROFILE%\.config\mimocode\skills\session-delegation\

# macOS / Linux
~/.config/mimocode/skills/session-delegation/
```

重启 MiMo Desktop 或新建会话即可生效。

## 会话命名规则

| 身份 | 命名格式 | 示例 |
|------|---------|------|
| 规划 | `[需求名称]-规划` | `用户系统-规划` |
| 主管 | `[需求名称]-主管-模块/职责` | `用户系统-主管-前端` |
| 实施 | `[需求名称]-[身份]-[任务编号]-[任务概要]` | `用户系统-实施-01-登录模块` |
| 降级模式 | `[需求名称]-[任务概要]` | `用户系统-登录模块` |

## 协调文件结构

按需求名称聚合顶层目录，一需求一目录，多需求并行互不冲突：

```
docs/
└── {需求名称}/
    ├── registry.md      # 统一登记表（任务/会话/回报模式）
    ├── log.md           # 交互日志（append-only 审计）
    ├── rulings.md       # 裁决台账（主管裁定，「勿重开」）
    ├── plans/           # 规划产出的实施计划
    ├── tasks/           # 主管产出的任务书
    ├── receipts/        # 实施产出的回执
    └── handoff/         # 跨会话交接文档
```

## 工作流概览

```
用户 → 总控入口
        ├─ 问身份分配（Question 式选项交互）
        ├─ 确认需求名称
        ├─ 确认回报模式
        └─ 创建身份会话
              │
              ▼
           规划（可选）
        ├─ grilling 拷问对齐（可选，未装则内置模拟）
        ├─ 产出实施计划 → docs/{需求名称}/plans/
        └─ 创建主管会话
              │
              ▼
            主管
        ├─ 拆任务书 → docs/{需求名称}/tasks/
        ├─ 分配编号（01, 02, 03…）
        ├─ 创建 task 任务清单（用户面板可见）
        ├─ 创建实施会话
        ├─ 统筹调度 + 阶段汇总
        └─ 巡检回执并合并进登记表
              │
              ▼
            实施
        ├─ 按任务书落地执行
        ├─ 回执 → docs/{需求名称}/receipts/
        └─ log.md 追加收工记录
```

## 要求

- MiMo Desktop（含 MiMoCode 引擎）
- 可选增强：[grilling](https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling) 技能（规划身份的拷问对齐用它，未安装则自动降级为内置 Question 式拷问）。同源的 [grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me) 是用户手动调用版（模型不能自动触发），规划会话请用 grilling。

### 安装 grilling（可选）

从 [mattpocock/skills](https://github.com/mattpocock/skills) 获取，复制到技能目录：

```bash
git clone https://github.com/mattpocock/skills.git
cp -r skills/skills/productivity/grilling ~/.config/mimocode/skills/grilling
```

> MiMo Desktop 的技能目录：Windows 为 `%USERPROFILE%\.config\mimocode\skills\`，macOS / Linux 为 `~/.config/mimocode/skills/`。

## License

[MIT](LICENSE)
