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

The structure of the repository:
<pre>
.
├─ apps
│  ├── moc.html
│  ├── moc.js
│  ├── operator -> ../../Doryphore/dist (the link to the doryphore app, see below)
│  ├── operator.js
│  ├── rtc-test.html
│  ├── rtc-test.js
│  ├── tests
│  │   └── NMEA-sentences.js
│  └── vessel.html
├──lib
│  ├── conning.js
│  ├── iceservers.js
│  └── peer.js
├── server.js
├── moc.js
├── operators.js
├── vessels.js
├── invalid-nmea-sentences.txt
├── package.json
└── ...
</pre>

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

### vrgp-spinache-lib

The structure of the repository:
<pre>
.
├── index.js
├── package.json
├── peer.js
├── README.md
├── tests
│   └── NMEA-sentences.js
└── vessel.js
</pre>

To get the server running, some file contents need to be copied into the
`vrgp-spinache` repository.

The modifications are:
- comment line 12 in the file `<spinache>/apps/vessel.html` (the one importing
  `VesselInterface`)
- copy the contents of the file `<spinache-lib>/vessel.js`, *except* for the
  very first and the very last lines (the ones that say `import ...` and `export
  ...`) into the above file, below the commented line.
- copy the contents of the file `<spinache-lib>/peer.js` below the commented
  line from point 1 (so basically above the code pasted from step 2)

This should bring everything needed into the file `vessel.html`. Now going in
the browser to `localhost:3001/vessel.html` should display a page which asks for
a vessel name and a `contact MOC` button. After pressing connect, the vessel
will connect to the local MOC server (the vessel is a mock-up). To observe
this, open another browser page pointing to `localhost:3001/operator`.

Important files in the application folder are:
- `peer.js`: This file is used by the Doryphore web interface.
- `vessel.js`: This file is used by the Spinache web application.
- `tests/NMEA-sentences.js`: Also used by the Spinache web application. This is
  duplicated however in the structure of the Spinache repository.

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
├── index.html
├── package.json
└── ...
</pre>

Not much to say about this, this is just the frontend of the Spinache-based MOC.
There are instructions on how to use this on the [official Doryphore Github
page](https://github.com/aboamare/vrgp-doryphore). Basically, all that needs to be done is `npm install`, followed by `npm
run build` after **every modification** in the repo. The second step will generate a
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
