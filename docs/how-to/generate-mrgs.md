---
title: Generate MRGs
---

# How To Generate (Machine Readable) Glossaries

The generation of [machine readable glossaries (MRGs)](mrg@tev2) consists of
finding the specifications of the [terminologies](@tev2) for which such 
[MRGs](@tev2) are to be created, and then generate them.

This results in the generated [MRGs](@tev2) to become available in the
`mrgs`-directory (as specified by the [SAF](@tev2)).
In our case, that would be 

- `mrg.mve.mve-terms.yaml`, which holds the [MRG](@tev2) that contains all [terms](@tev2)
that are defined in our [MVE](@), and
- `mrg.mve.yaml`, which holds the [MRG](@tev2) that contains all [terms](@tev2)
in the default [terminology](@tev2) of our MVE-[scope](@tev2).

It so happens that these files have the same contents, but that need not always be the case.

```bash
# use this command in a GitHub Action or for local testing:
mrgt -c "tev2-config.yaml"
```

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
   they will be overwritten with the newly generated contents.

4. **Additional documentation on the MRGT** can be found in its 
   [specifications](mrgt@tev2).