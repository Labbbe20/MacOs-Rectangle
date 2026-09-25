# Upstream Synchronization

This fork keeps the application source as close to upstream as possible. Local automation is limited to `.github/workflows/sync-upstream.yml` and the state files in this directory.

The workflow:

- Merges `rxhanson/Rectangle` `main` into this fork's `main` on a schedule and on manual runs.
- Force-syncs upstream tags into the fork.
- Mirrors the most recent upstream GitHub releases and their release assets into this fork.
- Runs a best-effort unsigned macOS build when upstream source changes or when the workflow is run manually.

Rectangle is open source and the upstream repository includes a public Xcode build workflow. The official upstream DMG, PKG, and Sparkle delta assets are still mirrored from upstream releases so the fork stays aligned with what upstream publishes.

The CI build artifact in this fork is ad-hoc signed by GitHub Actions and is not notarized with the upstream maintainer's Apple Developer credentials.

If GitHub Actions reports that the release API is not accessible by the default integration token, add a repository secret named `RELEASE_TOKEN` with permission to create releases and upload release assets. The workflow uses that secret automatically when it is present and falls back to `GITHUB_TOKEN` otherwise.
