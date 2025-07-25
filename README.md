#  Wallet Risk Scoring (No API / From Scratch)

Project calculates the risk score of Ethereum wallet addresses according to their structure — **without relying on APIs or transaction information**. It applies heuristic analysis such as entropy, hex variety, and pattern identification to indicate suspicious-looking wallets.

---

##Project Overview

As input, a CSV file of wallet addresses, the pipeline:
1. Loads addresses with pandas.
2. Calculates structural features:
- **Entropy**: randomness of characters.
- **Hex Diversity**: number of unique characters.
- **Suspicious Patterns**: such as repeated 0s or Fs.
3. Normalizes the features.
4. Computes a final **risk score (0–1000)**.
5. Outputs a `wallet_risk_scores.csv` with `wallet_id` and `score`.



##  Input Format

- A CSV file named `wallet.csv` with a single column:
```csv
wallet_id
0xabc123.
0x456def.
.
```.
## Feature Logic
Feature	Description
entropy	Shannon entropy of address characters (higher = safer)
diversity	Unique hex characters used (more diversity = better)
is_suspicious	1 if suspicious pattern found (e.g., all 0s/Fs, repeating)

## Scoring Method

Entropy → 50% weight
Diversity → 40% weight
Suspicious Pattern → -90% penalty
Final score normalized and scaled to 0–1000.

## Output
A CSV file: wallet_risk_scores.csv
