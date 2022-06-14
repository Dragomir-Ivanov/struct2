
[![codecov](https://codecov.io/gh/worldline-go/struct2/branch/master/graph/badge.svg)](https://codecov.io/gh/worldline-go/struct2)

# struct2

This repository helps to work with struct, convert map and get information about that.

This is a modified version of common struct to map libraries with cool features.

Supported tags: `-`, `omitempty`, `string`, `ptr2`, `omitnested`, `flatten`.

Convertion order is __`-`, `omitempty`, `string`, `ptr2`, custom hook function, hooker interface, `omitnested` + `flatten`__

## Usage

```sh
go get github.com/worldline-go/struct2
```

Get decoder and run `Map` method.

```go
type ColorGroup struct {
    ID     int      `db:"id"`
    Name   string   `db:"name"`
    Colors []string `db:"colors"`
    // custom type with implemented Hooker interface
    // covertion result to time.Time
    Date types.Time `db:"time"`
    // unkown type but to untouch it add omitnested to keep that struct type
    RGB *null.String `db:rgb,omitempty,omitnested`
}

decoder := struct2.Decoder{
    TagName: "db",
}

// get map[string]interface{}
result := decoder.Map(group)
```

Custom decoder can be use in struct witch have `struct2.Hooker` interface.  
Or set a slice of custom `struct2.HookFunc` functions in decoder.

Check documentation examples.

## Tags Information

__omitnested__: very helpful to don't want to touch data.

__ptr2__: convert pointer to the concrete value, if pointer is nil new value generating.
ptr2 to effect custom hook functions and hooker interface also omitnested.

---

## Inspired Projects

[fatih/structs](https://github.com/fatih/structs)  
[mitchellh/mapstructure](https://github.com/mitchellh/mapstructure)
