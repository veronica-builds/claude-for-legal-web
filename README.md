# Claude Projects Adaptation

A full adaptation of the Anthropic claude-for-legal plugin suite for law firms using **claude.ai (Claude Projects)** — no Claude Code, no MCP servers, no slash commands required.

**What this is:** Project instructions and knowledge base files for each practice area, ready to upload to a Claude Project on claude.ai. The practice-area workflows are fully preserved using trigger phrases and retrieved skill files in place of slash commands.

**Source:** Based on `anthropics/claude-for-legal` and `knowledge-work-plugins/legal` (installed plugin).

---

## Folder Structure

```
claude-for-legal-web/
├── commercial-legal/
│   ├── instructions.md                        ← paste into Project instructions
│   └── knowledge-base/
│       ├── skill-contract-review.md
│       ├── skill-nda-triage.md
│       ├── skill-vendor-check.md
│       ├── skill-canned-responses.md
│       ├── skill-legal-risk-assessment.md
│       ├── skill-meeting-briefing.md
│       ├── skill-signature-request.md
│       └── playbook-positions-template.md
├── privacy/
│   ├── instructions.md
│   └── knowledge-base/
│       ├── skill-dpa-review.md
│       ├── skill-dsar-response.md
│       ├── skill-pia-generation.md
│       └── skill-compliance-check.md
├── employment/
│   ├── instructions.md
│   └── knowledge-base/
│       ├── skill-termination-review.md
│       ├── skill-investigation-workflow.md
│       ├── skill-leave-tracking.md
│       ├── skill-hiring-review.md
│       └── skill-policy-drafting.md
├── litigation/
│   ├── instructions.md
│   └── knowledge-base/
│       ├── skill-legal-hold.md
│       ├── skill-privilege-analysis.md
│       ├── skill-demand-letter.md
│       ├── skill-matter-intake.md
│       └── skill-chronology.md
├── ip-legal/
│   ├── instructions.md
│   └── knowledge-base/
│       ├── skill-trademark-clearance.md
│       ├── skill-cease-desist.md
│       ├── skill-oss-review.md
│       └── skill-fto-triage.md
└── ai-governance/
    ├── instructions.md
    └── knowledge-base/
        ├── skill-ai-inventory.md
        ├── skill-aia-generation.md
        ├── skill-vendor-ai-review.md
        └── skill-ai-regulation-gap.md
```

---

## Setup: One Project per Practice Area per Client

Each folder in this repo = one Claude Project on claude.ai. Do not combine practice areas, clients, or matters into a single project.

### Step 1: Create the Project

1. Go to claude.ai → Projects → New Project
2. Name it after the practice area (e.g., "Commercial Legal", "Privacy & Data Protection")
3. Set sharing: Team or Enterprise plan required to share with the practice group

### Step 2: Add the Instructions

1. Open the project → Settings → Custom Instructions
2. Open the practice area's `instructions.md` in this repo
3. Run the cold-start interview first (see below) to fill in the firm-specific placeholders marked `[FIRM NAME]`, `[SUPERVISING PARTNER]`, `[ESCALATE TO]`, etc.
4. Paste the completed instructions into the Custom Instructions field
5. Save

**Do not skip the cold-start interview.** The instructions contain placeholders that must be filled with firm-specific content (privilege legend, playbook positions, escalation contacts, jurisdiction preferences) before the project is safe to use in production.

### Step 3: Upload the Knowledge Base

1. Open the project → Knowledge Base (or Files)
2. Upload every `.md` file from the practice area's `knowledge-base/` folder
3. For playbook positions: open `playbook-positions-template.md`, fill in the firm's actual positions (acceptable ranges, escalation triggers, standard positions), save as a new file, upload that — do not upload the blank template

**File naming matters.** Leave file names exactly as they are. The trigger phrase system in the instructions references files by name (e.g., "retrieve skill-contract-review.md"). Renaming files breaks retrieval.

---

## Cold-Start Interview (Required Before First Use)

The cold-start interview populates the firm-specific content in each project's instructions. Run it once per practice area before production use.

**Protocol:**

1. Open the practice area project
2. In the first conversation, type:

   > "I am setting up this project's configuration. Please interview me to build the practice profile and playbook for [PRACTICE AREA]. Ask everything needed to configure workflows for our firm. Ask one category at a time."

3. Answer each question. Key categories the interview must cover:
   - Firm name, practice group name, supervising partner(s)
   - Privilege legend — exact firm-standard language (paste verbatim; Claude will embed it into all outputs)
   - Escalation contacts and routing by risk level
   - Jurisdiction preferences and primary markets
   - Playbook positions for each major clause/issue type (acceptable ranges, walk-away points)
   - Standard template preferences (tone, format, signature block language)
   - Any firm-specific policies or carveouts that override the defaults

4. At the end of the interview, type:

   > "Now draft the complete instructions block for this project based on my answers."

5. Copy the output and paste it into the Project custom instructions field (replacing the template)

6. Save the interview conversation — title it "Setup Interview — [Practice Area] — [Date]"

**When the playbook changes:** Reopen the setup interview conversation, describe the change, ask Claude to update the instructions block, copy the updated version into the instructions field.

---

## Trigger Phrases: How to Use Each Skill

There are no slash commands. Type the trigger phrase to activate a workflow.

### Commercial Legal

| Say this | Activates |
|---|---|
| "review this contract" + paste/upload | Full contract review workflow |
| "triage this NDA" + paste/upload | NDA screening with GREEN/YELLOW/RED |
| "vendor check" | Vendor agreement status compilation |
| "draft a response" + describe the request | Canned response templates |
| "risk assessment" + describe the situation | Risk matrix and memo |
| "meeting briefing" + meeting details | Pre-meeting briefing document |
| "signature request" + contract name | Pre-signature checklist and instructions |

### Privacy

| Say this | Activates |
|---|---|
| "DPA review" + paste/upload | GDPR Article 28 DPA checklist |
| "draft DSR response" + paste the request | Data subject rights response workflow |
| "PIA" or "DPIA" + describe the project | Privacy impact assessment generation |
| "compliance check" + describe the activity | Multi-regulation compliance gap analysis |

### Employment

| Say this | Activates |
|---|---|
| "termination review" + employee details | Termination risk analysis |
| "open investigation" + incident description | Investigation matter file and workflow |
| "review leave log" + upload spreadsheet | FMLA/ADA/state leave analysis |
| "hiring review" + paste offer/NCA | Offer letter and restrictive covenant review |
| "draft policy" + topic | Policy template and multi-state review |

### Litigation

| Say this | Activates |
|---|---|
| "draft litigation hold" + matter description | Legal hold notice and log entry |
| "privilege analysis" + paste/upload | Document classification and privilege log |
| "demand letter" or "C&D" | Incoming triage or outgoing letter draft |
| "matter intake" + facts | Full matter intake form |
| "build chronology" + upload documents | Factual chronology table |

### IP Legal

| Say this | Activates |
|---|---|
| "trademark clearance" + mark details | Clearance analysis and DuPont factors |
| "FTO triage" + technology description | Freedom-to-operate brief for patent counsel |
| "OSS review" + component list | License classification (permissive/copyleft/viral) |
| "C&D response" or "DMCA takedown" | Incoming triage or outgoing notice draft |

### AI Governance

| Say this | Activates |
|---|---|
| "AI inventory" or "classify this AI system" | EU AI Act tier classification + inventory entry |
| "AI impact assessment" or "AIA" | AI Impact Assessment document |
| "vendor AI review" or "review AI contract" | AI-specific vendor contract provisions review |
| "AI regulation gap" or "AI compliance gap" | Regulatory gap analysis and remediation plan |

---

## Replacing Automated Agents: Manual Workflows

The claude-for-legal plugin included scheduled agents (renewal watcher, docket watcher, leave tracker). Claude Projects cannot run on a schedule or pull from external systems. Replace them with these manual workflows:

### Contract Renewal Watcher

1. Calendar: recurring reminder, first Monday of each month
2. Responsible person downloads contract list from CLM as CSV/spreadsheet
3. Uploads to Commercial Legal project
4. Types: "renewal review: here is our contract list. Flag everything expiring in the next 90 days and generate a renewal action checklist."

### Docket Watcher

1. Set up PACER RSS feeds or a service (CourtAlert, Docket Alarm) to email alerts on active matters
2. Weekly: litigation paralegal pulls new filings from PACER
3. Uploads to Litigation project (or the matter-specific project)
4. Types: "docket update: here are the new filings. Update the matter status, flag deadlines, and identify any required responses."

### Leave Tracker

1. Maintain a shared leave register spreadsheet
2. Weekly: HR paralegal downloads current version
3. Uploads to Employment Legal project
4. Types: "review this leave log and flag any entries approaching FMLA limits, ADA accommodation thresholds, or state-specific maximum leave periods."

### Document Intake (replacing MCP file connectors)

Claude Projects cannot connect to Box, SharePoint, or your document management system. The upload protocol:

- **Contracts under 20 pages:** Paste the text directly into the conversation (better clause analysis than PDF OCR)
- **Longer contracts:** Download PDF from DMS, upload to the conversation
- **Legal research:** Web search is available in Projects and covers most standard research questions. For deep precedent work or citation verification, continue using Westlaw/Lexis and paste the relevant authority into the conversation
- **Court dockets:** Pull docket sheet from PACER, upload PDF or copy text
- **E-discovery documents:** Export privilege log or document summary from your review platform, upload to the Litigation project

---

## Knowledge Base Maintenance

**One person per practice group** should own the knowledge base files. When a playbook position changes, a new regulation applies, or a workflow needs updating:

1. Edit the relevant `.md` file in this repo
2. Delete the old version from the Claude Project's knowledge base
3. Upload the updated file

**What to update when:**

| Trigger | Files to update |
|---|---|
| Playbook position changes | `playbook-positions-template.md` (firm-filled version) + the relevant skill file if it references the specific position |
| New regulation enacted | Add or update the relevant skill file; update `instructions.md` regulations list |
| Regulation deadline changes | Update [VERIFY] notes in AI governance files; update any deadline references in instructions |
| Firm acquires operations in new jurisdiction | Update jurisdiction tables in `skill-termination-review.md`, `skill-leave-tracking.md`, `skill-hiring-review.md`, `skill-compliance-check.md` |
| Standard template changes (privilege legend, signature block) | Update `instructions.md` — the legend in instructions governs all output |
| New escalation contact or routing change | Update `instructions.md` escalation rules |

---

## Verification Checklist (Run Before Production Use)

After setup, run each of these tests before attorneys use the project on live matters:

### 1. Trigger test
Start a new conversation. Type each trigger phrase for the practice area. Confirm Claude loads the correct skill and begins the workflow step by step (not just a summary of it).

### 2. Guardrail test
Upload a contract with a red-flag clause (uncapped liability, criminal indemnification, unilateral termination right). Confirm Claude flags it correctly, classifies it RED, and outputs ATTORNEY REVIEW REQUIRED.

### 3. [VERIFY] test
Ask a jurisdiction-specific legal question (e.g., "What is the FMLA leave entitlement for employees at a 40-person company?"). Confirm the answer includes a [VERIFY] marker on the specific threshold.

### 4. Limitation test
Ask Claude to "pull the latest filing from PACER for [matter name]." Confirm it responds with the standard limitation statement ("I don't have access to PACER. Please upload...") rather than attempting retrieval or fabricating a result.

### 5. Privilege test
Request a privileged analysis output. Confirm the privilege legend appears verbatim as entered in the instructions.

### 6. Escalation test
Describe a scenario that should trigger escalation (e.g., for Employment: an employee complaint from a protected class member who recently filed an EEOC charge). Confirm Claude stops, identifies the escalation trigger, and recommends escalation to the contact named in the instructions.

### 7. Attorney review gate test
Request any complete output (contract review, PIA, AIA, risk assessment). Confirm the output ends with ATTORNEY REVIEW REQUIRED specifying what the attorney must verify.

---

## Architecture Notes

### Why one project per practice area

Custom instructions degrade in quality when they cover too many domains. A single firm-wide project would need instructions covering every practice area's trigger phrases, playbook positions, escalation rules, and guardrails — this creates noise that reduces retrieval quality across all of them. One project per practice area = clean, focused system prompts.

### Why guardrails live in instructions, not only the knowledge base

Knowledge base files are retrieved on demand — they surface when a relevant trigger phrase is used. Instructions are always active. Guardrails that must never be missed (privilege flags, attorney review gates, [VERIFY] markers, escalation triggers) go in the instructions field so they apply to every single output, not just the ones where the right skill file happens to be retrieved.

### Why files are named `skill-*.md`

Claude uses file names as retrieval signals. A file named `skill-contract-review.md` will be retrieved when the conversation involves contract review. A file named `legal-reference.md` will not. The naming convention is load-bearing — do not change it.

### Litigation: consider matter-specific projects

For high-sensitivity active matters, create a separate matter-specific project so client-specific context stays isolated. The shared Litigation project holds the general playbook and skill files. The per-matter project holds the matter profile, key documents, and any matter-specific instructions. This prevents cross-matter contamination in conversation memory.

---

## Priority Order for Rollout

| Priority | Practice Area | Reason |
|---|---|---|
| 1 | Commercial Legal | Highest volume; zero integration dependency; full value from prompt logic alone |
| 2 | Privacy | DPA review, DSAR responses, PIA generation are pure analysis; no connectivity required |
| 3 | Employment | High-frequency workflows; termination and investigation review are upload-friendly |
| 4 | Litigation | Higher setup complexity (matter isolation, privilege sensitivity); prove first three first |
| 5 | IP Legal | Good fit, but lower volume at most firms and heavier dependency on Westlaw/PatSnap for search |
| 6 | AI Governance | Rising urgency as EU AI Act enters enforcement; but instructions need firm's own AI inventory as input before the tools are fully useful |

---

## Source Repos

- [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) — full plugin suite (Apache 2.0)
- `knowledge-work-plugins/legal` — installed Claude Code plugin (source of SKILL.md content)
- [Anthropic Claude Projects documentation](https://support.claude.com) — instructions limits, file types, sharing
