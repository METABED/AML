# AML Operations — interactive monitoring prototype

A standalone educational HTML application explaining transaction monitoring, alert thresholds, review capacity, risk management, and synthetic transaction data. Built for a **four-minute landscape touchscreen presentation**.

## Open it

Open `index.html` in a modern browser. No server, login, internet access, external libraries, or subscription is required. For publication, upload `index.html` to a public static hosting service such as GitHub Pages.

## Sections

1. **Overview** — A synthetic example transaction moves through five clickable AML monitoring stages. Select **Indicators** to see its live 0–100 score components.
2. **Threshold Analysis** — Choose a preset *first*, or adjust the monitoring threshold and analyst capacity using sliders. The output metrics, chart, and risk register recalculate automatically.
3. **Risk Register** — Four illustrative risk scores and associated owners and actions respond to the current scenario.
4. **Dataset** — Search or filter by reference label, download all active records as a CSV file, or import compatible CSV records.

The sidebar provides a **full reset** control, which restores the default 500-record synthetic dataset, threshold 55, capacity 45, baseline preset, first workflow stage, and Overview. Theme selection is preserved. The theme button switches the *entire application* between light and dark mode.

## Data model

The default dataset contains 500 reproducible, locally generated synthetic records. For each transaction, five binary indicators contribute weighted points:

| Indicator | Points |
|---|---:|
| High-risk geography | 22 |
| Unusual amount | 13 |
| Rapid transaction velocity | 25 |
| New beneficiary | 12 |
| Behavioural deviation | 28 |

The sum is a score from 0 to 100. A transaction **generates an alert if its score is greater than or equal to the selected threshold**. `reference_label` is a synthetic ground-truth label used to assess false positives and missed suspicious transactions; it is not visible to the simulated monitoring engine. Alert review backlog equals `max(0, alerts - analyst capacity)` for the current cycle.

The weights, indicator probabilities, and risk-register heuristics are **illustrative**, not calibrated from real AML banking data. Adjusting thresholds does not automatically close cases; flagged records are routed to a human FCI review step.

## CSV schema

`transaction_id,date,amount_jod,country_code,high_risk_country,unusual_amount,rapid_velocity,new_beneficiary,profile_deviation,score,reference_label`

Indicator fields must be 0 or 1; labels must be `Suspicious` or `Not suspicious`. Imported `score` values are recalculated from the five indicators so the simulation cannot disagree with the dataset. Import limit: 20,000 records. Export always downloads the **entire active dataset**, not only filtered rows.

You can filter labels using the dedicated dropdown, or type `suspicious` / `not suspicious` in the search field.

## Publish with GitHub Pages

1. Create a public GitHub repository (e.g. `aml-operations`).
2. Upload `index.html` to the repository root and commit it.
3. Under **Settings → Pages**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, and save.
4. Open the GitHub Pages URL after deployment. (The public hosting URL is not created by this local package.)

## Suggested four-minute route

- **0:00–0:55**: Overview — show the sample record and tap Intake, Indicators, Threshold, and FCI Queue.
- **0:55–2:40**: Threshold Analysis — switch from Baseline to Detection first and Efficiency first; point out the trade-offs in alerts, false positives, missed suspicious records, and backlog.
- **2:40–3:25**: Risk Register — connect the outcomes to governance decisions and owners.
- **3:25–4:00**: Dataset — filter suspicious labels and demonstrate the CSV download.

**Terminology:** The software is a *digital-twin-inspired operational simulation prototype*, not a live-connected digital twin of any banking platform. All inputs and outcomes are synthetic. There are no connections to real bank systems.
