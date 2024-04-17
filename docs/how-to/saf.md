
# How To Create the SAF (Scope Administration File)

A [Scope Administration File (SAF)](saf@tev2) is a
([YAML](https://yaml.org/spec/1.2.2/)) file 
that provides a centralized record of the resources in the documentation context
that are needed by the various [TEv2 tools](@tev2).

The directory that contains the [SAF](@tev2) of such a context 
(which in TEv2-parlance is called a [scope](@tev2)) 
is called the [scopedir](@tev2) (of that [scope](@tev2)).
It is the root relative to which all TEv2-related paths are specified.

Here is an example of the [SAF](@tev2) for this [MVE](@).
For starters, you can simply copy this text, and adjust the contents of the various fields. When you do so, please be very accurate with the values that you provide. 

~~~ yaml
scope:
  # Identifier that we use as a name for this scope
  scopetag: mve
  # URL of the scope-directory within the repo
  scopedir: https://github.com/tno-terminology-design/tev2-mve/tree/master/docs
  # path to directory where curated files are located. 
  # Full URL is `scopedir`/`curatedir`
  curatedir: terms
  # path to directory where all MRGs are located. 
  # Full URL is `scopedir`/`glossarydir`
  glossarydir: mrgs
  # vsntag that identifies the default terminology. 
  # Its MRG is located at `scopedir`/`glossarydir`/mrg.mve.yaml
  defaultvsn: mve-terms
  # Base URL for creating links to rendered versions of Curated Texts.
  # It should also serve as the home page of the terminology.
  website: https://tno-terminology-design.github.io/tev2-mve
  # Path to the directory where Curated Texts are rendered. 
  # What `curatedir` is for Curated Texts, `navpath` is for 
  # the rendered versions of Curated Texts.
  navpath: /terms
  # Name of a field that can be found in the front matter of a 
  # curated text file, that will be used to generate links that
  # are routable by the static site generator that is being used.
  # If not specified, the filename of the body file will be used.
  navid: term
#
# The `scopes` section contains a mapping between scopetags 
# that are used within the scope, and the associated scopedirs.
# This enables tools to find the SAF of these scopes,
# and from there all other directories, files etc. that live
# within them, e.g. to use/import their data.
#
scopes:
- scopetag: tev2 # name we use to identify the scope found at
  # the URL of the scope-directory:
  scopedir: https://github.com/tno-terminology-design/tev2-specifications/tree/master/docs
#
# The `versions` section specifies the terminologies 
# that are actively maintained by the curators of this scope.
# For each (version of such a) terminology, termselection instructions
# must be provided that specify which terms are to be included.
# One of these section must have a `vsntag` that matches 
# the value of `defaultvsn` in the `scope`-section.
#
versions:
  # this version contains all terms that are curated within this scope
- vsntag: mve-terms 
  termselection:
  # include all terms that are curated within the current scope
  - "*"
~~~

There is a more elaborate explanation of the [SAF](@tev2) in the [TEv2 specifications](saf@tev2).
