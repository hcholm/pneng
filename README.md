# Pneŋ

[Overview](README.md) | [Orthography](pneng-orthography.md) | [Grammar](pneng-grammar.md) | [Lexicon](pneng-lexicon.md) | [Examples](pneng-examples.md) | [Sample Text](pneng-sample-text.md)

Pneŋ is a parser-first analytic conlang designed to be easy to read, easy to parse, and powerful enough for real narrative and technical writing.

If you like language design, formal grammar, computational linguistics, or just learning unusual systems, Pneŋ is built to meet you where you are:

- Plain enough for curious beginners.
- Rigorous enough for conlangers and linguists.
- Deterministic enough for parser and tooling work.

## Why Pneŋ Exists

Most natural-language-inspired conlangs optimize for culture, aesthetics, or diachrony. Pneŋ instead starts with a different design target:

1. Deterministic parsing in a strict left-to-right pass.
2. Minimal ambiguity from morphology or movement.
3. Expressive syntax without inflectional complexity.

The result is a language where surface order carries most of the grammatical signal, and where structure can usually be recovered in a single left-to-right pass with bounded lookahead.

## At a Glance

- Core finite order: **VOS** (Verb–Object–Subject).
- Direct object marker: **`ta`**.
- Adverb block position: directly after the verb group.
- Clause linking: conjunctions and subordinators are **prefix operators**.
- Relative structures: **`ðæt`-first** with resumptives.
- Morphology: analytic; no inflectional agreement or case endings.
- Pronouns: invariant; role follows position.

## What It Feels Like

A simple declarative transitive clause:

`sī klīrli ta ðe kar šī`

Gloss:

- `sī` = see
- `klīrli` = clearly
- `ta ðe kar` = OBJ the car
- `šī` = she (subject)

English: "She clearly sees the car."

A coordinated sentence with prefix conjunction:

`ænd rid slowli ta ðe bük aj rajt kalmli ta æ nōt aj`

English: "I slowly read the book and calmly write a note."

Even in longer structures, clause boundaries and argument roles stay visible in linear order.

## Who This Project Is For

### General language learners

You can treat Pneŋ as an easy-entry constructed language with transparent sentence structure and relatively low memorization overhead.

### Conlangers

You get a constrained but expressive design space focused on syntax, valency, compositionality, and clarity of form-function mapping.

### Linguists and grammar nerds

You get explicit distributional constraints, EBNF, valency classes, and attachment-control strategies designed to reduce parse ambiguity.

### Tooling and NLP hobbyists

Pneŋ is friendly for deterministic parsers, grammar checkers, linters, and learning-oriented syntax visualizers.

## Design Principles

1. **Parser-first:** grammar should be machine-friendly and human-auditable.
2. **One pass where possible:** avoid constructions that force retrospective reinterpretation.
3. **Stable signaling:** key grammatical relations should be overt and local.
4. **Low morphology, high syntax:** rely on particles and position instead of inflection.
5. **Orthographic discipline:** avoid noisy or opaque spelling conventions.

## Core Grammar Snapshot

### 1. Clause skeleton

Canonical finite clause:

`[VerbGroup] [AdvP*] [(ta ObjNP)] [SubjNP] [CoreComp*]`

This single template carries most clause types.

### 2. Verb group

`(Modal)* (di)? (Aspect)* (not)? V`

- Modals: `wil`, `kan`, `möst`, `šöd`, `wud`
- Past: `di`
- Aspect: `iŋ`, `dän`, `jus`, `kon`
- Negation: `not`

### 3. Valency

- `I`: intransitive
- `T`: transitive (`ta` object required)
- `A`: ambitransitive (either frame)
- `D`: ditransitive (theme via `ta`, recipient oblique)

### 4. Questions

- Clause-initial `ke` marks both polar and content questions.
- Wh-forms occupy regular argument/adjunct positions.

### 5. Clause linking

Prefix strategy:

- Coordination: `CONJ clause-A clause-B`
- Subordination: `SUBCONJ clause-A clause-B`

This keeps the relationship known before either clause fully unfolds.

### 6. Relative structures

Relative phrases are introduced by `ðæt` and include resumptive pronouns inside the relative clause before the head noun appears.

## Orthography and Phonemic Policy

Pneŋ orthography is intentionally constrained:

- No `q`, `c`, or `x` in lexical forms.
- No consonant doubling.
- Distinct graphemes for key contrasts (`þ` vs `ð`, `š` vs `ž`, `č` vs `ǰ`, `ŋ`).
- Productive transliteration rules for English-source vocabulary.

See full details in `pneng-orthography.md`.

## Learn Pneŋ in 15 Minutes

1. Learn pronouns and particles (`ta`, `ke`, `du`, `let`, `hop`, `not`).
2. Learn the VOS clause shape.
3. Practice adverb placement (after verb, before object marker or subject).
4. Practice transitive vs intransitive minimal pairs.
5. Add coordination and subordination with prefix linkers.

Recommended progression:

1. Read `pneng-orthography.md`.
2. Read `pneng-grammar.md` sections 1–6.
3. Skim `pneng-lexicon.md` valency tags.
4. Drill with `pneng-examples.md`.
5. Read `pneng-sample-text.md` with parse notes.

## Documentation Map

- `pneng-orthography.md`: spelling and phoneme-grapheme rules.
- `pneng-grammar.md`: grammar, constraints, and EBNF.
- `pneng-lexicon.md`: lexicon with valency tags and notes.
- `pneng-examples.md`: curated sentence patterns.
- `pneng-sample-text.md`: connected narrative with commentary.

## For Conlangers and Linguists

### Typological profile (intentional)

- Strongly analytic.
- Head-initial clause with overt object marking.
- Strict linearization for parser stability.
- Reduced reliance on agreement and case morphology.

### Ambiguity control strategy

Pneŋ handles frequent ambiguity points explicitly:

- `ta` disambiguates transitivity at the first possible point.
- Adverb block position constrains PP attachment.
- Prefix conjunctions and subordinators avoid late clause-link surprises.
- Relative `ðæt` + resumptive system prevents gap-search uncertainty.

### Computationally useful properties

- Limited reorderings.
- Overt argument signaling.
- Predictable constituent boundaries.
- EBNF-aligned sentence templates.

These properties make Pneŋ suitable for educational parsers and controlled-language experiments.

## Mini Reference

### Pronouns

`aj`, `jū`, `hī`, `šī`, `it`, `wī`, `ðej`

### Core particles

`ta` (object marker), `ke` (question), `du` (imperative), `let` (hortative), `hop` (optative), `not` (negation)

### Common tense/aspect

`di` (past), `wil` (future), `iŋ` (progressive), `dän` (completive/perfect)

### Frequent linkers

`ænd`, `or`, `bät`, `sō`, `if`, `wen`, `bikoz`, `oldou`, `until`

For strict canonical forms and grapheme conventions, follow the dedicated documents.

## Example Workflow for New Content

When writing new Pneŋ text:

1. Draft in canonical clause order.
2. Verify each verb valency (`I/T/A/D`) from the lexicon.
3. Place adverbs immediately after the verb group.
4. Mark every direct object with `ta`.
5. Keep oblique and core complements in licensed positions.
6. Run consistency checks against grammar and orthography docs.

## Current Status

Pneŋ is an actively developed formalized conlang spec with example corpus material. The core syntax and documentation are stable enough for learning, writing, and parser prototyping, while lexical and stylistic expansion remains open.

## Contributing

If you are extending Pneŋ:

- Preserve parser-first constraints.
- Prefer explicitness over stylistic optionality.
- Document every new particle, valency pattern, or distribution rule.
- Add examples for each new grammatical feature.

Suggested contribution types:

- New validated example sets.
- Minimal-pair ambiguity tests.
- Additional narrative or dialogue samples.
- Parser or checker prototypes using the EBNF profile.

## License and Usage

Use Pneŋ for study, creative work, grammar engineering, and tooling experiments. If you redistribute adapted specs, keep source attribution and note your modifications.

