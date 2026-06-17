---
title: The Missing Layer in AI Security
categories: [AI Security, privacy, Systems Design, Security, sidsblog]
tags: [AI security, data privacy, PII, GDPR, DPDP Act, LLM security, AI governance, cybersecurity, Security, privacy, sidsblog]
date: 2026-06-17T17:26:04+05:30
description: "Personal thoughts on mail as how it is unsecure and privay concerns regarding the service."
author: Siddhant Mulajkar
draft: false
---


# Stop Pasting Sensitive Data into AI Tools: The Hidden Risk No One Is Talking About

```
> Apologies for the huge gap in writing posts, got busy with other aspects and job. 

```

Most conversations about AI safety start in the wrong place.

They focus on:

- ChatGPT hallucinations  
- Claude data retention policies  
- Copilot enterprise controls  
- Model-level security and compliance  

But that’s not where real-world data exposure happens.

The risk happens earlier.

**Before the prompt. Before the model. Before any system logs anything.**

It happens in a much smaller, invisible moment:

```
> When someone copies production data and pastes it into an AI tool.
```

That moment takes seconds.

And it happens thousands of times a day inside engineering teams, data teams, and product workflows.

---

### The overlooked workflow that creates data leaks

A typical AI-assisted workflow looks like this:

1. Production data lives in logs, SQL dumps, or internal systems  
2. A developer or analyst needs help debugging or transforming it  
3. The data is copied into ChatGPT, Claude, Cursor, or Copilot  
4. The AI generates an output  

On paper, this seems harmless.

In reality, it often includes:

- Customer PII (emails, phone numbers, addresses)
- Government IDs (Aadhaar, PAN, SSN, passport numbers)
- API keys and authentication tokens
- Internal system logs and infrastructure metadata
- AWS, Kubernetes, or GPU identifiers

This creates a critical issue:

```
> Sensitive data leaves your controlled environment and enters an external AI system in seconds.

```

No audit step.  
No validation step.  
No warning.

---

### Why traditional AI governance tools miss this problem

Most AI governance frameworks focus on:

- Model access control  
- Enterprise data retention policies  
- API-level monitoring  
- Network security boundaries  

These are important — but they operate **after the data is already inside the system.**

The real gap is earlier:

### The “pre-prompt” decision layer

This is the moment where:

- A log file becomes a copy-paste action  
- A CSV becomes a prompt  
- A debugging session becomes data exposure  

This decision is usually:

- Unstructured  
- Individual-driven  
- Time-sensitive  
- Not audited  

And that’s exactly why it fails under pressure.


![Lavabit Image](/images/fortress/playground.png)


---

### Why this problem is growing now

Several shifts are accelerating this issue:

#### 1. AI tools are now default in workflows

Developers routinely use:

- ChatGPT  
- Claude  
- Cursor  
- GitHub Copilot  

These are embedded in daily work, not occasional tools.

### 2. Faster debugging expectations

Teams are expected to resolve issues faster than ever.

### 3. Larger production datasets

Modern logs contain:

- structured events  
- identifiers  
- user traces  
- infrastructure metadata  

### 4. No safe input layer exists

Most tools optimize for output quality, not input safety.

---

### The real question is not “Are people aware?”

Most engineers already know:

- Don’t paste secrets into AI tools  
- Don’t expose customer data  
- Be careful with production logs  

Awareness is not the issue.

The issue is:

```
> What does a safe workflow look like when speed matters?
```

Because in practice:

- Deadlines override caution  
- Debugging overrides policy  
- Convenience overrides compliance  

And that’s where leaks happen.

---

# Introducing Fortress Zero

To explore this gap, I built **Fortress Zero** — a browser-based tool that runs entirely locally.

Its purpose is simple:


```
> Detect and sanitize sensitive data before it reaches any AI tool.
```


### What it does

Fortress Zero identifies and replaces:

### Personally Identifiable Information (PII)

- Aadhaar (Verhoeff validated)
- PAN numbers
- Emails
- Phone numbers
- SSNs and passport numbers
- Credit cards (Luhn validated)
- IBANs (checksum validated)

### AI security risks

- API keys (sk-, AKIA*)
- JWT tokens
- Access credentials

### Infrastructure fingerprints

- AWS EC2 instance IDs  
- GPU UUIDs  
- Kubernetes pod names  
- Container IDs  
- MAC addresses  
- Kernel memory addresses  
- Function offsets from logs  

---

### How it works

Everything runs locally in the browser:

```
Your Data → Fortress Zero (local engine) → Sanitized Output → AI Tool

```

No servers.  
No telemetry.  
No network calls.

### Workflow

1. Paste logs / CSV / SQL / text  
2. Run sanitization  
3. Copy sanitized output  
4. Paste safely into AI tools  

---

### Why this approach matters

Most security tools operate at:

- infrastructure level  
- policy level  
- enterprise governance level  

Fortress Zero operates at a different layer:

> The human decision moment.

It assumes something simple:

- People will keep using AI tools  
- People will keep working under pressure  
- Copy-paste workflows are not going away  

So instead of restricting behavior, it:

> Makes the safe action the easiest action.

---

# Compliance relevance (GDPR, DPDP, CCPA)

This approach aligns with modern privacy frameworks:

### GDPR (EU)

- Article 25: Data protection by design  
- Article 32: Security of processing  
- Supports pseudonymization before processing  

### DPDP Act 2023 (India)

- Section 8(5): Security safeguards  
- Section 16: Cross-border data risks  

### CCPA (US)

- Reasonable security expectations for personal data handling  

Fortress Zero is not a compliance tool, but it helps demonstrate **due diligence before data leaves the machine.**

---

### Who this is for

This is relevant for:

- Software engineers  
- Data engineers  
- Security teams  
- AI product teams  
- Startups using LLMs  
- Enterprises with AI governance requirements  

---

### What this is NOT

Fortress Zero is not:

- A model firewall  
- A cloud DLP system  
- An enterprise governance suite  
- A replacement for security policy  

It is a **pre-prompt safety layer**.

A missing layer in most AI workflows today.

---

### Open questions

This project started as an observation, not a conclusion:

- Do teams actually have a defined “pre-AI data step”?  
- Or is it always individual judgment?  
- Can this be standardized without slowing work?  
- Where does automation help — and where does it fail?  

These are still open questions.

That’s why this exists.

---

### Try Fortress Zero

👉 Live Playground: https://sidmulajkar.com/fortress/playground.html

Or run locally:

- Download `playground.html`
- Open in browser
- Paste data → sanitize → copy → use safely

No setup. No dependencies. No accounts.

---

# Final thought

Most AI safety discussions focus on models, policies, and enterprise controls.

But the real risk is smaller — and more frequent.

It happens in a single action:

> Copy → Paste → Send

If we want safer AI systems in practice, not just in theory, we need to examine that moment more closely.

```
That is the gap Fortress Zero is exploring.

```

---

### Read More Blogs related to:

***[db-concepts]({{< relref "/tags/database/">}}) / [linux]({{< relref "/tags/linux">}}) / [flutter-installation]({{< relref "/tags/flutter">}}) / [networking]({{< relref "/tags/networking">}}) / [raspberry-pi]({{< relref "/tags/raspberry">}})***

--