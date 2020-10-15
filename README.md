# Getting Started Tutorials

This repository contains tutorials mainly on how to configure and getting started
with various (Python + R) development tools on Ubuntu 20.04 LTS.

### Tutorials

* Ubuntu workplace setup
* Using R with conda package manager
* Building R package from scratch
* Getting started with PostgreSQL
* Getting started with MongoDB shell
* Create an Azure service principal with Azure CLI

### How to build
  
To build the tutorials, install the requirements and build the docs:

```
$ cd docs
$ pip install -r requirements.txt
$ make html
```

To read the documentation, open file `/docs/build/html/index.html` in your browser.
