# OpenRouter only takes USDC. Here's how to pay for LLM APIs when you hold USDT

> Maintained by the TeamoRouter team. Option B below is our own gateway; option A doesn't involve us.

OpenRouter accepts crypto, but only **USDC**. If your stablecoins are **USDT**, sitting on TRON, BNB Smart Chain or in an exchange account, you have two ways to pay for Claude, GPT and Gemini API usage:

- **A. Swap USDT to USDC and buy OpenRouter credits.**
- **B. Pay a gateway that takes USDT directly**, such as [TeamoRouter](https://teamorouter.com/?utm_source=github&utm_medium=readme&utm_campaign=b6_openrouter-usdt), and point your SDK or Claude Code at it.

## What OpenRouter accepts

From OpenRouter's FAQ (checked 2026-10-22):

- **Payment methods:** "all major credit cards, AliPay and cryptocurrency payments in USDC". Crypto goes through a Coinbase checkout on the credits page.
- **Crypto fee:** crypto purchases carry an extra fee on top of the usual fee for buying credits. The FAQ and the credits page show the current rate.
- **Refunds:** unused credits can be refunded within 24 hours, but "cryptocurrency payments are never refundable".
- **Model prices:** OpenRouter passes through each provider's list price without markup; you pay the fees when you buy credits.

## Option A: swap USDT to USDC, then pay OpenRouter

1. On your exchange (Binance, OKX, Bybit…), sell USDT for USDC on the USDT/USDC pair.
2. Open OpenRouter's credits page, choose crypto, and check which wallets and networks the Coinbase checkout offers.
3. Move the USDC there on a supported network and complete the payment.

What it costs: the exchange's trading fee, the USDC withdrawal fee, and OpenRouter's crypto fee.

Pick this if you want OpenRouter's large catalog or its routing features.

## Option B: pay with USDT directly (TeamoRouter)

TeamoRouter is an API gateway with one balance for Claude, GPT, Gemini, DeepSeek, Grok and 60+ other models. Top-ups accept USDT, USDC or ETH on a hosted checkout page. You send from your exchange app or any wallet, with no browser extension, and it works on a phone.

1. Sign up at [teamorouter.com](https://teamorouter.com/?utm_source=github&utm_medium=readme&utm_campaign=b6_openrouter-usdt), open the top-up dialog, pick an amount ($5 minimum) and click **Pay with crypto**.
2. On the checkout page choose the coin, then the network. Which networks you see depends on the amount:

   | Amount | Coins and networks |
   |---|---|
   | From $5 | USDT (BEP20), USDC (BEP20), ETH |
   | From $10 | also USDC on Base and USDT on Ethereum (ERC20) |
   | From $30 | also USDT on TRON (TRC20) |

3. Within 60 minutes, send at least the amount shown, on that same network, to the address on the page. The balance is credited automatically after confirmation.

Withdrawal fees are your exchange's. Binance, for example, charges about 0.01 USDT to withdraw on BEP20 and about 1.5 USDT on TRC20, so BEP20 is the cheap route for small top-ups. Crypto top-ups are non-refundable here too.

Step-by-step with error fixes: [How to pay for the Claude API with USDT](https://teamorouter.com/blogs/pay-claude-with-usdt?utm_source=github&utm_medium=readme&utm_campaign=b6_openrouter-usdt).

### Switch your code from OpenRouter

OpenAI-compatible (Python):

```python
from openai import OpenAI

client = OpenAI(
    api_key="sk-teamo-xxxxxx",                 # instead of your OpenRouter key
    base_url="https://api.teamorouter.com/v1",  # instead of https://openrouter.ai/api/v1
)

resp = client.chat.completions.create(
    model="gpt-6-sol",  # model IDs have no vendor prefix; list them with GET /v1/models
    messages=[{"role": "user", "content": "Hello"}],
)
print(resp.choices[0].message.content)
```

Claude Code, on the native Anthropic protocol:

```bash
export ANTHROPIC_BASE_URL=https://api.teamorouter.com
export ANTHROPIC_AUTH_TOKEN="sk-teamo-xxxxxx"
export ANTHROPIC_MODEL=claude-opus-5-5
```

List the model IDs your key can use:

```bash
curl https://api.teamorouter.com/v1/models -H "Authorization: Bearer sk-teamo-xxxxxx"
```

Full reference: [API integration docs](https://teamorouter.com/docs/api-integration?utm_source=github&utm_medium=readme&utm_campaign=b6_openrouter-usdt).

## Side by side

| | OpenRouter | TeamoRouter |
|---|---|---|
| Crypto accepted | USDC | USDT, USDC, ETH |
| How you pay with crypto | Coinbase checkout on the credits page | Checkout page, from any exchange app or wallet |
| Extra fee for crypto | Yes, per its FAQ | No |
| Crypto refunds | Never | Never |
| Model prices | Provider list price, plus fees on credits | Own price list, e.g. Claude Opus 5.5 at $1.108 / $5.54 per million tokens (Anthropic lists $4 / $20) |
| Catalog | Very large, with routing features | 60+ models: Claude, GPT, Gemini, DeepSeek, Grok, Qwen, image models |
| Other payment methods | Cards, AliPay | Cards, Alipay |

TeamoRouter prices are from its [models page](https://teamorouter.com/models?utm_source=github&utm_medium=readme&utm_campaign=b6_openrouter-usdt) on 2026-10-22 and can change.

## FAQ

**Does OpenRouter accept USDT?** No. Its FAQ lists crypto payments in USDC only.

**I only have USDT on TRON and want to top up less than $30.** Withdraw it from your exchange on BEP20 instead. TRC20 opens from $30 on TeamoRouter's checkout.

**No crypto at all?** Both take cards. If your card keeps getting declined, see [paying for Claude when your card is declined](https://teamorouter.com/blogs/claude-card-declined-payment-fixes-2026?utm_source=github&utm_medium=readme&utm_campaign=b6_openrouter-usdt).

## Related guides

- [teamo-lab/pay-openai-api-with-crypto](https://github.com/teamo-lab/pay-openai-api-with-crypto): OpenAI API and Codex without a card
- [teamo-lab/claude-api-usdt](https://github.com/teamo-lab/claude-api-usdt): Claude API with USDT
- [teamo-lab/pagar-claude-con-usdt](https://github.com/teamo-lab/pagar-claude-con-usdt): guía en español

Corrections welcome. Open an issue if something here is out of date.
- [teamo-lab/new-llm-api-releases](https://github.com/teamo-lab/new-llm-api-releases): new model IDs, official prices and code examples on launch day
