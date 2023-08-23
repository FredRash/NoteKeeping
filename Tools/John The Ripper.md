```bash
# Single Crack Mode
john --format=sha256 hashes_to_crack.txt

# Wordlist Mode
john --wordlist=<wordlist_file> --rules <hash_file>

# Incremental Mode
john --incremental <hash_file>

# Cracking Files with John
<johnTool> <file_to_crack> > file.hash
john file.hash

# getting all the tools 
locate *2john*

# Crack SSH keys
ssh2john SSH.private > ssh.hash
john --wordlist=rockyou.txt ssh.hash

# Crack MS Office documents
office2john Protected.docx > protected-docx.hash
john --wordlist=rockyou.txt protected-docx.hash

# Crack PDF files
pdf2john PDF.pdf > pdf.hash
john --wordlist=rockyou.txt pdf.hash
```