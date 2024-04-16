---
title: Import MRGs
---

# How To Import MRGs from others

This step is to be taken only if your documentation uses [terms](@tev2) 
that are defined elswhere (e.g., in another repo). In other cases, 
it can safely be skipped.

Importing [MRGs](@tev2) consists of finding the (so-called) [scopes](@tev2)
(and associated [scopedirs](@tev2)) from where the [MRGs](@tev2) need to be
imported, and subsequently importing all [MRGs](@tev2) that have been 
generated within that [scope](@tev2).

The result is that the [MRGs](@tev2) of such [scopes](@tev2) are retrieved
and put in the same directory where [MRGs](@tev2) are generated.
For our situation, that is `/docs/mrgs`.

As our [MVE](@) extensively uses [terms](@tev2) defined in the [scope](@tev2)
that we call `tev2` (which is located in the
[TEv2 Specifications repo](https://github.com/tno-terminology-design/tev2-specifications)),
we need to import its [MRGs].

~~~ bash
# use this command in a GitHub Action or for local testing:
mrg-import -c "tev2-config.yaml"
~~~

<div style="background-color: #ffffcc; padding: 15px; margin-bottom: 20px; border-left: 6px solid #ffeb3b;">
  <strong>Note:</strong> Make sure you execute this command 
  in the directory that contains the file `saf.yaml`.
  In our case, that would be `/docs`.
</div>

## Notes:

1. **We can use multiple configuration files**. 
  Each configuration file has a particular purpose.
  Using those makes it easer to generate stuff in different contexts,
  such as the local (testing) context of the GitHub (deployment) context.

2. **You can override the parameters in the [configuration file](@tev2)**
  by providing them yourself on the command-line. The list of parameters
  is documented in the [HRGT documentation](hrgt#calling-the-tool@tev2).

3. **The directory in which the MRGs are created** is the one as specified
   in the [SAF](@tev2). In our case, this is `/docs/mrgs`.
   This directory will be created if it doesn't yet exist.
   If this directory already contains an [MRG](@tev2) with the same name(s),
   they will be overwritten with the imported contents.

4. **Additional documentation on the MRG Importer** can be found in its 
   [specifications](mrg-import@tev2).