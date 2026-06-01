# Claude Code 更新日志 (中文版)

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

# Claude Code 更新日志 (中文版)

## 2.1.150

- 内部基础设施改进（无用户面向变更）

## 2.1.149

- `/usage` 现在显示按类别细分的使用量排行——skills、subagents、插件和各 MCP 服务器的费用
- `/diff` 详情视图现在支持键盘滚动（方向键、`j`/`k`、`PgUp`/`PgDn`、`Space`、`Home`/`End`）
- Markdown 输出现在渲染 GFM 任务列表复选框（`- [ ] 待办` / `- [x] 完成`）而非普通项目符号
- 企业版：新增 `allowAllClaudeAiMcps` 托管设置，用于加载 claude.ai 云 MCP 连接器配合 `managed-mcp.json` 使用
- 修复 PowerShell 权限绕过：内置 `cd` 函数（`cd..`、`cd\`、`cd~`、`X:`）在未检测到的情况下更改工作目录，使后续命令可读取工作区外的文件
- 修复 git worktree 中的沙盒写入白名单覆盖整个主仓库根目录而非仅共享的 `.git` 目录（`hooks/` 和 `config` 除外）
- 修复 PowerShell 前缀/通配符允许规则（例如 `PowerShell(dotnet.exe build *)`）未预先批准原生可执行文件和脚本
- 修复权限分析中的间隙：解析器在 `cd`/`pushd`/`popd` 时信任 `PWD`/`OLDPWD`/`DIRSTACK` 的过时变量跟踪值
- 修复 Bash 工具中的 `find` 在大型目录树下耗尽 macOS 系统文件/vnode 表导致主机崩溃
- 修复托管设置审批对话框在启动时接受后终端冻结的问题
- 修复工作树无实际变更时 `/ultraplan` 和远程会话创建失败并提示"无法捕获未提交变更"
- 修复 `otelHeadersHelper` 在脚本路径包含空格时静默失败；helper 失败现已在 `/doctor` 和调试日志中报告
- 修复 thinking 旋转动画在工具调用期间及新的 thinking 开始时保持琥珀色
- 修复折叠的 Bash 输出对多行短行的输出报告错误的隐藏行数
- 修复斜杠命令参数提示在提示溢出输入框时剪裁尾部已输入字符
- 修复 Tab 补全 skill 后（其 frontmatter `name:` 与目录名不同）参数提示和渐进式参数建议不出现
- 修复状态栏显示用户的基线 `/effort` 设置而非 skill/agent `effort:` frontmatter 应用的努力级别
- 修复 Ctrl+O 转录视图在打开时刻冻住而非跟踪新消息
- 修复编辑已调用的提示历史条目后在用方向键上下导航时丢失编辑内容
- 修复 `/config` 退出摘要在切换无关设置时报告自动压缩和主题的幻象变更
- 修复 `/insights` 在缓存的会话元数据文件缺少可选字段时崩溃
- 修复输入缺失的格式错误的 PowerShell 和 History 工具调用在转录折叠中被误分类为读取
- 修复从 claude.ai 或 Claude 移动应用重命名远程控制会话时未更新 `claude --resume` 的本地会话名
- 修复刚提交的提示可能在上箭头历史中重复出现的竞争条件
- 修复在全屏模式下点击"跳到底部"药丸未立即关闭它
- 改进 `/feedback` 报告以包含上下文压缩前发生的对话，使长会话中早期的问题更容易分类

## 2.1.148

- 修复部分用户所有命令返回退出码 127 的问题（2.1.147 引入的回归）

## 2.1.147

- 固定后台会话（`claude agents` 中的 `Ctrl+T`）现在空闲时保持活动、在 Claude Code 更新时原地重启、仅在非固定会话之后才在内存压力下释放
- 将 `/simplify` 重命名为 `/code-review`。现在按选定的努力级别报告正确性 bug（例如 `/code-review high`）；传入 `--comment` 可将发现作为内联 GitHub PR 评论发布。旧的清理修复行为已移除
- 改进自动更新程序：重试临时网络失败、报告具体错误类别和操作系统错误代码、显示更新失败时的当前版本
- 改进大型文件编辑的 diff 渲染性能
- 提示历史不再记录连续重复条目——用上箭头调出提示并再次提交不会添加另一份副本
- 修复企业版登录限制（`forceLoginOrgUUID` 和 `forceLoginMethod` 托管设置）未对第三方提供商和 API 密钥会话强制执行
- 修复 `!` 命令输出中的 `&` 显示为 `&amp;`，导致在无头机器上无法从 `gcloud auth login` 等命令复制 URL
- 修复无头/SDK 模式下未知斜杠命令静默无响应——现在显示错误消息
- 修复 `/help` 在非全屏模式的小型终端上渲染损坏的标签页标题且每页只显示一条命令
- 修复 shell 快照丢弃以单下划线开头的用户函数，破坏引用这些函数的别名
- 修复在 `tools:` frontmatter 中声明多个 `Agent(...)` 类型的插件 agent 只保留最后一个条目
- 修复 hook `if` 条件如 `PowerShell(git push*)` 从不匹配——只有 `PowerShell(*)` 有效
- 修复 PowerShell 工具丢失依赖默认格式化器的命令输出
- 修复：在 Windows 上，"是，且不再询问"对 PowerShell 脚本调用现在写入在后续运行中实际匹配的规则
- 修复通过 winget 或 Microsoft Store 安装的 `pwsh` 在 Windows 上以退出码 1 失败
- 修复 `/effort` 打开时滑块位于错误级别——现在从当前努力级别开始
- 修复分页 MCP 服务器时第 1 页之后的资源、模板和提示丢失
- 修复 Windows Terminal 上附加后台会话中的全屏频闪
- 修复：在 Windows 上移除后台作业工作树不再跟随 NTFS 链接到主仓库
- 修复 `/background` 拒绝唯一输入是 skill 或自定义斜杠命令的会话
- 修复自动模式在用户或 skill 明确依赖 `AskUserQuestion` 时抑制该功能；自动模式分类器现在将用户答案视为意图信号
- 修复 `/theme"新建自定义主题"和颜色编辑器对话框对 Esc 无响应
- 修复通过 Agent SDK 运行的流式会话结束时的未捕获异常
- 修复在 Windows 上等待滚动稳定时的罕见挂起
- 修复 Windows 上后台会话结果包含宽字符（CJK）时 agent 视图列表中的过时和重复行
- 修复粘贴的文本作为无法读取的 `[Pasted text #N]` 占位符而非实际内容传递给 agent
- 修复 `claude plugin details` 和 `/plugin` 中的插件组件计数在插件清单列出的路径与其默认目录重叠时翻倍
- 修复后台会话重新提示已用"不再询问"授予的工具权限
- 修复 GNOME Terminal 右键和中键粘贴未插入文本
- 修复 `CLAUDE_CODE_SUBAGENT_MODEL` 未应用到 agent 团队产生的队友进程
- 修复后跟 Tab 或换行的斜杠命令被当作未知命令
- 修复 `/plugin`、`/status`、`/mobile`、`/sandbox` 和 `/permissions` 菜单中的多个间距和布局问题
- 修复剥离图像提示模型重复读取已不存在的媒体

## 2.1.145

- 新增 `claude agents --json` 以 JSON 格式列出实时 Claude 会话，用于脚本化（tmux-resurrect、状态栏、会话选择器）
- 在 `claude_code.tool` OTEL 跨度中新增 `agent_id` 和 `parent_agent_id` 属性，修复跟踪父子关系使后台 subagent 跨度嵌套在调度 Agent 工具跨度下
- 状态栏 JSON 输入现在在检测到时包含 GitHub 仓库和 PR 信息
- `/plugin` 发现和浏览屏幕现在在安装前显示插件的命令、agent、skills、hooks 和 MCP/LSP 服务器
- `claude agents` 终端标签标题现在显示等待输入计数，以便在 alt-tab 切换时知道 agent 需要关注
- 斜杠命令和 @-提及建议列表现在在全屏模式下支持鼠标悬停和点击
- Stop 和 SubagentStop hook 输入现在包含 `background_tasks` 和 `session_crons` 字段
- 修复权限提示绕过：Bash 命令中对非白名单环境变量的裸露变量赋值被自动批准
- 修复 MCP 提示斜杠命令在省略必需参数时显示原始服务器验证错误——现在命名缺失参数并显示预期用法
- 修复终端调整大小或重新获得焦点后旋转动画和已用时间显示冻结
- 修复跨项目恢复提示在默认 Windows PowerShell 5.1 中失败——Windows 现在使用 `;` 作为命令分隔符
- 修复 agent 视图回复窗格中语音按键通话不工作
- 修复同时创建多个任务时任务列表随机排序
- 修复市场已安装时"安装 Anthropic 市场失败"横标显示过时
- 修复会话中运行 `gh pr create` 等其他更改 PR 状态的命令后页脚 PR 徽章未立即更新
- 修复具有非 ASCII 名称的 Agent Teams 队友因无效 header 编码导致每次 API 调用失败
- 修复 `/review` 使用已弃用的 `projectCards` GraphQL 查询在具有经典项目的仓库上出错
- 修复 `claude plugin validate` 未标记指向文件而非目录的 `skills:` 条目——现在建议父目录
- 修复使用 `context: fork` 的 skill 可能反复调用自身而非运行的无限循环
- 改进 Read 工具在全文件读取超出令牌限制时返回带"部分视图"通知的截断首页而非硬错误

## 2.1.144

- 新增 `/resume` 对后台会话的支持——通过 `claude --bg` 或 agent 视图启动的会话现在与交互式会话一起出现，标记为 `bg`
- 新增后台 subagent 完成通知中的已用时长（例如"Agent 完成 · 3小时 2分钟 5秒"）
- `/plugin` 浏览和发现窗格现在显示插件最后更新时间
- `/model` 现在只更改当前会话的模型；按 `d` 在模型选择器中设置新会话的默认模型
- 将"额外使用量"重命名为"使用量积分"；`/extra-usage` 现为 `/usage-credits`（旧名称仍可用）
- 修复当 `api.anthropic.com` 不可达时启动挂起长达 75 秒（ captive portal、防火墙、VPN 问题）——side-channel API 调用现在 15 秒后超时
- 修复错过窗口调整大小事件后终端输出乱码（例如拖动 VS Code 分屏分隔符）——现在在下一帧自愈而非需要 Ctrl+L
- 修复可能在超长会话中出现的渐进式终端显示损坏（过时/乱码字形）——仅在终端调整大小或重启时清除
- 减少 VS Code 中的终端渲染故障——减少旋转动画颜色数量
- 修复项目位于全磁盘访问保护文件夹下时 macOS 后台会话崩溃并显示"启动前退出 1"（2.1.143 回归）
- 修复读取图像扩展名与内容不匹配的文件（例如保存为 .png 的 HTML）时的无法恢复对话——现在回退到文本
- 减少搜索期间的虚假工具错误：`head`/`tail` 文件视图现在满足读取前编辑检查，`egrep`、`fgrep`、`git grep` 或 `git diff` 的"无匹配"结果（退出码 1）不再报告为命令失败
- 修复在工作树中或部分后台会话中进入后 `/branch` 失败并提示"无对话可分支"
- 修复在 AskUserQuestion 备注字段中按 Escape 终止回合而非返回答案选择
- 修复通过 IDE 模型选择器或 `applyFlagSettings` 在启动后更改的模型选择未应用
- 恢复的会话保留其使用的模型而非拾取其他会话的 `/model` 选择
- 修复 Bedrock 和 Vertex 用户无法从 `/model` 选择器中选择"Opus (1M 上下文)"（v2.1.129 回归）
- 修复具有 `forceLoginMethod` 和 `forceLoginOrgUUID` 设置的用户远程会话登录失败并提示"无法访问此组织"
- 修复具有分页 `tools/list` 响应的 MCP 服务器只返回第一页、静默丢弃后续工具
- 修复具有不支持的 MIME 类型（例如 SVG）的 MCP 图像破坏对话——现在保存到磁盘并在工具结果中引用
- 修复构建在 skill 目录内运行时文件描述符耗尽——非 `.md` 文件不再触发 skill 重载
- 修复会话标题从插件监视器输出而非用户第一条提示生成
- 修复 skill 工具在无头模式下的权限错误（v2.1.141 回归）
- 修复在全新机器上首次加载后在自己设置中启用的插件显示"未缓存"错误；现在仅由项目 `.claude/settings.json` 启用的插件显示可操作的 `claude plugin install` 提示
- 修复 `.mcp.json` 无法解析时 `claude mcp list` 静默报告无服务器（例如使用 VS Code 的 `"servers"` 键而非 `"mcpServers"`）——现在显示配置错误
- 修复自定义 `ANTHROPIC_BASE_URL` 设置和 Bedrock Mantle 上的后台 side 查询未使用 Haiku——现在在配置第一方 API 密钥或未设置 Haiku 模型时正确回退
- 修复 Windows 上附加后台会话中的滚动——PgUp/PgDn、鼠标滚轮和 Ctrl+O 转录导航现在可用
- 修复关闭附加后台会话时崩溃
- 修复在 Windows 上在 `claude agents` 中按 ← 使列表对键盘输入无响应
- 修复在 Windows Terminal 上使用 CJK 内容切换窗格时左侧边缘的幽灵字符
- `/bg` 和 `←` 分离现在保留通过 `/add-dir` 添加的目录
- 修复编辑/写入在刚分离已在原地编辑的会话时拒绝并提示"后台会话尚未隔离其变更"
- 修复在已停止后台会话上 `claude respawn <id>` 显示"已停止"而非"运行中"
- 修复 `/resume` 选择器不显示从后台会话分叉的会话
- 修复在后台服务无响应时从 `claude agents` 打开会话或运行 `claude logs <id>` 挂起——现在 10 秒后超时并显示恢复提示
- 修复 subagent 产生的后台 Bash 任务在进程退出后在 SDK 任务面板中保持"运行中"
- 修复已完成或停止的后台会话短暂唤醒失败被永久标记为启动崩溃
- 修复 `claude agents` 附加会话中的 Markdown 链接渲染为纯文本而非可点击超链接
- 修复自定义 `spinnerVerbs` 应用于回合结束时 duration 消息——其中的过去式内置函数如"工作了 5 秒"已恢复
- `claude agents` / `--bg` 拒绝消息现在命名具体关卡（非 TTY、环境变量或设置）而非通用消息
- `claude --bg --name <label>` 现在在生成后确认中回显名称
- `claude agents`：用 Ctrl+R 重命名后台会话现在立即更新附加会话的横幅
- 后台会话工作树隔离防护现在适用于配置了 `WorktreeCreate` hooks 的非 git VCS 用户
- 插件市场添加/更新现在遵循 `CLAUDE_CODE_PLUGIN_PREFER_HTTPS`
- `/plugin` 现在在启用、禁用或卸载插件后返回已安装列表
- `/doctor` 现在在命令 hook 缺少 `command` 字段时显示 exec-form 示例
- Skill 列表截断不再显示为启动通知——运行 `/doctor` 查看完整细分
- 改进罕见的响应前流停滞的恢复——现在重试流式传输一次而非回退到较慢的非流式请求
- 改进 SDK/无头 MCP 启动：预等待现在与启动重叠而非在第一回合前阻塞（使用慢速 MCP 服务器时快达 2 秒）
- 后续调查跟进提示现在在每次非忽略调查回复后显示上下文感知文案，使通过 /feedback 分享更多细节更容易

## 2.1.143

- 新增插件依赖强制执行：`claude plugin disable` 现在在另一个已启用插件依赖目标时拒绝（提供可复制粘贴的禁用链提示），`claude plugin enable` 强制启用传递依赖
- 新增预计上下文成本（每回合和每次调用的令牌估算）到 `/plugin` 市场浏览窗格
- 新增 `worktree.bgIsolation: "none"` 设置，允许后台会话直接在工作副本上编辑，无需 `EnterWorktree`，适用于 worktrees 不实用的仓库
- PowerShell 工具现在传递 `-ExecutionPolicy Bypass`。通过 `CLAUDE_CODE_POWERSHELL_RESPECT_EXECUTION_POLICY=1` 选择退出
- 后台会话现在在空闲唤醒后保留设置的模型和努力级别
- 附加 agent 会话中的 Shift+Tab 现在在循环中包含自动模式
- 修复 `.credentials.json` 中 `scopes` 值为非数组导致 CLI 启动挂起或静默中止 OAuth 令牌刷新
- 修复 Windows Terminal 和 WSL 上 `claude agents` 的右键粘贴
- 修复阻止反复循环的 stop hooks——现在在 8 次连续阻止后结束回合并发出警告（通过 `CLAUDE_CODE_STOP_HOOK_BLOCK_CAP` 覆盖）
- 修复 Esc/Ctrl+C 不取消待处理的 `/loop` 唤醒而 Claude 在迭代之间空闲
- 修复 `/goal` 评估器在后台 shell 或委托的 subagent 仍在运行时触发
- 修复 `settings.json` `env` 中的 `NO_COLOR`/`FORCE_COLOR` 剥离 Claude Code 自己的 UI 颜色——现在仅适用于子进程
- 修复 Windows 上列出会话时 agent 视图产生重复 PowerShell 进程
- 修复 `/bg` 无提示时向分叉会话发送"继续"——分叉现在等待输入
- 修复 `--agent <name>` 无法找到不带 `plugin:` 前缀的插件贡献 agent
- 修复从 agent 视图删除会话时未移除其转录文件
- 修复 Windows Terminal 上附加后台会话滚动中的过时片段渲染
- 修复主机睡眠或 macOS App Nap 后后台 agent 误报 worker-stall 检测风暴
- 修复 5xx 错误消息指向 status.claude.com 而非命名配置的网关或云提供商
- PowerShell 工具现在在 Bedrock、Vertex 和 Foundry 用户上默认启用。在 Windows 上通过 `CLAUDE_CODE_USE_POWERSHELL_TOOL=0` 选择退出
- `claude agents` 现在接受 `--add-dir`、`--settings`、`--mcp-config` 和 `--plugin-dir` 并将它们应用于仪表板和从其调度的后台会话
- `claude agents` 接受 `--permission-mode`、`--model`、`--effort` 和 `--dangerously-skip-permissions` 来设置从视图调度的会话的默认值
- `claude --bg --dangerously-skip-permissions` 现在在 retire→wake 后保持
- 修复后台会话静默捕获 IDE 文件引用到 warm spare 的输入中，导致引用被前置到从 `claude agents` 分派的下一条提示
- 工作树清理不再在 `git worktree remove` 失败时回退到 `rm -rf`，防止丢失 gitignored 或进行中的文件
- 修复 macOS 上后台作业会话在读取 `~/Documents`、`~/Desktop` 或 `~/Downloads` 下的文件时出现"操作不允许"错误，即使授予了全磁盘访问权限
- `/bg` 现在保留 `--mcp-config`、`--settings`、`--add-dir`、`--plugin-dir` 和 `--strict-mcp-config`，使后台会话在重新生成时保持其 MCP 服务器和设置
- 从 `claude agents` 启动的后台会话现在遵循 `settings.json` 中的 `permissions.defaultMode`（之前覆盖为自动模式）
- 修复：在 Windows 上，在响应流式传输时在 `claude agents` 中按 ← 可能使 agent 列表对所有输入无响应
- `/bg` 和 `←` 分离现在保留 `--fallback-model`，使后台工作器在过载时降级到回退模型而非硬失败
- `/bg` 和 `←` 分离现在保留 `--allow-dangerously-skip-permissions`，使分叉工作器在权限循环中保持绕过权限可用
- 修复：后台守护进程生成现在在 `~/.local/bin/claude` 启动器缺失或不可执行时回退到运行中的二进制文件
- 修复 `claude agents --allow-dangerously-skip-permissions` 将分派会话默认为绕过模式而非在权限循环中使其可用

## 2.1.142

- 新增新的 `claude agents` 标志：`--add-dir`、`--settings`、`--mcp-config`、`--plugin-dir`、`--permission-mode`、`--model`、`--effort` 和 `--dangerously-skip-permissions` 用于配置分派的后台会话
- 快速模式现在默认使用 Opus 4.7（之前为 Opus 4.6）。设置 `CLAUDE_CODE_OPUS_4_6_FAST_MODE_OVERRIDE=1` 可将快速模式固定到 Opus 4.6
- 具有根级 `SKILL.md` 且无 `skills/` 子目录的插件现在作为 skill 显示
- `/plugin` 详情窗格和 `claude plugin details` 现在显示插件提供的 LSP 服务器
- `/web-setup` 在替换现有 GitHub App 连接前发出警告
- 修复 `MCP_TOOL_TIMEOUT` 未为远程 HTTP 和 SSE MCP 服务器提高每请求获取超时，导致工具调用封顶为 60 秒而无视配置值
- 修复后台会话不识别预先存在的 git worktree，在 EnterWorktree 拒绝创建重复项时阻止编辑
- 修复 macOS 睡眠/唤醒后后台会话消失且守护进程重连失败——守护进程现在检测时钟跳跃而非将其视为经过的空闲时间
- 修复守护进程在二进制文件升级后未干净退出（例如 `brew upgrade`），导致调度的 agent 在已删除路径上崩溃循环
- 修复 Claude-in-Chrome 扩展连接但无共享标签时后台 agent 崩溃循环
- 修复在附加的 `claude agents` 会话中点击链接——后台工作器的无头浏览器填充在附加时不再应用
- 修复 `claude agents` "v 在编辑器中打开"使用守护进程的默认编辑器而非 shell 的 `$EDITOR`/`$VISUAL`
- 修复 `claude agents` 在具有网络驱动器工作目录的 Windows 上死锁；Ctrl+C 现在在启动期间有效
- 修复从 Apple Terminal 或其他仅 256 色终端附加到 `claude agents` 会话时的背景色渗透
- 修复 `claude --bg --dangerously-skip-permissions` 在 retire/wake 后未保持
- 修复会话标题从第一条消息是链接时的 URL 派生
- 修复远程客户端的冗余 `set_model` 请求将重复的 `/model` 面包屑注入转录
- 修复使用 `skills: ["./"]` 的插件显示虚假的"路径超出插件目录"错误
- 修复插件缓存清理在无安装元数据时删除活动插件版本目录
- 修复 `/plugin` 浏览窗格对新发布的插件显示"0 次安装"
- 修复插件警告未命名每个遮蔽默认文件夹的 `plugin.json` 键
- 改进响应式压缩：首次压缩尝试现在从原始请求的溢出大小播种，避免浪费的近乎满上下文的重试
- 改进 hook 配置错误：为 `SessionStart`/`Setup`/`SubagentStart` 配置提示型或 agent 型 hook 现在显示清晰的"使用命令型 hook"错误
- 移除使用策略拒绝消息中过时的 `/model claude-sonnet-4-20250514` 建议

## 2.1.141

- 新增 `terminalSequence` 字段到 hook JSON 输出，使 hook 可以在无控制终端的情况下发出桌面通知、窗口标题和铃声
- 新增 `CLAUDE_CODE_PLUGIN_PREFER_HTTPS` 用于通过 HTTPS 而非 SSH 克隆 GitHub 插件源，适用于无 GitHub SSH 密钥的环境
- 新增 `ANTHROPIC_WORKSPACE_ID` 环境变量用于工作负载身份联合——当联合规则覆盖多个工作区时，将 minted 令牌限定到特定工作区
- 新增 `claude agents --cwd <path>` 将会话列表限定到目录
- `/feedback` 现在可以包含最近会话（过去 24 小时或 7 天）用于跨会话的问题
- 回退菜单：新增"在此之前总结"以压缩早期上下文同时保持最近回合完整
- 自动模式权限对话框现在解释何时 `permissions.ask` 规则导致了提示
- 恢复 IDE 连接的文件编辑权限提示上的"在 IDE 中查看 diff"选项
- 通过 `/bg` 或 `←←` 启动的后台 agent 现在保留当前权限模式而非恢复为默认
- `claude agents`：完成工作但留下运行中后台 shell 的 agent 现在移至已完成而非保持在工作中
- 改进长时间 thinking 期间的旋转反馈——旋转动画现在在 10 秒后变为琥珀色以信号 Claude 仍在工作
- 改进插件菜单导航：`→`/Tab 切换标签页，`↑` 移动到标签页条，标签页标题和搜索框在全屏模式下可点击
- 修复后台 side 查询在 Bedrock/Vertex/Foundry/网关上的 Haiku 模型 ID 不可用时发送不可用的 Haiku 模型 ID——现在回退到主循环模型
- 修复 Windows 上 `claude daemon status` 和 `/doctor` 在守护进程管道密钥文件被锁定或不可读时抛出异常——现在显示底层错误而非不透明失败
- 修复通过添加标志的包装启动 `claude agents` 时显示 agent 类型列表而非仪表板
- 修复打开崩溃会话的 `claude agents` 在工作目录被删除时发出冗余调度
- 修复自定义 `ANTHROPIC_BASE_URL` 网关上后台作业未自动命名——命名器现在在未配置 Haiku 模型时使用主模型
- 修复一个会话中的 `/model` 静默更改其他并发会话的自动压缩阈值
- 修复在工具权限提示打开时切换权限模式不会在新设置允许工具时自动关闭提示
- 修复在权限/对话框提示打开时按 Enter 也提交输入框中的文本
- 修复 hooks 在 `EnterWorktree` 切换工作目录后收到不存在的 `transcript_path`
- 修复具有单元格换行的 Markdown 表格回退到垂直键值布局而非渲染为带边框网格（2.1.136 回归）
- 修复自动恢复到输入框时取消的提示从上箭头历史中移除，避免重复条目
- 修复在响应前用 Ctrl+C/Esc 取消的提示被从上箭头历史中丢弃
- 修复在 vim INSERT/VISUAL 模式下 Ctrl+C 不中断运行中的回合
- 修复替代 `chat:submit` 键绑定（例如 `meta+enter`、`ctrl+enter`）在 `enter` 重新绑定到 `chat:newline` 时不工作
- 修复在配置了输出样式时提示建议被静默禁用
- 修复 `spinnerVerbs` 设置未在回合完成消息中生效
- 修复 AskUserQuestion 弹出窗口隐藏最后一行聊天内容
- 修复 Web Search 状态在搜索返回错误时显示"进行了 0 次搜索"
- 修复多行状态行输出在任何行超出终端宽度时丢失或损坏行
- 修复 light-ansi 主题在浅色背景上对 diff 上下文行使用不可见的白色——现在使用黑色
- 修复错误叠加转储压缩的 bundle 源码而隐藏原始错误消息
- 修复在输入反馈调查评分数字后按 Enter 将其作为聊天消息提交而非评分
- 修复在 agent 面板中选定 subagent 上按 `x` 将字符输入到提示而非停止 agent
- 修复会话标题从插件监视器通知而非用户第一条提示派生
- 修复"已由 PermissionRequest hook 允许"在折叠的读取/搜索组下的每次工具调用重复
- 修复 `/tui` 静默丢弃运行中的后台 shell 和 subagent——现在拒绝并要求等待它们完成
- 修复欢迎横幅在 Bedrock、Vertex、Foundry 和其他第三方提供商上显示"API 使用量计费"——现在显示提供商名称
- 修复 `/mcp` 服务器列表在全屏模式下短终端上不保持焦点服务器可见
- 修复 `/feedback` bundle 中的脱敏产生引用值（如会话 ID）的无效 JSON
- 修复桌面和第三方提供商会话错误地从主机托管设置继承 `apiKeyHelper`/`ANTHROPIC_AUTH_TOKEN`
- 修复在记录器初始化前触发的早期分析事件被静默丢弃
- 修复在还固定了 `sha` 时市场 `ref` 不再存在的插件 `claude plugin install` 失败
- 修复插件详情窗格对通过 `.mcp.json` 声明的插件显示 0 个 MCP 服务器
- 修复具有未设置配置变量的插件 MCP 服务器显示通用连接失败而非"配置问题"消息和修复提示；格式错误的 `.mcp.json` 条目不再丢弃其他 MCP 服务器
- 修复使用 POSIX shell 参数扩展（例如 `${var%pattern}`）的 MCP 服务器配置被错误标记为缺少环境变量
- 修复返回 403 的 MCP HTTP/SSE 服务器连接显示为"失败"而非"需要认证"
- 修复可选服务器事件流重新连接失败时远程 MCP 服务器不必要断开——工具调用通过 POST 继续
- 修复 Remote Control MCP 连接器在工作器会话令牌在会话中期轮换时全部以 401 失败
- 修复 Remote Control 在服务器拒绝过期令牌时自动重新注册可信设备而非循环通过 `/login`
- 修复在启用 beta 跟踪的 SDK/无头模式下早期 OTel 跨度可能被静默丢弃的竞争条件
- 修复自定义 `voice:pushToTalk` 键绑定和 `"space": null` 解除绑定被静默忽略
- 修复 Windows Alt+V 图像粘贴在剪贴板包含截图时报告"未找到图像"
- 修复 Linux 上同时安装 glibc 和 musl 平台包时 SDK "未找到 Claude Code 原生二进制文件"
- Bedrock：`awsCredentialExport` 现在在配置时始终运行而非在环境 AWS 凭证解析时被跳过，修复跨账户访问认证
- [VSCode] 修复聊天内麦克风在麦克风仅产生静音时无反馈——现在显示"未检测到音频"
- [VSCode] 语音模式：WSL 错误现在建议 WSLg 用户安装 `sox libsox-fmt-pulse`
- `claude agents`：启动会话不再在前预热的后台工作器不健康时失败——现在回退到全新启动
- `claude agents` 不再显示从全新 REPL 后台化留下的空占位会话，并通过 ← 进入且无其他 agent 时显示入门文本
- 从 `←` 留下的空闲置后台会话现在由守护进程在 5 分钟后自动退役

## 2.1.140

- 改进 Agent 工具 `subagent_type` 匹配以接受大小写和分隔符不敏感的值（例如 `"Code Reviewer"` 解析为 `code-reviewer`）
- 更新 agent 调色板
- 修复 `/goal` 在设置 `disableAllHooks` 或 `allowManagedHooksOnly` 时静默挂起——现在显示清晰的消息而非永不解析的指示器
- 修复设置热重载中的回归，其中符号链接设置文件导致变更事件归因错误和虚假 `ConfigChange` hooks
- 修复 `claude --bg` 在后台服务即将空闲退出时失败并提示"连接在请求中途中断"
- 修复具有企业端点安全防护的机器上后台服务启动失败——允许更多时间
- 修复远程托管设置在 401 上不重试——现在使用强制刷新令牌重试一次
- 修复托管 `extraKnownMarketplaces` 自动更新策略未持久化到 `known_marketplaces.json`
- 修复 `/loop` 为已通过完成通知的后台任务调度冗余唤醒以轮询
- 修复在 Windows 上缺少可执行文件（例如 `gh`）导致同步 `where.exe` 重新生成并在每次检查时触发的反复事件循环停滞
- 修复在 `offset` 作为空白填充或 `+` 前缀字符串传递时 Read 工具调用验证失败
- 修复终端失去焦点时原生终端光标未保持在输入插入符号处
- 插件现在在默认组件文件夹（例如 `commands/`）被 `plugin.json` 设置匹配键静默忽略时发出警告。显示在 `/doctor`、`claude plugin list` 和 `/plugin` 中

## 2.1.139

- 新增 agent 视图（研究预览）：每个 Claude Code 会话的单一列表——运行中、阻塞于你或已完成。运行 `claude agents` 开始。参见 https://code.claude.com/docs/en/agent-view
- 新增 `/goal` 命令：设置完成条件，Claude 跨回合持续工作直到满足。在交互式、`-p` 和远程控制中工作。显示实时已用时间/回合/令牌作为覆盖面板
- 新增 `/scroll-speed` 命令以通过实时预览调优鼠标滚轮滚动速度
- 新增 `claude plugin details <name>` 显示插件组件清单和预计每会话令牌成本
- 新增转录视图导航：`?` 显示键盘快捷键，`{`/`}` 在用户提示间跳转，`v` 切换快捷键面板
- 新增 hook `args: string[]` 字段（exec 形式），直接生成命令而非通过 shell，因此路径占位符无需引号
- 新增 hook `continueOnBlock` 配置选项用于 `PostToolUse`——设置为 `true` 将 hook 拒绝原因反馈给 Claude 并继续回合
- MCP stdio 服务器现在在其环境中接收 `CLAUDE_PROJECT_DIR`，与 hooks 匹配。插件配置可在命令中引用 `${CLAUDE_PROJECT_DIR}`
- 压缩提示现在要求模型保留敏感用户指令
- `/mcp` Reconnect 现在在不重启的情况下拾取 `.mcp.json` 编辑，并在重新连接失败时显示 HTTP 状态和 URL
- `/context all` 每 skill 令牌估算现在考虑模型的 tokenizer 并显示四舍五入的值
- `claude plugin install <name>@<marketplace>` 现在在报告插件未找到前自动刷新市场并重试
- `/plugin` 已安装插件详情现在干净显示 hook 事件名称和 MCP 服务器名称
- `/context` 现在为插件来源的 skill 显示提供插件的名称
- 远程 MCP 服务器在临时失败时重新连接重试现在对所有用户启用
- Subagent 的 API 请求现在携带 `x-claude-code-agent-id` / `x-claude-code-parent-agent-id` headers，`claude_code.llm_request` OTEL 跨度包含 `agent_id` / `parent_agent_id` 属性
- Remote Control、`/schedule`、claude.ai MCP 连接器和通知偏好现在在设置 `ANTHROPIC_API_KEY` / `apiKeyHelper` / `ANTHROPIC_AUTH_TOKEN` 时被禁用，即使存在 claude.ai 登录。取消设置 API 密钥以使用这些功能
- 修复过期凭证和 `forceRemoteSettingsRefresh` 策略设置阻止 `claude auth login`/`logout`/`status` 且无法恢复的死锁
- 修复 `autoAllowBashIfSandboxed` 未自动批准包含 shell 扩展（如 `$VAR` 和 `$(cmd)`）的命令
- 修复写入终端的 hook 可能破坏屏幕上交互式提示的 bug；hooks 现在在没有终端访问的情况下运行
- 修复 HTTP/SSE MCP 服务器流式传输非协议数据时的无界内存增长——响应体现在每 SSE 帧上限为 16 MB
- 修复 `Skill(name *)` 权限规则——通配符形式现在作为前缀匹配工作，匹配 `Bash(ls *)` 行为
- 修复设置热重载未检测到对符号链接 `~/.claude/settings.json` 的编辑
- 修复插件详情在市场密钥与清单名称不同时加载失败
- 修复 `/model` 选择器"默认"行未反映 `ANTHROPIC_DEFAULT_OPUS_MODEL`/`ANTHROPIC_DEFAULT_SONNET_MODEL` 覆盖
- 修复响应完成后 5 分钟出现虚假的"流空闲超时"，由看门狗定时器在流取消时未清除导致
- 修复在缓存目录不可写时 10+ MCP 服务器配置导致静默 `exit 1`——错误消息现在包含底层原因
- 修复对话框中制表符名称、列表指针和选择行上的打字光标闪烁
- 修复鼠标点击后转录视图字母快捷键不工作
- 修复 Bash 模式下上箭头历史重复第一个条目并覆盖进行中的草稿
- 修复粘贴或拖放多个图像只插入最后一个
- 修复在深色主题上使用不可读的深海军蓝的超链接——现在适应活动主题
- 修复模型选择器对第三方用户（其模型设置为 `opus` 别名）显示冗余的"当前模型"行
- 修复 PAYG 3P 提供商的旧 Opus 选择器条目解析为与默认条目相同的模型
- 修复 Cursor 和 VS Code 1.92–1.104 中鼠标滚轮滚动速度