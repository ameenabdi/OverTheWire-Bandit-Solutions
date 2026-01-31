# OverTheWire-Bandit-Solutions
Walk through of my completion of the 1-20 Overthewire Bandit levels!

## 📊 Quick Progress Summary

| Level Range | Status | Focus / Tools Mastered |
| :--- | :--- | :--- |
| **0 - 5** | ✅ Complete | **File Navigation:** `cat`, `ls -a`, `file`, handling spaces/dashes |
| **6 - 10** | ✅ Complete | **Data Filtering:** `find` (size/user/group), `grep`, `sort`, `uniq` |
| **11 - 15** | ✅ Complete | **Cryptography & Archives:** `base64`, `tr` (ROT13), `tar`, `gzip`, `xxd` |
| **16 - 20** | ✅ Complete | **Networking & Permissions:** `nmap`, `ncat` (SSL), `diff`, `setuid` binaries |

# Bandit OverTheWire: Level 1-20 Full Walkthrough

## 📊 Quick Progress Summary
| Level Range | Status | Focus |
| :--- | :--- | :--- |
| **0 - 5** | ✅ Complete | Basic Navigation & Hidden Files |
| **6 - 10** | ✅ Complete | Advanced Searching & Filtering |
| **11 - 15** | ✅ Complete | Cryptography & Archive Handling |
| **16 - 20** | ✅ Complete | Networking & Privilege Escalation |

---

## 📝 Individual Level Write-ups

<details>
<summary><b>Levels 0 - 5: The Basics</b></summary>

### Level 0 → 1
* **Password:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`
* **Command:** `cat readme`
* **What I Learnt:** Basic file reading and connecting via SSH on a specific port (`2220`).

### Level 1 → 2
* **Password:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`
* **Command:** `cat ./-`
* **What I Learnt:** How to handle filenames that are identical to command flags. Using `./` tells the shell it's a path.

### Level 2 → 3
* **Password:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`
* **Command:** `cat "spaces in this filename"`
* **What I Learnt:** Using quotes to wrap filenames that contain spaces so the shell treats them as one argument.

### Level 3 → 4
* **Password:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`
* **Command:** `ls -a` then `cat ...Hiding-From-You`
* **What I Learnt:** Hidden files start with a `.` and require the `-a` (all) flag to be visible.

### Level 4 → 5
* **Password:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`
* **Command:** `file ./*` then `cat ./file07`
* **What I Learnt:** The `file` command is essential for identifying data types when filenames are misleading.
</details>

<details>
<summary><b>Levels 6 - 10: Data Searching</b></summary>

### Level 5 → 6
* **Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`
* **Command:** `find . -type f -size 1033c ! -executable`
* **What I Learnt:** Using `find` with specific parameters like size (`c` for bytes) and logical operators (`!`).

### Level 6 → 7
* **Password:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`
* **Command:** `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`
* **What I Learnt:** Searching the whole system and redirecting standard error (`2>`) to `/dev/null` to hide permission errors.

### Level 7 → 8
* **Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`
* **Command:** `grep "millionth" data.txt`
* **What I Learnt:** Using `grep` to find a specific string within a massive text file.

### Level 8 → 9
* **Password:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`
* **Command:** `sort data.txt | uniq -u`
* **What I Learnt:** `uniq` only works on adjacent lines, so data must be `sort`ed first.

### Level 9 → 10
* **Password:** `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`
* **Command:** `strings data.txt | grep "=="`
* **What I Learnt:** `strings` extracts human-readable text from binary files that `cat` can't display properly.
</details>

<details>
<summary><b>Levels 11 - 15: Encryption & Transformation</b></summary>

### Level 10 → 11
* **Password:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`
* **Command:** `base64 -d data.txt`
* **What I Learnt:** How to decode data that has been encoded in Base64 for transport.

### Level 11 → 12
* **Password:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`
* **Command:** `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`
* **What I Learnt:** Practical use of the `tr` (translate) command to solve a ROT13 substitution cipher.

### Level 12 → 13
* **Password:** `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`
* **Command:** `xxd -r`, `tar -xf`, `gunzip`, `bzip2 -d`
* **What I Learnt:** Nested compression. I had to use `file` repeatedly to see which tool to use next to "peel" the archive layers.

### Level 13 → 14
* **Password:** `MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS`
* **Command:** `ssh -i sshkey.private bandit14@localhost`
* **What I Learnt:** SSH Private Key authentication. I learned that keys must have strict permissions (`chmod 400`) to work.

### Level 14 → 15
* **Password:** `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`
* **Command:** `nc localhost 30000`
* **What I Learnt:** Using Netcat (`nc`) to interact with network services by piping strings directly to a port.
</details>

<details>
<summary><b>Levels 16 - 20: Networking & Security</b></summary>

### Level 15 → 16
* **Password:** `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx`
* **Command:** `ncat --ssl localhost 30001`
* **What I Learnt:** Establishing secure connections. Regular `nc` won't work for SSL/TLS ports; `ncat --ssl` or `openssl s_client` is required.

### Level 16 → 17
* **Password:** `EReVavePLFHtFlFsjn3hyzMlvSuSAcRD` (Key file)
* **Command:** `nmap -p 31000-32000 localhost` then `ncat --ssl`
* **What I Learnt:** Port scanning. Using `nmap` to find which ports are open and which one returns the RSA key.

### Level 17 → 18
* **Password:** `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO`
* **Command:** `diff passwords.old passwords.new`
* **What I Learnt:** Comparing file contents to find a single line of difference.

### Level 18 → 19
* **Password:** `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8`
* **Command:** `ssh bandit18@host 'cat ~/readme'`
* **What I Learnt:** How to bypass a `.bashrc` that automatically logs you out by sending a command directly through the SSH session.

### Level 19 → 20
* **Password:** `[REDACTED]`
* **Command:** `./bandit20-do cat /etc/bandit_pass/bandit20`
* **What I Learnt:** Understanding **SetUID**. The binary runs with the owner's privileges, allowing me to read a file my current user normally couldn't.
</details>
