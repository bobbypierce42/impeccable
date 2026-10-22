# CI runner contract

General CI, browser suites, generated-output sync, maintenance, and release
publication use the `self-hosted` and `kalana-ci` labels. Apple release builds
use `self-hosted` and `kalana-macos-ci`. Native Windows Rust/launcher checks,
MSVC builds, and signing retain GitHub-hosted Windows runners.

The Linux runner needs Git, curl, an available C/C++ linker, and Chromium's
system libraries for the Puppeteer/Playwright suites. Workflows install Node,
Bun, and Rust explicitly. Linux release builds also use the existing musl-tools
installation and Docker-backed `cross` build. Publication and issue triage
install the GitHub CLI through the existing sudo/apt setup when needed.

The Mac needs Xcode command-line tools. On Apple Silicon, Rosetta 2 is required
to execute the Intel release binary's smoke test; the workflow checks this
prerequisite and fails with an actionable message. CI does not install Rosetta
or change the Mac's system settings.

Runner names alone do not select runners. Both runner labels must be registered
and the runner must be online and accessible to this repository. External-fork
pull requests do not execute code on the persistent self-hosted machines.

The main CI workflow must be enabled in the fork's Actions settings. Provider
diagnostics retain their existing API-key and opt-in conditions; the
`skill_workflow` manual input defaults to false. Native release/signing jobs
still require their existing tag, environment, and identity configuration.
