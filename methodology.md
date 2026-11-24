# Methodology

## Question and unit of analysis

The field notes ask: when an AI agent's payment is refused by an owner-set limit, or changed after buyer approval, what record can the owner see afterward?

The unit of analysis is a dated scenario in a named product environment. Findings apply to that scenario, environment and test date—not automatically to other plans, features or later product versions.

## Version 0.1 environments

| Product | Test date | Environment | Money movement |
|---|---|---|---|
| Sapiom | 2026-11-10 | Sandbox | None; the test stopped before money movement. |
| Locus Pro | 2026-11-11 | Free workspace | Small paid control calls at 3.6 credits. |
| Catena | 2026-11-17 | Sandbox with test USDC on Base Sepolia | A $1 test control completed. |
| Crossmint Agent Checkouts | 2026-11-17 | Production keys against real merchants | None; tests stopped before payment and bought nothing. |

## Common questions

Each scenario considers, where applicable:

1. Did the control stop the attempted action?
2. Did the refusal or changed state leave a record?
3. Could the owner find that record through the tested API or console?
4. Did the record preserve the reason and the limit or approval state that applied, rather than only current settings?
5. Could the owner enumerate relevant events without already knowing every internal user or agent identifier?

The tests use positive controls alongside refusals. A completed or recorded control helps distinguish an evidence gap from a failure of the whole recording path. Exact amounts, status codes and relevant endpoints are retained in the public note where they help identify the scenario.

## Evidence categories

The writing distinguishes four kinds of statement:

- **Observed behavior:** an external API, CLI or console result seen in the dated test.
- **Documentation:** a statement about documented behavior, identified as such.
- **Vendor response:** a dated, attributed summary of a company's reply. A response is context, not independent proof of a fix.
- **Interpretation:** a conclusion or design suggestion, kept separate from the observation.

A missing record means it was absent from the tested owner-facing views. It does not establish that no internal log exists. Likewise, an externally observed block does not identify the internal mechanism that produced it.

## Reproduction and exclusions

Public reproduction materials are linked where available:

- [Locus limit-record note and reproduction script](https://github.com/Ectsang/locus-limit-record)
- [Sapiom purchase-receipt format and verifier](https://github.com/Ectsang/purchase-receipts)

The Sapiom receipts were replayed from saved API reads. Their capture timestamps were replay times, not original event timestamps. The receipts establish the integrity of the captured buyer-side records, not the truth of provider statements. The sandbox platform key also received `403 Missing required permissions: org.read` when reading spending-limit versions; whether that reflected permissions or setup remains unresolved, and it is not treated as an enforcement failure.

Confounded checks are excluded as findings. In v0.1, a later Locus concurrency round mostly hit the Free plan's rate limit and is not used as budget-enforcement evidence. An earlier Crossmint run instructed the agent "Do not buy," never evaluated the cap and is excluded.

## Known scope limits

Version 0.1 covers four products and a small scenario set. It does not exhaustively test retention, exports, enterprise features, validation failures or every owner-facing view. In particular:

- Locus was tested only on the Free plan; Enterprise webhooks, ledger features and policy-event endpoints may differ.
- Sapiom provider-side revision records were not available to the external test.
- Catena's November 19 improvement statement remains pending verification; the original scenarios must be rerun before claiming a fix.
- Crossmint's November 20 confirmation describes the API and console as of that date. The feature request had no ship date and requires a retest if shipped.

Future results should be published as dated corrections or updates rather than silently rewriting the original observations.
