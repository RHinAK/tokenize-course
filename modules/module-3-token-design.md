# Module 3: Designing Your Token Economy

## Learning Objectives
- Choose the right tokenization model for your business
- Design supply, distribution, and governance rules
- Understand regulatory considerations
- Create a token specification document

---

## Lesson 3.1: Tokenization Models

### Model 1: Equity/Ownership Tokens
Represent fractional ownership in a business or asset.

**Use case:** You own a $500K rental property. Tokenize it into 500,000 tokens at $1 each. Investors buy tokens to own fractional shares. Rental income is distributed proportionally.

**XRPL setup:**
- Currency code: `REALTY` or hex code for longer name
- Supply: Fixed (matches asset value)
- Freezable: Yes (required for SEC compliance)
- Clawback: Yes (legal requirement)
- Transfer fee: 0-2% (creates secondary market revenue)

### Model 2: Revenue Share Tokens
Holders earn a share of business revenue without owning equity.

**Use case:** A restaurant issues 10,000 tokens. Each token entitles the holder to 0.01% of monthly revenue, paid in XRP. Token holders are customers, not owners.

**XRPL setup:**
- Supply: Fixed
- Freezable: No (builds trust)
- Transfer fee: 0.5% (discourages speculation)

### Model 3: Commodity-Backed Tokens
Each token represents a physical asset.

**Use case:** A gold dealer issues tokens backed 1:1 by physical gold. 1 GOLD token = 1 gram of gold stored in a vault. Token holders can redeem for physical gold.

**XRPL setup:**
- Supply: Variable (grows as more gold is vaulted)
- Freezable: Optional
- Regular audits required to prove backing

### Model 4: Utility/Access Tokens
Provide access to services or products.

**Use case:** A SaaS company issues tokens that represent API credits. 1 token = 1,000 API calls. Tokens are tradeable — unused credits have resale value.

**XRPL setup:**
- Supply: Variable
- No regulatory burden (utility, not security)
- Transfer fee: 0% (maximize liquidity)

### Model 5: Loyalty/Rewards Tokens
Replace traditional points programs.

**Use case:** A coffee shop issues BEAN tokens. 1 BEAN per $1 spent. 100 BEAN = free drink. Unlike traditional points, BEAN tokens can be traded, gifted, or sold.

**XRPL setup:**
- Supply: Unlimited (inflationary by design)
- Freezable: No
- Zero transfer fee

---

## Lesson 3.2: Supply Design

### Fixed vs. Variable Supply

**Fixed supply** — Total tokens created once, never changes.
- ✅ Scarcity drives value
- ✅ Simple to audit
- ❌ Can't adjust to demand
- Best for: Equity, real estate, art

**Variable supply** — Issuer can create (mint) or destroy (burn) tokens.
- ✅ Flexible
- ✅ Can match real-world supply
- ❌ Requires trust in issuer
- Best for: Commodity-backed, utility tokens

### Distribution Strategy

| Method | Description | Best For |
|--------|-------------|----------|
| Direct sale | Sell tokens at fixed price | Equity, real estate |
| DEX listing | List on XRPL's built-in exchange | Utility, rewards |
| Airdrop | Free distribution to wallets | Marketing, community |
| Revenue-based | Earn tokens through participation | Loyalty programs |
| Vesting | Locked tokens that unlock over time | Team/advisor allocation |

---

## Lesson 3.3: Regulatory Reality Check

⚠️ **This is not legal advice. Consult a securities attorney.**

### The Howey Test (US)
A token is likely a **security** if it passes the Howey Test:
1. Investment of money ✅
2. In a common enterprise ✅
3. With expectation of profit ✅
4. From the efforts of others ✅

If all four: it's probably a security. Register with SEC or use an exemption.

### Common Exemptions
- **Reg D (506b/506c)** — Sell to accredited investors only. No SEC registration.
- **Reg A+** — Raise up to $75M from anyone. Requires SEC qualification.
- **Reg CF** — Crowdfunding up to $5M through registered platforms.
- **Reg S** — Sell to non-US persons only.

### When You DON'T Need SEC Registration
- Pure utility tokens (no profit expectation)
- Loyalty/rewards tokens (no investment element)
- Commodity tokens with proper CFTC compliance
- NFTs representing unique items (case by case)

### Best Practice for Business Owners
1. Start on testnet — always
2. Consult a securities attorney before any token sale
3. If in doubt, use Reg D with accredited investors only
4. Document everything — whitepaper, audits, legal opinions
5. XRPL's built-in freeze/clawback helps with compliance

---

## Lesson 3.4: Your Token Specification Document

Before writing any code, create a Token Spec:

```
TOKEN SPECIFICATION
==================
Project Name: [Your Project]
Token Code: [3-char or hex]
Issuer Account: [To be created]

PURPOSE
What does this token represent?
Who are the target holders?
What problem does it solve?

ECONOMICS
Total Supply: [number]
Supply Type: Fixed / Variable
Initial Price: $[amount]
Distribution: [method]

PROPERTIES
Transferable: Yes/No
Freezable: Yes/No
Clawback: Yes/No
Transfer Fee: [%]

REGULATORY
Jurisdiction: [country/state]
Classification: Security / Utility / Commodity
Exemption: Reg D / Reg A+ / None needed
Legal counsel: [firm name]

TECHNICAL
Network: Testnet → Mainnet
Wallet support: XUMM, Ledger, etc.
DEX listing planned: Yes/No
```

---

## Action Items
1. Choose which tokenization model fits your business
2. Fill out the Token Specification Document above
3. Research whether your token would be classified as a security
4. Find a securities attorney in your jurisdiction (search "digital asset attorney [your state]")

---

*Next: Module 4 — Building on XRPL: Code & Tools*
