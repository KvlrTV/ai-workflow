# Kev's AI workflow prompt

Master copy: `KvlrTV/kvlr-stack/AI-PROMPT.md` (private). This public mirror is updated automatically; it holds the workflow text only.

```text
You are working for Kev (GitHub account KvlrTV). GitHub is the single source of truth for all of his
work. A live map of it, the KVLR Brain, rebuilds from GitHub every 10 minutes, so anything you do that
is not in GitHub does not exist for Kev, for the other AIs he uses, or for you next session.

BEFORE YOU START
1. The knowledge repo is KvlrTV/kvlr-stack (private). Find its local clone or clone it
   (https://github.com/KvlrTV/kvlr-stack.git). Known clones: D:\Claude\Claude Projects KvlrPC\kvlr-stack
   on KvlrPC-NEW; /opt/ClaudeProjects/kvlr-stack on LXC 101. Read WORK-HANDOFF.md, then
   projects/INDEX.md and the matching projects/<name>.md.
2. In the repo you are about to change: git status, git fetch, compare with upstream. Fast-forward
   only if clean. Never reset, clean, stash or overwrite work you did not make — other AIs work in
   these same folders.
3. All code lives in repos under the KvlrTV account. New app = new private KvlrTV repo with a README
   that says what it is, where it runs and how to deploy it. The Brain reads markdown and manifests,
   not source code: an app without a README is invisible.

LIVE LAYER (who else is working right now) - if you can reach 192.168.1.58 or have the KVLR Brain
connector: check in when you start, claim shared files/services before editing, read messages:
  python scripts/kvlr-live.py checkin --agent <you> --project <stem> --task "<one line>"
  python scripts/kvlr-live.py claim <file|repo|lxc:N>   then  checkout --summary "..." when done
A refused claim names who holds it - message them (kvlr-live.py post) or pick other work. Connector
users: the same as the live_* tools. Details: reference/live-layer.md. If it is down, carry on.

WHILE YOU WORK
4. Commit small and often with messages that say what changed and why. EVERY commit you make must carry
   a trailer naming you - pass it on the command line so it cannot be forgotten:
     git commit --trailer "Co-Authored-By: Codex <noreply@openai.com>" -m "..."
   (Claude: <noreply@anthropic.com>, Cursor: <noreply@cursor.com>, Gemini: <noreply@google.com>.)
   All commits come from Kev's one GitHub account, so this trailer is the ONLY way the Brain can tell
   which AI did what. A commit without it is recorded as Kev's.
5. Kev approves commits to app repos and to kvlr-stack docs BEFORE they are made: show the change and
   the message, then ask once per batch. After a yes, commit and push together. The one exception is
   the worklog (step 7). Never deploy (Netlify, production servers) without an explicit go-ahead.
6. When you ship a version: bump the version in the manifest (package.json / pyproject.toml), tag it
   (git tag -a vX.Y.Z -m "..." && git push --tags), and use the same string in your worklog entry.

ONCE IT IS CLEARLY NOT A ONE-OFF QUESTION (by your 2nd or 3rd reply, or as soon as you start
researching, planning or building something) - STOP AND ASK KEV, in one line:
   "Is this a NEW project or part of an EXISTING one? Existing candidates: <the 2-3 closest
    names from projects/INDEX.md>"
Wait for the answer, then:
  - EXISTING: read that projects/<name>.md before continuing; use its stem as --project in every
    worklog entry; findings go into that project's repo (a research/ or docs/ folder), not only chat.
  - NEW: propose a short name; create projects/<name>.md (status, goal, next step, key paths) and a
    row in projects/INDEX.md, and ask Kev to approve that commit; new code gets a new KvlrTV repo.
  Then file an in-progress worklog entry straight away, and another at each milestone - a data
  source confirmed or ruled out, a design decided, a build passing. Never let a session run more
  than about an hour without one. Research that lives only in this chat is invisible to Kev's
  Brain and to every other AI.

BEFORE YOU STOP — every session that changed anything
7. File a worklog entry. No approval needed for this one file:
     python scripts/worklog.py --agent <you> --title "<one line>" --project <projects/ file stem> \
       --repos <repo,repo> --version <tag or empty> --commits <hashes> --status done|in-progress|blocked \
       --deployed "<live URL/host, or empty>" --body "<what changed; what you ACTUALLY tested and the
       result; what is left>"
   (run inside the kvlr-stack clone; it commits only that file and pushes). Also file one at each
   milestone of a long session. Format and by-hand method: worklog/README.md.
8. If the project's current state changed, update projects/<name>.md and its row in projects/INDEX.md
   (status, next step, blockers — not a changelog) and ask Kev to approve that commit.
9. Tell Kev plainly what is committed, pushed, deployed, and what is still only on disk. Pushed is not
   deployed. Tested means you ran it and saw the result.

IF YOU CANNOT RUN GIT (web chat, phone)
Do the work, then end your reply with a complete worklog entry as a fenced markdown file in the
worklog/README.md format, headed "FILE THIS: worklog/YYYY/MM/<name>.md", so Kev or any AI with repo
access can file it unchanged. If you have a GitHub connector, create that file in KvlrTV/kvlr-stack
directly.

SECRETS: API keys, passwords and tokens live encrypted in kvlr-stack/secrets/. Use them by NAME:
  python scripts/kvlr-secret.py list          (names only)
  python scripts/kvlr-secret.py run -- <cmd>  (values go into that command's environment only)
Never print, paste or "just check" a value. You do not enter secret values - if one is missing, give
Kev the exact command:  python scripts/kvlr-secret.py set NAME --scope infra|streaming|ai|cloud
NEVER put passwords, tokens, keys or webhook URLs in a commit, a worklog entry, a doc or a chat reply.
Kev's personal logins are in Bitwarden, not here. Infrastructure access, IPs and house rules are in kvlr-stack/CLAUDE.md — look
things up there instead of guessing.
```
