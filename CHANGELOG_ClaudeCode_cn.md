# Changelog

## 2.1.87

- 修复了 Cowork Dispatch 中消息未能送达的问题

## 2.1.86

- 新增 `X-Claude-Code-Session-Id` 请求头，方便代理按会话聚合请求
- 将 `.jj` 和 `.sl` 添加到 VCS 目录排除列表，避免 Grep 和文件自动补全进入 Jujutsu 或 Sapling 元数据目录
- 修复了 `--resume` 在 v2.1.85 之前创建的会话上失败的问题（报错"tool_use ids were found without tool_result blocks"）
- 修复了配置条件技能或规则时，Write/Edit/Read 操作项目根目录之外文件（如 `~/.claude/CLAUDE.md`）失败的问题
- 修复了每次技能调用时不必要的配置磁盘写入，可能导致性能问题和 Windows 上的配置损坏
- 修复了在使用 `/feedback` 时，长会话和大记录文件可能导致内存耗尽崩溃的问题
- 修复了 `--bare` 模式在交互会话中丢失 MCP 工具并静默丢弃中轮排入队列消息的问题
- 修复了 `c` 快捷键只复制 OAuth 登录 URL 约 20 个字符而非完整 URL 的问题
- 修复了窄终端多行换行时遮罩输入（如 OAuth 代码粘贴）泄露 token 开头的问题
- 修复了自 v2.1.83 起官方市场插件脚本在 macOS/Linux 上因"Permission denied"失败的问题
- 修复了运行多个 Claude Code 实例并在其中之一使用 `/model` 时，状态栏显示另一个会话模型的问题
- 修复了在长对话底部滚轮滚动或点击选择后，新消息不跟随滚动的问题
- 修复了 `/plugin` 卸载对话框：按 `n` 现在可以正确卸载插件同时保留其数据目录
- 修复了点击后按回车可能导致记录在响应到达前保持空白的问题
- 修复了删除关键词后 `ultrathink` 提示仍然残留的问题
- 修复了长会话中 markdown/高亮渲染缓存保留完整内容字符串导致的内存增长问题
- 减少了配置多个 claude.ai MCP 连接器时的启动事件循环阻塞（macOS 密钥链缓存从 5 秒延长至 30 秒）
- 减少了使用 `@` 提及文件时的 token 开销——原始字符串内容不再进行 JSON 转义
- 通过从工具描述中移除动态内容，提高了 Bedrock、Vertex 和 Foundry 用户的提示缓存命中率
- "已保存 N 条记忆"通知中的记忆文件名现在悬停时高亮并可点击打开
- `/skills` 列表中的技能描述现在限制在 250 个字符以内以减少上下文占用
- 将 `/skills` 菜单改为按字母顺序排列便于浏览
- 自动模式现显示"您的计划不可用"而非"暂时不可用"（当被计划限制禁用时）
- [VSCode] 修复了扩展在长时间运行操作期间错误显示"Not responding"的问题
- [VSCode] 修复了 OAuth token 刷新后（登录后 8 小时）Max 计划用户默认使用 Sonnet 的问题
- Read 工具现在使用紧凑的行号格式并去重未更改的重读，减少 token 使用

## 2.1.85

- 新增 `CLAUDE_CODE_MCP_SERVER_NAME` 和 `CLAUDE_CODE_MCP_SERVER_URL` 环境变量给 MCP `headersHelper` 脚本，允许一个 helper 服务多个服务器
- 新增条件 `if` 字段用于钩子，使用权限规则语法（如 `Bash(git *)`）过滤执行时机，减少进程生成开销
- 新增计划任务（`/loop`、`CronCreate`）触发时在记录中打时间戳
- 新增粘贴图片时 `[Image #N]` 占位符后的尾随空格
- 深度链接查询（`claude-cli://open?q=…`）现在支持最多 5000 字符，长预填提示附带"滚动查看"警告
- MCP OAuth 现遵循 RFC 9728 Protected Resource Metadata 发现来查找授权服务器
- 被组织策略阻止的插件（`managed-settings.json`）无法再安装或启用，且在市场视图中隐藏
- PreToolUse 钩子现可返回 `updatedInput` 以及 `permissionDecision: "allow"` 来满足 `AskUserQuestion`，实现通过自身 UI 收集答案的无头集成
- OpenTelemetry tool_result 事件中的 `tool_parameters` 现由 `OTEL_LOG_TOOL_DETAILS=1` 控制
- 修复了 `/compact` 在对话增长到紧致请求本身无法容纳时失败的问题（报错"context exceeded"）
- 修复了插件安装位置与设置中声明位置不同时 `/plugin enable` 和 `/plugin disable` 失败的问题
- 修复了 `--worktree` 在非 git 仓库中在 `WorktreeCreate` 钩子运行前就报错退出的问题
- 修复了 `deniedMcpServers` 设置未能阻止 claude.ai MCP 服务器的问题
- 修复了多显示器设置上 `switch_display` 在计算机使用工具中返回"此会话不可用"的问题
- 修复了 `OTEL_LOGS_EXPORTER`、`OTEL_METRICS_EXPORTER` 或 `OTEL_TRACES_EXPORTER` 设置为 `none` 时的崩溃问题
- 修复了非原生构建中 diff 语法高亮不工作的问题
- 修复了刷新 token 存在时 MCP 升级授权失败的问题——通过 `403 insufficient_scope` 请求提升作用域的服务器现在正确触发重新授权流程
- 修复了流式响应中断时远程会话中的内存泄漏问题
- 修复了边缘连接波动期间持续的 ECONNRESET 错误，重试时使用新的 TCP 连接
- 修复了运行某些斜杠命令后提示卡在队列中无法通过上箭头找回的问题
- 修复了 Python Agent SDK：通过 `--mcp-config` 传递的 `type:'sdk'` MCP 服务器在启动期间不再被丢弃
- 修复了通过 SSH 或 VS Code 集成终端运行时原始键序列出现在提示中的问题
- 修复了权限解析后 Remote Control 会话状态一直停留在"需要操作"的问题
- 修复了 shift+enter 和 meta+enter 被类型建议拦截而非插入换行符的问题
- 修复了滚动过程中流式传输时陈旧内容渗透的问题
- 修复了 Ghostty、Kitty、WezTerm 等支持 Kitty 键盘协议的终端退出后终端处于增强键盘模式的问题——Ctrl+C 和 Ctrl+D 现在退出后正常工作
- 改进了 `@` 提及文件自动补全在大型仓库上的性能
- 改进了 PowerShell 危险命令检测
- 通过用纯 TypeScript 实现替换 WASM yoga-layout 改进了大记录滚动性能
- 减少了紧致触发时大会话的 UI 卡顿

## 2.1.84

- 新增 Windows 选配预览的 PowerShell 工具。详见 https://code.claude.com/docs/en/tools-reference#powershell-tool
- 新增 `ANTHROPIC_DEFAULT_{OPUS,SONNET,HAIKU}_MODEL_SUPPORTS` 环境变量，用于覆盖第三方（Bedrock、Vertex、Foundry）固定默认模型的努力/思考能力检测，以及 `_MODEL_NAME`/`_DESCRIPTION` 用于自定义 `/model` 选择器标签
- 新增 `CLAUDE_STREAM_IDLE_TIMEOUT_MS` 环境变量配置流式空闲看门狗阈值（默认 90 秒）
- 新增 `TaskCreated` 钩子，在通过 `TaskCreate` 创建任务时触发
- 新增 `WorktreeCreate` 钩子对 `type: "http"` 的支持——通过响应 JSON 中的 `hookSpecificOutput.worktreePath` 返回创建的工作树路径
- 新增 `allowedChannelPlugins` 托管设置，供团队/企业管理员定义渠道插件白名单
- 新增 `x-client-request-id` 请求头用于调试超时
- 新增 75 分钟以上返回后的空闲返回提示，提示用户使用 `/clear`，减少陈旧会话上不必要的 token 重新缓存
- 深度链接（`claude-cli://`）现在在你首选的终端打开，而非检测列表中的第一个终端
- 规则和技能 `paths:` 前置参数现在接受 YAML glob 列表
- MCP 工具描述和服务器说明现在限制在 2KB 以防止 OpenAPI 生成的服务器膨胀上下文
- 本地和通过 claude.ai 连接器配置的 MCP 服务器现在去重——本地配置优先
- 出现在交互提示符上看起来卡住的背景 bash 任务现在约 45 秒后显示通知
- ≥1M 的 token 计数现在显示为"1.5m"而非"1512.6k"
- 启用 `ToolSearch` 时全局系统提示缓存现在可用，包括配置了 MCP 工具的用户
- 修复了语音按住说话：按住语音键不再向文本输入泄露字符，记录现在在正确位置插入
- 修复了页脚项目获得焦点时上下箭头键无响应的问题
- 修复了多行输入中行边界处 `Ctrl+U`（删除到行首）在边界处无效的问题，连续 `Ctrl+U` 现在可以跨行清除
- 修复了默认和弦绑定解绑 null（如 `"ctrl+x ctrl-k": null`）仍进入和弦等待模式而非释放前缀键的问题
- 修复了鼠标事件向记录搜索输入插入文字"mouse"的问题
- 修复了外部会话使用 `--json-schema` 且子代理也指定 schema 时工作流子代理 API 400 失败的问题
- 修复了某些终端用户消息气泡中某些 emoji 缺少背景色的问题
- 修复了"允许 Claude 为此会话编辑其自身设置"权限选项对于有 `Edit(.claude)` 允许规则的用户不生效的问题
- 修复了生成大编辑文件附件片段时的挂起问题
- 修复了服务器重连时 MCP 工具/资源缓存泄漏问题
- 修复了部分克隆仓库（Scalar/GVFS）触发大量 blob 下载时的启动性能问题
- 修复了本地终端光标未跟踪文本输入插入符号的问题，IME 组合（CJK 输入）现在内联渲染，屏幕阅读器可以跟随输入位置
- 修复了 macOS 上由瞬时密钥链读取失败引起的虚假"未登录"错误
- 修复了冷启动竞争条件，核心工具可能被延迟但旁路未激活，导致 typed 参数上 Edit/Write 因 InputValidationError 失败
- 改进了对危险移除 Windows 驱动器根目录（`C:\`、`C:\Windows` 等）的检测
- 通过并行运行 `setup()` 与斜杠命令和代理加载，改进了约 30ms 的交互式启动
- 改进了带 MCP 服务器的 `claude "prompt"` 启动——REPL 现在立即渲染而非阻塞等待所有服务器连接
- 改进了 Remote Control，阻止时显示具体原因而非通用"尚未启用"消息
- 改进了 p90 提示缓存命中率
- 减少了长会话中滚动到顶部的重置次数
- 减少了动画工具进度滚动到视口上方时的终端闪烁
- 更改问题/PR 引用仅在写成 `owner/repo#123` 时才变为可点击链接——裸 `#123` 不再自动链接
- 当前 auth 设置不可用的斜杠命令（`/voice`、`/mobile`、`/chrome`、`/upgrade` 等）现在隐藏而非显示
- [VSCode] 新增限流警告横幅，显示使用百分比和重置时间
- `/stats` 中 Ctrl+S 统计截图现在在所有构建中可用，快 16 倍

## 2.1.83

- 新增 `managed-settings.d/` 目录作为 `managed-settings.json` 的插入目录，允许不同团队部署独立策略片段，按字母顺序合并
- 新增 `CwdChanged` 和 `FileChanged` 钩子事件，用于反应式环境管理（如 direnv）
- 新增 `sandbox.failIfUnavailable` 设置，在启用沙箱但无法启动时退出并报错，而非无沙箱运行
- 新增 `disableDeepLinkRegistration` 设置以防止 `claude-cli://` 协议处理器注册
- 新增 `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB=1` 以从子进程环境（bash 工具、钩子、MCP stdio 服务器）中剥离 Anthropic 和云提供商凭据
- 新增记录搜索——在记录模式下按 `/` 搜索，`n`/`N` 逐步浏览匹配项
- 新增 `Ctrl+X Ctrl+E` 作为打开外部编辑器的别名（readline 原生绑定；`Ctrl+G` 仍然有效）
- 粘贴的图片现在在光标处插入 `[Image #N]` 芯片，便于在提示中按位置引用
- 代理现在可以声明 `initialPrompt` 前置参数以自动提交第一轮
- `chat:killAgents` 和 `chat:fastMode` 现在可通过 `~/.claude/keybindings.json` 重新绑定
- 修复了退出时鼠标跟踪转义序列泄露到 shell 提示符的问题
- 修复了 macOS 上 Claude Code 退出时挂起的问题
- 修复了空闲几秒后屏幕闪烁空白的问题
- 修复了差异非常大的文件（共同行很少）时挂起的问题——diff 现在 5 秒后超时并优雅降级
- 修复了启用语音输入时启动时 1-8 秒 UI 冻结的问题，原因是热切加载原生音频模块
- 修复了启动回归问题，Claude Code 会等待约 3 秒获取 claude.ai MCP 配置后才继续
- 修复了 `--mcp-config` CLI 标志绕过 `allowedMcpServers`/`deniedMcpServers` 托管策略执行的问题
- 修复了 claude.ai MCP 连接器（Slack、Gmail 等）在单轮 `--print` 模式下不可用的问题
- 修复了 Claude Code 退出时 `caffeinate` 进程未正确终止、阻止 Mac 进入睡眠的问题
- 修复了 tab 接受 `!` 前缀命令建议时 bash 模式未激活的问题
- 修复了陈旧斜杠命令选择在不导航建议后显示错误高亮命令的问题
- 修复了 `/config` 菜单同时显示搜索光标和列表选择的问题
- 修复了上下文紧致后后台子代理变得不可见，可能导致重复代理被生成的问题
- 修复了 git 或 API 调用在清理期间挂起时后台代理任务保持"运行"状态的问题
- 修复了升级后首次启动时 `--channels` 显示"渠道目前不可用"的问题
- 修复了卸载的插件钩子继续触发直到下一次会话的问题
- 修复了流式响应期间排队命令闪烁的问题
- 修复了斜杠命令在消息处理时提交被作为文本发送给模型的问题
- 修复了在 offscreen 滚动完成后折叠的读/搜索组滚动弹跳的问题
- 修复了模型开始或停止思考时滚动到顶部的问题
- 修复了 SDK 会话历史记录在恢复时因钩子进度/附件消息导致 parentUuid 链分叉而丢失的问题
- 修复了在终端窗口外释放鼠标时复制选择未触发的问题
- 修复了高度受限列表中项目溢出时出现幽灵字符的问题
- 修复了空闲提示符上 `Ctrl+B` 干扰 readline backward-char 的问题——现在仅在有可后台化的前台任务时触发
- 修复了工具结果文件从未清理、忽略 `cleanupPeriodDays` 设置的问题
- 修复了释放语音按住说话后空格键被吞掉最多 3 秒的问题
- 修复了在没有音频硬件的 Linux 上使用语音模式时 ALSA 库错误破坏终端 UI 的问题（Docker、无头、WSL1）
- 修复了 Termux/Android 上语音模式 SoX 检测的问题，在这些平台上生成 `which` 受到内核限制
- 修复了 Remote Control 会话在 web 会话列表中显示为 Idle 而实际正在运行的问题
- 修复了配置驱动模式下页脚导航选择不可见的 Remote Control 药丸的问题
- 修复了远程会话中工具使用 ID 无限累积的内存泄漏问题
- 改进了 Bedrock SDK 冷启动延迟，将配置文件获取与其他启动工作重叠
- 改进了大会话上 `--resume` 的内存使用和启动延迟
- 改进了插件启动——命令、技能和代理现在从磁盘缓存加载，无需重新获取
- 改进了 Remote Control 会话标题：AI 生成的标题现在在第一条消息后几秒内出现
- 改进了 `WebFetch` 标识为 `Claude-User`，以便站点运营商可以通过 `robots.txt` 识别并允许 Claude Code 流量
- 减少了大页面 `WebFetch` 峰值内存使用
- 减少了长会话中滚动累积重置，从每轮一次减少到每约 50 条消息一次
- 加快了带有未经身份验证的 HTTP/SSE MCP 服务器的 `claude -p` 启动（节省约 600ms）
- Bash ghost-text 建议现在立即包含刚提交的命令
- 增加了非流式回退 token 上限（21k → 64k）和超时（120s → 300s 本地），使回退请求不太可能被截断
- 在任何响应前中断提示现在自动恢复你的输入，以便编辑和重新提交
- `/status` 现在在 Claude 响应时可用，而非排队等待回合结束
- 重复组织管理连接器的插件 MCP 服务器现在被抑制而非运行第二个连接
- Linux：在注册 `claude-cli://` 协议处理器时尊重 `XDG_DATA_HOME`
- 将"停止所有后台代理"键绑定从 `Ctrl+F` 改为 `Ctrl+X Ctrl+K`，避免与 readline forward-char 冲突
- 弃用 `TaskOutput` 工具，转而使用 `Read` 读取后台任务的输出文件路径
- 新增 `CLAUDE_CODE_DISABLE_NONSTREAMING_FALLBACK` 环境变量以在流式传输失败时禁用非流式回退
- 插件选项（`manifest.userConfig`）现在可从外部获取——插件可在启用时提示配置，`sensitive: true` 值存储在密钥链（macOS）或其他平台的受保护凭据文件中
- Claude 现在可以引用剪贴板粘贴图片的磁盘路径以进行文件操作
- `Ctrl+L` 现在清除屏幕并强制完全重绘——当 Cmd+K 使 UI 部分空白时使用它恢复。使用 `Ctrl+U` 或双 Esc 清除提示输入。
- `--bare -p`（SDK 模式）到 API 请求快约 14%
- 内存：`MEMORY.md` 索引现在也在 25KB 处截断，而非仅 200 行
- `--channels` 激活时禁用 `AskUserQuestion` 和计划模式工具
- 修复了粘贴图片在失败的工具调用期间排队时的 API 400 错误
- 修复了 SSE 连接在调用中途断开并耗尽重连尝试时 MCP 工具调用无限挂起的问题
- 修复了后台代理在第一个用户消息前完成时 Remote Control 会话标题显示原始 XML 的问题
- 修复了容器重启后由于记录链中进度消息缺口导致远程会话忘记对话历史的问题
- 修复了瞬时 auth 错误后远程会话需要重新登录而非自动重试的问题
- 修复了沙箱模式下 `rg ... | wc -l` 及类似管道命令在 Linux 上挂起并返回 `0` 的问题
- 修复了 CJK IME 插入全角空格时语音输入按住说话未激活的问题
- 修复了工作树名称包含斜杠时 `--worktree` 静默挂起的问题
- [VSCode] 后端 60 秒未响应时 spinner 变为红色并显示"Not responding"
- [VSCode] 修复了通过 URL 重新打开会话或重启后会话历史记录未正确加载的问题
- [VSCode] 新增 Esc 两次（或 `/rewind`）打开键盘可导航的倒带选择器
- [VSCode] 修复了会话缓存变陈旧后"从这里分叉对话"和倒带操作静默失败的问题

## 2.1.81

- 新增 `--bare` 标志用于脚本化的 `-p` 调用——跳过钩子、LSP、插件同步和技能目录遍历；需要 `ANTHROPIC_API_KEY` 或通过 `--settings` 的 `apiKeyHelper`（禁用 OAuth 和密钥链 auth）；完全禁用自动内存
- 新增 `--channels` 权限中继——声明权限能力的渠道服务器可以将工具批准提示转发到你的手机
- 修复了多个并发 Claude Code 会话在一个会话刷新其 OAuth token 时需要重复身份验证的问题
- 修复了语音模式静默吞下重试失败并显示误导性"检查网络"消息而非实际错误的问题
- 修复了服务器静默断开 WebSocket 连接时语音模式音频未恢复的问题
- 修复了 `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` 未抑制结构化输出 beta 头的问题，导致转发到 Vertex/Bedrock 的代理网关返回 400 错误
- 修复了没有其他托管设置配置的团队/企业组织 `--channels` 绕过的问题
- 修复了 Node.js 18 上的崩溃问题
- 修复了包含字符串中短横线的 Bash 命令出现不必要权限提示的问题
- 修复了插件目录在会话中途删除时插件钩子阻止提示提交的问题
- 修复了任务在轮询间隔之间完成时后台代理任务输出可能无限挂起的竞争条件
- 恢复了处于工作树中的会话现在切换回该工作树
- 修复了活动响应期间使用 `/btw` 时未包含粘贴文本的问题
- 修复了快速 Cmd+Tab 后粘贴可能胜过 tmux 下剪贴板复制的竞争问题
- 修复了终端标签标题未随自动生成的会话描述更新的问题
- 修复了不可见钩子附件在记录模式下使消息计数膨胀的问题
- 修复了 Remote Control 会话显示通用标题而非从第一个提示派生的标题的问题
- 修复了 `/rename` 未同步 Remote Control 会话标题的问题
- 修复了 Remote Control `/exit` 未可靠归档会话的问题
- 改进了 MCP 读/搜索工具调用折叠为单个"查询了 {server}"行（用 Ctrl+O 展开）
- 改进了 `!` bash 模式可发现性——当你需要运行交互式命令时 Claude 现在会建议它
- 改进了插件新鲜度——跟踪引用的插件现在每次加载时重新克隆以获取上游更改
- 改进了 Remote Control 会话标题，在第三条消息后刷新
- 更新了 MCP OAuth 以支持客户端 ID 元数据文档（CIMD / SEP-991），用于没有动态客户端注册的服务器
- 更改计划模式默认隐藏"清除上下文"选项（通过 `"showClearContextOnPlanAccept": true` 恢复）
- 在 Windows（包含 Windows Terminal 中的 WSL）上禁用逐行响应流式传输，因渲染问题
- [VSCode] 修复了 Windows 上 Git Bash 使用 Bash 工具时 PATH 继承问题（v2.1.78 回归）

## 2.1.80

- 新增 `rate_limits` 字段到状态栏脚本，用于显示 claude.ai 速率限制使用情况（5 小时和 7 天窗口，含 `used_percentage` 和 `resets_at`）
- 新增 `source: 'settings'` 插件市场源——在 settings.json 中内联声明插件条目
- 新增 CLI 工具使用检测到插件提示，除了文件模式匹配
- 新增 `effort` 前置参数支持用于技能和斜杠命令，以在调用时覆盖模型努力级别
- 新增 `--channels`（研究预览）——允许 MCP 服务器将消息推入你的会话
- 修复了 `--resume` 丢弃并行工具结果的问题——带有并行工具调用的会话现在恢复所有 tool_use/tool_result 对，而非显示 `[Tool result missing]` 占位符
- 修复了通过非浏览器 TLS 指纹的 Cloudflare 机器人检测导致的语音模式 WebSocket 失败问题
- 修复了通过 API 代理、Bedrock 或 Vertex 使用细粒度工具流式传输时的 400 错误问题
- 修复了 `/remote-control` 出现在无法运行的网关和第三方提供商部署上的问题
- 修复了 `/sandbox` 标签切换不响应 Tab 或箭头键的问题
- 改进了大型 git 仓库中 `@` 文件自动补全的响应能力
- 改进了 `/effort` 显示自动当前解析的内容，与状态栏指示器匹配
- 改进了 `/permissions`——Tab 和箭头键现在在列表内切换标签
- 改进了后台任务面板——左箭头现在从列表视图关闭
- 简化了插件安装提示，使用单个 `/plugin install` 命令而非两步流程
- 减少了大型仓库上的启动内存使用（250k 文件仓库节省约 80MB）
- 修复了当 `remote-settings.json` 从先前会话缓存时托管设置（`enabledPlugins`、`permissions.defaultMode`、策略集环境变量）在启动时未应用的问题

## 2.1.79

- 新增 `claude auth login --console` 标志用于 Anthropic Console（API 计费）身份验证
- 新增"显示轮次时长"切换到 `/config` 菜单
- 修复了作为子进程生成时没有显式 stdin 的 `claude -p` 挂起的问题（如 Python `subprocess.run`）
- 修复了 `-p`（打印）模式下 Ctrl+C 不工作的问题
- 修复了在流式传输期间触发时 `/btw` 返回主代理输出而非回答附带问题的问题
- 修复了 `voiceEnabled: true` 设置时语音模式在启动时未正确激活的问题
- 修复了 `/permissions` 中左右箭头标签导航的问题
- 修复了 `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` 未阻止启动时终端标题设置的问题
- 修复了工作区信任阻止时自定义状态行显示为空的问题
- 修复了企业用户无法在速率限制（429）错误上重试的问题
- 修复了使用交互式 `/resume` 切换会话时 `SessionEnd` 钩子未触发的问题
- 通过约 18MB 改进所有场景的启动内存使用
- 改进非流式 API 回退，每次尝试 2 分钟超时，防止会话无限挂起
- `CLAUDE_CODE_PLUGIN_SEED_DIR` 现在支持多个种子目录，用平台路径分隔符分隔（Unix 上 `:`，Windows 上 `;`）
- [VSCode] 新增 `/remote-control`——将你的会话桥接到 claude.ai/code 以从浏览器或手机继续
- [VSCode] 会话标签现在根据你的第一条消息获得 AI 生成的标题
- [VSCode] 修复了响应完成后思考药丸显示"Thinking"而非"Thought for Ns"的问题
- [VSCode] 修复了从左侧边栏打开会话时会话差异按钮缺失的问题

## 2.1.78

- 新增 `StopFailure` 钩子事件，在因 API 错误（速率限制、auth 失败等）导致轮次结束时触发
- 新增 `${CLAUDE_PLUGIN_DATA}` 变量用于插件持久状态，在插件更新后保留；`/plugin uninstall` 在删除前提示
- 新增插件附带的代理对 `effort`、`maxTurns` 和 `disallowedTools` 前置参数的支持
- 在 tmux 内运行且 `set -g allow-passthrough on` 时，终端通知（iTerm2/Kitty/Ghostty 弹出窗口、进度条）现在到达外部终端
- 响应文本现在在生成时逐行流式传输
- 修复了 Linux 沙箱模式下 `git log HEAD` 因"ambiguous argument"失败，以及 stub 文件污染工作目录中 `git status` 的问题
- 修复了 `cc log` 和 `--resume` 在使用子代理的大型会话（>5MB）中静默截断对话历史的问题
- 修复了 API 错误触发的停止钩子将阻塞错误重新反馈给模型而导致无限循环的问题
- 修复了 `deny: ["mcp__servername"]` 权限规则未在发送给模型前移除 MCP 服务器工具的问题，允许其查看和尝试被阻止的工具
- 修复了 `sandbox.filesystem.allowWrite` 不适用于绝对路径的问题（之前需要 `//` 前缀）
- 修复了 `/sandbox` 依赖项选项卡在 macOS 上显示 Linux 先决条件而非 macOS 特定信息的问题
- **安全：** 修复了在设置了 `sandbox.enabled: true` 但缺少依赖项时静默禁用沙箱的问题——现在显示可见的启动警告
- 修复了 `.git`、`.claude` 和其他受保护目录在 `bypassPermissions` 模式下无需提示即可写入的问题
- 修复了正常模式下 ctrl+u 滚动而非 readline kill-line 的问题（ctrl+u/ctrl+d 半页滚动仅移到记录模式）
- 修复了语音模式修饰符组合按住说话键绑定（如 ctrl+k）需要按住而非立即激活的问题
- 修复了 WSL2 上使用 WSLg 的语音模式不工作的问题（Windows 11）；WSL1/Win10 用户现在收到明确错误
- 修复了 `--worktree` 标志未从工作树目录加载技能和钩子的问题
- 修复了 `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` 和 `includeGitInstructions` 设置未抑制 git 状态部分在系统提示中的显示问题
- 修复了 VS Code 从 Dock/Spotlight 启动时 Bash 工具找不到 Homebrew 和其他 PATH 依赖二进制文件的问题
- 修复了未宣传真彩色支持的 VS Code/Cursor/code-server 终端中 Claude 橙色褪色的问题
- 新增 `ANTHROPIC_CUSTOM_MODEL_OPTION` 环境变量以向 `/model` 选择器添加自定义条目，可选带 `_NAME` 和 `_DESCRIPTION` 后缀变量用于显示
- 修复了 Haiku 模型使用时被 `ANTHROPIC_BETAS` 环境变量静默忽略的问题
- 修复了排队提示被连接而没有换行符分隔符的问题
- 改进了恢复大型会话时的内存使用和启动时间
- [VSCode] 修复了打开侧边栏时已认证状态下短暂闪烁登录屏幕的问题
- [VSCode] 修复了选择 Opus 时出现"API Error: Rate limit reached"的问题——型号下拉菜单不再向计划层级未知的订阅者提供 1M 上下文变体

## 2.1.77

- 将 Claude Opus 4.6 的默认最大输出 token 限制增加到 64k，Opus 4.6 和 Sonnet 4.6 型号的上限增加到 128k
- 新增 `allowRead` 沙箱文件系统设置以在 `denyRead` 区域内重新允许读取访问
- `/copy` 现在接受可选索引：`/copy N` 复制第 N 条最新的助手响应
- 修复了复合 bash 命令（如 `cd src && npm test`）上的"始终允许"保存整个字符串的单一规则而非每个子命令的规则，导致死规则和重复权限提示
- 修复了斜杠命令叠加层反复打开和关闭时自动更新程序开始重叠的二进制下载，累积数十 GB 内存的问题
- 修复了 `--resume` 因内存提取写入和主记录之间的竞争而静默截断最近对话历史的问题
- 修复了 PreToolUse 钩子返回 `"allow"` 绕过 `deny` 权限规则（包括企业托管设置）的问题
- 修复了 Write 工具在覆盖 CRLF 文件或 CRLF 目录中创建文件时静默转换行结束符的问题
- 修复了长会话中进度消息在紧致后幸存的内存增长问题
- 修复了 API 回退到非流式模式时未跟踪成本和 token 使用的问题
- 修复了 `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` 未剥离 beta 工具模式字段的问题，导致代理网关拒绝请求
- 修复了系统临时目录路径包含空格时 Bash 工具报告成功命令错误的问题
- 修复了粘贴后立即键入时粘贴丢失的问题
- 修复了 `/feedback` 文本输入中 Ctrl+D 向后删除而非第二次按下退出会话的问题
- 修复了将 0 字节图像文件拖入提示时出现 API 错误的问题
- 修复了 Claude Desktop 会话错误使用终端 CLI 配置的 API key 而非 OAuth 的问题
- 修复了同一 monorepo 不同子目录的 `git-subdir` 插件在插件缓存中冲突的问题
- 修复了有序列表编号在终端 UI 中不渲染的问题
- 修复了陈旧工作树清理可能删除刚从先前崩溃恢复的代理工作树的竞争条件
- 修复了在代理运行时打开 `/mcp` 或类似对话框时的输入死锁问题
- 修复了 Backspace 和 Delete 键在 vim 正常模式下不工作的问题
- 修复了切换 vim 模式时状态行未更新的问题
- 修复了在 VS Code、Cursor 和其他基于 xterm.js 的终端中 Cmd+click 打开超链接两次的问题
- 修复了默认配置下 tmux 中终端默认背景色渲染为终端默认的问题
- 修复了 iTerm2 会话在通过 SSH 在 tmux 内选择文本时崩溃的问题
- 修复了 tmux 会话中剪贴板复制静默失败的问题；复制 toast 现在指示使用 `⌘V` 或 tmux `prefix+]` 粘贴
- 修复了设置、权限和沙箱对话框中导航列表时左右箭头意外切换标签的问题
- 修复了 Claude Code 在 tmux 或 screen 内启动时 IDE 集成未自动连接的问题
- 修复了 CJK 字符在右边缘剪断时视觉渗透到相邻 UI 元素的问题
- 修复了领导退出时队友窗格未关闭的问题
- 修复了 iTerm2 自动模式未检测到本机分割窗格队友的 iTerm2 的问题
- 通过在并行与模块加载的密钥链凭据读取，加快 macOS 启动约 60ms
- 加快了分叉重型和超大型会话的 `--resume`——加载快高达 45%，峰值内存减少约 100-150MB
- 改进了 Esc 中止飞行中非流式 API 请求
- 改进了 `claude plugin validate` 以检查技能、代理和命令前置参数以及 `hooks/hooks.json`，捕获 YAML 解析错误和模式冲突
- 后台 bash 任务现在在输出超过 5GB 时被终止，防止失控进程填满磁盘
- 当你接受计划时，会话现在从计划内容自动命名
- 改进了与 `CLAUDE_CODE_PLUGIN_SEED_DIR` 正确组合的头部模式插件安装
- 当 `apiKeyHelper` 超过 10 秒时显示通知，防止阻塞主循环
- Agent 工具不再接受 `resume` 参数——使用 `SendMessage({to: agentId})` 继续先前生成的代理
- `SendMessage` 现在自动恢复停止的后台代理而非返回错误
- 将 `/fork` 重命名为 `/branch`（`/fork` 仍作为别名工作）
- [VSCode] 改进了计划预览标签标题使用计划标题而非"Claude 的计划"
- [VSCode] 当 option+click 在 macOS 上不触发本机选择时，页脚现在指向 `macOptionClickForcesSelection` 设置

## 2.1.76

- 新增 MCP elicitation 支持——MCP 服务器现在可以通过交互式对话框（表单字段或浏览器 URL）请求结构化输入
- 新增 `Elicitation` 和 `ElicitationResult` 钩子以在发送回之前拦截和覆盖响应
- 新增 `-n` / `--name <name>` CLI 标志以在启动时设置会话显示名称
- 新增 `worktree.sparsePaths` 设置，用于大型 monorepo 中 `claude --worktree` 通过 git 稀疏检出只检出不你需要的目录
- 新增 `PostCompact` 钩子，在紧致完成后触发
- 新增 `/effort` 斜杠命令以设置模型努力级别
- 新增会话质量调查——企业管理员可以通过 `feedbackSurveyRate` 设置配置采样率
- 修复了通过 `ToolSearch` 加载的延迟工具在会话紧致后丢失输入模式的问题，导致数组和数字参数因类型错误被拒绝
- 修复了斜杠命令显示"未知技能"的问题
- 修复了计划模式在计划已接受后要求重新批准的问题
- 修复了权限对话框或计划编辑器打时语音模式吞掉按键的问题
- 修复了通过 npm 安装时 `/voice` 在 Windows 上不工作的问题
- 修复了在 1M 上下文会话上使用 `model:` 前置参数调用技能时出现虚假"上下文限制达到"的问题
- 修复了使用非标准模型字符串时"此模型不支持自适应思考"错误的问题
- 修复了包含 `#` 的引号参数中 `Bash(cmd:*)` 权限规则不匹配的问题
- 修复了 Bash 权限对话框中"不再询问"对管道和复合命令显示完整原始命令的问题
- 修复了连续失败后自动紧致无限重试的问题——断路器现在在 3 次尝试后停止
- 修复了成功重连后 MCP 重连旋转图标持续存在的问题
- 修复了 LSP 管理器在市场协调前初始化时 LSP 插件未注册服务器的问题
- 修复了通过 SSH 复制 tmux 中的剪贴板——现在尝试直接终端写入和 tmux 剪贴板集成
- 修复了 `/export` 在成功消息中仅显示文件名而非完整文件路径的问题
- 修复了选择文本后会话未自动滚动到新消息的问题
- 修复了 Escape 键无法退出登录方法选择屏幕的问题
- 修复了多个 Remote Control 问题：服务器 reap 空闲环境时会话静默死亡、快速消息被一一排队而非批处理、以及 JWT 刷新后导致重传的死工作项
- 修复了扩展 WebSocket 断开连接后桥接会话恢复失败的问题
- 修复了输入确切名称时找不到被软隐藏的斜杠命令的问题
- 改进了通过直接读取 git refs 跳过冗余 `git fetch` 时 `--worktree` 启动性能
- 改进了后台代理行为——终止后台代理现在在对话上下文中保留其部分结果
- 改进了模型回退通知——现在始终可见而非隐藏在详细模式之后，模型名称更人性化
- 改进了深色终端主题上的块引用可读性——文本现在使用左条斜体而非暗淡
- 改进了陈旧工作树清理——在中断的并行运行后遗留的工作树现在自动清理
- 改进了 Remote Control 会话标题——现在从你的第一个提示派生而非显示"交互式会话"
- 改进了 `/voice` 以在启用时显示你的听写语言并在 `language` 设置不支持语音输入时警告
- 更新了 `--plugin-dir` 以仅接受一个路径支持子命令——对多个目录使用重复的 `--plugin-dir`
- [VSCode] 修复了包含逗号的 .gitignore 模式从 @-提及文件选择器中静默排除整个文件类型的问题

## 2.1.75

- 默认情况下为 Max、Team 和 Enterprise 计划添加 1M 上下文窗口（之前需要额外使用）
- 为所有用户添加 `/color` 命令以设置会话的提示栏颜色
- 使用 `/rename` 时添加会话名称显示在提示栏上
- 为内存文件添加最后修改时间戳，帮助 Claude 推理哪些记忆是新的 vs. 陈旧的
- 在钩子需要确认时在权限提示中显示钩子源显示（设置/插件/技能）
- 修复了全新安装上未正确激活语音模式的问题，无需两次切换 `/voice`
- 修复了 Claude Code 标题在切换模型后未更新显示的模型名称的问题（使用 `/model` 或 Option+P）
- 修复了附件消息计算返回 undefined 值时会话崩溃的问题
- 修复了 Bash 工具在管道命令中搞乱 `!` 的问题（如 `jq 'select(.x != .y)'` 现在正确工作）
- 修复了托管禁用的插件在 `/plugin` 已安装选项卡中显示的问题——被组织强制禁用的插件现在隐藏
- 修复了思考和 `tool_use` 块的 token 估计过度计数问题，防止过早上下文紧致
- 修复了损坏的市场配置路径处理问题
- 修复了 `/resume` 在恢复分叉或继续的会话后丢失会话名称的问题
- 修复了访问配置选项卡后 Esc 无法关闭 `/status` 对话框的问题
- 修复了接受或拒绝计划时的输入处理问题
- 修复了代理团队中页脚提示显示"↓ 展开"而非正确的"shift + ↓ 展开"的问题
- 改进了非 MDM macOS 机器上的启动性能，跳过不必要的子进程生成
- 默认抑制异步钩子完成消息（用 `--verbose` 或记录模式可见）
- 破坏性更改：移除了已弃用的 Windows 托管设置回退 `C:\ProgramData\ClaudeCode\managed-settings.json`——使用 `C:\Program Files\ClaudeCode\managed-settings.json`

## 2.1.74

- 为 `/context` 命令添加可操作的建议——识别上下文重的工具、内存膨胀和容量警告，并提供具体优化提示
- 新增 `autoMemoryDirectory` 设置以配置自动内存存储的自定义目录
- 修复了流式 API 响应缓冲区在生成器提前终止时未释放的内存泄漏问题，导致 Node.js/npm 代码路径上的 RSS 无限增长
- 修复了托管策略 `ask` 规则被用户 `allow` 规则或技能 `allowed-tools` 绕过的问题
- 修复了代理前置参数 `model:` 字段和 `--agents` JSON 配置中的全模型 ID（如 `claude-opus-4-5`）被静默忽略的问题——代理现在接受与 `--model` 相同的模型值
- 修复了回调端口已被使用时 MCP OAuth 认证挂起的问题
- 修复了刷新 token 过期后 MCP OAuth 刷新从未提示重新授权的问题，对于返回 HTTP 200 错误的 OAuth 服务器（如 Slack）
- 修复了终端从未授予麦克风权限的用户的 macOS 原生二进制文件上语音模式静默失败的问题——二进制文件现在包含 `audio-input` entitlement 以便 macOS 正确提示
- 修复了 `SessionEnd` 钩子在退出后 1.5 秒被终止而不管 `hook.timeout` 的问题——现在可通过 `CLAUDE_CODE_SESSIONEND_HOOKS_TIMEOUT_MS` 配置
- 修复了市场插件的 `/plugin install` 在 REPL 内失败的问题
- 修复了市场更新未同步 git 子模块的问题——子模块中的插件源更新后不再破坏
- 修复了带参数的未知斜杠命令静默丢弃输入的问题——现在将你的输入显示为警告
- 修复了希伯来语、阿拉伯语和其他 RTL 文本在 Windows Terminal、conhost 和 VS Code 集成终端中不正确渲染的问题
- 修复了由于格式错误的文件 URI 导致 LSP 服务器在 Windows 上不工作的问题
- 更改了 `--plugin-dir` 使得本地开发副本现在覆盖具有相同名称的已安装市场插件（除非该插件被托管设置强制启用）
- [VSCode] 修复了未命名会话的删除按钮不工作的问题
- [VSCode] 改进了集成终端中滚动轮响应能力，支持终端感知加速

## 2.1.73

- 新增 `modelOverrides` 设置以将模型选择器条目映射到自定义提供商模型 ID（如 Bedrock 推理配置文件 ARN）
- 新增可操作指导，当 OAuth 登录或连接检查因 SSL 证书错误（企业代理、`NODE_EXTRA_CA_CERTS`）失败时显示
- 修复了复杂 bash 命令的权限提示导致的冻结和 100% CPU 循环问题
- 修复了可能导致 Claude Code 在许多技能文件同时更改时冻结的死锁问题（如在大型 `.claude/skills/` 目录中 `git pull`）
- 修复了在同一项目目录中运行多个 Claude Code 会话时 Bash 工具输出丢失的问题
- 修复了 Bedrock、Vertex 和 Microsoft Foundry 上具有 `model: opus`/`sonnet`/`haiku` 的子代理被静默降级到旧模型版本的问题
- 修复了代理退出时子代理生成的后台 bash 进程未清理的问题
- 修复了 `/resume` 在选择器中显示当前会话的问题
- 修复了自动安装扩展时 `/ide` 因 `onInstall is not defined` 崩溃的问题
- 修复了 Bedrock/Vertex/Foundry 上以及禁用遥测时 `/loop` 不可用的问题
- 修复了通过 `--resume` 或 `--continue` 恢复会话时 SessionStart 钩子触发两次的问题
- 修复了 JSON 输出钩子在每轮向模型上下文注入无操作 system-reminder 消息的问题
- 修复了慢速连接与新录制重叠时语音模式会话损坏的问题
- 修复了 Linux 沙箱在原生构建上因"ripgrep (rg) not found"启动失败的问题
- 修复了 Amazon Linux 2 和其他 glibc 2.26 系统上原生模块未加载的问题
- 修复了通过 Remote Control 接收图像时出现"media_type: Field required" API 错误的问题
- 修复了 `/heapdump` 在桌面文件夹已存在时在 Windows 上因 `EEXIST` 错误失败的问题
- 改进了中断 Claude 后的上箭头——现在一步恢复中断的提示并倒带对话
- 改进了启动时的 IDE 检测速度
- 改进了 macOS 上的剪贴板图像粘贴性能
- 改进了 `/effort` 在 Claude 响应时工作，匹配 `/model` 行为
- 改进了语音模式以在快速按住说话重新按下期间自动重试瞬时连接失败
- 改进了 Remote Control 生成模式选择提示，提供更好的上下文
- 将 Bedrock、Vertex 和 Microsoft Foundry 上的默认 Opus 模型更改为 Opus 4.6（之前是 Opus 4.1）
- 弃用了 `/output-style` 命令——改用 `/config`。输出样式现在在会话开始时固定，以更好地缓存提示
- VSCode: 修复了代理背后或使用 Claude 4.5 型号在 Bedrock/Vertex 上用户的 HTTP 400 错误

## 2.1.72

- 修复了只要设置了 `ENABLE_TOOL_SEARCH`，即使有 `ANTHROPIC_BASE_URL` 也会激活工具搜索的问题
- 在 `/copy` 中添加 `w` 键以将焦点选择直接写入文件，绕过剪贴板（通过 SSH 有用）
- 为 `/plan` 添加可选描述参数（如 `/plan fix the auth bug`），进入计划模式并立即开始
- 新增 `ExitWorktree` 工具以离开 `EnterWorktree` 会话
- 新增 `CLAUDE_CODE_DISABLE_CRON` 环境变量以立即停止会话中的计划 cron 作业
- 新增 `lsof`、`pgrep`、`tput`、`ss`、`fd` 和 `fdfind` 到 bash 自动批准白名单，减少常见只读操作的权限提示
- 恢复了 Agent 工具上用于每个调用模型覆盖的 `model` 参数
- 简化了努力级别为低/中/高（移除了最大），使用新符号（○ ◐ ●）和简短通知而非持久图标。使用 `/effort auto` 重置为默认
- 改进了 `/config`——Escape 现在取消更改，Enter 保存并关闭，空格切换设置
- 改进了上箭头历史记录，在运行多个并发会话时首先显示当前会话的消息
- 改进了 repo 名称和常见开发术语（regex、OAuth、JSON）的语音输入转录准确性
- 改进了 bash 命令解析，切换到原生模块——更快的初始化和无内存泄漏
- 减少了约 510 KB 的包大小
- 更改了 CLAUDE.md HTML 注释（`<!-- ... -->`）以便在自动注入时对 Claude 隐藏。使用 Read 工具读取时注释仍然可见
- 修复了后台任务或钩子响应慢时退出缓慢的问题
- 修复了代理任务进度卡在"初始化中…"的问题
- 修复了启用了钩子的技能被模型调用时技能钩子每事件触发两次的问题
- 修复了几个语音模式问题：偶尔输入延迟、释放按住说话后误报"No speech detected"、以及提交后在提示中重新填充的陈旧记录
- 修复了 `--continue` 在 `--compact` 后未从最新点恢复的问题
- 修复了 bash 安全解析边缘情况
- 新增了对没有 `.git` 后缀的市场 git URL 的支持（Azure DevOps、AWS CodeCommit）
- 改进了市场克隆失败消息，即使 git 没有产生 stderr 也显示诊断信息
- 修复了几个插件问题：在 OneDrive 文件夹中 Windows 上安装失败、`project-scope` 安装存在时阻止用户范围安装、`CLAUDE_CODE_PLUGIN_CACHE_DIR` 创建字面 `~` 目录、以及带市场唯一字段的 `plugin.json` 加载失败
- 修复了长会话中反馈调查出现过于频繁的问题
- 修复了 `--effort` CLI 标志在启动时被不相关的设置写入重置的问题
- 修复了后台 Ctrl+B 查询在 `/clear` 后丢失记录或破坏新对话的问题
- 修复了 `/clear` 终止后台代理/bash 任务的问题——现在只清除前台任务
- 修复了工作树隔离问题：Task 工具恢复未还原 cwd，以及后台任务通知缺少 `worktreePath` 和 `worktreeBranch`
- 修复了 `/model` 在 Claude 工作时未显示结果的问题
- 修复了在计划模式权限提示文本输入中数字键选择菜单选项而非键入的问题
- 修复了沙箱权限问题：某些文件写操作错误地允许而不提示，以及到白名单目录（如 `/tmp/claude/`）的输出重定向不必要地提示
- 改进了长会话中的 CPU 利用率
- 修复了 SDK `query()` 调用中的提示缓存失效，减少了高达 12 倍的输入 token 成本
- 修复了取消查询后 Escape 键无响应的问题
- 修复了后台代理或任务运行时双 Ctrl+C 未退出的问题
- 修复了团队代理继承领导模型的问题
- 修复了"始终允许"保存的权限规则永远无法再次匹配的问题
- 修复了几个钩子问题：`transcript_path` 指向恢复/分叉会话的错误目录、代理 `prompt` 在每次设置写入时从 settings.json 中静默删除、PostToolUse 阻止原因显示两次、异步钩子在使用 bash `read -r` 时未收到 stdin、以及验证错误消息显示验证失败的示例
- 修复了 Read 返回包含 U+2028/U+2029 字符的文件时 Desktop/SDK 会话崩溃的问题
- 修复了退出时即使设置了 `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` 也清除终端标题的问题
- 修复了几个权限规则匹配问题：通配符规则不匹配带 here-doc、嵌入式换行符或无参数的命令；`sandbox.excludedCommands` 使用环境变量前缀失败；"始终允许"为嵌套 CLI 工具建议过于宽泛的前缀；以及拒绝规则未应用于所有命令形式
- 修复了 Bash 数据 URL 输出中过大和截断的图像问题
- 修复了恢复包含 Bedrock API 错误的会话时崩溃的问题
- 修复了 Edit、Bash 和 Grep 工具输入上间歇性"expected boolean, received string"验证错误
- 修复了当第一条消息包含换行符时从对话分叉的多行会话标题问题
- 修复了排队消息未显示附加图像，以及按 ↑ 编辑排队消息时图像丢失的问题
- 修复了失败的 Read/WebFetch/Glob 取消其兄弟项的并行工具调用——现在只有 Bash 错误级联
- VSCode: 修复了集成终端中滚动速度与本机终端不匹配的问题
- VSCode: 修复了旧版键绑定的用户在 Shift+Enter 提交输入而非插入换行符的问题
- VSCode: 在输入边框上添加了努力级别指示器
- VSCode: 新增了 `vscode://anthropic.claude-code/open` URI 处理器以编程方式打开新的 Claude Code 标签，可选 `prompt` 和 `session` 查询参数

## 2.1.71

- 新增 `/loop` 命令以按重复间隔运行提示或斜杠命令（如 `/loop 5m check the deploy`）
- 新增 cron 调度工具用于会话中的重复提示
- 新增 `voice:pushToTalk` 键绑定以在 `keybindings.json` 中重新绑定语音激活键（默认：空格）——修饰符+字母组合如 `meta+k` 零打字干扰
- 新增 `fmt`、`comm`、`cmp`、`numfmt`、`expr`、`test`、`printf`、`getconf`、`seq`、`tsort` 和 `pr` 到 bash 自动批准白名单
- 修复了长时间会话中 stdin 冻结的问题，击键停止处理但进程保持存活
- 修复了语音模式启用用户系统唤醒后 CoreAudio 初始化阻塞主线程导致 5-8 秒启动冻结的问题
- 修复了许多 claude.ai 代理连接器同时刷新过期 OAuth token 时的启动 UI 冻结问题
- 修复了分叉对话（`/fork`）共享相同计划文件的问题，这导致一个分叉中的计划编辑覆盖另一个
- 修复了 Read 工具在图像处理失败时将过大图像放入上下文的问题，破坏了长图像密集会话中的后续回合
- 修复了包含 here-doc 提交消息的复合 bash 命令出现误报权限提示的问题
- 修复了运行多个 Claude Code 实例时插件安装丢失的问题
- 修复了 OAuth token 刷新后 claude.ai 连接器未能重新连接的问题
- 修复了每次启动而非仅针对先前连接的通知显示 claude.ai MCP 连接器启动通知的问题
- 修复了后台代理完成通知缺少输出文件路径的问题，这使得父代理难以在上下文紧致后恢复代理结果
- 修复了命令以非零状态退出时 Bash 工具错误消息中的重复输出问题
- 修复了 Chrome 扩展自动检测在没有本地 Chrome 的机器上运行后永久卡在"未安装"上的问题
- 修复了 `/plugin marketplace update` 在市场固定到分支/标签 ref 时因合并冲突失败的问题
- 修复了 `/plugin marketplace add owner/repo@ref` 错误解析 `@` 的问题——之前只有 `#` 作为 ref 分隔符工作，导致 `strictKnownMarketplaces` 下出现无法诊断的错误
- 修复了同一目录带和不带尾随斜杠添加时 `/permissions` 工作区选项卡中出现重复条目的问题
- 修复了配置了团队代理时 `--print` 永久挂起的问题——退出循环不再等待长寿命 `in_process_teammate` 任务
- 修复了每次 `ToolSearch` 调用后 REPL 中出现"❯ Tool loaded."的问题
- 修复了 Windows 上模型使用 mingw 风格路径时提示 `cd <cwd> && git ...` 的问题
- 改进了启动时间，将原生图像处理器加载延迟到首次使用
- 改进了桥接会话重新连接在笔记本从睡眠唤醒后数秒内完成，而非等待最多 10 分钟
- 改进了 `/plugin uninstall` 以在 `.claude/settings.local.json` 中禁用项目范围的插件，而非修改 `.claude/settings.json`，因此更改不影响队友
- 改进了插件提供的 MCP 服务器去重——复制手动配置的服务器（相同命令/URL）的服务器现在被跳过，防止重复连接和工具集。在 `/plugin` 菜单中显示抑制
- 更新了 `/debug` 以在会话中期切换调试日志记录，因为调试日志不再默认写入
- 移除了未经身份验证的组织注册 claude.ai 连接器的启动通知噪音

## 2.1.70

- 修复了将 `ANTHROPIC_BASE_URL` 与第三方网关使用时的 API 400 错误——工具搜索现在正确检测代理端点并禁用 `tool_reference` 块
- 修复了使用自定义 Bedrock 推理配置文件或其他不匹配标准 Claude 命名模式的模型标识符时出现"此模型不支持 effort 参数"API 错误的问题
- 修复了 `ToolSearch` 后立即出现空模型响应的问题——服务器使用系统提示样式标签在提示尾渲染工具模式，这可能使模型混淆而提前停止
- 修复了具有 `instructions` 的 MCP 服务器在第一轮后连接时的提示缓存失效问题
- 修复了在慢速 SSH 连接上 Enter 插入换行符而非提交的问题
- 修复了 Windows/WSL 上剪贴板损坏非 ASCII 文本（CJK、emoji）的问题，使用 PowerShell `Set-Clipboard`
- 修复了 VS Code 集成终端运行时在 Windows 上启动时打开额外 VS Code 窗口的问题
- 修复了语音模式在 Windows 原生二进制文件上失败并显示"无法加载原生音频模块"的问题
- 修复了 `voiceEnabled: true` 在设置中时按住说话在会话开始时未激活的问题
- 修复了包含 `#NNN` 引用的 markdown 链接错误指向当前仓库而非链接 URL 的问题
- 修复了项目 `.claude/settings.json` 固定了旧版 Opus 模型字符串时重复显示"模型已更新为 Opus 4.6"通知的问题
- 修复了插件在 `/plugin` 中显示为不准确安装的问题
- 修复了全新启动后市场插件显示"在市场中未找到"错误的问题，通过自动刷新市场安装
- 修复了 `/security-review` 命令在旧版 git 版本上因 `unknown option merge-base` 失败的问题
- 修复了 `/color` 命令无法重置回默认颜色的问题——`/color default`、`/color gray`、`/color reset` 和 `/color none` 现在恢复默认值
- 修复了 `AskUserQuestion` 预览对话框中性能回归问题，该问题在笔记输入中每个按键重新运行 markdown 渲染
- 修复了早期启动期间读取的功能标志从未刷新其磁盘缓存的问题，导致陈旧值跨会话持久化
- 修复了 `permissions.defaultMode` 设置值除了 `acceptEdits` 或 `plan` 之外在 Claude Code Remote 环境中被应用的问题——现在被忽略
- 修复了每次 `--resume` 时重新注入技能列表的问题（每次恢复节省约 600 token）
- 修复了 VS Code 远程传输会话中 teleport 标记不渲染的问题
- 改进了麦克风捕获沉默时的错误消息，以区别于"未检测到语音"
- 改进了紧致以在摘要请求中保留图像，允许提示缓存重用以实现更快更便宜的紧致
- 改进了 `/rename` 在 Claude 处理时工作，而非静默排队
- 减少了回合期间提示输入重新渲染约 74%
- 减少了没有自定义 CA 证书的用户启动内存约 426KB
- 减少了 Remote Control `/poll` 速率在连接时每 10 分钟一次（之前是 1-2 秒），将服务器负载减少约 300 倍。重新连接不受影响——传输丢失立即唤醒快速轮询。
- [VSCode] 在 VS Code activity bar 中添加了列出所有 Claude Code 会话的 spark 图标，会话作为完整编辑器打开
- [VSCode] 为 VS Code 中的计划添加了完整 markdown 文档视图，支持添加评论以提供反馈
- [VSCode] 新增了本机 MCP 服务器管理对话框——在聊天面板中使用 `/mcp` 来启用/禁用服务器、重新连接和管理 OAuth 身份验证，无需切换到终端

## 2.1.69

- 新增了用于使用 Claude API 和 Anthropic SDK 构建应用程序的 `/claude-api` 技能
- 新增了在空 bash 提示符上 `Ctrl+U`（`!`）退出 bash 模式，匹配 `escape` 和 `backspace`
- 新增了数字键盘支持，用于在 Claude 采访问题中选择选项（之前只有 QWERTY 上方的数字行有效）
- 为 `/remote-control` 和 `claude remote-control` 添加了可选名称参数（`/remote-control My Project` 或 `--name "My Project"`）以设置在 claude.ai/code 中可见的自定义会话标题
- 新增了 10 种新语言的语音 STT 支持（总共 20 种）——俄语、波兰语、土耳其语、荷兰语、乌克兰语、希腊语、捷克语、丹麦语、瑞典语、挪威语
- 新增了努力级别显示（如"低努力"）到徽标和旋转图标，使其更容易看出哪个努力设置处于活动状态
- 新增了在 `claude --agent` 时在终端标题中显示代理名称
- 新增了 `sandbox.enableWeakerNetworkIsolation` 设置（仅 macOS），允许 Go 程序如 `gh`、`gcloud` 和 `terraform` 在使用带有 `httpProxyPort` 的自定义 MITM 代理时验证 TLS 证书
- 新增了 `includeGitInstructions` 设置（和 `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` 环境变量）以从 Claude 的系统提示中移除内置提交和 PR 工作流说明
- 新增了 `/reload-plugins` 命令以在不重启的情况下激活待处理的插件更改
- 新增了一次性启动提示，建议 macOS 和 Windows 用户使用 Claude Code Desktop（最多显示 3 次，可关闭）
- 新增了 `${CLAUDE_SKILL_DIR}` 变量供技能在 SKILL.md 内容中引用自己的目录
- 新增了 `InstructionsLoaded` 钩子事件，在 CLAUDE.md 或 `.claude/rules/*.md` 文件加载到上下文时触发
- 新增了 `agent_id`（用于子代理）和 `agent_type`（用于子代理和 `--agent`）到钩子事件
- 新增了 `worktree` 字段到状态行钩子命令，包含在 `--worktree` 会话中运行时的名称、路径、分支和原始仓库目录
- 新增了 `pluginTrustMessage` 在托管设置中以在安装前显示的插件信任警告中附加组织特定上下文
- 为团队计划 OAuth 用户新增了策略限制获取（如远程控制限制），不仅仅是企业
- 新增了 `pathPattern` 到 `strictKnownMarketplaces` 用于与 `hostPattern` 限制一起使用正则表达式匹配文件/目录市场源
- 新增了 `git-subdir` 插件源类型，指向 git 仓库内的子目录
- 新增了 `oauth.authServerMetadataUrl` 配置选项，用于标准发现失败时为 MCP 服务器指定自定义 OAuth 元数据发现 URL
- 修复了嵌套技能发现可能从 gitignored 目录（如 `node_modules`）加载技能的安全问题
- 修复了信任对话框在首次运行时静默启用所有 `.mcp.json` 服务器的问题。你现在会看到预期的每服务器批准对话框
- 修复了 `claude remote-control` 在带有"bad option: --sdk-url"的 npm 安装上立即崩溃的问题
- 修复了 `--model claude-opus-4-0` 和 `--model claude-opus-4-1` 解析为已弃用的 Opus 版本而非当前版本的问题
- 修复了使用多个 OAuth MCP 服务器时 macOS 密钥链损坏的问题。大型 OAuth 元数据 blob 可能溢出 `security -i` stdin 缓冲区，静默地在后面留下陈旧凭据并导致重复 `/login` 提示
- 修复了 `.credentials.json` 在 token 刷新期间配置文件端点瞬时失败时丢失 `subscriptionType` 的问题（显示"Claude API"而非"Claude Pro"/"Claude Max"）
- 修复了在 Linux 沙箱 Bash 命令后幽灵 dotfiles（`.bashrc`、`HEAD` 等）显示为工作目录中未跟踪文件的问题
- 修复了 Ghostty over SSH 时 Shift+Enter 打印 `[27;2;13~` 而非插入换行符的问题
- 修复了在 Claude 工作时提交消息时 stash (Ctrl+S) 被清除的问题
- 修复了在具有大量文件编辑的长会话中 ctrl+o（记录切换）冻结数秒的问题
- 修复了计划模式反馈输入不支持多行文本输入的问题（反斜杠+Enter 和 Shift+Enter 现在插入换行符）
- 修复了光标未移动到输入框顶部空白行的问题
- 修复了记录文件包含缺失或格式错误时间戳的条目时 `/stats` 崩溃的问题
- 修复了流式传输错误后长会话中短暂挂起的问题（记录被完全重写以删除一行；现在就地截断）
- 修复了 `--setting-sources user` 未阻止动态发现的项目技能的问题
- 修复了在主仓库内的嵌套工作树（如 `claude -w`）中运行时重复的 CLAUDE.md、斜杠命令、代理和规则的问题
- 修复了任何 `/plugin` 操作后插件 Stop/SessionEnd/等 钩子未触发的问题
- 修复了当两个插件使用相同的 `${CLAUDE_PLUGIN_ROOT}/...` 命令模板时插件钩子被静默丢弃的问题
- 修复了长运行 SDK/CCR 会话中对话消息不必要保留的内存泄漏问题
- 修复了恢复在中断的 tool-batch 中间被中断的会话时叉代理（自动紧凑、摘要）中的 API 400 错误
- 修复了以孤立 tool result 开始对话时恢复时出现"在 tool_result 块中发现意外的 tool_use_id"错误的问题
- 修复了队友通过 Agent 工具的 `name` 参数意外生成嵌套队友的问题
- 修复了 `CLAUDE_CODE_MAX_OUTPUT_TOKENS` 在会话紧凑化期间被忽略的问题
- 修复了 `/compact` 摘要在 SDK 使用者（Claude Code Remote web UI、VSCode 扩展）中作为用户气泡渲染的问题
- 修复了失败语音激活后空格键卡住的问题（模块加载竞争、冷 GrowthBook）
- 修复了 Windows 上的工作树文件复制问题
- 修复了 Windows 上的全局 `.claude` 文件夹检测问题
- 修复了通过符号链接父目录写入新文件时符号链接绕过可能逃逸工作目录的问题（`acceptEdits` 模式下）
- 修复了在托管设置中启用 `allowManagedDomainsOnly` 时沙箱提示用户批准非允许域的问题——非允许域现在自动阻止，无绕过
- 修复了交互式工具（如 `AskUserQuestion`）在技能 `allowed-tools` 中列出时被静默自动允许的问题，绕过权限提示并使用空答案运行
- 修复了在工作树中有大型未跟踪二进制文件提交时出现多 GB 内存峰值的问题
- 修复了输入有草稿文本时 Escape 无法中断运行中回合的问题。使用上箭头拉回排队消息进行编辑，或 Ctrl+U 清除输入行。
- 修复了 Remote Control 会话中运行本地斜杠命令（`/voice`、`/cost`）时 Android 应用崩溃的问题
- 修复了 React Compiler `memoCache` 中旧消息数组版本在长会话中累积的内存泄漏问题
- 修复了长会话中 REPL 渲染作用域累积的内存泄漏问题（约 1000 回合 35MB）
- 修复了进程内队友中父级的完整对话历史记录被固定而无法 GC 的问题，导致 `/clear` 或自动紧凑化后无法垃圾回收
- 修复了交互模式中钩子事件可能无限累积的内存泄漏问题
- 修复了 `--mcp-config` 指向损坏文件时挂起的问题
- 修复了安装了许多技能/插件时启动缓慢的问题
- 修复了 `cd <outside-dir> && <cmd>` 权限提示以显示链式命令而非仅显示"是，允许从 <dir>/ 读取"的问题
- 修复了条件 `.claude/rules/*.md` 文件（带 `paths:` 前置参数）和嵌套 CLAUDE.md 文件在打印模式下（`claude -p`）未加载的问题
- 修复了 `/clear` 未完全清除所有会话缓存的问题，减少了长会话中的内存保留
- 修复了滚动累积边界处动画元素导致的终端闪烁问题
- 修复了在具有 OAuth 的 MCP 服务器上使用 macOS 时 UI 帧 drops 问题（v2.1.x 回归）
- 修复了键入期间偶尔出现的帧停顿问题，原因是同步调试日志刷新
- 修复了 `TeammateIdle` 和 `TaskCompleted` 钩子支持 `{"continue": false, "stopReason": "..."}` 以停止队友，匹配 `Stop` 钩子行为
- 修复了 `WorktreeCreate` 和 `WorktreeRemove` 插件钩子被静默忽略的问题
- 修复了带冒号的技能描述（如"Triggers include: X, Y, Z"）无法从 SKILL.md 前置参数加载的问题
- 修复了没有 `description:` 前置参数字段的项目技能未出现在 Claude 可用技能列表中的问题
- 修复了 `/context` 对所有 MCP 工具显示相同 token 计数的问题
- 修复了模型在 Git Bash 中使用 CMD 样式 `2>nul` 重定向时在 Windows 上创建字面 `nul` 文件的问题
- 修复了展开的子代理记录视图（Ctrl+O）中每个工具调用下方出现额外空行的问题
- 修复了 `/config` 搜索框获得焦点但为空时 Tab/箭头键未循环设置选项卡的问题
- 修复了服务密钥 OAuth 会话（CCR 容器）从配置文件范围的端点向 `profile-scoped` 端点发送 403 并伴随 `[ERROR]` 日志的问题
- 修复了"Remote Control 活动"状态指示器颜色不一致的问题
- 修复了语音波形光标在中间输入时覆盖第一个后缀字母的问题
- 修复了语音输入在预热期间显示所有 5 个空格而非限制为约 2 个的问题（与"保持按住…"提示对齐）
- 通过将 50ms 动画循环与周围 shell 隔离改进了旋转图标性能，减少了回合期间的渲染和 CPU 开销
- 改进了使用 React Compiler 的本机二进制文件的 UI 渲染性能
- 改进了通过消除启动路径上的 git 子进程来 `--worktree` 启动
- 改进了 macOS 启动，消除了托管设置解析时不必要的设置文件重载
- 改进了 macOS 上 claude.ai 企业/团队用户的启动，跳过不必要的密钥链查找
- 改进了 MCP `-p` 启动，将 claude.ai 配置获取与本地连接流水线化，并使用并发池而非顺序批处理
- 改进了语音启动，移除了难以察觉的预热脉冲动画，避免了回合期间的重新渲染卡顿
- 改进了 MCP 二进制内容处理：返回 PDF、Office 文档或音频的工具现在将解码字节保存到磁盘时使用正确的文件扩展名，而非将原始 base64 转储到对话上下文中。WebFetch 还保存了二进制响应及其摘要。
- 改进了长会话中的内存使用，通过跨消息更新稳定 `onSubmit`
- 改进了 LSP 工具渲染和内存上下文构建，不再读取整个文件
- 改进了会话上传和内存同步，避免在大小/二进制检查之前将大文件读入内存
- 改进了文件操作性能，避免读取文件内容进行存在性检查（6 个站点）
- 改进了文档，明确了 `--append-system-prompt-file` 和 `--system-prompt-file` 在交互模式下工作（文档之前说仅打印模式）
- 通过延迟 Yoga WASM 预加载减少了约 16MB 的基准内存
- 减少了使用 stream-json 输出的 SDK 和 CCR 会话的内存占用
- 减少了恢复大会话时的内存使用（包括紧凑化的历史）
- 减少了多代理任务中更简洁的子代理最终报告的 token 使用
- 更改 Sonnet 4.5 用户在 Pro/Max/Team Premium 上自动迁移到 Sonnet 4.6
- 更改 `/resume` 选择器显示你最近的提示而非第一个。这还解决了一些标题显示为`(会话）`的问题
- 更改 claude.ai MCP 连接器失败时显示通知而非从工具列表中静默消失
- 更改示例命令建议由确定性生成而非调用 Haiku
- 更改紧致后恢复不再在继续之前产生前amble 摘要
- [SDK] 更改任务创建不再需要 `activeForm` 字段——旋转图标回退到任务主题
- [VSCode] 新增紧致显示为可折叠的"已紧凑聊天"卡片，摘要在里面
- [VSCode] 权限模式选择器现在遵守你有效的 Claude Code 设置中的 `permissions.disableBypassPermissionsMode`（包括托管/策略设置）——当设置为 `disable` 时，绕过权限模式从选择器中隐藏
- [VSCode] 修复了聊天面板中 RTL 文本（阿拉伯语、希伯来语、波斯语）反向渲染的问题（v2.1.63 回归）

## 2.1.68

- Opus 4.6 现在默认为 Max 和 Team 订阅者使用中等努力。中等工作适合大多数任务——这是速度和彻底性之间的最佳平衡点。你可以随时通过 `/model` 更改此设置
- 重新引入了"ultrathink"关键词，为下一轮启用高努力
- 从第一方 API 上的 Claude Code 中移除了 Opus 4 和 4.1——固定了这些型号的用户自动移至 Opus 4.6

## 2.1.66

- 减少了虚假错误日志记录

## 2.1.63

- 新增了 `/simplify` 和 `/batch` 捆绑斜杠命令
- 修复了本地斜杠命令输出（如 /cost）在 UI 中显示为用户发送的消息而非系统消息的问题
- 项目配置和自动内存现在在同一仓库的 git 工作树之间共享
- 新增了 `ENABLE_CLAUDEAI_MCP_SERVERS=false` 环境变量以选择退出使 claude.ai MCP 服务器可用
- 改进了 `/model` 命令以在斜杠命令菜单中显示当前活动的模型
- 新增了 HTTP 钩子，可以向 URL POST JSON 并接收 JSON 而非运行 shell 命令
- 修复了桥接轮询循环中的监听器泄漏问题
- 修复了 MCP OAuth 流程清理中监听器泄漏问题
- 新增了 MCP OAuth 身份验证期间的手动 URL 粘贴回退。如果自动 localhost 重定向不起作用，你可以粘贴回调 URL 以完成身份验证
- 修复了导航钩子配置菜单时内存泄漏问题
- 修复了交互式权限处理程序中自动批准时监听器泄漏问题
- 修复了文件计数缓存忽略 glob 忽略模式的问题
- 修复了 bash 命令前缀缓存中内存泄漏问题
- 修复了服务器重连时 MCP 工具/资源缓存泄漏问题
- 修复了 IDE 主机 IP 检测缓存在端口之间错误共享结果的问题
- 修复了传输重连时 WebSocket 监听器泄漏问题
- 修复了 git 根检测缓存中可能导致长会话无限增长的内存泄漏问题
- 修复了 JSON 解析缓存中在长会话中无限增长的内存泄漏问题
- VSCode: 修复了远程会话未出现在对话历史记录中的问题
- 修复了 REPL 桥接中新的竞争条件问题，即新消息可能在初始连接刷新期间与历史消息交错到达服务器，导致消息排序问题
- 修复了长运行队友在会话紧致后保留 AppState 中所有消息的内存泄漏问题
- 修复了 MCP 服务器获取缓存在断开连接时未清除的内存泄漏问题，导致频繁重连的服务器内存使用增长
- 改进了使用子代理的长会话内存使用，通过在上下文紧致期间去除沉重的进度消息负载
- 新增了"始终复制完整响应"选项到 `/copy` 选择器。选中后，未来的 `/copy` 命令将跳过代码块选择器直接复制完整响应
- VSCode: 新增了会话列表中的会话重命名和删除操作
- 修复了 `/clear` 未重置缓存技能的问题，这可能导致陈旧技能内容在新对话中持续存在

## 2.1.62

- 修复了降低缓存命中率的提示建议缓存回归问题

## 2.1.61

- 修复了 Windows 上并发写入损坏配置文件的问题

## 2.1.59

- Claude 自动将有用的上下文保存到自动内存中。通过 /memory 管理
- 新增了 `/copy` 命令，在存在代码块时显示交互式选择器，允许选择单个代码块或完整响应
- 改进了复合 bash 命令（如 `cd /tmp && git fetch && git push`）的"始终允许"前缀建议，计算更智能的每个子命令前缀，而非将整个命令视为一个
- 改进了短任务列表的排序
- 改进了通过释放已完成的子代理任务状态来多代理会话中的内存使用
- 修复了同时运行多个 Claude Code 实例时 MCP OAuth token 刷新竞争条件问题
- 修复了工作目录被删除时 shell 命令未显示明确错误消息的问题
- 修复了多个 Claude Code 实例同时运行时可能导致身份验证被擦除的配置文件损坏问题

## 2.1.58

- 将 Remote Control 扩展到更多用户

## 2.1.56

- VS Code: 修复了"command 'claude-vscode.editor.openLast' not found"崩溃的另一个原因

## 2.1.55

- 修复了 BashTool 在 Windows 上因 EINVAL 错误失败的问题

## 2.1.53

- 修复了用户输入在提交后消息渲染前短暂消失的 UI 闪烁问题
- 修复了大容量代理终止（ctrl+f）发送单个聚合通知而非每个代理一个，并正确清除命令队列的问题
- 修复了使用 Remote Control 时有时在优雅关闭后留下陈旧会话的问题，通过并行化拆除网络调用
- 修复了 `--worktree` 有时在首次启动时被忽略的问题
- 修复了 Windows 上的恐慌（"switch on corrupted value"）问题
- 修复了可能在 Windows 上生成许多进程时发生的崩溃问题
- 修复了 Linux x64 和 Windows x64 上 WebAssembly 解释器中的崩溃问题
- 修复了 Windows ARM64 上 2 分钟后有时发生的崩溃问题

## 2.1.52

- VS Code: 修复了 Windows 上的扩展崩溃（"command 'claude-vscode.editor.openLast' not found"）

## 2.1.51

- 新增了 `claude remote-control` 子命令用于外部构建，启用本地环境服务供所有用户使用
- 更新了插件市场默认 git 超时从 30 秒到 120 秒，并新增了 `CLAUDE_CODE_PLUGIN_GIT_TIMEOUT_MS` 用于配置
- 新增了从 npm 源安装插件时支持自定义 npm 注册表和特定版本固定
- BashTool 现在在 shell 快照可用时默认跳过登录 shell（`-l` 标志），改进命令执行性能。之前这需要设置 `CLAUDE_BASH_NO_LOGIN=true`。
- 修复了一个安全问题，即 `statusLine` 和 `fileSuggestion` 钩子命令在交互模式下可能在工作区信任接受前执行
- 大于 50K 字符的工具结果现在持久化到磁盘（之前是 100K）。这减少了上下文窗口使用并改进了对话寿命
- 修复了一个 bug，其中重复的 `control_response` 消息（如来自 WebSocket 重连）可能导致 API 400 错误，将重复的助手消息推入对话
- 新增了 `CLAUDE_CODE_ACCOUNT_UUID`、`CLAUDE_CODE_USER_EMAIL` 和 `CLAUDE_CODE_ORGANIZATION_UUID` 环境变量，供 SDK 调用者同步提供账户信息，消除了早期遥测事件缺少账户元数据的竞争条件
- 修复了插件的 SKILL.md 描述是 YAML 数组或其他非字符串类型时斜杠命令自动完成崩溃的问题
- `/model` 选择器现在显示人类可读的标签（如"Sonnet 4.5"）而非固定模型版本的原始模型 ID，并在有新版本可用时显示升级提示
- 托管设置现在可以通过 macOS plist 或 Windows Registry 设置
