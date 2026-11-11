# Lending

The common lending vocabulary -- loan applications, the offers made against them, the loans and credit lines that result, the borrowers who hold them and the repayments that settle them -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Lending, Mortgage, Credit, Buy Now Pay Later, BNPL, Consumer Lending, Loan Origination, Loans, Embedded Lending in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| loan | 14 | 12 | id 67%, amount 50% | loans 12, loan 3, credit_lines 1 |
| borrower | 4 | 3 |  | borrowers 3, borrower 2 |

Cohort: 134 providers with harvested OpenAPI, 14 crosswalks. Of the providers exposing a loan: 57% create, 57% list, 64% fetch, 50% update, 36% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Lending publishes less than any context so far: 134 lending, mortgage, credit and BNPL providers in the cohort, 14 exposing loans. Origination, decisioning and servicing APIs are overwhelmingly private or partner-gated.
- What is public agrees only on a loan's id and amount. Balance, rate, term and maturity are each modelled by too few providers to call shared.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Applications, offers and repayments are not published as concepts: measured, 3, 1 and 1 providers expose them with a readable schema. They are recorded here so the next re-measure can add them when the market publishes.
- A borrower is `borrowers` or `applicants` only. `customers` and `members` brought in payment customers and workspace members from the wider fintech cohort.
- Credit lines, BNPL installment plans and mortgages are loans: each is a principal lent against a schedule.
- Duplicates merged: Figure, Oper, Orbii.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
