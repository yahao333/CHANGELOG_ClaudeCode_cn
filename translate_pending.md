## 2.1.159

- 内部基础设施改进（无用户面向变更）

## 2.1.158

- Auto 模式现已支持 Bedrock、Vertex 和 Foundry 上的 Opus 4.7 和 Opus 4.8。通过设置 `CLAUDE_CODE_ENABLE_AUTO_MODE=1` 选择启用

## 2.1.157

- `.claude/skills` 目录中的插件现在自动加载，无需通过市场
- 新增 `claude plugin init <name>` 用于在 `.claude/skills` 中搭建新插件
- 为 `/plugin` 参数添加自动补全：子命令、已安装插件名称及已知市场的插件
- `claude agents`：`settings.json` 中的 `agent` 字段现对调度会话生效，可用 `--agent <name>` 覆盖
- `EnterWorktree` 现可在会话中途切换 Claude 管理的工作树
- `tool_decision` 遥测事件现包含 `tool_parameters`（bash 命令、MCP/skill 名称），当 `OTEL_LOG_TOOL_DETAILS=1` 时
- Claude 管理的工作树在 agent 结束时保持解锁，以便 `git worktree remove`/`prune` 清理它们
- 修复通过粘贴、MCP 或对话框附加的无法处理图像（零字节、损坏）导致请求崩溃而非变为文本占位符
- 修复在桌面应用、IDE 扩展或 SDK 中使用 auto 模式和 bypass-permissions 模式时出现沙盒网络权限提示
- 修复 `claude agents` 中已完成会话在空闲 subagent 仍处于停放状态或泄漏后台 shell 时不退出
- 修复 `claude agents` 按 Esc 无法取消缓慢的"opening…"操作，导致列表无响应
- 修复 `.claude/worktrees/` 下的后台 agent 工作树在 30 天作业保留清理后被孤立
- 修复睡眠/唤醒后重新附加的后台会话未告知模型正确的日期
- 修复 `claude agents` 中的选择复制在 tmux 内 `set-clipboard on` 时未到达系统剪贴板（2.1.153 回归）
- 修复 `--resume` 未报告之前 Claude Code 进程退出时正在运行的后台 subagent
- 修复 `--resume` 会话选择器在全屏模式下退出后在终端留下内容
- 修复 `--worktree` 和 `--worktree --tmux` 返回到规范仓库根目录而非当前链接的工作树
- 修复 `/model` 选择器在选定模型已是其系列中最新时显示错误的"有新版本可用"提示；固定模型行现在显示模型描述而非原始 ID
- 修复全屏模式下进行中消息文本出现字面 Markdown 标记（反引号、星号）
- 修复在启动时批准托管设置安全对话框后终端冻结
- 修复终端 UI 重绘后回溯中出现罕见的重复行
- 修复在 VS Code、Cursor 和 Windsurf 集成终端中右键粘贴重复剪贴板内容
- WSL：修复图像粘贴（`alt+v` 快捷键）、Windows 11 上的截图粘贴，并添加从 Windows 资源管理器拖拽图像的支持
- 改进长时间和恢复会话的性能，消除冗余的消息渲染重计算
- `/terminal-setup` 现禁用 VS Code/Cursor/Windsurf 集成终端中的 GPU 加速以防止文字渲染乱码
- "本周功能"积分领取状态现作为通知显示在状态区域而非提示上方的行
- `claude agents`：调度输入中的斜杠命令自动补全现支持子字符串匹配
- 移除"bash 命令将被沙盒化"启动横幅——沙盒状态仍在 `/status` 和命令被阻止时显示
- 移除"/ide for …"启动提示 toast
- [IDE] 修复点击 Stop 时如果后台 subagent 正在运行实际上并未停止它
- [VSCode] 修复 Opus 4.8 上快速模式指示器不出现
- 在工作流触发关键字后立即按退格键现在关闭工作流请求（与 alt+w 相同）而非删除字符
- 在 /config 中新增"工作流关键字触发"设置，阻止提示中的单词"workflow"触发动态工作流

## 2.1.156

- 修复使用 Opus 4.8 时 thinking 块被修改导致 API 错误的问题

## 2.1.154

- Opus 4.8 来袭！现在默认为高努力 · `/effort xhigh` 应对最困难的任务
- 推出动态工作流：要求 Claude 创建工作流，它可以在后台编排数十到数百个 agent 的工作，让你承担更大、更复杂的任务。运行 `/workflows` 查看你的运行
- Opus 4.8 上的快速模式现以一小部分之前的成本提供：2 倍标准速率获得 2.5 倍速度
- 精简系统提示现已成为除 Haiku、Sonnet 和 Opus 4.7 及更早版本之外所有模型的默认设置
- Claude 现在将多选题提示留给自己真正无法做出的决定，而非在已有足够上下文继续时提问
- `/simplify` 现运行纯清理审查（重用、简化、效率、高度）并应用修复，而非运行完整的 `/code-review --fix` bug 搜索审查
- 将 `/effort` 滑块标签从"速度"/"智能"重命名为"更快"/"更聪明"以提高清晰度
- `claude agents`：输入 `! <command>` 作为后台会话运行，你可以附加和分离。也可作为 `claude --bg --exec '<command>'` 使用
- `claude agents`：`/logout` 现退出登录而非发送到后台会话
- `←←` 打开 agent 视图现支持 Bedrock、Vertex、Foundry 和禁用遥测
- Chrome 中的 Claude：通过 `/chrome` →"选择浏览器…"选择要使用的已连接浏览器，或在浏览器操作运行时有多个连接时在聊天中选择
- 插件现可在 `plugin.json` 或市场条目中声明 `defaultEnabled: false`；通过 `/plugin` 或 `claude plugin enable` 启用。已启用插件的依赖仍自动启用
- `/plugin` Discover 标签现固定其相关性信号与当前目录匹配的插件，标注"建议用于此目录"
- 流式工具执行现已始终启用，包括在遥测禁用或 Bedrock/Vertex/Foundry 上（之前在功能标志后面）
- Stdio MCP 服务器子进程现可在其环境中接收 `CLAUDE_CODE_SESSION_ID` 和 `CLAUDECODE=1`
- `claude mcp list`/`get` 现将未批准的 `.mcp.json` 服务器显示为 `⏸ 待批准` 而非在输出被管道化时自动批准并连接
- `/remote-control` 自动补全现显示"断开远程控制"当远程控制已激活时
- 在 `/claude-api` skill 中添加 Claude Opus 4.8 支持和 4.7 → 4.8 迁移指南
- 弃用 `CLAUDE_CODE_OPUS_4_6_FAST_MODE_OVERRIDE`（将于 6 月 1 日移除）。要在 Opus 4.6 上使用快速模式，通过 `/model claude-opus-4-6[1m]` 切换然后 `/fast on`
- 改进 auto 模式分类器的数据泄露检测，特别是仓库内容批量传输
- 修复 `rm -rf $HOME` 在 `HOME` 有尾随斜杠时未被阻止为危险路径
- 修复同一会话中沙盒 vs 非沙盒 Bash 命令的 `$TMPDIR` 解析到不同目录
- 修复 `claude agents` 中 Claude Code 主题与终端背景不匹配时突出显示行文本不可读
- 修复后台 agent 完成通知在某些 1M 上下文模型上触发过早的"上下文不足"行为
- 修复在计划的 `/command` 触发时后台会话分类器丢失用户目标
- 修复固定后台会话在 Claude Code 更新后每分钟重新生成，导致重复的 agent 启动通知和空闲时进程轮换
- 修复处于"blocked"、"running"或"working"状态的后台会话在空闲宽限期后不退出
- 修复后台会话中的 subagent 绕过工作树隔离防护并写入共享 checkout
- 修复在守护进程退出后在 macOS 上孤立 `claude --bg-pty-host` 进程以 100% CPU 旋转
- 修复选项对话框中分隔符下方显示的选项的数字快捷键不工作
- 修复 `worktree.baseRef: "head"` 在调度 subagent 或从链接工作树内调用 `EnterWorktree` 时解析为主 checkout 的 HEAD 而非当前工作树的 HEAD
- 修复当前一行恰好在终端宽度处结束时包装行上的 stray 前导空格
- 修复 VS Code 中间歇性终端渲染损坏——通过限制 thinking 旋转动画产生的不同颜色数量来修复
- 修复计划文件名在计划模式提示以粘贴图像或文本开头时包含 `[Image #N]` / `[Pasted text #N]` 占位符
- 修复着色工具输出上的 phantom 展开/点击提示：适合屏幕的短 ANSI 颜色行不再显示"ctrl+o 展开"提示
- 修复单个无效的 `allowedMcpServers`/`deniedMcpServers` 条目在托管设置中丢弃所有托管设置策略；坏条目现被丢弃并带有 `claude doctor` 警告
- 修复在不支持 effort 参数的模型上 API 400 错误当 `CLAUDE_CODE_ALWAYS_ENABLE_EFFORT` 设置时
- Windows：修复因 `claude.exe` 被占用导致更新失败显示通用错误而非告诉你关闭其他会话并重试
- 从快捷方式帮助面板中移除过时的"& for background"提示
- [VSCode] Auto 模式不再需要 bypass-permissions 设置出现在模式选择器中，并且在新会话屏幕上首次激活时显示解释 auto 模式的可关闭通知
- 修复提示下方仅在工作流运行时显示任务面板显示 stray 不可选的"main"行
- 修复 MCP 服务器有长或多行工具名称或长描述时 `/mcp` 工具列表和工具详情渲染
- 修复 auto 模式打开时 `/model` 选择器在快速模式开启时未显示 Default 选项的快速模式定价（针对 API 即用即付用户）
- 修复 auto 模式在安全分类器在推理过程中耗尽输出令牌时错误阻止带有"could not evaluate this action"的操作

## 2.1.153

- 在 `github`/`git` 插件 marketplace 源中添加 `skipLfs` 选项以在克隆和更新期间跳过 Git LFS 下载
- Claude Code 现已在 npm 全局安装无法自动更新时显示一次性通知；`/doctor` 列出修复方法
- 状态行命令现接收 `COLUMNS` 和 `LINES` 环境变量，以便脚本可以调整输出宽度以适应终端
- `claude agents`：调度输入中的自动补全现建议原生斜杠命令和捆绑 skill，而不仅仅是项目 skill
- `claude agents`：PR 列现显示单个 PR 的 `PR #N` 或多个 PR 的 `N PRs`
- `claude doctor` 现显示上次更新尝试的结果
- 将 MCP 服务器和连接器的独立"需要身份验证"启动通知合并为一条消息
- macOS：后台 agent 现作为"Claude Code"出现在隐私与安全中，并在升级时保持其权限授予
- 修复没有可选 GET SSE 流重新连接循环的状态ful MCP 服务器在 `tools/list` 上重新连接（在 v2.1.147 中回归）
- 修复自定义 API 网关可能收到用户的 Anthropic OAuth 凭证而非网关自己的令牌的回归
- 修复 subagent (Agent 工具) frontmatter MCP 服务器忽略 `--strict-mcp-config`、`--bare`、远程模式、企业托管 MCP 配置和托管设置 MCP 服务器允许/拒绝策略
- `--strict-mcp-config` 不再从明确传递的 agent 定义（`--agents` / SDK `agents`）中剥离内联 `mcpServers`，被阻止的 subagent MCP 服务器现显示可见警告
- 修复 Windows PowerShell 安装程序报告"安装完成！"而实际安装失败
- 修复 `claude update` 为 npm 安装安装最新版本而非配置的发布频道版本
- 修复在有许多已存储会话的机器上通过转录文件路径恢复会话时过度内存使用（多个 GB）
- 修复 `claude agents` 和 `claude --bg` 在由不支持二进制接管支持的旧守护进程启动时运行，即使之后升级
- 修复 CLI 在 stream-json 模式中 stdin 未以 EOF 关闭时可能无法退出，导致陈旧会话标记
- 修复 Claude 响应中格式错误的 `file://` 链接在终端中不可点击
- 修复 `claude --help` 在小于 92 列的终端上渲染未换行输出
- 修复 MCP 工具进度通知在折叠工具视图中不渲染
- 修复具有 `subagent_type: 'claude'` 的 `Agent` 工具在未记录临时工作树中运行，可能静默丢弃写入 gitignored 路径的输出
- 当 Claude 正在响应时 `/bg` 现在继续在后台会话中响应而非丢弃
- 修复后台会话中任务运行时 `/btw` 键盘快捷键无响应（回归）
- 修复后台会话写入 temp 文件到 `$CLAUDE_JOB_DIR` 触发"敏感文件"权限提示
- 修复恢复工作目录被删除的后台 agent 显示截断的堆栈跟踪而非清晰错误消息
- 修复 `EnterWorktree` 在后台会话中不能立即使用（之前需要 `ToolSearch`）
- 修复 iTerm2/Terminal.app 中 `cmd+k` 不重绘附加的后台会话
- 修复在 Windows 上附加后台会话中 IME 候选窗口显示在屏幕底部而非输入插入符号旁边
- 修复从 256 色仅终端附加后 agent 已渲染文件 diff 时背景色渗透
- 修复 `/copy` 和选择复制在附加到 tmux 内的后台会话时静默失败更新系统剪贴板
- 修复在启用远程控制时打开 `claude agents` 在退出后在代码标签上留下僵尸会话条目
- 修复后台会话中的 `/rename` 未立即更新会话横幅
- 修复 Windows 更新回滚：如果 Windows 更新失败，Claude Code 现通过复制恢复原始可执行文件并告诉你如何恢复
- [VSCode] 修复在 Windows 上关闭 VS Code 时 Claude Code 进程未干净关闭，导致虚假的"非干净退出"报告和孤立的 MCP 服务器
- `/model` 现保存你的选择作为新会话的默认值（与 IDE 匹配）。在选择器中按 `s` 仅切换当前会话的模型
- 如果你自定义了 `modelPicker:setAsDefault` 键绑定，在 keybindings.json 中将其重命名为 `modelPicker:thisSessionOnly`（`d` 操作被 `s` 替换）

## 2.1.152

- `/code-review --fix` 现在在审查后将其发现应用到你的工作树，呈现重用、简化和效率建议；`/simplify` 现调用 `/code-review --fix`
- Skill 和斜杠命令现可在 frontmatter 中设置 `disallowed-tools` 以在该 skill 激活时从模型中移除工具
- 新增 `/reload-skills` 命令以在不重启会话的情况下重新扫描 skill 目录
- `SessionStart` hooks 现可返回 `reloadSkills: true` 以重新扫描 skill 目录，使 hook 安装的 skill 在同一会话中可用
- `SessionStart` hooks 现可通过 `hookSpecificOutput.sessionTitle` 在启动和恢复时设置会话标题
- 新增 `MessageDisplay` hook 事件，允许 hooks 在显示助理消息文本时转换或隐藏
- 新增 `pluginSuggestionMarketplaces` 托管设置：管理员可以允许列出其插件可能通过上下文感知提示建议的组织市场
- `claude plugin marketplace remove` 现接受 `--scope user|project|local` 以与 `marketplace add`、`install` 和 `uninstall` 对称
- Claude Code 现当主模型未找到时切换到你配置的 `--fallback-model` 完成会话剩余部分，而非使每个请求失败
- Auto 模式不再需要选择同意

## 2.1.150

- 内部基础设施改进（无用户面向变更）