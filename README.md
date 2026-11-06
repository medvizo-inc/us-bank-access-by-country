# US bank access by country

Which US business accounts name a founder's country, and what each
provider's rule turns on: where the owner lives, their citizenship, where the
company is registered, or US status. 17 providers, 100 countries,
1,700 cells. Every cell is worked out from the provider's own published
list and carries the page, the words and the day it was read.

Published by [BaseAcross](https://baseacross.com). The same data is on
[US bank access by country](https://baseacross.com/tools/us-bank-access-by-country). Its sister dataset is
[US LLC state fees](https://github.com/medvizo-inc/us-llc-state-fees).

Checked up to 2026-11-06.

## Files

| File | What it holds |
|---|---|
| `data/us-bank-access-by-country.csv` | One row per provider and country (1,700 rows). |
| `data/us-bank-access-matrix.csv` | One row per country, one status column per provider. |
| `data/rule-basis.csv` | One row per provider: what its rule turns on, in its own words. |
| `data/us-bank-access-by-country.json` | All of it, as one object. |

## How to read it

- **Not on a refusal list is not a yes.** Some providers publish only the
  countries they refuse. A country absent from that list can apply, and the
  provider still decides each application.
- **A row is for an owner who lives in that country**, except where the
  provider's rule turns on citizenship (`rule_basis` = `citizenship`), where
  it is for a citizen of that country. Mixed cases (a citizen of one country
  living in another) are not worked out: that would be our inference, not the
  provider's rule.
- **Grouped by kind of account.** The order is not a recommendation.

## Statuses

| Status | Meaning |
|---|---|
| `named_open` | The provider names this country on its list of where it serves. |
| `not_named` | The provider lists the countries it refuses, and this one isn't on it. That isn't a yes: the provider still decides each application. |
| `named_closed` | The provider names this country on its list of where it won't open. |
| `absent_from_allowlist` | The provider lists where it serves, and this country isn't on it. |
| `lists_conflict` | The provider's own pages put this country on its refusal list and on its supported list. |
| `needs_us_presence` | Open only with a US address or an owner based in the US, wherever you live. |
| `us_persons_only` | Open only to owners with US status. The note says what the provider asks for. |
| `ofac_only` | The provider names no countries. Its terms bar places under US sanctions (OFAC), and let it stop serving other countries at any time without notice. |
| `unpublished` | The provider publishes no rule about where owners live. |
| `unverified` | We couldn't re-read the provider's page, so we don't say. |

## Rule bases

| Rule basis | Meaning |
|---|---|
| `residence` | Where you live |
| `residence_sometimes_citizenship` | Where you live, and sometimes your citizenship |
| `citizenship` | Your citizenship |
| `citizenship_or_residence` | Your citizenship or where you live |
| `company_registration` | Where the company is registered |
| `residence_and_company` | Where you live, and the company |
| `us_status` | US residence, address or SSN |
| `ofac_only` | Names no countries |
| `unpublished` | No rule published |

## Providers

| Provider | Rule basis | Bank named on its page | Read | Verification |
|---|---|---|---|---|
| Mercury | `residence` | Choice Financial Group and Column N.A. | 2026-11-06 | verified |
| Relay | `citizenship_or_residence` | Thread Bank | 2026-11-06 | verified |
| Bluevine | `residence_and_company` | Coastal Community Bank | 2026-11-06 | verified |
| Meow | `residence_sometimes_citizenship` | Grasshopper Bank, N.A. | 2026-11-06 | verified |
| Lili | `citizenship` | Sunrise Banks, N.A. | 2026-11-06 | verified |
| Rho | `us_status` | Webster Bank, a division of Santander Bank, N.A., and Lead Bank | 2026-11-06 | verified |
| Novo | `us_status` | Middlesex Federal Savings, F.A. | 2026-11-06 | verified |
| Found | `us_status` | Lead Bank | 2026-11-06 | verified |
| Brex | `us_status` | not named | 2026-11-06 | verified |
| Wise Business (USD details) | `residence_and_company` | not named | 2026-11-06 | verified |
| Airwallex | `company_registration` | not named | 2026-11-06 | verified |
| Revolut Business (US) | `residence` | not named | 2026-11-01 | unverified |
| Payoneer | `ofac_only` | not named | 2026-11-06 | verified |
| Grasshopper Bank | `us_status` | is the bank | 2026-11-06 | verified |
| Chase | `unpublished` | is the bank | 2026-11-06 | verified |
| Bank of America | `us_status` | is the bank | 2026-11-06 | verified |
| Wells Fargo | `unpublished` | is the bank | 2026-11-06 | verified |

### Not re-read for this release

- **Revolut Business (US)**: its page refused every read for this release, so every cell is `unverified` and no list is given.

## Columns (long file)

- `country_code`: ISO 3166-1 alpha-2 code of the country.
- `country`: The country's name.
- `region`: The region BaseAcross files the country under.
- `provider`: The account provider.
- `provider_kind`: `bank`, `fintech_with_partner_bank` (the provider's page names the bank that holds the money), or `not_stated`.
- `partner_bank`: The bank the provider's own page names. Empty where no page read names one.
- `product`: `checking`, `business_account`, `multi_currency` or `receiving_account`.
- `rule_basis`: What the provider's rule turns on. See the rule bases below.
- `list_type`: `denylist`, `allowlist`, `both` or `none`: the kind of country list the provider publishes.
- `status`: This cell's answer. See the statuses below.
- `note`: Why, in a sentence.
- `conditions`: What applies to every owner abroad, in a few words.
- `ssn_required`: `yes`, `no` or `not_stated`, from the provider's own words.
- `itin_accepted`: `yes`, `no` or `not_stated`.
- `owner_us_address_required`: Whether each owner needs a physical US address: `yes`, `no` or `not_stated`.
- `source_ids`: The ids of the sources the rule rests on, in BaseAcross's source register.
- `source_urls`: Those sources' pages.
- `source_quote`: Words from those pages, as the provider wrote them.
- `checked_on`: The oldest day any of those sources was read. Every cell is at least this fresh.
- `verification`: `verified` (read for this release), `last_read` (an older read) or `unverified` (no cell is stated).

## Earlier work

Global Solo's [US Banking Access Index](https://www.globalsolo.global/data/banking-access-index)
(CC BY) covers 8 countries, by where the founder lives.

## Licence and credit

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Use it anywhere, including commercially, with the
credit "Source: BaseAcross, US bank access by country" and a link to
https://baseacross.com/tools/us-bank-access-by-country.

Corrections are welcome as an issue, with the provider's own page.

Not legal, tax or banking advice. Check with the provider before you apply.
