# Module 1: Go Fundamentals - Super Complete Guide

## 🎯 Learning Objectives

Setelah menyelesaikan module ini, Anda akan mampu:

- ✅ Setup environment Go development yang optimal
- ✅ Menulis, compile, dan run program Go
- ✅ Memahami Go syntax dan struktur program
- ✅ Bekerja dengan semua tipe data dasar Go
- ✅ Menggunakan control flow statements dengan efektif
- ✅ Debug dan troubleshoot program Go sederhana
- ✅ Apply Go best practices untuk code quality

## 📚 Prerequisites

- [ ] Komputer dengan OS Windows/Mac/Linux
- [ ] Akses internet untuk download dependencies
- [ ] Basic understanding programming concepts
- [ ] Willingness to practice 1-2 hours daily

---

## 🔧 Section 1: Environment Setup (Super Complete)

### 1.1 Install Go - Step by Step Guide

#### Windows Installation

- [ ] **Download Go**: Pergi ke [golang.org/dl](https://golang.org/dl/)
- [ ] **Choose Version**: Download latest stable version (1.21+ recommended)
- [ ] **Run Installer**: Double-click .msi file
- [ ] **Installation Path**: Default `C:\Program Files\Go` (recommended)
- [ ] **Environment Variables**: Installer will set automatically
- [ ] **Verify Installation**: Open PowerShell dan run:

```powershell
go version
# Expected output: go version go1.21.x windows/amd64
```

#### Mac Installation

- [ ] **Option 1 - Installer Package**:
  - Download .pkg file dari golang.org
  - Run installer dengan default settings
- [ ] **Option 2 - Homebrew**:

```bash
brew install go
```

- [ ] **Verify Installation**:

```bash
go version
which go
# Should show: /usr/local/go/bin/go
```

#### Linux Installation

- [ ] **Download tar.gz**: Dari golang.org
- [ ] **Extract dan Install**:

```bash
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.21.x.linux-amd64.tar.gz
```

- [ ] **Update PATH**: Add to `~/.bashrc` atau `~/.zshrc`:

```bash
export PATH=$PATH:/usr/local/go/bin
```

- [ ] **Reload Shell**: `source ~/.bashrc`
- [ ] **Verify**: `go version`

### 1.2 Go Environment Variables - Deep Dive

#### Essential Environment Variables

- [ ] **GOROOT**: Go installation directory

```bash
go env GOROOT
# Shows where Go is installed
```

- [ ] **GOPATH**: Workspace directory (legacy, optional for modules)

```bash
go env GOPATH
# Default: ~/go (Unix) or %USERPROFILE%\go (Windows)
```

- [ ] **GOPROXY**: Module proxy settings

```bash
go env GOPROXY
# Default: https://proxy.golang.org,direct
```

- [ ] **GOSUMDB**: Checksum database

```bash
go env GOSUMDB
# Default: sum.golang.org
```

#### Advanced Configuration

- [ ] **Set Custom GOPATH** (if needed):

```bash
# Windows
set GOPATH=D:\MyGoWorkspace
# Unix
export GOPATH=$HOME/my-go-workspace
```

- [ ] **Private Module Configuration**:

```bash
go env -w GOPRIVATE=github.com/yourcompany/*
go env -w GONOPROXY=github.com/yourcompany/*
go env -w GONOSUMDB=github.com/yourcompany/*
```

### 1.3 Development Environment Setup

#### VS Code Setup (Recommended)

- [ ] **Install VS Code**: Download dari [code.visualstudio.com](https://code.visualstudio.com)
- [ ] **Install Go Extension**:
  1. Open VS Code
  2. Go to Extensions (Ctrl+Shift+X)
  3. Search "Go" oleh Google
  4. Install extension
- [ ] **Install Go Tools**: Command Palette (Ctrl+Shift+P) → "Go: Install/Update Tools"
  - [ ] gopls (language server)
  - [ ] dlv (debugger)
  - [ ] staticcheck (linter)
  - [ ] goimports (formatter)
  - [ ] gotests (test generator)
  - [ ] gomodifytags (struct tag editor)
  - [ ] impl (interface implementer)
  - [ ] goplay (Go playground)

#### VS Code Settings Optimization

```json
{
  "go.useLanguageServer": true,
  "go.formatTool": "goimports",
  "go.lintTool": "staticcheck",
  "go.vetOnSave": "package",
  "go.buildOnSave": "package",
  "go.lintOnSave": "package",
  "go.coverOnSave": true,
  "go.testFlags": ["-v"],
  "go.buildFlags": [],
  "go.testEnvVars": {},
  "go.generateTestsFlags": ["-parallel"]
}
```

#### Alternative IDEs

- [ ] **GoLand by JetBrains**: Professional IDE (paid)
- [ ] **Vim/Neovim**: Dengan vim-go plugin
- [ ] **Sublime Text**: Dengan GoSublime package
- [ ] **Atom**: Dengan go-plus package (deprecated)

### 1.4 Testing Installation

#### Create Test Workspace

```bash
mkdir -p ~/go-learning/hello-world
cd ~/go-learning/hello-world
```

#### Initialize Go Module

```bash
go mod init hello-world
# Creates go.mod file
```

#### Create First Program

```go
// main.go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go World!")
    fmt.Printf("Go version: %s\n", getGoVersion())
}

func getGoVersion() string {
    return "1.21.x" // Replace with actual version check
}
```

#### Test Commands

- [ ] **Run Program**: `go run main.go`
- [ ] **Build Executable**: `go build`
- [ ] **Install Program**: `go install`
- [ ] **Format Code**: `go fmt`
- [ ] **Check for Issues**: `go vet`

---

## 📖 Section 2: Go Program Structure (Complete Analysis)

### 2.1 Package System - Deep Dive

#### Package Declaration Rules

- [ ] **Main Package**: Entry point untuk executable programs

```go
package main // Executable program
```

- [ ] **Library Package**: Reusable code modules

```go
package utils // Library package
package models // Library package
```

#### Package Naming Conventions

- [ ] **Use lowercase**: `package user`, not `package User`
- [ ] **Single word**: `package auth`, not `package authentication`
- [ ] **Descriptive**: `package database`, not `package db`
- [ ] **No underscores**: `package httputil`, not `package http_util`

#### Package Organization Best Practices

```
project/
├── main.go           // package main
├── auth/
│   ├── auth.go       // package auth
│   └── token.go      // package auth
├── models/
│   ├── user.go       // package models
│   └── product.go    // package models
└── utils/
    └── helpers.go    // package utils
```

### 2.2 Import System - Advanced Usage

#### Basic Import Syntax

```go
import "fmt"           // Single import
import "net/http"      // Standard library
import "github.com/gin-gonic/gin" // External package
```

#### Multiple Imports

```go
import (
    "fmt"
    "os"
    "time"

    "github.com/gin-gonic/gin"
    "github.com/lib/pq"
)
```

#### Import Aliases

```go
import (
    "fmt"
    f "fmt"            // Alias import
    . "fmt"            // Dot import (avoid in production)
    _ "image/png"      // Blank import for side effects
)
```

#### Import Organization

```go
import (
    // Standard library imports
    "context"
    "fmt"
    "net/http"
    "time"

    // Third-party imports
    "github.com/gin-gonic/gin"
    "github.com/lib/pq"

    // Local imports
    "myproject/auth"
    "myproject/models"
)
```

### 2.3 Main Function - Complete Understanding

#### Basic Main Function

```go
func main() {
    // Program entry point
    fmt.Println("Program started")

    // Your application logic here

    fmt.Println("Program finished")
}
```

#### Command Line Arguments

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    // Get command line arguments
    args := os.Args
    fmt.Printf("Program name: %s\n", args[0])

    if len(args) > 1 {
        fmt.Printf("Arguments: %v\n", args[1:])
    }
}
```

#### Exit Codes

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    success := doSomething()

    if !success {
        fmt.Println("Operation failed")
        os.Exit(1) // Exit with error code
    }

    fmt.Println("Operation successful")
    // os.Exit(0) // Implicit success exit
}

func doSomething() bool {
    // Your logic here
    return true
}
```

### 2.4 Exported vs Unexported Identifiers

#### Capitalization Rules

```go
package mypackage

// Exported (public) - can be used by other packages
type User struct {
    Name  string // Exported field
    Email string // Exported field
    age   int    // Unexported field (private)
}

// Exported function
func CreateUser(name, email string) *User {
    return &User{
        Name:  name,
        Email: email,
        age:   0,
    }
}

// Unexported function (private)
func validateEmail(email string) bool {
    // Internal validation logic
    return true
}
```

#### Best Practices

- [ ] **Start with lowercase**: Internal functionality
- [ ] **Start with uppercase**: Public API
- [ ] **Minimize exported surface**: Only expose what's necessary
- [ ] **Document exported items**: Use godoc comments

---

## 🔢 Section 3: Variables and Data Types (Comprehensive)

### 3.1 Variable Declaration - All Methods

#### Method 1: var Keyword (Explicit)

```go
package main

import "fmt"

func main() {
    // Explicit type declaration
    var name string
    var age int
    var isActive bool

    // Assignment after declaration
    name = "John Doe"
    age = 25
    isActive = true

    fmt.Printf("Name: %s, Age: %d, Active: %t\n", name, age, isActive)
}
```

#### Method 2: var with Initialization

```go
func main() {
    // Declaration with initialization
    var name string = "Jane Doe"
    var age int = 30
    var isActive bool = true

    // Type inference
    var city = "Jakarta"      // string
    var population = 10000000 // int
    var isCapital = true      // bool

    fmt.Printf("City: %s, Population: %d, Capital: %t\n",
               city, population, isCapital)
}
```

#### Method 3: Short Declaration (:=)

```go
func main() {
    // Short variable declaration (only inside functions)
    name := "Bob Smith"
    age := 35
    isActive := false

    // Multiple variable declaration
    firstName, lastName := "Alice", "Johnson"
    x, y, z := 1, 2, 3

    fmt.Printf("Name: %s %s, Age: %d\n", firstName, lastName, age)
    fmt.Printf("Coordinates: (%d, %d, %d)\n", x, y, z)
}
```

#### Method 4: Multiple Variable Declaration

```go
func main() {
    // Multiple var declarations
    var (
        name     string = "Charlie"
        age      int    = 40
        isActive bool   = true
        salary   float64
    )

    // Multiple short declarations
    a, b, c := 1, 2.5, "hello"

    fmt.Printf("Employee: %s, Age: %d, Active: %t, Salary: %.2f\n",
               name, age, isActive, salary)
    fmt.Printf("Values: %d, %.1f, %s\n", a, b, c)
}
```

### 3.2 Data Types - Complete Reference

#### Numeric Types - Integer

```go
package main

import (
    "fmt"
    "unsafe"
)

func main() {
    // Signed integers
    var int8Val int8 = -128        // -128 to 127
    var int16Val int16 = -32768    // -32768 to 32767
    var int32Val int32 = -2147483648
    var int64Val int64 = -9223372036854775808

    // Unsigned integers
    var uint8Val uint8 = 255       // 0 to 255
    var uint16Val uint16 = 65535   // 0 to 65535
    var uint32Val uint32 = 4294967295
    var uint64Val uint64 = 18446744073709551615

    // Architecture-dependent
    var intVal int = -2147483648   // 32 or 64 bit
    var uintVal uint = 4294967295  // 32 or 64 bit
    var uintptrVal uintptr         // For pointers

    // Special aliases
    var byteVal byte = 255         // alias for uint8
    var runeVal rune = '🎯'        // alias for int32 (Unicode)

    fmt.Printf("int8: %d (size: %d bytes)\n", int8Val, unsafe.Sizeof(int8Val))
    fmt.Printf("int16: %d (size: %d bytes)\n", int16Val, unsafe.Sizeof(int16Val))
    fmt.Printf("rune: %d '%c' (size: %d bytes)\n", runeVal, runeVal, unsafe.Sizeof(runeVal))
}
```

#### Numeric Types - Floating Point

```go
func main() {
    // Floating point numbers
    var float32Val float32 = 3.14159265359 // ~6 decimal precision
    var float64Val float64 = 3.14159265359 // ~15 decimal precision

    // Scientific notation
    var scientific1 float64 = 1.23e10  // 12300000000
    var scientific2 float64 = 1.23e-4  // 0.000123

    // Complex numbers
    var complex64Val complex64 = 1 + 2i
    var complex128Val complex128 = 3.14 + 2.71i

    fmt.Printf("float32: %.10f\n", float32Val)
    fmt.Printf("float64: %.15f\n", float64Val)
    fmt.Printf("scientific: %.2e, %.6f\n", scientific1, scientific2)
    fmt.Printf("complex64: %v\n", complex64Val)
    fmt.Printf("complex128: %v\n", complex128Val)

    // Complex number operations
    real := real(complex128Val)
    imag := imag(complex128Val)
    fmt.Printf("Real: %.2f, Imaginary: %.2f\n", real, imag)
}
```

#### String Type - Advanced

```go
import (
    "fmt"
    "strings"
    "unicode/utf8"
)

func main() {
    // String literals
    var name string = "Golang"
    var message string = `This is a
    multi-line string
    with preserved formatting`

    // String with escape sequences
    var escaped string = "Hello\nWorld\t\"Go\"\\"

    // Unicode strings
    var unicode string = "Hello, 世界! 🌍"

    // Raw string literals
    var rawString string = `C:\Users\Name\Documents\file.txt`

    fmt.Printf("Name: %s (length: %d)\n", name, len(name))
    fmt.Printf("Message:\n%s\n", message)
    fmt.Printf("Escaped: %s\n", escaped)
    fmt.Printf("Unicode: %s\n", unicode)
    fmt.Printf("Unicode length (bytes): %d\n", len(unicode))
    fmt.Printf("Unicode length (runes): %d\n", utf8.RuneCountInString(unicode))
    fmt.Printf("Raw string: %s\n", rawString)

    // String operations
    fmt.Printf("Uppercase: %s\n", strings.ToUpper(name))
    fmt.Printf("Contains 'Go': %t\n", strings.Contains(name, "Go"))
    fmt.Printf("Index of 'lang': %d\n", strings.Index(name, "lang"))
}
```

#### Boolean Type

```go
func main() {
    // Boolean values
    var isTrue bool = true
    var isFalse bool = false
    var defaultBool bool // false (zero value)

    // Boolean expressions
    var result1 bool = 10 > 5
    var result2 bool = "hello" == "world"
    var result3 bool = !isTrue

    fmt.Printf("isTrue: %t\n", isTrue)
    fmt.Printf("isFalse: %t\n", isFalse)
    fmt.Printf("defaultBool: %t\n", defaultBool)
    fmt.Printf("10 > 5: %t\n", result1)
    fmt.Printf("hello == world: %t\n", result2)
    fmt.Printf("!isTrue: %t\n", result3)

    // Boolean operations
    fmt.Printf("true && false: %t\n", true && false)
    fmt.Printf("true || false: %t\n", true || false)
    fmt.Printf("!true: %t\n", !true)
}
```

### 3.3 Zero Values - Deep Understanding

#### Zero Values Table

```go
func main() {
    // Numeric types
    var intZero int           // 0
    var floatZero float64     // 0.0
    var complexZero complex128 // (0+0i)

    // String type
    var stringZero string     // ""

    // Boolean type
    var boolZero bool         // false

    // Pointer types
    var pointerZero *int      // nil

    // Function types
    var funcZero func()       // nil

    // Interface types
    var interfaceZero interface{} // nil

    // Channel types
    var chanZero chan int     // nil

    // Slice types
    var sliceZero []int       // nil

    // Map types
    var mapZero map[string]int // nil

    fmt.Printf("int zero: %d\n", intZero)
    fmt.Printf("float zero: %f\n", floatZero)
    fmt.Printf("complex zero: %v\n", complexZero)
    fmt.Printf("string zero: '%s'\n", stringZero)
    fmt.Printf("bool zero: %t\n", boolZero)
    fmt.Printf("pointer zero: %v\n", pointerZero)
    fmt.Printf("function zero: %v\n", funcZero)
    fmt.Printf("interface zero: %v\n", interfaceZero)
    fmt.Printf("channel zero: %v\n", chanZero)
    fmt.Printf("slice zero: %v\n", sliceZero)
    fmt.Printf("map zero: %v\n", mapZero)
}
```

### 3.4 Type Conversion - Complete Guide

#### Numeric Conversions

```go
import (
    "fmt"
    "strconv"
)

func main() {
    // Basic numeric conversions
    var intVal int = 42
    var floatVal float64 = float64(intVal)
    var float32Val float32 = float32(floatVal)
    var backToInt int = int(floatVal)

    fmt.Printf("int to float64: %d -> %.2f\n", intVal, floatVal)
    fmt.Printf("float64 to float32: %.2f -> %.2f\n", floatVal, float32Val)
    fmt.Printf("float64 to int: %.2f -> %d\n", floatVal, backToInt)

    // String conversions
    var str string = "123"
    var num int
    var err error

    // String to int
    num, err = strconv.Atoi(str)
    if err != nil {
        fmt.Printf("Error converting string to int: %v\n", err)
    } else {
        fmt.Printf("String to int: '%s' -> %d\n", str, num)
    }

    // Int to string
    var intToStr string = strconv.Itoa(num)
    fmt.Printf("Int to string: %d -> '%s'\n", num, intToStr)

    // Advanced string conversions
    var floatStr string = "3.14159"
    var floatFromStr float64
    floatFromStr, err = strconv.ParseFloat(floatStr, 64)
    if err != nil {
        fmt.Printf("Error: %v\n", err)
    } else {
        fmt.Printf("String to float: '%s' -> %.5f\n", floatStr, floatFromStr)
    }

    // Float to string
    var floatToStr string = strconv.FormatFloat(floatFromStr, 'f', 2, 64)
    fmt.Printf("Float to string: %.5f -> '%s'\n", floatFromStr, floatToStr)

    // Boolean conversions
    var boolStr string = "true"
    var boolFromStr bool
    boolFromStr, err = strconv.ParseBool(boolStr)
    if err != nil {
        fmt.Printf("Error: %v\n", err)
    } else {
        fmt.Printf("String to bool: '%s' -> %t\n", boolStr, boolFromStr)
    }
}
```

### 3.5 Constants - Advanced Usage

#### Basic Constants

```go
package main

import "fmt"

const (
    // Untyped constants
    Pi       = 3.14159265359
    E        = 2.71828182846
    GoldenRatio = 1.61803398875

    // Typed constants
    MaxAge    int     = 150
    MinAge    int     = 0
    Name      string  = "Go Language"
    IsActive  bool    = true
)

func main() {
    fmt.Printf("Pi: %.10f\n", Pi)
    fmt.Printf("E: %.10f\n", E)
    fmt.Printf("Golden Ratio: %.10f\n", GoldenRatio)
    fmt.Printf("Age range: %d - %d\n", MinAge, MaxAge)
    fmt.Printf("Language: %s, Active: %t\n", Name, IsActive)
}
```

#### iota - Auto-incrementing Constants

```go
package main

import "fmt"

// Basic iota usage
const (
    Sunday = iota    // 0
    Monday           // 1
    Tuesday          // 2
    Wednesday        // 3
    Thursday         // 4
    Friday           // 5
    Saturday         // 6
)

// iota with expressions
const (
    _  = iota             // 0 (ignored)
    KB = 1 << (10 * iota) // 1 << (10*1) = 1024
    MB                    // 1 << (10*2) = 1048576
    GB                    // 1 << (10*3) = 1073741824
    TB                    // 1 << (10*4) = 1099511627776
)

// iota with custom values
const (
    StatusPending = iota + 100  // 100
    StatusActive                // 101
    StatusInactive              // 102
    StatusSuspended             // 103
)

// Multiple iota in same block
const (
    a, b = iota + 1, iota + 2  // a=1, b=2
    c, d                       // c=2, d=3
    e, f                       // e=3, f=4
)

func main() {
    fmt.Printf("Days: Sunday=%d, Monday=%d, Saturday=%d\n", Sunday, Monday, Saturday)
    fmt.Printf("Storage: KB=%d, MB=%d, GB=%d, TB=%d\n", KB, MB, GB, TB)
    fmt.Printf("Status: Pending=%d, Active=%d, Suspended=%d\n", StatusPending, StatusActive, StatusSuspended)
    fmt.Printf("Multiple: a=%d, b=%d, c=%d, d=%d, e=%d, f=%d\n", a, b, c, d, e, f)
}
```

---

## 🔄 Section 4: Control Flow (Comprehensive)

### 4.1 If Statements - All Variations

#### Basic If Statements

```go
package main

import "fmt"

func main() {
    score := 85

    // Simple if
    if score >= 90 {
        fmt.Println("Excellent!")
    }

    // If-else
    if score >= 60 {
        fmt.Println("Pass")
    } else {
        fmt.Println("Fail")
    }

    // If-else if-else chain
    if score >= 90 {
        fmt.Println("Grade A")
    } else if score >= 80 {
        fmt.Println("Grade B")
    } else if score >= 70 {
        fmt.Println("Grade C")
    } else if score >= 60 {
        fmt.Println("Grade D")
    } else {
        fmt.Println("Grade F")
    }
}
```

#### If with Short Statement

```go
import (
    "fmt"
    "math"
    "strconv"
)

func main() {
    // If with short statement
    if num := 42; num%2 == 0 {
        fmt.Printf("%d is even\n", num)
    } else {
        fmt.Printf("%d is odd\n", num)
    }

    // Multiple conditions with short statement
    if x, y := 10, 20; x < y && x > 0 {
        fmt.Printf("%d is less than %d and positive\n", x, y)
    }

    // Error handling pattern
    if value, err := strconv.Atoi("123"); err != nil {
        fmt.Printf("Error: %v\n", err)
    } else {
        fmt.Printf("Converted value: %d\n", value)
    }

    // Function call in if condition
    if result := math.Sqrt(16); result == 4 {
        fmt.Printf("Square root of 16 is %.0f\n", result)
    }
}
```

#### Complex Conditional Logic

```go
func main() {
    age := 25
    hasLicense := true
    hasInsurance := true
    hasViolations := false

    // Complex boolean expressions
    if age >= 18 && hasLicense && hasInsurance && !hasViolations {
        fmt.Println("Eligible to drive")
    } else {
        fmt.Println("Not eligible to drive")

        // Detailed feedback
        if age < 18 {
            fmt.Println("- Too young")
        }
        if !hasLicense {
            fmt.Println("- No license")
        }
        if !hasInsurance {
            fmt.Println("- No insurance")
        }
        if hasViolations {
            fmt.Println("- Has violations")
        }
    }

    // Nested if statements
    username := "admin"
    password := "secret123"

    if username != "" {
        if len(username) >= 3 {
            if password != "" {
                if len(password) >= 8 {
                    fmt.Println("Valid credentials")
                } else {
                    fmt.Println("Password too short")
                }
            } else {
                fmt.Println("Password required")
            }
        } else {
            fmt.Println("Username too short")
        }
    } else {
        fmt.Println("Username required")
    }
}
```

### 4.2 Switch Statements - Advanced Usage

#### Basic Switch

```go
func main() {
    day := "Tuesday"

    switch day {
    case "Monday":
        fmt.Println("Start of work week")
    case "Tuesday", "Wednesday", "Thursday":
        fmt.Println("Middle of work week")
    case "Friday":
        fmt.Println("TGIF!")
    case "Saturday", "Sunday":
        fmt.Println("Weekend")
    default:
        fmt.Println("Invalid day")
    }
}
```

#### Switch with Expressions

```go
import (
    "fmt"
    "time"
)

func main() {
    score := 85

    // Switch with expression
    switch {
    case score >= 90:
        fmt.Println("Grade A - Excellent!")
    case score >= 80:
        fmt.Println("Grade B - Good!")
    case score >= 70:
        fmt.Println("Grade C - Average")
    case score >= 60:
        fmt.Println("Grade D - Below Average")
    default:
        fmt.Println("Grade F - Fail")
    }

    // Switch with time
    hour := time.Now().Hour()
    switch {
    case hour < 12:
        fmt.Println("Good morning!")
    case hour < 17:
        fmt.Println("Good afternoon!")
    case hour < 21:
        fmt.Println("Good evening!")
    default:
        fmt.Println("Good night!")
    }
}
```

#### Switch with Short Statement

```go
import (
    "fmt"
    "math/rand"
    "time"
)

func main() {
    // Switch with short statement
    switch num := rand.Intn(10); {
    case num < 3:
        fmt.Printf("%d is small\n", num)
    case num < 7:
        fmt.Printf("%d is medium\n", num)
    default:
        fmt.Printf("%d is large\n", num)
    }

    // Type switch (will cover in later modules)
    var x interface{} = 42
    switch v := x.(type) {
    case int:
        fmt.Printf("Integer: %d\n", v)
    case string:
        fmt.Printf("String: %s\n", v)
    case bool:
        fmt.Printf("Boolean: %t\n", v)
    default:
        fmt.Printf("Unknown type: %T\n", v)
    }
}
```

#### Fallthrough

```go
func main() {
    grade := "B"

    switch grade {
    case "A":
        fmt.Println("Excellent performance!")
        fallthrough
    case "B":
        fmt.Println("Good performance!")
        fallthrough
    case "C":
        fmt.Println("Satisfactory performance")
        fallthrough
    case "D":
        fmt.Println("Needs improvement")
    case "F":
        fmt.Println("Failing grade")
    default:
        fmt.Println("Invalid grade")
    }

    // Output for grade "B":
    // Good performance!
    // Satisfactory performance
    // Needs improvement
}
```

### 4.3 For Loops - All Variations

#### Classic For Loop

```go
func main() {
    // Basic for loop
    fmt.Println("Counting from 1 to 5:")
    for i := 1; i <= 5; i++ {
        fmt.Printf("%d ", i)
    }
    fmt.Println()

    // Reverse counting
    fmt.Println("Countdown from 5 to 1:")
    for i := 5; i >= 1; i-- {
        fmt.Printf("%d ", i)
    }
    fmt.Println()

    // Step by 2
    fmt.Println("Even numbers from 2 to 10:")
    for i := 2; i <= 10; i += 2 {
        fmt.Printf("%d ", i)
    }
    fmt.Println()

    // Multiple variables
    fmt.Println("Fibonacci-like sequence:")
    for i, j := 0, 1; i < 10; i, j = i+j, i {
        fmt.Printf("%d ", i)
    }
    fmt.Println()
}
```

#### While-style For Loop

```go
import (
    "fmt"
    "math/rand"
    "time"
)

func main() {
    // While-style loop
    count := 0
    for count < 5 {
        fmt.Printf("Count: %d\n", count)
        count++
    }

    // While with condition check
    number := 1
    for number <= 100 {
        fmt.Printf("%d ", number)
        number *= 2
    }
    fmt.Println()

    // Simulating do-while
    rand.Seed(time.Now().UnixNano())
    for {
        randomNum := rand.Intn(10)
        fmt.Printf("Random: %d\n", randomNum)
        if randomNum == 7 {
            fmt.Println("Lucky number 7! Breaking...")
            break
        }
    }
}
```

#### Infinite Loop with Break/Continue

```go
import (
    "fmt"
    "time"
)

func main() {
    // Infinite loop with break
    counter := 0
    for {
        counter++
        if counter > 10 {
            break
        }
        fmt.Printf("Counter: %d\n", counter)
    }

    // Loop with continue
    fmt.Println("Even numbers from 1 to 10:")
    for i := 1; i <= 10; i++ {
        if i%2 != 0 {
            continue // Skip odd numbers
        }
        fmt.Printf("%d ", i)
    }
    fmt.Println()

    // Real-world example: server-like loop
    fmt.Println("Simulating server (will run for 3 iterations):")
    iteration := 0
    for {
        iteration++
        fmt.Printf("Server iteration %d\n", iteration)

        if iteration >= 3 {
            fmt.Println("Shutting down server...")
            break
        }

        time.Sleep(1 * time.Second)
    }
}
```

#### Nested Loops

```go
func main() {
    // Multiplication table
    fmt.Println("Multiplication Table (5x5):")
    for i := 1; i <= 5; i++ {
        for j := 1; j <= 5; j++ {
            fmt.Printf("%2d ", i*j)
        }
        fmt.Println()
    }

    // Pattern printing
    fmt.Println("\nStar Pattern:")
    for i := 1; i <= 5; i++ {
        for j := 1; j <= i; j++ {
            fmt.Print("* ")
        }
        fmt.Println()
    }

    // Number triangle
    fmt.Println("\nNumber Triangle:")
    for i := 1; i <= 5; i++ {
        for j := 1; j <= i; j++ {
            fmt.Printf("%d ", j)
        }
        fmt.Println()
    }
}
```

#### Labeled Breaks and Continues

```go
func main() {
    // Labeled break
    fmt.Println("Finding first pair that sums to 10:")
outer:
    for i := 1; i <= 5; i++ {
        for j := 1; j <= 5; j++ {
            if i+j == 10 {
                fmt.Printf("Found: %d + %d = 10\n", i, j)
                break outer // Break out of both loops
            }
        }
    }

    // Labeled continue
    fmt.Println("\nSkipping when i equals j:")
outer2:
    for i := 1; i <= 3; i++ {
        for j := 1; j <= 3; j++ {
            if i == j {
                continue outer2 // Continue outer loop
            }
            fmt.Printf("(%d,%d) ", i, j)
        }
    }
    fmt.Println()
}
```

---

## 🛠️ Section 5: Hands-on Practice Programs

### 5.1 Basic Calculator

```go
package main

import (
    "fmt"
    "strconv"
    "strings"
)

func main() {
    for {
        fmt.Println("\n=== Go Calculator ===")
        fmt.Println("1. Addition (+)")
        fmt.Println("2. Subtraction (-)")
        fmt.Println("3. Multiplication (*)")
        fmt.Println("4. Division (/)")
        fmt.Println("5. Modulus (%)")
        fmt.Println("6. Power (^)")
        fmt.Println("7. Exit")
        fmt.Print("Choose operation (1-7): ")

        var choice string
        fmt.Scanln(&choice)

        if choice == "7" {
            fmt.Println("Goodbye!")
            break
        }

        if choice < "1" || choice > "6" {
            fmt.Println("Invalid choice! Please try again.")
            continue
        }

        fmt.Print("Enter first number: ")
        var num1Str string
        fmt.Scanln(&num1Str)

        fmt.Print("Enter second number: ")
        var num2Str string
        fmt.Scanln(&num2Str)

        num1, err1 := strconv.ParseFloat(num1Str, 64)
        num2, err2 := strconv.ParseFloat(num2Str, 64)

        if err1 != nil || err2 != nil {
            fmt.Println("Invalid number input! Please try again.")
            continue
        }

        var result float64
        var operation string

        switch choice {
        case "1":
            result = num1 + num2
            operation = "+"
        case "2":
            result = num1 - num2
            operation = "-"
        case "3":
            result = num1 * num2
            operation = "*"
        case "4":
            if num2 == 0 {
                fmt.Println("Error: Division by zero!")
                continue
            }
            result = num1 / num2
            operation = "/"
        case "5":
            if num2 == 0 {
                fmt.Println("Error: Modulus by zero!")
                continue
            }
            result = float64(int(num1) % int(num2))
            operation = "%"
        case "6":
            result = power(num1, num2)
            operation = "^"
        }

        fmt.Printf("Result: %.2f %s %.2f = %.2f\n", num1, operation, num2, result)
    }
}

func power(base, exponent float64) float64 {
    if exponent == 0 {
        return 1
    }
    if exponent == 1 {
        return base
    }

    result := 1.0
    exp := int(exponent)
    for i := 0; i < exp; i++ {
        result *= base
    }
    return result
}
```

### 5.2 Number Guessing Game

```go
package main

import (
    "fmt"
    "math/rand"
    "strconv"
    "time"
)

func main() {
    rand.Seed(time.Now().UnixNano())

    for {
        fmt.Println("\n=== Number Guessing Game ===")
        fmt.Println("1. Easy (1-10)")
        fmt.Println("2. Medium (1-50)")
        fmt.Println("3. Hard (1-100)")
        fmt.Println("4. Exit")
        fmt.Print("Choose difficulty: ")

        var choice string
        fmt.Scanln(&choice)

        if choice == "4" {
            fmt.Println("Thanks for playing!")
            break
        }

        var maxNum, maxAttempts int
        var difficulty string

        switch choice {
        case "1":
            maxNum, maxAttempts, difficulty = 10, 4, "Easy"
        case "2":
            maxNum, maxAttempts, difficulty = 50, 7, "Medium"
        case "3":
            maxNum, maxAttempts, difficulty = 100, 10, "Hard"
        default:
            fmt.Println("Invalid choice!")
            continue
        }

        playGame(maxNum, maxAttempts, difficulty)
    }
}

func playGame(maxNum, maxAttempts int, difficulty string) {
    secretNumber := rand.Intn(maxNum) + 1
    attempts := 0

    fmt.Printf("\n%s Mode: Guess the number between 1 and %d\n", difficulty, maxNum)
    fmt.Printf("You have %d attempts.\n\n", maxAttempts)

    for attempts < maxAttempts {
        attempts++
        fmt.Printf("Attempt %d/%d: ", attempts, maxAttempts)

        var guessStr string
        fmt.Scanln(&guessStr)

        guess, err := strconv.Atoi(guessStr)
        if err != nil {
            fmt.Println("Please enter a valid number!")
            attempts-- // Don't count invalid input as attempt
            continue
        }

        if guess < 1 || guess > maxNum {
            fmt.Printf("Please enter a number between 1 and %d!\n", maxNum)
            attempts-- // Don't count invalid range as attempt
            continue
        }

        if guess == secretNumber {
            fmt.Printf("🎉 Congratulations! You guessed it in %d attempts!\n", attempts)
            return
        } else if guess < secretNumber {
            fmt.Println("📈 Too low!")
        } else {
            fmt.Println("📉 Too high!")
        }

        // Give hints for remaining attempts
        remaining := maxAttempts - attempts
        if remaining > 0 {
            if remaining == 1 {
                fmt.Printf("💡 Last chance! The number is between %d and %d\n",
                    max(1, secretNumber-5), min(maxNum, secretNumber+5))
            } else if remaining == 2 {
                fmt.Printf("💡 Hint: The number is %s\n",
                    map[bool]string{true: "even", false: "odd"}[secretNumber%2 == 0])
            }
        }
    }

    fmt.Printf("😞 Game over! The number was %d\n", secretNumber)
}

func max(a, b int) int {
    if a > b {
        return a
    }
    return b
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

### 5.3 Grade Management System

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    var students map[string][]float64 = make(map[string][]float64)

    for {
        fmt.Println("\n=== Student Grade Management ===")
        fmt.Println("1. Add Student")
        fmt.Println("2. Add Grade")
        fmt.Println("3. View Student Grades")
        fmt.Println("4. Calculate Average")
        fmt.Println("5. List All Students")
        fmt.Println("6. Student Statistics")
        fmt.Println("7. Exit")
        fmt.Print("Choose option: ")

        var choice string
        fmt.Scanln(&choice)

        switch choice {
        case "1":
            addStudent(students)
        case "2":
            addGrade(students)
        case "3":
            viewGrades(students)
        case "4":
            calculateAverage(students)
        case "5":
            listStudents(students)
        case "6":
            studentStatistics(students)
        case "7":
            fmt.Println("Goodbye!")
            return
        default:
            fmt.Println("Invalid option!")
        }
    }
}

func addStudent(students map[string][]float64) {
    fmt.Print("Enter student name: ")
    var name string
    fmt.Scanln(&name)

    if name == "" {
        fmt.Println("Name cannot be empty!")
        return
    }

    if _, exists := students[name]; exists {
        fmt.Printf("Student %s already exists!\n", name)
        return
    }

    students[name] = make([]float64, 0)
    fmt.Printf("Student %s added successfully!\n", name)
}

func addGrade(students map[string][]float64) {
    if len(students) == 0 {
        fmt.Println("No students found! Add a student first.")
        return
    }

    fmt.Print("Enter student name: ")
    var name string
    fmt.Scanln(&name)

    grades, exists := students[name]
    if !exists {
        fmt.Printf("Student %s not found!\n", name)
        return
    }

    fmt.Print("Enter grade (0-100): ")
    var gradeStr string
    fmt.Scanln(&gradeStr)

    grade, err := strconv.ParseFloat(gradeStr, 64)
    if err != nil {
        fmt.Println("Invalid grade! Please enter a number.")
        return
    }

    if grade < 0 || grade > 100 {
        fmt.Println("Grade must be between 0 and 100!")
        return
    }

    students[name] = append(grades, grade)
    fmt.Printf("Grade %.2f added for %s\n", grade, name)
}

func viewGrades(students map[string][]float64) {
    if len(students) == 0 {
        fmt.Println("No students found!")
        return
    }

    fmt.Print("Enter student name: ")
    var name string
    fmt.Scanln(&name)

    grades, exists := students[name]
    if !exists {
        fmt.Printf("Student %s not found!\n", name)
        return
    }

    if len(grades) == 0 {
        fmt.Printf("%s has no grades yet.\n", name)
        return
    }

    fmt.Printf("\nGrades for %s:\n", name)
    for i, grade := range grades {
        fmt.Printf("  %d. %.2f (%s)\n", i+1, grade, getLetterGrade(grade))
    }
}

func calculateAverage(students map[string][]float64) {
    if len(students) == 0 {
        fmt.Println("No students found!")
        return
    }

    fmt.Print("Enter student name: ")
    var name string
    fmt.Scanln(&name)

    grades, exists := students[name]
    if !exists {
        fmt.Printf("Student %s not found!\n", name)
        return
    }

    if len(grades) == 0 {
        fmt.Printf("%s has no grades yet.\n", name)
        return
    }

    var sum float64
    for _, grade := range grades {
        sum += grade
    }

    average := sum / float64(len(grades))
    fmt.Printf("\n%s's Statistics:\n", name)
    fmt.Printf("  Number of grades: %d\n", len(grades))
    fmt.Printf("  Total points: %.2f\n", sum)
    fmt.Printf("  Average: %.2f (%s)\n", average, getLetterGrade(average))
}

func listStudents(students map[string][]float64) {
    if len(students) == 0 {
        fmt.Println("No students found!")
        return
    }

    fmt.Printf("\nAll Students (%d total):\n", len(students))
    for name, grades := range students {
        if len(grades) > 0 {
            var sum float64
            for _, grade := range grades {
                sum += grade
            }
            average := sum / float64(len(grades))
            fmt.Printf("  %s: %d grades, Average: %.2f (%s)\n",
                name, len(grades), average, getLetterGrade(average))
        } else {
            fmt.Printf("  %s: No grades yet\n", name)
        }
    }
}

func studentStatistics(students map[string][]float64) {
    if len(students) == 0 {
        fmt.Println("No students found!")
        return
    }

    var allGrades []float64
    studentsWithGrades := 0

    for _, grades := range students {
        if len(grades) > 0 {
            studentsWithGrades++
            allGrades = append(allGrades, grades...)
        }
    }

    if len(allGrades) == 0 {
        fmt.Println("No grades recorded yet!")
        return
    }

    // Calculate statistics
    var sum float64
    highest := allGrades[0]
    lowest := allGrades[0]

    for _, grade := range allGrades {
        sum += grade
        if grade > highest {
            highest = grade
        }
        if grade < lowest {
            lowest = grade
        }
    }

    classAverage := sum / float64(len(allGrades))

    fmt.Printf("\nClass Statistics:\n")
    fmt.Printf("  Total students: %d\n", len(students))
    fmt.Printf("  Students with grades: %d\n", studentsWithGrades)
    fmt.Printf("  Total grades recorded: %d\n", len(allGrades))
    fmt.Printf("  Class average: %.2f (%s)\n", classAverage, getLetterGrade(classAverage))
    fmt.Printf("  Highest grade: %.2f (%s)\n", highest, getLetterGrade(highest))
    fmt.Printf("  Lowest grade: %.2f (%s)\n", lowest, getLetterGrade(lowest))
}

func getLetterGrade(score float64) string {
    switch {
    case score >= 90:
        return "A"
    case score >= 80:
        return "B"
    case score >= 70:
        return "C"
    case score >= 60:
        return "D"
    default:
        return "F"
    }
}
```

---

## 🎯 Module 1 Final Project: Personal Finance Tracker

### Project Overview

Buat aplikasi console untuk tracking keuangan pribadi dengan fitur:

- [ ] Income/expense tracking
- [ ] Category management
- [ ] Monthly reports
- [ ] Budget setting dan monitoring
- [ ] Data persistence (simple file-based)

### Project Structure

```
personal-finance/
├── main.go
├── transaction.go
├── category.go
├── report.go
├── data.txt
└── README.md
```

### Required Features Implementation

```go
// main.go
package main

import (
    "fmt"
    "os"
    "strconv"
    "time"
)

type Transaction struct {
    ID          int
    Date        time.Time
    Amount      float64
    Category    string
    Description string
    Type        string // "income" or "expense"
}

type Budget struct {
    Category string
    Limit    float64
    Spent    float64
}

var transactions []Transaction
var budgets map[string]float64
var nextID int = 1

func main() {
    budgets = make(map[string]float64)
    loadData() // Load existing data

    for {
        showMainMenu()
        choice := getUserInput("Choose option: ")

        switch choice {
        case "1":
            addTransaction()
        case "2":
            viewTransactions()
        case "3":
            setBudget()
        case "4":
            viewBudgetStatus()
        case "5":
            generateMonthlyReport()
        case "6":
            deleteTransaction()
        case "7":
            saveData()
            fmt.Println("Data saved. Goodbye!")
            os.Exit(0)
        default:
            fmt.Println("Invalid option!")
        }
    }
}

func showMainMenu() {
    fmt.Println("\n=== Personal Finance Tracker ===")
    fmt.Println("1. Add Transaction")
    fmt.Println("2. View Transactions")
    fmt.Println("3. Set Budget")
    fmt.Println("4. View Budget Status")
    fmt.Println("5. Monthly Report")
    fmt.Println("6. Delete Transaction")
    fmt.Println("7. Save & Exit")
}

func getUserInput(prompt string) string {
    fmt.Print(prompt)
    var input string
    fmt.Scanln(&input)
    return input
}

// Add more functions here...
```

### Assessment Criteria

- [ ] **Functionality**: All features working correctly
- [ ] **Code Quality**: Clean, readable, well-commented code
- [ ] **Error Handling**: Proper validation dan error messages
- [ ] **User Experience**: Intuitive interface dan helpful prompts
- [ ] **Data Management**: Proper data structure usage
- [ ] **Documentation**: Clear README dengan usage instructions

---

## 📋 Module 1 Complete Checklist

### 🔧 Environment Setup

- [ ] Go installed dan verified
- [ ] VS Code dengan Go extension configured
- [ ] Go tools installed (gopls, dlv, staticcheck, etc.)
- [ ] GOPATH dan GOROOT understood
- [ ] First program compiled dan run successfully

### 📖 Program Structure

- [ ] Package declaration understood
- [ ] Import system mastered
- [ ] Main function concepts clear
- [ ] Exported vs unexported identifiers understood
- [ ] Module system basics (go.mod) familiar

### 🔢 Variables & Data Types

- [ ] All variable declaration methods practiced
- [ ] Numeric types (int, float, complex) mastered
- [ ] String operations practiced
- [ ] Boolean logic understood
- [ ] Zero values concept clear
- [ ] Type conversion techniques applied

### 🔄 Control Flow

- [ ] If statements (all variations) practiced
- [ ] Switch statements (including type switch) mastered
- [ ] For loops (all styles) implemented
- [ ] Break dan continue used appropriately
- [ ] Nested loops dan labeled breaks understood

### 🛠️ Practical Projects

- [ ] Calculator program completed
- [ ] Number guessing game implemented
- [ ] Grade management system built
- [ ] Final project (Finance Tracker) finished

### 📚 Additional Learning

- [ ] Go documentation consulted
- [ ] Error messages understood dan debugged
- [ ] Best practices research completed
- [ ] Code formatted dengan gofmt
- [ ] Basic debugging skills developed

---

## 🎯 Self Assessment

Rate your confidence level (1-10):

- [ ] **Go environment setup**: \_\_\_/10
- [ ] **Basic syntax mastery**: \_\_\_/10
- [ ] **Variable dan data types**: \_\_\_/10
- [ ] **Control flow statements**: \_\_\_/10
- [ ] **Problem-solving with Go**: \_\_\_/10
- [ ] **Code debugging ability**: \_\_\_/10
- [ ] **Overall Go fundamentals**: \_\_\_/10

**Minimum score to proceed**: 7/10 pada semua areas

### Areas for Improvement

```
List specific areas where you scored below 7:
1. ________________________________
2. ________________________________
3. ________________________________

Action plan untuk improvement:
1. ________________________________
2. ________________________________
3. ________________________________
```

---

## 📚 Additional Resources & Next Steps

### Must-Read Resources

- [ ] [Effective Go](https://golang.org/doc/effective_go.html)
- [ ] [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)
- [ ] [Go FAQ](https://golang.org/doc/faq)

### Practice Problems

- [ ] Complete 10 basic problems on [Exercism Go Track](https://exercism.io/tracks/go)
- [ ] Solve 5 easy problems on [LeetCode](https://leetcode.com/)
- [ ] Practice with [Go by Example](https://gobyexample.com/)

### Community Engagement

- [ ] Join [Go Indonesia Telegram](https://t.me/golangID)
- [ ] Follow [r/golang](https://reddit.com/r/golang)
- [ ] Read [Go blog](https://blog.golang.org/)

---

## 🎓 Module Completion Certificate

```
🎉 CONGRATULATIONS! 🎉

[Your Name] has successfully completed

MODULE 1: GO FUNDAMENTALS

Completion Date: _______________
Score: ____/10

Skills Mastered:
✅ Go Environment Setup
✅ Basic Syntax & Program Structure
✅ Variables & Data Types
✅ Control Flow Statements
✅ Practical Problem Solving

Ready for: Module 2 - Data Structures & Functions

Instructor: GitHub Copilot
Program: Complete Go API Development Bootcamp
```

---

**Estimated Completion Time**: 1-2 weeks (10-20 hours total)

**Next Module**: [Module 2: Data Structures & Functions](./module-02-data-structures.md)

---

## 📝 Personal Notes

```
Module 1 Learning Journey:

Start Date: _______________
End Date: _______________

Key Learnings:
1. ________________________________
2. ________________________________
3. ________________________________

Challenges Faced:
1. ________________________________
2. ________________________________
3. ________________________________

Breakthrough Moments:
1. ________________________________
2. ________________________________
3. ________________________________

Favorite Go Features So Far:
1. ________________________________
2. ________________________________
3. ________________________________

Goals for Next Module:
1. ________________________________
2. ________________________________
3. ________________________________
```
