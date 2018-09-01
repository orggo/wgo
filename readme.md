# WGO
极致简洁的 HTTP RESTful API 开发框架

<br>

### 开始

```go
package main

import "wgo"

func main() {
	w := wgo.New()
	
	w.Add("/", func(ctx wgo.Context) error {
		return ctx.JSON(200, "你好世界")
	})
	
	w.Start(":2000")
}
```

<br>

### Add & Group

```go
func main() {
    w := wgo.New()
    
    // http://127.0.0.1:2000/v1/v2/demo

	v1 := w.Group("/v1", func(ctx wgo.Context) error {
		fmt.Println("> 处理 handleFunc /v1")

		// 继续执行下一个 handleFunc
		return wgo.Next
	})

	v2 := v1.Group("/v2", func(ctx wgo.Context) error {
		fmt.Println("> 处理 handleFunc /v1/v2")
		return wgo.Next
	})

	v2.Add("/demo",

		func(ctx wgo.Context) error {
			fmt.Println("> 处理 handleFunc /v1/v2/demo: 1")
			return wgo.Next
		},

		func(ctx wgo.Context) error {
			fmt.Println("> 处理 handleFunc /v1/v2/demo: 2")
			return ctx.JSON(200, "你好世界")
		},
	)

	w.Start(":2000")
}
```
```sh
~$ go run main.go
> 处理 handleFunc /v1
> 处理 handleFunc /v1/v2
> 处理 handleFunc /v1/v2/demo: 1
> 处理 handleFunc /v1/v2/demo: 2
```

<br>

预告结束...
