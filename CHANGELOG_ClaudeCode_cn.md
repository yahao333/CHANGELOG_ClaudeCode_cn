# Claude Code 更新日志（中文版）

## 2.1.119

- `/config` 设置 (theme, editor mode, verbose, etc.) 现在 持久化 to `~/.Claude/设置.JSON` 和 participate in 项目/本地/policy 覆盖 precedence
- 新增 `prUrlTemplate` 设置 to point the footer PR badge at a 自定义 代码-review URL 而不是 GitHub.com
- 新增 `CLAUDE_CODE_HIDE_CWD` 环境 变量 to 隐藏 the working 目录 in the 启动 logo
- `--从-PR` 现在 accepts GitLab 合并-请求, Bitbucket 拉取-请求, 和 GitHub 企业 PR URLs
- `--print` mode 现在 honors the 代理's `工具:` 和 `disallowedTools:` frontmatter, matching interactive-mode behavior
- `--代理 <name>` 现在 honors the 代理 definition's `permissionMode` 用于 内置 代理
- PowerShell 工具 命令 can 现在 be auto-approved in 权限 mode, matching Bash behavior
- 钩子: `PostToolUse` 和 `PostToolUseFailure` 钩子 inputs 现在 include `duration_ms` (工具 执行 time, 排除 权限 prompts 和 PreToolUse 钩子)
- 子代理 和 SDK MCP 服务器 reconfiguration 现在 connects 服务器 in 并行 而不是 serially
- 插件 pinned by another 插件's 版本 约束 现在 auto-更新 to the highest satisfying git tag
- Vim mode: Esc in 插入 不再 pulls a queued 消息 back 进入 the 输入; press Esc again to 中断
- Slash 命令 建议 现在 highlight the characters that matched your 查询
- Slash 命令 picker 现在 wraps long descriptions onto a 秒 line 而不是 truncating
- `owner/仓库#N` shorthand links in 输出 现在 use your git 远程's 主机 而不是 always pointing at GitHub.com
- 安全: `blockedMarketplaces` 现在 correctly enforces `hostPattern` 和 `pathPattern` 条目
- OpenTelemetry: `tool_result` 和 `tool_decision` 事件 现在 include `tool_use_id`; `tool_result` also includes `tool_input_size_bytes`
- Status line: stdin JSON 现在 includes `effort.级别` 和 `thinking.已启用`
- 修复 pasting CRLF content (Windows clipboards, Xcode console) inserting an extra 空白 line between every line
- 修复 multi-line 粘贴 losing newlines in terminals 使用 kitty 键盘 协议 sequences inside bracketed 粘贴
- 修复 Glob 和 Grep 工具 disappearing on 原生 macOS/Linux builds 当 the Bash 工具 is 已拒绝 通过 权限
- 修复 滚动 up in 全屏 mode snapping back to the bottom every time a 工具 finishes
- 修复 MCP HTTP 连接 failing 与 "无效 OAuth 错误 响应" 当 服务器 returned non-JSON bodies 用于 OAuth discovery 请求
- 修复 Rewind overlay showing "(no 提示)" 用于 消息 与 image attachments
- 修复 自动模式 overriding 计划模式 与 conflicting "执行 immediately" instructions
- 修复 异步 `PostToolUse` 钩子 that emit no 响应 载荷 writing 空 条目 to the 会话 转录
- 修复 加载动画 staying on 当 a 子代理 任务 通知 is orphaned in the 队列
- 工具 搜索 is 现在 已禁用 by 默认 on Vertex AI to avoid an unsupported 测试版 头信息 错误 (opt in 与 `ENABLE_TOOL_SEARCH`)
- 修复 `@`-文件 标签页 completion replacing the entire 提示 当 used inside a slash 命令 与 an absolute 路径
- 修复 a stray `p` character appearing at the 提示 on 启动 in macOS 终端.应用 通过 Docker 或 SSH
- 修复 `${ENV_VAR}` placeholders in `头信息` 用于 HTTP/SSE/WebSocket MCP 服务器 not being substituted 之前 请求
- 修复 MCP OAuth 客户端 secret 已存储 通过 `--客户端-secret` not being sent 期间 令牌 exchange 用于 服务器 requiring `client_secret_post`
- 修复 `/skills` Enter 键 closing the 对话框 而不是 pre-filling `/<skill-name>` in the 提示
- 修复 `/代理` detail 视图 mislabeling 内置 工具 不可用 to 子代理 as "Unrecognized"
- 修复 MCP 服务器 从 插件 not spawning on Windows 当 the 插件 缓存 was incomplete
- 修复 `/export` showing the 当前 默认 模型 而不是 the 模型 the conversation actually used
- 修复 verbose 输出 设置 not persisting 之后 重启
- 修复 `/usage` progress bars overlapping 与 their "Resets …" labels
- 修复 插件 MCP 服务器 failing 当 `${user_config.*}` references an optional 字段 left 空白
- 修复 列表 项 containing a sentence-最终 数字 wrapping the 数字 onto its own line
- 修复 `/plan` 和 `/plan 打开` not acting on the existing plan 当 entering 计划模式
- 修复 skills invoked 之前 auto-compaction being re-executed against the 下一个 user 消息
- 修复 `/重新加载-插件` 和 `/doctor` reporting 加载 错误 用于 已禁用 插件
- 修复 代理 工具 与 `isolation: "工作树"` reusing stale 工作树 从 prior 会话
- 修复 已禁用 MCP 服务器 appearing as "失败" in `/status`
- 修复 `TaskList` returning 任务 in arbitrary filesystem order 而不是 sorted by ID
- 修复 spurious "GitHub API 速率限制 exceeded" 提示 当 `gh` 输出 contained PR titles mentioning "速率限制"
- 修复 SDK/bridge `read_file` not correctly enforcing size cap on growing 文件
- 修复 PR not linked to 会话 当 working in a git 工作树
- 修复 `/doctor` 警告 about MCP 服务器 条目 overridden by a higher-precedence 作用域
- Windows: 移除 false-positive "Windows requires 'cmd /c' wrapper" MCP config 警告
- [VSCode] 修复 语音 听写's 第一 recording producing nothing on macOS 当 the 麦克风 权限 提示 is showing

## 2.1.118

- 新增 vim visual mode (`v`) 和 visual-line mode (`V`) 与 selection, operators, 和 visual feedback
- Merged `/cost` 和 `/stats` 进入 `/usage` — both remain as typing shortcuts that 打开 the relevant 标签页
- 创建 和 switch between named 自定义 themes 从 `/theme`, 或 hand-编辑 JSON 文件 in `~/.Claude/themes/`; 插件 can also ship themes 通过 a `themes/` 目录
- 钩子 can 现在 invoke MCP 工具 directly 通过 `类型: "mcp_tool"`
- 新增 `DISABLE_UPDATES` 环境变量 var to completely 块 all 更新 路径 包括 manual `Claude 更新` — stricter 比 `DISABLE_AUTOUPDATER`
- WSL on Windows can 现在 inherit Windows-side managed 设置 通过 the `wslInheritsWindowsSettings` policy 键
- 自动模式: include `"$defaults"` in `autoMode.允许`, `autoMode.soft_deny`, 或 `autoMode.环境` to 添加 自定义 rules alongside the 内置 列表 而不是 replacing it
- 新增 a "Don't ask again" 选项 to the 自动模式 opt-in 提示
- 新增 `Claude 插件 tag` to 创建 发布 git tags 用于 插件 与 版本 validation
- `--继续`/`--恢复` 现在 查找 会话 that 新增 the 当前 目录 通过 `/添加-dir`
- `/color` 现在 syncs the 会话 accent color to Claude.ai/代码 当 远程 Control is connected
- The `/模型` picker 现在 honors `ANTHROPIC_DEFAULT_*_MODEL_NAME`/`_DESCRIPTION` overrides 当 使用 a 自定义 `ANTHROPIC_BASE_URL` gateway
- 当 auto-更新 skips a 插件 由于 another 插件's 版本 约束, the 跳过 现在 appears in `/doctor` 和 the `/插件` 错误 标签页
- 修复 `/MCP` 菜单 hiding OAuth 认证/Re-认证 actions 用于 服务器 configured 与 `headersHelper`, 和 HTTP/SSE MCP 服务器 与 自定义 头信息 being stuck in "needs 认证" 之后 a transient 401
- 修复 MCP 服务器 whose OAuth 令牌 响应 omits `expires_in` requiring re-认证 every 小时
- 修复 MCP 步骤-up 授权 silently refreshing 而不是 prompting 用于 re-consent 当 the 服务器's `insufficient_scope` 403 names a 作用域 the 当前 令牌 already has
- 修复 an unhandled promise rejection 当 an MCP 服务器's OAuth flow times out 或 is cancelled
- 修复 MCP OAuth 刷新 proceeding 无 its cross-流程 锁定 under contention
- 修复 macOS keychain race where a 并发 MCP 令牌 刷新 could overwrite a freshly-refreshed OAuth 令牌, causing unexpected "Please run /login" prompts
- 修复 OAuth 令牌 刷新 failing 当 the 服务器 revokes a 令牌 之前 its 本地 expiry time
- 修复 凭证 保存 崩溃 on Linux/Windows corrupting `~/.Claude/.credentials.JSON`
- 修复 `/login` having no effect in a 会话 launched 与 `CLAUDE_CODE_OAUTH_TOKEN` — the 环境变量 令牌 is 现在 cleared 所以 disk credentials take effect
- 修复 unreadable 文本 in the "新 消息" 滚动 pill 和 `/插件` badges
- 修复 plan acceptance 对话框 offering "自动模式" 而不是 "绕过 权限" 当 运行中 与 `--dangerously-跳过-权限`
- 修复 代理-类型 钩子 failing 与 "消息 are required 用于 代理 钩子" 当 configured 用于 事件 other 比 `停止` 或 `SubagentStop`
- 修复 `提示` 钩子 re-firing on 工具 calls made by an 代理-钩子 verifier 子代理
- 修复 `/分叉` writing the full parent conversation to disk per 分叉 — 现在 writes a 指针 和 hydrates on 读取
- 修复 Alt+K / Alt+X / Alt+^ / Alt+_ freezing 键盘 输入
- 修复 connecting to a 远程 会话 overwriting your 本地 `模型` 设置 in `~/.Claude/设置.JSON`
- 修复 typeahead showing "No 命令 匹配" 错误 当 pasting 文件 路径 that 启动 与 `/`
- 修复 `插件 安装` on an already-installed 插件 not re-resolving a dependency installed at the wrong 版本
- 修复 unhandled 错误 从 文件 watcher on 无效 路径 或 fd exhaustion
- 修复 远程 Control 会话 getting archived on transient CCR initialization blips 期间 JWT 刷新
- 修复 子代理 resumed 通过 `SendMessage` not restoring the explicit `cwd` they were spawned 与

## 2.1.117

- 已分叉 子代理 can 现在 be 已启用 on 外部 builds by 设置 `CLAUDE_CODE_FORK_SUBAGENT=1`
- 代理 frontmatter `mcpServers` are 现在 loaded 用于 main-线程 代理 会话 通过 `--代理`
- 改进 `/模型`: selections 现在 持久化 across restarts even 当 the 项目 pins a different 模型, 和 the 启动 头信息 shows 当 the 活动 模型 comes 从 a 项目 或 managed-设置 pin
- The `/恢复` 命令 现在 offers to summarize stale, large 会话 之前 re-reading them, matching the existing `--恢复` behavior
- 更快 启动 当 both 本地 和 Claude.ai MCP 服务器 are configured (并发 连接 现在 默认)
- `插件 安装` on an already-installed 插件 现在 installs any 缺失 dependencies 而不是 stopping at "already installed"
- 插件 dependency 错误 现在 say "not installed" 与 an 安装 提示, 和 `Claude 插件 marketplace 添加` 现在 auto-resolves 缺失 dependencies 从 configured marketplaces
- Managed-设置 `blockedMarketplaces` 和 `strictKnownMarketplaces` are 现在 enforced on 插件 安装, 更新, 刷新, 和 autoupdate
- Advisor 工具 (experimental): 对话框 现在 carries an "experimental" label, learn-more 链接, 和 启动 通知 当 已启用; 会话 不再 get stuck 与 "Advisor 工具 result content could not be processed" 错误 on every 提示 和 `/压缩`
- The `cleanupPeriodDays` retention sweep 现在 also covers `~/.Claude/任务/`, `~/.Claude/shell-snapshots/`, 和 `~/.Claude/备份/`
- OpenTelemetry: `user_prompt` 事件 现在 include `command_name` 和 `command_source` 用于 slash 命令; `cost.usage`, `令牌.usage`, `api_request`, 和 `api_error` 现在 include an `effort` 属性 当 the 模型 supports effort 级别. 自定义/MCP 命令 names are redacted 除非 `OTEL_LOG_TOOL_DETAILS=1` is 集合
- 原生 builds on macOS 和 Linux: the `Glob` 和 `Grep` 工具 are replaced by embedded `bfs` 和 `ugrep` 可用 through the Bash 工具 — 更快 searches 无 a separate 工具 round-trip (Windows 和 npm-installed builds unchanged)
- Windows: cached `where.exe` executable lookups per 流程 用于 更快 subprocess launches
- 默认 effort 用于 Pro/Max subscribers on Opus 4.6 和 Sonnet 4.6 is 现在 `high` (was `medium`)
- 修复 Plain-CLI OAuth 会话 dying 与 "Please run /login" 当 the 访问 令牌 expires mid-会话 — the 令牌 is 现在 refreshed reactively on 401
- 修复 `WebFetch` hanging on very large HTML pages by truncating 输入 之前 HTML-to-markdown conversion
- 修复 a 崩溃 当 a 代理 returns HTTP 204 No Content — 现在 surfaces a 清除 错误 而不是 a `TypeError`
- 修复 `/login` having no effect 当 launched 与 `CLAUDE_CODE_OAUTH_TOKEN` 环境变量 var 和 that 令牌 expires
- 修复 提示-输入 撤销 (`Ctrl+_`) doing nothing immediately 之后 typing, 和 skipping a state on each 撤销 步骤
- 修复 `NO_PROXY` not being respected 用于 远程 API 请求 当 运行中 under Bun
- 修复 rare spurious 转义/return triggers 当 键 names arrive as coalesced 文本 over 慢 连接
- 修复 SDK `reload_plugins` reconnecting all user MCP 服务器 serially
- 修复 Bedrock 应用程序-inference-分析 请求 failing 与 400 当 backed by Opus 4.7 与 thinking 已禁用
- 修复 MCP `elicitation/创建` 请求 auto-cancelling in print/SDK mode 当 the 服务器 finishes connecting mid-turn
- 修复 子代理 运行中 a different 模型 比 the main 代理 incorrectly flagging 文件 reads 与 a malware 警告
- 修复 idle re-渲染 loop 当 background 任务 are present, reducing 内存 growth on Linux
- [VSCode] 修复 "Manage 插件" 面板 breaking 当 multiple large marketplaces are configured
- 修复 Opus 4.7 会话 showing inflated `/上下文` percentages 和 autocompacting too 早期 — Claude 代码 was computing against a 200K 上下文窗口 而不是 Opus 4.7's 原生 1M

## 2.1.116

- `/恢复` on large 会话 is significantly 更快 (up to 67% on 40MB+ 会话) 和 handles 会话 与 many dead-分叉 条目 more efficiently
- 更快 MCP 启动 当 multiple stdio 服务器 are configured; `资源/templates/列表` is 现在 deferred to 第一 `@`-mention
- Smoother 全屏 滚动 in VS 代码, 光标, 和 Windsurf terminals — `/终端-设置` 现在 configures the editor's 滚动 sensitivity
- Thinking 加载动画 现在 shows progress 内联 ("still thinking", "thinking more", "almost done thinking"), replacing the separate 提示 行
- `/config` 搜索 现在 matches 选项 值 (e.g. searching "vim" finds the Editor mode 设置)
- `/doctor` can 现在 be opened 当 Claude is responding, 无 waiting 用于 the 当前 turn to finish
- `/重新加载-插件` 和 background 插件 auto-更新 现在 auto-安装 缺失 插件 dependencies 从 marketplaces you've already 新增
- Bash 工具 现在 surfaces a 提示 当 `gh` 命令 hit GitHub's API 速率限制, 所以 代理 can back off 而不是 retrying
- The Usage 标签页 in 设置 现在 shows your 5-小时 和 weekly usage immediately 和 不再 fails 当 the usage 端点 is rate-limited
- 代理 frontmatter `钩子:` 现在 fire 当 运行中 as a main-线程 代理 通过 `--代理`
- Slash 命令 菜单 现在 shows "No 命令 匹配" 当 your 过滤 has zero results, 而不是 disappearing
- 安全: 沙盒 auto-允许 不再 bypasses the dangerous-路径 safety check 用于 `rm`/`rmdir` targeting `/`, `$HOME`, 或 other critical 系统 directories
- Claude 代码 和 installer 现在 use `HTTPS://downloads.Claude.ai/Claude-代码-releases` 而不是 `HTTPS://storage.googleapis.com/Claude-代码-dist-86c565f3-f756-42ad-8dfa-d59b1c096819/Claude-代码-releases`
- 修复 Devanagari 和 other Indic 脚本 渲染 与 broken 列 alignment in the 终端 UI
- 修复 Ctrl+- not triggering 撤销 in terminals 使用 the Kitty 键盘 协议 (iTerm2, Ghostty, kitty, WezTerm, Windows 终端)
- 修复 Cmd+Left/Right not jumping to line 启动/end in terminals that use the Kitty 键盘 协议 (Warp 全屏, kitty, Ghostty, WezTerm)
- 修复 Ctrl+Z hanging the 终端 当 Claude 代码 is launched 通过 a wrapper 流程 (e.g. `npx`, `bun run`)
- 修复 scrollback duplication in 内联 mode where resizing the 终端 或 large 输出 bursts would repeat earlier conversation history
- 修复 modal 搜索 dialogs overflowing the 屏幕 at short 终端 heights, hiding the 搜索 box 和 键盘 提示
- 修复 scattered 空白 cells 和 disappearing composer Chrome in the VS 代码 integrated 终端 期间 滚动
- 修复 an intermittent API 400 错误 related to 缓存 control TTL ordering that could occur 当 a 并行 请求 完成 期间 请求 设置
- 修复 `/分支` rejecting conversations 与 transcripts larger 比 50MB
- 修复 `/恢复` silently showing an 空 conversation on large 会话 文件 而不是 reporting the 加载 错误
- 修复 `/插件` Installed 标签页 showing the same 项 twice 当 it appears under Needs attention 或 Favorites
- 修复 `/更新` 和 `/tui` not working 之后 entering a 工作树 mid-会话

## 2.1.114

- 修复 a 崩溃 in the 权限 对话框 当 an 代理 团队 teammate requested 工具 权限

## 2.1.113

- 更改 the CLI to 生成 a 原生 Claude 代码 二进制 (通过 a per-platform optional dependency) 而不是 bundled JavaScript
- 新增 `沙盒.网络.deniedDomains` 设置 to 块 specific domains even 当 a broader `allowedDomains` wildcard would otherwise permit them
- 全屏 mode: Shift+↑/↓ 现在 scrolls the viewport 当 extending a selection past the visible 边
- `Ctrl+A` 和 `Ctrl+E` 现在 移动 to the 启动/end of the 当前 logical line in multiline 输入, matching readline behavior
- Windows: `Ctrl+Backspace` 现在 deletes the 上一个 word
- Long URLs in 响应 和 bash 输出 stay clickable 当 they 包装 across lines (in terminals 与 OSC 8 hyperlinks)
- 改进 `/loop`: pressing Esc 现在 cancels 待处理 wakeups, 和 wakeups 显示 as "Claude resuming /loop wakeup" 用于 clarity
- `/extra-usage` 现在 works 从 远程 Control (mobile/web) clients
- 远程 Control clients can 现在 查询 `@`-文件 autocomplete 建议
- 改进 `/ultrareview`: 更快 启动 与 parallelized checks, diffstat in the 启动 对话框, 和 animated launching state
- 子代理 that stall mid-流 现在 失败 与 a 清除 错误 之后 10 分钟 而不是 hanging silently
- Bash 工具: multi-line 命令 whose 第一 line is a comment 现在 显示 the full 命令 in the 转录, closing a UI-spoofing vector
- 运行中 `cd <当前-目录> && git …` 不再 triggers a 权限 提示 当 the `cd` is a no-op
- 安全: on macOS, `/私有/{etc,var,tmp,home}` 路径 are 现在 treated as dangerous removal targets under `Bash(rm:*)` 允许 rules
- 安全: Bash 拒绝 rules 现在 匹配 命令 wrapped in `环境变量`/`sudo`/`watch`/`ionice`/`setsid` 和 similar exec wrappers
- 安全: `Bash(查找:*)` 允许 rules 不再 auto-approve `查找 -exec`/`-删除`
- 修复 MCP 并发-call 超时 handling where a 消息 用于 one 工具 call could silently disarm another call's watchdog
- 修复 Cmd-backspace / `Ctrl+U` to once again 删除 从 the 光标 to the 启动 of the line
- 修复 markdown tables breaking 当 a cell contains an 内联 代码 span 与 a pipe character
- 修复 会话 recap auto-firing 当 composing unsent 文本 in the 提示
- 修复 `/复制` "Full 响应" not aligning markdown table columns 用于 pasting 进入 GitHub, Notion, 或 Slack
- 修复 消息 typed 当 viewing a 运行中 子代理 being hidden 从 its 转录 和 misattributed to the parent AI
- 修复 Bash `dangerouslyDisableSandbox` 运行中 命令 outside the 沙盒 无 a 权限 提示
- 修复 `/effort auto` confirmation — 现在 says "Effort 级别 集合 to max" to 匹配 the status bar label
- 修复 the "copied N chars" toast overcounting emoji 和 other multi-代码-单元 characters
- 修复 `/insights` crashing 与 `EBUSY` on Windows
- 修复 退出 confirmation 对话框 mislabeling one-shot scheduled 任务 as recurring — 现在 shows a countdown
- 修复 slash/@ completion 菜单 not sitting flush against the 提示 border in 全屏 mode
- 修复 `CLAUDE_CODE_EXTRA_BODY` `output_config.effort` causing 400 错误 on 子代理 calls to 模型 that don't support effort 和 on Vertex AI
- 修复 提示 光标 disappearing 当 `NO_COLOR` is 集合
- 修复 `ToolSearch` ranking 所以 pasted MCP 工具 names surface the actual 工具 而不是 description-matching siblings
- 修复 compacting a resumed long-上下文 会话 failing 与 "Extra usage is required 用于 long 上下文 请求"
- 修复 `插件 安装` succeeding 当 a dependency 版本 conflicts 与 an already-installed 插件 — 现在 reports `范围-conflict`
- 修复 "Refine 与 Ultraplan" not showing the 远程 会话 URL in the 转录
- 修复 SDK image content 块 that 失败 to 流程 crashing the 会话 — 现在 degrade to a 文本 placeholder
- 修复 远程 Control 会话 not 流式 子代理 transcripts
- 修复 远程 Control 会话 not being archived 当 Claude 代码 exits
- 修复 `thinking.类型.已启用 is not 支持` 400 错误 当 使用 Opus 4.7 通过 a Bedrock 应用程序 Inference 分析 ARN

## 2.1.112

- 修复 "Claude-Opus-4-7 is temporarily 不可用" 用于 自动模式

## 2.1.111

- Claude Opus 4.7 xhigh is 现在 可用! Use /effort to tune speed vs. intelligence
- 自动模式 is 现在 可用 用于 Max subscribers 当 使用 Opus 4.7
- 新增 `xhigh` effort 级别 用于 Opus 4.7, sitting between `high` 和 `max`. 可用 通过 `/effort`, `--effort`, 和 the 模型 picker; other 模型 fall back to `high`
- `/effort` 现在 opens an interactive slider 当 called 无 arguments, 与 arrow-键 navigation between 级别 和 Enter to confirm
- 新增 "Auto (匹配 终端)" theme 选项 that matches your 终端's dark/light mode — select it 从 `/theme`
- 新增 `/less-权限-prompts` skill — scans transcripts 用于 common 读取-only Bash 和 MCP 工具 calls 和 proposes a prioritized allowlist 用于 `.Claude/设置.JSON`
- 新增 `/ultrareview` 用于 运行中 comprehensive 代码 review in the cloud 使用 并行 multi-代理 analysis 和 critique — invoke 与 no arguments to review your 当前 分支, 或 `/ultrareview <PR#>` to fetch 和 review a specific GitHub PR
- 自动模式 不再 requires `--启用-auto-mode`
- Windows: PowerShell 工具 is progressively rolling out. Opt in 或 out 与 `CLAUDE_CODE_USE_POWERSHELL_TOOL`. On Linux 和 macOS, 启用 与 `CLAUDE_CODE_USE_POWERSHELL_TOOL=1` (requires `pwsh` on 路径)
- 读取-only bash 命令 与 glob 模式 (e.g. `ls *.ts`) 和 命令 starting 与 `cd <项目-dir> &&` 不再 触发 a 权限 提示
- Suggest the closest matching subcommand 当 `Claude <word>` is invoked 与 a near-miss typo (e.g. `Claude udpate` → "Did you mean `Claude 更新`?")
- Plan 文件 are 现在 named 之后 your 提示 (e.g. `修复-认证-race-snug-otter.md`) 而不是 purely random words
- 改进 `/设置-Vertex` 和 `/设置-Bedrock` to 显示 the actual `设置.JSON` 路径 当 `CLAUDE_CONFIG_DIR` is 集合, seed 模型 candidates 从 existing pins on re-run, 和 offer a "与 1M 上下文" 选项 用于 支持 模型
- `/skills` 菜单 现在 supports sorting by estimated 令牌 count — press `t` to toggle
- `Ctrl+U` 现在 clears the entire 输入 缓冲区 (previously: 删除 to 启动 of line); press `Ctrl+Y` to 恢复
- `Ctrl+L` 现在 forces a full 屏幕 redraw 除了 clearing the 提示 输入
- 转录 视图 footer 现在 shows `[` (dump to scrollback) 和 `v` (打开 in editor) shortcuts
- The "+N lines" marker 用于 truncated long pastes is 现在 a full-width rule 用于 easier scanning
- Headless `--输出-格式 流-JSON` 现在 includes `plugin_errors` on the init 事件 当 插件 are demoted 用于 unsatisfied dependencies
- 新增 `OTEL_LOG_RAW_API_BODIES` 环境 变量 to emit full API 请求 和 响应 bodies as OpenTelemetry 日志 事件 用于 调试
- Suppressed spurious decompression, 网络, 和 transient 错误 消息 that could appear in the TUI 期间 normal operation
- 已回退 the v2.1.110 cap on non-流式 回退 retries — it traded long waits 用于 more outright 失败 期间 API overload
- 修复 终端 显示 tearing (random characters, drifting 输入) in iTerm2 + tmux setups 当 终端 通知 are sent
- 修复 `@` 文件 建议 re-scanning the entire 项目 on every turn in non-git working directories, 和 showing only config 文件 in freshly-initialized git repos 与 no tracked 文件
- 修复 LSP diagnostics 从 之前 an 编辑 appearing 之后 it, causing the 模型 to re-读取 文件 it just edited
- 修复 标签页-completing `/恢复` immediately resuming an arbitrary titled 会话 而不是 showing the 会话 picker
- 修复 `/上下文` grid 渲染 与 extra 空白 lines between rows
- 修复 `/清除` dropping the 会话 name 集合 by `/rename`, causing statusline 输出 to lose `session_name`
- 改进 插件 错误 handling: dependency 错误 现在 distinguish conflicting, 无效, 和 overly complex 版本 需求; 修复 stale resolved 版本 之后 `插件 更新`; `插件 安装` 现在 recovers 从 interrupted prior installs
- 修复 Claude calling a non-existent `提交` skill 和 showing "Unknown skill: 提交" 用于 用户 无 a 自定义 `/提交` 命令
- 修复 429 rate-限制 错误 on Bedrock/Vertex/Foundry referencing status.Claude.com (it only covers Anthropic-operated providers)
- 修复 feedback surveys appearing back-to-back 之后 dismissing one
- 修复 bare URLs in bash/PowerShell/MCP 工具 输出 being unclickable 当 the 终端 wraps them across lines
- Windows: `CLAUDE_ENV_FILE` 和 SessionStart 钩子 环境 文件 现在 apply (previously a no-op)
- Windows: 权限 rules 与 drive-letter 路径 are 现在 correctly 根-anchored, 和 路径 differing only by drive-letter case are recognized as the same 路径

## 2.1.110

- 新增 `/tui` 命令 和 `tui` 设置 — run `/tui 全屏` to switch to flicker-free 渲染 in the same conversation
- 新增 推送 通知 工具 — Claude can 发送 mobile 推送 通知 当 远程 Control 和 "推送 当 Claude decides" config are 已启用
- 更改 `Ctrl+O` to toggle between normal 和 verbose 转录 only; focus 视图 is 现在 toggled separately 与 the 新 `/focus` 命令
- 新增 `autoScrollEnabled` config to 禁用 conversation auto-滚动 in 全屏 mode
- 新增 选项 to 显示 Claude's 最后 响应 as commented 上下文 in the `Ctrl+G` 外部 editor (启用 通过 `/config`)
- 改进 `/插件` Installed 标签页 — 项 needing attention 和 favorites appear at the top, 已禁用 项 are hidden behind a fold, 和 `f` favorites the selected 项
- 改进 `/doctor` to warn 当 an MCP 服务器 is defined in multiple config scopes 与 different endpoints
- `--恢复`/`--继续` 现在 resurrects unexpired scheduled 任务
- `/上下文`, `/退出`, 和 `/重新加载-插件` 现在 work 从 远程 Control (mobile/web) clients
- 写入 工具 现在 informs the 模型 当 you 编辑 the proposed content in the IDE diff 之前 accepting
- Bash 工具 现在 enforces the documented maximum 超时 而不是 accepting arbitrarily large 值
- SDK/headless 会话 现在 读取 `TRACEPARENT`/`TRACESTATE` 从 the 环境 用于 distributed 追踪 linking
- 会话 recap is 现在 已启用 用于 用户 与 telemetry 已禁用 (Bedrock, Vertex, Foundry, `DISABLE_TELEMETRY`). Opt out 通过 `/config` 或 `CLAUDE_CODE_ENABLE_AWAY_SUMMARY=0`.
- 修复 MCP 工具 calls hanging indefinitely 当 the 服务器 连接 drops mid-响应 on SSE/HTTP transports
- 修复 non-流式 回退 retries causing multi-分钟 hangs 当 the API is unreachable
- 修复 会话 recap, 本地 slash-命令 输出, 和 other 系统 status lines not appearing in focus mode
- 修复 high CPU usage in 全屏 当 文本 is selected 当 a 工具 is 运行中
- 修复 插件 安装 not honoring dependencies declared in `插件.JSON` 当 the marketplace 条目 omits them; `/插件` 安装 现在 lists auto-installed dependencies
- 修复 skills 与 `禁用-模型-invocation: true` failing 当 invoked 通过 `/<skill>` mid-消息
- 修复 `--恢复` sometimes showing the 第一 提示 而不是 the `/rename` name 用于 会话 still 运行中 或 exited uncleanly
- 修复 queued 消息 briefly appearing twice 期间 multi-工具-call turns
- 修复 会话 清理 not removing the full 会话 目录 包括 子代理 transcripts
- 修复 dropped keystrokes 之后 the CLI relaunches (e.g. `/tui`, provider 设置 wizards)
- 修复 garbled 启动 渲染 in macOS 终端.应用 和 other terminals that don't support synchronized 输出
- Hardened "打开 in editor" actions against 命令 injection 从 untrusted filenames
- 修复 `PermissionRequest` 钩子 returning `updatedInput` not being re-checked against `权限.拒绝` rules; `setMode:'bypassPermissions'` updates 现在 respect `disableBypassPermissionsMode`
- 修复 `PreToolUse` 钩子 `additionalContext` being dropped 当 the 工具 call fails
- 修复 stdio MCP 服务器 that print stray non-JSON lines to stdout being disconnected on the 第一 stray line (回归 in 2.1.105)
- 修复 headless/SDK 会话 auto-title firing an extra Haiku 请求 当 `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` 或 `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` is 集合
- 修复 potential excessive 内存 allocation 当 piped (non-TTY) Ink 输出 contains a single very wide line
- 修复 `/skills` 菜单 not 滚动 当 the 列表 overflows the modal in 全屏 mode
- 修复 远程 Control 会话 showing a 泛型 错误 而不是 prompting 用于 re-login 当 the 会话 is too 旧
- 修复 远程 Control 会话 renames 从 Claude.ai not persisting the title to the 本地 CLI 会话

## 2.1.109

- 改进 the extended-thinking indicator 与 a rotating progress 提示

## 2.1.108

- 新增 `ENABLE_PROMPT_CACHING_1H` 环境变量 var to opt 进入 1-小时 提示 缓存 TTL on API 键, Bedrock, Vertex, 和 Foundry (`ENABLE_PROMPT_CACHING_1H_BEDROCK` is 弃用 but still honored), 和 `FORCE_PROMPT_CACHING_5M` to force 5-分钟 TTL
- 新增 recap 功能 to provide 上下文 当 returning to a 会话, configurable in `/config` 和 manually invocable 与 `/recap`; force 与 `CLAUDE_CODE_ENABLE_AWAY_SUMMARY` if telemetry 已禁用.
- The 模型 can 现在 discover 和 invoke 内置 slash 命令 like `/init`, `/review`, 和 `/安全-review` 通过 the Skill 工具
- `/撤销` is 现在 an alias 用于 `/rewind`
- 改进 `/模型` to warn 之前 switching 模型 mid-conversation, 自从 the 下一个 响应 re-reads the full history uncached
- 改进 `/恢复` picker to 默认 to 会话 从 the 当前 目录; press `Ctrl+A` to 显示 all projects
- 改进 错误 消息: 服务器 rate 限制 are 现在 distinguished 从 plan usage 限制; 5xx/529 错误 显示 a 链接 to status.Claude.com; unknown slash 命令 suggest the closest 匹配
- Reduced 内存 占用空间 用于 文件 reads, edits, 和 syntax highlighting by loading language grammars on demand
- 新增 "verbose" indicator 当 viewing the detailed 转录 (`Ctrl+O`)
- 新增 a 警告 at 启动 当 提示 缓存 is 已禁用 通过 `DISABLE_PROMPT_CACHING*` 环境 变量
- 修复 粘贴 not working in the `/login` 代码 提示 (回归 in 2.1.105)
- 修复 subscribers who 集合 `DISABLE_TELEMETRY` falling back to 5-分钟 提示 缓存 TTL 而不是 1 小时
- 修复 代理 工具 prompting 用于 权限 in 自动模式 当 the safety classifier's 转录 exceeded its 上下文窗口
- 修复 Bash 工具 producing no 输出 当 `CLAUDE_ENV_FILE` (e.g. `~/.zprofile`) ends 与 a `#` comment line
- 修复 `Claude --恢复 <会话-ID>` losing the 会话's 自定义 name 和 color 集合 通过 `/rename`
- 修复 会话 titles showing placeholder 示例 文本 当 the 第一 消息 is a short greeting
- 修复 终端 转义 codes appearing as garbage 文本 in the 提示 输入 之后 `--teleport`
- 修复 `/feedback` 重试: pressing Enter to resubmit 之后 a 失败 现在 works 无 第一 editing the description
- 修复 `--teleport` 和 `--恢复 <ID>` precondition 错误 (e.g. dirty git 树, 会话 not found) exiting silently 而不是 showing the 错误 消息
- 修复 远程 Control 会话 titles 集合 in the web UI being overwritten by auto-已生成 titles 之后 the third 消息
- 修复 `--恢复` truncating 会话 当 the 转录 contained a self-referencing 消息
- 修复 转录 写入 失败 (e.g., disk full) being silently dropped 而不是 being logged
- 修复 diacritical marks (accents, umlauts, cedillas) being dropped 从 响应 当 the `language` 设置 is configured
- 修复 policy-managed 插件 never auto-updating 当 运行中 从 a different 项目 比 where they were 第一 installed

## 2.1.107

- 显示 thinking 提示 sooner 期间 long operations

## 2.1.105

- 新增 `路径` 参数 to the `EnterWorktree` 工具 to switch 进入 an existing 工作树 of the 当前 仓库
- 新增 PreCompact 钩子 support: 钩子 can 现在 块 compaction by exiting 与 代码 2 或 returning `{"decision":"块"}`
- 新增 background 监控 support 用于 插件 通过 a top-级别 `monitors` manifest 键 that auto-arms at 会话 启动 或 on skill invoke
- `/proactive` is 现在 an alias 用于 `/loop`
- 改进 stalled API 流 handling: streams 现在 中止 之后 5 分钟 of no data 和 重试 non-流式 而不是 hanging indefinitely
- 改进 网络 错误 消息: 连接 错误 现在 显示 a 重试 消息 immediately 而不是 a silent 加载动画
- 改进 文件 写入 显示: long single-line writes (e.g. minified JSON) are 现在 truncated in the UI 而不是 paginating across many screens
- 改进 `/doctor` 布局 与 status icons; press `f` to have Claude 修复 reported 问题
- 改进 `/config` labels 和 descriptions 用于 clarity
- 改进 skill description handling: raised the listing cap 从 250 to 1,536 characters 和 新增 a 启动 警告 当 descriptions are truncated
- 改进 `WebFetch` to 去除 `<style>` 和 `<脚本>` contents 从 fetched pages 所以 CSS-heavy pages 不再 exhaust the content budget 之前 reaching actual 文本
- 改进 stale 代理 工作树 清理 to 移除 工作树 whose PR was squash-merged 而不是 keeping them indefinitely
- 改进 MCP large-输出 truncation 提示 to give 格式-specific recipes (e.g. `jq` 用于 JSON, computed 读取 块 sizes 用于 文本)
- 修复 images attached to queued 消息 (sent 当 Claude is working) being dropped
- 修复 屏幕 going 空白 当 the 提示 输入 wraps to a 秒 line in long conversations
- 修复 leading whitespace getting copied 当 selecting multi-line assistant 响应 in 全屏 mode
- 修复 leading whitespace being trimmed 从 assistant 消息, breaking ASCII art 和 indented diagrams
- 修复 garbled bash 输出 当 命令 print clickable 文件 links (e.g. Python `rich`/`loguru` 日志)
- 修复 alt+enter not inserting a newline in terminals 使用 ESC-前缀 alt 编码, 和 Ctrl+J not inserting a newline (回归 in 2.1.100)
- 修复 复制 "Creating 工作树" 文本 in EnterWorktree/ExitWorktree 工具 显示
- 修复 queued user prompts disappearing 从 focus mode
- 修复 one-shot scheduled 任务 re-firing repeatedly 当 the 文件 watcher missed the post-fire 清理
- 修复 inbound channel 通知 being silently dropped 之后 the 第一 消息 用于 团队/企业 用户
- 修复 marketplace 插件 与 `包.JSON` 和 lockfile not having dependencies installed automatically 之后 安装/更新
- 修复 marketplace auto-更新 leaving the official marketplace in a broken state 当 a 插件 流程 holds 文件 打开 期间 the 更新
- 修复 "恢复 this 会话 与..." 提示 not printing on 退出 之后 `/恢复`, `--工作树`, 或 `/分支`
- 修复 feedback survey shortcut 键 firing 当 typed at the end of a longer 提示
- 修复 stdio MCP 服务器 emitting malformed (non-JSON) 输出 hanging the 会话 而不是 failing 快速 与 "连接 closed"
- 修复 MCP 工具 缺失 on the 第一 turn of headless/远程-触发 会话 当 MCP 服务器 连接 asynchronously
- 修复 `/模型` picker on AWS Bedrock in non-US regions persisting 无效 `us.*` 模型 IDs to `设置.JSON` 当 inference 分析 discovery is still in-flight
- 修复 429 rate-限制 错误 showing a 原始 JSON dump 而不是 a clean 消息 用于 API-键, Bedrock, 和 Vertex 用户
- 修复 崩溃 on 恢复 当 会话 contains malformed 文本 块
- 修复 `/help` dropping the 标签页 bar, Shortcuts heading, 和 footer at short 终端 heights
- 修复 malformed keybinding 条目 值 in `keybindings.JSON` being silently loaded 而不是 rejected 与 a 清除 错误
- 修复 `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` in one 项目's 设置 permanently disabling usage metrics 用于 all projects on the machine
- 修复 washed-out 16-color palette 当 使用 Ghostty, Kitty, Alacritty, WezTerm, foot, rio, 或 Contour over SSH/mosh
- 修复 Bash 工具 suggesting `acceptEdits` 权限 mode 当 exiting 计划模式 would 降级 从 a higher 权限 级别

## 2.1.101

- 新增 `/团队-onboarding` 命令 to generate a teammate ramp-up 指南 从 your 本地 Claude 代码 usage
- 新增 OS CA 证书 存储 trust by 默认, 所以 企业 TLS proxies work 无 extra 设置 (集合 `CLAUDE_CODE_CERT_STORE=bundled` to use only bundled CAs)
- `/ultraplan` 和 other 远程-会话 功能 现在 auto-创建 a 默认 cloud 环境 而不是 requiring web 设置 第一
- 改进 brief mode to 重试 once 当 Claude responds 与 plain 文本 而不是 a structured 消息
- 改进 focus mode: Claude 现在 writes more self-contained summaries 自从 it knows you only see its 最终 消息
- 改进 工具-not-可用 错误 to explain why 和 how to proceed 当 the 模型 calls a 工具 that 存在 but isn't 可用 in the 当前 上下文
- 改进 rate-限制 重试 消息 to 显示 which 限制 was hit 和 当 it resets 而不是 an opaque 秒 countdown
- 改进 refusal 错误 消息 to include the API-provided explanation 当 可用
- 改进 `Claude -p --恢复 <name>` to accept 会话 titles 集合 通过 `/rename` 或 `--name`
- 改进 设置 resilience: an unrecognized 钩子 事件 name in `设置.JSON` 不再 causes the entire 文件 to be ignored
- 改进 插件 钩子 从 插件 force-已启用 by managed 设置 to run 当 `allowManagedHooksOnly` is 集合
- 改进 `/插件` 和 `Claude 插件 更新` to 显示 a 警告 当 the marketplace could not be refreshed, 而不是 silently reporting a stale 版本
- 改进 计划模式 to 隐藏 the "Refine 与 Ultraplan" 选项 当 the user's 组织 或 认证 设置 can't reach Claude 代码 on the web
- 改进 测试版 tracing to honor `OTEL_LOG_USER_PROMPTS`, `OTEL_LOG_TOOL_DETAILS`, 和 `OTEL_LOG_TOOL_CONTENT`; sensitive span attributes are 不再 emitted 除非 opted in
- 改进 SDK `查询()` to clean up subprocess 和 temp 文件 当 consumers `break` 从 `用于 等待` 或 use `等待 使用`
- 修复 a 命令 injection 漏洞 in the POSIX `which` 回退 used by LSP 二进制 detection
- 修复 a 内存 泄漏 where long 会话 retained dozens of historical copies of the 消息 列表 in the 虚拟 scroller
- 修复 `--恢复`/`--继续` losing conversation 上下文 on large 会话 当 the loader anchored on a dead-end 分支 而不是 the live conversation
- 修复 `--恢复` 链 恢复 bridging 进入 an unrelated 子代理 conversation 当 a 子代理 消息 landed near a main-链 写入 gap
- 修复 a 崩溃 on `--恢复` 当 a 已持久化 编辑/写入 工具 result was 缺失 its `file_path`
- 修复 a hardcoded 5-分钟 请求 超时 that aborted 慢 backends (本地 LLMs, extended thinking, 慢 gateways) regardless of `API_TIMEOUT_MS`
- 修复 `权限.拒绝` rules not overriding a PreToolUse 钩子's `permissionDecision: "ask"` — previously the 钩子 could 降级 a 拒绝 进入 a 提示
- 修复 `--设置-sources` 无 `user` causing background 清理 to ignore `cleanupPeriodDays` 和 删除 conversation history older 比 30 天
- 修复 Bedrock SigV4 认证 failing 与 403 当 `ANTHROPIC_AUTH_TOKEN`, `apiKeyHelper`, 或 `ANTHROPIC_CUSTOM_HEADERS` 集合 an 授权 头信息
- 修复 `Claude -w <name>` failing 与 "already 存在" 之后 a 上一个 会话's 工作树 清理 left a stale 目录
- 修复 子代理 not inheriting MCP 工具 从 dynamically-injected 服务器
- 修复 sub-代理 运行中 in isolated 工作树 being 已拒绝 读取/编辑 访问 to 文件 inside their own 工作树
- 修复 沙盒化 Bash 命令 failing 与 `mktemp: No such 文件 或 目录` 之后 a fresh boot
- 修复 `Claude MCP serve` 工具 calls failing 与 "工具 执行 失败" in MCP clients that 验证 `outputSchema`
- 修复 `RemoteTrigger` 工具's `run` action sending an 空 正文 和 being rejected by the 服务器
- 修复 several `/恢复` picker 问题: narrow 默认 视图 hiding 会话 从 other projects, unreachable 预览 on Windows 终端, incorrect cwd in 工作树, 会话-not-found 错误 not surfacing in stderr, 终端 title not being 集合, 和 恢复 提示 overlapping the 提示 输入
- 修复 Grep 工具 ENOENT 当 the embedded ripgrep 二进制 路径 becomes stale (VS 代码 extension auto-更新, macOS 应用 Translocation); 现在 falls back to 系统 `rg` 和 self-heals mid-会话
- 修复 `/btw` writing a 复制 of the entire conversation to disk on every use
- 修复 `/上下文` Free space 和 消息 breakdown disagreeing 与 the 头信息 percentage
- 修复 several 插件 问题: slash 命令 resolving to the wrong 插件 与 复制 `name:` frontmatter, `/插件 更新` failing 与 `ENAMETOOLONG`, Discover showing already-installed 插件, 目录-源 插件 loading 从 a stale 版本 缓存, 和 skills not honoring `上下文: 分叉` 和 `代理` frontmatter fields
- 修复 the `/MCP` 菜单 offering OAuth-specific actions 用于 MCP 服务器 configured 与 `headersHelper`; 重新连接 is 现在 offered instead to re-invoke the helper 脚本
- 修复 `ctrl+]`, `ctrl+\`, 和 `ctrl+^` keybindings not firing in terminals that 发送 原始 C0 control bytes (终端.应用, 默认 iTerm2, xterm)
- 修复 `/login` OAuth URL 渲染 与 padding that prevented clean 鼠标 selection
- 修复 渲染 问题: flicker in non-全屏 mode 当 content above the visible area 更改, 终端 scrollback being wiped 期间 long 会话 in non-全屏 mode, 和 鼠标-滚动 转义 sequences occasionally leaking 进入 the 提示 as 文本
- 修复 崩溃 当 `设置.JSON` 环境变量 值 are numbers 而不是 strings
- 修复 in-应用 设置 writes (e.g. `/添加-dir --remember`, `/config`) not refreshing the in-内存 snapshot, preventing 移除 directories 从 being revoked mid-会话
- 修复 自定义 keybindings (`~/.Claude/keybindings.JSON`) not loading on Bedrock, Vertex, 和 other third-party providers
- 修复 `Claude --继续 -p` not correctly continuing 会话 created by `-p` 或 the SDK
- 修复 several 远程 Control 问题: 工作树 移除 on 会话 崩溃, 连接 失败 not persisting in the 转录, spurious "Disconnected" indicator in brief mode 用于 本地 会话, 和 `/远程-control` failing over SSH 当 only `CLAUDE_CODE_ORGANIZATION_UUID` is 集合
- 修复 `/insights` sometimes omitting the report 文件 链接 从 its 响应
- [VSCode] 修复 the 文件 attachment below the chat 输入 not clearing 当 the 最后 editor 标签页 is closed

## 2.1.98

- 新增 interactive Google Vertex AI 设置 wizard accessible 从 the login 屏幕 当 selecting "3rd-party platform", guiding you through GCP 认证, 项目 和 region 配置, 凭证 verification, 和 模型 pinning
- 新增 `CLAUDE_CODE_PERFORCE_MODE` 环境变量 var: 当 集合, 编辑/写入/NotebookEdit 失败 on 读取-only 文件 与 a `p4 编辑` 提示 而不是 silently overwriting them
- 新增 监控 工具 用于 流式 事件 从 background 脚本
- 新增 subprocess sandboxing 与 PID namespace isolation on Linux 当 `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB` is 集合, 和 `CLAUDE_CODE_SCRIPT_CAPS` 环境变量 var to 限制 per-会话 脚本 invocations
- 新增 `--exclude-动态-系统-提示-部分` 标志 to print mode 用于 改进 cross-user 提示 缓存
- 新增 `工作区.git_worktree` to the status line JSON 输入, 集合 whenever the 当前 目录 is inside a linked git 工作树
- 新增 W3C `TRACEPARENT` 环境变量 var to Bash 工具 subprocesses 当 OTEL tracing is 已启用, 所以 child-流程 spans correctly parent to Claude 代码's 追踪 树
- LSP: Claude 代码 现在 identifies itself to language 服务器 通过 `clientInfo` in the 初始化 请求
- 修复 a Bash 工具 权限 绕过 where a backslash-escaped 标志 could be auto-允许 as 读取-only 和 lead to arbitrary 代码 执行
- 修复 compound Bash 命令 bypassing forced 权限 prompts 用于 safety checks 和 explicit ask rules in auto 和 绕过-权限 modes
- 修复 读取-only 命令 与 环境变量-var prefixes not prompting 除非 the var is known-safe (`LANG`, `TZ`, `NO_COLOR`, etc.)
- 修复 redirects to `/dev/TCP/...` 或 `/dev/udp/...` not prompting 而不是 auto-allowing
- 修复 stalled 流式 响应 timing out 而不是 falling back to non-流式 mode
- 修复 429 retries burning all attempts in ~13s 当 the 服务器 returns a small `重试-之后` — exponential backoff 现在 applies as a minimum
- 修复 MCP OAuth `OAuth.authServerMetadataUrl` config 覆盖 not being honored on 令牌 刷新 之后 重启, affecting ADFS 和 similar IdPs
- 修复 capital letters being dropped to lowercase on xterm 和 VS 代码 integrated 终端 当 the kitty 键盘 协议 is 活动
- 修复 macOS 文本 replacements deleting the 触发 word 而不是 inserting the substitution
- 修复 `--dangerously-跳过-权限` being silently downgraded to accept-edits mode 之后 approving a 写入 to a protected 路径 通过 Bash
- 修复 managed-设置 允许 rules remaining 活动 之后 an 管理员 移除 them, 直到 流程 重启
- 修复 `权限.additionalDirectories` 更改 not applying mid-会话 — 移除 directories lose 访问 immediately 和 新增 ones work 无 重启
- 修复 removing a 目录 从 `additionalDirectories` revoking 访问 to the same 目录 passed 通过 `--添加-dir`
- 修复 `Bash(cmd:*)` 和 `Bash(git 提交 *)` wildcard 权限 rules failing to 匹配 命令 与 extra spaces 或 标签页
- 修复 `Bash(...)` 拒绝 rules being downgraded to a 提示 用于 piped 命令 that mix `cd` 与 other 段
- 修复 false Bash 权限 prompts 用于 `cut -d /`, `粘贴 -d /`, `列 -s /`, `awk '{print $1}' 文件`, 和 filenames containing `%`
- 修复 权限 rules 与 names matching JavaScript prototype properties (e.g. `toString`) causing `设置.JSON` to be silently ignored
- 修复 代理 团队 成员 not inheriting the leader's 权限 mode 当 使用 `--dangerously-跳过-权限`
- 修复 a 崩溃 in 全屏 mode 当 hovering over MCP 工具 results
- 修复 copying wrapped URLs in 全屏 mode inserting spaces at line breaks
- 修复 文件-编辑 diffs disappearing 从 the UI on `--恢复` 当 the edited 文件 was larger 比 10KB
- 修复 several `/恢复` picker 问题: `--恢复 <name>` opening uneditable, 过滤 重新加载 wiping 搜索 state, 空 列表 swallowing arrow 键, cross-项目 staleness, 和 transient 任务-status 文本 replacing conversation summaries
- 修复 `/export` not honoring absolute 路径 和 `~`, 和 silently rewriting user-supplied extensions to `.txt`
- 修复 `/effort max` being 已拒绝 用于 unknown 或 future 模型 IDs
- 修复 slash 命令 picker breaking 当 a 插件's frontmatter `name` is a YAML 布尔值 keyword
- 修复 rate-限制 upsell 文本 being hidden 之后 消息 remounts
- 修复 MCP 工具 与 `_meta["Anthropic/maxResultSizeChars"]` not bypassing the 令牌-基于 持久化 层
- 修复 语音 mode leaking dozens of space characters 进入 the 输入 当 re-holding the 推送-to-talk 键 当 the 上一个 转录 is still processing
- 修复 `DISABLE_AUTOUPDATER` not fully suppressing the npm registry 版本 check 和 symlink 修改 on npm-基于 installs
- 修复 a 内存 泄漏 where 远程 Control 权限 处理器 条目 were retained 用于 the lifetime of the 会话
- 修复 background 子代理 that 失败 与 an 错误 not reporting partial progress to the parent 代理
- 修复 提示-类型 停止/SubagentStop 钩子 failing on long 会话, 和 钩子 evaluator API 错误 showing "JSON validation 失败" 而不是 the real 消息
- 修复 feedback survey 渲染 当 dismissed
- 修复 Bash `grep -f 文件` / `rg -f 文件` not prompting 当 reading a 模式 文件 outside the working 目录
- 修复 stale 子代理 工作树 清理 removing 工作树 that contain untracked 文件
- 修复 `沙盒.网络.allowMachLookup` not taking effect on macOS
- 改进 `/恢复` 过滤 提示 labels 和 新增 项目/工作树/分支 names in the 过滤 indicator
- 改进 footer indicators (Focus, 通知) to stay on the mode-indicator 行 而不是 wrapping at narrow 终端 widths
- 改进 `/代理` 与 a tabbed 布局: a 运行中 标签页 shows live 子代理, 和 the 库 标签页 adds Run 代理 和 视图 运行中 实例 actions
- 改进 `/重新加载-插件` to pick up 插件-provided skills 无 requiring a 重启
- 改进 Accept Edits mode to auto-approve filesystem 命令 prefixed 与 safe 环境变量 vars 或 流程 wrappers
- 改进 Vim mode: `j`/`k` in NORMAL mode 现在 navigate history 和 select the footer pill at the 输入 边界
- 改进 钩子 错误 in the 转录 to include the 第一 line of stderr 用于 self-diagnosis 无 `--调试`
- 改进 OTEL tracing: interaction spans 现在 correctly 包装 full turns under 并发 SDK calls, 和 headless turns end spans per-turn
- 改进 转录 条目 to carry 最终 令牌 usage 而不是 流式 placeholders
- Updated the `/Claude-API` skill to cover Managed 代理 alongside Claude API
- [VSCode] 修复 false-positive "requires git-bash" 错误 on Windows 当 `CLAUDE_CODE_GIT_BASH_PATH` is 集合 或 git is installed at a 默认 location
- 修复 `CLAUDE_CODE_MAX_CONTEXT_TOKENS` to honor `DISABLE_COMPACT` 当 it is 集合.
- Dropped `/压缩` 提示 当 `DISABLE_COMPACT` is 集合.

## 2.1.97

- 新增 focus 视图 toggle (`Ctrl+O`) in `NO_FLICKER` mode showing 提示, one-line 工具 summary 与 编辑 diffstats, 和 最终 响应
- 新增 `refreshInterval` status line 设置 to re-run the status line 命令 every N 秒
- 新增 `工作区.git_worktree` to the status line JSON 输入, 集合 当 the 当前 目录 is inside a linked git 工作树
- 新增 `● N 运行中` indicator in `/代理` 下一个 to 代理 类型 与 live 子代理 instances
- 新增 syntax highlighting 用于 Cedar policy 文件 (`.cedar`, `.cedarpolicy`)
- 修复 `--dangerously-跳过-权限` being silently downgraded to accept-edits mode 之后 approving a 写入 to a protected 路径
- 修复 和 hardened Bash 工具 权限, tightening checks around 环境变量-var prefixes 和 网络 redirects, 和 reducing false prompts on common 命令
- 修复 权限 rules 与 names matching JavaScript prototype properties (e.g. `toString`) causing `设置.JSON` to be silently ignored
- 修复 managed-设置 允许 rules remaining 活动 之后 an 管理员 移除 them 直到 流程 重启
- 修复 `权限.additionalDirectories` 更改 in 设置 not applying mid-会话
- 修复 removing a 目录 从 `设置.权限.additionalDirectories` revoking 访问 to the same 目录 passed 通过 `--添加-dir`
- 修复 MCP HTTP/SSE 连接 accumulating ~50 MB/hr of unreleased buffers 当 服务器 重新连接
- 修复 MCP OAuth `OAuth.authServerMetadataUrl` not being honored on 令牌 刷新 之后 重启, 修复中 ADFS 和 similar IdPs
- 修复 429 retries burning all attempts in ~13 秒 当 the 服务器 returns a small `重试-之后` — exponential backoff 现在 applies as a minimum
- 修复 rate-限制 升级 选项 disappearing 之后 上下文 compaction
- 修复 several `/恢复` picker 问题: `--恢复 <name>` opening uneditable, Ctrl+A 重新加载 wiping 搜索, 空 列表 swallowing navigation, 任务-status 文本 replacing conversation summary, 和 cross-项目 staleness
- 修复 文件-编辑 diffs disappearing on `--恢复` 当 the edited 文件 was larger 比 10KB
- 修复 `--恢复` 缓存 misses 和 lost mid-turn 输入 从 attachment 消息 not being saved to the 转录
- 修复 消息 typed 当 Claude is working not being 已持久化 to the 转录
- 修复 提示-类型 `停止`/`SubagentStop` 钩子 failing on long 会话, 和 钩子 evaluator API 错误 displaying "JSON validation 失败" 而不是 the actual 消息
- 修复 子代理 与 工作树 isolation 或 `cwd:` 覆盖 leaking their working 目录 back to the parent 会话's Bash 工具
- 修复 compaction writing 复制 multi-MB 子代理 转录 文件 on 提示-too-long retries
- 修复 `Claude 插件 更新` reporting "already at the 最新 版本" 用于 git-基于 marketplace 插件 当 the 远程 had newer commits
- 修复 slash 命令 picker breaking 当 a 插件's frontmatter `name` is a YAML 布尔值 keyword
- 修复 copying wrapped URLs in `NO_FLICKER` mode inserting spaces at line breaks
- 修复 滚动 渲染 artifacts in `NO_FLICKER` mode 当 运行中 inside zellij
- 修复 a 崩溃 in `NO_FLICKER` mode 当 hovering over MCP 工具 results
- 修复 a `NO_FLICKER` mode 内存 泄漏 where API retries left stale 流式 state
- 修复 慢 鼠标-wheel 滚动 in `NO_FLICKER` mode on Windows 终端
- 修复 自定义 status line not displaying in `NO_FLICKER` mode on terminals shorter 比 24 rows
- 修复 Shift+Enter 和 Alt/Cmd+arrow shortcuts not working in Warp 与 `NO_FLICKER` mode
- 修复 Korean/Japanese/Unicode 文本 becoming garbled 当 copied in no-flicker mode on Windows
- 修复 Bedrock SigV4 认证 failing 当 `AWS_BEARER_TOKEN_BEDROCK` 或 `ANTHROPIC_BEDROCK_BASE_URL` are 集合 to 空 strings (as GitHub Actions does 用于 unset inputs)
- 改进 Accept Edits mode to auto-approve filesystem 命令 prefixed 与 safe 环境变量 vars 或 流程 wrappers (e.g. `LANG=C rm foo`, `超时 5 mkdir out`)
- 改进 自动模式 和 绕过-权限 mode to auto-approve 沙盒 网络 访问 prompts
- 改进 沙盒: `沙盒.网络.allowMachLookup` 现在 takes effect on macOS
- 改进 image handling: pasted 和 attached images are 现在 已压缩 to the same 令牌 budget as images 读取 通过 the 读取 工具
- 改进 slash 命令 和 `@`-mention completion to 触发 之后 CJK sentence punctuation, 所以 Japanese/Chinese 输入 不再 requires a space 之前 `/` 或 `@`
- 改进 Bridge 会话 to 显示 the 本地 git 仓库, 分支, 和 working 目录 on the Claude.ai 会话 card
- 改进 footer 布局: indicators (Focus, 通知) 现在 stay on the mode-indicator 行 而不是 wrapping below
- 改进 上下文-low 警告 to 显示 as a transient footer 通知 而不是 a persistent 行
- 改进 markdown blockquotes to 显示 a continuous left bar across wrapped lines
- 改进 会话 转录 size by skipping 空 钩子 条目 和 capping 已存储 pre-编辑 文件 copies
- 改进 转录 accuracy: per-块 条目 现在 carry the 最终 令牌 usage 而不是 the 流式 placeholder
- 改进 Bash 工具 OTEL tracing: subprocesses 现在 inherit a W3C `TRACEPARENT` 环境变量 var 当 tracing is 已启用
- Updated `/Claude-API` skill to cover Managed 代理 alongside the Claude API

## 2.1.96

- 修复 Bedrock 请求 failing 与 `403 "授权 头信息 is 缺失"` 当 使用 `AWS_BEARER_TOKEN_BEDROCK` 或 `CLAUDE_CODE_SKIP_BEDROCK_AUTH` (回归 in 2.1.94)

## 2.1.94

- 新增 support 用于 Amazon Bedrock powered by Mantle, 集合 `CLAUDE_CODE_USE_MANTLE=1`
- 更改 默认 effort 级别 从 medium to high 用于 API-键, Bedrock/Vertex/Foundry, 团队, 和 企业 用户 (control this 与 `/effort`)
- 新增 压缩 `Slacked #channel` 头信息 与 a clickable channel 链接 用于 Slack MCP 发送-消息 工具 calls
- 新增 `keep-coding-instructions` frontmatter 字段 support 用于 插件 输出 styles
- 新增 `hookSpecificOutput.sessionTitle` to `UserPromptSubmit` 钩子 用于 设置 the 会话 title
- 插件 skills declared 通过 `"skills": ["./"]` 现在 use the skill's frontmatter `name` 用于 the invocation name 而不是 the 目录 basename, giving a 稳定 name across 安装 方法
- 修复 代理 appearing stuck 之后 a 429 rate-限制 响应 与 a long 重试-之后 头信息 — the 错误 现在 surfaces immediately 而不是 silently waiting
- 修复 Console login on macOS silently failing 与 "Not logged in" 当 the login keychain is locked 或 its password is out of 同步 — the 错误 is 现在 surfaced 和 `Claude doctor` diagnoses the 修复
- 修复 插件 skill 钩子 defined in YAML frontmatter being silently ignored
- 修复 插件 钩子 failing 与 "No such 文件 或 目录" 当 `CLAUDE_PLUGIN_ROOT` was not 集合
- 修复 `${CLAUDE_PLUGIN_ROOT}` resolving to the marketplace 源 目录 而不是 the installed 缓存 用于 本地-marketplace 插件 on 启动
- 修复 scrollback showing the same diff repeated 和 空白 pages in long-运行中 会话
- 修复 multiline user prompts in the 转录 indenting wrapped lines under the `❯` caret 而不是 under the 文本
- 修复 Shift+Space inserting the literal word "space" 而不是 a space character in 搜索 inputs
- 修复 hyperlinks opening two browser 标签页 当 clicked inside tmux 运行中 in an xterm.js-基于 终端 (VS 代码, Hyper, Tabby)
- 修复 an alt-屏幕 渲染 缺陷 where content height 更改 mid-滚动 could leave compounding ghost lines
- 修复 `FORCE_HYPERLINK` 环境 变量 being ignored 当 集合 通过 `设置.JSON` `环境变量`
- 修复 原生 终端 光标 not tracking the selected 标签页 in dialogs, 所以 屏幕 readers 和 magnifiers can follow 标签页 navigation
- 修复 Bedrock invocation of Sonnet 3.5 v2 by 使用 the `us.` inference 分析 ID
- 修复 SDK/print mode not preserving the partial assistant 响应 in conversation history 当 interrupted mid-流
- 改进 `--恢复` to 恢复 会话 从 other 工作树 of the same 仓库 directly 而不是 printing a `cd` 命令
- 修复 CJK 和 other multibyte 文本 being corrupted 与 U+FFFD in 流-JSON 输入/输出 当 块 boundaries 分割 a UTF-8 sequence
- [VSCode] Reduced cold-打开 subprocess work on starting a 会话
- [VSCode] 修复 dropdown menus selecting the wrong 项 当 the 鼠标 was over the 列表 当 typing 或 使用 arrow 键
- [VSCode] 新增 a 警告 banner 当 `设置.JSON` 文件 失败 to 解析, 所以 用户 know their 权限 rules are not being applied

## 2.1.92

- 新增 `forceRemoteSettingsRefresh` policy 设置: 当 集合, the CLI 块 启动 直到 远程 managed 设置 are freshly fetched, 和 exits if the fetch fails (失败-closed)
- 新增 interactive Bedrock 设置 wizard accessible 从 the login 屏幕 当 selecting "3rd-party platform" — guides you through AWS 认证, region 配置, 凭证 verification, 和 模型 pinning
- 新增 per-模型 和 缓存-hit breakdown to `/cost` 用于 subscription 用户
- `/发布-备注` is 现在 an interactive 版本 picker
- 远程 Control 会话 names 现在 use your hostname as the 默认 前缀 (e.g. `myhost-graceful-unicorn`), overridable 与 `--远程-control-会话-name-前缀`
- Pro 用户 现在 see a footer 提示 当 returning to a 会话 之后 the 提示 缓存 has expired, showing roughly how many 令牌 the 下一个 turn will 发送 uncached
- 修复 子代理 spawning permanently failing 与 "Could not determine pane count" 之后 tmux Windows are killed 或 renumbered 期间 a long-运行中 会话
- 修复 提示-类型 停止 钩子 incorrectly failing 当 the small 快速 模型 returns `ok:false`, 和 restored `preventContinuation:true` semantics 用于 non-停止 提示-类型 钩子
- 修复 工具 输入 validation 失败 当 流式 emits 数组/对象 fields as JSON-已编码 strings
- 修复 an API 400 错误 that could occur 当 extended thinking produced a whitespace-only 文本 块 alongside real content
- 修复 accidental feedback survey submissions 从 auto-pilot keypresses 和 consecutive-提示 digit collisions
- 修复 misleading "esc to 中断" 提示 appearing alongside "esc to 清除" 当 a 文本 selection 存在 in 全屏 mode 期间 processing
- 修复 Homebrew 安装 更新 prompts to use the cask's 发布 channel (`Claude-代码` → 稳定, `Claude-代码@最新` → 最新)
- 修复 `ctrl+e` jumping to the end of the 下一个 line 当 already at end of line in multiline prompts
- 修复 an 问题 where the same 消息 could appear at two positions 当 滚动 up in 全屏 mode (iTerm2, Ghostty, 和 other terminals 与 DEC 2026 support)
- 修复 idle-return "/清除 to 保存 X 令牌" 提示 showing cumulative 会话 令牌 而不是 当前 上下文 size
- 修复 插件 MCP 服务器 stuck "connecting" on 会话 启动 当 they 复制 a Claude.ai connector 即 unauthenticated
- 改进 写入 工具 diff computation speed 用于 large 文件 (60% 更快 on 文件 与 标签页/`&`/`$`)
- 移除 `/tag` 命令
- 移除 `/vim` 命令 (toggle vim mode 通过 `/config` → Editor mode)
- Linux 沙盒 现在 ships the `apply-seccomp` helper in both npm 和 原生 builds, restoring unix-socket blocking 用于 沙盒化 命令

## 2.1.91

- 新增 MCP 工具 result persistence 覆盖 通过 `_meta["Anthropic/maxResultSizeChars"]` annotation (up to 500K), allowing larger results like DB schemas to pass through 无 truncation
- 新增 `disableSkillShellExecution` 设置 to 禁用 内联 shell 执行 in skills, 自定义 slash 命令, 和 插件 命令
- 新增 support 用于 multi-line prompts in `Claude-cli://打开?q=` deep links (已编码 newlines `%0A` 不再 rejected)
- 插件 can 现在 ship executables under `bin/` 和 invoke them as bare 命令 从 the Bash 工具
- 修复 转录 链 breaks on `--恢复` that could lose conversation history 当 异步 转录 writes 失败 silently
- 修复 `cmd+删除` not deleting to 启动 of line on iTerm2, kitty, WezTerm, Ghostty, 和 Windows 终端
- 修复 计划模式 in 远程 会话 losing track of the plan 文件 之后 a container 重启, which caused 权限 prompts on plan edits 和 an 空 plan-approval modal
- 修复 JSON schema validation 用于 `权限.defaultMode: "auto"` in 设置.JSON
- 修复 Windows 版本 清理 not protecting the 活动 版本's 回滚 复制
- `/feedback` 现在 explains why it's 不可用 而不是 disappearing 从 the slash 菜单
- 改进 `/Claude-API` skill guidance 用于 代理 design 模式 包括 工具 surface decisions, 上下文 management, 和 缓存 策略
- 改进 性能: 更快 `stripAnsi` on Bun by routing through `Bun.stripANSI`
- 编辑 工具 现在 uses shorter `old_string` anchors, reducing 输出 令牌

## 2.1.90

- 新增 `/powerup` — interactive lessons teaching Claude 代码 功能 与 animated demos
- 新增 `CLAUDE_CODE_PLUGIN_KEEP_MARKETPLACE_ON_FAILURE` 环境变量 var to keep the existing marketplace 缓存 当 `git 拉取` fails, useful in offline environments
- 新增 `.husky` to protected directories (acceptEdits mode)
- 修复 an infinite loop where the rate-限制 选项 对话框 would repeatedly auto-打开 之后 hitting your usage 限制, eventually crashing the 会话
- 修复 `--恢复` causing a full 提示-缓存 miss on the 第一 请求 用于 用户 与 deferred 工具, MCP 服务器, 或 自定义 代理 (回归 自从 v2.1.69)
- 修复 `编辑`/`写入` failing 与 "文件 content has 更改" 当 a PostToolUse 格式-on-保存 钩子 rewrites the 文件 between consecutive edits
- 修复 `PreToolUse` 钩子 that emit JSON to stdout 和 退出 与 代码 2 not correctly blocking the 工具 call
- 修复 collapsed 搜索/读取 summary badge appearing multiple times in 全屏 scrollback 当 a Claude.md 文件 auto-loads 期间 a 工具 call
- 修复 自动模式 not respecting explicit user boundaries ("don't 推送", "wait 用于 X 之前 Y") even 当 the action would otherwise be 允许
- 修复 click-to-expand hover 文本 being nearly invisible on light 终端 themes
- 修复 UI 崩溃 当 malformed 工具 输入 reached the 权限 对话框
- 修复 头信息 disappearing 当 滚动 `/模型`, `/config`, 和 other selection screens
- Hardened PowerShell 工具 权限 checks: 修复 trailing `&` background 作业 绕过, `-ErrorAction Break` debugger hang, 归档-extraction TOCTOU, 和 解析-失败 回退 拒绝-rule degradation
- 改进 性能: eliminated per-turn JSON.stringify of MCP 工具 schemas on 缓存-键 查找
- 改进 性能: SSE transport 现在 handles large streamed frames in linear time (was quadratic)
- 改进 性能: SDK 会话 与 long conversations 不再 慢 down quadratically on 转录 writes
- 改进 `/恢复` all-projects 视图 to 加载 项目 会话 in 并行, improving 加载 times 用于 用户 与 many projects
- 更改 `--恢复` picker to 不再 显示 会话 created by `Claude -p` 或 SDK invocations
- 移除 `Get-DnsClientCache` 和 `ipconfig /displaydns` 从 auto-允许 (DNS 缓存 privacy)

## 2.1.89

- 新增 `"defer"` 权限 decision to `PreToolUse` 钩子 — headless 会话 can pause at a 工具 call 和 恢复 与 `-p --恢复` to have the 钩子 re-evaluate
- 新增 `CLAUDE_CODE_NO_FLICKER=1` 环境 变量 to opt 进入 flicker-free alt-屏幕 渲染 与 virtualized scrollback
- 新增 `PermissionDenied` 钩子 that fires 之后 自动模式 classifier denials — return `{重试: true}` to tell the 模型 it can 重试
- 新增 named 子代理 to `@` mention typeahead 建议
- 新增 `MCP_CONNECTION_NONBLOCKING=true` 用于 `-p` mode to 跳过 the MCP 连接 wait entirely, 和 bounded `--MCP-config` 服务器 连接 at 5s 而不是 blocking on the slowest 服务器
- 自动模式: 已拒绝 命令 现在 显示 a 通知 和 appear in `/权限` → Recent 标签页 where you can 重试 与 `r`
- 修复 `编辑(//路径/**)` 和 `读取(//路径/**)` 允许 rules to check the resolved symlink 目标, not just the requested 路径
- 修复 语音 推送-to-talk not activating 用于 some modifier-combo bindings, 和 语音 mode on Windows failing 与 "WebSocket 升级 rejected 与 HTTP 101"
- 修复 编辑/写入 工具 doubling CRLF on Windows 和 stripping Markdown hard line breaks (two trailing spaces)
- 修复 `StructuredOutput` schema 缓存 缺陷 causing ~50% 失败 rate 当 使用 multiple schemas
- 修复 内存 泄漏 where large JSON inputs were retained as LRU 缓存 键 in long-运行中 会话
- 修复 a 崩溃 当 removing a 消息 从 very large 会话 文件 (over 50MB)
- 修复 LSP 服务器 zombie state 之后 崩溃 — 服务器 现在 restarts on 下一个 请求 而不是 failing 直到 会话 重启
- 修复 提示 history 条目 containing CJK 或 emoji being silently dropped 当 they fall on a 4KB 边界 in `~/.Claude/history.jsonl`
- 修复 `/stats` undercounting 令牌 by 排除 子代理 usage, 和 losing historical data beyond 30 天 当 the stats 缓存 格式 更改
- 修复 `-p --恢复` hangs 当 the deferred 工具 输入 exceeds 64KB 或 no deferred marker 存在, 和 `-p --继续` not resuming deferred 工具
- 修复 `Claude-cli://` deep links not opening on macOS
- 修复 MCP 工具 错误 truncating to only the 第一 content 块 当 the 服务器 returns multi-元素 错误 content
- 修复 skill reminders 和 other 系统 上下文 being dropped 当 sending 消息 与 images 通过 the SDK
- 修复 PreToolUse/PostToolUse 钩子 to 接收 `file_path` as an absolute 路径 用于 写入/编辑/读取 工具, matching the documented behavior
- 修复 autocompact thrash loop — 现在 detects 当 上下文 refills to the 限制 immediately 之后 compacting three times in a 行 和 stops 与 an actionable 错误 而不是 burning API calls
- 修复 提示 缓存 misses in long 会话 caused by 工具 schema bytes changing mid-会话
- 修复 nested Claude.md 文件 being re-injected dozens of times in long 会话 that 读取 many 文件
- 修复 `--恢复` 崩溃 当 转录 contains a 工具 result 从 an older CLI 版本 或 interrupted 写入
- 修复 misleading "速率限制 reached" 消息 当 the API returned an entitlement 错误 — 现在 shows the actual 错误 与 actionable 提示
- 修复 钩子 `if` 条件 filtering not matching compound 命令 (`ls && git 推送`) 或 命令 与 环境变量-var prefixes (`FOO=bar git 推送`)
- 修复 collapsed 搜索/读取 组 badges duplicating in 终端 scrollback 期间 heavy 并行 工具 use
- 修复 通知 `invalidates` not clearing the currently-displayed 通知 immediately
- 修复 提示 briefly disappearing 之后 提交 当 background 消息 arrived 期间 processing
- 修复 Devanagari 和 other combining-mark 文本 being truncated in assistant 输出
- 修复 渲染 artifacts on main-屏幕 terminals 之后 布局 shifts
- 修复 语音 mode failing to 请求 麦克风 权限 on macOS Apple Silicon
- 修复 Shift+Enter submitting 而不是 inserting a newline on Windows 终端 预览 1.25
- 修复 periodic UI jitter 期间 流式 in iTerm2 当 运行中 inside tmux
- 修复 PowerShell 工具 incorrectly reporting 失败 当 命令 like `git 推送` wrote progress to stderr on Windows PowerShell 5.1
- 修复 a potential out-of-内存 崩溃 当 the 编辑 工具 was used on very large 文件 (>1 GiB)
- 改进 collapsed 工具 summary to 显示 "Listed N directories" 用于 `ls`/`树`/`du` 而不是 "读取 N 文件"
- 改进 Bash 工具 to warn 当 a formatter/linter 命令 modifies 文件 you have previously 读取, preventing stale-编辑 错误
- 改进 `@`-mention typeahead to 等级 源 文件 above MCP 资源 与 similar names
- 改进 PowerShell 工具 提示 与 版本-appropriate syntax guidance (5.1 vs 7+)
- 更改 `编辑` to work on 文件 viewed 通过 `Bash` 与 `sed -n` 或 `cat`, 无 requiring a separate `读取` call 第一
- 更改 钩子 输出 over 50K characters to be saved to disk 与 a 文件 路径 + 预览 而不是 being injected directly 进入 上下文
- 更改 `cleanupPeriodDays: 0` in 设置.JSON to be rejected 与 a validation 错误 — it previously silently 已禁用 转录 persistence
- 更改 thinking summaries to 不再 be 已生成 by 默认 in interactive 会话 — 集合 `showThinkingSummaries: true` in 设置.JSON to 恢复
- Documented `TaskCreated` 钩子 事件 和 its blocking behavior
- Preserved 任务 通知 当 backgrounding a 运行中 命令 与 Ctrl+B
- PowerShell 工具 on Windows: 外部-命令 arguments containing both a double-quote 和 whitespace 现在 提示 而不是 auto-allowing (PS 5.1 参数-splitting hardening)
- `/环境变量` 现在 applies to PowerShell 工具 命令 (previously only affected Bash)
- `/usage` 现在 hides redundant "当前 week (Sonnet only)" bar 用于 Pro 和 企业 plans
- Image 粘贴 不再 inserts a trailing space
- Pasting `!命令` 进入 an 空 提示 现在 enters bash mode, matching typed `!` behavior
- `/buddy` is here 用于 April 1st — hatch a small creature that watches you 代码

## 2.1.87

- 修复 消息 in Cowork Dispatch not getting delivered

## 2.1.86

- 新增 `X-Claude-代码-会话-ID` 头信息 to API 请求 所以 proxies can aggregate 请求 by 会话 无 解析中 the 正文
- 新增 `.jj` 和 `.sl` to VCS 目录 exclusion lists 所以 Grep 和 文件 autocomplete don't descend 进入 Jujutsu 或 Sapling 元数据
- 修复 `--恢复` failing 与 "tool_use ids were found 无 tool_result 块" on 会话 created 之前 v2.1.85
- 修复 写入/编辑/读取 failing on 文件 outside the 项目 根 (e.g., `~/.Claude/Claude.md`) 当 conditional skills 或 rules are configured
- 修复 unnecessary config disk writes on every skill invocation that could cause 性能 问题 和 config corruption on Windows
- 修复 potential out-of-内存 崩溃 当 使用 `/feedback` on very long 会话 与 large 转录 文件
- 修复 `--bare` mode dropping MCP 工具 in interactive 会话 和 silently discarding 消息 enqueued mid-turn
- 修复 the `c` shortcut copying only ~20 characters of the OAuth login URL 而不是 the full URL
- 修复 masked 输入 (e.g., OAuth 代码 粘贴) leaking the 启动 of the 令牌 当 wrapping across multiple lines on narrow terminals
- 修复 official marketplace 插件 脚本 failing 与 "权限 已拒绝" on macOS/Linux 自从 v2.1.83
- 修复 statusline showing another 会话's 模型 当 运行中 multiple Claude 代码 instances 和 使用 `/模型` in one of them
- 修复 滚动 not following 新 消息 之后 wheel 滚动 或 click-to-select at the bottom of a long conversation
- 修复 `/插件` 卸载 对话框: pressing `n` 现在 correctly uninstalls the 插件 当 preserving its data 目录
- 修复 a 回归 where pressing Enter 之后 clicking could leave the 转录 空白 直到 the 响应 arrived
- 修复 `超深度思考` 提示 lingering 之后 deleting the keyword
- 修复 内存 growth in long 会话 从 markdown/highlight 渲染 caches retaining full content strings
- Reduced 启动 事件-loop stalls 当 many Claude.ai MCP connectors are configured (macOS keychain 缓存 extended 从 5s to 30s)
- Reduced 令牌 开销 当 mentioning 文件 与 `@` — 原始 字符串 content 不再 JSON-escaped
- 改进 提示 缓存 hit rate 用于 Bedrock, Vertex, 和 Foundry 用户 by removing 动态 content 从 工具 descriptions
- 内存 filenames in the "Saved N memories" notice 现在 highlight on hover 和 打开 on click
- Skill descriptions in the `/skills` listing are 现在 capped at 250 characters to reduce 上下文 usage
- 更改 `/skills` 菜单 to sort alphabetically 用于 easier scanning
- 自动模式 现在 shows "不可用 用于 your plan" 当 已禁用 by plan restrictions (was "temporarily 不可用")
- [VSCode] 修复 extension incorrectly showing "Not responding" 期间 long-运行中 operations
- [VSCode] 修复 extension defaulting Max plan 用户 to Sonnet 之后 the OAuth 令牌 refreshes (8 小时 之后 login)
- 读取 工具 现在 uses 压缩 line-数字 格式 和 deduplicates unchanged re-reads, reducing 令牌 usage

## 2.1.85

- 新增 `CLAUDE_CODE_MCP_SERVER_NAME` 和 `CLAUDE_CODE_MCP_SERVER_URL` 环境 变量 to MCP `headersHelper` 脚本, allowing one helper to serve multiple 服务器
- 新增 conditional `if` 字段 用于 钩子 使用 权限 rule syntax (e.g., `Bash(git *)`) to 过滤 当 they run, reducing 流程 spawning 开销
- 新增 timestamp markers in transcripts 当 scheduled 任务 (`/loop`, `CronCreate`) fire
- 新增 trailing space 之后 `[Image #N]` placeholder 当 pasting images
- Deep 链接 queries (`Claude-cli://打开?q=…`) 现在 support up to 5,000 characters, 与 a "滚动 to review" 警告 用于 long pre-filled prompts
- MCP OAuth 现在 follows RFC 9728 Protected 资源 元数据 discovery to 查找 the 授权 服务器
- 插件 blocked by 组织 policy (`managed-设置.JSON`) can 不再 be installed 或 已启用, 和 are hidden 从 marketplace views
- PreToolUse 钩子 can 现在 satisfy `AskUserQuestion` by returning `updatedInput` alongside `permissionDecision: "允许"`, enabling headless 集成 that collect answers 通过 their own UI
- `tool_parameters` in OpenTelemetry tool_result 事件 are 现在 gated behind `OTEL_LOG_TOOL_DETAILS=1`
- 修复 `/压缩` failing 与 "上下文 exceeded" 当 the conversation has grown too large 用于 the 压缩 请求 itself to fit
- 修复 `/插件 启用` 和 `/插件 禁用` failing 当 a 插件's 安装 location differs 从 where it's declared in 设置
- 修复 `--工作树` exiting 与 an 错误 in non-git repositories 之前 the `WorktreeCreate` 钩子 could run
- 修复 `deniedMcpServers` 设置 not blocking Claude.ai MCP 服务器
- 修复 `switch_display` in the computer-use 工具 returning "not 可用 in this 会话" on multi-监控 setups
- 修复 崩溃 当 `OTEL_LOGS_EXPORTER`, `OTEL_METRICS_EXPORTER`, 或 `OTEL_TRACES_EXPORTER` is 集合 to `none`
- 修复 diff syntax highlighting not working in non-原生 builds
- 修复 MCP 步骤-up 授权 failing 当 a 刷新 令牌 存在 — 服务器 requesting elevated scopes 通过 `403 insufficient_scope` 现在 correctly 触发 the re-授权 flow
- 修复 内存 泄漏 in 远程 会话 当 a 流式 响应 is interrupted
- 修复 persistent ECONNRESET 错误 期间 边 连接 churn by 使用 a fresh TCP 连接 on 重试
- 修复 prompts getting stuck in the 队列 之后 运行中 certain slash 命令, 与 up-arrow unable to retrieve them
- 修复 Python 代理 SDK: `类型:'sdk'` MCP 服务器 passed 通过 `--MCP-config` are 不再 dropped 期间 启动
- 修复 原始 键 sequences appearing in the 提示 当 运行中 over SSH 或 in the VS 代码 integrated 终端
- 修复 远程 Control 会话 status staying stuck on "Requires Action" 之后 a 权限 is resolved
- 修复 shift+enter 和 meta+enter being intercepted by typeahead 建议 而不是 inserting newlines
- 修复 stale content bleeding through 当 滚动 up 期间 流式
- 修复 终端 left in enhanced 键盘 mode 之后 退出 in Ghostty, Kitty, WezTerm, 和 other terminals supporting the Kitty 键盘 协议 — Ctrl+C 和 Ctrl+D 现在 work correctly 之后 quitting
- 改进 @-mention 文件 autocomplete 性能 on large repositories
- 改进 PowerShell dangerous 命令 detection
- 改进 滚动 性能 与 large transcripts by replacing WASM yoga-布局 与 a pure TypeScript 实现
- Reduced UI stutter 当 compaction triggers on large 会话

## 2.1.84

- 新增 PowerShell 工具 用于 Windows as an opt-in 预览. Learn more at HTTPS://代码.Claude.com/文档/en/工具-引用#powershell-工具
- 新增 `ANTHROPIC_DEFAULT_{Opus,Sonnet,Haiku}_MODEL_SUPPORTS` 环境变量 vars to 覆盖 effort/thinking capability detection 用于 pinned 默认 模型 用于 3p (Bedrock, Vertex, Foundry), 和 `_MODEL_NAME`/`_DESCRIPTION` to customize the `/模型` picker label
- 新增 `CLAUDE_STREAM_IDLE_TIMEOUT_MS` 环境变量 var to 配置 the 流式 idle watchdog 阈值 (默认 90s)
- 新增 `TaskCreated` 钩子 that fires 当 a 任务 is created 通过 `TaskCreate`
- 新增 `WorktreeCreate` 钩子 support 用于 `类型: "HTTP"` — return the created 工作树 路径 通过 `hookSpecificOutput.worktreePath` in the 响应 JSON
- 新增 `allowedChannelPlugins` managed 设置 用于 团队/企业 admins to define a channel 插件 allowlist
- 新增 `x-客户端-请求-ID` 头信息 to API 请求 用于 调试 timeouts
- 新增 idle-return 提示 that nudges 用户 returning 之后 75+ 分钟 to `/清除`, reducing unnecessary 令牌 re-缓存 on stale 会话
- Deep links (`Claude-cli://`) 现在 打开 in your preferred 终端 而不是 whichever 终端 happens to be 第一 in the detection 列表
- Rules 和 skills `路径:` frontmatter 现在 accepts a YAML 列表 of globs
- MCP 工具 descriptions 和 服务器 instructions are 现在 capped at 2KB to prevent OpenAPI-已生成 服务器 从 bloating 上下文
- MCP 服务器 configured both locally 和 通过 Claude.ai connectors are 现在 deduplicated — the 本地 config wins
- Background bash 任务 that appear stuck on an interactive 提示 现在 surface a 通知 之后 ~45 秒
- 令牌 counts ≥1M 现在 显示 as "1.5m" 而不是 "1512.6k"
- 全局 系统-提示 缓存 现在 works 当 `ToolSearch` is 已启用, 包括 用于 用户 与 MCP 工具 configured
- 修复 语音 推送-to-talk: holding the 语音 键 不再 leaks characters 进入 the 文本 输入, 和 transcripts 现在 插入 at the correct 位置
- 修复 up/down arrow 键 being unresponsive 当 a footer 项 is focused
- 修复 `Ctrl+U` (终止-to-line-启动) being a no-op at line boundaries in multiline 输入, 所以 repeated `Ctrl+U` 现在 clears across lines
- 修复 空-unbinding a 默认 chord binding (e.g. `"ctrl+x ctrl+k": 空`) still entering chord-wait mode 而不是 freeing the 前缀 键
- 修复 鼠标 事件 inserting literal "鼠标" 文本 进入 转录 搜索 输入
- 修复 工作流 子代理 failing 与 API 400 当 the outer 会话 uses `--JSON-schema` 和 the 子代理 also specifies a schema
- 修复 缺失 background color behind certain emoji in user 消息 bubbles on some terminals
- 修复 the "允许 Claude to 编辑 its own 设置 用于 this 会话" 权限 选项 not sticking 用于 用户 与 `编辑(.Claude)` 允许 rules
- 修复 a hang 当 generating attachment snippets 用于 large edited 文件
- 修复 MCP 工具/资源 缓存 泄漏 on 服务器 重新连接
- 修复 a 启动 性能 问题 where partial 克隆 repositories (Scalar/GVFS) triggered mass blob downloads
- 修复 原生 终端 光标 not tracking the 文本 输入 caret, 所以 IME composition (CJK 输入) 现在 renders 内联 和 屏幕 readers can follow the 输入 位置
- 修复 spurious "Not logged in" 错误 on macOS caused by transient keychain 读取 失败
- 修复 cold-启动 race where core 工具 could be deferred 无 their 绕过 活动, causing 编辑/写入 to 失败 与 InputValidationError on typed parameters
- 改进 detection 用于 dangerous removals of Windows drive roots (`C:\`, `C:\Windows`, etc.)
- 改进 interactive 启动 by ~30ms by 运行中 `设置()` in 并行 与 slash 命令 和 代理 loading
- 改进 启动 用于 `Claude "提示"` 与 MCP 服务器 — the REPL 现在 renders immediately 而不是 blocking 直到 all 服务器 连接
- 改进 远程 Control to 显示 a specific reason 当 blocked 而不是 a 泛型 "not yet 已启用" 消息
- 改进 p90 提示 缓存 rate
- Reduced 滚动-to-top resets in long 会话 by making the 消息 窗口 immune to compaction 和 grouping 更改
- Reduced 终端 flickering 当 animated 工具 progress scrolls above the viewport
- 更改 问题/PR references to only become clickable links 当 written as `owner/仓库#123` — bare `#123` is 不再 auto-linked
- Slash 命令 不可用 用于 the 当前 认证 设置 (`/语音`, `/mobile`, `/Chrome`, `/升级`, etc.) are 现在 hidden 而不是 shown
- [VSCode] 新增 速率限制 警告 banner 与 usage percentage 和 reset time
- Stats screenshot (Ctrl+S in /stats) 现在 works in all builds 和 is 16× 更快

## 2.1.83

- 新增 `managed-设置.d/` drop-in 目录 alongside `managed-设置.JSON`, letting separate 团队 部署 independent policy 片段 that 合并 alphabetically
- 新增 `CwdChanged` 和 `FileChanged` 钩子 事件 用于 reactive 环境 management (e.g., direnv)
- 新增 `沙盒.failIfUnavailable` 设置 to 退出 与 an 错误 当 沙盒 is 已启用 but cannot 启动, 而不是 运行中 unsandboxed
- 新增 `disableDeepLinkRegistration` 设置 to prevent `Claude-cli://` 协议 处理器 registration
- 新增 `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB=1` to 去除 Anthropic 和 cloud provider credentials 从 subprocess environments (Bash 工具, 钩子, MCP stdio 服务器)
- 新增 转录 搜索 — press `/` in 转录 mode (`Ctrl+O`) to 搜索, `n`/`N` to 步骤 through matches
- 新增 `Ctrl+X Ctrl+E` as an alias 用于 opening the 外部 editor (readline-原生 binding; `Ctrl+G` still works)
- Pasted images 现在 插入 an `[Image #N]` chip at the 光标 所以 you can 引用 them positionally in your 提示
- 代理 can 现在 declare `initialPrompt` in frontmatter to auto-提交 a 第一 turn
- `chat:killAgents` 和 `chat:fastMode` are 现在 rebindable 通过 `~/.Claude/keybindings.JSON`
- 修复 鼠标 tracking 转义 sequences leaking to shell 提示 之后 退出
- 修复 Claude 代码 hanging on 退出 on macOS
- 修复 屏幕 flashing 空白 之后 being idle 用于 a few 秒
- 修复 a hang 当 diffing very large 文件 与 few common lines — diffs 现在 time out 之后 5 秒 和 fall back gracefully
- 修复 a 1–8 秒 UI freeze on 启动 当 语音 输入 was 已启用, caused by eagerly loading the 原生 audio 模块
- 修复 a 启动 回归 where Claude 代码 would wait ~3s 用于 Claude.ai MCP config fetch 之前 proceeding
- 修复 `--MCP-config` CLI 标志 bypassing `allowedMcpServers`/`deniedMcpServers` managed policy enforcement
- 修复 Claude.ai MCP connectors (Slack, Gmail, etc.) not being 可用 in single-turn `--print` mode
- 修复 `caffeinate` 流程 not properly terminating 当 Claude 代码 exits, preventing Mac 从 sleeping
- 修复 bash mode not activating 当 标签页-accepting `!`-prefixed 命令 建议
- 修复 stale slash 命令 selection showing wrong highlighted 命令 之后 navigating 建议
- 修复 `/config` 菜单 showing both the 搜索 光标 和 列表 selection 同时
- 修复 background 子代理 becoming invisible 之后 上下文 compaction, which could cause 复制 代理 to be spawned
- 修复 background 代理 任务 staying stuck in "运行中" state 当 git 或 API calls hang 期间 清理
- 修复 `--channels` showing "Channels are not currently 可用" on 第一 启动 之后 升级
- 修复 uninstalled 插件 钩子 continuing to fire 直到 the 下一个 会话
- 修复 queued 命令 flickering 期间 流式 响应
- 修复 slash 命令 being sent to the 模型 as 文本 当 submitted 当 a 消息 is processing
- 修复 scrollback jumping 当 collapsed 读取/搜索 组 finish 之后 滚动 offscreen
- 修复 scrollback jumping to top 当 the 模型 starts 或 stops thinking
- 修复 SDK 会话 history loss on 恢复 caused by 钩子 progress/attachment 消息 forking the parentUuid 链
- 修复 复制-on-select not firing 当 you 发布 the 鼠标 outside the 终端 窗口
- 修复 ghost characters appearing in height-constrained lists 当 项 overflow
- 修复 `Ctrl+B` interfering 与 readline backward-char at an idle 提示 — it 现在 only fires 当 a foreground 任务 can be backgrounded
- 修复 工具 result 文件 never being cleaned up, ignoring the `cleanupPeriodDays` 设置
- 修复 space 键 being swallowed 用于 up to 3 秒 之后 releasing 语音 hold-to-talk
- 修复 ALSA 库 错误 corrupting the 终端 UI 当 使用 语音 mode on Linux 无 audio 硬件 (Docker, headless, WSL1)
- 修复 语音 mode SoX detection on Termux/Android where spawning `which` is kernel-restricted
- 修复 远程 Control 会话 showing as Idle in the web 会话 列表 当 actively 运行中
- 修复 footer navigation selecting an invisible 远程 Control pill in config-driven mode
- 修复 内存 泄漏 in 远程 会话 where 工具 use IDs accumulate indefinitely
- 改进 Bedrock SDK cold-启动 延迟 by overlapping 分析 fetch 与 other boot work
- 改进 `--恢复` 内存 usage 和 启动 延迟 on large 会话
- 改进 插件 启动 — 命令, skills, 和 代理 现在 加载 从 disk 缓存 无 re-fetching
- 改进 远程 Control 会话 titles: AI-已生成 titles 现在 appear within 秒 of the 第一 消息
- 改进 `WebFetch` to identify as `Claude-User` 所以 site operators can recognize 和 allowlist Claude 代码 traffic 通过 `robots.txt`
- Reduced `WebFetch` peak 内存 usage 用于 large pages
- Reduced scrollback resets in long 会话 从 once per turn to once per ~50 消息
- 更快 `Claude -p` 启动 与 unauthenticated HTTP/SSE MCP 服务器 (~600ms saved)
- Bash ghost-文本 建议 现在 include just-submitted 命令 immediately
- Increased non-流式 回退 令牌 cap (21k → 64k) 和 超时 (120s → 300s 本地) 所以 回退 请求 are less likely to be truncated
- Interrupting a 提示 之前 any 响应 现在 automatically restores your 输入 所以 you can 编辑 和 resubmit
- `/status` 现在 works 当 Claude is responding, 而不是 being queued 直到 the turn finishes
- 插件 MCP 服务器 that 复制 an 组织-managed connector are 现在 suppressed 而不是 运行中 a 秒 连接
- Linux: respect `XDG_DATA_HOME` 当 registering the `Claude-cli://` 协议 处理器
- 更改 "停止 all background 代理" keybinding 从 `Ctrl+F` to `Ctrl+X Ctrl+K` to 停止 shadowing readline 转发-char
- 弃用 `TaskOutput` 工具 in favor of 使用 `读取` on the background 任务's 输出 文件 路径
- 新增 `CLAUDE_CODE_DISABLE_NONSTREAMING_FALLBACK` 环境变量 var to 禁用 the non-流式 回退 当 流式 fails
- 插件 选项 (`manifest.userConfig`) 现在 可用 externally — 插件 can 提示 用于 配置 at 启用 time, 与 `sensitive: true` 值 已存储 in keychain (macOS) 或 protected credentials 文件 (other platforms)
- Claude can 现在 引用 the on-disk 路径 of 剪贴板-pasted images 用于 文件 operations
- `Ctrl+L` 现在 clears the 屏幕 和 forces a full redraw — use this to recover 当 Cmd+K 叶子 the UI partially 空白. Use `Ctrl+U` 或 double-Esc to 清除 提示 输入.
- `--bare -p` (SDK 模式) is ~14% 更快 to the API 请求
- 内存: `内存.md` 索引 现在 truncates at 25KB 以及 200 lines
- 已禁用 `AskUserQuestion` 和 plan-mode 工具 当 `--channels` is 活动
- 修复 API 400 错误 当 a pasted image was queued 期间 a failing 工具 call
- 修复 MCP 工具 calls hanging indefinitely 当 an SSE 连接 drops mid-call 和 exhausts its reconnection attempts
- 修复 远程 Control 会话 titles showing 原始 XML 当 a background 代理 完成 之前 the 第一 user 消息
- 修复 远程 会话 forgetting conversation history 之后 a container 重启 由于 progress-消息 gaps in the resumed 转录 链
- 修复 远程 会话 requiring re-login on transient 认证 错误 而不是 retrying automatically
- 修复 `rg ... | wc -l` 和 similar piped 命令 hanging 和 returning `0` in 沙盒 mode on Linux
- 修复 语音 输入 hold-to-talk not activating 当 a CJK IME inserts a full-width space
- 修复 `--工作树` hanging silently 当 the 工作树 name contained a 转发 slash
- [VSCode] 加载动画 现在 turns red 与 "Not responding" 当 the backend hasn't responded 用于 60 秒
- [VSCode] 修复 会话 history not loading correctly 当 reopening a 会话 通过 URL 或 之后 重启
- [VSCode] 新增 Esc-twice (或 `/rewind`) to 打开 a 键盘-navigable rewind picker
- [VSCode] 修复 "分叉 conversation 从 here" 和 rewind actions failing silently 之后 the 会话 缓存 goes stale

## 2.1.81

- 新增 `--bare` 标志 用于 scripted `-p` calls — skips 钩子, LSP, 插件 同步, 和 skill 目录 walks; requires `ANTHROPIC_API_KEY` 或 an `apiKeyHelper` 通过 `--设置` (OAuth 和 keychain 认证 已禁用); auto-内存 fully 已禁用
- 新增 `--channels` 权限 relay — channel 服务器 that declare the 权限 capability can 转发 工具 approval prompts to your phone
- 修复 multiple 并发 Claude 代码 会话 requiring repeated re-认证 当 one 会话 refreshes its OAuth 令牌
- 修复 语音 mode silently swallowing 重试 失败 和 showing a misleading "check your 网络" 消息 而不是 the actual 错误
- 修复 语音 mode audio not recovering 当 the 服务器 silently drops the WebSocket 连接
- 修复 `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` not suppressing the structured-outputs 测试版 头信息, causing 400 错误 on 代理 gateways forwarding to Vertex/Bedrock
- 修复 `--channels` 绕过 用于 团队/企业 orgs 与 no other managed 设置 configured
- 修复 a 崩溃 on 节点.js 18
- 修复 unnecessary 权限 prompts 用于 Bash 命令 containing dashes in strings
- 修复 插件 钩子 blocking 提示 submission 当 the 插件 目录 is deleted mid-会话
- 修复 a race 条件 where background 代理 任务 输出 could hang indefinitely 当 the 任务 完成 between polling intervals
- Resuming a 会话 that was in a 工作树 现在 switches back to that 工作树
- 修复 `/btw` not 包括 pasted 文本 当 used 期间 an 活动 响应
- 修复 a race where 快速 Cmd+标签页 followed by 粘贴 could beat the 剪贴板 复制 under tmux
- 修复 终端 标签页 title not updating 与 an auto-已生成 会话 description
- 修复 invisible 钩子 attachments inflating the 消息 count in 转录 mode
- 修复 远程 Control 会话 showing a 泛型 title 而不是 deriving 从 the 第一 提示
- 修复 `/rename` not syncing the title 用于 远程 Control 会话
- 修复 远程 Control `/退出` not reliably archiving the 会话
- 改进 MCP 读取/搜索 工具 calls to collapse 进入 a single "Queried {服务器}" line (expand 与 Ctrl+O)
- 改进 `!` bash mode discoverability — Claude 现在 suggests it 当 you need to run an interactive 命令
- 改进 插件 freshness — ref-tracked 插件 现在 re-克隆 on every 加载 to pick up upstream 更改
- 改进 远程 Control 会话 titles to 刷新 之后 your third 消息
- Updated MCP OAuth to support 客户端 ID 元数据 Document (CIMD / SEP-991) 用于 服务器 无 动态 客户端 Registration
- 更改 计划模式 to 隐藏 the "清除 上下文" 选项 by 默认 (恢复 与 `"showClearContextOnPlanAccept": true`)
- 已禁用 line-by-line 响应 流式 on Windows (包括 WSL in Windows 终端) 由于 渲染 问题
- [VSCode] 修复 Windows 路径 inheritance 用于 Bash 工具 当 使用 git Bash (回归 in v2.1.78)

## 2.1.80

- 新增 `rate_limits` 字段 to statusline 脚本 用于 displaying Claude.ai 速率限制 usage (5-小时 和 7-天 Windows 与 `used_percentage` 和 `resets_at`)
- 新增 `源: '设置'` 插件 marketplace 源 — declare 插件 条目 内联 in 设置.JSON
- 新增 CLI 工具 usage detection to 插件 技巧, 除了 文件 模式 matching
- 新增 `effort` frontmatter support 用于 skills 和 slash 命令 to 覆盖 the 模型 effort 级别 当 invoked
- 新增 `--channels` (research 预览) — 允许 MCP 服务器 to 推送 消息 进入 your 会话
- 修复 `--恢复` dropping 并行 工具 results — 会话 与 并行 工具 calls 现在 恢复 all tool_use/tool_result pairs 而不是 showing `[工具 result 缺失]` placeholders
- 修复 语音 mode WebSocket 失败 caused by Cloudflare bot detection on non-browser TLS fingerprints
- 修复 400 错误 当 使用 fine-grained 工具 流式 through API proxies, Bedrock, 或 Vertex
- 修复 `/远程-control` appearing 用于 gateway 和 third-party provider 部署 where it cannot 函数
- 修复 `/沙盒` 标签页 switching not responding to 标签页 或 arrow 键
- 改进 responsiveness of `@` 文件 autocomplete in large git repositories
- 改进 `/effort` to 显示 what auto currently resolves to, matching the status bar indicator
- 改进 `/权限` — 标签页 和 arrow 键 现在 switch 标签页 从 within a 列表
- 改进 background 任务 面板 — left arrow 现在 closes 从 the 列表 视图
- Simplified 插件 安装 技巧 to use a single `/插件 安装` 命令 而不是 a two-步骤 flow
- Reduced 内存 usage on 启动 in large repositories (~80 MB saved on 250k-文件 repos)
- 修复 managed 设置 (`enabledPlugins`, `权限.defaultMode`, policy-集合 环境变量 vars) not being applied at 启动 当 `远程-设置.JSON` was cached 从 a prior 会话

## 2.1.79

- 新增 `--console` 标志 to `Claude 认证 login` 用于 Anthropic Console (API billing) 认证
- 新增 "显示 turn duration" toggle to the `/config` 菜单
- 修复 `Claude -p` hanging 当 spawned as a subprocess 无 explicit stdin (e.g. Python `subprocess.run`)
- 修复 Ctrl+C not working in `-p` (print) mode
- 修复 `/btw` returning the main 代理's 输出 而不是 answering the side question 当 triggered 期间 流式
- 修复 语音 mode not activating correctly on 启动 当 `voiceEnabled: true` is 集合
- 修复 left/right arrow 标签页 navigation in `/权限`
- 修复 `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` not preventing 终端 title 从 being 集合 on 启动
- 修复 自定义 status line showing nothing 当 工作区 trust is blocking it
- 修复 企业 用户 being unable to 重试 on 速率限制 (429) 错误
- 修复 `SessionEnd` 钩子 not firing 当 使用 interactive `/恢复` to switch 会话
- 改进 启动 内存 usage by ~18MB across all scenarios
- 改进 non-流式 API 回退 与 a 2-分钟 per-attempt 超时, preventing 会话 从 hanging indefinitely
- `CLAUDE_CODE_PLUGIN_SEED_DIR` 现在 supports multiple seed directories separated by the platform 路径 delimiter (`:` on Unix, `;` on Windows)
- [VSCode] 新增 `/远程-control` — bridge your 会话 to Claude.ai/代码 to 继续 从 a browser 或 phone
- [VSCode] 会话 标签页 现在 get AI-已生成 titles 基于 on your 第一 消息
- [VSCode] 修复 the thinking pill showing "Thinking" 而不是 "Thought 用于 Ns" 之后 a 响应 completes
- [VSCode] 修复 缺失 会话 diff 按钮 当 opening 会话 从 the left sidebar

## 2.1.78

- 新增 `StopFailure` 钩子 事件 that fires 当 the turn ends 由于 an API 错误 (速率限制, 认证 失败, etc.)
- 新增 `${CLAUDE_PLUGIN_DATA}` 变量 用于 插件 persistent state that survives 插件 updates; `/插件 卸载` prompts 之前 deleting it
- 新增 `effort`, `maxTurns`, 和 `disallowedTools` frontmatter support 用于 插件-shipped 代理
- 终端 通知 (iTerm2/Kitty/Ghostty popups, progress bar) 现在 reach the outer 终端 当 运行中 inside tmux 与 `集合 -g 允许-passthrough on`
- 响应 文本 现在 streams line-by-line as it's 已生成
- 修复 `git 日志 HEAD` failing 与 "ambiguous 参数" inside 沙盒化 Bash on Linux, 和 stub 文件 polluting `git status` in the working 目录
- 修复 `cc 日志` 和 `--恢复` silently truncating conversation history on large 会话 (>5 MB) that used 子代理
- 修复 infinite loop 当 API 错误 triggered 停止 钩子 that re-fed blocking 错误 to the 模型
- 修复 `拒绝: ["mcp__servername"]` 权限 rules not removing MCP 服务器 工具 之前 sending to the 模型, allowing it to see 和 attempt blocked 工具
- 修复 `沙盒.filesystem.allowWrite` not working 与 absolute 路径 (previously required `//` 前缀)
- 修复 `/沙盒` Dependencies 标签页 showing Linux 前提条件 on macOS 而不是 macOS-specific info
- **安全:** 修复 silent 沙盒 禁用 当 `沙盒.已启用: true` is 集合 but dependencies are 缺失 — 现在 shows a visible 启动 警告
- 修复 `.git`, `.Claude`, 和 other protected directories being writable 无 a 提示 in `bypassPermissions` mode
- 修复 ctrl+u in normal mode 滚动 而不是 readline 终止-line (ctrl+u/ctrl+d half-page 滚动 moved to 转录 mode only)
- 修复 语音 mode modifier-combo 推送-to-talk keybindings (e.g. ctrl+k) requiring a hold 而不是 activating immediately
- 修复 语音 mode not working on WSL2 与 WSLg (Windows 11); WSL1/Win10 用户 现在 get a 清除 错误
- 修复 `--工作树` 标志 not loading skills 和 钩子 从 the 工作树 目录
- 修复 `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` 和 `includeGitInstructions` 设置 not suppressing the git status 部分 in the 系统 提示
- 修复 Bash 工具 not finding Homebrew 和 other 路径-dependent binaries 当 VS 代码 is launched 从 Dock/Spotlight
- 修复 washed-out Claude orange color in VS 代码/光标/代码-服务器 terminals that don't advertise truecolor support
- 新增 `ANTHROPIC_CUSTOM_MODEL_OPTION` 环境变量 var to 添加 a 自定义 条目 to the `/模型` picker, 与 optional `_NAME` 和 `_DESCRIPTION` suffixed vars 用于 显示
- 修复 `ANTHROPIC_BETAS` 环境 变量 being silently ignored 当 使用 Haiku 模型
- 修复 queued prompts being concatenated 无 a newline separator
- 改进 内存 usage 和 启动 time 当 resuming large 会话
- [VSCode] 修复 a brief flash of the login 屏幕 当 opening the sidebar 当 already authenticated
- [VSCode] 修复 "API 错误: 速率限制 reached" 当 selecting Opus — 模型 dropdown 不再 offers 1M 上下文 变体 to subscribers whose plan 层级 is unknown

## 2.1.77

- Increased 默认 maximum 输出 令牌 限制 用于 Claude Opus 4.6 to 64k 令牌, 和 the upper bound 用于 Opus 4.6 和 Sonnet 4.6 模型 to 128k 令牌
- 新增 `allowRead` 沙盒 filesystem 设置 to re-允许 读取 访问 within `denyRead` regions
- `/复制` 现在 accepts an optional 索引: `/复制 N` copies the Nth-最新 assistant 响应
- 修复 "Always 允许" on compound bash 命令 (e.g. `cd src && npm 测试`) saving a single rule 用于 the full 字符串 而不是 per-subcommand, leading to dead rules 和 repeated 权限 prompts
- 修复 auto-updater starting overlapping 二进制 downloads 当 the slash-命令 overlay repeatedly opened 和 closed, accumulating tens of gigabytes of 内存
- 修复 `--恢复` silently truncating recent conversation history 由于 a race between 内存-extraction writes 和 the main 转录
- 修复 PreToolUse 钩子 returning `"允许"` bypassing `拒绝` 权限 rules, 包括 企业 managed 设置
- 修复 写入 工具 silently converting line endings 当 overwriting CRLF 文件 或 creating 文件 in CRLF directories
- 修复 内存 growth in long-运行中 会话 从 progress 消息 surviving compaction
- 修复 cost 和 令牌 usage not being tracked 当 the API falls back to non-流式 mode
- 修复 `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` not stripping 测试版 工具-schema fields, causing 代理 gateways to reject 请求
- 修复 Bash 工具 reporting 错误 用于 成功 命令 当 the 系统 temp 目录 路径 contains spaces
- 修复 粘贴 being lost 当 typing immediately 之后 pasting
- 修复 Ctrl+D in `/feedback` 文本 输入 deleting 转发 而不是 the 秒 press exiting the 会话
- 修复 API 错误 当 dragging a 0-byte image 文件 进入 the 提示
- 修复 Claude Desktop 会话 incorrectly 使用 the 终端 CLI's configured API 键 而不是 OAuth
- 修复 `git-subdir` 插件 at different subdirectories of the same monorepo 提交 colliding in the 插件 缓存
- 修复 ordered 列表 numbers not 渲染 in 终端 UI
- 修复 a race 条件 where stale-工作树 清理 could 删除 an 代理 工作树 just resumed 从 a 上一个 崩溃
- 修复 输入 deadlock 当 opening `/MCP` 或 similar dialogs 当 the 代理 is 运行中
- 修复 Backspace 和 删除 键 not working in vim NORMAL mode
- 修复 status line not updating 当 vim mode is toggled on 或 off
- 修复 hyperlinks opening twice on Cmd+click in VS 代码, 光标, 和 other xterm.js-基于 terminals
- 修复 background colors 渲染 as 终端-默认 inside tmux 与 默认 配置
- 修复 iTerm2 会话 崩溃 当 selecting 文本 inside tmux over SSH
- 修复 剪贴板 复制 silently failing in tmux 会话; 复制 toast 现在 indicates whether to 粘贴 与 `⌘V` 或 tmux `前缀+]`
- 修复 `←`/`→` accidentally switching 标签页 in 设置, 权限, 和 沙盒 dialogs 当 navigating lists
- 修复 IDE 集成 not auto-connecting 当 Claude 代码 is launched inside tmux 或 屏幕
- 修复 CJK characters visually bleeding 进入 adjacent UI 元素 当 clipped at the right 边
- 修复 teammate panes not closing 当 the leader exits
- 修复 iTerm2 自动模式 not detecting iTerm2 用于 原生 分割-pane teammates
- 更快 启动 on macOS (~60ms) by reading keychain credentials in 并行 与 模块 loading
- 更快 `--恢复` on 分叉-heavy 和 very large 会话 — up to 45% 更快 loading 和 ~100-150MB less peak 内存
- 改进 Esc to 中止 in-flight non-流式 API 请求
- 改进 `Claude 插件 验证` to check skill, 代理, 和 命令 frontmatter plus `钩子/钩子.JSON`, catching YAML 解析 错误 和 schema violations
- Background bash 任务 are 现在 killed if 输出 exceeds 5GB, preventing runaway 流程 从 filling disk
- 会话 are 现在 auto-named 从 plan content 当 you accept a plan
- 改进 headless mode 插件 安装 to compose correctly 与 `CLAUDE_CODE_PLUGIN_SEED_DIR`
- 显示 a notice 当 `apiKeyHelper` takes longer 比 10s, preventing it 从 blocking the main loop
- The 代理 工具 不再 accepts a `恢复` 参数 — use `SendMessage({to: agentId})` to 继续 a previously spawned 代理
- `SendMessage` 现在 auto-resumes 已停止 代理 in the background 而不是 returning an 错误
- Renamed `/分叉` to `/分支` (`/分叉` still works as an alias)
- [VSCode] 改进 plan 预览 标签页 titles to use the plan's heading 而不是 "Claude's Plan"
- [VSCode] 当 选项+click doesn't 触发 原生 selection on macOS, the footer 现在 points to the `macOptionClickForcesSelection` 设置

## 2.1.76

- 新增 MCP elicitation support — MCP 服务器 can 现在 请求 structured 输入 mid-任务 通过 an interactive 对话框 (form fields 或 browser URL)
- 新增 新 `Elicitation` 和 `ElicitationResult` 钩子 to intercept 和 覆盖 响应 之前 they're sent back
- 新增 `-n` / `--name <name>` CLI 标志 to 集合 a 显示 name 用于 the 会话 at 启动
- 新增 `工作树.sparsePaths` 设置 用于 `Claude --工作树` in large monorepos to check out only the directories you need 通过 git sparse-checkout
- 新增 `PostCompact` 钩子 that fires 之后 compaction completes
- 新增 `/effort` slash 命令 to 集合 模型 effort 级别
- 新增 会话 quality survey — 企业 admins can 配置 the sample rate 通过 the `feedbackSurveyRate` 设置
- 修复 deferred 工具 (loaded 通过 `ToolSearch`) losing their 输入 schemas 之后 conversation compaction, causing 数组 和 数字 parameters to be rejected 与 类型 错误
- 修复 slash 命令 showing "Unknown skill"
- 修复 计划模式 asking 用于 re-approval 之后 the plan was already accepted
- 修复 语音 mode swallowing keypresses 当 a 权限 对话框 或 plan editor was 打开
- 修复 `/语音` not working on Windows 当 installed 通过 npm
- 修复 spurious "上下文 限制 reached" 当 invoking a skill 与 `模型:` frontmatter on a 1M-上下文 会话
- 修复 "adaptive thinking is not 支持 on this 模型" 错误 当 使用 non-standard 模型 strings
- 修复 `Bash(cmd:*)` 权限 rules not matching 当 a quoted 参数 contains `#`
- 修复 "don't ask again" in the Bash 权限 对话框 showing the full 原始 命令 用于 pipes 和 compound 命令
- 修复 auto-compaction retrying indefinitely 之后 consecutive 失败 — a circuit breaker 现在 stops 之后 3 attempts
- 修复 MCP 重新连接 加载动画 persisting 之后 成功 reconnection
- 修复 LSP 插件 not registering 服务器 当 the LSP Manager initialized 之前 marketplaces were reconciled
- 修复 剪贴板 copying in tmux over SSH — 现在 attempts both direct 终端 写入 和 tmux 剪贴板 集成
- 修复 `/export` showing only the filename 而不是 the full 文件 路径 in the 成功 消息
- 修复 转录 not auto-滚动 to 新 消息 之后 selecting 文本
- 修复 转义 键 not working to 退出 the login 方法 selection 屏幕
- 修复 several 远程 Control 问题: 会话 silently dying 当 the 服务器 reaps an idle 环境, rapid 消息 being queued one-at-a-time 而不是 batched, 和 stale work 项 causing redelivery 之后 JWT 刷新
- 修复 bridge 会话 failing to recover 之后 extended WebSocket disconnects
- 修复 slash 命令 not found 当 typing the exact name of a soft-hidden 命令
- 改进 `--工作树` 启动 性能 by reading git refs directly 和 skipping redundant `git fetch` 当 the 远程 分支 is already 可用 locally
- 改进 background 代理 behavior — killing a background 代理 现在 preserves its partial results in the conversation 上下文
- 改进 模型 回退 通知 — 现在 always visible 而不是 hidden behind verbose mode, 与 human-friendly 模型 names
- 改进 blockquote readability on dark 终端 themes — 文本 is 现在 italic 与 a left bar 而不是 dim
- 改进 stale 工作树 清理 — 工作树 left behind 之后 an interrupted 并行 run are 现在 automatically cleaned up
- 改进 远程 Control 会话 titles — 现在 derived 从 your 第一 提示 而不是 showing "Interactive 会话"
- 改进 `/语音` to 显示 your 听写 language on 启用 和 warn 当 your `language` 设置 isn't 支持 用于 语音 输入
- Updated `--插件-dir` to only accept one 路径 to support subcommands — use repeated `--插件-dir` 用于 multiple directories
- [VSCode] 修复 gitignore 模式 containing commas silently 排除 entire filetypes 从 the @-mention 文件 picker

## 2.1.75

- 新增 1M 上下文窗口 用于 Opus 4.6 by 默认 用于 Max, 团队, 和 企业 plans (previously required extra usage)
- 新增 `/color` 命令 用于 all 用户 to 集合 a 提示-bar color 用于 your 会话
- 新增 会话 name 显示 on the 提示 bar 当 使用 `/rename`
- 新增 最后-modified timestamps to 内存 文件, helping Claude reason about which memories are fresh vs. stale
- 新增 钩子 源 显示 (设置/插件/skill) in 权限 prompts 当 a 钩子 requires confirmation
- 修复 语音 mode not activating correctly on fresh installs 无 toggling `/语音` twice
- 修复 the Claude 代码 头信息 not updating the displayed 模型 name 之后 switching 模型 与 `/模型` 或 选项+P
- 修复 会话 崩溃 当 an attachment 消息 computation returns undefined 值
- 修复 Bash 工具 mangling `!` in piped 命令 (e.g., `jq 'select(.x != .y)'` 现在 works correctly)
- 修复 managed-已禁用 插件 showing up in the `/插件` Installed 标签页 — 插件 force-已禁用 by your 组织 are 现在 hidden
- 修复 令牌 estimation over-counting 用于 thinking 和 `tool_use` 块, preventing premature 上下文 compaction
- 修复 corrupted marketplace config 路径 handling
- 修复 `/恢复` losing 会话 names 之后 resuming a 已分叉 或 continued 会话
- 修复 Esc not closing the `/status` 对话框 之后 visiting the Config 标签页
- 修复 输入 handling 当 accepting 或 rejecting a plan
- 修复 footer 提示 in 代理 团队 showing "↓ to expand" 而不是 the correct "shift + ↓ to expand"
- 改进 启动 性能 on macOS non-MDM machines by skipping unnecessary subprocess spawns
- Suppressed 异步 钩子 completion 消息 by 默认 (visible 与 `--verbose` 或 转录 mode)
- 破坏性更改: 移除 弃用 Windows managed 设置 回退 at `C:\ProgramData\ClaudeCode\managed-设置.JSON` — use `C:\程序 文件\ClaudeCode\managed-设置.JSON`

## 2.1.74

- 新增 actionable 建议 to `/上下文` 命令 — identifies 上下文-heavy 工具, 内存 bloat, 和 容量 警告 与 specific 优化 技巧
- 新增 `autoMemoryDirectory` 设置 to 配置 a 自定义 目录 用于 auto-内存 storage
- 修复 内存 泄漏 where 流式 API 响应 buffers were not released 当 the generator was terminated 早期, causing unbounded RSS growth on the 节点.js/npm 代码 路径
- 修复 managed policy `ask` rules being bypassed by user `允许` rules 或 skill `允许-工具`
- 修复 full 模型 IDs (e.g., `Claude-Opus-4-5`) being silently ignored in 代理 frontmatter `模型:` 字段 和 `--代理` JSON config — 代理 现在 accept the same 模型 值 as `--模型`
- 修复 MCP OAuth 认证 hanging 当 the 回调 端口 is already in use
- 修复 MCP OAuth 刷新 never prompting 用于 re-认证 之后 the 刷新 令牌 expires, 用于 OAuth 服务器 that return 错误 与 HTTP 200 (e.g. Slack)
- 修复 语音 mode silently failing on the macOS 原生 二进制 用于 用户 whose 终端 had never been granted 麦克风 权限 — the 二进制 现在 includes the `audio-输入` entitlement 所以 macOS prompts correctly
- 修复 `SessionEnd` 钩子 being killed 之后 1.5 s on 退出 regardless of `钩子.超时` — 现在 configurable 通过 `CLAUDE_CODE_SESSIONEND_HOOKS_TIMEOUT_MS`
- 修复 `/插件 安装` failing inside the REPL 用于 marketplace 插件 与 本地 sources
- 修复 marketplace 更新 not syncing git submodules — 插件 sources in submodules 不再 break 之后 更新
- 修复 unknown slash 命令 与 arguments silently dropping 输入 — 现在 shows your 输入 as a 警告
- 修复 Hebrew, Arabic, 和 other RTL 文本 not 渲染 correctly in Windows 终端, conhost, 和 VS 代码 integrated 终端
- 修复 LSP 服务器 not working on Windows 由于 malformed 文件 URIs
- 更改 `--插件-dir` 所以 本地 dev copies 现在 覆盖 installed marketplace 插件 与 the same name (除非 that 插件 is force-已启用 by managed 设置)
- [VSCode] 修复 删除 按钮 not working 用于 Untitled 会话
- [VSCode] 改进 滚动 wheel responsiveness in the integrated 终端 与 终端-aware acceleration

## 2.1.73

- 新增 `modelOverrides` 设置 to 映射 模型 picker 条目 to 自定义 provider 模型 IDs (e.g. Bedrock inference 分析 ARNs)
- 新增 actionable guidance 当 OAuth login 或 connectivity checks 失败 由于 SSL 证书 错误 (corporate proxies, `NODE_EXTRA_CA_CERTS`)
- 修复 freezes 和 100% CPU loops triggered by 权限 prompts 用于 complex bash 命令
- 修复 a deadlock that could freeze Claude 代码 当 many skill 文件 更改 at once (e.g. 期间 `git 拉取` in a 仓库 与 a large `.Claude/skills/` 目录)
- 修复 Bash 工具 输出 being lost 当 运行中 multiple Claude 代码 会话 in the same 项目 目录
- 修复 子代理 与 `模型: Opus`/`Sonnet`/`Haiku` being silently downgraded to older 模型 版本 on Bedrock, Vertex, 和 Microsoft Foundry
- 修复 background bash 流程 spawned by 子代理 not being cleaned up 当 the 代理 exits
- 修复 `/恢复` showing the 当前 会话 in the picker
- 修复 `/ide` crashing 与 `onInstall is not defined` 当 auto-installing the extension
- 修复 `/loop` not being 可用 on Bedrock/Vertex/Foundry 和 当 telemetry was 已禁用
- 修复 SessionStart 钩子 firing twice 当 resuming a 会话 通过 `--恢复` 或 `--继续`
- 修复 JSON-输出 钩子 injecting no-op 系统-reminder 消息 进入 the 模型's 上下文 on every turn
- 修复 语音 mode 会话 corruption 当 a 慢 连接 overlaps a 新 recording
- 修复 Linux 沙盒 failing to 启动 与 "ripgrep (rg) not found" on 原生 builds
- 修复 Linux 原生 modules not loading on Amazon Linux 2 和 other glibc 2.26 systems
- 修复 "media_type: 字段 required" API 错误 当 receiving images 通过 远程 Control
- 修复 `/heapdump` failing on Windows 与 `EEXIST` 错误 当 the Desktop 文件夹 already 存在
- 改进 Up arrow 之后 interrupting Claude — 现在 restores the interrupted 提示 和 rewinds the conversation in one 步骤
- 改进 IDE detection speed at 启动
- 改进 剪贴板 image pasting 性能 on macOS
- 改进 `/effort` to work 当 Claude is responding, matching `/模型` behavior
- 改进 语音 mode to automatically 重试 transient 连接 失败 期间 rapid 推送-to-talk re-press
- 改进 the 远程 Control 生成 mode selection 提示 与 better 上下文
- 更改 默认 Opus 模型 on Bedrock, Vertex, 和 Microsoft Foundry to Opus 4.6 (was Opus 4.1)
- 弃用 `/输出-style` 命令 — use `/config` instead. 输出 style is 现在 修复 at 会话 启动 用于 better 提示 缓存
- VSCode: 修复 HTTP 400 错误 用于 用户 behind proxies 或 on Bedrock/Vertex 与 Claude 4.5 模型

## 2.1.72

- 修复 工具 搜索 to activate even 与 `ANTHROPIC_BASE_URL` 只要 `ENABLE_TOOL_SEARCH` is 集合.
- 新增 `w` 键 in `/复制` to 写入 the focused selection directly to a 文件, bypassing the 剪贴板 (useful over SSH)
- 新增 optional description 参数 to `/plan` (e.g., `/plan 修复 the 认证 缺陷`) that enters 计划模式 和 immediately starts
- 新增 `ExitWorktree` 工具 to leave an `EnterWorktree` 会话
- 新增 `CLAUDE_CODE_DISABLE_CRON` 环境 变量 to immediately 停止 scheduled cron jobs mid-会话
- 新增 `lsof`, `pgrep`, `tput`, `ss`, `fd`, 和 `fdfind` to the bash auto-approval allowlist, reducing 权限 prompts 用于 common 读取-only operations
- Restored the `模型` 参数 on the 代理 工具 用于 per-invocation 模型 overrides
- Simplified effort 级别 to low/medium/high (移除 max) 与 新 symbols (○ ◐ ●) 和 a brief 通知 而不是 a persistent icon. Use `/effort auto` to reset to 默认
- 改进 `/config` — 转义 现在 cancels 更改, Enter saves 和 closes, Space toggles 设置
- 改进 up-arrow history to 显示 当前 会话's 消息 第一 当 运行中 multiple 并发 会话
- 改进 语音 输入 transcription accuracy 用于 仓库 names 和 common dev terms (regex, OAuth, JSON)
- 改进 bash 命令 解析中 by switching to a 原生 模块 — 更快 initialization 和 no 内存 泄漏
- Reduced 打包 size by ~510 KB
- 更改 Claude.md HTML comments (`<!-- ... -->`) to be hidden 从 Claude 当 auto-injected. Comments remain visible 当 读取 与 the 读取 工具
- 修复 慢 exits 当 background 任务 或 钩子 were 慢 to respond
- 修复 代理 任务 progress stuck on "Initializing…"
- 修复 skill 钩子 firing twice per 事件 当 a 钩子-已启用 skill is invoked by the 模型
- 修复 several 语音 mode 问题: occasional 输入 lag, false "No 语音 detected" 错误 之后 releasing 推送-to-talk, 和 stale transcripts re-filling the 提示 之后 submission
- 修复 `--继续` not resuming 从 the most recent point 之后 `--压缩`
- 修复 bash 安全 解析中 边 cases
- 新增 support 用于 marketplace git URLs 无 `.git` 后缀 (Azure DevOps, AWS CodeCommit)
- 改进 marketplace 克隆 失败 消息 to 显示 diagnostic info even 当 git produces no stderr
- 修复 several 插件 问题: 安装 failing on Windows 与 `EEXIST` 错误 in OneDrive folders, marketplace blocking user-作用域 installs 当 a 项目-作用域 安装 存在, `CLAUDE_CODE_PLUGIN_CACHE_DIR` creating literal `~` directories, 和 `插件.JSON` 与 marketplace-only fields failing to 加载
- 修复 feedback survey appearing too frequently in long 会话
- 修复 `--effort` CLI 标志 being reset by unrelated 设置 writes on 启动
- 修复 backgrounded Ctrl+B queries losing their 转录 或 corrupting the 新 conversation 之后 `/清除`
- 修复 `/清除` killing background 代理/bash 任务 — only foreground 任务 are 现在 cleared
- 修复 工作树 isolation 问题: 任务 工具 恢复 not restoring cwd, 和 background 任务 通知 缺失 `worktreePath` 和 `worktreeBranch`
- 修复 `/模型` not displaying results 当 run 当 Claude is working
- 修复 digit 键 selecting 菜单 选项 而不是 typing in 计划模式 权限 提示's 文本 输入
- 修复 沙盒 权限 问题: certain 文件 写入 operations incorrectly 允许 无 prompting, 和 输出 redirections to allowlisted directories (like `/tmp/Claude/`) prompting unnecessarily
- 改进 CPU utilization in long 会话
- 修复 提示 缓存 invalidation in SDK `查询()` calls, reducing 输入 令牌 costs up to 12x
- 修复 转义 键 becoming unresponsive 之后 cancelling a 查询
- 修复 double Ctrl+C not exiting 当 background 代理 或 任务 are 运行中
- 修复 团队 代理 to inherit the leader's 模型
- 修复 "Always 允许" saving 权限 rules that never 匹配 again
- 修复 several 钩子 问题: `transcript_path` pointing to the wrong 目录 用于 resumed/已分叉 会话, 代理 `提示` being silently deleted 从 设置.JSON on every 设置 写入, PostToolUse 块 reason displaying twice, 异步 钩子 not receiving stdin 与 bash `读取 -r`, 和 validation 错误 消息 showing an 示例 that fails validation
- 修复 会话 崩溃 in Desktop/SDK 当 读取 returned 文件 containing U+2028/U+2029 characters
- 修复 终端 title being cleared on 退出 even 当 `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` was 集合
- 修复 several 权限 rule matching 问题: wildcard rules not matching 命令 与 heredocs, embedded newlines, 或 no arguments; `沙盒.excludedCommands` failing 与 环境变量 var prefixes; "always 允许" suggesting overly broad prefixes 用于 nested CLI 工具; 和 拒绝 rules not applying to all 命令 forms
- 修复 oversized 和 truncated images 从 Bash data-URL 输出
- 修复 a 崩溃 当 resuming 会话 that contained Bedrock API 错误
- 修复 intermittent "expected 布尔值, received 字符串" validation 错误 on 编辑, Bash, 和 Grep 工具 inputs
- 修复 multi-line 会话 titles 当 forking 从 a conversation whose 第一 消息 contained newlines
- 修复 queued 消息 not showing attached images, 和 images being lost 当 pressing ↑ to 编辑 a queued 消息
- 修复 并行 工具 calls where a 失败 读取/WebFetch/Glob would 取消 its siblings — only Bash 错误 现在 cascade
- VSCode: 修复 滚动 speed in integrated terminals not matching 原生 terminals
- VSCode: 修复 Shift+Enter submitting 输入 而不是 inserting a newline 用于 用户 与 older keybindings
- VSCode: 新增 effort 级别 indicator on the 输入 border
- VSCode: 新增 `VSCode://Anthropic.Claude-代码/打开` URI 处理器 to 打开 a 新 Claude 代码 标签页 programmatically, 与 optional `提示` 和 `会话` 查询 parameters

## 2.1.71

- 新增 `/loop` 命令 to run a 提示 或 slash 命令 on a recurring interval (e.g. `/loop 5m check the 部署`)
- 新增 cron scheduling 工具 用于 recurring prompts within a 会话
- 新增 `语音:pushToTalk` keybinding to make the 语音 activation 键 rebindable in `keybindings.JSON` (默认: space) — modifier+letter combos like `meta+k` have zero typing interference
- 新增 `fmt`, `comm`, `cmp`, `numfmt`, `expr`, `测试`, `printf`, `getconf`, `seq`, `tsort`, 和 `PR` to the bash auto-approval allowlist
- 修复 stdin freeze in long-运行中 会话 where keystrokes 停止 being processed but the 流程 stays alive
- 修复 a 5–8 秒 启动 freeze 用于 用户 与 语音 mode 已启用, caused by CoreAudio initialization blocking the main 线程 之后 系统 wake
- 修复 启动 UI freeze 当 many Claude.ai 代理 connectors 刷新 an expired OAuth 令牌 simultaneously
- 修复 已分叉 conversations (`/分叉`) sharing the same plan 文件, which caused plan edits in one 分叉 to overwrite the other
- 修复 the 读取 工具 putting oversized images 进入 上下文 当 image processing 失败, breaking subsequent turns in long image-heavy 会话
- 修复 false-positive 权限 prompts 用于 compound bash 命令 containing heredoc 提交 消息
- 修复 插件 installations being lost 当 运行中 multiple Claude 代码 instances
- 修复 Claude.ai connectors failing to 重新连接 之后 OAuth 令牌 刷新
- 修复 Claude.ai MCP connector 启动 通知 appearing 用于 every 组织-configured connector 而不是 only previously connected ones
- 修复 background 代理 completion 通知 缺失 the 输出 文件 路径, which made it difficult 用于 parent 代理 to recover 代理 results 之后 上下文 compaction
- 修复 复制 输出 in Bash 工具 错误 消息 当 命令 退出 与 non-zero status
- 修复 Chrome extension auto-detection getting permanently stuck on "not installed" 之后 运行中 on a machine 无 本地 Chrome
- 修复 `/插件 marketplace 更新` failing 与 合并 conflicts 当 the marketplace is pinned to a 分支/tag ref
- 修复 `/插件 marketplace 添加 owner/仓库@ref` incorrectly 解析中 `@` — previously only `#` worked as a ref separator, causing undiagnosable 错误 与 `strictKnownMarketplaces`
- 修复 复制 条目 in `/权限` 工作区 标签页 当 the same 目录 is 新增 与 和 无 a trailing slash
- 修复 `--print` hanging forever 当 团队 代理 are configured — the 退出 loop 不再 waits on long-lived `in_process_teammate` 任务
- 修复 "❯ 工具 loaded." appearing in the REPL 之后 every `ToolSearch` call
- 修复 prompting 用于 `cd <cwd> && git ...` on Windows 当 the 模型 uses a mingw-style 路径
- 改进 启动 time by deferring 原生 image processor loading to 第一 use
- 改进 bridge 会话 reconnection to 完成 within 秒 之后 laptop wake 从 sleep, 而不是 waiting up to 10 分钟
- 改进 `/插件 卸载` to 禁用 项目-scoped 插件 in `.Claude/设置.本地.JSON` 而不是 modifying `.Claude/设置.JSON`, 所以 更改 don't affect teammates
- 改进 插件-provided MCP 服务器 deduplication — 服务器 that 复制 a manually-configured 服务器 (same 命令/URL) are 现在 skipped, preventing 复制 连接 和 工具 sets. Suppressions are shown in the `/插件` 菜单.
- Updated `/调试` to toggle 调试 日志 on mid-会话, 自从 调试 日志 are 不再 written by 默认
- 移除 启动 通知 noise 用于 unauthenticated 组织-registered Claude.ai connectors

## 2.1.70

- 修复 API 400 错误 当 使用 `ANTHROPIC_BASE_URL` 与 a third-party gateway — 工具 搜索 现在 correctly detects 代理 endpoints 和 disables `tool_reference` 块
- 修复 `API 错误: 400 This 模型 does not support the effort 参数` 当 使用 自定义 Bedrock inference profiles 或 other 模型 identifiers not matching standard Claude naming 模式
- 修复 空 模型 响应 immediately 之后 `ToolSearch` — the 服务器 renders 工具 schemas 与 系统-提示-style tags at the 提示 tail, which could confuse 模型 进入 stopping 早期
- 修复 提示-缓存 bust 当 an MCP 服务器 与 `instructions` connects 之后 the 第一 turn
- 修复 Enter inserting a newline 而不是 submitting 当 typing over a 慢 SSH 连接
- 修复 剪贴板 corrupting non-ASCII 文本 (CJK, emoji) on Windows/WSL by 使用 PowerShell `集合-剪贴板`
- 修复 extra VS 代码 Windows opening at 启动 on Windows 当 运行中 从 the VS 代码 integrated 终端
- 修复 语音 mode failing on Windows 原生 二进制 与 "原生 audio 模块 could not be loaded"
- 修复 推送-to-talk not activating on 会话 启动 当 `voiceEnabled: true` was 集合 in 设置
- 修复 markdown links containing `#NNN` references incorrectly pointing to the 当前 仓库 而不是 the linked URL
- 修复 repeated "模型 updated to Opus 4.6" 通知 当 a 项目's `.Claude/设置.JSON` has a legacy Opus 模型 字符串 pinned
- 修复 插件 showing as inaccurately installed in `/插件`
- 修复 插件 showing "not found in marketplace" 错误 on fresh 启动 by auto-refreshing 之后 marketplace 安装
- 修复 `/安全-review` 命令 failing 与 `unknown 选项 合并-base` on older git 版本
- 修复 `/color` 命令 having no way to reset back to the 默认 color — `/color 默认`, `/color gray`, `/color reset`, 和 `/color none` 现在 恢复 the 默认
- 修复 a 性能 回归 in the `AskUserQuestion` 预览 对话框 that re-ran markdown 渲染 on every keystroke in the 备注 输入
- 修复 功能 标志 读取 期间 早期 启动 never refreshing their disk 缓存, causing stale 值 to 持久化 across 会话
- 修复 `权限.defaultMode` 设置 值 other 比 `acceptEdits` 或 `plan` being applied in Claude 代码 远程 environments — they are 现在 ignored
- 修复 skill listing being re-injected on every `--恢复` (~600 令牌 saved per 恢复)
- 修复 teleport marker not 渲染 in VS 代码 teleported 会话
- 改进 错误 消息 当 麦克风 captures silence to distinguish 从 "no 语音 detected"
- 改进 compaction to preserve images in the summarizer 请求, allowing 提示 缓存 reuse 用于 更快 和 cheaper compaction
- 改进 `/rename` to work 当 Claude is processing, 而不是 being silently queued
- Reduced 提示 输入 re-renders 期间 turns by ~74%
- Reduced 启动 内存 by ~426KB 用于 用户 无 自定义 CA certificates
- Reduced 远程 Control `/poll` rate to once per 10 分钟 当 connected (was 1–2s), cutting 服务器 加载 ~300×. Reconnection is unaffected — transport loss immediately wakes 快速 polling.
- [VSCode] 新增 spark icon in VS 代码 activity bar that lists all Claude 代码 会话, 与 会话 opening as full editors
- [VSCode] 新增 full markdown document 视图 用于 plans in VS 代码, 与 support 用于 adding comments to provide feedback
- [VSCode] 新增 原生 MCP 服务器 management 对话框 — use `/MCP` in the chat 面板 to 启用/禁用 服务器, 重新连接, 和 manage OAuth 认证 无 switching to the 终端

## 2.1.69

- 新增 the `/Claude-API` skill 用于 building 应用程序 与 the Claude API 和 Anthropic SDK
- 新增 Ctrl+U on an 空 bash 提示 (`!`) to 退出 bash mode, matching `转义` 和 `backspace`
- 新增 numeric keypad support 用于 selecting 选项 in Claude's interview questions (previously only the 数字 行 above QWERTY worked)
- 新增 optional name 参数 to `/远程-control` 和 `Claude 远程-control` (`/远程-control My 项目` 或 `--name "My 项目"`) to 集合 a 自定义 会话 title visible in Claude.ai/代码
- 新增 语音 STT support 用于 10 新 languages (20 total) — Russian, Polish, Turkish, Dutch, Ukrainian, Greek, Czech, Danish, Swedish, Norwegian
- 新增 effort 级别 显示 (e.g., "与 low effort") to the logo 和 加载动画, making it easier to see which effort 设置 is 活动
- 新增 代理 name 显示 in 终端 title 当 使用 `Claude --代理`
- 新增 `沙盒.enableWeakerNetworkIsolation` 设置 (macOS only) to 允许 Go 程序 like `gh`, `gcloud`, 和 `terraform` to 验证 TLS certificates 当 使用 a 自定义 MITM 代理 与 `httpProxyPort`
- 新增 `includeGitInstructions` 设置 (和 `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` 环境变量 var) to 移除 内置 提交 和 PR 工作流 instructions 从 Claude's 系统 提示
- 新增 `/重新加载-插件` 命令 to activate 待处理 插件 更改 无 restarting
- 新增 a one-time 启动 提示 suggesting Claude 代码 Desktop on macOS 和 Windows (max 3 showings, dismissible)
- 新增 `${CLAUDE_SKILL_DIR}` 变量 用于 skills to 引用 their own 目录 in SKILL.md content
- 新增 `InstructionsLoaded` 钩子 事件 that fires 当 Claude.md 或 `.Claude/rules/*.md` 文件 are loaded 进入 上下文
- 新增 `agent_id` (用于 子代理) 和 `agent_type` (用于 子代理 和 `--代理`) to 钩子 事件
- 新增 `工作树` 字段 to status line 钩子 命令 与 name, 路径, 分支, 和 original 仓库 目录 当 运行中 in a `--工作树` 会话
- 新增 `pluginTrustMessage` in managed 设置 to 追加 组织-specific 上下文 to the 插件 trust 警告 shown 之前 安装
- 新增 policy 限制 fetching (e.g., 远程 control restrictions) 用于 团队 plan OAuth 用户, not just 企业
- 新增 `pathPattern` to `strictKnownMarketplaces` 用于 regex-matching 文件/目录 marketplace sources alongside `hostPattern` restrictions
- 新增 插件 源 类型 `git-subdir` to point to a subdirectory within a git 仓库
- 新增 `OAuth.authServerMetadataUrl` config 选项 用于 MCP 服务器 to specify a 自定义 OAuth 元数据 discovery URL 当 standard discovery fails
- 修复 a 安全 问题 where nested skill discovery could 加载 skills 从 gitignored directories like `node_modules`
- 修复 trust 对话框 silently enabling all `.MCP.JSON` 服务器 on 第一 run. You'll 现在 see the per-服务器 approval 对话框 as expected
- 修复 `Claude 远程-control` crashing immediately on npm installs 与 "bad 选项: --sdk-URL" (anthropics/Claude-代码#28334)
- 修复 `--模型 Claude-Opus-4-0` 和 `--模型 Claude-Opus-4-1` resolving to 弃用 Opus 版本 而不是 当前
- 修复 macOS keychain corruption 当 使用 multiple OAuth MCP 服务器. Large OAuth 元数据 blobs could overflow the `安全 -i` stdin 缓冲区, silently leaving stale credentials behind 和 causing repeated `/login` prompts.
- 修复 `.credentials.JSON` losing `subscriptionType` (showing "Claude API" 而不是 "Claude Pro"/"Claude Max") 当 the 分析 端点 transiently fails 期间 令牌 刷新 (anthropics/Claude-代码#30185)
- 修复 ghost dotfiles (`.bashrc`, `HEAD`, etc.) appearing as untracked 文件 in the working 目录 之后 沙盒化 Bash 命令 on Linux
- 修复 Shift+Enter printing `[27;2;13~` 而不是 inserting a newline in Ghostty over SSH
- 修复 stash (Ctrl+S) being cleared 当 submitting a 消息 当 Claude is working
- 修复 ctrl+o (转录 toggle) freezing 用于 many 秒 in long 会话 与 lots of 文件 edits
- 修复 计划模式 feedback 输入 not supporting multi-line 文本 条目 (backslash+Enter 和 Shift+Enter 现在 插入 newlines)
- 修复 光标 not moving down 进入 空白 lines at the top of the 输入 box
- 修复 `/stats` 崩溃 当 转录 文件 contain 条目 与 缺失 或 malformed timestamps
- 修复 a brief hang 之后 a 流式 错误 on long 会话 (the 转录 was being fully rewritten to drop one line; it is 现在 truncated in place)
- 修复 `--设置-sources user` not blocking dynamically discovered 项目 skills
- 修复 复制 Claude.md, slash 命令, 代理, 和 rules 当 运行中 从 a 工作树 nested inside its main 仓库 (e.g. `Claude -w`)
- 修复 插件 停止/SessionEnd/etc 钩子 not firing 之后 any `/插件` operation
- 修复 插件 钩子 being silently dropped 当 two 插件 use the same `${CLAUDE_PLUGIN_ROOT}/...` 命令 模板
- 修复 内存 泄漏 in long-运行中 SDK/CCR 会话 where conversation 消息 were retained unnecessarily
- 修复 API 400 错误 in 已分叉 代理 (autocompact, summarization) 当 resuming 会话 that were interrupted mid-工具-批
- 修复 "unexpected tool_use_id found in tool_result 块" 错误 当 resuming conversations that 启动 与 an orphaned 工具 result
- 修复 teammates accidentally spawning nested teammates 通过 the 代理 工具's `name` 参数
- 修复 `CLAUDE_CODE_MAX_OUTPUT_TOKENS` being ignored 期间 conversation compaction
- 修复 `/压缩` summary 渲染 as a user bubble in SDK consumers (Claude 代码 远程 web UI, VSCode extension)
- 修复 语音 space bar getting stuck 之后 a 失败 语音 activation (模块 loading race, cold GrowthBook)
- 修复 工作树 文件 复制 on Windows
- 修复 全局 `.Claude` 文件夹 detection on Windows
- 修复 symlink 绕过 where writing 新 文件 through a symlinked parent 目录 could 转义 the working 目录 in `acceptEdits` mode
- 修复 沙盒 prompting 用户 to approve non-允许 domains 当 `allowManagedDomainsOnly` is 已启用 in managed 设置 — non-允许 domains are 现在 blocked automatically 与 no 绕过
- 修复 interactive 工具 (e.g., `AskUserQuestion`) being silently auto-允许 当 listed in a skill's 允许-工具, bypassing the 权限 提示 和 运行中 与 空 answers
- 修复 multi-GB 内存 spike 当 committing 与 large untracked 二进制 文件 in the working 树
- 修复 转义 not interrupting a 运行中 turn 当 the 输入 box has draft 文本. Use Up arrow to 拉取 queued 消息 back 用于 editing, 或 Ctrl+U to 清除 the 输入 line.
- 修复 Android 应用 崩溃 当 运行中 本地 slash 命令 (`/语音`, `/cost`) in 远程 Control 会话
- 修复 a 内存 泄漏 where 旧 消息 数组 版本 accumulated in React Compiler `memoCache` over long 会话
- 修复 a 内存 泄漏 where REPL 渲染 scopes accumulated over long 会话 (~35MB over 1000 turns)
- 修复 内存 retention in in-流程 teammates where the parent's full conversation history was pinned 用于 the teammate's lifetime, preventing GC 之后 `/清除` 或 auto-压缩
- 修复 a 内存 泄漏 in interactive mode where 钩子 事件 could accumulate unboundedly 期间 long 会话
- 修复 hang 当 `--MCP-config` points to a corrupted 文件
- 修复 慢 启动 当 many skills/插件 are installed
- 修复 `cd <outside-dir> && <cmd>` 权限 提示 to surface the chained 命令 而不是 only showing "Yes, 允许 reading 从 <dir>/"
- 修复 conditional `.Claude/rules/*.md` 文件 (与 `路径:` frontmatter) 和 nested Claude.md 文件 not loading in print mode (`Claude -p`)
- 修复 `/清除` not fully clearing all 会话 caches, reducing 内存 retention in long 会话
- 修复 终端 flicker caused by animated 元素 at the scrollback 边界
- 修复 UI frame drops on macOS 当 使用 MCP 服务器 与 OAuth (回归 从 2.1.x)
- 修复 occasional frame stalls 期间 typing caused by synchronous 调试 日志 flushes
- 修复 `TeammateIdle` 和 `TaskCompleted` 钩子 to support `{"继续": false, "stopReason": "..."}` to 停止 the teammate, matching `停止` 钩子 behavior
- 修复 `WorktreeCreate` 和 `WorktreeRemove` 插件 钩子 being silently ignored
- 修复 skill descriptions 与 colons (e.g., "Triggers include: X, Y, Z") failing to 加载 从 SKILL.md frontmatter
- 修复 项目 skills 无 a `description:` frontmatter 字段 not appearing in Claude's 可用 skills 列表
- 修复 `/上下文` showing identical 令牌 counts 用于 all MCP 工具 从 a 服务器
- 修复 literal `nul` 文件 creation on Windows 当 the 模型 uses CMD-style `2>nul` redirection in git Bash
- 修复 extra 空白 lines appearing below each 工具 call in the expanded 子代理 转录 视图 (Ctrl+O)
- 修复 标签页/arrow 键 not cycling 设置 标签页 当 `/config` 搜索 box is focused but 空
- 修复 服务 键 OAuth 会话 (CCR containers) spamming `[错误]` 日志 与 403s 从 分析-scoped endpoints
- 修复 inconsistent color 用于 "远程 Control 活动" status indicator
- 修复 语音 waveform 光标 covering the 第一 后缀 letter 当 dictating mid-输入
- 修复 语音 输入 showing all 5 spaces 期间 warmup 而不是 capping at ~2 (aligning 与 the "keep holding…" 提示)
- 改进 加载动画 性能 by isolating the 50ms animation loop 从 the surrounding shell, reducing 渲染 和 CPU 开销 期间 turns
- 改进 UI 渲染 性能 in 原生 binaries 与 React Compiler
- 改进 `--工作树` 启动 by eliminating a git subprocess on the 启动 路径
- 改进 macOS 启动 by eliminating redundant 设置-文件 reloads 当 managed 设置 resolve
- 改进 macOS 启动 用于 Claude.ai 企业/团队 用户 by skipping an unnecessary keychain 查找
- 改进 MCP `-p` 启动 by pipelining Claude.ai config fetch 与 本地 连接 和 使用 a concurrency 池 而不是 顺序 batching
- 改进 语音 启动 by removing imperceptible warmup pulse animations that were causing re-渲染 stutter
- 改进 MCP 二进制 content handling: 工具 returning PDFs, Office documents, 或 audio 现在 保存 decoded bytes to disk 与 the correct 文件 extension 而不是 dumping 原始 base64 进入 the conversation 上下文. WebFetch also saves 二进制 响应 alongside its summary.
- 改进 内存 usage in long 会话 by stabilizing `onSubmit` across 消息 updates
- 改进 LSP 工具 渲染 和 内存 上下文 building to 不再 读取 entire 文件
- 改进 会话 上传 和 内存 同步 to avoid reading large 文件 进入 内存 之前 size/二进制 checks
- 改进 文件 operation 性能 by avoiding reading 文件 contents 用于 existence checks (6 sites)
- 改进 文档 to clarify that `--追加-系统-提示-文件` 和 `--系统-提示-文件` work in interactive mode (the 文档 previously said print mode only)
- Reduced baseline 内存 by ~16MB by deferring Yoga WASM preloading
- Reduced 内存 占用空间 用于 SDK 和 CCR 会话 使用 流-JSON 输出
- Reduced 内存 usage 当 resuming large 会话 (包括 compacted history)
- Reduced 令牌 usage on multi-代理 任务 与 more concise 子代理 最终 reports
- 更改 Sonnet 4.5 用户 on Pro/Max/团队 Premium to be automatically migrated to Sonnet 4.6
- 更改 the `/恢复` picker to 显示 your most recent 提示 而不是 the 第一 one. This also resolves some titles appearing as `(会话)`.
- 更改 Claude.ai MCP connector 失败 to 显示 a 通知 而不是 silently disappearing 从 the 工具 列表
- 更改 示例 命令 建议 to be 已生成 deterministically 而不是 calling Haiku
- 更改 resuming 之后 compaction to 不再 produce a preamble recap 之前 continuing
- [SDK] 更改 任务 creation to 不再 require the `activeForm` 字段 — the 加载动画 falls back to the 任务 subject
- [VSCode] 新增 compaction 显示 as a collapsible "Compacted chat" card 与 the summary inside
- [VSCode] The 权限 mode picker 现在 respects `权限.disableBypassPermissionsMode` 从 your effective Claude 代码 设置 (包括 managed/policy 设置) — 当 集合 to `禁用`, 绕过 权限 mode is hidden 从 the picker
- [VSCode] 修复 RTL 文本 (Arabic, Hebrew, Persian) 渲染 reversed in the chat 面板 (回归 in v2.1.63)

## 2.1.68

- Opus 4.6 现在 defaults to medium effort 用于 Max 和 团队 subscribers. Medium effort works well 用于 most 任务 — it's the sweet spot between speed 和 thoroughness. You can 更改 this anytime 与 `/模型`
- Re-introduced the "超深度思考" keyword to 启用 high effort 用于 the 下一个 turn
- 移除 Opus 4 和 4.1 从 Claude 代码 on the 第一-party API — 用户 与 these 模型 pinned are automatically moved to Opus 4.6

## 2.1.66

- Reduced spurious 错误 日志

## 2.1.63

- 新增 `/simplify` 和 `/批` bundled slash 命令
- 修复 本地 slash 命令 输出 like /cost appearing as user-sent 消息 而不是 系统 消息 in the UI
- 项目 configs & auto 内存 现在 shared across git 工作树 of the same 仓库
- 新增 `ENABLE_CLAUDEAI_MCP_SERVERS=false` 环境变量 var to opt out 从 making Claude.ai MCP 服务器 可用
- 改进 `/模型` 命令 to 显示 the currently 活动 模型 in the slash 命令 菜单
- 新增 HTTP 钩子, which can POST JSON to a URL 和 接收 JSON 而不是 运行中 a shell 命令
- 修复 listener 泄漏 in bridge polling loop
- 修复 listener 泄漏 in MCP OAuth flow 清理
- 新增 manual URL 粘贴 回退 期间 MCP OAuth 认证. If the automatic localhost 重定向 doesn't work, you can 粘贴 the 回调 URL to 完成 认证.
- 修复 内存 泄漏 当 navigating 钩子 配置 菜单
- 修复 listener 泄漏 in interactive 权限 处理器 期间 auto-approvals
- 修复 文件 count 缓存 ignoring glob ignore 模式
- 修复 内存 泄漏 in bash 命令 前缀 缓存
- 修复 MCP 工具/资源 缓存 泄漏 on 服务器 重新连接
- 修复 IDE 主机 IP detection 缓存 incorrectly sharing results across ports
- 修复 WebSocket listener 泄漏 on transport 重新连接
- 修复 内存 泄漏 in git 根 detection 缓存 that could cause unbounded growth in long-运行中 会话
- 修复 内存 泄漏 in JSON 解析中 缓存 that grew unbounded over long 会话
- VSCode: 修复 远程 会话 not appearing in conversation history
- 修复 a race 条件 in the REPL bridge where 新 消息 could arrive at the 服务器 interleaved 与 historical 消息 期间 the 初始 连接 flush, causing 消息 ordering 问题.
- 修复 内存 泄漏 where long-运行中 teammates retained all 消息 in AppState even 之后 conversation compaction
- 修复 a 内存 泄漏 where MCP 服务器 fetch caches were not cleared on 断开连接, causing growing 内存 usage 与 服务器 that 重新连接 frequently
- 改进 内存 usage in long 会话 与 子代理 by stripping heavy progress 消息 payloads 期间 上下文 compaction
- 新增 "Always 复制 full 响应" 选项 to the `/复制` picker. 当 selected, future `/复制` 命令 will 跳过 the 代码 块 picker 和 复制 the full 响应 directly.
- VSCode: 新增 会话 rename 和 移除 actions to the 会话 列表
- 修复 `/清除` not resetting cached skills, which could cause stale skill content to 持久化 in the 新 conversation

## 2.1.62

- 修复 提示 建议 缓存 回归 that reduced 缓存 hit rates

## 2.1.61

- 修复 并发 writes corrupting config 文件 on Windows

## 2.1.59

- Claude automatically saves useful 上下文 to auto-内存. Manage 与 /内存
- 新增 `/复制` 命令 to 显示 an interactive picker 当 代码 块 are present, allowing selection of individual 代码 块 或 the full 响应.
- 改进 "always 允许" 前缀 建议 用于 compound bash 命令 (e.g. `cd /tmp && git fetch && git 推送`) to compute smarter per-subcommand prefixes 而不是 treating the whole 命令 as one
- 改进 ordering of short 任务 lists
- 改进 内存 usage in multi-代理 会话 by releasing 完成 子代理 任务 state
- 修复 MCP OAuth 令牌 刷新 race 条件 当 运行中 multiple Claude 代码 instances simultaneously
- 修复 shell 命令 not showing a 清除 错误 消息 当 the working 目录 has been deleted
- 修复 config 文件 corruption that could wipe 认证 当 multiple Claude 代码 instances ran simultaneously

## 2.1.58

- Expand 远程 Control to more 用户

## 2.1.56

- VS 代码: 修复 another cause of "命令 'Claude-VSCode.editor.openLast' not found" 崩溃

## 2.1.55

- 修复 BashTool failing on Windows 与 EINVAL 错误

## 2.1.53

- 修复 a UI flicker where user 输入 would briefly disappear 之后 submission 之前 the 消息 rendered
- 修复 bulk 代理 终止 (ctrl+f) to 发送 a single aggregate 通知 而不是 one per 代理, 和 to properly 清除 the 命令 队列
- 修复 graceful shutdown sometimes leaving stale 会话 当 使用 远程 Control by parallelizing teardown 网络 calls
- 修复 `--工作树` sometimes being ignored on 第一 启动
- 修复 a panic ("switch on corrupted 值") on Windows
- 修复 a 崩溃 that could occur 当 spawning many 流程 on Windows
- 修复 a 崩溃 in the WebAssembly interpreter on Linux x64 & Windows x64
- 修复 a 崩溃 that sometimes occurred 之后 2 分钟 on Windows ARM64

## 2.1.52

- VS 代码: 修复 extension 崩溃 on Windows ("命令 'Claude-VSCode.editor.openLast' not found")

## 2.1.51

- 新增 `Claude 远程-control` subcommand 用于 外部 builds, enabling 本地 环境 serving 用于 all 用户.
- Updated 插件 marketplace 默认 git 超时 从 30s to 120s 和 新增 `CLAUDE_CODE_PLUGIN_GIT_TIMEOUT_MS` to 配置.
- 新增 support 用于 自定义 npm registries 和 specific 版本 pinning 当 installing 插件 从 npm sources
- BashTool 现在 skips login shell (`-l` 标志) by 默认 当 a shell snapshot is 可用, improving 命令 执行 性能. Previously this required 设置 `CLAUDE_BASH_NO_LOGIN=true`.
- 修复 a 安全 问题 where `statusLine` 和 `fileSuggestion` 钩子 命令 could 执行 无 工作区 trust acceptance in interactive mode.
- 工具 results larger 比 50K characters are 现在 已持久化 to disk (previously 100K). This reduces 上下文窗口 usage 和 improves conversation longevity.
- 修复 a 缺陷 where 复制 `control_response` 消息 (e.g. 从 WebSocket reconnects) could cause API 400 错误 by pushing 复制 assistant 消息 进入 the conversation.
- 新增 `CLAUDE_CODE_ACCOUNT_UUID`, `CLAUDE_CODE_USER_EMAIL`, 和 `CLAUDE_CODE_ORGANIZATION_UUID` 环境 变量 用于 SDK callers to provide account info synchronously, eliminating a race 条件 where 早期 telemetry 事件 lacked account 元数据.
- 修复 slash 命令 autocomplete crashing 当 a 插件's SKILL.md description is a YAML 数组 或 other non-字符串 类型
- The `/模型` picker 现在 shows human-readable labels (e.g., "Sonnet 4.5") 而不是 原始 模型 IDs 用于 pinned 模型 版本, 与 an 升级 提示 当 a newer 版本 is 可用.
- Managed 设置 can 现在 be 集合 通过 macOS plist 或 Windows Registry. Learn more at HTTPS://代码.Claude.com/文档/en/设置#设置-文件

## 2.1.50

- 新增 support 用于 `startupTimeout` 配置 用于 LSP 服务器
- 新增 `WorktreeCreate` 和 `WorktreeRemove` 钩子 事件, enabling 自定义 VCS 设置 和 teardown 当 代理 工作树 isolation creates 或 removes 工作树.
- 修复 a 缺陷 where resumed 会话 could be invisible 当 the working 目录 involved symlinks, 因为 the 会话 storage 路径 was resolved at different times 期间 启动. Also 修复 会话 data loss on SSH 断开连接 by flushing 会话 data 之前 钩子 和 analytics in the graceful shutdown sequence.
- Linux: 修复 原生 modules not loading on systems 与 glibc older 比 2.30 (e.g., RHEL 8)
- 修复 内存 泄漏 in 代理 团队 where 完成 teammate 任务 were never garbage collected 从 会话 state
- 修复 `CLAUDE_CODE_SIMPLE` to fully 去除 down skills, 会话 内存, 自定义 代理, 和 Claude.md 令牌 counting
- 修复 `/MCP 重新连接` freezing the CLI 当 given a 服务器 name that doesn't exist
- 修复 内存 泄漏 where 完成 任务 state 对象 were never 移除 从 AppState
- 新增 support 用于 `isolation: 工作树` in 代理 definitions, allowing 代理 to declaratively run in isolated git 工作树.
- `CLAUDE_CODE_SIMPLE` mode 现在 also disables MCP 工具, attachments, 钩子, 和 Claude.md 文件 loading 用于 a fully minimal 体验.
- 修复 缺陷 where MCP 工具 were not discovered 当 工具 搜索 is 已启用 和 a 提示 is passed in as a 启动 参数
- 改进 内存 usage 期间 long 会话 by clearing 内部 caches 之后 compaction
- 新增 `Claude 代理` CLI 命令 to 列表 all configured 代理
- 改进 内存 usage 期间 long 会话 by clearing large 工具 results 之后 they have been processed
- 修复 a 内存 泄漏 where LSP diagnostic data was never cleaned up 之后 delivery, causing unbounded 内存 growth in long 会话
- 修复 a 内存 泄漏 where 完成 任务 输出 was not freed 从 内存, reducing 内存 usage in long 会话 与 many 任务
- 改进 启动 性能 用于 headless mode (`-p` 标志) by deferring Yoga WASM 和 UI 组件 imports
- 修复 提示 建议 缓存 回归 that reduced 缓存 hit rates
- 修复 unbounded 内存 growth in long 会话 by capping 文件 history snapshots
- 新增 `CLAUDE_CODE_DISABLE_1M_CONTEXT` 环境 变量 to 禁用 1M 上下文窗口 support
- Opus 4.6 (快速 mode) 现在 includes the full 1M 上下文窗口
- VSCode: 新增 `/extra-usage` 命令 support in VS 代码 会话
- 修复 内存 泄漏 where TaskOutput retained recent lines 之后 清理
- 修复 内存 泄漏 in CircularBuffer where cleared 项 were retained in the backing 数组
- 修复 内存 泄漏 in shell 命令 执行 where ChildProcess 和 AbortController references were retained 之后 清理

## 2.1.49

- 改进 MCP OAuth 认证 与 步骤-up 认证 support 和 discovery 缓存, reducing redundant 网络 请求 期间 服务器 连接
- 新增 `--工作树` (`-w`) 标志 to 启动 Claude in an isolated git 工作树
- 子代理 support `isolation: "工作树"` 用于 working in a temporary git 工作树
- 新增 Ctrl+F keybinding to 终止 background 代理 (two-press confirmation)
- 代理 definitions support `background: true` to always run as a background 任务
- 插件 can ship `设置.JSON` 用于 默认 配置
- 修复 文件-not-found 错误 to suggest corrected 路径 当 the 模型 drops the 仓库 文件夹
- 修复 Ctrl+C 和 ESC being silently ignored 当 background 代理 are 运行中 和 the main 线程 is idle. Pressing twice within 3 秒 现在 kills all background 代理.
- 修复 提示 建议 缓存 回归 that reduced 缓存 hit rates.
- 修复 `插件 启用` 和 `插件 禁用` to auto-detect the correct 作用域 当 `--作用域` is not specified, 而不是 always defaulting to user 作用域
- Simple mode (`CLAUDE_CODE_SIMPLE`) 现在 includes the 文件 编辑 工具 除了 the Bash 工具, allowing direct 文件 editing in simple mode.
- 权限 建议 are 现在 populated 当 safety checks 触发 an ask 响应, enabling SDK consumers to 显示 权限 选项
- Sonnet 4.5 与 1M 上下文 is being 移除 从 the Max plan in favor of our frontier Sonnet 4.6 模型, which 现在 has 1M 上下文. Please switch in /模型.
- 修复 verbose mode not updating thinking 块 显示 当 toggled 通过 `/config` — memo comparators 现在 correctly detect verbose 更改
- 修复 unbounded WASM 内存 growth 期间 long 会话 by periodically resetting the 树-sitter parser
- 修复 potential 渲染 问题 caused by stale yoga 布局 references
- 改进 性能 in non-interactive mode (`-p`) by skipping unnecessary API calls 期间 启动
- 改进 性能 by 缓存 认证 失败 用于 HTTP 和 SSE MCP 服务器, avoiding repeated 连接 attempts to 服务器 requiring 认证
- 修复 unbounded 内存 growth 期间 long-运行中 会话 caused by Yoga WASM linear 内存 never shrinking
- SDK 模型 info 现在 includes `supportsEffort`, `supportedEffortLevels`, 和 `supportsAdaptiveThinking` fields 所以 consumers can discover 模型 capabilities.
- 新增 `ConfigChange` 钩子 事件 that fires 当 配置 文件 更改 期间 a 会话, enabling 企业 安全 auditing 和 optional blocking of 设置 更改.
- 改进 启动 性能 by 缓存 MCP 认证 失败 to avoid redundant 连接 attempts
- 改进 启动 性能 by reducing HTTP calls 用于 analytics 令牌 counting
- 改进 启动 性能 by batching MCP 工具 令牌 counting 进入 a single API call
- 修复 `disableAllHooks` 设置 to respect managed 设置 hierarchy — non-managed 设置 can 不再 禁用 managed 钩子 集合 by policy (#26637)
- 修复 `--恢复` 会话 picker showing 原始 XML tags 用于 会话 that 启动 与 命令 like `/清除`. 现在 correctly falls through to the 会话 ID 回退.
- 改进 权限 prompts 用于 路径 safety 和 working 目录 块 to 显示 the reason 用于 the restriction 而不是 a bare 提示 与 no 上下文

## 2.1.47

- 修复 FileWriteTool line counting to preserve intentional trailing 空白 lines 而不是 stripping them 与 `trimEnd()`.
- 修复 Windows 终端 渲染 缺陷 caused by `os.EOL` (`\r\n`) in 显示 代码 — line counts 现在 显示 correct 值 而不是 always showing 1 on Windows.
- 改进 VS 代码 plan 预览: auto-updates as Claude iterates, enables commenting only 当 the plan is ready 用于 review, 和 keeps the 预览 打开 当 rejecting 所以 Claude can revise.
- 修复 a 缺陷 where bold 和 colored 文本 in markdown 输出 could shift to the wrong characters on Windows 由于 `\r\n` line endings.
- 修复 compaction failing 当 conversation contains many PDF documents by stripping document 块 alongside images 之前 sending to the compaction API (anthropics/Claude-代码#26188)
- 改进 内存 usage in long-运行中 会话 by releasing API 流 buffers, 代理 上下文, 和 skill state 之后 use
- 改进 启动 性能 by deferring SessionStart 钩子 执行, reducing time-to-interactive by ~500ms.
- 修复 an 问题 where bash 工具 输出 was silently discarded on Windows 当 使用 MSYS2 或 Cygwin shells.
- 改进 性能 of `@` 文件 mentions - 文件 建议 现在 appear 更快 by pre-warming the 索引 on 启动 和 使用 会话-基于 缓存 与 background 刷新.
- 改进 内存 usage by trimming 代理 任务 消息 history 之后 任务 完成
- 改进 内存 usage 期间 long 代理 会话 by eliminating O(n²) 消息 accumulation in progress updates
- 修复 the bash 权限 classifier to 验证 that returned 匹配 descriptions correspond to actual 输入 rules, preventing hallucinated descriptions 从 incorrectly granting 权限
- 修复 user-defined 代理 only loading one 文件 on NFS/FUSE filesystems that report zero inodes (anthropics/Claude-代码#26044)
- 修复 插件 代理 skills silently failing to 加载 当 referenced by bare name 而不是 fully-qualified 插件 name (anthropics/Claude-代码#25834)
- 搜索 模式 in collapsed 工具 results are 现在 displayed in quotes 用于 clarity
- Windows: 修复 CWD tracking temp 文件 never being cleaned up, causing them to accumulate indefinitely (anthropics/Claude-代码#17600)
- Use `ctrl+f` to 终止 all background 代理 而不是 double-pressing ESC. Background 代理 现在 继续 运行中 当 you press ESC to 取消 the main 线程, giving you more control over 代理 lifecycle.
- 修复 API 400 错误 ("thinking 块 cannot be modified") that occurred in 会话 与 并发 代理, caused by interleaved 流式 content 块 preventing proper 消息 merging.
- Simplified teammate navigation to use only Shift+Down (与 wrapping) 而不是 both Shift+Up 和 Shift+Down.
- 修复 an 问题 where a single 文件 写入/编辑 错误 would 中止 all other 并行 文件 写入/编辑 operations. Independent 文件 mutations 现在 完成 even 当 a sibling fails.
- 新增 `last_assistant_message` 字段 to 停止 和 SubagentStop 钩子 inputs, providing the 最终 assistant 响应 文本 所以 钩子 can 访问 it 无 解析中 转录 文件.
- 修复 自定义 会话 titles 集合 通过 `/rename` being lost 之后 resuming a conversation (anthropics/Claude-代码#23610)
- 修复 collapsed 读取/搜索 提示 文本 overflowing on narrow terminals by truncating 从 the 启动.
- 修复 an 问题 where bash 命令 与 backslash-newline continuation lines (e.g., long 命令 分割 across multiple lines 与 `\`) would produce spurious 空 arguments, potentially breaking 命令 执行.
- 修复 内置 slash 命令 (`/help`, `/模型`, `/压缩`, etc.) being hidden 从 the autocomplete dropdown 当 many user skills are installed (anthropics/Claude-代码#22020)
- 修复 MCP 服务器 not appearing in the MCP Management 对话框 之后 deferred loading
- 修复 会话 name persisting in status bar 之后 `/清除` 命令 (anthropics/Claude-代码#26082)
- 修复 崩溃 当 a skill's `name` 或 `description` in SKILL.md frontmatter is a bare 数字 (e.g., `name: 3000`) — the 值 is 现在 properly coerced to a 字符串 (anthropics/Claude-代码#25837)
- 修复 /恢复 silently dropping 会话 当 the 第一 消息 exceeds 16KB 或 uses 数组-格式 content (anthropics/Claude-代码#25721)
- 新增 `chat:newline` keybinding action 用于 configurable multi-line 输入 (anthropics/Claude-代码#26075)
- 新增 `added_dirs` to the statusline JSON `工作区` 部分, exposing directories 新增 通过 `/添加-dir` to 外部 脚本 (anthropics/Claude-代码#26096)
- 修复 `Claude doctor` misclassifying mise 和 asdf-managed installations as 原生 installs (anthropics/Claude-代码#26033)
- 修复 zsh heredoc failing 与 "读取-only 文件 系统" 错误 in 沙盒化 命令 (anthropics/Claude-代码#25990)
- 修复 代理 progress indicator showing inflated 工具 use count (anthropics/Claude-代码#26023)
- 修复 image pasting not working on WSL2 systems where Windows copies images as BMP 格式 (anthropics/Claude-代码#25935)
- 修复 background 代理 results returning 原始 转录 data 而不是 the 代理's 最终 answer (anthropics/Claude-代码#26012)
- 修复 Warp 终端 incorrectly prompting 用于 Shift+Enter 设置 当 it supports it natively (anthropics/Claude-代码#25957)
- 修复 CJK wide characters causing misaligned timestamps 和 布局 元素 in the TUI (anthropics/Claude-代码#26084)
- 修复 自定义 代理 `模型` 字段 in `.Claude/代理/*.md` being ignored 当 spawning 团队 teammates (anthropics/Claude-代码#26064)
- 修复 计划模式 being lost 之后 上下文 compaction, causing the 模型 to switch 从 planning to 实现 mode (anthropics/Claude-代码#26061)
- 修复 `alwaysThinkingEnabled: true` in 设置.JSON not enabling thinking mode on Bedrock 和 Vertex providers (anthropics/Claude-代码#26074)
- 修复 `tool_decision` OTel telemetry 事件 not being emitted in headless/SDK mode (anthropics/Claude-代码#26059)
- 修复 会话 name being lost 之后 上下文 compaction — renamed 会话 现在 preserve their 自定义 title through compaction (anthropics/Claude-代码#26121)
- Increased 初始 会话 count in 恢复 picker 从 10 to 50 用于 更快 会话 discovery (anthropics/Claude-代码#26123)
- Windows: 修复 工作树 会话 matching 当 drive letter casing differs (anthropics/Claude-代码#26123)
- 修复 `/恢复 <会话-ID>` failing to 查找 会话 whose 第一 消息 exceeds 16KB (anthropics/Claude-代码#25920)
- 修复 "Always 允许" on multiline bash 命令 creating 无效 权限 模式 that corrupt 设置 (anthropics/Claude-代码#25909)
- 修复 React 崩溃 (错误 #31) 当 a skill's `参数-提示` in SKILL.md frontmatter uses YAML sequence syntax (e.g., `[topic: foo | bar]`) — the 值 is 现在 properly coerced to a 字符串 (anthropics/Claude-代码#25826)
- 修复 崩溃 当 使用 `/分叉` on 会话 that used web 搜索 — 空 条目 in 搜索 results 从 转录 deserialization are 现在 handled gracefully (anthropics/Claude-代码#25811)
- 修复 读取-only git 命令 triggering FSEvents 文件 watcher loops on macOS by adding --no-optional-locks 标志 (anthropics/Claude-代码#25750)
- 修复 自定义 代理 和 skills not being discovered 当 运行中 从 a git 工作树 — 项目-级别 `.Claude/代理/` 和 `.Claude/skills/` 从 the main 仓库 are 现在 included (anthropics/Claude-代码#25816)
- 修复 non-interactive subcommands like `Claude doctor` 和 `Claude 插件 验证` being blocked inside nested Claude 会话 (anthropics/Claude-代码#25803)
- Windows: 修复 the same Claude.md 文件 being loaded twice 当 drive letter casing differs between 路径 (anthropics/Claude-代码#25756)
- 修复 内联 代码 spans in markdown being incorrectly 已解析 as bash 命令 (anthropics/Claude-代码#25792)
- 修复 teammate spinners not respecting 自定义 spinnerVerbs 从 设置 (anthropics/Claude-代码#25748)
- 修复 shell 命令 permanently failing 之后 a 命令 deletes its own working 目录 (anthropics/Claude-代码#26136)
- 修复 钩子 (PreToolUse, PostToolUse) silently failing to 执行 on Windows by 使用 git Bash 而不是 cmd.exe (anthropics/Claude-代码#25981)
- 修复 LSP `findReferences` 和 other location-基于 operations returning results 从 gitignored 文件 (e.g., `node_modules/`, `venv/`) (anthropics/Claude-代码#26051)
- Moved config 备份 文件 从 home 目录 根 to `~/.Claude/备份/` to reduce home 目录 clutter (anthropics/Claude-代码#26130)
- 修复 会话 与 large 第一 prompts (>16KB) disappearing 从 the /恢复 列表 (anthropics/Claude-代码#26140)
- 修复 shell functions 与 double-underscore prefixes (e.g., `__git_ps1`) not being preserved across shell 会话 (anthropics/Claude-代码#25824)
- 修复 加载动画 showing "0 令牌" counter 之前 any 令牌 have been received (anthropics/Claude-代码#26105)
- VSCode: 修复 conversation 消息 appearing dimmed 当 the AskUserQuestion 对话框 is 打开 (anthropics/Claude-代码#26078)
- 修复 background 任务 failing in git 工作树 由于 远程 URL resolution reading 从 工作树-specific gitdir 而不是 the main 仓库 config (anthropics/Claude-代码#26065)
- 修复 Right Alt 键 leaving visible `[25~` 转义 sequence residue in the 输入 字段 on Windows/git Bash terminals (anthropics/Claude-代码#25943)
- The `/rename` 命令 现在 updates the 终端 标签页 title by 默认 (anthropics/Claude-代码#25789)
- 修复 编辑 工具 silently corrupting Unicode curly quotes (\u201c\u201d \u2018\u2019) by replacing them 与 straight quotes 当 making edits (anthropics/Claude-代码#26141)
- 修复 OSC 8 hyperlinks only being clickable on the 第一 line 当 链接 文本 wraps across multiple 终端 lines.

## 2.1.46

- 修复 orphaned CC 流程 之后 终端 断开连接 on macOS
- 新增 support 用于 使用 Claude.ai MCP connectors in Claude 代码

## 2.1.45

- 新增 support 用于 Claude Sonnet 4.6
- 新增 support 用于 reading `enabledPlugins` 和 `extraKnownMarketplaces` 从 `--添加-dir` directories
- 新增 `spinnerTipsOverride` 设置 to customize 加载动画 技巧 — 配置 `技巧` 与 an 数组 of 自定义 提示 strings, 和 optionally 集合 `excludeDefault: true` to 显示 only your 自定义 技巧 而不是 the 内置 ones
- 新增 `SDKRateLimitInfo` 和 `SDKRateLimitEvent` 类型 to the SDK, enabling consumers to 接收 速率限制 status updates 包括 utilization, reset times, 和 overage information
- 修复 代理 团队 teammates failing on Bedrock, Vertex, 和 Foundry by propagating API provider 环境 变量 to tmux-spawned 流程 (anthropics/Claude-代码#23561)
- 修复 沙盒 "operation not permitted" 错误 当 writing temporary 文件 on macOS by 使用 the correct per-user temp 目录 (anthropics/Claude-代码#21654)
- 修复 任务 工具 (backgrounded 代理) crashing 与 a `ReferenceError` on completion (anthropics/Claude-代码#22087)
- 修复 autocomplete 建议 not being accepted on Enter 当 images are pasted in the 输入
- 修复 skills invoked by 子代理 incorrectly appearing in main 会话 上下文 之后 compaction
- 修复 excessive `.Claude.JSON.备份` 文件 accumulating on every 启动
- 修复 插件-provided 命令, 代理, 和 钩子 not being 可用 immediately 之后 安装 无 requiring a 重启
- 改进 启动 性能 by removing eager loading of 会话 history 用于 stats 缓存
- 改进 内存 usage 用于 shell 命令 that produce large 输出 — RSS 不再 grows unboundedly 与 命令 输出 size
- 改进 collapsed 读取/搜索 组 to 显示 the 当前 文件 或 搜索 模式 being processed beneath the summary line 当 活动
- [VSCode] 改进 权限 destination 选择 (项目/user/会话) to 持久化 across 会话

## 2.1.44

- 修复 ENAMETOOLONG 错误 用于 deeply-nested 目录 路径
- 修复 认证 刷新 错误

## 2.1.43

- 修复 AWS 认证 刷新 hanging indefinitely by adding a 3-分钟 超时
- 修复 spurious 警告 用于 non-代理 markdown 文件 in `.Claude/代理/` 目录
- 修复 structured-outputs 测试版 头信息 being sent unconditionally on Vertex/Bedrock

## 2.1.42

- 改进 启动 性能 by deferring Zod schema construction
- 改进 提示 缓存 hit rates by moving date out of 系统 提示
- 新增 one-time Opus 4.6 effort callout 用于 eligible 用户
- 修复 /恢复 showing 中断 消息 as 会话 titles
- 修复 image dimension 限制 错误 to suggest /压缩

## 2.1.41

- 新增 guard against launching Claude 代码 inside another Claude 代码 会话
- 修复 代理 团队 使用 wrong 模型 identifier 用于 Bedrock, Vertex, 和 Foundry customers
- 修复 a 崩溃 当 MCP 工具 return image content 期间 流式
- 修复 /恢复 会话 previews showing 原始 XML tags 而不是 readable 命令 names
- 改进 模型 错误 消息 用于 Bedrock/Vertex/Foundry 用户 与 回退 建议
- 修复 插件 browse showing misleading "Space to Toggle" 提示 用于 already-installed 插件
- 修复 钩子 blocking 错误 (退出 代码 2) not showing stderr to the user
- 新增 `speed` 属性 to OTel 事件 和 追踪 spans 用于 快速 mode visibility
- 新增 `Claude 认证 login`, `Claude 认证 status`, 和 `Claude 认证 logout` CLI subcommands
- 新增 Windows ARM64 (win32-arm64) 原生 二进制 support
- 改进 `/rename` to auto-generate 会话 name 从 conversation 上下文 当 called 无 arguments
- 改进 narrow 终端 布局 用于 提示 footer
- 修复 文件 resolution failing 用于 @-mentions 与 anchor 片段 (e.g., `@README.md#安装`)
- 修复 FileReadTool blocking the 流程 on FIFOs, `/dev/stdin`, 和 large 文件
- 修复 background 任务 通知 not being delivered in 流式 代理 SDK mode
- 修复 光标 jumping to end on each keystroke in classifier rule 输入
- 修复 markdown 链接 显示 文本 being dropped 用于 原始 URL
- 修复 auto-压缩 失败 错误 通知 being shown to 用户
- 修复 权限 wait time being included in 子代理 elapsed time 显示
- 修复 proactive ticks firing 当 in 计划模式
- 修复 清除 stale 权限 rules 当 设置 更改 on disk
- 修复 钩子 blocking 错误 showing stderr content in UI

## 2.1.39

- 改进 终端 渲染 性能
- 修复 fatal 错误 being swallowed 而不是 displayed
- 修复 流程 hanging 之后 会话 关闭
- 修复 character loss at 终端 屏幕 边界
- 修复 空白 lines in verbose 转录 视图

## 2.1.38

- 修复 VS 代码 终端 滚动-to-top 回归 introduced in 2.1.37
- 修复 标签页 键 queueing slash 命令 而不是 autocompleting
- 修复 bash 权限 matching 用于 命令 使用 环境 变量 wrappers
- 修复 文本 between 工具 uses disappearing 当 not 使用 流式
- 修复 复制 会话 当 resuming in VS 代码 extension
- 改进 heredoc delimiter 解析中 to prevent 命令 smuggling
- Blocked writes to `.Claude/skills` 目录 in 沙盒 mode

## 2.1.37

- 修复 an 问题 where /快速 was not immediately 可用 之后 enabling /extra-usage

## 2.1.36

- 快速 mode is 现在 可用 用于 Opus 4.6. Learn more at HTTPS://代码.Claude.com/文档/en/快速-mode

## 2.1.34

- 修复 a 崩溃 当 代理 团队 设置 更改 between renders
- 修复 a 缺陷 where 命令 excluded 从 sandboxing (通过 `沙盒.excludedCommands` 或 `dangerouslyDisableSandbox`) could 绕过 the Bash ask 权限 rule 当 `autoAllowBashIfSandboxed` was 已启用

## 2.1.33

- 修复 代理 teammate 会话 in tmux to 发送 和 接收 消息
- 修复 警告 about 代理 团队 not being 可用 on your 当前 plan
- 新增 `TeammateIdle` 和 `TaskCompleted` 钩子 事件 用于 multi-代理 工作流
- 新增 support 用于 restricting which sub-代理 can be spawned 通过 `任务(agent_type)` syntax in 代理 "工具" frontmatter
- 新增 `内存` frontmatter 字段 support 用于 代理, enabling persistent 内存 与 `user`, `项目`, 或 `本地` 作用域
- 新增 插件 name to skill descriptions 和 `/skills` 菜单 用于 better discoverability
- 修复 an 问题 where submitting a 新 消息 当 the 模型 was in extended thinking would 中断 the thinking 阶段
- 修复 an API 错误 that could occur 当 aborting mid-流, where whitespace 文本 combined 与 a thinking 块 would 绕过 normalization 和 produce an 无效 请求
- 修复 API 代理 兼容性 问题 where 404 错误 on 流式 endpoints 不再 triggered non-流式 回退
- 修复 an 问题 where 代理 设置 configured 通过 `设置.JSON` 环境 变量 were not applied to WebFetch 和 other HTTP 请求 on the 节点.js 构建
- 修复 `/恢复` 会话 picker showing 原始 XML markup 而不是 clean titles 用于 会话 started 与 slash 命令
- 改进 错误 消息 用于 API 连接 失败 — 现在 shows specific cause (e.g., ECONNREFUSED, SSL 错误) 而不是 泛型 "连接 错误"
- 错误 从 无效 managed 设置 are 现在 surfaced
- VSCode: 新增 support 用于 远程 会话, allowing OAuth 用户 to browse 和 恢复 会话 从 Claude.ai
- VSCode: 新增 git 分支 和 消息 count to the 会话 picker, 与 support 用于 searching by 分支 name
- VSCode: 修复 滚动-to-bottom under-滚动 on 初始 会话 加载 和 会话 switch

## 2.1.32

- Claude Opus 4.6 is 现在 可用!
- 新增 research 预览 代理 团队 功能 用于 multi-代理 collaboration (令牌-intensive 功能, requires 设置 CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1)
- Claude 现在 automatically records 和 recalls memories as it works
- 新增 "Summarize 从 here" to the 消息 selector, allowing partial conversation summarization.
- Skills defined in `.Claude/skills/` within additional directories (`--添加-dir`) are 现在 loaded automatically.
- 修复 `@` 文件 completion showing incorrect relative 路径 当 运行中 从 a subdirectory
- Updated --恢复 to re-use --代理 值 specified in 上一个 conversation by 默认.
- 修复: Bash 工具 不再 throws "Bad substitution" 错误 当 heredocs contain JavaScript 模板 literals like `${索引 + 1}`, which previously interrupted 工具 执行
- Skill character budget 现在 scales 与 上下文窗口 (2% of 上下文), 所以 用户 与 larger 上下文 Windows can see more skill descriptions 无 truncation
- 修复 Thai/Lao spacing vowels (สระ า, ำ) not 渲染 correctly in the 输入 字段
- VSCode: 修复 slash 命令 incorrectly being executed 当 pressing Enter 与 preceding 文本 in the 输入 字段
- VSCode: 新增 加载动画 当 loading past conversations 列表

## 2.1.31

- 新增 会话 恢复 提示 on 退出, showing how to 继续 your conversation later
- 新增 support 用于 full-width (zenkaku) space 输入 从 Japanese IME in checkbox selection
- 修复 PDF too large 错误 permanently locking up 会话, requiring 用户 to 启动 a 新 conversation
- 修复 bash 命令 incorrectly reporting 失败 与 "读取-only 文件 系统" 错误 当 沙盒 mode was 已启用
- 修复 a 崩溃 that made 会话 unusable 之后 entering 计划模式 当 项目 config in `~/.Claude.JSON` was 缺失 默认 fields
- 修复 `temperatureOverride` being silently ignored in the 流式 API 路径, causing all 流式 请求 to use the 默认 temperature (1) regardless of the configured 覆盖
- 修复 LSP shutdown/退出 兼容性 与 strict language 服务器 that reject 空 params
- 改进 系统 prompts to more clearly 指南 the 模型 toward 使用 dedicated 工具 (读取, 编辑, Glob, Grep) 而不是 bash equivalents (`cat`, `sed`, `grep`, `查找`), reducing unnecessary bash 命令 usage
- 改进 PDF 和 请求 size 错误 消息 to 显示 actual 限制 (100 pages, 20MB)
- Reduced 布局 jitter in the 终端 当 the 加载动画 appears 和 disappears 期间 流式
- 移除 misleading Anthropic API pricing 从 模型 selector 用于 third-party provider (Bedrock, Vertex, Foundry) 用户

## 2.1.30

- 新增 `pages` 参数 to the 读取 工具 用于 PDFs, allowing specific page ranges to be 读取 (e.g., `pages: "1-5"`). Large PDFs (>10 pages) 现在 return a lightweight 引用 当 `@` mentioned 而不是 being inlined 进入 上下文.
- 新增 pre-configured OAuth 客户端 credentials 用于 MCP 服务器 that don't support 动态 客户端 Registration (e.g., Slack). Use `--客户端-ID` 和 `--客户端-secret` 与 `Claude MCP 添加`.
- 新增 `/调试` 用于 Claude to help troubleshoot the 当前 会话
- 新增 support 用于 additional `git 日志` 和 `git 显示` 标志 in 读取-only mode (e.g., `--topo-order`, `--cherry-pick`, `--格式`, `--原始`)
- 新增 令牌 count, 工具 uses, 和 duration metrics to 任务 工具 results
- 新增 reduced motion mode to the config
- 修复 phantom "(no content)" 文本 块 appearing in API conversation history, reducing 令牌 waste 和 potential 模型 confusion
- 修复 提示 缓存 not correctly invalidating 当 工具 descriptions 或 输入 schemas 更改, only 当 工具 names 更改
- 修复 400 错误 that could occur 之后 运行中 `/login` 当 the conversation contained thinking 块
- 修复 a hang 当 resuming 会话 与 corrupted 转录 文件 containing `parentUuid` cycles
- 修复 速率限制 消息 showing incorrect "/升级" 建议 用于 Max 20x 用户 当 extra-usage is 不可用
- 修复 权限 dialogs stealing focus 当 actively typing
- 修复 子代理 not being able to 访问 SDK-provided MCP 工具 因为 they were not synced to the shared 应用程序 state
- 修复 a 回归 where Windows 用户 与 a `.bashrc` 文件 could not run bash 命令
- 改进 内存 usage 用于 `--恢复` (68% reduction 用于 用户 与 many 会话) by replacing the 会话 索引 与 lightweight stat-基于 loading 和 progressive enrichment
- 改进 `TaskStop` 工具 to 显示 the 已停止 命令/任务 description in the result line 而不是 a 泛型 "任务 已停止" 消息
- 更改 `/模型` to 执行 immediately 而不是 being queued
- [VSCode] 新增 multiline 输入 support to the "Other" 文本 输入 in question dialogs (use Shift+Enter 用于 新 lines)
- [VSCode] 修复 复制 会话 appearing in the 会话 列表 当 starting a 新 conversation

## 2.1.29

- 修复 启动 性能 问题 当 resuming 会话 that have `saved_hook_context`

## 2.1.27

- 新增 工具 call 失败 和 denials to 调试 日志
- 修复 上下文 management validation 错误 用于 gateway 用户, ensuring `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1` avoids the 错误
- 新增 `--从-PR` 标志 to 恢复 会话 linked to a specific GitHub PR 数字 或 URL
- 会话 are 现在 automatically linked to PRs 当 created 通过 `gh PR 创建`
- 修复 /上下文 命令 not displaying colored 输出
- 修复 status bar duplicating background 任务 indicator 当 PR status was shown
- Windows: 修复 bash 命令 执行 failing 用于 用户 与 `.bashrc` 文件
- Windows: 修复 console Windows flashing 当 spawning child 流程
- VSCode: 修复 OAuth 令牌 expiration causing 401 错误 之后 extended 会话

## 2.1.25

- 修复 测试版 头信息 validation 错误 用于 gateway 用户 on Bedrock 和 Vertex, ensuring `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1` avoids the 错误

## 2.1.23

- 新增 customizable 加载动画 verbs 设置 (`spinnerVerbs`)
- 修复 mTLS 和 代理 connectivity 用于 用户 behind corporate proxies 或 使用 客户端 certificates
- 修复 per-user temp 目录 isolation to prevent 权限 conflicts on shared systems
- 修复 a race 条件 that could cause 400 错误 当 提示 缓存 作用域 was 已启用
- 修复 待处理 异步 钩子 not being cancelled 当 headless 流式 会话 ended
- 修复 标签页 completion not updating the 输入 字段 当 accepting a 建议
- 修复 ripgrep 搜索 timeouts silently returning 空 results 而不是 reporting 错误
- 改进 终端 渲染 性能 与 已优化 屏幕 data 布局
- 更改 Bash 命令 to 显示 超时 duration alongside elapsed time
- 更改 merged 拉取 请求 to 显示 a purple status indicator in the 提示 footer
- [IDE] 修复 模型 选项 displaying incorrect region strings 用于 Bedrock 用户 in headless mode

## 2.1.22

- 修复 structured outputs 用于 non-interactive (-p) mode

## 2.1.21

- 新增 support 用于 full-width (zenkaku) 数字 输入 从 Japanese IME in 选项 selection prompts
- 修复 shell completion 缓存 文件 being truncated on 退出
- 修复 API 错误 当 resuming 会话 that were interrupted 期间 工具 执行
- 修复 auto-压缩 triggering too 早期 on 模型 与 large 输出 令牌 限制
- 修复 任务 IDs potentially being reused 之后 deletion
- 修复 文件 搜索 not working in VS 代码 extension on Windows
- 改进 读取/搜索 progress indicators to 显示 "Reading…" 当 in progress 和 "读取" 当 完成
- 改进 Claude to prefer 文件 operation 工具 (读取, 编辑, 写入) over bash equivalents (cat, sed, awk)
- [VSCode] 新增 automatic Python 虚拟 环境 activation, ensuring `Python` 和 `pip` 命令 use the correct interpreter (configurable 通过 `claudeCode.usePythonEnvironment` 设置)
- [VSCode] 修复 消息 action buttons having incorrect background colors

## 2.1.20

- 新增 arrow 键 history navigation in vim normal mode 当 光标 cannot 移动 further
- 新增 外部 editor shortcut (Ctrl+G) to the help 菜单 用于 better discoverability
- 新增 PR review status indicator to the 提示 footer, showing the 当前 分支's PR state (approved, 更改 requested, 待处理, 或 draft) as a colored dot 与 a clickable 链接
- 新增 support 用于 loading `Claude.md` 文件 从 additional directories specified 通过 `--添加-dir` 标志 (requires 设置 `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1`)
- 新增 ability to 删除 任务 通过 the `TaskUpdate` 工具
- 修复 会话 compaction 问题 that could cause 恢复 to 加载 full history 而不是 the 压缩 summary
- 修复 代理 sometimes ignoring user 消息 sent 当 actively working on a 任务
- 修复 wide character (emoji, CJK) 渲染 artifacts where trailing columns were not cleared 当 replaced by narrower characters
- 修复 JSON 解析中 错误 当 MCP 工具 响应 contain special Unicode characters
- 修复 up/down arrow 键 in multi-line 和 wrapped 文本 输入 to prioritize 光标 movement over history navigation
- 修复 draft 提示 being lost 当 pressing UP arrow to navigate 命令 history
- 修复 ghost 文本 flickering 当 typing slash 命令 mid-输入
- 修复 marketplace 源 removal not properly deleting 设置
- 修复 复制 输出 in some 命令 like `/上下文`
- 修复 任务 列表 sometimes showing outside the main conversation 视图
- 修复 syntax highlighting 用于 diffs occurring within multiline constructs like Python docstrings
- 修复 崩溃 当 cancelling 工具 use
- 改进 `/沙盒` 命令 UI to 显示 dependency status 与 安装 instructions 当 dependencies are 缺失
- 改进 thinking status 文本 与 a subtle shimmer animation
- 改进 任务 列表 to dynamically adjust visible 项 基于 on 终端 height
- 改进 分叉 conversation 提示 to 显示 how to 恢复 the original 会话
- 更改 collapsed 读取/搜索 组 to 显示 present tense ("Reading", "Searching 用于") 当 in progress, 和 past tense ("读取", "Searched 用于") 当 完成
- 更改 `ToolSearch` results to appear as a brief 通知 而不是 内联 in the conversation
- 更改 the `/提交-推送-PR` skill to automatically post PR URLs to Slack channels 当 configured 通过 MCP 工具
- 更改 the `/复制` 命令 to be 可用 to all 用户
- 更改 background 代理 to 提示 用于 工具 权限 之前 launching
- 更改 权限 rules like `Bash(*)` to be accepted 和 treated as equivalent to `Bash`
- 更改 config 备份 to be timestamped 和 rotated (keeping 5 most recent) to prevent data loss

## 2.1.19

- 新增 环境变量 var `CLAUDE_CODE_ENABLE_TASKS`, 集合 to `false` to keep the 旧 系统 temporarily
- 新增 shorthand `$0`, `$1`, etc. 用于 accessing individual arguments in 自定义 命令
- 修复 崩溃 on processors 无 AVX instruction support
- 修复 dangling Claude 代码 流程 当 终端 is closed by catching EIO 错误 从 `流程.退出()` 和 使用 SIGKILL as 回退
- 修复 `/rename` 和 `/tag` not updating the correct 会话 当 resuming 从 a different 目录 (e.g., git 工作树)
- 修复 resuming 会话 by 自定义 title not working 当 run 从 a different 目录
- 修复 pasted 文本 content being lost 当 使用 提示 stash (Ctrl+S) 和 恢复
- 修复 代理 列表 displaying "Sonnet (默认)" 而不是 "Inherit (默认)" 用于 代理 无 an explicit 模型 设置
- 修复 backgrounded 钩子 命令 not returning 早期, potentially causing the 会话 to wait on a 流程 that was intentionally backgrounded
- 修复 文件 写入 预览 omitting 空 lines
- 更改 skills 无 additional 权限 或 钩子 to be 允许 无 requiring approval
- 更改 indexed 参数 syntax 从 `$ARGUMENTS.0` to `$ARGUMENTS[0]` (bracket syntax)
- [SDK] 新增 replay of `queued_command` attachment 消息 as `SDKUserMessageReplay` 事件 当 `replayUserMessages` is 已启用
- [VSCode] 已启用 会话 forking 和 rewind functionality 用于 all 用户

## 2.1.18

- 新增 customizable 键盘 shortcuts. 配置 keybindings per 上下文, 创建 chord sequences, 和 personalize your 工作流. Run `/keybindings` to get started. Learn more at HTTPS://代码.Claude.com/文档/en/keybindings

## 2.1.17

- 修复 崩溃 on processors 无 AVX instruction support

## 2.1.16

- 新增 新 任务 management 系统, 包括 新 capabilities like dependency tracking
- [VSCode] 新增 原生 插件 management support
- [VSCode] 新增 ability 用于 OAuth 用户 to browse 和 恢复 远程 Claude 会话 从 the 会话 对话框
- 修复 out-of-内存 崩溃 当 resuming 会话 与 heavy 子代理 usage
- 修复 an 问题 where the "上下文 remaining" 警告 was not hidden 之后 运行中 `/压缩`
- 修复 会话 titles on the 恢复 屏幕 not respecting the user's language 设置
- [IDE] 修复 a race 条件 on Windows where the Claude 代码 sidebar 视图 container would not appear on 启动

## 2.1.15

- 新增 deprecation 通知 用于 npm installations - run `Claude 安装` 或 see HTTPS://文档.Anthropic.com/en/文档/Claude-代码/getting-started 用于 more 选项
- 改进 UI 渲染 性能 与 React Compiler
- 修复 the "上下文 left 直到 auto-压缩" 警告 not disappearing 之后 运行中 `/压缩`
- 修复 MCP stdio 服务器 超时 not killing child 流程, which could cause UI freezes

## 2.1.14

- 新增 history-基于 autocomplete in bash mode (`!`) - 类型 a partial 命令 和 press 标签页 to 完成 从 your bash 命令 history
- 新增 搜索 to installed 插件 列表 - 类型 to 过滤 by name 或 description
- 新增 support 用于 pinning 插件 to specific git 提交 SHAs, allowing marketplace 条目 to 安装 exact 版本
- 修复 a 回归 where the 上下文窗口 blocking 限制 was calculated too aggressively, blocking 用户 at ~65% 上下文 usage 而不是 the intended ~98%
- 修复 内存 问题 that could cause 崩溃 当 运行中 并行 子代理
- 修复 内存 泄漏 in long-运行中 会话 where 流 资源 were not cleaned up 之后 shell 命令 完成
- 修复 `@` symbol incorrectly triggering 文件 autocomplete 建议 in bash mode
- 修复 `@`-mention 菜单 文件夹 click behavior to navigate 进入 directories 而不是 selecting them
- 修复 `/feedback` 命令 generating 无效 GitHub 问题 URLs 当 description is very long
- 修复 `/上下文` 命令 to 显示 the same 令牌 count 和 percentage as the status line in verbose mode
- 修复 an 问题 where `/config`, `/上下文`, `/模型`, 和 `/todos` 命令 overlays could 关闭 unexpectedly
- 修复 slash 命令 autocomplete selecting wrong 命令 当 typing similar 命令 (e.g., `/上下文` vs `/压缩`)
- 修复 inconsistent back navigation in 插件 marketplace 当 only one marketplace is configured
- 修复 iTerm2 progress bar not clearing properly on 退出, preventing lingering indicators 和 bell sounds
- 改进 backspace to 删除 pasted 文本 as a single 令牌 而不是 one character at a time
- [VSCode] 新增 `/usage` 命令 to 显示 当前 plan usage

## 2.1.12

- 修复 消息 渲染 缺陷

## 2.1.11

- 修复 excessive MCP 连接 请求 用于 HTTP/SSE transports

## 2.1.10

- 新增 新 `设置` 钩子 事件 that can be triggered 通过 `--init`, `--init-only`, 或 `--maintenance` CLI 标志 用于 仓库 设置 和 maintenance operations
- 新增 键盘 shortcut 'c' to 复制 OAuth URL 当 browser doesn't 打开 automatically 期间 login
- 修复 a 崩溃 当 运行中 bash 命令 containing heredocs 与 JavaScript 模板 literals like `${索引 + 1}`
- 改进 启动 to capture keystrokes typed 之前 the REPL is fully ready
- 改进 文件 建议 to 显示 as removable attachments 而不是 inserting 文本 当 accepted
- [VSCode] 新增 安装 count 显示 to 插件 listings
- [VSCode] 新增 trust 警告 当 installing 插件

## 2.1.9

- 新增 `auto:N` syntax 用于 configuring the MCP 工具 搜索 auto-启用 阈值, where N is the 上下文窗口 percentage (0-100)
- 新增 `plansDirectory` 设置 to customize where plan 文件 are 已存储
- 新增 外部 editor support (Ctrl+G) in AskUserQuestion "Other" 输入 字段
- 新增 会话 URL attribution to commits 和 PRs created 从 web 会话
- 新增 support 用于 `PreToolUse` 钩子 to return `additionalContext` to the 模型
- 新增 `${CLAUDE_SESSION_ID}` 字符串 substitution 用于 skills to 访问 the 当前 会话 ID
- 修复 long 会话 与 并行 工具 calls failing 与 an API 错误 about orphan tool_result 块
- 修复 MCP 服务器 reconnection hanging 当 cached 连接 promise never resolves
- 修复 Ctrl+Z suspend not working in terminals 使用 Kitty 键盘 协议 (Ghostty, iTerm2, kitty, WezTerm)

## 2.1.7

- 新增 `showTurnDuration` 设置 to 隐藏 turn duration 消息 (e.g., "Cooked 用于 1m 6s")
- 新增 ability to provide feedback 当 accepting 权限 prompts
- 新增 内联 显示 of 代理's 最终 响应 in 任务 通知, making it easier to see results 无 reading the full 转录 文件
- 修复 安全 漏洞 where wildcard 权限 rules could 匹配 compound 命令 containing shell operators
- 修复 false "文件 modified" 错误 on Windows 当 cloud 同步 工具, antivirus scanners, 或 git touch 文件 timestamps 无 changing content
- 修复 orphaned tool_result 错误 当 sibling 工具 失败 期间 流式 执行
- 修复 上下文窗口 blocking 限制 being calculated 使用 the full 上下文窗口 而不是 the effective 上下文窗口 (which reserves space 用于 max 输出 令牌)
- 修复 加载动画 briefly flashing 当 运行中 本地 slash 命令 like `/模型` 或 `/theme`
- 修复 终端 title animation jitter by 使用 修复-width braille characters
- 修复 插件 与 git submodules not being fully initialized 当 installed
- 修复 bash 命令 failing on Windows 当 temp 目录 路径 contained characters like `t` 或 `n` that were misinterpreted as 转义 sequences
- 改进 typing responsiveness by reducing 内存 allocation 开销 in 终端 渲染
- 已启用 MCP 工具 搜索 自动模式 by 默认 用于 all 用户. 当 MCP 工具 descriptions exceed 10% of the 上下文窗口, they are automatically deferred 和 discovered 通过 the MCPSearch 工具 而不是 being loaded upfront. This reduces 上下文 usage 用于 用户 与 many MCP 工具 configured. 用户 can 禁用 this by adding `MCPSearch` to `disallowedTools` in their 设置.
- 更改 OAuth 和 API Console URLs 从 console.Anthropic.com to platform.Claude.com
- [VSCode] 修复 `claudeProcessWrapper` 设置 passing the wrapper 路径 而不是 the Claude 二进制 路径

## 2.1.6

- 新增 搜索 functionality to `/config` 命令 用于 quickly filtering 设置
- 新增 Updates 部分 to `/doctor` showing auto-更新 channel 和 可用 npm 版本 (稳定/最新)
- 新增 date 范围 filtering to `/stats` 命令 - press `r` to cycle between 最后 7 天, 最后 30 天, 和 All time
- 新增 automatic discovery of skills 从 nested `.Claude/skills` directories 当 working 与 文件 in subdirectories
- 新增 `context_window.used_percentage` 和 `context_window.remaining_percentage` fields to status line 输入 用于 easier 上下文窗口 显示
- 新增 an 错误 显示 当 the editor fails 期间 Ctrl+G
- 修复 权限 绕过 通过 shell line continuation that could 允许 blocked 命令 to 执行
- 修复 false "文件 has been unexpectedly modified" 错误 当 文件 watchers touch 文件 无 changing content
- 修复 文本 styling (bold, colors) getting progressively misaligned in multi-line 响应
- 修复 the feedback 面板 closing unexpectedly 当 typing 'n' in the description 字段
- 修复 速率限制 警告 appearing at low usage 之后 weekly reset (现在 requires 70% usage)
- 修复 速率限制 选项 菜单 incorrectly auto-opening 当 resuming a 上一个 会话
- 修复 numpad 键 outputting 转义 sequences 而不是 characters in Kitty 键盘 协议 terminals
- 修复 选项+Return not inserting newlines in Kitty 键盘 协议 terminals
- 修复 corrupted config 备份 文件 accumulating in the home 目录 (现在 only one 备份 is created per config 文件)
- 修复 `MCP 列表` 和 `MCP get` 命令 leaving orphaned MCP 服务器 流程
- 修复 visual artifacts in ink2 mode 当 节点 become hidden 通过 `显示:none`
- 改进 the 外部 Claude.md imports approval 对话框 to 显示 which 文件 are being imported 和 从 where
- 改进 the `/任务` 对话框 to go directly to 任务 details 当 there's only one background 任务 运行中
- 改进 @ autocomplete 与 icons 用于 different 建议 类型 和 single-line formatting
- Updated "Help improve Claude" 设置 fetch to 刷新 OAuth 和 重试 当 it fails 由于 a stale OAuth 令牌
- 更改 任务 通知 显示 to cap at 3 lines 与 overflow summary 当 multiple background 任务 完成 simultaneously
- 更改 终端 title to "Claude 代码" on 启动 用于 better 窗口 identification
- 移除 ability to @-mention MCP 服务器 to 启用/禁用 - use `/MCP 启用 <name>` instead
- [VSCode] 修复 usage indicator not updating 之后 manual 压缩

## 2.1.5

- 新增 `CLAUDE_CODE_TMPDIR` 环境 变量 to 覆盖 the temp 目录 used 用于 内部 temp 文件, useful 用于 environments 与 自定义 temp 目录 需求

## 2.1.4

- 新增 `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` 环境 变量 to 禁用 all background 任务 functionality 包括 auto-backgrounding 和 the Ctrl+B shortcut
- 修复 "Help improve Claude" 设置 fetch to 刷新 OAuth 和 重试 当 it fails 由于 a stale OAuth 令牌

## 2.1.3

- Merged slash 命令 和 skills, simplifying the mental 模型 与 no 更改 in behavior
- 新增 发布 channel (`稳定` 或 `最新`) toggle to `/config`
- 新增 detection 和 警告 用于 unreachable 权限 rules, 与 警告 in `/doctor` 和 之后 saving rules that include the 源 of each rule 和 actionable 修复 guidance
- 修复 plan 文件 persisting across `/清除` 命令, 现在 ensuring a fresh plan 文件 is used 之后 clearing a conversation
- 修复 false skill 复制 detection on filesystems 与 large inodes (e.g., ExFAT) by 使用 64-bit precision 用于 inode 值
- 修复 mismatch between background 任务 count in status bar 和 项 shown in 任务 对话框
- 修复 sub-代理 使用 the wrong 模型 期间 conversation compaction
- 修复 web 搜索 in sub-代理 使用 incorrect 模型
- 修复 trust 对话框 acceptance 当 运行中 从 the home 目录 not enabling trust-requiring 功能 like 钩子 期间 the 会话
- 改进 终端 渲染 stability by preventing uncontrolled writes 从 corrupting 光标 state
- 改进 slash 命令 建议 readability by truncating long descriptions to 2 lines
- 更改 工具 钩子 执行 超时 从 60 秒 to 10 分钟
- [VSCode] 新增 clickable destination selector 用于 权限 请求, allowing you to choose where 设置 are saved (this 项目, all projects, shared 与 团队, 或 会话 only)

## 2.1.2

- 新增 源 路径 元数据 to images dragged onto the 终端, helping Claude understand where images originated
- 新增 clickable hyperlinks 用于 文件 路径 in 工具 输出 in terminals that support OSC 8 (like iTerm)
- 新增 support 用于 Windows 包 Manager (winget) installations 与 automatic detection 和 更新 instructions
- 新增 Shift+标签页 键盘 shortcut in 计划模式 to quickly select "auto-accept edits" 选项
- 新增 `FORCE_AUTOUPDATE_PLUGINS` 环境 变量 to 允许 插件 autoupdate even 当 the main auto-updater is 已禁用
- 新增 `agent_type` to SessionStart 钩子 输入, populated if `--代理` is specified
- 修复 a 命令 injection 漏洞 in bash 命令 processing where malformed 输入 could 执行 arbitrary 命令
- 修复 a 内存 泄漏 where 树-sitter 解析 树 were not being freed, causing WASM 内存 to grow unbounded over long 会话
- 修复 二进制 文件 (images, PDFs, etc.) being accidentally included in 内存 当 使用 `@include` directives in Claude.md 文件
- 修复 updates incorrectly claiming another 安装 is in progress
- 修复 崩溃 当 socket 文件 exist in watched directories (defense-in-depth 用于 EOPNOTSUPP 错误)
- 修复 远程 会话 URL 和 teleport being broken 当 使用 `/任务` 命令
- 修复 MCP 工具 names being exposed in analytics 事件 by sanitizing user-specific 服务器 配置
- 改进 选项-as-Meta 提示 on macOS to 显示 终端-specific instructions 用于 原生 CSIu terminals like iTerm2, Kitty, 和 WezTerm
- 改进 错误 消息 当 pasting images over SSH to suggest 使用 `scp` 而不是 the unhelpful 剪贴板 shortcut 提示
- 改进 权限 explainer to not 标志 routine dev 工作流 (git fetch/rebase, npm 安装, tests, PRs) as medium risk
- 更改 large bash 命令 outputs to be saved to disk 而不是 truncated, allowing Claude to 读取 the full content
- 更改 large 工具 outputs to be 已持久化 to disk 而不是 truncated, providing full 输出 访问 通过 文件 references
- 更改 `/插件` installed 标签页 to unify 插件 和 MCPs 与 作用域-基于 grouping
- 弃用 Windows managed 设置 路径 `C:\ProgramData\ClaudeCode\managed-设置.JSON` - administrators should 迁移 to `C:\程序 文件\ClaudeCode\managed-设置.JSON`
- [SDK] 更改 minimum zod peer dependency to ^4.0.0
- [VSCode] 修复 usage 显示 not updating 之后 manual 压缩

## 2.1.0

- 新增 automatic skill hot-重新加载 - skills created 或 modified in `~/.Claude/skills` 或 `.Claude/skills` are 现在 immediately 可用 无 restarting the 会话
- 新增 support 用于 运行中 skills 和 slash 命令 in a 已分叉 sub-代理 上下文 使用 `上下文: 分叉` in skill frontmatter
- 新增 support 用于 `代理` 字段 in skills to specify 代理 类型 用于 执行
- 新增 `language` 设置 to 配置 Claude's 响应 language (e.g., language: "japanese")
- 更改 Shift+Enter to work out of the box in iTerm2, WezTerm, Ghostty, 和 Kitty 无 modifying 终端 configs
- 新增 `respectGitignore` support in `设置.JSON` 用于 per-项目 control over @-mention 文件 picker behavior
- 新增 `IS_DEMO` 环境 变量 to 隐藏 email 和 组织 从 the UI, useful 用于 流式 或 recording 会话
- 修复 安全 问题 where sensitive data (OAuth 令牌, API 键, passwords) could be exposed in 调试 日志
- 修复 文件 和 skills not being properly discovered 当 resuming 会话 与 `-c` 或 `--恢复`
- 修复 pasted content being lost 当 replaying prompts 从 history 使用 up arrow 或 Ctrl+R 搜索
- 修复 Esc 键 与 queued prompts to only 移动 them to 输入 无 canceling the 运行中 任务
- Reduced 权限 prompts 用于 complex bash 命令
- 修复 命令 搜索 to prioritize exact 和 前缀 matches on 命令 names over fuzzy matches in descriptions
- 修复 PreToolUse 钩子 to 允许 `updatedInput` 当 returning `ask` 权限 decision, enabling 钩子 to act as middleware 当 still requesting user consent
- 修复 插件 路径 resolution 用于 文件-基于 marketplace sources
- 修复 LSP 工具 being incorrectly 已启用 当 no LSP 服务器 were configured
- 修复 background 任务 failing 与 "git 仓库 not found" 错误 用于 repositories 与 dots in their names
- 修复 Claude in Chrome support 用于 WSL environments
- 修复 Windows 原生 installer silently failing 当 executable creation fails
- 改进 CLI help 输出 to 显示 选项 和 subcommands in alphabetical order 用于 easier navigation
- 新增 wildcard 模式 matching 用于 Bash 工具 权限 使用 `*` at any 位置 in rules (e.g., `Bash(npm *)`, `Bash(* 安装)`, `Bash(git * main)`)
- 新增 unified Ctrl+B backgrounding 用于 both bash 命令 和 代理 - pressing Ctrl+B 现在 backgrounds all 运行中 foreground 任务 simultaneously
- 新增 support 用于 MCP `list_changed` 通知, allowing MCP 服务器 to dynamically 更新 their 可用 工具, prompts, 和 资源 无 requiring reconnection
- 新增 `/teleport` 和 `/远程-环境变量` slash 命令 用于 Claude.ai subscribers, allowing them to 恢复 和 配置 远程 会话
- 新增 support 用于 disabling specific 代理 使用 `任务(AgentName)` syntax in 设置.JSON 权限 或 the `--disallowedTools` CLI 标志
- 新增 钩子 support to 代理 frontmatter, allowing 代理 to define PreToolUse, PostToolUse, 和 停止 钩子 scoped to the 代理's lifecycle
- 新增 钩子 support 用于 skill 和 slash 命令 frontmatter
- 新增 新 Vim motions: `;` 和 `,` to repeat f/F/t/T motions, `y` operator 用于 yank 与 `yy`/`Y`, `p`/`P` 用于 粘贴, 文本 对象 (`iw`, `aw`, `iW`, `aW`, `i"`, `a"`, `i'`, `a'`, `i(`, `a(`, `i[`, `a[`, `i{`, `a{`), `>>` 和 `<<` 用于 indent/dedent, 和 `J` to 连接 lines
- 新增 `/plan` 命令 shortcut to 启用 计划模式 directly 从 the 提示
- 新增 slash 命令 autocomplete support 当 `/` appears anywhere in 输入, not just at the beginning
- 新增 `--工具` 标志 support in interactive mode to restrict which 内置 工具 Claude can use 期间 interactive 会话
- 新增 `CLAUDE_CODE_FILE_READ_MAX_OUTPUT_TOKENS` 环境 变量 to 覆盖 the 默认 文件 读取 令牌 限制
- 新增 support 用于 `once: true` config 用于 钩子
- 新增 support 用于 YAML-style lists in frontmatter `允许-工具` 字段 用于 cleaner skill declarations
- 新增 support 用于 提示 和 代理 钩子 类型 从 插件 (previously only 命令 钩子 were 支持)
- 新增 Cmd+V support 用于 image 粘贴 in iTerm2 (maps to Ctrl+V)
- 新增 left/right arrow 键 navigation 用于 cycling through 标签页 in dialogs
- 新增 real-time thinking 块 显示 in Ctrl+O 转录 mode
- 新增 filepath to full 输出 in background bash 任务 details 对话框
- 新增 Skills as a separate 类别 in the 上下文 visualization
- 修复 OAuth 令牌 刷新 not triggering 当 服务器 reports 令牌 expired but 本地 expiration check disagrees
- 修复 会话 persistence getting stuck 之后 transient 服务器 错误 by recovering 从 409 conflicts 当 the 条目 was actually 已存储
- 修复 会话 恢复 失败 caused by orphaned 工具 results 期间 并发 工具 执行
- 修复 a race 条件 where stale OAuth 令牌 could be 读取 从 the keychain 缓存 期间 并发 令牌 刷新 attempts
- 修复 AWS Bedrock 子代理 not inheriting EU/APAC cross-region inference 模型 配置, causing 403 错误 当 IAM 权限 are scoped to specific regions
- 修复 API 上下文 overflow 当 background 任务 produce large 输出 by truncating to 30K chars 与 文件 路径 引用
- 修复 a hang 当 reading FIFO 文件 by skipping symlink resolution 用于 special 文件 类型
- 修复 终端 键盘 mode not being reset on 退出 in Ghostty, iTerm2, Kitty, 和 WezTerm
- 修复 Alt+B 和 Alt+F (word navigation) not working in iTerm2, Ghostty, Kitty, 和 WezTerm
- 修复 `${CLAUDE_PLUGIN_ROOT}` not being substituted in 插件 `允许-工具` frontmatter, which caused 工具 to incorrectly require approval
- 修复 文件 created by the 写入 工具 使用 hardcoded 0o600 权限 而不是 respecting the 系统 umask
- 修复 命令 与 `$()` 命令 substitution failing 与 解析 错误
- 修复 multi-line bash 命令 与 backslash continuations being incorrectly 分割 和 flagged 用于 权限
- 修复 bash 命令 前缀 extraction to correctly identify subcommands 之后 全局 选项 (e.g., `git -C /路径 日志` 现在 correctly matches `Bash(git 日志:*)` rules)
- 修复 slash 命令 passed as CLI arguments (e.g., `Claude /上下文`) not being executed properly
- 修复 pressing Enter 之后 标签页-completing a slash 命令 selecting a different 命令 而不是 submitting the 完成 one
- 修复 slash 命令 参数 提示 flickering 和 inconsistent 显示 当 typing 命令 与 arguments
- 修复 Claude sometimes redundantly invoking the Skill 工具 当 运行中 slash 命令 directly
- 修复 skill 令牌 estimates in `/上下文` to accurately reflect frontmatter-only loading
- 修复 子代理 sometimes not inheriting the parent's 模型 by 默认
- 修复 模型 picker showing incorrect selection 用于 Bedrock/Vertex 用户 使用 `--模型 Haiku`
- 修复 复制 Bash 命令 appearing in 权限 请求 选项 labels
- 修复 noisy 输出 当 background 任务 完成 - 现在 shows clean completion 消息 而不是 原始 输出
- 修复 background 任务 completion 通知 to appear proactively 与 bullet point
- 修复 已分叉 slash 命令 showing "AbortError" 而不是 "Interrupted" 消息 当 cancelled
- 修复 光标 disappearing 之后 dismissing 权限 dialogs
- 修复 `/钩子` 菜单 selecting wrong 钩子 类型 当 滚动 to a different 选项
- 修复 images in queued prompts showing as "[对象 对象]" 当 pressing Esc to 取消
- 修复 images being silently dropped 当 queueing 消息 当 backgrounding a 任务
- 修复 large pasted images failing 与 "Image was too large" 错误
- 修复 extra 空白 lines in multiline prompts containing CJK characters (Japanese, Chinese, Korean)
- 修复 超深度思考 keyword highlighting being applied to wrong characters 当 user 提示 文本 wraps to multiple lines
- 修复 collapsed "Reading X 文件…" indicator incorrectly switching to past tense 当 thinking 块 appear mid-流
- 修复 Bash 读取 命令 (like `ls` 和 `cat`) not being counted in collapsed 读取/搜索 组, causing 组 to incorrectly 显示 "读取 0 文件"
- 修复 加载动画 令牌 counter to properly accumulate 令牌 从 子代理 期间 执行
- 修复 内存 泄漏 in git diff 解析中 where sliced strings retained large parent strings
- 修复 race 条件 where LSP 工具 could return "no 服务器 可用" 期间 启动
- 修复 feedback submission hanging indefinitely 当 网络 请求 超时
- 修复 搜索 mode in 插件 discovery 和 日志 selector views exiting 当 pressing up arrow
- 修复 钩子 成功 消息 showing trailing colon 当 钩子 has no 输出
- Multiple 优化 to improve 启动 性能
- 改进 终端 渲染 性能 当 使用 原生 installer 或 Bun, especially 用于 文本 与 emoji, ANSI codes, 和 Unicode characters
- 改进 性能 当 reading Jupyter notebooks 与 many cells
- 改进 可靠性 用于 piped 输入 like `cat refactor.md | Claude`
- 改进 可靠性 用于 AskQuestion 工具
- 改进 sed in-place 编辑 命令 to 渲染 as 文件 edits 与 diff 预览
- 改进 Claude to automatically 继续 当 响应 is cut off 由于 输出 令牌 限制, 而不是 showing an 错误 消息
- 改进 compaction 可靠性
- 改进 子代理 (任务 工具) to 继续 working 之后 权限 denial, allowing them to try 替代方案 方法
- 改进 skills to 显示 progress 当 executing, displaying 工具 uses as they happen
- 改进 skills 从 `/skills/` directories to be visible in the slash 命令 菜单 by 默认 (opt-out 与 `user-invocable: false` in frontmatter)
- 改进 skill 建议 to prioritize recently 和 frequently used skills
- 改进 加载动画 feedback 当 waiting 用于 the 第一 响应 令牌
- 改进 令牌 count 显示 in 加载动画 to include 令牌 从 background 代理
- 改进 incremental 输出 用于 异步 代理 to give the main 线程 more control 和 visibility
- 改进 权限 提示 UX 与 标签页 提示 moved to footer, cleaner Yes/No 输入 labels 与 contextual placeholders
- 改进 the Claude in Chrome 通知 与 shortened help 文本 和 persistent 显示 直到 dismissed
- 改进 macOS screenshot 粘贴 可靠性 与 TIFF 格式 support
- 改进 `/stats` 输出
- Updated Atlassian MCP 集成 to use a more 可靠 默认 配置 (streamable HTTP)
- 更改 "Interrupted" 消息 color 从 red to grey 用于 a less alarming appearance
- 移除 权限 提示 当 entering 计划模式 - 用户 can 现在 enter 计划模式 无 approval
- 移除 underline styling 从 image 引用 links
- [SDK] 更改 minimum zod peer dependency to ^4.0.0
- [VSCode] 新增 currently selected 模型 name to the 上下文 菜单
- [VSCode] 新增 descriptive labels on auto-accept 权限 按钮 (e.g., "Yes, 允许 npm 用于 this 项目" 而不是 "Yes, 和 don't ask again")
- [VSCode] 修复 paragraph breaks not 渲染 in markdown content
- [VSCode] 修复 滚动 in the extension inadvertently 滚动 the parent iframe
- [Windows] 修复 问题 与 improper 渲染

## 2.0.76

- 修复 问题 与 macOS 代码-签名 警告 当 使用 Claude in Chrome 集成

## 2.0.75

- Minor bugfixes

## 2.0.74

- 新增 LSP (Language 服务器 协议) 工具 用于 代码 intelligence 功能 like go-to-definition, 查找 references, 和 hover 文档
- 新增 `/终端-设置` support 用于 Kitty, Alacritty, Zed, 和 Warp terminals
- 新增 ctrl+t shortcut in `/theme` to toggle syntax highlighting on/off
- 新增 syntax highlighting info to theme picker
- 新增 guidance 用于 macOS 用户 当 Alt shortcuts 失败 由于 终端 配置
- 修复 skill `允许-工具` not being applied to 工具 invoked by the skill
- 修复 Opus 4.5 提示 incorrectly showing 当 user was already 使用 Opus
- 修复 a potential 崩溃 当 syntax highlighting isn't initialized correctly
- 修复 visual 缺陷 in `/插件 discover` where 列表 selection indicator showed 当 搜索 box was focused
- 修复 macOS 键盘 shortcuts to 显示 'opt' 而不是 'alt'
- 改进 `/上下文` 命令 visualization 与 grouped skills 和 代理 by 源, slash 命令, 和 sorted 令牌 count
- [Windows] 修复 问题 与 improper 渲染
- [VSCode] 新增 gift tag pictogram 用于 year-end promotion 消息

## 2.0.73

- 新增 clickable `[Image #N]` links that 打开 attached images in the 默认 viewer
- 新增 alt-y yank-pop to cycle through 终止 ring history 之后 ctrl-y yank
- 新增 搜索 filtering to the 插件 discover 屏幕 (类型 to 过滤 by name, description, 或 marketplace)
- 新增 support 用于 自定义 会话 IDs 当 forking 会话 与 `--会话-ID` combined 与 `--恢复` 或 `--继续` 和 `--分叉-会话`
- 修复 慢 输入 history cycling 和 race 条件 that could overwrite 文本 之后 消息 submission
- 改进 `/theme` 命令 to 打开 theme picker directly
- 改进 theme picker UI
- 改进 搜索 UX across 恢复 会话, 权限, 和 插件 screens 与 a unified SearchBox 组件
- [VSCode] 新增 标签页 icon badges showing 待处理 权限 (blue) 和 unread completions (orange)

## 2.0.72

- 新增 Claude in Chrome (测试版) 功能 that works 与 the Chrome extension (HTTPS://Claude.ai/Chrome) to let you control your browser directly 从 Claude 代码
- Reduced 终端 flickering
- 新增 scannable QR 代码 to mobile 应用 提示 用于 quick 应用 downloads
- 新增 loading indicator 当 resuming conversations 用于 better feedback
- 修复 `/上下文` 命令 not respecting 自定义 系统 prompts in non-interactive mode
- 修复 order of consecutive Ctrl+K lines 当 pasting 与 Ctrl+Y
- 改进 @ mention 文件 建议 speed (~3× 更快 in git repositories)
- 改进 文件 建议 性能 in repos 与 `.ignore` 或 `.rgignore` 文件
- 改进 设置 validation 错误 to be more prominent
- 更改 thinking toggle 从 标签页 to Alt+T to avoid accidental triggers

## 2.0.71

- 新增 /config toggle to 启用/禁用 提示 建议
- 新增 `/设置` as an alias 用于 the `/config` 命令
- 修复 @ 文件 引用 建议 incorrectly triggering 当 光标 is in the middle of a 路径
- 修复 MCP 服务器 从 `.MCP.JSON` not loading 当 使用 `--dangerously-跳过-权限`
- 修复 权限 rules incorrectly rejecting 有效 bash 命令 containing shell glob 模式 (e.g., `ls *.txt`, `用于 f in *.png`)
- Bedrock: 环境 变量 `ANTHROPIC_BEDROCK_BASE_URL` is 现在 respected 用于 令牌 counting 和 inference 分析 listing
- 新 syntax highlighting engine 用于 原生 构建

## 2.0.70

- 新增 Enter 键 to accept 和 提交 提示 建议 immediately (标签页 still accepts 用于 editing)
- 新增 wildcard syntax `mcp__server__*` 用于 MCP 工具 权限 to 允许 或 拒绝 all 工具 从 a 服务器
- 新增 auto-更新 toggle 用于 插件 marketplaces, allowing per-marketplace control over automatic updates
- 新增 `current_usage` 字段 to status line 输入, enabling accurate 上下文窗口 percentage calculations
- 修复 输入 being cleared 当 processing queued 命令 当 the user was typing
- 修复 提示 建议 replacing typed 输入 当 pressing 标签页
- 修复 diff 视图 not updating 当 终端 is resized
- 改进 内存 usage by 3x 用于 large conversations
- 改进 resolution of stats screenshots copied to 剪贴板 (Ctrl+S) 用于 crisper images
- 移除 # shortcut 用于 quick 内存 条目 (tell Claude to 编辑 your Claude.md instead)
- 修复 thinking mode toggle in /config not persisting correctly
- Improve UI 用于 文件 creation 权限 对话框

## 2.0.69

- Minor bugfixes

## 2.0.68

- 修复 IME (输入 方法 Editor) support 用于 languages like Chinese, Japanese, 和 Korean by correctly positioning the composition 窗口 at the 光标
- 修复 a 缺陷 where disallowed MCP 工具 were visible to the 模型
- 修复 an 问题 where steering 消息 could be lost 当 a 子代理 is working
- 修复 选项+Arrow word navigation treating entire CJK (Chinese, Japanese, Korean) 文本 sequences as a single word 而不是 navigating by word boundaries
- 改进 计划模式 退出 UX: 显示 simplified yes/no 对话框 当 exiting 与 空 或 缺失 plan 而不是 throwing an 错误
- 添加 support 用于 企业 managed 设置. Contact your Anthropic account 团队 to 启用 this 功能.

## 2.0.67

- Thinking mode is 现在 已启用 by 默认 用于 Opus 4.5
- Thinking mode 配置 has moved to /config
- 新增 搜索 functionality to `/权限` 命令 与 `/` 键盘 shortcut 用于 filtering rules by 工具 name
- 显示 reason why autoupdater is 已禁用 in `/doctor`
- 修复 false "Another 流程 is currently updating Claude" 错误 当 运行中 `Claude 更新` 当 another 实例 is already on the 最新 版本
- 修复 MCP 服务器 从 `.MCP.JSON` being stuck in 待处理 state 当 运行中 in non-interactive mode (`-p` 标志 或 piped 输入)
- 修复 滚动 位置 resetting 之后 deleting a 权限 rule in `/权限`
- 修复 word deletion (opt+删除) 和 word navigation (opt+arrow) not working correctly 与 non-Latin 文本 例如 Cyrillic, Greek, Arabic, Hebrew, Thai, 和 Chinese
- 修复 `Claude 安装 --force` not bypassing stale 锁定 文件
- 修复 consecutive @~/ 文件 references in Claude.md being incorrectly 已解析 由于 markdown strikethrough interference
- Windows: 修复 插件 MCP 服务器 failing 由于 colons in 日志 目录 路径

## 2.0.65

- 新增 ability to switch 模型 当 writing a 提示 使用 alt+p (Linux, Windows), 选项+p (macOS).
- 新增 上下文窗口 information to status line 输入
- 新增 `fileSuggestion` 设置 用于 自定义 `@` 文件 搜索 命令
- 新增 `CLAUDE_CODE_SHELL` 环境 变量 to 覆盖 automatic shell detection (useful 当 login shell differs 从 actual working shell)
- 修复 提示 not being saved to history 当 aborting a 查询 与 转义
- 修复 读取 工具 image handling to identify 格式 从 bytes 而不是 文件 extension

## 2.0.64

- Made auto-compacting instant
- 代理 和 bash 命令 can run asynchronously 和 发送 消息 to wake up the main 代理
- /stats 现在 provides 用户 与 interesting CC stats, 例如 favorite 模型, usage 图, usage streak
- 新增 named 会话 support: use `/rename` to name 会话, `/恢复 <name>` in REPL 或 `Claude --恢复 <name>` 从 the 终端 to 恢复 them
- 新增 support 用于 .Claude/rules/`.  See HTTPS://代码.Claude.com/文档/en/内存 用于 details.
- 新增 image dimension 元数据 当 images are resized, enabling accurate coordinate mappings 用于 large images
- 修复 auto-loading .环境变量 当 使用 原生 installer
- 修复 `--系统-提示` being ignored 当 使用 `--继续` 或 `--恢复` 标志
- 改进 `/恢复` 屏幕 与 grouped 已分叉 会话 和 键盘 shortcuts 用于 预览 (P) 和 rename (R)
- VSCode: 新增 复制-to-剪贴板 按钮 on 代码 块 和 bash 工具 inputs
- VSCode: 修复 extension not working on Windows ARM64 by falling back to x64 二进制 通过 emulation
- Bedrock: Improve efficiency of 令牌 counting
- Bedrock: 添加 support 用于 `AWS login` AWS Management Console credentials
- Unshipped AgentOutputTool 和 BashOutputTool, in favor of a 新 unified TaskOutputTool

## 2.0.62

- 新增 "(Recommended)" indicator 用于 multiple-选择 questions, 与 the recommended 选项 moved to the top of the 列表
- 新增 `attribution` 设置 to customize 提交 和 PR bylines (deprecates `includeCoAuthoredBy`)
- 修复 复制 slash 命令 appearing 当 ~/.Claude is symlinked to a 项目 目录
- 修复 slash 命令 selection not working 当 multiple 命令 share the same name
- 修复 an 问题 where skill 文件 inside symlinked skill directories could become circular symlinks
- 修复 运行中 版本 getting 移除 因为 锁定 文件 incorrectly going stale
- 修复 IDE diff 标签页 not closing 当 rejecting 文件 更改

## 2.0.61

- 已回退 VSCode support 用于 multiple 终端 clients 由于 responsiveness 问题.

## 2.0.60

- 新增 background 代理 support. 代理 run in the background 当 you work
- 新增 --禁用-slash-命令 CLI 标志 to 禁用 all slash 命令
- 新增 模型 name to "Co-Authored-By" 提交 消息
- 已启用 "/MCP 启用 [服务器-name]" 或 "/MCP 禁用 [服务器-name]" to quickly toggle all 服务器
- Updated Fetch to 跳过 summarization 用于 pre-approved websites
- VSCode: 新增 support 用于 multiple 终端 clients connecting to the IDE 服务器 simultaneously

## 2.0.59

- 新增 --代理 CLI 标志 to 覆盖 the 代理 设置 用于 the 当前 会话
- 新增 `代理` 设置 to 配置 main 线程 与 a specific 代理's 系统 提示, 工具 restrictions, 和 模型
- VS 代码: 修复 .Claude.JSON config 文件 being 读取 从 incorrect location

## 2.0.58

- Pro 用户 现在 have 访问 to Opus 4.5 as part of their subscription!
- 修复 timer duration showing "11m 60s" 而不是 "12m 0s"
- Windows: Managed 设置 现在 prefer `C:\程序 文件\ClaudeCode` if it 存在. Support 用于 `C:\ProgramData\ClaudeCode` will be 移除 in a future 版本.

## 2.0.57

- 新增 feedback 输入 当 rejecting plans, allowing 用户 to tell Claude what to 更改
- VSCode: 新增 流式 消息 support 用于 real-time 响应 显示

## 2.0.56

- 新增 设置 to 启用/禁用 终端 progress bar (OSC 9;4)
- VSCode Extension: 新增 support 用于 VS 代码's secondary sidebar (VS 代码 1.97+), allowing Claude 代码 to be displayed in the right sidebar 当 keeping the 文件 explorer on the left. Requires 设置 sidebar as Preferred Location in the config.

## 2.0.55

- 修复 代理 DNS resolution being forced on by 默认. 现在 opt-in 通过 `CLAUDE_CODE_PROXY_RESOLVES_HOSTS=true` 环境 变量
- 修复 键盘 navigation becoming unresponsive 当 holding down arrow 键 in 内存 location selector
- 改进 AskUserQuestion 工具 to auto-提交 single-select questions on the 最后 question, eliminating the extra review 屏幕 用于 simple question flows
- 改进 fuzzy matching 用于 `@` 文件 建议 与 更快, more accurate results

## 2.0.54

- 钩子: 启用 PermissionRequest 钩子 to 流程 'always 允许' 建议 和 apply 权限 updates
- 修复 问题 与 excessive iTerm 通知

## 2.0.52

- 修复 复制 消息 显示 当 starting Claude 与 a 命令 line 参数
- 修复 `/usage` 命令 progress bars to fill up as usage increases (而不是 showing remaining percentage)
- 修复 image pasting not working on Linux systems 运行中 Wayland (现在 falls back to wl-粘贴 当 xclip is 不可用)
- Permit some uses of `$!` in bash 命令

## 2.0.51

- 新增 Opus 4.5! HTTPS://www.Anthropic.com/news/Claude-Opus-4-5
- Introducing Claude 代码 用于 Desktop: HTTPS://Claude.com/下载
- To give you room to try out our 新 模型, we've updated usage 限制 用于 Claude 代码 用户. See the Claude Opus 4.5 blog 用于 full details
- Pro 用户 can 现在 purchase extra usage 用于 访问 to Opus 4.5 in Claude 代码
- 计划模式 现在 builds more precise plans 和 executes more thoroughly
- Usage 限制 通知 现在 easier to understand
- Switched `/usage` back to "% used"
- 修复 handling of thinking 错误
- 修复 性能 回归

## 2.0.50

- 修复 缺陷 preventing calling MCP 工具 that have nested references in their 输入 schemas
- Silenced a noisy but harmless 错误 期间 upgrades
- 改进 超深度思考 文本 显示
- 改进 clarity of 5-小时 会话 限制 警告 消息

## 2.0.49

- 新增 readline-style ctrl-y 用于 pasting deleted 文本
- 改进 clarity of usage 限制 警告 消息
- 修复 handling of 子代理 权限

## 2.0.47

- 改进 错误 消息 和 validation 用于 `Claude --teleport`
- 改进 错误 handling in `/usage`
- 修复 race 条件 与 history 条目 not getting logged at 退出
- 修复 Vertex AI 配置 not being applied 从 `设置.JSON`

## 2.0.46

- 修复 image 文件 being reported 与 incorrect media 类型 当 格式 cannot be detected 从 元数据

## 2.0.45

- 新增 support 用于 Microsoft Foundry! See HTTPS://代码.Claude.com/文档/en/azure-ai-Foundry
- 新增 `PermissionRequest` 钩子 to automatically approve 或 拒绝 工具 权限 请求 与 自定义 logic
- 发送 background 任务 to Claude 代码 on the web by starting a 消息 与 `&`

## 2.0.43

- 新增 `permissionMode` 字段 用于 自定义 代理
- 新增 `tool_use_id` 字段 to `PreToolUseHookInput` 和 `PostToolUseHookInput` 类型
- 新增 skills frontmatter 字段 to declare skills to auto-加载 用于 子代理
- 新增 the `SubagentStart` 钩子 事件
- 修复 nested `Claude.md` 文件 not loading 当 @-mentioning 文件
- 修复 复制 渲染 of some 消息 in the UI
- 修复 some visual flickers
- 修复 NotebookEdit 工具 inserting cells at incorrect positions 当 cell IDs matched the 模式 `cell-N`

## 2.0.42

- 新增 `agent_id` 和 `agent_transcript_path` fields to `SubagentStop` 钩子.

## 2.0.41

- 新增 `模型` 参数 to 提示-基于 停止 钩子, allowing 用户 to specify a 自定义 模型 用于 钩子 evaluation
- 修复 slash 命令 从 user 设置 being loaded twice, which could cause 渲染 问题
- 修复 incorrect labeling of user 设置 vs 项目 设置 in 命令 descriptions
- 修复 崩溃 当 插件 命令 钩子 超时 期间 执行
- 修复: Bedrock 用户 不再 see 复制 Opus 条目 in the /模型 picker 当 使用 `--模型 Haiku`
- 修复 broken 安全 文档 links in trust dialogs 和 onboarding
- 修复 问题 where pressing ESC to 关闭 the diff modal would also 中断 the 模型
- ctrl-r history 搜索 landing on a slash 命令 不再 cancels the 搜索
- SDK: Support 自定义 timeouts 用于 钩子
- 允许 more safe git 命令 to run 无 approval
- 插件: 新增 support 用于 sharing 和 installing 输出 styles
- Teleporting a 会话 从 web will automatically 集合 the upstream 分支

## 2.0.37

- 修复 how idleness is computed 用于 通知
- 钩子: 新增 matcher 值 用于 通知 钩子 事件
- 输出 Styles: 新增 `keep-coding-instructions` 选项 to frontmatter

## 2.0.36

- 修复: DISABLE_AUTOUPDATER 环境 变量 现在 properly disables 包 manager 更新 通知
- 修复 queued 消息 being incorrectly executed as bash 命令
- 修复 输入 being lost 当 typing 当 a queued 消息 is processed

## 2.0.35

- Improve fuzzy 搜索 results 当 searching 命令
- 改进 VS 代码 extension to respect `chat.fontSize` 和 `chat.fontFamily` 设置 throughout the entire UI, 和 apply font 更改 immediately 无 requiring 重新加载
- 新增 `CLAUDE_CODE_EXIT_AFTER_STOP_DELAY` 环境 变量 to automatically 退出 SDK mode 之后 a specified idle duration, useful 用于 automated 工作流 和 脚本
- Migrated `ignorePatterns` 从 项目 config to 拒绝 权限 in the localSettings.
- 修复 菜单 navigation getting stuck on 项 与 空 字符串 或 other falsy 值 (e.g., in the `/钩子` 菜单)

## 2.0.34

- VSCode Extension: 新增 设置 to 配置 the 初始 权限 mode 用于 新 conversations
- 改进 文件 路径 建议 性能 与 原生 Rust-基于 fuzzy finder
- 修复 infinite 令牌 刷新 loop that caused MCP 服务器 与 OAuth (e.g., Slack) to hang 期间 连接
- 修复 内存 崩溃 当 reading 或 writing large 文件 (especially base64-已编码 images)

## 2.0.33

- 原生 二进制 installs 现在 启动 quicker.
- 修复 `Claude doctor` incorrectly detecting Homebrew vs npm-全局 installations by properly resolving symlinks
- 修复 `Claude MCP serve` exposing 工具 与 incompatible outputSchemas

## 2.0.32

- Un-deprecate 输出 styles 基于 on community feedback
- 新增 `companyAnnouncements` 设置 用于 displaying announcements on 启动
- 修复 钩子 progress 消息 not updating correctly 期间 PostToolUse 钩子 执行

## 2.0.31

- Windows: 原生 安装 uses shift+标签页 as shortcut 用于 mode switching, 而不是 alt+m
- Vertex: 添加 support 用于 Web 搜索 on 支持 模型
- VSCode: Adding the respectGitIgnore 配置 to include .gitignored 文件 in 文件 searches (defaults to true)
- 修复 a 缺陷 与 子代理 和 MCP 服务器 related to "工具 names must be unique" 错误
- 修复 问题 causing `/压缩` to 失败 与 `prompt_too_long` by making it respect existing 压缩 boundaries
- 修复 插件 卸载 not removing 插件

## 2.0.30

- 新增 helpful 提示 to run `安全 解锁-keychain` 当 encountering API 键 错误 on macOS 与 locked keychain
- 新增 `allowUnsandboxedCommands` 沙盒 设置 to 禁用 the dangerouslyDisableSandbox 转义 hatch at policy 级别
- 新增 `disallowedTools` 字段 to 自定义 代理 definitions 用于 explicit 工具 blocking
- 新增 提示-基于 停止 钩子
- VSCode: 新增 respectGitIgnore 配置 to include .gitignored 文件 in 文件 searches (defaults to true)
- 已启用 SSE MCP 服务器 on 原生 构建
- 弃用 输出 styles. Review 选项 in `/输出-style` 和 use --系统-提示-文件, --系统-提示, --追加-系统-提示, Claude.md, 或 插件 instead
- 移除 support 用于 自定义 ripgrep 配置, resolving an 问题 where 搜索 returns no results 和 config discovery fails
- 修复 Explore 代理 creating unwanted .md investigation 文件 期间 codebase exploration
- 修复 a 缺陷 where `/上下文` would sometimes 失败 与 "max_tokens must be greater 比 thinking.budget_tokens" 错误 消息
- 修复 `--MCP-config` 标志 to correctly 覆盖 文件-基于 MCP 配置
- 修复 缺陷 that saved 会话 权限 to 本地 设置
- 修复 MCP 工具 not being 可用 to sub-代理
- 修复 钩子 和 插件 not executing 当 使用 --dangerously-跳过-权限 标志
- 修复 delay 当 navigating through typeahead 建议 与 arrow 键
- VSCode: Restored selection indicator in 输入 footer showing 当前 文件 或 代码 selection status

## 2.0.28

- 计划模式: introduced 新 Plan 子代理
- 子代理: Claude can 现在 choose to 恢复 子代理
- 子代理: Claude can dynamically choose the 模型 used by its 子代理
- SDK: 新增 --max-budget-usd 标志
- Discovery of 自定义 slash 命令, 子代理, 和 输出 styles 不再 respects .gitignore
- 停止 `/终端-设置` 从 adding backslash to `Shift + Enter` in VS 代码
- 添加 分支 和 tag support 用于 git-基于 插件 和 marketplaces 使用 片段 syntax (e.g., `owner/仓库#分支`)
- 修复 a 缺陷 where macOS 权限 prompts would 显示 up upon 初始 启动 当 launching 从 home 目录
- Various other 缺陷 fixes

## 2.0.27

- 新 UI 用于 权限 prompts
- 新增 当前 分支 filtering 和 搜索 to 会话 恢复 屏幕 用于 easier navigation
- 修复 目录 @-mention causing "No assistant 消息 found" 错误
- VSCode Extension: 添加 config 设置 to include .gitignored 文件 in 文件 searches
- VSCode Extension: 缺陷 fixes 用于 unrelated 'Warmup' conversations, 和 配置/设置 occasionally being reset to defaults

## 2.0.25

- 移除 legacy SDK entrypoint. Please 迁移 to @Anthropic-ai/Claude-代理-sdk 用于 future SDK updates: HTTPS://platform.Claude.com/文档/en/代理-sdk/migration-指南

## 2.0.24

- 修复 a 缺陷 where 项目-级别 skills were not loading 当 --设置-sources '项目' was specified
- Claude 代码 Web: Support 用于 Web -> CLI teleport
- 沙盒: Releasing a 沙盒 mode 用于 the BashTool on Linux & Mac
- Bedrock: 显示 awsAuthRefresh 输出 当 认证 is required

## 2.0.22

- 修复 content 布局 shift 当 滚动 through slash 命令
- IDE: 添加 toggle to 启用/禁用 thinking.
- 修复 缺陷 causing 复制 权限 prompts 与 并行 工具 calls
- 添加 support 用于 企业 managed MCP allowlist 和 denylist

## 2.0.21

- Support MCP `structuredContent` 字段 in 工具 响应
- 新增 an interactive question 工具
- Claude will 现在 ask you questions more often in 计划模式
- 新增 Haiku 4.5 as a 模型 选项 用于 Pro 用户
- 修复 an 问题 where queued 命令 don't have 访问 to 上一个 消息' 输出

## 2.0.20

- 新增 support 用于 Claude Skills

## 2.0.19

- Auto-background long-运行中 bash 命令 而不是 killing them. Customize 与 BASH_DEFAULT_TIMEOUT_MS
- 修复 a 缺陷 where Haiku was unnecessarily called in print mode

## 2.0.17

- 新增 Haiku 4.5 to 模型 selector!
- Haiku 4.5 automatically uses Sonnet in 计划模式, 和 Haiku 用于 执行 (i.e. SonnetPlan by 默认)
- 3P (Bedrock 和 Vertex) are not automatically upgraded yet. Manual upgrading can be done through 设置 `ANTHROPIC_DEFAULT_HAIKU_MODEL`
- Introducing the Explore 子代理. Powered by Haiku it'll 搜索 through your codebase efficiently to 保存 上下文!
- OTEL: support HTTP_PROXY 和 HTTPS_PROXY
- `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` 现在 disables 发布 备注 fetching

## 2.0.15

- 修复 缺陷 与 resuming where previously created 文件 needed to be 读取 again 之前 writing
- 修复 缺陷 与 `-p` mode where @-mentioned 文件 needed to be 读取 again 之前 writing

## 2.0.14

- 修复 @-mentioning MCP 服务器 to toggle them on/off
- Improve 权限 checks 用于 bash 与 内联 环境变量 vars
- 修复 超深度思考 + thinking toggle
- Reduce unnecessary logins
- Document --系统-提示
- Several 改进 to 渲染
- 插件 UI polish

## 2.0.13

- 修复 `/插件` not working on 原生 构建

## 2.0.12

- **插件 系统 Released**: Extend Claude 代码 与 自定义 命令, 代理, 钩子, 和 MCP 服务器 从 marketplaces
- `/插件 安装`, `/插件 启用/禁用`, `/插件 marketplace` 命令 用于 插件 management
- 仓库-级别 插件 配置 通过 `extraKnownMarketplaces` 用于 团队 collaboration
- `/插件 验证` 命令 用于 validating 插件 structure 和 配置
- 插件 announcement blog post at HTTPS://www.Anthropic.com/news/Claude-代码-插件
- 插件 文档 可用 at HTTPS://代码.Claude.com/文档/en/插件
- Comprehensive 错误 消息 和 diagnostics 通过 `/doctor` 命令
- Avoid flickering in `/模型` selector
- 改进 to `/help`
- Avoid mentioning 钩子 in `/恢复` summaries
- 更改 to the "verbose" 设置 in `/config` 现在 持久化 across 会话

## 2.0.11

- Reduced 系统 提示 size by 1.4k 令牌
- IDE: 修复 键盘 shortcuts 和 focus 问题 用于 smoother interaction
- 修复 Opus 回退 速率限制 错误 appearing incorrectly
- 修复 /添加-dir 命令 selecting wrong 默认 标签页

## 2.0.10

- Rewrote 终端 renderer 用于 buttery smooth UI
- 启用/禁用 MCP 服务器 by @mentioning, 或 in /MCP
- 新增 标签页 completion 用于 shell 命令 in bash mode
- PreToolUse 钩子 can 现在 modify 工具 inputs
- Press Ctrl-G to 编辑 your 提示 in your 系统's configured 文本 editor
- Fixes 用于 bash 权限 checks 与 环境 变量 in the 命令

## 2.0.9

- 修复 回归 where bash backgrounding 已停止 working

## 2.0.8

- 更新 Bedrock 默认 Sonnet 模型 to `全局.Anthropic.Claude-Sonnet-4-5-20250929-v1:0`
- IDE: 添加 drag-和-drop support 用于 文件 和 folders in chat
- /上下文: 修复 counting 用于 thinking 块
- Improve 消息 渲染 用于 用户 与 light themes on dark terminals
- 移除 弃用 .Claude.JSON allowedTools, ignorePatterns, 环境变量, 和 todoFeatureEnabled config 选项 (instead, 配置 these in your 设置.JSON)

## 2.0.5

- IDE: 修复 IME unintended 消息 submission 与 Enter 和 标签页
- IDE: 添加 "打开 in 终端" 链接 in login 屏幕
- 修复 unhandled OAuth expiration 401 API 错误
- SDK: 新增 SDKUserMessageReplay.isReplay to prevent 复制 消息

## 2.0.1

- 跳过 Sonnet 4.5 默认 模型 设置 更改 用于 Bedrock 和 Vertex
- Various 缺陷 fixes 和 presentation 改进

## 2.0.0

- 新 原生 VS 代码 extension
- Fresh coat of paint throughout the whole 应用
- /rewind a conversation to 撤销 代码 更改
- /usage 命令 to see plan 限制
- 标签页 to toggle thinking (sticky across 会话)
- Ctrl-R to 搜索 history
- Unshipped Claude config 命令
- 钩子: Reduced PostToolUse 'tool_use' ids were found 无 'tool_result' 块 错误
- SDK: The Claude 代码 SDK is 现在 the Claude 代理 SDK
- 添加 子代理 dynamically 与 `--代理` 标志

## 1.0.126

- 启用 /上下文 命令 用于 Bedrock 和 Vertex
- 添加 mTLS support 用于 HTTP-基于 OpenTelemetry exporters

## 1.0.124

- 集合 `CLAUDE_BASH_NO_LOGIN` 环境 变量 to 1 或 true to to 跳过 login shell 用于 BashTool
- 修复 Bedrock 和 Vertex 环境 变量 evaluating all strings as truthy
- 不再 inform Claude of the 列表 of 允许 工具 当 权限 is 已拒绝
- 修复 安全 漏洞 in Bash 工具 权限 checks
- 改进 VSCode extension 性能 用于 large 文件

## 1.0.123

- Bash 权限 rules 现在 support 输出 redirections 当 matching (e.g., `Bash(Python:*)` matches `Python 脚本.py > 输出.txt`)
- 修复 thinking mode triggering on negation phrases like "don't think"
- 修复 渲染 性能 degradation 期间 令牌 流式
- 新增 SlashCommand 工具, which enables Claude to invoke your slash 命令. HTTPS://代码.Claude.com/文档/en/slash-命令#SlashCommand-工具
- Enhanced BashTool 环境 snapshot 日志
- 修复 a 缺陷 where resuming a conversation in headless mode would sometimes 启用 thinking unnecessarily
- Migrated --调试 日志 to a 文件, to 启用 easy tailing & filtering

## 1.0.120

- 修复 输入 lag 期间 typing, especially noticeable 与 large prompts
- 改进 VSCode extension 命令 registry 和 会话 对话框 user 体验
- Enhanced 会话 对话框 responsiveness 和 visual feedback
- 修复 IDE 兼容性 问题 by removing 工作树 support check
- 修复 安全 漏洞 where Bash 工具 权限 checks could be bypassed 使用 前缀 matching

## 1.0.119

- 修复 Windows 问题 where 流程 visually freezes on entering interactive mode
- Support 动态 头信息 用于 MCP 服务器 通过 headersHelper 配置
- 修复 thinking mode not working in headless 会话
- 修复 slash 命令 现在 properly 更新 允许 工具 而不是 replacing them

## 1.0.117

- 添加 Ctrl-R history 搜索 to recall 上一个 命令 like bash/zsh
- 修复 输入 lag 当 typing, especially on Windows
- 添加 sed 命令 to auto-允许 命令 in acceptEdits mode
- 修复 Windows 路径 comparison to be case-insensitive 用于 drive letters
- 添加 权限 management 提示 to /添加-dir 输出

## 1.0.115

- Improve thinking mode 显示 与 enhanced visual effects
- 类型 /t to temporarily 禁用 thinking mode in your 提示
- Improve 路径 validation 用于 glob 和 grep 工具
- 显示 condensed 输出 用于 post-工具 钩子 to reduce visual clutter
- 修复 visual feedback 当 loading state completes
- Improve UI consistency 用于 权限 请求 dialogs

## 1.0.113

- 弃用 piped 输入 in interactive mode
- 移动 Ctrl+R keybinding 用于 toggling 转录 to Ctrl+O

## 1.0.112

- 转录 mode (Ctrl+R): 新增 the 模型 used to generate each assistant 消息
- Addressed 问题 where some Claude Max 用户 were incorrectly recognized as Claude Pro 用户
- 钩子: 新增 systemMessage support 用于 SessionEnd 钩子
- 新增 `spinnerTipsEnabled` 设置 to 禁用 加载动画 技巧
- IDE: Various 改进 和 缺陷 fixes

## 1.0.111

- /模型 现在 validates provided 模型 names
- 修复 Bash 工具 崩溃 caused by malformed shell syntax 解析中

## 1.0.110

- /终端-设置 命令 现在 supports WezTerm
- MCP: OAuth 令牌 现在 proactively 刷新 之前 expiration
- 修复 可靠性 问题 与 background Bash 流程

## 1.0.109

- SDK: 新增 partial 消息 流式 support 通过 `--include-partial-消息` CLI 标志

## 1.0.106

- Windows: 修复 路径 权限 matching to consistently use POSIX 格式 (e.g., `读取(//c/用户/...)`)

## 1.0.97

- 设置: /doctor 现在 validates 权限 rule syntax 和 suggests corrections

## 1.0.94

- Vertex: 添加 support 用于 全局 endpoints 用于 支持 模型
- /内存 命令 现在 allows direct editing of all imported 内存 文件
- SDK: 添加 自定义 工具 as callbacks
- 新增 /todos 命令 to 列表 当前 todo 项

## 1.0.93

- Windows: 添加 alt + v shortcut 用于 pasting images 从 剪贴板
- Support NO_PROXY 环境 变量 to 绕过 代理 用于 specified hostnames 和 IPs

## 1.0.90

- 设置 文件 更改 take effect immediately - no 重启 required

## 1.0.88

- 修复 问题 causing "OAuth 认证 is currently not 支持"
- Status line 输入 现在 includes `exceeds_200k_tokens`
- 修复 incorrect usage tracking in /cost.
- Introduced `ANTHROPIC_DEFAULT_SONNET_MODEL` 和 `ANTHROPIC_DEFAULT_OPUS_MODEL` 用于 controlling 模型 aliases opusplan, Opus, 和 Sonnet.
- Bedrock: Updated 默认 Sonnet 模型 to Sonnet 4

## 1.0.86

- 新增 /上下文 to help 用户 self-serve 调试 上下文 问题
- SDK: 新增 UUID support 用于 all SDK 消息
- SDK: 新增 `--replay-user-消息` to replay user 消息 back to stdout

## 1.0.85

- Status line 输入 现在 includes 会话 cost info
- 钩子: Introduced SessionEnd 钩子

## 1.0.84

- 修复 tool_use/tool_result ID mismatch 错误 当 网络 is 不稳定
- 修复 Claude sometimes ignoring real-time steering 当 wrapping up a 任务
- @-mention: 添加 ~/.Claude/\* 文件 to 建议 用于 easier 代理, 输出 style, 和 slash 命令 editing
- Use 内置 ripgrep by 默认; to opt out of this behavior, 集合 USE_BUILTIN_RIPGREP=0

## 1.0.83

- @-mention: Support 文件 与 spaces in 路径
- 新 shimmering 加载动画

## 1.0.82

- SDK: 添加 请求 cancellation support
- SDK: 新 additionalDirectories 选项 to 搜索 自定义 路径, 改进 slash 命令 processing
- 设置: Validation prevents 无效 fields in .Claude/设置.JSON 文件
- MCP: Improve 工具 name consistency
- Bash: 修复 崩溃 当 Claude tries to automatically 读取 large 文件

## 1.0.81

- Released 输出 styles, 包括 新 内置 educational 输出 styles "Explanatory" 和 "Learning". 文档: HTTPS://代码.Claude.com/文档/en/输出-styles
- 代理: 修复 自定义 代理 loading 当 代理 文件 are unparsable

## 1.0.80

- UI 改进: 修复 文本 contrast 用于 自定义 子代理 colors 和 加载动画 渲染 问题

## 1.0.77

- Bash 工具: 修复 heredoc 和 multiline 字符串 escaping, improve stderr redirection handling
- SDK: 添加 会话 support 和 权限 denial tracking
- 修复 令牌 限制 错误 in conversation summarization
- Opus 计划模式: 新 设置 in `/模型` to run Opus only in 计划模式, Sonnet otherwise

## 1.0.73

- MCP: Support multiple config 文件 与 `--MCP-config file1.JSON file2.JSON`
- MCP: Press Esc to 取消 OAuth 认证 flows
- Bash: 改进 命令 validation 和 reduced false 安全 警告
- UI: Enhanced 加载动画 animations 和 status line visual hierarchy
- Linux: 新增 support 用于 Alpine 和 musl-基于 distributions (requires separate ripgrep 安装)

## 1.0.72

- Ask 权限: have Claude 代码 always ask 用于 confirmation to use specific 工具 与 /权限

## 1.0.71

- Background 命令: (Ctrl-b) to run any Bash 命令 in the background 所以 Claude can keep working (great 用于 dev 服务器, tailing 日志, etc.)
- Customizable status line: 添加 your 终端 提示 to Claude 代码 与 /statusline

## 1.0.70

- 性能: 已优化 消息 渲染 用于 better 性能 与 large contexts
- Windows: 修复 原生 文件 搜索, ripgrep, 和 子代理 functionality
- 新增 support 用于 @-mentions in slash 命令 arguments

## 1.0.69

- Upgraded Opus to 版本 4.1

## 1.0.68

- 修复 incorrect 模型 names being used 用于 certain 命令 like `/PR-comments`
- Windows: improve 权限 checks 用于 允许 / 拒绝 工具 和 项目 trust. This may 创建 a 新 项目 条目 in `.Claude.JSON` - manually 合并 the history 字段 if desired.
- Windows: improve sub-流程 spawning to eliminate "No such 文件 或 目录" 当 运行中 命令 like pnpm
- Enhanced /doctor 命令 与 Claude.md 和 MCP 工具 上下文 用于 self-serve 调试
- SDK: 新增 canUseTool 回调 support 用于 工具 confirmation
- 新增 `disableAllHooks` 设置
- 改进 文件 建议 性能 in large repos

## 1.0.65

- IDE: 修复 连接 stability 问题 和 错误 handling 用于 diagnostics
- Windows: 修复 shell 环境 设置 用于 用户 无 .bashrc 文件

## 1.0.64

- 代理: 新增 模型 customization support - you can 现在 specify which 模型 an 代理 should use
- 代理: 修复 unintended 访问 to the recursive 代理 工具
- 钩子: 新增 systemMessage 字段 to 钩子 JSON 输出 用于 displaying 警告 和 上下文
- SDK: 修复 user 输入 tracking across multi-turn conversations
- 新增 hidden 文件 to 文件 搜索 和 @-mention 建议

## 1.0.63

- Windows: 修复 文件 搜索, @代理 mentions, 和 自定义 slash 命令 functionality

## 1.0.62

- 新增 @-mention support 与 typeahead 用于 自定义 代理. @<your-自定义-代理> to invoke it
- 钩子: 新增 SessionStart 钩子 用于 新 会话 initialization
- /添加-dir 命令 现在 supports typeahead 用于 目录 路径
- 改进 网络 connectivity check 可靠性

## 1.0.61

- 转录 mode (Ctrl+R): 更改 Esc to 退出 转录 mode rather 比 中断
- 设置: 新增 `--设置` 标志 to 加载 设置 从 a JSON 文件
- 设置: 修复 resolution of 设置 文件 路径 that are symlinks
- OTEL: 修复 reporting of wrong 组织 之后 认证 更改
- Slash 命令: 修复 权限 checking 用于 允许-工具 与 Bash
- IDE: 新增 support 用于 pasting images in VSCode macOS 使用 ⌘+V
- IDE: 新增 `CLAUDE_CODE_AUTO_CONNECT_IDE=false` 用于 disabling IDE auto-连接
- 新增 `CLAUDE_CODE_SHELL_PREFIX` 用于 wrapping Claude 和 user-provided shell 命令 run by Claude 代码

## 1.0.60

- You can 现在 创建 自定义 子代理 用于 specialized 任务! Run /代理 to get started

## 1.0.59

- SDK: 新增 工具 confirmation support 与 canUseTool 回调
- SDK: 允许 specifying 环境变量 用于 spawned 流程
- 钩子: Exposed PermissionDecision to 钩子 (包括 "ask")
- 钩子: UserPromptSubmit 现在 supports additionalContext in advanced JSON 输出
- 修复 问题 where some Max 用户 that specified Opus would still see 回退 to Sonnet

## 1.0.58

- 新增 support 用于 reading PDFs
- MCP: 改进 服务器 health status 显示 in 'Claude MCP 列表'
- 钩子: 新增 CLAUDE_PROJECT_DIR 环境变量 var 用于 钩子 命令

## 1.0.57

- 新增 support 用于 specifying a 模型 in slash 命令
- 改进 权限 消息 to help Claude understand 允许 工具
- 修复: 移除 trailing newlines 从 bash 输出 in 终端 wrapping

## 1.0.56

- Windows: 已启用 shift+标签页 用于 mode switching on 版本 of 节点.js that support 终端 VT mode
- Fixes 用于 WSL IDE detection
- 修复 an 问题 causing awsRefreshHelper 更改 to .AWS 目录 not to be picked up

## 1.0.55

- Clarified knowledge cutoff 用于 Opus 4 和 Sonnet 4 模型
- Windows: 修复 Ctrl+Z 崩溃
- SDK: 新增 ability to capture 错误 日志
- 添加 --系统-提示-文件 选项 to 覆盖 系统 提示 in print mode

## 1.0.54

- 钩子: 新增 UserPromptSubmit 钩子 和 the 当前 working 目录 to 钩子 inputs
- 自定义 slash 命令: 新增 参数-提示 to frontmatter
- Windows: OAuth uses 端口 45454 和 properly constructs browser URL
- Windows: mode switching 现在 uses alt + m, 和 计划模式 renders properly
- Shell: Switch to in-内存 shell snapshot to 修复 文件-related 错误

## 1.0.53

- Updated @-mention 文件 truncation 从 100 lines to 2000 lines
- 添加 helper 脚本 设置 用于 AWS 令牌 刷新: awsAuthRefresh (用于 foreground operations like AWS sso login) 和 awsCredentialExport (用于 background operation 与 STS-like 响应).

## 1.0.52

- 新增 support 用于 MCP 服务器 instructions

## 1.0.51

- 新增 support 用于 原生 Windows (requires git 用于 Windows)
- 新增 support 用于 Bedrock API 键 through 环境 变量 AWS_BEARER_TOKEN_BEDROCK
- 设置: /doctor can 现在 help you identify 和 修复 无效 设置 文件
- `--追加-系统-提示` can 现在 be used in interactive mode, not just --print/-p.
- Increased auto-压缩 警告 阈值 从 60% to 80%
- 修复 an 问题 与 handling user directories 与 spaces 用于 shell snapshots
- OTEL 资源 现在 includes os.类型, os.版本, 主机.arch, 和 WSL.版本 (if 运行中 on Windows Subsystem 用于 Linux)
- 自定义 slash 命令: 修复 user-级别 命令 in subdirectories
- 计划模式: 修复 问题 where rejected plan 从 sub-任务 would get discarded

## 1.0.48

- 修复 a 缺陷 in v1.0.45 where the 应用 would sometimes freeze on 启动
- 新增 progress 消息 to Bash 工具 基于 on the 最后 5 lines of 命令 输出
- 新增 expanding 变量 support 用于 MCP 服务器 配置
- Moved shell snapshots 从 /tmp to ~/.Claude 用于 more 可靠 Bash 工具 calls
- 改进 IDE extension 路径 handling 当 Claude 代码 runs in WSL
- 钩子: 新增 a PreCompact 钩子
- Vim mode: 新增 c, f/F, t/T

## 1.0.45

- Redesigned 搜索 (Grep) 工具 与 新 工具 输入 parameters 和 功能
- 已禁用 IDE diffs 用于 notebook 文件, 修复中 "超时 waiting 之后 1000ms" 错误
- 修复 config 文件 corruption 问题 by enforcing atomic writes
- Updated 提示 输入 撤销 to Ctrl+\_ to avoid breaking existing Ctrl+U behavior, matching zsh's 撤销 shortcut
- 停止 钩子: 修复 转录 路径 之后 /清除 和 修复 triggering 当 loop ends 与 工具 call
- 自定义 slash 命令: Restored namespacing in 命令 names 基于 on subdirectories. 例如, .Claude/命令/frontend/组件.md is 现在 /frontend:组件, not /组件.

## 1.0.44

- 新 /export 命令 lets you quickly export a conversation 用于 sharing
- MCP: resource_link 工具 results are 现在 支持
- MCP: 工具 annotations 和 工具 titles 现在 显示 in /MCP 视图
- 更改 Ctrl+Z to suspend Claude 代码. 恢复 by 运行中 `fg`. 提示 输入 撤销 is 现在 Ctrl+U.

## 1.0.43

- 修复 a 缺陷 where the theme selector was saving excessively
- 钩子: 新增 EPIPE 系统 错误 handling

## 1.0.42

- 新增 tilde (`~`) expansion support to `/添加-dir` 命令

## 1.0.41

- 钩子: 分割 停止 钩子 triggering 进入 停止 和 SubagentStop
- 钩子: 已启用 optional 超时 配置 用于 each 命令
- 钩子: 新增 "hook_event_name" to 钩子 输入
- 修复 a 缺陷 where MCP 工具 would 显示 twice in 工具 列表
- 新 工具 parameters JSON 用于 Bash 工具 in `tool_decision` 事件

## 1.0.40

- 修复 a 缺陷 causing API 连接 错误 与 UNABLE_TO_GET_ISSUER_CERT_LOCALLY if `NODE_EXTRA_CA_CERTS` was 集合

## 1.0.39

- 新 活动 Time metric in OpenTelemetry 日志

## 1.0.38

- Released 钩子. Special thanks to community 输入 in HTTPS://GitHub.com/anthropics/Claude-代码/问题/712. 文档: HTTPS://代码.Claude.com/文档/en/钩子

## 1.0.37

- 移除 ability to 集合 `代理-授权` 头信息 通过 ANTHROPIC_AUTH_TOKEN 或 apiKeyHelper

## 1.0.36

- Web 搜索 现在 takes today's date 进入 上下文
- 修复 a 缺陷 where stdio MCP 服务器 were not terminating properly on 退出

## 1.0.35

- 新增 support 用于 MCP OAuth 授权 服务器 discovery

## 1.0.34

- 修复 a 内存 泄漏 causing a MaxListenersExceededWarning 消息 to appear

## 1.0.33

- 改进 日志 functionality 与 会话 ID support
- 新增 提示 输入 撤销 functionality (Ctrl+Z 和 vim 'u' 命令)
- 改进 to 计划模式

## 1.0.32

- Updated loopback config 用于 litellm
- 新增 forceLoginMethod 设置 to 绕过 login selection 屏幕

## 1.0.31

- 修复 a 缺陷 where ~/.Claude.JSON would get reset 当 文件 contained 无效 JSON

## 1.0.30

- 自定义 slash 命令: Run bash 输出, @-mention 文件, 启用 thinking 与 thinking keywords
- 改进 文件 路径 autocomplete 与 filename matching
- 新增 timestamps in Ctrl-r mode 和 修复 Ctrl-c handling
- Enhanced jq regex support 用于 complex filters 与 pipes 和 select

## 1.0.29

- 改进 CJK character support in 光标 navigation 和 渲染

## 1.0.28

- Slash 命令: 修复 selector 显示 期间 history navigation
- Resizes images 之前 上传 to prevent API size 限制 错误
- 新增 XDG_CONFIG_HOME support to 配置 目录
- 性能 优化 用于 内存 usage
- 新 attributes (终端.类型, language) in OpenTelemetry 日志

## 1.0.27

- Streamable HTTP MCP 服务器 are 现在 支持
- 远程 MCP 服务器 (SSE 和 HTTP) 现在 support OAuth
- MCP 资源 can 现在 be @-mentioned
- /恢复 slash 命令 to switch conversations within Claude 代码

## 1.0.25

- Slash 命令: moved "项目" 和 "user" prefixes to descriptions
- Slash 命令: 改进 可靠性 用于 命令 discovery
- 改进 support 用于 Ghostty
- 改进 web 搜索 可靠性

## 1.0.24

- 改进 /MCP 输出
- 修复 a 缺陷 where 设置 arrays got overwritten 而不是 merged

## 1.0.23

- Released TypeScript SDK: import @Anthropic-ai/Claude-代码 to get started
- Released Python SDK: pip 安装 Claude-代码-sdk to get started

## 1.0.22

- SDK: Renamed `total_cost` to `total_cost_usd`

## 1.0.21

- 改进 editing of 文件 与 标签页-基于 indentation
- 修复 用于 tool_use 无 matching tool_result 错误
- 修复 a 缺陷 where stdio MCP 服务器 流程 would linger 之后 quitting Claude 代码

## 1.0.18

- 新增 --添加-dir CLI 参数 用于 specifying additional working directories
- 新增 流式 输入 support 无 require -p 标志
- 改进 启动 性能 和 会话 storage 性能
- 新增 CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR 环境 变量 to freeze working 目录 用于 bash 命令
- 新增 detailed MCP 服务器 工具 显示 (/MCP)
- MCP 认证 和 权限 改进
- 新增 auto-reconnection 用于 MCP SSE 连接 on 断开连接
- 修复 问题 where pasted content was lost 当 dialogs appeared

## 1.0.17

- We 现在 emit 消息 从 sub-任务 in -p mode (look 用于 the parent_tool_use_id 属性)
- 修复 崩溃 当 the VS 代码 diff 工具 is invoked multiple times quickly
- MCP 服务器 列表 UI 改进
- 更新 Claude 代码 流程 title to 显示 "Claude" 而不是 "节点"

## 1.0.11

- Claude 代码 can 现在 also be used 与 a Claude Pro subscription
- 新增 /升级 用于 smoother switching to Claude Max plans
- 改进 UI 用于 认证 从 API 键 和 Bedrock/Vertex/外部 认证 令牌
- 改进 shell 配置 错误 handling
- 改进 todo 列表 handling 期间 compaction

## 1.0.10

- 新增 markdown table support
- 改进 流式 性能

## 1.0.8

- 修复 Vertex AI region 回退 当 使用 CLOUD_ML_REGION
- Increased 默认 otel interval 从 1s -> 5s
- 修复 边 cases where MCP_TIMEOUT 和 MCP_TOOL_TIMEOUT weren't being respected
- 修复 a 回归 where 搜索 工具 unnecessarily asked 用于 权限
- 新增 support 用于 triggering thinking non-English languages
- 改进 compacting UI

## 1.0.7

- Renamed /允许-工具 -> /权限
- Migrated allowedTools 和 ignorePatterns 从 .Claude.JSON -> 设置.JSON
- 弃用 Claude config 命令 in favor of editing 设置.JSON
- 修复 a 缺陷 where --dangerously-跳过-权限 sometimes didn't work in --print mode
- 改进 错误 handling 用于 /安装-GitHub-应用
- Bugfixes, UI polish, 和 工具 可靠性 改进

## 1.0.6

- 改进 编辑 可靠性 用于 标签页-indented 文件
- Respect CLAUDE_CONFIG_DIR everywhere
- Reduced unnecessary 工具 权限 prompts
- 新增 support 用于 symlinks in @文件 typeahead
- Bugfixes, UI polish, 和 工具 可靠性 改进

## 1.0.4

- 修复 a 缺陷 where MCP 工具 错误 weren't being 已解析 correctly

## 1.0.1

- 新增 `DISABLE_INTERLEAVED_THINKING` to give 用户 the 选项 to opt out of interleaved thinking.
- 改进 模型 references to 显示 provider-specific names (Sonnet 3.7 用于 Bedrock, Sonnet 4 用于 Console)
- Updated 文档 links 和 OAuth 流程 descriptions

## 1.0.0

- Claude 代码 is 现在 generally 可用
- Introducing Sonnet 4 和 Opus 4 模型

## 0.2.125

- 破坏性更改: Bedrock ARN passed to `ANTHROPIC_MODEL` 或 `ANTHROPIC_SMALL_FAST_MODEL` should 不再 contain an escaped slash (specify `/` 而不是 `%2F`)
- 移除 `调试=true` in favor of `ANTHROPIC_LOG=调试`, to 日志 all 请求

## 0.2.117

- 破坏性更改: --print JSON 输出 现在 returns nested 消息 对象, 用于 forwards-兼容性 as we introduce 新 元数据 fields
- Introduced 设置.cleanupPeriodDays
- Introduced CLAUDE_CODE_API_KEY_HELPER_TTL_MS 环境变量 var
- Introduced --调试 mode

## 0.2.108

- You can 现在 发送 消息 to Claude 当 it works to steer Claude in real-time
- Introduced BASH_DEFAULT_TIMEOUT_MS 和 BASH_MAX_TIMEOUT_MS 环境变量 vars
- 修复 a 缺陷 where thinking was not working in -p mode
- 修复 a 回归 in /cost reporting
- 弃用 MCP wizard interface in favor of other MCP 命令
- Lots of other bugfixes 和 改进

## 0.2.107

- Claude.md 文件 can 现在 import other 文件. 添加 @路径/to/文件.md to ./Claude.md to 加载 additional 文件 on 启动

## 0.2.106

- MCP SSE 服务器 configs can 现在 specify 自定义 头信息
- 修复 a 缺陷 where MCP 权限 提示 didn't always 显示 correctly

## 0.2.105

- Claude can 现在 搜索 the web
- Moved 系统 & account status to /status
- 新增 word movement keybindings 用于 Vim
- 改进 延迟 用于 启动, todo 工具, 和 文件 edits

## 0.2.102

- 改进 thinking triggering 可靠性
- 改进 @mention 可靠性 用于 images 和 folders
- You can 现在 粘贴 multiple large 块 进入 one 提示

## 0.2.100

- 修复 a 崩溃 caused by a 栈 overflow 错误
- Made db storage optional; 缺失 db support disables --继续 和 --恢复

## 0.2.98

- 修复 an 问题 where auto-压缩 was 运行中 twice

## 0.2.96

- Claude 代码 can 现在 also be used 与 a Claude Max subscription (HTTPS://Claude.ai/升级)

## 0.2.93

- 恢复 conversations 从 where you left off 从 与 "Claude --继续" 和 "Claude --恢复"
- Claude 现在 has 访问 to a Todo 列表 that helps it stay on track 和 be more organized

## 0.2.82

- 新增 support 用于 --disallowedTools
- Renamed 工具 用于 consistency: LSTool -> LS, 视图 -> 读取, etc.

## 0.2.75

- Hit Enter to 队列 up additional 消息 当 Claude is working
- Drag in 或 复制/粘贴 image 文件 directly 进入 the 提示
- @-mention 文件 to directly 添加 them to 上下文
- Run one-off MCP 服务器 与 `Claude --MCP-config <路径-to-文件>`
- 改进 性能 用于 filename auto-完成

## 0.2.74

- 新增 support 用于 refreshing dynamically 已生成 API 键 (通过 apiKeyHelper), 与 a 5 分钟 TTL
- 任务 工具 can 现在 perform writes 和 run bash 命令

## 0.2.72

- Updated 加载动画 to indicate 令牌 loaded 和 工具 usage

## 0.2.70

- 网络 命令 like curl are 现在 可用 用于 Claude to use
- Claude can 现在 run multiple web queries in 并行
- Pressing ESC once immediately interrupts Claude in Auto-accept mode

## 0.2.69

- 修复 UI 故障 与 改进 Select 组件 behavior
- Enhanced 终端 输出 显示 与 better 文本 truncation logic

## 0.2.67

- Shared 项目 权限 rules can be saved in .Claude/设置.JSON

## 0.2.66

- Print mode (-p) 现在 supports 流式 输出 通过 --输出-格式=流-JSON
- 修复 问题 where pasting could 触发 内存 或 bash mode unexpectedly

## 0.2.63

- 修复 an 问题 where MCP 工具 were loaded twice, which caused 工具 call 错误

## 0.2.61

- Navigate menus 与 vim-style 键 (j/k) 或 bash/emacs shortcuts (Ctrl+n/p) 用于 更快 interaction
- Enhanced image detection 用于 more 可靠 剪贴板 粘贴 functionality
- 修复 an 问题 where ESC 键 could 崩溃 the conversation history selector

## 0.2.59

- 复制+粘贴 images directly 进入 your 提示
- 改进 progress indicators 用于 bash 和 fetch 工具
- Bugfixes 用于 non-interactive mode (-p)

## 0.2.54

- Quickly 添加 to 内存 by starting your 消息 与 '#'
- Press ctrl+r to see full 输出 用于 long 工具 results
- 新增 support 用于 MCP SSE transport

## 0.2.53

- 新 web fetch 工具 lets Claude 视图 URLs that you 粘贴 in
- 修复 a 缺陷 与 JPEG detection

## 0.2.50

- 新 MCP "项目" 作用域 现在 allows you to 添加 MCP 服务器 to .MCP.JSON 文件 和 提交 them to your 仓库

## 0.2.49

- 上一个 MCP 服务器 scopes have been renamed: 上一个 "项目" 作用域 is 现在 "本地" 和 "全局" 作用域 is 现在 "user"

## 0.2.47

- Press 标签页 to auto-完成 文件 和 文件夹 names
- Press Shift + 标签页 to toggle auto-accept 用于 文件 edits
- Automatic conversation compaction 用于 infinite conversation length (toggle 与 /config)

## 0.2.44

- Ask Claude to make a plan 与 thinking mode: just say 'think' 或 'think harder' 或 even '超深度思考'

## 0.2.41

- MCP 服务器 启动 超时 can 现在 be configured 通过 MCP_TIMEOUT 环境 变量
- MCP 服务器 启动 不再 块 the 应用 从 starting up

## 0.2.37

- 新 /发布-备注 命令 lets you 视图 发布 备注 at any time
- `Claude config 添加/移除` 命令 现在 accept multiple 值 separated by commas 或 spaces

## 0.2.36

- Import MCP 服务器 从 Claude Desktop 与 `Claude MCP 添加-从-Claude-desktop`
- 添加 MCP 服务器 as JSON strings 与 `Claude MCP 添加-JSON <n> <JSON>`

## 0.2.34

- Vim bindings 用于 文本 输入 - 启用 与 /vim 或 /config

## 0.2.32

- Interactive MCP 设置 wizard: Run "Claude MCP 添加" to 添加 MCP 服务器 与 a 步骤-by-步骤 interface
- 修复 用于 some PersistentShell 问题

## 0.2.31

- 自定义 slash 命令: Markdown 文件 in .Claude/命令/ directories 现在 appear as 自定义 slash 命令 to 插入 prompts 进入 your conversation
- MCP 调试 mode: Run 与 --MCP-调试 标志 to get more information about MCP 服务器 错误

## 0.2.30

- 新增 ANSI color theme 用于 better 终端 兼容性
- 修复 问题 where slash 命令 arguments weren't being sent properly
- (Mac-only) API 键 are 现在 已存储 in macOS Keychain

## 0.2.26

- 新 /approved-工具 命令 用于 managing 工具 权限
- Word-级别 diff 显示 用于 改进 代码 readability
- Fuzzy matching 用于 slash 命令

## 0.2.21

- Fuzzy matching 用于 /命令