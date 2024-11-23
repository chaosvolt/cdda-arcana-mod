---
tags: [json, transformation]
---

# Convert `condition` to `compare_string`

This pattern transforms JSON objects by converting a `condition` structure into
a `compare_string` array.

```grit
engine marzano(0.1)
language json

`"condition": { "u_has_var": $var, "value": $value }` => `"compare_string": [ $value, { "u_val": $var } ]`
```

## Example Transformation

### Input

```json
{
  "condition": {
    "u_has_var": "variable_name",
    "value": "example_value"
  }
}
```

### Output

```json
{
  "compare_string": [
    "example_value",
    { "u_val": "variable_name" }
  ]
}
```

## Test Case

- This test validates the pattern correctly replaces the `condition` structure.

### Input

```json
{
  "key": "example",
  "condition": {
    "u_has_var": "var",
    "value": "val"
  }
}
```

### Output

```json
{
  "key": "example",
  "compare_string": [
    "val",
    { "u_val": "var" }
  ]
}
```

### How It Works

1. Place this file in the `.grit/patterns` directory in your repository.
2. Use the `grit patterns test` command to test this transformation against your
   defined cases.
3. Once verified, the pattern can be applied using the Grit CLI
   (`grit apply migrate_to_new_variable_format`) to automatically make the
   changes across your project.
