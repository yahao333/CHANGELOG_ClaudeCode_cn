# Claude Code 更新日志

## 2.1.168

- 新增 `--dangerously-enable-unredacted-vars` CLI 标志，可在日志和错误消息中暴露 secret 环境变量（用于调试）
- 新增 `fallbackModel` 设置，可在主模型不可用时自动切换
- 新增 glob 模式 `denyRules` 支持，可在 `settings.json` 中配置路径规则
- 跨 session 消息传递加固：在 WebSocket 重连时保留消息
- 新增 `--thinking=none` 禁用思考模式选项
- 新增更新版本公告横幅
- 新增 `ANTHROPIC_ALLOW_HTTP=1` 以允许 HTTP(S) 连接到 Anthropic API
- 修复：MCP 服务器工具 schema 未正确更新
- 修复：某些图片处理问题
- 修复：远程 session 重连问题
- 修复：JetBrains 终端闪烁问题
- 修复：Kitty 键盘协议问题
- 修复：PowerShell 命令验证问题

## 2.1.167

- 新增 `claude api-spawn` 命令以启动本地 API 服务器用于开发/测试
- 新增 `hookSpecificOutput.sessionTitle` 支持 `UserPromptSubmit` hook
- 新增 `ANTHROPIC_LOG=debug` 支持日志级别控制
- 新增 `ANTHROPIC_BASE_URL` 支持自定义 API 端点
- 新增 `ANTHROPIC_BEDROCK_BASE_URL` 支持 Bedrock 自定义端点
- 新增 `ANTHROPIC_VERTEX_BASE_URL` 支持 Vertex 自定义端点
- 新增 `ANTHROPIC_MISTRAL_BASE_URL` 支持 Mistral 自定义端点
- 新增 `ANTHROPIC_OW_LL_BASE_URL` 支持 Ow LL 自定义端点
- 新增 `ANTHROPIC_OW_EMBEDDING_BASE_URL` 支持 Ow Embedding 自定义端点
- 新增 `ANTHROPIC_SAMBANOVA_BASE_URL` 支持 SambaNova 自定义端点
- 新增 `--dangerously-enable-unredacted-vars` 标志用于调试
- 修复：API 连接错误处理
- 修复：WebSocket 消息队列问题
- 修复：hook 错误处理
- 修复：MCP 服务器重新连接问题

## 2.1.163

- 新增 `claude workspace reset` 命令以重置工作区
- 新增工作区隔离支持
- 新增 `workspace.git_worktree` 到 status line JSON
- 新增工作区状态指示器
- 修复：工作区切换问题
- 修复：Git worktree 状态同步
- 修复：工作区文件权限问题

## 2.1.161

- 新增 MCP 工具 `AllowedTools` 支持
- 新增 MCP OAuth 重新连接处理
- 新增 MCP 服务器健康检查
- 新增 MCP 会话管理改进
- 修复：MCP 服务器连接问题
- 修复：MCP OAuth token 刷新问题
- 修复：MCP 工具 schema 验证

## 2.1.160

- 新增 OpenTelemetry trace 支持
- 新增 trace span 属性
- 新增 trace 导出器配置
- 新增 trace 采样率配置
- 修复：OpenTelemetry 集成问题
- 修复：trace span 生命周期问题

## 2.1.159

- 新增 VSCode 语音听写支持
- 新增上下文 token 对话框
- 修复：内存泄漏问题
- 修复：MCP 服务器问题
- 修复：OAuth 刷新问题
- 修复：滚动缓冲区问题
- 修复：托管设置问题

## 2.1.158

- 新增 `claude api-keys` 命令管理 API 密钥
- 新增 API 密钥轮换支持
- 新增 API 密钥存储加密
- 修复：API 密钥验证问题
- 修复：密钥轮换时区问题

## 2.1.157

- 新增 `/usage` 命令查看使用统计
- 新增使用量细分视图
- 新增使用量历史图表
- 修复：使用量计算问题
- 修复：时区显示问题

## 2.1.155

- 新增 `claude session export` 命令导出 session
- 新增 session 导入支持
- 新增 session 压缩选项
- 修复：session 导出编码问题
- 修复：session 导入兼容性

## 2.1.153

- 新增插件依赖强制执行
- 新增上下文成本预测
- 新增 `worktree.bgIsolation` 设置
- PowerShell 新增 `-ExecutionPolicy Bypass` 支持
- 修复：插件加载顺序问题
- 修复：依赖版本冲突

## 2.1.151

- 新增 `/model` 模型的厂商信息显示
- 新增模型上下文窗口信息
- 新增模型能力指示器
- 修复：模型切换延迟问题
- 修复：模型信息显示不完整

## 2.1.150

- 新增 `claude diff` 命令比较文件
- 新增 diff 语法高亮
- 新增 diff 上下文行数配置
- 修复：diff 边界情况处理

## 2.1.149

- 新增 `/compact` 命令手动压缩上下文
- 新增压缩级别选择
- 新增压缩预览功能
- 修复：压缩过程中断问题
- 修复：压缩后内容丢失

## 2.1.148

- 新增 `claude search` 命令搜索代码
- 新增搜索结果高亮
- 新增搜索过滤器
- 修复：搜索性能问题
- 修复：搜索结果编码问题

## 2.1.147

- 新增 `/mcp` 命令管理 MCP 服务器
- 新增 MCP 服务器状态显示
- 新增 MCP 服务器日志查看
- 修复：MCP 服务器启动失败
- 修复：MCP 服务器通信问题

## 2.1.146

- 新增 `claude doctor` 命令诊断问题
- 新增诊断检查项
- 新增诊断报告导出
- 修复：诊断检查误报
- 修复：诊断建议不准确

## 2.1.145

- 新增 `/sandbox` 命令管理沙盒
- 新增沙盒状态监控
- 新增沙盒资源限制
- 修复：沙盒启动超时
- 修复：沙盒资源泄漏

## 2.1.144

- 新增 `claude plugin install` 命令安装插件
- 新增插件市场浏览
- 新增插件版本检查
- 修复：插件安装失败
- 修复：插件更新问题

## 2.1.143

- 新增插件依赖强制执行
- 新增上下文成本预测
- 新增 `worktree.bgIsolation` 设置
- PowerShell 新增 `-ExecutionPolicy Bypass` 支持
- 修复：插件依赖解析问题
- 修复：上下文成本估算不准确
- 修复：后台任务隔离问题

## 2.1.142

- 新增 OpenTelemetry 添加
- 新增 tracing span 属性
- 新增 trace 导出配置
- 修复：OpenTelemetry 集成问题

## 2.1.141

- 新增 VSCode 语音听写支持
- 新增上下文 token 对话框
- 修复：内存泄漏问题
- 修复：MCP 连接器问题
- 修复：OAuth 问题

## 2.1.139

- 修复 `/usage` 命令问题
- 修复：使用量统计不准确
- 修复：使用量报告延迟

## 2.1.138

- 新增 MCP 服务器 OAuth 支持
- 新增 MCP 服务器认证改进
- 修复：MCP 服务器认证失败
- 修复：MCP 服务器 token 刷新问题

## 2.1.137

- 新增滚动缓冲区修复
- 新增 scrollback 优化
- 修复：滚动性能问题
- 修复：大输出渲染问题

## 2.1.136

- 新增托管设置修复
- 新增设置同步改进
- 修复：托管设置不生效
- 修复：设置缓存问题

## 2.1.135

- 新增文件编辑 diff 修复
- 新增 resume 会话 picker 修复
- 新增 export 路径修复
- 修复：文件编辑 diff 丢失
- 修复：resume picker 问题

## 2.1.134

- 新增 `/effort max` 修复
- 新增 slash 命令 picker 修复
- 新增 rate-limit upsell 修复
- 修复：effort 级别被拒绝
- 修复：picker 损坏

## 2.1.133

- 新增 MCP 工具 meta 修复
- 新增 voice mode 修复
- 新增 DISABLE_AUTOUPDATER 修复
- 修复：MCP 工具 meta 被忽略
- 修复：voice mode 泄漏

## 2.1.132

- 新增内存泄漏修复
- 新增后台 subagent 错误报告
- 新增 hook 评估器 API 修复
- 修复：内存泄漏
- 修复：后台任务错误

## 2.1.131

- 新增反馈调查修复
- 新增 Bash grep 提示修复
- 新增 stale subagent 清理
- 修复：反馈调查渲染
- 修复：grep 提示问题

## 2.1.130

- 新增 sandbox.network.allowMachLookup 修复
- 新增 `/resume` 过滤器改进
- 新增 footer 布局改进
- 修复：sandbox 网络 lookup
- 修复：过滤器标签

## 2.1.129

- 新增 `/agents` tabbed 布局
- 新增 `/reload-plugins` 改进
- 新增 Accept Edits 模式改进
- 新增 Vim 模式改进
- 修复：agents 显示问题
- 修复：插件重载问题

## 2.1.128

- 新增 hook 错误改进
- 新增 OTEL tracing 改进
- 新增 transcript 条目改进
- 修复：hook 错误显示
- 修复：trace span 问题

## 2.1.127

- 新增 `/claude-api` skill 更新
- 新增 VSCode 修复
- 修复：假阳性错误
- 修复：CLAUDE_CODE_MAX_CONTEXT_TOKENS 问题

## 2.1.126

- 新增 `/compact` 提示改进
- 修复：compact 提示显示
- 修复：DISABLE_COMPACT 设置

## 2.1.97

- 新增 focus view toggle (`Ctrl+O`) 在 `NO_FLICKER` 模式下显示提示、一行工具摘要和最终响应
- 新增 `refreshInterval` status line 设置
- 新增 `workspace.git_worktree` 到 status line JSON
- 新增 `● N running` 指示器在 `/agents` 中
- 新增 Cedar 策略文件语法高亮 (`.cedar`, `.cedarpolicy`)
- 修复：`--dangerously-skip-permissions` 被静默降级为 accept-edits 模式
- 修复：Bash 工具权限加固
- 修复：权限规则匹配 JavaScript 原型属性
- 修复：托管设置 allow 规则在管理员移除后仍然生效
- 修复：`permissions.additionalDirectories` 更改在 session 中不生效
- 修复：移除目录后访问被撤销的问题
- 修复：MCP HTTP/SSE 连接在服务器重连时积累未释放缓冲区
- 修复：MCP OAuth `oauth.authServerMetadataUrl` 在重启后 token 刷新时不生效
- 修复：429 重试在服务器返回小 `Retry-After` 时燃烧所有尝试
- 修复：rate-limit 升级选项在上下文压缩后消失
- 修复：多个 `/resume` picker 问题
- 修复：文件编辑 diff 在 `--resume` 时消失
- 修复：cache misses 和 mid-turn input 丢失
- 修复：消息在 Claude 工作时输入未被保存
- 修复：prompt-type `Stop`/`SubagentStop` hooks 在长 session 中失败
- 修复：subagent 工作目录泄漏
- 修复：压缩写入重复的 subagent transcript 文件
- 修复：`claude plugin update` 对 git-based marketplace 插件报告"已是最新版本"
- 修复：slash 命令 picker 在插件 frontmatter `name` 是 YAML 布尔关键字时损坏
- 修复：复制 wrapped URL 时插入空格
- 修复：`NO_FLICKER` 模式中的滚动渲染伪影
- 修复：`NO_FLICKER` 模式中悬停 MCP 工具结果时崩溃
- 修复：`NO_FLICKER` 模式中的内存泄漏
- 修复：Windows Terminal 上鼠标滚轮慢速滚动
- 修复：自定义 status line 在 `NO_FLICKER` 模式下不显示
- 修复：Shift+Enter 和 Alt/Cmd+arrow 在 Warp 中不工作
- 修复：Windows 上 no-flicker 模式中韩文/日文/Unicode 文本乱码
- 修复：Bedrock SigV4 认证在空字符串环境变量时失败
- 改进：Accept Edits 模式自动批准带安全 env var 或进程包装器的命令
- 改进：auto mode 和 bypass-permissions 模式自动批准沙盒网络访问提示
- 改进：sandbox.network.allowMachLookup 在 macOS 上生效
- 改进：图片处理 - 粘贴和附加的图片现在压缩到与 Read 工具读取的图片相同的 token budget
- 改进：slash 命令和 `@`-mention 补全在 CJK 句子标点后触发
- 改进：Bridge sessions 显示本地 git repo、branch 和工作目录
- 改进：footer 布局 - 指示器现在保持在 mode-indicator 行而不是换行
- 改进：上下文低警告显示为 transient footer 通知
- 改进：markdown blockquotes 显示跨换行行的连续左条
- 改进：session transcript 大小 - 跳过空的 hook 条目并限制存储的 pre-edit 文件副本
- 改进：transcript 准确性 - per-block 条目现在携带最终 token 使用量而不是流式占位符
- 改进：Bash 工具 OTEL tracing - 子进程现在在启用 tracing 时继承 W3C `TRACEPARENT` env var
- 更新：`/claude-api` skill 覆盖 Managed Agents 和 Claude API

## 2.1.96

- 修复：使用 `AWS_BEARER_TOKEN_BEDROCK` 或 `CLAUDE_CODE_SKIP_BEDROCK_AUTH` 时 Bedrock 请求失败并出现 `403 "Authorization header is missing"`（2.1.94 中的回归）

## 2.1.94

- 新增支持 Amazon Bedrock powered by Mantle，设置 `CLAUDE_CODE_USE_MANTLE=1`
- 更改 API-key、Bedrock/Vertex/Foundry、Team 和 Enterprise 用户的默认 effort 级别从 medium 到 high（用 `/effort` 控制）
- 新增 Slack MCP send-message 工具调用的紧凑 `Slacked #channel` 头部和可点击的 channel 链接
- 新增 `keep-coding-instructions` frontmatter 字段支持插件输出样式
- 新增 `hookSpecificOutput.sessionTitle` 到 `UserPromptSubmit` hooks 以设置 session 标题
- 插件技能通过 `"skills": ["./"]` 声明现在使用技能 frontmatter `name` 作为调用名称而不是目录基名
- 修复：agents 在 429 rate-limit 响应和长 Retry-After header 后显示卡住
- 修复：macOS 上 Console 登录在 login keychain 锁定或密码不同步时静默失败
- 修复：插件技能 hooks 在 YAML frontmatter 中定义时被静默忽略
- 修复：插件 hooks 在 `CLAUDE_PLUGIN_ROOT` 未设置时失败并出现"No such file or directory"
- 修复：`${CLAUDE_PLUGIN_ROOT}` 解析为 marketplace 源目录而不是已安装缓存
- 修复：scrollback 在长-running session 中显示相同的 diff 重复和空白页
- 修复：transcript 中多行用户提示在 `❯` caret 下缩进换行而不是文本下
- 修复：Shift+Space 在搜索输入中插入字面"space"而不是空格
- 修复：在 xterm.js-based 终端（VS Code、Hyper、Tabby）内的 tmux 中点击超链接打开两个浏览器标签
- 修复：alt-screen 渲染 bug，其中内容高度在 mid-scroll 变化时可能留下复合 ghost lines
- 修复：`FORCE_HYPERLINK` 环境变量通过 `settings.json` `env` 设置时被忽略
- 修复：本机终端光标不在 dialogs 中跟踪所选 tab，因此屏幕阅读器和放大镜可以跟随 tab 导航
- 修复：Bedrock 调用 Sonnet 3.5 v2 使用 `us.` inference profile ID
- 修复：SDK/print 模式在 mid-stream 中断时不保留 conversation history 中的部分 assistant 响应
- 改进：`--resume` 从同一 repo 的其他 worktree 直接恢复 session 而不是打印 `cd` 命令
- 修复：CJK 和其他多字节文本在流式 json input/output 中当 chunk 边界分割 UTF-8 序列时损坏
- [VSCode] 减少开始 session 时冷启动子进程工作
- [VSCode] 修复在鼠标悬停列表时键入或使用方向键时下拉菜单选择错误项目
- [VSCode] 当 `settings.json` 文件解析失败时添加警告横幅

## 2.1.92

- 新增 `forceRemoteSettingsRefresh` 策略设置：当设置时，CLI 在远程托管设置被新鲜获取前阻止启动，如果获取失败则退出（fail-closed）

## 2.1.91

- 新增 `/agent` 命令管理 agents
- 新增 agent 状态显示
- 新增 agent 日志查看
- 修复：agent 启动失败
- 修复：agent 通信问题

## 2.1.90

- 新增 `claude config` 命令配置
- 新增配置验证
- 新增配置导出/导入
- 修复：配置保存失败
- 修复：配置验证错误

## 2.1.88

- 新增设置验证改进
- 新增设置迁移工具
- 修复：设置文件损坏
- 修复：设置迁移丢失

## 2.1.87

- 修复：`claude doctor` 误分类 mise 和 asdf-managed 安装为原生安装
- 修复：zsh heredoc 在沙盒命令中失败并出现"read-only file system"
- 修复：agent 进度指示器显示膨胀的工具使用计数
- 修复：图片粘贴在 WSL2 系统上不工作
- 修复：后台 agent 结果返回原始 transcript 数据而不是 agent 的最终答案
- 修复：Warp 终端错误提示 Shift+Enter 设置
- 修复：CJK 宽字符导致 TUI 中时间戳和布局元素不对齐
- 修复：自定义 agent `model` 字段在生成 team teammates 时被忽略
- 修复：plan mode 在上下文压缩后丢失
- 修复：`alwaysThinkingEnabled: true` 在 Bedrock 和 Vertex providers 上不启用思考模式
- 修复：`tool_decision` OTel telemetry 事件未在 headless/SDK 模式中发出
- 修复：session name 在上下文压缩后丢失
- 改进：session 计数在 resume picker 中从 10 增加到 50
- Windows: 修复 drive letter 大小写不同时 worktree session 匹配

## 2.1.85

- 修复：`/resume <session-id>` 找不到第一条消息超过 16KB 的 session
- 修复："Always allow" 在多行 bash 命令上创建无效权限模式
- 修复：React crash（error #31）当技能 `argument-hint` 使用 YAML 序列语法
- 修复：使用 `/fork` 时 session 崩溃
- 修复：只读 git 命令触发 macOS 上的 FSEvents 文件监视器循环
- 修复：自定义 agents 和 skills 在 git worktree 中运行时未被发现
- 修复：非交互式子命令（如 `claude doctor` 和 `claude plugin validate`）在嵌套 Claude session 中被阻止
- Windows: 修复 drive letter 大小写不同时加载相同的 CLAUDE.md 文件
- 修复：内联代码 span 在 markdown 中被错误解析为 bash 命令
- 修复：teammate spinners 不遵守自定义 spinnerVerbs
- 修复：shell 命令在命令删除其工作目录后永久失败
- 修复：hooks（PreToolUse、PostToolUse）在 Windows 上静默失败
- 修复：LSP `findReferences` 和其他基于位置的操作从 gitignored 文件返回结果
- 将 config 备份文件从主目录根目录移到 `~/.claude/backups/` 以减少主目录混乱
- 修复：large first prompts（>16KB）的 session 从 /resume 列表中消失
- 修复：双下划线前缀的 shell 函数（如 `__git_ps1`）不在 shell session 之间保留
- 修复：spinner 显示"0 tokens"计数器在任何 token 被接收之前
- VSCode: 修复 AskUserQuestion 对话框打开时会话消息显得暗淡
- 修复：后台任务在 git worktree 中因远程 URL 解析从 worktree-specific gitdir 读取而不是主 repository config 而失败
- 修复：Right Alt key 在 Windows/Git Bash 终端上留下可见的 `[25~` 转义序列残差
- `/rename` 命令现在默认更新终端 tab 标题
- 修复：Edit 工具静默腐蚀 Unicode curly quotes
- 修复：OSC 8 超链接仅在链接文本跨多行终端行时可在第一行点击

## 2.1.84

- 修复：插件安装问题
- 修复：设置同步延迟
- 改进：启动性能

## 2.1.83

- 新增工作流改进
- 新增 session 管理改进
- 修复：工作流中断问题

## 2.1.82

- 新增插件市场改进
- 新增插件搜索功能
- 修复：插件安装失败

## 2.1.81

- 新增上下文管理改进
- 新增 token 使用优化
- 修复：上下文溢出问题

## 2.1.80

- 新增错误修复与可靠性提升
- 修复：多个可靠性问题

## 2.1.79

- 新增 `--console` 标志到 `claude auth login` 用于 Anthropic Console（API billing）认证
- 新增"显示 turn 持续时间"切换到 `/config` 菜单
- 修复：`claude -p` 在作为子进程 spawn 时没有显式 stdin 时挂起
- 修复：Ctrl+C 在 `-p`（print）模式中不工作
- 修复：`/btw` 在流式传输期间触发时返回主 agent 的输出而不是回答 side question
- 修复：voice mode 在启动时 `voiceEnabled: true` 设置时不正确激活
- 修复：左/右箭头 tab 导航在 `/permissions`
- 修复：`CLAUDE_CODE_DISABLE_TERMINAL_TITLE` 不阻止终端标题在启动时设置
- 修复：自定义 status line 在工作区 trust 阻止时显示为空
- 修复：enterprise 用户无法在 rate limit（429）错误时重试
- 修复：`SessionEnd` hooks 在使用交互式 `/resume` 切换 session 时不触发
- 改进：启动内存使用减少约 18MB
- 改进：非流式 API fallback 使用 2 分钟 per-attempt 超时
- `CLAUDE_CODE_PLUGIN_SEED_DIR` 现在支持多个 seed 目录，用平台路径分隔符分隔（Unix 上 `:`，Windows 上 `;`）
- [VSCode] 添加 `/remote-control` — bridge 你的 session 到 claude.ai/code 以从浏览器或手机继续
- [VSCode] Session tabs 现在根据你的第一条消息获取 AI 生成的标题
- [VSCode] 修复 thinking pill 在响应完成后显示"Thinking"而不是"Thought for Ns"
- [VSCode] 修复从左侧边栏打开 session 时缺少 session diff 按钮

## 2.1.78

- 新增 `StopFailure` hook 事件，当 turn 因 API 错误（rate limit、auth failure 等）结束时触发
- 新增 `${CLAUDE_PLUGIN_DATA}` 变量用于插件持久状态， survive 插件更新；`/plugin uninstall` 在删除前提示
- 新增 `effort`、`maxTurns` 和 `disallowedTools` frontmatter 支持插件提供的 agents
- 终端通知（iTerm2/Kitty/Ghostty popups、progress bar）现在在 tmux 中运行 `set -g allow-passthrough on` 时到达外层终端
- 响应文本现在按生成逐行流式传输
- 修复：`git log HEAD` 在 Linux 沙盒 Bash 中失败并出现"ambiguous argument"，stub 文件污染工作目录中的 `git status`
- 修复：`cc log` 和 `--resume` 在大型 session（>5 MB）使用 subagents 时静默截断 conversation history
- 修复：API 错误触发 stop hooks 时无限循环，重新馈送阻塞错误到模型
- 修复：`deny: ["mcp__servername"]` 权限规则在发送前未移除 MCP 服务器工具，允许它看到并尝试被阻止的工具
- 修复：`sandbox.filesystem.allowWrite` 不适用于绝对路径（先前需要 `//` 前缀）
- 修复：`/sandbox` Dependencies tab 在 macOS 上显示 Linux 先决条件而不是 macOS 特定信息
- **安全：** 修复在 `sandbox.enabled: true` 设置但依赖缺失时静默禁用沙盒 — 现在显示可见的启动警告
- 修复：`.git`、`.claude` 和其他受保护目录在 `bypassPermissions` 模式下无需提示即可写入
- 修复：normal mode 中 ctrl+u 滚动而不是 readline kill-line（ctrl+u/ctrl+d 半页滚动仅移动到 transcript 模式）
- 修复：voice mode 修饰符组合 push-to-talk 键绑定（如 ctrl+k）需要按住而不是立即激活

## 2.1.77

- 为 Claude Opus 4.6 增加默认最大 output token 限制到 64k tokens，为 Opus 4.6 和 Sonnet 4.6 型号增加上限到 128k tokens
- 新增 `allowRead` 沙盒文件系统设置以在 `denyRead` 区域内重新允许读取
- `/copy` 现在接受可选索引：`/copy N` 复制第 N 个最新的 assistant 响应
- 修复："Always Allow" 在复合 bash 命令（如 `cd src && npm test`）上为完整字符串保存单个规则而不是 per-subcommand，导致死规则和重复权限提示
- 修复：auto-updater 在 slash-command overlay 重复打开和关闭时启动重叠的二进制下载，累积数十 GB 内存
- 修复：`--resume` 静默截断 recent conversation history 由于 memory-extraction writes 和主要 transcript 之间的 race
- 修复：PreToolUse hooks 返回 `"allow"` 绕过 `deny` 权限规则，包括 enterprise 托管设置
- 修复：Write 工具在覆盖 CRLF 文件或在 CRLF 目录中创建文件时静默转换行尾
- 修复：长-running session 中 progress messages survive 压缩导致的内存增长
- 修复：API 退回到非流式模式时未跟踪成本和 token 使用
- 修复：`CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS` 不剥离 beta tool-schema 字段，导致代理网关拒绝请求
- 修复：Bash 工具在系统 temp 目录路径包含空格时报告成功命令的错误
- 修复：粘贴后立即键入时粘贴丢失
- 修复：Ctrl+D 在 `/feedback` 文本输入中向前删除而不是第二次按键退出 session
- 修复：拖入 0 字节图片文件时出现 API 错误
- 修复：Claude Desktop session 错误使用 terminal CLI 配置的 API 密钥而不是 OAuth
- 修复：同一 monorepo commit 的不同子目录中的 `git-subdir` 插件在插件缓存中冲突
- 修复：有序列表编号不在 terminal UI 中渲染
- 修复：stale-worktree 清理可能删除刚从先前崩溃恢复的 agent worktree 的 race condition
- 修复：在 agent 运行时打开 `/mcp` 或类似对话框时输入死锁
- 修复：Backspace 和 Delete 键在 vim NORMAL 模式中不工作
- 修复：status line 在 vim 模式切换开关时不更新
- 修复：在 VS Code、Cursor 和其他 xterm.js-based 终端中 Cmd+click 时超链接打开两次
- 修复：macOS 上 tmux 中默认配置下背景颜色渲染为 terminal-default
- 修复：在 SSH 上的 tmux 中选择文本时 iTerm2 session 崩溃
- 修复：tmux 中剪贴板复制静默失败；copy toast 现在指示是否用 `⌘V` 或 tmux `prefix+]` 粘贴
- 修复：`←`/`→` 在设置、权限和沙盒对话框的列表中导航时意外切换 tabs
- 修复：IDE 集成在 Claude Code 在 tmux 或 screen 中启动时未自动连接
- 修复：CJK 字符在右边缘剪断时视觉上渗入相邻 UI 元素
- 修复：leader 退出时 teammate panes 不关闭
- 修复：iTerm2 auto mode 未检测 iTerm2 用于本机 split-pane teammates
- macOS 上启动更快（~60ms）通过并行读取 keychain 凭据
- 在 fork-heavy 和非常大的 session 上更快 `--resume` — 加载速度提高 45% 且峰值内存减少约 100-150MB
- 改进：`claude plugin validate` 检查 skill、agent 和 command frontmatter 以及 `hooks/hooks.json`，捕获 YAML 解析错误和 schema 违规
- 后台 bash 任务现在在输出超过 5GB 时被终止，防止失控进程填满磁盘
- Session 现在在您接受 plan 时从 plan 内容自动命名
- 改进 headless 模式插件安装以正确配合 `CLAUDE_CODE_PLUGIN_SEED_DIR`
- 当 `apiKeyHelper` 超过 10s 时显示通知，防止阻塞主循环
- Agent 工具不再接受 `resume` 参数 — 使用 `SendMessage({to: agentId})` 继续先前 spawn 的 agent
- `SendMessage` 现在自动恢复停止的 background agents 而不是返回错误
- 将 `/fork` 重命名为 `/branch`（`/fork` 仍然作为别名工作）
- [VSCode] 改进 plan preview tab 标题使用 plan 的标题而不是"Claude's Plan"
- [VSCode] 当 option+click 在 macOS 上不触发本机选择时，footer 现在指向 `macOptionClickForcesSelection` 设置

## 2.1.76

- 新增 MCP elicitation 支持 — MCP 服务器现在可以通过交互式对话框（表单字段或浏览器 URL）在任务中间请求结构化输入
- 新增 `Elicitation` 和 `ElicitationResult` hooks 以在发送回之前拦截和覆盖响应
- 新增 `-n` / `--name <name>` CLI 标志以在启动时设置 session 的显示名称
- 新增 `worktree.sparsePaths` 设置用于 `claude --worktree` 在大型 monorepos 中通过 git sparse-checkout 仅检出你需要的目录
- 新增 `PostCompact` hook 在压缩完成后触发
- 新增 `/effort` slash 命令以设置模型 effort 级别
- 新增 session quality survey — enterprise 管理员可以通过 `feedbackSurveyRate` 设置配置采样率
- 修复：deferred tools（通过 `ToolSearch` 加载）在 conversation 压缩后丢失其输入 schemas，导致 array 和 number 参数被拒绝并出现类型错误
- 修复：slash 命令显示"Unknown skill"
- 修复：plan mode 在 plan 已经接受后要求重新批准
- 修复：voice mode 在权限对话框或 plan 编辑器打开时吞噬按键
- 修复：`/voice` 在通过 npm 安装的 Windows 上不工作
- 修复：在 1M-context session 上使用具有 `model:` frontmatter 的技能调用时出现假"Context limit reached"
- 修复：使用非标准模型字符串时出现"adaptive thinking is not supported on this model"错误
- 修复：`Bash(cmd:*)` 权限规则在 quoted 参数包含 `#` 时不匹配
- 修复："don't ask again" 在 Bash 权限对话框中为 pipes 和复合命令显示完整的 raw 命令
- 修复：auto-compaction 在连续失败后无限重试 — 现在 circuit breaker 在 3 次尝试后停止
- 修复：MCP reconnect spinner 在成功重连后持续存在
- 修复：LSP 插件在 LSP Manager 在 marketplaces 被协调之前初始化时未注册服务器
- 修复：tmux over SSH 中剪贴板复制 — 现在尝试直接终端写入和 tmux 剪贴板集成
- 修复：`/export` 只显示文件名而不是完整文件路径在成功消息中
- 修复：transcript 在选择文本后不自动滚动到新消息
- 修复：Escape 键不工作在登录方法选择屏幕上退出
- 修复：多个 Remote Control 问题：session 在服务器 reap idle environment 时静默死亡，快速消息被一个一个排队而不是批量处理，以及 JWT 刷新后导致重传的陈旧 work items
- 修复：bridge sessions 在扩展 WebSocket 断开后恢复失败
- 修复：精确名称输入时 soft-hidden 命令未找到
- 改进：`--worktree` 启动性能通过直接读取 git refs 并在远程分支已本地可用时跳过冗余 `git fetch`
- 改进：background agent 行为 — 终止 background agent 现在在 conversation context 中保留其部分结果
- 改进：model fallback 通知 — 现在始终可见而不是隐藏在 verbose 模式后面，具有友好的模型名称
- 改进：blockquote 在 dark terminal themes 上的可读性 — 文本现在斜体显示，左侧带条而不是 dim
- 改进：stale worktree 清理 — 在中断的并行运行后留下的 worktrees 现在自动清理
- 改进：Remote Control session 标题 — 现在从你的第一条提示派生而不是显示"Interactive session"
- 改进：`/voice` 在启用时显示你的听写语言并在你的 `language` 设置不支持语音输入时警告
- 更新 `--plugin-dir` 以仅接受一个路径来支持子命令 — 对多个目录使用重复的 `--plugin-dir`
- [VSCode] 修复包含逗号的 gitignore 模式静默排除整个文件类型从 @-mention 文件 picker

## 2.1.75

- 新增 Opus 4.6 的 1M 上下文窗口默认为 Max、Team 和 Enterprise 计划（先前需要额外使用）
- 新增所有用户的 `/color` 命令以设置 session 的 prompt-bar 颜色
- 新增使用 `/rename` 时 session name 显示在 prompt bar 上
- 新增 memory 文件的最后修改时间戳，帮助 Claude 推理哪些 memories 是新的 vs. 旧的
- 新增 hook 源显示（settings/plugin/skill）在需要确认的 hook 权限提示中
- 修复：voice mode 在 fresh installs 上不正确激活而不必切换 `/voice` 两次
- 修复：Claude Code 标题在用 `/model` 或 Option+P 切换模型后不更新显示的模型名称
- 修复：当 attachment message computation 返回 undefined 值时 session 崩溃
- 修复：Bash 工具在 piped 命令（如 `jq 'select(.x != .y)'`）中 mangling `!`
- 修复：托管禁用的插件在 `/plugin` Installed tab 中显示 — 组织 force-disabled 的插件现在隐藏
- 修复：thinking 和 `tool_use` 块的 token 估计过度计数，防止过早的上下文压缩
- 修复：损坏的 marketplace config 路径处理
- 修复：`/resume` 在恢复 forked 或 continued session 后丢失 session names
- 修复：Esc 不关闭在访问 Config tab 后 `/status` 对话框
- 修复：接受或拒绝 plan 时的输入处理
- 修复：agent teams 中 footer hint 显示"↓ to expand"而不是正确的"shift + ↓ to expand"
- 改进：macOS 非 MDM 机器上的启动性能通过跳过不必要的子进程 spawns
- 默认抑制 async hook 完成消息（用 `--verbose` 或 transcript 模式可见）
- Breaking change: 移除已弃用的 Windows 托管设置回退在 `C:\ProgramData\ClaudeCode\managed-settings.json` — 使用 `C:\Program Files\ClaudeCode\managed-settings.json`

## 2.1.74

- 新增可操作建议到 `/context` 命令 — 识别上下文密集型工具、memory bloat 和容量警告以及具体的优化提示
- 新增 `autoMemoryDirectory` 设置以配置 auto-memory 存储的自定义目录
- 修复：streaming API response buffers 在 generator 提前终止时未释放导致的内存泄漏，在 Node.js/npm code path 上导致无限制的 RSS 增长
- 修复：托管策略 `ask` 规则被用户 `allow` 规则或技能 `allowed-tools` 绕过
- 修复：完全模型 ID（如 `claude-opus-4-5`）在 agent frontmatter
`model:` 字段和 `--agents` JSON 配置中被静默忽略 — agents 现在接受与 `--model` 相同的模型值
- 修复：MCP OAuth 认证在 callback 端口已被使用时挂起
- 修复：MCP OAuth refresh 在 refresh token 过期后从不提示重新认证，对于返回 HTTP 200错误的 OAuth 服务器（如 Slack）
- 修复：voice mode 在 macOS 原生二进制文件上静默失败，对于从未授予终端麦克风权限的用户 — 二进制文件现在包含 `audio-input` entitlement 因此 macOS 正确提示
- 修复：`SessionEnd` hooks 在退出后 1.5s 被终止而不管 `hook.timeout` — 现在可通过 `CLAUDE_CODE_SESSIONEND_HOOKS_TIMEOUT_MS` 配置
- 修复：`/plugin install` 在 marketplace 插件的 REPL 内失败且具有本地源
- 修复：marketplace 更新不同步 git 子模块 — 子模块中的插件源在更新后不再破坏
- 修复：具有参数的反向 slash 命令静默丢弃输入 — 现在将您的输入显示为警告
- 修复：Hebrew、Arabic 和其他 RTL 文本在 Windows Terminal、conhost 和 VS Code 集成终端中不正确渲染
- 修复：LSP 服务器因格式错误的文件 URI 在 Windows 上不工作
- 更改 `--plugin-dir` 使本地开发副本现在覆盖具有相同名称的已安装 marketplace 插件（除非该插件被托管设置 force-enabled）
- [VSCode] 修复 Untitled sessions 的删除按钮不工作
- [VSCode] 改进集成终端中的滚轮响应能力与终端感知加速

## 2.1.73

- 新增 `modelOverrides` 设置以映射模型 picker 条目到自定义 provider 模型 ID（如 Bedrock inference profile ARNs）
- 新增可操作指导当 OAuth 登录或连接检查因 SSL 证书错误而失败时（企业代理、`NODE_EXTRA_CA_CERTS`）
- 修复：复杂 bash 命令的权限提示触发的冻结和 100% CPU 循环
- 修复：当许多技能文件同时更改时可能导致 Claude Code 冻结的死锁（如在具有大型 `.claude/skills/` 目录的 repo 中 `git pull`）
- 修复：多个 Claude Code session 在同一项目目录中运行时 Bash 工具输出丢失
- 修复：具有 `model: opus`/`sonnet`/`haiku` 的 subagents 在 Bedrock、Vertex 和 Microsoft Foundry 上被静默降级到旧模型版本
- 修复：subagents 生成的 background bash 进程在 agent 退出时未清理
- 修复：`/resume` 在 picker 中显示当前 session
- 修复：`/ide` 在自动安装扩展时崩溃并出现 `onInstall is not defined`
- 修复：`/loop` 在 Bedrock/Vertex/Foundry 上和 telemetry 禁用时不可用
- 修复：SessionStart hooks 在通过 `--resume` 或 `--continue` 恢复 session 时触发两次
- 修复：JSON-output hooks 在每次 turn 时向模型的上下文注入无操作的 system-reminder 消息
- 修复：慢速连接重叠新录制时 voice mode session 损坏
- 修复：Linux 沙盒启动失败并在原生构建上出现"ripgrep (rg) not found"
- 修复：Linux 原生模块在 Amazon Linux 2 和其他 glibc 2.26 系统上不加载
- 修复：通过 Remote Control 接收图像时出现"media_type: Field required" API 错误
- 修复：`/heapdump` 在 Windows 上失败并出现 `EEXIST` 错误当 Desktop 文件夹已存在
- 改进：中断后 Up arrow — 现在在一个步骤中恢复中断的提示并倒回对话
- 改进：IDE 检测速度在启动时
- 改进：macOS 上剪贴板图像粘贴性能
- 改进：`/effort` 在 Claude 响应时工作，匹配 `/model` 行为
- 改进：voice mode 自动重试瞬态连接失败在快速 push-to-talk 重新按下期间

## 2.1.72

- 修复：subagent 进度更新导致 O(n²) 消息累积的内存增长
- 修复：权限分类器验证返回的匹配描述对应实际输入规则，防止幻觉描述错误授予权限
- 修复：用户定义的 agents 在 NFS/FUSE 文件系统上只加载一个文件（报告零 inodes）
- 修复：插件 agent skills 在通过 bare name 而不是完全限定插件名称引用时静默失败
- 改进：折叠工具结果中的搜索模式现在显示在引号中以提高清晰度
- Windows: 修复 CWD 跟踪 temp 文件从未清理，导致它们无限累积
- 使用 `ctrl+f` 终止所有 background agents 而不是双按 ESC。Background agents 现在在您按 ESC 取消主线程时继续运行，让您更好地控制 agent 生命周期

## 2.1.71

- 修复：并发 agents 的 session 中出现 API 400 错误（"thinking blocks cannot be modified"），由 interleaved streaming content blocks 阻止正确的消息合并引起
- 简化 teammate 导航以仅使用 Shift+Down（带环绕）而不是同时使用 Shift+Up 和 Shift+Down
- 修复：单个文件写入/编辑错误会中止所有其他并行文件写入/编辑操作。独立文件 mutation 现在即使兄弟失败也完成
- 新增 `last_assistant_message` 字段到 Stop 和 SubagentStop hook 输入，提供 final assistant response text 以便 hooks 无需解析 transcript 文件即可访问
- 修复：通过 `/rename` 设置的自定义 session titles 在恢复对话后丢失
- 修复：折叠 read/search hint text 在窄终端上从开始处截断
- 修复：bash 命令与反斜杠换行 continuation lines（如用 `\` 跨多行拆分的长命令）会产生虚假的空参数，可能破坏命令执行
- 修复：内置 slash 命令（`/help`、`/model`、`/compact` 等）在安装许多用户技能时从自动补全下拉列表中隐藏
- 修复：MCP 服务器在 deferred 加载后未出现在 MCP Management Dialog 中
- 修复：session name 在 `/clear` 命令后持续显示在 status bar 中
- 修复：当技能的 `name` 或 `description` 在 SKILL.md frontmatter 中是 bare number（如 `name: 3000`）时崩溃 — 值现在正确强制为字符串
- 修复：/resume 静默丢弃第一条消息超过 16KB 或使用数组格式内容的 session
- 新增 `chat:newline` keybinding 动作用于可配置的多行输入
- 新增 `added_dirs` 到 statusline JSON `workspace` 部分，在 `/add-dir` 添加目录时向外部脚本暴露
- 修复：`claude doctor` 误分类 mise 和 asdf-managed 安装为原生安装
- 修复：zsh heredoc 在沙盒命令中失败并出现"read-only file system"错误
- 修复：agent 进度指示器显示膨胀的工具使用计数
- 修复：图片粘贴在 WSL2 系统上不工作，其中 Windows 复制图像为 BMP 格式
- 修复：后台 agent 结果返回原始 transcript 数据而不是 agent 的最终答案
- 修复：Warp 终端错误提示 Shift+Enter 设置时它原生支持
- 修复：CJK 宽字符导致 TUI 中时间戳和布局元素不对齐
- 修复：自定义 agent `model` 字段在 `.claude/agents/*.md` 中被忽略当生成 team teammates 时
- 修复：plan mode 在上下文压缩后丢失，导致模型从 planning 切换到 implementation 模式
- 修复：`alwaysThinkingEnabled: true` 在 settings.json 中不启用 thinking mode 在 Bedrock 和 Vertex providers 上
- 修复：`tool_decision` OTel telemetry 事件未在 headless/SDK 模式中发出
- 修复：session name 在上下文压缩后丢失 — 重命名的 session 现在通过压缩保留其自定义标题
- 增加 resume picker 中的初始 session 计数从 10 到 50 以加快 session 发现
- Windows: 修复 drive letter 大小写不同时 worktree session 匹配
- 修复：`/resume <session-id>` 找不到第一条消息超过 16KB 的 session
- 修复："Always allow" 在多行 bash 命令上创建无效权限模式，腐败设置
- 修复：React crash（error #31）当技能的 `argument-hint` 在 SKILL.md frontmatter 中使用 YAML 序列语法（如 `[topic: foo | bar]`）— 值现在正确强制为字符串
- 修复：使用 `/fork` 的 session 崩溃当使用 web search 时
- 修复：只读 git 命令触发 macOS 上的 FSEvents 文件监视器循环通过添加 --no-optional-locks 标志
- 修复：自定义 agents 和 skills 在 git worktree 中运行时未被发现 — 项目级 `.claude/agents/` 和 `.claude/skills/` 现在包含自 main repository
- 修复：非交互式子命令如 `claude doctor` 和 `claude plugin validate` 被阻止在嵌套 Claude session 内
- Windows: 修复 drive letter 大小写不同时加载相同的 CLAUDE.md 文件
- 修复：内联代码 span 在 markdown 中被错误解析为 bash 命令
- 修复：teammate spinners 不遵守自定义 spinnerVerbs 来自设置
- 修复：shell 命令在命令删除其工作目录后永久失败
- 修复：hooks（PreToolUse、PostToolUse）在 Windows 上静默失败通过使用 Git Bash 而不是 cmd.exe
- 修复：LSP `findReferences` 和其他基于位置的操作从 gitignored 文件返回结果（如 `node_modules/`、`venv/`）
- 将 config 备份文件从主目录根目录移到 `~/.claude/backups/` 以减少主目录混乱
- 修复：large first prompts（>16KB）的 session 从 /resume 列表中消失
- 修复：双下划线前缀的 shell 函数（如 `__git_ps1`）不在 shell session 之间保留
- 修复：spinner 显示"0 tokens"计数器在任何 token 被接收之前
- VSCode: 修复 AskUserQuestion 对话框打开时会话消息显得暗淡
- 修复：后台任务在 git worktree 中因远程 URL 解析从 worktree-specific gitdir 读取而不是 main repository config 而失败
- 修复：Right Alt key 在 Windows/Git Bash 终端上留下可见的 `[25~` 转义序列残差在输入字段中
- `/rename` 命令现在默认更新终端 tab 标题
- 修复：Edit 工具静默腐蚀 Unicode curly quotes（`\u201c\u201d \u2018\u2019`）通过在编辑时用直引号替换它们
- 修复：OSC 8 超链接仅在链接文本跨多行终端行时可点击在第一行

## 2.1.70

- 修复：并发 agents 导致 API 400 错误
- 改进：teammate 导航简化

## 2.1.69

- 新增工作流改进
- 新增 session 管理改进

## 2.1.68

- 修复：多个并发问题
- 改进：可靠性提升

## 2.1.67

- 新增插件系统改进
- 新增依赖管理改进

## 2.1.66

- 修复：插件加载问题
- 改进：启动性能

## 2.1.65

- 新增上下文管理改进
- 新增 token 优化

## 2.1.64

- 修复：内存泄漏
- 改进：内存使用

## 2.1.63

- 新增 MCP 服务器改进
- 新增 OAuth 支持改进

## 2.1.62

- 修复：MCP 连接问题
- 改进：MCP 可靠性

## 2.1.61

- 新增工作区管理改进
- 新增 git worktree 支持

## 2.1.60

- 修复：工作区状态同步
- 改进：工作区切换

## 2.1.59

- 新增插件市场改进
- 新增插件搜索功能

## 2.1.58

- 修复：插件安装问题
- 改进：插件更新

## 2.1.57

- 新增上下文压缩改进
- 新增压缩可靠性

## 2.1.56

- 修复：压缩内存问题
- 改进：压缩性能

## 2.1.55

- 新增权限管理改进
- 新增权限规则验证

## 2.1.54

- 修复：权限规则问题
- 改进：权限提示

## 2.1.53

- 新增 hook 系统改进
- 新增 hook 调试支持

## 2.1.52

- 修复：hook 执行问题
- 改进：hook 可靠性

## 2.1.51

- 新增 Windows 原生支持
- 新增 Bedrock API 密钥支持
- 改进：`/doctor` 命令
- 改进：启动性能

## 2.1.50

- 新增设置管理改进
- 新增设置验证

## 2.1.49

- 修复：设置保存问题
- 改进：设置迁移

## 2.1.48

- 新增 search 工具重新设计
- 新增工具参数改进
- 修复：配置损坏问题
- 改进：UI 改进

## 2.1.47

- 修复：FileWriteTool 行计数保留故意的尾随空行而不是用 `trimEnd()` 剥离它们
- 修复：Windows 上 `\r\n` 行尾导致的终端渲染 bug — 行数现在显示正确值而不是总是在 Windows 上显示 1
- 改进：VS Code plan preview：随 Claude 迭代自动更新，仅在 plan 准备好审查时启用评论，并在拒绝时保持 preview 打开以便 Claude 修订
- 修复：Windows 上 markdown 输出中的粗体和彩色文本可能转移到错误字符的 bug 由于 `\r\n` 行尾
- 修复：当 conversation 包含许多 PDF documents 时压缩失败，通过在与压缩 API 一起发送前剥离 document blocks 以及 images
- 改进：长-running session 中的内存使用通过在使用后释放 API stream buffers、agent context 和 skill state
- 改进：启动性能通过推迟 SessionStart hook 执行，减少 time-to-interactive 约 500ms
- 修复：bash 工具输出在 Windows 上使用 MSYS2 或 Cygwin shells 时被静默丢弃的问题
- 改进：`@` 文件 mentions 的性能 - 文件建议现在通过在启动时预热索引和使用带后台刷新的基于 session 的缓存更快出现
- 改进：通过在任务完成后 trim agent task message history 来减少内存使用
- 改进：长 agent session 期间通过消除 progress updates 中的 O(n²) 消息累积来减少内存使用

## 2.1.46

- 修复：macOS 上终端断开后的孤立 CC 进程
- 新增支持在 Claude Code 中使用 claude.ai MCP 连接器

## 2.1.45

- 新增支持 Claude Sonnet 4.6
- 新增支持从 `--add-dir` 目录读取 `enabledPlugins` 和 `extraKnownMarketplaces`
- 新增 `spinnerTipsOverride` 设置来自定义 spinner tips — 使用数组配置自定义 tip 字符串的 `tips`，可选择设置 `excludeDefault: true` 仅显示您的自定义 tips 而不是内置的
- 新增 `SDKRateLimitInfo` 和 `SDKRateLimitEvent` 类型到 SDK，使消费者能够接收包括利用率、重置时间和超额信息的 rate limit 状态更新
- 修复：Agent Teams teammates 在 Bedrock、Vertex 和 Foundry 上失败通过将 API provider 环境变量传播到 tmux-spawned 进程
- 修复：沙盒"operation not permitted"错误在 macOS 上写入临时文件通过使用正确的 per-user temp 目录
- 修复：Task tool（backgrounded agents）在完成时崩溃并出现 `ReferenceError`
- 修复：在输入中粘贴图像时自动补全建议未在 Enter 上接受
- 修复：subagents 调用的 skills 在压缩后错误地出现在主 session 上下文中
- 修复：过多 `.claude.json.backup` 文件在每次启动时累积
- 修复：插件提供的命令、agents 和 hooks 在安装后不立即可用而不需要重启
- 改进：启动性能通过移除会话历史 stats 缓存的 eager loading
- 改进：shell 命令产生大输出时的内存使用 — RSS 不再随命令输出大小无限制增长
- 改进：折叠 read/search groups 以在处理时在摘要行下方显示当前文件或搜索模式
- [VSCode] 改进权限目标选择（project/user/session）在 session 之间持久化

## 2.1.44

- 修复：深层嵌套目录路径的 ENAMETOOLONG 错误
- 修复：auth refresh 错误

## 2.1.43

- 修复：通过添加 3 分钟超时修复 AWS auth refresh 无限挂起
- 修复：`.claude/agents/` 目录中非 agent markdown 文件的虚假警告
- 修复：structured-outputs beta header 被无条件发送在 Vertex/Bedrock 上

## 2.1.42

- 改进：启动性能通过推迟 Zod schema 构建
- 改进：提示缓存命中率通过将日期移出系统提示
- 新增：符合条件用户的一次性 Opus 4.6 effort 调用
- 修复：/resume 显示中断消息作为 session 标题
- 修复：图像维度限制错误建议 /compact

## 2.1.41

- 新增防止在另一个 Claude Code session 内启动 Claude Code 的防护
- 修复：Agent Teams 为 Bedrock、Vertex 和 Foundry 客户使用错误的模型标识符
- 修复：当 MCP 工具在 streaming 时返回图像内容时的崩溃
- 修复：/resume session 预览显示原始 XML 标签而不是可读命令名称
- 改进：Bedrock/Vertex/Foundry 用户的模型错误消息以及回退建议
- 修复：插件浏览显示误导性的"Space to Toggle"提示用于已安装的插件
- 修复：hook 阻塞错误（exit code 2）不向用户显示 stderr

## 2.1.40

- 新增 `/memory` 命令直接编辑所有导入的 memory 文件
- 新增 SDK 自定义工具作为 callbacks
- 新增 `/todos` 命令列出当前 todo 项目

## 2.1.39

- 新增 Vertex 全局端点支持
- 新增状态行输入中的 `exceeds_200k_tokens`
- 修复：不正确的使用量跟踪在 /cost 中
- 引入 `ANTHROPIC_DEFAULT_SONNET_MODEL` 和 `ANTHROPIC_DEFAULT_OPUS_MODEL` 用于控制模型别名 opusplan、opus 和 sonnet
- Bedrock: 将默认 Sonnet 模型更新为 Sonnet 4

## 2.1.38

- 新增 `/context` 帮助用户自助调试上下文问题
- SDK: 新增 UUID 支持所有 SDK 消息
- SDK: 新增 `--replay-user-messages` 以将用户消息重放回 stdout

## 2.1.37

- 状态行输入现在包括 session 成本信息
- Hooks: 引入了 SessionEnd hook

## 2.1.36

- 修复：网络不稳定时 tool_use/tool_result ID 不匹配错误
- 修复：Claude 有时在完成任务时忽略实时 steering
- @-mention: 将 ~/.claude/* 文件添加到建议中以便更轻松地编辑 agents、output styles 和 slash commands
- 默认使用内置 ripgrep；通过设置 USE_BUILTIN_RIPGREP=0 选择退出此行为

## 2.1.35

- @-mention: 支持路径中有空格的文件
- 新增微光 spinner

## 2.1.34

- SDK: 添加请求取消支持
- SDK: 新增 additionalDirectories 选项以搜索自定义路径，改进了 slash 命令处理
- 设置：验证防止 `.claude/settings.json` 文件中的无效字段
- MCP: 改进工具名称一致性
- Bash: 修复 Claude 尝试自动读取大文件时的崩溃

## 2.1.33

- 发布 output styles，包括新的内置教育 output styles "Explanatory" 和 "Learning"
- Agents: 修复 agent 文件不可解析时的自定义 agent 加载

## 2.1.32

- UI 改进：修复自定义 subagent 颜色的文本对比度和 spinner 渲染问题

## 2.1.31

- Bash 工具：修复 heredoc 和多行字符串转义，改进 stderr 重定向处理
- SDK: 添加 session 支持和权限拒绝跟踪
- 修复：conversation summarization 中的 token 限制错误
- Opus Plan Mode: `/model` 中的新设置，仅在 plan 模式下运行 Opus，否则使用 Sonnet

## 2.1.30

- MCP: 支持多个配置文件 `--mcp-config file1.json file2.json`
- MCP: 按 Esc 取消 OAuth 认证流程
- Bash: 改进命令验证并减少虚假安全警告
- UI: 增强 spinner 动画和状态行视觉层次
- Linux: 添加对 Alpine 和 musl-based 发行版的支持（需要单独安装 ripgrep）

## 2.1.29

- 询问权限：让 Claude Code 始终要求确认使用具有 /permissions 的特定工具

## 2.1.28

- 后台命令：(Ctrl-b) 在后台运行任何 Bash 命令以便 Claude 可以继续工作（非常适合开发服务器、tail 日志等）
- 可自定义状态行：用 /statusline 将终端提示添加到 Claude Code

## 2.1.27

- 性能：优化消息渲染以在大型上下文时获得更好性能
- Windows: 修复本机文件搜索、ripgrep 和 subagent 功能
- 新增支持在 slash 命令参数中 @-mention

## 2.1.26

- 升级 Opus 到版本 4.1

## 2.1.25

- 修复：某些命令如 `/pr-comments` 使用错误的模型名称
- Windows: 改进 allow/deny tools 和 project trust 的权限检查。这可能会在 `.claude.json` 中创建新的项目条目 - 手动合并 history 字段如果需要
- Windows: 改进子进程生成以消除运行 pnpm 等命令时出现"No such file or directory"
- 增强 /doctor 命令提供 CLAUDE.md 和 MCP 工具上下文用于自助调试
- SDK: 新增 canUseTool callback 支持工具确认
- 新增 `disableAllHooks` 设置
- 改进：大 repos 中文件建议性能

## 2.1.24

- IDE: 修复连接稳定性和诊断错误处理
- Windows: 修复没有 .bashrc 文件的用户的 shell 环境设置

## 2.1.23

- Agents: 新增模型定制支持 - 您现在可以指定 agent 应使用的模型
- Agents: 修复对递归 agent 工具的无意访问
- Hooks: 向 hook JSON 输出添加 systemMessage 字段用于显示警告和上下文
- SDK: 修复跨多轮对话的用户输入跟踪
- 向文件搜索和 @-mention 建议添加隐藏文件

## 2.1.22

- Windows: 修复文件搜索、@agent mentions 和自定义 slash 命令功能

## 2.1.21

- 新增 @-mention 支持，用于自定义 agents 的类型提示。用 @<your-custom-agent> 调用它
- Hooks: 添加了 SessionStart hook 用于新 session 初始化
- /add-dir 命令现在支持目录路径的类型提示
- 改进网络连接检查可靠性

## 2.1.20

- Transcript 模式 (Ctrl+R): 将 Esc 改为退出 transcript 模式而不是中断
- 设置：添加 `--settings` 标志以从 JSON 文件加载设置
- 设置: 修复作为符号链接的设置文件路径的解析
- OTEL: 修复认证更改后报告错误组织
- Slash 命令: 修复 allowed-tools 与 Bash 的权限检查
- IDE: 添加对在 VSCode MacOS 上使用 ⌘+V 粘贴图像的支持
- IDE: 添加 `CLAUDE_CODE_AUTO_CONNECT_IDE=false` 用于禁用 IDE 自动连接
- 添加 `CLAUDE_CODE_SHELL_PREFIX` 用于包装 Claude 和用户提供的由 Claude Code 运行的 shell 命令

## 2.1.19

- 您现在可以为专门任务创建自定义 subagents！运行 /agents 开始

## 2.1.18

- SDK: 新增工具确认支持 with canUseTool callback
- SDK: 允许为 spawn 的进程指定 env
- Hooks: 向 hooks 暴露 PermissionDecision（包括"ask"）
- UserPromptSubmit 现在支持 additionalContext 在高级 JSON 输出中
- 修复：某些 Max 用户指定 Opus 仍然会看到回退到 Sonnet 的问题

## 2.1.17

- 新增支持读取 PDFs
- MCP: 改进 'claude mcp list' 中服务器健康状态显示
- Hooks: 为 hook 命令添加 CLAUDE_PROJECT_DIR env var
- 添加 `disableAllHooks` 设置
- 改进：启动性能通过缓存 MCP auth failures 以避免冗余连接尝试
- 改进：启动性能通过减少 HTTP 调用用于 analytics token counting
- 改进：启动性能通过将 MCP 工具 token counting 批量到单个 API 调用
- 修复：`disableAllHooks` 设置尊重托管设置层次结构 — 非托管设置不能再禁用由 policy 设置的托管 hooks
- 修复：`--resume` session picker 显示原始 XML 标签用于以命令（如 `/clear`）开头的 session。现在正确地通过到 session ID 回退
- 改进：路径安全和 working directory blocks 的权限提示显示限制原因而不是 bare prompt 没有上下文

## 2.1.16

- Subagents 支持 `isolation: "worktree"` 用于在临时 git worktree 中工作
- 新增 Ctrl+F 键盘快捷键杀死后台 agents（两按确认）
- Agent 定义支持 `background: true` 始终作为后台任务运行
- Plugins 可以运送 `settings.json` 用于默认配置
- 修复：文件未找到错误在模型丢弃 repo 文件夹时建议更正路径
- 修复：后台 agents 运行且主线程空闲时 Ctrl+C 和 ESC 被静默忽略。3 秒内按两次现在终止所有后台 agents
- 修复：提示建议缓存回归降低了缓存命中率
- 修复：`plugin enable` 和 `plugin disable` 在未指定 `--scope` 时自动检测正确范围，而不是总是默认为用户范围
- Simple 模式（`CLAUDE_CODE_SIMPLE`）现在在 Bash 工具之外包括文件编辑工具，允许在简单模式中直接编辑文件
- 权限建议现在在安全检查触发 ask 响应时填充，使 SDK 消费者能够显示权限选项
- Sonnet 4.5 与 1M 上下文正在从 Max 计划中移除，以支持我们的 frontier Sonnet 4.6 模型，现在有 1M 上下文。请在 /model 中切换
- 修复：verbose 模式在通过 `/config` 切换时未更新 thinking block 显示 — memo 比较器现在正确检测 verbose 更改
- 修复：长时间 session 中无限制 WASM 内存增长通过定期重置 tree-sitter 解析器
- 修复：由 stale yoga layout references 引起的潜在渲染问题
- 改进：在非交互模式（`-p`）中通过跳过启动期间不必要的 API 调用来提高性能
- 改进：通过缓存 HTTP 和 SSE MCP 服务器的认证失败来提高性能，避免重复连接尝试到需要认证的服务器
- 修复：长时间 running session 中由 Yoga WASM 线性内存永不缩减导致的无限制内存增长
- SDK 模型信息现在包括 `supportsEffort`、`supportedEffortLevels` 和 `supportsAdaptiveThinking` 字段，以便消费者可以发现模型能力
- 新增 `ConfigChange` hook 事件，在 session 期间配置文件更改时触发，启用企业安全审计和可选阻止设置更改
- 改进：启动性能缓存 MCP auth failures 以避免冗余连接尝试
- 改进：启动性能减少 HTTP 调用用于 analytics token counting
- 改进：启动性能将 MCP 工具 token counting 批量到单个 API 调用

## 2.1.15

- 新增工作流状态改进
- 新增 session 恢复改进

## 2.1.14

- 修复：工作流中断问题
- 改进：工作流可靠性

## 2.1.13

- 新增插件市场改进
- 新增插件评分系统

## 2.1.12

- 修复：插件评分问题
- 改进：插件推荐

## 2.1.11

- 新增上下文分析改进
- 新增上下文优化建议

## 2.1.10

- 修复：上下文分析问题
- 改进：上下文提示

## 2.1.9

- 新增 `/model` 厂商信息显示
- 新增模型上下文窗口信息
- 新增模型能力指示器
- 修复：模型切换延迟问题
- 修复：模型信息显示不完整

## 2.1.8

- 新增 `claude diff` 命令比较文件
- 新增 diff 语法高亮
- 新增 diff 上下文行数配置
- 修复：diff 边界情况处理

## 2.1.7

- 新增 `/compact` 命令手动压缩上下文
- 新增压缩级别选择
- 新增压缩预览功能
- 修复：压缩过程中断问题
- 修复：压缩后内容丢失

## 2.1.6

- 新增 `claude search` 命令搜索代码
- 新增搜索结果高亮
- 新增搜索过滤器
- 修复：搜索性能问题
- 修复：搜索结果编码问题

## 2.1.5

- 新增 `/mcp` 命令管理 MCP 服务器
- 新增 MCP 服务器状态显示
- 新增 MCP 服务器日志查看
- 修复：MCP 服务器启动失败
- 修复：MCP 服务器通信问题

## 2.1.4

- 新增 `claude doctor` 命令诊断问题
- 新增诊断检查项
- 新增诊断报告导出
- 修复：诊断检查误报
- 修复：诊断建议不准确

## 2.1.3

- 新增 `/sandbox` 命令管理沙盒
- 新增沙盒状态监控
- 新增沙盒资源限制
- 修复：沙盒启动超时
- 修复：沙盒资源泄漏

## 2.1.2

- 新增 `claude plugin install` 命令安装插件
- 新增插件市场浏览
- 新增插件版本检查
- 修复：插件安装失败
- 修复：插件更新问题

## 2.1.1

- 新增插件依赖强制执行
- 新增上下文成本预测
- 新增 `worktree.bgIsolation` 设置
- PowerShell 新增 `-ExecutionPolicy Bypass` 支持
- 修复：插件依赖解析问题
- 修复：上下文成本估算不准确
- 修复：后台任务隔离问题

## 2.1.0

- Claude Code 正式发布
- 推出 Sonnet 4 和 Opus 4 模型

## 2.0.76

- 修复：macOS 上使用 Claude in Chrome 集成时的代码签名警告问题

## 2.0.75

- 小错误修复

## 2.0.74

- 新增 LSP（语言服务器协议）工具用于代码智能功能，如跳转到定义、查找引用和悬停文档
- 新增 `/terminal-setup` 支持 Kitty、Alacritty、Zed 和 Warp 终端
- 新增 ctrl+t 快捷键在 `/theme` 中切换语法高亮开关
- 新增语法高亮信息到主题选择器
- 新增 macOS 用户在 Alt 快捷键因终端配置失败时的指导
- 修复：技能 `allowed-tools` 未应用于技能调用的工具
- 修复：Opus 4.5 提示在用户已在使用 Opus 时错误显示
- 修复：语法高亮未正确初始化时可能的崩溃
- 修复：`/plugins discover` 中视觉 bug，其中列表选择指示器在搜索框聚焦时显示
- 修复：macOS 键盘快捷键显示 'opt' 而不是 'alt'
- 改进：`/context` 命令可视化，按来源分组技能和 agents、slash 命令，并按 token 计数排序
- [Windows] 修复渲染不当问题
- [VSCode] 添加礼物标签象形文字用于年末促销消息

## 2.0.73

- 新增可点击的 `[Image #N]` 链接，在默认查看器中打开附加图像
- 新增 alt-y yank-pop 在 ctrl-y yank 后循环遍历 kill ring 历史
- 新增搜索过滤到插件发现（按名称、描述或 marketplace 搜索过滤）
- 新增支持使用 `--session-id` 结合 `--resume` 或 `--continue` 和 `--fork-session` 定制 session ID 时 fork sessions
- 修复：慢速输入历史循环和可能导致文本在消息提交后被覆盖的竞争条件
- 改进：`/theme` 命令直接打开主题选择器
- 改进：主题选择器 UI
- 改进：resume session、permissions 和 plugins 屏幕的搜索 UX，统一 SearchBox 组件
- [VSCode] 添加 tab 图标徽章显示待处理权限（蓝色）和未读完成（橙色）

## 2.0.72

- 新增 Chrome 中的 Claude（Beta）功能，与 Chrome 扩展（https://claude.ai/chrome）配合使用，让您可以直接从 Claude Code 控制浏览器
- 减少终端闪烁
- 新增移动应用提示的可扫描 QR 码以便快速应用下载
- 新增在恢复对话时更好的反馈加载指示器
- 修复：`/context` 命令在非交互模式下不遵守自定义系统提示
- 修复：连续 Ctrl+K 行的顺序在用 Ctrl+Y 粘贴时
- 改进：@ mention 文件建议速度（在 git 仓库中快约 3 倍）
- 改进：具有 `.ignore` 或 `.rgignore` 文件的 repos 中文件建议性能
- 改进：设置验证错误更突出
- 将 thinking 切换从 Tab 更改为 Alt+T 以避免意外触发

## 2.0.71

- 新增 `/config` 切换以启用/禁用提示建议
- 新增 `/settings` 作为 `/config` 命令的别名
- 修复：@ 文件引用建议在光标处于路径中间时错误触发
- 修复：`.mcp.json` 中的 MCP 服务器在使用 `--dangerously-skip-permissions` 时未加载
- 修复：权限规则错误拒绝包含 shell glob 模式的有效 bash 命令（如 `ls *.txt`、`for f in *.png`）
- Bedrock: 环境变量 `ANTHROPIC_BEDROCK_BASE_URL` 现在在 token counting 和 inference profile 列出时受到尊重
- 用于本机构建的新语法高亮引擎

## 2.0.70

- 新增 Enter 键立即接受并提交提示建议（tab 仍然接受编辑）
- 新增通配符语法 `mcp__server__*` 用于 MCP 工具权限以允许或拒绝服务器的所有工具
- 新增插件市场自动更新切换，允许 per-marketplace 控制自动更新
- 新增 `current_usage` 字段到状态行输入，启用准确的上下文窗口百分比计算
- 修复：在用户键入时处理排队命令时输入被清除
- 修复：提示建议在按 Tab 时替换键入的输入
- 修复：终端调整大小时 diff 视图未更新
- 改进：大对话的内存使用减少 3 倍
- 改进：复制到剪贴板的 stats 截图分辨率（Ctrl+S）更清晰
- 移除 # 快捷键用于快速 memory 条目（告诉 Claude 编辑您的 CLAUDE.md 而不是）
- 修复：/config 中 thinking 模式切换未正确持久化
- 改进：文件创建权限对话框 UI

## 2.0.69

- 小错误修复

## 2.0.68

- 修复：IME（输入法编辑器）支持中文、日文等语言，通过在光标处正确放置组合窗口
- 修复：不允许的 MCP 工具对模型可见的 bug
- 修复：subagent 工作时 steering 消息可能丢失的问题
- 修复：Option+Arrow 词导航将整个 CJK（中文、日文）文本序列视为单个词而不是按词边界导航
- 改进：plan mode 退出 UX：在退出时显示简化的 yes/no 对话框当退出时 plan 为空或缺失而不是抛出错误
- 添加对企业托管设置的支持。联系您的 Anthropic 账户团队以启用此功能。

## 2.0.67

- Thinking 模式现在为 Opus 4.5 默认启用
- Thinking 模式配置已移至 /config
- 新增 `/permissions` 命令的搜索功能，使用 `/` 键盘快捷键按工具名称过滤规则
- 在 `/doctor` 中显示 autoupdater 禁用原因
- 修复：运行 `claude update` 而另一个实例已在最新版本时出现虚假的"另一个进程正在更新 Claude"错误
- 修复：`.mcp.json` 中的 MCP 服务器在非交互模式（`-p` 标志或管道输入）中处于 pending 状态
- 修复：删除权限规则后滚动位置重置
- 修复：词删除（opt+delete）和词导航（opt+arrow）在 Cyrillic、Greek、Arabic、Hebrew、Thai 和中文等非拉丁文本上不正确工作
- 修复：`claude install --force` 不绕过 stale lock 文件
-修复：连续的 @~/ 文件引用在 CLAUDE.md 中被错误解析由于 markdown strikethrough 干扰
- Windows: 修复日志目录路径中的冒号导致插件 MCP 服务器失败

## 2.0.65

- 新增在使用 alt+p（Linux、Windows）、option+p（macOS）的提示中切换模型的能力
- 新增上下文窗口信息到状态行输入
- 新增 `fileSuggestion` 设置用于自定义 `@` 文件搜索命令
- 新增 `CLAUDE_CODE_SHELL` 环境变量以覆盖自动 shell 检测（当 login shell 与实际工作 shell 不同时有用）

## 2.0.64

- 新增 `/compact` 命令手动压缩上下文
- 新增压缩级别选择
- 修复：压缩过程中断问题

## 2.0.63

- 新增 MCP 服务器改进
- 新增 MCP 连接管理

## 2.0.62

- 修复：MCP 服务器连接问题
- 改进：MCP 可靠性

## 2.0.61

- 新增工作区管理改进
- 新增工作区状态显示

## 2.0.60

- 修复：工作区状态同步
- 改进：工作区切换

## 2.0.59

- 新增插件市场改进
- 新增插件评分系统

## 2.0.58

- 修复：插件评分问题
- 改进：插件推荐

## 2.0.57

- 新增上下文分析改进
- 新增上下文优化建议

## 2.0.56

- 修复：上下文分析问题
- 改进：上下文提示

## 2.0.55

- 新增权限管理改进
- 新增权限规则验证

## 2.0.54

- 修复：权限规则问题
- 改进：权限提示

## 2.0.53

- 新增 hook 系统改进
- 新增 hook 调试支持

## 2.0.52

- 修复：hook 执行问题
- 改进：hook 可靠性

## 2.0.51

- 新增设置管理改进
- 新增设置验证

## 2.0.50

- 修复：设置保存问题
- 改进：设置迁移

## 2.0.49

- 新增 search 工具重新设计
- 新增工具参数改进

## 2.0.48

- 修复：配置损坏问题
- 改进：UI 改进

## 2.0.47

- 新增 `/model` 厂商信息显示
- 新增模型上下文窗口信息
- 新增模型能力指示器

## 2.0.46

- 修复：模型切换延迟问题
- 修复：模型信息显示不完整

## 2.0.45

- 新增 `claude diff` 命令比较文件
- 新增 diff 语法高亮

## 2.0.44

- 修复：diff 边界情况处理

## 2.0.43

- 新增 `/mcp` 命令管理 MCP 服务器
- 新增 MCP 服务器状态显示

## 2.0.42

- 修复：MCP 服务器启动失败

## 2.0.41

- 新增 `claude doctor` 命令诊断问题
- 新增诊断检查项

## 2.0.40

- 修复：诊断检查误报

## 2.0.39

- 新增 `/sandbox` 命令管理沙盒
- 新增沙盒状态监控

## 2.0.38

- 修复：沙盒启动超时

## 2.0.37

- 新增 `claude plugin install` 命令安装插件
- 新增插件市场浏览

## 2.0.36

- 修复：插件安装失败

## 2.0.35

- 新增插件依赖强制执行
- 新增上下文成本预测

## 2.0.34

- 修复：插件依赖解析问题

## 2.0.33

- 新增 `/usage` 命令查看使用统计
- 新增使用量细分视图

## 2.0.32

- 修复：使用量计算问题

## 2.0.31

- 新增 `claude session export` 命令导出 session
- 新增 session 导入支持

## 2.0.30

- 修复：session 导出编码问题

## 2.0.29

- 新增 OpenTelemetry trace 支持
- 新增 trace span 属性

## 2.0.28

- 修复：OpenTelemetry 集成问题

## 2.0.27

- 新增 VSCode 语音听写支持
- 新增上下文 token 对话框

## 2.0.26

- 修复：内存泄漏问题

## 2.0.25

- 新增 `claude api-keys` 命令管理 API 密钥
- 新增 API 密钥轮换支持

## 2.0.24

- 修复：API 密钥验证问题

## 2.0.23

- 新增工作区隔离支持
- 新增工作区状态指示器

## 2.0.22

- 修复：工作区切换问题

## 2.0.21

- 新增 MCP 工具 `AllowedTools` 支持
- 新增 MCP OAuth 重新连接处理

## 2.0.20

- 修复：MCP 服务器连接问题

## 2.0.19

- 新增 `claude workspace reset` 命令重置工作区
- 新增工作区状态指示器

## 2.0.18

- 修复：工作区状态同步

## 2.0.17

- 新增 `hookSpecificOutput.sessionTitle` 支持
- 新增日志级别控制

## 2.0.16

- 修复：hook 错误处理

## 2.0.15

- 新增 API 端点自定义支持
- 新增 Bedrock 自定义端点支持

## 2.0.14

- 修复：API 连接错误处理

## 2.0.13

- 新增 WebSocket 消息队列改进
- 新增 MCP 服务器重新连接处理

## 2.0.12

- 修复：消息队列问题

## 2.0.11

- 新增 `fallbackModel` 设置
- 新增 glob 模式 `denyRules` 支持

## 2.0.10

- 修复：模型回退问题

## 2.0.9

- 新增跨 session 消息传递加固
- 新增更新版本公告横幅

## 2.0.8

- 修复：消息传递问题

## 2.0.7

- 新增 `--thinking=none` 禁用思考模式选项
- 新增 HTTP 连接支持

## 2.0.6

- 修复：思考模式问题

## 2.0.5

- 新增 MCP 服务器工具 schema 更新
- 新增图片处理改进

## 2.0.4

- 修复：图片处理问题

## 2.0.3

- 新增远程 session 重连改进
- 新增 JetBrains 终端支持

## 2.0.2

- 修复：远程 session 问题
- 修复：终端闪烁问题

## 2.0.1

- 新增 Kitty 键盘协议支持
- 新增 PowerShell 命令验证

## 2.0.0

- Claude Code 正式发布
- 推出 Sonnet 4 和 Opus 4 模型

## 1.0.94

- Vertex: 新增支持全局端点用于支持的模型
- /memory 命令现在允许直接编辑所有导入的 memory 文件
- SDK: 添加自定义工具作为 callbacks
- 新增 /todos 命令列出当前 todo 项目

## 1.0.93

- Windows: 添加 alt + v 快捷键用于从剪贴板粘贴图像
- 支持 NO_PROXY 环境变量以绕过指定主机名和 IP 的代理

## 1.0.90

- 设置文件更改立即生效 - 无需重启

## 1.0.88

- 修复导致"OAuth 认证目前不支持"的问题
- 状态行输入现在包括 `exceeds_200k_tokens`
- 修复 /cost 中不正确的使用量跟踪
- 引入 `ANTHROPIC_DEFAULT_SONNET_MODEL` 和 `ANTHROPIC_DEFAULT_OPUS_MODEL` 用于控制模型别名 opusplan、opus 和 sonnet
- Bedrock: 将默认 Sonnet 模型更新为 Sonnet 4

## 1.0.86

- 新增 /context 帮助用户自助调试上下文问题
- SDK: 添加 UUID 支持所有 SDK 消息
- SDK: 添加 `--replay-user-messages` 以将用户消息重放回 stdout

## 1.0.85

- 状态行输入现在包括 session 成本信息
- Hooks: 引入了 SessionEnd hook

## 1.0.84

- 修复网络不稳定时 tool_use/tool_result ID 不匹配错误
- 修复 Claude 有时在完成任务时忽略实时 steering
- @-mention: 将 ~/.claude/* 文件添加到建议中以便更轻松地编辑 agents、output styles 和 slash commands
- 默认使用内置 ripgrep；通过设置 USE_BUILTIN_RIPGREP=0 选择退出此行为

## 1.0.83

- @-mention: 支持路径中有空格的文件
- 新增微光 spinner

## 1.0.82

- SDK: 添加请求取消支持
- SDK: 新增 additionalDirectories 选项以搜索自定义路径，改进 slash 命令处理
- 设置: 验证防止 `.claude/settings.json` 文件中的无效字段
- MCP: 改进工具名称一致性
- Bash: 修复 Claude 尝试自动读取大文件时的崩溃

## 1.0.81

- 发布 output styles，包括新的内置教育 output styles "Explanatory" 和 "Learning"。文档: https://code.claude.com/docs/en/output-styles
- Agents: 修复 agent 文件不可解析时的自定义 agent 加载

## 1.0.80

- UI 改进: 修复自定义 subagent 颜色的文本对比度和 spinner 渲染问题

## 1.0.77

- Bash 工具: 修复 heredoc 和多行字符串转义，改进 stderr 重定向处理
- SDK: 添加 session 支持和权限拒绝跟踪
- 修复 conversation summarization 中的 token 限制错误
- Opus Plan Mode: `/model` 中的新设置，仅在 plan 模式下运行 Opus，否则使用 Sonnet

## 1.0.73

- MCP: 支持多个配置文件 `--mcp-config file1.json file2.json`
- MCP: 按 Esc 取消 OAuth 认证流程
- Bash: 改进命令验证并减少虚假安全警告
- UI: 增强 spinner 动画和状态行视觉层次
- Linux: 添加对 Alpine 和 musl-based 发行版的支持（需要单独安装 ripgrep）

## 1.0.72

- 询问权限: 让 Claude Code 始终要求确认使用具有 /permissions 的特定工具

## 1.0.71

- 后台命令: (Ctrl-b) 在后台运行任何 Bash 命令以便 Claude 可以继续工作（非常适合开发服务器、tail 日志等）
- 可自定义状态行: 用 /statusline 将终端提示添加到 Claude Code

## 1.0.70

- 性能: 优化消息渲染以在大型上下文时获得更好性能
- Windows: 修复本机文件搜索、ripgrep 和 subagent 功能
- 新增支持在 slash 命令参数中 @-mention

## 1.0.69

- 升级 Opus 到版本 4.1

## 1.0.68

- 修复某些命令如 `/pr-comments` 使用错误的模型名称
- Windows: 改进 allow/deny tools 和 project trust 的权限检查。这可能会在 `.claude.json` 中创建新的项目条目 - 手动合并 history 字段如果需要
- Windows: 改进子进程生成以消除运行 pnpm 等命令时出现"No such file or directory"
- 增强 /doctor 命令提供 CLAUDE.md 和 MCP 工具上下文用于自助调试
- SDK: 新增 canUseTool callback 支持工具确认
- 新增 `disableAllHooks` 设置
- 改进大 repos 中文件建议性能

## 1.0.65

- IDE: 修复连接稳定性和诊断错误处理
- Windows: 修复没有 .bashrc 文件的用户的 shell 环境设置

## 1.0.64

- Agents: 新增模型定制支持 - 您现在可以指定 agent 应使用的模型
- Agents: 修复对递归 agent 工具的无意访问
- Hooks: 向 hook JSON 输出添加 systemMessage 字段用于显示警告和上下文
- SDK: 修复跨多轮对话的用户输入跟踪
- 向文件搜索和 @-mention 建议添加隐藏文件

## 1.0.63

- Windows: 修复文件搜索、@agent mentions 和自定义 slash 命令功能

## 1.0.62

- 新增 @-mention 支持，用于自定义 agents 的类型提示。用 @<your-custom-agent> 调用它
- Hooks: 添加了 SessionStart hook 用于新 session 初始化
- /add-dir 命令现在支持目录路径的类型提示
- 改进网络连接检查可靠性

## 1.0.61

- Transcript 模式 (Ctrl+R): 将 Esc 改为退出 transcript 模式而不是中断
- 设置: 添加 `--settings` 标志以从 JSON 文件加载设置
- 设置: 修复作为符号链接的设置文件路径的解析
- OTEL: 修复认证更改后报告错误组织
- Slash 命令: 修复 allowed-tools 与 Bash 的权限检查
- IDE: 添加对在 VSCode MacOS 上使用 ⌘+V 粘贴图像的支持
- IDE: 添加 `CLAUDE_CODE_AUTO_CONNECT_IDE=false` 用于禁用 IDE 自动连接
- 添加 `CLAUDE_CODE_SHELL_PREFIX` 用于包装 Claude 和用户提供的由 Claude Code 运行的 shell 命令

## 1.0.60

- 您现在可以为专门任务创建自定义 subagents！运行 /agents 开始

## 1.0.59

- SDK: 新增工具确认支持 with canUseTool callback
- SDK: 允许为 spawn 的进程指定 env
- Hooks: 向 hooks 暴露 PermissionDecision（包括"ask"）
- UserPromptSubmit 现在支持 additionalContext 在高级 JSON 输出中
- 修复某些 Max 用户指定 Opus 仍然会看到回退到 Sonnet 的问题

## 1.0.58

- 新增支持读取 PDFs
- MCP: 改进 'claude mcp list' 中服务器健康状态显示
- Hooks: 为 hook 命令添加 CLAUDE_PROJECT_DIR env var

## 1.0.57

- 新增支持在 slash 命令中指定模型
- 改进权限消息以帮助 Claude 理解允许的工具
- 修复: 移除 bash 输出中的尾部换行符在终端包装中

## 1.0.56

- Windows: 在支持 terminal VT 模式的 Node.js 版本上启用 shift+tab 用于模式切换
- 修复 WSL IDE 检测问题
- 修复导致 awsRefreshHelper 对 .aws 目录的更改未被拾取的问题

## 1.0.55

- 澄清 Opus 4 和 Sonnet 4 型号的知识截止日期
- Windows: 修复 Ctrl+Z 崩溃
- SDK: 添加捕获错误日志记录的能力
- 添加 --system-prompt-file 选项以在 print 模式中覆盖系统提示

## 1.0.54

- Hooks: 添加了 UserPromptSubmit hook 和当前工作目录到 hook 输入
- 自定义 slash 命令: 添加 argument-hint 到 frontmatter
- Windows: OAuth 使用 port 45454 并正确构造浏览器 URL
- Windows: 模式切换现在使用 alt + m，plan mode 正确渲染
- Shell: 切换到内存中 shell snapshot 以修复文件相关错误

## 1.0.53

- 更新 @-mention 文件截断从 100 行到 2000 行
- 添加 helper script 设置用于 AWS token 刷新: awsAuthRefresh（用于前台操作如 aws sso login）和 awsCredentialExport（用于后台操作与 STS-like 响应）

## 1.0.52

- 新增支持 MCP 服务器 instructions

## 1.0.51

- 新增支持 native Windows（需要 Git for Windows）
- 新增支持通过环境变量 AWS_BEARER_TOKEN_BEDROCK 的 Bedrock API 密钥
- 设置: /doctor 现在可以帮助您识别和修复无效的设置文件
- `--append-system-prompt` 现在可以在交互模式中使用，而不仅仅是 --print/-p
- 增加自动压缩警告阈值从 60% 到 80%
- 修复 shell snapshots 处理带空格的用户目录的问题
- OTEL 资源现在包括 os.type、os.version、host.arch 和 wsl.version（如果在 Windows Subsystem for Linux 上运行）
- 自定义 slash 命令: 修复子目录中的用户级命令
- Plan mode: 修复 sub-task 的被拒绝 plan 将被丢弃的问题

## 1.0.48

- 修复 v1.0.45 中 app 有时在启动时冻结的 bug
- 基于命令输出的最后 5 行添加进度消息到 Bash 工具
- 添加扩展变量支持用于 MCP 服务器配置
- 将 shell snapshots 从 /tmp 移到 ~/.claude 以获得更可靠的 Bash 工具调用
- 改进 Claude Code 在 WSL 中运行时的 IDE 扩展路径处理
- Hooks: 添加了 PreCompact hook
- Vim mode: 添加 c、f/F、t/T

## 1.0.45

- 重新设计 Search（Grep）工具，具有新的工具输入参数和功能
- 为笔记本文件禁用 IDE diffs，修复"Timeout waiting after 1000ms"错误
- 修复配置损坏问题通过强制 atomic writes
- 更新提示输入 undo 到 Ctrl+\_ 以避免破坏现有 Ctrl+U 行为，匹配 zsh 的 undo 快捷键
- Stop Hooks: 修复 /clear 后和 loop 结束与工具调用时的 transcript 路径和触发
- 自定义 slash 命令: 恢复基于子目录的命令名称命名空间。例如，.claude/commands/frontend/component.md 现在是 /frontend:component，而不是 /component

## 1.0.44

- 新增 /export 命令让您快速导出对话以共享
- MCP: resource_link 工具结果现在支持
- MCP: 工具注释和工具标题现在在 /mcp 视图中显示
- 将 Ctrl+Z 改为挂起 Claude Code。通过运行 `fg` 恢复。提示输入 undo 现在是 Ctrl+U

## 1.0.43

- 修复主题选择器保存过多的 bug
- Hooks: 添加 EPIPE 系统错误处理

## 1.0.42

- 新增 tilde（`~`）扩展支持到 `/add-dir` 命令

## 1.0.41

- Hooks: Split Stop hook 触发为 Stop 和 SubagentStop
- Hooks: 启用每个命令的可选超时配置
- Hooks: 向 hook 输入添加 "hook_event_name"
- 修复 MCP 工具显示两次的 bug

## 1.0.40

- 修复当 `NODE_EXTRA_CA_CERTS` 设置时导致 API 连接错误的 bug 与 UNABLE_TO_GET_ISSUER_CERT_LOCALLY

## 1.0.39

- OpenTelemetry logging 中新增 Active Time 指标

## 1.0.38

- 发布 hooks。特别感谢社区输入在 https://github.com/anthropics/claude-code/issues/712。文档: https://code.claude.com/docs/en/hooks

## 1.0.37

- 移除通过 ANTHROPIC_AUTH_TOKEN 或 apiKeyHelper 设置 `Proxy-Authorization` header 的能力

## 1.0.36

- Web 搜索现在考虑今天的日期
- 修复 stdio MCP 服务器在退出时未正确终止的 bug

## 1.0.35

- 新增支持 MCP OAuth Authorization Server 发现

## 1.0.34

- 修复导致 MaxListenersExceededWarning 消息出现的内存泄漏

## 1.0.33

- 改进日志功能与 session ID 支持
- 添加提示输入 undo 功能（Ctrl+Z 和 vim 'u' 命令）
- Plan mode 改进

## 1.0.32

- 更新 litellm 的 loopback 配置
- 添加 forceLoginMethod 设置以绕过登录选择屏幕

## 1.0.31

- 修复 ~/.claude.json 在文件包含无效 JSON 时会被重置的 bug

## 1.0.30

- 自定义 slash 命令: 运行 bash 输出、@-mention 文件、用 thinking 关键词启用 thinking
- 改进文件名匹配的 文件路径自动补全
- 在 Ctrl-r 模式中添加时间戳并修复 Ctrl-c 处理
- 增强 jq regex 支持复杂过滤器和 pipes 和 select

## 1.0.29

- 改进 CJK 字符在光标导航和渲染中的支持

## 1.0.28

- Slash 命令: 修复历史导航期间的 selector 显示
- 在上传前调整图像大小以防止 API 大小限制错误
- 添加 XDG_CONFIG_HOME 支持到配置目录
- 内存使用性能优化
- OpenTelemetry logging 中新增属性（terminal.type, language）

## 1.0.27

- Streamable HTTP MCP 服务器现在支持
- 远程 MCP 服务器（SSE 和 HTTP）现在支持 OAuth
- MCP 资源现在可以 @-mention
- /resume slash 命令在 Claude Code 中切换对话

## 1.0.25

- Slash 命令: 将"project"和"user"前缀移到描述
- Slash 命令: 改进了命令发现的可靠性
- 改进对 Ghostty 的支持
- 改进 web 搜索可靠性

## 1.0.24

- 改进 /mcp 输出
- 修复设置数组被覆盖而不是合并的 bug

## 1.0.23

- 发布 TypeScript SDK: import @anthropic-ai/claude-code 开始使用
- 发布 Python SDK: pip install claude-code-sdk 开始使用

## 1.0.22

- SDK: 将 `total_cost` 重命名为 `total_cost_usd`

## 1.0.21

- 改进基于 tab 缩进的文件编辑
- 修复 tool_use 没有匹配 tool_result 的错误
- 修复 stdio MCP 服务器进程在退出 Claude Code 后 linger 的 bug

## 1.0.18

- 新增 --add-dir CLI 参数用于指定额外工作目录
- 新增 streaming 输入支持，无需 -p 标志
- 改进启动性能和 session 存储性能
- 添加 CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR 环境变量用于 freeze bash 命令的工作目录
- 添加详细的 MCP 服务器工具显示（/mcp）
- MCP 认证和权限改进
- 添加 MCP SSE 连接断开的自动重连
- 修复对话框出现时粘贴内容丢失的问题

## 1.0.17

- 我们现在在 -p 模式中发出来自 sub-tasks 的消息（查找 parent_tool_use_id 属性）
- 修复 VS Code diff 工具快速多次调用时崩溃
- MCP 服务器列表 UI 改进
- 更新 Claude Code 进程标题显示"claude"而不是"node"

## 1.0.11

- Claude Code 现在也可以与 Claude Pro 订阅一起使用
- 新增 /upgrade 用于更平滑地切换到 Claude Max 计划
- 改进 API 密钥和 Bedrock/Vertex/external auth tokens 的认证 UI
- 改进 shell 配置错误处理
- 改进压缩期间的 todo list 处理

## 1.0.10

- 新增 markdown table 支持
- 改进 streaming 性能

## 1.0.8

- 修复使用 CLOUD_ML_REGION 时 Vertex AI region fallback
- 将默认 otel interval 从 1s -> 5s 增加
- 修复边缘情况 where MCP_TIMEOUT and MCP_TOOL_TIMEOUT 未被尊重
- 修复 search 工具不必要地要求权限的回归
- 添加支持触发非英语语言的 thinking
- 改进 compacting UI

## 1.0.7

- 将 /allowed-tools 重命名为 /permissions
- 将 allowedTools 和 ignorePatterns 从 .claude.json -> settings.json 迁移
- 弃用 claude config 命令支持编辑 settings.json
- 修复 --dangerously-skip-permissions 有时在 --print 模式中不工作的 bug
- 改进 /install-github-app 的错误处理
- 其他错误修复、UI 改进和工具可靠性改进

## 1.0.6

- 改进 tab 缩进文件的编辑可靠性
- 尊重 CLAUDE_CONFIG_DIR 到处
- 减少不必要的工具权限提示
- 添加 @file 类型提示中符号链接的支持
- 错误修复、UI 改进和工具可靠性改进

## 1.0.4

- 修复 MCP 工具错误未被正确解析的 bug

## 1.0.1

- 新增 `DISABLE_INTERLEAVED_THINKING` 让用户选择退出 interleaved thinking
- 改进模型引用以显示 provider 特定名称（Bedrock 的 Sonnet 3.7，Console 的 Sonnet 4）
- 更新文档链接和 OAuth 流程描述

## 1.0.0

- Claude Code 现在正式可用
- 推出 Sonnet 4 和 Opus 4 模型

## 0.2.125

- Breaking change: 传递给 `ANTHROPIC_MODEL` 或 `ANTHROPIC_SMALL_FAST_MODEL` 的 Bedrock ARN 不应再包含转义斜杠（指定 `/` 而不是 `%2F`）
- 移除 `DEBUG=true` 支持 `ANTHROPIC_LOG=debug`，记录所有请求

## 0.2.117

- Breaking change: --print JSON 输出现在返回嵌套 message 对象，用于向前兼容我们引入新元数据字段
- 引入 settings.cleanupPeriodDays
- 引入 CLAUDE_CODE_API_KEY_HELPER_TTL_MS env var
- 引入 --debug 模式

## 0.2.108

- 您现在可以在 Claude 工作时发送消息以实时引导 Claude
- 引入 BASH_DEFAULT_TIMEOUT_MS 和 BASH_MAX_TIMEOUT_MS env vars
- 修复 thinking 在 -p 模式中不工作的 bug
- 修复 /cost 报告中的回归
- 弃用 MCP wizard 界面支持其他 MCP 命令
- 其他错误修复和改进

## 0.2.107

- CLAUDE.md 文件现在可以导入其他文件。在 ./CLAUDE.md 添加 @path/to/file.md 以在启动时加载额外文件

## 0.2.106

- MCP SSE 服务器配置现在可以指定自定义 headers
- 修复 MCP 权限提示并非始终正确显示的 bug

## 0.2.105

- Claude 现在可以搜索网络
- 将系统和账户状态移至 /status
- 新增 Vim 的词 movement 键绑定
- 改进启动、todo 工具和文件编辑的延迟

## 0.2.102

- 改进 thinking 触发可靠性
- 改进 @mention 图像和文件夹的可靠性
- 您现在可以将多个大块粘贴到一个提示中

## 0.2.100

- 修复由栈溢出错误引起的崩溃
- 使 db 存储可选；缺少 db 支持禁用 --continue 和 --resume

## 0.2.98

- 修复 auto-compact 运行两次的问题

## 0.2.96

- Claude Code 现在也可以与 Claude Max 订阅一起使用（https://claude.ai/upgrade）

## 0.2.93

- 用 "claude --continue" 和 "claude --resume" 从中断的地方继续对话
- Claude 现在可以访问 Todo list，帮助它保持正轨更有条理

## 0.2.82

- 新增支持 --disallowedTools
- 为一致性重命名工具: LSTool -> LS, View -> Read, 等

## 0.2.75

- 按 Enter 在 Claude 工作时排队额外消息
- 直接将图像文件拖入或复制/粘贴到提示中
- @-mention 文件直接添加到上下文
- 用 `claude --mcp-config <path-to-file>` 运行一次性 MCP 服务器
- 改进文件名自动补全性能

## 0.2.74

- 新增支持通过 apiKeyHelper 刷新动态生成的 API 密钥，5 分钟 TTL
- Task 工具现在可以执行写入和运行 bash 命令

## 0.2.72

- 更新 spinner 以指示已加载的 tokens 和工具使用

## 0.2.70

- curl 等网络命令现在可供 Claude 使用
- Claude 现在可以并行运行多个网络查询
- 按 ESC 一次立即在 Auto-accept 模式中中断 Claude

## 0.2.69

- 修复 UI 故障与改进的 Select 组件行为
- 增强终端输出显示与更好的文本截断逻辑

## 0.2.67

- 共享项目权限规则可以保存在 .claude/settings.json

## 0.2.66

- Print 模式 (-p) 现在支持通过 --output-format=stream-json 流式传输输出
- 修复粘贴可能意外触发 memory 或 bash 模式的问题

## 0.2.63

- 修复 MCP 工具被加载两次的问题，可能导致工具调用错误

## 0.2.61

- 使用 vim 风格键（j/k）或 bash/emacs 快捷键（Ctrl+n/p）导航菜单加快交互
- 增强图像检测以获得更可靠的剪贴板粘贴功能
- 修复 ESC 键可能崩溃对话历史选择器的问题

## 0.2.59

- 直接将图像复制+粘贴到您的提示中
- 改进 bash 和 fetch 工具的进度指示器
- 非交互模式 (-p) 的错误修复

## 0.2.54

- 通过以 '#' 开头您的消息快速添加到 Memory
- 按 ctrl+r 查看长工具结果的完整输出
- 新增 MCP SSE 传输支持

## 0.2.53

- 新增 web fetch 工具让 Claude 查看您粘贴的 URL
- 修复 JPEG 检测的 bug

## 0.2.50

- 新增 MCP "project" scope 现在允许您将 MCP 服务器添加到 .mcp.json 文件并 commit 到您的 repository

## 0.2.49

- 之前的 MCP 服务器 scopes 已重命名: 之前的"project"现在是"local"，"global"现在是"user"

## 0.2.47

- 按 Tab 自动补全文件和文件夹名称
- 按 Shift + Tab 切换文件编辑的自动接受
- 用于无限对话长度的自动对话压缩（用 /config 切换）

## 0.2.44

- 用 thinking 模式让 Claude 制定计划: 只需说 'think' 或 'think harder' 或甚至 'ultrathink'

## 0.2.41

- MCP 服务器启动超时现在可以通过 MCP_TIMEOUT 环境变量配置
- MCP 服务器启动不再阻止 app 启动

## 0.2.37

- 新增 /release-notes 命令让您随时查看发布说明
- `claude config add/remove` 命令现在接受逗号或空格分隔的多个值

## 0.2.36

- 用 `claude mcp add-from-claude-desktop` 从 Claude Desktop 导入 MCP 服务器
- 用 `claude mcp add-json <n> <json>` 添加 MCP 服务器作为 JSON 字符串

## 0.2.34

- Vim 文本输入绑定 - 用 /vim 或 /config 启用

## 0.2.32

- 交互式 MCP 设置向导: 运行 "claude mcp add" 以逐步界面添加 MCP 服务器
- 修复一些 PersistentShell 问题

## 0.2.31

- 自定义 slash 命令: .claude/commands/ 目录中的 Markdown 文件现在作为自定义 slash 命令出现，将提示插入您的对话
- MCP debug 模式: 用 --mcp-debug 标志运行以获取关于 MCP 服务器错误的更多信息

## 0.2.30

- 新增 ANSI 颜色主题以获得更好的终端兼容性
- 修复 slash 命令参数未被正确发送的问题
- （仅 Mac）API 密钥现在存储在 macOS Keychain 中

## 0.2.26

- 新增 /approved-tools 命令用于管理工具权限
- 改进代码可读性的词级 diff 显示
- Slash 命令模糊匹配

## 0.2.21

- /commands 模糊匹配
