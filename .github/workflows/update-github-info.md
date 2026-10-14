---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
engine:
  id: copilot
  copilot-sdk: true
tools:
  bash: false
  cli-proxy: false
  edit:
  github:
    toolsets: [repos]
  web-fetch:
network:
  allowed:
    - defaults
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[GitHub Info] "
    draft: false
    reviewers: [mona]
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md` before making any changes.

Use the `web-fetch` tool to fetch both:

- https://github.blog/latest/
- https://github.blog/changelog/

Find recent developments that would make useful, practical guidance for developers learning GitHub. Keep updates short, accurate, and consistent with Mona's editorial angle. Include a clear source link for every item based on the GitHub Blog or Changelog; do not add claims that the fetched sources do not support.

Use the GitHub repository API tools to read repository guidance or reference files when needed. Do not use the terminal, GitHub CLI, or sandboxed shell commands to read those files.

Edit only `site/content/github-info.md`, preserving its existing structure and replacing stale items only when the sources justify it. If there is no useful, well-supported update, leave the file unchanged and do not open a pull request.

When the file changes, propose the update with the configured `create-pull-request` safe output so Mona can review it. Do not write directly to `main`, push changes yourself, or modify any other file. Summarize the source links and editorial changes in the pull request description.