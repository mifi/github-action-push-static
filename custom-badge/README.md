# Custom badge example

We will use `badge-maker` from [shields.io](https://github.com/badges/shields) to generate a badge image to publish using the workflow from the parent example.

Example badge:

![](example.svg)

You need to run this setup to your source repo:

```bash
yarn init # Optional
yarn add -D badge-maker
```

We need another few steps in our `workflow.yml`, **before** the steps that push to the destination repo. This example will use jest to create a coverage report and then generate an SVG:

```yml
- name: Create JEST coverage
  run: jest --coverage --coverageReporters json json-summary lcov

- name: Generate the badge from the json-summary
  run: node generate-coverage-badge.js coverage/coverage-summary.json

- name: Copy the badge to the correct location
  run: cp coverage-badge.svg static-build/
```

Then add the provided [generate-coverage-badge.js](generate-coverage-badge.js)

Now your badge should be served from the static repo and can be included in a README.md with:
```
[![](https://your-username.github.io/static-files-destination-repo/coverage-badge.svg)](https://your-username.github.io/static-files-destination-repo/)
```

## Example live repo

- Source repo: [ical-expander](https://github.com/mifi/ical-expander)
- Static files destination repo: [ical-expander-coverage](https://github.com/mifi/ical-expander-coverage) ([mifi.github.io/ical-expander-coverage](https://mifi.github.io/ical-expander-coverage/ical-expander))

## Inspired by

- https://github.com/marketplace/actions/dynamic-badges