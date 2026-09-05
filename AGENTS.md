# Project Agent Instructions

## Scope

These instructions apply only to this portfolio repository and its subdirectories. This is a static public website; keep it deployable without a build step unless the user asks otherwise.

## Core files

- `index.html`: UI and client-side behavior.
- `content.json`: source of truth for English and Vietnamese copy.
- `content-fallback.js`: generated fallback for direct `file://` viewing.
- `cv.pdf`: canonical public CV filename.

Always use deployable relative URLs such as `./cv.pdf`, never local paths such as `/Users/...`.

## Automatic Git workflow

Run the automatic Git workflow when:

- the user sends standalone `done` (case-insensitive, with optional punctuation); or
- the user provides, finalizes, or asks to publish a new CV/resume.

Do not trigger it when the user is merely quoting or discussing the word `done`.

After a valid trigger:

1. Run only the minimal structural checks listed below.
2. Review `git status` and `git diff`, then stage only files belonging to the current task. Never use `git add .` or `git add -A` in a dirty worktree.
3. Commit with a concise task-specific message. For a CV-only update, prefer `chore(cv): update portfolio CV`.
4. Verify that `origin` is `https://github.com/dangtri73/thanhchinguyen_porfolio.git`, then push the current branch normally without asking again.
5. Report the commit hash, branch, and push result.

Never force-push, rewrite history, reset unrelated work, or create an empty commit. If there is no new diff, push an existing unpushed task commit if present; otherwise report that the branch is already synchronized.

## CV updates

When a new or finalized CV is involved:

1. Resolve the exact source PDF; ask only if multiple candidates make the choice unsafe.
2. Confirm it exists, is non-empty, and is recognized as a PDF.
3. Rename or move it to the repository root as exactly `cv.pdf`.
4. Confirm preview and download still use `./cv.pdf`, download links retain the `download` attribute, and no Google Drive CV URL is present.
5. Include the CV replacement and any required reference changes in the automatic Git workflow.

## Bilingual content

If the user requests a content change without specifying a language, update both:

- `content.json` → `languages.en`
- `content.json` → `languages.vi`

Keep both locale structures aligned. Translate naturally while preserving proper names, brands, URLs, campaign names, and verified metrics. If the user explicitly requests one language only, update only that language.

After changing `content.json`, regenerate `content-fallback.js` from it and verify that `window.PORTFOLIO_CONTENT` is structurally identical to the parsed JSON. Do not author the fallback separately.

## Minimal checks only

Run only checks relevant to files changed in the current task:

- Always run `git diff --check`.
- If `content.json` changed, confirm that it parses as JSON.
- If JavaScript changed, run a syntax check only.
- If the CV changed, confirm that `cv.pdf` is recognized as a PDF.

Do not run any other tests unless the user explicitly asks for them.

## Safety

Preserve pre-existing user changes and never stage unrelated files. Never commit credentials, private keys, environment files, or other secrets to this public repository.
