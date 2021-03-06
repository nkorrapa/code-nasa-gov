# CODE.NASA.GOV

[![Build Status](https://travis-ci.org/nasa/code-nasa-gov.svg?branch=master)](https://travis-ci.org/nasa/code-nasa-gov)

Catalog of Open Source Software from NASA. Built using [Polymer](https://www.polymer-project.org).

The code.json file feeds the <a href="https://code.nasa.gov">code.nasa.gov</a> website and is reflected in the NASA projects available on <a href="https://code.gov">code.gov</a>

Most of code projects listed in code.json have real open-source licenses. Some have licenses that constrain use to other US government agencies. The license type for each code project is flagged in the json. 

## Setup

### Prerequisites

Install bower and [polymer-cli](https://github.com/Polymer/polymer-cli):

    npm install -g bower polymer-cli

Check that you are using Node v8+

    node -v
    
### Install dependencies

    bower i

### Start the development server

This command serves the app at `http://localhost:8080` and provides basic URL
routing for the app:

    polymer serve --open


### Build

This command performs HTML, CSS, and JS minification on the application
dependencies, and generates a service-worker.js file with code to pre-cache the
dependencies based on the entrypoint and fragments specified in `polymer.json`.
The minified files are output to the `build/unbundled` folder, and are suitable
for serving from a HTTP/2+Push compatible server.

In addition the command also creates a fallback `build/bundled` folder,
generated using fragment bundling, suitable for serving from non
H2/push-compatible servers or to clients that do not support H2/Push.

    polymer build

### Preview the build

This command serves the minified version of the app at `http://localhost:8080`
in an unbundled state, as it would be served by a push-compatible server:

    polymer serve build/unbundled

This command serves the minified version of the app at `http://localhost:8080`
generated using fragment bundling:

    polymer serve build/bundled
    
### Deploying

When deploying to a static web server (with no HTTP/2+Push), be sure to copy
the files from `build/bundled` (**NOT** the project directory) which
contains a functional service worker and minified files.

### Adding a new view

You can extend the app by adding more views that will be demand-loaded
e.g. based on the route, or to progressively render non-critical sections
of the application.  Each new demand-loaded fragment should be added to the
list of `fragments` in the included `polymer.json` file.  This will ensure
those components and their dependencies are added to the list of pre-cached
components (and will have bundles created in the fallback `bundled` build).
