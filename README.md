# singleflight

This repo is a hard fork of [golang.org/x/sync/singleflight](https://pkg.go.dev/golang.org/x/sync/singleflight) that adds generics to the Group type so that there is no need for type assertion when using the library.

## Install

go get marwan.io/singleflight@latest

## Usage

Instead of writing 

```golang
var g Group
v, _, _ := g.Do("key", func() (interface{}, error) {
    return "bar", nil
})
useString(v.(string))
```

you can now just write

```golang
var g Group[string]
v, _, _ := g.Do("key", func() (string, error) {
    return "bar", nil
})
useString(v)
```

Diff:

```diff
- var g Group
+ var g Group[string]
- v, _, _ := g.Do("key", func() (interface{}, error) {
+ v, _, _ := g.Do("key", func() (string, error) {
    return "bar", nil
})
- useString(v.(string))
+ useString(v)
```
