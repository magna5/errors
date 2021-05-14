magna5/errors
================


Package errors adds stacktrace support to errors in go.

This is particularly useful when you want to understand the state of execution
when an error was returned unexpectedly.

It provides the type \*Error which implements the standard golang error
interface, so you can use this library interchangably with code that is
expecting a normal error return.

Usage
-----


```go
package crashy

import "github.com/magna5/errors"

var Crashed = errors.Errorf("oh dear")

func Crash() error {
    return errors.New(Crashed)
}
```

This can be called as follows:

```go
package main

import (
    "crashy"
    "fmt"
    "github.com/magna5/errors"
)

func main() {
    err := crashy.Crash()
    if err != nil {
        if errors.Is(err, crashy.Crashed) {
            fmt.Println(err.(*errors.Error).ErrorStack())
        } else {
            panic(err)
        }
    }
}
```

Meta-fu
-------

This package was original written to allow reporting to
[Bugsnag](https://bugsnag.com/) from
[bugsnag-go](https://github.com/bugsnag/bugsnag-go), but after I found similar
packages by Facebook and Dropbox, it was moved to one canonical location so
everyone can benefit.

This package is licensed under the MIT license, see LICENSE.MIT for details.


## Changelog
* v1.1.0 updated to use go1.13's standard-library errors.Is method instead of == in errors.Is
* v1.2.0 added `errors.As` from the standard library.
* v1.3.0 *BREAKING* updated error methods to return `error` instead of `*Error`.
* v1.4.0 *BREAKING* v1.4.0 reverted all changes from v1.3.0 and is identical to v1.2.0
* v1.5.0 Brinking back v1.3.0 changes.
