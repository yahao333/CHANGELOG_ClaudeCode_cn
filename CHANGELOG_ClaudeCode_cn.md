# 更新日志

## 2.1.195

- 新增 `CLAUDE_CODE_DISABLE_MOUSE_CLICKS` 环境变量，可在全屏模式下禁用鼠标点击/拖拽/悬停，同时保留滚轮滚动
- 修复了带连字符标识符的 hook 匹配器（如 `code-reviewer`、`mcp__brave-search`）意外进行子字符串匹配的问题——现在改为精确匹配。如需匹配带连字符的 MCP 服务器的所有工具，请使用 `mcp__brave-search__.*`
- 修复了 macOS 上语音听写在长时间运行会话中切换默认输入设备后仍捕获静音的问题
- 修复了语音听写自动提交功能对无空格语言（日语、中文、泰语）从不触发的问题
- 修复了仅通过项目 `.claude/settings.json` 启用的外部插件在每次加载器路径上不需要明确安装同意的问题
- 修复了当插件的 `plugin.json` `name` 与市场条目名称不同时，`/plugin` 启用/禁用功能不工作的问题
- 修复了 `claude agents` 中后台作业消失或被更新版本的 Claude Code 写入时丢失数据的问题
- 修复了重新打开崩溃的后台任务时显示长达 5 秒空白屏幕而非立即重启的问题
- 修复了后台代理守护进程在控制套接字启动失败时运行处于不可达状态，从而阻止重启的问题
- 改进了 Linux 上的语音模式：现在可以区分"无麦克风"和"SoX 未安装"——当 SoX 存在但没有音频捕获设备时
- 改进了 `claude agents` 完成列表以填充可用垂直空间；在短终端上，标题会紧湊化以保持实时会话可见
- 改进了远程会话启动，在容器启动时显示配置清单

## 2.1.193

- 新增 `autoMode.classifyAllShell` 设置，将所有 Bash/PowerShell 命令通过自动模式分类器路由，而非仅处理任意代码执行模式
- 新增自动模式拒绝原因，显示在记录文本、拒绝提示和 `/permissions` 最近拒绝中
- 新增 `claude_code.assistant_response` OpenTelemetry 日志事件，包含模型的响应文本。除非设置 `OTEL_LOG_ASSISTANT_RESPONSES=1`，否则会被编辑；在该变量未设置时遵循 `OTEL_LOG_USER_PROMPTS`，因此已记录提示内容的部署在升级后将开始接收响应内容——设置 `OTEL_LOG_ASSISTANT_RESPONSES=0` 可保持仅记录提示
- 新增 bash 模式下的实时文件路径自动补全（`!`）
- 新增启动通知，当 MCP 服务器需要认证时提示指向 `/mcp`
- 新增后台空闲 shell 命令的自动内存压力回收功能（可使用 `CLAUDE_CODE_DISABLE_BG_SHELL_PRESSURE_REAP=1` 禁用）
- 修复了 `/login` 后立即显示 `/model` 等客户端数据门控 UI 的陈旧/空状态的问题
- 修复了后台化（←←）在所有运行中任务延续到新会话时意外取消的问题，显示"N 个后台任务将被放弃"
- 修复了固定后台代理在每次自动更新后被重新提示"从中断处继续"的问题
- 修复了后台化主回合时生成幽灵"通用（恢复的）"子代理从而重新运行主对话的问题
- 修复了代理面板在查看子代理时隐藏同级代理的问题
- 改进了后台代理：启动结果不再指示 Claude"结束你的回复"——它会在代理运行期间继续处理其他任务
- 改进了 MCP `headersHelper` 认证：当工具调用返回 401/403 时，帮助程序现在会自动重新运行并重新连接
- 改进了插件自动重命名：市场 `renames` 映射现在会自动遵循，用新名称更新你的设置
- 改进了 `/add-dir` 消息，当目录已是工作目录时

## 2.1.191

- 新增 `/rewind` 支持，可从 `/clear` 之前的对话恢复
- 修复了流式响应期间阅读早期输出时滚动位置跳转到底部的问题
- 修复了停止后台代理后其复活的问题——从任务面板停止代理现在将是永久性的
- 修复了 `/voice` 在被组织策略禁用时显示通用"不可用"消息的问题——现在会解释限制原因
- 修复了 `/login` URL 在 Windows Terminal 中跨行换行时显示截断的问题
- 修复了在 ssh/tmux 上的 Ghostty 全屏模式下 Cmd+点击链接不工作的问题
- 修复了 `claude agents` 将内置斜杠命令（如 `/usage`）作为提示文本发送到后台会话而非显示提示的问题
- 修复了 `claude agents` 任务行对粘贴图片显示完整文件系统路径而非 `[Image #N]` 占位符的问题
- 修复了带逗号分隔匹配器的 hook（如 `"Bash,PowerShell"`）静默从不触发的问题
- 修复了 `/permissions` 最近拒绝标签：关闭时批准拒绝现在会持久化而非被静默丢弃
- 修复了在滚动超出溢出上限时代理面板跳转一行的问题
- 修复了欢迎页艺术在默认 80×24 macOS Terminal 窗口溢出的问题
- 修复了托管设置：`forceRemoteSettingsRefresh` 现在在通过 MDM 或文件策略设置时生效，并且获取请求发送 `Cache-Control: no-cache` 以防止代理提供过时响应
- 改进了沙箱网络权限对话框：你用"是"允许的主机现在会在整个会话中记住，而非每次连接时都重新提示
- 改进了 MCP 服务器可靠性：能力发现（`tools/list`、`prompts/list`、`resources/list`）现在会用短退避重试瞬态网络错误
- 改进了 MCP OAuth：发现和令牌请求现在在瞬态网络错误后重试一次，无头环境跳过浏览器弹出窗口直接进入粘贴 URL 提示
- 改进了 MCP 错误消息：HTTP 404 错误现在显示 URL 并指向你的 MCP 配置
- 改进了 vim 模式提示历史搜索（NORMAL `/`）以提示如何访问斜杠命令
- 通过将文本更新合并到 100ms，减少了流式响应期间约 37% 的 CPU 使用
- 减少了终端输出缓存导致的长时间会话内存增长

## 2.1.190

- 错误修复和可靠性改进

## 2.1.187

- 新增 `sandbox.credentials` 设置，阻止沙箱化命令读取凭证文件和密钥环境变量
- 新增组织配置的模型限制，适用于模型选择器、`--model`、`/model` 和 `ANTHROPIC_MODEL`，当选择受限时显示"受组织设置限制"消息
- 新增鼠标点击支持以选择菜单（权限提示、`/model`、`/config` 等）全屏模式
- 修复了当原始 `-p` 运行没有产生模型回合时 `--resume` 失败并显示"未找到对话"的问题
- 修复了 `--json-schema` 和工作流 `agent({schema})` 结构化输出：模型在成功调用后不再无限重新调用 `StructuredOutput`，后续回合现在可靠地返回结构化输出
- 修复了远程 MCP 工具调用在 5 分钟无响应时挂起的问题——现在会中止并显示错误（可使用 `CLAUDE_CODE_MCP_TOOL_IDLE_TIMEOUT` 覆盖）
- 修复了由于添加了代理 CA 系统信任安装，Claude Code Remote 会话启动时间增加约 2.7 秒的问题
- 修复了在按字节传输扩展键事件的终端中粘贴韩文/CJK 文本变成乱码的问题
- 修复了通过远程控制进行 `/update` 时在启动信任对话框会显示时挂起的问题
- 修复了代理视图中的后台任务在代理回合结束时没有产生结构化输出时永久显示"工作中"的问题
- 修复了在导航到代理视图及返回后，以及 `/bg`、`/tui` 或 `/update` 后通道连接断开的问题
- 修复了代理停止通知未正确归属停止代理的人的问题，改进了措辞（"已完成"/"已停止"而非"停止运行"）
- 修复了子代理深度跟踪：恢复的子代理现在恢复其原始生成深度，分叉的子代理现在计入深度上限
- 修复了泄漏的代理 worktree 注册：被杀死的代理的锁定 `.git/worktrees/` 条目现在自动清理
- 修复了在 macOS 上 Ghostty 全屏模式中 Cmd+点击不打开 URL 的问题
- 修复了 `claude --help` 未列出 `--bg`/`--background` 标志的问题
- 修复了 `/share` 上传时 Esc、Ctrl-C 和 Ctrl-D 不工作的问题
- 改进了 `/install-github-app`：GitHub Actions 工作流设置现在是可选的——你可以只安装 GitHub App 并跳过工作流/密钥步骤
- 改进了 `/btw`，使用 ←/→ 箭头导航来逐步查看较早的回复
- 改进了 `/plugin`，显示你最近未使用的插件以便清理
- [VSCode] 修复了恢复大会话时扩展无响应的问题

## 2.1.186

- 新增 `claude mcp login <name>` 和 `claude mcp logout <name>`，用于从 CLI 认证 MCP 服务器，无需打开交互式 `/mcp` 菜单，支持通过 SSH 完成时的 `--no-browser` stdin 重定向
- 新增 `/workflows` 代理详情视图的状态过滤（按 `f`）
- 新增 `/plugin` 已安装标签页的"技能"部分
- 新增 `teammateMode: "iterm2"` 设置，当自动模式找不到 `it2` CLI 时发出警告
- 当配置了 `awsAuthRefresh` 时，在 `/login` 新增"Claude Platform on AWS - 刷新凭证"选项
- `!` bash 命令现在自动触发 Claude 响应输出；在 settings.json 中设置 `"respondToBashCommands": false` 可保持之前的仅上下文行为
- 修复了机器从睡眠唤醒后流式请求失败并显示"未找到内容块"或 JSON 解析错误的问题
- 修复了子代理记录滚动位置在退出时渗入主记录的问题
- 修复了后台任务预览在代理计划加载前闪烁原始工具名称的问题
- 修复了当产品内权限门关闭时 Chrome 标签页组隔离不适用于并发 CLI 会话的问题
- 修复了后台会话回顾重复；代理自己的回合结束摘要现在显示为回顾行
- 修复了从 `claude agents` 打开后台会话时在先前屏幕留下残影的问题
- 修复了命名子代理生成未强制执行 `Agent(type)` 拒绝规则和 `Agent(x,y)` 允许类型限制的问题
- 修复了后台代理仍在运行且主回合结束后 Esc 和 Ctrl+C 无响应的问题
- 修复了权限提示中选项文本溢出时选项编号对齐错误的问题
- 修复了在代理面板中按已完成子代理的 `x` 不解散它的问题
- 修复了恢复旧会话时对故意停用的工具显示误导性"MCP 服务器断开连接"通知的问题
- 修复了 `/plugin` 已安装显示"上方还有更多"指示器时已经滚动到顶部的问题
- 修复了 `~~删除线~~` 在助手消息中显示字面上的波浪号而非渲染为删除线的问题
- 修复了 `--tools` 在冷启动首次启动时允许功能门控工具在标志加载前通过的问题
- 修复了 `claude agents` 中后台任务状态在回复后显示过时"需要输入"消息的问题
- 修复了在浅色终端上从 `claude agents` 打开后台会话时深色主题闪烁的问题
- 修复了在 `claude agents` 中删除后鼠标选择的文本保持高亮的问题
- 修复了基于用量的 Enterprise 和 Team 订阅者不显示会话成本的问题
- 修复了代理团队：通过 tmux/pane 后端生成的队友现在继承领导者的 `--effort` 级别
- 修复了工作流 `agent({schema})` 子代理在重复模式验证失败时无限循环而非 5 次后中止的问题
- 改进了 `claude mcp get` 和 `claude mcp remove`，在拼写错误时建议最接近的配置服务器名称，并截断长服务器列表
- 改进了内存：当接近大小时，代理现在会收到压缩 `MEMORY.md` 索引的提醒
- 改进了技能 frontmatter：`display-name`、`default-enabled`、`fallback` 和 `metadata.*` 键现在接受 kebab-case、snake_case 和 camelCase
- 改进了格式错误的 `SKILL.md` YAML frontmatter 处理：用空元数据加载技能体而非静默失败
- 将 `CLAUDE_CODE_MAX_RETRIES` 上限改为 15；对于无人值守会话，请改用 `CLAUDE_CODE_RETRY_WATCHDOG`
- 更改了后台子代理，将权限提示显示在主会话中而非自动拒绝；对话框显示是哪个代理在询问，Esc 仅拒绝该工具
- 将 `/review <pr>` 改为使用与 `/code-review medium` 相同的审查引擎

## 2.1.185

- 流停顿提示现在显示"等待 API 响应 · 将在 … 后重试"而非"API 无响应 · 正在重试 …"，并在沉默 20 秒后触发而非 10 秒

## 2.1.183

- 改进了自动模式安全性：破坏性 git 命令（`git reset --hard`、`git checkout -- .`、`git clean -fd`、`git stash drop`）现在在你未要求放弃本地工作时被阻止，`git commit --amend` 在提交不是本会话代理所做时被阻止，`terraform destroy`/`pulumi destroy`/`cdk destroy` 除非你要求了特定堆栈否则被阻止
- 新增当你请求的模型已弃用或自动更新到更新模型时的警告，在打印模式（`-p`）的 stderr 中显示，现在也涵盖在代理 frontmatter 中设置的模型
- 新增 `attribution.sessionUrl` 设置，用于在 web 和 Remote Control 会话的提交和 PR 中省略 claude.ai 会话链接
- 新增 `/config --help` 列出 `/config key=value` 所有可用的简写键
- 更改了 `/config` 切换行为：Enter 和 Space 都更改所选设置，Esc 现在保存并关闭而非还原
- 移除了 logo 下的启动"设置问题"行——运行 `/doctor` 查看配置问题或使用 `--debug`
- 修复了受影响的配置中子代理生成和会话标题生成的 `thinking.disabled.display: Extra inputs are not permitted` 400 错误
- 修复了 WebSearch 在子代理中返回空结果的问题
- 修复了在启用原生光标且 vim 模式下导航历史记录后终端光标停留在提示上方的问题
- 修复了在 Windows Terminal 重负载嵌套子代理下全屏 TUI 损坏（状态行在屏幕中间、重复旋转行、合并文本）的问题
- 修复了当模型仅返回思考块时回合静默完成且无可见输出；Claude 现在会重新提示一次
- 修复了当启用多个插件时用户级技能在斜杠命令自动补全中多次出现的问题
- 修复了在无头/SDK 模式下需要认证的 MCP 服务器向模型暴露 auth-stub 工具的问题
- 修复了 tmux 队友窗格在 shell 初始化文件慢时启动失败的问题，以及在代理生成期间键入的按键泄漏到新 tmux 窗格而非领导提示的问题
- 修复了由队友启动的后台任务在队友完成回合时被杀死的问题
- 修复了计划任务和 webhook 触发器传递被当作键盘输入处理的问题；它们现在分类为任务通知，不能再批准待处理操作或在自动模式下设置会话标题
- 修复了焦点模式在每个回复下显示"运行了 N 个 PostToolUse hook"计时行的问题

## 2.1.181

- 新增 `/config key=value` 语法，可从提示符设置任何设置（如 `/config thinking=false`）——在交互式、`-p` 和 Remote Control 中都有效
- 新增 `sandbox.allowAppleEvents` 可选设置，允许沙箱化命令在 macOS 上发送 Apple Events
- 新增 `CLAUDE_CLIENT_PRESENCE_FILE` 环境变量：指向一个标记文件以在你在机器前时抑制手机推送通知
- 升级了捆绑的 Bun 运行时到 1.4
- 改进了长段落的流式传输：文本现在逐行出现而非等待第一个换行符
- 改进了自动重试：思考中 API 连接断开现在自动重试而非显示"连接关闭而正在思考"
- 改进了子代理面板：空闲子代理 30 秒后自动隐藏，列表限制为 5 行并带有滚动提示，键盘提示现在显示在页脚
- 改进了 MCP OAuth 浏览器页面以匹配 Claude Code 的视觉风格并在成功时自动关闭
- 更改了全屏模式 URL 打开需要 Cmd+点击（macOS）/Ctrl+点击，匹配原生终端行为
- 更改了"改进了 N 个记忆"行，在非详细模式下不再列出单个文件
- 修复了自定义 `ANTHROPIC_BASE_URL` 和 Foundry 上提示缓存因每请求证明令牌每回合变化而不读取的问题
- 修复了 Write/Edit 在网络驱动器和云同步文件夹上产生 0 字节或截断文件的问题
- 修复了 `open`、`osascript` 和基于浏览器的认证流程在 macOS 上因添加 Apple Events 权限而失败并显示错误 -600 的问题
- 修复了启动回归（约在全新环境中每次启动 120ms，引入于 2.1.169）：在未配置 MCP 服务器时第一个提示不再等待托管设置获取
- 修复了当账户设置获取在降级网络上缓慢时启动阻塞空白终端长达 15 秒的问题
- 修复了当 `.claude.json` 包含损坏的空项目条目时启动崩溃（`TypeError: Cannot read properties of null`）
- 修复了 macOS TUI 在 Spotlight 忙于重新索引时会话启动时冻结（Ctrl+C 无响应）的问题
- 修复了长时间空闲会话在另一个 Claude Code 进程运行 30 天记录清理时丢失其历史的问题
- 修复了前台子代理生成无限制嵌套链的问题；它们现在遵守与后台子代理相同的 5 级深度限制
- 修复了模型切换后 `/recap` 和对话分叉使用先前模型的问题
- 修复了子代理"思考"持续时间显示父代理的已用时间而非子代理自己的时间的问题
- 修复了被嵌套代理阻止的子代理在代理面板中显示递增已用时间而非"等待"的问题
- 修复了 API 重试指示器（"将在 0 秒重试 · 尝试 N/10"）在重试成功后仍停留在屏幕上的问题
- 修复了 AWS `awsCredentialExport` 凭证剩余寿命短导致每分钟刷新凭证的问题，现在接受 `aws configure export-credentials` 的 JSON 格式
- 修复了 `claude mcp get`/`list` 在 tools/list 失败时显示 `✓ 已连接`；它们现在显示 `! 已连接 · 工具获取失败` 及错误详情
- 修复了 `/remote-control` 留下过时"正在连接…"行；现在连接后会在记录中确认
- 修复了 ExitWorktree 在 Windows 上无法解析裸 `git` 时拒绝移除干净 worktree 并显示"无法验证 worktree 状态"的问题
- 修复了当 `~/.claude/settings.json` 是符号链接下 `~/.claude` 下的相对符号链接时设置更改（如 `/effort` 或 `/model`）失败并显示 ENOENT 的问题
- 修复了上下文提醒中 IDE 选择行号偏移一个的问题（IntelliJ 和 VS Code）
- 修复了全屏中原生终端选择（修饰符+拖拽）后 Ctrl+C 用应用的先前选择覆盖剪贴板的问题
- 修复了剪贴板包含文本时 Ctrl+V 显示"剪贴板中未找到图片"而非粘贴的问题
- 修复了当 agents 目录已存在时代理创建失败并显示"EEXIST: file already exists"的问题（Windows/OneDrive）
- 修复了 AskUserQuestion 预览内容在对话框边缘截断而非自动换行的问题
- 修复了 AskUserQuestion 多选问题在提交时静默丢弃键入的"其他"自由文本答案的问题
- 修复了 `/stats"最活跃的一天"和每日令牌图表日期在 UTC 负时区早一天显示的问题
- 修复了 Linux 上 `/copy` 和选择复制在 Claude Code 启动后安装剪贴板实用程序时未检测到的问题
- 修复了 Write（创建文件）预览中制表符缩进代码渲染缩进不正确的问题
- 修复了用户提示在回合中途排队时在记录中不显示全宽背景高亮的问题
- 修复了活动旋转器在 Ghostty 中脉冲停留在错误字形大小上的问题

## 2.1.179

- 修复了流连接断开：部分响应现在保留而非显示原始错误，旋转器不再在"运行工具"时卡住
- 修复了 Windows Terminal 和 VS Code 下 WSL2 中鼠标滚轮滚动不工作的问题（回归于 2.1.172）
- 修复了沙箱 `denyRead`/`allowRead` glob 匹配大目录树使 Bash 工具描述变得非常大且会话在 Linux 上无法使用的问题
- 修复了反馈调查在回合完成后将单个数字回复捕获为会话评分的问题
- 修复了欢迎屏幕堆叠多个促销横幅的问题——每个会话最多显示一个促销
- 修复了 Ctrl+O 在查看子代理时不显示子代理记录的问题
- 修复了点击提示输入框不从子代理/页脚面板返回焦点的问题
- 修复了远程会话后台任务在回合之间显示为"仍在运行"的问题
- 改进了远程会话中的插件加载性能

## 2.1.178

- 代理团队：移除了 `TeamCreate` 和 `TeamDelete` 工具。设置了 `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` 后，每个会话现在有一个隐式团队——使用 Agent 工具的 `name` 参数直接生成队友，无需设置步骤。Agent 工具上的 `team_name` 参数仍被接受但被忽略。
- 新增权限规则的 `Tool(param:value)` 语法以匹配工具的输入参数（带 `*` 通配符），如 `Agent(model:opus)` 阻止 Opus 子代理
- 现在在嵌套 `.claude/skills` 目录中的技能在处理其文件时会加载；名称冲突时，嵌套技能显示为 `<dir>:<name>` 以便两者都可用
- 嵌套 `.claude/` 目录：当名称冲突时，最接近工作目录的代理、工作流和输出样式获胜；项目范围的工作流保存现在指向最近的现有 `.claude/workflows/`
- 改进了自动模式：子代理生成现在在启动前由分类器评估，关闭了子代理可能在无审查情况下请求被阻止操作的安全漏洞
- 改进了 `/doctor`，使用一致的扁平树布局跨所有部分，更清晰的节状态图标，以及突出显示的命令名称
- 改进了技能列表截断警告以显示有多少技能描述受影响
- 更改了工作流提示关键词使用紫色闪光高亮，仅在明确短语如"运行工作流"或"工作流："时触发，而非在该词的任何提及时
- 改进了 Remote Control 错误消息：连接失败现在在页脚显示持久红色"/rc failed"指示器，"尚未启用"错误现在解释是门、检查失败、过时授权还是组织策略
- `/bug` 现在在提交前需要描述，不再使用模型拒绝文本作为 GitHub issue 标题
- 修复了 CLI 从父进程继承过时的 websocket/OAuth 文件描述符环境变量时崩溃（内存不足）的问题
- 修复了 Claude in Chrome 在 OAuth 令牌属于与 Claude Code 登录不同的账户时静默连接失败的问题
- 修复了在非交互式运行中具有目录限定名称的嵌套 `.claude/skills` 技能被权限提示阻止的问题
- 修复了多个子代理问题：查看子代理记录现在显示工具结果和实时进度，在它完成回合时发送的消息不再丢失，后台化运行中的子代理（ctrl+b）不再从头重启
- 修复了当守护进程从具有自定义 API 网关的 shell（通过 `ANTHROPIC_BASE_URL` 和 `ANTHROPIC_AUTH_TOKEN`）启动时 `claude agents` 工作线程失败并显示 `401 Invalid bearer token` 的问题
- 修复了压缩不遵守 `--fallback-model`：压缩现在在过载或模型可用性错误时回退到配置的备用模型链
- 修复了在会话外刷新凭证后模型请求因过时缓存请求配置继续失败并显示认证错误的问题
- 修复了在回合结束后用 `/bg` 或 `←←` 创建的后台会话在代理列表中永久显示"工作中"的问题
- 修复了 Linux 沙箱在 `.claude/skills` 或 `.claude/hooks` 是符号链接时无法启动的问题
- 修复了 `CLAUDE_CODE_PLUGIN_KEEP_MARKETPLACE_ON_FAILURE=1` 阻止全新市场安装克隆的问题
- 修复了子代理 `disallowedTools` 中的 MCP 服务器级规范（`mcp__server`、`mcp__server__*`、`mcp__*`）被静默忽略的问题
- 修复了 vim 模式撤销：`u` 现在逐步执行 NORMAL/VISUAL 模式命令，而非将快速连续的命令合并为单个撤销步骤
- 修复了 `claude agents` 中点击具有自定义 URI 方案（如 `vscode://`）的状态行链接不打开的问题
- [VSCode] 修复了按 Esc 关闭 CJK IME 候选窗口取消运行中的 Claude 任务的问题
# 更新日志

## 2.1.176

- 对话标题现在使用对话语言生成（可通过 `language` 设置锁定特定语言）
- 新增 `footerLinksRegexes` 设置，支持在页脚行通过正则匹配添加链接徽章，可通过用户设置或托管设置配置
- 改进了 Bedrock 凭证缓存：`awsCredentialExport` 的凭证现在会缓存至其 `Expiration` 时间，而不是固定的 1 小时
- 修复了 `availableModels` 强制执行：别名模型选择不能再通过 `ANTHROPIC_DEFAULT_*_MODEL` 环境变量重定向到被封禁的模型，且当 `/fast` 切换到允许列表外的模型时会拒绝切换
- 修复了未启用 Opus 4.8 的组织在 Fable 5 上自动模式失败的问题——分类器现在会回退到可用的最佳 Opus 模型
- 修复了 Read/Edit/Write 工具路径的 hook `if` 条件：文档中的 `Edit(src/**)`、`Read(~/.ssh/**)`、`Read(.env)` 等模式现在可以正确匹配
- 修复了 Linux 沙箱在 `.claude/settings.json` 是指向绝对路径的符号链接时无法启动的问题
- 修复了通过 SSH 在 tmux 中时 `/copy` 和鼠标选择复制无法到达系统剪贴板的问题，以及 tmux 粘贴缓冲区在 3.2 以下版本无法加载的问题
- 修复了远程控制从 web/mobile 连接时静默切换会话模型的问题
- 修复了远程控制断开通知显示裸数字代码而非人类可读原因的问题，以及连接失败在对话记录中多加一行的问题
- 修复了远程控制会话在登录不同账户时不会断开的问题
- 修复了 `/cd` 和 worktree 移动后会话仍报告之前目录 git 分支的问题
- 修复了在 `claude agents` 中一个窗口按返回键导致其他窗口脱离同一会话的问题
- 修复了后台会话在 `/bg` 中途无内容继续时永远显示"Working"的问题
- 修复了按 PR URL 搜索后台代理时，在计划唤醒时或任务被阻塞期间打开的 PR 现在可以出现在 `claude agents` 搜索结果中的问题
- 修复了 Windows 上代理视图输入框不显示文本光标的问题
- 修复了 `claude --bg -cn <name>` 未填充会话名称的问题
- 修复了后台会话在持久化状态前未中和 Windows 网络路径的问题
- 修复了后台会话重spawn时拒绝来自损坏状态文件的畸形 resume ID 的问题
- 修复了 Windows 后台服务守护进程在 `~/.claude/daemon` 设置了只读属性时无法启动的问题
- 修复了云会话在空闲过久被认领前出现"Could not resolve authentication method"错误的问题
- 后台会话现在显示更清晰的指导：当跨自动更新的窗口无法提交回复时，以及 `claude daemon status` 解释了版本偏移行为

## 2.1.175

- 新增 `enforceAvailableModels` 托管设置——启用后，`availableModels` 白名单也会约束默认模型（如果默认模型解析到不允许的模型，现在会回退到第一个允许的模型），且用户或项目设置不能再扩大托管的 `availableModels` 列表

## 2.1.174

- 新增 `wheelScrollAccelerationEnabled` 设置，可在全屏模式下禁用鼠标滚轮滚动加速
- 修复了 `/model` 选择器隐藏默认模型所属模型家族的问题——Opus 现在在 Max/Team Premium/Enterprise 计划中显示为独立行，Sonnet 在 Pro/Team 计划中显示为独立行，Opus 在按量付费 API 账户中显示为独立行
- 修复了 `/model` 选择器在 `ANTHROPIC_DEFAULT_SONNET_MODEL` 固定了不同 Sonnet 时仍显示硬编码 Sonnet 版本标签的问题
- 修复了"现已消耗使用额度"横幅错误地为具有按量计费的企业账户显示的问题
- 修复了 Bedrock GovCloud 区域（`us-gov-*`）推导出错误的推理配置文件前缀（`global` 而非 `us-gov`），导致派生模型 ID 出现 400 错误的问题
- 修复了后台会话从启动后台守护进程的 shell 继承另一个会话的 `ANTHROPIC_*` 提供商环境变量（网关 URL、自定义请求头、`/model` 别名）的问题
- 修复了在 macOS 和 Linux 上在 shell 命令被中断或终止后不久退出 Claude Code 时出现 1-2 秒停顿的问题
- 修复了 git commit 共同作者署名显示某些模型的错误模型名称的问题
- 修复了 `/advisor` 对话框预选了被 `availableModels` 白名单阻止的已保存顾问模型的问题
- 修复了技能热重载在单个技能更改时重新发送整个技能列表的问题；现在只重新声明已更改的技能
- 修复了 Workflow 工具 `agent()` 子代理缺少每代理归因头部的问题
- [VSCode] 在账户与使用量对话框（`/usage`）中添加了使用量归因，显示过去 24 小时或 7 天的缓存未命中、长上下文、子代理，以及每个技能/代理/插件/MCP 的细分
- 修复了预热后台工作线程在空闲被认领后出现"Could not resolve authentication method"错误的问题

## 2.1.173

- 修复了带 `[1m]` 后缀的 Fable 5 模型名称未被规范化的问题——Fable 5 默认包含 1M 上下文，因此现在自动去除后缀
- 修复了在 Windows 上沙箱在设置中启用时出现虚假的"沙箱依赖缺失"启动警告的问题

## 2.1.172

- 子代理现在可以生成自己的子代理（最多 5 层深度）
- Amazon Bedrock 现在在未设置 `AWS_REGION` 时从 `~/.aws` 配置文件读取 AWS 区域，与 AWS SDK 优先级一致；`/status` 显示区域来源
- 在 `/plugin` 中浏览市场插件时新增搜索栏
- 为 `claude_code.lines_of_code.count` OTEL 指标新增 `model` 属性
- 修复了使用 1M 上下文但没有使用额度导致会话永久卡住的问题——会话现在自动压缩回标准上下文限制
- 修复了会话中包含多张图片时重复出现"会话中的图片无法处理已被移除"错误的问题
- 修复了代理视图在工作线程回复后保持最多 30 秒显示忙碌旋转动画的问题
- 修复了后台代理可能被调度到预热工作线程时读取另一个目录项目设置（`.mcp.json` 审批、信任）的问题
- 修复了守护进程自动更新后重新附加会话时失败并显示 EAUTH 的问题
- 修复了嵌套代理停止后后台子代理在代理面板中保持"active"状态的问题
- 修复了 `claude agents` 调度输入中 `/model` 建议渲染时带有误导性斜杠前缀并显示组织已禁用的模型的问题
- 修复了 `availableModels` 限制未应用于子代理模型覆盖、代理调度模型选择器和顾问模型的问题
- 修复了 `availableModels` 白名单在使用特定版本 ID（如 `claude-opus-4-8`）时隐藏 `/model` 选择器的 Opus 和 Sonnet 1M 行的问题
- 修复了 Bedrock 上 `/model` 选择器显示提供商不服务的模型的问题——选择一个会静默切换会话模型并在多行上点亮选择标记
- 修复了模型 ID 在 `ANTHROPIC_DEFAULT_OPUS_MODEL` 已包含后缀时获得重复的 1M 上下文后缀（如 `[1M][1m]`）的问题
- 修复了 `opusplan` 模型设置在计划模式下未随 1M 上下文一同附带的问题；`opusplan[1m]` 变通方案现在也能正确切换到计划模式下的 Opus
- 修复了 `WebFetch(domain:*.example.com)` 通配符域规则在允许、拒绝和询问状态下永远无法匹配子域名的问题，以及中间带通配符的文件权限规则（如 `Read(secrets-*/config.json)`）在启动时被拒绝的问题
- 修复了在子代理聊天标签页打开时上箭头提示历史显示主代理提示的问题
- 修复了在远程会话中无法找到挂载的团队记忆存储（`CLAUDE_MEMORY_STORES`）的问题
- 修复了工作流验证拒绝在提示字符串或注释中仅提及 `Date.now()`/`Math.random()` 的脚本的问题
- 在不支持完整鼠标跟踪的 Windows 控制台中禁用鼠标跟踪
- 修复了从长插件列表返回时 `/plugin` 市场列表丢失光标的问题，以及从插件浏览器按 Esc 返回到错误标签页的问题
- 通过移除冗余消息规范化和在流式工具使用状态未更改时避免全消息历史转换来提升长对话性能
- 降低空闲 CPU 使用率：`/goal` 状态芯片在空闲时不再以 5Hz 重新渲染终端，且在子代理并行运行时减少 UI 重新渲染
- 提升了 Chrome 中 Claude 工具加载的性能：浏览器工具现在在单次批量调用中加载，而不是每个工具一次
- 改进了非交互式使用策略拒绝消息，建议开始新会话或更换模型
- `/code-review` 现在在未登录 claude.ai 时保持 `ultra` 选项可见，并解释云端代码审查需要 claude.ai 账户
- 将远程控制页脚指示器缩短为"/rc active"并在窄终端上隐藏
- 停止在远程会话中推广 `/loop`，因为待处理循环无法保持容器存活
- [VSCode] 修复了 PowerShell 工具调用显示为原始 JSON 而非适当命令展示和权限对话框的问题，并剥离了显示 shell 输出中的 ANSI 转义码

## 2.1.170

- 推出 Claude Fable 5：一款我们已将其打造为安全通用的人工智能模型。其能力超越了我们有史以来任何通用模型的水平。更新至 2.1.170 即可访问。https://www.anthropic.com/news/claude-fable-5-mythos-5
- 修复了从 VS Code 集成终端或继承 Claude Code 环境变量的任何 shell 启动时会话不保存对话记录（且不出现在 `--resume` 中）的问题

## 2.1.169

- 自托管运行器：新增 `post-session` 生命周期钩子，在会话结束之后、工作区删除之前运行，可用于快照未提交的工作或导出日志；同时将子进程 SIGTERM→SIGKILL 窗口改为可配置（默认保持 5s 不变）
- 新增 `--safe-mode` 标志（及 `CLAUDE_CODE_SAFE_MODE`），以禁用所有自定义（CLAUDE.md、插件、技能、钩子、MCP 服务器）启动 Claude Code，用于故障排除
- 新增 `/cd` 命令，将会话移至新的工作目录而不破坏会话中途的提示缓存
- 新增 `disableBundledSkills` 设置和 `CLAUDE_CODE_DISABLE_BUNDLED_SKILLS` 环境变量，从模型隐藏捆绑的技能、工作流和内置斜杠命令
- 修复了上/下箭头在长输入行换行行历史中跳到命令历史过去的问题——现在先浏览每个视觉行，历史记录回调在近边缘进入
- 修复了企业托管 MCP 策略（`allowedMcpServers`/`deniedMcpServers`）在重连时、IDE 类型配置、`--mcp-config` 服务器在安装后第一次会话时或远程设置加载前未强制执行的问题；同时修复了无远程设置组织的冷启动慢问题
- 修复了 macOS 上使用 claude.ai 凭证登录的用户每轮开始时有约 30-50ms UI 停顿的问题
- 修复了 `claude -p` 在 Windows 上在斜杠命令/技能扫描时缓慢或看起来挂起的问题（2.1.161 中的回归）
- 修复了在恢复会话时 OAuth token 刷新与工作线程注册同时发生导致远程控制卡在"reconnecting"的问题
- 修复了 Git Credential Manager 的"连接到 GitHub"弹出窗口在 Windows 上启动时后台 git 命令运行时出现的问题（当时没有缓存凭证）
- 修复了页脚提示（如"esc to interrupt"）对有自定义状态行的用户不显示的问题
- 修复了每次重新附加到工作线程死亡时等待的远程会话时过期权限和对话框提示重新出现的问题
- 修复了 `claude agents --json` 遗漏被阻止和刚调度的后台会话的问题；新增 `--all` 包含已完成会话，以及新的 `id` 和 `state` 字段
- 修复了在 Windows Terminal 中 WSL 上从代理返回后代理视图留下过时/乱码帧的问题
- 修复了后台代理在调度到预热工作线程时忽略项目级设置 `env` 值（如 `ANTHROPIC_MODEL`）的问题
- 修复了 Windows 上 MCPB 插件缓存被错误地使失效的问题，导致不必要的重新提取
- 修复了插件 `.in_use` PID 锁文件无限制积累的问题；崩溃会话的过时标记现在每天清理一次
- 修复了不受信任的项目设置能够设置 OTEL 客户端证书路径而无需信任确认的问题
- `/workflows` 现在即使在轮次进行中也能立即打开
- 提升了 `TaskCreate` 可靠性：自动修复格式错误的输入，未加载工具的验证错误包含 schema
- 改进了组织禁用 API 密钥认证时显示的错误消息，根据活动 API 密钥来源提供指导
- 降低了响应流式传输和旋转动画期间的 CPU 使用率
- 在 Vertex/Foundry 上恢复了默认 5 分钟空闲超时，以便流停止时中止而不是无限挂起；设置 `API_FORCE_IDLE_TIMEOUT=0` 可选择退出
- 带有无效条目的远程托管设置现在应用其剩余有效策略并显示验证错误，而不是静默丢弃整个负载
- 后台会话现在在 retire→wake 过程中保留 `--ide`、`--chrome`、`--bare`、`--remote-control` 和其他标志，并加强了对重spawn状态验证
- 后台会话现在被告知共享检出编辑在被输入工作树之前被阻止，避免在 `EnterWorktree` 之前浪费一次被拒绝的编辑
- "CLAUDE.md 太长"警告阈值现在随模型上下文窗口缩放
- Windows 上的自动更新程序在 `claude.exe` 被其他进程持有时不再在会话中重试
- 改进了技能标签在斜杠命令菜单中的颜色对比度
- Apple/Google 计费订阅者（无支付方式）的促销积分领取现在解释了在哪里添加支付方式
- 新增了在运行多个并发会话时建议使用 `claude agents` 的提示

## 2.1.168

- 错误修复和可靠性改进

## 2.1.167

- 错误修复和可靠性改进

## 2.1.166

- 新增 `fallbackModel` 设置，配置最多三个后备模型按顺序在主模型过载或不可用时尝试；`--fallback-model` 现在也适用于交互式会话
- 新增拒绝规则工具名位置中的 glob 模式支持（`"*"` 拒绝所有工具）；允许规则拒绝非 MCP glob，未知工具名称在拒绝规则中会在启动时警告
- 加固了跨会话消息传递：通过 `SendMessage` 从其他 Claude 会话转发的消息不再携带用户授权——接收方拒绝转发的权限请求，自动模式阻止它们
- `MAX_THINKING_TOKENS=0`、`--thinking disabled` 和每模型思考开关现在对通过 Claude API 默认思考的模型禁用思考（第三方提供商不变）
- Claude Code 现在在后备模型上对 API 拒绝的意外不可重试错误重试一次；auth、rate-limit、request-size 和传输错误仍然立即暴露
- `claude update` 现在在下载前宣布目标版本而不是静默
- `claude agents`：在列表中输入 URL 现在过滤到第一个提示包含该 URL 的会话
- 修复了在会话中发送无法处理的图片时出现重复"图片无法处理"错误和额外 token 使用的问题
- 修复了在启动时工作线程注册期间短暂后端中断导致远程会话永久卡住的问题
- 修复了 2026.1+ 上 JetBrains IDE 终端（IntelliJ、PyCharm、WebStorm 等）的闪烁问题，方法为启用同步输出
- 修复了在使用 Kitty 键盘协议的终端（WezTerm、Ghostty、kitty）中 Shift+非 ASCII 字符（如 Shift+ä → Ä）被丢弃的问题
- 修复了 Windows 上 PowerShell 命令验证在杀死进程的子进程持有其输出管道时偶尔远超时间预算而挂起的问题
- 修复了守护进程在 macOS 上连接时死亡后孤立的 `claude --bg-pty-host` 进程以 100% CPU 旋转的问题
- 修复了在切换 `/voice` 后需要 `/login` 来清除过时认证检查的问题
- 修复了带有无效条目的托管设置静默禁用了其余有效策略强制执行的问题
- 修复了托管设置 `allowedMcpServers`/`deniedMcpServers` 谓词在使用 `${VAR}` 引用时无法匹配的问题
- 修复了在 `claude agents` 中重新附加后因 Claude Code 更新而丢失运行中后台任务的后台会话问题
- 修复了 Ctrl+O 对话记录视图中流式传输时思考文本重复的问题
- 修复了 `/doctor` 在远程会话中运行时显示矛盾的"不在远程会话中"检查失败的问题
- 修复了在 `claude agents` 调度和回复输入中输入多行提示时光标卡在第一行末尾的问题
- 修复了在不支持 Unicode 的终端上后台代理行之间出现空行的问题

## 2.1.165

- 错误修复和可靠性改进

## 2.1.163

- 新增 `requiredMinimumVersion` 和 `requiredMaximumVersion` 托管设置——当 Claude Code 版本超出允许范围时拒绝启动，并引导用户使用批准版本
- 新增 `/plugin list` 命令列出已安装插件，带 `--enabled`/`--disabled` 过滤器
- 新增"c 复制"快捷方式到 `/btw`，将原始 markdown 答案复制到剪贴板，在粘贴到其他位置时保留格式
- 钩子：Stop 和 SubagentStop 钩子现在可以返回 `hookSpecificOutput.additionalContext` 来给 Claude 反馈并让轮次继续而不被标记为钩子错误
- 技能：在命令体中加入字面 `$` 后接数字的 `\ `$ 转义语法
- stdio MCP 服务器现在接收与 hooks/Bash 在 `--resume` 时相同的 `CLAUDE_CODE_SESSION_ID`
- 修复了 `claude -p` 在后台命令未退出时永远挂起的问题——后台 shell 现在在 stdin 关闭后约 5s 停止
- 修复了在 Bedrock/Vertex/Foundry 上 `CI=true` 且未设置 Anthropic API 密钥时 `claude -p` 失败并显示"ANTHROPIC_API_KEY required"的问题
- 修复了 `$TMPDIR` 被覆盖为所有命令的 `/tmp/claude-{uid}` 而不仅是沙盒命令的问题（bazel 和 EDR 保护的 Go 工作流下 Bash 命令失败）（2.1.154 中的回归）
- 修复了 Windows 上 Bash 命令在会话 env 目录具有只读属性或在 OneDrive 内时失败并显示"EEXIST: file already exists"的问题
- 修复了托管设置提取在全新配置目录启动期间完成时组织托管权限规则未对整个会话应用的问题
- 修复了 Claude Code 更新后重新附加时 `claude agents` 中后台会话丢失其运行中后台任务的问题
- 修复了按 Esc 退出代理视图时的终端错位和多秒挂起问题
- 修复了在桌面应用中点击后台任务 chip 上的 Stop 在底层进程已消失时未清除 chip 的问题
- 修复了在粘贴操作结束标记被终端丢弃后键盘输入永久无响应的问题
- 修复了 hook `if: "Bash(...)"` 条件触发时