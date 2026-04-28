---
name: buy-smart
description: >
  Run this skill whenever the user wants to buy something and needs a no-BS evaluation report.
  Triggers on: "should I buy X", "is X worth it", "help me buy X", "comparing X vs Y to buy",
  "I want to buy", "thinking of getting", "is this a good deal", or when user shares a product
  URL, image, or product name with purchase intent. Cuts through tech/product marketing lies,
  imaginary specs, fake benchmarks, and hype to give a clear buy/skip verdict.
---

# Buy Smart Skill

Cut through marketing BS and give a clear buying verdict.

## What You Do

User gives you a product (URL, image, name, or category). You dig, verify, and return a structured no-BS report.

## Step-by-Step

### 1. Identify the Product

- If URL: `web_fetch` the product page
- If image: read visible specs/name from image
- If name only: `web_search` to find the official product page and fetch it
- Extract: product name, price, key marketed specs, category

### 2. Flag Marketing BS (check every one)

Cross-reference the product page claims against this checklist:

**"Up to" claims**
- Any stat starting with "up to" means nothing. Flag it.
- Search for real-world benchmarks: `web_search "{product name} real world benchmark"`

**Imaginary specs**
- Max performance + min price shown together but not achievable together
- Example: best range + lowest price but you can't get both
- Check: does the base model actually deliver the headline number?

**Invented specs**
- Unified Memory vs RAM, Motion Rate vs Hz, ULED/QLED/QNED vs OLED
- Flag any made-up category names designed to avoid direct comparison
- Search: `web_search "{spec name} what does it actually mean"`

**Fake measurements**
- "1-inch sensor" is NOT 1 inch
- "1.5K display" is NOT 1500 pixels
- Peak nits ≠ typical brightness. Always find typical/sustained brightness
- Search: `web_search "{product} typical brightness nits"` or `"{product} sustained brightness"`

**Old comparison trick**
- "X times faster than [old model]" - how old is that model?
- Find gen-to-gen real improvement: `web_search "{product} vs previous gen real world"`
- Flag if comparison is 3+ years old

**Software features sold as hardware upgrades**
- Is this feature also on older phones/devices via update?
- Is this feature also on competitors?
- Search: `web_search "{feature name} which devices supported"`

**Efficiency trap**
- "+X% performance AND +X% efficiency" = you don't get both at the same time
- Flag when both are claimed together without clarification

**Materials fluff**
- "Aerospace aluminum" = standard 6000/7000 series (used in scooters too)
- "Surgical grade stainless steel" = 316L (also used in kitchen sinks)
- Note it, don't let it impress you

**Thickness/thinness claims**
- "Thinnest ever" at the thinnest point only
- Find actual max thickness including camera bump
- Search: `web_search "{product} thickness with camera bump mm"`

**Zoom megapixel camera traps**
- High max zoom = meaningless. Find optical zoom only
- High megapixels ≠ better photos. Find sensor size
- Search: `web_search "{product} camera sensor size optical zoom test"`

### 3. Real World Check

Run these searches:

```
web_search "{product} reddit review after 1 month"
web_search "{product} problems complaints issues"
web_search "{product} vs {main competitor} honest review"
web_search "{product} price history"
```

Pull:
- Common complaints from real owners
- How it compares to main competitor at same price
- Is this actually a good deal or is price inflated/on fake sale

### 4. Who Is This Actually For

Based on everything found, define:
- **Best fit user**: who actually benefits from this product
- **Bad fit user**: who should avoid it
- **Use case match**: does it fit what the user said they need

### 5. Output: The Report

Format exactly like this:

---

## 🛒 Buy Smart Report: [Product Name]

**Price:** [price] | **Category:** [category]

---

### ⚠️ Marketing BS Detected

| Claim | What They Said | Reality |
|-------|---------------|---------|
| [claim] | [their words] | [actual truth] |

(Only include rows where BS was found. Skip clean claims.)

---

### 📊 Real Specs That Matter

- **[Spec]:** [actual value with source]
- **[Spec]:** [actual value with source]

(Focus on specs that matter for this product category. Drop the fluff.)

---

### 💬 What Real Owners Say

- [Key finding from Reddit/forums - positive]
- [Key finding from Reddit/forums - negative]
- [Most common complaint]

---

### 🆚 vs Main Competitor at Same Price

**[Competitor]** at ~[price]:
- Wins: [where competitor is better]
- Loses: [where this product is better]

---

### 👤 Who Should Buy This

✅ Buy if: [specific profile]
❌ Skip if: [specific profile]

---

### 💰 Deal Check

- Price history: [normal price vs current]
- Verdict: [Good deal / Wait for sale / Overpriced]

---

### 🏁 Final Verdict

**[BUY / SKIP / WAIT]**

[2-3 sentences. Direct. No fluff. Say exactly why.]

---

## Notes

- Never take "up to" numbers at face value
- Always find gen-to-gen comparison, not 3+ year old model comparison
- Typical brightness > peak brightness
- Sensor size > megapixels
- Optical zoom > max digital zoom
- If competitor data not found, say so - don't guess
- If price history not found, say so
- Keep the whole report under 600 words
- Use simple English throughout
