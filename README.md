# Dictim

[![CircleCI](https://dl.circleci.com/status-badge/img/gh/judepayne/dictim/tree/main.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/judepayne/dictim/tree/main)

[![bb compatible](https://raw.githubusercontent.com/babashka/babashka/master/logo/badge.svg)](https://babashka.org)

Dictim is an edn syntax for expressing a graph diagram, and compiling it to either [d2's](https://github.com/terrastruct/d2) or [Graphviz's](https://graphviz.org) text languages. You can also parse any piece of d2 into dictim syntax.

Any piece of dictim syntax data can be expressed as json as well as edn.

Dictim supprts both Clojure and Babashka and comes as a library, a command line tool and a microservice (see dictim.server below).

## Rationale

Diagrams as data: dynamically generate rather than locking away information in hand produced diagrams. Dynamic diagrams create opportunities to better understand the information being visualized, e.g. group this way or that, style one way or another, dynamically include/ exclude information.

## Library Release Information

Latest release:

[deps.edn](https://clojure.org/reference/deps_and_cli) dependency information:

As a git dep:

```clojure
io.github.judepayne/dictim {:git/tag "0.7.00" :git/sha "0683371"}
```

d2 version compatibility: 0.6.4


## Docs

* [Wiki](https://github.com/judepayne/dictim/wiki)


## Basic usage

Let's round trip from dictim to d2, and back!

### From dictim to d2

dictim and d2 have three principle types of elements: shapes, connections and containers.

Here's an example of producing a d2 specifiction of a diagram with two shapes and a connection:

```clojure
user=> (use 'dictim.d2.compile)
nil
user=> (d2 [:s1 "Shape 1"][:s2 "Shape 2"][:s1 "->" :s2 "reln"])
"s1: Shape 1\ns2: Shape 2\ns1 -> s2: reln"

```

When sent to the d2 CLI executable:

<img src="img/ex1.png" width="250">

### From d2 to dictim

let's turn the above d2 string back into dictim.

```clojure
user=> (use 'dictim.d2.parse)
nil
user> (dictim "s1: Shape 1\ns2: Shape 2\ns1 -> s2: reln" :key-fn keyword)
([:s1 "Shape 1"] [:s2 "Shape 2"] [:s1 "->" :s2 "reln"])

```

For details on dictim syntax, the compile, parse and other operations, please see the [wiki](https://github.com/judepayne/dictim/wiki).


## Command line tool

This project contains a command line tool version (a babashka script) that you can install and use to play with dictim on the command line. You can easily create a toolchain that goes directly from dictim edn to a diagram. See the [wiki](https://github.com/judepayne/dictim/wiki/Command-Line) for details.


## Related Projects

This project is the base project for a number of other projects:

- [dictim.graph](https://github.com/judepayne/dictim.graph) Convert a representation of a graph into dictim: ideal for boxes and arrows/ network diagrams
- [dictim.cookbook](https://github.com/judepayne/dictim.cookbook) Examples of dictim in action!
- [dictim.server](https://github.com/judepayne/dictim.server) A easy-to-deploy microservice for converting dictim into d2 diagrams.


## License

Copyright © 2024 Jude Payne

Distributed under the [MIT License](http://opensource.org/licenses/MIT)
