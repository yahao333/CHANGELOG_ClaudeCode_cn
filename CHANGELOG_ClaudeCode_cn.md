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