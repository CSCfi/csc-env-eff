---
topic: connecting
title: Tutorial - Log in Puhti with ssh
---

# Log in Puhti with ssh

This tutorial requires that you have a [user account at CSC](https://docs.csc.fi/accounts/how-to-create-new-user-account/)
and it is a member of a project that [has access to Puhti service](https://docs.csc.fi/accounts/how-to-add-service-access-for-project/).

Different operating systems have a little bit different SSH-clients (programs that
you can use to take the connection with).

## Windows10

On Windows 10, you can use the *Windows Power Shell*
or [download Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), or 
[download and install MobaXterm](https://mobaxterm.mobatek.net/download.html).

In this tutorial, we assume you use Windows Power Shell. More examples can be found
in docs](https://docs.csc.fi/computing/connecting/).
- Select Windows Power Shell from the applications list (opens from the windows logo) or search for it
in the bottom bar search box.

- In the windows-blue terminal window type:
```bash
ssh <your_csc_username>@puhti.csc.fi
```
- replace above `<your_csc_username>` with your actual csc username, or training account
  which ever you're using, and press enter

## MacOS

In MacOS, you can use Terminal similarly as with Linux machines (see below). Simply open the Terminal application and type:
```bash
ssh <your_csc_username>@puhti.csc.fi
```

## Linux

Laptops and workstations running Linux typically have SSH installed. Simply open a terminal
and give:
```bash
ssh <your_csc_username>@puhti.csc.fi
```

- if you're connecting to Puhti (or that Puhti login node) for the first time, SSH will
  ask you if you trust the authenticity of the host, e.g.:

```text
The authenticity of host 'puhti-login1.csc.fi (86.50.164.166)' can't be established.
ECDSA key fingerprint is SHA256:EXhadfadsfsaffasjhdlfjhasdlfkjhadsl.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
- the first time you connect, you need to accept, but the key should not change for the next
  login (but be sure to check whether it's login1 or login2).
- Once you've logged in you'll see a greeting starting something like this:
```
Last login: Mon Dec 14 14:53:15 2020 from jabadabaduu.fi
┌─ Welcome ───────────────────────────────────────────────────────────────────┐
│         CSC - Tieteen tietotekniikan keskus - IT Center for Science         │
│            ____        __    __  _                                          │
│           / __ \__  __/ /_  / /_(_)   - -  -   -                            │
│          / /_/ / / / / __ \/ __/ /   - -  -   -                             │
│         / ____/ /_/ / / / / /_/ /   - -  -   -                              │
│        /_/    \__,_/_/ /_/\__/_/   - -  -   -                               │
│                                                                             │
│      Puhti.csc.fi - Atos BullSequana X400 - 682 CPU nodes - 80 GPU nodes    │
├─ Contact ───────────────────────────────────────────────────────────────────┤
│ Servicedesk : 09-457 2821, servicedesk@csc.fi   Switchboard : 09-457 2001   │
├─ User Guide ────────────────────────────────────────────────────────────────┤
│ https://docs.csc.fi                                                         │
├─ Manage my account ─────────────────────────────────────────────────────────┤
│ https://my.csc.fi/                                                          │
...

└─────────────────────────────────────────────────────────────────────────────┘
[<your username>@puhti-login1 ~]$
```
Now, you're ready to go. Note, however, that remote graphics will not work. You could
add X11-tunneling to your ssh-connection, by adding `-X` or `-Y` to your command, and
[in Windows a separate X11-emulator](),  but [for intesive remote graphics we recommend
using NoMachine](). 
