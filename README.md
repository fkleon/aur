# fkleon's AUR packages

Package sources for all the AUR packages I officially [maintain](https://aur.archlinux.org/packages?SeB=m&K=mysticx), or unofficially host modified versions of.

Package subtrees were historically maintained using
[aurpublish](https://github.com/eli-schwartz/aurpublish). Automated publishing now uses
[`github-actions-aur-publish`](https://github.com/ulises-jeremias/github-actions-aur-publish).

## GitHub Actions publishing

`.github/workflows/publish-aur.yml` runs on pushes to the `main` branch. Its `changes`
job checks the nine package-directory patterns listed in the workflow; each matching
directory produces a matrix job that invokes the AUR publish action. Changes outside
those directories do not create publish jobs.

Each matrix value is used both as the AUR `pkgname` and as the source directory passed to
`asset_dir`. That directory is mirrored to AUR, so file additions, updates, and removals
within it are reflected there. The workflow sets `allow_empty_commits` to false. Removing
an entire package directory does not delete the AUR package; the publish job will fail
because its source directory is missing, so handle package deletion manually.

The publish job uses the GitHub Environment named `aur`. Configure these **environment
secrets** there:

- `AUR_SSH_PRIVATE_KEY`: a dedicated, unencrypted SSH private key whose public key is
  registered with your AUR account.
- `AUR_COMMIT_USERNAME` and `AUR_COMMIT_EMAIL`: the author identity for AUR commits.

The action obtains AUR SSH host keys with `ssh-keyscan` at runtime rather than using a
pinned `known_hosts` file. It creates commits directly in each AUR repository rather
than splitting the monorepo history with `aurpublish`. `dry_run` is enabled when the push
branch is not the repository's default branch; because the workflow triggers only on
`main`, it publishes only when `main` is the default branch.