# Contributing to SG docs

This document is for developers interested in contributing documentation.

If you are looking for the docs, use https://socialgorithm.org/docs/

# Making changes

Edit the .md files in this repository (mostly in the `sections` directory). 

To edit the left navigation, edit `SUMMARY.md`.

## Editing Images

Edit images by going to https://www.draw.io and loading the PNG file. When done, remember to **EXPORT as PNG and "Include a copy of my image"**.

# Publishing changes

Documentation is published to Github Pages from the `docs/` folder. You **must** run

```
$ yarn build
```

before you push your changes. This will build the docs folder.