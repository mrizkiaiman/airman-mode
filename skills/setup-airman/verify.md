# Verify

The commands that prove a change works in this repo. Skills run these instead of guessing.

| Check | Command |
| --- | --- |
| Install | [e.g. `pnpm install`] |
| Test, all | [e.g. `pnpm test`] |
| Test, one file | [e.g. `pnpm test -- <path>`] |
| Typecheck | [e.g. `pnpm typecheck`, or `none`] |
| Lint | [e.g. `pnpm lint`, or `none`] |
| Run the app | [e.g. `pnpm dev`, serves http://localhost:3000] |
| CI | [e.g. `.github/workflows/ci.yml` runs test, typecheck, and lint] |

## How to use these

- While working, run the single-file test and the typecheck often.
- Before each commit, run the full test suite, typecheck, and lint.
- When the change has a visible surface (a page, an endpoint, a CLI), also run the app and exercise it. A passing unit test shows one branch works. It doesn't show the feature works.
- "Inconclusive" counts as a failure. Report it instead of claiming the change is done.

## Gaps

[List each check above marked `none`, in one line each, or write "None".]
