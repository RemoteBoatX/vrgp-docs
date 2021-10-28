# Åboat software environment

This document contains all notes and other findings we made during getting
familiar with the Åboat software environment. This should be mostly how to set
up the environment, any particular problems we found (and how to fix them),
questions and answers and other takeaways.

---

## 1. Setting up the environment

---

## 2. Problems with the environment/code

### There is no consistency in how Åboat initializes variables.

This is of course a problem of code style and should be avoided. There should be
static checks at commit time to check for a particular style we choose.

### Functions longer than 250 lines

Of course another code style problem. Functions longer than 50 lines should be a
warning, functions longer than 100 lines shouldn't be allowed to be committed,
and you deserve bad things to happen to you if you do that.

### Wrong or no formatting

Code style problem again. Should be checked by a tool at commit time.

---

## 3. Other questions and takeaways

### opendlv-vehicle-view Docker container problem

The opendlv-vehicle-view Docker container could be started easily without
console arguments, the arguments from the README did not work apparently. The
web interface was accessible but did not contain any actual contents.

### opendlv::proxy and routerdatamessage.odvd correspondence

The opendlv::proxy functions correspond to messages defined in
routerdatamessage.odvd

### Where is the opendlv-service-router service accessed?

[TODO]
