---
# Front matter for TEv2 Curated Texts
term: spec-up-definition
glossaryTerm: "Definition (Spec-Up style)"
glossaryText: "a construct of the form `[[def: {term}, {alias1}, {alias2}, ... ]] ~ {definition}`, which specifies the mapping between the term `{term}` and a description of the term's meaning (provided by `{definition}`."
glossaryNotes:
- "`{alias1}, {alias2}, ...` is optional syntax that specifies aliases (synomyms) for `{term}`."
- "In [TEv2](@tev2), `{term}` and its aliases would be specified as [form phrases](@tev2)."
- "A recent addition is the use of so-called [[ref: XRefs]], which allows definitions to be used across diffrent files and projects."
formPhrases: [ "definition{ss}", "spec-up definition{ss}" ]
---

# Definition (Spec-Up style)

A [[ref: Spec-Up Definition]] is a construct of the form `[[def: {term}, {term alias}, ... ]] ~ {definition}`, where 

- `{definition}` is a descrition of the meaning of term `{term}`, and
- `{term alias}, ...` is a (comma separated) list of words or phrases that are considered to have the same meaning as `{term}`. They are not necessarily synonyms, but are typically what [TEv2](@tev2) would call [form phrases](@tev2).

## How Spec-Up uses Definitions and Term References

In [Spec-Up's](https://identity.foundation/spec-up/) way of thinking, a specification file contains: 

1. a [definition list](https://github.com/decentralized-identity/spec-up/blob/master/single-file-test/spec.md#definition-lists), which contains all [[ref: definitions]] used within the file. It typically sits somewhere at the beginning of the specification file.
2. [[ref: term references]], whose `{term}` part is one of the `{term}`s (or aliases) in a [[ref: definition]].

An example of this is given in the [single-file-test/spec.md file](https://github.com/decentralized-identity/spec-up/blob/master/single-file-test/spec.md#definition-lists) in the [Spec-Up Github repo](https://github.com/decentralized-identity/spec-up/tree/master/).

## TEv2 does NOT use Spec-Up Definitions

The reason for this is that such [[ref: definitions]] only provide the very minimal things that, in the [TEv2](@tev2) vision, people would want to do with them.

The most obvious features that TEv2 provides that are not facilitated by [[ref: Spec-Up definitions]] are:

- the generation of a wide variety of (human readable) glossaries from the [[ref: definitions]];
- generating (persistent) links to the documentation pages of terms;
- extending terminology-features without changing the underlying (programming) code.

## Notes

Terms can still be defined and curated in various ways, but that does require that the curated texts that define terms (regardless of they are [[ref: spec-up definitions]] or specified in another way, e.g., as Wiki pages), are somehow converted in either

- a [TEv2-style machine readable glossary](mrg@tev2), so that [[ref: term references]] can be resolved using the [TEv2 TRRT tool](trrt@tev2), regardless of they are [[ref: Spec-Up term references]] or [TEv2 TermRefs](term-ref@tev2), or
- a set of [TEv2-style curated texts](curated-text@tev2), which can be processed by the [TEv2 MRGT tool](mrgt@tev2) to create such a [TEv2-style machine readable glossary](mrg@tev2).


