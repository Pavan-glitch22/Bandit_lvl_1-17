# Bandit_lvl_1-17
````markdown
# OverTheWire Bandit Walkthrough (Level 0 → 17) 🚀

> A hands-on cybersecurity learning project focused on Linux, networking, troubleshooting, and problem-solving using the OverTheWire Bandit wargame.

---

## 📌 About This Project

This repository documents my progress through **OverTheWire Bandit Levels 0 to 17**.  
Bandit is designed to teach essential Linux and cybersecurity fundamentals through practical challenges.

Instead of only reading theory, I solved real tasks involving:

- Linux command-line usage
- File handling
- Permissions
- Searching and enumeration
- Encoding / decoding
- Compression formats
- SSH authentication
- Networking basics
- Port scanning
- Secure communication (TLS/SSL)
- Debugging mindset

---

## 🛠️ Lab Environment

| Item | Details |
|------|---------|
| OS | Kali Linux |
| Platform | Virtual Machine |
| Access Method | SSH |
| Challenge Site | OverTheWire |
| Levels Completed | 0 → 17 |

---

## 📚 Levels Completed

## 🔹 Level 0 → 1
### Objective
Connect to Bandit using SSH and read the password from `readme`.

### Commands
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
ls
cat readme
````

### Concepts Learned

* SSH login
* Listing files
* Reading file contents

---

## 🔹 Level 1 → 2

### Objective

Read a file named `-`

### Command

```bash
cat ./-
```

### Concepts Learned

* Special filenames
* Current directory paths

---

## 🔹 Level 2 → 3

### Objective

Read a file with spaces in its name.

### Command

```bash
cat "./--spaces in this filename--"
```

### Concepts Learned

* Quoting arguments
* Handling spaces in filenames

---

## 🔹 Level 3 → 4

### Objective

Find a hidden file in `inhere`

### Commands

```bash
cd inhere
ls -a
cat ...Hiding-From-You
```

### Concepts Learned

* Hidden files
* `ls -a`

---

## 🔹 Level 4 → 5

### Objective

Find the only human-readable file.

### Commands

```bash
file ./*
cat ./-file07
```

### Concepts Learned

* File type detection
* ASCII vs binary files

---

## 🔹 Level 5 → 6

### Objective

Find a file that is:

* 1033 bytes
* not executable
* human-readable

### Command

```bash
find . -type f -size 1033c ! -executable
```

### Concepts Learned

* Recursive search
* Filtering by file size
* Permissions logic

---

## 🔹 Level 6 → 7

### Objective

Find a file with:

* user: bandit7
* group: bandit6
* size: 33 bytes

### Command

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

### Concepts Learned

* Ownership
* Error redirection
* System-wide enumeration

---

## 🔹 Level 7 → 8

### Objective

Find the password next to the word `millionth`

### Command

```bash
grep millionth data.txt
```

### Concepts Learned

* Text searching
* Pattern matching

---

## 🔹 Level 8 → 9

### Objective

Find the only unique line.

### Command

```bash
sort data.txt | uniq -u
```

### Concepts Learned

* Sorting data
* Removing duplicates
* Pipelines

---

## 🔹 Level 9 → 10

### Objective

Find readable text in a binary-like file.

### Command

```bash
strings data.txt | grep "==="
```

### Concepts Learned

* Extracting readable strings
* Binary inspection

---

## 🔹 Level 10 → 11

### Objective

Decode Base64 data.

### Command

```bash
base64 -d data.txt
```

### Concepts Learned

* Encoding vs encryption
* Base64 decoding

---

## 🔹 Level 11 → 12

### Objective

Decode ROT13 text.

### Command

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### Concepts Learned

* Character translation
* ROT13 cipher

---

## 🔹 Level 12 → 13

### Objective

Recover password from layered compressed data.

### Workflow

```bash
xxd -r data.txt > data
file data
gunzip
bunzip2
tar -xf
```

### Concepts Learned

* Hexdump reversal
* Compression tools
* Nested archives
* Troubleshooting

---

## 🔹 Level 13 → 14

### Objective

Login using SSH private key.

### Commands

```bash
chmod 600 keyfile
ssh -i keyfile bandit14@bandit.labs.overthewire.org -p 2220
```

### Concepts Learned

* SSH keys
* File permissions
* Secure authentication

---

## 🔹 Level 14 → 15

### Objective

Send password to service on port 30000.

### Command

```bash
echo PASSWORD | nc localhost 30000
```

### Concepts Learned

* Netcat
* TCP communication
* Ports

---

## 🔹 Level 15 → 16

### Objective

Send password over TLS on port 30001.

### Command

```bash
echo PASSWORD | openssl s_client -connect localhost:30001 -quiet
```

### Concepts Learned

* TLS basics
* Encrypted communication

---

## 🔹 Level 16 → 17

### Objective

Scan ports 31000–32000 and identify the correct TLS service.

### Commands

```bash
nmap -p 31000-32000 localhost
openssl s_client -connect localhost:PORT -quiet
```

### Concepts Learned

* Port scanning
* Service discovery
* Reconnaissance
* Enumeration mindset

---

## 🧠 Key Skills Gained

* Linux command-line confidence
* File and directory handling
* Searching with `grep` and `find`
* Text processing
* Permissions management
* SSH authentication
* Networking fundamentals
* Port scanning with `nmap`
* Secure connections with OpenSSL
* Structured troubleshooting

---

## 💼 Career Relevance

This project demonstrates skills valuable for:

* Cybersecurity Analyst
* SOC Analyst
* Penetration Tester
* Linux Administrator
* DevOps Engineer
* CTF Competitor

---

## 🚀 Next Goals

* Continue higher Bandit levels
* TryHackMe labs
* Web security practice
* Python scripting
* Privilege escalation labs
* Build public cybersecurity portfolio

---

## 📖 Final Reflection

Bandit Level 0 → 17 was more than solving puzzles.
It was practical training in how Linux systems, files, permissions, and networks really work.

Every challenge improved my technical knowledge and problem-solving mindset.

This is only the beginning of my cybersecurity journey. 🔐🔥

```
```
