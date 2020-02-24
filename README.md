# ruut-ruby

**This project is no longer maintained. [Check out the rewrite in Rust][ruut-rust].**

## Why

I deal with folder structures a lot for work at @DocSend. I also love the
output of [`tree(1)`][tree-wiki] for talking about folder structures.

Unfortunately, most of the time I'm not talking about folder structures on my
file-system, so in order to get the pretty output with `tree(1)`, I would have
to create the directories and/or files on my computer, which seems a bit
ridiculous.

That's why I created `ruut`. It takes a fairly easy-to-type expression like
this:
```
Parent (Child 1, Child 2 (Grandchild 1, Grandchild 2), Child 3)
```

and turns it into something pretty like

```
Parent
├── Child 1
├── Child 2
│   ├── Grandchild 1
│   └── Grandchild 2
└── Child 3
```

## Usage

`ruut` can either take the "structure" from stdin or as an argument:

```sh
$ ruut 'Parent (Child 1, Child 2 (Grandchild 1, Grandchild 2), Child 3)'
# Equivalent to
$ echo 'Parent (Child 1, Child 2 (Grandchild 1, Grandchild 2), Child 3)' | ruut
```

## Installation

It's just a Ruby script, so all you need to do is the following:
1. Make sure Ruby is installed
2. Put it in a directory that's in your `$PATH` (e.g. `/usr/local/bin/`)
3. Allow yourself to execute it (e.g. `chmod u+x /where/you/put/ruut`)

## Syntax

The "structure" should abide by the following syntax. Surrounding `<`,`>` means
you fill in those values yourself. Surrounding `[`,`]` means that part is
optional.

```
<name of folder> [(<name of subfolder 1> [(<name of subsubfolder1>[, <name of
subsubfolder2>[, ...]])][, <name of subfolder 2> [, ...]])]
```

It's much easier to see through examples:

```
Parent (Child 1, Child 2 (Grandchild 1, Grandchild 2), Child 3 (Grandchild 3))
```

yields

```
Parent
├── Child 1
├── Child 2
│   ├── Grandchild 1
│   └── Grandchild 2
└── Child 3
    └── Grandchild 3
```

Note that whitespace in  the middle of a folder name is preserved.

[ruut-rust]: https://github.com/HarrisonB/ruut
[tree-wiki]: https://en.wikipedia.org/wiki/Tree_(command) 
[lisp-parser-python]: https://norvig.com/lispy.html
