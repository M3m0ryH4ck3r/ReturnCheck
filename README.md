# ReturnCheck

# Description/About

A working Return Check bypass. Look down below for Information and a Bypass for the Return Check.

# Info

Where is the Return Check located? It is primary located in ROBLOX's Lua C Functions. Not all Lua C Functions found in ROBLOX have the Return Check. The Return Check's Signature is: 72 ?? A1 ?? ?? ?? ?? 8B just go to IDA, Search->Sequence Of Bytes.

This changes a JB instruction into a JMP, therefore allowing to call the function without client disconnection. But ROBLOX has a Memory Check! ROBLOX's Memory Check takes a while to protect and scan for any changes made to Memory. We can quickly make the modifications and restore it before the Memory Check can detect the changes, this means we won't shutdown since the Memory Check can take a while.

# Credits

Credits go to M3m0ryH4cker#7089, Thanks to Variable for releasing a method how to bypass the Return Check. We will use that method to bypass the Return Check, known as changing a JB instruction into a JMP then restoring that JMP back into a JB.

# Code

```cpp

void Unprotect(DWORD Address, int RetNum)
{
	DWORD Function = Address;
	for (int i = 0; i < RetNum; Function++)
	{
		char AddressOPCode = *(char*)Function;
		if (AddressOPCode == 0x72) /* Checks if it is a JB. */
		{
			char AddressSecondOPCode = *(char*)(Function + 0x12);
			if (AddressSecondOPCode == 0x72) /* Checks if the SecondAddress's OPCode is a JB. */
			{
				WriteProcessMemory(GetCurrentProcess(), *(LPVOID*)&Function, "\xEB", 1, NULL);
				i++;
			}
		}
	}
}

void Protect(DWORD Address, int RetNum) 
{
	DWORD Function = Address;
	for (int i = 0; i < RetNum; Function++)
	{
		char AddressOPCode = *(char*)Function;
		if (AddressOPCode == 0xEB) /* Checks if the Address is a JMP. */
		{
			char AddressSecondOPCode = *(char*)(Function + 0x12);
			if (AddressSecondOPCode == 0x72)
			{
				WriteProcessMemory(GetCurrentProcess(), *(LPVOID*)&Function, "\x72", 1, NULL);
				i++;
			}
		}
	}
}
```

