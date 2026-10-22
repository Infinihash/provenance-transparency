# Open abuse/safety data as a public good: transferable mechanisms (non-crypto)

Method note: three facts were web-verified (marked [V], URLs inline). The rest is from background knowledge as of mid-2026 and marked [B]. Check [B] items before citing them in anything external.

## 1. Spamhaus and DNS blocklists (DNSBL/RBL)
- Who pays: Spamhaus Technology sells commercial products. Free DNS-query use is cut off above a volume cap or for commercial use. Corporate sales subsidise the free public tier. [B]
- Free vs paid: free for low-volume non-commercial queries over public mirrors. Paid: Data Query Service (DQS) with a per-customer key, private mirrors, rsync feeds, higher volume, SLA, extra zones. [B]
- Quality: listings are staff-curated, built on spamtraps and sensor networks. Lists are tiered by confidence (SBL, XBL, PBL, DBL). Relying parties choose which zone to enforce, so a bad listing costs only the sites that chose to trust it. [B]
- Disputes: each listing has a public lookup page with evidence, and a delisting request process. Some zones (PBL) let the owner self-delist. [B]
- Legal shield: US Section 230(c)(2) protects good-faith filtering. Spamhaus is UK/Swiss-based and ignored the US court. In e360 Insight v. Spamhaus, an $11M default-type award was cut to $27k and then to $3 on appeal, and the Section 230 argument was never ruled on [V]: https://blog.ericgoldman.org/?p=9923 , https://blog.ericgoldman.org/?p=10307 . Practical shield: an "opinion" framing, evidence-backed listings, a foreign domicile, and no dependency on any one US forum.
- Why it survived: sells a premium tier of the same data. It is a filter, not a verdict, because each recipient decides. The reputation is built on low false positives.
- Transferable: listings are advisory and each consumer sets its own policy. Free tier is capped by volume. Commercial users pay for keyed, SLA-backed access.

## 2. abuse.ch (URLhaus, MalwareBazaar, ThreatFox, Feodo, SSLBL)
- Who pays: a research project at the Institute for Cybersecurity and Engineering, Bern University of Applied Sciences (BFH) since 2021. It is financed by private-sector donations [V]: https://www.bfh.ch/en/research/reference-projects/abuse-ch/ . Spamhaus Technology has been the primary commercial licensee of abuse.ch data since 1 Aug 2022 [V], per https://abuse.ch/blog/ and BFH.
- Free vs paid: all public feeds and APIs are free. Since 2025 an auth key is needed, which is free. Spamhaus resells it commercially. Licence is CC0 [B]. A university host holds the data, and the commercial licensee supplies money and distribution.
- Quality: community submissions plus staff review. Entries are classified (malware family, tags). URLs expire and are marked offline, so staleness is explicit. Reputation scoring of contributors exists on the platform. [B]
- Disputes: public contact form and per-entry reporting. Removal is on evidence. [B]
- Legal shield: Swiss non-profit and university host. Entries are technical indicators (URLs, hashes), not accusations about named people. [B]
- Why it survived: very cheap to run. An institutional anchor plus a commercial licensee and donors. Contributors get free data back, which is reciprocity.
- Transferable: park the registry in a university or non-profit. License one commercial redistributor, and let that revenue fund the free tier. Use a free API key to track abuse without charging.

## 3. Google Safe Browsing
- Who pays: Google, as a cost of making the web safe for its ads and Search businesses. Free for non-commercial use. Commercial use goes through the Web Risk API, which is paid and carries an SLA. [B]
- Free vs paid: Safe Browsing v4/v5 Lookup and Update APIs are free for non-commercial use. Web Risk is the paid commercial variant. [B]
- Distribution: the Update API sends clients hash prefixes (about 4 bytes of a SHA-256) of the lists. The client checks locally and fetches full hashes only on a prefix hit. This preserves privacy and keeps bandwidth tiny. v5 adds a global cache and privacy-preserving checks. The stated mechanism is hash-prefix lists, not a Bloom filter. Chrome historically used a Bloom filter and now uses prefix sets. [B]
- Quality: crawler/ML detection plus partner feeds. Warnings are interstitials, with classes (malware, social engineering, unwanted software). [B]
- Disputes: Search Console shows the site owner the flagged issue. The owner fixes it and requests a review, which is usually answered within about a day. There is also a public report-incorrect-warning form. [B]
- Legal shield: Section 230(c)(2), warning-not-block UX, ToS disclaimers, and disclosure that it is "provided as is". [B]
- Why it survived: it is a corporate cost centre with a strategic payoff. All major browsers consume it, so Google gets scale and everyone else gets protection.
- Transferable: ship a free client-side API with local hash-prefix lookup so lookups don't leak what the user is checking. Charge for commercial volume or SLA. Warn instead of block. Give owners a console to see and contest the flag.

## 4. VirusTotal
- Who pays: owned by Google since 2012 (Chronicle/Google Cloud now). Enterprise API, Intelligence, Hunting and Livehunt are paid. [B]
- Free vs paid: free file/URL uploads and lookups, with a low-rate public API for non-commercial use. [B]
- Reciprocity: AV vendors must join the contributor programme. They share detection engines and receive samples and verdicts back from VT in exchange. Public use is the carrot. Vendors get free access to the sample stream. [B]
- Quality: multi-engine consensus. VT shows each engine's verdict and does not issue a single opinion. A disagreeing engine is visible, which is itself a false-positive check. [B]
- Disputes: each vendor owns its own verdict, so disputes go to that vendor. VT itself does not edit them. [B]
- Legal shield: VT is an aggregator of third-party opinions, which sits well with Section 230 and with "not our verdict" language. [B]
- Why it survived: a two-sided network effect (vendors give detections, VT gives samples) and a paid intelligence product on top.
- Transferable: a multi-source aggregator that displays each issuer's verdict instead of merging them into one. Reciprocity for contributors, and paid hunting and bulk APIs.

## 5. PhishTank and APWG eCrime Exchange
- PhishTank: community submission and voting (Cisco Talos/OpenDNS). Free API with an app key. It needs several votes from trusted voters to verify. Reputation points weigh the voters. It is fast but has seen quality and capacity decline, and its registration is intermittently closed. [B]
- APWG eCX: member-funded. Members contribute phishing URLs and receive the combined feed. Fees fund the secretariat. Public data is delayed or limited. Law enforcement and researchers get access. Reciprocity: you give to get. [B]
- Quality: voting plus automatic verification for PhishTank. For eCX, vetted-member submissions and APWG staff. [B]
- Disputes: submitter or site owner can request re-check. [B]
- Legal shield: facts about URLs, not people. Membership terms and T&Cs. [B]
- Survival risk: PhishTank depended on one sponsor and has been neglected. eCX has dues and a mission.
- Transferable: reputation-weighted voting for the public tier, and a give-to-get members tier with a delay on public data.

## 6. Have I Been Pwned (HIBP)
- Who pays: Troy Hunt. Sponsor, API and domain-search subscriptions, and Cloudflare. In 2025 he took on staff and reported seeking an acquirer, then stayed independent. The Pwned Passwords API is free and runs on k-anonymity (5-character SHA-1 prefix). [B]
- Free vs paid: free email lookup for individuals and free domain verification for site owners. The paid API key is for programmatic or commercial use, in tiers. Bulk domain search is paid for large orgs. [B]
- Quality: breaches are verified before loading. Sensitive breaches can be flagged so they are not searchable publicly. Email-confirmation protects the subject. [B]
- Disputes and removal: opt-out of a public listing is available, and sensitive-breach handling is by email-verified lookup. [B]
- Legal shield: no passwords stored for emails. Operated from Australia. Data is limited to identifiers (emails) and breach names. Verification of ownership before disclosure. [B]
- Partnerships: the FBI and NCA (UK) feed HIBP breach data and passwords. Governments share data with it. Pwned Passwords is also integrated into NIST-aligned password checks. [B]
- Sustainability risk: key-person dependency. A mission-led person is the single point of failure and of trust.
- Transferable: k-anonymity prefix lookup for privacy. Verified-owner disclosure of sensitive entries. Law-enforcement feeds. Paid API for companies.

## 7. Certificate Transparency (CT)
- Who pays: CAs and browsers. Google, Cloudflare, DigiCert, Let's Encrypt, Sectigo and others each run logs. Logging cost is borne by whoever runs the log. CAs submit certs, so issuers fund the ledger indirectly. [B]
- Free vs paid: log reads are free for everyone. Paid products are monitoring services (e.g., SSLMate, Cert Spotter, Facebook/Meta, Censys). [B]
- Quality: logs are append-only Merkle trees (RFC 6962 and RFC 9162). Browsers require SCTs (signed timestamps) from several independent logs (Chrome requires two or three, depending on lifetime). Misbehaving logs lose browser trust. Monitors and gossip catch split views. [B]
- Disputes: there is no removal, by design. A certificate in the log can be misissued, and the fix is revocation at the CA. Logs may reject by expiry-range shards (temporal sharding) and may be retired. [B]
- Legal shield: logs record public facts (certificates are public), not accusations. Operators hold no opinions about anyone. [B]
- Why transparency beat a blocklist: nobody has to be trusted to say a cert is bad. The log only proves that it exists. Misissuance became detectable by anybody. Browser policy turned a voluntary log into a hard requirement, giving incentive alignment.
- Transferable: separate "recording a claim" from "judging it". Append-only claim logs with receipts, multiple independent operators, a client policy that demands receipts, and a competitive monitor market on top.

## 8. CVE / NVD / MITRE
- Who pays: US government. CISA/DHS funds MITRE under an FFRDC contract. NIST funds NVD. [B]
- 2025 scare: the MITRE contract was due to expire on 16 Apr 2025 and CISA extended it for roughly 11 months at the last minute [V]: https://www.theregister.com/2025/04/16/cve_program_funding_save/ . In parallel, the CVE Foundation was set up by Board members to give the program an independent non-profit home [V], per https://www.techrepublic.com/article/news-mitre-cisa-contract-expiration-cve-database/ . NVD also had an enrichment backlog from 2024. The ENISA EUVD and the GCVE alternatives emerged. Check the current contract status for after Mar 2026. [B]
- Free vs paid: IDs, records and the NVD feeds are all free. Commercial feeds layer enrichment on top. [B]
- Distribution: CNA model. More than 400 CNAs (vendors, CERTs, research orgs, bug bounty platforms) assign IDs inside their own scope. A root CNA structure (MITRE, CISA ICS, JPCERT and others) governs them. CNA rules govern record quality. [B]
- Disputes: a dispute process with the assigning CNA, and escalation to its root and then the Board. Records can be marked REJECTED or DISPUTED. [B]
- Legal shield: government sponsorship, and the entry is about software, not a person. [B]
- Sustainability risk: a single sponsor. The scare shows why a neutral foundation and distribution of numbering authority matter.
- Transferable: distributed issuers with a central registry of rules. Scope-limited authority, with REJECTED/DISPUTED status in place of deletion. Avoid a single funder.

## 9. ISACs, MISP, STIX/TAXII, TLP
- Who pays: member dues. FS-ISAC dues are tiered by size, with a large share from banks. Some ISACs get a government grant. Sector ISACs also sell intelligence products. [B]
- Free vs paid: basic or public alerts are free or partly public. Real-time and detailed feeds are member-only. [B]
- Quality control: analyst vetting, a member-submission trust model, and an anonymous submission option for sensitive incidents. [B]
- Governance tools: TLP (RED, AMBER, GREEN, CLEAR) tells recipients how far they may share. MISP is open source and handles sharing groups and distribution levels. STIX/TAXII give a standard schema and transport. [B]
- Legal shield: the US Cybersecurity Information Sharing Act of 2015 gives liability protection and antitrust exemptions for sharing cyber threat indicators with the government and among private entities, plus a FOIA exemption, if sharing follows the statute's rules (including stripping personal information not directly related to the threat). The act lapsed on 30 Sep 2025 and was extended temporarily; check whether it has been reauthorised since. [B]
- Why it survives: the members need the data and have the budget. Legal safe harbour removes the lawyer's veto.
- Transferable: dues from institutional consumers, TLP-style marking per record, a standard exchange schema, and an explicit statutory or contractual safe harbour that covers the exchange.

## 10. Credit bureaus and fraud consortia (CIFAS, Early Warning, others)
- Who pays: members, i.e., banks, lenders and insurers, through fees and per-query charges. CIFAS is a UK non-profit membership association. Early Warning is owned by large US banks. [B]
- Free vs paid: members pay per use. Consumers get statutory free access. [B]
- Consumer rights: in the US, FCRA gives a free annual credit file disclosure (annualcreditreport.com), free copies after an adverse action or fraud alert, and the right to dispute. Dispute duties fall on both the bureau and the data furnisher, with about a 30-day investigation period. Early Warning's reports (ChexSystems-style) fall under FCRA too. In the UK, UK GDPR subject-access rights give a free copy of data, and CIFAS offers Protective Registration for victims. A CIFAS filing requires the member to hold evidence meeting a standard of proof. [B]
- Quality control: member rules on standard of proof (CIFAS), data accuracy duties on furnishers (FCRA Sec. 623), audits, and mandatory removal if unsubstantiated. [B]
- Legal shield: FCRA qualified immunity for defamation claims unless malice, in exchange for regulated accuracy and dispute duties. In the UK, the legal basis is a legitimate interest under data protection law, with a DPIA and fraud-prevention carve-outs. [B]
- Why it survives: members value the shared protection. Regulation makes the trade explicit: data subject rights in exchange for a legal shield.
- Transferable: a statutory-style trade of "free consumer access and dispute rights" for "shield for the registry", a standard-of-proof gate for listing, and furnisher accountability.

---

## Comparison table

| Model | Who pays | Free to whom | Quality control | Dispute path | Legal shield | Sustainability risk |
|---|---|---|---|---|---|---|
| Spamhaus/DNSBL | Commercial licensees (DQS, feeds) | Low-volume, non-commercial queries | Curated spamtraps, tiered zones, consumer picks policy | Per-listing page and delisting request | Sec. 230(c)(2) in principle, foreign domicile, opinion framing; e360 ended at $3 [V] | Litigation cost; staff-curated; moderate |
| abuse.ch | Industry donations, university host, Spamhaus licence [V] | Everyone (CC0, free key) | Community plus staff, classification, expiry | Contact form, evidence-based removal | Swiss non-profit; indicators only | Donor concentration; low cost mitigates |
| Safe Browsing | Google | Non-commercial apps and all major browsers | Crawler/ML, partner feeds, warning classes | Search Console review, report-incorrect form | Sec. 230, warning UX, ToS | Single sponsor decision; low in practice |
| VirusTotal | Enterprise intelligence customers (Google-owned) | Public upload and lookup, low-rate API | Multi-engine, verdicts shown per vendor | Vendor owns its verdict | Aggregator of third-party opinions | Parent-company priorities |
| PhishTank / APWG eCX | Cisco (PhishTank), member dues (eCX) | Public API key (PT); members and LE (eCX) | Reputation-weighted voting; vetted members | Re-check request | Facts about URLs; T&Cs | PT neglect; eCX dues churn |
| HIBP | Subscriptions, API keys, sponsors | Individuals, domain owners, Pwned Passwords | Verified breaches; sensitive-breach flag | Opt-out; verified-owner lookup | No credentials for emails; AU base; minimal data | Key-person dependency |
| Certificate Transparency | CAs and browsers, log operators | Reads free; monitors paid | Append-only Merkle log; multiple SCTs; auditors | None by design; fix at CA | Records public facts, no judgment | Log operator costs and retirement; mitigated by diversity |
| CVE/NVD | US gov (CISA, NIST); CVE Foundation emerging [V] | Everyone | CNA rules, root CNAs, Board | CNA dispute, REJECTED/DISPUTED | Gov sponsor; software not people | Single funder; 2025 scare [V] |
| ISAC/MISP/TAXII | Member dues, grants | Public subset; members for full feed | Analyst vetting, TLP, trust circles | Intra-community | CISA 2015 safe harbour (lapse risk) [B] | Dues base; statute renewal |
| Bureaus/CIFAS/Early Warning | Member institutions per query | Consumers (statutory free access) | Standard of proof, furnisher accuracy duty, audits | FCRA/GDPR dispute, Protective Registration | FCRA qualified immunity; UK legitimate interest | Regulatory change; cost of disputes |

## Most transferable mechanisms for a crypto stolen-funds registry

1. CT-style claim log. Append-only Merkle log of reports and status changes, run by several independent operators, with signed receipts and public monitors. It records the claim, not the verdict, so there is no deletion. Corrections are new entries ("withdrawn", "disputed", "resolved"), which also lines up with a CVE-style REJECTED/DISPUTED state.
2. Verdict separation (VirusTotal and DNSBL). Display each issuer's attestation and let each consumer (exchange, wallet) set its own policy. This puts the blocking decision, and its liability, on the consumer.
3. Safe-Browsing-style distribution. A free client API with hash-prefix lookup (privacy for the querier, which HIBP also shows), and a paid tier for commercial volume, SLAs and bulk feeds. A free tier for wallets and individuals keeps adoption high.
4. CNA-style distributed issuers. Vetted issuers (exchanges, forensics firms, law enforcement, victim groups) each get authority within a scope, under common rules. A root body sets standards and can suspend an issuer. This spreads both the workload and the liability.
5. ISAC-style member funding with TLP-like marking. Institutional consumers (exchanges, custodians, compliance vendors) pay dues. Each record carries sharing and visibility labels, so sensitive cases can be restricted.
6. Consumer free-access and dispute right (FCRA/GDPR logic). Anyone can look up and contest a listing for free, within a fixed investigation window, with a standard of evidence for listing. This is the legal trade that keeps the registry defensible.
7. Anchor in a non-profit or university with a single commercial redistributor (abuse.ch plus Spamhaus). It avoids dependence on one sponsor, as with the CVE funding scare, and avoids key-person risk (HIBP).
8. Legal posture. Frame entries as reports of facts with evidence and pointers, not accusations about named people. Use a foreign or neutral domicile where appropriate. Rely on Section 230(c)(2)-type good-faith filtering where it exists. Seek an explicit safe harbour for sharing (CISA 2015 is the model), and don't assume it will persist.

Open items to verify before external use: all [B] items; CISA 2015 reauthorisation status; the current CVE contract status after March 2026; and whether PhishTank is still accepting registrations.

Verified sources: 
- https://blog.ericgoldman.org/?p=9923
- https://blog.ericgoldman.org/?p=10307
- https://www.bfh.ch/en/research/reference-projects/abuse-ch/
- https://abuse.ch/blog/
- https://www.theregister.com/2025/04/16/cve_program_funding_save/
- https://www.techrepublic.com/article/news-mitre-cisa-contract-expiration-cve-database/
