# ReturnCheck

# Description/About

A working Return Check bypass. Look down below for Information and a Bypass for the Return Check.

# Info

Where is the Return Check located? It is primary located in ROBLOX's Lua C Functions. Not all Lua C Functions found in ROBLOX have the Return Check. The Return Check's Signature is: 72 ?? A1 ?? ?? ?? ?? 8B just go to IDA, Search->Sequence Of Bytes.

This changes a JB instruction into a JMP, therefore allowing to call the function without client disconnection. But ROBLOX has a Memory Check! ROBLOX's Memory Check takes a while to protect and scan for any changes made to Memory. We can quickly make the modifications and restore it before the Memory Check can detect the changes.

# Credits

Credits go to M3m0ryH4cker#7089, Thanks to Variable for releasing a method how to bypass the Return Check. We will use that method to bypass the Return Check, known as changing a JB instruction into a JMP then restoring that JMP back into a JB.
