Xiriar Software C++ code style
==============================

Table of contents
-----------------
[[FMT] Formatting](#fmt-formatting "[FMT] Formatting")  
[[FMT:#1] Line length](#fmt1-line-length "[FMT:#1] Line length]")  
[[FMT:#2] Spaces vs. Tabs](#fmt2-spaces-vs-tabs "[FMT:#2] Spaces vs. Tabs]")  
[[FMT:#3] Indentation](#fmt3-indentation "[FMT:#3] Indentation]")  

[FMT] Formatting
----------------

### [FMT:#1] Line length

Each line should be limited to a maximum of 80 characters.

**Rationale**

Although most modern computers already have screens wide enough, there is still
couple of reasons, why we prefer to limit the maximum line length to 80
characters:
* Readability and style. Very long source lines can be difficult to read and
  understand [JSF-41].
* Unix and Linux terminals have the default width of 80 characters, and the same
  applies to the Windows default command line settings. The limit is useful for
  remote SSH editing or reviewing e.g. git diffs on the command line.
* It is easier to see multiple files at the same time in columns side-by-side
  (this proves especially useful when doing a three-way merge).
* The code is not mangled when printed or sent via e-mail.
* We plan to also support the IBM mainframe systems to some extent, where the
  C++ source code line length is limited to a maximum of 80 (longer lines are
  split or trimmed during the upload).

**Exceptions**

If a C-style comment line contains an example command or a literal URL longer
than 80 characters, that line may be longer than 80 characters for ease of cut
and paste.
This is only allowed in C-style comments:
```cpp
/* a long comment line - correct */
```
and not in C++ style comments:
```cpp
// a long comment line - wrong!
```
because in some situations, the long lines might be split automatically when the
file is uploaded (e.g. the case of IBM mainframe). That is (usually) not an
issue for a C-style comment, but it would break the code in case of C++ style
comments.

**Remarks**

If the limit of 80 characters is hard to achieve because of the indentation,
then it is usually a sign to refactor the code, as too much indentation is hard
to follow and understanding of the code is more complicated.

### [FMT:#2] Spaces vs. Tabs

Only spaces should be used, no tabs.

**Rationale**

There is always endless discussion on this topic, the decision to use spaces
over tabs is based on the following:
* Tabs are interpreted differently across various editors and printers [JSF-43].
* If indenting by tabs, they must be only used for the structural indentation
  (i.e. for the block indentation to the start of the line), but not behind
  that. For alignment etc., spaces still must be used to preserve the correct
  alignment across various settings of the Tab size. Such combined scheme is
  very hard to follow (for example, the Tab key can then only be used to indent
  the line, but not to move up to the alignment).
* Tabs can mess with compilers/parsers and report wrong positions on the line -
  because it sees the Tab as a single column instead of multiple (in particular,
  the compiler or parser has usually no way to determine, which size of the Tab
  character you use in your specific source code editor).
* It must be also taken into account, that if we indented by Tabs, we'd always
  have to count 8 columns for the Tab character in scope of the [maximum line
  length constraint](#fmt1-line-length "[FMT:#1] Line length"), regardless of
  the actual setting of the Tab size in the editor. That is because in most
  cases, where the maximum line length actually matters (command line, SSH
  terminal, IBM mainframe, printers, e-mail), the Tab size of 8 columns is
  usually implied. That would in turn force us to actually require having the
  Tab size set to 8 in the editor, and use the value of 8 columns for the
  indentation (which is the case of the [Linux kernel coding
  style](https://www.kernel.org/doc/Documentation/CodingStyle
  "Linux kernel coding style")).

**Remarks**

Many editors can be configured to map the 'Tab' key to a specified number of
spaces.

### [FMT:#3] Indentation

The indentation of the source code should be 4 spaces.

**Rationale**

The decision to use spaces over tabs has been [already
made](#fmt2-spaces-vs-tabs "[FMT:#2] Spaces vs. Tabs"). For the number of
indentation columns itself, the opinions also differ widely, some people prefer
2 space indentation, whereas others prefer even [8 character
indentation](https://www.kernel.org/doc/Documentation/CodingStyle
"Linux kernel coding style").

The value of 4 column indentation has been selected as the most common value
across various projects/standards/editors, which produces sufficient visual
separation for most programmers.

Keep in mind, that in Open Source projects and/or in a team development, you're
writing a code that other people would be reading - so it is not only important
what you prefer, but it is of even more importance what the majority of
users/contributors/team members prefer.

---

&copy; 2014 [Xiriar Software](http://www.xiriar.com/)  
Licensed under the [Apache License, Version 2.0](LICENSE)
