# Solution to Lab4b

## Exercise 2: Spelunking

1. I chose `tree` package
2. Dependency is found in `contol` file, in line "Depends: "
```
Package: tree
Version: 2.0.2-1
Architecture: amd64
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Florian Ernst <florian@debian.org>
Installed-Size: 113
Depends: libc6 (>= 2.34)
Section: utils
Priority: optional
Homepage: http://mama.indstate.edu/users/ice/tree/
Description: displays an indented directory tree, in color
 Tree is a recursive directory listing command that produces a depth indented
 listing of files, which is colorized ala dircolors if the LS_COLORS environment
 variable is set and output is to tty.
```

3. The `tree` command is a standalone utility that displays the directory structure of a path or disk in a terminal. It does not require complex dependencies, additional system configuration files, or libraries that might necessitate further directories outside of `/usr/bin` for the executable and `/usr/share` for documentation and man pages.
```
.
├── control
├── debian-binary
├── md5sums
└── usr
    ├── bin
    │   └── tree
    └── share
        ├── doc
        │   └── tree
        │       ├── changelog.Debian.gz
        │       ├── copyright
        │       ├── README.gz
        │       └── TODO
        └── man
            ├── fr
            │   └── man1
            │       └── tree.1.gz
            └── man1
                └── tree.1.gz
```

4. I found that the package includes `man` pages for different languages, the `/usr/share/man/fr` stands for French, interesting.
