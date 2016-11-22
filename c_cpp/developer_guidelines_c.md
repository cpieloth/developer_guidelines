# Developer Guidelines for C Projects

## Code Format

* Encoding: US-ASCII
* Line Ending: Unix `\n`
* Line Length: 120
* Indent Brace Style: Allman/BSD style
* Indent Style: Spaces
* Indent Size: 4
* CamelCase or snake_case: snake_case


## Coding Guidelines

### Functions: Use _self_ as "this" Pointer

For object-oriented class methods the this-pointer must be named `self` and NOT `this`.

*Example:*

```c
struct set;
bool set_add(struct set* self, void* data);
```

*Pros:*

* Compatibility with C++ keyword `this`, if using C code in C++;
* Consistent naming improves readability


### Functions: Parameter Order

Output parameters of a method must be placed before input parameters.
For OO-like methods the self pointer is the first parameter.

*Example:*

```c
struct set my_set;
set_to_array(&my_set, &array, array_len);

size_t read_socket(void* out_buf, size_t len, int sd);
size_t read_socket_timeout(void* out_buf, size_t len, int sd, size_t timeout_ms);
```

*Pros:*

* New input parameter "can be appended"
* Common for C++, which supports default parameters
* Consistent API


### Functions: Private Methods

Use `static` keyword and an underscore for local/private functions & variables.

*Example:*

```c
static void _foo();
static int _bar;
```

*Pros:*

* principle of information hiding & restrict access
* avoid naming conflicts
* readability & consistency


### Variables/Parameter: Suffix for Units

Use a suffix to indicate an unit of a variable, e.g. for seconds or millimeters.

*Example:*

```c
size_t timeout_ms = 100;  // timeout in millisecond

/**
 * Calculate potential energy.
 *
 * @param weight_kg  weight in kilogram
 * @param height_m   height in meter
 * @return potential energy in Joule
 */
double potential_energy(double weight_kg, double height_m);
```

*Pros:*

* units are visible in API
* units are known without reading documentation


### Includes

Some rules for includes:

* include what you use
* include order by groups and alphabetical:
 1. C library
 2. system header
 3. external dependencies includes
 4. project includes
* include notation:
 * angle brackets for external includes, e.g. `#include <stdio.h>`
 * double quotes for project includes, e.g. `#include "foo.h"`
* comment uncommon include, e.g. `#include <check.h> // functions for unit testing`


*Example:*

```c
#include <stdio.h>
#include <string.h>

#include <sys/queue.h>
#include <sys/syslog.h>

#include "foo/bar.h"
#include "bar.h"
```

### for-loop

Declare counter variable of for-loops in the _init_clause_ (supported since C99).

*Example:*

```c
for(size_t i = 0; i < n_array; ++i)
{
    sum += array[i];
}
```

*Pros:*

* restrict scope, prevents accidental access
* readability


### Enumerations

Use enum name as prefix for enumerator names.

*Example:*

```c
enum IO_MODE
{
    IO_MODE_READ, IO_MODE_WRITE, IO_MODE_APPEND
}
```

*Pros:*

* reduce naming conflicts
* better auto-completion

*Cons:*

* long enumerator names


### Prefer Types over Documentation

Data types should be preferred over variable names/documentation when designing interface/API.

*Example:*

```c
// bad:
int set_is_empty(const struct set *self);
// good:
bool set_is_empty(const struct set *self);

// bad:
size_t write(FILE* fd, const void *data, int nbytes, int mode);
// good:
enum IO_MODE
{
    IO_MODE_APPEND, ...
}

size_t write(FILE* fd, const void *data, int nbytes, enum IO_MODE mode);
```

*Pros:*

* accidentally swapped parameters raises compiler errors
* reduces bugs produced by wrong assumptions, e.g. <0, 0 or >0 on error?


### Common Names, Abbreviation & Prefixes

Agree on a set common names, abbreviation and prefixes.

*Example:*

* `self, cls, rc, len, mgr, utl, ptr, cb, ...`

*Pros:*

* readability & consistency

### Misc

* use const-correctness
* define use of typedefs


## Documentation

### API Documentation

Use [Doxygen](http://www.doxygen.org) with the following notation for API documentation:

```c
/**
 * User record.
 */
struct user
{
    unsigned int id; //!< The user ID.
}

/**
 * Adds a user to something.
 *
 * @param user The user to add.
 * @return True on success.
 */
bool user_add(struct user* user);
```

### Code Comments

Use backslash notation for single-line and multi-line comments:

*Example:*

```c
// Initialization:
struct user my_user;
my_user.id = 1;

// Processing:
// 1. Add user to database
// 2. Print user information
// 3. ...
user_add(&my_user);
user_print(&my_user);
```

*Pros:*

* temporarily disable code blocks using `/* ... */`


## Project File Structure

A common and clear file structure for C projects:

```
project/             # project root
project/build        # build folder for compilation, artifacts and more
project/cmake        # CMake files for build system
project/doc          # documentation in a text document format, e.g. Markdown or AsciiDoc
project/resources    # Resources, e.g. images, configs
project/src          # source code
project/submodules   # Git submodules
project/tools        # useful tools/scripts, e.g. packaging, config files/generator for IDE
```

## Tools, Links, Further Reading

* Auto Formatter & Code Templates functionality of IDEs (e.g. Eclipse, CLion)
* [cppcheck](http://cppcheck.sourceforge.net): static code analysis
* [Cpplint](https://en.wikipedia.org/wiki/Cpplint): code style check
* [Doxygen](http://www.doxygen.org): API documentation
* [Editorconfig](http://editorconfig.org): maintains consistent coding styles between different editors and IDEs
* [git autocrlf & whitespace](https://git-scm.com/book/tr/v2/Customizing-Git-Git-Configuration#Formatting-and-Whitespace): check correct line endings and spacing
* [git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks): call scripts before a commit
* https://github.com/github/gitignore/blob/master/C.gitignore
* https://google.github.io/styleguide/cppguide.html
* http://www.misra-c.com
* https://en.wikipedia.org/wiki/Indent_style
* https://en.wikipedia.org/wiki/CamelCase
* https://en.wikipedia.org/wiki/Snake_case
* https://en.wikipedia.org/wiki/Const_%28computer_programming%29
