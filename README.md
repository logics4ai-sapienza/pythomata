# Pythomata


[![](https://img.shields.io/pypi/v/pythomata.svg)](https://pypi.python.org/pypi/pythomata)
[![](https://img.shields.io/travis/marcofavorito/pythomata.svg)](https://travis-ci.org/marcofavorito/pythomata)
[![](https://img.shields.io/pypi/pyversions/pythomata.svg)](https://pypi.python.org/pypi/pythomata)
[![](https://img.shields.io/badge/docs-mkdocs-9cf)](https://www.mkdocs.org/)
[![](https://img.shields.io/badge/status-development-orange.svg)](https://img.shields.io/badge/status-development-orange.svg)
[![](https://coveralls.io/repos/github/marcofavorito/pythomata/badge.svg?branch=master)](https://coveralls.io/github/marcofavorito/pythomata?branch=master)
[![](https://img.shields.io/badge/flake8-checked-blueviolet)](https://img.shields.io/badge/flake8-checked-blueviolet)
[![](https://img.shields.io/badge/mypy-checked-blue)](https://img.shields.io/badge/mypy-checked-blue)
[![](https://img.shields.io/badge/license-Apache%202-lightgrey)](https://img.shields.io/badge/license-Apache%202-lightgrey)

Python implementation of automata theory.


* Free software: Apache 2.0
* Documentation: https://marcofavorito.github.io/pythomata.

## Dependencies

### Graphviz


For Debian systems, the following commands should work:

    $ wget http://ftp.it.debian.org/debian/pool/main/g/graphviz/graphviz_2.38.0-17_amd64.deb
    $ sudo dpkg -i graphviz_2.38.0-1~saucy_amd64.deb
    $ sudo apt-get install -f

Otherwise check the installation guide from the [official site](https://www.graphviz.org/download/).

## Install

Install from `master` branch:

- with `pip`:


        pip3 install git+https://github.com/marcofavorito/pythomata.git


- or, clone the repository and install:


        git clone htts://github.com/marcofavorito/pythomata.git
        cd temprl
        pip install .



## How to use

* Define an automaton:

```python
from pythomata.dfa import DFA
alphabet = {"a", "b", "c"}
states = {"s1", "s2", "s3"}
initial_state = "s1"
accepting_states = {"s3"}
transition_function = {
    "s1": {
        "b" : "s1",
        "a" : "s2"
    },
    "s2": {
        "a" : "s3",
        "b" : "s1"
    },
    "s3":{
        "c" : "s3"
    }
}
dfa = DFA(states, alphabet, initial_state, accepting_states, transition_function)  
```

* Test word acceptance:

```python
# a word is a list of symbols
word = [b, b, b, a, b, c]

dfa.accepts(word)        # True

# without the last symbol c, the final state is not reached
dfa.accepts(word[:-1])   # False
```

* Operations such as minimization and trimming:

```python
dfa_minimized = dfa.minimize()
dfa_trimmed = dfa.trim()
```

* Print the automata:

```python
filepath = "./my_awesome_automaton"
dfa.minimize().trim().to_dot(filepath)
```

The output in .svg format is the following:

![](img/my_awesome_automaton.svg)


## Features


* Basic DFA and NFA support;
* Algorithms for DFA minimization and trimming;
* Algorithm for NFA determinization;
* Print automata in SVG format.


## Tests

To run the tests:

    tox

To run only the code style checks:

    tox -e flake8

## Docs

To build the docs:


    mkdocs build
    

To view documentation in a browser


    mkdocs serve


and then go to [http://localhost:8000](http://localhost:8000)


## License

Copyright 2018-2019 Marco Favorito
