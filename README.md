# My OverTheWire Levels (1-20) Completion
Welcome to my walkthrough to the doucmentation of my overthewire bandit challenge! 
- Part 1 includes a quick summary table of what the level entails.
- Part 2 includes a detailed version of the completed individual bandit levels including the password and most importantly how i tackled it, learnt from it.
- Part 3 includes the different resources i used to tackle each level.
- Part 4 includes my future objectives after the completing levels 1-20 of this challenge.
   

> [!IMPORTANT]
> **DISCLAIMER:** This repository contains solutions and passwords for the OverTheWire Bandit wargame. These are intended for educational purposes and documenting my personal learning journey. If you are currently playing Bandit, I highly recommend trying the levels yourself before looking at the solutions!


## 📊 1. Quick Progress Summary

| Level Range | Status | Focus / Tools Mastered |
| :--- | :--- | :--- |
| **0 - 5** | ✅ Complete | **File Navigation:** `cat`, `ls -a`, `file`, handling spaces/dashes |
| **6 - 10** | ✅ Complete | **Data Searching:** `find` (size/user/group), `grep`, `sort`, `uniq` |
| **11 - 15** | ✅ Complete | **Encryption & Transformation:** `base64`, `tr` (ROT13), `tar`, `gzip`, `xxd` |
| **16 - 20** | ✅ Complete | **Networking & Security:** `nmap`, `ncat` (SSL), `diff`, `setuid` binaries |

---

## 📝 2. Individual Level Write-ups

<details>
<summary><b>Levels 0 - 5: File Navigation</b></summary>

### Level 0 → 1
* **Password:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`
* **Command:** `cat readme`
* **What I Learnt:** Basic file system interaction and connecting to remote servers via SSH on non-standard ports (2220).
* **Logic:** Accessed the home directory and used `cat` to output the string stored in the cleartext readme file.

### Level 1 → 2
* **Password:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`
* **Command:** `cat ./-`
* **What I Learnt:** Handling special characters in filenames.
* **Logic:** A filename named `-` is often mistaken by the shell as an argument. Using the relative path `./-` clarifies that I am targeting a file.

### Level 2 → 3
* **Password:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`
* **Command:** `cat "spaces in this filename"`
* **What I Learnt:** Space preservation in Bash.
* **Logic:** Wrapped the filename in double quotes to ensure the shell read the entire string as a single object rather than multiple arguments.

### Level 3 → 4
* **Password:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`
* **Command:** `ls -a` -> `cat ...Hiding-From-You`
* **What I Learnt:** Identifying hidden "dot" files.
* **Logic:** Standard `ls` hides files starting with a period. Used the `-a` flag to reveal the hidden directory and password file.

### Level 4 → 5
* **Password:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`
* **Command:** `file ./*`
* **What I Learnt:** Analyzing file metadata to find human-readable data.
* **Logic:** When faced with multiple files, I used the `file` command to skip binary data and locate the only ASCII text file.
</details>

<details>
<summary><b>Levels 6 - 10: Data Searching</b></summary>

### Level 5 → 6
* **Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`
* **Command:** `find . -type f -size 1033c ! -executable`
* **What I Learnt:** Advanced `find` filtering.
* **Logic:** Filtered by type (file), exact size in bytes (`1033c`), and excluded executable files to narrow down the search in a large directory tree.

### Level 6 → 7
* **Password:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`
* **Command:** `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`
* **What I Learnt:** Permissions and error redirection.
* **Logic:** Searched the root directory for specific ownership. Redirected `stderr` to `/dev/null` to suppress thousands of "Permission Denied" warnings.

### Level 7 → 8
* **Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`
* **Command:** `grep "millionth" data.txt`
* **What I Learnt:** Pattern matching in large datasets.
* **Logic:** Used `grep` to isolate a specific line of text from a file containing millions of entries.

### Level 8 → 9
* **Password:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`
* **Command:** `sort data.txt | uniq -u`
* **What I Learnt:** Pipelining and data de-duplication.
* **Logic:** `uniq` only detects duplicates on adjacent lines. I sorted the file first, then used `-u` to extract the only unique string.

### Level 9 → 10
* **Password:** `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`
* **Command:** `strings data.txt | grep "=="`
* **What I Learnt:** Extracting strings from binary data.
* **Logic:** Used `strings` to ignore binary junk and `grep` to find the password signaled by the `==` prefix.
</details>

<details>
<summary><b>Levels 11 - 15: Encryption & Transformation</b></summary>

### Level 10 → 11
* **Password:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`
* **Command:** `base64 -d data.txt`
* **What I Learnt:** Handling common encoding formats.
* **Logic:** Recognized the Base64 format and used the `-d` (decode) flag to revert it to plaintext.

### Level 11 → 12
* **Password:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`
* **Command:** `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`
* **What I Learnt:** Substitution ciphers (ROT13).
* **Logic:** Used `tr` to rotate alphabet characters by 13 positions, effectively decrypting the message.

### Level 12 → 13
* **Password:** `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`
* **Command:** `xxd -r`, `tar`, `gzip`, `bzip2`
* **What I Learnt:** Reverse hex-dumping and multi-layered compression.
* **Logic:** Converted a hex dump back to binary using `xxd`, then used `file` at every step to identify the compression type (Gzip/Bzip2/Tar) to decompress it layer by layer.

### Level 13 → 14
* **Password:** `MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS`
* **Command:** `ssh -i sshkey.private bandit14@localhost`
* **What I Learnt:** Key-based authentication vs. password authentication.
* **Logic:** Leveraged a private RSA key. Ensured file permissions were set to `400` so the SSH agent would accept the key as secure.

### Level 14 → 15
* **Password:** `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`
* **Command:** `nc localhost 30000`
* **What I Learnt:** Direct socket communication via Netcat.
* **Logic:** Connected to a local port and submitted the current level password to receive the next credential.
</details>

<details>
<summary><b>Levels 16 - 20: Networking & Security</b></summary>

### Level 15 → 16
* **Password:** `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx`
* **Command:** `ncat --ssl localhost 30001`
* **What I Learnt:** Secure network communication (SSL/TLS).
* **Logic:** Used `ncat` with the `--ssl` flag to communicate with a port requiring an encrypted handshake.

### Level 16 → 17
* **Password:** `EReVavePLFHtFlFsjn3hyzMlvSuSAcRD` (RSA Key)
* **Command:** `nmap -p 31000-32000 localhost`
* **What I Learnt:** Automated port scanning and service identification.
* **Logic:** Scanned the target range to find open ports, then used SSL to submit the password to the correct listener to retrieve an RSA private key.

### Level 17 → 18
* **Password:** `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO`
* **Command:** `diff passwords.old passwords.new`
* **What I Learnt:** Comparing file deltas.
* **Logic:** Used `diff` to find the unique change between two versions of a password file.

### Level 18 → 19
* **Password:** `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8`
* **Command:** `ssh bandit18@host 'cat ~/readme'`
* **What I Learnt:** Bypassing restrictive shell environments.
* **Logic:** The account was configured to log out immediately upon shell initialization. I bypassed this by passing the `cat` command directly to SSH without requesting an interactive shell.

### Level 19 → 20
* **Password:** `[REDACTED]`
* **Command:** `./bandit20-do cat /etc/bandit_pass/bandit20`
* **What I Learnt:** Privilege escalation via SetUID binaries.
* **Logic:** Exploited a binary with the SetUID bit set, allowing me to execute commands with the higher permissions of the `bandit20` user.
</details>

---

## 🛠️ 3. Resources Used
* **OverTheWire Bandit:** [Official Site](https://overthewire.org/wargame/bandit/)
* **Linux Man/Help Pages:** Used `man [command]` &  `[command] --help`extensively to understand flags.
* **[TLDR Pages](https://tldr.sh/):** Used for simplified command-line examples and quick syntax lookups.
* **Theoretical Research:** Used Google,Wikipedia and AI tools for researching specific concepts like SetUID and ROT13.
* **Peer Collaboration:** Engaged with my CoderCo Community to discuss logic and troubleshoot high-level concepts with fellow peers.

## 🚀 4. Future Goals
- [ ] Complete Bandit Levels 21-34
- [ ] To learn and document bash script automation.
