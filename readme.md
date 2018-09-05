# WGO
Go http server RESTful API 开发框架

<br>

- Add

```go
func main() {
	w := wgo.New()
	w.Add("/",
		func(ctx wgo.Context) error {
			fmt.Println("处理 handleFunc A")
			return wgo.Next
		},
		func(ctx wgo.Context) error {
			fmt.Println("处理 handleFunc B")
			return wgo.Next
		},
		func(ctx wgo.Context) error {
			fmt.Println("处理 handleFunc C")
			return wgo.Next
		},
	)
	w.Start(":2000")
}
```
