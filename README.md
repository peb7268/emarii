# Emarii

**Emarii** (M-Ari) — a desktop app for reviewing GitLab merge requests and GitHub pull requests.
One list for both, triage from a right-click menu, an AI review you edit before posting,
a merge that refuses to fire unless every check passes, and a loop that re-reviews
watched MRs as they change.

**This repository holds releases only.** The source is private.

## Download

Grab the latest build from [Releases](../../releases).

- **macOS** — `Emarii_<version>_universal.dmg`, Intel and Apple Silicon, macOS 13+
- **Windows** — `Emarii_<version>_x64.exe`, a portable executable, Windows 10/11 x64

The Windows filename carries the version it was **built** at. Windows builds are produced
on a separate machine, so when that number is lower than the release's, the Windows build
is behind the macOS one.

## First run

Builds are **unsigned**.

**macOS** — Gatekeeper refuses a downloaded copy. Either right-click the app → **Open**
once, or:

```bash
xattr -dr com.apple.quarantine /Applications/Emarii.app
```

**Windows** — SmartScreen warns on first run: **More info → Run anyway**.

## What you need installed

Emarii shells out to the CLIs you already use and **never reads or stores a token** — `gh`
and `glab` keep their own credentials in your OS keychain.

| | Why | Install |
|---|---|---|
| [`gh`](https://cli.github.com) | GitHub pull requests | `brew install gh` · `winget install GitHub.cli` |
| [`glab`](https://gitlab.com/gitlab-org/cli) | GitLab merge requests | `brew install glab` · `winget install GitLab.glab` |
| [`claude`](https://claude.com/claude-code) | writes the reviews | `npm install -g @anthropic-ai/claude-code` |

Sign in to each once (`gh auth login`, `glab auth login`, `claude` then `/login`).
Settings → **Required tools** shows what is missing and the exact command to fix it.

## What it does

- Both providers in one list, with pipeline, approvals, unresolved threads and conflicts
- Source → target branch on every row
- Right-click triage: approve, request changes, review, merge
- **Guarded merge** — reads every check live and pins the merge to the checked commit, so
  a push between the check and the merge fails instead of landing unreviewed code
- **Review loop** — watch an MR and it re-reviews as the author pushes, carrying findings
  forward and closing them when they are fixed
- **Autopilot** — review everything not yet reviewed, honouring your semi-auto/auto setting
- Menu-bar item with a ready count, global shortcut, notification bell with history

## Privacy

MR content goes only to the review command you configure. There is no telemetry, and no
credential ever passes through Emarii.
