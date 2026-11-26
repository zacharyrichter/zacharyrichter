# Hey, I'm Zach

I'm an IT support tech. I get to touch some of the bigger systems at work too, and I'm lucky to have a sysadmin there who's generous about teaching me. The rest of my learning happens at home, in a homelab that started as "let me self-host a few things" and grew into separate networks, certificate-based logins and a lot of lessons learned the hard way.

Where I'm headed: sysadmin, or network or identity engineering. Identity is the part I find most interesting. Who gets in, how you prove it, and what they can reach once they're in shows up in almost everything I build (single sign-on, SSH certificates, hardware keys).

I learn by building something, breaking it, and writing down what happened so I don't break it the same way twice. That last part is why every project below has a "what went wrong" section. Those are my favorite parts to write.

## Stuff I've built

**[air-gap-the-keys](https://github.com/zacharyrichter/air-gap-the-keys)**
I asked myself one uncomfortable question: *if my everyday PC gets compromised, what can an attacker reach?* The honest answer was "everything." So I rebuilt how I get into my own lab: an SSH certificate authority, hardware keys, one locked-down jump host, and a root key that lives offline. The write-up includes the ideas I rejected and the isolation claims that turned out to be weaker than I thought.

**[trust-but-verify](https://github.com/zacharyrichter/trust-but-verify)**
Twenty-plus containers means a constant choice between "update everything blindly" and "never update anything". I built a pipeline that opens a pull request for every update and only deploys the ones I've approved. It also refuses to touch the few services where a surprise restart would take down the tooling doing the updating. It includes the bugs that ate my evenings, like a misspelled config key that silently turned off half my rules.

**[trust-no-cache](https://github.com/zacharyrichter/trust-no-cache)**
A hardened VPS running services that apps talk to, so there's no login page to hide behind. The firewall and the reverse proxy both follow one allowlist that tracks my home IP, and the server has no route back into my house. It also has a postmortem of the time removing one "unused" package took my server offline two weeks later.

**[homelab-compose](https://github.com/zacharyrichter/homelab-compose)**
The real Docker Compose files that run my lab, with the secrets and addresses swapped out. If you're learning Docker, the homepage stack is a good place to start.

## How I like to work

- I'd rather check what a system is actually doing than trust a green checkmark.
- I'd rather have an explicit rule than a setup that works because of timing.
- I write docs against the running system and fix them when they drift, so they stay useful.
- I'm still learning, and I'd rather say "I haven't touched that yet" than bluff.

## What's in the lab

Debian and Fedora, Proxmox, OPNsense, Docker, Traefik, WireGuard, Ansible, Authentik, Wazuh, and more. The repos above show how much of it I've written up so far.
