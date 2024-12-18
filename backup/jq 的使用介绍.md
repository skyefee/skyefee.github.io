# jq 的使用介绍

`jq` 是一个强大的命令行工具，用于解析、查询和操作 JSON 数据。以下是 `jq` 的常用功能和使用方法：

---

## 1. 基本用法

### **格式化 JSON**
`jq` 默认会美化 JSON 输出：
```bash
echo '{"name":"张三","age":30}' | jq
```

**输出：**
```json
{
  "name": "张三",
  "age": 30
}
```

---

### **提取字段**
- 提取 `name` 字段：
  ```bash
  echo '{"name":"张三","age":30}' | jq '.name'
  ```
  **输出：**
  ```
  "张三"
  ```

- 提取嵌套字段：
  ```bash
  echo '{"person":{"name":"张三","age":30}}' | jq '.person.name'
  ```
  **输出：**
  ```
  "张三"
  ```

---

### **遍历数组**
- 输出数组中的所有元素：
  ```bash
  echo '[10, 20, 30]' | jq '.[]'
  ```
  **输出：**
  ```
  10
  20
  30
  ```

- 提取数组中的第一个元素：
  ```bash
  echo '[10, 20, 30]' | jq '.[0]'
  ```
  **输出：**
  ```
  10
  ```

---

### **遍历对象**
- 提取对象中的所有键：
  ```bash
  echo '{"a":1,"b":2}' | jq 'keys'
  ```
  **输出：**
  ```json
  ["a", "b"]
  ```

- 提取对象的值：
  ```bash
  echo '{"a":1,"b":2}' | jq '.[]'
  ```
  **输出：**
  ```
  1
  2
  ```

---

## 2. 高级查询

### **筛选**
- 筛选数组中符合条件的元素：
  ```bash
  echo '[{"name":"小红","age":25},{"name":"小明","age":30}]' | jq '.[] | select(.age > 25)'
  ```
  **输出：**
  ```json
  {
    "name": "小明",
    "age": 30
  }
  ```

---

### **修改字段**
- 修改 JSON 中的字段值：
  ```bash
  echo '{"name":"张三","age":30}' | jq '.age = 31'
  ```
  **输出：**
  ```json
  {
    "name": "张三",
    "age": 31
  }
  ```

- 增加新字段：
  ```bash
  echo '{"name":"张三"}' | jq '. + {"age":30}'
  ```
  **输出：**
  ```json
  {
    "name": "张三",
    "age": 30
  }
  ```

---

### **删除字段**
- 删除 `age` 字段：
  ```bash
  echo '{"name":"张三","age":30}' | jq 'del(.age)'
  ```
  **输出：**
  ```json
  {
    "name": "张三"
  }
  ```

---

### **组合输出**
- 输出多个字段的值：
  ```bash
  echo '{"name":"张三","age":30}' | jq '{name, age}'
  ```
  **输出：**
  ```json
  {
    "name": "张三",
    "age": 30
  }
  ```

---

## 3. 处理 JSON 文件

### **从文件中读取 JSON**
假设 JSON 文件为 `data.json`：
```bash
jq '.name' data.json
```

### **保存输出到文件**
```bash
jq '.name' data.json > output.json
```

---

## 4. 实用功能

### **原始字符串输出**
使用 `-r` 去掉引号：
```bash
echo '{"name":"张三"}' | jq -r '.name'
```

**输出：**
```
张三
```

---

### **统计操作**
- 求和：
  ```bash
  echo '[1, 2, 3]' | jq 'add'
  ```
  **输出：**
  ```
  6
  ```

- 计算数组长度：
  ```bash
  echo '[1, 2, 3]' | jq 'length'
  ```
  **输出：**
  ```
  3
  ```

---

### **生成 JSON**
使用 `jq` 生成 JSON 数据：
```bash
echo '{}' | jq '. + {"name":"张三","age":30}'
```

**输出：**
```json
{
  "name": "张三",
  "age": 30
}
```

---

## 5. 常见场景示例

### **提取数组中所有符合条件的元素**
```bash
echo '[{"id":1},{"id":2},{"id":3}]' | jq '.[] | select(.id > 1)'
```

**输出：**
```json
{
  "id": 2
}
{
  "id": 3
}
```

### **合并多个 JSON 对象**
```bash
echo '{"a":1} {"b":2}' | jq -s 'add'
```

**输出：**
```json
{
  "a": 1,
  "b": 2
}
```

### **处理嵌套数据**
提取嵌套对象中的值：
```bash
echo '{"data":{"list":[{"id":1},{"id":2}]}}' | jq '.data.list[].id'
```

**输出：**
```
1
2
```

---

## 6. 总结
- **基础操作**：访问字段、遍历数组和对象。
- **高级功能**：筛选、修改和删除字段。
- **工具支持**：轻松处理文件输入/输出。

通过 `jq`，可以高效地在命令行中操作 JSON 数据。如果需要更复杂的功能或示例，请随时告诉我！