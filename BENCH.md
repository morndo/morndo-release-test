# Release bench

This repository is the test bench for the Morndo release pipeline. It is not a product: every release here is a test and
nothing should install from it. The tree is a copy of morndo/morndo, and these files differ (the bench overlay):

- `trust/*`: public keys of throwaway test keys made for this bench. Their private halves are the repository secrets
  `RELEASE_SSH_KEY` (environment `release`); nothing here is the real release identity.
- `.github/workflows/release.yml`: the `release-please` job is replaced by one that makes the tag and the draft release
  the way Release Please does (the org does not let Actions open pull requests, and this repository has no release app),
  and the feed and Pages jobs are left out. Every job from `build` to `published` is the pipeline's own. Release Please
  itself is not exercised here.

Also differing, since they pin the production files the bench replaces: the workflows other than `release.yml` and the
four test files that read them (`scripts/release/workflow.test.ts`, `scripts/release/signing.test.ts`,
`apps/hub/test/val-b12-e2e-listed.test.ts`, `plugins/transcribe-whisper-cpp/test/install.test.ts`) are removed. The
history is the branch's full history, because the downgrade-contract tests read an earlier commit.
