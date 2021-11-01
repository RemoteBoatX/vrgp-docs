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

### vrgp-spinache

`vrgp-spinache` is based on the [HAPI framework](https://hapi.dev/). A short tutorial to get
started with HAPI can be found [here](https://hapi.dev/tutorials?lang=en_US).

Both `vrgp-spinache` and `vrgp-spinache-lib` have to be installed in order to
get the server up and running. Additionally, `vrgp-doryphore` can be installed
for a web interface.

After downloading them locally (either using `git clone` or manually downloading
and extracting the zip archive), the dependencies can be installed by running
`npm install` in all the repositories. The server can be started by running
`node server.js` in `vrgp-spinache`.

**NOTE:** To be able to run this with the web interface (i.e. `vrgp-doryphore`),
you need to link to that project. This basically means locating the Doryphore
directory, and doing (in Linux) `ln -s </absolute/path/to/doryphore>/dist
<path/to/spinache>/apps/operator`. This makes it so the Spinache based HAPI
application will run the `index.html` file located in the Doryphore repository
when running in the browser.

### vrgp-doryphore

The structure of the repository:
<pre>
.
├─src
│ ├── App.vue
│ ├── assets
│ │   └── logo.png
│ ├── components
│ │   ├── icon.vue
│ │   └── Vessel.vue
│ ├── index.css
│ └── main.js
├index.html
├package.json
└...
</pre>

Not much to say about this, this is just the frontend of the Spinache-based MOC.
There are instructions on how to use this on the [official Doryphore Github
page](https://github.com/aboamare/vrgp-doryphore). Basically, all that needs to be done is `npm install`, followed by `npm
run build` after every modification in the repo. The second step will generate a
`dist` folder (this needs to be linked to, check the [vrgp-spinache](#vrgp-spinache) section).
There is an important note down below though, so read on!

The app is [Vue](https://vuejs.org/)-based. There is nothing really important about this.

Important files in the application folder are:
- `src/App.vue`: This is the main template file. What this means is that it
  contains both html and javascript code. This is what will be inserted as an
  html page in the browser. The file contains most of the logic of the
  web app.
- `src/main.js`: The main application file that launches Vue. Nothing too important.
- `index.html`: This is just some basic setup that imports `src/main.js`, which
  in turn imports `src/App.vue`. This file is automatically loaded by
  `vrgp-spinache` when going to the web page `localhost:3001/operator/`.
- `package.json`: describes the dependencies of the project. **NOTE:** in the
  file, there is `vrgp-spinache-lib` as a dependency. You should change this to
  wherever you have it installed in your path *before* running `npm install`. If
  you already ran that, completely delete the `node_modules` folder and do the
  steps above.

---

## 2. Problems with the environment/code

---

## 3. Other questions and takeaways
