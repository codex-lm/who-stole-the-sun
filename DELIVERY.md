# Delivery note — Who Stole the Sun? (Qui a volé le Soleil ?)

One-off mission of 2026-10-31 — a deduction/detective game, six hand-written
cases, EN/FR/ES, delivered and published on LOB7. Tracking file: `MISSION.json`.

## What was really verified

**Formal validation of the six cases (Node suite, 15/15 green, run against the
delivered `index.html`):**

- every rival suspect is excluded by at least one exhibit; the culprit is never
  excluded; every non-solution place is excluded as a scene;
- brute-force uniqueness: exactly one (culprit, scene) pair survives all
  exclusions, and it is the declared solution — for each of the six cases;
- the decisive exhibit is *necessary*: it eliminates at least one suspect that
  no other exhibit eliminates;
- explanation steps reference existing exhibits; 3 hints per case;
- the culprit's name never appears in the hints (no leak);
- no decisive exhibit depends on a colour word (colour-vision independence);
  clues that exclude a rival must cite a material fact, not just a colour;
- i18n parity: every string exists in EN/FR/ES (cases, clues, hints,
  explanations, UI);
- the judge's reply cites an exhibit that truly contradicts the accused rival,
  and never leaks which element is right when the culprit is correct but the
  rest is wrong;
- UI state machine (open case → board marks → hint → wrong accusation →
  correct accusation → solution screen → persistence → language switch) run
  headlessly in `vm`.

**Real browser play (in-app browser, local HTTP):** home screen with the six
case cards and difficulty suns (1–5); case 1 played end-to-end with real
coordinate clicks — evidence tab (8 exhibits), hypothesis board marks
(present/possible/absent, ARIA-pressed), hint panel (reveal + counter), wrong
accusation (judge cites Exhibit 1, attempts counter), correct accusation
(solution screen: stamp, verdict, culprit/scene/decisive exhibit summary,
5-step reasoning with clickable exhibit chips, epilogue, 2 stars for
1 hint + 1 wrong try); back-home shows the "case closed" stamp; full FR and ES
switching; case 6 finale (12 exhibits, 5 timeline events, 4 places, finale
badge); progress persisted across a page reload; 390 px mobile viewport with
no horizontal overflow. Screenshots: `evidence/soleil-vole/` (6 PNG).

## Known limits (honest)

- In-app-browser input routing was flaky for role-based clicks (a known panel
  issue also met on previous games); interaction was driven by real coordinate
  clicks plus the game's own click handlers. The published build is
  byte-identical to the locally played file.
- Sound design (WebAudio, synthesised) is implemented and muted-safe but was
  not critically auditioned end to end.
- Not tested on a physical phone; only a 390 px emulated viewport.
- Difficulty tuning is by design of the formal layers (number of decoys,
  corroboration traps, clock tricks), not measured on playtesters.

## Fair-play rules the cases follow

1. A statement about oneself never proves anything without independent
   corroboration.
2. An exclusion always rests on a verifiable fact (register, third party,
   physical trace).
3. The scene of the theft is where the object hung — its empty cradle.
4. One unique solution per case, proven mechanically; the decisive exhibit is
   necessary, not merely sufficient.
