# UI prototypes

Two interactive prototypes designed for the admin screens of a commission and remuneration system for financial advisors. Both were built as hand-off artefacts: a developer can open them, click through every state, and read the data rules the screens enforce.

Everything runs in the browser from a single HTML file. There is no build step and no server. Data is demo data and is saved in your browser only (use **Reset demo data** in the Help dialog to start over).

| Prototype | What it shows |
| --- | --- |
| [`classes-types.html`](classes-types.html) | Classes and types for revenue, cost, expense and commission, with a hierarchy table and a side drawer editor. |
| [`commission-policy-rules.html`](commission-policy-rules.html) | Commission policies built rule-first: a rule maps a rate to a class or type, with optional tiered rates driven by accrued revenue pools. |

When this repo is served with GitHub Pages, they open at:

- `/prototypes/classes-types.html`
- `/prototypes/commission-policy-rules.html`

## Design problem

The setup screens are used by people who are not highly technical, but the data behind them has strict rules: which rule wins, how tiers join up, which pool feeds a tier. The aim was to make the screens simple to use while still enforcing those rules, and to show a developer exactly how each action is stored.

## Decisions worth noting

- **Start from the rule.** A policy begins empty with one clear first step ("Start with the first rule"), instead of asking for a default rate and policy settings up front.
- **Tiers as plain bands.** Tiers are entered as From, Up to and Rate. From is filled in for the user, the last tier is open-ended, and the editor prevents gaps and overlaps.
- **Rules enforced on the screen.** The deepest matching rule wins, a rule sits under at most one parent, rates are range-checked for their type (percentage, basis points or flat), and a pool cannot be taken out of use while an active tiered rule depends on it.
- **A developer layer that stays out of the way.** Each rule has a collapsible "For developers" block showing the table columns it writes and the tier seeding value (`lower:upper:rate; …`).
- **Open questions are listed, not hidden.** The Help dialog ends with the points the business still needs to confirm, such as whether tiers apply to the whole event or in slices.
- **Readable and responsive.** Labelled controls, text contrast of at least 4.5:1 in light and dark mode, and layouts checked from 375px to 1440px.

## How it was checked

The policies prototype was tested end to end in a real browser (Playwright, Chromium): rule and tier editing, validation, accrued revenue pool management and saving, plus responsive and contrast checks in light and dark mode.

Designed by Belinda Kennedy, [Inzicht Analytics](https://github.com/Inzicht-Analytics).
