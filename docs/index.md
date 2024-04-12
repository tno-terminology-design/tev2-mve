---
id: index
---

# Minimum Viable Example - Explainer

This is an example of a documentation file. In this case, it explains how the
[TEv2 tools](@tev2) can be used to process the files in this Minimal Viable Example (MVE).

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

