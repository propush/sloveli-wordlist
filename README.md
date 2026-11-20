# Sloveli word list

A graded vocabulary of about 6,000 meanings in **English, Russian and Serbian** (Serbian in
Cyrillic, Ekavian), levelled A1–C2 on the CEFR scale, for flashcard learning in any direction
between the three languages. It is the library of the Sloveli app, published as open data.

- `library_v3.json`: the word list.
- `reports/`: the review report, per language and level: how every term was decided, every
  adjudication with its reason, every collision and every quarantined term, plus the automated
  audit's error rates. Start with `reports/README.md`.
- `LICENSE`: CC BY-SA 4.0. `ATTRIBUTION.md`: the sources and how to credit them.
- `CHANGELOG.md`: what changed in each release.

## Format

`library_v3.json` is one JSON object:

- `version` (3), `generated_at` (date), `models` (which model did which step),
  `shared_terms` (language → terms that several meanings share on purpose, checked homonyms).
- `entries`: one per meaning, in the order a learner meets them:
  - `key`: a stable id (`water_n`, `light_adj_not_heavy`); keys are never renamed.
  - `pos`: noun, verb, adjective, adverb, pronoun, numeral or interjection.
  - `topic`: one of a fixed list (food_drink, city_transport, ...).
  - `level`: the meaning's CEFR level, `A1` to `C2`.
  - `rank`: the order within the list (by level, then English frequency, with parts of speech
    and topics interleaved).
  - `sense_note_en`: a few English words that identify the meaning.
  - `terms`: `en`, `ru` and `sr`, each with:
    - `term`: the word (Russian and Serbian lowercase; Russian with ё; verbs in Russian and
      Serbian as the imperfective infinitive);
    - `note` (optional): grammar a learner can't guess, as `label: value` items joined by
      `; `: `g` the gender (`m`, `f`, `n`, or `pl` for a plural-only noun) where the ending
      doesn't show it, `pl` an irregular plural, `pf` the perfective partner of a verb,
      `past` the past tense and past participle of an irregular English verb;
    - `sense_note` (optional): a short gloss in that language, given where several meanings
      share the term, so a learner can tell them apart, and where the term is narrower than
      the English headword (Russian свекровь, «мать мужа», for mother-in-law); an entry has
      sense notes in every shown language or in none;
    - `level` (optional): a per-language level, at most one step from the meaning's, set when
      the word is clearly rarer or more basic in that language;
    - `status`: `ok`, `collision` or `quarantined` (below);
    - `audit`: how the term was decided (the models that agreed, the adjudicator's verdict and
      reason, the checks), for review.

## Levels

One level per meaning, from the English sources: CEFR-J 1.5 for A1–B2 and the Octanove
Vocabulary Profile 1.0 for C1–C2. A CEFR level describes how basic a meaning is, so "water" is
A1 in every language; a per-language `level` adjusts it by one step where needed. Within A1–B2, some
meanings that didn't fit their level's target size moved up one level. Every B2–C2 meaning was also checked as
learner vocabulary: rare or odd senses of a headword (a noun used as a verb in a narrow way,
such as man "to staff a post") and duplicates of another part of speech were left out.

## Statuses

- `ok`: a word to learn in this language.
- `collision`: a correct translation, but another meaning has the same word in this language
  (big and large are both большой). It is shown to native speakers of the language as the
  translation, but only one of the meanings is offered to learners of it.
- `quarantined`: the term failed verification. It is kept, with its reasons, for a later fix,
  and is never shown: the meaning isn't offered between this language and any other, neither
  as a word to learn nor as a translation.

## How to cite

> Sloveli word list (version 3). https://github.com/propush/sloveli-wordlist. Licensed under
> CC BY-SA 4.0. Based on the CEFR-J Wordlist 1.5 (Yukio Tono, TUFS), the Octanove Vocabulary
> Profile C1/C2 1.0 (Octanove Labs), wordfreq (Robyn Speer) and Wiktionary (via kaikki.org).

Keep the attributions in `ATTRIBUTION.md` when you reuse the data.
