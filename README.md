# Provenance Transparency: crypto safety data without a paywall

Proposal, Oct 22, 2026. Built on `research_open_safety_landscape.md` and `research_open_safety_models.md` (read their [V]/[M]/[B] markers: several funding and legal claims there are from memory and need checking before anything is said publicly).

## 1. The problem, stated precisely

Crypto safety data is paywalled because the paid product and the public good are the same thing: **labels**. Vendors sell "this address is bad" to exchanges at $26k–$295k a year, labels carry defamation liability, and so nobody publishes them. The free sources that exist are funnels (Chainabuse: 10 API calls a month, data owned by TRM), throttled (Etherscan labels are an enterprise product), or dead (CryptoScamDB, the Etherscan-scrape repos) because they had no revenue and no trust layer. The result is what this case showed: a ring with ~46 thefts and $16M of proceeds, and almost none of its wallets carried a public warning until a victim's team filed them by hand.

Every other industry that solved this did it by **splitting facts from judgments**: Certificate Transparency publishes certificates, not "this CA is bad"; CVE publishes vulnerability records, not "don't buy this software"; Spamhaus publishes evidence-backed listings with a dispute path. The verdict is made by the consumer (browser, scanner, mail server) under its own policy. That split is what moves the liability off the publisher and makes the data safe to give away.

## 2. The design in one paragraph

A **public, append-only transparency log of evidenced provenance claims** ("funds from tx X at address Y are proceeds of incident Z; evidence hashes; issuer; confidence; time"), run by several independent operators, **free to read forever**, written to by **accredited issuers** with scoped authority, with CVE-style DISPUTED/WITHDRAWN states and a fixed-window dispute right. Wallets and individuals query it free through a privacy-preserving hash-prefix API. What stays commercial is everything *downstream* of the facts: risk scores, clustering, SLAs, bulk redistribution and legal-grade evidence packs. The log is the commons; the judgment is the market.

## 3. What is new here (the five mechanisms that don't exist today)

1. **Claims, not verdicts, on an append-only log.** Nothing in the log says "bad wallet". Every entry is a dated, signed, evidence-hashed *claim* that a specific transaction's outputs are proceeds of a specific incident, with a confidence. Corrections are new entries (DISPUTED, WITHDRAWN, SUPERSEDED), never deletions, so the record of what was claimed and when is itself public. This is the CT/CVE posture and it is the legal shield: the operator publishes what an accredited issuer attested, with the evidence attached, and the consumer decides what to do with it.
2. **Proof-of-notice receipts.** Today's on-chain "dye packs" become first-class log entries: the notice text hash, the tx that delivered it, and the time. Any later holder of the same funds can be shown to have had notice *available* — the "knowing receipt" element victims' lawyers need. This gives the log a direct legal use for victims, which is a reason their counsel will pay **filing fees** to issue entries (court-filing economics), while reading stays free. In this case the broker's Oct 20 purchase, made after labels and notices were on the chain, is exactly the fact pattern the receipts would prove.
3. **Reciprocity for institutions.** Exchanges and custodians get free bulk access *only if* they contribute their own confirmed-scam deposit addresses and sweep mappings (the VirusTotal model). The biggest data holders become contributors instead of customers, and the log fills in the one place current lists are blind: which exchange account received the money.
4. **Recovery-funded endowment.** Issuers may attach an opt-in, counsel-administered pledge: a small percentage of any funds recovered on the back of a logged claim goes to the operator foundation. Funding then scales with the log's usefulness rather than with a sponsor's mood (the CVE funding scare of 2025 is the cautionary tale). Precedents to model: cy-près awards and whistleblower-award structures; this needs a lawyer's design.
5. **A consumer bill of rights baked into the schema.** Free lookup of any address; a free dispute path with a fixed investigation window and an evidence standard for listing (the FCRA/CIFAS trade); addresses treated as pseudonymous identifiers with an erasure process for persons who prove innocence (the EDPB 2025 posture). The rights are what make the shield defensible.

## 4. Who pays, who reads free

| Layer | Free to | Paid by |
|---|---|---|
| The log itself (claims + evidence hashes + receipts), read access, monitors | Everyone: wallets, individuals, researchers, journalists, small exchanges | Operator foundation: issuer filing fees, institutional reciprocity dues, recovery pledges, public-goods grants |
| Hash-prefix client API (Safe Browsing / HIBP style) | Wallets and apps at consumer volume | Volume tier for commercial heavy use (Spamhaus DQS model) |
| Enrichment: clustering, risk scores, multi-hop exposure, case packs, SLAs | — | Commercial vendors (Infinihash KYT among them) built *on top of* the log |
| Legal-grade evidence bundles for freezing orders | Victims at cost | Counsel; recoverable as costs |

Rule of thumb from Spamhaus and HIBP: free for the people being protected, paid for the people making money from the data.

## 5. Governance (borrowed, not invented)

- **Operators:** at least three independent log operators (a university host like abuse.ch at BFH; a security collective such as SEAL; one exchange or custodian). Each signs receipts; monitors check they agree.
- **Issuers (CNA model):** exchanges, forensics firms, law-enforcement units and accredited victim-side investigators, each with scoped authority (an exchange may attest only its own deposit addresses; a forensics firm may attest traced flows with evidence). A root body sets the evidence standard and can suspend an issuer.
- **Policy stays with consumers:** a wallet may warn at confidence ≥6; an exchange may hold at ≥8 from two issuers. The log never blocks anything.
- **Disputes:** fixed window (say 10 business days), evidence-based, resolved by a panel not including the issuer; outcomes are log entries.
- **Legal posture:** evidenced reports of facts about transactions, never statements about named persons; Section 230(c)(2)-style good-faith filtering where it applies; GDPR process for identifiers.

## 6. Why it survives where CryptoScamDB didn't

- It has **revenue that doesn't depend on selling labels**: filing fees, reciprocity dues, pledges, enrichment vendors paying for feed SLAs.
- It has a **trust layer** (accredited issuers, evidence standard, disputes), so it isn't poisoned by the address-poisoning bots and recovery scammers that drown open report sites.
- It has **users with a legal reason to write to it** (victims' counsel) and institutions with a **business reason to read it** (exchanges want the deposit-address map).
- It **cannot be quietly censored**: append-only, multi-operator, monitored.

## 7. What Infinihash's role would be

Reference implementation and first issuer (the EAS schema and propagation engine in `provenance_attestations.md` are 80% of it), first commercial enrichment vendor on top, and the convener of the first two outside operators. Not the sole operator and not the owner: the moment one company owns the log, it's a paywall waiting to happen.

## 8. Bootstrap (90 days)

1. Publish the schema and the consumer rights document; recruit two outside operators (a university, SEAL or a comparable body).
2. Seed the log: this case's 102 tier-A wallets and 64 exchange accounts, ScamSniffer's open blocklist (licence permitting), the OFAC SDN crypto addresses.
3. Ship the hash-prefix lookup API and a MetaMask/Rabby-style warning integration.
4. Sign the first reciprocity agreement with one exchange (the deposit-address map is the carrot).
5. Run the first dispute end-to-end on a deliberately weak entry, publicly.

## 9. Open questions (check before any public claim)

- Verify the funding figures and licence terms marked [M]/[B] in the two research files.
- Whether the US CISA 2015 sharing safe harbour was reauthorised after its Sept 2025 lapse, and the CVE contract status after March 2026.
- The exact EDPB wording on wallet addresses as personal data, and what an erasure process must look like.
- Whether a recovery pledge can be structured without becoming a "recovery service" in the regulatory sense; counsel to design it.
- Whether exchanges will accept reciprocity; no precedent for exchanges jointly funding an open fraud feed was found.
