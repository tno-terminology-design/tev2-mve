---
Title: Add TEv2 to GitHub Actions
---

# How To Add TEv2 Tools to the Actions Script

You only need to do this if you intend to use the tools in a GitHub workflow.

All you need to do is add some texts to the workflow file 
that is used to generate the static website. This file is located
in the `/.github/workflows` directory of your repo.

In this MVE, we also have such a file. 
It is called [`deploy-docs.yml`](https://github.com/tno-terminology-design/tev2-mve/blob/main/.github/workflows/deploy-docs.yml).
You can use this as an example.

You can also see there the particular parts that you must have in your workflow file

This file is a standard/minimal workflow for creating a GitHub Pages website,
where we have inserted the following action-steps:

~~~
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

~~~
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







The [TEv2 tools] you need are avaiable as NPM packages. We use the [MRG import](@tev2), [MRGT](@tev2), [HRGT](@tev2) and [TRRT](@tev2), which can be installed by executing:

~~~
npm install -g @tno-terminology-design/mrg-import
npm install -g @tno-terminology-design/mrgt
npm install -g @tno-terminology-design/hrgt
npm install -g @tno-terminology-design/trrt
~~~

You can verify that they are installed correctly by 
making the `docs` directory your current directory,
and then run the following commands

~~~
mrg-import --version
mrgt --version
hrgt --version
trrt --version
~~~

all of which should return a version number. 
In case of trouble, you may consult

- [npm Troubleshooting Guide](https://docs.npmjs.com/troubleshooting)
  This is the official npm troubleshooting guide which covers common problems including installation issues on different operating systems.

- [Stack Overflow](https://stackoverflow.com/questions/tagged/npm)
  Stack Overflow has a vast number of questions and answers on npm issues across all platforms. Users can search for their specific issues or ask new questions.

- [Issues on the Node.js GitHub repo](https://github.com/nodejs/node/issues)
  The Node.js GitHub repository can be useful for browsing or reporting issues directly related to Node.js, which may indirectly solve npm issues.

- [npm Community](https://npm.community/)
  The npm Community forum is a place to discuss problems and share solutions with other npm users across different environments.

## File/Directory Structure

The `docs` directory is the root directory in which TEv2 works (the reason for
this is that it contains the [Scope Administration File](saf@tev2) (`saf.yaml`)
for the MVE scope). This directory is constructed as follows:

~~~
├── mrgs
│   ├── mrg.mve.terms.yaml
│   └── mrg.mve.yaml
├── terms
│   ├── term-1.md
│   └── term-2.md
├── outputs
│   └── readme.md
├── index.md
├── mve-glossary.md
├── saf.yaml
└── tev2-configs.yaml
~~~

- `mrgs` (directory) contains [machine readable glossaries](@tev2). They are either
imported (by the [mrg-import](@tev2) tool), or generated (by the [mrgt](@tev2) tool). 
The [glossaries](@tev2) generated within this scope are `mrg.mve.terms.yaml` 
(the [mrg](@tev2) of [terms](@tev2) that are defined within this scope) and
`mrg.mve.yaml` (the [mrg](@tev2) that holds the default [terminology](@tev2) 
of this [scope](@tev2)). Other [mrgs](@tev2) that might exist would be imported.

- `terms` (directory) contains files with [curated texts](@tev2), i.e., 
markdown texts that document the terminology defined within this [scope](@tev2). 
These are `term-1.md`, which documents [first term](@) and `term-2.md`, 
which documents [second term](@).

- `index.md` file (this file).

- `mve-glossary.md` is a markdown file that contains a [marker](mrg-ref@tev2)
that the [hrgt tool](hrgt@tev2) converts into a [human readable glossary](@tev2)
of the [terms](@tev2) that are defined in this [scope](@tev2).

- `saf.yaml` is the [scope administration file](saf@tev2).

- `tev2-configs.yaml` is a [TEv2 configuration file](@tev2) that holds 
configurations for the [TEv2 tools](@tev2).

## Working with TEv2 tools

The purpose of this site is to provide you with an initial setup that enables you to run the tools by yourselves, so that you can see what they do.

**We assume that all commands are run from the directory that contains the file `saf.yaml`**

You can do this as follows:

### Step 0: Make sure the tools become available

You can do this by installing npm (the node packet manager) on your machine, and subsequently making all tools available, as follows:

~~~ cmd
npm install -g @tno-terminology-design/mrg-import
npm install -g @tno-terminology-design/mrgt
npm install -g @tno-terminology-design/hrgt
npm install -g @tno-terminology-design/trrt
~~~

You can verify they are available by

1. going to the directory that contains `saf.yaml`, and then
2. executing the following command(s) from within that directory:

~~~ cmd
<toolname> --version
~~~

(where `<toolname>` is `mrg-import`, `mrgt`, `hrgt`, or `trrt`).

### Step 1: importing MRGs

The first step consists of ensuring that [terminologies](@tev2) that are
defined elsewhere, and that you rely on to be available (e.g., as you refer
to its [terms](@tev2)), are actually available.

You can skip this step if there are no such [terminologies](@tev2).

As this file makes extensive use of the [terms](@tev2) defined by TEv2,
we need to import its (default) [MRG](@tev2). You can do that by executing
the following command from within the directory that contains `saf.yaml`

~~~ cmd
mrg-import -c "tev2-configs.yaml"
~~~

This will add various files in the `mrgs` directory, called `mrg.tev2*.yaml`.
You can discard all, except `mrg.tev2.yaml`, but you can also leave them
where they are, as they are not in the way.

### Step 2: generating Machine Readable Glossaries (MRGs)

In the second step, we will generate [machine readable glossaries](@tev2)
for the [terminologies](@tev2) that are defined in the [saf](@tev2).
You can do that by executing the following command:

~~~ cmd
mrgt -c "tev2-configs.yaml"
~~~

This adds another two [MRGs](@tev2) to the `mrgs` directory:

- `mrg.mve.terms.yaml` holds the [MRG](@tev2) that contains all [terms](@tev2)
that are defined in our MVE-[scope](@tev2).
- `mrg.mve.yaml` holds the [MRG](@tev2) that contains all [terms](@tev2)
in the default [terminology](@tev2) of our MVE-[scope](@tev2).

It so happens that these files have the same contents.

### Step 3: generating Human Readable Glossaries (HRGs)

Next, we can generate the [human readable glossaries](@tev2).

You can do that by executing the following command:

~~~ cmd
hrgt -c "tev2-configs.yaml"
~~~

