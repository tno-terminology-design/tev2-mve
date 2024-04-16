---
title: Generate Glossaries
---

# How To Generate (Human Readable) Glossaries

The generation of [human readable glossaries](@tev2) consists of
finding [MRGRef](@tev2) markers in a file, and
replacing them with a chunk of characters that,
when rendered, typically list the definitions of the [terms](@tev2)
as specified in the one particular [machine readable glossary](@tev2)
that is specified in the [MRGRef](@tev2).

What a particular [entry in the glossary](hrg-entry@tev2) would actually look
like can be customized by creating and using so-called [converters](@tev2).

~~~ bash
# use this command in a GitHub Action for actual deployment
hrgt -c "tev2-config.yaml" -f

# use this command for local testing
hrgt -c "tev2-config.yaml" -o "test-output" 
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

3. **The `-f` flag** is used in the deployment case, to prevent the tool
   from testing whether it is overwriting the files that it is processing
   with the results thereof.

4. **The `-o "test-output"`** argument is used in the local (testing) case
   to make sure that the results of processing are put at a location
   (i.e.: in `/docs/testoutput`) different from where the sources are kept
   so that you do not inadvertently overwrite these sources.

5. **Additional documentation on the HRGT** can be found in its 
   [specifications](hrgt@tev2).