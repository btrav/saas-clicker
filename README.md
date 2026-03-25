<div align="center">

```
  ╔══════════════════════════════════════════════╗
  ║  COMPANY   Stripclub          STAGE   Seed   ║
  ║  MRR       $142,800           BURN    $31k   ║
  ║  USERS     48,293             CHURN   2.1%   ║
  ║  RUNWAY    4.6 mo             EQUITY  18%    ║
  ╚══════════════════════════════════════════════╝
                 [ ACQUIRE USER ]   +47/click
```

# SAAS CLICKER

**Build · Grow · Exit · Repeat**

![No Dependencies](https://img.shields.io/badge/dependencies-none-22c55e?style=for-the-badge)
![Single File](https://img.shields.io/badge/bundle%20size-1%20file-6366f1?style=for-the-badge)
![Vanilla JS](https://img.shields.io/badge/vanilla-js-eab308?style=for-the-badge)
![License: MIT](https://img.shields.io/badge/license-MIT-94a3b8?style=for-the-badge)

</div>

---

A clicker game that judges you.

You're a founder. Pick a name — maybe **Confusence**, maybe **Stripclub**, maybe **DocuSigh** — acquire your first users, watch churn eat into MRR, and decide whether to take a VC term sheet or stay equity-free. Bootstrap your way to acquisition or ride the funding treadmill all the way to IPO. Either way, there's a prestige bonus waiting on the other side.

> *Acquiring users costs nothing. Enterprise plans are $500/mo. This is both a game mechanic and an accurate description of the SaaS industry.*

---

## THE CHOICE

The game doesn't ask you which path you want. It shows you a term sheet.

**Accept it** → you're on the VC track. Pre-Seed through Series B, then IPO. Dilution compounds. Investor expectations compound faster.

**Decline it** → you stay bootstrapped. The acquisition offer comes when you hit the MRR threshold, equity-free. Costs more runway. Ends on your terms.

```
  Pre-Seed ──► Seed ──► Series A ──► Series B ──► IPO
                                                    ↑
                                             you are here
                                          (please wake up)
```

Three IPOs unlocks the **Hall of Fame**. Three bootstrap exits unlocks the **Newsletter Ending**. Both have endings that will make you screenshot and send them to someone.

---

## COMPANIES

A new name is randomly assigned each run. Here are a few:

| Company | Tagline |
|---|---|
| **Stripclub** | We take a small cut. Of everything. Forever. |
| **DocuSigh** | Legally binding regret, delivered as a service. |
| **Confusence** | A wiki graveyard where documentation goes to die. |
| **JirAAAA** | Sprint planning for teams allergic to sprinting. |
| **Salesfarce** | A CRM you'll customize for six months and abandon. |
| **Flack** | A messaging app for teams who miss having inboxes. |
| **Zoombomb** | Video calls with the energy of a dentist appointment. |
| **Slop** | AI-generated content at scale. For brands. |

*25 total. Finding all of them is part of the game.*

---

## CAN YOU LOSE

Yes. Run out of cash and your company dies.

```
  The servers are dark.
  The Slack is quiet.
  Somewhere, a VC updates their portfolio page.
  Your domain expires in 14 days.
```

Progress does not save between sessions. Closing the tab wipes the run.

This is a feature.

---

## DIGNITY

Some upgrades have a dignity cost.

```
  Cold Email Blast         $500    💔 2 dignity
  Post to Social Every Day  free   💔 1 dignity
```

There is no dignity stat. It doesn't do anything mechanically.

It just sits there.

---

## HOW TO PLAY

```bash
git clone https://github.com/btrav/saas-clicker.git && open index.html
```

No build step. No `npm install`. No dependencies. Drop `index.html` into a browser tab and start burning runway.

---

## MECHANICS

<details>
<summary>Full game mechanics</summary>

<br>

**Core loop**

Click to acquire users → free users convert to paying customers over time → MRR = paying users × ARPU → MRR covers burn rate → positive cash flow → unlock upgrades → repeat at scale

**Stats modeled**

- MRR, ARR, ARPU
- Burn rate & runway
- Monthly churn rate
- Free-to-paid conversion rate
- Investor equity %

**Upgrade paths**

30+ upgrades across bootstrap and VC tracks. Hire a Head of Growth, launch a referral program, unlock a Pro plan, acquire a competitor's users, or buy a Sketchy Mailing List (💔 3 dignity). Path diverges meaningfully after seed stage.

**Random events**

Viral moments, influencer dunks, support crises, product launches. Events fire on a timer and modify your metrics temporarily. Not all of them are good. The sketchy mailing list one is never good.

**Funding rounds**

Pre-Seed → Seed → Series A → Series B, each gated by user count and MRR thresholds. Each round deposits cash and dilutes equity. The dilution stacks.

**Prestige system**

Completing a run (IPO or acquisition) adds permanent bonuses to every future run: revenue multiplier, click multiplier, conversion rate bonus. VC and bootstrap paths award different bonuses, so the meta-game rewards trying both.

</details>

---

## ENDINGS

**3× Bootstrap exits → Newsletter Ending**

You get a randomized newsletter name (*"Cap Table of One"*, *"Default Alive, Actually"*, *"The Ramen Billionaire"*), a personalized roast, and a scenario for what you did with your life after:

> *You buy eleven alpacas. They are difficult and expensive and occasionally aggressive. You love them in a way you cannot explain to anyone who has not owned alpacas.*

**3× IPOs → Hall of Fame**

You are, by any reasonable definition, a problem. Possible outcomes include:

> *You moved to Austin. You tell people about Austin.*

> *You bought a boat. The boat has structural issues. The boat is the first thing in ten years you cannot iterate on. The boat is winning.*

---

## TECHNICAL

Single `index.html`. ~47KB. Zero dependencies. Pure vanilla JS. 10-tick/sec game loop. Runs in any modern browser.

```
saas-clicker/
└── index.html     ← the whole game
```

---

<div align="center">

*Made by [btrav](https://github.com/btrav)*

</div>
