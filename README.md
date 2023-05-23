# av-bypass
## Windows AV Bypass - Lab Test

## - Intro
A Youtube video by @xct_de (Martin Milke) [Vulnlab | Wutai: Writing a Loader & Getting a Beacon](https://www.youtube.com/watch?v=dShZR6FUV2w) showed a way to create a method to bypass Windows Defender for a Sliver beacon implant shellcode. Previously, I created a Active Directory Lab using my repo [active-directory](https://github.com/jjkirn/active-directory) together with my repo [sliver-c2](https://github.com/jjkirn/sliver-c2) and I was looking for a way to bypass Windows Defender for the beacon implants. This repo shows how it was done in @xct's video. I have included the source code for all the steps needed to complete the bypass.

## - Steps
- Perform the [steps documented for creating the beacon implant shellcode via sliver on Kali](/linux/kali.md) and move output to Windows.
- [Use the steps shown here](/windows/windows.md) to complete the goal - get a beacon call back to sliver without Defender blocking it!


