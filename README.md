amd-three.js 
============

amd-three.js is an example of how to structure an [three.js](http://threejs.org/) application, with functionality split into different [Require.js](http://requirejs.org/) modules.

It is meant as a starting point for more involved projects involving three.js, where having all the code in one file can quickly get unwieldy.

It is also useful for prototyping, as a lot of the boilerplate is moved out of your way.

[Live demo](http://felixpalmer.github.io/amd-three.js/) of this repository can be found at http://felixpalmer.github.io/amd-three.js/

Running
=======

Just host this directory with a webserver of your choice. You can also use the `webserver.sh` script included (provided you have Python) to set up a simple development server.

Then visit http://localhost:8000 in your browser.

Shaders
=======

Custom shaders are put in `/js/shaders` and are saved as .vert or .frag files, for ease of editing. To convert these into a require.js module, run `/js/shaders/compile.py`. This will create `/js/app/shader.js`, which will export a `shader` object with the relevant shaders attached. E.g. `test.frag` will be available as `shader.fragment.test`

Structure
=========

The structure of the file is as per the recommendations in the docs for Require.js. Namely, all the Javascript lives in the `js` folder, with the Three.js library and extension code in `js/lib`, while the app specific code is in `js/app`. The idea is that you shouldn't ever need to modify the files in `js/lib`, only add third party code.

The common three.js constructs, e.g. `camera`, `renderer` are all put into their own modules within the `js/app` directory, and are injected into the `js/app/app.js` file where they are brought together. They sometimes include each other, e.g. the `light` module needs to know about the `scene`. By splitting these object into modules, we are in essence creating singletons, which means we don't have to worry about which order we create them in, as Require.js will figure out the dependencies for us.
