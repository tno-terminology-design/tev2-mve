---
# Front matter for the static site generator
title: Workflow File
# Front matter for TEv2 Curated Texts
term: workflow-file
glossaryTerm: "Workflow file"
glossaryText: "a YAML file stored in the `.github/workflows` directory of a GitHub repository that defines jobs, steps, and triggers for GitHub Actions. In our context, this file is used to compile and deploy the static website of an [MVE](@)."
formPhrases: [ "Workflow file{ss}" ]
---

# Workflow File

A **workflow file** is a YAML file stored in the `.github/workflows` directory of a GitHub repository that defines jobs, steps, and triggers for GitHub Actions.

The contents of that file follows the [workflow syntax for GitHub Actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions).

You may consult [GitHub's documentation about workflows](https://docs.github.com/en/actions/using-workflows/about-workflows) to get more backgrounds on this.

## Example

Here is an example of a [workflow file](@) that can be used
to compile and deploy the static website of an [MVE](@)
that uses GitHub Pages (or Jekyll) for its deployment:

~~~ yaml
# Simple workflow for deploying static content to GitHub Pages
name: Deploy static content to Pages

on:
  push:
    branches: ["main"]
  pull_request:
    branches: ["main"]

permissions:
  contents: write # this is needed for step "Commit MRGs to repository" to work
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
      with:
        fetch-depth: 0

# Setting up Node, as this is needed to install the TEv2 tools
# You should copy this part to your workflow-file
#   unless it already has Node.js installed.
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: 20

# <TEv2 specific steps start here>
# You should copy everything up to the comment that says the TEv2 specific steps ends
    # TEv2 Tool installation
    - name: Install terminology tools globally
      run: npm install -g @tno-terminology-design/trrt @tno-terminology-design/hrgt @tno-terminology-design/mrgt @tno-terminology-design/mrg-import

    # TEv2 Tool usage
    - name: Run terminology tools
      run: |
        cd docs
        mrg-import -c tev2-config.yaml
        mrgt       -c tev2-config.yaml
        hrgt -f    -c tev2-config.yaml
        trrt -f    -c tev2-config.yaml

    # Commit generated MRGs to repo, so other projects can use 
    # (import) these generated MRGs. 
    - name: Commit MRGs to repository
      uses: stefanzweifel/git-auto-commit-action@v5
      with:
        commit_message: Update MRGs
        file_pattern: 'docs/glossaries/mrg.mve*.yaml'
# <TEv2 specific steps end here>

# The stuff below is what MkDocs needs to generate the static site
    - name: Set up Python
      uses: actions/setup-python@v5
      with:
        python-version: '3.x'

    - name: Install MkDocs and extensions
      run: |
        python -m pip install --upgrade pip
        pip install mkdocs mkdocs-material  # Optionally add any specific MkDocs plugins you require

    - name: Build the MkDocs site
      run: mkdocs build
      working-directory: ${{github.workspace}}

    - name: Setup Pages
      uses: actions/configure-pages@v5

    - name: Upload artifact
      uses: actions/upload-pages-artifact@v3
      with:
        path: './site'

    - name: Deploy to GitHub Pages
      id: deployment
      uses: actions/deploy-pages@v4
~~~
