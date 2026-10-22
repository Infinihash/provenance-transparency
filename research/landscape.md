# Open vs paywalled crypto wallet-safety data: landscape (2026-10-22)

Method note: web-search budget ran out after ~9 queries. Items tagged [V] were confirmed by a search/fetch this session
(source URL given). Items tagged [M] are from model memory (cutoff Jun 2026), NOT re-verified; check before relying on them.
Pricing and license items are the most likely to have drifted.

## 0. Why the data is paywalled (synthesis)
1. Labels are the product. Attribution (cluster -> entity) is expensive human + heuristic work (subpoena-adjacent, law-enforcement
   cooperation, exchange KYC tips). Vendors sell it per seat/per API call; publishing it destroys the moat. [M]
2. Liability asymmetry. A false "scam/sanctioned" label can freeze a user's funds at an exchange. A vendor selling to regulated
   customers can disclaim via contract ("risk indicator, not a determination"); a free public list has no such contract. [M]
3. Buyer is compliance, not the end user. Exchanges/banks pay for a defensible audit trail (AML/Travel Rule/OFAC), not for
   "is this wallet a scammer". Consumer safety has no budget line. Pricing evidence below. [V]
4. Free data is thin because it is user-reported, unverified, and Sybil-able. Verified data costs analysts; those are the paid vendors.
5. Law-enforcement/gov data (OFAC SDN) is public domain but tiny (hundreds of addresses), so it is not a scam-coverage solution.

## 1. Free / public sources (one verdict each)
Format: funder | publishes | coverage/latency | machine-readable | reuse/license

**Chainabuse (TRM Labs)** [V partly]. Funder: TRM Labs (paid vendor; acquired/ran it as a funnel for its own intel). Publishes
community scam reports (addresses, domains, tokens, txs). Public API exists but a standard free key is capped at 10 calls/month
(1 call = max 50 reports) per TRM docs. Machine-readable yes but throttled; bulk reuse requires TRM agreement. Verdict: the largest
public report corpus, but unverified, noisy (reports are claims), and rate-limited so it cannot be mirrored. Reuse beyond
personal lookup is not clearly licensed. Also a TRM dependency risk: if TRM changes terms, the data goes with it.
https://docs.trmlabs.com/guides/chainabuse/verifying-the-accuracy-of-reported-information
https://docs.trmlabs.com/guides/chainabuse/informing-product
https://apis.apievangelist.com/store/trm-labs-reports-api/

**CryptoScamDB** [M]. Community/volunteer; JSON/YAML lists of scam domains+addresses, MIT-style repo and API. Largely dormant since
~2020-21 (maintainers moved on, MetaMask phishing list absorbed its role). Verdict: best example of a permissive open dataset that
died from lack of funding and no revenue path. Treat as stale; check last commit.

**ScamSniffer** [V partly]. Funder: VC-backed company (free extension, paid API/enterprise). Open-source "scam-database" repo on GitHub
with a blocklist of 258K+ domains and malicious addresses, updated continuously. Machine-readable (JSON/GitHub). License: check repo
LICENSE (I did not confirm; verify before bundling). Verdict: the most reusable current free feed; the open repo is a deliberate
top-of-funnel, so the freshest/richest data stays in the paid API. Latency good for drainer domains, weaker for address-only.
https://scamsniffer.io/   (GitHub org: scamsniffer/scam-database)

**Etherscan / Tronscan labels, "Fake_Phishing" tags** [V partly]. Funder: Etherscan (private, profitable). Labels visible per page;
the machine-readable "Label Cloud"/Metadata CSV is an Enterprise paid product (contact sales) per Etherscan docs. Scraping is
against ToS. Verdict: widest human-curated coverage on EVM, but lookup-only for free; reuse needs a license. Fake_Phishing tags are
added by Etherscan staff from reports, so latency is hours-days.
https://docs.etherscan.io/metadata-api/api-endpoint/metadata-csv

**Blockaid (MetaMask)** [M]. Funder: Blockaid (VC-backed); MetaMask/Wallets integrate it for tx simulation and malicious-dapp warnings.
Free to end users inside wallets; API is commercial. Not a downloadable dataset. Verdict: best real-time consumer protection but
closed; not reusable by third parties without paying.

**GoPlus** [M; free-tier details not confirmed]. Funder: GoPlus (token/VC-funded). Free API tier with rate limits for token/address/
approval/dapp risk checks across many chains; paid tiers above. Machine-readable yes. Reuse: ToS allows API use, not bulk
redistribution. Verdict: the most generous free *API* for developers; confidence of its flags is unaudited.

**Revoke.cash** [M]. Funder: self-funded/small team (Rosco Kalis), some grants; open-source (GitHub), free. Publishes no scam list;
it is a tool to see/revoke approvals (consumes others' lists, e.g., Blockaid-style warnings). Verdict: good UX for hygiene,
irrelevant as a data source.

**Harpie** [M]. Funder: VC-backed. Mempool-level front-running of drainer txs to rescue assets; free tier + paid. No public dataset.
Verdict: active defense service, closed data.

**Forta** [M]. Funder: Forta Foundation, FORT token; decentralized detection bots; alerts via free-ish API/Firewall. No shutdown found in
my search (nothing confirmed either way). Verdict: open detection framework, but alerts are bot-quality and the economics are token-
dependent; low reuse as a "wallet reputation" dataset.

**OpenSanctions / OFAC SDN crypto addresses** [V partly]. OFAC SDN list is public domain (Treasury) and includes digital-currency
addresses; OpenSanctions normalizes OFAC, Israel NBCTF, Japan MoF, UK OFSI crypto wallets. OpenSanctions data is free for
non-commercial but requires a paid license for business use (internal-use and financial-services tiers). Chainalysis also runs a
free on-chain sanctions oracle and API (launched Mar 2022), sanctions-only. Verdict: highest-confidence, legally safest, but tiny and
sanctions-only. Use OFAC direct (public domain) rather than OpenSanctions to avoid license cost.
https://www.opensanctions.org/faq/25/crypto
https://cointelegraph.com/news/chainalysis-launches-free-sanctions-screening-tools/

**Arkham Intel Exchange** [M]. Funder: Arkham (VC + ARKM token). Free explorer with entity labels; bounty marketplace for intel. Terms
restrict scraping; API gated. Verdict: broad entity labels (exchanges, funds), weak on scam addresses; not reusable.

**SEAL 911 / Security Alliance** [V partly]. Funder: donations from Paradigm, a16z, Electric Capital, Framework, Dragonfly, EF,
Filecoin Foundation; Vitalik gave 250 ETH; operates as nonprofit (Open Security Alliance Inc). Provides incident-response help, Safe
Harbor agreement, a free SEAL-ISAC (Apr 2024) with ~2 dozen security teams incl. Chainalysis, MetaMask, Uniswap Labs. Verdict: the
only open, trusted human network, but it shares incident intel among members, not a public per-address feed. Closest vehicle for a
shared, vetted layer.
https://www.businesswire.com/news/home/20240417493276/en/Security-Alliance-SEAL-Launches-Free-Crypto-Native-ISAC
https://cointelegraph.com/magazine/seal-911-team-white-hat-forms-fight-crypto-hacks-real-time/
https://www.guidestar.org/Profile/92-3456081

**ZachXBT-style public investigations** [M]. Individual/community, funded by bounties and audience. Publishes narrative + address lists
on Telegram/X; extremely high signal, no schema, no license, non-systematic, per-person liability.

**Hypernative / Cyvers free tiers** [M]. VC-backed; free dashboards/alerts or limited address risk lookup to feed enterprise sales. No
bulk data. Verdict: marketing funnels.

## 2. Paywalled vendors
[V] Pricing (no public rate cards; third-party estimates, treat as ballparks):
- Chainalysis: Vendr data $26K-$295K/yr, median ~$69.5K (13 purchases); typical enterprise year-one ~$175K.
- Elliptic: ~EUR 80K-180K/yr (one source up to $500K).
- TRM Labs: ~EUR 60K-150K/yr (another source $50K-$700K).
- Crystal Intelligence: positioned lower; Merkle Science: lower/mid-tier, quote-based. [M]
https://www.vendr.com/marketplace/chainalysis
https://www.spark.money/tools/crypto-aml-tool-comparison
https://costbench.com/compare/chainalysis-vs-elliptic/

What is behind the wall [M]: (a) entity labels and cluster attribution (the core), (b) address/tx risk scores and exposure
(direct/indirect, by category), (c) real-time tx monitoring/alerts + case management, (d) investigation graph tooling (Reactor,
Elliptic Investigator, TRM Forensics), (e) API/bulk feeds, (f) law-enforcement-only attribution. Free tiers are limited to sanctions
screening (Chainalysis) or small lookups.
Stated reasons for not publishing [M, inferred from public statements/ToS, not a single quote]: competitive (labels are the
asset), data-quality/false positive claims need context, ongoing investigations/law-enforcement confidentiality, and contractual
disclaimers that scores are indicators not findings. Evidence of a quote was not found this session.

## 3. Past open/shared label attempts [mostly M]
- Etherscan label scrapes (brianleect/etherscan-labels, EasyChris/etherscan-labels, PyPI "etherscanlabel"): snapshot scrapes, go stale,
  ToS-risky; Etherscan later productized labels as paid Metadata CSV. [V that repos/packages exist]
- dawsbot/evm-labels: aggregated community label JSON; I could not confirm its status (repo may be unmaintained; check GitHub).
- CryptoScamDB: see above (dormant).
- MetaMask eth-phishing-detect: still the main open domain blocklist (MIT), maintained by MetaMask/Consensys; domains only, and
  governance of removals is a recurring complaint. [M]
- Ethereum Attestation Service scam-report schemas / OpenRank-type reputation: experiments; no sustained adoption, Sybil and
  spam problem, no one trusted to adjudicate. [M, low confidence]
- Chainabuse: not abandoned but became TRM's property; open reports, closed economics.
- Pattern: every open dataset dies of (1) no revenue, (2) no adjudication/trust layer, (3) a vendor absorbing or out-scraping it.

## 4. Legal and liability
- US: CDA 230 protects a host for third-party user reports (Chainabuse-style) but NOT content the publisher itself creates or
  materially develops. A curated "bad wallet" list is the publisher's own speech, so 230 is weak there; defense shifts to truth,
  opinion, First Amendment, and clear disclaimers. [M; confirm with counsel]
- Spamhaus precedent [V partly]: e360 Insight v. Spamhaus (N.D. Ill., 2006) produced a ~$11.7M default judgment against Spamhaus
  (a UK-based non-participant); on appeal (7th Cir., 2008) the damages were largely vacated and the case did not result in
  collection. Survival factors: operates from UK/Switzerland, publishes as opinion ("listing criteria"), no contractual
  privity with listed parties, transparent delisting process, and the judgment was unenforceable in practice. Wikipedia/ICANN
  notes: https://en.wikipedia.org/wiki/The_Spamhaus_Project ; https://www.icann.org/en/announcements/details/spamhaus-litigation-update-10-10-2006-en
  Lesson: transparent criteria + published appeal path + labeled as risk opinion + offshore entity.
- UK: Defamation Act 2013 (truth, honest opinion, public interest; s.5 website-operator defense for third-party posts if poster is
  identifiable/notice process followed). EU: e-Commerce Directive hosting safe harbor, now DSA (notice-and-action). [M]
- GDPR [V]: EDPB Guidelines 02/2025 on blockchain (final v2.0 adopted July 2026 per search) say wallet addresses/public keys can be
  personal data when identification is reasonably likely. A list of "scam wallets" tied to natural persons is personal data
  possibly relating to offences (Art. 10). Mitigations: legitimate interest (fraud prevention, Rec. 47), publish minimal data,
  correction/delisting process. Fraud-prevention data sharing has precedent (CIFAS in UK). 
  https://www.edpb.europa.eu/system/files/2026-07/edpbreport_publicconsultaton_guidelines_blockchain_202502_en.pdf
  https://ppc.land/edpb-forces-blockchain-firms-to-avoid-storing-personal-data-on-chain/
- Practical design to reduce risk: accept reports, publish only evidence-backed entries, tier confidence, show provenance, honor
  disputes, never claim "innocent"/"guilty", offer machine-readable delisting log.

## 5. Funding of a free safety layer [mostly M; searches for this section failed on budget]
- Ethereum Foundation: ESP grants and security-related donations (EF is a SEAL donor [V]); has funded security tooling.
- Optimism RetroPGF: retroactive rounds funded security/tooling projects; rounds shrank/restructured in 2024-25, so recurring
  funding is uncertain. Gitcoin: grants rounds continue in reduced form; quadratic-funding favors popular, not critical, infra.
  Protocol Guild: pays core Ethereum devs; shows a pooled-vesting model other public goods copy, not security-specific.
  All four: values need to be verified; I could not pull current numbers.
- SEAL funding [V]: donations from funds/foundations plus a Safe Harbor / legal defense fund (SRLDF) for whitehats.
- Exchange/industry consortia [V partly]: Crypto ISAC (SEAL-ISAC) founding members include Coinbase, Kraken, Circle, Consensys,
  Fireblocks, Solana Foundation, Hedera, Offchain Labs; Binance.US joined; Coinbase announced automated threat-intel sharing
  into it. Membership is free. https://www.nasdaq.com/press-release/coinbase-expands-automated-threat-intelligence-sharing-crypto-isac-strengthen
  https://blog.binance.us/crypto-isac/
- Precedents outside crypto: FS-ISAC, CIFAS (UK shared fraud database funded by member fees), Spamhaus (sponsor/data-license
  funded), Abuse.ch (university + sponsors), Google Safe Browsing (single-sponsor). The Spamhaus/CIFAS model (free to small users,
  paid license for commercial bulk users) is the most proven funding template.
- Crypto-specific precedent for exchanges jointly funding shared fraud intel as an *open* feed: none found; Crypto ISAC is the
  nearest, and it shares among members only.

## Gaps for a follow-up (needs more search)
Exact LICENSE of scamsniffer/scam-database; GoPlus free-tier limits and ToS on redistribution; status of dawsbot/evm-labels and
CryptoScamDB; Forta current status; current RetroPGF/Gitcoin/Protocol Guild numbers; vendor quotes on label non-publication;
Spamhaus appellate details.
