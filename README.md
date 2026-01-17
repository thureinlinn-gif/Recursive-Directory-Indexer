# Recursive Directory Indexer

A robust Bash script that generates JSON-based indices for directory structures, handling complex file hierarchies with special configurations and blacklisting capabilities.

## 🎯 Overview

This tool recursively traverses directory trees and creates `index.json` files that catalog files, subdirectories, and special items. It demonstrates proficiency in shell scripting, recursive algorithms, and handling edge cases in file system operations.

## ✨ Key Features

- **Recursive Traversal**: Automatically processes nested directory structures
- **Special Character Handling**: Correctly manages filenames with spaces, quotes, and special characters
- **Blacklist Support**: Excludes specific files/directories via `_blacklist` configuration
- **Special File Marking**: Highlights important files/directories via `_special` configuration
- **Valid JSON Output**: Generates syntactically correct, parseable JSON
- **Relative Path Tracking**: Maintains navigation context with `outer` field

## 🛠️ Technical Implementation

### Core Functionality

```bash
# Handles JSON string escaping
json_escape()

# Converts Bash arrays to JSON arrays
create_json_array()

# Computes relative path back to root
compute_outer()

# Processes individual directories
process_directory()

# Recursively processes directory tree
process_recursively()
```

### JSON Schema

Each `index.json` contains:

```json
{
  "files": ["file1.txt", "file2.txt"],
  "directories": ["subdir1", "subdir2"],
  "special_files": ["important.txt"],
  "special_directories": ["special_dir"],
  "outer": "../.."
}
```

## 📋 Usage

### Basic Invocation

```bash
chmod +x indexer
./indexer /path/to/directory
```

### Example Directory Structure

```
sample/
├── bar/
│   └── index.json
├── foo/
│   ├── baaz/
│   │   ├── _blacklist
│   │   ├── _special
│   │   ├── a_different_directory/
│   │   ├── abc/
│   │   ├── another file
│   │   ├── file1
│   │   ├── some_directory/
│   │   ├── this_file
│   │   ├── x
│   │   ├── y
│   │   ├── z
│   │   └── index.json
│   └── index.json
└── index.json
```

### Configuration Files

**`_blacklist`** - Excludes items from indexing:
```
yet another file
abc
```

**`_special`** - Marks items as special:
```
x
a_different_directory
y
z
```

### Sample Output

For `sample/foo/baaz/index.json`:

```json
{
  "files": ["another file", "file1", "this_file"],
  "directories": ["some_directory"],
  "special_files": ["x", "y", "z"],
  "special_directories": ["a_different_directory"],
  "outer": "../.."
}
```

## 🖥️ Terminal Output

### Execution Screenshot with pretty format

![Terminal Output](https://github.com/user-attachments/assets/f3c0fd3d-588c-4b04-9578-3d6804cba54a)

### Execution Screenshot with normal format

![Terminal Output](https://github.com/user-attachments/assets/28686290-e660-4444-b780-6e1a6b819e4c)

*Screenshot showing successful execution of the indexer script*

## 🔍 Technical Highlights

### Robust Error Handling
- Validates command-line arguments
- Verifies directory existence
- Handles missing configuration files gracefully

### Edge Case Management
- Empty directories (no files/subdirectories)
- Missing `_blacklist` or `_special` files
- Filenames with spaces, quotes, newlines
- Relative vs. absolute path inputs
- Trailing slashes in paths

### Path Normalization
Uses `realpath` to handle various path formats:
- Relative paths: `./sample` or `sample`
- Absolute paths: `/home/user/sample`
- Paths with trailing slashes: `sample/`

## 💡 Skills Demonstrated

- **Bash Scripting**: Advanced array manipulation, string processing
- **Recursion**: Depth-first directory traversal
- **Data Structures**: Array sorting, filtering, transformation
- **JSON Generation**: Manual construction with proper escaping
- **File I/O**: Reading configuration files, writing output
- **Error Handling**: Input validation, edge case management
- **POSIX Compliance**: Portable shell scripting practices

## 📊 Complexity Analysis

- **Time Complexity**: O(n) where n = total files + directories
- **Space Complexity**: O(d) where d = maximum directory depth
- **Scalability**: Efficiently handles large directory trees

## 🚀 Future Enhancements

- Add support for symbolic links
- Implement concurrent processing for large directories
- Add JSON schema validation
- Support custom output formats (YAML, XML)
- Include file metadata (size, permissions, timestamps)

## 📝 License

Academic project - educational use only


