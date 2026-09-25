# Opportunities Store

This directory stores Opportunity Cards produced by [`skills/opportunity-scorer`](../skills/opportunity-scorer/SKILL.md) and tracked by [`skills/opportunity-ledger`](../skills/opportunity-ledger/SKILL.md).

## Naming Convention

Each Opportunity Card is stored as a Markdown file:
```text
OPP-[YYYYMMDD]-[NN].md
```
- `YYYYMMDD`: Date the card was scored (e.g., `20260925`)
- `NN`: Zero-padded sequence number for that date (e.g., `01`, `02`)

Example: `OPP-20260925-01.md`

## Card Lifecycle & States

1. **Scored (Pending Founder Decision)**: Produced by `opportunity-scorer`. Contains advisory recommendation (`Proceed`, `Shrink further`, or `Kill`).
2. **Pursued / Declined**: Marked once the founder makes an explicit commercial decision.
3. **Delivery & Execution**: If pursued, delivery must aim for initial completion within ~72 hours for the Minimal Monetizable Unit (MMU).
4. **Logged**: When the outcome is determined (converted, declined, failed, or learned), the transaction is recorded in the ledger via `opportunity-ledger` (Mode A).
5. **Re-scored (Update Mode)**: If an opportunity becomes stale or market conditions change, `opportunity-scorer` appends a re-score row in the card's history table.

Template reference: [`templates/opportunity_card.md`](../templates/opportunity_card.md)
