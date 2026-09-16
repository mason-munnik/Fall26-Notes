---
title: Exit Codes, Chaining & Scripting
date: 2026-08-26
course: CS3620 Operating Systems
tags: [linux-shell, bash-scripting]
related:
  - "[[Linux Shell MOC]]"
  - "[[Streams, Redirection & Pipes]]"
  - "[[Executables & Environment]]"
---

# Exit Codes, Chaining & Scripting

## Table of Contents

- [Exit Code](#exit-code)
- [Multiple Commands in One Line](#multiple-commands-in-one-line)
- [Scripting](#scripting)
- [Key Terms](#key-terms)

---

## Exit Code

> **Cues:** `$?`, 0 = success

**Notes:**

- Every completed command returns an **exit code**.
- Typically, `0` means "no problems".
- Automatically stored in a variable called `$?`; check with `echo $?`.

**Summary:** A command's exit code is stored in `$?`, and `0` typically means no problems.

---

## Multiple Commands in One Line

> **Cues:** `;`, `&&`

**Notes:**

- `<command1>; <command2>` — execute command1 and then command2.
- `<command1> && <command2>` — execute command1 and then, if command1 completed with no errors (exit code == 0), execute command2.

**Summary:** `&&` only runs the second command if the first succeeded (exit code 0), while `;` always runs both.

---

## Scripting

> **Cues:** `#!/bin/bash`, chmod +x, `$1 $2 $3`

**Notes:**

- A script consists of multiple shell commands and must start with `#!/bin/bash`.
- A string can be given directly to bash for execution: `bash -c "ls"`.
- The script needs to be executable: `chmod +x <script>` (see [[Executables & Environment]]).
- Scripts can access arguments via variables: `"$1"`, `"$2"`, `"$3"`, ...
- Supports programming constructs (variables, if, for, functions, ...).
- Reference: [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/)

Example script (connectivity test):

```bash
#!/bin/bash
if [ $# -eq 0 ]; then
  URL="https://google.com"
else
  URL="$1"
fi
echo "testing connectivity using $URL"
while true
do
  DATE=$(date)
  timeout 5 wget "$URL" -O /dev/null 2>/dev/null
  if [ $? -eq 0 ]; then
    echo "YOU ARE CONNECTED ($DATE)"
  else
    echo "CONNECTION ERROR ($DATE)"
  fi
  sleep 5
done
```

**Summary:** A shell script must start with `#!/bin/bash`, be made executable with `chmod +x`, and can access its arguments via `$1`, `$2`, `$3`, etc.

---

## Key Terms

|Term|Definition|
|---|---|
|**Exit code**|The value a completed command returns, stored in `$?`; `0` typically means success.|
