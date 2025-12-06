# Things-Kit Testing

**Testing Utilities for Things-Kit**

Testing utilities to simplify integration testing of Things-Kit applications.

## Installation

```bash
go get github.com/things-kit/things-kit-testing
```

## Features

- Test-friendly logger implementation
- Fx application testing helpers
- Integration test utilities

## Quick Start

```go
package myservice_test

import (
    "testing"
    "github.com/things-kit/things-kit-testing"
    "go.uber.org/fx"
)

func TestMyService(t *testing.T) {
    app := testing.NewTestApp(t,
        viperconfig.Module,
        logging.Module,
        fx.Provide(NewMyService),
        fx.Invoke(func(svc *MyService) {
            // Test your service
            result := svc.DoSomething()
            if result != expected {
                t.Errorf("expected %v, got %v", expected, result)
            }
        }),
    )
    
    app.RequireStart()
    app.RequireStop()
}
```

## Test Logger

The testing module provides a test-friendly logger:

```go
func TestWithLogging(t *testing.T) {
    logger := testing.NewTestLogger(t)
    
    logger.Info("test message", log.Field{Key: "key", Value: "value"})
    // Output goes to t.Log()
}
```

## License

MIT License - see LICENSE file for details
