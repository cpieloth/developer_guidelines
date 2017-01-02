# Developer Guidelines for CMake Files

## Code Format

* Encoding: US-ASCII
* Line Ending: Unix `\n`
* Line Length: 120
* Indent Style: Spaces
* Indent Size: 4
* CamelCase or snake_case: snake_case


## Find Modules, Dependencies & Targets

* check dependencies with `find_package()` instead of `include()`, see [Using
external libraries](https://cmake.org/Wiki/CMake:How_To_Find_Libraries#Using_external_libraries)
* write proper ﬁnd modules, see [Writing ﬁnd modules](https://cmake.org/Wiki/CMake:How_To_Find_Libraries#Writing_find_modules)
 * document deﬁned variables
 * use `find_package_handle_standard_args()`
 * do not set/modify project specific or external variables/settings, this is
the task of the caller
 * specify `<NAME>_TARGET` variable/target to resolve this library, e.g. via [ExternalProject](https://cmake.org/cmake/help/latest/module/ExternalProject.html), [File Download](https://cmake.org/cmake/help/latest/command/file.html), apt-get, ...
* use deﬁned `<NAME>_TARGET` variable for target dependencies to resolve a library (if provided)
* use `target_include_directories()` and `target_link_libraries()` to keep global dependencies clean
* example with Boost library dependency:

```shell
find_package(Boost REQUIRED)
add_library(my_module SHARED ${my_module_sources})
# For resolving/download Boost (if such a mechanism is provided):
# add_dependencies(my_module ${Boost_TARGET})
target_include_directories(my_module SYSTEM ${Boost_INCLUDE_DIRS})
target_link_libraries(my_module ${Boost_Log_LIBRARY_RELEASE})
```


## Types & Arguments

* String
 * use double quotes for strings, e.g. `set(CMAKE_BUILD_TYPE "Release")`
 * exceptions can be: targets, files, paths
* Boolean
 * use `ON/OFF`, e.g. `set(IS_SNAPSHOT ON)`
 * do not use any quotes
* List
 * use `list` for lists, e.g. `list(APPEND sources foo.c bar.c)`
 * use `list(APPEND ...)` and not `set(...)` to add values to a list
* Arguments
 * put arguments in double quotes, e.g. `my_func("foo" "${my_sources}")`
 * except variable names, e.g. `list(APPEND my_sources ...)`, or variables which should be expanded


## Naming

* Functions
 * lower_case, e.g. `add_dependencies(...)`
 * use preﬁx for functions if namespace is useful, e.g.

```shell
function(test_create_ctest ...)
    # ...
endfunction(test_create_ctest)

function(test_create_cpptest ...)
    # ...
endfunction(test_create_cpptest)
```

* Operators: UPPER CASE, e.g. `list(APPEND ...)`
* Control statements: lower case, e.g. `if(condition) ... endif()`
* Global variables: UPPER CASE, e.g. `set(CMAKE_BUILD_TYPE "Release")`


## Documentation

Use Doxygen-style API documentation, e.g.

```shell
##
# Sum of a and b.
#
# @param[out] sum Result of a+b.
# @param[in]  a   Summand 1.
# @param[in]  b   Summand 2.
#
function(math_add sum a b)
    # ...
endfunction(math_add)
```


## Tools, Links, Further Reading

* [Editorconfig](http://editorconfig.org): maintains consistent coding styles between different editors and IDEs
* https://github.com/github/gitignore/blob/master/CMake.gitignore
