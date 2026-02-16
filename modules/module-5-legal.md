# Module 5: Legal & Compliance

## Learning Objectives
- Understand when a token is a security vs. utility
- Know the major SEC exemptions for token offerings
- Build a compliance framework for your token
- Prepare documentation for legal counsel

---

## Lesson 5.1: Is Your Token a Security?

### The Howey Test (1946 — Still the Standard)

The SEC uses a 4-part test from *SEC v. W.J. Howey Co.* to determine if something is a security:

1. **Investment of money** — Did the buyer pay cash, crypto, or anything of value?
2. **Common enterprise** — Are all investors' funds pooled together?
3. **Expectation of profit** — Does the buyer expect to make money?
4. **From the efforts of others** — Does the profit come from the issuer's work, not the buyer's?

**If ALL FOUR = YES → It's likely a security.**

### Token Classification Matrix

| Token Type | Investment? | Common Enterprise? | Profit Expected? | Efforts of Others? | Security? |
|-----------|------------|-------------------|-----------------|-------------------|-----------|
| Real estate equity token | ✅ | ✅ | ✅ | ✅ | **YES** |
| Revenue share token | ✅ | ✅ | ✅ | ✅ | **YES** |
| Gold-backed token | ✅ | ❌ | Maybe | ❌ | **Likely no** |
| Utility/access token | ✅ | ❌ | ❌ | ❌ | **No** |
| Loyalty points token | ❌ | ❌ | ❌ | ❌ | **No** |

### The Gray Areas
- **Governance tokens** — Could be securities if there's profit expectation
- **NFTs** — Generally not securities, but fractionalized NFTs might be
- **Stablecoins** — Regulatory frameworks still evolving

---

## Lesson 5.2: SEC Exemptions

If your token IS a security, you don't necessarily need full SEC registration. These exemptions let you issue legally:

### Regulation D — Rule 506(b)
- **Who can buy**: Up to 35 non-accredited + unlimited accredited investors
- **Fundraising limit**: None
- **General solicitation**: ❌ Not allowed
- **Filing**: Form D within 15 days
- **Holding period**: 12 months (restricted securities)
- **Best for**: Friends & family rounds, private placements

### Regulation D — Rule 506(c)
- **Who can buy**: Accredited investors ONLY (must verify)
- **Fundraising limit**: None
- **General solicitation**: ✅ Allowed (advertise openly)
- **Filing**: Form D within 15 days
- **Holding period**: 12 months
- **Best for**: Public marketing to wealthy investors

### Regulation A+ (Mini-IPO)
- **Tier 1**: Up to $20M from anyone. State filing required.
- **Tier 2**: Up to $75M from anyone. SEC qualification required.
- **General solicitation**: ✅ Allowed
- **Filing**: Form 1-A with SEC
- **Holding period**: None for Tier 2
- **Cost**: $50K-$150K in legal/accounting fees
- **Best for**: Larger raises from the general public

### Regulation Crowdfunding (Reg CF)
- **Who can buy**: Anyone
- **Fundraising limit**: $5M per year
- **Platform**: Must use SEC-registered funding portal
- **General solicitation**: ✅ Allowed
- **Filing**: Form C with SEC
- **Cost**: $10K-$50K
- **Best for**: Small raises with public marketing

### Regulation S
- **Who can buy**: Non-US persons only
- **Fundraising limit**: None
- **Filing**: None with SEC
- **Best for**: International token offerings

---

## Lesson 5.3: State Considerations

### Blue Sky Laws
Every US state has its own securities laws ("blue sky laws"). Even with federal exemptions:

- **Rule 506**: Preempts state registration (states can't block your offering)
- **Reg A+ Tier 2**: Also preempts state registration
- **Reg CF**: Preempts state registration
- **Reg A+ Tier 1**: Must register in each state where you sell

### State Money Transmitter Licenses
If your token is used as a payment method (not just investment), you may need money transmitter licenses in each state. This is expensive and complex. Most tokenization projects avoid this by:
- Making tokens non-transferable between users
- Using XRPL's authorized trust line feature
- Classifying as investment, not payment

---

## Lesson 5.4: Building Your Compliance Framework

### Required Documents

1. **Private Placement Memorandum (PPM)**
   - Detailed description of the offering
   - Risk factors
   - Use of proceeds
   - Financial statements
   - Management team bios

2. **Subscription Agreement**
   - Terms of purchase
   - Investor representations
   - Accreditation verification (for 506c)

3. **Operating Agreement Amendment**
   - If tokenizing LLC interests
   - Token holder rights and restrictions
   - Transfer restrictions

4. **Token Purchase Agreement**
   - Technical details of the token
   - Delivery mechanism
   - Lockup periods

5. **Legal Opinion Letter**
   - Attorney's analysis of security classification
   - Exemption applicability
   - Regulatory compliance confirmation

### Finding an Attorney

Search for: "digital asset attorney" or "blockchain securities lawyer" + your state.

Key qualifications:
- Experience with token offerings (not just general securities)
- Understanding of XRPL specifically
- Familiarity with your chosen exemption
- Reasonable fees ($5K-$25K for a Reg D offering)

**Organizations with attorney directories:**
- Digital Chamber of Commerce
- Blockchain Association
- State bar association (search "blockchain" or "digital assets")

---

## Lesson 5.5: XRPL Compliance Features

XRPL has built-in features specifically designed for regulated tokens:

### Authorized Trust Lines
- Only approved addresses can hold your token
- Issuer must explicitly authorize each holder
- Perfect for KYC/AML compliance

### Freeze
- **Individual freeze**: Freeze a specific holder's tokens
- **Global freeze**: Freeze ALL transfers of your token
- Required by regulators for security tokens
- Enable this BEFORE distributing tokens

### Clawback
- Recover tokens from any holder
- Required for certain regulated instruments
- Must be enabled at account creation (can't add later)
- Use case: Court-ordered recovery, compliance violations

### Transfer Fee
- Automatic fee on every secondary transfer
- Revenue for the issuer on resale
- Helps control speculation

---

## Action Items
1. Determine if your token is a security using the Howey Test
2. Choose the most appropriate exemption (Reg D is usually the starting point)
3. Budget $5K-$25K for legal fees
4. Find a digital asset attorney in your jurisdiction
5. Enable freeze and clawback on your issuer account BEFORE distributing

---

*Next: Module 6 — Launch Strategy*
