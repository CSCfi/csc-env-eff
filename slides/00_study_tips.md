---
theme: csc-2019
lang: en
---
# Study tips for self learning {.title}

# Using these materials

- The material is organized by topics in increasing complexity
   - Feel free to jump if you know the basics already
- Read the slides / watch the video first
- Complete the tutorial to make sure you've got the steps right
- Try out one or more of the exercises to verify your new skill
- If you get stuck, consult [the docs](https://docs.csc.fi) linked to the topic slides

# General problem solving

1. Try in [docs.csc.fi](https://docs.csc.fi) in the right section in the *hierarchy*
2. Try in the [FAQ](https://docs.csc.fi/support/faq/)
3. Try the search in docs or google for it
4. Send an email to [servicedesk@csc.fi](mailto:servicedesk@csc.fi) containing:
   - A descriptive title
   - What you wanted to achieve, and on which which computer
   - Which commands you had given
   - What error messages resulted
   - [More tips to help us quickly solve your issue](https://docs.csc.fi/support/support-howto/))

# Learning a new method or application

- If it comes with tutorials, do at least one
   - This will likely be the fastest way forward
- Check if there's a page for it in [docs.csc.fi/apps/](https://docs.csc.fi/apps/)
   - If there is, use the batch script example from _there_
- First try a small / quick job and when you're sure it works, scale up   

# Document your discoveries

- When you've successfully solved an issue, make it easy to rediscover it
- Set up a file in your `$HOME` and add your commands there with keywords for yourself
   - e.g. it's quick to copy/paste your command from the screen to the end of the file

```bash
cat >> $HOME/vault
<copy/paste>
Ctlr-C
```

- and `grep`'ing it later is quick
- Store scripts in `$HOME/bin` and take backups

# Keep notes

Save useful commands and short scripts to a file for later reference, and push
your notes to GitHub every now and then. Bash history keeps all the commands
that you typed, but it also keeps the ones that did not work...
