# Personal Injury New Matter Intake & Case Screening Workflow

Three-step AI workflow for processing a new personal injury matter from raw
intake materials to a client-ready confirmation email. Built for internal
case team use during the initial screening window (first 48-72 hours).

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
STEP 3: Client Intake Confirmation Email  ------> step-3-client-intake-email.md
        | (client-ready email)
        v
Case team review -> send to client / open matter
```

Each step is a standalone prompt template. Run them in order, feeding the
prior step's full output into the next step's input variables. `workflow.json`
is the machine-readable version of the same pipeline for orchestration.

## Required inputs (collected once, at Step 1)

| Variable | Description |
|---|---|
| `{{JURISDICTION}}` | State/jurisdiction governing the matter (client-supplied) |
| `{{INTAKE_NOTES}}` | Raw intake call/interview notes |
| `{{POLICE_REPORT}}` | Police/incident report text or OCR output, if any |
| `{{MEDICAL_RECORDS}}` | Any medical records provided at intake |
| `{{ATTORNEY_NAME}}` | Handling attorney, for the Step 3 email signature |
| `{{FIRM_NAME}}` | Firm name, for the Step 3 email |

If a document type was not provided, say so explicitly in the workflow run
rather than omitting the section - Step 1 is required to flag it as a gap.

## Output handling

- Steps 1 and 2 are internal work product. Keep them in the case management
  file; do not send to the client.
- Step 3 output is client-facing. A supervising attorney must review before
  it goes out - the workflow drafts it, it does not authorize sending it.
- Nothing in this workflow's output constitutes a final liability, damages,
  or statute-of-limitations determination. Every output must be verified by
  a licensed attorney against the actual jurisdiction's statutes and current
  case law before being relied on.

## Files

- `step-1-fact-chronology.md` - fact chronology + missing-facts prompt
- `step-2-liability-analysis.md` - causes of action / defendants / SOL / comparative fault prompt
- `step-3-client-intake-email.md` - client confirmation email prompt
- `workflow.json` - machine-readable step definitions for orchestration
