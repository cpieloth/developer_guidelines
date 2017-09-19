# Developer Guidelines for Python Projects

Run pylint, pep8 and pep257 on your code! Use provided targets by `setup.py`.


## Code Format

* Encoding: UTF-8
* Line Ending: Unix, `\n`
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
* use shebang only for entry scripts, not for API files!
* example:

```python
#!/usr/bin/env python3

import sys

def main(argv):
    # code

if __name__ == "__main__":
    sys.exit(main(sys.argv))
```

### Logging

* use `print()` only for CLI/TUI
* use `logging` module for everything else, i.e. API/library
* prefer _module-level logger_, see [Advanced Logging Tutorial](https://docs.python.org/3/howto/logging.html#advanced-logging-tutorial)
* log variable data using format string and append the variable data as arguments, see [Logging Variable Data](https://docs.python.org/3/howto/logging.html#logging-variable-data)
* example:

```python
import logging

logger = logging.getLogger(__name__)  # module-level logger

logger.info('foo=%s', foo)            # correct

logger.info('foo=%s' % foo)           # WRONG!
logger.info('foo={}'.format(foo))     # WRONG!
```

### String Formatting

* use "new style" string formatting, see [PyFormat](https://pyformat.info/)

```python
foo_bar_str = 'foo={}, bar={}'.format(foo, bar)    # correct

foo_str = 'foo=' + str(foo) + ', bar=' + str(bar)  # in certain cases to increase readability

foo_bar_str = 'foo=%s, bar=%s' % (foo, bar)        # WRONG!
```

### Property, Getter, Setter

* use public member variables, if read & write access is required
* use properties to restrict access of member variables or when additional logic is required, e.g. range or type checks
* use property instead of getter and setter
* pro: A public member variable can be easily transformed to a property later/when required, without touching the external interface! So do not write more code than you have to.

### Project Structure

A common and clear file structure for Python projects:

```
project/               # project root
project/build/         # temp. created for artifacts
project/doc/           # documentation in a text document format, e.g. Markdown or AsciiDoc
project/project/       # python API of the project and namespace, i.e. the actual source code folder
project/tests/         # unit tests
project/tools/         # external tools and configuration files for them, ...
project/venv/          # temp. created virtual environment
project/.editorconfig  # basic code style definition
project/project.py     # entry point/top-level script for developers
project/setup.py       # distutils/packaging, generate HTML documentation, trigger tests, ...
```


## Tools, Links, Further Reading

* [Editorconfig](http://editorconfig.org): maintains consistent coding styles between different editors and IDEs
* [Logging HOWTO](https://docs.python.org/3/howto/logging.htm)
* [Logging Cookbook](https://docs.python.org/3/howto/logging-cookbook.html)
* [PEP 0008, pep8](https://www.python.org/dev/peps/pep-0008/): style guide for python code and style guide checker module
* [PEP 0257, pep257](https://www.python.org/dev/peps/pep-0257/): Docstring Conventions and python docstring style checker module
* [Project Templates](https://github.com/cpieloth/project_templates): Templates for software project, e.g. file structure, build-management and more
* [Pylint](https://www.pylint.org/): code analysis for Python
* [PyFormat](https://pyformat.info/): "new style" string formatting
* [Sphinx](http://www.sphinx-doc.org): API documentation for Python, like Doxygen
* [Virtualenv](https://virtualenv.pypa.io): tool to create isolated Python environments
* https://github.com/github/gitignore/blob/master/Python.gitignore
* https://google.github.io/styleguide/pyguide.html
