# mingw-w64-guile1.8

This repository provides legacy Guile 1.8 for the [MSys2/Mingw-w32/Mingw-w64](https://sourceforge.net/p/msys2/wiki/MSYS2%20introduction/) environment. 

## Why?
-Presently, although the source packet exists, [Guile 2.0 does not build at all in MSys2/Mingw-w32/Mingw-w64](https://github.com/Alexpux/MINGW-packages/issues/699). A 32-bit Mingw build can however be found [here](https://sourceforge.net/projects/ezwinports/files/)

-Because of profound changes in Guile 2.0 several GNU project still require linking with Guile 1.8, notably [TeXmacs](http://www.texmacs.org/), [GNUCash](http://www.gnucash.org/) or [LilyPond](http://lilypond.org/).

## Caveat
At the moment only 32-bits builds actually work [(see building for X86_64)](./X86_64_building.md).

## Jan 2021
many patches (including security ones) added, from [Mageia](http://distrib-coffee.ipsl.jussieu.fr/pub/linux/Mageia/distrib/cauldron/SRPMS/core/release/guile1.8-1.8.8-32.mga8.src.rpm) that still builds guile1.8
[fix](https://github.com/msys2/MINGW-packages/issues/7712) building on Win10
