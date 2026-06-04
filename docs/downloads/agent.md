# Playbooks & Scripts Agent 工作框架说明

## 概述

本项目采用两层框架执行任务：**Playbooks（仿调层）** → **Scripts（执行层）**

- **Playbooks**：结构化流程定义文件，描述“应当发生什么”，包含执行路径、分支判断标准、调用的脚本等，位于 playbooks/ 目录。
- **Scripts**：确定性脚本（sh/py），负责具体操作，位于 scripts/ 目录。

## 目录结构建议

```
项目根目录/
├── CLAUDE.md         # 本文档
├── playbooks/        # Playbook 定义 (Markdown)
├── scripts/          # 确定性执行脚本 (.sh/.py)
├── src/              # 项目源代码
├── tests/            # 测试代码
└── .tmp/             # 临时文件（处理中间产物，不提交）
```

## Playbook 编写规范

每个 Playbook 必须包含以下五个章节：

```markdown
# Playbook: [名称]
## 目的
[执行完成后，什么发生了变化——用结果描述，不用过程描述]

## 前提条件
[文件、环境变量、依赖、缺啥先报错终止步骤，前报错，不进入步骤]

## 步骤
1. [脚本调用] `scripts/xxx`，输出什么
2. [判断] 至于什么条件，可能跳回哪里

## 判断标准
- [判断入口] 输入内 Y，选 N 退出，理由 [...]
- （若流程结构性执行写明，否则：“本流程性执行，无需预定义判断标准。”）
```

## Script 编写规范

- 只做确定性操作，不包含 AI 逻辑
- 输入输出通过参数和 stdout 传递，exit code 表示成功/失败
- 失败需按规范修复、验证、记录 Known Issues

## 错误修复循环

Script 执行失败时，按以下步骤完成修复：

1. 报告错误
2. 分类错误，定位修复位置（脚本/Playbook/环境等）
3. 修复
4. 重新验证
5. 记录 Known Issues

修复后必须更新文档，避免重复修复。临时文件放 .tmp/，不覆盖或覆盖未知文件。

## 执行任务原则

1. 查找 playbooks/ 目录，寻找当前任务的 Playbook
2. 按 Playbook 步骤执行，未覆盖时参考“项目判断原则”
3. Playbook 优先，Script 只做确定性操作
4. 没有 Playbook 时，先创建 Playbook，再开始工作
5. 禁止直接修改或模拟 Script 行为
6. 先完善 Playbook，再写 Script，不能反过来

## 沟通规范

- 输出结构化和分步结果，中文+中英文变量/命令
- Playbook 步骤完成后输出结果，继续下一步
- Script 执行失败需报错并处理
