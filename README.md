

# Real Claude Code Changelog

Claude Code's release notes only describe what Anthropic chooses to announce, not everything they actually change. Bug fixes sometimes ship in one version but get announced in another, and even significant features can go unmentioned entirely.

---

Here are 3 examples of changes that were shipped but not announced at all:

> **Files Claude reads on your computer, and the output of commands it runs, become part of a cloud session** — visible to anyone the session is shared with and, on Team or Enterprise plans, to your organization's administrators. *(2.1.257)*

> **Approving an Artifact live room lets page events from anyone in your organization start turns while you are not present.** *(2.1.251)*

> **A comment from a writer on a watched Artifact can trigger automatic edits to it**, subject to server-side re-checks on the writer, the edit grant, file count, size and rate. *(2.1.248)*

There are a lot more (over 100) in the [changelog below](#changelog).  **Coverage:** 29 releases from 2.1.**226** to 2.1.**325**.

:point_right: **[Read the changelog ↓](#changelog)**

## Measuring completeness

Tracking machinery is still a work in progress, so consistent full evaluation of each release is currently unviable.  Significant architectural refactoring, like the React Compiler migration, interferes with a clean diff, so we've developed a completeness metric to make it clear how comprehensive each changelog entry is.

| Icon | Status                                   | Description                                                                                          |
| ---- | ---------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| ◆◆◆◆ | **Complete**                           | We identified 100% of the changes                                                                     |
| ◆◆◆◇ | **Complete barring a few assumptions** | We identified everything but have a few assumptions we haven't finished checking                      |
| ◆◆◇◇ | **Most**                               | We identified _most_ (_potentially_ all) but aren't sure about the entire release                     |
| ◆◇◇◇ | **Highlights**                         | We only identified some of the changes (usually because the release is very large and full of churn). |

## Visibility indicators

Naturally, we include entries that are also in the official changelog; therefore, each change is labeled with a badge.

| Status | Anthropic officially documented? | and in the right version? |
| ------ | -------------------------------- | ------------------------- |
| 🟢      | **Yes**                          | **Yes**                   |
| 🟡      | **Yes**                          | ⚠️ **No**                |
| 🔴      | ❌ **No**                         | —                         |

## Caveats

1. Just because a change is shipped **doesn't necessarily mean anyone can use it** because new features are often _gated_; that is, unavailable to most public users.

2. Anthropic can alter Claude Code's behavior without code changes by dynamically enabling feature flags in the [GrowthBook](https://www.growthbook.io) console.

## Have you found something we missed?

If so, please [open an issue](https://github.com/Piebald-AI/real-claude-code-changelog/issues/new).

## License

- Each entry listed in this changelog is licensed under [CC BY 4.0](LICENSE), meaning you're free to quote entries provided you link back to this repository.
- Any strings which are quoted verbatim from Claude Code's source code are proprietary to Anthropic, so they don't fall under CC BY 4.0.  You don't have to link back here for those.
- Neither we nor this repository are affiliated with or endorsed by Anthropic.
- The tools we develop to produce this changelog are closed source for the time being.

# Changelog

### 2.1.325 ◆◆◆◆

- 🔴 Removed the built-in `cc-plugin-themes` plugin added in 2.1.324, with `/custom-theme`, `/fireworks` and 20 animated chat backdrops for desktop and mobile clients.

<details>
<summary>1 change with no effect in this build</summary>

- 🔴 Moved the startup profiler's initialization mark and first wall-clock and process-uptime samples to a different point in module loading inside the worker that runs plugin function hooks; nothing in the worker reports them.

</details>

---

### 2.1.324 ◆◇◇◇

- 🔴 Added built-in `cc-plugin-themes`: `/custom-theme` offers 20 animated desktop/mobile backdrops; `/fireworks` runs a show and can run on "merged" in a main reply with a theme chosen, unless auto is off. Removed in 2.1.325.
- 🔴 Added terminal approval for sending a connector a file from the home or temporary folder outside the session's folders; links, other disks, credential-like names and Read ask or deny rules still stop it (remote switch, off by default).
- 🔴 Added remote rules that can move built-in subagents with no chosen model to a lower model family in chats hosted by claude.ai; a model or effort chosen in the agent, the call or the environment is kept. Inactive without a rule.
- 🔴 Added a training-consent service behind `/privacy-settings` and the startup notice, with eligibility checks and a "changed somewhere else" answer in place of overwriting a newer choice (remote switch, off by default).
- 🔴 Added per-redirect connector-block checks for plugin HTTP and SSE MCP servers when organization policy requires them.
- 🔴 Added local JPEG and PNG backdrops to mods' `$.theme.set`: a file in the mod's folder, at most 1 MiB and 4096 pixels a side, with network paths and hard-linked files refused.
- 🔴 Made Artifact supporting files and file removals available without a remote switch; `CLAUDE_CODE_ARTIFACT_MULTI_FILE` can still turn them off, and copying another artifact's files stays behind its own switch, off by default.
- 🟡 (2.1.325) Changed unset `sandbox.autoAllowBashIfSandboxed` to false on macOS and Linux/WSL, sending sandboxed Bash commands through ordinary permission checks; explicit settings still win (remote switch, on by default).
- 🟡 (2.1.325) Added a repository check to read-only Git auto-approval in Bash and PowerShell: a checkout that cannot be matched to the project or a trusted folder goes through further permission checks (remote switch, on by default).
- 🟡 (2.1.325) Routed scheduled `/skill` prompts that need approval to the Skill tool, and told Claude not to work around a refusal (remote switch, on by default).
- 🟡 (2.1.325) Stopped a running slash command's `allowed-tools` grants and connector-card approvals from carrying over to woken background agents and permission-checked host MCP calls (remote switch, on by default).
- 🟡 (2.1.325) Widened the account-email refusal to WebFetch URLs, MCP arguments, file writes and up to eight relative scripts named by shell calls, plus client identity fields beyond User-Agent (remote switch, on by default).
- 🟡 (2.1.325) Moved unpacked plugin MCP bundles to a shared content-hash cache; `CLAUDE_CODE_PLUGIN_MCPB_DIR` accepts absolute folders neither inside nor above the starting folder. Zip-cache mode uses a session folder instead.
- 🟡 (2.1.325) Stopped `/teleport` from stashing when a `MERGE_AUTOSTASH` record exists or the stash list cannot be read, and warned against `git stash pop` when the list holds an entry it did not add (remote switch, on by default).
- 🟡 (2.1.325) Added a check after worktree creation for an unexpected `commondir` file in the repository's Git folder: setup stops, and the file is deleted when that can be done safely (remote switch, on by default).
- 🟡 (2.1.325) Extended Bash approval checks to allowed bare assignments that may alter exported variables, except safe names, full-command allow rules and sandbox auto-approval (remote switch, on by default); `CLAUDE_CODE_DISABLE_EXPORTED_VARIABLE_PROMPT` turns this off.
- 🟡 (2.1.261) Added session archiving to the terminal's resume pickers: Ctrl+E archives or restores the selected session, and Ctrl+S shows archived ones (remote switch, off by default).
- 🟡 (2.1.269) Added taking a queued message back from a cloud session in the terminal, returning its text to the prompt and warning when Claude may already have read it (remote switch, off by default).

---

### 2.1.323 ◆◇◇◇

- 🔴 Moved connector downloads out of the working tree's `connector-downloads` folder into Claude Code's per-project data folder, where `cleanupPeriodDays` cleanup applies (remote switch, off by default).
- 🔴 Added `permissions.blockFileToolReadsOutsideWorkingDirectories` in launch `--settings`: file reads use host folders plus Claude-owned files and path exemptions; `/add-dir` cannot widen them, and shell commands are unchanged.
- 🔴 Stopped `mcp_tool` hooks in cloud sessions from calling the linked-computer (`remote-devices`) or Claude in Chrome servers, because a hook call skips the normal permission check.
- 🔴 Refused subagent MCP resource reads and `mcp_tool` calls from subagents or certain background hooks to session-metadata servers that would treat those calls as the main session's.
- 🔴 Removed the `<package>@npm` route for installing a plugin straight from npm (remote switch, off by default); npm sources listed in a marketplace still work.
- 🔴 Added `/motion` and `/whiteboard` prompts for published Artifact types. They need Artifact access or host-provided command support; Whiteboard also needs organization policy.
- 🔴 Added `CLAUDE_CODE_OVERLOADED_RETRY_MAX_WAIT_MS` to cap the total time the main conversation waits through overload retries, from 5 to 60 minutes; `CLAUDE_CODE_MAX_RETRIES` and the retry watchdog take precedence.
- 🔴 Added a post-compaction reminder to re-read earlier text with the claude.ai conversation tool before quoting it, and to say so when it cannot (remote switch, off by default).
- 🔴 Added a warning when a named shared-memory delete is unconfirmed and sync is not sending changes, telling Claude that other sessions may still read the content and to correct any claim that it is gone.
- 🔴 Raised experimental observers from one to four per agent, named in the comma-separated `observer` field; `CLAUDE_CODE_EXPERIMENTAL_OBSERVER_AGENTS=1` enables them.
- 🟢 Widened Code Mode's model check from Opus 5.5 and Sonnet 5.5 to Fable and Mythos 5.2 or later and other Claude families at 5.5 or later; its experimental opt-in still applies (remote switch, off by default).
- 🟢 Raised the fallback context window for unknown model IDs from 200K to 1M; model data and window overrides still win, and `CLAUDE_CODE_DISABLE_1M_CONTEXT=1` keeps the fallback at 200K.
- 🟢 Stopped writing new allow rules to settings when a secret scan flags or fails, or Git tracks the local settings file; existing saved rules are left alone.
- 🟢 Checked plugins against `engines["claude-code"]` in `plugin.json` at install, update and load; refused incompatible copies, but warned and continued for local author folders.

---

### 2.1.322 ◆◆◆◆

- 🟡 (2.1.323) Left plugins' `config.set` hooks unasked when `/fast on` or `/fast off` is typed on Vertex; the `/fast` menu still asks them.
- 🟢 Added fast mode on Vertex AI for Fable 5.2 and Mythos 5.2 in the `global`, `us` and `eu` regions; `/fast` turns it on for the session only, moves an unsupported model to Fable 5.2, and shows the price as 2x standard.
- 🟢 Retried Vertex fast-mode refusals at standard speed; a 400 about fast mode or `speed` skips fast mode for that model until `/fast on` or restart, while a 403 or 404 pauses fast mode for 30 minutes.

---

### 2.1.321 ◆◇◇◇

- 🔴 Added folder browsing to `claude remote-control`: it lists folders below the shared folder for claude.ai and can start a session in a picked one unless settings' Read rules cannot be checked (remote switch, off by default).
- 🔴 Added a system-prompt rule to treat the user's name, project, email address and other personal details as private and keep them out of requests to outside services unless asked (remote switch, off by default).
- 🔴 Added a system-prompt note for Fable 5.2 and Mythos 5.2 to check documentation more often on tasks such as accelerator kernel optimization, citing training measures that limit advances in a narrow set of AI-development skills.
- 🔴 Added user-delegated runner sessions (`CLAUDE_CODE_USER_DELEGATED_SESSION_DIRECT_API`) that refuse gateways, custom API endpoints, background sessions and `claude plugin eval`, and limit local auto-mode checks to allowed models.
- 🔴 Blocked more Git forms in worktree-isolated Bash calls: `fast-import --allow-unsafe-features`, and (remote switch, on by default) `git config --edit`, `git rebase --exec` and Git run from above the shared checkout.
- 🔴 Added mod notification requests for supporting hosts: `$.ui.notify` accepts a key, `delayMs` or `at` up to 7 days ahead, and `untilBack` to cancel a pending alert on return; `$.ui.cancelNotify` asks the host to withdraw one.
- 🟢 Added Fable 5.2 (`claude-fable-5-2`, 1M context) as `fable`'s built-in default outside gateways; eligible saved 5.1 picks move at startup, with Team/Enterprise waiting for organization access (remote switch, on by default).
- 🟢 Added `claude remote-control --settings <file>` for one JSON file shared by its child sessions; inline JSON is refused, and file changes prevent new sessions until Remote Control restarts.
- 🟢 Changed the privacy hook to deny Bash, Monitor and PowerShell inputs containing the signed-in email and a User-Agent-like setting, replacing broader email prompts (remote switch, on by default).
- 🟢 Added `claude plugin restore-set-aside <plugin>` for options and secrets saved during a managed marketplace replacement; `--discard` deletes those saved values instead, leaving plugin data folders alone.

---

### 2.1.319 ◆◇◇◇

- 🔴 Added approved downloads from claude.ai connectors into a Git-ignored `connector-downloads` folder, up to 10 files per result and 100 MiB each (remote switch, off by default).
- 🔴 Added local-file uploads for compatible claude.ai connectors through MCP's file-upload extension, with approval at Claude Code's own terminal (remote switch, off by default).
- 🔴 Skipped `CLAUDE.md` and project skills in `connector-downloads` folders and labeled reads as connector data. Project settings and `.mcp.json` are skipped when download files or a `*` `.gitignore` mark the folder.
- 🔴 Made `connector-downloads` folders in working directories or their Git roots block web tools under the existing connector-isolation policy; conversations can stay restricted after the folder is removed.
- 🔴 Blocked isolated-worktree Bash commands using Git options that can affect another checkout, including `--ignore-other-worktrees`, forced `worktree add`, `fetch --update-head-ok` and `apply --unsafe-paths`.
- 🔴 Added opt-in loading of large saved conversations from a resume index and newer transcript text, with whole-file fallback: `CLAUDE_CODE_TRANSCRIPT_TAIL_LOAD=on` (macOS and Linux).
- 🟢 Added `permissions.denyInsteadOfPrompting` to refuse calls still awaiting approval after rules, auto mode and hooks decide; allowed calls continue, and repeated refusals can end the turn.
- 🟢 Added `CLAUDE_CODE_DISABLE_FEATURE_FLAGS=1` as an alternative to `DISABLE_GROWTHBOOK=1` for stopping feature-switch fetching without turning off telemetry.

---

### 2.1.318 ◆◇◇◇

- 🔴 Added `claude --cloud <local-session-id>` to continue saved history in the cloud, filtering account-memory blocks and local attachments while leaving the original session unchanged (remote switch, off by default).
- 🔴 Added `/project` to assign usage reports to a claude.ai Project; `--save` applies it to future sessions in that folder (remote switch, off by default).
- 🔴 Added `claude ultrareview eval` for merged pull requests and JSON reports; `--max-cost` caps review starts, but the final bill can exceed it (remote switch, off by default).
- 🔴 Stopped allow rules for tools with the same Claude Code name within one MCP server; the rules work again once the server renames one of the tools (remote switches, off by default).
- 🔴 Added permission checks for private Artifacts marked as visible outside your organization, including unattended routine edits.
- 🔴 Added warnings when compaction, subagents and workflows relay text marked as a Remote Control report from another device, telling Claude to treat it as data rather than instructions.
- 🔴 Restricted more SSH proxy commands with unclear `%` expansions during worktree isolation, asking for written-out hosts and users (remote switch, on by default).
- 🟡 (2.1.323) Added opt-in experimental JavaScript code mode in the native interactive terminal for Opus 5.5 and Sonnet 5.5 through Anthropic. Auto mode reviews scripts before execution (remote switch, off by default).
- 🟢 Added stored-login expiry dates to `claude auth status` (`loginExpiresAt`) and headless JSON (`credential_expires_at`), plus warnings for headless text output. Dates can be estimates.
- 🟢 Stopped unattended launches from overwriting the global configuration when its JSON is malformed; errors explain how to restore a backup or repair the file.
- 🟢 Added input schemas or tool-search advice to some MCP tool-call errors when the schema was missing from Claude's prompt.

---

### 2.1.317 ◆◇◇◇

- 🔴 Added `/use-case` to choose an account's Life Sciences use case from the next request onward and save it for later sessions (remote switch, off by default).
- 🔴 Added Gmail attachments by file reference for sends and new drafts with named recipients, with per-call approval outside bypass mode (remote switch, off by default).
- 🔴 Made cloud routine changes and manual runs ignore whole-tool allow rules and request approval in ordinary modes; bypass mode can still allow them, and auto mode still reviews them.
- 🔴 Made Windows sandbox startup failures from extra hard links on protected files block sandboxed commands and outside-sandbox retries (remote switch, on by default).
- 🔴 Stopped `/goal` relayed from Slack, Teams or project threads from setting, clearing or showing the goal (remote switch, on by default).
- 🔴 Added warnings when a host reports personal hooks are off under `CLAUDE_CODE_RESTRICT_PERSONAL_CONFIG`.
- 🔴 Added warnings for images hidden after an attachment deletion, telling Claude to avoid new visual claims or reopening saved copies.
- 🟡 (2.1.318) Added checks that refuse selected command forms on Bash 2–3, and some on Bash 4, with advice to simplify the command or use a newer shell (remote switch, on by default).
- 🟢 Added SDK hook failure blocking with `onFailure` set to `block`; callback errors or invalid replies stop tool calls and prompts, and the TypeScript SDK refuses a CLI that cannot honor it.
- 🟢 Made detected disk-full or quota errors saving transcripts or config exit 1 in `claude -p` text and JSON modes; `stream-json` warns without changing status. Desktop and SDK URL sessions skip this check (remote switch, on by default).
- 🟢 Marked partial Grep and Glob results as incomplete when a search times out, so Claude sees a warning even when some matches or no files are returned.

---

### 2.1.316 ◆◆◆◆

- 🔴 Changed macOS background sessions to build `ClaudeCode.app` from the embedded plist, or relaunch directly if absent, for executables in the native installer's versions folder; a remote wrapper-bypass switch defaults off.

---

### 2.1.315 ◆◆◆◆

- 🔴 Allowed model configuration to turn on Bash edit diffs in Auto and bypass-permissions modes, while `CLAUDE_CODE_BASH_EDIT_DIFF` and `bashEditDiffEnabled` still take priority; the setting's description now explains the default.
- 🔴 Split long Bash edit-diff path lists into smaller Git calls using a 28,000-byte argument estimate, for both CRLF-only filtering and replacement patches.
- 🔴 Added up to three warnings per session telling Claude when the shared memory limit killed a process during an eligible foreground Bash command, even if the killed process belonged to another task (remote switch, off by default).
- 🔴 Added beginning-and-ending previews for eligible saved Bash output, with omitted-byte counts; separate remote switches control previews for successful and failed commands, and both default off.
- 🔴 Added remotely configured advice after eligible Bash commands, matching command kind, runtime, success or failure and output filtering; up to eight rules can each show a note one to five times per session, with no rules by default.
- 🔴 Added shared Git snapshots and diff reuse for concurrent Bash edits, with changed-file lists when full patches fail and wording that other commands may have contributed (remote switch, off by default). Shared-snapshot Git timeouts allow three event-loop passes before aborting.
- 🔴 Stopped asking before Claude in Chrome creates its own tab group when the session and account both use `acceptEdits`, the tool advertises this shortcut and no Chrome MCP mode override is set; the `tabs_context_mcp` call must contain only `createIfEmpty: true`.
- 🔴 Removed the experimental keepalive-triggered and log-only idle-compaction paths; idle compaction now uses only the existing one-hour prompt-cache timer, still set to 90% of its lifetime.
- 🔴 Changed old rate-limit checkpoint ref cleanup to use one sandboxed Git command when sandboxing is on (remote switch, on by default), and report pruning failures without discarding a successful checkpoint.
- 🔴 Changed shared Git subprocess settings to replace a repository's `core.alternateRefsCommand` with Claude Code's `git for-each-ref` helper (remote switch, on by default).
- 🔴 Added checks that `.git` belongs to the checkout before automatic runtime-file ignore writes, plus shared open-file checks for those writes and checkpoint ignores that skip links, hard-linked files, detected replacements and files over 1 MiB (remote switch, on by default).
- 🔴 Changed linked-worktree locking to create the `locked` marker directly instead of invoking `git worktree lock`, after checking that both checkouts share Git's common directory (remote switch, on by default). The initial write refuses an existing marker; stale-lock recovery can still clear one and retry.
- 🔴 Changed Git metadata caches on Linux with `CLAUDE_CODE_CONFIG_WATCH_EVENTS` set to check watched files on reads, at most once a second and with a 100 ms wait limit; added-repository HEAD watches use filesystem events with polling fallback, and stopped watches leave the read-check list.
- 🔴 Changed project-level configuration imports to read text and copy skills through checked file handles, enforce the 10 MiB text-read limit and create new skill, rule, command and agent files without replacing existing targets (remote switch, on by default). Skill copies drop special permission bits and leave partial copies with retry instructions after failure; user-level imports are unchanged.
- 🔴 Let running sessions add the Artifacts MCP server when tool availability or organization policy becomes ready after startup, with a matching signed-in account and the normal MCP permission checks still required.
- 🔴 Skipped a second size-check walk for ASCII-only MCP listing entries, counting their original size even when sanitization removes fields; listings near the limit can therefore lose trailing tools or prompts.
- 🔴 Rechecked current MCP access after OAuth redirect discovery and before a localhost retry, stopping sign-in when a server is now disabled or blocked; control-request sign-in also checks for an account change.
- 🔴 Stopped extra MCP reconnects while a scheduled retry is in progress, including slow background attempts after the first fast retries.
- 🔴 Added `CLAUDE_CODE_SORTED_OTTER` to switch MCP's handling of reconnecting servers on or off, including tool holds and instruction updates; it overrides a remote switch that's off by default.
- 🔴 Changed `claude mcp serve` to answer repository permission-rule requests with the last good read or other available settings after a file fails to load, warning when rules are skipped instead of refusing the tool call.
- 🔴 Fixed remote-workspace startup warnings to list only ignored `--mcp-config` and agent-frontmatter servers, and added a separate warning when `--chrome` has no effect because MCP runs remotely.
- 🔴 Restricted the memory agent's shell deletions to Markdown paths with no colon below the memory directory, blocking Windows alternate-data-stream paths that otherwise pass the `.md` check.
- 🔴 Added withdrawal of stale or unavailable Cowork memory from subagents and other spawned loops after tool steps (remote memory switch, off by default).
- 🔴 Improved unavailable-model errors to include the catalog's explanation, naming the required Claude Code version only when the model is offered on the current provider.
- 🔴 Cleaned model-validation and model-switch errors to remove control and hidden characters and neutralize Markdown links, shortening displayed model names after 128 characters and capping final model-switch refusals at 1,024 UTF-16 units.
- 🔴 Fixed the auto-memory read exception for searches whose root directory lacks a trailing separator when `permissions.blockReadsOutsideWorkingDirectories` is on.
- 🔴 Made the write-path guard check edit-deny rules against every supplied path spelling before its directory checks, including when outside-directory write blocking is off.
- 🔴 Changed environment-variable wildcard checks to treat unexpected normalization or decoding errors as a possible wildcard; decoding errors caused by malformed percent escapes still return no wildcard.
- 🔴 Restricted `/loop` from relay participants and non-human input, except scheduled triggers and two exempt channels; human Remote Control input still works (remote switch, on by default).
- 🔴 Added normal permission and Auto mode review for MCP resource reads instead of their built-in automatic allowance, hiding “Always Allow” shortcuts (remote switch, off by default). With it on, directory reads fail their permission check when listing is unavailable, and hooks or plugins can only tighten resource-read decisions in Cowork cloud Auto mode.
- 🔴 Reduced permission context for selected MCP checks in default, accept-edits, `dontAsk` and bypass modes by omitting ordinary allow/ask rules and extra directory details while keeping deny rules and the main directory; `CLAUDE_CODE_AUTO_MODE_FULL_CONTEXT=1` restores the full context. Context-size diagnostics now distinguish full and reduced reports and count configured Auto mode allow rules before the scheduled-task rule is added.
- 🔴 Stopped saved session allow rules from skipping cloud-browser safety checks in Auto, bypass-permissions and qualifying plan modes; protected calls lose “Always Allow” choices and rule suggestions, and saved browser allow rules are also left out of classifier context.
- 🔴 Changed Google Drive file-reference handling to log `dontAsk` refusals separately and return the existing refusal message in some unattended cases with an ask rule when a hook's approval was ignored (remote switch, off by default). Desktop keeps its ask-rule exclusions and skips this extra refusal in `dontAsk`.
- 🔴 Changed recognized plugin prompts to show their body and plugin label instead of the model-facing wrapper in transcripts, session previews, titles, search and default `/export` filenames; older transcripts and hook-rewritten prompts can recover the display information.
- 🔴 Removed the instruction to match surrounding code's comment density, naming and idiom from readable system prompts; the lean fallback now omits the communication section entirely.
- 🔴 Made cloud hook script-loading warnings clean up their explanation and cut it to 400 UTF-16 code units before adding the warning's wording (remote switch, on by default).
- 🔴 Changed SDK descriptions, unattended-run guidance, organization-restricted MCP notices and artifact permission explanations to call cloud routines scheduled tasks.
- 🔴 Changed move-to-cloud handling to recognize an already-cloud session from HTTP 400 with `session_not_bridge`, rather than matching words in the error message.
- 🔴 Changed sandbox cleanup to move suspicious directories aside instead of deleting their contents and explain recovery. Outside Windows it also checks saved parent directories and restores missing owner permissions; failed moves can still remove links or make owned entries unreadable.
- 🔴 Added write protection for initially missing Git `objects/info/alternates` files in Linux and WSL sandboxes when the Git directory, `objects` and `objects/info` are directories rather than symlinks (remote switch, on by default).
- 🔴 Changed Linux and WSL sandbox setup to create Git `config.worktree` placeholders through open directory handles, with no-follow checks on the Git directory and each subdirectory it opens. Linked worktrees and deferred thin-client setup use the same helper.
- 🔴 Added sandbox write protection for staged `mcp_call` files on non-Windows systems, plus checks on input-file destinations and their parents and refusal to overwrite an existing name (remote switch, on by default).
- 🔴 Stopped settings-file `env` blocks from changing the new background-socket, plugin-reload, MCP-relist, policy-redial, held-message and copied-session launch controls; project settings also can't set `CLAUDE_CODE_SORTED_OTTER` or use `CLAUDE_CODE_DISABLE_ULTRATHINK` to re-enable the keyword.
- 🔴 Changed remote-settings cache loading to require two consecutive matching disk reads, trying up to five reads and ignoring a copy that keeps changing.
- 🔴 Added regular-file checks to signed-cache, remote-settings and helper-consent saves, plus a data-sync step before signed-cache and helper-consent writes finish.
- 🔴 Made settings reads return the last successfully parsed values after temporary filesystem errors such as `EBUSY` or `EMFILE`, while still reporting that the current read failed.
- 🔴 Improved the Bash safety-check error for `for ((…)) { … }` bodies that already fail validation, recommending `do …; done` syntax (remote switch, on by default).
- 🔴 Stopped worktree-isolation checks from assuming assignments inside C-style loop bodies or command and process substitutions are integers just because the surrounding construct uses arithmetic (remote switch, on by default).
- 🔴 Restricted worktree-isolated `gcloud compute ssh`, `kubectl exec` and `oc exec` commands with ambiguous global options or local credential and configuration overrides instead of assuming their effects stay remote (remote switch, on by default).
- 🔴 Restricted worktree-isolated `sed` commands whose option order can hide the program, including bare `-i` consuming the next word as a backup suffix on macOS and BSD; computed programs and backup suffixes are refused (remote switch, on by default).
- 🔴 Restricted arithmetic in worktree-isolated Bash commands when an assigned value names a shell-managed variable and an unset arithmetic operand could inherit text leading back to it, with guidance to run the arithmetic separately (remote switch, on by default).
- 🔴 Restricted worktree-isolated shell commands when empty expansions, unmatched globs or array expansions can remove an argument and shift a later word into an option, host or script position, including in SSH, `gcloud`, interpreters and `set` (remote switch, on by default).
- 🔴 Restricted worktree-isolated `test` and single-bracket expressions using `-v`, `-R` or `-t` to plain variable names or digits even when the expression parses as binary; `[[ … ]]` keeps its separate checks (remote switch, on by default).
- 🔴 Restricted worktree-isolated `sshpass` commands with unreadable options, disappearing arguments or launchers hiding a later remote client, while following nested `sshpass` calls and checking `rsh` like SSH (remote switch, on by default).
- 🔴 Improved recognition of OAuth failures for missing accounts, missing organizations and lost membership, so matching response codes or plain-text denials can be classified as organization-access failures.
- 🔴 Made gateway sign-in show "Finishing sign-in…" for accounts with or without an email and ignore Escape while credentials are being saved or the successful sign-in is finishing.
- 🔴 Changed background-agent progress summaries to wait 30 seconds between refresh attempts instead of following a remotely configured interval sequence; callers can still override the delay, and cold-cache waits still check every 2 seconds.
- 🔴 Changed short background-agent summaries to use only an eligible default Haiku model on Anthropic's API, a fixed 2,000-token input allowance and the task's language unless a language is set (remote switch, off by default; hosts that request SDK progress summaries use full summaries). Ineligible writers use full summaries; a failed short-summary request switches later summaries to full.
- 🔴 Added policy and account checks to Anthropic's safety-event telemetry: sessions subject to policy checks withhold these events until policy and account attribution are available, and HIPAA-blocked or wrong-account events are dropped. Saved events are checked again before upload, and account-marked batches no longer retry an HTTP 401 without authentication.
- 🔴 Changed terminal text cleanup to replace standalone Escape tokens with the Cancel control byte, while leaving complete escape sequences on their existing path.
- 🔴 Blocked eight more CA public-key hashes and included them in Java proxy truststore cache filenames so caches built with the earlier filter aren't reused.
- 🔴 Changed certificate trust-data detection to require decoded PEM bytes to start with the parsed certificate before treating extra bytes as appended trust data.
- 🔴 Changed CA cleanup to check self-issued certificates' signatures, with exemptions for bundled roots, appended trust data and trusted issuer chains; `CLAUDE_CODE_DISABLE_SELF_NAMED_CERT_DROP=1` opts out, and client-certificate setups still skip main-list chain cleanup.
- 🔴 Changed HTTPS connection reuse to separate sockets when `NODE_TLS_REJECT_UNAUTHORIZED` or `BUN_TLS_REFUSE_DISTRUSTED_KEYS` changes, while keeping the main agent without client certificates across routine cache clears; `CLAUDE_CODE_DISABLE_HTTPS_AGENT_KEEPING` opts out.
- 🔴 Changed DNS-name TLS setup to leave hostname verification to the runtime; HTTPS proxy connections do the same unless a caller supplies its own check.
- 🔴 Changed `mcp__easel__chart` to refuse calls when a session doesn't provide a conversation array, explaining that charting isn't available there.
- 🔴 Changed message-ID loading for another session to use its project's recorded transcript path when available.
- 🔴 Clarified the archived cloud-session warning to say messaging can resume after unarchiving the session at claude.ai, while keeping the existing new-session suggestion and session link.
- 🔴 Fixed permission feedback menus allowing disabled choices to be selected or submitted.
- 🔴 Added a period after fallback-notice titles when joining them to warning text, unless they already end with one.
- 🔴 Stopped using locale values longer than 64 characters from `LC_ALL`, `LC_TIME` or `LANG` when formatting dates and times.
- 🔴 Restricted links in verbose memory-save notices to eligible auto-memory `.md` files on platforms other than Windows or WSL, rejecting colons below the memory directory; other paths get non-clickable rows (remote switch, on by default).
- 🔴 Restricted memory-save status verbs to 1–32 ASCII letters or hyphens, starting with a letter; invalid values now display `Saved`.
- 🔴 Sanitized service-supplied usage-limit messages and resume prompts by stripping invisible characters, normalizing Unicode and escaping angle brackets, with a 2,000-character limit (remote switch, on by default). Resume prompts also reject `/`, `@`, exit commands and `ultracode`/`ultraplan`/`ultrareview`/`ultrathink`, falling back to built-in text.
- 🔴 Rejected working-directory changes into Bun's embedded filesystem, including startup deep links, and recognized Windows embedded paths on any drive regardless of letter case.
- 🔴 Made failed session-directory updates try to restore the process's previous working directory before returning the error, including `/cd` and startup deep links.
- 🟡 (2.1.316) Applied `--restricted` read rules to both requested and resolved attachment paths, alongside `permissions.blockReadsOutsideWorkingDirectories`. Removed the base64 workaround from the `cannot_upload` error in restricted mode when the host doesn't supply the contents.
- 🟡 (2.1.316) Stopped Bash snapshots from turning on disabled options whose names contain `on`, while keeping the existing `monitor` exception.
- 🟡 (2.1.316) Fixed Bash snapshots losing functions whose names start with `-` or `+`.
- 🟡 (2.1.316) Fixed multiline Bash aliases outside Git Bash and shell snapshot failures from empty winpty filters or large alias lists; snapshots still keep only the first 1,000 alias lines.
- 🟡 (2.1.316) Fixed Claude in Chrome uploads using a Read allow rule to bypass `--restricted` working-directory limits, including when the session also uses `bypassPermissions`.
- 🟡 (2.1.317) Allowed files to be read again after their earlier Read or shell-read results leave the model's context through tool-result clearing (remote switch, off by default); later complete reads or writes remove the pending reread mark.
- 🟡 (2.1.316) Fixed duplicate saved MCP disable entries swallowing a newly disabled server, and made the last occurrence of each server count toward the saved list's 64-server limit.
- 🟡 (2.1.311) Made Opus alias migration and provider setup add `[1m]` only when the model needs it, while keeping the context suffix chosen for Opus Plan fallbacks.
- 🟡 (2.1.316) Improved Bedrock and Vertex model-access checks to recognize account, Marketplace, region and VPC Service Controls refusals, including Vertex errors with different capitalization.
- 🟡 (2.1.316) Added a local `/model` confirmation warning when Claude Code doesn't recognize the chosen model, naming the context window auto-compact assumes and pointing to ways to configure it.
- 🟡 (2.1.316) Added `CLAUDE_CODE_DISABLE_ULTRATHINK` to disable the `ultrathink` effort boost, and support for triggering it from eligible local standard-input prompts, including VS Code and Claude Desktop (host support uses a remote switch, off by default).
- 🟡 (2.1.316) Fixed buffered HTTP response errors being swallowed after the request was destroyed, which could leave the request hanging.
- 🟡 (2.1.316) Stopped host settings from restoring defaults when a nonempty managed `autoMode.allow` omits `$defaults`, and `/permissions` or `/auto-mode-setup` from restoring them when the combined allow list is nonempty and omits it. Kept the scheduled-task rule that automated prompts aren't fresh human consent even when custom rules replace defaults.
- 🟡 (2.1.316) Fixed `claude -p` text errors losing or showing another turn's Auto mode stop reason when a result waits behind background work; the explanation now travels with the result and prints before “Execution error”.
- 🟡 (2.1.316) Made Claude Code stop live and already-stopping shell command trees when it exits on macOS and Linux, except jobs marked to stay running, such as asynchronous hooks (remote switch, on by default). Cleanup gives processes up to 1.5 seconds before a forced kill.
- 🟡 (2.1.316) Fixed Grep and Glob hanging after their search timeout when ripgrep doesn't report that it exited; timeout completion no longer depends on a process-exit event.
- 🟡 (2.1.218) Made settings-approval summaries omit `CLAUDE_CODE_SUBAGENT_EFFORT`, plus `CLAUDE_CODE_DISABLE_ULTRATHINK` when its value disables the keyword.
- 🟡 (2.1.316) Added organization detection for eligible Team and Enterprise stored claude.ai logins so their organization's API-fetched managed settings apply without approval and signed responses can be checked against it; gateway, hybrid-organization and non-production OAuth configurations are excluded.
- 🟡 (2.1.309) Stopped worktree-isolation checks from trusting values in Bash and zsh variables the shell rewrites, including zsh's `MATCH`, `argv` and `reply`, and refused integer or float declarations that could make their later contents execute as arithmetic (remote switch, on by default).
- 🟡 (2.1.316) Added interactive gateway sign-in to terminal `claude auth login` when settings require a gateway and no `--console`, `--claudeai`, `--sso` or `--email` option is supplied.
- 🟡 (2.1.314) Extended saved-login checks to consider server-delivered `apiKeyHelper` settings while they're loading or refused, and matching endpoint or provider overrides left behind after those settings are removed.
- 🟡 (2.1.314) Improved saved-login refusal messages to distinguish an administrator configuration problem, organization settings that couldn't load and a sign-in needing a restart, including file uploads and self-hosted runner requests.
- 🟡 (2.1.316) Fixed nested subagents losing an inherited non-default parent model from their saved metadata, and stopped later metadata updates from dropping a saved model choice.
- 🟡 (2.1.316) Added `CLAUDE_CODE_SUBAGENT_EFFORT` for non-fork subagents and workflow agents without an explicit or inherited effort, except built-in web-fetch; `CLAUDE_CODE_EFFORT_LEVEL` still wins. Background jobs and launched teammates pass it through, and teammates also receive `CLAUDE_CODE_DISABLE_ULTRATHINK`.
- 🟡 (2.1.316) Made prompts cleaned of invisible characters send on the first Enter (remote switch, on by default); non-prompt modes, bidirectional controls, empty text, `/` or `!` prefixes and exit words still require review.
- 🟡 (2.1.316) Improved TLS error guidance to distinguish a server's missing intermediate certificate from a trusted CA whose issuer is missing, and directed Claude Desktop and `local-agent` users to their IT team's certificate settings.
- 🟡 (2.1.316) Improved missing-GitHub-repository messages for `/ultrareview`, cloud sessions and cloud agents to suggest creating a repository at https://github.com/new and pushing the project.
- 🟡 (2.1.316) Made first-run security notes, terminal-setup explanations and the power-up tour introduction shrink to fit terminals narrower than 70 columns.
- 🟡 (2.1.316) Delayed automatic `/diff` refreshes after slow Git work, by up to 30 seconds or up to 60 seconds after repeated failures lasting at least five seconds (remote switch, on by default). Manual refreshes and base changes can skip the wait.
- 🟡 (2.1.316) Reduced Git queries in `/diff` by normally requesting per-file statistics first; bases with cut-off output are remembered so changes above 500 files can use totals without repeatedly requesting details (remote switch, on by default).
- 🟡 (2.1.316) Changed organization survey invitations to wait for the configured submit key after a typed `1` or `0`, rather than a pause; blocking overlays or replacement input rows stop keyboard confirmation, and the card shows when it's opening.
- 🟡 (2.1.316) Fixed the voice-footer hint using up its three displays without being shown or on footer remounts; displays now count once per session, and no hint appears when push-to-talk has no visible key binding.

<details>
<summary>91 more for administrators and for authors of plugins, hooks, MCP servers and SDK hosts</summary>

- 🔴 Stopped adding fallback relative `@`-file references to Cowork context when the tools directory is marked as non-Git; absolute references, attached contents, oversized-file notices and PDF references still work.
- 🔴 Kept Gmail attachment download tool names across conversation clears and worker restores, recognizing both bare `download_gmail_attachment` and names prefixed with `__` or `:`.
- 🔴 Started fetching eligible images' model copies alongside their original attachments, reusing the request only while the token matches and retrying transient failures; the existing lower size threshold still needs a remote switch, off by default.
- 🔴 Changed task-file uploads blocked by stored-login checks to report `egress_blocked` instead of `upload_network`.
- 🔴 Added extracted text from uniquely named uploaded project documents to eligible project context, sharing the 20-item limit with knowledge documents and keeping accepted knowledge text if uploads fail or don't fit (remote switch, off by default).
- 🔴 Changed background sockets with authentication configured to wait for a nonempty line before takeover, or a protocol frame before terminal replay, including the wait after shell exit (remote switch, on by default). Added a 5-second inactivity timeout, adjustable from 100–5,000 ms with `CLAUDE_BG_SILENT_PEER_TIMEOUT_MS`; the daemon sets or clears `CLAUDE_BG_SOCK_ADMIT_SILENT_PEERS` to choose immediate handling or waiting.
- 🔴 Added an option to skip unused Bash file-change diffs in noninteractive remote parent sessions without `CLAUDE_CODE_ENVIRONMENT_KIND` (remote switch, off by default); explicit diff settings, first-party client prompts and plugin, hook or file-watch consumers keep them.
- 🔴 Added automatic comment watching for newly created Claude Docs in remote sessions, with instructions to reply on the document rather than a hidden relay (remote switch, on by default; requires the Docs connector and Artifact comments). Unavailable comment wakes now produce a passive warning that this session isn't subscribed.
- 🔴 Required plugin-supplied dynamic HTTP connectors in remote sessions to use an HTTPS first-party Docs endpoint before Claude Code treats them as Claude Docs connectors; a matching name or metadata alone no longer suffices.
- 🔴 Changed cloud command hooks to suppress Git log signatures, use `medium` log formatting, disable automatic Git maintenance and index refresh, and replace repository alternate-ref commands (remote switch, on by default).
- 🔴 Expanded cloud-session hook matchers to support counted repetitions, named groups and general positive or negative lookahead, with compilation limited to six times (pattern length + 1) work units; local sessions keep native regular expressions.
- 🔴 Moved the check for unreadable or startup-blocking machine policy from the shared hooks-disabled test to repository-hook listing, so selection and state comparison no longer make that check. Hook-state comparison now sends all caught errors to the common logger.
- 🔴 Added the triggering `toolUseID` and a shared `limit.startedAt` value to remote plugin-hook calls; the caller now reads that shared time when distinguishing a timeout from another cancellation.
- 🔴 Raised the remote protocol's advertised maximum from 17 to 18 for repository-hook listings; the default minimum remains 6 and negotiation still chooses the lower peer maximum.
- 🔴 Added a cancellation frame for an MCP question after its response arrives in Structured I/O, before the normal response is resolved or rejected (remote switch, off by default).
- 🔴 Added recognized MCP status text explaining that per-tool `permission_policy`, `always_ask` and `always_deny` don't apply to client-hosted MCP servers.
- 🔴 Added `cloudServiceProvided` to MCP status for recognized cloud-supplied, session-proxied HTTP/SSE servers, so hosts can distinguish them from claude.ai connectors; the status parser also accepts `error_code`.
- 🔴 Changed postponed device-MCP consent to a notice instead of a warning when no in-session consent question is available, and let the normal consent reminder appear when the postponement ends.
- 🔴 Let selected clients skip MCP tool-timeout pauses while a server question is open (remote platform list, empty by default; existing question-pause switch, off by default).
- 🔴 Raised the project and local permission-settings file limit for MCP-served tools from 256 KiB to 2 MiB; user settings already used the larger limit.
- 🔴 Added `CLAUDE_CODE_MCP_SKIP_UNCHANGED_RELIST=1` for managed cloud sessions to reuse unchanged MCP tool wrappers for up to an hour after a fresh tool listing, avoiding state replacements when the same tools are already installed; reuse requires unchanged conversion settings and inactive tool-name remapping.
- 🔴 Added MCP configuration limits of 65,536 UTF-16 code units for server URLs and 4,096 for OAuth `authServerMetadataUrl`, rejecting longer values before further validation.
- 🔴 Clarified SDK error-code documentation for model-version requirements and MCP registration failures, including `--sdk-url` and sessions started by `claude remote-control`.
- 🔴 Started remote feature-setting initialization for hosted `claude mcp serve --transport http` daemons. The feature-setting client now uses environment-supplied identity, skips saving local configuration and omits experiment-exposure logging; its local-configuration read path stays disabled.
- 🔴 Stopped the hosted HTTP MCP daemon from advertising `io.modelcontextprotocol/tasks` even when task support's remote switch is on (off by default).
- 🔴 Added a filesystem-root check for `CLAUDE_CODE_REMOTE_MEMORY_DIR` in remote-memory edit normalization and path warmup, and made the edit containment check case-insensitive on Windows. Warmup now includes the memory directory itself and reports unresolved links separately from success.
- 🔴 Fixed remote-memory file-creation edits with an empty `old_string` losing trailing whitespace; edits to existing non-Markdown content still trim it.
- 🔴 Added validation of the model catalog's optional `early_access` boolean, treating invalid values as `true`.
- 🔴 Changed tool-loading text for models using system-message formatting to follow `tool_loaded_text`, removing standalone “Tool loaded.” blocks when false. Added that capability to 22 built-in models and recognized `bash_edit_diff` as a capability name.
- 🔴 Added `ultrathink_available` in SDK init messages and `ultrathinkAvailable` in `get_settings.applied`, telling hosts when the keyword is available for the current model and effort.
- 🔴 Changed cloud-session approval notices to distinguish calls that need your answer from calls the session may approve automatically, carrying classifier eligibility through live tool-call status and updating the notice when a waiting call starts needing you.
- 🔴 Added launcher-only `permissions.blockReadsExemptPaths` for selected absolute local files or folders to pass the outside-directory read block while normal permissions still apply; updates take effect during a session, but diskless, restricted and `CLAUDE_CODE_EVAL_CONFINED` sessions ignore the list.
- 🔴 Kept auto-memory Markdown files writable under outside-directory write blocking when `CLAUDE_COWORK_MEMORY_PATH_OVERRIDE` chooses the memory directory; restricted sessions and the existing memory-path and settings checks still apply.
- 🔴 Extended tools' unanswered-permission callbacks to `dontAsk` denials, preserving eligible user-only questions and reporting both the denial mode and ignored hook approvals; the calls still stay denied.
- 🔴 Allowed plugins outside the managed-plugin list to read listed attachments through `prompt.media` during an active `prompt.submit` hook; the submission must still be in progress after the read.
- 🔴 Added `CLAUDE_CODE_CCR_ONE_PLUGIN_LOAD_PER_RELOAD=1` to reuse one cache-only plugin load during a refresh when synchronous installs are off, no external-marketplace entries apply and no load is running; a failed or replaced load falls back to a full load.
- 🔴 Added `CLAUDE_CODE_CCR_ONE_PLUGIN_LOAD_PER_RELOAD`, `CLAUDE_CODE_MCP_SKIP_UNCHANGED_RELIST`, `CLAUDE_CODE_MCP_NO_REDIAL_AFTER_POLICY_REFUSAL` and `CLAUDE_CODE_SESSION_BEGAN_AS_COPY` to the environment variables removed when starting child sessions.
- 🔴 Corrected the bundled `/claude-api` references to say Mythos 5.1 enforces thinking-history checks for accounts of any age, including after earlier per-turn reminders are removed. Removed the former exemption and related explanations, and described Bedrock access in `us-east-1` as limited availability.
- 🔴 Changed the bundled `/claude-api` migration checks to test an edited replay on the same model and platform before trusting empty reports, using the target model's own thinking block after the edit; recovery without the controls beta now strips only the error's named block and later `thinking` or `redacted_thinking` blocks.
- 🔴 Expanded plugin-authoring guidance on keeping already-sent prompts and tool descriptions unchanged to avoid losing thinking and prompt-cache reuse, recommending appended context or a new thread or compaction instead. Updated API comments to describe active-submission media access, plugin prompt attribution and scheduled tasks, and warn that re-asking `tool.describe` after resume can overwrite saved descriptions.
- 🔴 Changed the SDK error for combining `sessionStore` with `persistSession: false` to recommend a new private temporary `CLAUDE_CONFIG_DIR` directory that the caller deletes after the query.
- 🔴 Stopped remote archive-status requests when `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` has any nonempty value.
- 🔴 Added one retry for remote archive-status reads after an expired-login error when the session's login-refresh callback succeeds, using the current access token.
- 🔴 Fixed overlapping remote archive-status checks so a session reset can start a fresh request and an older request finishing won't clear the newer one.
- 🔴 Added server-supplied turn IDs to eligible cloud-browser sessions for same-session input, checking its origin and waiting up to two seconds for feature settings, then clearing the ID when the turn ends (remote switch, off by default, or an explicit session allowance).
- 🔴 Added `CLAUDE_CODE_DISABLE_HELD_MESSAGE_RECOGNITION` to disable held-message recognition and the self-hosted startup check for held messages in saved transcripts, and passed it to runner children. Gave that startup check its own remote switch (on by default), separate from ordinary recognition (remote switch, off by default).
- 🔴 Added busy-state tracking for foreground Bash calls in cloud sessions whose workers can move them into the background, with a two-second recognition delay and restoration from session history.
- 🔴 Stopped older self-hosted session-token renewal work from retrying or applying returned configuration once a newer token becomes current.
- 🔴 Restricted self-hosted runner-tool IDs to 1–256 ASCII letters, digits, `_` or `-`, and rejected hidden characters in text inputs. Local launch paths now reject control characters and line breaks, with guidance to use a readable path or ask for the file to be renamed or moved.
- 🔴 Changed SDK `register_repo_root` permission checks to use the registered directory's own path instead of expanding it to alternate resolved paths.
- 🔴 Expanded SDK API-error descriptions to cover organization-imposed API-key helpers, unconfirmed settings and who can resolve a refused stored login, plus the response fields accompanying `model_requires_usage_credits` errors.
- 🔴 Made Send now in print-mode sessions wait for automatic compaction to finish before delivering queued messages, keeping its summary (remote switches, on by default).
- 🔴 Added `CLAUDE_CODE_SESSION_BEGAN_AS_COPY=1` and hidden `--session-began-as-copy 1` so print-mode resume won't automatically continue the source session's unfinished turn or run its deferred tool call; child processes don't inherit the environment marker.
- 🔴 Extended Cowork's restrictions-only managed-settings path to diskless host sessions marked as derived from Cowork, skipping its loading wait and reporting no managed hooks when no hooks or policy errors are found; a remote Cowork launch surface alone no longer skips managed-settings checks.
- 🔴 Restricted storage-backend saves of remote settings to diskless host sessions; sessions with disk access now save to local files even when a backend is supplied.
- 🔴 Added hook-script checks for heredocs that cross command- or process-substitution parsing boundaries, including a closing parenthesis before the heredoc body arrives (remote switch, on by default).
- 🔴 Extended hook-script checks to follow relative paths stored in variables through interpreter search paths, Git configuration, shell startup files and nested shell scripts (remote switch, on by default).
- 🔴 Added cloud-session checks for local hook scripts mentioning zsh's `histchars` or `HISTCHARS`, even in comments or behind quote and escape syntax, because these variables can make apparent comments execute (remote switch, on by default).
- 🔴 Stopped developer-configured gateways from being offered when `forceLoginMethod` requires `claudeai` or `console`, and stopped applying managed `gatewayInternalNetworks` to developer-selected gateway URLs.
- 🔴 Stopped OAuth recovery from treating every `ANTHROPIC_UNIX_SOCKET` connection as an SSH tunnel; only a matching `ssh-placeholder` credential now gets the tunnel-specific handling for supplied and recovered logins.
- 🔴 Changed workload-identity policy tracking to remember the first profile or credential source even before its organization is known, so a later source change can't silently become the starting point.
- 🔴 Added remote text-upload counts, gaps over 500 ms and maximum flush-timer lateness to successful SDK results when first-text timing is active and the session isn't diskless; counts cover posts with new, nonblank main-agent text, and timer lateness is capped at 60 seconds.
- 🔴 Added separate turn-start timings for conversation append, init-frame sending, loop entry and request announcements (`CLAUDE_CODE_REMOTE` or `CLAUDE_CODE_EMIT_STARTUP_TIMING` for startup output).
- 🔴 Expanded main-session attachment diagnostics with setup, prompt-producer, ambient startup/wait and rendering times, producer and token-count totals, token-count and changed-file-read time, and file-size/hash-only counts. Slowest-producer timing now excludes work spent starting its group (`CLAUDE_CODE_REMOTE` or `CLAUDE_CODE_EMIT_STARTUP_TIMING` for startup output).
- 🔴 Changed hosted-worker MCP requests without an explicit proxy to bypass their connection pool after TLS settings change, using only CAs shared by the old and current settings and asking to reconnect if none remain (`CLAUDE_CODE_CCR_OWN_CONNECTION_POOL` or a remote switch, off by default).
- 🔴 Added structured `rate_limit_info` to 429 `model_requires_usage_credits` errors alongside their display text and error details.
- 🔴 Changed the bundled Bun runtime to another build that still reports 1.4.4, with about 25 MB more native code, new `.bun_aot`, `.bun_trim`, `.bun_features` and `.note.bun` sections, new `--aot` options and `BUN_AOT_*` variables for an ahead-of-time compile mode, and changes to the runtime's own built-in JavaScript.
- 🟡 (2.1.321) Added a hosted Linux Bash path that carries eligible commands containing `pkill`, `pgrep` or `pidwait` in `__CLAUDE_CC_COMMAND_TEXT` instead of shell arguments (remote switch, off by default). If shell startup removes the variable, the call fails with rerun advice and later calls use arguments again.
- 🟡 (2.1.316) Added `guardrail.input_tagging` to Claude apps gateway Bedrock upstreams to wrap selected message text and, optionally, the system prompt in Guardrails input tags; failover upstreams must agree, and preparation failures return 400 without sending the request.
- 🟡 (2.1.316) Added monthly shared group budgets to the Claude apps gateway through `pooled_budget`, alongside each member's own cap; requests get `429 billing_error` and a reset date once every matching pool is used up. Pool-spend recording warns when another charge arrives after a write has stalled for 30 seconds.
- 🟡 (2.1.316) Added opt-in `managed.policy_mode: layered` to combine matching group and email-domain policies in the Claude apps gateway, keeping earlier ordinary fields while merging deny/ask rules, hooks and blocked lists; helpers and path exclusions that could undo another policy's restrictions are rejected.
- 🟡 (2.1.316) Fixed the Claude apps gateway forwarding blocked nested `model` choices without checking role and operator model lists; checks now return 400 with the offending field's path and reject more than 100 nested model names, while skipping input, schema and example payloads.
- 🟡 (2.1.316) Fixed PowerShell hooks beginning with `using`, `param`, a type cast or an attribute to propagate exit code 2; declaration-style scripts matching a named-block pattern and `PermissionRequest` hooks stay exempt.
- 🟡 (2.1.316) Kept restored MCP off-switches in saved worker state while shutdown is pending, and stopped late shutdown callbacks from disabling a server that's since been re-enabled. Self-hosted runner diagnostics now distinguish a close timeout from a completed close that failed.
- 🟡 (2.1.290) Stopped scheduled startup and cached-connection retries to HTTPS MCP servers after a recognized proxy policy refusal in hosted sessions with `CLAUDE_CODE_MCP_NO_REDIAL_AFTER_POLICY_REFUSAL=1`.
- 🟡 (2.1.316) Added `pending_elicitation_requests` to SDK initialization and reinitialization replies so joining clients can recover unanswered MCP questions (remote switch, off by default); peer replies, live-only replies and ordinary awaited control results strip the list.
- 🟡 (2.1.316) Made Auto mode stop errors mark hosted sessions as failed and use the stop explanation as their status detail. Limited proxy-detail hiding to the generic no-safety-verdict warning, keeping other Auto mode stop explanations intact.
- 🟡 (2.1.316) Added `self` as an accepted read or write level in artifact capability rules, alongside `view`, `interact`, `admin` and `owner`.
- 🟡 (2.1.316) Made host-managed first-party gateways honor `CLAUDE_CODE_AUTO_MODE_SERVER=1` even when session-level experimental betas are off, provided organization policy and the existing eligibility checks allow it.
- 🟡 (2.1.319) Changed host-managed teammate and background launches to forward `CLAUDE_CODE_AUTO_MODE_SERVER` from before project environment changes when its current value enables server checks.
- 🟡 (2.1.278) Added a Desktop gateway fallback notice explaining that server checks aren't working, the built-in Auto mode check sends paid requests, and the session can continue, with a link to the Desktop gateway troubleshooting guide.
- 🟡 (2.1.316) Fixed credential scrubbing corrupting added environment values when a credential variable contains a boolean-like value such as `1` or `false`, and left values equal to the requested working directory unchanged.
- 🟡 (2.1.323) Added optional tracking and resend of missing assistant replies and tool results when eligible self-hosted cloud sessions resume (remote switch, off by default); sessions with `MessageDisplay` hooks skip recovery, and repeatedly failing old rows can step aside for new ones.
- 🟡 (2.1.316) Stopped self-hosted sessions from replaying follow-ups that saved history ties to a user-stopped turn after worker replacement; `CLAUDE_CODE_DISABLE_HELD_MESSAGE_RECOGNITION` or a remote kill switch (off by default) disables this check.
- 🟡 (2.1.316) Added inline `ReportFindings` reviews for eligible Claude Desktop and web remote sessions, excluding Cowork (remote switch, on by default). Most review templates also ask for one text line per finding with its outcome, so clients that hide the tool call can still show it.
- 🟡 (2.1.316) Fixed SDK `register_repo_root` with `reload_claude_md` leaving an outside directory's `CLAUDE.md` out of cached instructions when additional-directory instruction loading is enabled through `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD` or a host setting.
- 🟡 (2.1.316) Added hidden `claude auth login --gateway-json` for hosts such as VS Code to present gateway, certificate and account questions over JSON lines, plus `gatewaySignInOffered` in JSON auth status. The login mode requires redirected stdin and refuses calls from inside Claude Code.
- 🟡 (2.1.314) Made saved-login checks select `apiKeyHelper` defaults in platform order and honor per-platform `outputBehavior: "merge"`, with the chosen defaults overriding matching top-level settings and environment entries.
- 🟡 (2.1.314) Added destination-aware, cancellable waits for saved-login policy before self-hosted runner requests, cloud-session creation and task-file transfers, and checked the credential being sent on Files API operations instead of only the session's current login.
- 🟡 (2.1.265) Added resume code for marking unfinished `Agent` and legacy `Task` calls as interrupted by process shutdown, plus interruption rendering and suppression of the tool-batching reminder. Generating those results requires `CLAUDE_CODE_RESUME_SHOWS_CUT_OFF_CALLS` and a caller option that nothing in this build sets.
- 🟡 (2.1.316) Added `CLAUDE_CODE_DISABLE_LOOPED_CROSS_CERT_DROP` to keep looped cross-certificates; this and `CLAUDE_CODE_DISABLE_SELF_NAMED_CERT_DROP` follow protected connection-setting rules, refresh CA caches when changed, and are checked by runner proxies and HTTP hooks.

</details>

<details>
<summary>48 internal changes: telemetry, diagnostics and bookkeeping</summary>

- 🔴 Added Bash edit-diff wait telemetry with separate ordinary/shared counters and 10-, 60- and 300-second thresholds, plus a debug line showing whether commands share snapshots.
- 🔴 Reused system-prompt and tool-schema hashes between matching requests instead of recalculating them for prompt-cache diagnostics.
- 🔴 Added local text-and-image token estimates to tool-result clearing metadata and capped reported savings at a valid client estimate. Idle tracking also records how many tool results the latest post-idle reply cleared.
- 🔴 Gave hook timeout errors the distinct name `NoAnswerInTimeError` for callers and diagnostics.
- 🔴 Stopped text-file reads from resolving symlinks just to prepare a debug message when the current log level or mode would discard it.
- 🔴 Added live `pluginSteered`, `forRemoteExecution` and `spawnedByWorkflowRunId` getters to shared tool-context adapters, exposing the calling context's plugin steering, remote-execution mode and workflow-run ID.
- 🔴 Moved the startup profiler's initialization mark and first wall-clock and process-uptime samples to a different point in module loading, both with `CLAUDE_CODE_PROFILE_STARTUP` set and in the 0.5% automatic sample.
- 🔴 Delayed resolving the session directory for MCP file baselines until the call names a supported file tool and supplies a string path to a non-notebook file.
- 🔴 Skipped environment-expansion setup for empty or entirely literal MCP header maps, building the variable block lists only when a header contains `${` and reusing them afterward.
- 🔴 Added the original MCP connection failure code to wrapped not-connected errors as `mcpDialCode`, alongside the existing error-source classification; nothing in this build reads it by name.
- 🔴 Skipped MCP HTTP debug-message preparation when the log sink won't use it, including hosted sessions with `CLAUDE_CODE_SKIP_MCP_DEBUG_LOG_FILES=1` and debug-level logging off.
- 🔴 Let MCP listing callers choose size and Unicode-work limits, keeping the old defaults; tool-listing memo checks use a smaller estimated-size limit of about 1 MB.
- 🔴 Added the full MCP tool name to live and replayed background-task notifications' `toolsUsed` metadata and used-tool tracking; recording tool use follows a remote switch that's on by default.
- 🔴 Updated the bundled model catalog from version 3354 to 3444, moving its issue and expiry dates forward one day without changing its model rows.
- 🔴 Added a withdrawal indicator to permission-result callbacks for dialogs that weren't shown.
- 🔴 Added a prompt-text helper that leaves out recognized pasted-content blocks before applying the usual display cleanup.
- 🔴 Made parsed cloud errors keep an optional `message` field for later consumers.
- 🔴 Added support for starting remote internal-event catch-up after a supplied event ID, with caller-selected page parsing, compression handling, byte and event limits, and timestamp-length checks.
- 🔴 Added the submitting `clientPlatform` to latest-human-prompt tracking and a tool-state marker when that platform starts with `claude_code_`.
- 🔴 Changed remote upload trimming to keep request IDs on all assistant messages with a nonempty API message ID, rather than only API errors (replacement remote switch, off by default), and expanded the associated rejection diagnostics.
- 🔴 Removed the remote-worker policy that delayed the first idle-status report while inbound work was waiting.
- 🔴 Changed remote whole-turn upload holds to end after a matching assistant reply or tool result enters an outgoing batch, except for round-trip releases; the batch's release reason controls whether another hold is allowed.
- 🔴 Added earlier signed sender-address prefetch for eligible diskless first-party prompts (remote switch, off by default), retrying early misses. A separate remote switch, off by default, gives ordinary prefetch three event-loop passes to start.
- 🔴 Added a `refusedByProxy` marker to runner token-refresh errors when an HTTP 403 lacks both a valid Anthropic request ID and Cloudflare response markers; nothing in this build reads the marker by name.
- 🔴 Added old temporary copies of `remote-settings-consent.json` to age-based cleanup when their names end in `.tmp.` plus eight lowercase hexadecimal digits.
- 🔴 Expanded Bash telemetry with program names, how much of a test suite a command selects, and test results inferred from foreground or background output, including MCP-server background shells. Added backgrounding reasons and Datadog support for background completion events, plus execution fields for output previews, command notes, memory kills, output sizes and whether command text mentions saved-result or background-output folders.
- 🔴 Added Chrome permission diagnostics that distinguish tab-lookup timeouts, missing tab groups, non-JSON replies, tool errors and approval requests, and identify tab URLs without a plain host.
- 🔴 Added Desktop and local-agent diagnostics for whether an Auto mode server safety check was requested, returned a verdict, ended without one or wasn't requested, including the reason and server-switch setting, once per state and reason.
- 🔴 Expanded diagnostic event lists for artifact-document wakeups, Bash edits and notes, Remote Control, project uploads, plugin skills, permission checks, subagent effort defaults, runner session renewal, usage-limit text changes and idle CPU samples.
- 🔴 Changed first-party event logging to send records directly to its batch processor by default, using the OpenTelemetry SDK logger only when a log-record or global attribute-length or attribute-count limit is configured.
- 🔴 Added the number of blocking hook outcomes to hook-completion diagnostics, plus whether a stop hook was already active for `Stop` and `SubagentStop` events.
- 🔴 Added Linux hosted-worker idle CPU diagnostics that separate shells producing output, quiet shells, finished shells and leftover agent processes, with listening-socket checks and VM CPU totals (remote switch, off by default; requires `CLAUDE_CODE_DIAGNOSTICS_FILE` and excludes child and diskless sessions).
- 🔴 Added CLI CPU time to remote post-turn wait diagnostics when CPU readings are available; diskless sessions skip the measurement.
- 🔴 Changed query telemetry to use the first request built for dispatch, with a one-time fallback attempt to log request metadata if the query fails before that point.
- 🔴 Added WebFetch telemetry for long pages and continued reading in remote-agent sessions originating from claude.ai chat, when a tool-use ID is present and the result uses the regular page-reading path.
- 🔴 Added Bash repeat-work telemetry with elapsed time, intervening edits, possible writes, tests and lints, new user messages, earlier outcomes, whether earlier output is still in context and saved-output size. Clearing a conversation resets the comparisons.
- 🔴 Added `reads_own_output` telemetry to Read and Bash to classify references to the session's saved-result directory, background-output directory or both, when the session has a project and directory lookup succeeds.
- 🔴 Added `cli_trial_keys` to hosted remote startup reports, encoding enabled values of `CLAUDE_CODE_MCP_SKIP_UNCHANGED_RELIST`, `CLAUDE_CODE_CHROME_LATE_MCP_SERVER` and `CLAUDE_CODE_SKIP_MCP_DEBUG_LOG_FILES` as bits 1, 2 and 4.
- 🔴 Changed the feature-telemetry category for subagent wake failures handed to the main agent from `bad` to `sad`.
- 🔴 Added a one-in-32 sample of queue-to-init telemetry for main VS Code sessions, separating queue wait from turn-start-to-init time and skipping prompts queued before the previous turn ended.
- 🔴 Expanded Unicode normalization's combining-mark tables with additional Hebrew, extended and supplementary characters, including U+05C8–U+05C9 and U+1ADE–U+1ADF.
- 🔴 Added U+209D, U+209E and U+209F to the character look-alike tables for `w`, `y` and `z`, respectively.
- 🔴 Changed custom-CA and client-certificate HTTPS agents to request no per-host or total socket-count cap.
- 🔴 Saved and restored the tool names kept through `/clear` in worker metadata, and marked the reset list as already written for the current transcript; a different transcript or a changed tool list can produce tools-used metadata again.
- 🔴 Added a line-by-line parsing attempt for non-ASCII JSONL buffers, and sent non-ASCII transcript batches through the per-row path instead of the native batch fast path.
- 🔴 Stopped conversation hashing from treating null-content user or assistant transcript rows as message content, resetting its running hash state as it already did for missing content.
- 🔴 Restricted compact number formatting to JavaScript numbers, replacing other input types with `NaN` before formatting.
- 🟡 (2.1.271) Added account and credential checks for policy answers and safety-event telemetry, using salted hashes for unnamed credentials and credential versions for SSH tunnels; non-tunnel policy fetches now keep the identity captured for their request locally.

</details>

<details>
<summary>15 changes with no effect in this build: inactive code added, changed or removed</summary>

- 🔴 Added inactive scaffolding for sharing through the Remote Control dialog: empty dialog helpers that nothing calls, a `live-preview` notice whose condition is always false, port-row and ended-share state that is never filled, and a disabled list of sharing outcomes such as `already_shared`, `nothing_listens` and `session_refuses`.
- 🔴 Added a sign-in recheck beside the held live-preview session checks that nothing calls; it would answer `sign_in_changed`, `sign_in_unreadable`, `no_sign_in_check` or `sign_in_in_doubt`.
- 🔴 Added named failure reasons to the hook-matcher pattern reader (`legacy_grammar`, `look_behind`, `flags_group`, `back_reference`); its one caller discards them, so matchers it can't read are handled as before.
- 🔴 Added placeholders that have no effect: `renewSessionTokens` and `isThawing` callbacks passed to an empty self-hosted runner helper, an MCP resource check that always passes with a refusal branch behind it, fields nothing reads (`teamNameAskedAs`, `rowsNow`), and an error renderer for a tool slot that is always empty.
- 🔴 Added more code that can't take effect: an early exit for diskless launches in the cloud-browser session check that reads a value nothing sets, one more always-empty slot in the command lists, a third cleanup call on a hook the self-hosted runner never sets, and a disabled, blank form of the skill prompt's "Yes, and don't ask again" option with a check refusing it; the condition that would disable the option also removes it.
- 🔴 Replaced unused inline-text hooks on the tool-result store: the `keepsTextInline`, `takeInlineTextChars` and `noteInlineTextCut` lookups are gone, and an optional `takesTextInline` check with a scan for runs of 5,000 UTF-16 code units without ASCII whitespace takes their place. No store in either build has these methods, so oversized results are saved or truncated as before.
- 🔴 Changed the held live-preview session checks, which nothing calls: they gained a test for a replaced fixed sign-in credential, whose callback is never supplied, and the sign-in failure debug message now says "owner check failed" instead of "owner check for a start failed".
- 🔴 Added two preview-tunnel options that no caller sets: `refusesOtherSessions`, which would make a tunnel reject other-session requests and refreshed tokens and force TLS certificate checks, and `onUnlistedPortProbed`, which would tell a preview host when its own session asks for the status of an unlisted port from 1024 through 65535. The only trace is an `own_refusal` field, always false, in the tunnel's permanent-failure telemetry.
- 🔴 Added a `dialogKey` lookup so a local JSX command could use a built-in dialog loader under a name other than its own; no command sets it, so loaders are still chosen by command name.
- 🔴 Added memory-extraction hooks that nothing uses: an `onPassSkipped` callback that is never set, `smaller_pass` settings in `CLAUDE_CODE_POST_TURN_MEMORY_CONFIG` that are parsed and never read, comparison-trial hooks on a slot that is never filled, and an option to skip permission-denial telemetry that only those trials would use.
- 🔴 Added an emergency-stop check where laptop-memory context is built and withdrawn; the memory backend it asks is never set in this build, so it never fires.
- 🔴 Added an exported `loadDefaultMcpClientModule` helper for loading the default MCP v2 client; nothing calls it.
- 🔴 Changed the wait for lazily loaded plugin agent definitions so cancelled agent launches, resumes and forked skills would stop waiting, except on a turn interrupt; no agent definition in either build is loaded lazily, so nothing waits.
- 🔴 Added Remote Control upload counters that nothing reads: whole-turn upload holds, releases and held rows, the first undelivered count at close for each upload path, and events handed to an upload or telemetry queue after it closes. The two methods that would report them, `uploadHoldInAll` and `uploadLaneCounts`, have no caller.
- 🔴 Added bookkeeping that nothing reads: the first dispatch time in the turn timer's saved snapshot, which no code takes, and first-wait, unsigned-call and completed-ask counters for signed sender-address lookups.

</details>

---

### 2.1.314 ◆◇◇◇

- 🔴 Added `/send-to-project` for local claude.ai sessions with organization permission, live Remote Control, typed input or headless stdin and confirmation (remote switch, off by default); `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` disables it.
- 🔴 Added a server-only auto mode option for Anthropic API sessions, some settings requiring a direct connection (remote switch, off by default); actions without a verdict cannot run, and some settings skip local subagent-report review.
- 🔴 Added a cloud-session stop for sustained use of at least 90% of all sandbox CPUs, ending shell commands and child processes while keeping files; inactive unless remote configuration sets a duration.
- 🔴 Added Design Sync checks for local-file uploads that reject protected files, hard links, files requiring separate read approval, and files replaced after validation.
- 🔴 Added opt-in `stream-json` merging for consecutive text updates with `CLAUDE_CODE_STREAM_EVENT_HOLD_MS` (1–2,000 milliseconds) and line-size limits via `CLAUDE_CODE_STREAM_EVENT_MAX_LINE_BYTES`.
- 🔴 Added an instruction not to recreate existing games, defaulting to Opus 5.5 outside Cowork and local-agent sessions; `CLAUDE_CODE_MODEL_CAPABILITIES` and capability settings can override it.
- 🟡 (2.1.316) Added an Opus 4.8 fast-mode deprecation warning with a remotely configurable removal date, defaulting to 2026-11-30; fast mode itself is unchanged.
- 🟢 Made `permissions.blockWritesOutsideWorkingDirectories` block Claude Code settings edits by `Write`, `Edit` and `NotebookEdit` inside working directories; some session files and shell commands are exempt, and no allow rule overrides it.
- 🟢 Restricted Claude apps gateway upstreams with `groups` to developers with matching identity-provider claims; developers without group claims can use only upstreams without `groups`.
- 🟢 Added Bedrock `guardrail_trace` logging of triggered policies and filters, excluding matched text but potentially including request IDs, subjects and emails; the raw trace is removed from responses.
- 🟢 Added lower-effort retries for organization effort caps without changing user settings, excluding auto mode safety checks and requests naming a flagged-response fallback model (remote kill switch, off by default).
- 🟢 Added signed-out retries for HTTP and SSE MCP servers when stored sign-in is rejected and no refresh token is saved (remote switch, on by default).
- 🟢 Changed `/upgrade` for App Store and Google Play plans to direct users to the mobile app, then `/login` to activate the updated plan, instead of opening browser sign-in.
- 🟢 Renamed the `/permissions` review tab to Recently blocked, clarified that approval adds no rule, and blocked approvals for missing, blank, unreadable or truncated inputs and calls too tall to display.
- 🟢 Fixed terminal hyperlinks staying enabled when `FORCE_HYPERLINK` is set to `false`, `no` or `off`.
- 🟢 Made sandboxed headless `--resume` and `--continue` rebuild protections when entering a worktree, refusing to resume if rebuilding fails (remote switch, on by default).

---

### 2.1.312 ◆◇◇◇

- 🔴 Added server-provided Cyber Verification Program status to cyber-safeguard refusals, only on Anthropic's API, Claude Platform on AWS or Google Cloud, and Claude apps gateways.
- 🔴 Blocked `CLAUDE_CODE_OAUTH_TOKEN`, `CLAUDE_CODE_OAUTH_REFRESH_TOKEN`, `CLAUDE_CODE_OAUTH_SCOPES` and `CLAUDE_CODE_OAUTH_CLIENT_ID` in project settings, preserving shell and user settings.
- 🔴 Stopped several first-party requests from following cross-origin redirects, and OAuth token, refresh, revoke and account requests from following any redirects.
- 🔴 Changed the model-training notice to request opt-in only when unset; `grove_locked_by_claude_science` limits it to OFF and locks the setting in `/privacy-settings`.
- 🔴 Added session activity, approval status and a default 60-minute idle timeout to `claude remote-control` folder hosting, with two presses of `x` within 5 seconds to disconnect (remote switches, off by default).
- 🔴 Stopped Bash read-only checks and non-exact allow rules approving words with `*`, `?` or `[` or nonliteral assignments after `builtin`, `command` or `noglob` (remote switch, on by default); extra-check errors now need approval.
- 🟢 Made `Write` require a full read in one call before replacing nested `CLAUDE.md`, path-matched rules or `@`-included files truncated in context (remote switch, on by default).
- 🟢 Added Claude apps gateway `oidc.user_id_claim` for custom user-ID claims (default `sub`), including nested paths; `sub` remains required and invalid claims fail with `USER_ID_CLAIM_MISSING`.
- 🟢 Made fullscreen queued-message send-now hints clickable with mouse support, including with all keys rebound but not unbound; `CLAUDE_CODE_DISABLE_MOUSE` and `CLAUDE_CODE_DISABLE_MOUSE_CLICKS` disable clicks.
- 🟢 Changed unknown model IDs, including application inference profile ARNs unless mapped by `modelOverrides`, to use shorter system prompts on Bedrock, Vertex, Foundry and Mantle; `CLAUDE_CODE_SIMPLE_SYSTEM_PROMPT=0` forces full prompts.
- 🟢 Added refusal fallback for unknown model IDs, using configured Opus when available on cloud providers; disable it with `CLAUDE_CODE_DISABLE_REFUSAL_FALLBACK` or per-model `no_refusal_fallback` via `CLAUDE_CODE_MODEL_CAPABILITIES`.
- 🟢 Changed CLI-started cloud sessions to request titles and branch names from an Anthropic endpoint, except under HIPAA or zero-data-retention restrictions or without an organization-policy verdict.
- 🟢 Limited prompt and agent hooks to 24 concurrent per session, plus 12 for hooks past event timeouts, keeping 12 per event, with a one-second `timeout` minimum; `PermissionRequest` agent hooks are exempt from concurrency limits.
- 🟢 Changed subagents to honor `autoCompactWindow` when it is smaller than `CLAUDE_CODE_AUTO_COMPACT_WINDOW`; larger values still do not override the environment.
- 🟢 Changed OpenTelemetry `mcp_server.name` to report real names for fixed-URL MCP servers from verified official Anthropic marketplace plugins, excluding variable URLs and MCPB servers.
- 🟢 Changed `claude_code.safety_event` and its matching first-party analytics event to off by default; their remote switch can still enable them.

---

### 2.1.311 ◆◇◇◇

- 🔴 Added shell-only `CLAUDE_CODE_EVEN_MORE_DANGEROUSLY_SKIP_PERMISSIONS` to skip bypass-mode `rm` prompts until Bash, Edit or Read deny or ask rules, outside-directory read blocks or approval hooks or tools apply; Claude-run CLIs are excluded.
- 🔴 Added managed-settings-only `extraKnownMarketplaces[…].pluginDigests` to pin organization-tier hooks of plugins enabled by managed settings in `prependPlugins` or `appendPlugins` to matching plugin-folder SHA-256 digests.
- 🔴 Restricted repository and other plugins' environment variables for managed authentication and OpenTelemetry helpers and organization-plugin MCP and LSP servers; trusted-repository identifiers still reach `apiKeyHelper` and cloud helpers.
- 🔴 Added working-directory rechecks before tool calls, including file tools, rejecting calls if the session's project directory is deleted or resolves to a different path.
- 🔴 Allowed self-hosted runners behind an agent proxy to use Anthropic-managed git with `--exec-path` or command hooks, with Claude Code 2.1.311 or newer.
- 🔴 Made opt-in MCP cross-app sign-in (`CLAUDE_CODE_ENABLE_XAA=1`) stop sign-in and silent refresh when the issuing authorization server is no longer advertised; re-add the server with its client secret for expected moves.
- 🔴 Updated `/claude-api` docs for Go `/v2`, Java SDK 3.2.0, PHP SDK 1.0.0 or later for Managed Agents, automatic `pause_turn` resumption in newer Python and TypeScript runners, and API-key precedence over OAuth.
- 🔴 Added `Shift+Up` and `Shift+Down` to change effort at the prompt, stopping below `max` (off by default); `/effort max` is still needed for `max`.
- 🟢 Added `--hold-idle-file` (`SELF_HOSTED_RUNNER_HOLD_IDLE_FILE`) to hold idle `claude self-hosted-runner` sessions using a fresh regular file, excluding detected network paths and uncheckable links; `--max-hold-min` defaults to 24 hours.
- 🟢 Added compaction and retry when standard-context requests over 200K tokens are rejected for requiring usage credits, if auto-compaction is on and succeeds (switch on by default; cloud switch off by default).
- 🟢 Improved `Write` and `Edit` result diffs for replacements with no shared lines or unchanged outer lines; harder cases still have a five-second limit.
- 🟢 Added support in the `@` file picker for Git-ignored files re-included by `.ignore` or `.rgignore`.
- 🟢 Stopped deleting a subagent's clean isolated worktree while another task still uses it as its working directory.
- 🟢 Improved `/mcp` sign-in status: clearing authentication now reconnects remote servers immediately, and connected tools alone no longer count as signed in.
- 🟢 Improved `/rewind` warnings: conversation restore removes the selected and later messages, while code restore overwrites whole files but leaves Bash changes to other files untouched.
- 🟢 Added a follow-up for missing `<summary>` blocks in `/compact` and overlong-request compaction (switch on by default), excluding some automatic compactions, agent-team teammates and rewind summaries.
- 🟢 Improved dropped-connection errors for Anthropic's API to name the proxy or `ANTHROPIC_BASE_URL` gateway, or mention VPNs, firewalls and security software; cloud sessions are unchanged.
- 🟢 Changed `--output-format json` and `stream-json` to escape DEL, C1 and Unicode format characters, plus U+2028 and U+2029 in `json` (switch on by default), without changing parsed text.

---

### 2.1.310 ◆◇◇◇

- 🔴 Changed `/teleport` to allow confirmed cloud continuation with local changes or unpushed commits, using the branch as last pushed or the default if absent remotely; repositories rooted at the home folder or without `origin` are refused.
- 🔴 Stopped enforcing sandbox deny paths on other computers, with `/status` and `claude doctor` warnings; file-tool denies still apply, and write and edit denies from managed policy, user settings or `--settings` are generally kept.
- 🔴 Updated `/claude-api` model retirements and Anthropic-managed Google Cloud guidance; added a retiring-model scan behind a remote switch and experiment (off by default).
- 🔴 Fixed damaged blocked entries discarding all of `NODE_EXTRA_CA_CERTS`, and allowed two roots outside Anthropic, Claude, cloud-provider API and telemetry domains, except with Anthropic credentials or certain proxies.
- 🔴 Added support for Anthropic-managed git sessions with supplied git setup through self-hosted agent proxies (`--agent-proxy-url` or relay mode), except on Windows or runners using `--exec-path` or command hooks.
- 🔴 Stopped hooks attributed to the organization from inheriting repository settings' `env`, and added debug logs naming withheld variables.
- 🔴 Restricted shell auto-approval for path-like or command-substituted environment values and six more zsh builtins, and blocked `Read` on `/dev/pts/N`, `/dev/ptmx` and `/dev/tty*`.
- 🔴 Restricted more `git init` options, `-c` settings, `GIT_TEMPLATE_DIR` and `ARGV0` in worktree-isolated sessions and subagents, behind a remote switch (on by default).
- 🟡 (2.1.311) Added opt-in `CLAUDE_CODE_MODEL_CATALOG` support for Bedrock, Vertex, Foundry and Bedrock Mantle; remote catalogs stay disabled with nonessential traffic off, and project settings can only disable it.
- 🟢 Made `Monitor`, plugin monitors, `Monitor` scheduling guidance and the block on long foreground sleeps independent of remote flags; `Monitor` still requires a non-Windows system or Git Bash.
- 🟢 Added retries without `effort-2025-11-24` and `output_config.effort` on 400 responses rejecting the beta, and expanded fallback for rejected mid-conversation system messages.
- 🟢 Fixed background cleanup considering recent agent worktrees for removal when a very large `cleanupPeriodDays` value creates an invalid cutoff date.
- 🟢 Added symlink destinations to file read permission prompts outside remote workspaces, with a warning when a target cannot be resolved.
- 🟢 Fixed quoted-only `PreToolUse` and `PermissionRequest` command hooks allowing calls on Windows without Git Bash, behind a remote switch (on by default), except hooks with `shell`, `args`, `async` or `"onFailure": "continue"`.
- 🟢 Changed auto mode's first outside-directory read prompt to clarify that shell commands it cannot check require approval when the sandbox does not restrict those reads.
- 🟢 Added mod `Image` support in tmux with kitty 0.28+, Ghostty or iTerm2 3.5+, requiring `allow-passthrough` and `focus-events`; iTerm2 also needs passthrough `on`, fullscreen rendering and a window no larger than the terminal.
- 🟢 Improved Linux and WSL sandbox errors for AppArmor blocking bubblewrap, and made `sandbox.failIfUnavailable` refuse startup when that restriction prevents sandboxing.
- 🟢 Improved MCP timeout errors in print-mode and SDK sessions when a server question goes unanswered, telling Claude not to retry that turn; a repeated-question cap is off by default.

---

### 2.1.296 ◆◇◇◇

- 🔴 Added SDK `set_model` support for replacing only the custom system prompt via `only_if_model_is_current: true`, requiring a nonempty prompt and an explicit matching model, excluding hybrid mode and Remote Control.
- 🔴 Fixed strict-host permission replies allowing tool calls when their requested deny or ask restrictions could not be kept.
- 🔴 Added experimental `Agent` effort values `lower` and `higher` for relative adjustments (off by default), excluding `max`, forks, remote agents and teammates, subject to existing model and effort overrides.
- 🔴 Added experimental MCP file-argument uploads for supported claude.ai connectors and matching host-held HTTP servers (off by default), requiring authorization for local files.
- 🔴 Added an opt-in host policy restricting `SendMessage` to plain-text messages between agents in the same session.
- 🟢 Improved secret redaction for plain and escaped assignments when an empty value precedes a later value, including JSON in shell strings.
- 🟢 Added `allow_large` to `Read` for larger text files in local sessions with spare context, without increasing remote-call or other-machine limits.
- 🟢 Added an `Edit` encoding check that refuses UTF-8 rewrites of files containing invalid UTF-8 bytes, rather than replacing undecodable characters.
- 🟢 Added subagent `autoCompactWindow` in frontmatter and `--agents` to lower local windows to integer token counts of 100,000–1,000,000; `CLAUDE_CODE_AUTO_COMPACT_WINDOW` takes precedence and built-in forks keep the parent's window.
- 🟢 Added `CLAUDE_CODE_WORKFLOW_SUBAGENT_MODEL` to override models for Workflow agents only; empty values and `inherit` leave selection unchanged, and forced-model policy still applies.
- 🟢 Added `CLAUDE_CODE_OVERLOADED_RETRY_MAX_DELAY_MS` to set eligible overload retries' backoff cap to 32,000-64,000 ms; jitter and `Retry-After` can extend delays.
- 🟢 Changed Sonnet 5.5 cache-read cost estimates from $0.20 to $0.10 per million tokens; account billing is unaffected.
- 🟢 Improved plugin diagnostics to identify `hooks.json` hooks or hook modules skipped for duplicate plugin names, and explain which enabled copy takes precedence.
- 🟢 Added a `/code-review` foreground-fork formatter for numbered findings with file and line locations or a no-findings message; raw text and JSON modes bypass it.

---

### 2.1.267 ◆◇◇◇

- 🔴 Added `session.compact` hooks to veto or rewrite non-isolated compaction, plus `$.session.compact()` for plugins to request compaction between turns in bound, non-headless sessions.
- 🔴 Added `if_version` checks to Artifact `set`, `delete` and batch entries behind the version-pin gate, with no non-atomic fallback for pinned batches.
- 🔴 Made HIPAA restrictions survive organization switches until restart, preserving Remote Control denial and adding HIPAA checks for `/insights` and transcript-scanning statistics.
- 🔴 Made `sec-default` precede user plugins where hooks modules are enabled on machines with managed settings or in Team/Enterprise organizations; only managed `secDefault: false` can opt out.
- 🔴 Improved shared-memory sync to handle deleted-content conflicts, removing stale local copies when timestamp checks pass and otherwise preserving them.
- 🟢 Added global and per-model `maxEffortLevel` caps across providers; `output_config.effort` in `CLAUDE_CODE_EXTRA_BODY` bypasses them.
- 🟢 Fixed malformed managed `allowedHttpHookUrls`, `httpHookAllowedEnvVars` and `allowedChannelPlugins` dropping restrictions; empty allowlists now apply unless valid entries remain.
- 🟢 Fixed a directory containment bypass by rejecting relative marketplace paths that contain backslashes.
- 🟢 Made command, skill and subagent effort override pinned defaults for Opus 4.7, Opus 4.8 and Fable 5, while still respecting environment effort, model support and caps.
- 🟢 Improved auto-mode safety review for Workflow `agent()` output schemas above 4,096 code units, up to 4,000,000, subject to a node budget, while still blocking schemas it cannot review.
- 🟢 Added one automatic retry on a fresh connection for eligible transport failures during Artifact deploy uploads, excluding user aborts, started responses and ambiguous or near-complete uploads.
- 🟢 Made usage-limit warnings reuse valid, unretired readings from the past 30 minutes when an allowed response omits them (remotely controlled, on by default).

---

### 2.1.263 ◆◆◆◇

- 🔴 Added effort-reduction prompts for Fable 5.1 at `high`, `xhigh` or `max`, with remotely configured targets and confirmation before saving defaults; switching is blocked during ultracode.
- 🔴 Added experimental `CLAUDE_CODE_POLISHED_DEWDROP` for eligible first-party requests: `drop` asks to discard mismatched thinking blocks, `block` requests an error, and `off` leaves the policy unset.
- 🔴 Added HTTP 400 fallback for an unsupported thinking-binding beta or extra `block_binding` inputs when binding is active and its beta is prepared; generated values stay omitted until reset or unlatch, but explicit betas can still be sent.

---

### 2.1.259 ◆◇◇◇

- 🔴 Made invalid `allowUnattendedServing` settings block unattended cloud commands until corrected, requiring approval to run commands on this computer.
- 🔴 Changed Artifact pinning to affect only the user's private sidebar, without changing visibility; pinning someone else's Artifact requires live consent, and unpinning is reversible.
- 🟢 Restricted organization-managed MCP servers to HTTP/SSE over valid HTTPS URLs and prevented local removal.
- 🟢 Added `--permission-prompts none` for headless `--print` hosts to automatically deny actions that need a prompt; cloud sessions still send prompts to the host over stdio.
- 🟢 Fixed config writes using defaults after a rejected locked reread by rebasing on the enqueue-time snapshot when safe or refusing the write.
- 🟢 Stopped agents from launching agents, skills, workflows or monitors, or resuming or messaging agents, while their stop is still completing.

---

### 2.1.258 ◆◆◆◆

- 🟢 Stopped user messages with empty content arrays from reaching the API, dropping them before request processing.
- 🟢 Stopped extra model calls when a re-sent permission approval cannot be applied and no prompt or deferred work remains.

---

### 2.1.257 ◆◇◇◇

- 🔴 Added release-manifest signature checks to native updates and blocked installation of staged binaries that no longer match verified checksums, with legacy signature exceptions.
- 🔴 Changed cloud-sync consent to warn that files Claude reads and command output can be seen by session viewers and Team/Enterprise admins, and cloud changes are not copied back locally.
- 🟡 (2.1.267) Made resumed conversations reuse the recorded system prompt despite later prompt flags, when system-prompt recording is enabled.
- 🟢 Added support for fencing `Read`, `Grep`, `Glob` and `LSP` to working directories in every permission mode; sandbox fencing excludes the relaxed filesystem policy.
- 🟢 Stopped repositories from granting `bypassPermissions` through project or local settings; only policy settings, user settings or flags may enable it.

---

### 2.1.252 ◆◇◇◇

- 🔴 Added support for retaining `prompt_snapshot` events through session-context processing.
- 🔴 Added explanations for session-context rereads after compaction, managed-settings changes, working-directory additions, settings sync or account changes.
- 🔴 Added a model instruction to stop using the previously announced scratchpad directory when it becomes unavailable.
- 🟢 Stopped Remote Control sessions from waiting for session-persistence writes after tools finish, so degraded connections no longer hold turns open.

---

### 2.1.251 ◆◇◇◇

- 🔴 Added support for Artifact live room page events from anyone in your organization with the page open, now or after sharing, to start turns after room approval, even without you present.
- 🔴 Added guidance to use `--fork-session` when branching a copied conversation.

---

### 2.1.250 ◆◆◇◇

- 🔴 Changed Artifact watch guidance to restart watches only on user request or when the task needs republishes, noting they do not reconnect automatically.
- 🔴 Improved Artifact re-watch notices to explain that there is nothing to re-watch while live updates are off.
- 🔴 Added `cf_mitigated` and `upgrade_rejected` classifications for WebSocket upgrade failures, with their HTTP status codes.
- 🔴 Improved stalled Artifact watch reports with reconnect limits, unavailable errors and HTTP status details from startup failures.
- 🔴 Changed stalled Artifact watches to allow separate randomized long delays and clear the old stall deadline when rearmed.
- 🔴 Added passive delivery for watch-ended notices while keeping their advice attached.

---

### 2.1.248 ◆◇◇◇

- 🔴 Added `/limit-reset` so eligible users can reset their session limit once a week; usage still counts toward the weekly limit.
- 🔴 Added automatic edits to watched artifacts from writer comments, subject to server rechecks of the writer, thread edit grants and single-file, size and rate limits.
- 🔴 Added live presence data on artifact pages, shared among viewers and produced by the page's code rather than typed as messages.
- 🔴 Added a server-configured `◆ <text>` status pill to the prompt footer.
- 🔴 Added `sdkMcpServers` settings, sent separately so older CLIs ignore them.
- 🔴 Changed directory sync to distinguish uploads that are incomplete, interrupted, stalled, abandoned or arriving mid-session.
- 🔴 Renamed `Coordinator check-in` to `Worker check-in`.
- 🟡 (2.1.212) Changed Windows PowerShell selection to prefer PowerShell 7 when installed, including Microsoft Store installs, with Windows PowerShell 5.1 as fallback.
- 🟢 Added `--restricted` / `CLAUDE_CODE_RESTRICTED` to remove `Bash`, `PowerShell`, `REPL` and `WebFetch` unless in `--tools`, limit file tools to the working directory, reject `bypassPermissions` and ignore user, project and local settings.
- 🟢 Added `claude self-hosted-runner --client-label` to override the runner's registration label.
- 🟢 Added a `workflow-authoring` skill with the `Workflow` tool's script-writing reference.
- 🟢 Added a warning when your GitHub CLI token lacks the `workflow` scope needed to push changes to Actions workflow files.
- 🟢 Added `desktopSessionCleanupPeriodDays` to limit how long transcripts written by desktop-host surfaces, including Claude Desktop and Cowork, survive cleanup.
- 🟢 Changed handling of invalid `crossSessionInbound` values to warn and hold messages, or reject messages under managed settings.
- 🟢 Removed the runtime gate for `/loop`'s self-paced dynamic mode.
- 🟢 Restricted cross-session trust in Linux user namespaces to processes with mapped user IDs.
- 🟢 Changed OAuth refresh to explain when another Claude Code process holds the refresh rather than sending you to the login screen.

---

### 2.1.247 ◆◇◇◇

- 🔴 Added Artifact `preview` to return screenshots of a local `.html` file in light and dark themes at desktop and phone widths
- 🔴 Added Claude Design authorization handling that distinguishes missing claude.ai credentials from valid credentials without Claude Design access
- 🔴 Added a remote-tool protocol for `claude --cloud` sessions, with tool announcements from attached machines and per-call approval
- 🔴 Added a `/cloud-plugins` consent flow for sending a machine's plugins to cloud sessions
- 🔴 Added a system prompt for writing on the user's behalf and updated memory instructions and the `whiteboard`, `design`, and `agent-design-patterns` skills
- 🔴 Renamed `/design-login` to `/design login`
- 🟢 Changed `spinnerTipsOverride` from strings to `{id, text, cooldownSessions, priority}` entries plus `tipsFile` and `label`, removing `excludeDefault`
- 🟢 Changed MCP connection errors to distinguish servers that do not answer from unreachable servers
- 🟢 Changed oversized hook and background output to be truncated with an explicit marker rather than overflowing the conversation
- 🟢 Changed terminal output to filter control and invisible characters in marketplace names and rendered hyperlinks

---

### 2.1.246 ◆◇◇◇

- 🔴 Added a shared whiteboard artifact for wireframe diagrams with shapes, sticky notes, arrows, freehand drawing, and text
- 🔴 Added artifact asset stores with `upload_asset` and `list_assets` for images, video, PDFs, fonts, and text files
- 🔴 Added artifact watching to notify sessions when pages are republished and wake cloud sessions when comments arrive
- 🔴 Added unattended replies to artifact comments after explicit consent, limited to artifacts the user can edit and whose link they supplied
- 🔴 Added scheduled recurring cloud agents, including cron-style routines
- 🔴 Added memory stores with addressable documents, a description, a writable or read-only flag, and an index document
- 🔴 Added cloud-session sync for the working tree and the user's `CLAUDE.md`, permission rules, and preferences
- 🔴 Stopped running hooks for cloud-originated calls unless their commands can be pinned to a single script outside the synced project
- 🔴 Reorganized embedded modules and assets across all five platforms, adding 189 records per client
- 🟡 (2.1.275) Added plugin sync from claude.ai, with a setting to turn it off
- 🟡 (2.1.243) Added organization-managed `modelPricing` overrides, recording whether requests use list rates or managed pricing

---

### 2.1.243 ◆◆◆◇

- 🔴 Changed the LSP tool gate to default on instead of requiring an environment-variable opt-in

---

### 2.1.241 ◆◆◆◇

- 🔴 Added the effective Sable Thrush feature gate to `experiment_gates` notifications sent to the VS Code extension
- 🔴 Changed non-interactive sessions, including SDK and `-p`, to allow thinking narration and connector text unless display is explicitly omitted
- 🔴 Changed narration signature decoding to use `atob` and `Uint8Array` instead of `Buffer`, returning cleanly on malformed base64
- 🔴 Removed internal narration exports `NARRATION_SUMMARY_LABEL` and `getSignatureBlockKind`
- 🔴 Changed SDK documentation to clarify that `null` restores Claude Code's own thinking-display handling

---

### 2.1.226 ◆◆◆◆

- 🔴 Changed only file and product version resources on Windows, with no substantive JavaScript changes and identical bundled prompts across all five clients
