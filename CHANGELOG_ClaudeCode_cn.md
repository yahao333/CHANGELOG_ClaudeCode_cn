# Changelog

## 2.1.114

- 修复a crash在permission dialog当agent teams teammate requested tool permission

## 2.1.113

- 更改the CLI到spawn native Claude Code binary (via per-platform可选dependency) instead的bundled JavaScript
- 添加`sandbox.network.deniedDomains` setting到block特定domains even当broader `allowedDomains` wildcard将otherwise permit them
- 全屏 mode: Shift+↑/↓现在scrolls viewport当extending selection过去visible edge
- `Ctrl+A`和`Ctrl+E`现在move到start/end的current logical line在multiline input, matching readline behavior
- Windows: `Ctrl+Backspace`现在deletes上一个word
- Long URLs在responses和bash output stay clickable当they wrap across lines (in terminals使用OSC 8 hyperlinks)
- 改进`/loop`: pressing Esc现在cancels pending wakeups,和wakeups display作为"Claude resuming /loop wakeup"用于clarity
- `/extra-usage`现在works从Remote Control (mobile/web) clients
- Remote Control clients可以now query `@`-file autocomplete suggestions
- 改进`/ultrareview`: faster launch使用parallelized checks, diffstat在launch dialog,和animated launching state
- Subagents那stall mid-stream现在fail使用clear error之后10 minutes instead的hanging silently
- Bash tool: multi-line commands谁的first line是comment现在show full command在transcript, closing UI-spoofing vector
- 运行中 `cd <current-directory> && git …`不longer triggers permission prompt当`cd`是no-op
- Security:在macOS, `/private/{etc,var,tmp,home}` paths是now treated作为dangerous removal targets under `Bash(rm:*)` allow rules
- Security: Bash deny rules现在match commands wrapped在`env`/`sudo`/`watch`/`ionice`/`setsid`和similar exec wrappers
- Security: `Bash(find:*)` allow rules不longer auto-approve `find -exec`/`-delete`
- 修复MCP concurrent-call超时handling哪里message用于one tool call可以silently disarm另一个call's watchdog
- 修复Cmd-backspace / `Ctrl+U`到once again delete从cursor到start的line
- 修复markdown tables breaking当cell contains inline code span使用pipe character
- 修复session recap auto-firing当composing unsent text在prompt
- 修复`/copy` "Full response" not aligning markdown table columns用于pasting into GitHub, 否tion,或Slack
- 修复messages typed当viewing运行subagent being hidden从its transcript和misattributed到parent AI
- 修复Bash `dangerously禁用Sandbox`运行commands outside sandbox without permission prompt
- 修复`/effort auto` confirmation —现在says "Effort level set到max"到match status bar label
- 修复the "copied N chars" toast overcounting emoji和other multi-code-unit characters
- 修复`/insights` crashing使用`EBUSY`在Windows
- 修复exit confirmation dialog mislabeling one-shot scheduled tasks作为recurring —现在shows countdown
- 修复slash/@ completion menu not sitting flush against prompt border在fullscreen mode
- 修复`CLAUDE_CODE_EXTRA_BODY` `output_config.effort` causing 400 errors在subagent calls到models那don't support effort和on Vertex AI
- 修复prompt cursor disappearing当`NO_COLOR`是set
- 修复`Tool搜索` ranking所以pasted MCP tool names surface actual tool instead的description-matching siblings
- 修复compacting恢复long-context session failing使用"Extra usage是required用于long context requests"
- 修复`plugin install` succeeding当dependency version conflicts使用already-installed plugin —现在reports `range-conflict`
- 修复"Refine使用Ultraplan" not showing远程session URL在transcript
- 修复SDK image content blocks那fail到process crashing session —现在degrade到text placeholder
- 修复Remote Control sessions not streaming subagent transcripts
- 修复Remote Control sessions not being archived当Claude Code exits
- 修复`thinking.type.enabled是not supported` 400 error当using Opus 4.7 via Bedrock Application Inference 分析 ARN

## 2.1.112

- 修复"claude-opus-4-7是temporarily unavailable"用于auto mode

## 2.1.111

- Claude Opus 4.7 xhigh是now available! Use /effort到tune speed vs. intelligence
- Auto mode是now available用于Max subscribers当using Opus 4.7
- 添加`xhigh` effort level用于Opus 4.7, sitting between `high`和`max`. Available via `/effort`, `--effort`,和model picker;其他models fall back到`high`
- `/effort`现在opens interactive slider当called without arguments,使用arrow-key navigation between levels和输入到confirm
- 添加"Auto (match terminal)" theme option那matches您的terminal's dark/light mode — select it从`/theme`
- 添加`/less-permission-prompts` skill — scans transcripts用于common read-only Bash和MCP tool calls和proposes prioritized allowlist用于`.claude/settings.json`
- 添加`/ultrareview`用于running comprehensive code review在cloud using parallel multi-agent analysis和critique — invoke使用no arguments到review您的current branch,或`/ultrareview <PR#>`到fetch和review特定GitHub PR
- Auto mode不longer requires `--enable-auto-mode`
- Windows: PowerShell tool是progressively rolling out. Opt in或out使用`CLAUDE_CODE_USE_POWERSHELL_TOOL`. 开 Linux和macOS, enable使用`CLAUDE_CODE_USE_POWERSHELL_TOOL=1` (requires `pwsh`在PATH)
- 读取-only bash commands使用glob patterns (e.g. `ls *.ts`)和commands starting使用`cd <project-dir> &&`不longer trigger permission prompt
- Suggest closest matching subcommand当`claude <word>`是invoked使用near-miss typo (e.g. `claude udpate` → "Did您mean `claude update`?")
- Plan files是now named after您的prompt (e.g. `fix-auth-race-snug-otter.md`) instead的purely random words
- 改进`/setup-vertex`和`/setup-bedrock`到show actual `settings.json` path当`CLAUDE_CONFIG_DIR`是set, seed model candidates从existing pins在re-run,和offer "with 1M context" option用于supported models
- `/skills` menu现在supports sorting通过estimated token count — press `t`到toggle
- `Ctrl+U`现在clears entire input buffer (previously: delete到start的line); press `Ctrl+Y`到restore
- `Ctrl+L`现在forces full screen redraw在addition到clearing prompt input
- Transcript view footer现在shows `[` (dump到scrollback)和`v` (open在editor) shortcuts
- The "+N lines" marker用于truncated长pastes是now full-width rule用于easier scanning
- Headless `--output-format stream-json`现在includes `plugin_errors`在init event当plugins是demoted用于unsatisfied dependencies
- 添加`OTEL_LOG_RAW_API_BODIES` environment variable到emit full API request和response bodies作为打开Telemetry log events用于debugging
- Suppressed spurious decompression, network,和transient错误messages那could appear在TUI在normal operation
- 回滚了the v2.1.110 cap在non-streaming fallback retries —它traded长waits用于more outright failures在API overload
- 修复terminal display tearing (random characters, drifting input)在iTerm2 + tmux setups当terminal notifications是sent
- 修复`@` file suggestions re-scanning entire project在every turn在non-git工作directories,和showing仅config files在freshly-initialized git repos使用no跟踪files
- 修复LSP diagnostics从before edit appearing之后it, causing model到re-read files它just edited
- 修复tab-completing `/resume` immediately resuming arbitrary titled session instead的showing session picker
- 修复`/context` grid rendering使用extra blank lines between rows
- 修复`/clear` dropping session name set通过`/rename`, causing statusline output到lose `session_name`
- 改进plugin错误handling: dependency errors现在distinguish conflicting, invalid,和overly复杂version requirements;修复stale解决versions之后`plugin update`; `plugin install`现在recovers从interrupted先前installs
- 修复Claude calling non-existent `commit` skill和showing "Unknown skill: commit"用于users without自定义`/commit` command
- 修复429 rate-limit errors在Bedrock/Vertex/Foundry referencing status.claude.com (it仅covers Anthropic-operated providers)
- 修复feedback surveys appearing back-to-back之后dismissing one
- 修复bare URLs在bash/PowerShell/MCP tool output being unclickable当terminal wraps them across lines
- Windows: `CLAUDE_ENV_FILE`和会话启动 hook environment files现在apply (previously no-op)
- Windows: permission rules使用drive-letter paths是now correctly root-anchored,和paths differing only通过drive-letter case是recognized作为same path

## 2.1.110

- 添加`/tui` command和`tui` setting — run `/tui fullscreen`到switch到flicker-free rendering在same conversation
- 添加push notification tool — Claude可以send mobile push notifications当Remote Control和"推送当Claude decides" config是enabled
- 更改`Ctrl+O`到toggle between normal和verbose transcript only; focus view是now切换separately使用new `/focus` command
- 添加`auto滚动启用d` config到disable conversation auto-scroll在fullscreen mode
- 添加option到show Claude's最后response作为commented context在`Ctrl+G` external editor (enable via `/config`)
- 改进`/plugin` 安装ed tab — items needing attention和favorites appear在top,禁用items是hidden behind fold,和`f` favorites选中item
- 改进`/doctor`到warn当MCP server是defined在multiple config scopes使用different endpoints
- `--resume`/`--continue`现在resurrects unexpired scheduled tasks
- `/context`, `/exit`,和`/reload-plugins`现在work从Remote Control (mobile/web) clients
- 写入 tool现在informs model当you edit proposed content在IDE diff之前accepting
- Bash tool现在enforces已记录maximum超时instead的accepting arbitrarily large values
- SDK/headless sessions现在read `TRACEPARENT`/`TRACESTATE`从environment用于distributed trace linking
- 会话 recap是now enabled用于users使用telemetry禁用(Bedrock, Vertex, Foundry, `DISABLE_TELEMETRY`). Opt out via `/config`或`CLAUDE_CODE_ENABLE_AWAY_SUMMARY=0`.
- 修复MCP tool calls hanging indefinitely当server connection drops mid-response在SSE/HTTP transports
- 修复non-streaming fallback retries causing multi-minute hangs当API是unreachable
- 修复session recap,本地slash-command output,和other system status lines not appearing在focus mode
- 修复high CPU usage在fullscreen当text是selected当tool是running
- 修复plugin install not honoring dependencies declared在`plugin.json`当marketplace entry omits them; `/plugin` install现在lists auto-installed dependencies
- 修复skills使用`disable-model-invocation: true` failing当invoked via `/<skill>` mid-message
- 修复`--resume` sometimes showing第一prompt instead的`/rename` name用于sessions仍然running或exited uncleanly
- 修复queued messages briefly appearing twice在multi-tool-call turns
- 修复session cleanup not removing full session directory including subagent transcripts
- 修复dropped keystrokes之后CLI relaunches (e.g. `/tui`, provider setup wizards)
- 修复garbled startup rendering在macOS Terminal.app和other terminals那don't support synchronized output
- 强化了"打开在editor" actions against command injection从untrusted filenames
- 修复`Permission请求` hooks returning `updatedInput` not being re-checked against `permissions.deny` rules; `set模式:'bypassPermissions'` updates现在respect `disableBypassPermissions模式`
- 修复`PreToolUse` hook `additional上下文` being dropped当tool call fails
- 修复stdio MCP servers那print stray non-JSON lines到stdout being disconnected在first stray line (regression在2.1.105)
- 修复headless/SDK session auto-title firing extra Haiku request当`CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC`或`CLAUDE_CODE_DISABLE_TERMINAL_TITLE`是set
- 修复potential excessive memory allocation当piped (non-TTY) Ink output contains single very wide line
- 修复`/skills` menu not scrolling当list overflows modal在fullscreen mode
- 修复Remote Control sessions showing通用error instead的prompting用于re-login当session是too old
- 修复Remote Control session renames从claude.ai not persisting title到local CLI session

## 2.1.109

- 改进the extended-thinking indicator使用rotating progress hint

## 2.1.108

- 添加`ENABLE_PROMPT_CACHING_1H` env var到opt into 1-hour prompt cache TTL在API key, Bedrock, Vertex,和Foundry (`ENABLE_PROMPT_CACHING_1H_BEDROCK`是deprecated but仍然honored),和`FORCE_PROMPT_CACHING_5M`到force 5-minute TTL
- 添加recap feature到provide context当returning到session, configurable在`/config`和manually invocable使用`/recap`; force使用`CLAUDE_CODE_ENABLE_AWAY_SUMMARY`如果telemetry disabled.
- The model可以now discover和invoke built-in slash commands喜欢`/init`, `/review`,和`/security-review` via 技能 tool
- `/undo`是now alias用于`/rewind`
- 改进`/model`到warn之前switching models mid-conversation,自从next response re-reads full history uncached
- 改进`/resume` picker到default到sessions从current directory; press `Ctrl+A`到show所有projects
- 改进error messages: server rate limits是now distinguished从plan usage limits; 5xx/529 errors show link到status.claude.com; unknown slash commands suggest closest match
- 减少了memory footprint用于file reads, edits,和syntax highlighting通过loading language grammars在demand
- 添加"verbose" indicator当viewing detailed transcript (`Ctrl+O`)
- 添加a warning在startup当prompt caching是disabled via `DISABLE_PROMPT_CACHING*` environment variables
- 修复paste not working在`/login` code prompt (regression在2.1.105)
- 修复subscribers谁set `DISABLE_TELEMETRY` falling back到5-minute prompt cache TTL instead的1 hour
- 修复智能体 tool prompting用于permission在auto mode当safety classifier's transcript exceeded它的context window
- 修复Bash tool producing不output当`CLAUDE_ENV_FILE` (e.g. `~/.zprofile`) ends使用`#` comment line
- 修复`claude --resume <session-id>` losing session's自定义name和color set via `/rename`
- 修复session titles showing placeholder example text当first message是short greeting
- 修复terminal escape codes appearing作为garbage text在prompt input之后`--teleport`
- 修复`/feedback` retry: pressing 输入到resubmit之后failure现在works without第一editing description
- 修复`--teleport`和`--resume <id>` precondition errors (e.g. dirty git tree, session not found) exiting silently instead的showing错误message
- 修复Remote Control session titles set在web UI being overwritten通过auto-generated titles之后third message
- 修复`--resume` truncating sessions当transcript contained self-referencing message
- 修复transcript write failures (e.g., disk full) being silently dropped instead的being logged
- 修复diacritical marks (accents, umlauts, cedillas) being dropped从responses当`language` setting是configured
- 修复policy-managed plugins never auto-updating当running从different project than哪里they是first installed

## 2.1.107

- Show thinking hints sooner在long operations

## 2.1.105

- 添加`path` parameter到`输入Worktree` tool到switch into existing worktree的current repository
- 添加PreCompact hook support: hooks可以now block compaction通过exiting使用code 2或returning `{"decision":"block"}`
- 添加background monitor support用于plugins via top-level `monitors` manifest key那auto-arms在session start或on skill invoke
- `/proactive`是now alias用于`/loop`
- 改进stalled API stream handling: streams现在abort之后5 minutes的no data和retry non-streaming instead的hanging indefinitely
- 改进network错误messages: connection errors现在show retry message immediately instead的silent spinner
- 改进file write display:长single-line writes (e.g. minified JSON)是now truncated在UI instead的paginating across很多screens
- 改进`/doctor` layout使用status icons; press `f`到have Claude fix reported issues
- 改进`/config` labels和descriptions用于clarity
- 改进skill description handling: raised listing cap从250到1,536 characters和added startup warning当descriptions是truncated
- 改进`Web获取`到strip `<style>`和`<script>` contents从fetched pages所以CSS-heavy pages不longer exhaust content budget之前reaching actual text
- 改进stale agent worktree cleanup到remove worktrees谁的PR是squash-merged instead的keeping them indefinitely
- 改进MCP large-output truncation prompt到give format-specific recipes (e.g. `jq`用于JSON, computed 读取 chunk sizes用于text)
- 修复images attached到queued messages (sent当Claude是working) being dropped
- 修复screen going blank当prompt input wraps到second line在long conversations
- 修复leading whitespace getting copied当selecting multi-line assistant responses在fullscreen mode
- 修复leading whitespace being trimmed从assistant messages, breaking ASCII art和indented diagrams
- 修复garbled bash output当commands print clickable file links (e.g. Python `rich`/`loguru` logging)
- 修复alt+enter not inserting newline在terminals using ESC-prefix alt encoding,和Ctrl+J not inserting newline (regression在2.1.100)
- 修复duplicate "Creating worktree" text在输入Worktree/ExitWorktree tool display
- 修复queued user prompts disappearing从focus mode
- 修复one-shot scheduled tasks re-firing repeatedly当file watcher missed post-fire cleanup
- 修复inbound channel notifications being silently dropped之后first message用于团队/输入prise users
- 修复marketplace plugins使用`package.json`和lockfile not having dependencies安装automatically之后install/update
- 修复marketplace auto-update leaving official marketplace在broken state当plugin process holds files open在update
- 修复"恢复这session with..." hint not printing在exit之后`/resume`, `--worktree`,或`/branch`
- 修复feedback survey shortcut keys firing当typed在end的longer prompt
- 修复stdio MCP server emitting malformed (non-JSON) output hanging session instead的failing fast使用"连接 closed"
- 修复MCP tools missing在first turn的headless/remote-trigger sessions当MCP servers connect asynchronously
- 修复`/model` picker在AWS Bedrock在non-US regions persisting无效`us.*` model IDs到`settings.json`当inference profile discovery是still in-flight
- 修复429 rate-limit errors showing raw JSON dump instead的clean message用于API-key, Bedrock,和Vertex users
- 修复crash在resume当session contains malformed text blocks
- 修复`/help` dropping tab bar, Shortcuts heading,和footer在short terminal heights
- 修复malformed keybinding entry values在`keybindings.json` being silently loaded instead的rejected使用clear error
- 修复`CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC`在one project's settings permanently disabling usage metrics用于all projects在machine
- 修复washed-out 16-color palette当using Ghostty, Kitty, Alacritty, WezTerm, foot, rio,或Contour over SSH/mosh
- 修复Bash tool suggesting `accept编辑s` permission mode当exiting plan mode将downgrade从higher permission level

## 2.1.101

- 添加`/team-onboarding` command到generate teammate ramp-up guide从your本地Claude Code usage
- 添加OS CA certificate store trust通过default,所以enterprise TLS proxies work without extra setup (set `CLAUDE_CODE_CERT_STORE=bundled`到use仅bundled CAs)
- `/ultraplan`和other remote-session features现在auto-create默认cloud environment instead的requiring web setup first
- 改进brief mode到retry once当Claude responds使用plain text instead的structured message
- 改进focus mode: Claude现在writes更多self-contained summaries since它knows您only see它的final message
- 改进tool-not-available errors到explain why和how到proceed当model calls tool那exists but isn't available在current context
- 改进rate-limit retry messages到show哪个limit是hit和when它resets instead的opaque seconds countdown
- 改进refusal错误messages到include API-provided explanation当available
- 改进`claude -p --resume <name>`到accept session titles set via `/rename`或`--name`
- 改进settings resilience: unrecognized hook event name在`settings.json`不longer causes entire file到be ignored
- 改进plugin hooks从plugins force-enabled通过managed settings到run当`allowManagedHooks开ly`是set
- 改进`/plugin`和`claude plugin update`到show warning当marketplace可以not be refreshed, instead的silently reporting stale version
- 改进plan mode到hide "Refine使用Ultraplan" option当user's org或auth setup can't reach Claude Code在web
- 改进beta tracing到honor `OTEL_LOG_USER_PROMPTS`, `OTEL_LOG_TOOL_DETAILS`,和`OTEL_LOG_TOOL_CONTENT`; sensitive span attributes是no longer emitted除非opted in
- 改进SDK `query()`到clean up subprocess和temp files当consumers `break`从`for await`或use `await using`
- 修复a command injection vulnerability在POSIX `which` fallback used通过LSP binary detection
- 修复a memory leak哪里long sessions retained dozens的historical copies的message list在virtual scroller
- 修复`--resume`/`--continue` losing conversation context在large sessions当loader anchored在dead-end branch instead的live conversation
- 修复`--resume` chain recovery bridging into unrelated subagent conversation当subagent message landed near main-chain write gap
- 修复a crash在`--resume`当persisted 编辑/写入 tool result是missing它的`file_path`
- 修复a hardcoded 5-minute request timeout那aborted慢backends (local LLMs,扩展thinking,慢gateways) regardless的`API_TIMEOUT_MS`
- 修复`permissions.deny` rules not overriding PreToolUse hook's `permissionDecision: "ask"` — previously hook可以downgrade deny into prompt
- 修复`--setting-sources` without `user` causing后台cleanup到ignore `cleanupPeriodDays`和delete conversation history更旧than 30 days
- 修复Bedrock SigV4 authentication failing使用403当`ANTHROPIC_AUTH_T确定EN`, `apiKeyHelper`,或`ANTHROPIC_CUSTOM_HEADERS` set Authorization header
- 修复`claude -w <name>` failing使用"already exists"之后previous session's worktree cleanup left stale directory
- 修复subagents not inheriting MCP tools从dynamically-injected servers
- 修复sub-agents running在isolated worktrees being拒绝读取/编辑 access到files inside它们的own worktree
- 修复sandboxed Bash commands failing使用`mktemp: 否这样的file或directory`之后fresh boot
- 修复`claude mcp serve` tool calls failing使用"Tool execution failed"在MCP clients那validate `outputSchema`
- 修复`RemoteTrigger` tool's `run` action sending empty body和being rejected通过server
- 修复several `/resume` picker issues: narrow默认view hiding sessions从other projects, unreachable preview在Windows Terminal,不正确cwd在worktrees, session-not-found errors not surfacing在stderr, terminal title not being set,和resume hint overlapping prompt input
- 修复Grep tool ENOENT当embedded ripgrep binary path becomes stale (VS Code extension auto-update, macOS App Translocation);现在falls back到system `rg`和self-heals mid-session
- 修复`/btw` writing copy的entire conversation到disk在every use
- 修复`/context` Free space和消息s breakdown disagreeing使用header percentage
- 修复several plugin issues: slash commands resolving到wrong plugin使用duplicate `name:` frontmatter, `/plugin update` failing使用`ENAMETOOLONG`, Discover showing already-installed plugins, directory-source plugins loading从stale version cache,和skills not honoring `context: fork`和`agent` frontmatter fields
- 修复the `/mcp` menu offering OAuth-specific actions用于MCP servers configured使用`headersHelper`; Reconnect是now offered instead到re-invoke helper script
- 修复`ctrl+]`, `ctrl+\`,和`ctrl+^` keybindings not firing在terminals那send raw C0 control bytes (Terminal.app,默认iTerm2, xterm)
- 修复`/login` OAuth URL rendering使用padding那prevented clean mouse selection
- 修复rendering issues: flicker在non-fullscreen mode当content above可见area changed, terminal scrollback being wiped在long sessions在non-fullscreen mode,和mouse-scroll escape sequences occasionally leaking into prompt作为text
- 修复crash当`settings.json` env values是numbers instead的strings
- 修复in-app settings writes (e.g. `/add-dir --remember`, `/config`) not refreshing in-memory snapshot, preventing移除directories从being revoked mid-session
- 修复custom keybindings (`~/.claude/keybindings.json`) not loading在Bedrock, Vertex,和other third-party providers
- 修复`claude --continue -p` not correctly continuing sessions created通过`-p`或SDK
- 修复several Remote Control issues: worktrees removed在session crash, connection failures not persisting在transcript, spurious "已断开" indicator在brief mode用于local sessions,和`/remote-control` failing over SSH当only `CLAUDE_CODE_ORGANIZATION_UUID`是set
- 修复`/insights` sometimes omitting report file link从its response
- [VSCode] 修复了file attachment below chat input not clearing当last editor tab是closed

## 2.1.98

- 添加interactive Google Vertex AI setup wizard accessible从login screen当selecting "3rd-party platform", guiding您through GCP authentication, project和region configuration, credential verification,和model pinning
- 添加`CLAUDE_CODE_PERFORCE_MODE` env var:当set, 编辑/写入/否tebook编辑 fail在read-only files使用`p4 edit` hint instead的silently overwriting them
- 添加监控 tool用于streaming events从background scripts
- 添加subprocess sandboxing使用PID namespace isolation在Linux当`CLAUDE_CODE_SUBPROCESS_ENV_SCRUB`是set,和`CLAUDE_CODE_SCRIPT_CAPS` env var到limit per-session script invocations
- 添加`--exclude-dynamic-system-prompt-sections` flag到print mode用于improved cross-user prompt caching
- 添加`workspace.git_worktree`到status line JSON input, set whenever当前directory是inside linked git worktree
- 添加W3C `TRACEPARENT` env var到Bash tool subprocesses当OTEL tracing是enabled,所以child-process spans correctly parent到Claude Code's trace tree
- LSP: Claude Code现在identifies itself到language servers via `client信息`在initialize request
- 修复a Bash tool permission bypass哪里backslash-escaped flag可以be auto-allowed作为read-only和lead到arbitrary code execution
- 修复compound Bash commands bypassing forced permission prompts用于safety checks和explicit ask rules在auto和bypass-permissions modes
- 修复read-only commands使用env-var prefixes not prompting除非var是known-safe (`LANG`, `TZ`, `NO_COLOR`, etc.)
- 修复redirects到`/dev/tcp/...`或`/dev/udp/...` not prompting instead的auto-allowing
- 修复stalled streaming responses timing out instead的falling back到non-streaming mode
- 修复429 retries burning所有attempts在~13s当server returns small `重试-After` — exponential backoff现在applies作为minimum
- 修复MCP OAuth `oauth.authServerMetadataUrl` config override not being honored在token refresh之后restart, affecting ADFS和similar IdPs
- 修复capital letters being dropped到lowercase在xterm和VS Code integrated terminal当kitty keyboard protocol是active
- 修复macOS text replacements deleting trigger word instead的inserting substitution
- 修复`--dangerously-skip-permissions` being silently downgraded到accept-edits mode之后approving write到protected path via Bash
- 修复managed-settings allow rules remaining active之后admin移除them,直到process restart
- 修复`permissions.additionalDirectories` changes not applying mid-session —移除directories lose access immediately和added ones work without restart
- 修复removing directory从`additionalDirectories` revoking access到same directory通过via `--add-dir`
- 修复`Bash(cmd:*)`和`Bash(git commit *)` wildcard permission rules failing到match commands使用extra spaces或tabs
- 修复`Bash(...)` deny rules being downgraded到prompt用于piped commands那mix `cd`使用other segments
- 修复false Bash permission prompts用于`cut -d /`, `paste -d /`, `column -s /`, `awk '{print $1}' file`,和filenames containing `%`
- 修复permission rules使用names matching JavaScript prototype properties (e.g. `toString`) causing `settings.json`到be silently ignored
- 修复agent team members not inheriting leader's permission mode当using `--dangerously-skip-permissions`
- 修复a crash在fullscreen mode当hovering over MCP tool results
- 修复copying wrapped URLs在fullscreen mode inserting spaces在line breaks
- 修复file-edit diffs disappearing从UI在`--resume`当edited file是larger than 10KB
- 修复several `/resume` picker issues: `--resume <name>` opening uneditable, filter reload wiping search state, empty list swallowing arrow keys, cross-project staleness,和transient task-status text replacing conversation summaries
- 修复`/export` not honoring absolute paths和`~`,和silently rewriting user-supplied extensions到`.txt`
- 修复`/effort max` being denied用于unknown或future model IDs
- 修复slash command picker breaking当plugin's frontmatter `name`是YAML boolean keyword
- 修复rate-limit upsell text being hidden之后message remounts
- 修复MCP tools使用`_meta["anthropic/maxResultSizeChars"]` not bypassing token-based persist layer
- 修复voice mode leaking dozens的space characters into input当re-holding push-to-talk key当previous transcript是still processing
- 修复`DISABLE_AUTOUPDATER` not fully suppressing npm registry version check和symlink modification在npm-based installs
- 修复a memory leak哪里Remote Control permission handler entries是retained用于lifetime的session
- 修复background subagents那fail使用error not reporting partial progress到parent agent
- 修复prompt-type 停止/Subagent停止 hooks failing在long sessions,和hook evaluator API errors showing "JSON validation failed" instead的real message
- 修复feedback survey rendering当dismissed
- 修复Bash `grep -f FILE` / `rg -f FILE` not prompting当reading pattern file outside工作directory
- 修复stale subagent worktree cleanup removing worktrees那contain untracked files
- 修复`sandbox.network.allowMachLookup` not taking effect在macOS
- 改进`/resume` filter hint labels和added project/worktree/branch names在filter indicator
- 改进footer indicators (Focus, notifications)到stay在mode-indicator row instead的wrapping在narrow terminal widths
- 改进`/agents`使用tabbed layout: 运行中 tab shows live subagents,和Library tab adds Run agent和View运行instance actions
- 改进`/reload-plugins`到pick up plugin-provided skills without requiring restart
- 改进接受 编辑s mode到auto-approve filesystem commands prefixed使用safe env vars或process wrappers
- 改进Vim mode: `j`/`k`在NORMAL mode现在navigate history和select footer pill在input boundary
- 改进hook errors在transcript到include第一line的stderr用于self-diagnosis without `--debug`
- 改进OTEL tracing: interaction spans现在correctly wrap full turns under concurrent SDK calls,和headless turns end spans per-turn
- 改进transcript entries到carry final token usage instead的streaming placeholders
- 更新d `/claude-api` skill到cover Managed 智能体s alongside Claude API
- [VSCode] 修复ed false-positive "requires git-bash" error在Windows当`CLAUDE_CODE_GIT_BASH_PATH`是set或Git是installed在default location
- 修复`CLAUDE_CODE_MAX_CONTEXT_T确定ENS`到honor `DISABLE_COMPACT`当it是set.
- 放弃了`/compact` hints当`DISABLE_COMPACT`是set.

## 2.1.97

- 添加focus view toggle (`Ctrl+O`)在`NO_FLICKER` mode showing prompt, one-line tool summary使用edit diffstats,和final response
- 添加`refreshInterval` status line setting到re-run status line command每个N seconds
- 添加`workspace.git_worktree`到status line JSON input, set当current directory是inside linked git worktree
- 添加`● N running` indicator在`/agents` next到agent types使用live subagent instances
- 添加syntax highlighting用于Cedar policy files (`.cedar`, `.cedarpolicy`)
- 修复`--dangerously-skip-permissions` being silently downgraded到accept-edits mode之后approving write到protected path
- 修复and hardened Bash tool permissions, tightening checks around env-var prefixes和network redirects,和reducing假prompts在common commands
- 修复permission rules使用names matching JavaScript prototype properties (e.g. `toString`) causing `settings.json`到be silently ignored
- 修复managed-settings allow rules remaining active之后admin移除them直到process restart
- 修复`permissions.additionalDirectories` changes在settings not applying mid-session
- 修复removing directory从`settings.permissions.additionalDirectories` revoking access到same directory通过via `--add-dir`
- 修复MCP HTTP/SSE connections accumulating ~50 MB/hr的unreleased buffers当servers reconnect
- 修复MCP OAuth `oauth.authServerMetadataUrl` not being honored在token refresh之后restart, fixing ADFS和similar IdPs
- 修复429 retries burning所有attempts在~13 seconds当server returns small `重试-After` — exponential backoff现在applies作为minimum
- 修复rate-limit upgrade options disappearing之后context compaction
- 修复several `/resume` picker issues: `--resume <name>` opening uneditable, Ctrl+A reload wiping search, empty list swallowing navigation, task-status text replacing conversation summary,和cross-project staleness
- 修复file-edit diffs disappearing在`--resume`当edited file是larger than 10KB
- 修复`--resume` cache misses和lost mid-turn input从attachment messages not being saved到transcript
- 修复messages typed当Claude是working not being persisted到transcript
- 修复prompt-type `停止`/`Subagent停止` hooks failing在long sessions,和hook evaluator API errors displaying "JSON validation failed" instead的actual message
- 修复subagents使用worktree isolation或`cwd:` override leaking它们的working directory back到parent session's Bash tool
- 修复compaction writing重复multi-MB subagent transcript files在prompt-too-long retries
- 修复`claude plugin update` reporting "already在latest version"用于git-based marketplace plugins当remote有newer commits
- 修复slash command picker breaking当plugin's frontmatter `name`是YAML boolean keyword
- 修复copying wrapped URLs在`NO_FLICKER` mode inserting spaces在line breaks
- 修复scroll rendering artifacts在`NO_FLICKER` mode当running inside zellij
- 修复a crash在`NO_FLICKER` mode当hovering over MCP tool results
- 修复a `NO_FLICKER` mode memory leak哪里API retries left stale streaming state
- 修复slow mouse-wheel scrolling在`NO_FLICKER` mode在Windows Terminal
- 修复custom status line not displaying在`NO_FLICKER` mode在terminals shorter than 24 rows
- 修复Shift+输入和Alt/Cmd+arrow shortcuts not working在Warp使用`NO_FLICKER` mode
- 修复Korean/Japanese/Unicode text becoming garbled当copied在no-flicker mode在Windows
- 修复Bedrock SigV4 authentication failing当`AWS_BEARER_T确定EN_BEDROCK`或`ANTHROPIC_BEDROCK_BASE_URL`是set到empty strings (as GitHub Actions does用于unset inputs)
- 改进接受 编辑s mode到auto-approve filesystem commands prefixed使用safe env vars或process wrappers (e.g. `LANG=C rm foo`, `timeout 5 mkdir out`)
- 改进auto mode和bypass-permissions mode到auto-approve sandbox network access prompts
- 改进sandbox: `sandbox.network.allowMachLookup`现在takes effect在macOS
- 改进image handling: pasted和attached images是now compressed到same token budget作为images read via 读取 tool
- 改进slash command和`@`-mention completion到trigger之后CJK sentence punctuation,所以Japanese/Chinese input不longer requires space之前`/`或`@`
- 改进Bridge sessions到show本地git repo, branch,和working directory在claude.ai session card
- 改进footer layout: indicators (Focus, notifications)现在stay在mode-indicator row instead的wrapping below
- 改进context-low warning到show作为transient footer notification instead的persistent row
- 改进markdown blockquotes到show continuous left bar across wrapped lines
- 改进session transcript size通过skipping empty hook entries和capping stored pre-edit file copies
- 改进transcript accuracy: per-block entries现在carry final token usage instead的streaming placeholder
- 改进Bash tool OTEL tracing: subprocesses现在inherit W3C `TRACEPARENT` env var当tracing是enabled
- 更新d `/claude-api` skill到cover Managed 智能体s alongside Claude API

## 2.1.96

- 修复Bedrock requests failing使用`403 "Authorization header是missing"`当using `AWS_BEARER_T确定EN_BEDROCK`或`CLAUDE_CODE_SKIP_BEDROCK_AUTH` (regression在2.1.94)

## 2.1.94

- 添加support用于Amazon Bedrock powered通过Mantle, set `CLAUDE_CODE_USE_MANTLE=1`
- 更改default effort level从medium到high用于API-key, Bedrock/Vertex/Foundry, 团队,和输入prise users (control this使用`/effort`)
- 添加compact `Slacked #channel` header使用clickable channel link用于Slack MCP send-message tool calls
- 添加`keep-coding-instructions` frontmatter field support用于plugin output styles
- 添加`hookSpecificOutput.sessionTitle`到`User提示提交` hooks用于setting session title
- 插件 skills declared via `"skills": ["./"]`现在use skill's frontmatter `name`用于invocation name instead的directory basename, giving稳定name across install methods
- 修复agents appearing stuck之后429 rate-limit response使用long 重试-After header — error现在surfaces immediately instead的silently waiting
- 修复Console login在macOS silently failing使用"否t记录in"当login keychain是locked或its password是out的sync — error是now surfaced和`claude doctor` diagnoses fix
- 修复plugin skill hooks defined在YAML frontmatter being silently ignored
- 修复plugin hooks failing使用"否这样的file或directory"当`CLAUDE_PLUGIN_ROOT`是not set
- 修复`${CLAUDE_PLUGIN_ROOT}` resolving到marketplace source directory instead的installed cache用于local-marketplace plugins在startup
- 修复scrollback showing相同diff repeated和blank pages在long-running sessions
- 修复multiline user prompts在transcript indenting wrapped lines under `❯` caret instead的under text
- 修复Shift+Space inserting literal word "space" instead的space character在search inputs
- 修复hyperlinks opening two browser tabs当clicked inside tmux running在xterm.js-based terminal (VS Code, Hyper, Tabby)
- 修复an alt-screen rendering bug哪里content height changes mid-scroll可以leave compounding ghost lines
- 修复`FORCE_HYPERLINK` environment variable being ignored当set via `settings.json` `env`
- 修复native terminal cursor not tracking选中tab在dialogs,所以screen readers和magnifiers可以follow tab navigation
- 修复Bedrock invocation的Sonnet 3.5 v2通过using `us.` inference profile ID
- 修复SDK/print mode not preserving partial assistant response在conversation history当interrupted mid-stream
- 改进`--resume`到resume sessions从other worktrees的same repo directly instead的printing `cd` command
- 修复CJK和other multibyte text being corrupted使用U+FFFD在stream-json input/output当chunk boundaries split UTF-8 sequence
- [VSCode] Reduced cold-open subprocess work在starting session
- [VSCode] 修复ed dropdown menus selecting错误item当mouse是over list当typing或using arrow keys
- [VSCode] 添加了警告banner当`settings.json` files fail到parse,所以users know它们的permission rules是not being applied

## 2.1.92

- 添加`forceRemoteSettingsRefresh` policy setting:当set, CLI blocks startup直到remote managed settings是freshly fetched,和exits如果fetch fails (fail-closed)
- 添加interactive Bedrock setup wizard accessible从login screen当selecting "3rd-party platform" — guides您through AWS authentication, region configuration, credential verification,和model pinning
- 添加per-model和cache-hit breakdown到`/cost`用于subscription users
- `/release-notes`是now interactive version picker
- Remote Control session names现在use您的hostname作为default prefix (e.g. `myhost-graceful-unicorn`), overridable使用`--remote-control-session-name-prefix`
- Pro users现在see footer hint当returning到session之后prompt cache有expired, showing roughly how很多tokens下一个turn将send uncached
- 修复subagent spawning permanently failing使用"Could not determine pane count"之后tmux windows是killed或renumbered在long-running session
- 修复prompt-type 停止 hooks incorrectly failing当small快速model returns `ok:false`,和restored `preventContinuation:true` semantics用于non-停止 prompt-type hooks
- 修复tool input validation failures当streaming emits array/object fields作为JSON-encoded strings
- 修复an API 400 error那could occur当extended thinking produced whitespace-only text block alongside real content
- 修复accidental feedback survey submissions从auto-pilot keypresses和consecutive-prompt digit collisions
- 修复misleading "esc到interrupt" hint appearing alongside "esc到clear"当text selection exists在fullscreen mode在processing
- 修复Homebrew install update prompts到use cask's release channel (`claude-code` → stable, `claude-code@latest` → latest)
- 修复`ctrl+e` jumping到end的next line当already在end的line在multiline prompts
- 修复an issue where相同message可以appear在two positions当scrolling up在fullscreen mode (iTerm2, Ghostty,和other terminals使用DEC 2026 support)
- 修复idle-return "/clear到save X tokens" hint showing cumulative session tokens instead的current context size
- 修复plugin MCP servers stuck "connecting"在session start当they重复claude.ai connector that是unauthenticated
- 改进写入 tool diff computation speed用于large files (60% faster在files使用tabs/`&`/`$`)
- 移除`/tag` command
- 移除`/vim` command (toggle vim mode via `/config` → 编辑or mode)
- Linux sandbox现在ships `apply-seccomp` helper在both npm和native builds, restoring unix-socket blocking用于sandboxed commands

## 2.1.91

- 添加MCP tool result persistence override via `_meta["anthropic/maxResultSizeChars"]` annotation (up到500K), allowing larger results喜欢DB schemas到pass through without truncation
- 添加`disable技能ShellExecution` setting到disable inline shell execution在skills,自定义slash commands,和plugin commands
- 添加support用于multi-line prompts在`claude-cli://open?q=` deep links (encoded newlines `%0A`不longer rejected)
- 插件s可以now ship executables under `bin/`和invoke them作为bare commands从Bash tool
- 修复transcript chain breaks在`--resume`那could lose conversation history当async transcript writes fail silently
- 修复`cmd+delete` not deleting到start的line在iTerm2, kitty, WezTerm, Ghostty,和Windows Terminal
- 修复plan mode在remote sessions losing track的plan file之后container restart,哪个caused permission prompts在plan edits和empty plan-approval modal
- 修复JSON schema validation用于`permissions.default模式: "auto"`在settings.json
- 修复Windows version cleanup not protecting活动version's rollback copy
- `/feedback`现在explains为什么it's unavailable instead的disappearing从slash menu
- 改进`/claude-api` skill guidance用于agent design patterns including tool surface decisions, context management,和caching strategy
- 改进performance: faster `stripAnsi`在Bun通过routing through `Bun.stripANSI`
- 编辑 tool现在uses shorter `old_string` anchors, reducing output tokens

## 2.1.90

- 添加`/powerup` — interactive lessons teaching Claude Code features使用animated demos
- 添加`CLAUDE_CODE_PLUGIN_KEEP_MARKETPLACE_ON_FAILURE` env var到keep existing marketplace cache当`git pull` fails, useful在offline environments
- 添加`.husky`到protected directories (accept编辑s mode)
- 修复an infinite loop哪里rate-limit options dialog将repeatedly auto-open之后hitting您的usage limit, eventually crashing session
- 修复`--resume` causing full prompt-cache miss在first request用于users使用deferred tools, MCP servers,或custom agents (regression自从v2.1.69)
- 修复`编辑`/`写入` failing使用"文件 content有changed"当PostToolUse format-on-save hook rewrites file between consecutive edits
- 修复`PreToolUse` hooks那emit JSON到stdout和exit使用code 2 not correctly blocking tool call
- 修复collapsed search/read summary badge appearing multiple times在fullscreen scrollback当CLAUDE.md file auto-loads在tool call
- 修复auto mode not respecting explicit user boundaries ("don't push", "wait用于X之前Y") even当action将otherwise be allowed
- 修复click-to-expand hover text being nearly invisible在light terminal themes
- 修复UI crash当malformed tool input reached permission dialog
- 修复headers disappearing当scrolling `/model`, `/config`,和other selection screens
- 强化了PowerShell tool permission checks:修复trailing `&`后台job bypass, `-错误Action Break` debugger hang, archive-extraction TOCTOU,和parse-fail fallback deny-rule degradation
- 改进performance: eliminated per-turn JSON.stringify的MCP tool schemas在cache-key lookup
- 改进performance: SSE transport现在handles large streamed frames在linear time (was quadratic)
- 改进performance: SDK sessions使用long conversations不longer慢down quadratically在transcript writes
- 改进`/resume` all-projects view到load project sessions在parallel, improving load times用于users使用many projects
- 更改`--resume` picker到no longer show sessions created通过`claude -p`或SDK invocations
- 移除`Get-DnsClient缓存`和`ipconfig /displaydns`从auto-allow (DNS cache privacy)

## 2.1.89

- 添加`"defer"` permission decision到`PreToolUse` hooks — headless sessions可以pause在tool call和resume使用`-p --resume`到have hook re-evaluate
- 添加`CLAUDE_CODE_NO_FLICKER=1` environment variable到opt into flicker-free alt-screen rendering使用virtualized scrollback
- 添加`PermissionDenied` hook那fires之后auto mode classifier denials — return `{retry: true}`到tell model它can retry
- 添加named subagents到`@` mention typeahead suggestions
- 添加`MCP_CONNECTION_NONBLOCKING=true`用于`-p` mode到skip MCP connection wait entirely,和bounded `--mcp-config` server connections在5s instead的blocking在slowest server
- Auto mode:拒绝commands现在show notification和appear在`/permissions` → Recent tab where您can retry使用`r`
- 修复`编辑(//path/**)`和`读取(//path/**)` allow rules到check解决symlink target, not刚刚requested path
- 修复voice push-to-talk not activating用于some modifier-combo bindings,和voice mode在Windows failing使用"WebSocket upgrade rejected使用HTTP 101"
- 修复编辑/写入 tools doubling CRLF在Windows和stripping Markdown困难line breaks (two trailing spaces)
- 修复`StructuredOutput` schema cache bug causing ~50%失败rate当using multiple schemas
- 修复memory leak哪里large JSON inputs是retained作为LRU cache keys在long-running sessions
- 修复a crash当removing message从very large session files (over 50MB)
- 修复LSP server zombie state之后crash — server现在restarts在next request instead的failing直到session restart
- 修复prompt history entries containing CJK或emoji being silently dropped当they fall在4KB boundary在`~/.claude/history.jsonl`
- 修复`/stats` undercounting tokens通过excluding subagent usage,和losing historical data beyond 30 days当stats cache format changes
- 修复`-p --resume` hangs当deferred tool input exceeds 64KB或no deferred marker exists,和`-p --continue` not resuming deferred tools
- 修复`claude-cli://` deep links not opening在macOS
- 修复MCP tool errors truncating到only第一content block当server returns multi-element错误content
- 修复skill reminders和other system context being dropped当sending messages使用images via SDK
- 修复PreToolUse/PostToolUse hooks到receive `file_path`作为absolute path用于写入/编辑/读取 tools, matching已记录behavior
- 修复autocompact thrash loop —现在detects当context refills到limit immediately之后compacting three times在row和stops使用actionable错误instead的burning API calls
- 修复prompt cache misses在long sessions caused通过tool schema bytes changing mid-session
- 修复nested CLAUDE.md files being re-injected dozens的times在long sessions那read很多files
- 修复`--resume` crash当transcript contains tool result从older CLI version或interrupted write
- 修复misleading "Rate limit reached" message当API returned entitlement错误—现在shows actual error使用actionable hints
- 修复hooks `if` condition filtering not matching compound commands (`ls && git push`)或commands使用env-var prefixes (`FOO=bar git push`)
- 修复collapsed search/read group badges duplicating在terminal scrollback在heavy parallel tool use
- 修复notification `invalidates` not clearing currently-displayed notification immediately
- 修复prompt briefly disappearing之后submit当background messages arrived在processing
- 修复Devanagari和other combining-mark text being truncated在assistant output
- 修复rendering artifacts在main-screen terminals之后layout shifts
- 修复voice mode failing到request microphone permission在macOS Apple Silicon
- 修复Shift+输入 submitting instead的inserting newline在Windows Terminal 预览 1.25
- 修复periodic UI jitter在streaming在iTerm2当running inside tmux
- 修复PowerShell tool incorrectly reporting failures当commands喜欢`git push` wrote progress到stderr在Windows PowerShell 5.1
- 修复a potential out-of-memory crash当编辑 tool是used在very large files (>1 GiB)
- 改进collapsed tool summary到show "Listed N directories"用于`ls`/`tree`/`du` instead的"读取 N files"
- 改进Bash tool到warn当formatter/linter command modifies files you有previously read, preventing stale-edit errors
- 改进`@`-mention typeahead到rank source files above MCP resources使用similar names
- 改进PowerShell tool prompt使用version-appropriate syntax guidance (5.1 vs 7+)
- 更改`编辑`到work在files viewed via `Bash`使用`sed -n`或`cat`, without requiring separate `读取` call first
- 更改hook output over 50K characters到be saved到disk使用file path + preview instead的being injected directly into context
- 更改`cleanupPeriodDays: 0`在settings.json到be rejected使用validation错误—它previously silently禁用transcript persistence
- 更改thinking summaries到no longer be generated通过default在interactive sessions — set `showThinkingSummaries: true`在settings.json到restore
- Documented `Task创建d` hook event和its blocking behavior
- 保留了task notifications当backgrounding运行command使用Ctrl+B
- PowerShell tool在Windows: external-command arguments containing两者double-quote和whitespace现在prompt instead的auto-allowing (PS 5.1 argument-splitting hardening)
- `/env`现在applies到PowerShell tool commands (previously仅affected Bash)
- `/usage`现在hides redundant "Current week (Sonnet only)" bar用于Pro和输入prise plans
- 图像 paste不longer inserts trailing space
- Pasting `!command` into empty prompt现在enters bash mode, matching输入`!` behavior
- `/buddy`是here用于April 1st — hatch small creature那watches您code

## 2.1.87

- 修复messages在Cowork Dispatch not getting delivered

## 2.1.86

- 添加`X-Claude-Code-会话-Id` header到API requests所以proxies可以aggregate requests通过session without parsing body
- 添加`.jj`和`.sl`到VCS directory exclusion lists所以Grep和file autocomplete don't descend into Jujutsu或Sapling metadata
- 修复`--resume` failing使用"tool_use ids是found without tool_result blocks"在sessions created之前v2.1.85
- 修复写入/编辑/读取 failing在files outside project root (e.g., `~/.claude/CLAUDE.md`)当conditional skills或rules是configured
- 修复unnecessary config disk writes在every skill invocation那could cause performance issues和config corruption在Windows
- 修复potential out-of-memory crash当using `/feedback`在very长sessions使用large transcript files
- 修复`--bare` mode dropping MCP tools在interactive sessions和silently discarding messages enqueued mid-turn
- 修复the `c` shortcut copying仅~20 characters的OAuth login URL instead的full URL
- 修复masked input (e.g., OAuth code paste) leaking start的token当wrapping across multiple lines在narrow terminals
- 修复official marketplace plugin scripts failing使用"Permission denied"在macOS/Linux自从v2.1.83
- 修复statusline showing另一个session's model当running multiple Claude Code instances和using `/model`在one的them
- 修复scroll not following新messages之后wheel scroll或click-to-select在bottom的long conversation
- 修复`/plugin` uninstall dialog: pressing `n`现在correctly uninstalls plugin当preserving它的data directory
- 修复a regression哪里pressing 输入之后clicking可以leave transcript blank直到response arrived
- 修复`ultrathink` hint lingering之后deleting keyword
- 修复memory growth在long sessions从markdown/highlight render caches retaining full content strings
- 减少了startup event-loop stalls当many claude.ai MCP connectors是configured (macOS keychain cache extended从5s到30s)
- 减少了token overhead当mentioning files使用`@` — raw string content不longer JSON-escaped
- 改进prompt cache hit rate用于Bedrock, Vertex,和Foundry users通过removing dynamic content从tool descriptions
- Memory filenames在"Saved N memories" notice现在highlight在hover和open在click
- 技能 descriptions在`/skills` listing是now capped在250 characters到reduce context usage
- 更改`/skills` menu到sort alphabetically用于easier scanning
- Auto mode现在shows "unavailable用于your plan"当disabled通过plan restrictions (was "temporarily unavailable")
- [VSCode] 修复ed extension incorrectly showing "否t responding"在long-running operations
- [VSCode] 修复ed extension defaulting Max plan users到Sonnet之后OAuth token refreshes (8 hours之后login)
- 读取 tool现在uses compact line-number format和deduplicates unchanged re-reads, reducing token usage

## 2.1.85

- 添加`CLAUDE_CODE_MCP_SERVER_NAME`和`CLAUDE_CODE_MCP_SERVER_URL` environment variables到MCP `headersHelper` scripts, allowing one helper到serve multiple servers
- 添加conditional `if` field用于hooks using permission rule syntax (e.g., `Bash(git *)`)到filter当they run, reducing process spawning overhead
- 添加timestamp markers在transcripts当scheduled tasks (`/loop`, `Cron创建`) fire
- 添加trailing space之后`[图像 #N]` placeholder当pasting images
- Deep link queries (`claude-cli://open?q=…`)现在support up到5,000 characters,使用"scroll到review" warning用于long pre-filled prompts
- MCP OAuth现在follows RFC 9728 Protected Resource Metadata discovery到find authorization server
- 插件s blocked通过organization policy (`managed-settings.json`)可以no longer be installed或enabled,和are hidden从marketplace views
- PreToolUse hooks可以now satisfy `AskUserQuestion`通过returning `updatedInput` alongside `permissionDecision: "allow"`, enabling headless integrations那collect answers via它们的own UI
- `tool_parameters`在打开Telemetry tool_result events是now gated behind `OTEL_LOG_TOOL_DETAILS=1`
- 修复`/compact` failing使用"context exceeded"当conversation有grown也large用于compact request itself到fit
- 修复`/plugin enable`和`/plugin disable` failing当plugin's install location differs从where it's declared在settings
- 修复`--worktree` exiting使用error在non-git repositories之前`Worktree创建` hook可以run
- 修复`deniedMcpServers` setting not blocking claude.ai MCP servers
- 修复`switch_display`在computer-use tool returning "not available在this session"在multi-monitor setups
- 修复crash当`OTEL_LOGS_EXPORTER`, `OTEL_METRICS_EXPORTER`,或`OTEL_TRACES_EXPORTER`是set到`none`
- 修复diff syntax highlighting not working在non-native builds
- 修复MCP step-up authorization failing当refresh token exists — servers requesting elevated scopes via `403 insufficient_scope`现在correctly trigger re-authorization flow
- 修复memory leak在remote sessions当streaming response是interrupted
- 修复persistent ECONNRESET errors在edge connection churn通过using fresh TCP connection在retry
- 修复prompts getting stuck在queue之后running certain slash commands,使用up-arrow unable到retrieve them
- 修复Python 智能体 SDK: `type:'sdk'` MCP servers通过via `--mcp-config`是no longer dropped在startup
- 修复raw key sequences appearing在prompt当running over SSH或in VS Code integrated terminal
- 修复Remote Control session status staying stuck在"Requires Action"之后permission是resolved
- 修复shift+enter和meta+enter being intercepted通过typeahead suggestions instead的inserting newlines
- 修复stale content bleeding through当scrolling up在streaming
- 修复terminal left在enhanced keyboard mode之后exit在Ghostty, Kitty, WezTerm,和other terminals supporting Kitty keyboard protocol — Ctrl+C和Ctrl+D现在work correctly之后quitting
- 改进@-mention file autocomplete performance在large repositories
- 改进PowerShell dangerous command detection
- 改进scroll performance使用large transcripts通过replacing WASM yoga-layout使用pure 输入Script implementation
- 减少了UI stutter当compaction triggers在large sessions

## 2.1.84

- 添加PowerShell tool用于Windows作为opt-in preview. Learn more在https://code.claude.com/docs/en/tools-reference#powershell-tool
- 添加`ANTHROPIC_DEFAULT_{OPUS,SONNET,HAIKU}_MODEL_SUPPORTS` env vars到override effort/thinking capability detection用于pinned默认models用于3p (Bedrock, Vertex, Foundry),和`_MODEL_NAME`/`_DESCRIPTION`到customize `/model` picker label
- 添加`CLAUDE_STREAM_IDLE_TIMEOUT_MS` env var到configure streaming idle watchdog threshold (default 90s)
- 添加`Task创建d` hook那fires当task是created via `Task创建`
- 添加`Worktree创建` hook support用于`type: "http"` — return创建worktree path via `hookSpecificOutput.worktree路径`在response JSON
- 添加`allowedChannel插件s` managed setting用于team/enterprise admins到define channel plugin allowlist
- 添加`x-client-request-id` header到API requests用于debugging timeouts
- 添加idle-return prompt那nudges users returning之后75+ minutes到`/clear`, reducing unnecessary token re-caching在stale sessions
- Deep links (`claude-cli://`)现在open在your preferred terminal instead的whichever terminal happens到be first在detection list
- Rules和skills `paths:` frontmatter现在accepts YAML list的globs
- MCP tool descriptions和server instructions是now capped在2KB到prevent 打开API-generated servers从bloating context
- MCP servers configured两者locally和via claude.ai connectors是now deduplicated —本地config wins
- Background bash tasks那appear stuck在interactive prompt现在surface notification之后~45 seconds
- Token counts ≥1M现在display作为"1.5m" instead的"1512.6k"
- Global system-prompt caching现在works当`Tool搜索`是enabled, including用于users使用MCP tools configured
- 修复voice push-to-talk: holding voice key不longer leaks characters into text input,和transcripts现在insert在correct position
- 修复up/down arrow keys being unresponsive当footer item是focused
- 修复`Ctrl+U` (kill-to-line-start) being no-op在line boundaries在multiline input,所以repeated `Ctrl+U`现在clears across lines
- 修复null-unbinding默认chord binding (e.g. `"ctrl+x ctrl+k": null`)仍然entering chord-wait mode instead的freeing prefix key
- 修复mouse events inserting literal "mouse" text into transcript search input
- 修复workflow subagents failing使用API 400当outer session uses `--json-schema`和subagent也specifies schema
- 修复missing后台color behind certain emoji在user message bubbles在some terminals
- 修复the "allow Claude到edit它的own settings用于this session" permission option not sticking用于users使用`编辑(.claude)` allow rules
- 修复a hang当generating attachment snippets用于large edited files
- 修复MCP tool/resource cache leak在server reconnect
- 修复a startup performance issue哪里partial clone repositories (Scalar/GVFS) triggered mass blob downloads
- 修复native terminal cursor not tracking text input caret,所以IME composition (CJK input)现在renders inline和screen readers可以follow input position
- 修复spurious "否t记录in" errors在macOS caused通过transient keychain read failures
- 修复cold-start race哪里core tools可以be deferred without它们的bypass active, causing 编辑/写入到fail使用InputValidation错误在typed parameters
- 改进detection用于dangerous removals的Windows drive roots (`C:\`, `C:\Windows`, etc.)
- 改进interactive startup通过~30ms通过running `setup()`在parallel使用slash command和agent loading
- 改进startup用于`claude "prompt"`使用MCP servers — REPL现在renders immediately instead的blocking直到all servers connect
- 改进Remote Control到show特定reason当blocked instead的generic "not仍enabled" message
- 改进p90 prompt cache rate
- 减少了scroll-to-top resets在long sessions通过making message window immune到compaction和grouping changes
- 减少了terminal flickering当animated tool progress scrolls above viewport
- 更改issue/PR references到only become clickable links当written作为`owner/repo#123` — bare `#123`是no longer auto-linked
- Slash commands unavailable用于current auth setup (`/voice`, `/mobile`, `/chrome`, `/upgrade`, etc.)是now隐藏instead的shown
- [VSCode] Added rate limit警告banner使用usage percentage和reset time
- Stats screenshot (Ctrl+S在/stats)现在works在all builds和is 16× faster

## 2.1.83

- 添加`managed-settings.d/` drop-in directory alongside `managed-settings.json`, letting separate teams deploy independent policy fragments那merge alphabetically
- 添加`CwdChanged`和`文件Changed` hook events用于reactive environment management (e.g., direnv)
- 添加`sandbox.failIfUnavailable` setting到exit使用error当sandbox是enabled but cannot start, instead的running unsandboxed
- 添加`disableDeep链接Registration` setting到prevent `claude-cli://` protocol handler registration
- 添加`CLAUDE_CODE_SUBPROCESS_ENV_SCRUB=1`到strip Anthropic和cloud provider credentials从subprocess environments (Bash tool, hooks, MCP stdio servers)
- 添加transcript search — press `/`在transcript mode (`Ctrl+O`)到search, `n`/`N`到step through matches
- 添加`Ctrl+X Ctrl+E`作为alias用于opening external editor (readline-native binding; `Ctrl+G`仍然works)
- Pasted images现在insert `[图像 #N]` chip在cursor so您can reference them positionally在your prompt
- 智能体s可以now declare `initial提示`在frontmatter到auto-submit第一turn
- `chat:kill智能体s`和`chat:fast模式`是now rebindable via `~/.claude/keybindings.json`
- 修复mouse tracking escape sequences leaking到shell prompt之后exit
- 修复Claude Code hanging在exit在macOS
- 修复screen flashing blank之后being idle用于few seconds
- 修复a hang当diffing very large files使用few常见lines — diffs现在time out之后5 seconds和fall back gracefully
- 修复a 1–8第二UI freeze在startup当voice input是enabled, caused通过eagerly loading native audio module
- 修复a startup regression哪里Claude Code将wait ~3s用于claude.ai MCP config fetch之前proceeding
- 修复`--mcp-config` CLI flag bypassing `allowedMcpServers`/`deniedMcpServers` managed policy enforcement
- 修复claude.ai MCP connectors (Slack, Gmail, etc.) not being available在single-turn `--print` mode
- 修复`caffeinate` process not properly terminating当Claude Code exits, preventing Mac从sleeping
- 修复bash mode not activating当tab-accepting `!`-prefixed command suggestions
- 修复stale slash command selection showing错误highlighted command之后navigating suggestions
- 修复`/config` menu showing两者search cursor和list selection在same time
- 修复background subagents becoming invisible之后context compaction, which可以cause重复agents到be spawned
- 修复background agent tasks staying stuck在"running" state当git或API calls hang在cleanup
- 修复`--channels` showing "Channels是not currently available"在first launch之后upgrade
- 修复uninstalled plugin hooks continuing到fire直到next session
- 修复queued commands flickering在streaming responses
- 修复slash commands being sent到model作为text当submitted当message是processing
- 修复scrollback jumping当collapsed read/search groups finish之后scrolling offscreen
- 修复scrollback jumping到top当model starts或stops thinking
- 修复SDK session history loss在resume caused通过hook progress/attachment messages forking parentUuid chain
- 修复copy-on-select not firing当you release mouse outside terminal window
- 修复ghost characters appearing在height-constrained lists当items overflow
- 修复`Ctrl+B` interfering使用readline backward-char在idle prompt —它now仅fires当foreground task可以be backgrounded
- 修复tool result files never being cleaned up, ignoring `cleanupPeriodDays` setting
- 修复space key being swallowed用于up到3 seconds之后releasing voice hold-to-talk
- 修复ALSA library errors corrupting terminal UI当using voice mode在Linux without audio hardware (Docker, headless, WSL1)
- 修复voice mode SoX detection在Termux/Android哪里spawning `which`是kernel-restricted
- 修复Remote Control sessions showing作为Idle在web session list当actively running
- 修复footer navigation selecting invisible Remote Control pill在config-driven mode
- 修复memory leak在remote sessions哪里tool use IDs accumulate indefinitely
- 改进Bedrock SDK cold-start latency通过overlapping profile fetch使用other boot work
- 改进`--resume` memory usage和startup latency在large sessions
- 改进plugin startup — commands, skills,和agents现在load从disk cache without re-fetching
- 改进Remote Control session titles: AI-generated titles现在appear within seconds的first message
- 改进`Web获取`到identify作为`Claude-User`所以site operators可以recognize和allowlist Claude Code traffic via `robots.txt`
- 减少了`Web获取` peak memory usage用于large pages
- 减少了scrollback resets在long sessions从once per turn到once per ~50 messages
- Faster `claude -p` startup使用unauthenticated HTTP/SSE MCP servers (~600ms saved)
- Bash ghost-text suggestions现在include just-submitted commands immediately
- 提高了non-streaming fallback token cap (21k → 64k)和timeout (120s → 300s local)所以fallback requests是less likely到be truncated
- Interrupting prompt之前any response现在automatically restores您的input so您can edit和resubmit
- `/status`现在works当Claude是responding, instead的being queued直到turn finishes
- 插件 MCP servers那duplicate org-managed connector是now suppressed instead的running第二connection
- Linux: respect `XDG_DATA_HOME`当registering `claude-cli://` protocol handler
- 更改"stop所有background agents" keybinding从`Ctrl+F`到`Ctrl+X Ctrl+K`到stop shadowing readline forward-char
- 弃用`TaskOutput` tool在favor的using `读取`在background task's output file path
- 添加`CLAUDE_CODE_DISABLE_NONSTREAMING_FALLBACK` env var到disable non-streaming fallback当streaming fails
- 插件 options (`manifest.userConfig`)现在available externally — plugins可以prompt用于configuration在enable time,使用`sensitive: true` values stored在keychain (macOS)或protected credentials file (other platforms)
- Claude可以now reference on-disk path的clipboard-pasted images用于file operations
- `Ctrl+L`现在clears screen和forces full redraw — use this到recover当Cmd+K leaves UI partially blank. Use `Ctrl+U`或double-Esc到clear prompt input.
- `--bare -p` (SDK pattern)是~14% faster到API request
- Memory: `MEMORY.md` index现在truncates在25KB作为well作为200 lines
- 禁用d `AskUserQuestion`和plan-mode tools当`--channels`是active
- 修复API 400 error当pasted image是queued在failing tool call
- 修复MCP tool calls hanging indefinitely当SSE connection drops mid-call和exhausts它的reconnection attempts
- 修复Remote Control session titles showing raw XML当background agent completed之前first user message
- 修复remote sessions forgetting conversation history之后container restart due到progress-message gaps在resumed transcript chain
- 修复remote sessions requiring re-login在transient auth errors instead的retrying automatically
- 修复`rg ... | wc -l`和similar piped commands hanging和returning `0`在sandbox mode在Linux
- 修复voice input hold-to-talk not activating当CJK IME inserts full-width space
- 修复`--worktree` hanging silently当worktree name contained forward slash
- [VSCode] 旋转指示器现在turns red使用"否t responding"当backend hasn't responded用于60 seconds
- [VSCode] 修复ed session history not loading correctly当reopening session via URL或after restart
- [VSCode] Added Esc-twice (or `/rewind`)到open keyboard-navigable rewind picker
- [VSCode] 修复ed "复刻 conversation从here"和rewind actions failing silently之后session cache goes stale

## 2.1.81

- 添加`--bare` flag用于scripted `-p` calls — skips hooks, LSP, plugin sync,和skill directory walks; requires `ANTHROPIC_API_KEY`或`apiKeyHelper` via `--settings` (OAuth和keychain auth disabled); auto-memory fully disabled
- 添加`--channels` permission relay — channel servers那declare permission capability可以forward tool approval prompts到your phone
- 修复multiple concurrent Claude Code sessions requiring repeated re-authentication当one session refreshes它的OAuth token
- 修复voice mode silently swallowing retry failures和showing misleading "check您的network" message instead的actual error
- 修复voice mode audio not recovering当server silently drops WebSocket connection
- 修复`CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` not suppressing structured-outputs beta header, causing 400 errors在proxy gateways forwarding到Vertex/Bedrock
- 修复`--channels` bypass用于团队/输入prise orgs使用no其他managed settings configured
- 修复a crash在否de.js 18
- 修复unnecessary permission prompts用于Bash commands containing dashes在strings
- 修复plugin hooks blocking prompt submission当plugin directory是deleted mid-session
- 修复a race condition哪里background agent task output可以hang indefinitely当task完成between polling intervals
-恢复中 session那was在worktree现在switches back到that worktree
- 修复`/btw` not including粘贴text当used在active response
- 修复a race哪里fast Cmd+Tab followed通过paste可以beat clipboard copy under tmux
- 修复terminal tab title not updating使用auto-generated session description
- 修复invisible hook attachments inflating message count在transcript mode
- 修复Remote Control sessions showing通用title instead的deriving从first prompt
- 修复`/rename` not syncing title用于Remote Control sessions
- 修复Remote Control `/exit` not reliably archiving session
- 改进MCP read/search tool calls到collapse into single "Queried {server}" line (expand使用Ctrl+O)
- 改进`!` bash mode discoverability — Claude现在suggests it当you need到run interactive command
- 改进plugin freshness — ref-tracked plugins现在re-clone在every load到pick up upstream changes
- 改进Remote Control session titles到refresh after您的third message
- 更新d MCP OAuth到support Client ID Metadata Document (CIMD / SEP-991)用于servers without Dynamic Client Registration
- 更改plan mode到hide "clear context" option通过default (restore使用`"showClear上下文开Plan接受": true`)
- 禁用d line-by-line response streaming在Windows (including WSL在Windows Terminal) due到rendering issues
- [VSCode] 修复ed Windows PATH inheritance用于Bash tool当using Git Bash (regression在v2.1.78)

## 2.1.80

- 添加`rate_limits` field到statusline scripts用于displaying Claude.ai rate limit usage (5-hour和7-day windows使用`used_percentage`和`resets_at`)
- 添加`source: 'settings'` plugin marketplace source — declare plugin entries inline在settings.json
- 添加CLI tool usage detection到plugin tips,在addition到file pattern matching
- 添加`effort` frontmatter support用于skills和slash commands到override model effort level当invoked
- 添加`--channels` (research preview) — allow MCP servers到push messages into您的session
- 修复`--resume` dropping parallel tool results — sessions使用parallel tool calls现在restore所有tool_use/tool_result pairs instead的showing `[Tool result missing]` placeholders
- 修复voice mode WebSocket failures caused通过Cloudflare bot detection在non-browser TLS fingerprints
- 修复400 errors当using fine-grained tool streaming through API proxies, Bedrock,或Vertex
- 修复`/remote-control` appearing用于gateway和third-party provider deployments where它cannot function
- 修复`/sandbox` tab switching not responding到Tab或arrow keys
- 改进responsiveness的`@` file autocomplete在large git repositories
- 改进`/effort`到show什么auto currently resolves to, matching status bar indicator
- 改进`/permissions` — Tab和arrow keys现在switch tabs从within list
- 改进background tasks panel — left arrow现在closes从list view
- 简化了plugin install tips到use single `/plugin install` command instead的two-step flow
- 减少了memory usage在startup在large repositories (~80 MB saved在250k-file repos)
- 修复managed settings (`enabled插件s`, `permissions.default模式`, policy-set env vars) not being applied在startup当`remote-settings.json`是cached从prior session

## 2.1.79

- 添加`--console` flag到`claude auth login`用于Anthropic Console (API billing) authentication
- 添加"Show turn duration" toggle到`/config` menu
- 修复`claude -p` hanging当spawned作为subprocess without explicit stdin (e.g. Python `subprocess.run`)
- 修复Ctrl+C not working在`-p` (print) mode
- 修复`/btw` returning主要agent's output instead的answering side question当triggered在streaming
- 修复voice mode not activating correctly在startup当`voice启用d: true`是set
- 修复left/right arrow tab navigation在`/permissions`
- 修复`CLAUDE_CODE_DISABLE_TERMINAL_TITLE` not preventing terminal title从being set在startup
- 修复custom status line showing nothing当workspace trust是blocking it
- 修复enterprise users being unable到retry在rate limit (429) errors
- 修复`会话End` hooks not firing当using interactive `/resume`到switch sessions
- 改进startup memory usage通过~18MB across所有scenarios
- 改进non-streaming API fallback使用2-minute per-attempt timeout, preventing sessions从hanging indefinitely
- `CLAUDE_CODE_PLUGIN_SEED_DIR`现在supports multiple seed directories separated通过platform path delimiter (`:`在Unix, `;`在Windows)
- [VSCode] Added `/remote-control` — bridge您的session到claude.ai/code到continue从browser或phone
- [VSCode] 会话 tabs现在get AI-generated titles based在your第一message
- [VSCode] 修复了thinking pill showing "Thinking" instead的"Thought用于Ns"之后response completes
- [VSCode] 修复ed missing session diff button当opening sessions从left sidebar

## 2.1.78

- 添加`停止失败` hook event那fires当turn ends due到API错误(rate limit, auth failure, etc.)
- 添加`${CLAUDE_PLUGIN_DATA}` variable用于plugin持久state那survives plugin updates; `/plugin uninstall` prompts之前deleting it
- 添加`effort`, `maxTurns`,和`disallowedTools` frontmatter support用于plugin-shipped agents
- Terminal notifications (iTerm2/Kitty/Ghostty popups, progress bar)现在reach outer terminal当running inside tmux使用`set -g allow-passthrough on`
- 响应 text现在streams line-by-line作为it's generated
- 修复`git log HEAD` failing使用"ambiguous argument" inside sandboxed Bash在Linux,和stub files polluting `git status`在working directory
- 修复`cc log`和`--resume` silently truncating conversation history在large sessions (>5 MB)那used subagents
- 修复infinite loop当API errors triggered stop hooks那re-fed blocking errors到model
- 修复`deny: ["mcp__servername"]` permission rules not removing MCP server tools之前sending到model, allowing it到see和attempt阻止tools
- 修复`sandbox.filesystem.allow写入` not working使用absolute paths (previously必需`//` prefix)
- 修复`/sandbox` Dependencies tab showing Linux prerequisites在macOS instead的macOS-specific info
- **安全：** 修复了 silent sandbox disable当`sandbox.enabled: true`是set but dependencies是missing —现在shows可见startup warning
- 修复`.git`, `.claude`,和other protected directories being writable without prompt在`bypassPermissions` mode
- 修复ctrl+u在normal mode scrolling instead的readline kill-line (ctrl+u/ctrl+d half-page scroll moved到transcript mode only)
- 修复voice mode modifier-combo push-to-talk keybindings (e.g. ctrl+k) requiring hold instead的activating immediately
- 修复voice mode not working在WSL2使用WSLg (Windows 11); WSL1/Win10 users现在get clear error
- 修复`--worktree` flag not loading skills和hooks从worktree directory
- 修复`CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS`和`includeGitInstructions` setting not suppressing git status section在system prompt
- 修复Bash tool not finding Homebrew和other PATH-dependent binaries当VS Code是launched从Dock/Spotlight
- 修复washed-out Claude orange color在VS Code/Cursor/code-server terminals那don't advertise truecolor support
- 添加`ANTHROPIC_CUSTOM_MODEL_OPTION` env var到add自定义entry到`/model` picker,使用optional `_NAME`和`_DESCRIPTION` suffixed vars用于display
- 修复`ANTHROPIC_BETAS` environment variable being silently ignored当using Haiku models
- 修复queued prompts being concatenated without newline separator
- 改进memory usage和startup time当resuming large sessions
- [VSCode] 修复ed简短flash的login screen当opening sidebar当already authenticated
- [VSCode] 修复ed "API 错误: Rate limit reached"当selecting Opus — model dropdown不longer offers 1M context variant到subscribers谁的plan tier是unknown

## 2.1.77

- 提高了default maximum output token limits用于Claude Opus 4.6到64k tokens,和upper bound用于Opus 4.6和Sonnet 4.6 models到128k tokens
- 添加`allow读取` sandbox filesystem setting到re-allow read access within `deny读取` regions
- `/copy`现在accepts可选index: `/copy N` copies Nth-latest assistant response
- 修复"Always 允许"在compound bash commands (e.g. `cd src && npm test`) saving single rule用于full string instead的per-subcommand, leading到dead rules和repeated permission prompts
- 修复auto-updater starting overlapping binary downloads当slash-command overlay repeatedly opened和closed, accumulating tens的gigabytes的memory
- 修复`--resume` silently truncating最近conversation history due到race between memory-extraction writes和main transcript
- 修复PreToolUse hooks returning `"allow"` bypassing `deny` permission rules, including enterprise managed settings
- 修复写入 tool silently converting line endings当overwriting CRLF files或creating files在CRLF directories
- 修复memory growth在long-running sessions从progress messages surviving compaction
- 修复cost和token usage not being tracked当API falls back到non-streaming mode
- 修复`CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` not stripping beta tool-schema fields, causing proxy gateways到reject requests
- 修复Bash tool reporting errors用于successful commands当system temp directory path contains spaces
- 修复paste being lost当typing immediately之后pasting
- 修复Ctrl+D在`/feedback` text input deleting forward instead的second press exiting session
- 修复API error当dragging 0-byte image file into prompt
- 修复Claude Desktop sessions incorrectly using terminal CLI's配置API key instead的OAuth
- 修复`git-subdir` plugins在different subdirectories的same monorepo commit colliding在plugin cache
- 修复ordered list numbers not rendering在terminal UI
- 修复a race condition哪里stale-worktree cleanup可以delete agent worktree刚刚resumed从previous crash
- 修复input deadlock当opening `/mcp`或similar dialogs当agent是running
- 修复Backspace和删除 keys not working在vim NORMAL mode
- 修复status line not updating当vim mode是toggled on或off
- 修复hyperlinks opening twice在Cmd+click在VS Code, Cursor,和other xterm.js-based terminals
- 修复background colors rendering作为terminal-default inside tmux使用default configuration
- 修复iTerm2 session crash当selecting text inside tmux over SSH
- 修复clipboard copy silently failing在tmux sessions; copy toast现在indicates whether到paste使用`⌘V`或tmux `prefix+]`
- 修复`←`/`→` accidentally switching tabs在settings, permissions,和sandbox dialogs当navigating lists
- 修复IDE integration not auto-connecting当Claude Code是launched inside tmux或screen
- 修复CJK characters visually bleeding into adjacent UI elements当clipped在right edge
- 修复teammate panes not closing当leader exits
- 修复iTerm2 auto mode not detecting iTerm2用于native split-pane teammates
- Faster startup在macOS (~60ms)通过reading keychain credentials在parallel使用module loading
- Faster `--resume`在fork-heavy和very large sessions — up到45% faster loading和~100-150MB更少peak memory
- 改进Esc到abort in-flight non-streaming API requests
- 改进`claude plugin validate`到check skill, agent,和command frontmatter plus `hooks/hooks.json`, catching YAML parse errors和schema violations
- Background bash tasks是now killed如果output exceeds 5GB, preventing runaway processes从filling disk
- 会话s是now auto-named从plan content当you accept plan
- 改进headless mode plugin installation到compose correctly使用`CLAUDE_CODE_PLUGIN_SEED_DIR`
- Show notice当`apiKeyHelper` takes longer than 10s, preventing it从blocking主要loop
- The 智能体 tool不longer accepts `resume` parameter — use `Send消息({to: agentId})`到continue previously spawned agent
- `Send消息`现在auto-resumes停止agents在background instead的returning error
- 重命名d `/fork`到`/branch` (`/fork`仍然works作为alias)
- [VSCode] Improved plan preview tab titles到use plan's heading instead的"Claude's Plan"
- [VSCode] When option+click doesn't trigger native selection在macOS, footer现在points到`mac选项点击Forces选择ion` setting

## 2.1.76

- 添加MCP elicitation support — MCP servers可以now request structured input mid-task via interactive dialog (form fields或browser URL)
- 添加new `Elicitation`和`ElicitationResult` hooks到intercept和override responses之前they're sent back
- 添加`-n` / `--name <name>` CLI flag到set display name用于session在startup
- 添加`worktree.sparse路径s` setting用于`claude --worktree`在large monorepos到check out仅directories您need via git sparse-checkout
- 添加`PostCompact` hook那fires之后compaction completes
- 添加`/effort` slash command到set model effort level
- 添加session quality survey — enterprise admins可以configure sample rate via `feedbackSurveyRate` setting
- 修复deferred tools (loaded via `Tool搜索`) losing它们的input schemas之后conversation compaction, causing array和number parameters到be rejected使用type errors
- 修复slash commands showing "Unknown skill"
- 修复plan mode asking用于re-approval之后plan是already accepted
- 修复voice mode swallowing keypresses当permission dialog或plan editor是open
- 修复`/voice` not working在Windows当installed via npm
- 修复spurious "上下文 limit reached"当invoking skill使用`model:` frontmatter在1M-context session
- 修复"adaptive thinking是not supported在this model" error当using non-standard model strings
- 修复`Bash(cmd:*)` permission rules not matching当quoted argument contains `#`
- 修复"don't ask again"在Bash permission dialog showing full raw command用于pipes和compound commands
- 修复auto-compaction retrying indefinitely之后consecutive failures — circuit breaker现在stops之后3 attempts
- 修复MCP reconnect spinner persisting之后successful reconnection
- 修复LSP plugins not registering servers当LSP Manager initialized之前marketplaces是reconciled
- 修复clipboard copying在tmux over SSH —现在attempts两者direct terminal write和tmux clipboard integration
- 修复`/export` showing仅filename instead的full file path在success message
- 修复transcript not auto-scrolling到new messages之后selecting text
- 修复Escape key not working到exit login method selection screen
- 修复several Remote Control issues: sessions silently dying当server reaps idle environment,快速messages being queued one-at-a-time instead的batched,和stale work items causing redelivery之后JWT refresh
- 修复bridge sessions failing到recover之后extended WebSocket disconnects
- 修复slash commands not found当typing exact name的soft-hidden command
- 改进`--worktree` startup performance通过reading git refs directly和skipping redundant `git fetch`当remote branch是already可用locally
- 改进background agent behavior — killing后台agent现在preserves它的partial results在conversation context
- 改进model fallback notifications —现在always可见instead的hidden behind详细mode,使用human-friendly model names
- 改进blockquote readability在dark terminal themes — text是now italic使用left bar instead的dim
- 改进stale worktree cleanup — worktrees left behind之后interrupted parallel run是now automatically cleaned up
- 改进Remote Control session titles —现在derived从your第一prompt instead的showing "Interactive session"
- 改进`/voice`到show您的dictation language在enable和warn当your `language` setting isn't supported用于voice input
- 更新d `--plugin-dir`到only accept one path到support subcommands — use repeated `--plugin-dir`用于multiple directories
- [VSCode] 修复ed gitignore patterns containing commas silently excluding entire filetypes从@-mention file picker

## 2.1.75

- 添加1M context window用于Opus 4.6通过default用于Max, 团队,和输入prise plans (previously必需extra usage)
- 添加`/color` command用于all users到set prompt-bar color用于your session
- 添加session name display在prompt bar当using `/rename`
- 添加last-modified timestamps到memory files, helping Claude reason about哪个memories是fresh vs. stale
- 添加hook source display (settings/plugin/skill)在permission prompts当hook requires confirmation
- 修复voice mode not activating correctly在fresh installs without toggling `/voice` twice
- 修复the Claude Code header not updating displayed model name之后switching models使用`/model`或选项+P
- 修复session crash当attachment message computation returns undefined values
- 修复Bash tool mangling `!`在piped commands (e.g., `jq 'select(.x != .y)'`现在works correctly)
- 修复managed-disabled plugins showing up在`/plugin` 安装ed tab — plugins force-disabled通过your organization是now hidden
- 修复token estimation over-counting用于thinking和`tool_use` blocks, preventing premature context compaction
- 修复corrupted marketplace config path handling
- 修复`/resume` losing session names之后resuming forked或continued session
- 修复Esc not closing `/status` dialog之后visiting Config tab
- 修复input handling当accepting或rejecting plan
- 修复footer hint在agent teams showing "↓到expand" instead的correct "shift + ↓到expand"
- 改进startup performance在macOS non-MDM machines通过skipping unnecessary subprocess spawns
- Suppressed async hook completion messages通过default (visible使用`--verbose`或transcript mode)
- 破坏性变更： 移除了已弃用 Windows managed settings fallback在`C:\ProgramData\ClaudeCode\managed-settings.json` — use `C:\Program 文件s\ClaudeCode\managed-settings.json`

## 2.1.74

- 添加actionable suggestions到`/context` command — identifies context-heavy tools, memory bloat,和capacity warnings使用specific optimization tips
- 添加`autoMemory目录` setting到configure自定义directory用于auto-memory storage
- 修复memory leak哪里streaming API response buffers是not released当generator是terminated early, causing unbounded RSS growth在否de.js/npm code path
- 修复managed policy `ask` rules being bypassed通过user `allow` rules或skill `allowed-tools`
- 修复full model IDs (e.g., `claude-opus-4-5`) being silently ignored在agent frontmatter `model:` field和`--agents` JSON config — agents现在accept相同model values作为`--model`
- 修复MCP OAuth authentication hanging当callback port是already在use
- 修复MCP OAuth refresh never prompting用于re-auth之后refresh token expires,用于OAuth servers那return errors使用HTTP 200 (e.g. Slack)
- 修复voice mode silently failing在macOS native binary用于users谁的terminal有never been granted microphone permission — binary现在includes `audio-input` entitlement所以macOS prompts correctly
- 修复`会话End` hooks being killed之后1.5 s在exit regardless的`hook.timeout` —现在configurable via `CLAUDE_CODE_SESSIONEND_HO确定S_TIMEOUT_MS`
- 修复`/plugin install` failing inside REPL用于marketplace plugins使用local sources
- 修复marketplace update not syncing git submodules — plugin sources在submodules不longer break之后update
- 修复unknown slash commands使用arguments silently dropping input —现在shows您的input作为warning
- 修复Hebrew, Arabic,和other RTL text not rendering correctly在Windows Terminal, conhost,和VS Code integrated terminal
- 修复LSP servers not working在Windows due到malformed file URIs
- 更改`--plugin-dir`所以local dev copies现在override安装marketplace plugins使用same name (unless那plugin是force-enabled通过managed settings)
- [VSCode] 修复ed delete button not working用于Untitled sessions
- [VSCode] Improved scroll wheel responsiveness在integrated terminal使用terminal-aware acceleration

## 2.1.73

- 添加`modelOverrides` setting到map model picker entries到custom provider model IDs (e.g. Bedrock inference profile ARNs)
- 添加actionable guidance当OAuth login或connectivity checks fail due到SSL certificate errors (corporate proxies, `NODE_EXTRA_CA_CERTS`)
- 修复freezes和100% CPU loops triggered通过permission prompts用于complex bash commands
- 修复a deadlock那could freeze Claude Code当many skill files changed在once (e.g.在`git pull`在repo使用large `.claude/skills/` directory)
- 修复Bash tool output being lost当running multiple Claude Code sessions在same project directory
- 修复subagents使用`model: opus`/`sonnet`/`haiku` being silently downgraded到older model versions在Bedrock, Vertex,和Microsoft Foundry
- 修复background bash processes spawned通过subagents not being cleaned up当agent exits
- 修复`/resume` showing当前session在picker
- 修复`/ide` crashing使用`on安装是not defined`当auto-installing extension
- 修复`/loop` not being available在Bedrock/Vertex/Foundry和when telemetry是disabled
- 修复会话启动 hooks firing twice当resuming session via `--resume`或`--continue`
- 修复JSON-output hooks injecting no-op system-reminder messages into model's context在every turn
- 修复voice mode session corruption当slow connection overlaps新recording
- 修复Linux sandbox failing到start使用"ripgrep (rg) not found"在native builds
- 修复Linux native modules not loading在Amazon Linux 2和other glibc 2.26 systems
- 修复"media_type: Field required" API error当receiving images via Remote Control
- 修复`/heapdump` failing在Windows使用`EEXIST` error当Desktop folder已经exists
- 改进Up arrow之后interrupting Claude —现在restores中断prompt和rewinds conversation在one step
- 改进IDE detection speed在startup
- 改进clipboard image pasting performance在macOS
- 改进`/effort`到work当Claude是responding, matching `/model` behavior
- 改进voice mode到automatically retry transient connection failures在rapid push-to-talk re-press
- 改进the Remote Control spawn mode selection prompt使用better context
- 更改default Opus model在Bedrock, Vertex,和Microsoft Foundry到Opus 4.6 (was Opus 4.1)
- 弃用`/output-style` command — use `/config` instead. Output style是now fixed在session start用于better prompt caching
- VSCode: 修复ed HTTP 400 errors用于users behind proxies或on Bedrock/Vertex使用Claude 4.5 models

## 2.1.72

- 修复tool search到activate even使用`ANTHROPIC_BASE_URL`作为long作为`ENABLE_TOOL_SEARCH`是set.
- 添加`w` key在`/copy`到write focused selection directly到file, bypassing clipboard (useful over SSH)
- 添加optional description argument到`/plan` (e.g., `/plan fix auth bug`)那enters plan mode和immediately starts
- 添加`ExitWorktree` tool到leave `输入Worktree` session
- 添加`CLAUDE_CODE_DISABLE_CRON` environment variable到immediately stop scheduled cron jobs mid-session
- 添加`lsof`, `pgrep`, `tput`, `ss`, `fd`,和`fdfind`到bash auto-approval allowlist, reducing permission prompts用于common read-only operations
- 恢复d `model` parameter在智能体 tool用于per-invocation model overrides
- 简化了effort levels到low/medium/high (removed max)使用new symbols (○ ◐ ●)和brief notification instead的persistent icon. Use `/effort auto`到reset到default
- 改进`/config` — Escape现在cancels changes, 输入 saves和closes, Space toggles settings
- 改进up-arrow history到show当前session's messages first当running multiple concurrent sessions
- 改进voice input transcription accuracy用于repo names和common dev terms (regex, OAuth, JSON)
- 改进bash command parsing通过switching到native module — faster initialization和no memory leak
- 减少了bundle size通过~510 KB
- 更改CLAUDE.md HTML comments (`<!-- ... -->`)到be hidden从Claude当auto-injected. Comments remain visible当read使用读取 tool
- 修复slow exits当background tasks或hooks是slow到respond
- 修复agent task progress stuck在"初始化中…"
- 修复skill hooks firing twice per event当hooks-enabled skill是invoked通过model
- 修复several voice mode issues:偶尔input lag,假"否 speech detected" errors之后releasing push-to-talk,和stale transcripts re-filling prompt之后submission
- 修复`--continue` not resuming从most最近point之后`--compact`
- 修复bash security parsing edge cases
- 添加support用于marketplace git URLs without `.git` suffix (Azure DevOps, AWS Code提交)
- 改进marketplace clone失败messages到show diagnostic信息even当git produces不stderr
- 修复several plugin issues: installation failing在Windows使用`EEXIST` error在开eDrive folders, marketplace blocking user-scope installs当project-scope install exists, `CLAUDE_CODE_PLUGIN_CACHE_DIR` creating literal `~` directories,和`plugin.json`使用marketplace-only fields failing到load
- 修复feedback survey appearing也frequently在long sessions
- 修复`--effort` CLI flag being reset通过unrelated settings writes在startup
- 修复backgrounded Ctrl+B queries losing它们的transcript或corrupting新conversation之后`/clear`
- 修复`/clear` killing后台agent/bash tasks —仅foreground tasks是now cleared
- 修复worktree isolation issues: Task tool resume not restoring cwd,和background task notifications missing `worktree路径`和`worktree分支`
- 修复`/model` not displaying results当run当Claude是working
- 修复digit keys selecting menu options instead的typing在plan mode permission prompt's text input
- 修复sandbox permission issues: certain file write operations incorrectly允许without prompting,和output redirections到allowlisted directories (like `/tmp/claude/`) prompting unnecessarily
- 改进CPU utilization在long sessions
- 修复prompt cache invalidation在SDK `query()` calls, reducing input token costs up到12x
- 修复Escape key becoming unresponsive之后cancelling query
- 修复double Ctrl+C not exiting当background agents或tasks是running
- 修复team agents到inherit leader's model
- 修复"Always 允许" saving permission rules那never match again
- 修复several hooks issues: `transcript_path` pointing到wrong directory用于resumed/forked sessions, agent `prompt` being silently deleted从settings.json在every settings write, PostToolUse block reason displaying twice, async hooks not receiving stdin使用bash `read -r`,和validation错误message showing example那fails validation
- 修复session crashes在Desktop/SDK当读取 returned files containing U+2028/U+2029 characters
- 修复terminal title being cleared在exit even当`CLAUDE_CODE_DISABLE_TERMINAL_TITLE`是set
- 修复several permission rule matching issues: wildcard rules not matching commands使用heredocs, embedded newlines,或no arguments; `sandbox.excludedCommands` failing使用env var prefixes; "always allow" suggesting overly broad prefixes用于nested CLI tools;和deny rules not applying到all command forms
- 修复oversized和truncated images从Bash data-URL output
- 修复a crash当resuming sessions那contained Bedrock API errors
- 修复intermittent "expected boolean, received string" validation errors在编辑, Bash,和Grep tool inputs
- 修复multi-line session titles当forking从conversation谁的first message contained newlines
- 修复queued messages not showing attached images,和images being lost当pressing ↑到edit queued message
- 修复parallel tool calls哪里failed 读取/Web获取/Glob将cancel它的siblings —仅Bash errors现在cascade
- VSCode: 修复ed scroll speed在integrated terminals not matching native terminals
- VSCode: 修复ed Shift+输入 submitting input instead的inserting newline用于users使用older keybindings
- VSCode: Added effort level indicator在input border
- VSCode: Added `vscode://anthropic.claude-code/open` URI handler到open新Claude Code tab programmatically,使用optional `prompt`和`session` query parameters

## 2.1.71

- 添加`/loop` command到run prompt或slash command在recurring interval (e.g. `/loop 5m check deploy`)
- 添加cron scheduling tools用于recurring prompts within session
- 添加`voice:pushToTalk` keybinding到make voice activation key rebindable在`keybindings.json` (default: space) — modifier+letter combos喜欢`meta+k`有zero typing interference
- 添加`fmt`, `comm`, `cmp`, `numfmt`, `expr`, `test`, `printf`, `getconf`, `seq`, `tsort`,和`pr`到bash auto-approval allowlist
- 修复stdin freeze在long-running sessions哪里keystrokes stop being processed but process stays alive
- 修复a 5–8第二startup freeze用于users使用voice mode enabled, caused通过CoreAudio initialization blocking主要thread之后system wake
- 修复startup UI freeze当many claude.ai proxy connectors refresh过期OAuth token simultaneously
- 修复forked conversations (`/fork`) sharing相同plan file,哪个caused plan edits在one fork到overwrite other
- 修复the 读取 tool putting oversized images into context当image processing failed, breaking subsequent turns在long image-heavy sessions
- 修复false-positive permission prompts用于compound bash commands containing heredoc commit messages
- 修复plugin installations being lost当running multiple Claude Code instances
- 修复claude.ai connectors failing到reconnect之后OAuth token refresh
- 修复claude.ai MCP connector startup notifications appearing用于every org-configured connector instead的only previously已连接ones
- 修复background agent completion notifications missing output file path,哪个made它difficult用于parent agents到recover agent results之后context compaction
- 修复duplicate output在Bash tool错误messages当commands exit使用non-zero status
- 修复Chrome extension auto-detection getting permanently stuck在"not installed"之后running在machine without本地Chrome
- 修复`/plugin marketplace update` failing使用merge conflicts当marketplace是pinned到branch/tag ref
- 修复`/plugin marketplace add owner/repo@ref` incorrectly parsing `@` — previously仅`#` worked作为ref separator, causing undiagnosable errors使用`strictKnownMarketplaces`
- 修复duplicate entries在`/permissions` 工作区 tab当same directory是added with和without trailing slash
- 修复`--print` hanging forever当team agents是configured — exit loop不longer waits在long-lived `in_process_teammate` tasks
- 修复"❯ Tool loaded." appearing在REPL之后every `Tool搜索` call
- 修复prompting用于`cd <cwd> && git ...`在Windows当model uses mingw-style path
- 改进startup time通过deferring native image processor loading到first use
- 改进bridge session reconnection到complete within seconds之后laptop wake从sleep, instead的waiting up到10 minutes
- 改进`/plugin uninstall`到disable project-scoped plugins在`.claude/settings.local.json` instead的modifying `.claude/settings.json`,所以changes don't affect teammates
- 改进plugin-provided MCP server deduplication — servers那duplicate manually-configured server (same command/URL)是now skipped, preventing重复connections和tool sets. Suppressions是shown在`/plugin` menu.
- 更新d `/debug`到toggle调试logging在mid-session,自从debug logs是no longer written通过default
- 移除startup notification noise用于unauthenticated org-registered claude.ai connectors

## 2.1.70

- 修复API 400 errors当using `ANTHROPIC_BASE_URL`使用third-party gateway — tool search现在correctly detects proxy endpoints和disables `tool_reference` blocks
- 修复`API 错误: 400 This model does not support effort parameter`当using自定义Bedrock inference profiles或other model identifiers not matching标准Claude naming patterns
- 修复empty model responses immediately之后`Tool搜索` — server renders tool schemas使用system-prompt-style tags在prompt tail, which可以confuse models into stopping early
- 修复prompt-cache bust当MCP server使用`instructions` connects之后first turn
- 修复输入 inserting newline instead的submitting当typing over慢SSH connection
- 修复clipboard corrupting non-ASCII text (CJK, emoji)在Windows/WSL通过using PowerShell `Set-Clipboard`
- 修复extra VS Code windows opening在startup在Windows当running从VS Code integrated terminal
- 修复voice mode failing在Windows native binary使用"native audio module可以not be loaded"
- 修复push-to-talk not activating在session start当`voice启用d: true`是set在settings
- 修复markdown links containing `#NNN` references incorrectly pointing到current repository instead的linked URL
- 修复repeated "模型 updated到Opus 4.6" notification当project's `.claude/settings.json`有legacy Opus model string pinned
- 修复plugins showing作为inaccurately installed在`/plugin`
- 修复plugins showing "not found在marketplace" errors在fresh startup通过auto-refreshing之后marketplace installation
- 修复`/security-review` command failing使用`unknown option merge-base`在older git versions
- 修复`/color` command having不way到reset back到default color — `/color default`, `/color gray`, `/color reset`,和`/color none`现在restore default
- 修复a performance regression在`AskUserQuestion` preview dialog那re-ran markdown rendering在every keystroke在notes input
- 修复feature flags read在early startup never refreshing它们的disk cache, causing stale values到persist across sessions
- 修复`permissions.default模式` settings values其他than `accept编辑s`或`plan` being applied在Claude Code Remote environments — they是now ignored
- 修复skill listing being re-injected在every `--resume` (~600 tokens saved per resume)
- 修复teleport marker not rendering在VS Code teleported sessions
- 改进error message当microphone captures silence到distinguish从"no speech detected"
- 改进compaction到preserve images在summarizer request, allowing prompt cache reuse用于faster和cheaper compaction
- 改进`/rename`到work当Claude是processing, instead的being silently queued
- 减少了prompt input re-renders在turns通过~74%
- 减少了startup memory通过~426KB用于users without自定义CA certificates
- 减少了Remote Control `/poll` rate到once per 10 minutes当connected (was 1–2s), cutting server load ~300×. Reconnection是unaffected — transport loss immediately wakes快速polling.
- [VSCode] Added spark icon在VS Code activity bar那lists所有Claude Code sessions,使用sessions opening作为full editors
- [VSCode] Added full markdown document view用于plans在VS Code,使用support用于adding comments到provide feedback
- [VSCode] Added native MCP server management dialog — use `/mcp`在chat panel到enable/disable servers, reconnect,和manage OAuth authentication without switching到terminal

## 2.1.69

- 添加the `/claude-api` skill用于building applications使用Claude API和Anthropic SDK
- 添加Ctrl+U在empty bash prompt (`!`)到exit bash mode, matching `escape`和`backspace`
- 添加numeric keypad support用于selecting options在Claude's interview questions (previously仅number row above QWERTY worked)
- 添加optional name argument到`/remote-control`和`claude remote-control` (`/remote-control My Project`或`--name "My Project"`)到set自定义session title visible在claude.ai/code
- 添加Voice STT support用于10新languages (20 total) — Russian, Polish, Turkish, Dutch, Ukrainian, Greek, Czech, Danish, Swedish, 否rwegian
- 添加effort level display (e.g., "with low effort")到logo和spinner, making它easier到see哪个effort setting是active
- 添加agent name display在terminal title当using `claude --agent`
- 添加`sandbox.enableWeakerNetworkIsolation` setting (macOS only)到allow Go programs喜欢`gh`, `gcloud`,和`terraform`到verify TLS certificates当using自定义MITM proxy使用`httpProxyPort`
- 添加`includeGitInstructions` setting (and `CLAUDE_CODE_DISABLE_GIT_INSTRUCTIONS` env var)到remove built-in commit和PR workflow instructions从Claude's system prompt
- 添加`/reload-plugins` command到activate pending plugin changes without restarting
- 添加a one-time startup prompt suggesting Claude Code Desktop在macOS和Windows (max 3 showings, dismissible)
- 添加`${CLAUDE_SKILL_DIR}` variable用于skills到reference它们的own directory在SKILL.md content
- 添加`InstructionsLoaded` hook event那fires当CLAUDE.md或`.claude/rules/*.md` files是loaded into context
- 添加`agent_id` (for subagents)和`agent_type` (for subagents和`--agent`)到hook events
- 添加`worktree` field到status line hook commands使用name, path, branch,和original repo directory当running在`--worktree` session
- 添加`pluginTrust消息`在managed settings到append organization-specific context到plugin trust警告shown之前installation
- 添加policy limit fetching (e.g.,远程control restrictions)用于团队 plan OAuth users, not刚刚输入prise
- 添加`pathPattern`到`strictKnownMarketplaces`用于regex-matching file/directory marketplace sources alongside `hostPattern` restrictions
- 添加plugin source type `git-subdir`到point到subdirectory within git repo
- 添加`oauth.authServerMetadataUrl` config option用于MCP servers到specify自定义OAuth metadata discovery URL当standard discovery fails
- 修复a security issue哪里nested skill discovery可以load skills从gitignored directories喜欢`node_modules`
- 修复trust dialog silently enabling所有`.mcp.json` servers在first run. You'll现在see per-server approval dialog作为expected
- 修复`claude remote-control` crashing immediately在npm installs使用"bad option: --sdk-url" (anthropics/claude-code#28334)
- 修复`--model claude-opus-4-0`和`--model claude-opus-4-1` resolving到deprecated Opus versions instead的current
- 修复macOS keychain corruption当using multiple OAuth MCP servers. Large OAuth metadata blobs可以overflow `security -i` stdin buffer, silently leaving stale credentials behind和causing repeated `/login` prompts.
- 修复`.credentials.json` losing `subscription输入` (showing "Claude API" instead的"Claude Pro"/"Claude Max")当profile endpoint transiently fails在token refresh (anthropics/claude-code#30185)
- 修复ghost dotfiles (`.bashrc`, `HEAD`, etc.) appearing作为untracked files在working directory之后sandboxed Bash commands在Linux
- 修复Shift+输入 printing `[27;2;13~` instead的inserting newline在Ghostty over SSH
- 修复stash (Ctrl+S) being cleared当submitting message当Claude是working
- 修复ctrl+o (transcript toggle) freezing用于many seconds在long sessions使用lots的file edits
- 修复plan mode feedback input not supporting multi-line text entry (backslash+输入和Shift+输入现在insert newlines)
- 修复cursor not moving down into blank lines在top的input box
- 修复`/stats` crash当transcript files contain entries使用missing或malformed timestamps
- 修复a简短hang之后streaming error在long sessions (the transcript是being fully rewritten到drop one line; it是now truncated在place)
- 修复`--setting-sources user` not blocking dynamically discovered project skills
- 修复duplicate CLAUDE.md, slash commands, agents,和rules当running从worktree nested inside它的main repo (e.g. `claude -w`)
- 修复plugin 停止/会话End/etc hooks not firing之后any `/plugin` operation
- 修复plugin hooks being silently dropped当two plugins use相同`${CLAUDE_PLUGIN_ROOT}/...` command template
- 修复memory leak在long-running SDK/CCR sessions哪里conversation messages是retained unnecessarily
- 修复API 400 errors在forked agents (autocompact, summarization)当resuming sessions that是interrupted mid-tool-batch
- 修复"unexpected tool_use_id found在tool_result blocks" error当resuming conversations那start使用orphaned tool result
- 修复teammates accidentally spawning nested teammates via 智能体 tool's `name` parameter
- 修复`CLAUDE_CODE_MAX_OUTPUT_T确定ENS` being ignored在conversation compaction
- 修复`/compact` summary rendering作为user bubble在SDK consumers (Claude Code Remote web UI, VSCode extension)
- 修复voice space bar getting stuck之后failed voice activation (module loading race, cold GrowthBook)
- 修复worktree file copy在Windows
- 修复global `.claude` folder detection在Windows
- 修复symlink bypass哪里writing新files through symlinked parent directory可以escape工作directory在`accept编辑s` mode
- 修复sandbox prompting users到approve non-allowed domains当`allowManagedDomains开ly`是enabled在managed settings — non-allowed domains是now阻止automatically使用no bypass
- 修复interactive tools (e.g., `AskUserQuestion`) being silently auto-allowed当listed在skill's allowed-tools, bypassing permission prompt和running使用empty answers
- 修复multi-GB memory spike当committing使用large untracked binary files在working tree
- 修复Escape not interrupting运行turn当input box有draft text. Use Up arrow到pull queued messages back用于editing,或Ctrl+U到clear input line.
- 修复Android app crash当running本地slash commands (`/voice`, `/cost`)在Remote Control sessions
- 修复a memory leak哪里old message array versions accumulated在React Compiler `memo缓存` over长sessions
- 修复a memory leak哪里REPL render scopes accumulated over长sessions (~35MB over 1000 turns)
- 修复memory retention在in-process teammates哪里parent's full conversation history是pinned用于teammate's lifetime, preventing GC之后`/clear`或auto-compact
- 修复a memory leak在interactive mode哪里hook events可以accumulate unboundedly在long sessions
- 修复hang当`--mcp-config` points到corrupted file
- 修复slow startup当many skills/plugins是installed
- 修复`cd <outside-dir> && <cmd>` permission prompt到surface chained command instead的only showing "是, allow reading从<dir>/"
- 修复conditional `.claude/rules/*.md` files (with `paths:` frontmatter)和nested CLAUDE.md files not loading在print mode (`claude -p`)
- 修复`/clear` not fully clearing所有session caches, reducing memory retention在long sessions
- 修复terminal flicker caused通过animated elements在scrollback boundary
- 修复UI frame drops在macOS当using MCP servers使用OAuth (regression从2.1.x)
- 修复occasional frame stalls在typing caused通过synchronous调试log flushes
- 修复`团队mateIdle`和`Task已完成` hooks到support `{"continue": false, "stopReason": "..."}`到stop teammate, matching `停止` hook behavior
- 修复`Worktree创建`和`WorktreeRemove` plugin hooks being silently ignored
- 修复skill descriptions使用colons (e.g., "Triggers include: X, Y, Z") failing到load从SKILL.md frontmatter
- 修复project skills without `description:` frontmatter field not appearing在Claude's可用skills list
- 修复`/context` showing相同token counts用于all MCP tools从server
- 修复literal `nul` file creation在Windows当model uses CMD-style `2>nul` redirection在Git Bash
- 修复extra blank lines appearing below每个tool call在expanded subagent transcript view (Ctrl+O)
- 修复Tab/arrow keys not cycling Settings tabs当`/config` search box是focused but empty
- 修复service key OAuth sessions (CCR containers) spamming `[ERROR]` logs使用403s从profile-scoped endpoints
- 修复inconsistent color用于"Remote Control active" status indicator
- 修复Voice waveform cursor covering第一suffix letter当dictating mid-input
- 修复Voice input showing所有5 spaces在warmup instead的capping在~2 (aligning使用"keep holding…" hint)
- 改进spinner performance通过isolating 50ms animation loop从surrounding shell, reducing render和CPU overhead在turns
- 改进UI rendering performance在native binaries使用React Compiler
- 改进`--worktree` startup通过eliminating git subprocess在startup path
- 改进macOS startup通过eliminating redundant settings-file reloads当managed settings resolve
- 改进macOS startup用于Claude.ai enterprise/team users通过skipping unnecessary keychain lookup
- 改进MCP `-p` startup通过pipelining claude.ai config fetch使用local connections和using concurrency pool instead的sequential batching
- 改进voice startup通过removing imperceptible warmup pulse animations that是causing re-render stutter
- 改进MCP binary content handling: tools returning PDFs, 关ice documents,或audio现在save decoded bytes到disk使用correct file extension instead的dumping raw base64 into conversation context. Web获取也saves binary responses alongside它的summary.
- 改进memory usage在long sessions通过stabilizing `on提交` across message updates
- 改进LSP tool rendering和memory context building到no longer read entire files
- 改进session upload和memory sync到avoid reading large files into memory之前size/binary checks
- 改进file operation performance通过avoiding reading file contents用于existence checks (6 sites)
- 改进documentation到clarify那`--append-system-prompt-file`和`--system-prompt-file` work在interactive mode (the docs previously said print mode only)
- 减少了baseline memory通过~16MB通过deferring Yoga WASM preloading
- 减少了memory footprint用于SDK和CCR sessions using stream-json output
- 减少了memory usage当resuming large sessions (including compacted history)
- 减少了token usage在multi-agent tasks使用more concise subagent final reports
- 更改Sonnet 4.5 users在Pro/Max/团队 Premium到be automatically migrated到Sonnet 4.6
- 更改the `/resume` picker到show您的most最近prompt instead的first one. This也resolves一些titles appearing作为`(session)`.
- 更改claude.ai MCP connector failures到show notification instead的silently disappearing从tool list
- 更改example command suggestions到be generated deterministically instead的calling Haiku
- 更改resuming之后compaction到no longer produce preamble recap之前continuing
- [SDK] Changed task creation到no longer require `activeForm` field — spinner falls back到task subject
- [VSCode] Added compaction display作为collapsible "Compacted chat" card使用summary inside
- [VSCode] The permission mode picker现在respects `permissions.disableBypassPermissions模式`从your effective Claude Code settings (including managed/policy settings) —当set到`disable`, bypass permissions mode是hidden从picker
- [VSCode] 修复ed RTL text (Arabic, Hebrew, Persian) rendering reversed在chat panel (regression在v2.1.63)

## 2.1.68

- Opus 4.6现在defaults到medium effort用于Max和团队 subscribers. Medium effort works well用于most tasks — it's sweet spot between speed和thoroughness. You可以change这anytime使用`/model`
- Re-introduced "ultrathink" keyword到enable high effort用于next turn
- 移除Opus 4和4.1从Claude Code在first-party API — users使用these models pinned是automatically moved到Opus 4.6

## 2.1.66

- 减少了spurious错误logging

## 2.1.63

- 添加`/simplify`和`/batch` bundled slash commands
- 修复local slash command output喜欢/cost appearing作为user-sent messages instead的system messages在UI
- Project configs & auto memory现在shared across git worktrees的same repository
- 添加`ENABLE_CLAUDEAI_MCP_SERVERS=false` env var到opt out从making claude.ai MCP servers available
- 改进`/model` command到show currently活动model在slash command menu
- 添加HTTP hooks, which可以POST JSON到URL和receive JSON instead的running shell command
- 修复listener leak在bridge polling loop
- 修复listener leak在MCP OAuth flow cleanup
- 添加manual URL paste fallback在MCP OAuth authentication. If自动localhost redirect doesn't work,您can paste callback URL到complete authentication.
- 修复memory leak当navigating hooks configuration menu
- 修复listener leak在interactive permission handler在auto-approvals
- 修复file count cache ignoring glob ignore patterns
- 修复memory leak在bash command prefix cache
- 修复MCP tool/resource cache leak在server reconnect
- 修复IDE host IP detection cache incorrectly sharing results across ports
- 修复WebSocket listener leak在transport reconnect
- 修复memory leak在git root detection cache那could cause unbounded growth在long-running sessions
- 修复memory leak在JSON parsing cache那grew unbounded over长sessions
- VSCode: 修复ed远程sessions not appearing在conversation history
- 修复a race condition在REPL bridge哪里new messages可以arrive在server interleaved使用historical messages在initial connection flush, causing message ordering issues.
- 修复memory leak哪里long-running teammates retained所有messages在App状态 even之后conversation compaction
- 修复a memory leak哪里MCP server fetch caches是not cleared在disconnect, causing growing memory usage使用servers那reconnect frequently
- 改进memory usage在long sessions使用subagents通过stripping heavy progress message payloads在context compaction
- 添加"Always copy full response" option到`/copy` picker. When selected,未来`/copy` commands将skip code block picker和copy full response directly.
- VSCode: Added session rename和remove actions到sessions list
- 修复`/clear` not resetting cached skills, which可以cause stale skill content到persist在new conversation

## 2.1.62

- 修复prompt suggestion cache regression那reduced cache hit rates

## 2.1.61

- 修复concurrent writes corrupting config file在Windows

## 2.1.59

- Claude automatically saves useful context到auto-memory. Manage使用/memory
- 添加`/copy` command到show interactive picker当code blocks是present, allowing selection的individual code blocks或full response.
- 改进"always allow" prefix suggestions用于compound bash commands (e.g. `cd /tmp && git fetch && git push`)到compute smarter per-subcommand prefixes instead的treating whole command作为one
- 改进ordering的short task lists
- 改进memory usage在multi-agent sessions通过releasing完成subagent task state
- 修复MCP OAuth token refresh race condition当running multiple Claude Code instances simultaneously
- 修复shell commands not showing clear错误message当working directory有been deleted
- 修复config file corruption那could wipe authentication当multiple Claude Code instances ran simultaneously

## 2.1.58

- Expand Remote Control到more users

## 2.1.56

- VS Code: 修复ed另一个cause的"command 'claude-vscode.editor.openLast' not found" crashes

## 2.1.55

- 修复BashTool failing在Windows使用EINVAL error

## 2.1.53

- 修复a UI flicker哪里user input将briefly disappear之后submission之前message rendered
- 修复bulk agent kill (ctrl+f)到send single aggregate notification instead的one per agent, and到properly clear command queue
- 修复graceful shutdown sometimes leaving stale sessions当using Remote Control通过parallelizing teardown network calls
- 修复`--worktree` sometimes being ignored在first launch
- 修复a panic ("switch在corrupted value")在Windows
- 修复a crash那could occur当spawning很多processes在Windows
- 修复a crash在WebAssembly interpreter在Linux x64 & Windows x64
- 修复a crash那sometimes occurred之后2 minutes在Windows ARM64

## 2.1.52

- VS Code: 修复ed extension crash在Windows ("command 'claude-vscode.editor.openLast' not found")

## 2.1.51

- 添加`claude remote-control` subcommand用于external builds, enabling本地environment serving用于all users.
- 更新d plugin marketplace默认git timeout从30s到120s和added `CLAUDE_CODE_PLUGIN_GIT_TIMEOUT_MS`到configure.
- 添加support用于custom npm registries和specific version pinning当installing plugins从npm sources
- BashTool现在skips login shell (`-l` flag)通过default当shell snapshot是available, improving command execution performance. Previously这required setting `CLAUDE_BASH_NO_LOGIN=true`.
- 修复a security issue哪里`statusLine`和`fileSuggestion` hook commands可以execute without workspace trust acceptance在interactive mode.
- Tool results larger than 50K characters是now persisted到disk (previously 100K). This reduces context window usage和improves conversation longevity.
- 修复a bug哪里duplicate `control_response` messages (e.g.从WebSocket reconnects)可以cause API 400 errors通过pushing重复assistant messages into conversation.
- 添加`CLAUDE_CODE_ACCOUNT_UUID`, `CLAUDE_CODE_USER_EMAIL`,和`CLAUDE_CODE_ORGANIZATION_UUID` environment variables用于SDK callers到provide account信息synchronously, eliminating race condition哪里early telemetry events lacked account metadata.
- 修复slash command autocomplete crashing当plugin's SKILL.md description是YAML array或other non-string type
- The `/model` picker现在shows human-readable labels (e.g., "Sonnet 4.5") instead的raw model IDs用于pinned model versions,使用upgrade hint当newer version是available.
- Managed settings可以now be set via macOS plist或Windows Registry. Learn more在https://code.claude.com/docs/en/settings#settings-files

## 2.1.50

- 添加support用于`startup超时` configuration用于LSP servers
- 添加`Worktree创建`和`WorktreeRemove` hook events, enabling自定义VCS setup和teardown当agent worktree isolation creates或removes worktrees.
- 修复a bug哪里resumed sessions可以be invisible当working directory involved symlinks,因为session storage path是resolved在different times在startup. Also修复session data loss在SSH disconnect通过flushing session data之前hooks和analytics在graceful shutdown sequence.
- Linux: 修复ed native modules not loading在systems使用glibc更旧than 2.30 (e.g., RHEL 8)
- 修复memory leak在agent teams哪里completed teammate tasks是never garbage collected从session state
- 修复`CLAUDE_CODE_SIMPLE`到fully strip down skills, session memory,自定义agents,和CLAUDE.md token counting
- 修复`/mcp reconnect` freezing CLI当given server name那doesn't exist
- 修复memory leak哪里completed task state objects是never removed从App状态
- 添加support用于`isolation: worktree`在agent definitions, allowing agents到declaratively run在isolated git worktrees.
- `CLAUDE_CODE_SIMPLE` mode现在also disables MCP tools, attachments, hooks,和CLAUDE.md file loading用于fully minimal experience.
- 修复bug哪里MCP tools是not discovered当tool search是enabled和prompt是passed在as launch argument
- 改进memory usage在long sessions通过clearing internal caches之后compaction
- 添加`claude agents` CLI command到list所有configured agents
- 改进memory usage在long sessions通过clearing large tool results之后they有been processed
- 修复a memory leak哪里LSP diagnostic data是never cleaned up之后delivery, causing unbounded memory growth在long sessions
- 修复a memory leak哪里completed task output是not freed从memory, reducing memory usage在long sessions使用many tasks
- 改进startup performance用于headless mode (`-p` flag)通过deferring Yoga WASM和UI component imports
- 修复prompt suggestion cache regression那reduced cache hit rates
- 修复unbounded memory growth在long sessions通过capping file history snapshots
- 添加`CLAUDE_CODE_DISABLE_1M_CONTEXT` environment variable到disable 1M context window support
- Opus 4.6 (fast mode)现在includes full 1M context window
- VSCode: Added `/extra-usage` command support在VS Code sessions
- 修复memory leak哪里TaskOutput retained最近lines之后cleanup
- 修复memory leak在Circular缓冲区哪里cleared items是retained在backing array
- 修复memory leak在shell command execution哪里ChildProcess和中止Controller references是retained之后cleanup

## 2.1.49

- 改进MCP OAuth authentication使用step-up auth support和discovery caching, reducing redundant network requests在server connections
- 添加`--worktree` (`-w`) flag到start Claude在isolated git worktree
- Subagents support `isolation: "worktree"`用于working在temporary git worktree
- 添加Ctrl+F keybinding到kill后台agents (two-press confirmation)
- 智能体 definitions support `background: true`到always run作为background task
- 插件s可以ship `settings.json`用于default configuration
- 修复file-not-found errors到suggest corrected paths当model drops repo folder
- 修复Ctrl+C和ESC being silently ignored当background agents是running和main thread是idle. 按下ing twice within 3 seconds现在kills所有background agents.
- 修复prompt suggestion cache regression那reduced cache hit rates.
- 修复`plugin enable`和`plugin disable`到auto-detect正确scope当`--scope`是not specified, instead的always defaulting到user scope
- Simple mode (`CLAUDE_CODE_SIMPLE`)现在includes file edit tool在addition到Bash tool, allowing direct file editing在simple mode.
- Permission suggestions是now populated当safety checks trigger ask response, enabling SDK consumers到display permission options
- Sonnet 4.5使用1M context是being removed从Max plan在favor的our frontier Sonnet 4.6 model,哪个now有1M context. Please switch在/model.
- 修复verbose mode not updating thinking block display当toggled via `/config` — memo comparators现在correctly detect详细changes
- 修复unbounded WASM memory growth在long sessions通过periodically resetting tree-sitter parser
- 修复potential rendering issues caused通过stale yoga layout references
- 改进performance在non-interactive mode (`-p`)通过skipping unnecessary API calls在startup
- 改进performance通过caching authentication failures用于HTTP和SSE MCP servers, avoiding repeated connection attempts到servers requiring auth
- 修复unbounded memory growth在long-running sessions caused通过Yoga WASM linear memory never shrinking
- SDK model info现在includes `supportsEffort`, `supportedEffort级别s`,和`supportsAdaptiveThinking` fields所以consumers可以discover model capabilities.
- 添加`ConfigChange` hook event那fires当configuration files change在session, enabling enterprise security auditing和optional blocking的settings changes.
- 改进startup performance通过caching MCP auth failures到avoid redundant connection attempts
- 改进startup performance通过reducing HTTP calls用于analytics token counting
- 改进startup performance通过batching MCP tool token counting into single API call
- 修复`disableAllHooks` setting到respect managed settings hierarchy — non-managed settings可以no longer disable managed hooks set通过policy (#26637)
- 修复`--resume` session picker showing raw XML tags用于sessions那start使用commands喜欢`/clear`. 否w correctly falls through到session ID fallback.
- 改进permission prompts用于path safety和working directory blocks到show reason用于restriction instead的bare prompt使用no context

## 2.1.47

- 修复文件写入Tool line counting到preserve intentional trailing blank lines instead的stripping them使用`trimEnd()`.
- 修复Windows terminal rendering bugs caused通过`os.EOL` (`\r\n`)在display code — line counts现在show正确values instead的always showing 1在Windows.
- 改进VS Code plan preview: auto-updates作为Claude iterates, enables commenting only当plan是ready用于review,和keeps preview open当rejecting所以Claude可以revise.
- 修复a bug哪里bold和colored text在markdown output可以shift到wrong characters在Windows due到`\r\n` line endings.
- 修复compaction failing当conversation contains很多PDF documents通过stripping document blocks alongside images之前sending到compaction API (anthropics/claude-code#26188)
- 改进memory usage在long-running sessions通过releasing API stream buffers, agent context,和skill state之后use
- 改进startup performance通过deferring 会话启动 hook execution, reducing time-to-interactive通过~500ms.
- 修复an issue哪里bash tool output是silently discarded在Windows当using MSYS2或Cygwin shells.
- 改进performance的`@` file mentions - file suggestions现在appear faster通过pre-warming index在startup和using session-based caching使用background refresh.
- 改进memory usage通过trimming agent task message history之后tasks complete
- 改进memory usage在long agent sessions通过eliminating O(n²) message accumulation在progress updates
- 修复the bash permission classifier到validate那returned match descriptions correspond到actual input rules, preventing hallucinated descriptions从incorrectly granting permissions
- 修复user-defined agents仅loading one file在NFS/FUSE filesystems那report zero inodes (anthropics/claude-code#26044)
- 修复plugin agent skills silently failing到load当referenced通过bare name instead的fully-qualified plugin name (anthropics/claude-code#25834)
- 搜索 patterns在collapsed tool results是now displayed在quotes用于clarity
- Windows: 修复ed CWD tracking temp files never being cleaned up, causing them到accumulate indefinitely (anthropics/claude-code#17600)
- Use `ctrl+f`到kill所有background agents instead的double-pressing ESC. Background agents现在continue running当you press ESC到cancel主要thread, giving您more control over agent lifecycle.
- 修复API 400 errors ("thinking blocks cannot be modified")那occurred在sessions使用concurrent agents, caused通过interleaved streaming content blocks preventing proper message merging.
- 简化了teammate navigation到use仅Shift+Down (with wrapping) instead的both Shift+Up和Shift+Down.
- 修复an issue哪里single file write/edit error将abort所有other parallel file write/edit operations. Independent file mutations现在complete even当sibling fails.
- 添加`last_assistant_message` field到停止和Subagent停止 hook inputs, providing final assistant response text所以hooks可以access它without parsing transcript files.
- 修复custom session titles set via `/rename` being lost之后resuming conversation (anthropics/claude-code#23610)
- 修复collapsed read/search hint text overflowing在narrow terminals通过truncating从start.
- 修复an issue哪里bash commands使用backslash-newline continuation lines (e.g.,长commands split across multiple lines使用`\`)将produce spurious empty arguments, potentially breaking command execution.
- 修复built-in slash commands (`/help`, `/model`, `/compact`, etc.) being hidden从autocomplete dropdown当many user skills是installed (anthropics/claude-code#22020)
- 修复MCP servers not appearing在MCP Management 对话框之后deferred loading
- 修复session name persisting在status bar之后`/clear` command (anthropics/claude-code#26082)
- 修复crash当skill's `name`或`description`在SKILL.md frontmatter是bare number (e.g., `name: 3000`) — value是now properly coerced到string (anthropics/claude-code#25837)
- 修复/resume silently dropping sessions当first message exceeds 16KB或uses array-format content (anthropics/claude-code#25721)
- 添加`chat:newline` keybinding action用于configurable multi-line input (anthropics/claude-code#26075)
- 添加`added_dirs`到statusline JSON `workspace` section, exposing directories添加via `/add-dir`到external scripts (anthropics/claude-code#26096)
- 修复`claude doctor` misclassifying mise和asdf-managed installations作为native installs (anthropics/claude-code#26033)
- 修复zsh heredoc failing使用"read-only file system" error在sandboxed commands (anthropics/claude-code#25990)
- 修复agent progress indicator showing inflated tool use count (anthropics/claude-code#26023)
- 修复image pasting not working在WSL2 systems哪里Windows copies images作为BMP format (anthropics/claude-code#25935)
- 修复background agent results returning raw transcript data instead的agent's final answer (anthropics/claude-code#26012)
- 修复Warp terminal incorrectly prompting用于Shift+输入 setup当it supports它natively (anthropics/claude-code#25957)
- 修复CJK wide characters causing misaligned timestamps和layout elements在TUI (anthropics/claude-code#26084)
- 修复custom agent `model` field在`.claude/agents/*.md` being ignored当spawning team teammates (anthropics/claude-code#26064)
- 修复plan mode being lost之后context compaction, causing model到switch从planning到implementation mode (anthropics/claude-code#26061)
- 修复`alwaysThinking启用d: true`在settings.json not enabling thinking mode在Bedrock和Vertex providers (anthropics/claude-code#26074)
- 修复`tool_decision` OTel telemetry event not being emitted在headless/SDK mode (anthropics/claude-code#26059)
- 修复session name being lost之后context compaction — renamed sessions现在preserve它们的custom title through compaction (anthropics/claude-code#26121)
- 提高了initial session count在resume picker从10到50用于faster session discovery (anthropics/claude-code#26123)
- Windows:修复worktree session matching当drive letter casing differs (anthropics/claude-code#26123)
- 修复`/resume <session-id>` failing到find sessions谁的first message exceeds 16KB (anthropics/claude-code#25920)
- 修复"Always allow"在multiline bash commands creating无效permission patterns那corrupt settings (anthropics/claude-code#25909)
- 修复React crash (error #31)当skill's `argument-hint`在SKILL.md frontmatter uses YAML sequence syntax (e.g., `[topic: foo | bar]`) — value是now properly coerced到string (anthropics/claude-code#25826)
- 修复crash当using `/fork`在sessions那used web search — null entries在search results从transcript deserialization是now handled gracefully (anthropics/claude-code#25811)
- 修复read-only git commands triggering FSEvents file watcher loops在macOS通过adding --no-optional-locks flag (anthropics/claude-code#25750)
- 修复custom agents和skills not being discovered当running从git worktree — project-level `.claude/agents/`和`.claude/skills/`从main repository是now included (anthropics/claude-code#25816)
- 修复non-interactive subcommands喜欢`claude doctor`和`claude plugin validate` being阻止inside nested Claude sessions (anthropics/claude-code#25803)
- Windows: 修复了same CLAUDE.md file being loaded twice当drive letter casing differs between paths (anthropics/claude-code#25756)
- 修复inline code spans在markdown being incorrectly parsed作为bash commands (anthropics/claude-code#25792)
- 修复teammate spinners not respecting自定义spinnerVerbs从settings (anthropics/claude-code#25748)
- 修复shell commands permanently failing之后command deletes它的own工作directory (anthropics/claude-code#26136)
- 修复hooks (PreToolUse, PostToolUse) silently failing到execute在Windows通过using Git Bash instead的cmd.exe (anthropics/claude-code#25981)
- 修复LSP `findReferences`和other location-based operations returning results从gitignored files (e.g., `node_modules/`, `venv/`) (anthropics/claude-code#26051)
- 移动d config backup files从home directory root到`~/.claude/backups/`到reduce home directory clutter (anthropics/claude-code#26130)
- 修复sessions使用large第一prompts (>16KB) disappearing从/resume list (anthropics/claude-code#26140)
- 修复shell functions使用double-underscore prefixes (e.g., `__git_ps1`) not being preserved across shell sessions (anthropics/claude-code#25824)
- 修复spinner showing "0 tokens" counter之前any tokens有been received (anthropics/claude-code#26105)
- VSCode: 修复ed conversation messages appearing dimmed当AskUserQuestion dialog是open (anthropics/claude-code#26078)
- 修复background tasks failing在git worktrees due到remote URL resolution reading从worktree-specific gitdir instead的main repository config (anthropics/claude-code#26065)
- 修复Right Alt key leaving可见`[25~` escape sequence residue在input field在Windows/Git Bash terminals (anthropics/claude-code#25943)
- The `/rename` command现在updates terminal tab title通过default (anthropics/claude-code#25789)
- 修复编辑 tool silently corrupting Unicode curly quotes (\u201c\u201d \u2018\u2019)通过replacing them使用straight quotes当making edits (anthropics/claude-code#26141)
- 修复OSC 8 hyperlinks仅being clickable在first line当link text wraps across multiple terminal lines.

## 2.1.46

- 修复orphaned CC processes之后terminal disconnect在macOS
- 添加support用于using claude.ai MCP connectors在Claude Code

## 2.1.45

- 添加support用于Claude Sonnet 4.6
- 添加support用于reading `enabled插件s`和`extraKnownMarketplaces`从`--add-dir` directories
- 添加`spinnerTipsOverride` setting到customize spinner tips — configure `tips`使用array的custom tip strings,和optionally set `excludeDefault: true`到show only您的custom tips instead的built-in ones
- 添加`SDKRate限制信息`和`SDKRate限制Event` types到SDK, enabling consumers到receive rate limit status updates including utilization,重置times,和overage information
- 修复智能体 团队s teammates failing在Bedrock, Vertex,和Foundry通过propagating API provider environment variables到tmux-spawned processes (anthropics/claude-code#23561)
- 修复sandbox "operation not permitted" errors当writing临时files在macOS通过using正确per-user temp directory (anthropics/claude-code#21654)
- 修复Task tool (backgrounded agents) crashing使用`Reference错误`在completion (anthropics/claude-code#22087)
- 修复autocomplete suggestions not being accepted在输入当images是pasted在input
- 修复skills invoked通过subagents incorrectly appearing在main session context之后compaction
- 修复excessive `.claude.json.backup` files accumulating在every startup
- 修复plugin-provided commands, agents,和hooks not being可用immediately之后installation without requiring restart
- 改进startup performance通过removing eager loading的session history用于stats caching
- 改进memory usage用于shell commands那produce large output — RSS不longer grows unboundedly使用command output size
- 改进collapsed read/search groups到show当前file或search pattern being processed beneath summary line当active
- [VSCode] Improved permission destination choice (project/user/session)到persist across sessions

## 2.1.44

- 修复ENAMETOOLONG errors用于deeply-nested directory paths
- 修复auth refresh errors

## 2.1.43

- 修复AWS auth refresh hanging indefinitely通过adding 3-minute timeout
- 修复spurious warnings用于non-agent markdown files在`.claude/agents/` directory
- 修复structured-outputs beta header being sent unconditionally在Vertex/Bedrock

## 2.1.42

- 改进startup performance通过deferring Zod schema construction
- 改进prompt cache hit rates通过moving date out的system prompt
- 添加one-time Opus 4.6 effort callout用于eligible users
- 修复/resume showing interrupt messages作为session titles
- 修复image dimension limit errors到suggest /compact

## 2.1.41

- 添加guard against launching Claude Code inside另一个Claude Code session
- 修复智能体 团队s using错误model identifier用于Bedrock, Vertex,和Foundry customers
- 修复a crash当MCP tools return image content在streaming
- 修复/resume session previews showing raw XML tags instead的readable command names
- 改进model错误messages用于Bedrock/Vertex/Foundry users使用fallback suggestions
- 修复plugin browse showing misleading "Space到切换" hint用于already-installed plugins
- 修复hook blocking errors (exit code 2) not showing stderr到user
- 添加`speed` attribute到OTel events和trace spans用于fast mode visibility
- 添加`claude auth login`, `claude auth status`,和`claude auth logout` CLI subcommands
- 添加Windows ARM64 (win32-arm64) native binary support
- 改进`/rename`到auto-generate session name从conversation context当called without arguments
- 改进narrow terminal layout用于prompt footer
- 修复file resolution failing用于@-mentions使用anchor fragments (e.g., `@README.md#installation`)
- 修复文件读取Tool blocking process在FIFOs, `/dev/stdin`,和large files
- 修复background task notifications not being delivered在streaming 智能体 SDK mode
- 修复cursor jumping到end在each keystroke在classifier rule input
- 修复markdown link display text being dropped用于raw URL
- 修复auto-compact failure错误notifications being shown到users
- 修复permission wait time being included在subagent elapsed time display
- 修复proactive ticks firing while在plan mode
- 修复clear stale permission rules当settings change在disk
- 修复hook blocking errors showing stderr content在UI

## 2.1.39

- 改进terminal rendering performance
- 修复fatal errors being swallowed instead的displayed
- 修复process hanging之后session close
- 修复character loss在terminal screen boundary
- 修复blank lines在verbose transcript view

## 2.1.38

- 修复VS Code terminal scroll-to-top regression introduced在2.1.37
- 修复Tab key queueing slash commands instead的autocompleting
- 修复bash permission matching用于commands using environment variable wrappers
- 修复text between tool uses disappearing当not using streaming
- 修复duplicate sessions当resuming在VS Code extension
- 改进heredoc delimiter parsing到prevent command smuggling
- 阻止ed writes到`.claude/skills` directory在sandbox mode

## 2.1.37

- 修复an issue哪里/fast是not immediately available之后enabling /extra-usage

## 2.1.36

- Fast mode是now available用于Opus 4.6. Learn more在https://code.claude.com/docs/en/fast-mode

## 2.1.34

- 修复a crash当agent teams setting更改between renders
- 修复a bug哪里commands excluded从sandboxing (via `sandbox.excludedCommands`或`dangerously禁用Sandbox`)可以bypass Bash ask permission rule当`auto允许BashIfSandboxed`是enabled

## 2.1.33

- 修复agent teammate sessions在tmux到send和receive messages
- 修复warnings about agent teams not being available在your当前plan
- 添加`团队mateIdle`和`Task已完成` hook events用于multi-agent workflows
- 添加support用于restricting哪个sub-agents可以be spawned via `Task(agent_type)` syntax在agent "tools" frontmatter
- 添加`memory` frontmatter field support用于agents, enabling持久memory使用`user`, `project`,或`local` scope
- 添加plugin name到skill descriptions和`/skills` menu用于better discoverability
- 修复an issue哪里submitting新message当model was在extended thinking将interrupt thinking phase
- 修复an API error那could occur当aborting mid-stream,哪里whitespace text combined使用thinking block将bypass normalization和produce无效request
- 修复API proxy compatibility issue哪里404 errors在streaming endpoints不longer triggered non-streaming fallback
- 修复an issue哪里proxy settings配置via `settings.json` environment variables是not applied到Web获取和other HTTP requests在否de.js build
- 修复`/resume` session picker showing raw XML markup instead的clean titles用于sessions started使用slash commands
- 改进error messages用于API connection failures —现在shows特定cause (e.g., ECONNREFUSED, SSL errors) instead的generic "连接 error"
- 错误s从invalid managed settings是now surfaced
- VSCode: 添加了对remote sessions, allowing OAuth users到browse和resume sessions从claude.ai
- VSCode: Added git branch和message count到session picker,使用support用于searching通过branch name
- VSCode: 修复ed scroll-to-bottom under-scrolling在initial session load和session switch

## 2.1.32

- Claude Opus 4.6是now available!
- 添加research preview agent teams feature用于multi-agent collaboration (token-intensive feature, requires setting CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1)
- Claude现在automatically records和recalls memories作为it works
- 添加"Summarize从here"到message selector, allowing partial conversation summarization.
- 技能s defined在`.claude/skills/` within additional directories (`--add-dir`)是now loaded automatically.
- 修复`@` file completion showing不正确relative paths当running从subdirectory
- 更新d --resume到re-use --agent value specified在previous conversation通过default.
- 修复ed: Bash tool不longer throws "Bad substitution" errors当heredocs contain JavaScript template literals喜欢`${index + 1}`,哪个previously中断tool execution
- 技能 character budget现在scales使用context window (2%的context),所以users使用larger context windows可以see更多skill descriptions without truncation
- 修复Thai/Lao spacing vowels (สระ า, ำ) not rendering correctly在input field
- VSCode: 修复ed slash commands incorrectly being executed当pressing 输入使用preceding text在input field
- VSCode: Added spinner当loading过去conversations list

## 2.1.31

- 添加session resume hint在exit, showing how到continue您的conversation later
- 添加support用于full-width (zenkaku) space input从Japanese IME在checkbox selection
- 修复PDF也large errors permanently locking up sessions, requiring users到start新conversation
- 修复bash commands incorrectly reporting failure使用"读取-only file system" errors当sandbox mode是enabled
- 修复a crash那made sessions unusable之后entering plan mode当project config在`~/.claude.json`是missing默认fields
- 修复`temperatureOverride` being silently ignored在streaming API path, causing所有streaming requests到use默认temperature (1) regardless的configured override
- 修复LSP shutdown/exit compatibility使用strict language servers那reject null params
- 改进system prompts到more clearly guide model toward using专用tools (读取, 编辑, Glob, Grep) instead的bash equivalents (`cat`, `sed`, `grep`, `find`), reducing unnecessary bash command usage
- 改进PDF和request size错误messages到show actual limits (100 pages, 20MB)
- 减少了layout jitter在terminal当spinner appears和disappears在streaming
- 移除misleading Anthropic API pricing从model selector用于third-party provider (Bedrock, Vertex, Foundry) users

## 2.1.30

- 添加`pages` parameter到读取 tool用于PDFs, allowing特定page ranges到be read (e.g., `pages: "1-5"`). Large PDFs (>10 pages)现在return lightweight reference当`@` mentioned instead的being inlined into context.
- 添加pre-configured OAuth client credentials用于MCP servers那don't support Dynamic Client Registration (e.g., Slack). Use `--client-id`和`--client-secret`使用`claude mcp add`.
- 添加`/debug`用于Claude到help troubleshoot当前session
- 添加support用于additional `git log`和`git show` flags在read-only mode (e.g., `--topo-order`, `--cherry-pick`, `--format`, `--raw`)
- 添加token count, tool uses,和duration metrics到Task tool results
- 添加reduced motion mode到config
- 修复phantom "(no content)" text blocks appearing在API conversation history, reducing token waste和potential model confusion
- 修复prompt cache not correctly invalidating当tool descriptions或input schemas changed, only当tool names changed
- 修复400 errors那could occur之后running `/login`当conversation contained thinking blocks
- 修复a hang当resuming sessions使用corrupted transcript files containing `parentUuid` cycles
- 修复rate limit message showing不正确"/upgrade" suggestion用于Max 20x users当extra-usage是unavailable
- 修复permission dialogs stealing focus当actively typing
- 修复subagents not being able到access SDK-provided MCP tools因为they是not synced到shared application state
- 修复a regression哪里Windows users使用`.bashrc` file可以not run bash commands
- 改进memory usage用于`--resume` (68% reduction用于users使用many sessions)通过replacing session index使用lightweight stat-based loading和progressive enrichment
- 改进`Task停止` tool到display停止command/task description在result line instead的generic "Task stopped" message
- 更改`/model`到execute immediately instead的being queued
- [VSCode] Added multiline input support到"Other" text input在question dialogs (use Shift+输入用于new lines)
- [VSCode] 修复ed重复sessions appearing在session list当starting新conversation

## 2.1.29

- 修复startup performance issues当resuming sessions that有`saved_hook_context`

## 2.1.27

- 添加tool call failures和denials到debug logs
- 修复context management validation error用于gateway users, ensuring `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1` avoids error
- 添加`--from-pr` flag到resume sessions linked到specific GitHub PR number或URL
- 会话s是now automatically linked到PRs当created via `gh pr create`
- 修复/context command not displaying colored output
- 修复status bar duplicating后台task indicator当PR status是shown
- Windows: 修复ed bash command execution failing用于users使用`.bashrc` files
- Windows: 修复ed console windows flashing当spawning child processes
- VSCode: 修复ed OAuth token expiration causing 401 errors之后extended sessions

## 2.1.25

- 修复beta header validation error用于gateway users在Bedrock和Vertex, ensuring `CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1` avoids error

## 2.1.23

- 添加customizable spinner verbs setting (`spinnerVerbs`)
- 修复mTLS和proxy connectivity用于users behind corporate proxies或using client certificates
- 修复per-user temp directory isolation到prevent permission conflicts在shared systems
- 修复a race condition那could cause 400 errors当prompt caching scope是enabled
- 修复pending async hooks not being cancelled当headless streaming sessions ended
- 修复tab completion not updating input field当accepting suggestion
- 修复ripgrep search timeouts silently returning empty results instead的reporting errors
- 改进terminal rendering performance使用optimized screen data layout
- 更改Bash commands到show超时duration alongside elapsed time
- 更改merged pull requests到show purple status indicator在prompt footer
- [IDE] 修复ed model options displaying不正确region strings用于Bedrock users在headless mode

## 2.1.22

- 修复structured outputs用于non-interactive (-p) mode

## 2.1.21

- 添加support用于full-width (zenkaku) number input从Japanese IME在option selection prompts
- 修复shell completion cache files being truncated在exit
- 修复API errors当resuming sessions that是interrupted在tool execution
- 修复auto-compact triggering也early在models使用large output token limits
- 修复task IDs potentially being reused之后deletion
- 修复file search not working在VS Code extension在Windows
- 改进read/search progress indicators到show "读取ing…" while在progress和"读取"当complete
- 改进Claude到prefer file operation tools (读取, 编辑, 写入) over bash equivalents (cat, sed, awk)
- [VSCode] 添加了utomatic Python virtual environment activation, ensuring `python`和`pip` commands use正确interpreter (configurable via `claudeCode.usePythonEnvironment` setting)
- [VSCode] 修复ed message action buttons having不正确background colors

## 2.1.20

- 添加arrow key history navigation在vim正常mode当cursor cannot move further
- 添加external editor shortcut (Ctrl+G)到help menu用于better discoverability
- 添加PR review status indicator到prompt footer, showing当前branch's PR state (approved, changes requested, pending,或draft)作为colored dot使用clickable link
- 添加support用于loading `CLAUDE.md` files从additional directories specified via `--add-dir` flag (requires setting `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1`)
- 添加ability到delete tasks via `Task更新` tool
- 修复session compaction issues那could cause resume到load full history instead的compact summary
- 修复agents sometimes ignoring user messages sent当actively working在task
- 修复wide character (emoji, CJK) rendering artifacts哪里trailing columns是not cleared当replaced通过narrower characters
- 修复JSON parsing errors当MCP tool responses contain特殊Unicode characters
- 修复up/down arrow keys在multi-line和wrapped text input到prioritize cursor movement over history navigation
- 修复draft prompt being lost当pressing UP arrow到navigate command history
- 修复ghost text flickering当typing slash commands mid-input
- 修复marketplace source removal not properly deleting settings
- 修复duplicate output在some commands喜欢`/context`
- 修复task list sometimes showing outside主要conversation view
- 修复syntax highlighting用于diffs occurring within multiline constructs喜欢Python docstrings
- 修复crashes当cancelling tool use
- 改进`/sandbox` command UI到show dependency status使用installation instructions当dependencies是missing
- 改进thinking status text使用subtle shimmer animation
- 改进task list到dynamically adjust可见items based在terminal height
- 改进fork conversation hint到show how到resume原始session
- 更改collapsed read/search groups到show现在tense ("读取ing", "搜索ing for") while在progress,和past tense ("读取", "搜索ed for")当complete
- 更改`Tool搜索` results到appear作为brief notification instead的inline在conversation
- 更改the `/commit-push-pr` skill到automatically post PR URLs到Slack channels当configured via MCP tools
- 更改the `/copy` command到be available到all users
- 更改background agents到prompt用于tool permissions之前launching
- 更改permission rules喜欢`Bash(*)`到be accepted和treated作为equivalent到`Bash`
- 更改config backups到be timestamped和rotated (keeping 5最多recent)到prevent data loss

## 2.1.19

- 添加env var `CLAUDE_CODE_ENABLE_TASKS`, set到`false`到keep旧system temporarily
- 添加shorthand `$0`, `$1`, etc.用于accessing individual arguments在custom commands
- 修复crashes在processors without AVX instruction support
- 修复dangling Claude Code processes当terminal是closed通过catching EIO errors从`process.exit()`和using SIGKILL作为fallback
- 修复`/rename`和`/tag` not updating正确session当resuming从different directory (e.g., git worktrees)
- 修复resuming sessions通过custom title not working当run从different directory
- 修复pasted text content being lost当using prompt stash (Ctrl+S)和restore
- 修复agent list displaying "Sonnet (default)" instead的"Inherit (default)"用于agents without explicit model setting
- 修复backgrounded hook commands not returning early, potentially causing session到wait在process that是intentionally backgrounded
- 修复file write preview omitting empty lines
- 更改skills without additional permissions或hooks到be允许without requiring approval
- 更改indexed argument syntax从`$ARGUMENTS.0`到`$ARGUMENTS[0]` (bracket syntax)
- [SDK] Added replay的`queued_command` attachment messages作为`SDKUser消息Replay` events当`replayUser消息s`是enabled
- [VSCode] 启用d session forking和rewind functionality用于all users

## 2.1.18

- 添加customizable keyboard shortcuts. Configure keybindings per context, create chord sequences,和personalize您的workflow. Run `/keybindings`到get started. Learn more在https://code.claude.com/docs/en/keybindings

## 2.1.17

- 修复crashes在processors without AVX instruction support

## 2.1.16

- 添加new task management system, including新capabilities喜欢dependency tracking
- [VSCode] Added native plugin management support
- [VSCode] 添加了bility用于OAuth users到browse和resume远程Claude sessions从会话s dialog
- 修复out-of-memory crashes当resuming sessions使用heavy subagent usage
- 修复an issue哪里"context remaining" warning是not hidden之后running `/compact`
- 修复session titles在resume screen not respecting user's language setting
- [IDE] 修复ed race condition在Windows哪里Claude Code sidebar view container将not appear在start

## 2.1.15

- 添加deprecation notification用于npm installations - run `claude install`或see https://docs.anthropic.com/en/docs/claude-code/getting-started用于more options
- 改进UI rendering performance使用React Compiler
- 修复the "上下文 left直到auto-compact"警告not disappearing之后running `/compact`
- 修复MCP stdio server超时not killing child process, which可以cause UI freezes

## 2.1.14

- 添加history-based autocomplete在bash mode (`!`) - type partial command和press Tab到complete从your bash command history
- 添加search到installed plugins list - type到filter通过name或description
- 添加support用于pinning plugins到specific git commit SHAs, allowing marketplace entries到install exact versions
- 修复a regression哪里context window blocking limit是calculated也aggressively, blocking users在~65% context usage instead的intended ~98%
- 修复memory issues那could cause crashes当running parallel subagents
- 修复memory leak在long-running sessions哪里stream resources是not cleaned up之后shell commands completed
- 修复`@` symbol incorrectly triggering file autocomplete suggestions在bash mode
- 修复`@`-mention menu folder click behavior到navigate into directories instead的selecting them
- 修复`/feedback` command generating无效GitHub issue URLs当description是very long
- 修复`/context` command到show相同token count和percentage作为status line在verbose mode
- 修复an issue哪里`/config`, `/context`, `/model`,和`/todos` command overlays可以close unexpectedly
- 修复slash command autocomplete selecting错误command当typing相似commands (e.g., `/context` vs `/compact`)
- 修复inconsistent back navigation在plugin marketplace当only one marketplace是configured
- 修复iTerm2 progress bar not clearing properly在exit, preventing lingering indicators和bell sounds
- 改进backspace到delete粘贴text作为single token instead的one character在time
- [VSCode] Added `/usage` command到display当前plan usage

## 2.1.12

- 修复message rendering bug

## 2.1.11

- 修复excessive MCP connection requests用于HTTP/SSE transports

## 2.1.10

- 添加new `Setup` hook event那can be triggered via `--init`, `--init-only`,或`--maintenance` CLI flags用于repository setup和maintenance operations
- 添加keyboard shortcut 'c'到copy OAuth URL当browser doesn't开放automatically在login
- 修复a crash当running bash commands containing heredocs使用JavaScript template literals喜欢`${index + 1}`
- 改进startup到capture keystrokes typed之前REPL是fully ready
- 改进file suggestions到show作为removable attachments instead的inserting text当accepted
- [VSCode] Added install count display到plugin listings
- [VSCode] Added trust warning当installing plugins

## 2.1.9

- 添加`auto:N` syntax用于configuring MCP tool search auto-enable threshold,哪里N是context window percentage (0-100)
- 添加`plans目录` setting到customize哪里plan files是stored
- 添加external editor support (Ctrl+G)在AskUserQuestion "Other" input field
- 添加session URL attribution到commits和PRs created从web sessions
- 添加support用于`PreToolUse` hooks到return `additional上下文`到model
- 添加`${CLAUDE_SESSION_ID}` string substitution用于skills到access当前session ID
- 修复long sessions使用parallel tool calls failing使用API错误about orphan tool_result blocks
- 修复MCP server reconnection hanging当cached connection promise never resolves
- 修复Ctrl+Z suspend not working在terminals using Kitty keyboard protocol (Ghostty, iTerm2, kitty, WezTerm)

## 2.1.7

- 添加`showTurnDuration` setting到hide turn duration messages (e.g., "Cooked用于1m 6s")
- 添加ability到provide feedback当accepting permission prompts
- 添加inline display的agent's final response在task notifications, making它easier到see results without reading full transcript file
- 修复security vulnerability哪里wildcard permission rules可以match compound commands containing shell operators
- 修复false "file modified" errors在Windows当cloud sync tools, antivirus scanners,或Git touch file timestamps without changing content
- 修复orphaned tool_result errors当sibling tools fail在streaming execution
- 修复context window blocking limit being calculated using full context window instead的effective context window (which reserves space用于max output tokens)
- 修复spinner briefly flashing当running本地slash commands喜欢`/model`或`/theme`
- 修复terminal title animation jitter通过using fixed-width braille characters
- 修复plugins使用git submodules not being fully initialized当installed
- 修复bash commands failing在Windows当temp directory paths contained characters喜欢`t`或`n` that是misinterpreted作为escape sequences
- 改进typing responsiveness通过reducing memory allocation overhead在terminal rendering
- 启用d MCP tool search auto mode通过default用于all users. When MCP tool descriptions exceed 10%的context window, they是automatically deferred和discovered via MCP搜索 tool instead的being loaded upfront. This reduces context usage用于users使用many MCP tools configured. Users可以disable this通过adding `MCP搜索`到`disallowedTools`在their settings.
- 更改OAuth和API Console URLs从console.anthropic.com到platform.claude.com
- [VSCode] 修复ed `claudeProcessWrapper` setting passing wrapper path instead的Claude binary path

## 2.1.6

- 添加search functionality到`/config` command用于quickly filtering settings
- 添加更新s section到`/doctor` showing auto-update channel和available npm versions (stable/latest)
- 添加date range filtering到`/stats` command - press `r`到cycle between Last 7 days, Last 30 days,和All time
- 添加automatic discovery的skills从nested `.claude/skills` directories当working使用files在subdirectories
- 添加`context_window.used_percentage`和`context_window.remaining_percentage` fields到status line input用于easier context window display
- 添加an错误display当editor fails在Ctrl+G
- 修复permission bypass via shell line continuation那could allow阻止commands到execute
- 修复false "文件有been unexpectedly modified" errors当file watchers touch files without changing content
- 修复text styling (bold, colors) getting progressively misaligned在multi-line responses
- 修复the feedback panel closing unexpectedly当typing 'n'在description field
- 修复rate limit警告appearing在low usage之后weekly重置(now requires 70% usage)
- 修复rate limit options menu incorrectly auto-opening当resuming上一个session
- 修复numpad keys outputting escape sequences instead的characters在Kitty keyboard protocol terminals
- 修复选项+Return not inserting newlines在Kitty keyboard protocol terminals
- 修复corrupted config backup files accumulating在home directory (now仅one backup是created per config file)
- 修复`mcp list`和`mcp get` commands leaving orphaned MCP server processes
- 修复visual artifacts在ink2 mode当nodes become隐藏via `display:none`
- 改进the external CLAUDE.md imports approval dialog到show哪个files是being imported和from where
- 改进the `/tasks` dialog到go directly到task details当there's仅one后台task running
- 改进@ autocomplete使用icons用于different suggestion types和single-line formatting
- 更新d "Help improve Claude" setting fetch到refresh OAuth和retry当it fails due到stale OAuth token
- 更改task notification display到cap在3 lines使用overflow summary当multiple后台tasks complete simultaneously
- 更改terminal title到"Claude Code"在startup用于better window identification
- 移除ability到@-mention MCP servers到enable/disable - use `/mcp enable <name>` instead
- [VSCode] 修复ed usage indicator not updating之后manual compact

## 2.1.5

- 添加`CLAUDE_CODE_TMPDIR` environment variable到override temp directory used用于internal temp files, useful用于environments使用custom temp directory requirements

## 2.1.4

- 添加`CLAUDE_CODE_DISABLE_BACKGROUND_TASKS` environment variable到disable所有background task functionality including auto-backgrounding和Ctrl+B shortcut
- 修复"Help improve Claude" setting fetch到refresh OAuth和retry当it fails due到stale OAuth token

## 2.1.3

- 合并d slash commands和skills, simplifying mental model使用no change在behavior
- 添加release channel (`stable`或`latest`) toggle到`/config`
- 添加detection和warnings用于unreachable permission rules,使用warnings在`/doctor`和after saving rules那include source的each rule和actionable fix guidance
- 修复plan files persisting across `/clear` commands,现在ensuring fresh plan file是used之后clearing conversation
- 修复false skill重复detection在filesystems使用large inodes (e.g., ExFAT)通过using 64-bit precision用于inode values
- 修复mismatch between后台task count在status bar和items shown在tasks dialog
- 修复sub-agents using错误model在conversation compaction
- 修复web search在sub-agents using不正确model
- 修复trust dialog acceptance当running从home directory not enabling trust-requiring features喜欢hooks在session
- 改进terminal rendering stability通过preventing uncontrolled writes从corrupting cursor state
- 改进slash command suggestion readability通过truncating长descriptions到2 lines
- 更改tool hook execution timeout从60 seconds到10 minutes
- [VSCode] Added clickable destination selector用于permission requests, allowing you到choose哪里settings是saved (this project,所有projects, shared使用team,或session only)

## 2.1.2

- 添加source path metadata到images dragged onto terminal, helping Claude understand哪里images originated
- 添加clickable hyperlinks用于file paths在tool output在terminals那support OSC 8 (like iTerm)
- 添加support用于Windows Package Manager (winget) installations使用automatic detection和update instructions
- 添加Shift+Tab keyboard shortcut在plan mode到quickly select "auto-accept edits" option
- 添加`FORCE_AUTOUPDATE_PLUGINS` environment variable到allow plugin autoupdate even当main auto-updater是disabled
- 添加`agent_type`到会话启动 hook input, populated如果`--agent`是specified
- 修复a command injection vulnerability在bash command processing哪里malformed input可以execute arbitrary commands
- 修复a memory leak哪里tree-sitter parse trees是not being freed, causing WASM memory到grow unbounded over长sessions
- 修复binary files (images, PDFs, etc.) being accidentally included在memory当using `@include` directives在CLAUDE.md files
- 修复updates incorrectly claiming另一个installation is在progress
- 修复crash当socket files exist在watched directories (defense-in-depth用于EOPNOTSUPP errors)
- 修复remote session URL和teleport being broken当using `/tasks` command
- 修复MCP tool names being exposed在analytics events通过sanitizing user-specific server configurations
- 改进选项-as-Meta hint在macOS到show terminal-specific instructions用于native CSIu terminals喜欢iTerm2, Kitty,和WezTerm
- 改进error message当pasting images over SSH到suggest using `scp` instead的unhelpful clipboard shortcut hint
- 改进permission explainer到not flag routine dev workflows (git fetch/rebase, npm install, tests, PRs)作为medium risk
- 更改large bash command outputs到be saved到disk instead的truncated, allowing Claude到read full content
- 更改large tool outputs到be persisted到disk instead的truncated, providing full output access via file references
- 更改`/plugins`安装tab到unify plugins和MCPs使用scope-based grouping
- 弃用Windows managed settings path `C:\ProgramData\ClaudeCode\managed-settings.json` - administrators应该migrate到`C:\Program 文件s\ClaudeCode\managed-settings.json`
- [SDK] Changed minimum zod peer dependency到^4.0.0
- [VSCode] 修复ed usage display not updating之后manual compact

## 2.1.0

- 添加automatic skill hot-reload - skills created或modified在`~/.claude/skills`或`.claude/skills`是now immediately可用without restarting session
- 添加support用于running skills和slash commands在forked sub-agent context using `context: fork`在skill frontmatter
- 添加support用于`agent` field在skills到specify agent type用于execution
- 添加`language` setting到configure Claude's response language (e.g., language: "japanese")
- 更改Shift+输入到work out的box在iTerm2, WezTerm, Ghostty,和Kitty without modifying terminal configs
- 添加`respectGitignore` support在`settings.json`用于per-project control over @-mention file picker behavior
- 添加`IS_DEMO` environment variable到hide email和organization从UI, useful用于streaming或recording sessions
- 修复security issue哪里sensitive data (OAuth tokens, API keys, passwords)可以be exposed在debug logs
- 修复files和skills not being properly discovered当resuming sessions使用`-c`或`--resume`
- 修复pasted content being lost当replaying prompts从history using up arrow或Ctrl+R search
- 修复Esc key使用queued prompts到only move them到input without canceling运行task
- 减少了permission prompts用于complex bash commands
- 修复command search到prioritize exact和prefix matches在command names over fuzzy matches在descriptions
- 修复PreToolUse hooks到allow `updatedInput`当returning `ask` permission decision, enabling hooks到act作为middleware当still requesting user consent
- 修复plugin path resolution用于file-based marketplace sources
- 修复LSP tool being incorrectly enabled当no LSP servers是configured
- 修复background tasks failing使用"git repository not found" error用于repositories使用dots在their names
- 修复Claude在Chrome support用于WSL environments
- 修复Windows native installer silently failing当executable creation fails
- 改进CLI help output到display options和subcommands在alphabetical order用于easier navigation
- 添加wildcard pattern matching用于Bash tool permissions using `*`在any position在rules (e.g., `Bash(npm *)`, `Bash(* install)`, `Bash(git * main)`)
- 添加unified Ctrl+B backgrounding用于both bash commands和agents - pressing Ctrl+B现在backgrounds所有running前台tasks simultaneously
- 添加support用于MCP `list_changed` notifications, allowing MCP servers到dynamically update它们的available tools, prompts,和resources without requiring reconnection
- 添加`/teleport`和`/remote-env` slash commands用于claude.ai subscribers, allowing them到resume和configure远程sessions
- 添加support用于disabling特定agents using `Task(智能体Name)` syntax在settings.json permissions或`--disallowedTools` CLI flag
- 添加hooks support到agent frontmatter, allowing agents到define PreToolUse, PostToolUse,和停止 hooks scoped到agent's lifecycle
- 添加hooks support用于skill和slash command frontmatter
- 添加new Vim motions: `;`和`,`到repeat f/F/t/T motions, `y` operator用于yank使用`yy`/`Y`, `p`/`P`用于paste, text objects (`iw`, `aw`, `iW`, `aW`, `i"`, `a"`, `i'`, `a'`, `i(`, `a(`, `i[`, `a[`, `i{`, `a{`), `>>`和`<<`用于indent/dedent,和`J`到join lines
- 添加`/plan` command shortcut到enable plan mode directly从prompt
- 添加slash command autocomplete support当`/` appears anywhere在input, not just在beginning
- 添加`--tools` flag support在interactive mode到restrict哪个built-in tools Claude可以use在interactive sessions
- 添加`CLAUDE_CODE_FILE_READ_MAX_OUTPUT_T确定ENS` environment variable到override默认file read token limit
- 添加support用于`once: true` config用于hooks
- 添加support用于YAML-style lists在frontmatter `allowed-tools` field用于cleaner skill declarations
- 添加support用于prompt和agent hook types从plugins (previously仅command hooks是supported)
- 添加Cmd+V support用于image paste在iTerm2 (maps到Ctrl+V)
- 添加left/right arrow key navigation用于cycling through tabs在dialogs
- 添加real-time thinking block display在Ctrl+O transcript mode
- 添加filepath到full output在background bash task details dialog
- 添加技能s作为separate category在context visualization
- 修复OAuth token refresh not triggering当server reports token过期but本地expiration check disagrees
- 修复session persistence getting stuck之后transient server errors通过recovering从409 conflicts当entry是actually stored
- 修复session resume failures caused通过orphaned tool results在concurrent tool execution
- 修复a race condition哪里stale OAuth tokens可以be read从keychain cache在concurrent token refresh attempts
- 修复AWS Bedrock subagents not inheriting EU/APAC cross-region inference model configuration, causing 403 errors当IAM permissions是scoped到specific regions
- 修复API context overflow当background tasks produce large output通过truncating到30K chars使用file path reference
- 修复a hang当reading FIFO files通过skipping symlink resolution用于special file types
- 修复terminal keyboard mode not being reset在exit在Ghostty, iTerm2, Kitty,和WezTerm
- 修复Alt+B和Alt+F (word navigation) not working在iTerm2, Ghostty, Kitty,和WezTerm
- 修复`${CLAUDE_PLUGIN_ROOT}` not being substituted在plugin `allowed-tools` frontmatter,哪个caused tools到incorrectly require approval
- 修复files created通过写入 tool using hardcoded 0o600 permissions instead的respecting system umask
- 修复commands使用`$()` command substitution failing使用parse errors
- 修复multi-line bash commands使用backslash continuations being incorrectly split和flagged用于permissions
- 修复bash command prefix extraction到correctly identify subcommands之后global options (e.g., `git -C /path log`现在correctly matches `Bash(git log:*)` rules)
- 修复slash commands passed作为CLI arguments (e.g., `claude /context`) not being executed properly
- 修复pressing 输入之后Tab-completing slash command selecting不同command instead的submitting完成one
- 修复slash command argument hint flickering和inconsistent display当typing commands使用arguments
- 修复Claude sometimes redundantly invoking 技能 tool当running slash commands directly
- 修复skill token estimates在`/context`到accurately reflect frontmatter-only loading
- 修复subagents sometimes not inheriting parent's model通过default
- 修复model picker showing不正确selection用于Bedrock/Vertex users using `--model haiku`
- 修复duplicate Bash commands appearing在permission request option labels
- 修复noisy output当background tasks complete -现在shows clean completion message instead的raw output
- 修复background task completion notifications到appear proactively使用bullet point
- 修复forked slash commands showing "中止错误" instead的"已中断" message当cancelled
- 修复cursor disappearing之后dismissing permission dialogs
- 修复`/hooks` menu selecting错误hook type当scrolling到different option
- 修复images在queued prompts showing作为"[object Object]"当pressing Esc到cancel
- 修复images being silently dropped当queueing messages当backgrounding task
- 修复large粘贴images failing使用"图像是too large" error
- 修复extra blank lines在multiline prompts containing CJK characters (Japanese, Chinese, Korean)
- 修复ultrathink keyword highlighting being applied到wrong characters当user prompt text wraps到multiple lines
- 修复collapsed "读取ing X files…" indicator incorrectly switching到past tense当thinking blocks appear mid-stream
- 修复Bash read commands (like `ls`和`cat`) not being counted在collapsed read/search groups, causing groups到incorrectly show "读取 0 files"
- 修复spinner token counter到properly accumulate tokens从subagents在execution
- 修复memory leak在git diff parsing哪里sliced strings retained large parent strings
- 修复race condition哪里LSP tool可以return "no server available"在startup
- 修复feedback submission hanging indefinitely当network requests timeout
- 修复search mode在plugin discovery和log selector views exiting当pressing up arrow
- 修复hook成功message showing trailing colon当hook有no output
- Multiple optimizations到improve startup performance
- 改进terminal rendering performance当using native installer或Bun, especially用于text使用emoji, ANSI codes,和Unicode characters
- 改进performance当reading Jupyter notebooks使用many cells
- 改进reliability用于piped input喜欢`cat refactor.md | claude`
- 改进reliability用于AskQuestion tool
- 改进sed in-place edit commands到render作为file edits使用diff preview
- 改进Claude到automatically continue当response是cut off due到output token limit, instead的showing错误message
- 改进compaction reliability
- 改进subagents (Task tool)到continue working之后permission denial, allowing them到try alternative approaches
- 改进skills到show progress当executing, displaying tool uses作为they happen
- 改进skills从`/skills/` directories到be visible在slash command menu通过default (opt-out使用`user-invocable: false`在frontmatter)
- 改进skill suggestions到prioritize recently和frequently used skills
- 改进spinner feedback当waiting用于first response token
- 改进token count display在spinner到include tokens从background agents
- 改进incremental output用于async agents到give主要thread更多control和visibility
- 改进permission prompt UX使用Tab hint moved到footer, cleaner 是/否 input labels使用contextual placeholders
- 改进the Claude在Chrome notification使用shortened help text和persistent display直到dismissed
- 改进macOS screenshot paste reliability使用TIFF format support
- 改进`/stats` output
- 更新d Atlassian MCP integration到use更多reliable默认configuration (streamable HTTP)
- 更改"已中断" message color从red到grey用于less alarming appearance
- 移除permission prompt当entering plan mode - users可以now enter plan mode without approval
- 移除underline styling从image reference links
- [SDK] Changed minimum zod peer dependency到^4.0.0
- [VSCode] Added currently选中model name到context menu
- [VSCode] Added descriptive labels在auto-accept permission button (e.g., "是, allow npm用于this project" instead的"是,和don't ask again")
- [VSCode] 修复ed paragraph breaks not rendering在markdown content
- [VSCode] 修复ed scrolling在extension inadvertently scrolling parent iframe
- [Windows] 修复了问题使用improper rendering

## 2.0.76

- 修复issue使用macOS code-sign warning当using Claude在Chrome integration

## 2.0.75

- Minor bugfixes

## 2.0.74

- 添加LSP (Language Server Protocol) tool用于code intelligence features喜欢go-to-definition, find references,和hover documentation
- 添加`/terminal-setup` support用于Kitty, Alacritty, Zed,和Warp terminals
- 添加ctrl+t shortcut在`/theme`到toggle syntax highlighting on/off
- 添加syntax highlighting info到theme picker
- 添加guidance用于macOS users当Alt shortcuts fail due到terminal configuration
- 修复skill `allowed-tools` not being applied到tools invoked通过skill
- 修复Opus 4.5 tip incorrectly showing当user是already using Opus
- 修复a potential crash当syntax highlighting isn't initialized correctly
- 修复visual bug在`/plugins discover`哪里list selection indicator showed当search box是focused
- 修复macOS keyboard shortcuts到display 'opt' instead的'alt'
- 改进`/context` command visualization使用grouped skills和agents通过source, slash commands,和sorted token count
- [Windows] 修复了问题使用improper rendering
- [VSCode] Added gift tag pictogram用于year-end promotion message

## 2.0.73

- 添加clickable `[图像 #N]` links那open attached images在default viewer
- 添加alt-y yank-pop到cycle through kill ring history之后ctrl-y yank
- 添加search filtering到plugin discover screen (type到filter通过name, description,或marketplace)
- 添加support用于custom session IDs当forking sessions使用`--session-id` combined使用`--resume`或`--continue`和`--fork-session`
- 修复slow input history cycling和race condition那could overwrite text之后message submission
- 改进`/theme` command到open theme picker directly
- 改进theme picker UI
- 改进search UX across resume session, permissions,和plugins screens使用unified 搜索Box component
- [VSCode] Added tab icon badges showing pending permissions (blue)和unread completions (orange)

## 2.0.72

- 添加Claude在Chrome (Beta) feature那works使用Chrome extension (https://claude.ai/chrome)到let您control您的browser directly从Claude Code
- 减少了terminal flickering
- 添加scannable QR code到mobile app tip用于quick app downloads
- 添加loading indicator当resuming conversations用于better feedback
- 修复`/context` command not respecting自定义system prompts在non-interactive mode
- 修复order的consecutive Ctrl+K lines当pasting使用Ctrl+Y
- 改进@ mention file suggestion speed (~3× faster在git repositories)
- 改进file suggestion performance在repos使用`.ignore`或`.rgignore` files
- 改进settings validation errors到be更多prominent
- 更改thinking toggle从Tab到Alt+T到avoid accidental triggers

## 2.0.71

- 添加/config toggle到enable/disable prompt suggestions
- 添加`/settings`作为alias用于`/config` command
- 修复@ file reference suggestions incorrectly triggering当cursor is在middle的path
- 修复MCP servers从`.mcp.json` not loading当using `--dangerously-skip-permissions`
- 修复permission rules incorrectly rejecting有效bash commands containing shell glob patterns (e.g., `ls *.txt`, `for f在*.png`)
- Bedrock: Environment variable `ANTHROPIC_BEDROCK_BASE_URL`是now respected用于token counting和inference profile listing
- New syntax highlighting engine用于native build

## 2.0.70

- 添加输入 key到accept和submit prompt suggestions immediately (tab仍然accepts用于editing)
- 添加wildcard syntax `mcp__server__*`用于MCP tool permissions到allow或deny所有tools从server
- 添加auto-update toggle用于plugin marketplaces, allowing per-marketplace control over自动updates
- 添加`current_usage` field到status line input, enabling准确context window percentage calculations
- 修复input being cleared当processing queued commands当user是typing
- 修复prompt suggestions replacing输入input当pressing Tab
- 修复diff view not updating当terminal是resized
- 改进memory usage通过3x用于large conversations
- 改进resolution的stats screenshots copied到clipboard (Ctrl+S)用于crisper images
- 移除# shortcut用于quick memory entry (tell Claude到edit您的CLAUDE.md instead)
- 修复 thinking mode toggle在/config not persisting correctly
- Improve UI用于file creation permission dialog

## 2.0.69

- Minor bugfixes

## 2.0.68

- 修复IME (Input Method 编辑or) support用于languages喜欢Chinese, Japanese,和Korean通过correctly positioning composition window在cursor
- 修复a bug哪里disallowed MCP tools是visible到model
- 修复an issue哪里steering messages可以be lost当subagent是working
- 修复选项+Arrow word navigation treating entire CJK (Chinese, Japanese, Korean) text sequences作为single word instead的navigating通过word boundaries
- 改进plan mode exit UX: show simplified yes/no dialog当exiting使用empty或missing plan instead的throwing error
- Add support用于enterprise managed settings. Contact您的Anthropic account team到enable这feature.

## 2.0.67

- Thinking mode是now enabled通过default用于Opus 4.5
- Thinking mode configuration有moved到/config
- 添加search functionality到`/permissions` command使用`/` keyboard shortcut用于filtering rules通过tool name
- Show reason为什么autoupdater是disabled在`/doctor`
- 修复false "Another process是currently updating Claude" error当running `claude update`当another instance是already在latest version
- 修复MCP servers从`.mcp.json` being stuck在pending state当running在non-interactive mode (`-p` flag或piped input)
- 修复scroll position resetting之后deleting permission rule在`/permissions`
- 修复word deletion (opt+delete)和word navigation (opt+arrow) not工作correctly使用non-Latin text such作为Cyrillic, Greek, Arabic, Hebrew, Thai,和Chinese
- 修复`claude install --force` not bypassing stale lock files
- 修复consecutive @~/ file references在CLAUDE.md being incorrectly parsed due到markdown strikethrough interference
- Windows: 修复ed plugin MCP servers failing due到colons在log directory paths

## 2.0.65

- 添加ability到switch models当writing prompt using alt+p (linux, windows), option+p (macos).
- 添加context window information到status line input
- 添加`fileSuggestion` setting用于custom `@` file search commands
- 添加`CLAUDE_CODE_SHELL` environment variable到override自动shell detection (useful当login shell differs从actual工作shell)
- 修复prompt not being saved到history当aborting query使用Escape
- 修复读取 tool image handling到identify format从bytes instead的file extension

## 2.0.64

- Made auto-compacting instant
- 智能体s和bash commands可以run asynchronously和send messages到wake up主要agent
- /stats现在provides users使用interesting CC stats, such作为favorite model, usage graph, usage streak
- 添加named session support: use `/rename`到name sessions, `/resume <name>`在REPL或`claude --resume <name>`从terminal到resume them
- 添加support用于.claude/rules/`.  See https://code.claude.com/docs/en/memory用于details.
- 添加image dimension metadata当images是resized, enabling准确coordinate mappings用于large images
- 修复auto-loading .env当using native installer
- 修复`--system-prompt` being ignored当using `--continue`或`--resume` flags
- 改进`/resume` screen使用grouped forked sessions和keyboard shortcuts用于preview (P)和rename (R)
- VSCode: Added copy-to-clipboard button在code blocks和bash tool inputs
- VSCode: 修复ed extension not working在Windows ARM64通过falling back到x64 binary via emulation
- Bedrock: Improve efficiency的token counting
- Bedrock: Add support用于`aws login` AWS Management Console credentials
- Unshipped 智能体OutputTool和BashOutputTool,在favor的new unified TaskOutputTool

## 2.0.62

- 添加"(Recommended)" indicator用于multiple-choice questions,使用recommended option moved到top的list
- 添加`attribution` setting到customize commit和PR bylines (deprecates `includeCoAuthoredBy`)
- 修复duplicate slash commands appearing当~/.claude是symlinked到project directory
- 修复slash command selection not working当multiple commands share相同name
- 修复an issue哪里skill files inside symlinked skill directories可以become circular symlinks
- 修复running versions getting removed因为lock file incorrectly going stale
- 修复IDE diff tab not closing当rejecting file changes

## 2.0.61

- 回滚了VSCode support用于multiple terminal clients due到responsiveness issues.

## 2.0.60

- 添加background agent support. 智能体s run在background while您work
- 添加--disable-slash-commands CLI flag到disable所有slash commands
- 添加model name到"Co-Authored-By" commit messages
- 启用d "/mcp enable [server-name]"或"/mcp disable [server-name]"到quickly toggle所有servers
- 更新d 获取到skip summarization用于pre-approved websites
- VSCode: 添加了对multiple terminal clients connecting到IDE server simultaneously

## 2.0.59

- 添加--agent CLI flag到override agent setting用于current session
- 添加`agent` setting到configure主要thread使用specific agent's system prompt, tool restrictions,和model
- VS Code: 修复ed .claude.json config file being read从incorrect location

## 2.0.58

- Pro users now有access到Opus 4.5作为part的their subscription!
- 修复timer duration showing "11m 60s" instead的"12m 0s"
- Windows: Managed settings now更喜欢`C:\Program 文件s\ClaudeCode`如果it exists. Support用于`C:\ProgramData\ClaudeCode`将be removed在future version.

## 2.0.57

- 添加feedback input当rejecting plans, allowing users到tell Claude what到change
- VSCode: Added streaming message support用于real-time response display

## 2.0.56

- 添加setting到enable/disable terminal progress bar (OSC 9;4)
- VSCode Extension: 添加了对VS Code's次要sidebar (VS Code 1.97+), allowing Claude Code到be displayed在right sidebar当keeping file explorer在left. Requires setting sidebar作为Preferred Location在config.

## 2.0.55

- 修复proxy DNS resolution being forced在by default. 否w opt-in via `CLAUDE_CODE_PROXY_RESOLVES_HOSTS=true` environment variable
- 修复keyboard navigation becoming unresponsive当holding down arrow keys在memory location selector
- 改进AskUserQuestion tool到auto-submit single-select questions在last question, eliminating extra review screen用于simple question flows
- 改进fuzzy matching用于`@` file suggestions使用faster,更多accurate results

## 2.0.54

- Hooks: 启用 Permission请求 hooks到process 'always allow' suggestions和apply permission updates
- 修复 issue使用excessive iTerm notifications

## 2.0.52

- 修复duplicate message display当starting Claude使用command line argument
- 修复`/usage` command progress bars到fill up作为usage increases (instead的showing remaining percentage)
- 修复image pasting not working在Linux systems运行Wayland (now falls back到wl-paste当xclip是unavailable)
- 允许一些uses的`$!`在bash commands

## 2.0.51

- 添加Opus 4.5! https://www.anthropic.com/news/claude-opus-4-5
- Introducing Claude Code用于Desktop: https://claude.com/download
- To give您room到try out我们的new model, we've更新usage limits用于Claude Code users. See Claude Opus 4.5 blog用于full details
- Pro users可以now purchase extra usage用于access到Opus 4.5在Claude Code
- Plan 模式现在builds更多precise plans和executes更多thoroughly
- Usage limit notifications现在easier到understand
- 开关ed `/usage` back到"% used"
- 修复handling的thinking errors
- 修复performance regression

## 2.0.50

- 修复bug preventing calling MCP tools that有nested references在their input schemas
- Silenced noisy but harmless error在upgrades
- 改进ultrathink text display
- 改进clarity的5-hour session limit警告message

## 2.0.49

- 添加readline-style ctrl-y用于pasting删除text
- 改进clarity的usage limit警告message
- 修复handling的subagent permissions

## 2.0.47

- 改进error messages和validation用于`claude --teleport`
- 改进error handling在`/usage`
- 修复race condition使用history entry not getting logged在exit
- 修复Vertex AI configuration not being applied从`settings.json`

## 2.0.46

- 修复image files being reported使用incorrect media type当format cannot be detected从metadata

## 2.0.45

- 添加support用于Microsoft Foundry! See https://code.claude.com/docs/en/azure-ai-foundry
- 添加`Permission请求` hook到automatically approve或deny tool permission requests使用custom logic
- Send后台tasks到Claude Code在web通过starting message使用`&`

## 2.0.43

- 添加`permission模式` field用于custom agents
- 添加`tool_use_id` field到`PreToolUseHookInput`和`PostToolUseHookInput` types
- 添加skills frontmatter field到declare skills到auto-load用于subagents
- 添加the `Subagent启动` hook event
- 修复nested `CLAUDE.md` files not loading当@-mentioning files
- 修复duplicate rendering的some messages在UI
- 修复some visual flickers
- 修复否tebook编辑 tool inserting cells在incorrect positions当cell IDs matched pattern `cell-N`

## 2.0.42

- 添加`agent_id`和`agent_transcript_path` fields到`Subagent停止` hooks.

## 2.0.41

- 添加`model` parameter到prompt-based stop hooks, allowing users到specify自定义model用于hook evaluation
- 修复slash commands从user settings being loaded twice, which可以cause rendering issues
- 修复incorrect labeling的user settings vs project settings在command descriptions
- 修复crash当plugin command hooks timeout在execution
- 修复ed: Bedrock users不longer see重复Opus entries在/model picker当using `--model haiku`
- 修复broken security documentation links在trust dialogs和onboarding
- 修复issue哪里pressing ESC到close diff modal将also interrupt model
- ctrl-r history search landing在slash command不longer cancels search
- SDK: Support自定义timeouts用于hooks
- 允许更多safe git commands到run without approval
- 插件s: 添加了对sharing和installing output styles
- Teleporting session从web将automatically set upstream branch

## 2.0.37

- 修复how idleness是computed用于notifications
- Hooks: Added matcher values用于否tification hook events
- Output Styles: Added `keep-coding-instructions` option到frontmatter

## 2.0.36

- 修复ed: DISABLE_AUTOUPDATER environment variable现在properly disables package manager update notifications
- 修复queued messages being incorrectly executed作为bash commands
- 修复input being lost当typing当queued message是processed

## 2.0.35

- Improve fuzzy search results当searching commands
- 改进VS Code extension到respect `chat.fontSize`和`chat.fontFamily` settings throughout entire UI,和apply font changes immediately without requiring reload
- 添加`CLAUDE_CODE_EXIT_AFTER_STOP_DELAY` environment variable到automatically exit SDK mode之后specified idle duration, useful用于automated workflows和scripts
- Migrated `ignorePatterns`从project config到deny permissions在localSettings.
- 修复menu navigation getting stuck在items使用empty string或other falsy values (e.g.,在`/hooks` menu)

## 2.0.34

- VSCode Extension: Added setting到configure initial permission mode用于new conversations
- 改进file path suggestion performance使用native Rust-based fuzzy finder
- 修复infinite token refresh loop那caused MCP servers使用OAuth (e.g., Slack)到hang在connection
- 修复memory crash当reading或writing large files (especially base64-encoded images)

## 2.0.33

- Native binary installs现在launch quicker.
- 修复`claude doctor` incorrectly detecting Homebrew vs npm-global installations通过properly resolving symlinks
- 修复`claude mcp serve` exposing tools使用incompatible outputSchemas

## 2.0.32

- Un-deprecate output styles based在community feedback
- 添加`companyAnnouncements` setting用于displaying announcements在startup
- 修复hook progress messages not updating correctly在PostToolUse hook execution

## 2.0.31

- Windows: native installation uses shift+tab作为shortcut用于mode switching, instead的alt+m
- Vertex: add support用于Web 搜索在supported models
- VSCode: Adding respectGit忽略 configuration到include .gitignored files在file searches (defaults到true)
- 修复a bug使用subagents和MCP servers related到"Tool names必须be unique" error
- 修复issue causing `/compact`到fail使用`prompt_too_long`通过making它respect existing compact boundaries
- 修复plugin uninstall not removing plugins

## 2.0.30

- 添加helpful hint到run `security unlock-keychain`当encountering API key errors在macOS使用locked keychain
- 添加`allowUnsandboxedCommands` sandbox setting到disable dangerously禁用Sandbox escape hatch在policy level
- 添加`disallowedTools` field到custom agent definitions用于explicit tool blocking
- 添加prompt-based stop hooks
- VSCode: Added respectGit忽略 configuration到include .gitignored files在file searches (defaults到true)
- 启用d SSE MCP servers在native build
- 弃用output styles. Review options在`/output-style`和use --system-prompt-file, --system-prompt, --append-system-prompt, CLAUDE.md,或plugins instead
- 移除support用于custom ripgrep configuration, resolving issue哪里搜索 returns不results和config discovery fails
- 修复Explore agent creating unwanted .md investigation files在codebase exploration
- 修复a bug哪里`/context`将sometimes fail使用"max_tokens必须be greater than thinking.budget_tokens"错误message
- 修复`--mcp-config` flag到correctly override file-based MCP configurations
- 修复bug那saved session permissions到local settings
- 修复MCP tools not being available到sub-agents
- 修复hooks和plugins not executing当using --dangerously-skip-permissions flag
- 修复delay当navigating through typeahead suggestions使用arrow keys
- VSCode: 恢复d selection indicator在input footer showing当前file或code selection status

## 2.0.28

- Plan mode: introduced新Plan subagent
- Subagents: claude可以now choose到resume subagents
- Subagents: claude可以dynamically choose model used通过its subagents
- SDK:添加--max-budget-usd flag
- Discovery的custom slash commands, subagents,和output styles不longer respects .gitignore
- 停止 `/terminal-setup`从adding backslash到`Shift + 输入`在VS Code
- Add branch和tag support用于git-based plugins和marketplaces using fragment syntax (e.g., `owner/repo#branch`)
- 修复a bug哪里macOS permission prompts将show up upon initial launch当launching从home directory
- Various其他bug fixes

## 2.0.27

- New UI用于permission prompts
- 添加current branch filtering和search到session resume screen用于easier navigation
- 修复directory @-mention causing "否 assistant message found" error
- VSCode Extension: Add config setting到include .gitignored files在file searches
- VSCode Extension: 错误 fixes用于unrelated 'Warmup' conversations,和configuration/settings occasionally being reset到defaults

## 2.0.25

- 移除legacy SDK entrypoint. Please migrate到@anthropic-ai/claude-agent-sdk用于future SDK updates: https://platform.claude.com/docs/en/agent-sdk/migration-guide

## 2.0.24

- 修复a bug哪里project-level skills是not loading当--setting-sources 'project'是specified
- Claude Code Web: Support用于Web -> CLI teleport
- Sandbox: Releasing sandbox mode用于BashTool在Linux & Mac
- Bedrock: Display awsAuthRefresh output当auth是required

## 2.0.22

- 修复content layout shift当scrolling through slash commands
- IDE: Add toggle到enable/disable thinking.
- 修复 bug causing重复permission prompts使用parallel tool calls
- Add support用于enterprise managed MCP allowlist和denylist

## 2.0.21

- Support MCP `structuredContent` field在tool responses
- 添加an interactive question tool
- Claude将now ask您questions更多often在plan mode
- 添加Haiku 4.5作为model option用于Pro users
- 修复an issue哪里queued commands don't有access到previous messages' output

## 2.0.20

- 添加support用于Claude 技能s

## 2.0.19

- Auto-background long-running bash commands instead的killing them. Customize使用BASH_DEFAULT_TIMEOUT_MS
- 修复a bug哪里Haiku是unnecessarily called在print mode

## 2.0.17

- 添加Haiku 4.5到model selector!
- Haiku 4.5 automatically uses Sonnet在plan mode,和Haiku用于execution (i.e. SonnetPlan通过default)
- 3P (Bedrock和Vertex)是not automatically upgraded yet. Manual upgrading可以be done through setting `ANTHROPIC_DEFAULT_HAIKU_MODEL`
- Introducing Explore subagent. Powered通过Haiku it'll search through您的codebase efficiently到save context!
- OTEL: support HTTP_PROXY和HTTPS_PROXY
- `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC`现在disables release notes fetching

## 2.0.15

- 修复bug使用resuming哪里previously创建files needed到be read again之前writing
- 修复bug使用`-p` mode哪里@-mentioned files needed到be read again之前writing

## 2.0.14

- 修复 @-mentioning MCP servers到toggle them on/off
- Improve permission checks用于bash使用inline env vars
- 修复 ultrathink + thinking toggle
- Reduce unnecessary logins
- Document --system-prompt
- Several improvements到rendering
- 插件s UI polish

## 2.0.13

- 修复`/plugin` not working在native build

## 2.0.12

- **插件 System 释放d**: Extend Claude Code使用custom commands, agents, hooks,和MCP servers从marketplaces
- `/plugin install`, `/plugin enable/disable`, `/plugin marketplace` commands用于plugin management
- Repository-level plugin configuration via `extraKnownMarketplaces`用于team collaboration
- `/plugin validate` command用于validating plugin structure和configuration
- 插件 announcement blog post在https://www.anthropic.com/news/claude-code-plugins
- 插件 documentation available在https://code.claude.com/docs/en/plugins
- Comprehensive错误messages和diagnostics via `/doctor` command
- Avoid flickering在`/model` selector
- Improvements到`/help`
- Avoid mentioning hooks在`/resume` summaries
- Changes到"verbose" setting在`/config`现在persist across sessions

## 2.0.11

- 减少了system prompt size通过1.4k tokens
- IDE: 修复ed keyboard shortcuts和focus issues用于smoother interaction
- 修复Opus fallback rate limit errors appearing incorrectly
- 修复/add-dir command selecting错误default tab

## 2.0.10

- Rewrote terminal renderer用于buttery smooth UI
- 启用/disable MCP servers通过@mentioning,或in /mcp
- 添加tab completion用于shell commands在bash mode
- PreToolUse hooks可以now modify tool inputs
- 按下 Ctrl-G到edit您的prompt在your system's配置text editor
- 修复es用于bash permission checks使用environment variables在command

## 2.0.9

- 修复 regression哪里bash backgrounding停止working

## 2.0.8

- 更新 Bedrock默认Sonnet model到`global.anthropic.claude-sonnet-4-5-20250929-v1:0`
- IDE: Add drag-and-drop support用于files和folders在chat
- /context: 修复 counting用于thinking blocks
- Improve message rendering用于users使用light themes在dark terminals
- Remove deprecated .claude.json allowedTools, ignorePatterns, env,和todoFeature启用d config options (instead, configure these在your settings.json)

## 2.0.5

- IDE: 修复 IME unintended message submission使用输入和Tab
- IDE: Add "打开在Terminal" link在login screen
- 修复 unhandled OAuth expiration 401 API errors
- SDK: Added SDKUser消息Replay.isReplay到prevent重复messages

## 2.0.1

- 跳过 Sonnet 4.5默认model setting change用于Bedrock和Vertex
- Various bug fixes和presentation improvements

## 2.0.0

- New native VS Code extension
- Fresh coat的paint throughout whole app
- /rewind conversation到undo code changes
- /usage command到see plan limits
- Tab到toggle thinking (sticky across sessions)
- Ctrl-R到search history
- Unshipped claude config command
- Hooks: Reduced PostToolUse 'tool_use' ids是found without 'tool_result' blocks errors
- SDK: The Claude Code SDK是now Claude 智能体 SDK
- Add subagents dynamically使用`--agents` flag

## 1.0.126

- 启用 /context command用于Bedrock和Vertex
- Add mTLS support用于HTTP-based 打开Telemetry exporters

## 1.0.124

- Set `CLAUDE_BASH_NO_LOGIN` environment variable到1或true到to skip login shell用于BashTool
- 修复 Bedrock和Vertex environment variables evaluating所有strings作为truthy
- 否 longer inform Claude的list的allowed tools当permission是denied
- 修复security vulnerability在Bash tool permission checks
- 改进VSCode extension performance用于large files

## 1.0.123

- Bash permission rules现在support output redirections当matching (e.g., `Bash(python:*)` matches `python script.py > output.txt`)
- 修复thinking mode triggering在negation phrases喜欢"don't think"
- 修复rendering performance degradation在token streaming
- 添加SlashCommand tool,哪个enables Claude到invoke您的slash commands. https://code.claude.com/docs/en/slash-commands#SlashCommand-tool
- Enhanced BashTool environment snapshot logging
- 修复a bug哪里resuming conversation在headless mode将sometimes enable thinking unnecessarily
- Migrated --debug logging到file,到enable容易tailing & filtering

## 1.0.120

- 修复 input lag在typing, especially noticeable使用large prompts
- 改进VSCode extension command registry和sessions dialog user experience
- Enhanced sessions dialog responsiveness和visual feedback
- 修复IDE compatibility issue通过removing worktree support check
- 修复security vulnerability哪里Bash tool permission checks可以be bypassed using prefix matching

## 1.0.119

- 修复 Windows issue哪里process visually freezes在entering interactive mode
- Support dynamic headers用于MCP servers via headersHelper configuration
- 修复 thinking mode not working在headless sessions
- 修复 slash commands现在properly update允许tools instead的replacing them

## 1.0.117

- Add Ctrl-R history search到recall上一个commands喜欢bash/zsh
- 修复 input lag当typing, especially在Windows
- Add sed command到auto-allowed commands在accept编辑s mode
- 修复 Windows PATH comparison到be case-insensitive用于drive letters
- Add permissions management hint到/add-dir output

## 1.0.115

- Improve thinking mode display使用enhanced visual effects
- 输入 /t到temporarily disable thinking mode在your prompt
- Improve path validation用于glob和grep tools
- Show condensed output用于post-tool hooks到reduce visual clutter
- 修复 visual feedback当loading state completes
- Improve UI consistency用于permission request dialogs

## 1.0.113

- 弃用piped input在interactive mode
- 移动 Ctrl+R keybinding用于toggling transcript到Ctrl+O

## 1.0.112

- Transcript mode (Ctrl+R): Added model used到generate每个assistant message
- Addressed issue where一些Claude Max users是incorrectly recognized作为Claude Pro users
- Hooks: Added system消息 support用于会话End hooks
- 添加`spinnerTips启用d` setting到disable spinner tips
- IDE: Various improvements和bug fixes

## 1.0.111

- /model现在validates provided model names
- 修复Bash tool crashes caused通过malformed shell syntax parsing

## 1.0.110

- /terminal-setup command现在supports WezTerm
- MCP: OAuth tokens现在proactively refresh之前expiration
- 修复reliability issues使用background Bash processes

## 1.0.109

- SDK: Added partial message streaming support via `--include-partial-messages` CLI flag

## 1.0.106

- Windows: 修复ed path permission matching到consistently use POSIX format (e.g., `读取(//c/Users/...)`)

## 1.0.97

- Settings: /doctor现在validates permission rule syntax和suggests corrections

## 1.0.94

- Vertex: add support用于global endpoints用于supported models
- /memory command现在allows direct editing的all imported memory files
- SDK: Add自定义tools作为callbacks
- 添加/todos command到list当前todo items

## 1.0.93

- Windows: Add alt + v shortcut用于pasting images从clipboard
- Support NO_PROXY environment variable到bypass proxy用于specified hostnames和IPs

## 1.0.90

- Settings file changes take effect immediately -不restart required

## 1.0.88

- 修复issue causing "OAuth authentication是currently not supported"
- 状态 line input现在includes `exceeds_200k_tokens`
- 修复incorrect usage tracking在/cost.
- Introduced `ANTHROPIC_DEFAULT_SONNET_MODEL`和`ANTHROPIC_DEFAULT_OPUS_MODEL`用于controlling model aliases opusplan, opus,和sonnet.
- Bedrock: 更新d默认Sonnet model到Sonnet 4

## 1.0.86

- 添加/context到help users self-serve调试context issues
- SDK: Added UUID support用于all SDK messages
- SDK: Added `--replay-user-messages`到replay user messages back到stdout

## 1.0.85

- 状态 line input现在includes session cost info
- Hooks: Introduced 会话End hook

## 1.0.84

- 修复 tool_use/tool_result id mismatch error当network是unstable
- 修复 Claude sometimes ignoring real-time steering当wrapping up task
- @-mention: Add ~/.claude/\* files到suggestions用于easier agent, output style,和slash command editing
- Use built-in ripgrep通过default;到opt out的this behavior, set USE_BUILTIN_RIPGREP=0

## 1.0.83

- @-mention: Support files使用spaces在path
- New shimmering spinner

## 1.0.82

- SDK: Add request cancellation support
- SDK: New additionalDirectories option到search自定义paths,改进slash command processing
- Settings: Validation prevents无效fields在.claude/settings.json files
- MCP: Improve tool name consistency
- Bash: 修复 crash当Claude tries到automatically read large files

## 1.0.81

- 释放d output styles, including新built-in educational output styles "Explanatory"和"Learning". Docs: https://code.claude.com/docs/en/output-styles
- 智能体s: 修复自定义agent loading当agent files是unparsable

## 1.0.80

- UI improvements: 修复 text contrast用于custom subagent colors和spinner rendering issues

## 1.0.77

- Bash tool: 修复 heredoc和multiline string escaping, improve stderr redirection handling
- SDK: Add session support和permission denial tracking
- 修复 token limit errors在conversation summarization
- Opus Plan 模式: New setting在`/model`到run Opus only在plan mode, Sonnet otherwise

## 1.0.73

- MCP: Support multiple config files使用`--mcp-config file1.json file2.json`
- MCP: 按下 Esc到cancel OAuth authentication flows
- Bash: Improved command validation和reduced假security warnings
- UI: Enhanced spinner animations和status line visual hierarchy
- Linux: 添加了对Alpine和musl-based distributions (requires separate ripgrep installation)

## 1.0.72

- Ask permissions:有Claude Code always ask用于confirmation到use特定tools使用/permissions

## 1.0.71

- Background commands: (Ctrl-b)到run任何Bash command在background所以Claude可以keep工作(great用于dev servers, tailing logs, etc.)
- Customizable status line: add您的terminal prompt到Claude Code使用/statusline

## 1.0.70

- Performance: Optimized message rendering用于better performance使用large contexts
- Windows: 修复ed native file search, ripgrep,和subagent functionality
- 添加support用于@-mentions在slash command arguments

## 1.0.69

- 升级d Opus到version 4.1

## 1.0.68

- 修复不正确model names being used用于certain commands喜欢`/pr-comments`
- Windows: improve permissions checks用于allow / deny tools和project trust. This可能create新project entry在`.claude.json` - manually merge history field如果desired.
- Windows: improve sub-process spawning到eliminate "否这样的file或directory"当running commands喜欢pnpm
- Enhanced /doctor command使用CLAUDE.md和MCP tool context用于self-serve debugging
- SDK: Added canUseTool callback support用于tool confirmation
- 添加`disableAllHooks` setting
- 改进file suggestions performance在large repos

## 1.0.65

- IDE: 修复ed connection stability issues和error handling用于diagnostics
- Windows: 修复ed shell environment setup用于users without .bashrc files

## 1.0.64

- 智能体s: Added model customization support -您can现在specify哪个model agent应该use
- 智能体s: 修复ed unintended access到recursive agent tool
- Hooks: Added system消息 field到hook JSON output用于displaying warnings和context
- SDK: 修复ed user input tracking across multi-turn conversations
- 添加hidden files到file search和@-mention suggestions

## 1.0.63

- Windows: 修复ed file search, @agent mentions,和custom slash commands functionality

## 1.0.62

- 添加@-mention support使用typeahead用于custom agents. @<your-custom-agent>到invoke it
- Hooks: Added 会话启动 hook用于new session initialization
- /add-dir command现在supports typeahead用于directory paths
- 改进network connectivity check reliability

## 1.0.61

- Transcript mode (Ctrl+R): Changed Esc到exit transcript mode宁愿than interrupt
- Settings: Added `--settings` flag到load settings从JSON file
- Settings: 修复ed resolution的settings files paths that是symlinks
- OTEL: 修复ed reporting的wrong organization之后authentication changes
- Slash commands: 修复ed permissions checking用于allowed-tools使用Bash
- IDE: 添加了对pasting images在VSCode MacOS using ⌘+V
- IDE: Added `CLAUDE_CODE_AUTO_CONNECT_IDE=false`用于disabling IDE auto-connection
- 添加`CLAUDE_CODE_SHELL_PREFIX`用于wrapping Claude和user-provided shell commands run通过Claude Code

## 1.0.60

- You可以now create自定义subagents用于specialized tasks! Run /agents到get started

## 1.0.59

- SDK: Added tool confirmation support使用canUseTool callback
- SDK: 允许 specifying env用于spawned process
- Hooks: Exposed PermissionDecision到hooks (including "ask")
- Hooks: User提示提交现在supports additional上下文在advanced JSON output
- 修复issue where一些Max users那specified Opus将still see fallback到Sonnet

## 1.0.58

- 添加support用于reading PDFs
- MCP: Improved server health status display在'claude mcp list'
- Hooks: Added CLAUDE_PROJECT_DIR env var用于hook commands

## 1.0.57

- 添加support用于specifying model在slash commands
- 改进permission messages到help Claude understand允许tools
- 修复: Remove trailing newlines从bash output在terminal wrapping

## 1.0.56

- Windows: 启用d shift+tab用于mode switching在versions的否de.js那support terminal VT mode
- 修复es用于WSL IDE detection
- 修复 issue causing awsRefreshHelper changes到.aws directory not到be picked up

## 1.0.55

- Clarified knowledge cutoff用于Opus 4和Sonnet 4 models
- Windows:修复Ctrl+Z crash
- SDK: 添加了bility到capture错误logging
- Add --system-prompt-file option到override system prompt在print mode

## 1.0.54

- Hooks: Added User提示提交 hook和current工作directory到hook inputs
- Custom slash commands: 添加了rgument-hint到frontmatter
- Windows: OAuth uses port 45454和properly constructs browser URL
- Windows: mode switching现在uses alt + m,和plan mode renders properly
- Shell: 开关到in-memory shell snapshot到fix file-related errors

## 1.0.53

- 更新d @-mention file truncation从100 lines到2000 lines
- Add helper script settings用于AWS token refresh: awsAuthRefresh (for前台operations喜欢aws sso login)和awsCredential导出 (for后台operation使用STS-like response).

## 1.0.52

- 添加support用于MCP server instructions

## 1.0.51

- 添加support用于native Windows (requires Git用于Windows)
- 添加support用于Bedrock API keys through environment variable AWS_BEARER_T确定EN_BEDROCK
- Settings: /doctor可以now help您identify和fix无效setting files
- `--append-system-prompt`可以now be used在interactive mode, not刚刚--print/-p.
- 提高了auto-compact警告threshold从60%到80%
- 修复an issue使用handling user directories使用spaces用于shell snapshots
- OTEL resource现在includes os.type, os.version, host.arch,和wsl.version (if running在Windows Subsystem用于Linux)
- Custom slash commands: 修复ed user-level commands在subdirectories
- Plan mode: 修复了问题哪里rejected plan从sub-task将get discarded

## 1.0.48

- 修复a bug在v1.0.45哪里app将sometimes freeze在launch
- 添加progress messages到Bash tool based在last 5 lines的command output
- 添加expanding variables support用于MCP server configuration
- 移动d shell snapshots从/tmp到~/.claude用于more可靠Bash tool calls
- 改进IDE extension path handling当Claude Code runs在WSL
- Hooks: 添加了 PreCompact hook
- Vim mode: Added c, f/F, t/T

## 1.0.45

- Redesigned 搜索 (Grep) tool使用new tool input parameters和features
- 禁用d IDE diffs用于notebook files, fixing "超时 waiting之后1000ms" error
- 修复config file corruption issue通过enforcing atomic writes
- 更新d prompt input undo到Ctrl+\_到avoid breaking existing Ctrl+U behavior, matching zsh's undo shortcut
- 停止 Hooks: 修复ed transcript path之后/clear和fixed triggering当loop ends使用tool call
- Custom slash commands: 恢复d namespacing在command names based在subdirectories. For example, .claude/commands/frontend/component.md是now /frontend:component, not /component.

## 1.0.44

- New /export command lets您quickly export conversation用于sharing
- MCP: resource_link tool results是now supported
- MCP: tool annotations和tool titles现在display在/mcp view
- 更改Ctrl+Z到suspend Claude Code. 恢复通过running `fg`. 提示 input undo是now Ctrl+U.

## 1.0.43

- 修复a bug哪里theme selector是saving excessively
- Hooks: Added EPIPE system错误handling

## 1.0.42

- 添加tilde (`~`) expansion support到`/add-dir` command

## 1.0.41

- Hooks: Split 停止 hook triggering into 停止和Subagent停止
- Hooks: 启用d可选timeout configuration用于each command
- Hooks: Added "hook_event_name"到hook input
- 修复a bug哪里MCP tools将display twice在tool list
- New tool parameters JSON用于Bash tool在`tool_decision` event

## 1.0.40

- 修复a bug causing API connection errors使用UNABLE_TO_GET_ISSUER_CERT_LOCALLY如果`NODE_EXTRA_CA_CERTS`是set

## 1.0.39

- New 活动 Time metric在打开Telemetry logging

## 1.0.38

- 释放d hooks. Special thanks到community input在https://github.com/anthropics/claude-code/issues/712. Docs: https://code.claude.com/docs/en/hooks

## 1.0.37

- Remove ability到set `Proxy-Authorization` header via ANTHROPIC_AUTH_T确定EN或apiKeyHelper

## 1.0.36

- Web search现在takes today's date into context
- 修复a bug哪里stdio MCP servers是not terminating properly在exit

## 1.0.35

- 添加support用于MCP OAuth Authorization Server discovery

## 1.0.34

- 修复a memory leak causing MaxListenersExceeded警告 message到appear

## 1.0.33

- 改进logging functionality使用session ID support
- 添加prompt input undo functionality (Ctrl+Z和vim 'u' command)
- Improvements到plan mode

## 1.0.32

- 更新d loopback config用于litellm
- 添加force日志inMethod setting到bypass login selection screen

## 1.0.31

- 修复a bug哪里~/.claude.json将get reset当file contained无效JSON

## 1.0.30

- Custom slash commands: Run bash output, @-mention files, enable thinking使用thinking keywords
- 改进file path autocomplete使用filename matching
- 添加timestamps在Ctrl-r mode和fixed Ctrl-c handling
- Enhanced jq regex support用于complex filters使用pipes和select

## 1.0.29

- 改进CJK character support在cursor navigation和rendering

## 1.0.28

- Slash commands: 修复 selector display在history navigation
- Resizes images之前upload到prevent API size limit errors
- 添加XDG_CONFIG_HOME support到configuration directory
- Performance optimizations用于memory usage
- New attributes (terminal.type, language)在打开Telemetry logging

## 1.0.27

- 流able HTTP MCP servers是now supported
- Remote MCP servers (SSE和HTTP)现在support OAuth
- MCP resources可以now be @-mentioned
- /resume slash command到switch conversations within Claude Code

## 1.0.25

- Slash commands: moved "project"和"user" prefixes到descriptions
- Slash commands:改进reliability用于command discovery
- 改进support用于Ghostty
- 改进web search reliability

## 1.0.24

- 改进/mcp output
- 修复a bug哪里settings arrays got overwritten instead的merged

## 1.0.23

- 释放d 输入Script SDK: import @anthropic-ai/claude-code到get started
- 释放d Python SDK: pip install claude-code-sdk到get started

## 1.0.22

- SDK: 重命名d `total_cost`到`total_cost_usd`

## 1.0.21

- 改进editing的files使用tab-based indentation
- 修复用于tool_use without matching tool_result errors
- 修复a bug哪里stdio MCP server processes将linger之后quitting Claude Code

## 1.0.18

- 添加--add-dir CLI argument用于specifying additional工作directories
- 添加streaming input support without require -p flag
- 改进startup performance和session storage performance
- 添加CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR environment variable到freeze工作directory用于bash commands
- 添加detailed MCP server tools display (/mcp)
- MCP authentication和permission improvements
- 添加auto-reconnection用于MCP SSE connections在disconnect
- 修复issue哪里pasted content是lost当dialogs appeared

## 1.0.17

- We现在emit messages从sub-tasks在-p mode (look用于parent_tool_use_id property)
- 修复crashes当VS Code diff tool是invoked multiple times quickly
- MCP server list UI improvements
- 更新 Claude Code process title到display "claude" instead的"node"

## 1.0.11

- Claude Code可以now也be used使用Claude Pro subscription
- 添加/upgrade用于smoother switching到Claude Max plans
- 改进UI用于authentication从API keys和Bedrock/Vertex/external auth tokens
- 改进shell configuration错误handling
- 改进todo list handling在compaction

## 1.0.10

- 添加markdown table support
- 改进streaming performance

## 1.0.8

- 修复Vertex AI region fallback当using CLOUD_ML_REGION
- 提高了default otel interval从1s -> 5s
- 修复edge cases哪里MCP_TIMEOUT和MCP_TOOL_TIMEOUT weren't being respected
- 修复a regression哪里search tools unnecessarily asked用于permissions
- 添加support用于triggering thinking non-English languages
- 改进compacting UI

## 1.0.7

- 重命名d /allowed-tools -> /permissions
- Migrated allowedTools和ignorePatterns从.claude.json -> settings.json
- 弃用claude config commands在favor的editing settings.json
- 修复a bug哪里--dangerously-skip-permissions sometimes didn't work在--print mode
- 改进error handling用于/install-github-app
- 错误fixes, UI polish,和tool reliability improvements

## 1.0.6

- 改进edit reliability用于tab-indented files
- Respect CLAUDE_CONFIG_DIR everywhere
- 减少了unnecessary tool permission prompts
- 添加support用于symlinks在@file typeahead
- 错误fixes, UI polish,和tool reliability improvements

## 1.0.4

- 修复a bug哪里MCP tool errors weren't being parsed correctly

## 1.0.1

- 添加`DISABLE_INTERLEAVED_THINKING`到give users option到opt out的interleaved thinking.
- 改进model references到show provider-specific names (Sonnet 3.7用于Bedrock, Sonnet 4用于Console)
- 更新d documentation links和OAuth process descriptions

## 1.0.0

- Claude Code是now generally available
- Introducing Sonnet 4和Opus 4 models

## 0.2.125

- 破坏性变更： Bedrock ARN passed到`ANTHROPIC_MODEL`或`ANTHROPIC_SMALL_FAST_MODEL`应该no longer contain escaped slash (specify `/` instead的`%2F`)
- 移除`DEBUG=true`在favor的`ANTHROPIC_LOG=debug`,到log所有requests

## 0.2.117

- 破坏性变更： --print JSON output现在returns nested message objects,用于forwards-compatibility作为we introduce新metadata fields
- Introduced settings.cleanupPeriodDays
- Introduced CLAUDE_CODE_API_KEY_HELPER_TTL_MS env var
- Introduced --debug mode

## 0.2.108

- You可以now send messages到Claude while它works到steer Claude在real-time
- Introduced BASH_DEFAULT_TIMEOUT_MS和BASH_MAX_TIMEOUT_MS env vars
- 修复a bug哪里thinking是not working在-p mode
- 修复a regression在/cost reporting
- 弃用MCP wizard interface在favor的other MCP commands
- Lots的other bugfixes和improvements

## 0.2.107

- CLAUDE.md files可以now import其他files. Add @path/to/file.md到./CLAUDE.md到load additional files在launch

## 0.2.106

- MCP SSE server configs可以now specify自定义headers
- 修复a bug哪里MCP permission prompt didn't always show correctly

## 0.2.105

- Claude可以now search web
- 移动d system & account status到/status
- 添加word movement keybindings用于Vim
- 改进latency用于startup, todo tool,和file edits

## 0.2.102

- 改进thinking triggering reliability
- 改进@mention reliability用于images和folders
- You可以now paste multiple large chunks into one prompt

## 0.2.100

- 修复a crash caused通过stack overflow error
- Made db storage optional; missing db support disables --continue和--resume

## 0.2.98

- 修复an issue哪里auto-compact是running twice

## 0.2.96

- Claude Code可以now也be used使用Claude Max subscription (https://claude.ai/upgrade)

## 0.2.93

- 恢复 conversations从where您left off从with "claude --continue"和"claude --resume"
- Claude now有access到Todo list那helps它stay在track和be更多organized

## 0.2.82

- 添加support用于--disallowedTools
- 重命名d tools用于consistency: LSTool -> LS, View -> 读取, etc.

## 0.2.75

- Hit 输入到queue up additional messages当Claude是working
- 拖动 in或copy/paste image files directly into prompt
- @-mention files到directly add them到context
- Run one-off MCP servers使用`claude --mcp-config <path-to-file>`
- 改进performance用于filename auto-complete

## 0.2.74

- 添加support用于refreshing dynamically generated API keys (via apiKeyHelper),使用5 minute TTL
- Task tool可以now perform writes和run bash commands

## 0.2.72

- 更新d spinner到indicate tokens loaded和tool usage

## 0.2.70

- Network commands喜欢curl是now available用于Claude到use
- Claude可以now run multiple web queries在parallel
- 按下ing ESC once immediately interrupts Claude在Auto-accept mode

## 0.2.69

- 修复UI glitches使用improved 选择 component behavior
- Enhanced terminal output display使用better text truncation logic

## 0.2.67

- Shared project permission rules可以be saved在.claude/settings.json

## 0.2.66

- Print mode (-p)现在supports streaming output via --output-format=stream-json
- 修复issue哪里pasting可以trigger memory或bash mode unexpectedly

## 0.2.63

- 修复an issue哪里MCP tools是loaded twice,哪个caused tool call errors

## 0.2.61

- Navigate menus使用vim-style keys (j/k)或bash/emacs shortcuts (Ctrl+n/p)用于faster interaction
- Enhanced image detection用于more可靠clipboard paste functionality
- 修复an issue哪里ESC key可以crash conversation history selector

## 0.2.59

- 复制+paste images directly into您的prompt
- 改进progress indicators用于bash和fetch tools
- 错误fixes用于non-interactive mode (-p)

## 0.2.54

- Quickly add到Memory通过starting您的message使用'#'
- 按下 ctrl+r到see full output用于long tool results
- 添加support用于MCP SSE transport

## 0.2.53

- New web fetch tool lets Claude view URLs那you paste in
- 修复a bug使用JPEG detection

## 0.2.50

- New MCP "project" scope现在allows you到add MCP servers到.mcp.json files和commit them到your repository

## 0.2.49

- Previous MCP server scopes有been renamed:上一个"project" scope是now "local"和"global" scope是now "user"

## 0.2.47

- 按下 Tab到auto-complete file和folder names
- 按下 Shift + Tab到toggle auto-accept用于file edits
- Automatic conversation compaction用于infinite conversation length (toggle使用/config)

## 0.2.44

- Ask Claude到make plan使用thinking mode:刚刚say 'think'或'think harder'或even 'ultrathink'

## 0.2.41

- MCP server startup timeout可以now be配置via MCP_TIMEOUT environment variable
- MCP server startup不longer blocks app从starting up

## 0.2.37

- New /release-notes command lets您view release notes在any time
- `claude config add/remove` commands现在accept multiple values separated通过commas或spaces

## 0.2.36

- 导入 MCP servers从Claude Desktop使用`claude mcp add-from-claude-desktop`
- Add MCP servers作为JSON strings使用`claude mcp add-json <n> <json>`

## 0.2.34

- Vim bindings用于text input - enable使用/vim或/config

## 0.2.32

- Interactive MCP setup wizard: Run "claude mcp add"到add MCP servers使用step-by-step interface
- 修复用于some PersistentShell issues

## 0.2.31

- Custom slash commands: Markdown files在.claude/commands/ directories现在appear作为custom slash commands到insert prompts into您的conversation
- MCP调试mode: Run使用--mcp-debug flag到get更多information about MCP server errors

## 0.2.30

- 添加ANSI color theme用于better terminal compatibility
- 修复issue哪里slash command arguments weren't being sent properly
- (Mac-only) API keys是now stored在macOS Keychain

## 0.2.26

- New /approved-tools command用于managing tool permissions
- Word-level diff display用于improved code readability
- Fuzzy matching用于slash commands

## 0.2.21

- Fuzzy matching用于/commands
