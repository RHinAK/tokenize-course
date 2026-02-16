# Module 4: Building on XRPL — Code & Tools

## Learning Objectives
- Create tokens using TokenForge (no code required)
- Understand xrpl.js for developers who want to go deeper
- Configure issuer account settings for compliance
- Set up batch token distribution

---

## Lesson 4.1: TokenForge — No-Code Token Creation

TokenForge (tokenforgehq.com) handles the technical complexity so you can focus on your business.

### Step 1: Connect Your Wallet
- Sign up at tokenforgehq.com
- Connect your XRPL wallet (XUMM recommended)
- Choose testnet for learning, mainnet when ready

### Step 2: Configure Your Token
- **Currency code**: 3 characters (e.g., `TST`) or up to 40 characters via hex encoding
- **Total supply**: How many tokens to create
- **Decimal places**: How divisible (0 = whole tokens only, 6 = micro-units)

### Step 3: Set Token Properties
- **Transfer fee**: 0-100% fee on secondary transfers (you earn this)
- **Require authorization**: Holders must be approved before receiving tokens
- **Freeze enabled**: Ability to freeze individual accounts (compliance)
- **No rippling**: Prevent tokens from being used as intermediary in payments
- **Clawback**: Ability to recover tokens from holders (regulated assets)

### Step 4: Deploy
- TokenForge submits the transactions to XRPL
- You sign with your wallet (non-custodial — we never see your keys)
- Token is live in 3-5 seconds

---

## Lesson 4.2: Developer Path — xrpl.js

For developers who want full control:

### Setting Up the Issuer Account

```javascript
const xrpl = require('xrpl')

async function setupIssuer() {
  const client = new xrpl.Client('wss://s.altnet.rippletest.net:51233')
  await client.connect()

  const issuer = (await client.fundWallet()).wallet

  // Enable recommended flags for token issuers
  const settings = {
    TransactionType: 'AccountSet',
    Account: issuer.address,
    // Require destination tags (helps identify payments)
    SetFlag: xrpl.AccountSetAsfFlags.asfRequireDestTag,
  }
  await client.submitAndWait(settings, { wallet: issuer })

  // Enable transfer fees (e.g., 0.5%)
  const transferFee = {
    TransactionType: 'AccountSet',
    Account: issuer.address,
    TransferRate: 1005000000, // 0.5% fee (1 billion = 0%, add basis points)
  }
  await client.submitAndWait(transferFee, { wallet: issuer })

  // Enable Default Ripple (REQUIRED for token issuers)
  const ripple = {
    TransactionType: 'AccountSet',
    Account: issuer.address,
    SetFlag: xrpl.AccountSetAsfFlags.asfDefaultRipple,
  }
  await client.submitAndWait(ripple, { wallet: issuer })

  console.log('✅ Issuer configured:', issuer.address)
  await client.disconnect()
  return issuer
}
```

### Creating a DEX Offer

```javascript
async function createDexOffer(issuer, currency, priceInXRP) {
  // Create a sell offer on XRPL's built-in DEX
  const offer = {
    TransactionType: 'OfferCreate',
    Account: issuer.address,
    TakerGets: {
      currency: currency,
      issuer: issuer.address,
      value: '1000', // Selling 1000 tokens
    },
    TakerPays: xrpl.xrpToDrops(priceInXRP * 1000), // For X XRP
  }
  // This lists your token for sale on the DEX immediately
}
```

---

## Lesson 4.3: Batch Distribution (Airdrops)

### Using TokenForge Pro
1. Upload a CSV: `wallet_address, amount`
2. TokenForge batches transactions (50 per ledger close)
3. Real-time progress tracking
4. Failed transactions automatically retry

### Using Code

```javascript
async function airdrop(issuer, currency, recipients) {
  // recipients = [{ address: 'rXXX...', amount: '100' }, ...]
  
  for (const recipient of recipients) {
    try {
      const payment = {
        TransactionType: 'Payment',
        Account: issuer.address,
        Destination: recipient.address,
        Amount: {
          currency: currency,
          issuer: issuer.address,
          value: recipient.amount,
        },
      }
      const result = await client.submitAndWait(payment, { wallet: issuer })
      console.log(`✅ Sent ${recipient.amount} to ${recipient.address}`)
    } catch (err) {
      console.log(`❌ Failed: ${recipient.address} — ${err.message}`)
      // Common failure: recipient hasn't set up trust line
    }
  }
}
```

### Important: Trust Lines First!
Recipients MUST create a trust line to your token BEFORE you can send them tokens. This is a feature, not a bug — it prevents spam tokens from appearing in wallets without consent.

**Strategy for distribution:**
1. Announce your token and share the trust line link
2. Wait for recipients to opt in (create trust lines)
3. Then distribute tokens to opted-in wallets

---

## Lesson 4.4: Monitoring Your Token

### XRPL Analytics API
Use xrplanalytics.com to track:
- Total trust lines (adoption metric)
- Token holder distribution
- DEX trading volume
- Transfer activity

### Key Metrics to Track
| Metric | Why It Matters |
|--------|----------------|
| Trust line count | Shows adoption/interest |
| Unique holders | Actual distribution |
| DEX volume | Liquidity health |
| Transfer count | Usage activity |
| Top holders % | Concentration risk |

---

## Action Items
1. Create a testnet token using TokenForge or code
2. Set up a trust line from a second wallet
3. Send tokens between wallets
4. Create a DEX offer for your token
5. Check your token on the testnet explorer

---

*Next: Module 5 — Legal & Compliance*
