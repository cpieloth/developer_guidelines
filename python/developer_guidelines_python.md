# Developer Guidelines for Python Projects

## Code Format

* Encoding: UTF-8
* Line Ending: Unix `\n`
* Line Length: 120
* Indent Style: Spaces
* Indent Size: 4
* [PEP 0008 - Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)
* [PEP 0257 - Docstring Conventions](https://www.python.org/dev/peps/pep-0257/)


## Coding Guidelines

### Scripting, Top-level Script, Entry Points

* top-level script must use the shebang: `#!/usr/bin/env python3`
* top-level script must use: `if __name__ == "__main__: ..."`
* top-level script should use `sys.exit()` and `sys.argv`
* use shebang only for entry scrips, not for API files!
* Example:

```python
#!/usr/bin/env python3

def main(argv):
    # code

if __name__ == "__main__":
    sys.exit(main(sys.argv))
```

### Logging, User Output, String Formatting

* use `print()` only for CLI output
* use `logging` module for everything else, i.e. API/library
* use "new style" string formatting: see [PyFormat](https://pyformat.info/)

```python
## logging
# do
logging.info('foo=%s', foo)
# DO NOT
logging.info('foo=%s' % foo)

## string format and concatenation
# do
foo_str = 'foo={}'.format(foo)
foo_bar_str = 'foo={}, bar={}'.format(foo, bar)
# DO NOT
foo_str = 'foo=' + str(foo)
foo_str = 'foo=%s' % foo
foo_bar_str = 'foo=%s, bar=%s' % (foo, bar)
```

### Property, Getter, Setter

* use public member variables if read & write access is required
* use properties only to restrict access of member variables or when additional logic is required, e.g. range or type checks
* use property instead of getter and setter
* pro: A public member variable can be easily transformed to a property later/when required, without touching the external interface! So do not write more code than you have to.

### Project Structure

A common and clear file structure for Python projects:

```
project/               # project root
project/build/         # temp. created for artifacts
project/doc/           # documentation in a text document format, e.g. Markdown or AsciiDoc
project/project/       # python API of the project and namespace
project/tests/         # unit tests
project/tools/         # external tools, files for pylint, sphinx, ...
project/.editorconfig  # basic code style definition
project/Makefile       # Makefile to generate HTML documentation, trigger tests, ...
project/project.py     # entry point/top-level script for developers
project/setup.py       # setup.py for distutils/packaging
```


## Tools, Links, Further Reading

* [Editorconfig](http://editorconfig.org): maintains consistent coding styles between different editors and IDEs
* [PEP 0008, pep8](https://www.python.org/dev/peps/pep-0008/): style guide for python code and style guide checker module
* [PEP 0257, pep257](https://www.python.org/dev/peps/pep-0257/): Docstring Conventions and python docstring style checker module
* [Pylint](https://www.pylint.org/): code analysis for Python
* [PyFormat](https://pyformat.info/): "new style" string formatting
* [Sphinx](http://www.sphinx-doc.org): API documentation for Python, like Doxygen
* [Virtualenv](https://virtualenv.pypa.io): tool to create isolated Python environments
* https://github.com/github/gitignore/blob/master/Python.gitignore
* https://google.github.io/styleguide/pyguide.html

Run pylint, pep8 and pep257 on your code! Use provided targets by `Makefile`.
