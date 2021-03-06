# Building and testing Canopy

To build and test the project, you will need to install dependencies for several
languages. The build and test suite only requires Node.js installed, and you
only need other languages and libraries installed to run the examples for those
languages.

## Getting the source code

    git clone git://github.com/jcoglan/canopy.git

## Installing dependencies

To install the dependencies for the build and test suite:

    npm install

To install the dependencies for the Python examples:

    pip install -r requirements.txt

To install the dependencies for the Ruby examples (and the tools used to build
the website):

    bundle install

## Building the project

Canopy is self-hosting, which means it contains code that was generated by its
own compiler. This means that it can be tricky to build, but I've tried to
arrange things so that it's difficult to end up with a working copy that won't
execute.

After cloning the repo and running `npm install` you should immediately be able
to run the tests:

    make test

This only tests the code in `src`, which is the canonical source code and where
you should make changes. The code in `bin` is not tested, and the code in `src`
is designed not to be tied to Node but to run on any JS platform. All file I/O
happens in `bin/canopy`.

If you want to run the `bin/canopy` script to run the command-line interface,
you need to bootstrap the project, which meeans taking a copy of the last-known
working instance of the code. To do this just run:

    make

This runs the tests, and if they pass, it copies all the code from `src` into
`lib`. `bin/canopy` loads code from `lib`, not `src`, so the compiler should
always have working source code to use.

Finally, if you want to recompile Canopy's metagrammar, i.e. the grammar that
defines how grammars are written (that's the self-hosting bit), run:

    make compile

You need to have bootstrapped the project for this to work.

To regenerate the example Canopy parsers:

    make java
    make js
    make python
    make ruby

To regenerate the example PEG.js parsers:

    make pegjs

## Running the examples

To run the Java examples:

    javac examples/JavaExample.java && java examples.JavaExample

To run the JavaScript examples:

    node examples/javascript.js

To run the Python examples:

    py.test examples/python.py

To run the Ruby examples:

    ruby examples/ruby.rb
