# CI runner contract

General CI, browser suites, generated-output sync, maintenance, and release
publication use the `kalana-ci` scale-set label. Apple release builds
use `self-hosted` and `kalana-macos-ci`. Native Windows Rust/launcher checks,
MSVC builds, and signing retain GitHub-hosted Windows runners.

The Linux runner needs Git, curl, and an available C/C++ linker. Playwright E2E
jobs install Chromium and its Linux system packages with `--with-deps` on every
run, including browser-cache hits; the runner must permit that package setup.
Puppeteer suites still need their Chrome runtime libraries. Workflows install
Node, Bun, and Rust explicitly. Linux release builds also use the existing musl-tools
installation and Docker-backed `cross` build. The sheriff jobs install a
checksum-verified GitHub CLI into a temporary directory when absent. Publication
retains its existing sudo/apt GitHub CLI setup.

The Mac needs Xcode command-line tools. On Apple Silicon, Rosetta 2 is required
to execute the Intel release binary's smoke test; the workflow checks this
prerequisite and fails with an actionable message. CI does not install Rosetta
or change the Mac's system settings.

Runner names alone do not select runners. The selected runner label must be
registered and online and accessible to this repository. The Linux scale set
uses only `kalana-ci`; it does not require the default `self-hosted` label. External-fork
pull requests do not execute code on the persistent self-hosted machines.

The main CI workflow must be enabled in the fork's Actions settings. Provider
diagnostics retain their existing API-key and opt-in conditions; the
`skill_workflow` manual input defaults to false. Native release/signing jobs
still require their existing tag, environment, and identity configuration.
