# TEv2 MVE for Github Pages

This repo contains an example of what 
[documentation could look like](https://tno-terminology-design.github.io/tev2-mve)
when TEv2 terminology tools are used in conjunction with GitHub Pages.

The repo started out with contents that can be processed according
to the specification of Github Pages. It is assumed that the documentation
for GH-Pages resides in the `/docs` directory (which is typical).

## Adding TEv2 to the existing GH-Pages sources 

First, some files are created and added in the `/docs` directory:

- `saf.yaml` (a so-called Scope Administration File)
- `glossary.md` (a markdown file in which a (human readable) glossary is generated)
- `tev2-config.yaml` (a configuration file that TEv2 tools use to find parameters)

Then, the following directories are added:

- `mrgs` (a directory in which (machine readable) glossaries are generated)
- `terms` (a directory in which so-called 'curated texts' are placed)

Next, any terms in the documentation are converted into so-called 'TermRefs'

Finally, for every term that needs to be defined, a so-called 'curated file'
is created in the `/docs/terms` directory.

## Modifying the GitHub Workflow

In this repo, the file `/.github/workflows/deploy-docs.yml` specifies how
the site is to be generated. In this file, a section has been added 
(and clearly marked so you can easily identify it)
that executse the relevant TEv2 tools.

A more elaborate description of all this, and instructions of how you can test this
using the TEv2 tools is given in [`/docs/doc-1.md`](/docs/doc-1.md).
