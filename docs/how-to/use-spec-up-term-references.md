---
title: Using Spec-Up Term References
---

# Spec-Up Term References Integration

[TEv2](@tev2) allows customization of the syntax that authors use for [TermRefs](@tev2). In this page, we show what it takes to use the syntax as [defined by Spec-Up](https://identity.foundation/spec-up/), which is a tool that aims to facilitate the writing of technical specifications aimed at standards bodies or industry groups.

##  Background: Spec-Up Syntax for Term References

The [Spec-Up syntax for (regular) term references](https://github.com/decentralized-identity/spec-up/blob/master/single-file-test/spec.md#term-references) consists of [[ref: Spec-Up definitions]] (located in a so-called [definition list](https://github.com/decentralized-identity/spec-up/blob/master/single-file-test/spec.md#definition-lists)), and [[ref: Spec-Up term references]], that can be used to refer to such definitions.

Recently, Spec-Up introduced a [syntax for external term references](https://github.com/decentralized-identity/spec-up/blob/master/single-file-test/spec.md#external-term-references), that uses new feature called [[ref: XRefs]]. This feature allows authors to refer to terms that are defined in the text they are writing themselves, but in a text that is curated elsewhere.

## Requirements for using Spec-Up syntax by TEv2 tools

In this [MVE](@), we only support the Spec-Up syntax for [[ref: term references]] and [[ref: XRefs]]. This means that

- we do not use [[ref: Spec-Up definitions]] or [definition lists](https://github.com/decentralized-identity/spec-up/blob/master/single-file-test/spec.md#definition-lists)).
- we use [TEv2 machine readable glossaries](mrg@tev2) to find the definitions of terms that are being referred to. 
- [[ref: Spec-Up term references]] are resolved using the default [terminology](@tev2) of the [current scope](@tev2). 
- [[ref: Spec-Up XRefs]] are resolved in a similar fashion, using the `{title}` part as a [scopetag](@tev2).

##  The TRRT Interpreter for Spec-Up Term References

In order to use Spec-Up [[ref: term references]] and [[ref: XRefs]], we need to write a [TEv2 interpreter](interpreter@tev2) that recognizes them. This can be done by mapping the `{term}` and `{title}` fields of the Spec-Up references to the [named capturing groups](@tev2) specified in the [interpreter profile of the TRRT](trrt#interpreter-profile@tev2), as follows:

| Spec-Up syntax | TEv2 equivalent | Comments |
| -------------- | --------------- | -------- |
| `[[ref: {term}]]` | `[{term}](@)` | A Spec-Up `{term}` maps onto the `showtext` capturing group of a [TEv2 TermRef](term-ref@tev2). |
| `[[xref: {title}, {term}]]` | `[{term}](@{title})` | A Spec-Up `{title}` maps onto the `scopetag` captruing group of a [TEv2 TermRef](term-ref@tev2). |

This leads to the [following regex](https://www.debuggex.com/r/I1gqkMGPKMs9dfeE):

```regex 
(?:(?<=[^`])|^)\[\[(?:xref:\s*(?<scopetag>[a-z0-9_-]+),|ref:)\s*(?<showtext>[^\n\],]+)\]\]
```

## Notes:

When applying the regex in a YAML file (e.g. a [TEv2 configuration file](config-file@tev2)), the escape character `\` must be escaped. So the `trrt` section would read as follows:

```yaml
trrt:
  interpreter: "(?:(?<=[^`])|^)\\[\\[(?:xref:\\s*(?<scopetag>[a-z0-9_-]+),|ref:)\\s*(?<showtext>[^\n\\],]+)\\]\\]"
  converter: html-hovertext-link # style in which TermRefs are to be rendered - change as you like
  input:                         # glob pattern for files to be processed - adjust as necessary
    - "**/*.md"
```

If a [[ref: Spec-Up term reference]] or a [[ref: Spec-Up XRef]] are to be rendered in a different way, that means that the [TRRT](@tev2) must be called using another, appropriate [converter](@tev2) (either a [predefined one](trrt#predefined-converters@tev2), or a [customized one](trrt#converter-customization@tev2)).

The following text (below the horizontal line) is a literal quote from the Spec-Up single-file-test spec.md file, showing that [[ref: Spec Up definitions]] are untouched, whereas [[ref: Spec-Up term references]] are converted as we would expect them to.

Note that the [[ref: term references]] for `Term 1`, `Term 2` and `Term 3` will actually work. That is NOT because the [[ref: definitions]] are processed, but because they are defined as [curated texts](@tev2), and therefor they end up in the [TEv2 MRG](mrg@tev2) that is used to dereference them.

-----

### Definition Lists

Many specs may want to include a section for terminology references, and Definition Lists are a great way to do that. Here's how to leverage Spec-Up's automatic term reference features via Definition List markup:

<pre>
[[def: Term 1, Term One]]:
~ This is the first term we will define.

[[def: Term 2, Term Two]]:
~ This is the second term, but not the last.

[[def: Term 3, Term Three]]:
~ This is the last term, because you know what they say: third term's the charm!
</pre>

[[def: Term 1, Term One]]:
~ This is the first term we will define.

[[def: Term 2, Term Two]]:
~ This is the second term, but not the last.

[[def: Term 3, Term Three]]:
~ This is the last term, because you know what they say: third term's the charm!

Now let's refer to some of the terms defined above to show how the auto-linking of terms works: [[ref: Term 1]], [[ref: Term Two]], [[ref: Term 3]]. Additionally, as long as you define your terms using Definition Lists (as seen in the markdown above), you will be able to hover any reference to a term to see a tooltip with its definition.