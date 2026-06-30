# B2B Rocket — Mobile Onboarding Journey

A simulated, mobile-first onboarding walkthrough for **B2B Rocket's** V1 Automated Onboarding. Apple-style glassmorphism (frosted surfaces, blur, floating depth, an animated aurora) rendered in B2B Rocket brand colors.

> **Simulated demo.** Every action is mocked client-side — no real OAuth, uploads, ordering, or sending. Built for a staging walkthrough.

## Open it

It's a single self-contained file — no build, no dependencies.

- **On your phone:** open the published link, or AirDrop / send yourself `index.html` and open it in Safari (the `-apple-system` font renders as real SF Pro).
- **On desktop:** just open `index.html` in any browser — it previews inside a phone bezel.

## The journey (10 screens)

1. **Welcome** — what the setup covers.
2. **Products & Services** — website + repeatable product/service cards (name & description required, link optional) + optional doc uploads.
3. **Domains & mailboxes** — primary/forwarding domain, a sending-volume tier (required, nothing preselected), and senders (≥1 with first & last name required) with auto-balancing volume split.
4. **Infrastructure** — auto-selected domains + order summary, simulated provisioning.
5. **Connect** — primary inbox (Google/Microsoft) + LinkedIn accounts. Fully optional — add now or later, with an iOS-style provider chooser and add/remove.
6. **Invite team** — optional teammate invites (work email + role).
7. **AI Research** — staged "researching → human review" animation, then editable Knowledge Center docs.
8. **ICP** — AI-drafted Ideal Customer Profile to review/edit, saved to the Knowledge Center.
9. **Campaigns** — 1 LinkedIn campaign + 3 email campaigns as swipeable carousels; approve each, then launch (spintax + defaults + mailbox attach applied on launch, live post-warmup).
10. **Done** — completion summary + an expanded warmup→launch timeline.

## Customizing the brand

All colors are CSS variables in the `:root` block at the top of `index.html`. To drop in B2B Rocket's exact brand hex, edit `--brand`, `--glow`, and `--accent` in one place.
