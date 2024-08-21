`golint` 本身并没有针对代码长度的特定检查功能。它主要关注代码风格和命名规范，比如变量名、注释风格等。然而，像 `golangci-lint` 这样的综合性 linter 工具包中包含的某些 linters（如 `funlen`、`lll` 等）确实会检查代码长度，包括函数长度、行长度等。

以下是详细介绍：

### 1. **函数长度检查 (`funlen`)**

- **`funlen`** 是一个用于检测函数长度的 linter，它会根据配置的限制来检查函数的行数是否超过设定的阈值。这个检查是为了确保函数保持简短和易于理解。

- **如何忽略**：如果你有一个长函数且想忽略这个检查，可以使用以下注释：

  ```go
  // nolint:funlen
  func MyLongFunction() {
      // 很长的代码块
  }
  ```

- **配置**：你可以通过配置 `golangci-lint` 来自定义函数长度的阈值。例如：

  ```yaml
  linters-settings:
    funlen:
      lines: 100   # 设置函数最大行数为100
  ```

### 2. **行长度检查 (`lll`)**

- **`lll`**（Long Line Linter）检查单行代码的长度。通常，默认的行长度限制是 120 个字符。如果一行代码超过这个限制，`lll` 就会发出警告。

- **如何忽略**：如果某一行代码超过长度限制且你不希望收到警告，可以在该行前面加上以下注释：

  ```go
  // nolint:lll
  fmt.Println("This is a very long line of code that exceeds the recommended length but we want to keep it intact for some reason")
  ```

- **配置**：可以在 `golangci-lint` 的配置文件中设置自定义行长度：

  ```yaml
  linters-settings:
    lll:
      line-length: 100  # 将行长度限制设置为100个字符
  ```

### 3. **代码复杂度检查 (`gocyclo` 和 `gocognit`)**

- **`gocyclo`** 检查函数的圈复杂度（Cyclomatic Complexity）。较高的圈复杂度通常表明函数中的控制流非常复杂，这可能会导致代码难以理解和维护。

- **`gocognit`** 检查函数的认知复杂度（Cognitive Complexity）。它比圈复杂度更细化，考虑了代码中嵌套逻辑的影响。

- **如何忽略**：你可以使用以下注释忽略这些检查：

  ```go
  // nolint:gocyclo
  func MyComplexFunction() {
      // 复杂的代码块
  }

  // nolint:gocognit
  func AnotherComplexFunction() {
      // 另一个复杂的代码块
  }
  ```

- **配置**：可以通过配置 `golangci-lint` 来调整允许的复杂度阈值：

  ```yaml
  linters-settings:
    gocyclo:
      min-complexity: 10  # 设置允许的最小圈复杂度
    gocognit:
      min-complexity: 15  # 设置允许的最小认知复杂度
  ```

### 总结

虽然 `golint` 本身没有特定的长度检查功能，但通过 `golangci-lint` 和其他 lint 工具可以实现对函数长度、行长度、复杂度的检查。你可以根据项目的需要配置这些工具，并在特定情况下使用 `// nolint:<linter>` 注释来忽略这些检查。对于大多数情况下，建议优先调整代码结构以符合这些规则，从而提高代码的可读性和可维护性。