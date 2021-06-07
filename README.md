# log
Simple, customizable, leveled, zero allocation logging in Go

[![Go](https://github.com/ermanimer/log/actions/workflows/go.yml/badge.svg?branch=main)](https://github.com/ermanimer/log/actions/workflows/go.yml) [![Go Report Card](https://goreportcard.com/badge/github.com/ermanimer/log)](https://goreportcard.com/report/github.com/ermanimer/log)

# Installation
```bash
go get -u github.com/ermanimer/logger
```

# Features
...

# Usage
...

# Logging Levels
 - Debug
 - Info
 - Warning
 - Error
 - Fatal

# Default Parameters
| Parameter | Value |
|:----------|:-----:|
| Time Format | RFC3339 |
| Debug Prefix | debug |
| Info Prefix | info |
| Warning Prefix | warning |
| Error Prefix | error |
| Fatal Prefix | fatal |
| Logging Level | Debug |


# Set Time Format
```go
l.SetTimeFormat(time.RFC3339Nano)
```

# Set Prefixes
```go
l.SetDebugPrefix("DEB")
l.SetDebugPrefix("INF")
l.SetDebugPrefix("WAR")
l.SetDebugPrefix("ERR")
l.SetDebugPrefix("FAT")
```

# Set Logging Level
```go
l.SetLoggingLevel(InfoLevel)
```

# Set Hook Function
```go
l.SetHookFunction(func(prefix, message string) {
  //filter messages with prefix and capture for Sentry.io
  //...
})
```

# Benchmark Tests
**Test Code:**
```go
func BenchmarkDebug(b *testing.B) {
	// create logger
	l := NewLogger(ioutil.Discard)

	// start benchmark test
	b.RunParallel(func(pb *testing.PB) {
		for pb.Next() {
			l.Debug("test")
		}
	})
}

func BenchmarkDebugf(b *testing.B) {
	// create logger
	l := NewLogger(ioutil.Discard)

	// start benchmark test
	b.RunParallel(func(pb *testing.PB) {
		for pb.Next() {
			l.Debugf("%s", "test")
		}
	})
}
```
**Results:**
| Function | Time | Bytes Allocated | Objects Allocated |
|:---------|:----:|:---------------:|:-----------------:|
| Debug | 410.7 ns/op | 4 B/op | 1 allocs/op |
| Debugf | 408.7 ns/op | 4 B/op | 1 allocs/op |
| Info | 404.0 ns/op |  4 B/op | 1 allocs/op |
| Infof | 403.9 ns/op | 4 B/op | 1 allocs/op |
| Warning  | 407.0 ns/op | 4 B/op | 1 allocs/op |
| Warningf | 409.4 ns/op | 4 B/op | 1 allocs/op |
| Error | 404.6 ns/op | 4 B/op | 1 allocs/op |
| Errorf | 406.2 ns/op | 4 B/op	| 1 allocs/op |
| Fatal |  402.1 ns/op | 4 B/op | 1 allocs/op |
| Fatalf | 406.0 ns/op | 4 B/op |	1 allocs/op |
