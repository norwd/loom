# loom

Loom is a [Literate Programming] tool that can tangle machine code and weave documentation.

<img src="https://raw.githubusercontent.com/norwd/human/b1bc793d7085ed4532349a4125a5d3d171f6c568/docs/automatic-logo.svg" height="50" />

## What is Literate Programming?

Literate Programming is a paradigm invented by [Donald Knuth].
It is essentially swapping the priority of code and comments in a program.
Instead of writing some comments in a code file, in Literate Programming, you write snippets of code in a documentation file.
This has several benefits, the most important being that
since the program is written *as documentation* instead of *with documentation*,
the focus is on explaining the reasoning and thought process behind the implementation.

## What is Tangling?

Tangling is the process of taking a Literate Programming document and compiling machine-executable code from it.
This is called tangling because it takes all the pieces of code spread throughout the document and makes sense of the web of connections between them.

The reason that the code can be so widely spread out is because,
unlike in ordinary programming,
in Literate Programming the code can be given in any order or layout,
whichever leads to the most straightforward description of the implementation,
rather than the structure required by the language one is using.

For example, Go code must be structured in the following order; package declaration, import list, function declarations, etc.
But in Literate Programming, there is no need to follow this structure.
Instead, it may be better to structure the code with the most important function first,
then it's required imports,
then any supplemental function declarations,
then any boilerplate for the package declaration.

## What is Weaving?

Weaving is the process of taking a Literate Programming document and extracting human-readable documentation from it.
Ideally weaving should be minimally necessary, as the Literate Programming document should be useful as documentation in its own right.
However, depending on the format, the documentation may be enhanced by additional post-processing.

For example, Go code allows for semi-literate documentation comments, that can be rendered using the `go doc` command.
This is not true Literate Programming, as the implementation in not shown in the documentation,
and private (non-exported) functions and types are not shown at all.
Truly Literate Programming with Go is possible, and should output all the necessary comments for a complete Go Doc to be created from it.

## Example

The following is an example Literate Programming document, written in markdown, that describes and implements a Hello World program in Go.

````markdown
# Hello World

Prints a world-wide greeting to the console.

This is a short Literate Programming example, showing the construction of a Hello World program in Go.

## Greet the world by printing the message to the console on a new line.

The heart of every Hello World program is the greeting.

```go
func Greet() {
    fmt.Println("hello world")
}
```

This implementation uses the `fmt` package to print the greeting to the console, so the `fmt` package must be imported.

```go
import "fmt"
```

## Main entry point

Since this Hello World Program is written in Go, and is an executable and not a library, we need to define an entry point in the `main` package.
This entry point should simply call the `greet()` function to show the greeting.

```go
func main() {
    Greet()
}
```
````

This markdown document, if processed correctly, should produce the exact same Go code as the following:

```go
// HelloWorld
//
// Prints a world-wide greeting to the console.
//
// This is a short Literate Programming example, showing the construction of a Hello World program in Go.
package main

import (
    "fmt" // This implementation uses the `fmt` package to print the greeting to the console, so the `fmt` package must be imported.
)

// Greet the world by printing the message to the console on a new line.
//
// The heart of every Hello World program is the greeting.
func Greet() {
    fmt.Println("hello world")
}

// Main entry point
//
// Since this Hello World Program is written in Go, and is an executable and not a library, we need to define an entry point in the `main` package.
// This entry point should simply call the `greet()` function to show the greeting.
func main() {
    Greet()
}
```

[Literate Programming]: https://en.wikipedia.org/wiki/Literate_programming
[Donald Knuth]: https://en.wikipedia.org/wiki/Donald_Knuth
