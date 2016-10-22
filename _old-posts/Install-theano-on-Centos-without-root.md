title: Install Theano on Centos without root privilege
date: 2015-09-02 13:46:13
tags: DL
---

For some reason, I need installing Theano on a server running Centos6 to do some deep learning experiments. But I don't have the root privilege to it, and to make things worse, the server doesn't have connection to Internet...

Centos6 use a python of version 2.6 as default, for further convenience, we should install python2.7 instead.

The sequence of python package to install are:

* python2.7 itself
* six
* numpy
* scipy
* setup-tools (for python setup.py install)
* theano

We should install python2.7 given the prefix parameter to install it as user mode. And the other package listed also should install with `python setup.py develop --user`. The develop can replaced with install, if you don't want to modify the package latter. Additionally, the uninstallation of python package is `python setup.py install --record files.txt && cat files.txt | xargs rm -rf`.

To make Theano work, when compiling python2.7, we should specific `--enable-shard` parameter, namely `./configure --enable-shard --prefix=...`. 

What's more, for running Theano, we should also know about the cpu architecture. run `cc -march=native -E -v - </dev/null 2>&1 | grep cc1 ` to detect the compiler and cpu related information. Then, add the `-march=xxx` to the `[gcc]` section of .theanorc file. xxx depends your cpu architecture. Theano says that it recommends for detect it automatic, but it surely will fail in some situation (like mine). The .theanorc file will look like:
```
[gcc]
cxxflags = -march = ivybridge
```

The true value depends what's your output of the command above. With these previous work, the Theano then works well.