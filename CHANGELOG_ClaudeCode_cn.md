# Claude Code 更新日志（中文版）


## 2.1.119

- `/config` 设置 (theme, editor mode, 详细, etc.) 现在 persist to `~/.claude/设置.json` and participate in project/local/policy override precedence
- 新增 `prUrlTemplate` setting to point the footer PR badge at a custom code-review URL instead of github.com
- 新增 `CLAUDE_CODE_HIDE_CWD` 环境变量 to hide the working 目录 in the 启动 logo
- `--from-pr` 现在 accepts GitLab 合并-request, Bitbucket pull-request, and GitHub Enterprise PR URLs
- `--print` mode 现在 honors the agent's `tools:` and `disallowedTools:` frontmatter, matching interactive-mode behavior
- `--agent <name>` 现在 honors the agent definition's `权限Mode` for built-in agents
- PowerShell tool commands can 现在 be auto-approved in 权限 mode, matching Bash behavior
- 钩子: `PostToolUse` and `PostToolUse失败` 钩子 inputs 现在 include `duration_ms` (tool execution time, excluding 权限 提示s and PreToolUse 钩子)
- 子 agent and SDK MCP 服务器 re配置 现在 connects servers in parallel instead of serially
- 插件 pinned by another 插件's version constraint 现在 auto-更新 to the highest satisfying git tag
- Vim mode: Esc in INSERT no longer pulls a queued message back into the input; press Esc again to interrupt
- Slash command suggestions 现在 highlight the characters that matched your query
- Slash command picker 现在 wraps long descriptions onto a second line instead of truncating
- `owner/repo#N` shorthand links in output 现在 use your git remote's host instead of always pointing at github.com
- 安全： `blocked市场s` 现在 correctly enforces `hostPattern` and `路径Pattern` entries
- Open遥测: `tool_result` and `tool_decision` events 现在 include `tool_use_id`; `tool_result` also includes `tool_input_size_bytes`
- Status line: stdin JSON 现在 includes `effort.level` and `thinking.启用`
- 修复了 pasting CRLF content (Windows clipboards, Xcode console) inserting an extra blank line between every line
- 修复了 multi-line paste losing newlines in 终端s using kitty keyboard protocol sequences inside bracketed paste
- 修复了 Glob and Grep 工具s disappearing on native macOS/Linux builds when the Bash 工具 is denied via 权限
- 修复了 scrolling up in 全屏模式 snapping back to the bottom every time a tool finishes
- 修复了 MCP HTTP connections failing with "Invalid OAuth 错误 response" when servers returned non-JSON bodies for OAuth discovery requests
- 修复了 Rewind overlay showing "(no 提示)" for messages with image attachments
- 修复了 auto mode overriding plan mode with conflicting "Execute immediately" instructions
- 修复了 async `PostToolUse` 钩子 that emit no response pay加载 writing empty entries to the 会话 transcript
- 修复了 spinner staying on when a 子 agent task notification is orphaned in the queue
- Tool search is 现在 禁用 by 默认 on Vertex AI to avoid an 不支持 beta header 错误 (opt in with `ENABLE_TOOL_SEARCH`)
- 修复了 `@`-文件 标签页 完成 replacing the entire 提示 when used inside a 斜杠命令 with an absolute 路径
- 修复了 a stray `p` character appearing at the 提示 on 启动 in macOS 终端.app via Docker or SSH
- 修复了 `${ENV_VAR}` placeholders in `headers` for HTTP/SSE/WebSocket MCP 服务器 not being substituted before requests
- 修复了 MCP OAuth client secret stored via `--client-secret` not being sent during token exchange for servers requiring `client_secret_post`
- 修复了 `/skills` Enter key closing the 对话框 instead of pre-filling `/<skill-name>` in the 提示
- 修复了 `/agents` detail view mislabeling built-in tools 不可用 to 子 agent as "Unrecognized"
- 修复了 MCP 服务器 from 插件 not spawning on Windows when the 插件 缓存 was incomplete
- 修复了 `/export` showing the current 默认 model instead of the model the conversation actually used
- 修复了 详细 output setting not persisting after restart
- 修复了 `/usage` progress bars overlapping with their "Resets …" labels
- 修复了 插件 MCP 服务器 failing when `${user_config.*}` references an 可选 field left blank
- 修复了 list items containing a sentence-final number wrapping the number onto its own line
- 修复了 `/plan` and `/plan open` not acting on the existing plan when entering plan mode
- 修复了 skills invoked before auto-compaction being re-executed against the next user message
- 修复了 `/重新加载-插件` and `/doctor` reporting 加载 错误 for 禁用 插件
- 修复了 Agent 工具 with `isolation: "worktree"` reusing stale worktree from prior 会话
- 修复了 禁用 MCP 服务器 appearing as "失败" in `/status`
- 修复了 `TaskList` returning tasks in arbitrary 文件ystem order instead of sorted by ID
- 修复了 spurious "GitHub API 速率限制 exceeded" hints when `gh` output contained PR titles mentioning "速率限制"
- 修复了 SDK/bridge `read_文件` not correctly enforcing size cap on growing 文件
- 修复了 PR not linked to 会话 when working in a git worktree
- 修复了 `/doctor` 警告 about MCP 服务器 entries overridden by a higher-precedence scope
- Windows: 移除 false-positive "Windows requires 'cmd /c' wrapper" MCP config 警告
- [VSCode] 修复了 voice dictation's first recording producing nothing on macOS while the microphone 权限 提示 is showing

## 2.1.118

- 新增 vim visual mode (`v`) and visual-line mode (`V`) with selection, operators, and visual feedback
- 合并d `/cost` and `/stats` into `/usage` — both remain as typing shortcuts that open the relevant 标签页
- 创建 and switch between named custom themes from `/theme`, or hand-edit JSON 文件 in `~/.claude/themes/`; 插件 can also ship themes via a `themes/` 目录
- 钩子 can 现在 invoke MCP tools directly via `type: "mcp_tool"`
- 新增 `DISABLE_UPDATES` env var to completely block all 更新 路径s including manual `claude 更新` — stricter than `DISABLE_AUTOUPDATER`
- WSL on Windows can 现在 inherit Windows-side managed 设置 via the `wslInheritsWindows设置` policy key
- Auto mode: include `"$默认s"` in `autoMode.allow`, `autoMode.soft_deny`, or `autoMode.environment` to add custom rules alongside the built-in list instead of replacing it
- 新增 a "Don't ask again" option to the auto mode opt-in 提示
- 新增 `claude 插件 tag` to 创建 release git tags for 插件 with version validation
- `--continue`/`--恢复` 现在 find 会话 that 新增 the current 目录 via `/add-dir`
- `/color` 现在 syncs the 会话 accent color to claude.ai/code when Remote Control is connected
- The `/model` picker 现在 honors `ANTHROPIC_DEFAULT_*_MODEL_NAME`/`_DESCRIPTION` overrides when using a custom `ANTHROPIC_BASE_URL` gateway
- When auto-更新 skips a 插件 due to another 插件's version constraint, the skip 现在 appears in `/doctor` and the `/插件` 错误 标签页
- 修复了 `/mcp` 菜单 hiding OAuth Authenticate/Re-authenticate actions for servers configured with `headersHelper`, and HTTP/SSE MCP 服务器 with custom headers being 卡住 in "needs authentication" after a transient 401
- 修复了 MCP 服务器 whose OAuth token response omits `expires_in` requiring re-authentication every hour
- 修复了 MCP step-up authorization silently 刷新ing instead of 提示ing for re-consent when the server's `insufficient_scope` 403 names a scope the current token already has
- 修复了 an unhandled promise rejection when an MCP 服务器's OAuth flow times out or is 取消led
- 修复了 MCP OAuth 刷新 proceeding without its cross-process lock under contention
- 修复了 macOS keychain race where a concurrent MCP token 刷新 could overwrite a freshly-刷新ed OAuth token, causing unexpected "Please run /login" 提示s
- 修复了 OAuth token 刷新 failing when the server revokes a token before its local expiry time
- 修复了 credential save 崩溃 on Linux/Windows corrupting `~/.claude/.credentials.json`
- 修复了 `/login` having no effect in a 会话 launched with `CLAUDE_CODE_OAUTH_TOKEN` — the env token is 现在 cleared so 磁盘 credentials take effect
- 修复了 unreadable text in the "new messages" scroll pill and `/插件` badges
- 修复了 plan acceptance 对话框 offering "auto mode" instead of "bypass 权限" when running with `--dangerously-skip-权限`
- 修复了 agent-type 钩子 failing with "Messages are required for agent 钩子" when configured for events other than `Stop` or `子 agentStop`
- 修复了 `提示` 钩子 re-firing on tool calls made by an agent-钩子 verifier 子 agent
- 修复了 `/fork` writing the full parent conversation to 磁盘 per fork — 现在 writes a pointer and hydrates on read
- 修复了 Alt+K / Alt+X / Alt+^ / Alt+_ freezing keyboard input
- 修复了 连接中 to a remote 会话 overwriting your local `model` setting in `~/.claude/设置.json`
- 修复了 typeahead showing "No commands match" 错误 when pasting 文件 路径s that start with `/`
- 修复了 `插件 安装` on an already-安装ed 插件 not re-resolving a dependency 安装ed at the wrong version
- 修复了 unhandled 错误 from 文件 watcher on invalid 路径s or fd exhaustion
- 修复了 Remote Control 会话 getting archived on transient CCR initialization blips during JWT 刷新
- 修复了 子 agent 恢复d via `SendMessage` not restoring the explicit `cwd` they were spawned with

## 2.1.117

- Forked 子 agent can 现在 be 启用 on external builds by setting `CLAUDE_CODE_FORK_SUBAGENT=1`
- Agent frontmatter `mcpServers` are 现在 加载ed for main-thread agent 会话 via `--agent`
- 改进了 `/model`: selections 现在 persist across restarts even when the project pins a different model, and the 启动 header shows when the active model comes from a project or managed-设置 pin
- The `/恢复` command 现在 offers to summarize stale, large 会话 before re-reading them, matching the existing `--恢复` behavior
- Faster 启动 when both local and claude.ai MCP 服务器 are configured (concurrent connect 现在 默认)
- `插件 安装` on an already-安装ed 插件 现在 安装s any missing dependencies instead of stopping at "已安装"
- 插件 dependency 错误 现在 say "not 安装ed" with an 安装 hint, and `claude 插件 市场 add` 现在 auto-resolves missing dependencies from configured 市场
- Managed-设置 `blocked市场s` and `strictK现在n市场s` are 现在 enforced on 插件 安装, 更新, 刷新, and auto更新
- Advisor Tool (experimental): 对话框 现在 carries an "experimental" label, learn-more link, and 启动 notification when 启用; 会话 no longer get 卡住 with "Advisor tool result content could not be processed" 错误 on every 提示 and `/compact`
- The `cleanupPeriodDays` retention sweep 现在 also covers `~/.claude/tasks/`, `~/.claude/shell-snapshots/`, and `~/.claude/备份s/`
- Open遥测: `user_提示` events 现在 include `command_name` and `command_source` for 斜杠命令; `cost.usage`, `token.usage`, `api_request`, and `api_错误` 现在 include an `effort` attribute when the model 支持 effort levels. Custom/MCP command names are redacted unless `OTEL_LOG_TOOL_DETAILS=1` is set
- Native builds on macOS and Linux: the `Glob` and `Grep` tools are replaced by embedded `bfs` and `ugrep` 可用 through the Bash 工具 — faster searches without a separate tool round-trip (Windows and npm-安装ed builds un更改)
- Windows: 缓存 `where.exe` execu标签页le lookups per process for faster subprocess launches
- 默认 effort for Pro/Max subscribers on Opus 4.6 and Sonnet 4.6 is 现在 `high` (was `medium`)
- 修复了 Plain-CLI OAuth 会话 dying with "Please run /login" when the access token expires mid-会话 — the token is 现在 刷新ed reactively on 401
- 修复了 `WebFetch` hanging on very large HTML pages by truncating input before HTML-to-markdown conversion
- 修复了 a 崩溃 when a proxy returns HTTP 204 No Content — 现在 surfaces a clear 错误 instead of a `Type错误`
- 修复了 `/login` having no effect when launched with `CLAUDE_CODE_OAUTH_TOKEN` env var and that token expires
- 修复了 提示-input undo (`Ctrl+_`) doing nothing immediately after typing, and skipping a state on each undo step
- 修复了 `NO_PROXY` not being respected for remote API requests when running under Bun
- 修复了 rare spurious escape/return triggers when key names arrive as coalesced text over slow connections
- 修复了 SDK `重新加载_插件` re连接中 all user MCP 服务器 serially
- 修复了 Bedrock application-inference-pro文件 requests failing with 400 when backed by Opus 4.7 with thinking 禁用
- 修复了 MCP `elicitation/创建` requests auto-取消ling in print/SDK mode when the server finishes 连接中 mid-turn
- 修复了 子 agent running a different model than the main agent incorrectly 标志ging 文件 reads with a malware 警告
- 修复了 idle re-render loop when background tasks are present, reducing 内存 growth on Linux
- [VSCode] 修复了 "Manage 插件" panel breaking when multiple large 市场 are configured
- 修复了 Opus 4.7 会话 showing inflated `/上下文` percentages and autocompacting too early — Claude Code was computing against a 200K 上下文 window instead of Opus 4.7's native 1M

## 2.1.116

- `/恢复` on large 会话 is significantly faster (up to 67% on 40MB+ 会话) and handles 会话 with many dead-fork entries more efficiently
- Faster MCP 启动 when multiple stdio servers are configured; `resources/templates/list` is 现在 deferred to first `@`-mention
- Smoother fullscreen scrolling in VS Code, Cursor, and Windsurf 终端s — `/终端-setup` 现在 configures the editor's scroll sensitivity
- Thinking spinner 现在 shows progress inline ("still thinking", "thinking more", "almost done thinking"), replacing the separate hint row
- `/config` search 现在 matches option values (e.g. searching "vim" finds the Editor mode setting)
- `/doctor` can 现在 be opened while Claude is responding, without waiting for the current turn to finish
- `/重新加载-插件` and background 插件 auto-更新 现在 auto-安装 missing 插件 dependencies from 市场 you've already 新增
- Bash 工具 现在 surfaces a hint when `gh` commands hit GitHub's API 速率限制, so agents can back off instead of retrying
- The Usage 标签页 in 设置 现在 shows your 5-hour and weekly usage immediately and no longer fails when the usage endpoint is rate-limited
- Agent frontmatter `钩子:` 现在 fire when running as a main-thread agent via `--agent`
- Slash command 菜单 现在 shows "No commands match" when your filter has zero results, instead of disappearing
- 安全： 沙箱 auto-allow no longer bypasses the dangerous-路径 safety check for `rm`/`rmdir` targeting `/`, `$HOME`, or other critical system 目录
- Claude Code and 安装er 现在 use `https://down加载s.claude.ai/claude-code-releases` instead of `https://storage.googleapis.com/claude-code-dist-86c565f3-f756-42ad-8dfa-d59b1c096819/claude-code-releases`
- 修复了 Devanagari and other Indic scripts rendering with broken column alignment in the 终端 UI
- 修复了 Ctrl+- not triggering undo in 终端s using the Kitty keyboard protocol (iTerm2, Ghostty, kitty, WezTerm, Windows 终端)
- 修复了 Cmd+Left/Right not jumping to line start/end in 终端s that use the Kitty keyboard protocol (Warp fullscreen, kitty, Ghostty, WezTerm)
- 修复了 Ctrl+Z hanging the 终端 when Claude Code is launched via a wrapper process (e.g. `npx`, `bun run`)
- 修复了 sc回滚 duplication in inline mode where resizing the 终端 or large output bursts would repeat earlier conversation history
- 修复了 模态 search 对话框s overflowing the screen at short 终端 heights, hiding the search box and keyboard hints
- 修复了 scattered blank cells and disappearing composer chrome in the VS Code integrated 终端 during scrolling
- 修复了 an intermittent API 400 错误 related to 缓存 control TTL ordering that could occur when a parallel request completed during request setup
- 修复了 `/分支` rejecting conversations with transcripts larger than 50MB
- 修复了 `/恢复` silently showing an empty conversation on large 会话 文件 instead of reporting the 加载 错误
- 修复了 `/插件` 安装ed 标签页 showing the same item twice when it appears under Needs attention or Favorites
- 修复了 `/更新` and `/tui` not working after entering a worktree mid-会话

## 2.1.114

- 修复了 a 崩溃 in the 权限 对话框 when an agent teams teammate requested tool 权限

## 2.1.113

- 更改 the CLI to spawn a native Claude Code binary (via a per-platform 可选 dependency) instead of bundled JavaScript
- 新增 `沙箱.network.deniedDomains` setting to block specific domains even when a broader `allowedDomains` wildcard would otherwise permit them
- Fullscreen mode: Shift+↑/↓ 现在 scrolls the viewport when extending a selection past the visible edge
- `Ctrl+A` and `Ctrl+E` 现在 move to the start/end of the current logical line in multiline input, matching readline behavior
- Windows: `Ctrl+Backspace` 现在 删除s the previous word
- Long URLs in responses and bash output stay clickable when they wrap across lines (in 终端s with OSC 8 hyperlinks)
- 改进了 `/loop`: pressing Esc 现在 取消s 待处理 wakeups, and wakeups display as "Claude resuming /loop wakeup" for clarity
- `/extra-usage` 现在 works from Remote Control (mobile/web) clients
- Remote Control clients can 现在 query `@`-文件 自动完成 suggestions
- 改进了 `/ultrareview`: faster launch with parallelized checks, diffstat in the launch 对话框, and animated launching state
- 子 agent that stall mid-stream 现在 fail with a clear 错误 after 10 minutes instead of hanging silently
- Bash 工具: multi-line commands whose first line is a comment 现在 show the full command in the transcript, closing a UI-spoofing vector
- Running `cd <current-目录> && git …` no longer triggers a 权限 提示 when the `cd` is a no-op
- 安全： on macOS, `/private/{etc,var,tmp,home}` 路径s are 现在 treated as dangerous removal targets under `Bash(rm:*)` allow rules
- 安全： Bash deny rules 现在 match commands wrapped in `env`/`sudo`/`watch`/`ionice`/`setsid` and similar exec wrappers
- 安全： `Bash(find:*)` allow rules no longer auto-approve `find -exec`/`-删除`
- 修复了 MCP concurrent-call 超时 handling where a message for one tool call could silently disarm another call's watchdog
- 修复了 Cmd-backspace / `Ctrl+U` to once again 删除 from the cursor to the start of the line
- 修复了 markdown 标签页les breaking when a cell contains an inline code span with a pipe character
- 修复了 会话 recap auto-firing while composing unsent text in the 提示
- 修复了 `/copy` "Full response" not aligning markdown 标签页le columns for pasting into GitHub, Notion, or Slack
- 修复了 messages typed while viewing a running 子 agent being hidden from its transcript and misattributed to the parent AI
- 修复了 Bash `dangerously禁用沙箱` running commands outside the 沙箱 without a 权限 提示
- 修复了 `/effort auto` 确认ation — 现在 says "Effort level set to max" to match the 状态栏 label
- 修复了 the "copied N chars" toast overcounting emoji and other multi-code-unit characters
- 修复了 `/insights` 崩溃ing with `EBUSY` on Windows
- 修复了 退出 确认ation 对话框 mislabeling one-shot scheduled tasks as recurring — 现在 shows a countdown
- 修复了 slash/@ 完成 菜单 not sitting flush against the 提示 border in 全屏模式
- 修复了 `CLAUDE_CODE_EXTRA_BODY` `output_config.effort` causing 400 错误 on 子 agent calls to models that don't 支持 effort and on Vertex AI
- 修复了 提示 cursor disappearing when `NO_COLOR` is set
- 修复了 `ToolSearch` ranking so pasted MCP tool names surface the actual tool instead of description-matching siblings
- 修复了 compacting a 恢复d long-上下文 会话 failing with "Extra usage is required for long 上下文 requests"
- 修复了 `插件 安装` succeeding when a dependency version conflicts with an already-安装ed 插件 — 现在 reports `range-conflict`
- 修复了 "Refine with Ultraplan" not showing the remote 会话 URL in the transcript
- 修复了 SDK image content blocks that fail to process 崩溃ing the 会话 — 现在 degrade to a text placeholder
- 修复了 Remote Control 会话 not 流式传输 子 agent transcripts
- 修复了 Remote Control 会话 not being archived when Claude Code 退出s
- 修复了 `thinking.type.启用 is not 支持ed` 400 错误 when using Opus 4.7 via a Bedrock Application Inference Pro文件 ARN

## 2.1.112

- 修复了 "claude-opus-4-7 is temporarily 不可用" for auto mode

## 2.1.111

- Claude Opus 4.7 xhigh is 现在 可用! Use /effort to tune speed vs. intelligence
- Auto mode is 现在 可用 for Max subscribers when using Opus 4.7
- 新增 `xhigh` effort level for Opus 4.7, sitting between `high` and `max`. 可用 via `/effort`, `--effort`, and the model picker; other models fall back to `high`
- `/effort` 现在 opens an interactive slider when called without arguments, with arrow-key navigation between levels and Enter to 确认
- 新增 "Auto (match 终端)" theme option that matches your 终端's dark/light mode — select it from `/theme`
- 新增 `/less-权限-提示s` skill — scans transcripts for common read-only Bash and MCP tool calls and proposes a prioritized allowlist for `.claude/设置.json`
- 新增 `/ultrareview` for running comprehensive code review in the cloud using parallel multi-agent analysis and critique — invoke with no arguments to review your current 分支, or `/ultrareview <PR#>` to fetch and review a specific GitHub PR
- Auto mode no longer requires `--启用-auto-mode`
- Windows: PowerShell tool is progressively rolling out. Opt in or out with `CLAUDE_CODE_USE_POWERSHELL_TOOL`. On Linux and macOS, 启用 with `CLAUDE_CODE_USE_POWERSHELL_TOOL=1` (requires `pwsh` on PATH)
- Read-only bash commands with glob patterns (e.g. `ls *.ts`) and commands starting with `cd <project-dir> &&` no longer trigger a 权限 提示
- Suggest the closest matching subcommand when `claude <word>` is invoked with a near-miss typo (e.g. `claude udpate` → "Did you mean `claude 更新`?")
- Plan 文件 are 现在 named after your 提示 (e.g. `修复-auth-race-snug-otter.md`) instead of purely random words
- 改进了 `/setup-vertex` and `/setup-bedrock` to show the actual `设置.json` 路径 when `CLAUDE_CONFIG_DIR` is set, seed model candidates from existing pins on re-run, and offer a "with 1M 上下文" option for 支持ed models
- `/skills` 菜单 现在 支持 sorting by estimated token count — press `t` to toggle
- `Ctrl+U` 现在 clears the entire input buffer (之前: 删除 to start of line); press `Ctrl+Y` to 恢复
- `Ctrl+L` 现在 forces a full screen redraw in addition to clearing the 提示 input
- Transcript view footer 现在 shows `[` (dump to sc回滚) and `v` (open in editor) shortcuts
- The "+N lines" marker for truncated long pastes is 现在 a full-width rule for easier scanning
- Headless `--output-format stream-json` 现在 includes `插件_错误` on the init event when 插件 are demoted for unsatisfied dependencies
- 新增 `OTEL_LOG_RAW_API_BODIES` 环境变量 to emit full API request and response bodies as Open遥测 log events for 调试ging
- Suppressed spurious decompression, network, and transient 错误 messages that could appear in the TUI during normal operation
- Reverted the v2.1.110 cap on non-流式传输 fallback retries — it traded long waits for more outright 失败s during API over加载
- 修复了 终端 display tearing (random characters, drifting input) in iTerm2 + tmux setups when 终端 notifications are sent
- 修复了 `@` 文件 suggestions re-scanning the entire project on every turn in non-git working 目录, and showing only config 文件 in freshly-initialized git repos with no tracked 文件
- 修复了 LSP diagnostics from before an edit appearing after it, causing the model to re-read 文件 it just edited
- 修复了 标签页-completing `/恢复` immediately resuming an arbitrary titled 会话 instead of showing the 会话 picker
- 修复了 `/上下文` grid rendering with extra blank lines between rows
- 修复了 `/clear` dropping the 会话 name set by `/rename`, causing statusline output to lose `会话_name`
- 改进了 插件 错误 handling: dependency 错误 现在 distinguish conflicting, invalid, and overly complex version requirements; 修复了 stale resolved versions after `插件 更新`; `插件 安装` 现在 recovers from interrupted prior 安装s
- 修复了 Claude calling a non-existent `提交` skill and showing "Unk现在n skill: 提交" for users without a custom `/提交` command
- 修复了 429 rate-limit 错误 on Bedrock/Vertex/Foundry referencing status.claude.com (it only covers Anthropic-operated providers)
- 修复了 feedback surveys appearing back-to-back after dismissing one
- 修复了 bare URLs in bash/PowerShell/MCP tool output being unclickable when the 终端 wraps them across lines
- Windows: `CLAUDE_ENV_FILE` and 会话Start 钩子 environment 文件 现在 apply (之前 a no-op)
- Windows: 权限 rules with drive-letter 路径s are 现在 correctly root-anchored, and 路径s differing only by drive-letter case are recognized as the same 路径

## 2.1.110

- 新增 `/tui` command and `tui` setting — run `/tui fullscreen` to switch to flicker-free rendering in the same conversation
- 新增 push notification tool — Claude can send mobile push notifications when Remote Control and "Push when Claude decides" config are 启用
- 更改 `Ctrl+O` to toggle between normal and 详细 transcript only; focus view is 现在 toggled separately with the new `/focus` command
- 新增 `autoScroll启用` config to 禁用 conversation auto-scroll in 全屏模式
- 新增 option to show Claude's last response as commented 上下文 in the `Ctrl+G` external editor (启用 via `/config`)
- 改进了 `/插件` 安装ed 标签页 — items needing attention and favorites appear at the top, 禁用 items are hidden behind a fold, and `f` favorites the selected item
- 改进了 `/doctor` to warn when an MCP 服务器 is defined in multiple config scopes with different endpoints
- `--恢复`/`--continue` 现在 resurrects unexpired scheduled tasks
- `/上下文`, `/退出`, and `/重新加载-插件` 现在 work from Remote Control (mobile/web) clients
- Write 工具 现在 informs the model when you edit the proposed content in the IDE diff before accepting
- Bash 工具 现在 enforces the documented maximum 超时 instead of accepting arbitrarily large values
- SDK/headless 会话 现在 read `TRACEPARENT`/`TRACESTATE` from the environment for distributed 跟踪 linking
- 会话 recap is 现在 启用 for users with 遥测 禁用 (Bedrock, Vertex, Foundry, `DISABLE_TELEMETRY`). Opt out via `/config` or `CLAUDE_CODE_ENABLE_AWAY_SUMMARY=0`.
- 修复了 MCP tool calls hanging indefinitely when the server connection drops mid-response on SSE/HTTP transports
- 修复了 non-流式传输 fallback retries causing multi-minute hangs when the API is unreachable
- 修复了 会话 recap, local slash-command output, and other system status lines not appearing in focus mode
- 修复了 high CPU usage in fullscreen when text is selected while a tool is running
- 修复了 插件 安装 not honoring dependencies declared in `插件.json` when the 市场 entry omits them; `/插件` 安装 现在 lists auto-安装ed dependencies
- 修复了 skills with `禁用-model-invocation: true` failing when invoked via `/<skill>` mid-message
- 修复了 `--恢复` sometimes showing the first 提示 instead of the `/rename` name for 会话 still running or 退出ed uncleanly
- 修复了 queued messages briefly appearing twice during multi-tool-call turns
- 修复了 会话 cleanup not removing the full 会话 目录 including 子 agent transcripts
- 修复了 dropped keystrokes after the CLI relaunches (e.g. `/tui`, provider setup wizards)
- 修复了 garbled 启动 rendering in macOS 终端.app and other 终端s that don't 支持 synchronized output
- Hardened "Open in editor" actions against command injection from untrusted 文件names
- 修复了 `权限Request` 钩子 returning `更新dInput` not being re-checked against `权限.deny` rules; `setMode:'bypass权限'` 更新s 现在 respect `禁用Bypass权限Mode`
- 修复了 `PreToolUse` 钩子 `additional上下文` being dropped when the tool call fails
- 修复了 stdio MCP 服务器 that print stray non-JSON lines to stdout being disconnected on the first stray line (regression in 2.1.105)
- 修复了 headless/SDK 会话 auto-title firing an extra Haiku request when `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` or `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` is set
- 修复了 potential excessive 内存 allocation when piped (non-TTY) Ink output contains a single very wide line
- 修复了 `/skills` 菜单 not scrolling when the list overflows the 模态 in 全屏模式
- 修复了 Remote Control 会话 showing a generic 错误 instead of 提示ing for re-login when the 会话 is too old
- 修复了 Remote Control 会话 renames from claude.ai not persisting the title to the local CLI 会话

## 2.1.109

- 改进了 extended-thinking indicator with a rotating progress hint

## 2.1.108

- 新增 `ENABLE_PROMPT_CACHING_1H` env var to opt into 1-hour 提示 缓存 TTL on API key, Bedrock, Vertex, and Foundry (`ENABLE_PROMPT_CACHING_1H_BEDROCK` is 弃用 but still honored), and `FORCE_PROMPT_CACHING_5M` to force 5-minute TTL
- 新增 recap feature to provide 上下文 when returning to a 会话, configurable in `/config` and manually invocable with `/recap`; force with `CLAUDE_CODE_ENABLE_AWAY_SUMMARY` if 遥测 禁用.
- The model can 现在 discover and invoke built-in 斜杠命令 like `/init`, `/review`, and `/security-review` via the Skill tool
- `/undo` is 现在 an alias for `/rewind`
- 改进了 `/model` to warn before switching models mid-conversation, since the next response re-reads the full history un缓存
- 改进了 `/恢复` picker to 默认 to 会话 from the current 目录; press `Ctrl+A` to show all projects
- 改进了 错误 messages: server 速率限制s are 现在 distinguished from plan usage limits; 5xx/529 错误 show a link to status.claude.com; unk现在n 斜杠命令 suggest the closest match
- Reduced 内存 footprint for 文件 reads, edits, and 语法高亮 by 加载ing language grammars on demand
- 新增 "详细" indicator when viewing the detailed transcript (`Ctrl+O`)
- 新增 a 警告 at 启动 when 提示 缓存 is 禁用 via `DISABLE_PROMPT_CACHING*` 环境变量
- 修复了 paste not working in the `/login` code 提示 (regression in 2.1.105)
- 修复了 subscribers who set `DISABLE_TELEMETRY` falling back to 5-minute 提示 缓存 TTL instead of 1 hour
- 修复了 Agent 工具 提示ing for 权限 in auto mode when the safety classifier's transcript exceeded its 上下文 window
- 修复了 Bash 工具 producing no output when `CLAUDE_ENV_FILE` (e.g. `~/.zpro文件`) ends with a `#` comment line
- 修复了 `claude --恢复 <会话-id>` losing the 会话's custom name and color set via `/rename`
- 修复了 会话 titles showing placeholder example text when the first message is a short greeting
- 修复了 终端 escape codes appearing as garbage text in the 提示 input after `--teleport`
- 修复了 `/feedback` retry: pressing Enter to re提交 after a 失败 现在 works without first editing the description
- 修复了 `--teleport` and `--恢复 <id>` precondition 错误 (e.g. dirty git tree, 会话 未找到) 退出ing silently instead of showing the 错误 message
- 修复了 Remote Control 会话 titles set in the web UI being overwritten by auto-generated titles after the third message
- 修复了 `--恢复` truncating 会话 when the transcript contained a self-referencing message
- 修复了 transcript write 失败s (e.g., 磁盘 full) being silently dropped instead of being logged
- 修复了 diacritical marks (accents, umlauts, cedillas) being dropped from responses when the `language` setting is configured
- 修复了 policy-managed 插件 never auto-updating when running from a different project than where they were first 安装ed

## 2.1.107

- Show thinking hints sooner during long operations

## 2.1.105

- 新增 `路径` parameter to the `EnterWorktree` tool to switch into an existing worktree of the current repository
- 新增 PreCompact 钩子 支持: 钩子 can 现在 block compaction by 退出ing with code 2 or returning `{"decision":"block"}`
- 新增 background monitor 支持 for 插件 via a top-level `monitors` manifest key that auto-arms at 会话 start or on skill invoke
- `/proactive` is 现在 an alias for `/loop`
- 改进了 stalled API stream handling: streams 现在 abort after 5 minutes of no data and retry non-流式传输 instead of hanging indefinitely
- 改进了 network 错误 messages: connection 错误 现在 show a retry message immediately instead of a silent spinner
- 改进了 文件 write display: long single-line writes (e.g. minified JSON) are 现在 truncated in the UI instead of paginating across many screens
- 改进了 `/doctor` layout with status icons; press `f` to have Claude 修复 reported issues
- 改进了 `/config` labels and descriptions for clarity
- 改进了 skill description handling: raised the listing cap from 250 to 1,536 characters and 新增 a 启动 警告 when descriptions are truncated
- 改进了 `WebFetch` to strip `<style>` and `<script>` contents from fetched pages so CSS-heavy pages no longer exhaust the content budget before reaching actual text
- 改进了 stale agent worktree cleanup to remove worktree whose PR was squash-合并d instead of keeping them indefinitely
- 改进了 MCP large-output truncation 提示 to give format-specific recipes (e.g. `jq` for JSON, computed Read chunk sizes for text)
- 修复了 images attached to queued messages (sent while Claude is working) being dropped
- 修复了 screen going blank when the 提示 input wraps to a second line in long conversations
- 修复了 leading whitespace getting copied when selecting multi-line assistant responses in 全屏模式
- 修复了 leading whitespace being trimmed from assistant messages, breaking ASCII art and indented diagrams
- 修复了 garbled bash output when commands print clickable 文件 links (e.g. Python `rich`/`loguru` logging)
- 修复了 alt+enter not inserting a newline in 终端s using ESC-pre修复 alt encoding, and Ctrl+J not inserting a newline (regression in 2.1.100)
- 修复了 duplicate "Creating worktree" text in EnterWorktree/退出Worktree tool display
- 修复了 queued user 提示s disappearing from focus mode
- 修复了 one-shot scheduled tasks re-firing repeatedly when the 文件 watcher missed the post-fire cleanup
- 修复了 inbound channel notifications being silently dropped after the first message for Team/Enterprise users
- 修复了 市场 插件 with `package.json` and lock文件 not having dependencies 安装ed automatically after 安装/更新
- 修复了 市场 auto-更新 leaving the official 市场 in a broken state when a 插件 process holds 文件 open during the 更新
- 修复了 "恢复 this 会话 with..." hint not printing on 退出 after `/恢复`, `--worktree`, or `/分支`
- 修复了 feedback survey shortcut keys firing when typed at the end of a longer 提示
- 修复了 stdio MCP 服务器 emitting malformed (non-JSON) output hanging the 会话 instead of failing fast with "连接 closed"
- 修复了 MCP tools missing on the first turn of headless/remote-trigger 会话 when MCP 服务器 connect asynchronously
- 修复了 `/model` picker on AWS Bedrock in non-US regions persisting invalid `us.*` model IDs to `设置.json` when inference pro文件 discovery is still in-flight
- 修复了 429 rate-limit 错误 showing a raw JSON dump instead of a clean message for API-key, Bedrock, and Vertex users
- 修复了 崩溃 on 恢复 when 会话 contains malformed text blocks
- 修复了 `/help` dropping the 标签页 bar, Shortcuts heading, and footer at short 终端 heights
- 修复了 malformed keybinding entry values in `keybindings.json` being silently 加载ed instead of rejected with a clear 错误
- 修复了 `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` in one project's 设置 permanently disabling usage 指标s for all projects on the machine
- 修复了 washed-out 16-color palette when using Ghostty, Kitty, Alacritty, WezTerm, foot, rio, or Contour over SSH/mosh
- 修复了 Bash 工具 suggesting `acceptEdits` 权限 mode when 退出ing plan mode would downgrade from a higher 权限 level

## 2.1.101

- 新增 `/team-onboarding` command to generate a teammate ramp-up guide from your local Claude Code usage
- 新增 OS CA certificate store trust by 默认, so enterprise TLS proxies work without extra setup (set `CLAUDE_CODE_CERT_STORE=bundled` to use only bundled CAs)
- `/ultraplan` and other remote-会话 features 现在 auto-创建 a 默认 cloud environment instead of requiring web setup first
- 改进了 brief mode to retry once when Claude responds with plain text instead of a structured message
- 改进了 focus mode: Claude 现在 writes more self-contained summaries since it k现在s you only see its final message
- 改进了 tool-not-可用 错误 to explain why and how to proceed when the model calls a tool that exists but isn't 可用 in the current 上下文
- 改进了 rate-limit retry messages to show which limit was hit and when it resets instead of an opaque seconds countdown
- 改进了 refusal 错误 messages to include the API-provided explanation when 可用
- 改进了 `claude -p --恢复 <name>` to accept 会话 titles set via `/rename` or `--name`
- 改进了 设置 resilience: an unrecognized 钩子 event name in `设置.json` no longer causes the entire 文件 to be ignored
- 改进了 插件 钩子 from 插件 force-启用 by managed 设置 to run when `allowManaged钩子Only` is set
- 改进了 `/插件` and `claude 插件 更新` to show a 警告 when the 市场 could not be 刷新ed, instead of silently reporting a stale version
- 改进了 plan mode to hide the "Refine with Ultraplan" option when the user's org or auth setup can't reach Claude Code on the web
- 改进了 beta tracing to honor `OTEL_LOG_USER_PROMPTS`, `OTEL_LOG_TOOL_DETAILS`, and `OTEL_LOG_TOOL_CONTENT`; sensitive span attributes are no longer emitted unless opted in
- 改进了 SDK `query()` to clean up subprocess and temp 文件 when consumers `break` from `for await` or use `await using`
- 修复了 a command injection vulnerability in the POSIX `which` fallback used by LSP binary detection
- 修复了 a 内存 leak where long 会话 retained dozens of historical copies of the message list in the virtual scroller
- 修复了 `--恢复`/`--continue` losing conversation 上下文 on large 会话 when the 加载er anchored on a dead-end 分支 instead of the live conversation
- 修复了 `--恢复` chain recovery bridging into an unrelated 子 agent conversation when a 子 agent message landed near a main-chain write gap
- 修复了 a 崩溃 on `--恢复` when a persisted Edit/Write 工具 result was missing its `文件_路径`
- 修复了 a hardcoded 5-minute request 超时 that aborted slow backends (local LLMs, extended thinking, slow gateways) regardless of `API_TIMEOUT_MS`
- 修复了 `权限.deny` rules not overriding a PreToolUse 钩子's `权限Decision: "ask"` — 之前 the 钩子 could downgrade a deny into a 提示
- 修复了 `--setting-sources` without `user` causing background cleanup to ignore `cleanupPeriodDays` and 删除 conversation history older than 30 days
- 修复了 Bedrock SigV4 authentication failing with 403 when `ANTHROPIC_AUTH_TOKEN`, `apiKeyHelper`, or `ANTHROPIC_CUSTOM_HEADERS` set an Authorization header
- 修复了 `claude -w <name>` failing with "已存在" after a previous 会话's worktree cleanup left a stale 目录
- 修复了 子 agent not inheriting MCP tools from dynamically-injected servers
- 修复了 sub-agents running in isolated worktree being denied Read/Edit access to 文件 inside their own worktree
- 修复了 沙箱ed Bash commands failing with `mktemp: No such 文件 or 目录` after a fresh boot
- 修复了 `claude mcp serve` tool calls failing with "Tool execution 失败" in MCP clients that validate `outputSchema`
- 修复了 `RemoteTrigger` tool's `run` action sending an empty body and being rejected by the server
- 修复了 several `/恢复` picker issues: narrow 默认 view hiding 会话 from other projects, unreachable preview on Windows 终端, incorrect cwd in worktree, 会话-not-found 错误 not surfacing in stderr, 终端 title not being set, and 恢复 hint overlapping the 提示 input
- 修复了 Grep 工具 ENOENT when the embedded ripgrep binary 路径 becomes stale (VS Code extension auto-更新, macOS App Translocation); 现在 falls back to system `rg` and self-heals mid-会话
- 修复了 `/btw` writing a copy of the entire conversation to 磁盘 on every use
- 修复了 `/上下文` Free space and Messages breakdown disagreeing with the header percentage
- 修复了 several 插件 issues: 斜杠命令 resolving to the wrong 插件 with duplicate `name:` frontmatter, `/插件 更新` failing with `ENAMETOOLONG`, Discover showing already-安装ed 插件, 目录-source 插件 加载ing from a stale version 缓存, and skills not honoring `上下文: fork` and `agent` frontmatter fields
- 修复了 the `/mcp` 菜单 offering OAuth-specific actions for MCP 服务器 configured with `headersHelper`; Reconnect is 现在 offered instead to re-invoke the helper script
- 修复了 `ctrl+]`, `ctrl+\`, and `ctrl+^` keybindings not firing in 终端s that send raw C0 control bytes (终端.app, 默认 iTerm2, xterm)
- 修复了 `/login` OAuth URL rendering with padding that prevented clean mouse selection
- 修复了 rendering issues: flicker in non-全屏模式 when content above the visible area 更改, 终端 sc回滚 being wiped during long 会话 in non-全屏模式, and mouse-scroll escape sequences occasionally leaking into the 提示 as text
- 修复了 崩溃 when `设置.json` env values are numbers instead of strings
- 修复了 in-app 设置 writes (e.g. `/add-dir --remember`, `/config`) not 刷新ing the in-内存 snapshot, preventing 移除 目录 from being revoked mid-会话
- 修复了 custom keybindings (`~/.claude/keybindings.json`) not 加载ing on Bedrock, Vertex, and other third-party providers
- 修复了 `claude --continue -p` not correctly continuing 会话 创建d by `-p` or the SDK
- 修复了 several Remote Control issues: worktree 移除 on 会话 崩溃, connection 失败s not persisting in the transcript, spurious "Disconnected" indicator in brief mode for local 会话, and `/remote-control` failing over SSH when only `CLAUDE_CODE_ORGANIZATION_UUID` is set
- 修复了 `/insights` sometimes omitting the report 文件 link from its response
- [VSCode] 修复了 the 文件 attachment below the chat input not clearing when the last editor 标签页 is closed

## 2.1.98

- 新增 interactive Google Vertex AI setup wizard accessible from the login screen when selecting "3rd-party platform", guiding you through GCP authentication, project and region 配置, credential verification, and model pinning
- 新增 `CLAUDE_CODE_PERFORCE_MODE` env var: when set, Edit/Write/NotebookEdit fail on read-only 文件 with a `p4 edit` hint instead of silently overwriting them
- 新增 Monitor tool for 流式传输 events from background scripts
- 新增 subprocess 沙箱ing with PID namespace isolation on Linux when `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB` is set, and `CLAUDE_CODE_SCRIPT_CAPS` env var to limit per-会话 script invocations
- 新增 `--exclude-dynamic-system-提示-sections` 标志 to print mode for 改进了 cross-user 提示 缓存
- 新增 `工作区.git_worktree` to the status line JSON input, set whenever the current 目录 is inside a linked git worktree
- 新增 W3C `TRACEPARENT` env var to Bash 工具 subprocesses when OTEL tracing is 启用, so child-process spans correctly parent to Claude Code's 跟踪 tree
- LSP: Claude Code 现在 identifies itself to language servers via `clientInfo` in the initialize request
- 修复了 a Bash 工具 权限 bypass where a backslash-escaped 标志 could be auto-allowed as read-only and lead to arbitrary code execution
- 修复了 compound Bash commands bypassing forced 权限 提示s for safety checks and explicit ask rules in auto and bypass-权限 modes
- 修复了 read-only commands with env-var pre修复es not 提示ing unless the var is k现在n-safe (`LANG`, `TZ`, `NO_COLOR`, etc.)
- 修复了 redirects to `/dev/tcp/...` or `/dev/udp/...` not 提示ing instead of auto-allowing
- 修复了 stalled 流式传输 responses timing out instead of falling back to non-流式传输 mode
- 修复了 429 retries burning all attempts in ~13s when the server returns a small `Retry-After` — exponential backoff 现在 applies as a minimum
- 修复了 MCP OAuth `oauth.authServerMetadataUrl` config override not being honored on token 刷新 after restart, affecting ADFS and similar IdPs
- 修复了 capital letters being dropped to lowercase on xterm and VS Code integrated 终端 when the kitty keyboard protocol is active
- 修复了 macOS text replacements deleting the trigger word instead of inserting the substitution
- 修复了 `--dangerously-skip-权限` being silently downgraded to accept-edits mode after approving a write to a protected 路径 via Bash
- 修复了 managed-设置 allow rules remaining active after an admin 移除 them, until process restart
- 修复了 `权限.additionalDirectories` changes not applying mid-会话 — 移除 目录 lose access immediately and 新增 ones work without restart
- 修复了 removing a 目录 from `additionalDirectories` revoking access to the same 目录 passed via `--add-dir`
- 修复了 `Bash(cmd:*)` and `Bash(git 提交 *)` wildcard 权限 rules failing to match commands with extra spaces or 标签页
- 修复了 `Bash(...)` deny rules being downgraded to a 提示 for piped commands that mix `cd` with other segments
- 修复了 false Bash 权限 提示s for `cut -d /`, `paste -d /`, `column -s /`, `awk '{print $1}' 文件`, and 文件names containing `%`
- 修复了 权限 rules with names matching JavaScript prototype properties (e.g. `toString`) causing `设置.json` to be silently ignored
- 修复了 agent team members not inheriting the leader's 权限 mode when using `--dangerously-skip-权限`
- 修复了 a 崩溃 in 全屏模式 when hovering over MCP tool results
- 修复了 copying wrapped URLs in 全屏模式 inserting spaces at line breaks
- 修复了 文件-edit diffs disappearing from the UI on `--恢复` when the edited 文件 was larger than 10KB
- 修复了 several `/恢复` picker issues: `--恢复 <name>` opening unedi标签页le, filter 重新加载 wiping search state, empty list swallowing arrow keys, cross-project staleness, and transient task-status text replacing conversation summaries
- 修复了 `/export` not honoring absolute 路径s and `~`, and silently rewriting user-supplied extensions to `.txt`
- 修复了 `/effort max` being denied for unk现在n or future model IDs
- 修复了 斜杠命令 picker breaking when a 插件's frontmatter `name` is a YAML boolean keyword
- 修复了 rate-limit upsell text being hidden after message remounts
- 修复了 MCP tools with `_meta["anthropic/maxResultSizeChars"]` not bypassing the token-based persist layer
- 修复了 voice mode leaking dozens of space characters into the input when re-holding the push-to-talk key while the previous transcript is still processing
- 修复了 `DISABLE_AUTOUPDATER` not fully suppressing the npm registry version check and symlink modification on npm-based 安装s
- 修复了 a 内存 leak where Remote Control 权限 handler entries were retained for the lifetime of the 会话
- 修复了 background 子 agent that fail with an 错误 not reporting partial progress to the parent agent
- 修复了 提示-type Stop/子 agentStop 钩子 failing on long 会话, and 钩子 evaluator API 错误 showing "JSON validation 失败" instead of the real message
- 修复了 feedback survey rendering when dismissed
- 修复了 Bash `grep -f FILE` / `rg -f FILE` not 提示ing when reading a pattern 文件 outside the working 目录
- 修复了 stale 子 agent worktree cleanup removing worktree that contain untracked 文件
- 修复了 `沙箱.network.allowMachLookup` not taking effect on macOS
- 改进了 `/恢复` filter hint labels and 新增 project/worktree/分支 names in the filter indicator
- 改进了 footer indicators (Focus, notifications) to stay on the mode-indicator row instead of wrapping at narrow 终端 widths
- 改进了 `/agents` with a 标签页bed layout: a Running 标签页 shows live 子 agent, and the Library 标签页 adds Run agent and View running instance actions
- 改进了 `/重新加载-插件` to pick up 插件-provided skills without requiring a restart
- 改进了 Accept Edits mode to auto-approve 文件ystem commands pre修复了 with safe env vars or process wrappers
- 改进了 Vim mode: `j`/`k` in NORMAL mode 现在 navigate history and select the footer pill at the input boundary
- 改进了 钩子 错误 in the transcript to include the first line of stderr for self-diagnosis without `--调试`
- 改进了 OTEL tracing: interaction spans 现在 correctly wrap full turns under concurrent SDK calls, and headless turns end spans per-turn
- 改进了 transcript entries to carry final token usage instead of 流式传输 placeholders
- 更新d the `/claude-api` skill to cover Managed Agents alongside Claude API
- [VSCode] 修复了 false-positive "requires git-bash" 错误 on Windows when `CLAUDE_CODE_GIT_BASH_PATH` is set or Git is 安装ed at a 默认 location
- 修复了 `CLAUDE_CODE_MAX_CONTEXT_TOKENS` to honor `DISABLE_COMPACT` when it is set.
- Dropped `/compact` hints when `DISABLE_COMPACT` is set.

## 2.1.97

- 新增 focus view toggle (`Ctrl+O`) in `NO_FLICKER` mode showing 提示, one-line tool summary with edit diffstats, and final response
- 新增 `刷新Interval` status line setting to re-run the status line command every N seconds
- 新增 `工作区.git_worktree` to the status line JSON input, set when the current 目录 is inside a linked git worktree
- 新增 `● N running` indicator in `/agents` next to agent types with live 子 agent instances
- 新增 语法高亮 for Cedar policy 文件 (`.cedar`, `.cedarpolicy`)
- 修复了 `--dangerously-skip-权限` being silently downgraded to accept-edits mode after approving a write to a protected 路径
- 修复了 and hardened Bash 工具 权限, tightening checks around env-var pre修复es and network redirects, and reducing false 提示s on common commands
- 修复了 权限 rules with names matching JavaScript prototype properties (e.g. `toString`) causing `设置.json` to be silently ignored
- 修复了 managed-设置 allow rules remaining active after an admin 移除 them until process restart
- 修复了 `权限.additionalDirectories` changes in 设置 not applying mid-会话
- 修复了 removing a 目录 from `设置.权限.additionalDirectories` revoking access to the same 目录 passed via `--add-dir`
- 修复了 MCP HTTP/SSE connections accumulating ~50 MB/hr of unreleased buffers when servers reconnect
- 修复了 MCP OAuth `oauth.authServerMetadataUrl` not being honored on token 刷新 after restart, 修复ing ADFS and similar IdPs
- 修复了 429 retries burning all attempts in ~13 seconds when the server returns a small `Retry-After` — exponential backoff 现在 applies as a minimum
- 修复了 rate-limit upgrade options disappearing after 上下文 compaction
- 修复了 several `/恢复` picker issues: `--恢复 <name>` opening unedi标签页le, Ctrl+A 重新加载 wiping search, empty list swallowing navigation, task-status text replacing conversation summary, and cross-project staleness
- 修复了 文件-edit diffs disappearing on `--恢复` when the edited 文件 was larger than 10KB
- 修复了 `--恢复` 缓存 misses and lost mid-turn input from attachment messages not being saved to the transcript
- 修复了 messages typed while Claude is working not being persisted to the transcript
- 修复了 提示-type `Stop`/`子 agentStop` 钩子 failing on long 会话, and 钩子 evaluator API 错误 displaying "JSON validation 失败" instead of the actual message
- 修复了 子 agent with worktree isolation or `cwd:` override leaking their working 目录 back to the parent 会话's Bash 工具
- 修复了 compaction writing duplicate multi-MB 子 agent transcript 文件 on 提示-too-long retries
- 修复了 `claude 插件 更新` reporting "already at the latest version" for git-based 市场 插件 when the remote had newer 提交s
- 修复了 斜杠命令 picker breaking when a 插件's frontmatter `name` is a YAML boolean keyword
- 修复了 copying wrapped URLs in `NO_FLICKER` mode inserting spaces at line breaks
- 修复了 scroll rendering artifacts in `NO_FLICKER` mode when running inside zellij
- 修复了 a 崩溃 in `NO_FLICKER` mode when hovering over MCP tool results
- 修复了 a `NO_FLICKER` mode 内存 leak where API retries left stale 流式传输 state
- 修复了 slow mouse-wheel scrolling in `NO_FLICKER` mode on Windows 终端
- 修复了 custom status line not displaying in `NO_FLICKER` mode on 终端s shorter than 24 rows
- 修复了 Shift+Enter and Alt/Cmd+arrow shortcuts not working in Warp with `NO_FLICKER` mode
- 修复了 Korean/Japanese/Unicode text becoming garbled when copied in no-flicker mode on Windows
- 修复了 Bedrock SigV4 authentication failing when `AWS_BEARER_TOKEN_BEDROCK` or `ANTHROPIC_BEDROCK_BASE_URL` are set to empty strings (as GitHub Actions does for unset inputs)
- 改进了 Accept Edits mode to auto-approve 文件ystem commands pre修复了 with safe env vars or process wrappers (e.g. `LANG=C rm foo`, `超时 5 mkdir out`)
- 改进了 auto mode and bypass-权限 mode to auto-approve 沙箱 network access 提示s
- 改进了 沙箱: `沙箱.network.allowMachLookup` 现在 takes effect on macOS
- 改进了 image handling: pasted and attached images are 现在 compressed to the same token budget as images read via the Read 工具
- 改进了 斜杠命令 and `@`-mention 完成 to trigger after CJK sentence punctuation, so Japanese/Chinese input no longer requires a space before `/` or `@`
- 改进了 Bridge 会话 to show the local git repo, 分支, and working 目录 on the claude.ai 会话 card
- 改进了 footer layout: indicators (Focus, notifications) 现在 stay on the mode-indicator row instead of wrapping below
- 改进了 上下文-low 警告 to show as a transient footer notification instead of a persistent row
- 改进了 markdown blockquotes to show a continuous left bar across wrapped lines
- 改进了 会话 transcript size by skipping empty 钩子 entries and capping stored pre-edit 文件 copies
- 改进了 transcript accuracy: per-block entries 现在 carry the final token usage instead of the 流式传输 placeholder
- 改进了 Bash 工具 OTEL tracing: subprocesses 现在 inherit a W3C `TRACEPARENT` env var when tracing is 启用
- 更新d `/claude-api` skill to cover Managed Agents alongside the Claude API

## 2.1.96

- 修复了 Bedrock requests failing with `403 "Authorization header is missing"` when using `AWS_BEARER_TOKEN_BEDROCK` or `CLAUDE_CODE_SKIP_BEDROCK_AUTH` (regression in 2.1.94)

## 2.1.94

- 新增 支持 for Amazon Bedrock powered by Mantle, set `CLAUDE_CODE_USE_MANTLE=1`
- 更改 默认 effort level from medium to high for API-key, Bedrock/Vertex/Foundry, Team, and Enterprise users (control this with `/effort`)
- 新增 compact `Slacked #channel` header with a clickable channel link for Slack MCP send-message tool calls
- 新增 `keep-coding-instructions` frontmatter field 支持 for 插件 output styles
- 新增 `钩子SpecificOutput.会话Title` to `User提示提交` 钩子 for setting the 会话 title
- 插件 skills declared via `"skills": ["./"]` 现在 use the skill's frontmatter `name` for the invocation name instead of the 目录 basename, giving a s标签页le name across 安装 methods
- 修复了 agents appearing 卡住 after a 429 rate-limit response with a long Retry-After header — the 错误 现在 surfaces immediately instead of silently waiting
- 修复了 Console login on macOS silently failing with "Not logged in" when the login keychain is locked or its password is out of sync — the 错误 is 现在 surfaced and `claude doctor` diagnoses the 修复
- 修复了 插件 skill 钩子 defined in YAML frontmatter being silently ignored
- 修复了 插件 钩子 failing with "No such 文件 or 目录" when `CLAUDE_PLUGIN_ROOT` was not set
- 修复了 `${CLAUDE_PLUGIN_ROOT}` resolving to the 市场 source 目录 instead of the 安装ed 缓存 for local-市场 插件 on 启动
- 修复了 sc回滚 showing the same diff repeated and blank pages in long-running 会话
- 修复了 multiline user 提示s in the transcript indenting wrapped lines under the `❯` caret instead of under the text
- 修复了 Shift+Space inserting the literal word "space" instead of a space character in search inputs
- 修复了 hyperlinks opening two browser 标签页 when clicked inside tmux running in an xterm.js-based 终端 (VS Code, Hyper, 标签页by)
- 修复了 an alt-screen rendering bug where content height changes mid-scroll could leave compounding ghost lines
- 修复了 `FORCE_HYPERLINK` 环境变量 being ignored when set via `设置.json` `env`
- 修复了 native 终端 cursor not tracking the selected 标签页 in 对话框s, so screen readers and magnifiers can follow 标签页 navigation
- 修复了 Bedrock invocation of Sonnet 3.5 v2 by using the `us.` inference pro文件 ID
- 修复了 SDK/print mode not preserving the partial assistant response in conversation history when interrupted mid-stream
- 改进了 `--恢复` to 恢复 会话 from other worktree of the same repo directly instead of printing a `cd` command
- 修复了 CJK and other multibyte text being corrupted with U+FFFD in stream-json input/output when chunk boundaries split a UTF-8 sequence
- [VSCode] Reduced cold-open subprocess work on starting a 会话
- [VSCode] 修复了 dropdown 菜单s selecting the wrong item when the mouse was over the list while typing or using arrow keys
- [VSCode] 新增 a 警告 banner when `设置.json` 文件 fail to parse, so users k现在 their 权限 rules are not being applied

## 2.1.92

- 新增 `forceRemote设置刷新` policy setting: when set, the CLI blocks 启动 until remote managed 设置 are freshly fetched, and 退出s if the fetch fails (fail-closed)
- 新增 interactive Bedrock setup wizard accessible from the login screen when selecting "3rd-party platform" — guides you through AWS authentication, region 配置, credential verification, and model pinning
- 新增 per-model and 缓存-hit breakdown to `/cost` for subscription users
- `/release-notes` is 现在 an interactive version picker
- Remote Control 会话 names 现在 use your hostname as the 默认 pre修复 (e.g. `myhost-graceful-unicorn`), overridable with `--remote-control-会话-name-pre修复`
- Pro users 现在 see a footer hint when returning to a 会话 after the 提示 缓存 has expired, showing roughly how many token the next turn will send un缓存
- 修复了 子 agent spawning permanently failing with "Could not determine pane count" after tmux windows are killed or renumbered during a long-running 会话
- 修复了 提示-type Stop 钩子 incorrectly failing when the small fast model returns `ok:false`, and 恢复d `preventContinuation:true` semantics for non-Stop 提示-type 钩子
- 修复了 tool input validation 失败s when 流式传输 emits array/object fields as JSON-encoded strings
- 修复了 an API 400 错误 that could occur when extended thinking produced a whitespace-only text block alongside real content
- 修复了 accidental feedback survey submissions from auto-pilot keypresses and consecutive-提示 digit collisions
- 修复了 misleading "esc to interrupt" hint appearing alongside "esc to clear" when a text selection exists in 全屏模式 during processing
- 修复了 Homebrew 安装 更新 提示s to use the cask's release channel (`claude-code` → s标签页le, `claude-code@latest` → latest)
- 修复了 `ctrl+e` jumping to the end of the next line when already at end of line in multiline 提示s
- 修复了 an issue where the same message could appear at two positions when scrolling up in 全屏模式 (iTerm2, Ghostty, and other 终端s with DEC 2026 支持)
- 修复了 idle-return "/clear to save X token" hint showing cumulative 会话 token instead of current 上下文 size
- 修复了 插件 MCP 服务器 卡住 "连接中" on 会话 start when they duplicate a claude.ai connector that is unauthenticated
- 改进了 Write 工具 diff computation speed for large 文件 (60% faster on 文件 with 标签页/`&`/`$`)
- 移除 `/tag` command
- 移除 `/vim` command (toggle vim mode via `/config` → Editor mode)
- Linux 沙箱 现在 ships the `apply-seccomp` helper in both npm and native builds, restoring unix-socket blocking for 沙箱ed commands

## 2.1.91

- 新增 MCP tool result persistence override via `_meta["anthropic/maxResultSizeChars"]` annotation (up to 500K), allowing larger results like DB schemas to pass through without truncation
- 新增 `禁用SkillShellExecution` setting to 禁用 inline shell execution in skills, custom 斜杠命令, and 插件 commands
- 新增 支持 for multi-line 提示s in `claude-cli://open?q=` deep links (encoded newlines `%0A` no longer rejected)
- 插件 can 现在 ship execu标签页les under `bin/` and invoke them as bare commands from the Bash 工具
- 修复了 transcript chain breaks on `--恢复` that could lose conversation history when async transcript writes fail silently
- 修复了 `cmd+删除` not deleting to start of line on iTerm2, kitty, WezTerm, Ghostty, and Windows 终端
- 修复了 plan mode in remote 会话 losing track of the plan 文件 after a container restart, which caused 权限 提示s on plan edits and an empty plan-approval 模态
- 修复了 JSON schema validation for `权限.默认Mode: "auto"` in 设置.json
- 修复了 Windows version cleanup not protecting the active version's 回滚 copy
- `/feedback` 现在 explains why it's 不可用 instead of disappearing from the slash 菜单
- 改进了 `/claude-api` skill guidance for agent design patterns including tool surface decisions, 上下文 management, and 缓存 strategy
- 改进了 performance: faster `stripAnsi` on Bun by routing through `Bun.stripANSI`
- Edit 工具 现在 uses shorter `old_string` anchors, reducing output token

## 2.1.90

- 新增 `/powerup` — interactive lessons teaching Claude Code features with animated demos
- 新增 `CLAUDE_CODE_PLUGIN_KEEP_MARKETPLACE_ON_FAILURE` env var to keep the existing 市场 缓存 when `git pull` fails, useful in offline environments
- 新增 `.husky` to protected 目录 (acceptEdits mode)
- 修复了 an infinite loop where the rate-limit options 对话框 would repeatedly auto-open after hitting your usage limit, eventually 崩溃ing the 会话
- 修复了 `--恢复` causing a full 提示-缓存 miss on the first request for users with deferred tools, MCP 服务器, or custom agents (regression since v2.1.69)
- 修复了 `Edit`/`Write` failing with "文件 content has 更改" when a PostToolUse format-on-save 钩子 rewrites the 文件 between consecutive edits
- 修复了 `PreToolUse` 钩子 that emit JSON to stdout and 退出 with code 2 not correctly blocking the tool call
- 修复了 collapsed search/read summary badge appearing multiple times in fullscreen sc回滚 when a CLAUDE.md 文件 auto-加载s during a tool call
- 修复了 auto mode not respecting explicit user boundaries ("don't push", "wait for X before Y") even when the action would otherwise be allowed
- 修复了 click-to-expand hover text being nearly invisible on light 终端 themes
- 修复了 UI 崩溃 when malformed tool input reached the 权限 对话框
- 修复了 headers disappearing when scrolling `/model`, `/config`, and other selection screens
- Hardened PowerShell tool 权限 checks: 修复了 trailing `&` background job bypass, `-错误Action Break` 调试ger hang, archive-extraction TOCTOU, and parse-fail fallback deny-rule degradation
- 改进了 performance: eliminated per-turn JSON.stringify of MCP tool schemas on 缓存-key lookup
- 改进了 performance: SSE transport 现在 handles large streamed frames in linear time (was quadratic)
- 改进了 performance: SDK 会话 with long conversations no longer slow down quadratically on transcript writes
- 改进了 `/恢复` all-projects view to 加载 project 会话 in parallel, improving 加载 times for users with many projects
- 更改 `--恢复` picker to no longer show 会话 创建d by `claude -p` or SDK invocations
- 移除 `Get-DnsClient缓存` and `ipconfig /displaydns` from auto-allow (DNS 缓存 privacy)

## 2.1.89

- 新增 `"defer"` 权限 decision to `PreToolUse` 钩子 — headless 会话 can 暂停 at a tool call and 恢复 with `-p --恢复` to have the 钩子 re-evaluate
- 新增 `CLAUDE_CODE_NO_FLICKER=1` 环境变量 to opt into flicker-free alt-screen rendering with virtualized sc回滚
- 新增 `权限Denied` 钩子 that fires after auto mode classifier denials — return `{retry: true}` to tell the model it can retry
- 新增 named 子 agent to `@` mention typeahead suggestions
- 新增 `MCP_CONNECTION_NONBLOCKING=true` for `-p` mode to skip the MCP connection wait entirely, and bounded `--mcp-config` server connections at 5s instead of blocking on the slowest server
- Auto mode: denied commands 现在 show a notification and appear in `/权限` → Recent 标签页 where you can retry with `r`
- 修复了 `Edit(//路径/**)` and `Read(//路径/**)` allow rules to check the resolved symlink target, not just the requested 路径
- 修复了 voice push-to-talk not activating for some modifier-combo bindings, and voice mode on Windows failing with "WebSocket upgrade rejected with HTTP 101"
- 修复了 Edit/Write 工具s doubling CRLF on Windows and stripping Markdown hard line breaks (two trailing spaces)
- 修复了 `StructuredOutput` schema 缓存 bug causing ~50% 失败 rate when using multiple schemas
- 修复了 内存 leak where large JSON inputs were retained as LRU 缓存 keys in long-running 会话
- 修复了 a 崩溃 when removing a message from very large 会话 文件 (over 50MB)
- 修复了 LSP server zombie state after 崩溃 — server 现在 restarts on next request instead of failing until 会话 restart
- 修复了 提示 history entries containing CJK or emoji being silently dropped when they fall on a 4KB boundary in `~/.claude/history.jsonl`
- 修复了 `/stats` undercounting token by excluding 子 agent usage, and losing historical data beyond 30 days when the stats 缓存 format changes
- 修复了 `-p --恢复` hangs when the deferred tool input exceeds 64KB or no deferred marker exists, and `-p --continue` not resuming deferred tools
- 修复了 `claude-cli://` deep links not opening on macOS
- 修复了 MCP tool 错误 truncating to only the first content block when the server returns multi-element 错误 content
- 修复了 skill reminders and other system 上下文 being dropped when sending messages with images via the SDK
- 修复了 PreToolUse/PostToolUse 钩子 to receive `文件_路径` as an absolute 路径 for Write/Edit/Read 工具s, matching the documented behavior
- 修复了 autocompact thrash loop — 现在 detects when 上下文 refills to the limit immediately after compacting three times in a row and stops with an actionable 错误 instead of burning API calls
- 修复了 提示 缓存 misses in long 会话 caused by tool schema bytes changing mid-会话
- 修复了 nested CLAUDE.md 文件 being re-injected dozens of times in long 会话 that read many 文件
- 修复了 `--恢复` 崩溃 when transcript contains a tool result from an older CLI version or interrupted write
- 修复了 misleading "速率限制 reached" message when the API returned an entitlement 错误 — 现在 shows the actual 错误 with actionable hints
- 修复了 钩子 `if` condition filtering not matching compound commands (`ls && git push`) or commands with env-var pre修复es (`FOO=bar git push`)
- 修复了 collapsed search/read group badges duplicating in 终端 sc回滚 during heavy parallel tool use
- 修复了 notification `invalidates` not clearing the currently-displayed notification immediately
- 修复了 提示 briefly disappearing after 提交 when background messages arrived during processing
- 修复了 Devanagari and other combining-mark text being truncated in assistant output
- 修复了 rendering artifacts on main-screen 终端s after layout shifts
- 修复了 voice mode failing to request microphone 权限 on macOS Apple Silicon
- 修复了 Shift+Enter 提交ting instead of inserting a newline on Windows 终端 Preview 1.25
- 修复了 periodic UI jitter during 流式传输 in iTerm2 when running inside tmux
- 修复了 PowerShell tool incorrectly reporting 失败s when commands like `git push` wrote progress to stderr on Windows PowerShell 5.1
- 修复了 a potential out-of-内存 崩溃 when the Edit 工具 was used on very large 文件 (>1 GiB)
- 改进了 collapsed tool summary to show "Listed N 目录" for `ls`/`tree`/`du` instead of "Read N 文件"
- 改进了 Bash 工具 to warn when a formatter/linter command modifies 文件 you have 之前 read, preventing stale-edit 错误
- 改进了 `@`-mention typeahead to rank source 文件 above MCP resources with similar names
- 改进了 PowerShell tool 提示 with version-appropriate syntax guidance (5.1 vs 7+)
- 更改 `Edit` to work on 文件 viewed via `Bash` with `sed -n` or `cat`, without requiring a separate `Read` call first
- 更改 钩子 output over 50K characters to be saved to 磁盘 with a 文件 路径 + preview instead of being injected directly into 上下文
- 更改 `cleanupPeriodDays: 0` in 设置.json to be rejected with a validation 错误 — it 之前 silently 禁用 transcript persistence
- 更改 thinking summaries to no longer be generated by 默认 in interactive 会话 — set `showThinkingSummaries: true` in 设置.json to 恢复
- Documented `Task创建d` 钩子 event and its blocking behavior
- Preserved task notifications when backgrounding a running command with Ctrl+B
- PowerShell tool on Windows: external-command arguments containing both a double-quote and whitespace 现在 提示 instead of auto-allowing (PS 5.1 argument-splitting hardening)
- `/env` 现在 applies to PowerShell tool commands (之前 only affected Bash)
- `/usage` 现在 hides redundant "Current week (Sonnet only)" bar for Pro and Enterprise plans
- Image paste no longer inserts a trailing space
- Pasting `!command` into an empty 提示 现在 enters bash mode, matching typed `!` behavior
- `/buddy` is here for April 1st — hatch a small creature that watches you code

## 2.1.87

- 修复了 messages in Cowork Dispatch not getting delivered

## 2.1.86

- 新增 `X-Claude-Code-会话-Id` header to API requests so proxies can aggregate requests by 会话 without parsing the body
- 新增 `.jj` and `.sl` to VCS 目录 exclusion lists so Grep and 文件 自动完成 don't descend into Jujutsu or Sapling metadata
- 修复了 `--恢复` failing with "tool_use ids were found without tool_result blocks" on 会话 创建d before v2.1.85
- 修复了 Write/Edit/Read failing on 文件 outside the project root (e.g., `~/.claude/CLAUDE.md`) when conditional skills or rules are configured
- 修复了 unnecessary config 磁盘 writes on every skill invocation that could cause performance issues and config corruption on Windows
- 修复了 potential out-of-内存 崩溃 when using `/feedback` on very long 会话 with large transcript 文件
- 修复了 `--bare` mode dropping MCP tools in interactive 会话 and silently discarding messages enqueued mid-turn
- 修复了 the `c` shortcut copying only ~20 characters of the OAuth login URL instead of the full URL
- 修复了 masked input (e.g., OAuth code paste) leaking the start of the token when wrapping across multiple lines on narrow 终端s
- 修复了 official 市场 插件 scripts failing with "权限 denied" on macOS/Linux since v2.1.83
- 修复了 statusline showing another 会话's model when running multiple Claude Code instances and using `/model` in one of them
- 修复了 scroll not following new messages after wheel scroll or click-to-select at the bottom of a long conversation
- 修复了 `/插件` 卸载 对话框: pressing `n` 现在 correctly 卸载s the 插件 while preserving its data 目录
- 修复了 a regression where pressing Enter after clicking could leave the transcript blank until the response arrived
- 修复了 `ultrathink` hint lingering after deleting the keyword
- 修复了 内存 growth in long 会话 from markdown/highlight render 缓存s retaining full content strings
- Reduced 启动 event-loop stalls when many claude.ai MCP connectors are configured (macOS keychain 缓存 extended from 5s to 30s)
- Reduced token overhead when mentioning 文件 with `@` — raw string content no longer JSON-escaped
- 改进了 提示 缓存 hit rate for Bedrock, Vertex, and Foundry users by removing dynamic content from tool descriptions
- 内存 文件names in the "Saved N memories" notice 现在 highlight on hover and open on click
- Skill descriptions in the `/skills` listing are 现在 capped at 250 characters to reduce 上下文 usage
- 更改 `/skills` 菜单 to sort alphabetically for easier scanning
- Auto mode 现在 shows "不可用 for your plan" when 禁用 by plan restrictions (was "temporarily 不可用")
- [VSCode] 修复了 extension incorrectly showing "Not responding" during long-running operations
- [VSCode] 修复了 extension 默认ing Max plan users to Sonnet after the OAuth token 刷新es (8 hours after login)
- Read 工具 现在 uses compact line-number format and deduplicates un更改 re-reads, reducing token usage

## 2.1.85

- 新增 `CLAUDE_CODE_MCP_SERVER_NAME` and `CLAUDE_CODE_MCP_SERVER_URL` 环境变量 to MCP `headersHelper` scripts, allowing one helper to serve multiple servers
- 新增 conditional `if` field for 钩子 using 权限 rule syntax (e.g., `Bash(git *)`) to filter when they run, reducing process spawning overhead
- 新增 timestamp markers in transcripts when scheduled tasks (`/loop`, `Cron创建`) fire
- 新增 trailing space after `[Image #N]` placeholder when pasting images
- Deep link queries (`claude-cli://open?q=…`) 现在 支持 up to 5,000 characters, with a "scroll to review" 警告 for long pre-filled 提示s
- MCP OAuth 现在 follows RFC 9728 Protected Resource Metadata discovery to find the authorization server
- 插件 blocked by organization policy (`managed-设置.json`) can no longer be 安装ed or 启用, and are hidden from 市场 views
- PreToolUse 钩子 can 现在 satisfy `AskUserQuestion` by returning `更新dInput` alongside `权限Decision: "allow"`, enabling headless integrations that collect answers via their own UI
- `tool_parameters` in Open遥测 tool_result events are 现在 gated behind `OTEL_LOG_TOOL_DETAILS=1`
- 修复了 `/compact` failing with "上下文 exceeded" when the conversation has grown too large for the compact request itself to fit
- 修复了 `/插件 启用` and `/插件 禁用` failing when a 插件's 安装 location differs from where it's declared in 设置
- 修复了 `--worktree` 退出ing with an 错误 in non-git repositories before the `Worktree创建` 钩子 could run
- 修复了 `deniedMcpServers` setting not blocking claude.ai MCP 服务器
- 修复了 `switch_display` in the computer-use tool returning "not 可用 in this 会话" on multi-monitor setups
- 修复了 崩溃 when `OTEL_LOGS_EXPORTER`, `OTEL_METRICS_EXPORTER`, or `OTEL_TRACES_EXPORTER` is set to `none`
- 修复了 diff 语法高亮 not working in non-native builds
- 修复了 MCP step-up authorization failing when a 刷新 token exists — servers requesting elevated scopes via `403 insufficient_scope` 现在 correctly trigger the re-authorization flow
- 修复了 内存 leak in remote 会话 when a 流式传输 response is interrupted
- 修复了 persistent ECONNRESET 错误 during edge connection churn by using a fresh TCP connection on retry
- 修复了 提示s getting 卡住 in the queue after running certain 斜杠命令, with up-arrow unable to retrieve them
- 修复了 Python Agent SDK: `type:'sdk'` MCP 服务器 passed via `--mcp-config` are no longer dropped during 启动
- 修复了 raw key sequences appearing in the 提示 when running over SSH or in the VS Code integrated 终端
- 修复了 Remote Control 会话 status staying 卡住 on "Requires Action" after a 权限 is resolved
- 修复了 shift+enter and meta+enter being intercepted by typeahead suggestions instead of inserting newlines
- 修复了 stale content bleeding through when scrolling up during 流式传输
- 修复了 终端 left in enhanced keyboard mode after 退出 in Ghostty, Kitty, WezTerm, and other 终端s 支持ing the Kitty keyboard protocol — Ctrl+C and Ctrl+D 现在 work correctly after quitting
- 改进了 @-mention 文件 自动完成 performance on large repositories
- 改进了 PowerShell dangerous command detection
- 改进了 scroll performance with large transcripts by replacing WASM yoga-layout with a pure TypeScript implementation
- Reduced UI stutter when compaction triggers on large 会话

## 2.1.84

- 新增 PowerShell tool for Windows as an opt-in preview. Learn more at https://code.claude.com/docs/en/tools-reference#powershell-tool
- 新增 `ANTHROPIC_DEFAULT_{OPUS,SONNET,HAIKU}_MODEL_SUPPORTS` env vars to override effort/thinking capability detection for pinned 默认 models for 3p (Bedrock, Vertex, Foundry), and `_MODEL_NAME`/`_DESCRIPTION` to customize the `/model` picker label
- 新增 `CLAUDE_STREAM_IDLE_TIMEOUT_MS` env var to configure the 流式传输 idle watchdog threshold (默认 90s)
- 新增 `Task创建d` 钩子 that fires when a task is 创建d via `Task创建`
- 新增 `Worktree创建` 钩子 支持 for `type: "http"` — return the 创建d worktree 路径 via `钩子SpecificOutput.worktree路径` in the response JSON
- 新增 `allowedChannel插件` managed setting for team/enterprise admins to define a channel 插件 allowlist
- 新增 `x-client-request-id` header to API requests for 调试ging 超时s
- 新增 idle-return 提示 that nudges users returning after 75+ minutes to `/clear`, reducing unnecessary token re-缓存 on stale 会话
- Deep links (`claude-cli://`) 现在 open in your preferred 终端 instead of whichever 终端 happens to be first in the detection list
- Rules and skills `路径s:` frontmatter 现在 accepts a YAML list of globs
- MCP tool descriptions and server instructions are 现在 capped at 2KB to prevent OpenAPI-generated servers from bloating 上下文
- MCP 服务器 configured both locally and via claude.ai connectors are 现在 deduplicated — the local config wins
- Background bash tasks that appear 卡住 on an interactive 提示 现在 surface a notification after ~45 seconds
- token counts ≥1M 现在 display as "1.5m" instead of "1512.6k"
- Global system-提示 缓存 现在 works when `ToolSearch` is 启用, including for users with MCP tools configured
- 修复了 voice push-to-talk: holding the voice key no longer leaks characters into the text input, and transcripts 现在 insert at the correct position
- 修复了 up/down arrow keys being unresponsive when a footer item is focused
- 修复了 `Ctrl+U` (kill-to-line-start) being a no-op at line boundaries in multiline input, so repeated `Ctrl+U` 现在 clears across lines
- 修复了 null-unbinding a 默认 chord binding (e.g. `"ctrl+x ctrl+k": null`) still entering chord-wait mode instead of freeing the pre修复 key
- 修复了 mouse events inserting literal "mouse" text into transcript search input
- 修复了 workflow 子 agent failing with API 400 when the outer 会话 uses `--json-schema` and the 子 agent also specifies a schema
- 修复了 missing background color behind certain emoji in user message bubbles on some 终端s
- 修复了 the "allow Claude to edit its own 设置 for this 会话" 权限 option not sticking for users with `Edit(.claude)` allow rules
- 修复了 a hang when generating attachment 代码片段s for large edited 文件
- 修复了 MCP tool/resource 缓存 leak on server reconnect
- 修复了 a 启动 performance issue where partial clone repositories (Scalar/GVFS) triggered mass blob down加载s
- 修复了 native 终端 cursor not tracking the text input caret, so IME composition (CJK input) 现在 renders inline and screen readers can follow the input position
- 修复了 spurious "Not logged in" 错误 on macOS caused by transient keychain read 失败s
- 修复了 cold-start race where core tools could be deferred without their bypass active, causing Edit/Write to fail with InputValidation错误 on typed parameters
- 改进了 detection for dangerous removals of Windows drive roots (`C:\`, `C:\Windows`, etc.)
- 改进了 interactive 启动 by ~30ms by running `setup()` in parallel with 斜杠命令 and agent 加载ing
- 改进了 启动 for `claude "提示"` with MCP 服务器 — the REPL 现在 renders immediately instead of blocking until all servers connect
- 改进了 Remote Control to show a specific reason when blocked instead of a generic "not yet 启用" message
- 改进了 p90 提示 缓存 rate
- Reduced scroll-to-top resets in long 会话 by making the message window immune to compaction and grouping changes
- Reduced 终端 flickering when animated tool progress scrolls above the viewport
- 更改 issue/PR references to only become clickable links when written as `owner/repo#123` — bare `#123` is no longer auto-linked
- Slash commands 不可用 for the current auth setup (`/voice`, `/mobile`, `/chrome`, `/upgrade`, etc.) are 现在 hidden instead of shown
- [VSCode] 新增 速率限制 警告 banner with usage percentage and reset time
- Stats screenshot (Ctrl+S in /stats) 现在 works in all builds and is 16× faster

## 2.1.83

- 新增 `managed-设置.d/` drop-in 目录 alongside `managed-设置.json`, letting separate teams deploy independent policy fragments that 合并 alphabetically
- 新增 `Cwd更改` and `文件更改` 钩子 events for reactive environment management (e.g., direnv)
- 新增 `沙箱.failIfUn可用` setting to 退出 with an 错误 when 沙箱 is 启用 but cannot start, instead of running un沙箱ed
- 新增 `禁用DeepLinkRegistration` setting to prevent `claude-cli://` protocol handler registration
- 新增 `CLAUDE_CODE_SUBPROCESS_ENV_SCRUB=1` to strip Anthropic and cloud provider credentials from subprocess environments (Bash 工具, 钩子, MCP stdio servers)
- 新增 transcript search — press `/` in transcript mode (`Ctrl+O`) to search, `n`/`N` to step through matches
- 新增 `Ctrl+X Ctrl+E` as an alias for opening the external editor (readline-native binding; `Ctrl+G` still works)
- Pasted images 现在 insert an `[Image #N]` chip at the cursor so you can reference them positionally in your 提示
- Agents can 现在 declare `initial提示` in frontmatter to auto-提交 a first turn
- `chat:killAgents` and `chat:fastMode` are 现在 rebindable via `~/.claude/keybindings.json`
- 修复了 mouse tracking escape sequences leaking to shell 提示 after 退出
- 修复了 Claude Code hanging on 退出 on macOS
- 修复了 screen flashing blank after being idle for a few seconds
- 修复了 a hang when diffing very large 文件 with few common lines — diffs 现在 time out after 5 seconds and fall back gracefully
- 修复了 a 1–8 second UI freeze on 启动 when voice input was 启用, caused by eagerly 加载ing the native audio module
- 修复了 a 启动 regression where Claude Code would wait ~3s for claude.ai MCP config fetch before proceeding
- 修复了 `--mcp-config` CLI 标志 bypassing `allowedMcpServers`/`deniedMcpServers` managed policy enforcement
- 修复了 claude.ai MCP connectors (Slack, Gmail, etc.) not being 可用 in single-turn `--print` mode
- 修复了 `caffeinate` process not properly terminating when Claude Code 退出s, preventing Mac from sleeping
- 修复了 bash mode not activating when 标签页-accepting `!`-pre修复了 command suggestions
- 修复了 stale 斜杠命令 selection showing wrong highlighted command after navigating suggestions
- 修复了 `/config` 菜单 showing both the search cursor and list selection at the same time
- 修复了 background 子 agent becoming invisible after 上下文 compaction, which could cause duplicate agents to be spawned
- 修复了 background agent tasks staying 卡住 in "running" state when git or API calls hang during cleanup
- 修复了 `--channels` showing "Channels are not currently 可用" on first launch after upgrade
- 修复了 卸载ed 插件 钩子 continuing to fire until the next 会话
- 修复了 queued commands flickering during 流式传输 responses
- 修复了 斜杠命令 being sent to the model as text when 提交ted while a message is processing
- 修复了 sc回滚 jumping when collapsed read/search groups finish after scrolling offscreen
- 修复了 sc回滚 jumping to top when the model starts or stops thinking
- 修复了 SDK 会话 history loss on 恢复 caused by 钩子 progress/attachment messages forking the parentUuid chain
- 修复了 copy-on-select not firing when you release the mouse outside the 终端 window
- 修复了 ghost characters appearing in height-constrained lists when items overflow
- 修复了 `Ctrl+B` interfering with readline backward-char at an idle 提示 — it 现在 only fires when a foreground task can be backgrounded
- 修复了 tool result 文件 never being cleaned up, ignoring the `cleanupPeriodDays` setting
- 修复了 space key being swallowed for up to 3 seconds after releasing voice hold-to-talk
- 修复了 ALSA library 错误 corrupting the 终端 UI when using voice mode on Linux without audio hardware (Docker, headless, WSL1)
- 修复了 voice mode SoX detection on Termux/Android where spawning `which` is kernel-restricted
- 修复了 Remote Control 会话 showing as Idle in the web 会话 list while actively running
- 修复了 footer navigation selecting an invisible Remote Control pill in config-driven mode
- 修复了 内存 leak in remote 会话 where tool use IDs accumulate indefinitely
- 改进了 Bedrock SDK cold-start latency by overlapping pro文件 fetch with other boot work
- 改进了 `--恢复` 内存 usage and 启动 latency on large 会话
- 改进了 插件 启动 — commands, skills, and agents 现在 加载 from 磁盘 缓存 without re-fetching
- 改进了 Remote Control 会话 titles: AI-generated titles 现在 appear within seconds of the first message
- 改进了 `WebFetch` to identify as `Claude-User` so site operators can recognize and allowlist Claude Code traffic via `robots.txt`
- Reduced `WebFetch` peak 内存 usage for large pages
- Reduced sc回滚 resets in long 会话 from once per turn to once per ~50 messages
- Faster `claude -p` 启动 with unauthenticated HTTP/SSE MCP 服务器 (~600ms saved)
- Bash ghost-text suggestions 现在 include just-提交ted commands immediately
- Increased non-流式传输 fallback token cap (21k → 64k) and 超时 (120s → 300s local) so fallback requests are less likely to be truncated
- Interrupting a 提示 before any response 现在 automatically 恢复s your input so you can edit and re提交
- `/status` 现在 works while Claude is responding, instead of being queued until the turn finishes
- 插件 MCP 服务器 that duplicate an org-managed connector are 现在 suppressed instead of running a second connection
- Linux: respect `XDG_DATA_HOME` when registering the `claude-cli://` protocol handler
- 更改 "stop all background agents" keybinding from `Ctrl+F` to `Ctrl+X Ctrl+K` to stop shadowing readline forward-char
- 弃用 `TaskOutput` tool in favor of using `Read` on the background task's output 文件 路径
- 新增 `CLAUDE_CODE_DISABLE_NONSTREAMING_FALLBACK` env var to 禁用 the non-流式传输 fallback when 流式传输 fails
- 插件 options (`manifest.userConfig`) 现在 可用 externally — 插件 can 提示 for 配置 at 启用 time, with `sensitive: true` values stored in keychain (macOS) or protected credentials 文件 (other platforms)
- Claude can 现在 reference the on-磁盘 路径 of clipboard-pasted images for 文件 operations
- `Ctrl+L` 现在 clears the screen and forces a full redraw — use this to recover when Cmd+K leaves the UI partially blank. Use `Ctrl+U` or double-Esc to clear 提示 input.
- `--bare -p` (SDK pattern) is ~14% faster to the API request
- 内存: `MEMORY.md` index 现在 truncates at 25KB as well as 200 lines
- 禁用 `AskUserQuestion` and plan-mode tools when `--channels` is active
- 修复了 API 400 错误 when a pasted image was queued during a failing tool call
- 修复了 MCP tool calls hanging indefinitely when an SSE connection drops mid-call and exhausts its reconnection attempts
- 修复了 Remote Control 会话 titles showing raw XML when a background agent completed before the first user message
- 修复了 remote 会话 forgetting conversation history after a container restart due to progress-message gaps in the 恢复d transcript chain
- 修复了 remote 会话 requiring re-login on transient auth 错误 instead of retrying automatically
- 修复了 `rg ... | wc -l` and similar piped commands hanging and returning `0` in 沙箱 mode on Linux
- 修复了 voice input hold-to-talk not activating when a CJK IME inserts a full-width space
- 修复了 `--worktree` hanging silently when the worktree name contained a forward slash
- [VSCode] Spinner 现在 turns red with "Not responding" when the backend hasn't responded for 60 seconds
- [VSCode] 修复了 会话 history not 加载ing correctly when reopening a 会话 via URL or after restart
- [VSCode] 新增 Esc-twice (or `/rewind`) to open a keyboard-navigable rewind picker
- [VSCode] 修复了 "Fork conversation from here" and rewind actions failing silently after the 会话 缓存 goes stale

## 2.1.81

- 新增 `--bare` 标志 for scripted `-p` calls — skips 钩子, LSP, 插件 sync, and skill 目录 walks; requires `ANTHROPIC_API_KEY` or an `apiKeyHelper` via `--设置` (OAuth and keychain auth 禁用); auto-内存 fully 禁用
- 新增 `--channels` 权限 relay — channel servers that declare the 权限 capability can forward tool approval 提示s to your phone
- 修复了 multiple concurrent Claude Code 会话 requiring repeated re-authentication when one 会话 刷新es its OAuth token
- 修复了 voice mode silently swallowing retry 失败s and showing a misleading "check your network" message instead of the actual 错误
- 修复了 voice mode audio not recovering when the server silently drops the WebSocket connection
- 修复了 `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` not suppressing the structured-outputs beta header, causing 400 错误 on proxy gateways forwarding to Vertex/Bedrock
- 修复了 `--channels` bypass for Team/Enterprise orgs with no other managed 设置 configured
- 修复了 a 崩溃 on Node.js 18
- 修复了 unnecessary 权限 提示s for Bash commands containing dashes in strings
- 修复了 插件 钩子 blocking 提示 submission when the 插件 目录 is 删除d mid-会话
- 修复了 a race condition where background agent task output could hang indefinitely when the task completed between polling intervals
- Resuming a 会话 that was in a worktree 现在 switches back to that worktree
- 修复了 `/btw` not including pasted text when used during an active response
- 修复了 a race where fast Cmd+标签页 followed by paste could beat the clipboard copy under tmux
- 修复了 终端 标签页 title not updating with an auto-generated 会话 description
- 修复了 invisible 钩子 attachments inflating the message count in transcript mode
- 修复了 Remote Control 会话 showing a generic title instead of deriving from the first 提示
- 修复了 `/rename` not syncing the title for Remote Control 会话
- 修复了 Remote Control `/退出` not reliably archiving the 会话
- 改进了 MCP read/search tool calls to collapse into a single "Queried {server}" line (expand with Ctrl+O)
- 改进了 `!` bash mode discoverability — Claude 现在 suggests it when you need to run an interactive command
- 改进了 插件 freshness — ref-tracked 插件 现在 re-clone on every 加载 to pick up upstream changes
- 改进了 Remote Control 会话 titles to 刷新 after your third message
- 更新d MCP OAuth to 支持 Client ID Metadata Document (CIMD / SEP-991) for servers without Dynamic Client Registration
- 更改 plan mode to hide the "clear 上下文" option by 默认 (恢复 with `"showClear上下文OnPlanAccept": true`)
- 禁用 line-by-line response 流式传输 on Windows (including WSL in Windows 终端) due to rendering issues
- [VSCode] 修复了 Windows PATH inheritance for Bash 工具 when using Git Bash (regression in v2.1.78)

## 2.1.80

- 新增 `rate_limits` field to statusline scripts for displaying Claude.ai 速率限制 usage (5-hour and 7-day windows with `used_percentage` and `resets_at`)
- 新增 `source: '设置'` 插件 市场 source — declare 插件 entries inline in 设置.json
- 新增 CLI tool usage detection to 插件 tips, in addition to 文件 pattern matching
- 新增 `effort` frontmatter 支持 for skills and 斜杠命令 to override the model effort level when invoked
- 新增 `--channels` (research preview) — allow MCP 服务器 to push messages into your 会话
- 修复了 `--恢复` dropping parallel tool results — 会话 with parallel tool calls 现在 恢复 all tool_use/tool_result pairs instead of showing `[Tool result missing]` placeholders
- 修复了 voice mode WebSocket 失败s caused by Cloudflare bot detection on non-browser TLS fingerprints
- 修复了 400 错误 when using fine-grained tool 流式传输 through API proxies, Bedrock, or Vertex
- 修复了 `/remote-control` appearing for gateway and third-party provider deployments where it cannot function
- 修复了 `/沙箱` 标签页 switching not responding to 标签页 or arrow keys
- 改进了 responsiveness of `@` 文件 自动完成 in large git repositories
- 改进了 `/effort` to show what auto currently resolves to, matching the 状态栏 indicator
- 改进了 `/权限` — 标签页 and arrow keys 现在 switch 标签页 from within a list
- 改进了 background tasks panel — left arrow 现在 closes from the list view
- Simplified 插件 安装 tips to use a single `/插件 安装` command instead of a two-step flow
- Reduced 内存 usage on 启动 in large repositories (~80 MB saved on 250k-文件 repos)
- 修复了 managed 设置 (`启用插件`, `权限.默认Mode`, policy-set env vars) not being applied at 启动 when `remote-设置.json` was 缓存 from a prior 会话

## 2.1.79

- 新增 `--console` 标志 to `claude auth login` for Anthropic Console (API billing) authentication
- 新增 "Show turn duration" toggle to the `/config` 菜单
- 修复了 `claude -p` hanging when spawned as a subprocess without explicit stdin (e.g. Python `subprocess.run`)
- 修复了 Ctrl+C not working in `-p` (print) mode
- 修复了 `/btw` returning the main agent's output instead of answering the side question when triggered during 流式传输
- 修复了 voice mode not activating correctly on 启动 when `voice启用: true` is set
- 修复了 left/right arrow 标签页 navigation in `/权限`
- 修复了 `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` not preventing 终端 title from being set on 启动
- 修复了 custom status line showing nothing when 工作区 trust is blocking it
- 修复了 enterprise users being unable to retry on 速率限制 (429) 错误
- 修复了 `会话End` 钩子 not firing when using interactive `/恢复` to switch 会话
- 改进了 启动 内存 usage by ~18MB across all scenarios
- 改进了 non-流式传输 API fallback with a 2-minute per-attempt 超时, preventing 会话 from hanging indefinitely
- `CLAUDE_CODE_PLUGIN_SEED_DIR` 现在 支持 multiple seed 目录 separated by the platform 路径 delimiter (`:` on Unix, `;` on Windows)
- [VSCode] 新增 `/remote-control` — bridge your 会话 to claude.ai/code to continue from a browser or phone
- [VSCode] 会话 标签页 现在 get AI-generated titles based on your first message
- [VSCode] 修复了 the thinking pill showing "Thinking" instead of "Thought for Ns" after a response completes
- [VSCode] 修复了 missing 会话 diff button when opening 会话 from the left sidebar

## 2.1.78

- 新增 `Stop失败` 钩子 event that fires when the turn ends due to an API 错误 (速率限制, auth 失败, etc.)
- 新增 `${CLAUDE_PLUGIN_DATA}` variable for 插件 persistent state that survives 插件 更新s; `/插件 卸载` 提示s before deleting it
- 新增 `effort`, `maxTurns`, and `disallowedTools` frontmatter 支持 for 插件-shipped agents
- 终端 notifications (iTerm2/Kitty/Ghostty popups, progress bar) 现在 reach the outer 终端 when running inside tmux with `set -g allow-passthrough on`
- Response text 现在 streams line-by-line as it's generated
- 修复了 `git log HEAD` failing with "ambiguous argument" inside 沙箱ed Bash on Linux, and stub 文件 polluting `git status` in the working 目录
- 修复了 `cc log` and `--恢复` silently truncating conversation history on large 会话 (>5 MB) that used 子 agent
- 修复了 infinite loop when API 错误 triggered stop 钩子 that re-fed blocking 错误 to the model
- 修复了 `deny: ["mcp__servername"]` 权限 rules not removing MCP 服务器 tools before sending to the model, allowing it to see and attempt blocked tools
- 修复了 `沙箱.文件ystem.allowWrite` not working with absolute 路径s (之前 required `//` pre修复)
- 修复了 `/沙箱` Dependencies 标签页 showing Linux prerequisites on macOS instead of macOS-specific info
- **安全：** 修复了 silent 沙箱 禁用 when `沙箱.启用: true` is set but dependencies are missing — 现在 shows a visible 启动 警告
- 修复了 `.git`, `.claude`, and other protected 目录 being wri标签页le without a 提示 in `bypass权限` mode
- 修复了 ctrl+u in normal mode scrolling instead of readline kill-line (ctrl+u/ctrl+d half-page scroll moved to transcript mode only)
- 修复了 voice mode modifier-combo push-to-talk keybindings (e.g. ctrl+k) requiring a hold instead of activating immediately
- 修复了 voice mode not working on WSL2 with WSLg (Windows 11); WSL1/Win10 users 现在 get a clear 错误
- 修复了 `--worktree` 标志 not 加载ing skills and 钩子 from the worktree 目录
- 修复了 `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` and `includeGitInstructions` setting not suppressing the git status section in the system 提示
- 修复了 Bash 工具 not finding Homebrew and other PATH-dependent binaries when VS Code is launched from Dock/Spotlight
- 修复了 washed-out Claude orange color in VS Code/Cursor/code-server 终端s that don't advertise truecolor 支持
- 新增 `ANTHROPIC_CUSTOM_MODEL_OPTION` env var to add a custom entry to the `/model` picker, with 可选 `_NAME` and `_DESCRIPTION` suf修复了 vars for display
- 修复了 `ANTHROPIC_BETAS` 环境变量 being silently ignored when using Haiku models
- 修复了 queued 提示s being concatenated without a newline separator
- 改进了 内存 usage and 启动 time when resuming large 会话
- [VSCode] 修复了 a brief flash of the login screen when opening the sidebar while already authenticated
- [VSCode] 修复了 "API 错误: 速率限制 reached" when selecting Opus — model dropdown no longer offers 1M 上下文 variant to subscribers whose plan tier is unk现在n

## 2.1.77

- Increased 默认 maximum output token limits for Claude Opus 4.6 to 64k token, and the upper bound for Opus 4.6 and Sonnet 4.6 models to 128k token
- 新增 `allowRead` 沙箱 文件ystem setting to re-allow read access within `denyRead` regions
- `/copy` 现在 accepts an 可选 index: `/copy N` copies the Nth-latest assistant response
- 修复了 "Always Allow" on compound bash commands (e.g. `cd src && npm test`) saving a single rule for the full string instead of per-subcommand, leading to dead rules and repeated 权限 提示s
- 修复了 auto-更新r starting overlapping binary down加载s when the slash-command overlay repeatedly opened and closed, accumulating tens of gigabytes of 内存
- 修复了 `--恢复` silently truncating recent conversation history due to a race between 内存-extraction writes and the main transcript
- 修复了 PreToolUse 钩子 returning `"allow"` bypassing `deny` 权限 rules, including enterprise managed 设置
- 修复了 Write 工具 silently converting line endings when overwriting CRLF 文件 or creating 文件 in CRLF 目录
- 修复了 内存 growth in long-running 会话 from progress messages surviving compaction
- 修复了 cost and token usage not being tracked when the API falls back to non-流式传输 mode
- 修复了 `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` not stripping beta tool-schema fields, causing proxy gateways to reject requests
- 修复了 Bash 工具 reporting 错误 for 成功ful commands when the system temp 目录 路径 contains spaces
- 修复了 paste being lost when typing immediately after pasting
- 修复了 Ctrl+D in `/feedback` text input deleting forward instead of the second press 退出ing the 会话
- 修复了 API 错误 when dragging a 0-byte image 文件 into the 提示
- 修复了 Claude Desktop 会话 incorrectly using the 终端 CLI's configured API key instead of OAuth
- 修复了 `git-subdir` 插件 at different sub目录 of the same monorepo 提交 colliding in the 插件 缓存
- 修复了 ordered list numbers not rendering in 终端 UI
- 修复了 a race condition where stale-worktree cleanup could 删除 an agent worktree just 恢复d from a previous 崩溃
- 修复了 input deadlock when opening `/mcp` or similar 对话框s while the agent is running
- 修复了 Backspace and 删除 keys not working in vim NORMAL mode
- 修复了 status line not updating when vim mode is toggled on or off
- 修复了 hyperlinks opening twice on Cmd+click in VS Code, Cursor, and other xterm.js-based 终端s
- 修复了 background colors rendering as 终端-默认 inside tmux with 默认 配置
- 修复了 iTerm2 会话 崩溃 when selecting text inside tmux over SSH
- 修复了 clipboard copy silently failing in tmux 会话; copy toast 现在 indicates whether to paste with `⌘V` or tmux `pre修复+]`
- 修复了 `←`/`→` accidentally switching 标签页 in 设置, 权限, and 沙箱 对话框s while navigating lists
- 修复了 IDE integration not auto-连接中 when Claude Code is launched inside tmux or screen
- 修复了 CJK characters visually bleeding into adjacent UI elements when clipped at the right edge
- 修复了 teammate panes not closing when the leader 退出s
- 修复了 iTerm2 auto mode not detecting iTerm2 for native split-pane teammates
- Faster 启动 on macOS (~60ms) by reading keychain credentials in parallel with module 加载ing
- Faster `--恢复` on fork-heavy and very large 会话 — up to 45% faster 加载ing and ~100-150MB less peak 内存
- 改进了 Esc to abort in-flight non-流式传输 API requests
- 改进了 `claude 插件 validate` to check skill, agent, and command frontmatter plus `钩子/钩子.json`, catching YAML parse 错误 and schema violations
- Background bash tasks are 现在 killed if output exceeds 5GB, preventing runaway processes from filling 磁盘
- 会话 are 现在 auto-named from plan content when you accept a plan
- 改进了 headless mode 插件 安装ation to compose correctly with `CLAUDE_CODE_PLUGIN_SEED_DIR`
- Show a notice when `apiKeyHelper` takes longer than 10s, preventing it from blocking the main loop
- The Agent 工具 no longer accepts a `恢复` parameter — use `SendMessage({to: agentId})` to continue a 之前 spawned agent
- `SendMessage` 现在 auto-恢复s stopped agents in the background instead of returning an 错误
- Renamed `/fork` to `/分支` (`/fork` still works as an alias)
- [VSCode] 改进了 plan preview 标签页 titles to use the plan's heading instead of "Claude's Plan"
- [VSCode] When option+click doesn't trigger native selection on macOS, the footer 现在 points to the `macOptionClickForcesSelection` setting

## 2.1.76

- 新增 MCP elicitation 支持 — MCP 服务器 can 现在 request structured input mid-task via an interactive 对话框 (form fields or browser URL)
- 新增 new `Elicitation` and `ElicitationResult` 钩子 to intercept and override responses before they're sent back
- 新增 `-n` / `--name <name>` CLI 标志 to set a display name for the 会话 at 启动
- 新增 `worktree.sparse路径s` setting for `claude --worktree` in large monorepos to check out only the 目录 you need via git sparse-checkout
- 新增 `PostCompact` 钩子 that fires after compaction completes
- 新增 `/effort` 斜杠命令 to set model effort level
- 新增 会话 quality survey — enterprise admins can configure the sample rate via the `feedbackSurveyRate` setting
- 修复了 deferred tools (加载ed via `ToolSearch`) losing their input schemas after conversation compaction, causing array and number parameters to be rejected with type 错误
- 修复了 斜杠命令 showing "Unk现在n skill"
- 修复了 plan mode asking for re-approval after the plan was already accepted
- 修复了 voice mode swallowing keypresses while a 权限 对话框 or plan editor was open
- 修复了 `/voice` not working on Windows when 安装ed via npm
- 修复了 spurious "上下文限制已达到" when invoking a skill with `model:` frontmatter on a 1M-上下文 会话
- 修复了 "adaptive thinking is not 支持ed on this model" 错误 when using non-standard model strings
- 修复了 `Bash(cmd:*)` 权限 rules not matching when a quoted argument contains `#`
- 修复了 "don't ask again" in the Bash 权限 对话框 showing the full raw command for pipes and compound commands
- 修复了 auto-compaction retrying indefinitely after consecutive 失败s — a circuit breaker 现在 stops after 3 attempts
- 修复了 MCP reconnect spinner persisting after 成功ful reconnection
- 修复了 LSP 插件 not registering servers when the LSP Manager initialized before 市场 were reconciled
- 修复了 clipboard copying in tmux over SSH — 现在 attempts both direct 终端 write and tmux clipboard integration
- 修复了 `/export` showing only the 文件name instead of the full 文件 路径 in the 成功 message
- 修复了 transcript not auto-scrolling to new messages after selecting text
- 修复了 Escape key not working to 退出 the login method selection screen
- 修复了 several Remote Control issues: 会话 silently dying when the server reaps an idle environment, rapid messages being queued one-at-a-time instead of batched, and stale work items causing redelivery after JWT 刷新
- 修复了 bridge 会话 failing to recover after extended WebSocket disconnects
- 修复了 斜杠命令 未找到 when typing the exact name of a soft-hidden command
- 改进了 `--worktree` 启动 performance by reading git refs directly and skipping redundant `git fetch` when the remote 分支 is already 可用 locally
- 改进了 background agent behavior — killing a background agent 现在 preserves its partial results in the conversation 上下文
- 改进了 model fallback notifications — 现在 always visible instead of hidden behind 详细 mode, with human-friendly model names
- 改进了 blockquote readability on dark 终端 themes — text is 现在 italic with a left bar instead of dim
- 改进了 stale worktree cleanup — worktree left behind after an interrupted parallel run are 现在 automatically cleaned up
- 改进了 Remote Control 会话 titles — 现在 derived from your first 提示 instead of showing "Interactive 会话"
- 改进了 `/voice` to show your dictation language on 启用 and warn when your `language` setting isn't 支持ed for voice input
- 更新d `--插件-dir` to only accept one 路径 to 支持 subcommands — use repeated `--插件-dir` for multiple 目录
- [VSCode] 修复了 gitignore patterns containing commas silently excluding entire 文件types from the @-mention 文件 picker

## 2.1.75

- 新增 1M 上下文 window for Opus 4.6 by 默认 for Max, Team, and Enterprise plans (之前 required extra usage)
- 新增 `/color` command for all users to set a 提示-bar color for your 会话
- 新增 会话 name display on the 提示 bar when using `/rename`
- 新增 last-modified timestamps to 内存 文件, helping Claude reason about which memories are fresh vs. stale
- 新增 钩子 source display (设置/插件/skill) in 权限 提示s when a 钩子 requires 确认ation
- 修复了 voice mode not activating correctly on fresh 安装s without toggling `/voice` twice
- 修复了 the Claude Code header not updating the displayed model name after switching models with `/model` or Option+P
- 修复了 会话 崩溃 when an attachment message computation returns undefined values
- 修复了 Bash 工具 mangling `!` in piped commands (e.g., `jq 'select(.x != .y)'` 现在 works correctly)
- 修复了 managed-禁用 插件 showing up in the `/插件` 安装ed 标签页 — 插件 force-禁用 by your organization are 现在 hidden
- 修复了 token estimation over-counting for thinking and `tool_use` blocks, preventing premature 上下文 compaction
- 修复了 corrupted 市场 config 路径 handling
- 修复了 `/恢复` losing 会话 names after resuming a forked or continued 会话
- 修复了 Esc not closing the `/status` 对话框 after visiting the Config 标签页
- 修复了 input handling when accepting or rejecting a plan
- 修复了 footer hint in agent teams showing "↓ to expand" instead of the correct "shift + ↓ to expand"
- 改进了 启动 performance on macOS non-MDM machines by skipping unnecessary subprocess spawns
- Suppressed async 钩子 完成 messages by 默认 (visible with `--详细` or transcript mode)
- 破坏性更改: 移除 弃用 Windows managed 设置 fallback at `C:\ProgramData\ClaudeCode\managed-设置.json` — use `C:\Program 文件\ClaudeCode\managed-设置.json`

## 2.1.74

- 新增 actionable suggestions to `/上下文` command — identifies 上下文-heavy tools, 内存 bloat, and capacity 警告 with specific optimization tips
- 新增 `auto内存目录` setting to configure a custom 目录 for auto-内存 storage
- 修复了 内存 leak where 流式传输 API response buffers were not released when the generator was terminated early, causing unbounded RSS growth on the Node.js/npm code 路径
- 修复了 managed policy `ask` rules being bypassed by user `allow` rules or skill `allowed-tools`
- 修复了 full model IDs (e.g., `claude-opus-4-5`) being silently ignored in agent frontmatter `model:` field and `--agents` JSON config — agents 现在 accept the same model values as `--model`
- 修复了 MCP OAuth authentication hanging when the callback port is already in use
- 修复了 MCP OAuth 刷新 never 提示ing for re-auth after the 刷新 token expires, for OAuth servers that return 错误 with HTTP 200 (e.g. Slack)
- 修复了 voice mode silently failing on the macOS native binary for users whose 终端 had never been granted microphone 权限 — the binary 现在 includes the `audio-input` entitlement so macOS 提示s correctly
- 修复了 `会话End` 钩子 being killed after 1.5 s on 退出 regardless of `钩子.超时` — 现在 configurable via `CLAUDE_CODE_SESSIONEND_HOOKS_TIMEOUT_MS`
- 修复了 `/插件 安装` failing inside the REPL for 市场 插件 with local sources
- 修复了 市场 更新 not syncing git submodules — 插件 sources in submodules no longer break after 更新
- 修复了 unk现在n 斜杠命令 with arguments silently dropping input — 现在 shows your input as a 警告
- 修复了 Hebrew, Arabic, and other RTL text not rendering correctly in Windows 终端, conhost, and VS Code integrated 终端
- 修复了 LSP servers not working on Windows due to malformed 文件 URIs
- 更改 `--插件-dir` so local dev copies 现在 override 安装ed 市场 插件 with the same name (unless that 插件 is force-启用 by managed 设置)
- [VSCode] 修复了 删除 button not working for Untitled 会话
- [VSCode] 改进了 scroll wheel responsiveness in the integrated 终端 with 终端-aware acceleration

## 2.1.73

- 新增 `modelOverrides` setting to map model picker entries to custom provider model IDs (e.g. Bedrock inference pro文件 ARNs)
- 新增 actionable guidance when OAuth login or connectivity checks fail due to SSL certificate 错误 (corporate proxies, `NODE_EXTRA_CA_CERTS`)
- 修复了 freezes and 100% CPU loops triggered by 权限 提示s for complex bash commands
- 修复了 a deadlock that could freeze Claude Code when many skill 文件 更改 at once (e.g. during `git pull` in a repo with a large `.claude/skills/` 目录)
- 修复了 Bash 工具 output being lost when running multiple Claude Code 会话 in the same project 目录
- 修复了 子 agent with `model: opus`/`sonnet`/`haiku` being silently downgraded to older model versions on Bedrock, Vertex, and Microsoft Foundry
- 修复了 background bash processes spawned by 子 agent not being cleaned up when the agent 退出s
- 修复了 `/恢复` showing the current 会话 in the picker
- 修复了 `/ide` 崩溃ing with `on安装 is not defined` when auto-安装ing the extension
- 修复了 `/loop` not being 可用 on Bedrock/Vertex/Foundry and when 遥测 was 禁用
- 修复了 会话Start 钩子 firing twice when resuming a 会话 via `--恢复` or `--continue`
- 修复了 JSON-output 钩子 injecting no-op system-reminder messages into the model's 上下文 on every turn
- 修复了 voice mode 会话 corruption when a slow connection overlaps a new recording
- 修复了 Linux 沙箱 failing to start with "ripgrep (rg) 未找到" on native builds
- 修复了 Linux native modules not 加载ing on Amazon Linux 2 and other glibc 2.26 systems
- 修复了 "media_type: Field required" API 错误 when receiving images via Remote Control
- 修复了 `/heapdump` failing on Windows with `EEXIST` 错误 when the Desktop folder 已存在
- 改进了 Up arrow after interrupting Claude — 现在 恢复s the interrupted 提示 and rewinds the conversation in one step
- 改进了 IDE detection speed at 启动
- 改进了 clipboard image pasting performance on macOS
- 改进了 `/effort` to work while Claude is responding, matching `/model` behavior
- 改进了 voice mode to automatically retry transient connection 失败s during rapid push-to-talk re-press
- 改进了 Remote Control spawn mode selection 提示 with better 上下文
- 更改 默认 Opus model on Bedrock, Vertex, and Microsoft Foundry to Opus 4.6 (was Opus 4.1)
- 弃用 `/output-style` command — use `/config` instead. Output style is 现在 修复了 at 会话 start for better 提示 缓存
- VSCode: 修复了 HTTP 400 错误 for users behind proxies or on Bedrock/Vertex with Claude 4.5 models

## 2.1.72

- 修复了 tool search to activate even with `ANTHROPIC_BASE_URL` as long as `ENABLE_TOOL_SEARCH` is set.
- 新增 `w` key in `/copy` to write the focused selection directly to a 文件, bypassing the clipboard (useful over SSH)
- 新增 可选 description argument to `/plan` (e.g., `/plan 修复 the auth bug`) that enters plan mode and immediately starts
- 新增 `退出Worktree` tool to leave an `EnterWorktree` 会话
- 新增 `CLAUDE_CODE_DISABLE_CRON` 环境变量 to immediately stop scheduled cron jobs mid-会话
- 新增 `lsof`, `pgrep`, `tput`, `ss`, `fd`, and `fdfind` to the bash auto-approval allowlist, reducing 权限 提示s for common read-only operations
- 恢复d the `model` parameter on the Agent 工具 for per-invocation model overrides
- Simplified effort levels to low/medium/high (移除 max) with new symbols (○ ◐ ●) and a brief notification instead of a persistent icon. Use `/effort auto` to reset to 默认
- 改进了 `/config` — Escape 现在 取消s changes, Enter saves and closes, Space toggles 设置
- 改进了 up-arrow history to show current 会话's messages first when running multiple concurrent 会话
- 改进了 voice input transcription accuracy for repo names and common dev terms (regex, OAuth, JSON)
- 改进了 bash command parsing by switching to a native module — faster initialization and no 内存 leak
- Reduced bundle size by ~510 KB
- 更改 CLAUDE.md HTML comments (`<!-- ... -->`) to be hidden from Claude when auto-injected. Comments remain visible when read with the Read 工具
- 修复了 slow 退出s when background tasks or 钩子 were slow to respond
- 修复了 agent task progress 卡住 on "Initializing…"
- 修复了 skill 钩子 firing twice per event when a 钩子-启用 skill is invoked by the model
- 修复了 several voice mode issues: occasional input lag, false "No speech detected" 错误 after releasing push-to-talk, and stale transcripts re-filling the 提示 after submission
- 修复了 `--continue` not resuming from the most recent point after `--compact`
- 修复了 bash security parsing edge cases
- 新增 支持 for 市场 git URLs without `.git` suf修复 (Azure DevOps, AWS Code提交)
- 改进了 市场 clone 失败 messages to show diagnostic info even when git produces no stderr
- 修复了 several 插件 issues: 安装ation failing on Windows with `EEXIST` 错误 in OneDrive folders, 市场 blocking user-scope 安装s when a project-scope 安装 exists, `CLAUDE_CODE_PLUGIN_CACHE_DIR` creating literal `~` 目录, and `插件.json` with 市场-only fields failing to 加载
- 修复了 feedback survey appearing too frequently in long 会话
- 修复了 `--effort` CLI 标志 being reset by unrelated 设置 writes on 启动
- 修复了 backgrounded Ctrl+B queries losing their transcript or corrupting the new conversation after `/clear`
- 修复了 `/clear` killing background agent/bash tasks — only foreground tasks are 现在 cleared
- 修复了 worktree isolation issues: Task 工具 恢复 not restoring cwd, and background task notifications missing `worktree路径` and `worktree分支`
- 修复了 `/model` not displaying results when run while Claude is working
- 修复了 digit keys selecting 菜单 options instead of typing in plan mode 权限 提示's text input
- 修复了 沙箱 权限 issues: certain 文件 write operations incorrectly allowed without 提示ing, and output redirections to allowlisted 目录 (like `/tmp/claude/`) 提示ing unnecessarily
- 改进了 CPU utilization in long 会话
- 修复了 提示 缓存 invalidation in SDK `query()` calls, reducing input token costs up to 12x
- 修复了 Escape key becoming unresponsive after 取消ling a query
- 修复了 double Ctrl+C not 退出ing when background agents or tasks are running
- 修复了 team agents to inherit the leader's model
- 修复了 "Always Allow" saving 权限 rules that never match again
- 修复了 several 钩子 issues: `transcript_路径` pointing to the wrong 目录 for 恢复d/forked 会话, agent `提示` being silently 删除d from 设置.json on every 设置 write, PostToolUse block reason displaying twice, async 钩子 not receiving stdin with bash `read -r`, and validation 错误 message showing an example that fails validation
- 修复了 会话 崩溃es in Desktop/SDK when Read returned 文件 containing U+2028/U+2029 characters
- 修复了 终端 title being cleared on 退出 even when `CLAUDE_CODE_DISABLE_TERMINAL_TITLE` was set
- 修复了 several 权限 rule matching issues: wildcard rules not matching commands with heredocs, embedded newlines, or no arguments; `沙箱.excludedCommands` failing with env var pre修复es; "always allow" suggesting overly broad pre修复es for nested CLI tools; and deny rules not applying to all command forms
- 修复了 oversized and truncated images from Bash data-URL output
- 修复了 a 崩溃 when resuming 会话 that contained Bedrock API 错误
- 修复了 intermittent "expected boolean, received string" validation 错误 on Edit, Bash, and Grep 工具 inputs
- 修复了 multi-line 会话 titles when forking from a conversation whose first message contained newlines
- 修复了 queued messages not showing attached images, and images being lost when pressing ↑ to edit a queued message
- 修复了 parallel tool calls where a 失败 Read/WebFetch/Glob would 取消 its siblings — only Bash 错误 现在 cascade
- VSCode: 修复了 scroll speed in integrated 终端s not matching native 终端s
- VSCode: 修复了 Shift+Enter 提交ting input instead of inserting a newline for users with older keybindings
- VSCode: 新增 effort level indicator on the input border
- VSCode: 新增 `vscode://anthropic.claude-code/open` URI handler to open a new Claude Code 标签页 programmatically, with 可选 `提示` and `会话` query parameters

## 2.1.71

- 新增 `/loop` command to run a 提示 or 斜杠命令 on a recurring interval (e.g. `/loop 5m check the deploy`)
- 新增 cron scheduling tools for recurring 提示s within a 会话
- 新增 `voice:pushToTalk` keybinding to make the voice activation key rebindable in `keybindings.json` (默认: space) — modifier+letter combos like `meta+k` have zero typing interference
- 新增 `fmt`, `comm`, `cmp`, `numfmt`, `expr`, `test`, `printf`, `getconf`, `seq`, `tsort`, and `pr` to the bash auto-approval allowlist
- 修复了 stdin freeze in long-running 会话 where keystrokes stop being processed but the process stays alive
- 修复了 a 5–8 second 启动 freeze for users with voice mode 启用, caused by CoreAudio initialization blocking the main thread after system wake
- 修复了 启动 UI freeze when many claude.ai proxy connectors 刷新 an expired OAuth token simultaneously
- 修复了 forked conversations (`/fork`) sharing the same plan 文件, which caused plan edits in one fork to overwrite the other
- 修复了 the Read 工具 putting oversized images into 上下文 when image processing 失败, breaking subsequent turns in long image-heavy 会话
- 修复了 false-positive 权限 提示s for compound bash commands containing heredoc 提交 messages
- 修复了 插件 安装ations being lost when running multiple Claude Code instances
- 修复了 claude.ai connectors failing to reconnect after OAuth token 刷新
- 修复了 claude.ai MCP connector 启动 notifications appearing for every org-configured connector instead of only 之前 connected ones
- 修复了 background agent 完成 notifications missing the output 文件 路径, which made it difficult for parent agents to recover agent results after 上下文 compaction
- 修复了 duplicate output in Bash 工具 错误 messages when commands 退出 with non-zero status
- 修复了 Chrome extension auto-detection getting permanently 卡住 on "not 安装ed" after running on a machine without local Chrome
- 修复了 `/插件 市场 更新` failing with 合并 conflicts when the 市场 is pinned to a 分支/tag ref
- 修复了 `/插件 市场 add owner/repo@ref` incorrectly parsing `@` — 之前 only `#` worked as a ref separator, causing undiagnosable 错误 with `strictK现在n市场s`
- 修复了 duplicate entries in `/权限` 工作区 标签页 when the same 目录 is 新增 with and without a trailing slash
- 修复了 `--print` hanging forever when team agents are configured — the 退出 loop no longer waits on long-lived `in_process_teammate` tasks
- 修复了 "❯ Tool 加载ed." appearing in the REPL after every `ToolSearch` call
- 修复了 提示ing for `cd <cwd> && git ...` on Windows when the model uses a mingw-style 路径
- 改进了 启动 time by deferring native image processor 加载ing to first use
- 改进了 bridge 会话 reconnection to complete within seconds after laptop wake from sleep, instead of waiting up to 10 minutes
- 改进了 `/插件 卸载` to 禁用 project-scoped 插件 in `.claude/设置.local.json` instead of modifying `.claude/设置.json`, so changes don't affect teammates
- 改进了 插件-provided MCP 服务器 deduplication — servers that duplicate a manually-configured server (same command/URL) are 现在 skipped, preventing duplicate connections and tool sets. Suppressions are shown in the `/插件` 菜单.
- 更新d `/调试` to toggle 调试 logging on mid-会话, since 调试 logs are no longer written by 默认
- 移除 启动 notification noise for unauthenticated org-registered claude.ai connectors

## 2.1.70

- 修复了 API 400 错误 when using `ANTHROPIC_BASE_URL` with a third-party gateway — tool search 现在 correctly detects proxy endpoints and 禁用s `tool_reference` blocks
- 修复了 `API 错误: 400 This model does not 支持 the effort parameter` when using custom Bedrock inference pro文件 or other model identifiers not matching standard Claude naming patterns
- 修复了 empty model responses immediately after `ToolSearch` — the server renders tool schemas with system-提示-style tags at the 提示 tail, which could confuse models into stopping early
- 修复了 提示-缓存 bust when an MCP 服务器 with `instructions` connects after the first turn
- 修复了 Enter inserting a newline instead of 提交ting when typing over a slow SSH connection
- 修复了 clipboard corrupting non-ASCII text (CJK, emoji) on Windows/WSL by using PowerShell `Set-Clipboard`
- 修复了 extra VS Code windows opening at 启动 on Windows when running from the VS Code integrated 终端
- 修复了 voice mode failing on Windows native binary with "native audio module could not be 加载ed"
- 修复了 push-to-talk not activating on 会话 start when `voice启用: true` was set in 设置
- 修复了 markdown links containing `#NNN` references incorrectly pointing to the current repository instead of the linked URL
- 修复了 repeated "Model 更新d to Opus 4.6" notification when a project's `.claude/设置.json` has a legacy Opus model string pinned
- 修复了 插件 showing as inaccurately 安装ed in `/插件`
- 修复了 插件 showing "未找到 in 市场" 错误 on fresh 启动 by auto-刷新ing after 市场 安装ation
- 修复了 `/security-review` command failing with `unk现在n option 合并-base` on older git versions
- 修复了 `/color` command having no way to reset back to the 默认 color — `/color 默认`, `/color gray`, `/color reset`, and `/color none` 现在 恢复 the 默认
- 修复了 a performance regression in the `AskUserQuestion` preview 对话框 that re-ran markdown rendering on every keystroke in the notes input
- 修复了 feature 标志s read during early 启动 never 刷新ing their 磁盘 缓存, causing stale values to persist across 会话
- 修复了 `权限.默认Mode` 设置 values other than `acceptEdits` or `plan` being applied in Claude Code Remote environments — they are 现在 ignored
- 修复了 skill listing being re-injected on every `--恢复` (~600 token saved per 恢复)
- 修复了 teleport marker not rendering in VS Code teleported 会话
- 改进了 错误 message when microphone captures silence to distinguish from "no speech detected"
- 改进了 compaction to preserve images in the summarizer request, allowing 提示 缓存 reuse for faster and cheaper compaction
- 改进了 `/rename` to work while Claude is processing, instead of being silently queued
- Reduced 提示 input re-renders during turns by ~74%
- Reduced 启动 内存 by ~426KB for users without custom CA certificates
- Reduced Remote Control `/poll` rate to once per 10 minutes while connected (was 1–2s), cutting server 加载 ~300×. Reconnection is unaffected — transport loss immediately wakes fast polling.
- [VSCode] 新增 spark icon in VS Code activity bar that lists all Claude Code 会话, with 会话 opening as full editors
- [VSCode] 新增 full markdown document view for plans in VS Code, with 支持 for adding comments to provide feedback
- [VSCode] 新增 native MCP 服务器 management 对话框 — use `/mcp` in the chat panel to 启用/禁用 servers, reconnect, and manage OAuth authentication without switching to the 终端

## 2.1.69

- 新增 the `/claude-api` skill for building applications with the Claude API and Anthropic SDK
- 新增 Ctrl+U on an empty bash 提示 (`!`) to 退出 bash mode, matching `escape` and `backspace`
- 新增 numeric keypad 支持 for selecting options in Claude's interview questions (之前 only the number row above QWERTY worked)
- 新增 可选 name argument to `/remote-control` and `claude remote-control` (`/remote-control My Project` or `--name "My Project"`) to set a custom 会话 title visible in claude.ai/code
- 新增 Voice STT 支持 for 10 new languages (20 total) — Russian, Polish, Turkish, Dutch, Ukrainian, Greek, Czech, Danish, Swedish, Norwegian
- 新增 effort level display (e.g., "with low effort") to the logo and spinner, making it easier to see which effort setting is active
- 新增 agent name display in 终端 title when using `claude --agent`
- 新增 `沙箱.启用WeakerNetworkIsolation` setting (macOS only) to allow Go programs like `gh`, `gcloud`, and `terraform` to verify TLS certificates when using a custom MITM proxy with `httpProxyPort`
- 新增 `includeGitInstructions` setting (and `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` env var) to remove built-in 提交 and PR workflow instructions from Claude's system 提示
- 新增 `/重新加载-插件` command to activate 待处理 插件 changes without restarting
- 新增 a one-time 启动 提示 suggesting Claude Code Desktop on macOS and Windows (max 3 showings, dismissible)
- 新增 `${CLAUDE_SKILL_DIR}` variable for skills to reference their own 目录 in SKILL.md content
- 新增 `Instructions加载ed` 钩子 event that fires when CLAUDE.md or `.claude/rules/*.md` 文件 are 加载ed into 上下文
- 新增 `agent_id` (for 子 agent) and `agent_type` (for 子 agent and `--agent`) to 钩子 events
- 新增 `worktree` field to status line 钩子 commands with name, 路径, 分支, and original repo 目录 when running in a `--worktree` 会话
- 新增 `插件TrustMessage` in managed 设置 to append organization-specific 上下文 to the 插件 trust 警告 shown before 安装ation
- 新增 policy limit fetching (e.g., remote control restrictions) for Team plan OAuth users, not just Enterprise
- 新增 `路径Pattern` to `strictK现在n市场s` for regex-matching 文件/目录 市场 sources alongside `hostPattern` restrictions
- 新增 插件 source type `git-subdir` to point to a sub目录 within a git repo
- 新增 `oauth.authServerMetadataUrl` config option for MCP 服务器 to specify a custom OAuth metadata discovery URL when standard discovery fails
- 修复了安全 issue where nested skill discovery could 加载 skills from gitignored 目录 like `node_modules`
- 修复了 trust 对话框 silently enabling all `.mcp.json` servers on first run. You'll 现在 see the per-server approval 对话框 as expected
- 修复了 `claude remote-control` 崩溃ing immediately on npm 安装s with "bad option: --sdk-url" (anthropics/claude-code#28334)
- 修复了 `--model claude-opus-4-0` and `--model claude-opus-4-1` resolving to 弃用 Opus versions instead of current
- 修复了 macOS keychain corruption when using multiple OAuth MCP 服务器. Large OAuth metadata blobs could overflow the `security -i` stdin buffer, silently leaving stale credentials behind and causing repeated `/login` 提示s.
- 修复了 `.credentials.json` losing `subscriptionType` (showing "Claude API" instead of "Claude Pro"/"Claude Max") when the pro文件 endpoint transiently fails during token 刷新 (anthropics/claude-code#30185)
- 修复了 ghost dot文件 (`.bashrc`, `HEAD`, etc.) appearing as untracked 文件 in the working 目录 after 沙箱ed Bash commands on Linux
- 修复了 Shift+Enter printing `[27;2;13~` instead of inserting a newline in Ghostty over SSH
- 修复了 stash (Ctrl+S) being cleared when 提交ting a message while Claude is working
- 修复了 ctrl+o (transcript toggle) freezing for many seconds in long 会话 with lots of 文件 edits
- 修复了 plan mode feedback input not 支持ing multi-line text entry (backslash+Enter and Shift+Enter 现在 insert newlines)
- 修复了 cursor not moving down into blank lines at the top of the input box
- 修复了 `/stats` 崩溃 when transcript 文件 contain entries with missing or malformed timestamps
- 修复了 a brief hang after a 流式传输 错误 on long 会话 (the transcript was being fully rewritten to drop one line; it is 现在 truncated in place)
- 修复了 `--setting-sources user` not blocking dynamically discovered project skills
- 修复了 duplicate CLAUDE.md, 斜杠命令, agents, and rules when running from a worktree nested inside its main repo (e.g. `claude -w`)
- 修复了 插件 Stop/会话End/etc 钩子 not firing after any `/插件` operation
- 修复了 插件 钩子 being silently dropped when two 插件 use the same `${CLAUDE_PLUGIN_ROOT}/...` command template
- 修复了 内存 leak in long-running SDK/CCR 会话 where conversation messages were retained unnecessarily
- 修复了 API 400 错误 in forked agents (autocompact, summarization) when resuming 会话 that were interrupted mid-tool-batch
- 修复了 "unexpected tool_use_id found in tool_result blocks" 错误 when resuming conversations that start with an orphaned tool result
- 修复了 teammates accidentally spawning nested teammates via the Agent 工具's `name` parameter
- 修复了 `CLAUDE_CODE_MAX_OUTPUT_TOKENS` being ignored during conversation compaction
- 修复了 `/compact` summary rendering as a user bubble in SDK consumers (Claude Code Remote web UI, VSCode extension)
- 修复了 voice space bar getting 卡住 after a 失败 voice activation (module 加载ing race, cold GrowthBook)
- 修复了 worktree 文件 copy on Windows
- 修复了 global `.claude` folder detection on Windows
- 修复了 symlink bypass where writing new 文件 through a symlinked parent 目录 could escape the working 目录 in `acceptEdits` mode
- 修复了 沙箱 提示ing users to approve non-allowed domains when `allowManagedDomainsOnly` is 启用 in managed 设置 — non-allowed domains are 现在 blocked automatically with no bypass
- 修复了 interactive tools (e.g., `AskUserQuestion`) being silently auto-allowed when listed in a skill's allowed-tools, bypassing the 权限 提示 and running with empty answers
- 修复了 multi-GB 内存 spike when 提交ting with large untracked binary 文件 in the working tree
- 修复了 Escape not interrupting a running turn when the input box has draft text. Use Up arrow to pull queued messages back for editing, or Ctrl+U to clear the input line.
- 修复了 Android app 崩溃 when running local 斜杠命令 (`/voice`, `/cost`) in Remote Control 会话
- 修复了 a 内存 leak where old message array versions accumulated in React Compiler `memo缓存` over long 会话
- 修复了 a 内存 leak where REPL render scopes accumulated over long 会话 (~35MB over 1000 turns)
- 修复了 内存 retention in in-process teammates where the parent's full conversation history was pinned for the teammate's lifetime, preventing GC after `/clear` or auto-compact
- 修复了 a 内存 leak in interactive mode where 钩子 events could accumulate unboundedly during long 会话
- 修复了 hang when `--mcp-config` points to a corrupted 文件
- 修复了 slow 启动 when many skills/插件 are 安装ed
- 修复了 `cd <outside-dir> && <cmd>` 权限 提示 to surface the chained command instead of only showing "Yes, allow reading from <dir>/"
- 修复了 conditional `.claude/rules/*.md` 文件 (with `路径s:` frontmatter) and nested CLAUDE.md 文件 not 加载ing in print mode (`claude -p`)
- 修复了 `/clear` not fully clearing all 会话 缓存s, reducing 内存 retention in long 会话
- 修复了 终端 flicker caused by animated elements at the sc回滚 boundary
- 修复了 UI frame drops on macOS when using MCP 服务器 with OAuth (regression from 2.1.x)
- 修复了 occasional frame stalls during typing caused by synchronous 调试 log flushes
- 修复了 `TeammateIdle` and `TaskCompleted` 钩子 to 支持 `{"continue": false, "stopReason": "..."}` to stop the teammate, matching `Stop` 钩子 behavior
- 修复了 `Worktree创建` and `WorktreeRemove` 插件 钩子 being silently ignored
- 修复了 skill descriptions with colons (e.g., "Triggers include: X, Y, Z") failing to 加载 from SKILL.md frontmatter
- 修复了 project skills without a `description:` frontmatter field not appearing in Claude's 可用 skills list
- 修复了 `/上下文` showing identical token counts for all MCP tools from a server
- 修复了 literal `nul` 文件 creation on Windows when the model uses CMD-style `2>nul` redirection in Git Bash
- 修复了 extra blank lines appearing below each tool call in the expanded 子 agent transcript view (Ctrl+O)
- 修复了 标签页/arrow keys not cycling 设置 标签页 when `/config` search box is focused but empty
- 修复了 service key OAuth 会话 (CCR containers) spamming `[ERROR]` logs with 403s from pro文件-scoped endpoints
- 修复了 inconsistent color for "Remote Control active" status indicator
- 修复了 Voice waveform cursor covering the first suf修复 letter when dictating mid-input
- 修复了 Voice input showing all 5 spaces during warmup instead of capping at ~2 (aligning with the "keep holding…" hint)
- 改进了 spinner performance by isolating the 50ms animation loop from the surrounding shell, reducing render and CPU overhead during turns
- 改进了 UI rendering performance in native binaries with React Compiler
- 改进了 `--worktree` 启动 by eliminating a git subprocess on the 启动 路径
- 改进了 macOS 启动 by eliminating redundant 设置-文件 重新加载s when managed 设置 resolve
- 改进了 macOS 启动 for Claude.ai enterprise/team users by skipping an unnecessary keychain lookup
- 改进了 MCP `-p` 启动 by pipelining claude.ai config fetch with local connections and using a concurrency pool instead of sequential batching
- 改进了 voice 启动 by removing imperceptible warmup pulse animations that were causing re-render stutter
- 改进了 MCP binary content handling: tools returning PDFs, Office documents, or audio 现在 save decoded bytes to 磁盘 with the correct 文件 extension instead of dumping raw base64 into the conversation 上下文. WebFetch also saves binary responses alongside its summary.
- 改进了 内存 usage in long 会话 by s标签页ilizing `on提交` across message 更新s
- 改进了 LSP tool rendering and 内存 上下文 building to no longer read entire 文件
- 改进了 会话 up加载 and 内存 sync to avoid reading large 文件 into 内存 before size/binary checks
- 改进了 文件 operation performance by avoiding reading 文件 contents for existence checks (6 sites)
- 改进了 documentation to clarify that `--append-system-提示-文件` and `--system-提示-文件` work in interactive mode (the docs 之前 said print mode only)
- Reduced baseline 内存 by ~16MB by deferring Yoga WASM p重新加载ing
- Reduced 内存 footprint for SDK and CCR 会话 using stream-json output
- Reduced 内存 usage when resuming large 会话 (including compacted history)
- Reduced token usage on multi-agent tasks with more concise 子 agent final reports
- 更改 Sonnet 4.5 users on Pro/Max/Team Premium to be automatically 迁移d to Sonnet 4.6
- 更改 the `/恢复` picker to show your most recent 提示 instead of the first one. This also resolves some titles appearing as `(会话)`.
- 更改 claude.ai MCP connector 失败s to show a notification instead of silently disappearing from the tool list
- 更改 example command suggestions to be generated deterministically instead of calling Haiku
- 更改 resuming after compaction to no longer produce a preamble recap before continuing
- [SDK] 更改 task creation to no longer require the `activeForm` field — the spinner falls back to the task subject
- [VSCode] 新增 compaction display as a collapsible "Compacted chat" card with the summary inside
- [VSCode] The 权限 mode picker 现在 respects `权限.禁用Bypass权限Mode` from your effective Claude Code 设置 (including managed/policy 设置) — when set to `禁用`, bypass 权限 mode is hidden from the picker
- [VSCode] 修复了 RTL text (Arabic, Hebrew, Persian) rendering reversed in the chat panel (regression in v2.1.63)

## 2.1.68

- Opus 4.6 现在 默认s to medium effort for Max and Team subscribers. Medium effort works well for most tasks — it's the sweet spot between speed and thoroughness. You can change this anytime with `/model`
- Re-introduced the "ultrathink" keyword to 启用 high effort for the next turn
- 移除 Opus 4 and 4.1 from Claude Code on the first-party API — users with these models pinned are automatically moved to Opus 4.6

## 2.1.66

- Reduced spurious 错误 logging

## 2.1.63

- 新增 `/simplify` and `/batch` bundled 斜杠命令
- 修复了 local 斜杠命令 output like /cost appearing as user-sent messages instead of system messages in the UI
- Project configs & auto 内存 现在 shared across git worktree of the same repository
- 新增 `ENABLE_CLAUDEAI_MCP_SERVERS=false` env var to opt out from making claude.ai MCP 服务器 可用
- 改进了 `/model` command to show the currently active model in the 斜杠命令 菜单
- 新增 HTTP 钩子, which can POST JSON to a URL and receive JSON instead of running a shell command
- 修复了 listener leak in bridge polling loop
- 修复了 listener leak in MCP OAuth flow cleanup
- 新增 manual URL paste fallback during MCP OAuth authentication. If the automatic localhost redirect doesn't work, you can paste the callback URL to complete authentication.
- 修复了 内存 leak when navigating 钩子 配置 菜单
- 修复了 listener leak in interactive 权限 handler during auto-approvals
- 修复了 文件 count 缓存 ignoring glob ignore patterns
- 修复了 内存 leak in bash command pre修复 缓存
- 修复了 MCP tool/resource 缓存 leak on server reconnect
- 修复了 IDE host IP detection 缓存 incorrectly sharing results across ports
- 修复了 WebSocket listener leak on transport reconnect
- 修复了 内存 leak in git root detection 缓存 that could cause unbounded growth in long-running 会话
- 修复了 内存 leak in JSON parsing 缓存 that grew unbounded over long 会话
- VSCode: 修复了 remote 会话 not appearing in conversation history
- 修复了 a race condition in the REPL bridge where new messages could arrive at the server interleaved with historical messages during the initial connection flush, causing message ordering issues.
- 修复了 内存 leak where long-running teammates retained all messages in AppState even after conversation compaction
- 修复了 a 内存 leak where MCP 服务器 fetch 缓存s were not cleared on disconnect, causing growing 内存 usage with servers that reconnect frequently
- 改进了 内存 usage in long 会话 with 子 agent by stripping heavy progress message pay加载s during 上下文 compaction
- 新增 "Always copy full response" option to the `/copy` picker. When selected, future `/copy` commands will skip the code block picker and copy the full response directly.
- VSCode: 新增 会话 rename and remove actions to the 会话 list
- 修复了 `/clear` not resetting 缓存 skills, which could cause stale skill content to persist in the new conversation

## 2.1.62

- 修复了 提示 suggestion 缓存 regression that reduced 缓存 hit rates

## 2.1.61

- 修复了 concurrent writes corrupting config 文件 on Windows

## 2.1.59

- Claude automatically saves useful 上下文 to auto-内存. Manage with /内存
- 新增 `/copy` command to show an interactive picker when code blocks are present, allowing selection of individual code blocks or the full response.
- 改进了 "always allow" pre修复 suggestions for compound bash commands (e.g. `cd /tmp && git fetch && git push`) to compute smarter per-subcommand pre修复es instead of treating the whole command as one
- 改进了 ordering of short task lists
- 改进了 内存 usage in multi-agent 会话 by releasing completed 子 agent task state
- 修复了 MCP OAuth token 刷新 race condition when running multiple Claude Code instances simultaneously
- 修复了 shell commands not showing a clear 错误 message when the working 目录 has been 删除d
- 修复了 config 文件 corruption that could wipe authentication when multiple Claude Code instances ran simultaneously

## 2.1.58

- Expand Remote Control to more users

## 2.1.56

- VS Code: 修复了 another cause of "command 'claude-vscode.editor.openLast' 未找到" 崩溃es

## 2.1.55

- 修复了 BashTool failing on Windows with EINVAL 错误

## 2.1.53

- 修复了 a UI flicker where user input would briefly disappear after submission before the message rendered
- 修复了 bulk agent kill (ctrl+f) to send a single aggregate notification instead of one per agent, and to properly clear the command queue
- 修复了 graceful 关闭 sometimes leaving stale 会话 when using Remote Control by parallelizing teardown network calls
- 修复了 `--worktree` sometimes being ignored on first launch
- 修复了 a panic ("switch on corrupted value") on Windows
- 修复了 a 崩溃 that could occur when spawning many processes on Windows
- 修复了 a 崩溃 in the WebAssembly interpreter on Linux x64 & Windows x64
- 修复了 a 崩溃 that sometimes occurred after 2 minutes on Windows ARM64

## 2.1.52

- VS Code: 修复了 extension 崩溃 on Windows ("command 'claude-vscode.editor.openLast' 未找到")

## 2.1.51

- 新增 `claude remote-control` subcommand for external builds, enabling local environment serving for all users.
- 更新d 插件 市场 默认 git 超时 from 30s to 120s and 新增 `CLAUDE_CODE_PLUGIN_GIT_TIMEOUT_MS` to configure.
- 新增 支持 for custom npm registries and specific version pinning when 安装ing 插件 from npm sources
- BashTool 现在 skips login shell (`-l` 标志) by 默认 when a shell snapshot is 可用, improving command execution performance. 之前 this required setting `CLAUDE_BASH_NO_LOGIN=true`.
- 修复了安全 issue where `statusLine` and `文件Suggestion` 钩子 commands could execute without 工作区 trust acceptance in interactive mode.
- Tool results larger than 50K characters are 现在 persisted to 磁盘 (之前 100K). This reduces 上下文 window usage and improves conversation longevity.
- 修复了 a bug where duplicate `control_response` messages (e.g. from WebSocket reconnects) could cause API 400 错误 by pushing duplicate assistant messages into the conversation.
- 新增 `CLAUDE_CODE_ACCOUNT_UUID`, `CLAUDE_CODE_USER_EMAIL`, and `CLAUDE_CODE_ORGANIZATION_UUID` 环境变量 for SDK callers to provide account info synchronously, eliminating a race condition where early 遥测 events lacked account metadata.
- 修复了 斜杠命令 自动完成 崩溃ing when a 插件's SKILL.md description is a YAML array or other non-string type
- The `/model` picker 现在 shows human-readable labels (e.g., "Sonnet 4.5") instead of raw model IDs for pinned model versions, with an upgrade hint when a newer version is 可用.
- Managed 设置 can 现在 be set via macOS plist or Windows Registry. Learn more at https://code.claude.com/docs/en/设置#设置-文件

## 2.1.50

- 新增 支持 for `启动超时` 配置 for LSP servers
- 新增 `Worktree创建` and `WorktreeRemove` 钩子 events, enabling custom VCS setup and teardown when agent worktree isolation 创建s or removes worktree.
- 修复了 a bug where 恢复d 会话 could be invisible when the working 目录 involved symlinks, because the 会话 storage 路径 was resolved at different times during 启动. Also 修复了 会话 data loss on SSH disconnect by flushing 会话 data before 钩子 and analytics in the graceful 关闭 sequence.
- Linux: 修复了 native modules not 加载ing on systems with glibc older than 2.30 (e.g., RHEL 8)
- 修复了 内存 leak in agent teams where completed teammate tasks were never garbage collected from 会话 state
- 修复了 `CLAUDE_CODE_SIMPLE` to fully strip down skills, 会话 内存, custom agents, and CLAUDE.md token counting
- 修复了 `/mcp reconnect` freezing the CLI when given a server name that doesn't exist
- 修复了 内存 leak where completed task state objects were never 移除 from AppState
- 新增 支持 for `isolation: worktree` in agent definitions, allowing agents to declaratively run in isolated git worktree.
- `CLAUDE_CODE_SIMPLE` mode 现在 also 禁用s MCP tools, attachments, 钩子, and CLAUDE.md 文件 加载ing for a fully minimal experience.
- 修复了 bug where MCP tools were not discovered when tool search is 启用 and a 提示 is passed in as a launch argument
- 改进了 内存 usage during long 会话 by clearing internal 缓存s after compaction
- 新增 `claude agents` CLI command to list all configured agents
- 改进了 内存 usage during long 会话 by clearing large tool results after they have been processed
- 修复了 a 内存 leak where LSP diagnostic data was never cleaned up after delivery, causing unbounded 内存 growth in long 会话
- 修复了 a 内存 leak where completed task output was not freed from 内存, reducing 内存 usage in long 会话 with many tasks
- 改进了 启动 performance for headless mode (`-p` 标志) by deferring Yoga WASM and UI component imports
- 修复了 提示 suggestion 缓存 regression that reduced 缓存 hit rates
- 修复了 unbounded 内存 growth in long 会话 by capping 文件 history snapshots
- 新增 `CLAUDE_CODE_DISABLE_1M_CONTEXT` 环境变量 to 禁用 1M 上下文 window 支持
- Opus 4.6 (fast mode) 现在 includes the full 1M 上下文 window
- VSCode: 新增 `/extra-usage` command 支持 in VS Code 会话
- 修复了 内存 leak where TaskOutput retained recent lines after cleanup
- 修复了 内存 leak in CircularBuffer where cleared items were retained in the backing array
- 修复了 内存 leak in shell command execution where ChildProcess and AbortController references were retained after cleanup

## 2.1.49

- 改进了 MCP OAuth authentication with step-up auth 支持 and discovery 缓存, reducing redundant network requests during server connections
- 新增 `--worktree` (`-w`) 标志 to start Claude in an isolated git worktree
- 子 agent 支持 `isolation: "worktree"` for working in a temporary git worktree
- 新增 Ctrl+F keybinding to kill background agents (two-press 确认ation)
- Agent definitions 支持 `background: true` to always run as a background task
- 插件 can ship `设置.json` for 默认 配置
- 修复了 文件-not-found 错误 to suggest corrected 路径s when the model drops the repo folder
- 修复了 Ctrl+C and ESC being silently ignored when background agents are running and the main thread is idle. Pressing twice within 3 seconds 现在 kills all background agents.
- 修复了 提示 suggestion 缓存 regression that reduced 缓存 hit rates.
- 修复了 `插件 启用` and `插件 禁用` to auto-detect the correct scope when `--scope` is not specified, instead of always 默认ing to user scope
- Simple mode (`CLAUDE_CODE_SIMPLE`) 现在 includes the 文件 edit tool in addition to the Bash 工具, allowing direct 文件 editing in simple mode.
- 权限 suggestions are 现在 populated when safety checks trigger an ask response, enabling SDK consumers to display 权限 options
- Sonnet 4.5 with 1M 上下文 is being 移除 from the Max plan in favor of our frontier Sonnet 4.6 model, which 现在 has 1M 上下文. Please switch in /model.
- 修复了 详细 mode not updating thinking block display when toggled via `/config` — memo comparators 现在 correctly detect 详细 changes
- 修复了 unbounded WASM 内存 growth during long 会话 by periodically resetting the tree-sitter parser
- 修复了 potential rendering issues caused by stale yoga layout references
- 改进了 performance in non-interactive mode (`-p`) by skipping unnecessary API calls during 启动
- 改进了 performance by 缓存 authentication 失败s for HTTP and SSE MCP 服务器, avoiding repeated connection attempts to servers requiring auth
- 修复了 unbounded 内存 growth during long-running 会话 caused by Yoga WASM linear 内存 never shrinking
- SDK model info 现在 includes `支持Effort`, `支持edEffortLevels`, and `支持AdaptiveThinking` fields so consumers can discover model capabilities.
- 新增 `ConfigChange` 钩子 event that fires when 配置 文件 change during a 会话, enabling enterprise security auditing and 可选 blocking of 设置 changes.
- 改进了 启动 performance by 缓存 MCP auth 失败s to avoid redundant connection attempts
- 改进了 启动 performance by reducing HTTP calls for analytics token counting
- 改进了 启动 performance by batching MCP tool token counting into a single API call
- 修复了 `禁用All钩子` setting to respect managed 设置 hierarchy — non-managed 设置 can no longer 禁用 managed 钩子 set by policy (#26637)
- 修复了 `--恢复` 会话 picker showing raw XML tags for 会话 that start with commands like `/clear`. 现在 correctly falls through to the 会话 ID fallback.
- 改进了 权限 提示s for 路径 safety and working 目录 blocks to show the reason for the restriction instead of a bare 提示 with no 上下文

## 2.1.47

- 修复了 文件WriteTool line counting to preserve intentional trailing blank lines instead of stripping them with `trimEnd()`.
- 修复了 Windows 终端 rendering bugs caused by `os.EOL` (`\r\n`) in display code — line counts 现在 show correct values instead of always showing 1 on Windows.
- 改进了 VS Code plan preview: auto-更新s as Claude iterates, 启用s commenting only when the plan is ready for review, and keeps the preview open when rejecting so Claude can revise.
- 修复了 a bug where bold and colored text in markdown output could shift to the wrong characters on Windows due to `\r\n` line endings.
- 修复了 compaction failing when conversation contains many PDF documents by stripping document blocks alongside images before sending to the compaction API (anthropics/claude-code#26188)
- 改进了 内存 usage in long-running 会话 by releasing API stream buffers, agent 上下文, and skill state after use
- 改进了 启动 performance by deferring 会话Start 钩子 execution, reducing time-to-interactive by ~500ms.
- 修复了 an issue where bash tool output was silently discarded on Windows when using MSYS2 or Cygwin shells.
- 改进了 performance of `@` 文件 mentions - 文件 suggestions 现在 appear faster by pre-warming the index on 启动 and using 会话-based 缓存 with background 刷新.
- 改进了 内存 usage by trimming agent task message history after tasks complete
- 改进了 内存 usage during long agent 会话 by eliminating O(n²) message accumulation in progress 更新s
- 修复了 the bash 权限 classifier to validate that returned match descriptions correspond to actual input rules, preventing hallucinated descriptions from incorrectly granting 权限
- 修复了 user-defined agents only 加载ing one 文件 on NFS/FUSE 文件ystems that report zero inodes (anthropics/claude-code#26044)
- 修复了 插件 agent skills silently failing to 加载 when referenced by bare name instead of fully-qualified 插件 name (anthropics/claude-code#25834)
- Search patterns in collapsed tool results are 现在 displayed in quotes for clarity
- Windows: 修复了 CWD tracking temp 文件 never being cleaned up, causing them to accumulate indefinitely (anthropics/claude-code#17600)
- Use `ctrl+f` to kill all background agents instead of double-pressing ESC. Background agents 现在 continue running when you press ESC to 取消 the main thread, giving you more control over agent lifecycle.
- 修复了 API 400 错误 ("thinking blocks cannot be modified") that occurred in 会话 with concurrent agents, caused by interleaved 流式传输 content blocks preventing proper message merging.
- Simplified teammate navigation to use only Shift+Down (with wrapping) instead of both Shift+Up and Shift+Down.
- 修复了 an issue where a single 文件 write/edit 错误 would abort all other parallel 文件 write/edit operations. Independent 文件 mutations 现在 complete even when a sibling fails.
- 新增 `last_assistant_message` field to Stop and 子 agentStop 钩子 inputs, providing the final assistant response text so 钩子 can access it without parsing transcript 文件.
- 修复了 custom 会话 titles set via `/rename` being lost after resuming a conversation (anthropics/claude-code#23610)
- 修复了 collapsed read/search hint text overflowing on narrow 终端s by truncating from the start.
- 修复了 an issue where bash commands with backslash-newline continuation lines (e.g., long commands split across multiple lines with `\`) would produce spurious empty arguments, potentially breaking command execution.
- 修复了 built-in 斜杠命令 (`/help`, `/model`, `/compact`, etc.) being hidden from the 自动完成 dropdown when many user skills are 安装ed (anthropics/claude-code#22020)
- 修复了 MCP 服务器 not appearing in the MCP Management 对话框 after deferred 加载ing
- 修复了 会话 name persisting in 状态栏 after `/clear` command (anthropics/claude-code#26082)
- 修复了 崩溃 when a skill's `name` or `description` in SKILL.md frontmatter is a bare number (e.g., `name: 3000`) — the value is 现在 properly coerced to a string (anthropics/claude-code#25837)
- 修复了 /恢复 silently dropping 会话 when the first message exceeds 16KB or uses array-format content (anthropics/claude-code#25721)
- 新增 `chat:newline` keybinding action for configurable multi-line input (anthropics/claude-code#26075)
- 新增 `新增_dirs` to the statusline JSON `工作区` section, exposing 目录 新增 via `/add-dir` to external scripts (anthropics/claude-code#26096)
- 修复了 `claude doctor` misclassifying mise and asdf-managed 安装ations as native 安装s (anthropics/claude-code#26033)
- 修复了 zsh heredoc failing with "read-only 文件 system" 错误 in 沙箱ed commands (anthropics/claude-code#25990)
- 修复了 agent progress indicator showing inflated tool use count (anthropics/claude-code#26023)
- 修复了 image pasting not working on WSL2 systems where Windows copies images as BMP format (anthropics/claude-code#25935)
- 修复了 background agent results returning raw transcript data instead of the agent's final answer (anthropics/claude-code#26012)
- 修复了 Warp 终端 incorrectly 提示ing for Shift+Enter setup when it 支持 it natively (anthropics/claude-code#25957)
- 修复了 CJK wide characters causing misaligned timestamps and layout elements in the TUI (anthropics/claude-code#26084)
- 修复了 custom agent `model` field in `.claude/agents/*.md` being ignored when spawning team teammates (anthropics/claude-code#26064)
- 修复了 plan mode being lost after 上下文 compaction, causing the model to switch from planning to implementation mode (anthropics/claude-code#26061)
- 修复了 `alwaysThinking启用: true` in 设置.json not enabling thinking mode on Bedrock and Vertex providers (anthropics/claude-code#26074)
- 修复了 `tool_decision` OTel 遥测 event not being emitted in headless/SDK mode (anthropics/claude-code#26059)
- 修复了 会话 name being lost after 上下文 compaction — renamed 会话 现在 preserve their custom title through compaction (anthropics/claude-code#26121)
- Increased initial 会话 count in 恢复 picker from 10 to 50 for faster 会话 discovery (anthropics/claude-code#26123)
- Windows: 修复了 worktree 会话 matching when drive letter casing differs (anthropics/claude-code#26123)
- 修复了 `/恢复 <会话-id>` failing to find 会话 whose first message exceeds 16KB (anthropics/claude-code#25920)
- 修复了 "Always allow" on multiline bash commands creating invalid 权限 patterns that corrupt 设置 (anthropics/claude-code#25909)
- 修复了 React 崩溃 (错误 #31) when a skill's `argument-hint` in SKILL.md frontmatter uses YAML sequence syntax (e.g., `[topic: foo | bar]`) — the value is 现在 properly coerced to a string (anthropics/claude-code#25826)
- 修复了 崩溃 when using `/fork` on 会话 that used web search — null entries in search results from transcript deserialization are 现在 handled gracefully (anthropics/claude-code#25811)
- 修复了 read-only git commands triggering FSEvents 文件 watcher loops on macOS by adding --no-可选-locks 标志 (anthropics/claude-code#25750)
- 修复了 custom agents and skills not being discovered when running from a git worktree — project-level `.claude/agents/` and `.claude/skills/` from the main repository are 现在 included (anthropics/claude-code#25816)
- 修复了 non-interactive subcommands like `claude doctor` and `claude 插件 validate` being blocked inside nested Claude 会话 (anthropics/claude-code#25803)
- Windows: 修复了 the same CLAUDE.md 文件 being 加载ed twice when drive letter casing differs between 路径s (anthropics/claude-code#25756)
- 修复了 inline code spans in markdown being incorrectly parsed as bash commands (anthropics/claude-code#25792)
- 修复了 teammate spinners not respecting custom spinnerVerbs from 设置 (anthropics/claude-code#25748)
- 修复了 shell commands permanently failing after a command 删除s its own working 目录 (anthropics/claude-code#26136)
- 修复了 钩子 (PreToolUse, PostToolUse) silently failing to execute on Windows by using Git Bash instead of cmd.exe (anthropics/claude-code#25981)
- 修复了 LSP `findReferences` and other location-based operations returning results from gitignored 文件 (e.g., `node_modules/`, `venv/`) (anthropics/claude-code#26051)
- Moved config 备份 文件 from home 目录 root to `~/.claude/备份s/` to reduce home 目录 clutter (anthropics/claude-code#26130)
- 修复了 会话 with large first 提示s (>16KB) disappearing from the /恢复 list (anthropics/claude-code#26140)
- 修复了 shell functions with double-underscore pre修复es (e.g., `__git_ps1`) not being preserved across shell 会话 (anthropics/claude-code#25824)
- 修复了 spinner showing "0 token" counter before any token have been received (anthropics/claude-code#26105)
- VSCode: 修复了 conversation messages appearing dimmed while the AskUserQuestion 对话框 is open (anthropics/claude-code#26078)
- 修复了 background tasks failing in git worktree due to remote URL resolution reading from worktree-specific gitdir instead of the main repository config (anthropics/claude-code#26065)
- 修复了 Right Alt key leaving visible `[25~` escape sequence residue in the input field on Windows/Git Bash 终端s (anthropics/claude-code#25943)
- The `/rename` command 现在 更新s the 终端 标签页 title by 默认 (anthropics/claude-code#25789)
- 修复了 Edit 工具 silently corrupting Unicode curly quotes (\u201c\u201d \u2018\u2019) by replacing them with straight quotes when making edits (anthropics/claude-code#26141)
- 修复了 OSC 8 hyperlinks only being clickable on the first line when link text wraps across multiple 终端 lines.

## 2.1.46

- 修复了 orphaned CC processes after 终端 disconnect on macOS
- 新增 支持 for using claude.ai MCP connectors in Claude Code

## 2.1.45

- 新增 支持 for Claude Sonnet 4.6
- 新增 支持 for reading `启用插件` and `extraK现在n市场s` from `--add-dir` 目录
- 新增 `spinnerTipsOverride` setting to customize spinner tips — configure `tips` with an array of custom tip strings, and 可选ly set `exclude默认: true` to show only your custom tips instead of the built-in ones
- 新增 `SDKRateLimitInfo` and `SDKRateLimitEvent` types to the SDK, enabling consumers to receive 速率限制 status 更新s including utilization, reset times, and overage information
- 修复了 Agent Teams teammates failing on Bedrock, Vertex, and Foundry by propagating API provider 环境变量 to tmux-spawned processes (anthropics/claude-code#23561)
- 修复了 沙箱 "operation not permitted" 错误 when writing temporary 文件 on macOS by using the correct per-user temp 目录 (anthropics/claude-code#21654)
- 修复了 Task 工具 (backgrounded agents) 崩溃ing with a `Reference错误` on 完成 (anthropics/claude-code#22087)
- 修复了 自动完成 suggestions not being accepted on Enter when images are pasted in the input
- 修复了 skills invoked by 子 agent incorrectly appearing in main 会话 上下文 after compaction
- 修复了 excessive `.claude.json.备份` 文件 accumulating on every 启动
- 修复了 插件-provided commands, agents, and 钩子 not being 可用 immediately after 安装ation without requiring a restart
- 改进了 启动 performance by removing eager 加载ing of 会话 history for stats 缓存
- 改进了 内存 usage for shell commands that produce large output — RSS no longer grows unboundedly with command output size
- 改进了 collapsed read/search groups to show the current 文件 or search pattern being processed beneath the summary line while active
- [VSCode] 改进了 权限 destination choice (project/user/会话) to persist across 会话

## 2.1.44

- 修复了 ENAMETOOLONG 错误 for deeply-nested 目录 路径s
- 修复了 auth 刷新 错误

## 2.1.43

- 修复了 AWS auth 刷新 hanging indefinitely by adding a 3-minute 超时
- 修复了 spurious 警告 for non-agent markdown 文件 in `.claude/agents/` 目录
- 修复了 structured-outputs beta header being sent unconditionally on Vertex/Bedrock

## 2.1.42

- 改进了 启动 performance by deferring Zod schema construction
- 改进了 提示 缓存 hit rates by moving date out of system 提示
- 新增 one-time Opus 4.6 effort callout for eligible users
- 修复了 /恢复 showing interrupt messages as 会话 titles
- 修复了 image dimension limit 错误 to suggest /compact

## 2.1.41

- 新增 guard against launching Claude Code inside another Claude Code 会话
- 修复了 Agent Teams using wrong model identifier for Bedrock, Vertex, and Foundry customers
- 修复了 a 崩溃 when MCP tools return image content during 流式传输
- 修复了 /恢复 会话 previews showing raw XML tags instead of readable command names
- 改进了 model 错误 messages for Bedrock/Vertex/Foundry users with fallback suggestions
- 修复了 插件 browse showing misleading "Space to Toggle" hint for already-安装ed 插件
- 修复了 钩子 blocking 错误 (退出 code 2) not showing stderr to the user
- 新增 `speed` attribute to OTel events and 跟踪 spans for fast mode visibility
- 新增 `claude auth login`, `claude auth status`, and `claude auth logout` CLI subcommands
- 新增 Windows ARM64 (win32-arm64) native binary 支持
- 改进了 `/rename` to auto-generate 会话 name from conversation 上下文 when called without arguments
- 改进了 narrow 终端 layout for 提示 footer
- 修复了 文件 resolution failing for @-mentions with anchor fragments (e.g., `@README.md#安装ation`)
- 修复了 文件ReadTool blocking the process on FIFOs, `/dev/stdin`, and large 文件
- 修复了 background task notifications not being delivered in 流式传输 Agent SDK mode
- 修复了 cursor jumping to end on each keystroke in classifier rule input
- 修复了 markdown link display text being dropped for raw URL
- 修复了 auto-compact 失败 错误 notifications being shown to users
- 修复了 权限 wait time being included in 子 agent elapsed time display
- 修复了 proactive ticks firing while in plan mode
- 修复了 clear stale 权限 rules when 设置 change on 磁盘
- 修复了 钩子 blocking 错误 showing stderr content in UI

## 2.1.39

- 改进了 终端 rendering performance
- 修复了 fatal 错误 being swallowed instead of displayed
- 修复了 process hanging after 会话 close
- 修复了 character loss at 终端 screen boundary
- 修复了 blank lines in 详细 transcript view

## 2.1.38

- 修复了 VS Code 终端 scroll-to-top regression introduced in 2.1.37
- 修复了 标签页 key queueing 斜杠命令 instead of autocompleting
- 修复了 bash 权限 matching for commands using 环境变量 wrappers
- 修复了 text between tool uses disappearing when not using 流式传输
- 修复了 duplicate 会话 when resuming in VS Code extension
- 改进了 heredoc delimiter parsing to prevent command smuggling
- Blocked writes to `.claude/skills` 目录 in 沙箱 mode

## 2.1.37

- 修复了 an issue where /fast was not immediately 可用 after enabling /extra-usage

## 2.1.36

- Fast mode is 现在 可用 for Opus 4.6. Learn more at https://code.claude.com/docs/en/fast-mode

## 2.1.34

- 修复了 a 崩溃 when agent teams setting 更改 between renders
- 修复了 a bug where commands excluded from 沙箱ing (via `沙箱.excludedCommands` or `dangerously禁用沙箱`) could bypass the Bash ask 权限 rule when `autoAllowBashIf沙箱ed` was 启用

## 2.1.33

- 修复了 agent teammate 会话 in tmux to send and receive messages
- 修复了 警告 about agent teams not being 可用 on your current plan
- 新增 `TeammateIdle` and `TaskCompleted` 钩子 events for multi-agent workflows
- 新增 支持 for restricting which sub-agents can be spawned via `Task(agent_type)` syntax in agent "tools" frontmatter
- 新增 `内存` frontmatter field 支持 for agents, enabling persistent 内存 with `user`, `project`, or `local` scope
- 新增 插件 name to skill descriptions and `/skills` 菜单 for better discoverability
- 修复了 an issue where 提交ting a new message while the model was in extended thinking would interrupt the thinking phase
- 修复了 an API 错误 that could occur when aborting mid-stream, where whitespace text combined with a thinking block would bypass normalization and produce an invalid request
- 修复了 API proxy compatibility issue where 404 错误 on 流式传输 endpoints no longer triggered non-流式传输 fallback
- 修复了 an issue where proxy 设置 configured via `设置.json` 环境变量 were not applied to WebFetch and other HTTP requests on the Node.js build
- 修复了 `/恢复` 会话 picker showing raw XML markup instead of clean titles for 会话 started with 斜杠命令
- 改进了 错误 messages for API connection 失败s — 现在 shows specific cause (e.g., ECONNREFUSED, SSL 错误) instead of generic "连接 错误"
- 错误 from invalid managed 设置 are 现在 surfaced
- VSCode: 新增 支持 for remote 会话, allowing OAuth users to browse and 恢复 会话 from claude.ai
- VSCode: 新增 git 分支 and message count to the 会话 picker, with 支持 for searching by 分支 name
- VSCode: 修复了 scroll-to-bottom under-scrolling on initial 会话 加载 and 会话 switch

## 2.1.32

- Claude Opus 4.6 is 现在 可用!
- 新增 research preview agent teams feature for multi-agent collaboration (token-intensive feature, requires setting CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1)
- Claude 现在 automatically records and recalls memories as it works
- 新增 "Summarize from here" to the message selector, allowing partial conversation summarization.
- Skills defined in `.claude/skills/` within additional 目录 (`--add-dir`) are 现在 加载ed automatically.
- 修复了 `@` 文件 完成 showing incorrect relative 路径s when running from a sub目录
- 更新d --恢复 to re-use --agent value specified in previous conversation by 默认.
- 修复了: Bash 工具 no longer throws "Bad substitution" 错误 when heredocs contain JavaScript template literals like `${index + 1}`, which 之前 interrupted tool execution
- Skill character budget 现在 scales with 上下文 window (2% of 上下文), so users with larger 上下文 windows can see more skill descriptions without truncation
- 修复了 Thai/Lao spacing vowels (สระ า, ำ) not rendering correctly in the input field
- VSCode: 修复了 斜杠命令 incorrectly being executed when pressing Enter with preceding text in the input field
- VSCode: 新增 spinner when 加载ing past conversations list

## 2.1.31

- 新增 会话 恢复 hint on 退出, showing how to continue your conversation later
- 新增 支持 for full-width (zenkaku) space input from Japanese IME in checkbox selection
- 修复了 PDF too large 错误 permanently locking up 会话, requiring users to start a new conversation
- 修复了 bash commands incorrectly reporting 失败 with "Read-only 文件 system" 错误 when 沙箱 mode was 启用
- 修复了 a 崩溃 that made 会话 unusable after entering plan mode when project config in `~/.claude.json` was missing 默认 fields
- 修复了 `temperatureOverride` being silently ignored in the 流式传输 API 路径, causing all 流式传输 requests to use the 默认 temperature (1) regardless of the configured override
- 修复了 LSP 关闭/退出 compatibility with strict language servers that reject null params
- 改进了 system 提示s to more clearly guide the model toward using dedicated tools (Read, Edit, Glob, Grep) instead of bash equivalents (`cat`, `sed`, `grep`, `find`), reducing unnecessary bash command usage
- 改进了 PDF and request size 错误 messages to show actual limits (100 pages, 20MB)
- Reduced layout jitter in the 终端 when the spinner appears and disappears during 流式传输
- 移除 misleading Anthropic API pricing from model selector for third-party provider (Bedrock, Vertex, Foundry) users

## 2.1.30

- 新增 `pages` parameter to the Read 工具 for PDFs, allowing specific page ranges to be read (e.g., `pages: "1-5"`). Large PDFs (>10 pages) 现在 return a lightweight reference when `@` mentioned instead of being inlined into 上下文.
- 新增 pre-configured OAuth client credentials for MCP 服务器 that don't 支持 Dynamic Client Registration (e.g., Slack). Use `--client-id` and `--client-secret` with `claude mcp add`.
- 新增 `/调试` for Claude to help troubleshoot the current 会话
- 新增 支持 for additional `git log` and `git show` 标志s in read-only mode (e.g., `--topo-order`, `--cherry-pick`, `--format`, `--raw`)
- 新增 token count, tool uses, and duration 指标s to Task 工具 results
- 新增 reduced motion mode to the config
- 修复了 phantom "(no content)" text blocks appearing in API conversation history, reducing token waste and potential model confusion
- 修复了 提示 缓存 not correctly invalidating when tool descriptions or input schemas 更改, only when tool names 更改
- 修复了 400 错误 that could occur after running `/login` when the conversation contained thinking blocks
- 修复了 a hang when resuming 会话 with corrupted transcript 文件 containing `parentUuid` cycles
- 修复了 速率限制 message showing incorrect "/upgrade" suggestion for Max 20x users when extra-usage is 不可用
- 修复了 权限 对话框s stealing focus while actively typing
- 修复了 子 agent not being able to access SDK-provided MCP tools because they were not synced to the shared application state
- 修复了 a regression where Windows users with a `.bashrc` 文件 could not run bash commands
- 改进了 内存 usage for `--恢复` (68% reduction for users with many 会话) by replacing the 会话 index with lightweight stat-based 加载ing and progressive enrichment
- 改进了 `TaskStop` tool to display the stopped command/task description in the result line instead of a generic "Task stopped" message
- 更改 `/model` to execute immediately instead of being queued
- [VSCode] 新增 multiline input 支持 to the "Other" text input in question 对话框s (use Shift+Enter for new lines)
- [VSCode] 修复了 duplicate 会话 appearing in the 会话 list when starting a new conversation

## 2.1.29

- 修复了 启动 performance issues when resuming 会话 that have `saved_钩子_上下文`

## 2.1.27

- 新增 tool call 失败s and denials to 调试 logs
- 修复了 上下文 management validation 错误 for gateway users, ensuring `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1` avoids the 错误
- 新增 `--from-pr` 标志 to 恢复 会话 linked to a specific GitHub PR number or URL
- 会话 are 现在 automatically linked to PRs when 创建d via `gh pr 创建`
- 修复了 /上下文 command not displaying colored output
- 修复了 状态栏 duplicating background task indicator when PR status was shown
- Windows: 修复了 bash command execution failing for users with `.bashrc` 文件
- Windows: 修复了 console windows flashing when spawning child processes
- VSCode: 修复了 OAuth token expiration causing 401 错误 after extended 会话

## 2.1.25

- 修复了 beta header validation 错误 for gateway users on Bedrock and Vertex, ensuring `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1` avoids the 错误

## 2.1.23

- 新增 customizable spinner verbs setting (`spinnerVerbs`)
- 修复了 mTLS and proxy connectivity for users behind corporate proxies or using client certificates
- 修复了 per-user temp 目录 isolation to prevent 权限 conflicts on shared systems
- 修复了 a race condition that could cause 400 错误 when 提示 缓存 scope was 启用
- 修复了 待处理 async 钩子 not being 取消led when headless 流式传输 会话 ended
- 修复了 标签页 完成 not updating the input field when accepting a suggestion
- 修复了 ripgrep search 超时s silently returning empty results instead of reporting 错误
- 改进了 终端 rendering performance with optimized screen data layout
- 更改 Bash commands to show 超时 duration alongside elapsed time
- 更改 合并d 拉取请求s to show a purple status indicator in the 提示 footer
- [IDE] 修复了 model options displaying incorrect region strings for Bedrock users in headless mode

## 2.1.22

- 修复了 structured outputs for non-interactive (-p) mode

## 2.1.21

- 新增 支持 for full-width (zenkaku) number input from Japanese IME in option selection 提示s
- 修复了 shell 完成 缓存 文件 being truncated on 退出
- 修复了 API 错误 when resuming 会话 that were interrupted during tool execution
- 修复了 auto-compact triggering too early on models with large output token limits
- 修复了 task IDs potentially being reused after deletion
- 修复了 文件 search not working in VS Code extension on Windows
- 改进了 read/search progress indicators to show "Reading…" while in progress and "Read" when complete
- 改进了 Claude to prefer 文件 operation tools (Read, Edit, Write) over bash equivalents (cat, sed, awk)
- [VSCode] 新增 automatic Python virtual environment activation, ensuring `python` and `pip` commands use the correct interpreter (configurable via `claudeCode.usePythonEnvironment` setting)
- [VSCode] 修复了 message action buttons having incorrect background colors

## 2.1.20

- 新增 arrow key history navigation in vim normal mode when cursor cannot move further
- 新增 external editor shortcut (Ctrl+G) to the help 菜单 for better discoverability
- 新增 PR review status indicator to the 提示 footer, showing the current 分支's PR state (approved, changes requested, 待处理, or draft) as a colored dot with a clickable link
- 新增 支持 for 加载ing `CLAUDE.md` 文件 from additional 目录 specified via `--add-dir` 标志 (requires setting `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1`)
- 新增 ability to 删除 tasks via the `Task更新` tool
- 修复了 会话 compaction issues that could cause 恢复 to 加载 full history instead of the compact summary
- 修复了 agents sometimes ignoring user messages sent while actively working on a task
- 修复了 wide character (emoji, CJK) rendering artifacts where trailing columns were not cleared when replaced by narrower characters
- 修复了 JSON parsing 错误 when MCP tool responses contain special Unicode characters
- 修复了 up/down arrow keys in multi-line and wrapped text input to prioritize cursor movement over history navigation
- 修复了 draft 提示 being lost when pressing UP arrow to navigate command history
- 修复了 ghost text flickering when typing 斜杠命令 mid-input
- 修复了 市场 source removal not properly deleting 设置
- 修复了 duplicate output in some commands like `/上下文`
- 修复了 task list sometimes showing outside the main conversation view
- 修复了 语法高亮 for diffs occurring within multiline constructs like Python docstrings
- 修复了 崩溃es when 取消ling tool use
- 改进了 `/沙箱` command UI to show dependency status with 安装ation instructions when dependencies are missing
- 改进了 thinking status text with a subtle shimmer animation
- 改进了 task list to dynamically adjust visible items based on 终端 height
- 改进了 fork conversation hint to show how to 恢复 the original 会话
- 更改 collapsed read/search groups to show present tense ("Reading", "Searching for") while in progress, and past tense ("Read", "Searched for") when complete
- 更改 `ToolSearch` results to appear as a brief notification instead of inline in the conversation
- 更改 the `/提交-push-pr` skill to automatically post PR URLs to Slack channels when configured via MCP tools
- 更改 the `/copy` command to be 可用 to all users
- 更改 background agents to 提示 for tool 权限 before launching
- 更改 权限 rules like `Bash(*)` to be accepted and treated as equivalent to `Bash`
- 更改 config 备份s to be timestamped and rotated (keeping 5 most recent) to prevent data loss

## 2.1.19

- 新增 env var `CLAUDE_CODE_ENABLE_TASKS`, set to `false` to keep the old system temporarily
- 新增 shorthand `$0`, `$1`, etc. for accessing individual arguments in custom commands
- 修复了 崩溃es on processors without AVX instruction 支持
- 修复了 dangling Claude Code processes when 终端 is closed by catching EIO 错误 from `process.退出()` and using SIGKILL as fallback
- 修复了 `/rename` and `/tag` not updating the correct 会话 when resuming from a different 目录 (e.g., git worktree)
- 修复了 resuming 会话 by custom title not working when run from a different 目录
- 修复了 pasted text content being lost when using 提示 stash (Ctrl+S) and 恢复
- 修复了 agent list displaying "Sonnet (默认)" instead of "Inherit (默认)" for agents without an explicit model setting
- 修复了 backgrounded 钩子 commands not returning early, potentially causing the 会话 to wait on a process that was intentionally backgrounded
- 修复了 文件 write preview omitting empty lines
- 更改 skills without additional 权限 or 钩子 to be allowed without requiring approval
- 更改 indexed argument syntax from `$ARGUMENTS.0` to `$ARGUMENTS[0]` (bracket syntax)
- [SDK] 新增 replay of `queued_command` attachment messages as `SDKUserMessageReplay` events when `replayUserMessages` is 启用
- [VSCode] 启用 会话 forking and rewind functionality for all users

## 2.1.18

- 新增 customizable 键盘快捷键. Configure keybindings per 上下文, 创建 chord sequences, and personalize your workflow. Run `/keybindings` to get started. Learn more at https://code.claude.com/docs/en/keybindings

## 2.1.17

- 修复了 崩溃es on processors without AVX instruction 支持

## 2.1.16

- 新增 new task management system, including new capabilities like dependency tracking
- [VSCode] 新增 native 插件 management 支持
- [VSCode] 新增 ability for OAuth users to browse and 恢复 remote Claude 会话 from the 会话 对话框
- 修复了 out-of-内存 崩溃es when resuming 会话 with heavy 子 agent usage
- 修复了 an issue where the "上下文 remaining" 警告 was not hidden after running `/compact`
- 修复了 会话 titles on the 恢复 screen not respecting the user's language setting
- [IDE] 修复了 a race condition on Windows where the Claude Code sidebar view container would not appear on start

## 2.1.15

- 新增 deprecation notification for npm 安装ations - run `claude 安装` or see https://docs.anthropic.com/en/docs/claude-code/getting-started for more options
- 改进了 UI rendering performance with React Compiler
- 修复了 the "上下文 left until auto-compact" 警告 not disappearing after running `/compact`
- 修复了 MCP stdio server 超时 not killing child process, which could cause UI freezes

## 2.1.14

- 新增 history-based 自动完成 in bash mode (`!`) - type a partial command and press 标签页 to complete from your bash command history
- 新增 search to 安装ed 插件 list - type to filter by name or description
- 新增 支持 for pinning 插件 to specific git 提交 SHAs, allowing 市场 entries to 安装 exact versions
- 修复了 a regression where the 上下文 window blocking limit was calculated too aggressively, blocking users at ~65% 上下文 usage instead of the intended ~98%
- 修复了 内存 issues that could cause 崩溃es when running parallel 子 agent
- 修复了 内存 leak in long-running 会话 where stream resources were not cleaned up after shell commands completed
- 修复了 `@` symbol incorrectly triggering 文件 自动完成 suggestions in bash mode
- 修复了 `@`-mention 菜单 folder click behavior to navigate into 目录 instead of selecting them
- 修复了 `/feedback` command generating invalid GitHub issue URLs when description is very long
- 修复了 `/上下文` command to show the same token count and percentage as the status line in 详细 mode
- 修复了 an issue where `/config`, `/上下文`, `/model`, and `/todos` command overlays could close unexpectedly
- 修复了 斜杠命令 自动完成 selecting wrong command when typing similar commands (e.g., `/上下文` vs `/compact`)
- 修复了 inconsistent back navigation in 插件 市场 when only one 市场 is configured
- 修复了 iTerm2 progress bar not clearing properly on 退出, preventing lingering indicators and bell sounds
- 改进了 backspace to 删除 pasted text as a single token instead of one character at a time
- [VSCode] 新增 `/usage` command to display current plan usage

## 2.1.12

- 修复了 message rendering bug

## 2.1.11

- 修复了 excessive MCP connection requests for HTTP/SSE transports

## 2.1.10

- 新增 new `Setup` 钩子 event that can be triggered via `--init`, `--init-only`, or `--maintenance` CLI 标志s for repository setup and maintenance operations
- 新增 键盘快捷键 'c' to copy OAuth URL when browser doesn't open automatically during login
- 修复了 a 崩溃 when running bash commands containing heredocs with JavaScript template literals like `${index + 1}`
- 改进了 启动 to capture keystrokes typed before the REPL is fully ready
- 改进了 文件 suggestions to show as removable attachments instead of inserting text when accepted
- [VSCode] 新增 安装 count display to 插件 listings
- [VSCode] 新增 trust 警告 when 安装ing 插件

## 2.1.9

- 新增 `auto:N` syntax for configuring the MCP tool search auto-启用 threshold, where N is the 上下文 window percentage (0-100)
- 新增 `plans目录` setting to customize where plan 文件 are stored
- 新增 external editor 支持 (Ctrl+G) in AskUserQuestion "Other" input field
- 新增 会话 URL attribution to 提交s and PRs 创建d from web 会话
- 新增 支持 for `PreToolUse` 钩子 to return `additional上下文` to the model
- 新增 `${CLAUDE_SESSION_ID}` string substitution for skills to access the current 会话 ID
- 修复了 long 会话 with parallel tool calls failing with an API 错误 about orphan tool_result blocks
- 修复了 MCP 服务器 reconnection hanging when 缓存 connection promise never resolves
- 修复了 Ctrl+Z suspend not working in 终端s using Kitty keyboard protocol (Ghostty, iTerm2, kitty, WezTerm)

## 2.1.7

- 新增 `showTurnDuration` setting to hide turn duration messages (e.g., "Cooked for 1m 6s")
- 新增 ability to provide feedback when accepting 权限 提示s
- 新增 inline display of agent's final response in task notifications, making it easier to see results without reading the full transcript 文件
- 修复了 security vulnerability where wildcard 权限 rules could match compound commands containing shell operators
- 修复了 false "文件 modified" 错误 on Windows when cloud sync tools, antivirus scanners, or Git touch 文件 timestamps without changing content
- 修复了 orphaned tool_result 错误 when sibling tools fail during 流式传输 execution
- 修复了 上下文 window blocking limit being calculated using the full 上下文 window instead of the effective 上下文 window (which reserves space for max output token)
- 修复了 spinner briefly flashing when running local 斜杠命令 like `/model` or `/theme`
- 修复了 终端 title animation jitter by using 修复了-width braille characters
- 修复了 插件 with git submodules not being fully initialized when 安装ed
- 修复了 bash commands failing on Windows when temp 目录 路径s contained characters like `t` or `n` that were misinterpreted as escape sequences
- 改进了 typing responsiveness by reducing 内存 allocation overhead in 终端 rendering
- 启用 MCP tool search auto mode by 默认 for all users. When MCP tool descriptions exceed 10% of the 上下文 window, they are automatically deferred and discovered via the MCPSearch tool instead of being 加载ed upfront. This reduces 上下文 usage for users with many MCP tools configured. Users can 禁用 this by adding `MCPSearch` to `disallowedTools` in their 设置.
- 更改 OAuth and API Console URLs from console.anthropic.com to platform.claude.com
- [VSCode] 修复了 `claudeProcessWrapper` setting passing the wrapper 路径 instead of the Claude binary 路径

## 2.1.6

- 新增 search functionality to `/config` command for quickly filtering 设置
- 新增 更新s section to `/doctor` showing auto-更新 channel and 可用 npm versions (s标签页le/latest)
- 新增 date range filtering to `/stats` command - press `r` to cycle between Last 7 days, Last 30 days, and All time
- 新增 automatic discovery of skills from nested `.claude/skills` 目录 when working with 文件 in sub目录
- 新增 `上下文_window.used_percentage` and `上下文_window.remaining_percentage` fields to status line input for easier 上下文 window display
- 新增 an 错误 display when the editor fails during Ctrl+G
- 修复了 权限 bypass via shell line continuation that could allow blocked commands to execute
- 修复了 false "文件 has been unexpectedly modified" 错误 when 文件 watchers touch 文件 without changing content
- 修复了 text styling (bold, colors) getting progressively misaligned in multi-line responses
- 修复了 the feedback panel closing unexpectedly when typing 'n' in the description field
- 修复了 速率限制 警告 appearing at low usage after weekly reset (现在 requires 70% usage)
- 修复了 速率限制 options 菜单 incorrectly auto-opening when resuming a previous 会话
- 修复了 numpad keys outputting escape sequences instead of characters in Kitty keyboard protocol 终端s
- 修复了 Option+Return not inserting newlines in Kitty keyboard protocol 终端s
- 修复了 corrupted config 备份 文件 accumulating in the home 目录 (现在 only one 备份 is 创建d per config 文件)
- 修复了 `mcp list` and `mcp get` commands leaving orphaned MCP 服务器 processes
- 修复了 visual artifacts in ink2 mode when nodes become hidden via `display:none`
- 改进了 external CLAUDE.md imports approval 对话框 to show which 文件 are being imported and from where
- 改进了 `/tasks` 对话框 to go directly to task details when there's only one background task running
- 改进了 @ 自动完成 with icons for different suggestion types and single-line formatting
- 更新d "Help improve Claude" setting fetch to 刷新 OAuth and retry when it fails due to a stale OAuth token
- 更改 task notification display to cap at 3 lines with overflow summary when multiple background tasks complete simultaneously
- 更改 终端 title to "Claude Code" on 启动 for better window identification
- 移除 ability to @-mention MCP 服务器 to 启用/禁用 - use `/mcp 启用 <name>` instead
- [VSCode] 修复了 usage indicator not updating after manual compact

## 2.1.5

- 新增 `CLAUDE_CODE_TMPDIR` 环境变量 to override the temp 目录 used for internal temp 文件, useful for environments with custom temp 目录 requirements

## 2.1.4

- 新增 `CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` 环境变量 to 禁用 all background task functionality including auto-backgrounding and the Ctrl+B shortcut
- 修复了 "Help improve Claude" setting fetch to 刷新 OAuth and retry when it fails due to a stale OAuth token

## 2.1.3

- 合并d 斜杠命令 and skills, simplifying the mental model with no change in behavior
- 新增 release channel (`s标签页le` or `latest`) toggle to `/config`
- 新增 detection and 警告 for unreachable 权限 rules, with 警告 in `/doctor` and after saving rules that include the source of each rule and actionable 修复 guidance
- 修复了 plan 文件 persisting across `/clear` commands, 现在 ensuring a fresh plan 文件 is used after clearing a conversation
- 修复了 false skill duplicate detection on 文件ystems with large inodes (e.g., ExFAT) by using 64-bit precision for inode values
- 修复了 mismatch between background task count in 状态栏 and items shown in tasks 对话框
- 修复了 sub-agents using the wrong model during conversation compaction
- 修复了 web search in sub-agents using incorrect model
- 修复了 trust 对话框 acceptance when running from the home 目录 not enabling trust-requiring features like 钩子 during the 会话
- 改进了 终端 rendering s标签页ility by preventing uncontrolled writes from corrupting cursor state
- 改进了 斜杠命令 suggestion readability by truncating long descriptions to 2 lines
- 更改 tool 钩子 execution 超时 from 60 seconds to 10 minutes
- [VSCode] 新增 clickable destination selector for 权限 requests, allowing you to choose where 设置 are saved (this project, all projects, shared with team, or 会话 only)

## 2.1.2

- 新增 source 路径 metadata to images dragged onto the 终端, helping Claude understand where images originated
- 新增 clickable hyperlinks for 文件 路径s in tool output in 终端s that 支持 OSC 8 (like iTerm)
- 新增 支持 for Windows Package Manager (winget) 安装ations with automatic detection and 更新 instructions
- 新增 Shift+标签页 键盘快捷键 in plan mode to quickly select "auto-accept edits" option
- 新增 `FORCE_AUTOUPDATE_PLUGINS` 环境变量 to allow 插件 auto更新 even when the main auto-更新r is 禁用
- 新增 `agent_type` to 会话Start 钩子 input, populated if `--agent` is specified
- 修复了 a command injection vulnerability in bash command processing where malformed input could execute arbitrary commands
- 修复了 a 内存 leak where tree-sitter parse trees were not being freed, causing WASM 内存 to grow unbounded over long 会话
- 修复了 binary 文件 (images, PDFs, etc.) being accidentally included in 内存 when using `@include` directives in CLAUDE.md 文件
- 修复了 更新s incorrectly claiming another 安装ation is in progress
- 修复了 崩溃 when socket 文件 exist in watched 目录 (defense-in-depth for EOPNOTSUPP 错误)
- 修复了 remote 会话 URL and teleport being broken when using `/tasks` command
- 修复了 MCP tool names being exposed in analytics events by sanitizing user-specific server 配置s
- 改进了 Option-as-Meta hint on macOS to show 终端-specific instructions for native CSIu 终端s like iTerm2, Kitty, and WezTerm
- 改进了 错误 message when pasting images over SSH to suggest using `scp` instead of the unhelpful clipboard shortcut hint
- 改进了 权限 explainer to not 标志 routine dev workflows (git fetch/rebase, npm 安装, tests, PRs) as medium risk
- 更改 large bash command outputs to be saved to 磁盘 instead of truncated, allowing Claude to read the full content
- 更改 large tool outputs to be persisted to 磁盘 instead of truncated, providing full output access via 文件 references
- 更改 `/插件` 安装ed 标签页 to unify 插件 and MCPs with scope-based grouping
- 弃用 Windows managed 设置 路径 `C:\ProgramData\ClaudeCode\managed-设置.json` - administrators should 迁移 to `C:\Program 文件\ClaudeCode\managed-设置.json`
- [SDK] 更改 minimum zod peer dependency to ^4.0.0
- [VSCode] 修复了 usage display not updating after manual compact

## 2.1.0

- 新增 automatic skill hot-重新加载 - skills 创建d or modified in `~/.claude/skills` or `.claude/skills` are 现在 immediately 可用 without restarting the 会话
- 新增 支持 for running skills and 斜杠命令 in a forked sub-agent 上下文 using `上下文: fork` in skill frontmatter
- 新增 支持 for `agent` field in skills to specify agent type for execution
- 新增 `language` setting to configure Claude's response language (e.g., language: "japanese")
- 更改 Shift+Enter to work out of the box in iTerm2, WezTerm, Ghostty, and Kitty without modifying 终端 configs
- 新增 `respectGitignore` 支持 in `设置.json` for per-project control over @-mention 文件 picker behavior
- 新增 `IS_DEMO` 环境变量 to hide email and organization from the UI, useful for 流式传输 or recording 会话
- 修复了 security issue where sensitive data (OAuth token, API keys, passwords) could be exposed in 调试 logs
- 修复了 文件 and skills not being properly discovered when resuming 会话 with `-c` or `--恢复`
- 修复了 pasted content being lost when replaying 提示s from history using up arrow or Ctrl+R search
- 修复了 Esc key with queued 提示s to only move them to input without 取消ing the running task
- Reduced 权限 提示s for complex bash commands
- 修复了 command search to prioritize exact and pre修复 matches on command names over fuzzy matches in descriptions
- 修复了 PreToolUse 钩子 to allow `更新dInput` when returning `ask` 权限 decision, enabling 钩子 to act as middleware while still requesting user consent
- 修复了 插件 路径 resolution for 文件-based 市场 sources
- 修复了 LSP tool being incorrectly 启用 when no LSP servers were configured
- 修复了 background tasks failing with "git repository 未找到" 错误 for repositories with dots in their names
- 修复了 Claude in Chrome 支持 for WSL environments
- 修复了 Windows native 安装er silently failing when execu标签页le creation fails
- 改进了 CLI help output to display options and subcommands in alphabetical order for easier navigation
- 新增 wildcard pattern matching for Bash 工具 权限 using `*` at any position in rules (e.g., `Bash(npm *)`, `Bash(* 安装)`, `Bash(git * main)`)
- 新增 unified Ctrl+B backgrounding for both bash commands and agents - pressing Ctrl+B 现在 backgrounds all running foreground tasks simultaneously
- 新增 支持 for MCP `list_更改` notifications, allowing MCP 服务器 to dynamically 更新 their 可用 tools, 提示s, and resources without requiring reconnection
- 新增 `/teleport` and `/remote-env` 斜杠命令 for claude.ai subscribers, allowing them to 恢复 and configure remote 会话
- 新增 支持 for disabling specific agents using `Task(AgentName)` syntax in 设置.json 权限 or the `--disallowedTools` CLI 标志
- 新增 钩子 支持 to agent frontmatter, allowing agents to define PreToolUse, PostToolUse, and Stop 钩子 scoped to the agent's lifecycle
- 新增 钩子 支持 for skill and 斜杠命令 frontmatter
- 新增 new Vim motions: `;` and `,` to repeat f/F/t/T motions, `y` operator for yank with `yy`/`Y`, `p`/`P` for paste, text objects (`iw`, `aw`, `iW`, `aW`, `i"`, `a"`, `i'`, `a'`, `i(`, `a(`, `i[`, `a[`, `i{`, `a{`), `>>` and `<<` for indent/dedent, and `J` to join lines
- 新增 `/plan` command shortcut to 启用 plan mode directly from the 提示
- 新增 斜杠命令 自动完成 支持 when `/` appears anywhere in input, not just at the beginning
- 新增 `--tools` 标志 支持 in interactive mode to restrict which built-in tools Claude can use during interactive 会话
- 新增 `CLAUDE_CODE_FILE_READ_MAX_OUTPUT_TOKENS` 环境变量 to override the 默认 文件 read token limit
- 新增 支持 for `once: true` config for 钩子
- 新增 支持 for YAML-style lists in frontmatter `allowed-tools` field for cleaner skill declarations
- 新增 支持 for 提示 and agent 钩子 types from 插件 (之前 only command 钩子 were 支持ed)
- 新增 Cmd+V 支持 for image paste in iTerm2 (maps to Ctrl+V)
- 新增 left/right arrow key navigation for cycling through 标签页 in 对话框s
- 新增 real-time thinking block display in Ctrl+O transcript mode
- 新增 文件路径 to full output in background bash task details 对话框
- 新增 Skills as a separate category in the 上下文 visualization
- 修复了 OAuth token 刷新 not triggering when server reports token expired but local expiration check disagrees
- 修复了 会话 persistence getting 卡住 after transient server 错误 by recovering from 409 conflicts when the entry was actually stored
- 修复了 会话 恢复 失败s caused by orphaned tool results during concurrent tool execution
- 修复了 a race condition where stale OAuth token could be read from the keychain 缓存 during concurrent token 刷新 attempts
- 修复了 AWS Bedrock 子 agent not inheriting EU/APAC cross-region inference model 配置, causing 403 错误 when IAM 权限 are scoped to specific regions
- 修复了 API 上下文 overflow when background tasks produce large output by truncating to 30K chars with 文件 路径 reference
- 修复了 a hang when reading FIFO 文件 by skipping symlink resolution for special 文件 types
- 修复了 终端 keyboard mode not being reset on 退出 in Ghostty, iTerm2, Kitty, and WezTerm
- 修复了 Alt+B and Alt+F (word navigation) not working in iTerm2, Ghostty, Kitty, and WezTerm
- 修复了 `${CLAUDE_PLUGIN_ROOT}` not being substituted in 插件 `allowed-tools` frontmatter, which caused tools to incorrectly require approval
- 修复了 文件 创建d by the Write 工具 using hardcoded 0o600 权限 instead of respecting the system umask
- 修复了 commands with `$()` command substitution failing with parse 错误
- 修复了 multi-line bash commands with backslash continuations being incorrectly split and 标志ged for 权限
- 修复了 bash command pre修复 extraction to correctly identify subcommands after global options (e.g., `git -C /路径 log` 现在 correctly matches `Bash(git log:*)` rules)
- 修复了 斜杠命令 passed as CLI arguments (e.g., `claude /上下文`) not being executed properly
- 修复了 pressing Enter after 标签页-completing a 斜杠命令 selecting a different command instead of 提交ting the completed one
- 修复了 斜杠命令 argument hint flickering and inconsistent display when typing commands with arguments
- 修复了 Claude sometimes redundantly invoking the Skill tool when running 斜杠命令 directly
- 修复了 skill token estimates in `/上下文` to accurately reflect frontmatter-only 加载ing
- 修复了 子 agent sometimes not inheriting the parent's model by 默认
- 修复了 model picker showing incorrect selection for Bedrock/Vertex users using `--model haiku`
- 修复了 duplicate Bash commands appearing in 权限 request option labels
- 修复了 noisy output when background tasks complete - 现在 shows clean 完成 message instead of raw output
- 修复了 background task 完成 notifications to appear proactively with bullet point
- 修复了 forked 斜杠命令 showing "Abort错误" instead of "Interrupted" message when 取消led
- 修复了 cursor disappearing after dismissing 权限 对话框s
- 修复了 `/钩子` 菜单 selecting wrong 钩子 type when scrolling to a different option
- 修复了 images in queued 提示s showing as "[object Object]" when pressing Esc to 取消
- 修复了 images being silently dropped when queueing messages while backgrounding a task
- 修复了 large pasted images failing with "Image was too large" 错误
- 修复了 extra blank lines in multiline 提示s containing CJK characters (Japanese, Chinese, Korean)
- 修复了 ultrathink keyword highlighting being applied to wrong characters when user 提示 text wraps to multiple lines
- 修复了 collapsed "Reading X 文件…" indicator incorrectly switching to past tense when thinking blocks appear mid-stream
- 修复了 Bash read commands (like `ls` and `cat`) not being counted in collapsed read/search groups, causing groups to incorrectly show "Read 0 文件"
- 修复了 spinner token counter to properly accumulate token from 子 agent during execution
- 修复了 内存 leak in git diff parsing where sliced strings retained large parent strings
- 修复了 race condition where LSP tool could return "no server 可用" during 启动
- 修复了 feedback submission hanging indefinitely when network requests 超时
- 修复了 search mode in 插件 discovery and log selector views 退出ing when pressing up arrow
- 修复了 钩子 成功 message showing trailing colon when 钩子 has no output
- Multiple optimizations to improve 启动 performance
- 改进了 终端 rendering performance when using native 安装er or Bun, especially for text with emoji, ANSI codes, and Unicode characters
- 改进了 performance when reading Jupyter notebooks with many cells
- 改进了 reliability for piped input like `cat refactor.md | claude`
- 改进了 reliability for AskQuestion tool
- 改进了 sed in-place edit commands to render as 文件 edits with diff preview
- 改进了 Claude to automatically continue when response is cut off due to output token limit, instead of showing an 错误 message
- 改进了 compaction reliability
- 改进了 子 agent (Task 工具) to continue working after 权限 denial, allowing them to try alternative approaches
- 改进了 skills to show progress while executing, displaying tool uses as they happen
- 改进了 skills from `/skills/` 目录 to be visible in the 斜杠命令 菜单 by 默认 (opt-out with `user-invocable: false` in frontmatter)
- 改进了 skill suggestions to prioritize recently and frequently used skills
- 改进了 spinner feedback when waiting for the first response token
- 改进了 token count display in spinner to include token from background agents
- 改进了 incremental output for async agents to give the main thread more control and visibility
- 改进了 权限 提示 UX with 标签页 hint moved to footer, cleaner Yes/No input labels with 上下文ual placeholders
- 改进了 Claude in Chrome notification with shortened help text and persistent display until dismissed
- 改进了 macOS screenshot paste reliability with TIFF format 支持
- 改进了 `/stats` output
- 更新d Atlassian MCP integration to use a more reliable 默认 配置 (streamable HTTP)
- 更改 "Interrupted" message color from red to grey for a less alarming appearance
- 移除 权限 提示 when entering plan mode - users can 现在 enter plan mode without approval
- 移除 underline styling from image reference links
- [SDK] 更改 minimum zod peer dependency to ^4.0.0
- [VSCode] 新增 currently selected model name to the 上下文 菜单
- [VSCode] 新增 descriptive labels on auto-accept 权限 button (e.g., "Yes, allow npm for this project" instead of "Yes, and don't ask again")
- [VSCode] 修复了 paragraph breaks not rendering in markdown content
- [VSCode] 修复了 scrolling in the extension inadvertently scrolling the parent iframe
- [Windows] 修复了 issue with improper rendering

## 2.0.76

- 修复了 issue with macOS code-sign 警告 when using Claude in Chrome integration

## 2.0.75

- Minor bug修复es

## 2.0.74

- 新增 LSP (Language Server Protocol) tool for code intelligence features like go-to-definition, find references, and hover documentation
- 新增 `/终端-setup` 支持 for Kitty, Alacritty, Zed, and Warp 终端s
- 新增 ctrl+t shortcut in `/theme` to toggle 语法高亮 on/off
- 新增 语法高亮 info to theme picker
- 新增 guidance for macOS users when Alt shortcuts fail due to 终端 配置
- 修复了 skill `allowed-tools` not being applied to tools invoked by the skill
- 修复了 Opus 4.5 tip incorrectly showing when user was already using Opus
- 修复了 a potential 崩溃 when 语法高亮 isn't initialized correctly
- 修复了 visual bug in `/插件 discover` where list selection indicator showed while search box was focused
- 修复了 macOS 键盘快捷键 to display 'opt' instead of 'alt'
- 改进了 `/上下文` command visualization with grouped skills and agents by source, 斜杠命令, and sorted token count
- [Windows] 修复了 issue with improper rendering
- [VSCode] 新增 gift tag pictogram for year-end promotion message

## 2.0.73

- 新增 clickable `[Image #N]` links that open attached images in the 默认 viewer
- 新增 alt-y yank-pop to cycle through kill ring history after ctrl-y yank
- 新增 search filtering to the 插件 discover screen (type to filter by name, description, or 市场)
- 新增 支持 for custom 会话 IDs when forking 会话 with `--会话-id` combined with `--恢复` or `--continue` and `--fork-会话`
- 修复了 slow input history cycling and race condition that could overwrite text after message submission
- 改进了 `/theme` command to open theme picker directly
- 改进了me picker UI
- 改进了 search UX across 恢复 会话, 权限, and 插件 screens with a unified SearchBox component
- [VSCode] 新增 标签页 icon badges showing 待处理 权限 (blue) and unread 完成s (orange)

## 2.0.72

- 新增 Claude in Chrome (Beta) feature that works with the Chrome extension (https://claude.ai/chrome) to let you control your browser directly from Claude Code
- Reduced 终端 flickering
- 新增 scannable QR code to mobile app tip for quick app down加载s
- 新增 加载ing indicator when resuming conversations for better feedback
- 修复了 `/上下文` command not respecting custom system 提示s in non-interactive mode
- 修复了 order of consecutive Ctrl+K lines when pasting with Ctrl+Y
- 改进了 @ mention 文件 suggestion speed (~3× faster in git repositories)
- 改进了 文件 suggestion performance in repos with `.ignore` or `.rgignore` 文件
- 改进了 设置 validation 错误 to be more prominent
- 更改 thinking toggle from 标签页 to Alt+T to avoid accidental triggers

## 2.0.71

- 新增 /config toggle to 启用/禁用 提示 suggestions
- 新增 `/设置` as an alias for the `/config` command
- 修复了 @ 文件 reference suggestions incorrectly triggering when cursor is in the middle of a 路径
- 修复了 MCP 服务器 from `.mcp.json` not 加载ing when using `--dangerously-skip-权限`
- 修复了 权限 rules incorrectly rejecting valid bash commands containing shell glob patterns (e.g., `ls *.txt`, `for f in *.png`)
- Bedrock: Environment variable `ANTHROPIC_BEDROCK_BASE_URL` is 现在 respected for token counting and inference pro文件 listing
- New 语法高亮 engine for native build

## 2.0.70

- 新增 Enter key to accept and 提交 提示 suggestions immediately (标签页 still accepts for editing)
- 新增 wildcard syntax `mcp__server__*` for MCP tool 权限 to allow or deny all tools from a server
- 新增 auto-更新 toggle for 插件 市场, allowing per-市场 control over automatic 更新s
- 新增 `current_usage` field to status line input, enabling accurate 上下文 window percentage calculations
- 修复了 input being cleared when processing queued commands while the user was typing
- 修复了 提示 suggestions replacing typed input when pressing 标签页
- 修复了 diff view not updating when 终端 is resized
- 改进了 内存 usage by 3x for large conversations
- 改进了 resolution of stats screenshots copied to clipboard (Ctrl+S) for crisper images
- 移除 # shortcut for quick 内存 entry (tell Claude to edit your CLAUDE.md instead)
- Fix thinking mode toggle in /config not persisting correctly
- Improve UI for 文件 creation 权限 对话框

## 2.0.69

- Minor bug修复es

## 2.0.68

- 修复了 IME (Input Method Editor) 支持 for languages like Chinese, Japanese, and Korean by correctly positioning the composition window at the cursor
- 修复了 a bug where disallowed MCP tools were visible to the model
- 修复了 an issue where steering messages could be lost while a 子 agent is working
- 修复了 Option+Arrow word navigation treating entire CJK (Chinese, Japanese, Korean) text sequences as a single word instead of navigating by word boundaries
- 改进了 plan mode 退出 UX: show simplified yes/no 对话框 when 退出ing with empty or missing plan instead of throwing an 错误
- Add 支持 for enterprise managed 设置. Contact your Anthropic account team to 启用 this feature.

## 2.0.67

- Thinking mode is 现在 启用 by 默认 for Opus 4.5
- Thinking mode 配置 has moved to /config
- 新增 search functionality to `/权限` command with `/` 键盘快捷键 for filtering rules by tool name
- Show reason why auto更新r is 禁用 in `/doctor`
- 修复了 false "Another process is currently updating Claude" 错误 when running `claude 更新` while another instance is already on the latest version
- 修复了 MCP 服务器 from `.mcp.json` being 卡住 in 待处理 state when running in non-interactive mode (`-p` 标志 or piped input)
- 修复了 scroll position resetting after deleting a 权限 rule in `/权限`
- 修复了 word deletion (opt+删除) and word navigation (opt+arrow) not working correctly with non-Latin text such as Cyrillic, Greek, Arabic, Hebrew, Thai, and Chinese
- 修复了 `claude 安装 --force` not bypassing stale lock 文件
- 修复了 consecutive @~/ 文件 references in CLAUDE.md being incorrectly parsed due to markdown strikethrough interference
- Windows: 修复了 插件 MCP 服务器 failing due to colons in log 目录 路径s

## 2.0.65

- 新增 ability to switch models while writing a 提示 using alt+p (linux, windows), option+p (macos).
- 新增 上下文 window information to status line input
- 新增 `文件Suggestion` setting for custom `@` 文件 search commands
- 新增 `CLAUDE_CODE_SHELL` 环境变量 to override automatic shell detection (useful when login shell differs from actual working shell)
- 修复了 提示 not being saved to history when aborting a query with Escape
- 修复了 Read 工具 image handling to identify format from bytes instead of 文件 extension

## 2.0.64

- Made auto-compacting instant
- Agents and bash commands can run asynchronously and send messages to wake up the main agent
- /stats 现在 provides users with interesting CC stats, such as favorite model, usage graph, usage streak
- 新增 named 会话 支持: use `/rename` to name 会话, `/恢复 <name>` in REPL or `claude --恢复 <name>` from the 终端 to 恢复 them
- 新增 支持 for .claude/rules/`.  See https://code.claude.com/docs/en/内存 for details.
- 新增 image dimension metadata when images are resized, enabling accurate coordinate mappings for large images
- 修复了 auto-加载ing .env when using native 安装er
- 修复了 `--system-提示` being ignored when using `--continue` or `--恢复` 标志s
- 改进了 `/恢复` screen with grouped forked 会话 and 键盘快捷键 for preview (P) and rename (R)
- VSCode: 新增 copy-to-clipboard button on code blocks and bash tool inputs
- VSCode: 修复了 extension not working on Windows ARM64 by falling back to x64 binary via emulation
- Bedrock: Improve efficiency of token counting
- Bedrock: Add 支持 for `aws login` AWS Management Console credentials
- Unshipped AgentOutputTool and BashOutputTool, in favor of a new unified TaskOutputTool

## 2.0.62

- 新增 "(Recommended)" indicator for multiple-choice questions, with the recommended option moved to the top of the list
- 新增 `attribution` setting to customize 提交 and PR bylines (deprecates `includeCoAuthoredBy`)
- 修复了 duplicate 斜杠命令 appearing when ~/.claude is symlinked to a project 目录
- 修复了 斜杠命令 selection not working when multiple commands share the same name
- 修复了 an issue where skill 文件 inside symlinked skill 目录 could become circular symlinks
- 修复了 running versions getting 移除 because lock 文件 incorrectly going stale
- 修复了 IDE diff 标签页 not closing when rejecting 文件 changes

## 2.0.61

- Reverted VSCode 支持 for multiple 终端 clients due to responsiveness issues.

## 2.0.60

- 新增 background agent 支持. Agents run in the background while you work
- 新增 --禁用-slash-commands CLI 标志 to 禁用 all 斜杠命令
- 新增 model name to "Co-Authored-By" 提交 messages
- 启用 "/mcp 启用 [server-name]" or "/mcp 禁用 [server-name]" to quickly toggle all servers
- 更新d Fetch to skip summarization for pre-approved websites
- VSCode: 新增 支持 for multiple 终端 clients 连接中 to the IDE server simultaneously

## 2.0.59

- 新增 --agent CLI 标志 to override the agent setting for the current 会话
- 新增 `agent` setting to configure main thread with a specific agent's system 提示, tool restrictions, and model
- VS Code: 修复了 .claude.json config 文件 being read from incorrect location

## 2.0.58

- Pro users 现在 have access to Opus 4.5 as part of their subscription!
- 修复了 timer duration showing "11m 60s" instead of "12m 0s"
- Windows: Managed 设置 现在 prefer `C:\Program 文件\ClaudeCode` if it exists. 支持 for `C:\ProgramData\ClaudeCode` will be 移除 in a future version.

## 2.0.57

- 新增 feedback input when rejecting plans, allowing users to tell Claude what to change
- VSCode: 新增 流式传输 message 支持 for real-time response display

## 2.0.56

- 新增 setting to 启用/禁用 终端 progress bar (OSC 9;4)
- VSCode Extension: 新增 支持 for VS Code's secondary sidebar (VS Code 1.97+), allowing Claude Code to be displayed in the right sidebar while keeping the 文件 explorer on the left. Requires setting sidebar as Preferred Location in the config.

## 2.0.55

- 修复了 proxy DNS resolution being forced on by 默认. 现在 opt-in via `CLAUDE_CODE_PROXY_RESOLVES_HOSTS=true` 环境变量
- 修复了 keyboard navigation becoming unresponsive when holding down arrow keys in 内存 location selector
- 改进了 AskUserQuestion tool to auto-提交 single-select questions on the last question, eliminating the extra review screen for simple question flows
- 改进了 fuzzy matching for `@` 文件 suggestions with faster, more accurate results

## 2.0.54

- 钩子: 启用 权限Request 钩子 to process 'always allow' suggestions and apply 权限 更新s
- Fix issue with excessive iTerm notifications

## 2.0.52

- 修复了 duplicate message display when starting Claude with a command line argument
- 修复了 `/usage` command progress bars to fill up as usage increases (instead of showing remaining percentage)
- 修复了 image pasting not working on Linux systems running Wayland (现在 falls back to wl-paste when xclip is 不可用)
- Permit some uses of `$!` in bash commands

## 2.0.51

- 新增 Opus 4.5! https://www.anthropic.com/news/claude-opus-4-5
- Introducing Claude Code for Desktop: https://claude.com/down加载
- To give you room to try out our new model, we've 更新d usage limits for Claude Code users. See the Claude Opus 4.5 blog for full details
- Pro users can 现在 purchase extra usage for access to Opus 4.5 in Claude Code
- Plan Mode 现在 builds more precise plans and executes more thoroughly
- Usage limit notifications 现在 easier to understand
- Switched `/usage` back to "% used"
- 修复了 handling of thinking 错误
- 修复了 performance regression

## 2.0.50

- 修复了 bug preventing calling MCP tools that have nested references in their input schemas
- Silenced a noisy but harmless 错误 during upgrades
- 改进了 ultrathink text display
- 改进了 clarity of 5-hour 会话 limit 警告 message

## 2.0.49

- 新增 readline-style ctrl-y for pasting 删除d text
- 改进了 clarity of usage limit 警告 message
- 修复了 handling of 子 agent 权限

## 2.0.47

- 改进了 错误 messages and validation for `claude --teleport`
- 改进了 错误 handling in `/usage`
- 修复了 race condition with history entry not getting logged at 退出
- 修复了 Vertex AI 配置 not being applied from `设置.json`

## 2.0.46

- 修复了 image 文件 being reported with incorrect media type when format cannot be detected from metadata

## 2.0.45

- 新增 支持 for Microsoft Foundry! See https://code.claude.com/docs/en/azure-ai-foundry
- 新增 `权限Request` 钩子 to automatically approve or deny tool 权限 requests with custom logic
- Send background tasks to Claude Code on the web by starting a message with `&`

## 2.0.43

- 新增 `权限Mode` field for custom agents
- 新增 `tool_use_id` field to `PreToolUse钩子Input` and `PostToolUse钩子Input` types
- 新增 skills frontmatter field to declare skills to auto-加载 for 子 agent
- 新增 the `子 agentStart` 钩子 event
- 修复了 nested `CLAUDE.md` 文件 not 加载ing when @-mentioning 文件
- 修复了 duplicate rendering of some messages in the UI
- 修复了 some visual flickers
- 修复了 NotebookEdit 工具 inserting cells at incorrect positions when cell IDs matched the pattern `cell-N`

## 2.0.42

- 新增 `agent_id` and `agent_transcript_路径` fields to `子 agentStop` 钩子.

## 2.0.41

- 新增 `model` parameter to 提示-based stop 钩子, allowing users to specify a custom model for 钩子 evaluation
- 修复了 斜杠命令 from user 设置 being 加载ed twice, which could cause rendering issues
- 修复了 incorrect labeling of user 设置 vs project 设置 in command descriptions
- 修复了 崩溃 when 插件 command 钩子 超时 during execution
- 修复了: Bedrock users no longer see duplicate Opus entries in the /model picker when using `--model haiku`
- 修复了 broken security documentation links in trust 对话框s and onboarding
- 修复了 issue where pressing ESC to close the diff 模态 would also interrupt the model
- ctrl-r history search landing on a 斜杠命令 no longer 取消s the search
- SDK: 支持 custom 超时s for 钩子
- Allow more safe git commands to run without approval
- 插件: 新增 支持 for sharing and 安装ing output styles
- Teleporting a 会话 from web will automatically set the upstream 分支

## 2.0.37

- 修复了 how idleness is computed for notifications
- 钩子: 新增 matcher values for Notification 钩子 events
- Output Styles: 新增 `keep-coding-instructions` option to frontmatter

## 2.0.36

- 修复了: DISABLE_AUTOUPDATER 环境变量 现在 properly 禁用s package manager 更新 notifications
- 修复了 queued messages being incorrectly executed as bash commands
- 修复了 input being lost when typing while a queued message is processed

## 2.0.35

- Improve fuzzy search results when searching commands
- 改进了 VS Code extension to respect `chat.fontSize` and `chat.fontFamily` 设置 throughout the entire UI, and apply font changes immediately without requiring 重新加载
- 新增 `CLAUDE_CODE_EXIT_AFTER_STOP_DELAY` 环境变量 to automatically 退出 SDK mode after a specified idle duration, useful for automated workflows and scripts
- 迁移d `ignorePatterns` from project config to deny 权限 in the local设置.
- 修复了 菜单 navigation getting 卡住 on items with empty string or other falsy values (e.g., in the `/钩子` 菜单)

## 2.0.34

- VSCode Extension: 新增 setting to configure the initial 权限 mode for new conversations
- 改进了 文件 路径 suggestion performance with native Rust-based fuzzy finder
- 修复了 infinite token 刷新 loop that caused MCP 服务器 with OAuth (e.g., Slack) to hang during connection
- 修复了 内存 崩溃 when reading or writing large 文件 (especially base64-encoded images)

## 2.0.33

- Native binary 安装s 现在 launch quicker.
- 修复了 `claude doctor` incorrectly detecting Homebrew vs npm-global 安装ations by properly resolving symlinks
- 修复了 `claude mcp serve` exposing tools with incompatible outputSchemas

## 2.0.32

- Un-deprecate output styles based on community feedback
- 新增 `companyAnnouncements` setting for displaying announcements on 启动
- 修复了 钩子 progress messages not updating correctly during PostToolUse 钩子 execution

## 2.0.31

- Windows: native 安装ation uses shift+标签页 as shortcut for mode switching, instead of alt+m
- Vertex: add 支持 for Web Search on 支持ed models
- VSCode: Adding the respectGitIgnore 配置 to include .gitignored 文件 in 文件 searches (默认s to true)
- 修复了 a bug with 子 agent and MCP 服务器 related to "Tool names must be unique" 错误
- 修复了 issue causing `/compact` to fail with `提示_too_long` by making it respect existing compact boundaries
- 修复了 插件 卸载 not removing 插件

## 2.0.30

- 新增 helpful hint to run `security unlock-keychain` when encountering API key 错误 on macOS with locked keychain
- 新增 `allowUn沙箱edCommands` 沙箱 setting to 禁用 the dangerously禁用沙箱 escape hatch at policy level
- 新增 `disallowedTools` field to custom agent definitions for explicit tool blocking
- 新增 提示-based stop 钩子
- VSCode: 新增 respectGitIgnore 配置 to include .gitignored 文件 in 文件 searches (默认s to true)
- 启用 SSE MCP 服务器 on native build
- 弃用 output styles. Review options in `/output-style` and use --system-提示-文件, --system-提示, --append-system-提示, CLAUDE.md, or 插件 instead
- 移除 支持 for custom ripgrep 配置, resolving an issue where Search returns no results and config discovery fails
- 修复了 Explore agent creating unwanted .md investigation 文件 during codebase exploration
- 修复了 a bug where `/上下文` would sometimes fail with "max_token must be greater than thinking.budget_token" 错误 message
- 修复了 `--mcp-config` 标志 to correctly override 文件-based MCP 配置s
- 修复了 bug that saved 会话 权限 to local 设置
- 修复了 MCP tools not being 可用 to sub-agents
- 修复了 钩子 and 插件 not executing when using --dangerously-skip-权限 标志
- 修复了 delay when navigating through typeahead suggestions with arrow keys
- VSCode: 恢复d selection indicator in input footer showing current 文件 or code selection status

## 2.0.28

- Plan mode: introduced new Plan 子 agent
- 子 agent: claude can 现在 choose to 恢复 子 agent
- 子 agent: claude can dynamically choose the model used by its 子 agent
- SDK: 新增 --max-budget-usd 标志
- Discovery of custom 斜杠命令, 子 agent, and output styles no longer respects .gitignore
- Stop `/终端-setup` from adding backslash to `Shift + Enter` in VS Code
- Add 分支 and tag 支持 for git-based 插件 and 市场 using fragment syntax (e.g., `owner/repo#分支`)
- 修复了 a bug where macOS 权限 提示s would show up upon initial launch when launching from home 目录
- Various other bug 修复es

## 2.0.27

- New UI for 权限 提示s
- 新增 current 分支 filtering and search to 会话 恢复 screen for easier navigation
- 修复了 目录 @-mention causing "No assistant message found" 错误
- VSCode Extension: Add config setting to include .gitignored 文件 in 文件 searches
- VSCode Extension: Bug 修复es for unrelated 'Warmup' conversations, and 配置/设置 occasionally being reset to 默认s

## 2.0.25

- 移除 legacy SDK entrypoint. Please 迁移 to @anthropic-ai/claude-agent-sdk for future SDK 更新s: https://platform.claude.com/docs/en/agent-sdk/migration-guide

## 2.0.24

- 修复了 a bug where project-level skills were not 加载ing when --setting-sources 'project' was specified
- Claude Code Web: 支持 for Web -> CLI teleport
- 沙箱: Releasing a 沙箱 mode for the BashTool on Linux & Mac
- Bedrock: Display awsAuth刷新 output when auth is required

## 2.0.22

- 修复了 content layout shift when scrolling through 斜杠命令
- IDE: Add toggle to 启用/禁用 thinking.
- Fix bug causing duplicate 权限 提示s with parallel tool calls
- Add 支持 for enterprise managed MCP allowlist and denylist

## 2.0.21

- 支持 MCP `structuredContent` field in tool responses
- 新增 an interactive question tool
- Claude will 现在 ask you questions more often in plan mode
- 新增 Haiku 4.5 as a model option for Pro users
- 修复了 an issue where queued commands don't have access to previous messages' output

## 2.0.20

- 新增 支持 for Claude Skills

## 2.0.19

- Auto-background long-running bash commands instead of killing them. Customize with BASH_DEFAULT_TIMEOUT_MS
- 修复了 a bug where Haiku was unnecessarily called in print mode

## 2.0.17

- 新增 Haiku 4.5 to model selector!
- Haiku 4.5 automatically uses Sonnet in plan mode, and Haiku for execution (i.e. SonnetPlan by 默认)
- 3P (Bedrock and Vertex) are not automatically upgraded yet. Manual upgrading can be done through setting `ANTHROPIC_DEFAULT_HAIKU_MODEL`
- Introducing the Explore 子 agent. Powered by Haiku it'll search through your codebase efficiently to save 上下文!
- OTEL: 支持 HTTP_PROXY and HTTPS_PROXY
- `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` 现在 禁用s release notes fetching

## 2.0.15

- 修复了 bug with resuming where 之前 创建d 文件 needed to be read again before writing
- 修复了 bug with `-p` mode where @-mentioned 文件 needed to be read again before writing

## 2.0.14

- Fix @-mentioning MCP 服务器 to toggle them on/off
- Improve 权限 checks for bash with inline env vars
- Fix ultrathink + thinking toggle
- Reduce unnecessary logins
- Document --system-提示
- Several improvements to rendering
- 插件 UI polish

## 2.0.13

- 修复了 `/插件` not working on native build

## 2.0.12

- **插件 System Released**: Extend Claude Code with custom commands, agents, 钩子, and MCP 服务器 from 市场
- `/插件 安装`, `/插件 启用/禁用`, `/插件 市场` commands for 插件 management
- Repository-level 插件 配置 via `extraK现在n市场s` for team collaboration
- `/插件 validate` command for validating 插件 structure and 配置
- 插件 announcement blog post at https://www.anthropic.com/news/claude-code-插件
- 插件 documentation 可用 at https://code.claude.com/docs/en/插件
- Comprehensive 错误 messages and diagnostics via `/doctor` command
- Avoid flickering in `/model` selector
- Improvements to `/help`
- Avoid mentioning 钩子 in `/恢复` summaries
- Changes to the "详细" setting in `/config` 现在 persist across 会话

## 2.0.11

- Reduced system 提示 size by 1.4k token
- IDE: 修复了 键盘快捷键 and focus issues for smoother interaction
- 修复了 Opus fallback 速率限制 错误 appearing incorrectly
- 修复了 /add-dir command selecting wrong 默认 标签页

## 2.0.10

- Rewrote 终端 renderer for buttery smooth UI
- 启用/禁用 MCP 服务器 by @mentioning, or in /mcp
- 新增 标签页 完成 for shell commands in bash mode
- PreToolUse 钩子 can 现在 modify tool inputs
- Press Ctrl-G to edit your 提示 in your system's configured text editor
- Fixes for bash 权限 checks with 环境变量 in the command

## 2.0.9

- Fix regression where bash backgrounding stopped working

## 2.0.8

- 更新 Bedrock 默认 Sonnet model to `global.anthropic.claude-sonnet-4-5-20250929-v1:0`
- IDE: Add drag-and-drop 支持 for 文件 and folders in chat
- /上下文: Fix counting for thinking blocks
- Improve message rendering for users with light themes on dark 终端s
- Remove 弃用 .claude.json allowedTools, ignorePatterns, env, and todoFeature启用 config options (instead, configure these in your 设置.json)

## 2.0.5

- IDE: Fix IME unintended message submission with Enter and 标签页
- IDE: Add "Open in 终端" link in login screen
- Fix unhandled OAuth expiration 401 API 错误
- SDK: 新增 SDKUserMessageReplay.isReplay to prevent duplicate messages

## 2.0.1

- Skip Sonnet 4.5 默认 model setting change for Bedrock and Vertex
- Various bug 修复es and presentation improvements

## 2.0.0

- New native VS Code extension
- Fresh coat of paint throughout the whole app
- /rewind a conversation to undo code changes
- /usage command to see plan limits
- 标签页 to toggle thinking (sticky across 会话)
- Ctrl-R to search history
- Unshipped claude config command
- 钩子: Reduced PostToolUse 'tool_use' ids were found without 'tool_result' blocks 错误
- SDK: The Claude Code SDK is 现在 the Claude Agent SDK
- Add 子 agent dynamically with `--agents` 标志

## 1.0.126

- 启用 /上下文 command for Bedrock and Vertex
- Add mTLS 支持 for HTTP-based Open遥测 exporters

## 1.0.124

- Set `CLAUDE_BASH_NO_LOGIN` 环境变量 to 1 or true to to skip login shell for BashTool
- Fix Bedrock and Vertex 环境变量 evaluating all strings as truthy
- No longer inform Claude of the list of allowed tools when 权限 is denied
- 修复了 security vulnerability in Bash 工具 权限 checks
- 改进了 VSCode extension performance for large 文件

## 1.0.123

- Bash 权限 rules 现在 支持 output redirections when matching (e.g., `Bash(python:*)` matches `python script.py > output.txt`)
- 修复了 thinking mode triggering on negation phrases like "don't think"
- 修复了 rendering performance degradation during token 流式传输
- 新增 SlashCommand tool, which 启用s Claude to invoke your 斜杠命令. https://code.claude.com/docs/en/slash-commands#SlashCommand-tool
- Enhanced BashTool environment snapshot logging
- 修复了 a bug where resuming a conversation in headless mode would sometimes 启用 thinking unnecessarily
- 迁移d --调试 logging to a 文件, to 启用 easy tailing & filtering

## 1.0.120

- Fix input lag during typing, especially noticeable with large 提示s
- 改进了 VSCode extension command registry and 会话 对话框 user experience
- Enhanced 会话 对话框 responsiveness and visual feedback
- 修复了 IDE compatibility issue by removing worktree 支持 check
- 修复了 security vulnerability where Bash 工具 权限 checks could be bypassed using pre修复 matching

## 1.0.119

- Fix Windows issue where process visually freezes on entering interactive mode
- 支持 dynamic headers for MCP 服务器 via headersHelper 配置
- Fix thinking mode not working in headless 会话
- Fix 斜杠命令 现在 properly 更新 allowed tools instead of replacing them

## 1.0.117

- Add Ctrl-R history search to recall previous commands like bash/zsh
- Fix input lag while typing, especially on Windows
- Add sed command to auto-allowed commands in acceptEdits mode
- Fix Windows PATH comparison to be case-insensitive for drive letters
- Add 权限 management hint to /add-dir output

## 1.0.115

- Improve thinking mode display with enhanced visual effects
- Type /t to temporarily 禁用 thinking mode in your 提示
- Improve 路径 validation for glob and grep tools
- Show condensed output for post-tool 钩子 to reduce visual clutter
- Fix visual feedback when 加载ing state completes
- Improve UI consistency for 权限 request 对话框s

## 1.0.113

- 弃用 piped input in interactive mode
- Move Ctrl+R keybinding for toggling transcript to Ctrl+O

## 1.0.112

- Transcript mode (Ctrl+R): 新增 the model used to generate each assistant message
- Addressed issue where some Claude Max users were incorrectly recognized as Claude Pro users
- 钩子: 新增 systemMessage 支持 for 会话End 钩子
- 新增 `spinnerTips启用` setting to 禁用 spinner tips
- IDE: Various improvements and bug 修复es

## 1.0.111

- /model 现在 validates provided model names
- 修复了 Bash 工具 崩溃es caused by malformed shell syntax parsing

## 1.0.110

- /终端-setup command 现在 支持 WezTerm
- MCP: OAuth token 现在 proactively 刷新 before expiration
- 修复了 reliability issues with background Bash processes

## 1.0.109

- SDK: 新增 partial message 流式传输 支持 via `--include-partial-messages` CLI 标志

## 1.0.106

- Windows: 修复了 路径 权限 matching to consistently use POSIX format (e.g., `Read(//c/Users/...)`)

## 1.0.97

- 设置: /doctor 现在 validates 权限 rule syntax and suggests corrections

## 1.0.94

- Vertex: add 支持 for global endpoints for 支持ed models
- /内存 command 现在 allows direct editing of all imported 内存 文件
- SDK: Add custom tools as callbacks
- 新增 /todos command to list current todo items

## 1.0.93

- Windows: Add alt + v shortcut for pasting images from clipboard
- 支持 NO_PROXY 环境变量 to bypass proxy for specified hostnames and IPs

## 1.0.90

- 设置 文件 changes take effect immediately - no restart required

## 1.0.88

- 修复了 issue causing "OAuth authentication is currently not 支持ed"
- Status line input 现在 includes `exceeds_200k_token`
- 修复了 incorrect usage tracking in /cost.
- Introduced `ANTHROPIC_DEFAULT_SONNET_MODEL` and `ANTHROPIC_DEFAULT_OPUS_MODEL` for controlling model aliases opusplan, opus, and sonnet.
- Bedrock: 更新d 默认 Sonnet model to Sonnet 4

## 1.0.86

- 新增 /上下文 to help users self-serve 调试 上下文 issues
- SDK: 新增 UUID 支持 for all SDK messages
- SDK: 新增 `--replay-user-messages` to replay user messages back to stdout

## 1.0.85

- Status line input 现在 includes 会话 cost info
- 钩子: Introduced 会话End 钩子

## 1.0.84

- Fix tool_use/tool_result id mismatch 错误 when network is uns标签页le
- Fix Claude sometimes ignoring real-time steering when wrapping up a task
- @-mention: Add ~/.claude/\* 文件 to suggestions for easier agent, output style, and 斜杠命令 editing
- Use built-in ripgrep by 默认; to opt out of this behavior, set USE_BUILTIN_RIPGREP=0

## 1.0.83

- @-mention: 支持 文件 with spaces in 路径
- New shimmering spinner

## 1.0.82

- SDK: Add request 取消lation 支持
- SDK: New additionalDirectories option to search custom 路径s, 改进了 斜杠命令 processing
- 设置: Validation prevents invalid fields in .claude/设置.json 文件
- MCP: Improve tool name consistency
- Bash: Fix 崩溃 when Claude tries to automatically read large 文件

## 1.0.81

- Released output styles, including new built-in educational output styles "Explanatory" and "Learning". Docs: https://code.claude.com/docs/en/output-styles
- Agents: Fix custom agent 加载ing when agent 文件 are unparsable

## 1.0.80

- UI improvements: Fix text contrast for custom 子 agent colors and spinner rendering issues

## 1.0.77

- Bash 工具: Fix heredoc and multiline string escaping, improve stderr redirection handling
- SDK: Add 会话 支持 and 权限 denial tracking
- Fix token limit 错误 in conversation summarization
- Opus Plan Mode: New setting in `/model` to run Opus only in plan mode, Sonnet otherwise

## 1.0.73

- MCP: 支持 multiple config 文件 with `--mcp-config 文件1.json 文件2.json`
- MCP: Press Esc to 取消 OAuth authentication flows
- Bash: 改进了 command validation and reduced false security 警告
- UI: Enhanced spinner animations and status line visual hierarchy
- Linux: 新增 支持 for Alpine and musl-based distributions (requires separate ripgrep 安装ation)

## 1.0.72

- Ask 权限: have Claude Code always ask for 确认ation to use specific tools with /权限

## 1.0.71

- Background commands: (Ctrl-b) to run any Bash command in the background so Claude can keep working (great for dev servers, tailing logs, etc.)
- Customizable status line: add your 终端 提示 to Claude Code with /statusline

## 1.0.70

- Performance: Optimized message rendering for better performance with large 上下文s
- Windows: 修复了 native 文件 search, ripgrep, and 子 agent functionality
- 新增 支持 for @-mentions in 斜杠命令 arguments

## 1.0.69

- Upgraded Opus to version 4.1

## 1.0.68

- Fix incorrect model names being used for certain commands like `/pr-comments`
- Windows: improve 权限 checks for allow / deny tools and project trust. This may 创建 a new project entry in `.claude.json` - manually 合并 the history field if desired.
- Windows: improve sub-process spawning to eliminate "No such 文件 or 目录" when running commands like pnpm
- Enhanced /doctor command with CLAUDE.md and MCP tool 上下文 for self-serve 调试ging
- SDK: 新增 canUseTool callback 支持 for tool 确认ation
- 新增 `禁用All钩子` setting
- 改进了 文件 suggestions performance in large repos

## 1.0.65

- IDE: 修复了 connection s标签页ility issues and 错误 handling for diagnostics
- Windows: 修复了 shell environment setup for users without .bashrc 文件

## 1.0.64

- Agents: 新增 model customization 支持 - you can 现在 specify which model an agent should use
- Agents: 修复了 unintended access to the recursive agent tool
- 钩子: 新增 systemMessage field to 钩子 JSON output for displaying 警告 and 上下文
- SDK: 修复了 user input tracking across multi-turn conversations
- 新增 hidden 文件 to 文件 search and @-mention suggestions

## 1.0.63

- Windows: 修复了 文件 search, @agent mentions, and custom 斜杠命令 functionality

## 1.0.62

- 新增 @-mention 支持 with typeahead for custom agents. @<your-custom-agent> to invoke it
- 钩子: 新增 会话Start 钩子 for new 会话 initialization
- /add-dir command 现在 支持 typeahead for 目录 路径s
- 改进了 network connectivity check reliability

## 1.0.61

- Transcript mode (Ctrl+R): 更改 Esc to 退出 transcript mode rather than interrupt
- 设置: 新增 `--设置` 标志 to 加载 设置 from a JSON 文件
- 设置: 修复了 resolution of 设置 文件 路径s that are symlinks
- OTEL: 修复了 reporting of wrong organization after authentication changes
- Slash commands: 修复了 权限 checking for allowed-tools with Bash
- IDE: 新增 支持 for pasting images in VSCode MacOS using ⌘+V
- IDE: 新增 `CLAUDE_CODE_AUTO_CONNECT_IDE=false` for disabling IDE auto-connection
- 新增 `CLAUDE_CODE_SHELL_PREFIX` for wrapping Claude and user-provided shell commands run by Claude Code

## 1.0.60

- You can 现在 创建 custom 子 agent for specialized tasks! Run /agents to get started

## 1.0.59

- SDK: 新增 tool 确认ation 支持 with canUseTool callback
- SDK: Allow specifying env for spawned process
- 钩子: Exposed 权限Decision to 钩子 (including "ask")
- 钩子: User提示提交 现在 支持 additional上下文 in advanced JSON output
- 修复了 issue where some Max users that specified Opus would still see fallback to Sonnet

## 1.0.58

- 新增 支持 for reading PDFs
- MCP: 改进了 server health status display in 'claude mcp list'
- 钩子: 新增 CLAUDE_PROJECT_DIR env var for 钩子 commands

## 1.0.57

- 新增 支持 for specifying a model in 斜杠命令
- 改进了 权限 messages to help Claude understand allowed tools
- Fix: Remove trailing newlines from bash output in 终端 wrapping

## 1.0.56

- Windows: 启用 shift+标签页 for mode switching on versions of Node.js that 支持 终端 VT mode
- Fixes for WSL IDE detection
- Fix an issue causing aws刷新Helper changes to .aws 目录 not to be picked up

## 1.0.55

- Clarified k现在ledge cutoff for Opus 4 and Sonnet 4 models
- Windows: 修复了 Ctrl+Z 崩溃
- SDK: 新增 ability to capture 错误 logging
- Add --system-提示-文件 option to override system 提示 in print mode

## 1.0.54

- 钩子: 新增 User提示提交 钩子 and the current working 目录 to 钩子 inputs
- Custom 斜杠命令: 新增 argument-hint to frontmatter
- Windows: OAuth uses port 45454 and properly constructs browser URL
- Windows: mode switching 现在 uses alt + m, and plan mode renders properly
- Shell: Switch to in-内存 shell snapshot to 修复 文件-related 错误

## 1.0.53

- 更新d @-mention 文件 truncation from 100 lines to 2000 lines
- Add helper script 设置 for AWS token 刷新: awsAuth刷新 (for foreground operations like aws sso login) and awsCredentialExport (for background operation with STS-like response).

## 1.0.52

- 新增 支持 for MCP 服务器 instructions

## 1.0.51

- 新增 支持 for native Windows (requires Git for Windows)
- 新增 支持 for Bedrock API keys through 环境变量 AWS_BEARER_TOKEN_BEDROCK
- 设置: /doctor can 现在 help you identify and 修复 invalid setting 文件
- `--append-system-提示` can 现在 be used in interactive mode, not just --print/-p.
- Increased auto-compact 警告 threshold from 60% to 80%
- 修复了 an issue with handling user 目录 with spaces for shell snapshots
- OTEL resource 现在 includes os.type, os.version, host.arch, and wsl.version (if running on Windows Subsystem for Linux)
- Custom 斜杠命令: 修复了 user-level commands in sub目录
- Plan mode: 修复了 issue where rejected plan from sub-task would get discarded

## 1.0.48

- 修复了 a bug in v1.0.45 where the app would sometimes freeze on launch
- 新增 progress messages to Bash 工具 based on the last 5 lines of command output
- 新增 expanding variables 支持 for MCP 服务器 配置
- Moved shell snapshots from /tmp to ~/.claude for more reliable Bash 工具 calls
- 改进了 IDE extension 路径 handling when Claude Code runs in WSL
- 钩子: 新增 a PreCompact 钩子
- Vim mode: 新增 c, f/F, t/T

## 1.0.45

- Redesigned Search (Grep) tool with new tool input parameters and features
- 禁用 IDE diffs for notebook 文件, 修复ing "超时 waiting after 1000ms" 错误
- 修复了 config 文件 corruption issue by enforcing atomic writes
- 更新d 提示 input undo to Ctrl+\_ to avoid breaking existing Ctrl+U behavior, matching zsh's undo shortcut
- Stop 钩子: 修复了 transcript 路径 after /clear and 修复了 triggering when loop ends with tool call
- Custom 斜杠命令: 恢复d namespacing in command names based on sub目录. For example, .claude/commands/frontend/component.md is 现在 /frontend:component, not /component.

## 1.0.44

- New /export command lets you quickly export a conversation for sharing
- MCP: resource_link tool results are 现在 支持ed
- MCP: tool annotations and tool titles 现在 display in /mcp view
- 更改 Ctrl+Z to suspend Claude Code. 恢复 by running `fg`. 提示 input undo is 现在 Ctrl+U.

## 1.0.43

- 修复了 a bug where the theme selector was saving excessively
- 钩子: 新增 EPIPE system 错误 handling

## 1.0.42

- 新增 tilde (`~`) expansion 支持 to `/add-dir` command

## 1.0.41

- 钩子: Split Stop 钩子 triggering into Stop and 子 agentStop
- 钩子: 启用 可选 超时 配置 for each command
- 钩子: 新增 "钩子_event_name" to 钩子 input
- 修复了 a bug where MCP tools would display twice in tool list
- New tool parameters JSON for Bash 工具 in `tool_decision` event

## 1.0.40

- 修复了 a bug causing API connection 错误 with UNABLE_TO_GET_ISSUER_CERT_LOCALLY if `NODE_EXTRA_CA_CERTS` was set

## 1.0.39

- New Active Time 指标 in Open遥测 logging

## 1.0.38

- Released 钩子. Special thanks to community input in https://github.com/anthropics/claude-code/issues/712. Docs: https://code.claude.com/docs/en/钩子

## 1.0.37

- Remove ability to set `Proxy-Authorization` header via ANTHROPIC_AUTH_TOKEN or apiKeyHelper

## 1.0.36

- Web search 现在 takes today's date into 上下文
- 修复了 a bug where stdio MCP 服务器 were not terminating properly on 退出

## 1.0.35

- 新增 支持 for MCP OAuth Authorization Server discovery

## 1.0.34

- 修复了 a 内存 leak causing a MaxListenersExceeded警告 message to appear

## 1.0.33

- 改进了 logging functionality with 会话 ID 支持
- 新增 提示 input undo functionality (Ctrl+Z and vim 'u' command)
- Improvements to plan mode

## 1.0.32

- 更新d loopback config for litellm
- 新增 forceLoginMethod setting to bypass login selection screen

## 1.0.31

- 修复了 a bug where ~/.claude.json would get reset when 文件 contained invalid JSON

## 1.0.30

- Custom 斜杠命令: Run bash output, @-mention 文件, 启用 thinking with thinking keywords
- 改进了 文件 路径 自动完成 with 文件name matching
- 新增 timestamps in Ctrl-r mode and 修复了 Ctrl-c handling
- Enhanced jq regex 支持 for complex filters with pipes and select

## 1.0.29

- 改进了 CJK character 支持 in cursor navigation and rendering

## 1.0.28

- Slash commands: Fix selector display during history navigation
- Resizes images before up加载 to prevent API size limit 错误
- 新增 XDG_CONFIG_HOME 支持 to 配置 目录
- Performance optimizations for 内存 usage
- New attributes (终端.type, language) in Open遥测 logging

## 1.0.27

- Streamable HTTP MCP 服务器 are 现在 支持ed
- Remote MCP 服务器 (SSE and HTTP) 现在 支持 OAuth
- MCP resources can 现在 be @-mentioned
- /恢复 斜杠命令 to switch conversations within Claude Code

## 1.0.25

- Slash commands: moved "project" and "user" pre修复es to descriptions
- Slash commands: 改进了 reliability for command discovery
- 改进了 支持 for Ghostty
- 改进了 web search reliability

## 1.0.24

- 改进了 /mcp output
- 修复了 a bug where 设置 arrays got overwritten instead of 合并d

## 1.0.23

- Released TypeScript SDK: import @anthropic-ai/claude-code to get started
- Released Python SDK: pip 安装 claude-code-sdk to get started

## 1.0.22

- SDK: Renamed `total_cost` to `total_cost_usd`

## 1.0.21

- 改进了 editing of 文件 with 标签页-based indentation
- Fix for tool_use without matching tool_result 错误
- 修复了 a bug where stdio MCP 服务器 processes would linger after quitting Claude Code

## 1.0.18

- 新增 --add-dir CLI argument for specifying additional working 目录
- 新增 流式传输 input 支持 without require -p 标志
- 改进了 启动 performance and 会话 storage performance
- 新增 CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR 环境变量 to freeze working 目录 for bash commands
- 新增 detailed MCP 服务器 tools display (/mcp)
- MCP authentication and 权限 improvements
- 新增 auto-reconnection for MCP SSE connections on disconnect
- 修复了 issue where pasted content was lost when 对话框s appeared

## 1.0.17

- We 现在 emit messages from sub-tasks in -p mode (look for the parent_tool_use_id property)
- 修复了 崩溃es when the VS Code diff tool is invoked multiple times quickly
- MCP 服务器 list UI improvements
- 更新 Claude Code process title to display "claude" instead of "node"

## 1.0.11

- Claude Code can 现在 also be used with a Claude Pro subscription
- 新增 /upgrade for smoother switching to Claude Max plans
- 改进了 UI for authentication from API keys and Bedrock/Vertex/external auth token
- 改进了 shell 配置 错误 handling
- 改进了 todo list handling during compaction

## 1.0.10

- 新增 markdown 标签页le 支持
- 改进了 流式传输 performance

## 1.0.8

- 修复了 Vertex AI region fallback when using CLOUD_ML_REGION
- Increased 默认 otel interval from 1s -> 5s
- 修复了 edge cases where MCP_TIMEOUT and MCP_TOOL_TIMEOUT weren't being respected
- 修复了 a regression where search tools unnecessarily asked for 权限
- 新增 支持 for triggering thinking non-English languages
- 改进了 compacting UI

## 1.0.7

- Renamed /allowed-tools -> /权限
- 迁移d allowedTools and ignorePatterns from .claude.json -> 设置.json
- 弃用 claude config commands in favor of editing 设置.json
- 修复了 a bug where --dangerously-skip-权限 sometimes didn't work in --print mode
- 改进了 错误 handling for /安装-github-app
- Bug修复es, UI polish, and tool reliability improvements

## 1.0.6

- 改进了 edit reliability for 标签页-indented 文件
- Respect CLAUDE_CONFIG_DIR everywhere
- Reduced unnecessary tool 权限 提示s
- 新增 支持 for symlinks in @文件 typeahead
- Bug修复es, UI polish, and tool reliability improvements

## 1.0.4

- 修复了 a bug where MCP tool 错误 weren't being parsed correctly

## 1.0.1

- 新增 `DISABLE_INTERLEAVED_THINKING` to give users the option to opt out of interleaved thinking.
- 改进了 model references to show provider-specific names (Sonnet 3.7 for Bedrock, Sonnet 4 for Console)
- 更新d documentation links and OAuth process descriptions

## 1.0.0

- Claude Code is 现在 generally 可用
- Introducing Sonnet 4 and Opus 4 models

## 0.2.125

- 破坏性更改: Bedrock ARN passed to `ANTHROPIC_MODEL` or `ANTHROPIC_SMALL_FAST_MODEL` should no longer contain an escaped slash (specify `/` instead of `%2F`)
- 移除 `DEBUG=true` in favor of `ANTHROPIC_LOG=调试`, to log all requests

## 0.2.117

- 破坏性更改: --print JSON output 现在 returns nested message objects, for forwards-compatibility as we introduce new metadata fields
- Introduced 设置.cleanupPeriodDays
- Introduced CLAUDE_CODE_API_KEY_HELPER_TTL_MS env var
- Introduced --调试 mode

## 0.2.108

- You can 现在 send messages to Claude while it works to steer Claude in real-time
- Introduced BASH_DEFAULT_TIMEOUT_MS and BASH_MAX_TIMEOUT_MS env vars
- 修复了 a bug where thinking was not working in -p mode
- 修复了 a regression in /cost reporting
- 弃用 MCP wizard interface in favor of other MCP commands
- Lots of other bug修复es and improvements

## 0.2.107

- CLAUDE.md 文件 can 现在 import other 文件. Add @路径/to/文件.md to ./CLAUDE.md to 加载 additional 文件 on launch

## 0.2.106

- MCP SSE server configs can 现在 specify custom headers
- 修复了 a bug where MCP 权限 提示 didn't always show correctly

## 0.2.105

- Claude can 现在 search the web
- Moved system & account status to /status
- 新增 word movement keybindings for Vim
- 改进了 latency for 启动, todo tool, and 文件 edits

## 0.2.102

- 改进了 thinking triggering reliability
- 改进了 @mention reliability for images and folders
- You can 现在 paste multiple large chunks into one 提示

## 0.2.100

- 修复了 a 崩溃 caused by a stack overflow 错误
- Made db storage 可选; missing db 支持 禁用s --continue and --恢复

## 0.2.98

- 修复了 an issue where auto-compact was running twice

## 0.2.96

- Claude Code can 现在 also be used with a Claude Max subscription (https://claude.ai/upgrade)

## 0.2.93

- 恢复 conversations from where you left off from with "claude --continue" and "claude --恢复"
- Claude 现在 has access to a Todo list that helps it stay on track and be more organized

## 0.2.82

- 新增 支持 for --disallowedTools
- Renamed tools for consistency: LSTool -> LS, View -> Read, etc.

## 0.2.75

- Hit Enter to queue up additional messages while Claude is working
- Drag in or copy/paste image 文件 directly into the 提示
- @-mention 文件 to directly add them to 上下文
- Run one-off MCP 服务器 with `claude --mcp-config <路径-to-文件>`
- 改进了 performance for 文件name auto-complete

## 0.2.74

- 新增 支持 for 刷新ing dynamically generated API keys (via apiKeyHelper), with a 5 minute TTL
- Task 工具 can 现在 perform writes and run bash commands

## 0.2.72

- 更新d spinner to indicate token 加载ed and tool usage

## 0.2.70

- Network commands like curl are 现在 可用 for Claude to use
- Claude can 现在 run multiple web queries in parallel
- Pressing ESC once immediately interrupts Claude in Auto-accept mode

## 0.2.69

- 修复了 UI glitches with 改进了 Select component behavior
- Enhanced 终端 output display with better text truncation logic

## 0.2.67

- Shared project 权限 rules can be saved in .claude/设置.json

## 0.2.66

- Print mode (-p) 现在 支持 流式传输 output via --output-format=stream-json
- 修复了 issue where pasting could trigger 内存 or bash mode unexpectedly

## 0.2.63

- 修复了 an issue where MCP tools were 加载ed twice, which caused tool call 错误

## 0.2.61

- Navigate 菜单s with vim-style keys (j/k) or bash/emacs shortcuts (Ctrl+n/p) for faster interaction
- Enhanced image detection for more reliable clipboard paste functionality
- 修复了 an issue where ESC key could 崩溃 the conversation history selector

## 0.2.59

- Copy+paste images directly into your 提示
- 改进了 progress indicators for bash and fetch tools
- Bug修复es for non-interactive mode (-p)

## 0.2.54

- Quickly add to 内存 by starting your message with '#'
- Press ctrl+r to see full output for long tool results
- 新增 支持 for MCP SSE transport

## 0.2.53

- New web fetch tool lets Claude view URLs that you paste in
- 修复了 a bug with JPEG detection

## 0.2.50

- New MCP "project" scope 现在 allows you to add MCP 服务器 to .mcp.json 文件 and 提交 them to your repository

## 0.2.49

- Previous MCP 服务器 scopes have been renamed: previous "project" scope is 现在 "local" and "global" scope is 现在 "user"

## 0.2.47

- Press 标签页 to auto-complete 文件 and folder names
- Press Shift + 标签页 to toggle auto-accept for 文件 edits
- Automatic conversation compaction for infinite conversation length (toggle with /config)

## 0.2.44

- Ask Claude to make a plan with thinking mode: just say 'think' or 'think harder' or even 'ultrathink'

## 0.2.41

- MCP 服务器 启动 超时 can 现在 be configured via MCP_TIMEOUT 环境变量
- MCP 服务器 启动 no longer blocks the app from starting up

## 0.2.37

- New /release-notes command lets you view release notes at any time
- `claude config add/remove` commands 现在 accept multiple values separated by commas or spaces

## 0.2.36

- Import MCP 服务器 from Claude Desktop with `claude mcp add-from-claude-desktop`
- Add MCP 服务器 as JSON strings with `claude mcp add-json <n> <json>`

## 0.2.34

- Vim bindings for text input - 启用 with /vim or /config

## 0.2.32

- Interactive MCP setup wizard: Run "claude mcp add" to add MCP 服务器 with a step-by-step interface
- Fix for some PersistentShell issues

## 0.2.31

- Custom 斜杠命令: Markdown 文件 in .claude/commands/ 目录 现在 appear as custom 斜杠命令 to insert 提示s into your conversation
- MCP 调试 mode: Run with --mcp-调试 标志 to get more information about MCP 服务器 错误

## 0.2.30

- 新增 ANSI color theme for better 终端 compatibility
- 修复了 issue where 斜杠命令 arguments weren't being sent properly
- (Mac-only) API keys are 现在 stored in macOS Keychain

## 0.2.26

- New /approved-tools command for managing tool 权限
- Word-level diff display for 改进了 code readability
- Fuzzy matching for 斜杠命令

## 0.2.21

- Fuzzy matching for /commands

