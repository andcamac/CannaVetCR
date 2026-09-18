# Cannabis & Veterinary Medicine — Knowledge Base

A structured, sourced repository of **publicly available information** on cannabinoids (CBD, CBDA, THC, hemp) in veterinary practice. Built as a prototype knowledge base for an AI agent that clinic staff could consult for species-specific dosing ranges, evidence quality, and safety information by condition.

## ⚠️ Read before using or building on this

- **This is a literature/regulatory summary, not a formulary.** Nothing here is an approved label dose — there is currently **no FDA-approved cannabinoid drug for veterinary use** in the US (aside from human epilepsy drug Epidiolex, which is occasionally used off-label). Every dose cited below comes from a specific published study, and studies vary in size, product (isolate vs. full/broad-spectrum vs. THC-containing), and formulation.
- **An agent built on this should present ranges + evidence strength + sourcing, and route anything client-facing back to a licensed veterinarian** — not output a single number as if it were a prescription. Many state veterinary boards still restrict what a vet can recommend vs. discuss (see `01-legal-regulatory.md`).
- Food-producing animals (cattle, swine, poultry, etc.) are a **legal red line**: no hemp/cannabis ingredient is currently FDA/AAFCO-approved for use in animals whose products enter the human food supply. See `05-livestock-food-animals.md`.
- This repo does not cover recreational/illicit-drug dosing for humans. All content concerns non-human animal patients.

## Contents

| File | Covers |
|---|---|
| `01-legal-regulatory.md` | Federal (Farm Bill, FDA-CVM, DEA) + state-level status, AVMA/AAVSB positions, board discipline risk |
| `02-canine.md` | Dogs — osteoarthritis, epilepsy, anxiety, atopic dermatitis, pharmacokinetics |
| `03-feline.md` | Cats — safety/tolerance data, dosing caveats, hepatic metabolism differences |
| `04-equine.md` | Horses — OA/lameness, pharmacokinetics, competition/FEI drug-testing rules |
| `05-livestock-food-animals.md` | Cattle, poultry, swine — feed legality, residue/withdrawal concerns |
| `06-toxicity-emergency.md` | THC toxicosis recognition & supportive treatment (dogs/cats) |
| `07-sources.md` | Full bibliography with links |
| `data/conditions.json` | Machine-readable condition → species → dose-range → evidence-level → source map, for the agent to query |

## Suggested agent behavior

1. User asks about a species + condition (e.g., "dog, osteoarthritis").
2. Agent queries `data/conditions.json`, returns the studied dose range(s), the evidence tier, key cautions, and citations.
3. Agent always appends: *"This is published-literature information, not a prescription. Confirm with the treating veterinarian, verify product (THC content, third-party testing), and check state-specific rules before recommending."*
4. Agent refuses to advise on food-animal use beyond "not currently legal/approved — flag to a vet/regulatory contact."

## Gaps / what's still missing (good next steps)

- Swine- and poultry-specific pharmacokinetic data (essentially none published)
- Long-term (>6 month) safety data in any species
- Standardized product potency/purity data (most commercial pet CBD products are not third-party verified against label claims)
- State-by-state legal matrix (only a handful of states have explicit statutes; most are silent — see `01-legal-regulatory.md`)
