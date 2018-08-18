# eno

This repository contains the specification documents for the [eno notation
language](https://eno-lang.org).

*TERMINOLOGY.md* contains a glossary with all terms that are used to describe
the eno language.

The technical specification write-up in ABNF notation is currently work in
progress, in the meantime please gather further information from the the
[website](https://eno-lang.org) and the terminology glossary, and feel free to
open an issue here in the issue tracker if anything is unclear.

## Encoding

Eno documents must be encoded as `UTF-8`.

## Filename Extension

Eno documents use the `.eno` extension.

## MIME Type

On the internet eno documents are transferred as `text/eno`.

## Language stability and development plan

The eno language as documented, shown and used throughout [eno-lang.org](https://eno-lang.org), all repositories, and all case studies,
is a fully designed and developed release candidate (*1.0.0-RC* if you will), whose aptness for a
broad variety of usecases has already been tested in multiple, diverse case studies.

For the coming months up until the end of 2018 this stage (frozen RC) will be
kept, with the goal of gathering more and broader data and insights on any
possibly overlooked language design flaws, inconsistencies or absolutely
required changes.

Based on this data a final specification will be compiled and ratified around Q2
2019, which should only introduce breaking changes if there are fundamental
reasons found for such changes.

As soon as this second and at the same time last specification goes into effect
and is fully supported by all library implementations it will consequently be
frozen and locked, with no further changes planned nor allowed from that point
on, or in other words, eno *1.0.0 Final* (or whatever the name then) will be the next and last iteration
of the language.
