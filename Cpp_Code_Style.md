Xiriar Software C++ code style
==============================

Table of contents
-----------------
[[FMT] Formatting](#fmt-formatting)

[FMT] Formatting
----------------

### [FMT-#1] Line length

Each line should be limited to a maximum of 80 characters.

**Rationale**

Although most modern computers already have screens wide enough, there are still
couple of reasons, why we prefer to limit the maximum line length to 80
characters:
* Limiting of maximum line length can improve the readability (no need to scroll
  left to right).
* Unix and Linux terminals have default width of 80 characters, and the same
  applies to the Windows default command line terminal. The limit is useful for
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
This is only allowed for C-style comments:
```cpp
/* a long comment line */
```
and not for C++ style comments
```cpp
// a long comment line
```
because in some situations, the long lines might be splitted or trimmed
automatically when the file is uploaded (e.g. the case of IBM mainframe). That
is not an issue for C-style comments, but it would break the code in case
of C++ style comments.

**Remarks**

If the limit of 80 characters is hard to achieve because of the indentation,
then it is usually a sign to refactor the code, as too much indentation is hard
to follow and understanding of the code is more complicated.

---

&copy; 2014 [Xiriar Software](http://www.xiriar.com/)

Licensed under the [Apache License, Version 2.0](LICENSE)
