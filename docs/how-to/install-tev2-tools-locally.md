---
Title: Install TEv2 Locally
---

# Installing TEv2 Tools Locally

You only need to do this if you intend to exercise the tools 
in your local clone of the repo. 
You should then first make sure you can run `npm`.
You do this by installing `Node.js`.
Help for all this is available, e.g.:

1. [`Node.js` Downloads](https://nodejs.org/en/download/)
   This page provides the installation files for Node.js on various operating systems including Windows, macOS, and Linux. It offers both LTS (Long Term Support) and Current versions.

2. [Installing `Node.js` via package manager](https://nodejs.org/en/download/package-manager/)
   This section of the official Node.js website offers detailed instructions on how to install Node.js using package managers for a variety of platforms, including Ubuntu, Debian, macOS, Windows, and others.

3. [Getting started with `npm`](https://docs.npmjs.com/getting-started)
   This is the official guide from npm, which includes a section on installing Node.js (because npm comes bundled with Node.js). It’s particularly useful for understanding how npm works alongside Node.js.

The [TEv2 tools] you need are avaiable as NPM packages. We use the [MRG import](@tev2), [MRGT](@tev2), [HRGT](@tev2) and [TRRT](@tev2), which can be installed by executing:

```
npm install -g @tno-terminology-design/mrg-import
npm install -g @tno-terminology-design/mrgt
npm install -g @tno-terminology-design/hrgt
npm install -g @tno-terminology-design/trrt
```

You can verify that they are installed correctly by 
making the `docs` directory your current directory,
and then run the following commands

```
mrg-import --version
mrgt --version
hrgt --version
trrt --version
```

all of which should return a version number. 
In case of trouble, you may consult

- [npm Troubleshooting Guide](https://docs.npmjs.com/troubleshooting)
  This is the official npm troubleshooting guide which covers common problems including installation issues on different operating systems.

- [Stack Overflow](https://stackoverflow.com/questions/tagged/npm)
  Stack Overflow has a vast number of questions and answers on npm issues across all platforms. Users can search for their specific issues or ask new questions.

- [Issues on the Node.js GitHub repo](https://github.com/nodejs/node/issues)
  The Node.js GitHub repository can be useful for browsing or reporting issues directly related to Node.js, which may indirectly solve npm issues.

- [npm Community](https://npm.community/)
  The npm Community forum is a place to discuss problems and share solutions with other npm users across different environments.
