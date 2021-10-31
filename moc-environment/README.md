# MOC software environment

This document contains all notes and other findings we made during getting
familiar with the MOC software environment. This should be mostly how to set
up the environment, any particular problems we found (and how to fix them),
questions and answers and other takeaways.

---

## 1. Setting up the environment

The MOC environment is split into multiple repositories, each achieving a
different goal. The repositories are:
- [vrgp-spinache](https://github.com/aboamare/vrgp-spinache): the API for the MOC. This is the main point of the MOC test
  implementation.
- [vrgp-spinace-lib](https://github.com/aboamare/vrgp-spinache-lib): A library used by `vrgp-spinache`, contains some
  necessary libraries.
- [vrgp-doryphore](https://github.com/aboamare/vrgp-doryphore): A web interface for the vrgp-spinache MOC.
- [vrgp-teapilot](https://github.com/aboamare/vrgp-teapilot): A phone test implementation of the vessel side of the VRGP.

`vrgp-spinache` is based on the [HAPI framework](https://hapi.dev/). A short tutorial to get
started with HAPI can be found [here](https://hapi.dev/tutorials?lang=en_US).

Both `vrgp-spinache` and `vrgp-spinache-lib` have to be installed in order to
get the server up and running. Additionally, `vrgp-doryphore` can be installed
for a web interface.

After downloading them locally (either using `git clone` or manually downloading
and extracting the zip archive), the dependencies can be installed by running
`npm install` in all the repositories. The server can be started by running
`node server.js` in `vrgp-spinache`.

---

## 2. Problems with the environment/code

---

## 3. Other questions and takeaways
