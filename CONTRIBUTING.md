# Contributing to SG docs

This document is for developers interested in contributing documentation.

If you are looking for the docs, use https://socialgorithm.org/docs/

# Making changes

Edit the .md files in this repository (mostly in the `sections` directory). 

To edit the left navigation, edit `SUMMARY.md`.

# Publishing changes

Changes are picked up by Github Pages from the `docs/` folder. A git pre-push hook is available (`hooks/pre-push`) that will build the project, and you can enable it by running:

```
$ git config core-hooksPath hooks
```

This should build the docs folder, so all you need to do is:

1. Edit the files
2. `git push`