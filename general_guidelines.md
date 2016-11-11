# General Developer Guidelines

## 	Terms & Definitions

**Code Format:**  
A consistent code format reduces the diff size between commits, whereby the changeset is reduced to code changes only. Furthermore it is required for development on different environment, e.g. Unix and Windows.

**Coding Guidelines:**  
Coding guidelines should improve readability, consistency, compatibility and code quality.
Furthermore it is a collection of project related best practices and made commitments.

**Developer Guidelines:**  
Dos and Don'ts for software developers including Code Formats & Coding Guidelines.


## Language Independent Guidelines

### Commit Messages

A commit message should contain a tag followed by a brief description and an optional detailed description.
The tag can have different structures, very common are:

* `<project>-<ticket id>: ` or
* `[<modifiers> #<ticket id>]: `.

Possible modifiers are: `ADD`, `REMOVE`, `CHANGE`, `FIX`, `DOC`, `MISC`.

**Example #1:**
```
MyProject-42: Add feature xyz.

Feature xyz does this and that ...
```

**Example #2:**
```
[ADD #42] Add feature xyz.

Feature xyz does this and that ...
```

### Documentation

Documentation can be grouped at least into:

1. Code Documentation
2. API Documentation
3. Developer Documentation
4. User/Customer Documentation

If possible, documentation should be placed into the project repository. Thus it is easy to keep the code and documentation in sync.
It is very popular to use  lightweight markup languages like [Markdown](http://daringfireball.net/projects/markdown) or [AsciiDoc](http://asciidoc.org) and generate HTML or PDF.

### Automation & Tooling

Automate your workflow as much as possible. The following areas should be automated:

* Build automation (_Maven_, _CMake_, ...)
* Code format checking (_checkstyle_, _cpplint_, ...)
* Static code analysis (_PMD_, _cppcheck_, ...)
* Continuous integration (_Jenkins_, ...)
* Deployment & configuration management (_Vagrant_, _Ansible_, ...)


## Further Reading

* [Google Style Guides](https://github.com/google/styleguide)
* [EditorConfig](http://editorconfig.org)
