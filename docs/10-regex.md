# 10. Regular Expressions (Regex)

## 10.1 Core Concept

- **What:** A sequence of characters defining a search pattern, used for matching character combinations in strings.
- **Why:** Essential for powerful text searching (`grep`), manipulation (`sed`, `awk`), scripting, input validation, and log analysis.
- **Flavors:** Different tools might use slightly different Regex syntax (e.g., Basic vs. Extended).

## 10.2 Basic Metacharacters (Common to Most Flavors)

- `.` (Dot): Matches any single character (except newline).
  - Example: `gr.p` matches `grep`, `grip`, `gr@p`.
- `^` (Caret): Matches the beginning of a line.
  - Example: `^Start` matches lines beginning with "Start".
- `$` (Dollar): Matches the end of a line.
  - Example: `end$` matches lines ending with "end".
- `*` (Asterisk): Matches the preceding item zero or more times.
  - Example: `colou*r` matches `color`, `colour`.
- `\` (Backslash): Escapes the next character. Used to match literal metacharacters.
  - Example: `\.` matches a literal dot, `\$` matches a literal dollar sign.

## 10.3 Character Sets & Classes

- `[...]` (Square Brackets): Matches any single character within the brackets.
  - Example: `gr[ae]y` matches `gray` or `grey`.
  - Ranges: `[0-9]` matches any digit, `[a-z]` matches any lowercase letter.
- `[^...]` (Negated Set): Matches any single character NOT within the brackets.
  - Example: `[^0-9]` matches any non-digit character.
- **POSIX Character Classes** (within `[[:...:]]`): More portable than ranges.
  - `[[:alnum:]]` : Alphanumeric characters (`[a-zA-Z0-9]`).
  - `[[:alpha:]]` : Alphabetic characters (`[a-zA-Z]`).
  - `[[:digit:]]` : Digits (`[0-9]`).
  - `[[:lower:]]` : Lowercase letters (`[a-z]`).
  - `[[:upper:]]` : Uppercase letters (`[A-Z]`).
  - `[[:space:]]` : Whitespace characters (space, tab, newline, etc.).
  - `[[:punct:]]` : Punctuation characters.
  - Example: `grep '[[:digit:]]' file` finds lines with digits.

## 10.4 Quantifiers (Specify Repetition)

*(Note: Syntax differs between Basic (BRE) and Extended (ERE) Regex)*

- `*` : Zero or more times (already covered).
- `+` (Plus - ERE): Matches the preceding item one or more times.
  - BRE equivalent: `\+`.
  - Example (ERE): `go+d` matches `god`, `good`.
- `?` (Question Mark - ERE): Matches the preceding item zero or one time (optional).
  - BRE equivalent: `\?`.
  - Example (ERE): `colou?r` matches `color`, `colour`.
- `{n}` (Curly Braces - ERE): Matches the preceding item exactly `n` times.
  - BRE equivalent: `\{n\}`.
  - Example (ERE): `[0-9]{3}` matches exactly three digits.
- `{n,}` (ERE): Matches the preceding item `n` or more times.
  - BRE equivalent: `\{n,\}`.
  - Example (ERE): `[a-z]{2,}` matches two or more lowercase letters.
- `{n,m}` (ERE): Matches the preceding item at least `n` times, but no more than `m` times.
  - BRE equivalent: `\{n,m\}`.
  - Example (ERE): `\b[A-Z]{2,4}\b` matches words with 2 to 4 uppercase letters.

## 10.5 Grouping & Alternation (ERE)

- `(...)` (Parentheses - ERE): Groups parts of the pattern together. Allows applying quantifiers to the group or capturing the matched text.
  - BRE equivalent: `\(...\)`.
  - Example (ERE): `(ab)+` matches `ab`, `abab`, `ababab`.
- `|` (Pipe - ERE): Acts as an OR operator. Matches the pattern on the left OR the pattern on the right.
  - BRE equivalent: `\|`.
  - Example (ERE): `cat|dog` matches `cat` or `dog`.
  - Example (ERE): `^(ERROR|WARNING):` matches lines starting with `ERROR:` or `WARNING:`.

## 10.6 Anchors & Boundaries

- `^` : Beginning of the line (already covered).
- `$` : End of the line (already covered).
- `\b` : Word boundary. Matches the position between a word character (`[[:alnum:]_]`) and a non-word character, or start/end of line.
  - Example: `\bcat\b` matches `cat` but not `catalog`.
- `\B` : Non-word boundary.

## 10.7 Using Regex with Linux Tools

**`grep` (Basic Regex - BRE by default):**
```bash
grep 'pattern' file
```
Need to escape `+`, `?`, `{}`, `|`, `()` with backslashes (e.g., `grep 'go\+d' file`).

**`grep -E` or `egrep` (Extended Regex - ERE):**
```bash
grep -E 'pattern' file
egrep 'pattern' file
```
No need to escape `+`, `?`, `{}`, `|`, `()`. Generally easier to write complex patterns.

Example: `egrep '^(ERROR|WARNING):' /var/log/syslog`.

**`sed` (Basic Regex - BRE by default):**
```bash
sed 's/bre_pattern/replacement/' file
```
Use `sed -E` or `sed -r` (depending on version) for ERE.

Example (BRE):
```bash
sed 's/\([0-9]\{3\}\) \([0-9]\{4\}\)/AreaCode: \1, Number: \2/' phone_list
```
(using capturing groups `\(...\)` and backreferences `\1`, `\2`)

Example (ERE):
```bash
sed -E 's/([0-9]{3}) ([0-9]{4})/AreaCode: \1, Number: \2/' phone_list
```

**`awk` (Extended Regex - ERE):**
```bash
awk '/ere_pattern/ { action }' file
```
Example: `awk '/^[0-9]+$/ { print "Line contains only digits:" $0 }' file`.

## 10.8 Key Takeaways for Recall

- `.` = any char, `^` = start, `$` = end.
- `[...]` = specific chars, `[^...]` = not specific chars.
- `*` = 0+, `+` = 1+, `?` = 0 or 1, `{n,m}` = range (ERE syntax shown, BRE needs `\`).
- `(...)` = grouping, `|` = OR (ERE syntax shown, BRE needs `\`).
- `\` = escape special chars.
- Use `grep -E` or `egrep` for easier ERE syntax.
