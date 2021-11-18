# OpenDLV microservices framework

This document contains all notes and other findings we made during getting
familiar with the OpenDLV framework. This should be mostly problems, answers to
some questions we had, and how to set up certain things in programs.

This directory _**SHOULDN'T**_, however, include code examples. Such code
examples should be kept in a different repository and linked to from here. For
small code samples, the code can directly be embedded into this README file.

---

## 1. Small code examples

For very easy and quick starting code for a sender and a receiver, see [the
Cluon tutorial](https://wandbox.org/permlink/3S1bSOaLakXfdWWZ) (see below for what Cluon is).

There are further tutorials for Cluon [here](https://github.com/chrberger/libcluon#tutorials--api-documentation).

---

## 2. Problems with the OpenDLV framework and how we solved them

---

## 3. Other questions and takeaways

### Some notes about OpenDLV

OpenDLV is based on [Cluon](https://github.com/chrberger/libcluon). Cluon is the low-level code that takes care of
the OD4 communication between services.

The microservices are communicating to each other through UDP multicast, i.e. if
one wants to send data to another one, it will multicast it on an UDP port
address and number, and all the microservices in a specific group will get the
message, but only the interested microservice will listen for the message and
actually do something with that (the low-level stuff is taken care of by Cluon).
The default UDP port used is `224.0.0.{CID}`, where `CID` is the ID of the OD4
group.

Messages that are sent to each other are encoded in a `odvd`-type message. How
this works is:
- You write a `odvd`-type message with a specification of how you want the
  message to look like, for example

```odvd
message MyMessage1 [id = 123] {
    uint32 myNumber [id = 1];
    string myText   [id = 2];
}
```

- You call the Cluon library to generate a `.hpp` file with the specification of
  the class following the message above.
- Import the `.hpp` file in your code, and then use OD4 Sessions provided by
  Cluon to pass the messages around. See the tutorial above for full
  instructions on how to do this.

---

## 4. Useful links

- [The OpenDLV framework Github](https://github.com/chalmers-revere/opendlv)
- [OpenDLV tutorial on Github](https://github.com/chalmers-revere/opendlv-tutorial-kiwi)
