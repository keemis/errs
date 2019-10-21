# errs 

Package errors provides simple error handling primitives.

`go get github.com/keemi-zhou/errs`

The traditional error handling idiom in Go is roughly akin to
```go
if err != nil {
        return err
}
```

## New an error

Using `errs.New` new an error
```go
err := errs.New("system error")
```

Using `errs.NewWithOption` new an error, with some option
```go
// simple
err := errs.NewWithOption(errs.OptMsg("system error"))
// commonly use
err := errs.NewWithOption(errs.OptCode(-5019), errs.OptMsg("system error"))
// has data
err := errs.NewWithOption(errs.OptCode(-5019), errs.OptMsg("system error"), errs.OptData(nil))
```

## Wrap rewrite an error

Using `errs.Wrap` rewrite an error
```go
err = errs.Wrap(err, errs.OptCode(-5019), errs.OptMsg("system error"))
```

## Print an error info

Using `err.Error` print an error message
```go
fmt.Println(err.Error())
// system error
```

Using `err.Printf` print an error some detail
```go
fmt.Printf("%+v \n", err)
// system error
// main.init.0
//         /develop/src/errs/main.go:55
// runtime.doInit
//         /usr/local/go/src/runtime/proc.go:5222
// runtime.main
//         /usr/local/go/src/runtime/proc.go:190
// runtime.goexit
//         /usr/local/go/src/runtime/asm_amd64.s:1357 
```

## Return error info

Using `errs.GetCode` return error code
```go
fmt.Println(errs.GetCode(err))
// 5019
```

Using `errs.GetData` return error data
```go
fmt.Println(errs.GetData(err))
// nil
```

Using `errs.GetStack` return error stack
```go
fmt.Println(errs.GetStack(err))
// main.init.0
//         /develop/src/errs/main.go:55
// runtime.doInit
//         /usr/local/go/src/runtime/proc.go:5222
// runtime.main
//         /usr/local/go/src/runtime/proc.go:190
// runtime.goexit
//         /usr/local/go/src/runtime/asm_amd64.s:1357 
```
