---
title: "Self-Hosting: Immich, Nextcloud, and the Trade-Offs"
description: "Storage architecture, backups, security risks, and why self-hosting your own cloud is empowering but not always rational."
publishDate: "18 Feb 2026"
updatedDate: 18 Feb 2026
tags: ["self-hosting", "linux", "devops", "cloud", "docker"]
coverImage:
  src: "./cover.png"
  alt: "Self hosted cloud architecture diagram"
---

## Introduction

At some point, paying for cloud storage starts to feel unnecessary.

You look at your monthly bill. You look at your server. You think:

> I can do this myself.

So I did.

I deployed **Immich** for photo management.  
I deployed **Nextcloud** for file sync and collaboration.  
I stopped relying on fully managed SaaS storage platforms.

It felt empowering.

But self-hosting your own cloud is not always rational.

This post breaks down the real trade-offs: storage design, backups, security risks, cost, and responsibility.

---

## Architecture Overview

My simplified stack:

- Immich (photo management)
- Nextcloud (file sync and sharing)
- Docker-based deployment
- Reverse proxy (Caddy or Nginx)
- Cloudflare at the edge
- Tailscale for private management access
- Scheduled local and offsite backups

### Example Deployment

```bash
docker compose up -d
```

Deployment is simple.

Long-term reliability is not.

---

## Private Access Strategy (Why I Use Tailscale)

Public exposure is convenient.

But when something breaks — reverse proxy misconfig, firewall mistake, DNS issue — you don’t want to depend on your public endpoint to fix it.

That’s where Tailscale comes in.

I use Tailscale as a private mesh network to:

- Access the server securely without opening SSH to the public internet
- Debug services when the reverse proxy fails
- Perform maintenance without relying on public DNS
- Recover from misconfigurations safely

Instead of exposing port 22:

- No direct SSH from the internet
- No port forwarding on the router
- No public SSH attack surface

I can simply:

```bash
ssh user@100.x.x.x
```

Or use the Tailscale hostname.

This gives me:

- Encrypted point-to-point access
- Zero-trust style connectivity
- A recovery path when public access fails

Self-hosting without a private management channel is risky.

If you:

- Break TLS
- Misconfigure Cloudflare
- Mess up firewall rules
- Lock yourself out

You need a way back in.

Tailscale acts as the control plane.

Public services are for users.  
Tailscale is for operations.

That separation matters.

---

## Storage Architecture (The Part Most People Ignore)

Running a cloud application is easy.

Running a reliable storage backend is where things become serious.

### Critical Questions

- Are you using RAID or single disk?
- What filesystem are you running?
- Where are backups stored?
- What happens if a disk fails?
- What happens if the entire server fails?

### Example Backup Strategy

- RAID1 or ZFS mirror for redundancy
- Separate physical drive for local backups
- Nightly offsite backup
- Daily database dumps

```bash
docker exec nextcloud-db mysqldump -u root -pPASSWORD nextcloud > backup.sql
```

If you do not have at least three copies of your data, you do not have a cloud.  
You have a single point of failure.

---

## Immich vs Nextcloud

They solve different problems.

| Feature       | Immich              | Nextcloud           |
|---------------|--------------------|---------------------|
| Primary Use   | Photo management    | File sync & share   |
| AI Tagging    | Yes                 | Limited             |
| Mobile App    | Excellent           | Good                |
| Performance   | Media optimized     | General purpose     |
| Complexity    | Lower               | Higher              |

Immich is modern and focused.

Nextcloud is broader and more enterprise-oriented.

Running both makes sense when responsibilities are clearly separated.

---

## Security Risks Nobody Mentions

When you self-host, you become the cloud provider.

That means:

- Managing TLS certificates
- Applying security patches
- Securing open ports
- Monitoring logs
- Handling intrusion attempts

A single misconfigured firewall rule can expose everything.

Minimum requirements:

- Reverse proxy with HTTPS
- Strong authentication
- Fail2ban or rate limiting
- Closed unused ports
- Log monitoring

```bash
journalctl -u docker -f
```

There is no support ticket system.  
You are operations and security.

---

## The Backup Reality

Large cloud providers offer:

- Multi-region replication
- Automated failover
- Distributed storage systems

A typical self-hosted setup offers:

- One machine
- One power supply
- One internet connection

If your ISP goes down, your cloud goes down.  
If your hardware fails, your cloud goes down.

Self-hosting shifts responsibility. It does not eliminate risk.

---

## Cost: Is It Actually Cheaper?

### SaaS Cloud Storage

- Predictable pricing
- No hardware cost
- Minimal maintenance
- High redundancy

### Self-Hosting

- Hardware investment
- Electricity costs
- Maintenance time
- Monitoring overhead

If your time has value, self-hosting is rarely cheaper.

It is not primarily about saving money.

It is about control.

---

## When Self-Hosting Makes Sense

Self-host if:

- You enjoy managing infrastructure.
- You understand backup strategies.
- You are comfortable troubleshooting failures.
- You want full data ownership.

Do not self-host if:

- You want zero maintenance.
- You do not monitor your systems.
- You expect SaaS-level redundancy without building it.

---

## What I Learned

1. Self-hosting is empowering.
2. Backups matter more than uptime.
3. Storage architecture is critical.
4. Cloud convenience is underrated.
5. Ownership comes with operational responsibility.

I continue to self-host.

But I do it knowing I am now responsible for uptime, security, and data durability.

---

## Conclusion

Self-hosting Immich and Nextcloud provided:

- Deeper understanding of storage systems
- Better operational discipline
- Greater control over data

It also introduced:

- Increased responsibility
- More monitoring tasks
- Additional failure scenarios

Self-hosting is not about avoiding the cloud.

It is about becoming your own cloud provider.

And that always has a cost.

---

## Resources

- https://immich.app  
- https://nextcloud.com  
- https://tailscale.com  
- https://docs.docker.com  
- https://cloudflare.com  

---

Build your backup strategy first.  
The applications come second.
