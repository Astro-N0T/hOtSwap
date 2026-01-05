# hOtSwap
This is mostly a place for me to dump my thoughts on a project idea: Automating the switch between OSs (specifically Windows to Linux).

### The Problem
Windows 10 is dying. Windows 11 has annoying hardware requirements. A lot of people want to switch to Linux but they're scared of losing their photos or messing up their partitions.

### The Idea
Build a tool that does the "scary stuff" for you.

* It shouldn't need a USB stick if possible.
* It needs to "shim" the transition—basically a middleman that lives in RAM, wipes the old OS, and moves your files into the new one.
* It’s like a brain transplant for your PC.

### Why I'm posting this
I'm a bachelor's student and I don't have all the answers yet. I know I'll need to figure out:

1. **Bootloaders:** How to not brick the BIOS.
2. **Permissions:** Mapping Windows users to Linux users.
3. **Networking:** Probably needs "host" mode access to handle data transfers without getting blocked by the OS firewall.

If you're into low-level systems stuff, feel free to open an issue or message me.
