---
Title: Add TEv2 to GitHub Actions
---

# How To Add TEv2 Tools to the Actions Script

You only need to do this if you intend to use the tools in a GitHub workflow.

All you need to do is add some texts to the [workflow file](@) 
that is used to generate the static website. This file is located
in the `/.github/workflows` directory of your repo.

In this [MVE](@), we also have such a file. It is called
[`deploy-docs.yml`](https://github.com/tno-terminology-design/tev2-mve/blob/main/.github/workflows/deploy-docs.yml).
You can use this as an example.

This file is a standard/minimal workflow for creating a GitHub Pages website,
where we have inserted the following action-steps:

~~~ yaml
    # Setting up Node, as this is needed to install the TEv2 tools
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: 20
~~~

In many cases, `Node.js` also needs to be set up for static site generator features.
In such cases, something similar to the above would already exist, 
and it is not necessary to duplicate that then.

The TEv2-specific part that (always) needs to be added is as follows:

~~~ yaml
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

    # Commit generated MRGs to repo, so other projects can use (import) them
    - name: Commit MRGs to repository
      uses: stefanzweifel/git-auto-commit-action@v5
      with:
        commit_message: Update MRGs
        file_pattern: 'docs/glossaries/mrg.mve*.yaml'
~~~

That's all.

## Notes