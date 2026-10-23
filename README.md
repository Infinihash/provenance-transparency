# Provenance Transparency: crypto safety data without a paywall

**Status:** request for comment, v0.3 draft (October 2026). Comments are open until 30 November 2026 in this repository's Discussions, or by email to hello@infinihash.com. A revised Each revision will say what changed, why, and who argued for it.

**Read:** the [web page](https://kyt.infinihash.com/provenance) · the [one-page brief (PDF)](onepager.pdf) · this document, the full proposal.

**Licence:** the text is CC BY 4.0 (see LICENSE). Quote it, adapt it, argue with it.

---

Proposal, Oct 22–23, 2026. Built on two research notes in this repository: [research/landscape.md](research/landscape.md) (who sells crypto safety data, and what the free lists did) and [research/models.md](research/models.md) (how other industries made abuse data a public good). Both mark each claim [V] verified, [M] from memory or [B] background knowledge. Several funding and legal figures are [M]/[B]: treat them as leads to check, not facts, and tell us where they are wrong.

## Part 1 · Why

Someone is about to send money to a wallet that received stolen funds last week. The fact that it did is known. It sits in a database that an exchange compliance team pays five or six figures a year to query. The person with their finger on Send does not have that database. Their wallet does not have it. The scam-report site they might check allows ten lookups a month on a free key. So the warning exists, and the one person who needed it never sees it.

That is the whole problem, and it is a market structure, not a technical gap. Three things hold it in place.

- **Labels are the product.** Every forensics vendor sells the same thing: a list of addresses and what they are. Publish the list and the business is gone. No vendor will do it, and no one should expect them to.
- **A label is a liability.** "This wallet is a scammer" is a statement about a person. Get it wrong and you are sued. The vendors carry that risk behind contracts and indemnities; a free list has nothing behind it, so a free list says nothing, or says it recklessly.
- **The free lists that were tried died.** No revenue, no trust layer, no reason for anyone to keep writing. Bots and recovery scammers poisoned the open ones; the curated ones went quiet when the one volunteer moved on. Each failure is now cited as proof that open safety data cannot work.

Reported figures (third-party estimates, see research/landscape.md): vendor wallet labels run $26k–$295k a year; the largest free scam-report site allows 10 lookups a month on a standard key.

**Why it matters more every year: crypto has become trade.** Crypto is no longer only something people buy and sell on exchanges. Stablecoins settle at the scale of card networks: about $9 trillion moved in the year to late 2025 once bot activity is stripped out, more than half of Visa's volume [1]. The fastest-growing use is not trading but paying. Payment firms handling real invoices report $122 billion a year in stablecoin payments, with business-to-business transfers the largest and fastest-growing part at $76 billion, up from $36 billion six months earlier [3]. In Nigeria, Turkey, Brazil, India and Indonesia people hold dollars in stablecoins and pay across borders with them [5]. Commodities are part of it: Reuters reports Russian oil sold to China and India settled partly in Tether, and Venezuela's state oil company moved its sales to USDT under sanctions [9][10].

The consequence that matters here: more and more of that value never touches an exchange. In several regions a third to a half of activity happens off centralized exchanges [8]. Chainalysis records regular multi-million-dollar stablecoin transfers in energy and merchant trade between Africa, the Middle East and Asia, and notes that its own exchange data misses business-to-business and over-the-counter flows [7]. The BIS finds capital controls barely slow these flows [11]. Regulators now treat stablecoins as payment infrastructure (the US GENIUS Act, Hong Kong's licensing regime) and banks are running settlement pilots [13][14].

So the people transacting are increasingly transacting with each other, not with an exchange. Exchange-side compliance, which is where all the paid safety data lives, does not reach a direct transfer between two businesses or two people. Neither party gets a warning before it pays. The BIS itself warns that stablecoins are weak on identity checks [12]. The gap this proposal closes is not shrinking. It grows with the trade.

*What the evidence does not show:* most on-chain stablecoin volume is still trading, DeFi and bots, and identifiable payments are about 1% of settlement [4]; on-chain data cannot prove a transfer is business-to-business; the oil reports rest on anonymous sources and economists' estimates [9][10]; stablecoins remain under 1% of global FX and money supply [6]. "Tipping point" describes the growth and the new rules, not market share. Numbered references: [research/trade.md](research/trade.md).

**Why it matters more than one theft.** In October 2026 a $1M proof-of-funds theft was traced across four chains. It belonged to a ring of about 46 thefts, about $16M, running since 2022. The trace mapped 102 wallets and 64 exchange accounts. Every exchange the ring used had bought the paid data. Almost none of the ring's wallets carried a public warning until the victim's team filed them, one form at a time, while the ring kept moving money through fresh addresses no form had reached yet. Multiply that by every ring. The data that would keep people safer already exists. It is priced for the wrong buyer.

> The rule from every industry that beat abuse at scale: free for the people being protected, paid by the people making money from the data.

Spam blocklists, breach-notification services, certificate transparency, CVE: each publishes the evidence for free and lets a market sell the judgment on top. Crypto does it backwards. It sells the evidence. This proposal turns it the right way round.

### What exists already, and what this adds

Public scam reporting exists. Chainabuse takes reports from anyone and is read widely. The Security Alliance's sharing networks move warnings between security teams quickly. Exchange and vendor lists are deep and well funded. None of that is dismissed here; the log is designed to sit underneath all of it.

What none of them provides: a claim that is signed by an accountable issuer, tied to hashes of the evidence behind it, entered in a public record that no operator can quietly edit, with a dispute process whose outcome is as public as the claim, and an erasure path for the person who was wrongly named by circumstance. Reports can be anonymous and are hard to test. Membership lists are closed. Vendor lists are products. A fact that a victim's counsel needs to rely on, in front of a court, has to be attributable, evidenced and correctable in public. That is the gap this proposal fills, and it is a narrow one on purpose.

Operators of existing services are invited to mirror the log and to file to it. If the record becomes substrate for the tools people already use, it has done its job.

## Part 2 · How

Split the data in two. The **facts** go in a public, append-only log that anyone can read for free, forever. The **judgments** stay with whoever is making the decision: the wallet, the exchange, the vendor. The log never says "bad wallet". It says "funds from this transaction are proceeds of this incident, here is the evidence, here is who says so and how sure they are." Everything below is a consequence of that split.

| Facts: the log | Judgments: the market |
|---|---|
| Append-only, several independent operators, free to read | Each consumer applies its own policy to the same record |
| An entry is a signed claim about a transaction: evidence hashes, issuer, confidence | A wallet may warn at confidence 6; an exchange may hold at 8 from two issuers |
| Corrections are new entries (disputed, withdrawn, superseded); nothing is deleted | Scores, clustering, exposure, service levels stay commercial, built on top |

### How a fact gets in

1. **An accredited issuer files a claim.** Exchanges, forensics firms, police units and accredited victim-side investigators, each with scoped authority under a root body that sets the evidence standard and can suspend an issuer. Anyone can report; only an issuer can file. That is the trust layer the dead lists never had.
2. **The claim carries evidence, not opinion.** Transaction hash, address, amount, incident reference, and hashes of the evidence bundle (victim statement, police reference, trace). Confidence is a number the issuer signs its name to. A claim with no evidence hashes is rejected at the door.
3. **The issuer pays a filing fee.** Small, flat, per claim. It funds the operators and makes bulk poisoning expensive. Reading stays free. Victims' counsel will pay it gladly: a logged claim is the thing they need next.
4. **Operators sign a receipt and monitors check them.** At least three independent operators (a university host, a security collective, an exchange) each sign the entry into their copy. Public monitors compare the copies; an operator that drops or alters an entry is caught by the other two. Certificate transparency, applied to stolen funds.

### How a fact gets out

1. **Wallets look up by hash prefix.** A wallet about to sign sends the first bytes of a hash of the destination address, gets back the matching bucket, checks locally. The log never learns which address was queried. Free at consumer volume; a paid tier for heavy commercial use.
2. **The wallet applies its own policy.** The log returns claims, not verdicts. The wallet decides what to show. The policy sits with the wallet, and so does liability for the warning it chooses to show. The split does not make the log liability-free, and it is not presented as a shield. An issuer is responsible for the truth of what it signs. An operator is responsible for publishing the record faithfully, including corrections and dispute outcomes. The evidence hashes, the dispute process and the erasure path exist because that responsibility is real, not as decoration.
3. **On-chain notices become receipts.** When an issuer sends an on-chain notice to a wallet holding stolen funds, the notice transaction is logged. Anyone who later receives those funds can be shown to have had notice available — what victims' counsel need to argue knowing receipt, today reconstructed by hand.
4. **Exchanges get bulk access by contributing.** An exchange gets the bulk feed only by filing its own confirmed scam deposit addresses and sweep mappings. The largest holders of safety data become its largest contributors, and the log fills the one gap every list has: which account the money finally reached.

### How it stays honest

**Disputes:** a fixed window, an evidence standard, a panel that excludes the issuer; the outcome is itself a log entry. **Erasure:** a person who proves the address is theirs and the funds are clean gets a superseding entry and, where the law requires it, removal of identifiers. **Suspension:** an issuer whose claims keep losing disputes loses its authority; only the root body can grant or remove it, and its decisions are logged too.

The window is thirty days from filing, shortened to seven where the claim is attached to funds still moving. A dispute pauses nothing by itself; it marks the claim as disputed in the record, and consumers set their own policy for disputed claims. The panel decides within thirty days of the window closing. Every step is an entry.

### How it is paid for

Filing fees will not fund this at the start, and the table below describes the steady state, not the launch. The bootstrap is a subsidy: public-goods grants and recovery pledges from firms that expect to use the record, covering operator costs and dispute panels for the first two years, with the amounts and the funders published. The log runs at a loss while it proves itself. That is stated here because a funding model that only works on paper is how the earlier lists died quietly.

| Layer | Free to | Paid by |
|---|---|---|
| The log, receipts, monitors | Everyone | Issuer filing fees, institutional reciprocity dues, recovery pledges, public-goods grants |
| Hash-prefix lookup API | Wallets and apps at consumer volume | A volume tier for heavy commercial use |
| Scores, clustering, exposure, SLAs | Nobody | Commercial vendors built on top of the log |
| Legal-grade evidence bundles | Victims, at cost | Counsel; recoverable as costs |

One more source, opt-in and in need of legal structuring: an issuer may attach a pledge that a small share of funds recovered on a logged claim goes to the operator foundation. Funding then scales with usefulness, not with how many exchanges renew a licence.

### How it survives where the free lists died

| What killed the open lists | What this has instead |
|---|---|
| No revenue path | Filing fees, reciprocity dues, recovery pledges, vendor service tiers; none from selling labels |
| No trust layer; poisoned by bots and recovery scammers | Accredited issuers, an evidence standard, filing fees, disputes |
| Nobody with a reason to keep writing | Victims' counsel, who need logged notice to prove knowing receipt |
| Nobody with a reason to keep reading | Exchanges, who want the map of which accounts received the money |
| A single owner who could quietly remove entries | Append-only, several operators, public monitors |

Nothing here is invented. Each piece has run for a decade or more somewhere else (Certificate Transparency operators and monitors; CVE numbering authorities; Spamhaus's free/paid split; credit-fraud consortia's consumer rights). The new part is combining them for stolen-funds provenance.

## Part 3 · What — DRAFT

The concrete thing we propose to build, written as a first draft so it can be argued with line by line. Everything in this part is open to change in v0.4.

### The claim record

One schema, versioned, signed. Addresses and hashes are illustrative.

```jsonc
// provenance claim, schema v0.1 (draft)
{
  "claim_id":   "pt:2026-10-22:000418",
  "kind":       "proceeds_of_theft",   // | proceeds_of_fraud | notice_delivered | dispute | withdrawal
  "incident":   "inc-2026-1014-pof",
  "chain":      "ethereum",
  "tx":         "0x3c54…5cb0",
  "address":    "0xa91c…6f43",
  "amount":     {"asset": "USDT", "value": "1000000.79"},
  "evidence":   ["sha256:9f2c…e41a", "sha256:71bd…0c88"],
  "issuer":     "did:issuer:accredited-0007",
  "confidence": 8,                     // 1–10, signed by the issuer
  "status":     "active",              // active | disputed | withdrawn | superseded
  "supersedes": null,
  "notice_tx":  "0xad19…b6f8",          // on-chain notice delivered, if any
  "issued_at":  "2026-10-22T17:46:53Z",
  "signature":  "ed25519:…"
}
```

Deliberately absent: any name, any KYC identifier, any statement about who controls the address. The record is about a transaction and the money in it.

### The confidence rubric

A confidence score is only useful if two issuers mean roughly the same thing by it. The rubric below is a first draft; the evidence standard, once set by the root body, owns it.

| Score | Meaning |
|---|---|
| 9–10 | Filed in or referenced by a court proceeding or a law-enforcement report, with the full evidence bundle hashed into the claim. |
| 7–8 | Investigator trace plus a victim statement, both hashed. Two independent sources agree on the flow of funds. |
| 5–6 | A single credible source: a trace or a victim statement with supporting records, hashed. |
| 3–4 | A report with partial corroboration. Published, but no consumer should hard-stop on it alone. |
| 1–2 | Uncorroborated. Reserved for notice-delivered records and early warnings clearly labelled as such. |

An issuer whose scores repeatedly fail to match outcomes in disputes is miscalibrated, and miscalibration is a ground for suspension, the same as filing without evidence.

### The log

- **Structure.** An append-only Merkle log, one entry per claim, with a signed tree head published by each operator at a fixed interval.
- **Operators.** Three at launch, independent of each other and of Infinihash: a university host, a security collective, an exchange. Each runs the reference implementation or its own.
- **Monitors.** Anyone can run one; it fetches tree heads from every operator and alarms on divergence. Infinihash will run one; so should at least one party that distrusts Infinihash.
- **Retention.** Forever. Erasure replaces identifiers with a redaction marker and a reason; the entry and its hash chain remain.

### Governance at the start, stated plainly

At launch, Infinihash holds the root: it accredits the first issuers against the published evidence standard and can suspend them. That is centralisation, and pretending otherwise would cost more trust than admitting it.

The exit is part of the design, not a promise about intentions. Every accreditation and suspension decision is a public log entry from day one, so the record of how the root was used exists whether or not Infinihash keeps it. The root passes to a body with at least three members, no one of them Infinihash, when two conditions are met: three independent operators are live, and at least five accredited issuers are filing. Until then, Infinihash publishes each quarter how many operators and issuers are live, so progress toward the handoff can be checked by anyone. A single owner is a paywall waiting to happen; a temporary steward with published conditions is a bootstrap.

### The lookup

```text
GET  /v1/lookup/{chain}/{sha256_prefix_4_bytes}   # k-anonymity: the log never sees the address
  -> { "bucket": [ { "address_hash": "sha256:…", "claims": [claim_id, …], "max_confidence": 8 }, … ] }
GET  /v1/claim/{claim_id}                          # full record, free
GET  /v1/incident/{incident_id}                    # all claims under one incident
POST /v1/claim                                     # issuers only, signed, filing fee
POST /v1/dispute/{claim_id}                        # anyone, with evidence; opens the window
```

The reference wallet integration shows one line when a destination matches: *"This address received funds that an accredited issuer has logged as proceeds of theft (confidence 8 of 10, incident inc-2026-1014). Continue?"* The wallet chooses the threshold and the wording. The log supplies only the fact.

### The consumer bill of rights

1. Free lookup of any address, by anyone, with no account.
2. A free dispute, with a fixed window and a published evidence standard, decided by a panel that excludes the issuer.
3. Erasure of identifiers for a person who proves innocence, logged as a superseding entry.
4. No statement about any named person, ever. Claims are about transactions.
5. Every decision that affects an entry (accept, dispute, suspend, erase) is itself a public entry.

### The reciprocity agreement, in two steps

An exchange that wants the bulk feed signs one agreement, in two steps. Step one: it files, as an accredited issuer, every deposit address it has itself confirmed as receiving scam or theft proceeds, within a fixed number of days of confirmation. In return it receives the full log as a feed, with a service level, and pays no licence fee. Step two, once it has seen the feed's value: it adds the sweep mapping from each deposit address to its hot wallet, the record no single list has today. If it stops filing, the feed stops. The first step is deliberately cheap to accept; dependence on the feed is what makes the second step reasonable.

### The first ninety days

1. Publish the schema and the consumer rights; recruit two outside operators.
2. Seed the log from the anonymised October 2026 case and from open blocklists whose licences permit it.
3. Ship the hash-prefix lookup API and one wallet warning integration.
4. Sign the first reciprocity agreement with one exchange.
5. Run the first dispute end to end, in public.

### What we are asking for

- Two independent operators: a university or a security collective, and an exchange.
- One exchange willing to be the first reciprocity signatory.
- Public-goods funding for the bootstrap, so no single company pays for the log and therefore owns it.
- Argument. The open questions below are the ones we most want challenged.

**Infinihash** builds the reference implementation and acts as first issuer. It will not own the log. A single owner is a paywall waiting to happen.

One interest, stated plainly: Infinihash intends to sell judgements built on top of this log. That is the business the log makes possible, for Infinihash and for every other vendor. The log is structured so that it never needs Infinihash to survive: independent operators, public monitors, and a root that leaves on published conditions. Judge the structure, not the motive.

### Open questions for v0.4

- Will exchanges accept reciprocity? No precedent for exchanges jointly funding an open fraud feed was found.
- How is the recovery pledge structured so it is not a recovery service in the regulatory sense?
- Wallet addresses as personal data under the 2025 EDPB guidelines; the shape of the erasure process.
- The status of information-sharing safe harbours in the US and UK.
- The right size of a filing fee: enough to deter poisoning, not enough to deter small victims' counsel.
- Verify the funding figures and licence terms marked [M]/[B] in [research/](research/).

## Discuss

Comments are open until 30 November 2026 in [Discussions](https://github.com/Infinihash/provenance-transparency/discussions) (thread #1) or by email to hello@infinihash.com. Say whether we may quote you. v0.2 will say what changed, why, and who argued for it.
