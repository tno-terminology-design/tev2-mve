---
# Front matter for TEv2 Curated Texts that is required
term: spec-up-xref
# Spec-up section
spec-up-term: "xref"
spec-up-aliases: [ "xrefs", "external reference", "external references" ]
spec-up-definition: "a construct of the form `[[xref: {title} {term}]]`, where `{title}` is a tag that identifies the source of the definition of `{term}`."
# TEv2 specific frontmatter (can be discarded if you only use Spec-Up)
formPhrases: [ "External Reference{ss}", "XRef{ss}", "spec-up XRef{ss}" ]
glossaryTerm: "External Reference (Spec-Up style)"
glossaryAbbr: "XRef"
glossaryText: "a construct of the form `[[xref: {title} {term}]]`, where `{title}` is a tag that identifies the source of the definition of `{term}`."
glossaryNotes:
- "The `{title}` tags are defined [to be described, link to actual specs thereof]."
- "When an XRef is processed by a [TEv2 tool](@tev2), `{title}` is treated as the equivalent of a [scopetag](@tev2) and/or the default [terminology](@tev2) in the associated [scope](@tev2)."
---

# Spec-Up XRefs

A [[ref: XRef]] (Spec-Up style) is a construct of the form `[[xref: {title} {term}]]`, where `{title}` is a tag that identifies the source of the [[ref: definition]] that defines `{term}`. 

In a [TEv2](@tev2) context, `{title}` is considered a [scopetag](@tev2) that is defined in the `scopes` section of the [SAF](@tev2), which specifies the URL of at which the [scopedir](@tev2) is located. When it is used as part of an [[ref: XRef]], the `{term}` in that [[ref: XRef]] will be looked up in the default [terminology](@tev2) of that [scope]@tev2).
