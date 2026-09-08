# Step 3: Client Intake Confirmation Email

**Client-facing draft. Requires supervising attorney review and approval
before sending. Contains no privileged case-strategy content by design.**

## Purpose

Turn the internal screening work from Steps 1-2 into a plain-language email
the client can receive: what the firm understands happened, what documents
the firm still needs, and what happens next.

## Inputs

- `{{LIABILITY_ANALYSIS_OUTPUT}}` - full output from Step 2
- `{{CHRONOLOGY_OUTPUT}}` - full output from Step 1 (for the missing-documents list)
- `{{CLIENT_NAME}}`
- `{{ATTORNEY_NAME}}`
- `{{FIRM_NAME}}`
- `{{JURISDICTION}}`

## Prompt

```
You are drafting a client intake confirmation email for a personal injury
law firm. The client is not a lawyer - write in plain language, no legal
jargon, no case citations, no statute numbers, and no discussion of
comparative fault exposure, defendant theories, or internal viability
ratings. This email confirms the firm is handling the matter and tells the
client what is needed from them next. It is not a legal opinion and must
not promise an outcome or a settlement value.

INTERNAL LIABILITY SCREENING (Step 2 - for your reference only, do not
quote legal analysis from this into the email):
{{LIABILITY_ANALYSIS_OUTPUT}}

INTERNAL FACT CHRONOLOGY AND GAPS (Step 1 - use this to build the client
document request list):
{{CHRONOLOGY_OUTPUT}}

Client name: {{CLIENT_NAME}}
Attorney name: {{ATTORNEY_NAME}}
Firm name: {{FIRM_NAME}}
Jurisdiction: {{JURISDICTION}}

Draft an email with the following structure:

SUBJECT LINE: a clear subject naming the firm and confirming the matter is
open (e.g. "Confirming Your Case with {{FIRM_NAME}}").

GREETING: addressed to {{CLIENT_NAME}}.

1. MATTER SUMMARY
   Two to four sentences restating, in the client's own plain terms, what
   happened and when (date and general nature of the incident), and
   confirming the firm has opened a file and is investigating. Do not state
   who is at fault or predict an outcome.

2. DOCUMENTS WE NEED FROM YOU
   A bulleted list built from the Step 1 "Documents Not Yet Received" and
   "Missing Facts" items, translated into plain requests the client can
   act on (e.g. turn "physical therapy notes referenced but not provided"
   into "Records from any physical therapy or follow-up treatment you've
   received"). Always include, regardless of what Step 1 found:
   - A signed HIPAA medical records authorization (note that the firm will
     provide this form separately if not already signed)
   - Photos or video of the scene, vehicles, property, or injuries, if any
     exist
   - Contact information for any witnesses
   - Copies of any insurance correspondence received so far
   - Documentation of missed work or lost income, if applicable
   Briefly explain, in one sentence per category, why the item is needed.

3. NEXT STEPS
   A short numbered list of what happens next and roughly when (e.g. firm
   requests records, firm follows up with the client, firm evaluates once
   materials are received). Include one line telling the client who to
   contact with questions ({{ATTORNEY_NAME}} at {{FIRM_NAME}}) and one line
   reminding them not to discuss the case or post about it on social media,
   and not to sign anything from an insurance company without checking with
   the firm first.

CLOSING: professional sign-off from {{ATTORNEY_NAME}}, {{FIRM_NAME}}.

Output only the finished email (subject line plus body), formatted for
direct copy into an email client. No internal notes, no headers other than
the three numbered sections above, no legal analysis carried over from
Step 2.
```

## Output

A client-ready draft email. Route to the supervising attorney for review
and any required edits before sending; do not send directly from workflow
output.
