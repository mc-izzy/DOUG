<img src="./inverse-batman-logo.jpg" alt="Inverse Batman Logo" width=400 />
> "\[Batman is] the hero Gotham deserves, but not the one it needs right now" -Jim Gordon

> "Bash is not the scripting language you deserve, but it's the one you get." -Jacob Thompson

# Bourne Again Shell
- bash manual [https://www.gnu.org/software/bash/manual/bash.html]
- Types are for the weak. All things are string.
- Every statement is first assumed to be a 'command' and strings don't need quotes.
    - This has major implications and causes much of the weirdness of bash
    - Why must all variable references be preceded by a `$` ?
    - Variable assignment cannot include spaces around the equals sign.
        - How would bash parse the statement `foo = 12` ?

## Wanna do some math ? 
<sub><sup>but only on integers</sup></sub>

- `1 + 2` cannot work. Why?
- We use double parens to open an 'arithmetic context'
    - ((foo = 1 + 2)) creates a variable called foo and sets it to 3
    - ((x++)) creates a variable called x and sets it to 1 or if that
    variable exists increments it.
```bash
x=0
while ((x < 5)); do
    echo "x is $x"
    ((x++))
done

```

### You want to do math with floats?
<details>
<summary>no.</summary>(just kidding use <code>bc</code>)
</details>

## Control Flow

```bash
if \<command>|\<test> ; then
....
fi
```

```bash
echo "Enter a number between 1 and 3:"
read num

case $num in
  1)
    echo "You chose number one."
    ;; # this is the equivalent to break;
  2)
    echo "You chose number two."
    ;;
  3)
    echo "You chose number three."
    ;;
  *) # default
    echo "Invalid choice. Please enter a number between 1 and 3."
    ;;
esac
```

- While loops, we got 'em (see example above)
- for loops:
```bash
for arg in "$@"; do
  echo "Argument: $arg"
done
```
- loop over index (uncommon):
```bash
for n in {1..5}; do  
    echo $n  
done
```
- or in some older bash
```bash
for i in $(seq 5); do echo $i; done
```

### The almighty `&&`
- \<command> \[\<args>] && \<command2> \[...]
	- do command 1 then once it is done, if the status code is 0, run command 2 
```bash
cat grep foo ./file-that-doesnt-have-foo && echo 'unreachable'
```

## Test command
- \[ is a special command in bash
- bash has extended test syntax with \[\[ ... ]]
- see: [https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html]
## Special Variables

Bash provides several **special variables** that are commonly used in shell scripts.

### 1. **`$?`** — Exit status of the last command
- **Description**: Holds the exit status (return code) of the last executed command.
- **Common Usage**: Checking if a command succeeded or failed.
  
  Example:
  ```bash
  command
  if [ $? -eq 0 ]; then
    echo "Command succeeded"
  else
    echo "Command failed"
  fi
  ```

### 2. **`$0`** — Name of the script or shell
- **Description**: Contains the name of the script or shell that is being executed.
- **Common Usage**: Typically used to print the script name in error messages or when checking how the script was invoked.

  Example:
  ```bash
  echo "Script name: $0"
  ```

### 3. **`$1`, `$2`, ...`$N`** — Positional parameters
- **Description**: Holds the command-line arguments passed to the script or function. `$1` is the first argument, `$2` is the second, and so on.
- **Common Usage**: Accessing arguments provided when running a script.

  Example:
  ```bash
  echo "First argument: $1"
  echo "Second argument: $2"
  ```

### 4. **`$#`** — Number of positional parameters
- **Description**: Holds the number of positional parameters passed to the script or function.
- **Common Usage**: Checking the number of arguments passed to a script.

  Example:
  ```bash
  if [ $# -eq 0 ]; then
    echo "No arguments provided"
  fi
  ```

### 5. **`$@`** — All arguments as separate words
- **Description**: Contains all the arguments passed to the script or function, treated as separate words. If you want to loop through the arguments, `$@` is the preferred choice.
- **Common Usage**: Looping through all arguments passed to the script.

  Example:
  ```bash
  for arg in "$@"; do
    echo "Argument: $arg"
  done
  ```

### 6. **`$*`** — All arguments as a single string
- **Description**: Similar to `$@`, but treats all arguments as a single string.
- **Common Usage**: When you want to process all arguments together (less commonly used than `$@`).

  Example:
  ```bash
  echo "All arguments: $*"
  ```
### Subshells and Pipes

- $(command) - run command and inline its return value
    - e.x. vimf
## Spawning and manging background jobs
- jobs, fg, bg, kill, &
- try `eslint &` to start eslint as a background task

## Example scripts
```bash
case $1 in
  -c)
    echo $2 | python3 -m json.tool | pbcopy
    ;;
  -h | --help)
    echo "This script formats json using pythons json.tool utility. Use the -c flag to redirect output to clipboard. Remeber output must be wrapped in single quotes"
          ;;
  *)
    echo $1 | python3 -m json.tool
    ;;
esac

```
```bash
init_gs=$(git status --short)
cleanupcmd=""
if [ -n "$init_gs" ]; then
	git stash -u --quiet
	cleanupcmd="git stash pop --quiet"
fi

echo -e "\033[32mRunning eslint --cache --fix\033[0m"
eslint --cache --fix --color
eslint_error=$?

if git diff --quiet; then
	if [$eslint_error -gt 0 ]; then
		exec < /dev/tty
		read -p "ESLint errors found, but not file modified. Continue?(Y/n)" choice
		if [ "$choice" == 'N' ] || [ "$choice" == 'n' ]; then
			echo "Push aborted"
			$cleanupcmd
			exit 1
		fi
	fi
	$cleanupcmd
	exit 0
else
	echo ""
	echo -e "** \033[33mESLint modified files. Stage changes and commit again.\033[0m"
	echo ""
	git status
	$cleanupcmd
	exit 1
fi
```

```bash
function fzfh() {
  valid_flags=("-t" "-e" "--help" "-h")

  if [ "$1" = "--help" ] || [ "$1" = "-h" ]; then
    echo "Usage: fzfh [-t] [-e]"
    echo "Options:"
    echo "  -t    Use the tail command for history"
    echo "  -e    Evaluate the selected command"
    return 0
  fi

  for arg in "$@"; do
    if [[ ! " ${valid_flags[@]} " =~ " $arg " ]]; then
      echo "Error: Invalid flag '$arg'. Use --help or -h for usage information."
      return 1
    fi
  done

  if [ "$1" = "-t" ] || [ "$2" = "-t" ]; then
    fzfcommand=$(tail -n 100 ~/.zsh_history | cut -f 2 -d ";" | awk '!x[$0]++' | fzf)
  else
    fzfcommand=$(cut -f 2 -d ";" ~/.zsh_history | awk '!x[$0]++' | fzf)
  fi

  if [ "$1" = "-e" ] || [ "$2" = "-e" ]; then
    eval $fzfcommand
  else
    echo "$fzfcommand"
  fi
}

```