# OverTheWire Bandit — Walkthrough (Level 0 → 17)

> A detailed writeup of my journey through OverTheWire Bandit, covering Linux fundamentals, shell usage, file handling, permissions, encoding, networking, and real troubleshooting through practical exercises.

---

## Environment Setup

| Item | Detail |
|------|--------|
| Platform | Kali Linux (Virtual Machine) |
| Connection | SSH |
| Notes | Local text file for passwords and progress |
| Goal | Learn by solving manually and understanding every concept |

---

## Table of Contents

- [Level 0 → 1](#level-0--1)
- [Level 1 → 2](#level-1--2)
- [Level 2 → 3](#level-2--3)
- [Level 3 → 4](#level-3--4)
- [Level 4 → 5](#level-4--5)
- [Level 5 → 6](#level-5--6)
- [Level 6 → 7](#level-6--7)
- [Level 7 → 8](#level-7--8)
- [Level 8 → 9](#level-8--9)
- [Level 9 → 10](#level-9--10)
- [Level 10 → 11](#level-10--11)
- [Level 11 → 12](#level-11--12)
- [Level 12 → 13](#level-12--13)
- [Level 13 → 14](#level-13--14)
- [Level 14 → 15](#level-14--15)
- [Level 15 → 16](#level-15--16)
- [Level 16 → 17](#level-16--17)
- [Key Skills Learned](#key-skills-learned)
- [Final Reflection](#final-reflection)

---

## Level 0 → 1

**Objective:** Connect to Bandit and read the password stored in `readme`.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
ls
cat readme
```

**Explanation:**
- `ssh` opens a secure remote shell.
- `-p 2220` specifies a custom SSH port.
- `ls` lists files in the current directory.
- `cat` prints file contents.

**Skills Learned:** First remote login · Basic Linux navigation · Reading files

---

## Level 1 → 2

**Objective:** Read a file named `-`.

```bash
cat ./-
```

**Explanation:** A lone `-` is often interpreted as standard input. Prefixing with `./` tells the shell it is a filename in the current directory.

**Skills Learned:** Special filenames · Path-based disambiguation

---

## Level 2 → 3

**Objective:** Read a filename containing spaces.

```bash
cat "./spaces in this filename"
```

**Explanation:** Spaces split command arguments. Quotes preserve the entire filename as one argument.

**Skills Learned:** Quoting arguments · Handling spaces in filenames

---

## Level 3 → 4

**Objective:** Find a hidden file in `inhere`.

```bash
cd inhere
ls -a
cat ...Hiding-From-You
```

**Explanation:** Files beginning with `.` are hidden. `ls -a` shows hidden entries.

**Skills Learned:** Hidden files · Directory traversal

---

## Level 4 → 5

**Objective:** Find the only human-readable file among many files.

```bash
cd inhere
file ./*
cat ./-file07
```

**Explanation:** The `file` command detects file type based on content rather than extension. The readable file was identified as ASCII text.

**Skills Learned:** File type identification · Efficient investigation

---

## Level 5 → 6

**Objective:** Find a file that is human-readable, 1033 bytes, and not executable.

```bash
find . -type f -size 1033c ! -executable
cat <result>
```

**Explanation:**
- `find .` searches from current directory.
- `-type f` limits results to files.
- `-size 1033c` means exactly 1033 bytes.
- `! -executable` excludes executable files.

**Skills Learned:** Advanced searching · Filtering with conditions

---

## Level 6 → 7

**Objective:** Find a file owned by a specific user/group with an exact size.

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

**Explanation:** Searching `/` scans the whole system. `2>/dev/null` hides permission errors by discarding stderr.

**Skills Learned:** System-wide enumeration · Error redirection

---

## Level 7 → 8

**Objective:** Find the password next to the word `millionth`.

```bash
grep millionth data.txt
```

**Explanation:** `grep` searches lines matching a pattern.

**Skills Learned:** Text searching · Log/data extraction basics

---

## Level 8 → 9

**Objective:** Find the only line that appears once.

```bash
sort data.txt | uniq -u
```

**Explanation:** `sort` groups duplicates together. `uniq -u` prints only unique lines.

**Skills Learned:** Pipelines · Text processing workflow

---

## Level 9 → 10

**Objective:** Find a readable string preceded by `===` signs.

```bash
strings data.txt | grep "==="
```

**Explanation:** `strings` extracts readable text from binary-like files. `grep` filters the relevant line.

**Skills Learned:** Binary inspection · Useful forensic technique

---

## Level 10 → 11

**Objective:** Decode Base64 data.

```bash
base64 -d data.txt
```

**Explanation:** Base64 is encoding, not encryption. `-d` decodes encoded text back to original content.

**Skills Learned:** Data encoding concepts · Decoding workflows

---

## Level 11 → 12

**Objective:** Decode ROT13 text.

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

**Explanation:** ROT13 rotates letters by 13 positions. `tr` translates characters from one set to another.

**Skills Learned:** Character substitution · Text transformation

---

## Level 12 → 13

**Objective:** Recover password from repeatedly compressed hexdump data.

```bash
xxd -r data.txt > data
file data
# then repeatedly use gunzip / bunzip2 / tar -xf
```

**Explanation:** This level required identifying each compression layer, then applying the correct decompression tool until plain text appeared.

**Skills Learned:** Hexdump reversal · Nested archive handling · Methodical troubleshooting · Trusting `file` output over guessing

---

## Level 13 → 14

**Objective:** Use an SSH private key instead of a password.

```bash
chmod 600 keyfile
ssh -i keyfile bandit14@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit14
```

**Explanation:** Private keys must have restricted permissions. `-i` tells SSH which identity file to use.

**Skills Learned:** Key-based authentication · Permission hardening · Local vs remote file context

---

## Level 14 → 15

**Objective:** Send the current password to a service on port 30000.

```bash
echo PASSWORD | nc localhost 30000
```

**Explanation:** `nc` (netcat) opens a TCP connection. The password is sent to the listening service, which returns the next password.

**Skills Learned:** Ports and services · Client/server communication · Meaning of `localhost`

---

## Level 15 → 16

**Objective:** Send the password over TLS on port 30001.

```bash
echo PASSWORD | openssl s_client -connect localhost:30001 -quiet
```

**Explanation:** Unlike plain TCP, this level required encrypted communication using TLS.

**Skills Learned:** TLS basics · Secure connections · OpenSSL client usage

---

## Level 16 → 17

**Objective:** Scan ports 31000–32000, identify the correct TLS service, submit the password, and obtain an SSH key.

```bash
nmap -p 31000-32000 localhost
openssl s_client -connect localhost:PORT -quiet
```

**Explanation:** Open ports were tested individually. Some were decoys, one echoed input, and one valid TLS service returned the private key for bandit17.

**Skills Learned:** Reconnaissance · Port scanning · Service fingerprinting · Distinguishing signal from noise

---

## Key Skills Learned

| Category | Skills |
|----------|--------|
| Shell | Linux shell confidence, file & directory handling |
| Search | `find`, `grep`, `strings`, search automation |
| Permissions | Linux permissions model, key-based auth |
| Encodings | Base64, ROT13, hexdump, text transformations |
| Compression | gzip, bzip2, tar — nested archive handling |
| Networking | TCP/UDP basics, ports, netcat, TLS, OpenSSL |
| Mindset | Persistence through debugging, methodical troubleshooting |

---

## Final Reflection

Bandit Level 0 → 17 was more than a set of puzzles. It was practical training in how Linux systems behave, how services communicate, and how to think like a problem solver. Every mistake became a lesson, and every solved level increased confidence.

This journey built a strong foundation for deeper cybersecurity learning in penetration testing, system administration, and CTF problem solving.

---

## Next Goal

Continue Bandit beyond Level 17 and keep documenting progress publicly on [GitHub](https://github.com/Pavan-glitch22), [LinkedIn](https://www.linkedin.com/in/pavan-n-cosmic/), and [Medium](https://medium.com/@Pavan_cosmic).
