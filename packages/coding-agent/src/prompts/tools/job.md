Inspects, waits, or cancels async jobs.

Background job results are delivered automatically when complete. Reach for this tool only when you need to intervene.

# Operations

## `list: true`
Use to inspect what's running.

## `poll: [id, …]`
Block until the specified jobs finish or the wait window elapses.
- Use when you are genuinely blocked on a result and have no other work to do.
- Returns the current snapshot when the timer elapses; running jobs remain running.
- Completed jobs include their final output in the returned snapshot.

You **MUST NOT** poll the same job repeatedly without evidence of progress. Between calls, inspect `read jobs://<id>` to confirm new output or activity.
{{#if allowCancel}}

## `cancel: [id, …]`
Stop running jobs.
- Use when a job is stalled, hung, or no longer needed.
- Returns immediately after cancelling.

`poll` and `cancel` may be combined in a single call: cancellations apply first, then polling waits on the remaining ids.
{{/if}}
