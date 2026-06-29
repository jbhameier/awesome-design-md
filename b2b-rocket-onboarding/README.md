# B2B Rocket — Mobile Onboarding Journey

A simulated, mobile-first onboarding walkthrough for **B2B Rocket's** V1 Automated Onboarding. Apple-style glassmorphism (frosted surfaces, blur, floating depth, an animated aurora) rendered in B2B Rocket brand colors.

> **Simulated demo.** Every action is mocked client-side — no real OAuth, uploads, ordering, or sending. Built for a staging walkthrough.

## Open it

It's a single self-contained file — no build, no dependencies.

- **On your phone:** open the published link, or AirDrop / send yourself `index.html` and open it in Safari (the `-apple-system` font renders as real SF Pro).
- **On desktop:** just open `index.html` in any browser — it previews inside a phone bezel.

## The journey (9 screens)

1. **Welcome** — what the setup covers.
2. **Business** — website + repeatable product/service cards (name & description required, link optional) + optional doc uploads.
3. **Domains & mailboxes** — primary/forwarding domain, domain & mailbox steppers, auto-generated editable mailbox list with distribution.
4. **Connect** — primary inbox (Google/Microsoft) + LinkedIn accounts.
5. **InboxKit** — auto-selected domains + order summary, simulated order placement.
6. **AI Research** — staged "researching → human review" animation, then editable Knowledge Center docs.
7. **ICP** — AI-drafted Ideal Customer Profile to review/edit, saved to the Knowledge Center.
8. **Campaigns** — 4 editable campaigns; confirm each, then launch (spintax + defaults + mailbox attach applied on launch, live post-warmup).
9. **Done** — completion summary + warmup→launch timeline.

## Customizing the brand

All colors are CSS variables in the `:root` block at the top of `index.html`. To drop in B2B Rocket's exact brand hex, edit `--brand`, `--glow`, and `--accent` in one place.
