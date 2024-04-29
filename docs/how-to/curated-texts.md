---
title: Curated Texts
---

# Managing Terms and Definitions

The [terms](@tev2) and [definitions](@tev2) that you use,
as well as any related documentation,
go in a single file - a so-called [curated text](@tev2) file.

In this [MVE](@), all such files live in the
[`terms` subdirectory](https://github.com/tno-terminology-design/tev2-mve/tree/main/docs/terms)
of the repo. That's where you would add and modify files
that describe your terms.

These files are normal markdown files, with a header (frontmatter)
and a body (regular markdown).

- a [body](@tev2) of such a markdown file contains any markdown 
  that the static site generator you use can process.

## Header (Frontmatter)

The minimum [header](@tev2) consists of everything that
your static site generator (MkDocs/Jekyll) uses, and 
the minimum stuff needed by [TEv2 tools](@tev2).
We refer to the [TEv2 header documentation](header#header@tev2)
for additional information.

The minimal amount of front matter is given in the following example:

```yaml
# Front matter for the static site generator
title: MVE
# Front matter for TEv2 Curated Texts
term: mve
glossaryTerm: "Minimal Viable Example"
glossaryText: "a GitHub repo, the contents of which is documentation that is published as a static website using GitHub Pages or Jekyll, and that includes the minimal stuff for using the [TEv2 tools](@tev2) and demonstrating its results."
formPhrases: [ "minimal viable example{ss}", "minumum viable example{ss}", "mve{ss}" ]
```
Let's consider the section `Front matter for TEv2 Curated Texts`

| field | description |
| ----- | ----------- |
| term  | this is a word that is used internally to refer to this file. Within the context of this [MVE](@), it MUST be equal to the filename (without the `.md` extension. This has to do with the way in which MkDocs/Jekyll do the routing to these files. |
| glossaryTerm | This is a word or phrase that is used as the title of the glossary entry. |
| glossaryText | This is the text that appears as the description of the term in the glossary. It is also used (in the current configuration of the [MVE](@)) as the text in a  popup when this term is referred to (in a [TermRef](@tev2)). |
| [formPhrases](@tev2) | This is a list of words or phrases that typically are not the term itself, but should be treated as such when used in a [TermRef](@tev2).|

## Body

The [body](@tev2) contains any markdown that your static site generator
can process.
