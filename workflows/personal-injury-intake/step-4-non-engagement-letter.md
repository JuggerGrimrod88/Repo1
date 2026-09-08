# Step 4: Non-Engagement / Decline Letter

**Client-facing draft. Requires supervising attorney review and approval
before sending. Use only when the firm has decided not to take the matter -
never alongside Step 3, and never for a matter the firm is still deciding
on.**

## Purpose

When the firm reviews a matter and decides not to represent the
prospective client, send clear, prompt, written notice of that decision -
including a warning about the applicable filing deadline, and any shorter
government notice-of-claim deadline that applies - so the prospective
client has time to find other counsel. This is a standard malpractice-
prevention practice: a prospective client who is left believing the firm
is "still reviewing" past a filing deadline has a real claim against the
firm even though no attorney-client relationship existed.

## Inputs

- `{{LIABILITY_ANALYSIS_OUTPUT}}` - full output from Step 2 (for the
  filing deadline only - the statute of limitations AND any shorter
  government notice-of-claim deadline Step 2 identified; nothing else from
  it belongs in this letter)
- `{{CLIENT_NAME}}`
- `{{ATTORNEY_NAME}}`
- `{{FIRM_NAME}}`
- `{{JURISDICTION}}`
- `{{DECLINE_REASON}}` - optional. Leave blank to give no reason. If set,
  it must already be neutral and non-merits-based (e.g. "this falls
  outside the type of case we currently handle") - never a reason that
  comments on the strength or weakness of the claim.

## Prompt

```
You are drafting a non-engagement (decline) letter for a personal injury
law firm to a prospective client the firm has decided not to represent.
The client is not a lawyer - write in plain language, no legal jargon. Do
not discuss causes of action, potential defendants, comparative fault
exposure, or any internal viability rating from the Step 2 analysis - none
of that belongs in this letter, whether or not it was favorable. Do not
state or imply that the firm has evaluated the merits of the claim, only
that the firm is not able to take it on. If {{DECLINE_REASON}} is set,
state it in one neutral sentence; if it reads as a comment on the strength
or weakness of the claim, rewrite it in neutral terms instead of using it
as given. If {{DECLINE_REASON}} is blank, give no reason at all.

This letter must make three things unambiguous: (1) the firm is not
representing the prospective client in this matter and no attorney-client
relationship has been formed, (2) there is a deadline for filing a claim
and time is limited, and (3) the prospective client needs to contact
another attorney promptly.

INTERNAL LIABILITY SCREENING (Step 2 - extract only the filing deadline(s);
ignore everything else in this section. If Step 2's STATUTE OF LIMITATIONS
section identifies a government defendant with a shorter notice-of-claim
deadline, that deadline is the one that matters most here - it typically
runs out long before the general statute of limitations does):
{{LIABILITY_ANALYSIS_OUTPUT}}

Client name: {{CLIENT_NAME}}
Attorney name: {{ATTORNEY_NAME}}
Firm name: {{FIRM_NAME}}
Jurisdiction: {{JURISDICTION}}
Decline reason (optional): {{DECLINE_REASON}}

Draft a letter with the following structure:

SUBJECT LINE: neutral and clear that this is a decision on representation,
e.g. "Regarding Your Potential Claim - {{FIRM_NAME}}."

GREETING: addressed to {{CLIENT_NAME}}.

1. DECISION
   State plainly that {{FIRM_NAME}} has decided not to represent
   {{CLIENT_NAME}} in this matter, and that no attorney-client relationship
   has been formed. If {{DECLINE_REASON}} is set, include the neutral
   sentence here. Do not apologize in a way that implies the claim lacks
   merit, and do not thank the client for "the opportunity to review a
   strong case" or similar language implying an opinion on the merits
   either way.

2. TIME IS LIMITED
   State that claims like this are subject to a legal deadline, and that
   missing it can permanently bar the claim. If Step 2 identified a
   government notice-of-claim deadline in addition to the statute of
   limitations, use that earlier deadline here - it is the one that
   actually controls, and state it clearly as a separate, shorter deadline
   rather than only mentioning the general statute of limitations. If a
   specific calculated deadline is available (notice-of-claim or statute of
   limitations, whichever is earlier), state that date, framed as the
   firm's understanding based on the information available and not a
   guarantee - e.g. "based on the information you provided, we understand
   the deadline to file a claim may be on or around [date], but you should
   confirm this with another attorney immediately, since deadlines can be
   affected by facts we may not be aware of, and some deadlines - such as
   claims against a government agency - can be much shorter and stricter
   than a typical filing deadline." If the Step 2 output could not
   calculate a deadline, or expressed uncertainty about the citation or
   calculation, do not state a date - instead say plainly that the firm is
   not able to confirm the deadline from the information available, and
   that this makes it more urgent, not less, to consult another attorney
   immediately. Urge the client to act quickly - do not soften this
   section.

3. NEXT STEPS
   Recommend the client contact another attorney promptly to evaluate the
   matter. Do not name or recommend a specific other firm or attorney.
   Offer to return any documents or records the client provided, and give
   a way to request that ({{ATTORNEY_NAME}} at {{FIRM_NAME}}).

CLOSING: professional sign-off from {{ATTORNEY_NAME}}, {{FIRM_NAME}}.

Output only the finished letter (subject line plus body), formatted for
direct copy into an email or physical letter. No internal notes, no
headers other than the three numbered sections above, no legal analysis
carried over from Step 2 beyond the single deadline statement described
above.
```

## Output

A client-ready draft decline letter. Route to the supervising attorney for
review and any required edits before sending - particularly the filing
deadline(s) stated (including any government notice-of-claim deadline),
which must be independently verified before this letter goes out, not
relied on solely from Step 2's output. Send promptly; do not let this
letter sit in review while the filing deadline runs.
