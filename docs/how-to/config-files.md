---
title: Config Files
---

# How To Create Config Files

A [TEv2 Configuration File](@tev2) is a ([YAML](https://yaml.org/spec/1.2.2/)) file 
that provides the various [TEv2 tools](@tev2) with a set of predefined parameters
that configure their runtime behavior. 

Such parameters may specify, for example, which files to process (input files),
where output files are to be put, whether overwriting input files is permitted,
and so on. An overview of all such parameters is given by the [documentation on
such configuration files](config-files@tev2).

While [configuration files](@tev2) can be located anywhere within the [scopedir](@tev2),
the preferred (i.e., most practical) location is the [scopedir](@tev2) itself.

Here is an example of the [TEv2 configuration file](@tev2) that is used for this [MVE](@).
[This file](/docs/tev2-config.yaml) is located in the [scopedir](@tev2).

~~~ yaml
# TEv2 configuration file (for the MVE context)

## General
scopedir: .          # URL of (or relative path to) the scope directory (where the SAF is located)
onNotExist: warn     # Action in case something doesn't exist
output:   .          # (root) directory for output files to be written to

## Machine Readable Glossary Tool
mrgt:
  vsntag:            # versiontag of MRG to generate. Default: all MRGs

## Human Readable Glossary Tool
hrgt:
  converter: markdown-section-2  # style in which glossary entries are to be rendered
  input:                         # glob pattern for files to be processed
    - "*.md"

## Term Reference Resolution Tool
trrt:
  converter: html-hovertext-link # style in which TermRefs are to be rendered
  input:                         # glob pattern for files to be processed
    - "**/*.md"
~~~

All [tools](@tev2) use the fields in the beginning of the file, 
i.e.: `scopedir`, `onNotExist` and `output`.
Individual tools also use the fields in the section that is identified with
their name. 

For example,

- the [TRRT](@tev2) tool also takes the fields `converter` and `input`
  from the section `trrt`. So, the [TRRT](@tev2) will use `html-hovertext-link`
  as the value for its `converter` argument. Also, it will process all files
  within the [scopedir](@tev2) that have the `.md` extension.
- the [HRGT](@tev2) tool will take its `converter` and `input` arguments
- from the section `hrgt`. So, the [HRGT](@tev2) will use `markdown-section-2`
  as the value for its `converter` argument. And it will only process files that
  have the extension `.md` and that are located in the [scopedir](@tev2) itself.

# Notes

1. **Converters determine what the output of a tool looks like**.
   Each tool that uses [converters](@tev2) comes with a set of predefined ones.
   So there are [TRRT converters](trrt#predefined-converters@tev2) and also
   [HRGT converters](hrgt#predefined-converters). 
   [Converters](@tev2) can be customized, both [for the TRRT](trrt#converter-customization)
   and [for the HRGT](hrgt#converter-customization).