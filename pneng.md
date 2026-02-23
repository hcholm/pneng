# Pneŋ

[Overview](pneng.md) | [Orthography](pneng-orthography.md) | [Grammar](pneng-grammar.md) | [Lexicon](pneng-lexicon.md) | [Examples](pneng-examples.md) | [Sample Text](pneng-sample-text.md)

`Pneŋ` is a strictly analytic conlang with parser-first design.

Core rules:

1. Finite clause order is **VOS** (Verb – Object – Subject).
2. No parsing lookahead is ever required.
3. No inflection; all grammar is particle-based.
4. Orthography never uses `q`, `c`, or `x`.
5. Pronouns are invariant (no case morphology); position signals role.

## Design Philosophy

Pneŋ is designed so that a left-to-right parser can determine clause structure at each word without backtracking. The object marker `ta` resolves transitive/intransitive ambiguity immediately. Prefix conjunctions mean a parser knows clause boundaries before reading clauses. Relative phrases are headed by `ðæt` and always precede their head noun.

## Known Homograph Policies

| Form | Readings | Resolution |
|---|---|---|
| `ðæt` | relativizer, subordinator, content-clause marker | distinguished by syntactic position |
| `wen` | wh-word "when", subordinating conj "when" | wh-use only inside `ke`-questions |
| `du` | imperative particle, verb "do" | particle use is always clause-initial |
| `bifor` | preposition, subordinating conjunction | subordinator use introduces a full clause |

## File Index

1. `pneng-orthography.md` — phoneme-to-grapheme rules
2. `pneng-grammar.md` — clause structure, EBNF
3. `pneng-lexicon.md` — vocabulary with valency tags
4. `pneng-examples.md` — annotated example sentences
5. `pneng-sample-text.md` — extended narrative sample

