## Developer Guidelines for Bash

## Code Format

* Encoding: US-ASCII
* Line Ending: Unix `\n`
* Line Length: 120
* Indent Brace Style: [Allman/BSD style](https://en.wikipedia.org/wiki/Indent_style#Allman_style)
* Indent Style: Spaces
* Indent Size: 4
* CamelCase/snake_case: snake_case
* Loops & conditions: put `; do` and `; then` on the same line
* Function: don't use the keyword `function`, use `func()` instead
* Variable access: prefer `${var}` over `$var`

## Coding Guidelines

### Scripting, Top-level Script, Entry Points

* top-level script must use the shebang: `#!/usr/bin/env bash`
* top-level script should use a main function and call `main "$@"` on last line
* Example:

```bash
#!/usr/bin/env bash

main()
{
    # code
}

main "$@"
```

## Documentation

Use Doxygen-style API documentation, e.g.

```bash
##
# Sum of a and b.
#
# @param[in]  $1   Summand 1.
# @param[in]  $2   Summand 2.
# @return sum Result of $1+$2.
#
add()
{
    # implementation
}
```


## Tools, Links, Further Reading

* [Allman/BSD style](https://en.wikipedia.org/wiki/Indent_style#Allman_style)
* [Google's Shell Style Guide](https://google.github.io/styleguide/shell.xml)
