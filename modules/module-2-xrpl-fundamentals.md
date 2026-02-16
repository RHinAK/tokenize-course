# Module 2: XRPL Fundamentals

## Learning Objectives
- Create and fund an XRPL wallet
- Understand trust lines and how tokens work on XRPL
- Know the difference between testnet and mainnet
- Execute your first token transaction

---

## Lesson 2.1: Wallets & Accounts

### Account Basics
Every XRPL account has:
- **Address** — Starts with 'r' (e.g., `rN7n3473SaZBCG4dFL83w7p1W9cgPBKpao`)
- **Secret key** — Never share this. Controls the account.
- **Reserve** — 10 XRP minimum balance (can't be spent — holds your account open)
- **Owner reserve** — 2 XRP per object you own (trust lines, offers, etc.)

### Creating Your First Wallet

**Testnet (free, for learning):**
1. Go to https://xrpl.org/resources/dev-tools/xrp-faucets
2. Click "Generate Testnet Credentials"
3. Save your address and secret somewhere safe
4. You'll receive 1,000 test XRP automatically

**Mainnet (real money):**
1. Use a reputable wallet: XUMM (Xaman), Ledger, or Trust Wallet
2. Send at least 10 XRP to activate the account
3. Back up your secret key / recovery phrase in multiple secure locations

⚠️ **SECURITY RULE**: Never share your secret key. No legitimate service will ever ask for it. If someone asks for your secret, it's a scam. Period.

---

## Lesson 2.2: Trust Lines

Trust lines are the mechanism that enables tokens on XRPL. They're like saying "I'm willing to hold this token from this issuer."

### How Trust Lines Work
1. **Issuer creates a token** (just by having people create trust lines to them)
2. **Holder creates a trust line** to the issuer for that currency
3. **Issuer sends tokens** along the trust line
4. **Holder can trade** the tokens on the DEX or send to other trust line holders

### Think of It Like a Bank Account
- The **issuer** is like a bank
- The **trust line** is like opening an account at that bank
- The **token balance** is like your account balance
- You choose which "banks" (issuers) you trust

### Cost
Each trust line requires a 2 XRP owner reserve. If you create trust lines to 5 different tokens, that's 10 XRP locked up (in addition to the 10 XRP base reserve).

---

## Lesson 2.3: Token Properties on XRPL

When creating a token, you have control over:

| Property | Description | Example |
|----------|-------------|---------|
| Currency code | 3-char or hex string | `USD`, `GOLD`, `REALTY` |
| Total supply | How many tokens exist | 1,000,000 |
| Transferable | Can holders send to each other? | Yes/No |
| Freezable | Can issuer freeze transfers? | Yes/No (compliance) |
| Clawback | Can issuer claw back tokens? | Yes/No (regulated assets) |
| Transfer fee | % fee on each transfer | 0.1% |

### For Business Owners: Which Properties Matter?

**Tokenizing equity/membership interests:**
- Freezable: YES (compliance requirement)
- Clawback: YES (legal requirement in many jurisdictions)
- Transfer fee: Optional (creates revenue on secondary trading)

**Tokenizing a commodity or product:**
- Freezable: Usually NO
- Clawback: Usually NO
- Transfer fee: Optional

**Creating a loyalty/rewards token:**
- Freezable: NO
- Clawback: NO
- Transfer fee: NO

---

## Lesson 2.4: Hands-On — Your First Token

### Step-by-Step on Testnet

```javascript
// Using xrpl.js (Node.js)
const xrpl = require('xrpl')

async function createToken() {
  const client = new xrpl.Client('wss://s.altnet.rippletest.net:51233')
  await client.connect()

  // Fund two test wallets
  const issuer = (await client.fundWallet()).wallet
  const holder = (await client.fundWallet()).wallet

  console.log('Issuer:', issuer.address)
  console.log('Holder:', holder.address)

  // Step 1: Holder creates trust line to issuer
  const trustSet = {
    TransactionType: 'TrustSet',
    Account: holder.address,
    LimitAmount: {
      currency: 'TST', // Your token code
      issuer: issuer.address,
      value: '1000000', // Max they'll hold
    },
  }
  await client.submitAndWait(trustSet, { wallet: holder })
  console.log('✅ Trust line created')

  // Step 2: Issuer sends tokens to holder
  const payment = {
    TransactionType: 'Payment',
    Account: issuer.address,
    Destination: holder.address,
    Amount: {
      currency: 'TST',
      issuer: issuer.address,
      value: '1000', // Send 1000 tokens
    },
  }
  await client.submitAndWait(payment, { wallet: issuer })
  console.log('✅ 1000 TST tokens sent!')

  await client.disconnect()
}

createToken()
```

### What Just Happened?
1. Created two funded accounts on testnet
2. The "holder" said "I trust the issuer for up to 1M TST tokens"
3. The "issuer" sent 1,000 TST tokens
4. The holder now owns 1,000 TST tokens — verifiable on the blockchain

---

## Action Items
1. Create a testnet wallet and save your credentials
2. Create a trust line to a test token
3. Send yourself tokens between two test wallets
4. Explore the testnet explorer: https://testnet.xrpl.org

---

*Next: Module 3 — Designing Your Token Economy*
