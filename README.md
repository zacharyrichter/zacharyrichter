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

**[no-open-doors](https://github.com/zacharyrichter/no-open-doors)**
I wanted to share a couple of apps with people outside my house without opening a single port on my router. A small tunnel client dials out, one reverse proxy sits behind it, and a brute-force detector watches the logs before anything reaches the apps. It also has a postmortem of a harmless-looking log rotation that kept stopping my reverse proxy, and the second incident that showed me it was the same bug.

**[diff-is-the-audit](https://github.com/zacharyrichter/diff-is-the-audit)**
Twelve hosts, and the documents describing them kept drifting. So the standard became the playbook: run it in check mode and it shows exactly where a host has strayed. It also has my CIS hardening results, including every check I chose to accept as a failure and why.

**[expire-on-purpose](https://github.com/zacharyrichter/expire-on-purpose)**
My lab's SSH host certificates expire every year on purpose. Renewing them is one supervised run that keeps the signing key in RAM and checks that every host is serving the new certificate, and a monthly check tells me when the next run is due. It also has the reasoning for why I used Ansible and not a secrets engine.

**[no-mail-server](https://github.com/zacharyrichter/no-mail-server)**
Linux tools still expect a local mail server to report problems. I didn't want to run one, so every host sends through one short script to my own notification server. The unattended-upgrades report lands on my phone, and nothing listens on port 25.

**[backups-nobody-watches](https://github.com/zacharyrichter/backups-nobody-watches)**
My backups run at 1 a.m. on a weekend and nobody looks at them, so I built the system so a broken backup can't stay quiet. It covers where the backups live, why my database VMs get stopped instead of snapshotted, how I'd rebuild the backup server from the data alone, and the checks that prove the whole path works.

**[graceful-power-loss](https://github.com/zacharyrichter/graceful-power-loss)**
When the power goes, my router tells every Proxmox node to shut down its VMs and then itself before the battery runs out. It covers the chain from the UPS to the VMs, the one firewall rule it needs, and a way to test the shutdown path on one node without shutting anything down.

**[alerts-worth-a-look](https://github.com/zacharyrichter/alerts-worth-a-look)**
My security monitor only pushes an alert to my phone when it's worth a look. Everything else waits in a dashboard, and I tune the noise with rules and never by raising the threshold. It covers the rules, the exact-match allowlist for container healthchecks, and how I test the alert path end to end.

**[assume-it-walks](https://github.com/zacharyrichter/assume-it-walks)**
My laptop leaves the house, so I built it assuming it will be lost, stolen or used on hostile Wi-Fi. Nothing listens on it, unknown USB devices are blocked, all traffic goes through a WireGuard tunnel away from home, and its SSH keys are useless without a hardware key and PIN. It covers the build, the checklist for cutting it off if it goes missing, and the checks that prove it.

**[one-front-door](https://github.com/zacharyrichter/one-front-door)**
Every internal app signs in through one identity provider that only answers from inside my network. It covers how each app is wired in (OIDC, SAML or a forward-auth proxy), who can open what, and a tested way back in if my own admin account gets locked out.

**[narrow-tunnel](https://github.com/zacharyrichter/narrow-tunnel)**
Every device I own gets a full WireGuard tunnel home, but only the least it needs once it's in. Everyone gets the apps and the internet, a couple of admin devices get a few more rules, and a VPS fallback that can't reach home is switched on by hand. It covers the firewall rule order, why I dropped automatic failover, and how a lost device is cut off.

**[homelab-compose](https://github.com/zacharyrichter/homelab-compose)**
The real Docker Compose files that run my lab, with the secrets and addresses swapped out. If you're learning Docker, the homepage stack is a good place to start.

## How I like to work

- I'd rather check what a system is actually doing than trust a green checkmark.
- I'd rather have an explicit rule than a setup that works because of timing.
- I write docs against the running system and fix them when they drift, so they stay useful.
- I'm still learning, and I'd rather say "I haven't touched that yet" than bluff.

## What's in the lab

Debian and Fedora, Proxmox, OPNsense, Docker, Traefik, WireGuard, Ansible, Authentik, Wazuh, and more. The repos above show how much of it I've written up so far.
