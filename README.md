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
| `01-legal-regulatory.md` | **Costa Rica first**: Ley N.º 10113, SENASA veterinary product registration, CPMVCR — plus US federal status (Farm Bill, FDA-CVM) as background context only |
| `02-canine.md` | Dogs — osteoarthritis, epilepsy, anxiety, atopic dermatitis, pharmacokinetics |
| `03-feline.md` | Cats — safety/tolerance data, dosing caveats, hepatic metabolism differences |
| `04-equine.md` | Horses — OA/lameness, pharmacokinetics, competition/FEI drug-testing rules |
| `05-livestock-food-animals.md` | Cattle, poultry, swine — feed legality, residue/withdrawal concerns |
| `06-toxicity-emergency.md` | THC toxicosis recognition & supportive treatment (dogs/cats) |
| `08-oncology.md` | Cancer/oncology — the one real animal safety trial + preclinical (cell-line) findings by tumor type, clearly separated |
| `07-sources.md` | Full bibliography with direct links |
| `data/app-data.json` | Machine-readable dataset the app actually reads: species + oncology topic + reference pages, with per-entry source links and calculator fields |
| `data/conditions.json` | Earlier flat data export, kept for reference; not read by the app |

## Suggested agent behavior

1. User asks about a species + condition (e.g., "dog, osteoarthritis").
2. Agent queries `data/app-data.json`, returns the studied dose range(s), the evidence tier, key cautions, and a direct source link.
3. Agent always appends: *"This is published-literature information, not a prescription. Confirm with the treating veterinarian, verify the product (THC content, third-party testing), and check current Costa Rican regulatory status (SENASA, CPMVCR) before recommending."*
4. Agent refuses to advise on food-animal use beyond "not currently legal/approved — flag to a vet/regulatory contact."
5. **Cancer questions get extra care.** Almost all oncology entries are preclinical (cell-culture) findings, not evidence a product treats cancer in a live patient. The agent should never phrase a preclinical finding as if it supports a treatment recommendation — see `08-oncology.md` and the tier-`P` entries in the data.
6. The live app includes a **dose calculator** (species + condition + patient weight → total dose) built directly from each entry's `calc` field. It refuses to calculate for preclinical/regulatory/no-fixed-dose entries by design — that refusal is intentional, not a bug to fix.

## Gaps / what's still missing (good next steps)

- Swine- and poultry-specific pharmacokinetic data (essentially none published)
- Long-term (>6 month) safety data in any species
- Standardized product potency/purity data (most commercial pet CBD products are not third-party verified against label claims)
- State-by-state legal matrix (only a handful of states have explicit statutes; most are silent — see `01-legal-regulatory.md`)
