# Personal Injury New Matter Intake & Case Screening Workflow

AI workflow for processing a new personal injury matter from raw intake
materials to a client-ready outcome letter. Built for internal case team
use during the initial screening window (first 48-72 hours).

## Before you start

Run the firm's standard conflicts-of-interest check against the client's
name, the adverse party's name, and any other party named in the intake
file before starting Step 1. This workflow does not perform a conflicts
check and assumes one has already cleared the matter for substantive work.

## Pipeline

```
Uploaded documents (intake notes, police report, medical records)
        |
        v
STEP 1: Fact Chronology & Gap Analysis  --------> step-1-fact-chronology.md
        | (chronology + missing facts/questions)
        v
STEP 2: Liability & Case Screening Analysis  ---> step-2-liability-analysis.md
        | (causes of action, defendants, SOL, comparative fault)
        v
Case team review -> still reviewing, taking the matter, or declining?
        |                              |                    |
        v                              v                    v
STEP 3 (ENGAGEMENT_CONFIRMED=no)  STEP 3 (=yes)        STEP 4: Non-
Client Intake Confirmation Email  same template        Engagement / Decline
step-3-client-intake-email.md     -----------          Letter
        |                              |                step-4-non-engagement-
        v                              v                letter.md
   Neutral receipt, request      Confirms firm is             |
   documents, review continues  handling the matter           v
                                                        Send to prospective
                                                        client (do not open
                                                        matter)
```

Each step is a standalone prompt template. Run Steps 1 and 2 in order,
feeding the prior step's full output into the next step's input variables.
After case team review, use Step 3 for both an ongoing screening-stage
intake (`ENGAGEMENT_CONFIRMED = no`, neutral receipt language) and a
confirmed engagement (`ENGAGEMENT_CONFIRMED = yes`) - it is the only
template with a documented path for "still reviewing." Use Step 4 only
once the firm has made an affirmative decision to decline the matter;
never run Step 3 and Step 4 for the same matter at the same time.
`workflow.json` is the machine-readable version of the same pipeline for
orchestration.

## Required inputs (collected once, at Step 1)

| Variable | Description |
|---|---|
| `{{JURISDICTION}}` | State/jurisdiction governing the matter (client-supplied) |
| `{{INTAKE_NOTES}}` | Raw intake call/interview notes |
| `{{POLICE_REPORT}}` | Police/incident report text or OCR output, if any |
| `{{MEDICAL_RECORDS}}` | Any medical records provided at intake |
| `{{CLIENT_NAME}}` | Client's full name, for the Step 3 email greeting |
| `{{ATTORNEY_NAME}}` | Handling attorney, for the Step 3 email signature |
| `{{FIRM_NAME}}` | Firm name, for the Step 3 email |
| `{{ENGAGEMENT_CONFIRMED}}` | Whether the firm has formally agreed to represent the client (yes/no) - controls the language Step 3 is allowed to use |
| `{{DECLINE_REASON}}` | Optional, Step 4 only. Leave blank unless the firm wants to state a neutral, non-merits reason for declining (e.g. "outside our current caseload") |

If a document type was not provided, say so explicitly in the workflow run
rather than omitting the section - Step 1 is required to flag it as a gap.

## Data handling

Step 1 submits raw intake notes, police report text, and medical records -
including protected health information - into a prompt sent to whatever
model/vendor is running this workflow. Before using this workflow on a real
matter, confirm with the firm's IT and general counsel that the vendor in
use has a signed business associate agreement covering this data, and that
the vendor does not retain or train on submitted data beyond what the BAA
permits. This workflow's prompt text cannot resolve that - it is a
prerequisite, not a step.

## Output handling

- Steps 1 and 2 are internal work product. Keep them in the case management
  file; do not send to the client.
- Steps 3 and 4 output is client-facing. A supervising attorney must review
  before either goes out - the workflow drafts it, it does not authorize
  sending it.
- Nothing in this workflow's output constitutes a final liability, damages,
  or statute-of-limitations determination. Every output must be verified by
  a licensed attorney against the actual jurisdiction's statutes and current
  case law before being relied on.
- Never docket a statute-of-limitations deadline from Step 2's output on
  the strength of an attorney's overall sign-off on the analysis alone.
  Verify the specific date independently against the actual statute before
  it goes on any calendar - a wrong docketed deadline is a missed filing,
  not just an inaccurate memo.
- Confirm with the firm whether the Step 3 email should reference fee or
  contingency arrangements. The current template does not - some firms
  want that in the first client letter, others hold it for the signed
  retainer. Adjust Step 3 to match the firm's practice before relying on it
  as-is.

## Files

- `step-1-fact-chronology.md` - fact chronology + missing-facts prompt
- `step-2-liability-analysis.md` - causes of action / defendants / SOL / comparative fault prompt
- `step-3-client-intake-email.md` - client confirmation email prompt, for a matter the firm is taking
- `step-4-non-engagement-letter.md` - decline letter prompt, for a matter the firm is not taking
- `workflow.json` - machine-readable step definitions for orchestration
