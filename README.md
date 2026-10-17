# Linux & Bash Scripting: Purdue IEEE Software Saturdays

Materials, code snippets, and hands-on lab exercises for the **Linux & Bash Scripting Certificate** modules of Purdue IEEE's Software Saturdays.

## Topics

- Navigating the Linux terminal and filesystem
- Git basics: creating repositories, committing, and pushing to GitHub
- Installing and using packages (`apt`, `sudo`)
- Inspecting network interfaces (`ifconfig`)
- Input/output redirection (`>`, `>>`)
- Searching text with `grep`
- Regular expressions (basic, extended, and Perl-style)
- Sorting and processing text (`sort`)
- Pipelines: chaining commands without intermediate files
- Bash scripting fundamentals

## Repository Structure

```
.
├── regex/
│   ├── commands.txt                    # Commands for each step
│   ├── twocities.txt                   # Novel text
│   ├── twocities_quotes.txt            # Quoted text from the novel
│   ├── twocities_sentence_endings.txt  # Words that end sentences
│   └── twocities_five_letters.txt      # Five-letter sentence endings
├── ifconfig/
│   ├── commands.txt                    # Commands for each step
│   ├── ifconfig.txt                    # ifconfig info
│   ├── ifconfig_v4.txt                 # Extracted lines from ifconfig
│   ├── ip.txt                          # Unsorted IPv4 addresses from ifconfig
│   ├── sorted_ip.txt                   # Sorted IPv4 addresses from ifconfig
│   └── ipv6_regex.txt                  # Bonus: IPv6 regex
└── README.md
```

Each homework folder contains the files requested in that assignment's worksheet.

## Homework 1: Regex and `grep` on *A Tale of Two Cities*

**Goal:** Use regular expressions with `grep` to extract quotes, sentence endings, and specific words from the novel (`twocities.txt`, public domain), tracking the work in a Git repository.

**Tools and concepts used**

| Tool / Concept | Role in this homework |
|---|---|
| `git init` | Turns the `hw1` directory into a repository |
| `git add` | Stages `commands.txt` for commit |
| `git commit -m` | Records the "First Commit" snapshot |
| `git push` | Sends the repo to a remote GitHub repository for submission |
| `grep` | Searches the novel line by line for pattern matches |
| `grep -P` | Enables Perl-compatible regex, which supports shortcuts like `\w` and `\b` |
| `grep -o` | Prints only the matched text instead of the entire line |
| `grep -c` | Counts matching lines (used for the chapter count) |
| `>` (redirection) | Saves each search result to its own output file |
| Character classes (`[^"]`) | Matches any character except a double quote, for quoted text |
| `\w` and `\b` | Word characters and word boundaries, for finding whole words |
| Quantifiers (`+`, `{n}`) | "One or more" and "exactly n" repetitions, for word lengths |
| Anchors (`^`) | Ties a match to the start of a line, for finding `CHAPTER` headings |

**Parts at a glance**

1. Extract all quoted text
2. Extract words that end a sentence (including the period)
3. Narrow that to five-letter words
4. Find the only seventeen-letter word and count the chapters

## Homework 2: `ifconfig`, `grep`, and Pipelines

**Goal:** Isolate and numerically sort the IPv4 addresses reported by `ifconfig`, first with intermediate files and then as a single pipeline. The bonus builds a regex for IPv6 addresses.

**Tools and concepts used**

| Tool / Concept | Role in this homework |
|---|---|
| `ifconfig` | Displays network interfaces, IP addresses, and status |
| `sudo apt install net-tools` | Installs the package that provides `ifconfig` (`sudo` for elevated privileges, `apt` as the package manager) |
| `>` (redirection) | Saves command output to files at each intermediate step |
| `grep` | Filters `ifconfig` output down to IPv4 lines (`inet` vs. `inet6`) |
| `grep -P` | Perl-compatible regex for matching IP address patterns |
| `grep -o` | Extracts only the address itself from each line |
| `sort -n` | Sorts values numerically instead of alphabetically |
| `\|` (pipe) | Chains commands so output flows directly into the next, with no intermediate files |
| Quantifiers (`{1,3}`) | Allows 1 to 3 digits per address segment (the 0 to 999 simplification) |
| Alternation (`\|`) and groups | Combine the many valid IPv6 layouts into one regex (bonus) |
| Anchors (`^`, `$`) | Require the whole line to be an address (bonus) |
| Regex101 | Browser tool for building and testing the bonus regex |

**Deliverables:** `commands.txt`, `sorted_ip.txt`, and `ipv6_regex.txt` (bonus).

## Requirements

- A Linux environment (native, VM, or WSL)
- `git` and a GitHub account
- `net-tools` for `ifconfig`: `sudo apt install net-tools`

## Notes

- `ifconfig` output differs per machine, so regenerate `sorted_ip.txt` by running the pipeline on your own system.
- [Regex101](https://regex101.com) (PCRE2 flavor) is great for building and testing patterns.

## Credit

Assignments by Ryan Baker for Purdue IEEE Software Saturdays.
