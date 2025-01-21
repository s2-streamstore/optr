# optr

<!-- pkg.go.dev -->
![https://pkg.go.dev/badge/github.com/s2-streamstore/optr.svg](https://pkg.go.dev/github.com/s2-streamstore/optr)
<!-- Discord (chat) -->
![https://img.shields.io/discord/1209937852528599092?logo=discord](https://discord.gg/vTCs7kMkAf)
<!-- Github Actions (CI) -->
![https://github.com/s2-streamstore/optr/actions/workflows/ci.yml/badge.svg](https://github.com/s2-streamstore/optr/actions?query=branch%3Amain++)
<!-- LICENSE -->
![https://img.shields.io/github/license/s2-streamstore/optr](./LICENSE)

Package optr provides utility functions for working with optional values
represented as pointers in Go. It simplifies common operations like mapping,
cloning, and handling default values.

## Features

* Create pointers from non-pointer values.
  ```go
  value := optr.Some(42)
  fmt.Println(*value) // Output: 42
  ```

* Create new values from existing pointers.
  ```go
  original := optr.Some(42)
  copy := optr.Cloned(original)
  fmt.Println(*copy) // Output: 42
  fmt.Println(copy != original) // Output: true
  ```

* Apply transformations to pointer values.
  ```go
  value := optr.Some(42)
  result := optr.Map(value, func(v int) string { return fmt.Sprintf("Value: %d", v) })
  fmt.Println(*result) // Output: "Value: 42"
  ```

* Handle default values and fallbacks with ease.
  ```go
  value := optr.Or(nil, func() (int, bool) {
    return 42, true
  })
  fmt.Println(*value) // Output: 42
  ```

* Support for functions that may fail, returning errors where applicable.
  ```go
  value, err := optr.TryAnd(Some(42), func(v int) (string, bool, error) {
    if v > 40 {
      return "Greater than 40", true, nil
    }
    return "", false, fmt.Errorf("value is not greater than 40")
  })
  if err != nil {
    fmt.Println("Error:", err)
  } else {
    fmt.Println(*value) // Output: "Greater than 40"
  }
  ```

## Installation

Install the package using `go get`:

```bash
go get github.com/s2-streamstore/optr@latest
```

## SDK Docs and Reference

Head over to [pkg.go.dev](https://pkg.go.dev/github.com/s2-streamstore/optr)
for detailed documentation and package reference.

## Feedback

We use [Github Issues](https://github.com/s2-streamstore/optr/issues) to
track feature requests and issues with the SDK. If you wish to provide feedback,
report a bug or request a feature, feel free to open a Github issue.

### Contributing

Developers are welcome to submit Pull Requests on the repository. If there is
no tracking issue for the bug or feature request corresponding to the PR, we
encourage you to open one for discussion before submitting the PR.

## Reach out to us

Join our [Discord](https://discord.gg/vTCs7kMkAf) server. We would love to hear
from you.

You can also email us at [hi@s2.dev](mailto:hi@s2.dev).

## License

This project is licensed under the [Apache-2.0 License](./LICENSE).
