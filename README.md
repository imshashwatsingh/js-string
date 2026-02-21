# JavaScript String Methods Cheat Sheet (2025–2026)

Most important string methods in modern JavaScript (ES6+ to ES2025/ES2026).  
Strings are **immutable** — no method modifies the original string.

Each entry includes: **syntax**, **returns**, **time complexity**, **purpose**, **example**, **output**.

## 1. Basic Access & Information

| Method/Property       | Returns          | Time Complexity | Purpose / How it works                              | Example                                              | Output                  |
|-----------------------|------------------|------------------|-----------------------------------------------------|------------------------------------------------------|-------------------------|
| `length` (property)   | number           | O(1)            | Number of UTF-16 code units                         | `'hello 🌍'.length`                                  | 7 (not 6!)             |
| `charAt(index)`       | string (char)    | O(1)            | Character at position (or empty string)             | `'hello'.charAt(1)`                                  | 'e'                    |
| `at(index)`           | string or undefined | O(1)         | Char at index (supports negative indices) – ES2022+ | `'hello'.at(-1)`                                     | 'o'                    |
| `charCodeAt(index)`   | number           | O(1)            | UTF-16 code unit at index                           | `'hello'.charCodeAt(0)`                              | 104                    |
| `codePointAt(index)`  | number           | O(1)            | Full Unicode code point (handles surrogates)        | `'🌍'.codePointAt(0)`                                | 127757                 |
| `indexOf(search, from?)` | number (-1 if not found) | O(n)     | First position of substring                         | `'hello world'.indexOf('world')`                     | 6                      |
| `lastIndexOf(search, from?)` | number      | O(n)            | Last position of substring                          | `'hello hello'.lastIndexOf('hello')`                 | 6                      |
| `includes(search, from?)` | boolean     | O(n)            | Contains substring? (ES2015+)                       | `'hello'.includes('ell')`                            | true                   |
| `startsWith(search, pos?)` | boolean    | O(n)            | Begins with substring? (ES2015+)                    | `'hello'.startsWith('he')`                           | true                   |
| `endsWith(search, len?)` | boolean      | O(n)            | Ends with substring? (ES2015+)                      | `'hello'.endsWith('lo')`                             | true                   |

## 2. Case Conversion & Trimming

| Method                | Returns          | Time Complexity | Purpose                                             | Example                                              | Output                  |
|-----------------------|------------------|------------------|-----------------------------------------------------|------------------------------------------------------|-------------------------|
| `toLowerCase()`       | new string       | O(n)            | Convert to lowercase                                | `'Hello World'.toLowerCase()`                        | 'hello world'          |
| `toUpperCase()`       | new string       | O(n)            | Convert to uppercase                                | `'hello'.toUpperCase()`                              | 'HELLO'                |
| `toLocaleLowerCase(locale?)` | new string | O(n)     | Locale-sensitive lowercase                          | `'İSTANBUL'.toLocaleLowerCase('tr')`                 | 'istanbul'             |
| `toLocaleUpperCase(locale?)` | new string | O(n)     | Locale-sensitive uppercase                          | `'i'.toLocaleUpperCase('tr')`                        | 'İ'                    |
| `trim()`              | new string       | O(n)            | Remove whitespace from both ends                    | `'  hello  '.trim()`                                 | 'hello'                |
| `trimStart()` / `trimLeft()` | new string | O(n)     | Remove leading whitespace (ES2019+)                 | `'  hello'.trimStart()`                              | 'hello'                |
| `trimEnd()` / `trimRight()`  | new string | O(n)     | Remove trailing whitespace (ES2019+)                | `'hello  '.trimEnd()`                                | 'hello'                |

## 3. Substring Extraction (Non-mutating)

| Method                | Returns          | Time Complexity | Purpose / Difference                                | Example                                              | Output                  |
|-----------------------|------------------|------------------|-----------------------------------------------------|------------------------------------------------------|-------------------------|
| `slice(start?, end?)` | new string       | O(n)            | Extract portion (negative indices ok)               | `'hello world'.slice(6,11)`                          | 'world'                |
| `substring(start, end?)` | new string    | O(n)            | Like slice but negative → 0, start > end swaps      | `'hello'.substring(4,1)`                             | 'olle'                 |
| `substr(start, length?)` | new string   | O(n)            | From start, take length chars (deprecated)          | `'hello'.substr(1,3)`                                | 'ell'                  |

**Recommendation 2025+**: Prefer `slice()` — clearest and supports negative indices.

## 4. Splitting & Joining

| Method                | Returns          | Time Complexity | Purpose                                             | Example                                              | Output                        |
|-----------------------|------------------|------------------|-----------------------------------------------------|------------------------------------------------------|-------------------------------|
| `split(separator?, limit?)` | array of strings | O(n)     | Split into array                                    | `'a,b,c'.split(',')`                                 | `['a','b','c']`              |
| `split('')`           | array of chars   | O(n)            | Split into characters (careful with surrogates)     | `'hello🌍'.split('')`                                | `['h','e','l','l','o','�','�']` (bad) |
| `[...str]`            | array of chars   | O(n)            | Correct spread → handles Unicode                    | `[...'hello🌍']`                                     | `['h','e','l','l','o','🌍']` |

## 5. Search & Replace

| Method                | Returns          | Time Complexity | Purpose                                             | Example                                              | Output                  |
|-----------------------|------------------|------------------|-----------------------------------------------------|------------------------------------------------------|-------------------------|
| `search(regexp)`      | number or -1     | O(n)            | Index of first match (regex or string)              | `'hello 123'.search(/\d+/)`                          | 6                      |
| `match(regexp)`       | array or null    | O(n)            | Match details (with g → all matches)                | `'hello hello'.match(/hello/g)`                      | `['hello','hello']`    |
| `matchAll(regexp)`    | iterator         | O(n)            | All matches with groups & indices (ES2020+)         | `for (const m of 'test1 test2'.matchAll(/t..t/g)) console.log(m)` | —                      |
| `replace(search, replacement)` | new string | O(n)     | Replace first occurrence (string or regex)          | `'hello hello'.replace('hello', 'hi')`               | 'hi hello'             |
| `replaceAll(search, replacement)` | new string | O(n)  | Replace all occurrences (ES2021+)                   | `'hello hello'.replaceAll('hello', 'hi')`            | 'hi hi'                |

## 6. Padding & Repeating

| Method                | Returns          | Time Complexity | Purpose                                             | Example                                              | Output                  |
|-----------------------|------------------|------------------|-----------------------------------------------------|------------------------------------------------------|-------------------------|
| `padStart(targetLen, pad?)` | new string | O(n)     | Pad at beginning (ES2017+)                          | `'7'.padStart(3, '0')`                               | '007'                  |
| `padEnd(targetLen, pad?)`   | new string | O(n)     | Pad at end (ES2017+)                                | `'42'.padEnd(5, '-')`                                | '42---'                |
| `repeat(count)`       | new string       | O(n)            | Repeat string count times                           | `'la'.repeat(3)`                                     | 'lalala'               |

## 7. Unicode & Safety (ES2024+)

| Method                | Returns          | Time Complexity | Purpose                                             | Example                                              | Output                  |
|-----------------------|------------------|------------------|-----------------------------------------------------|------------------------------------------------------|-------------------------|
| `normalize(form?)`    | new string       | O(n)            | Unicode normalization (NFC, NFD, etc.)              | `'\u1E9B\u0323'.normalize('NFC')`                   | single char (precomposed) |
| `isWellFormed()`      | boolean          | O(n)            | Is string valid UTF-16? (ES2024+)                   | `'\uD800'.isWellFormed()`                            | false                  |
| `toWellFormed()`      | new string       | O(n)            | Replace lone surrogates with � (ES2024+)            | `'\uD800'.toWellFormed()`                            | '�'                    |

## 8. Static / Utility Methods

| Method                        | Returns          | Purpose                                             | Example                                              | Output                  |
|-------------------------------|------------------|-----------------------------------------------------|------------------------------------------------------|-------------------------|
| `String.fromCharCode(...codes)` | string        | Create from UTF-16 code units                       | `String.fromCharCode(104, 101, 108, 108, 111)`      | 'hello'                |
| `String.fromCodePoint(...points)` | string      | Create from Unicode code points                     | `String.fromCodePoint(127757)`                       | '🌍'                   |
| `String.raw`tag`              | string           | Raw template literal (no escapes)                   | `String.raw`hello\nworld``                           | 'hello\\nworld'        |

## Quick Best Practices (2025+)

- Prefer `` `template literals` `` over concatenation
- Use `at(-1)` instead of `[str.length-1]`
- Use `slice()` over `substring()`/`substr()`
- Prefer spread `[...str]` or `Array.from(str)` for correct Unicode char iteration
- Use `replaceAll()` when you want all replacements (no /g needed)
- Use `isWellFormed()` + `toWellFormed()` when handling user input / external data
- Chain methods: `str.trim().toUpperCase().padStart(10, '*')`

Happy coding! 🚀
