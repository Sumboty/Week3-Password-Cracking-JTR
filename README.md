# Week 3 - Password Cracking with JTR & NW Tools | Networkwalks

## Modules Completed
- W3-PM1: Password Cracking with JTR (John + Johnny)
- W3-PM2: Password Cracking with NW Tools (Hash Calculator + Password Cracker)
- 7.2.1: HexStrike MCP + Claude Desktop Setup on Kali Linux

## Method - PM1: JTR John + Johnny
1. Extracted $pdf$ hash from locked PDF
2. Saved hash as hash1.txt (format: $pdf$...)
3. Opened hash1.txt in Johnny GUI
4. Clicked "Open password file" > "Start new attack"
5. Johnny cracked 100% (1/1: 1 cracked, 0 left) [format=PDF]

## Method - PM2: Networkwalks Tools
1. Hash Calculator: https://networkwalks.com/hash-calculator/
   - Uploaded locked PDF -> Got $pdf$ hash (R4 / 128-bit)
2. Password Cracker: https://networkwalks.com/password-cracker/
   - Pasted $pdf$ hash
   - Used Built-in list (100 passwords)
   - Dictionary attack: Hash every word, compare to PDF hash

## Results - Verified

### File 1: My Locked PDF1.pdf - password1
- Cracked Password: password1
- Tool 1: Johnny (JTR) - 100% cracked
- Tool 2: NW Password Cracker - Cracked at Tried: 91 / 100 - [+] MATCH password1
- Verified: PDF opened
- Flag 1: nw{networkwalks_persistence_jtr_270521}
- Flag 2: nw{cybersecurity_flag_captured_2608}

### File 2: My Locked PDF3.pdf - 1qaz2wsx
- Cracked Password: 1qaz2wsx
- Tool 1: Johnny (JTR) - 100% cracked
- Tool 2: NW Password Cracker - Cracked at Tried: 35 / 100
- Verified: PDF opened
- Flag: nw{networkwalks_flag_260821_1}

### Important Finding - Wordlist Size Matters
- NW Password Cracker with built-in 100-word list on another hash:
  Tried: 100 / 100 -> Exhausted wordlist. No match. ACCESS DENIED
- Same type of hash cracked by JTR with larger wordlist.
- Lesson: Small wordlist = fail. Larger wordlist / right wordlist = success.

## HexStrike MCP Setup (7.2.1)
1. Installed Claude Desktop on Kali Linux (Claude for Linux)
2. Cloned: https://github.com/0x4m4/hexstrike-ai.git
3. Created venv: python3 -m venv hexstrike-env
4. Installed: pip3 install -r requirements.txt
5. Ran: python3 hexstrike_server.py
6. Verified: Server starting on 127.0.0.1:8888, 150+ modules active, Running on http://127.0.0.1:8888
7. MCP Config in Claude Desktop:
```json
{
  "mcpServers": {
    "hexstrike-ai": {
      "command": "/home/kali/hexstrike-ai/hexstrike-env/bin/python",
      "args": ["/home/kali/hexstrike-ai/hexstrike_mcp.py", "--server", "http://localhost:8888"]
    }
  }
}
