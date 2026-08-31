# SME Cybersecurity Audit Engine

A rules-based cybersecurity audit engine for small and medium businesses (SMEs), built to identify real-world breach risk and deliver a plain-language, prioritised action plan, without requiring any technical knowledge from the business owner.

## The Problem

Cyber security breaches are now a routine part of doing business in the UK, and small and medium businesses are the least equipped to absorb the impact, financially, operationally, or reputationally.

- **46%** of small businesses identified a cyber security breach or attack in the last 12 months, rising to **65%** for medium-sized businesses.
- **38%** of businesses experienced phishing attacks, by far the most common type of breach.
- Only **19%** of businesses carried out any cyber security training or awareness activity for staff in the last 12 months, a figure that has remained flat year on year.

*(Source: Cyber Security Breaches Survey 2025–2026, DSIT and the Home Office)*

Unlike large organisations, SMEs typically have no dedicated IT security staff, no formal incident response plan, and no budget for external consultants. A breach a large firm could treat as manageable can be existential for a small one. What's missing isn't awareness that breaches happen, it's a structured way of telling a specific business, in plain language, exactly which door to close first. This project exists to do that.

## How It Works

The engine takes a business through **ten evidence-based diagnostic questions**, each mapped to a recognised security framework, and scores exposure against a fixed **Red / Amber / Green** model.

### The Ten Diagnostic Questions

**Q1 - Backup and Business Continuity**
If your most important device was stolen tonight, could the business keep running tomorrow, and would anything be permanently lost? When did you last restore something from your backup to check that it works?

**Q2 - Passwords and Multi-Factor Authentication**
Do all your business accounts, email, banking, and cloud tools require more than just a password to log in, and are those passwords long, unique, and not shared across more than one account?

**Q3 - Access Control and Former Staff**
Are there people, former staff, contractors, or old suppliers, who may still be able to access your business systems or files? Can you say who currently has access to each of your systems?

**Q4 - Staff Awareness and Phishing**
Do you and your staff know what a convincing scam looks like today, not five years ago, but now? When did you last have any training or briefing on it?

**Q5 - Shadow IT and App Risk**
How many tools and apps does the business use, and do you know what the free ones do with your data?

**Q6 - Past Incidents and Near Misses**
Has anything ever felt wrong, a suspicious email, a login alert you ignored, a call asking you to confirm your account details? What did you do about it, and did anything change as a result?

**Q7 - Offboarding and Leavers**
When a staff member or contractor leaves, what is the process for removing their access, and has it always been followed?

**Q8 - Supplier and Third-Party Access**
Do the suppliers and contractors who help run your business have access to your systems, and do you know how they protect it? Is there anything in writing covering that access?

**Q9 - Incident Response Readiness**
If your systems went down tonight, email inaccessible, files locked, what would you do in the first hour and who would you call? Is any of that written down, and when was it last checked or practised?

**Q10 - GDPR and Legal Obligations**
Does your business have a privacy policy, and do you know you may be legally required to report certain data incidents to the regulator within 72 hours? Has anything like that ever happened, and how was it handled?

These questions are grounded in **five root causes** behind most UK SME breaches, identified through NCSC and ICO research: phishing and staff deception, weak or stolen credentials, poorly configured systems, supply chain vulnerabilities, and poor access control.

### Frameworks Used

- **ISO 27001:2022**
- **NCSC Cyber Essentials**
- **GDPR / ICO Guidance**
- **NIST Cybersecurity Framework (CSF)**
- **CIS Controls v8**

## System Architecture

**1. The JSON Rules Engine**
A structured, version-controlled file that holds every scoring band, escalation trigger, and safety rule. It defines exactly what the model must do, and must never do, on every audit, keeping behaviour fixed regardless of which interface calls it.

**2. The Master Prompt**
A deliberately thin, replaceable layer that carries no scoring or safety logic itself. Its only job is passing input through to the JSON engine via an API connection, so the interface can change without ever affecting how the engine behaves.

**3. The Escalation Layer**
Live, active threats (for example, a former employee who may still have system access) are pulled out of normal scoring entirely rather than treated as a routine finding. These are routed straight to **mandatory human review** before anything reaches the client. A set of **do-not-touch safety rules** prevents the engine from ever instructing a client to remove access, delete data, reset a device, or alter a system directly. Every one of those actions must be agreed with a lead consultant first: **Stop. Document. Escalate. Agree. Then act.**

## Output

The final deliverable is a client-facing report containing:

- A business summary and overall risk rating (**Secure**, **Needs Attention**, or **At Risk**)
- A findings table across all ten domains, each with a written justification for its score
- An escalation section for any urgent, active threats, with an immediate first-hour response plan
- A prioritised **30-day action plan**, pairing each finding with a fix and an ongoing check, with urgent items always placed in week one

## Validation and Testing

The engine was tested against **five simulated businesses** (Bright Leaf Bakery, Aldridge Legal Associates, Marlow Design Studio, and two versions of Riverside Veterinary Clinic) to confirm ratings and escalations were consistent, not just correct once.

Each business was tested **twice per version, on separate days**, to surface any inconsistency caused by the engine inventing its own judgement calls rather than following a fixed rule. Every gap found was closed with an explicit rule, driving the engine through several versions, from v2 through to the final **v3.0.1**, at which point repeated testing confirmed identical outputs on every run.

## Tech Stack

- **JSON** — core rules engine and scoring logic
- **API-driven prompt layer** — thin, replaceable interface wrapper
- Framework alignment: ISO 27001, NCSC Cyber Essentials, GDPR, NIST CSF, CIS Controls v8

## Project Background

Built during an 8-week cybersecurity placement, this project moved through independent research into SME breach causes, question design, rules engine development, and a full regression testing programme, ending with a complete handover pack (rule provenance history, fixture set, regression procedure, and defect register) for future continuity.

## Disclaimer

Example reports and business names used in testing are entirely simulated fixtures created for validation purposes and do not represent real clients or businesses.
