---
title: Resolving TermRefs
---

# How To Resolve TermRefs

Resolving [TermRefs](@tev2) consists of finding them in the various files,
and replacing them with a so-called [renderable ref](@tev2), i.e., 
a series of characters that, when rendered, have particular characteristics.
Typically, such characteristcs are that they stand out from the adjacent texts,
that they can be clicked on to navigate to the page where they are documented,
and that they have a popup text that specifies their definitions.

What a particular [renderable ref](@tev2) would actually look like can be 
customized by creating and using so-called [converters](@tev2).

~~~ bash
# use this command in a GitHub Action for actual deployment
trrt -c "tev2-config.yaml -f" 

# use this command for local testing
trrt -c "tev2-config.yaml" -o "test-output" 
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
  is documented in the [TRRT documentation](trrt#calling-the-tool@tev2).

3. **The `-f` flag** is used in the deployment case, to prevent the tool
   from testing whether it is overwriting the files that it is processing
   with the results thereof.

4. **The `-o "test-output"`** argument is used in the local (testing) case
   to make sure that the results of processing are put at a location
   (i.e.: in `/docs/testoutput`) different from where the sources are kept
   so that you do not inadvertently overwrite these s

5. **Additional documentation on the TRRT** can be found in its 
   [specifications](trrt@tev2).
