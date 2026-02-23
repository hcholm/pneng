# Pneŋ Grammar (Parser-Strict v0.6)

[Overview](README.md) | [Orthography](pneng-orthography.md) | [Grammar](pneng-grammar.md) | [Lexicon](pneng-lexicon.md) | [Examples](pneng-examples.md) | [Sample Text](pneng-sample-text.md)

## 1. Core Parsing Constraints

Pneŋ grammar is optimized for deterministic left-to-right parsing with zero lookahead.

Hard rules:

1. Finite clause order is **VOS** (Verb – Object – Subject).
2. Direct objects are marked by `ta` immediately before the object NP.
3. Adverbs and adverbial phrases must immediately follow the verb (before `ta`).
4. Conjunctions and subordinators are **prefix operators**: `CONJ clause-A clause-B`.
5. Relative constructions are `ðæt`-first.
6. Pronouns are invariant; position determines grammatical role.

## 2. Canonical Clause Shape

### 2.1 Finite Clause

```
[VerbGroup] [AdvP*] [(ta ObjNP)] [SubjNP] [CoreComp*]
```

The adverb block (`AdvP*`) always precedes the object marker `ta`. No constituent may intervene between the verb group and the adverb block.

### 2.2 Verb Group

```
(Modal)* (di)? (Aspect)* (not)? V
```

Internal precedence: `modal > di > aspect > not > V`

| Slot | Particles |
|---|---|
| Modal | `wil`, `kan`, `möst`, `šöd` |
| Past | `di` |
| Aspect | `iŋ`, `dän`, `jus`, `kon` |
| Negation | `not` |

## 3. Argument Structure

### 3.1 Intransitive

```
V [AdvP*] SUBJ [CoreComp*]
```

Example: `run fast hī` — "He runs fast."

### 3.2 Transitive

```
V [AdvP*] ta OBJ SUBJ [CoreComp*]
```

Example: `sī klīrli ta æ kar šī` — "She clearly sees a car."

The presence of `ta` signals that the next NP is the direct object. This resolves the transitive/intransitive distinction at first token after the adverb block, with no lookahead.

### 3.3 Ambitransitive

Ambitransitive verbs (`A` tag) permit both frames:

- Intransitive: `opən slowli ðe dōr` — "The door opens slowly."
- Transitive: `opən kareföli ta ðe dōr aj` — "I carefully open the door."

The parser reads `ta` as the unambiguous transitive signal.

### 3.4 Ditransitive

```
V [AdvP*] ta THEME SUBJ (tu RECIPIENT | for RECIPIENT)
```

Example: `giv kindli ta æ bük aj tu šī` — "I kindly give a book to her."

The recipient phrase (`tu`/`for` + NP) follows the subject as a core complement.

## 4. Noun Phrase

```
NP := Pronoun | NBar | RelNP
NBar := (Det)? (Num)? (AdjP*) N
```

### 4.1 Determiners

| Form | Gloss |
|---|---|
| `æ` | indefinite singular |
| `ðe` | definite |
| `ðis` | proximal demonstrative |
| `ðat` | distal demonstrative |

### 4.2 Number

The plural particle `s` occupies the Num slot and precedes the adjective block:

```
ðe s big dōg   "the big dogs"
```

`s` is a free particle, not a suffix. It never attaches orthographically to the noun.

### 4.3 Adjective Phrases

Adjectives and adjective phrases precede the noun:

```
æ veri old man   "a very old man"
```

### 4.4 Post-Nominal Prepositional Phrases

A PP may follow the head noun inside an NBar to express origin, content, material, or other close modification:

```
NBar := (Det)? (Num)? (AdjP*) N (PP*)
```

Example:

```
ðe kraj fram ðe vilij    "the cry from the village"
æ bük about ðe war       "a book about the war"
```

Post-nominal PPs are parsed as part of the NP and do not extend beyond the NP boundary.

## 5. Pronouns

Pneŋ pronouns are **invariant**: the same form is used regardless of whether the pronoun is subject, object, or oblique. Position signals role.

| Form | Gloss |
|---|---|
| `aj` | I / me |
| `jū` | you |
| `hī` | he / him |
| `šī` | she / her |
| `it` | it |
| `wī` | we / us |
| `ðej` | they / them |

Reflexive is marked with `self` appended as a separate particle: `aj self`, `šī self`, etc.

## 6. Adverbs and Adverbial Phrases

Adverbs must immediately follow the verb group. The adverb block ends at `ta` (if transitive) or at the subject NP (if intransitive).

```
sī klīrli ta æ kar šī        ✓  V Adv ta OBJ SUBJ
sī ta æ kar klīrli šī        ✗  adverb displaced
```

### 6.1 Adverb Formation

- Many adverbs are bare forms: `fast`, `hard`, `nau`, `sūn`, `hīr`, `ðer`.
- The suffix `-li` derives manner adverbs from adjectives: `slowli`, `kalmli`, `kareföli`, `direktli`.
- Both classes are syntactically equivalent and occupy the same post-verbal slot.

### 6.2 Adverb vs. Adjective

Bare forms like `fast` and `hard` function as both adjective (pre-nominal) and adverb (post-verbal). The `-li` suffix is not required for all adjectives but is always grammatical as a manner adverb.

### 6.3 PP Placement and Attachment

PPs can occur in two positions within a clause. Their position determines their attachment unambiguously:

**Adverb-block PP (before `ta` or before the subject):**
Attaches to the verb. Expresses scene-setting location, time, or manner.

```
sī sudənli in ðe forest ta ðe fajər šī
```
`in ðe forest` modifies the act of seeing, not the fire and not the subject.

```
wejt kalmli nīr ðe brij hī
```
`nīr ðe brij` modifies `wejt`, not `hī`.

**CoreComp PP (after the subject):**
Attaches to the verb as a directional or locative complement. Used with motion verbs (`gō`, `kəm`, `run`, `wok`) and a limited class of static verbs (`rimejn`, `wejt`, `sit`) where the location is an argument, not an adjunct.

```
gō kalmli tu ðe siti ðej
```
`tu ðe siti` is the destination argument of `gō`, following the subject `ðej`.

**Rule:** If a PP could plausibly modify the subject NP or the object NP, it must not be placed after the subject. Move it into the adverb block or embed it inside the relevant NP.

## 7. Copula `bī`

`bī` is the sole copula. It takes a predicate complement (adjective phrase, noun phrase, or prepositional phrase) in the position following the subject:

```
bī veri tajərd šī      "She is very tired."       (Pred: AdjP)
bī æ tīčər hī          "He is a teacher."         (Pred: NP)
bī in ðe garden ðej    "They are in the garden."  (Pred: PP)
```

`bī` is tagged `I` (intransitive) and never takes a `ta` object.

## 8. Conjunctions and Clause Linking

All conjunctions are prefix operators taking exactly two clause arguments.

### 8.1 Coordination

`CONJ clause-A clause-B`

| Form | Gloss |
|---|---|
| `ænd` | and |
| `or` | or |
| `nor` | nor |
| `bät` | but |
| `yet` | yet |
| `sō` | so |
| `for` | for (causal coord.) |

### 8.2 Subordination

`SUBCONJ clause-A clause-B`

The subordinate clause is always clause-A; the matrix clause is clause-B.

| Form | Gloss |
|---|---|
| `if` | if |
| `unless` | unless |
| `wen` | when (subord.) |
| `whajl` | while |
| `bifor` | before |
| `after` | after |
| `sins` | since |
| `until` | until |
| `bikoz` | because |
| `ðou` | though |
| `oldou` | although |
| `az` | as |
| `wæðer` | whether |

### 8.3 Content Clauses

Content clauses (complements of verbs like `no`, `tel`, `belīv`, `þiŋk`) are introduced by `ðæt` as a subordinator:

```
no ðæt sī sūn ta ðe rōd hī ðej
"They know that he soon sees the road."
```

Here `ðæt` is the complementizer; the embedded clause is `sī sūn ta ðe rōd hī`.

## 9. Relative Constructions

The relativizer `ðæt` is always the first element of a relative NP. The relative clause follows, using a **resumptive pronoun** in the gap position. The head noun follows the entire relative clause:

```
ðæt [relative clause with resumptive] [head NBar]
```

The resumptive pronoun agrees in animacy with the head noun:

| Head type | Resumptive |
|---|---|
| human | `hī`, `šī`, `ðej` (by referent gender/number) |
| non-human | `it` |

Examples:

```
ðæt lajk reeli ta it šī    æ dogg
"a dog that she really likes"

ðæt rid jesterdej ta it aj    ðe bük
"the book that I read yesterday"

ðæt sī klīrli ta hī wī at ðe markit    ðe man
"the man that we clearly see at the market"
```

Note: the resumptive pronoun (`it`, `hī`, etc.) occupies the object slot; its referent is the head noun.

## 10. Sentence Types

### 10.1 Declarative

Plain finite clause:

```
sī klīrli ta æ kar šī
"She clearly sees a car."
```

### 10.2 Polar Question

`ke` precedes an otherwise unchanged finite clause:

```
ke lajk reeli ta jū šī
"Does she really like you?"
```

### 10.3 Content Question (Object)

The wh-word replaces the object NP inside `ta`:

```
ke sī klīrli ta wat šī
"What does she clearly see?"
```

### 10.4 Content Question (Subject)

The wh-word replaces the subject NP. `ke` still precedes the clause:

```
ke sī klīrli ta æ kar hū
"Who clearly sees a car?"
```

### 10.5 Content Question (Oblique)

The wh-word replaces the PP complement:

```
ke gō sūn hī tu wer
"Where does he go soon?"
```

### 10.6 Imperative

`du` precedes a finite clause. The subject is always `jū` and is mandatory (the parser requires a subject NP):

```
du rid klīrli ta ðis bük jū
"Read this book clearly."
```

### 10.7 Prohibitive

`not du` precedes the clause:

```
not du brek sudənli ta ðe glas jū
"Do not suddenly break the glass."
```

### 10.8 Hortative

`let` precedes the clause:

```
let bild nau ta æ nū brij wī
"Let us build a new bridge now."
```

### 10.9 Optative / Wish

`hop` (the particle, distinct from the verb `hop` "hope") precedes the clause. The particle `hop` is always clause-initial and is never followed by `du`:

```
hop rain sūn it
"May it rain soon."
```

## 11. Possessives

Pneŋ has no genitive inflection. Possession is expressed with the particle `ov` (of) as a post-nominal PP, or with a dedicated possessive pronoun series that precedes the noun in the Det slot.

### 11.1 Possessive Pronouns

Possessive pronouns occupy the Det slot and are incompatible with `æ`, `ðe`, `ðis`, `ðat` in the same NP.

| Form | Gloss |
|---|---|
| `maj` | my |
| `jor` | your |
| `hiz` | his |
| `hör` | her |
| `its` | its |
| `aur` | our |
| `ðer` | their |

Example:
```
rid slowli ta maj bük aj
"I read my book slowly."

lajk reeli ta hör dogg šī
"She really likes her dog."
```

### 11.2 Genitive with `ov`

For non-pronominal possessors, use a post-nominal `ov`-PP on the possessed noun:

```
ðe dōr ov ðe hūs
"the door of the house"

ðe plæn ov ðe tīm
"the team's plan"
```

The `ov`-PP is a post-nominal PP inside NBar, following the head noun (see §4.4).

---

## 12. Quantifiers and Indefinite Determiners

These occupy the Det slot. They are incompatible with `æ` but may combine with `ðe` in some uses (see notes).

| Form | Gloss | Notes |
|---|---|---|
| `ol` | all, every | `ol ðe s man` = "all the men" |
| `evri` | every | takes singular NBar |
| `ič` | each | takes singular NBar |
| `sam` | some | indefinite plural or mass |
| `eni` | any | in questions and negatives |
| `nō` | no, none | negative quantifier |
| `meni` | many | takes plural `s` |
| `fū` | few | takes plural `s` |
| `mätš` | much | mass nouns |
| `litəl` | little | mass nouns |

Examples:
```
sī klīrli ta ol ðe s kar šī
"She clearly sees all the cars."

nīd eni help jū
"Do you need any help?"  (in question contexts)

hæv nō tajm aj
"I have no time."

kəm meni pörzən
"Many people came."
```

Note: `nō` as a quantifier is distinct from the interjection "no" (`nō` as an interjection is the same form; context disambiguates).

---

## 13. NP Coordination

NPs, AdjPs, and PPs can be coordinated using the same prefix conjunctions as clauses, but operating at phrase level. The coordinator precedes both conjuncts.

```
ænd [NP-A] [NP-B]          "NP-A and NP-B"
or  [NP-A] [NP-B]          "NP-A or NP-B"
```

Examples:
```
sī klīrli ta ænd ðe man ðe wuman šī
"She clearly sees the man and the woman."

rid slowli ta or ðe bük ðe letər aj
"I slowly read the book or the letter."

wil kəm ænd hī šī
"He and she will come."
```

For subject coordination, the coordinated NP functions as a plural subject and triggers no other agreement (Pneŋ has none). For "neither...nor" at NP level:

```
sī klīrli ta nor ðe man ðe wuman šī
"She clearly sees neither the man nor the woman."
```

---

## 14. Comparatives and Superlatives

### 14.1 Comparatives

Use `mor` (more) or `les` (less) immediately before the adjective, followed by `ðan` (than) introducing the standard of comparison:

```
mor [AdjP] ðan [NP/Clause]
les [AdjP] ðan [NP/Clause]
```

Examples:
```
bī mor tajərd šī ðan hī
"She is more tired than he is."

bī les stroŋ ðe nū brij ðan ðe old brij
"The new bridge is less strong than the old one."
```

Equality comparison uses `az [AdjP] az [NP]`:

```
bī az fast hī az šī
"He is as fast as she is."
```

### 14.2 Superlatives

Use `most` or `līst` immediately before the adjective:

```
bī most tajərd šī in ðe tīm
"She is the most tired in the team."

lajk most ta wij hī
"Which one does he like most?"
```

### 14.3 Comparative Adverbs

The same `mor`/`les`/`most`/`līst` system applies to adverbs:

```
run mor fast hī ðan šī
"He runs faster than she does."
```

---

## 15. Degree Constructions

### 15.1 `tu` … `tu` (too … to)

The particle `tu` (too/excessively) precedes the adjective or adverb. The resulting-infinitive is expressed with `for [SUBJ] tu [V]` (see §16 on infinitivals):

```
bī tu tajərd šī for šī tu wörk
"She is too tired to work."
```

### 15.2 `enäf` (enough)

`enäf` follows the adjective or adverb it modifies. The resulting-infinitive uses the same `for [SUBJ] tu [V]` form:

```
bī stroŋ enäf hī for hī tu lift ta ðe ston hī
"He is strong enough to lift the stone."
```

### 15.3 `sō` … `ðæt` (so … that)

`sō` precedes the adjective; `ðæt` introduces the result clause:

```
bī sō tajərd šī ðæt fol aslīp sudənli šī
"She was so tired that she suddenly fell asleep."
```

---

## 16. Infinitival Complements

Pneŋ uses the particle `tu` before a bare verb to mark an infinitival (non-finite) complement. This `tu` is the same form as the directional preposition but is distinguished by position: it precedes a verb, not an NP.

```
tu [V] ...     infinitival clause
```

### 16.1 Subject-Control (want, try, plan, decide)

The subject of the infinitival is the same as the matrix subject. The infinitival follows the matrix object slot:

```
want tu gō šī tu ðe markit
"She wants to go to the market."

plæn tu bild nau ta æ nū hūs wī
"We plan to build a new house now."
```

### 16.2 Object-Control (ask, tell, help, force)

The subject of the infinitival is the matrix object. The object is marked with `ta`, the infinitival follows:

```
tel klīrli ta jū aj tu gō
"I clearly tell you to go."

æsk kindli ta hī šī tu rimejn
"She kindly asks him to remain."
```

### 16.3 Raising (seem, appear)

Raising verbs take an infinitival complement in which the raised subject surfaces as the matrix subject:

```
sīm tu nō taj šī
"She seems to know a lot."

sīm tu bī veri old ðe brij
"The bridge seems to be very old."
```

### 16.4 Perception Verb Complements (see, hear, watch)

Perception verbs take a bare infinitival complement (no `tu`). The perceived entity is the object (`ta`), and the bare verb follows:

```
sī ta hī aj run
"I saw him run."

hīr ta ðe glas šī brek
"She heard the glass break."

wäč ta ðej wī wörk
"We watched them work."
```

The bare complement is distinguished from a regular object by the presence of a following bare verb rather than a following subject NP or CoreComp.

### 16.5 Infinitival Purpose Clauses

Purpose is expressed with `for [SUBJ] tu [V]`:

```
kəm sūn šī for šī tu help ta wī
"She came early in order to help us."

bild nau ta æ brij wī for ðej tu kros
"We are building a bridge so that they can cross."
```

---

## 17. Passive Voice

Pneŋ forms the passive with the auxiliary `get` followed by a passive participle. The passive participle is formed with the prefix `en-` on the verb stem. The agent, if expressed, is introduced by `baj`.

```
get en[V] [SUBJ] (baj [AGENT])
```

Examples:
```
get enrid ðe bük
"The book was/gets read."

get enbrek ðe glas baj hī
"The glass was broken by him."

get engiv ta šī ðe bük baj ðe tīčər
"The book was given to her by the teacher."
```

Notes:
- The passive subject occupies the normal subject slot.
- The agent PP (`baj [NP]`) is a CoreComp following the subject.
- `get` here is an auxiliary, not the full verb. It takes the tense and aspect particles normally: `di get enrid ðe bük` = "The book was read."
- The `en-` prefix is written solid with the verb stem: `enrid`, `enbrek`, `engiv`.

---

## 18. Existential Sentences

Existential and presentational sentences use the expletive subject `ðer` with `bī`:

```
bī [NP] ðer (PP)
```

The real subject NP follows `ðer` as a CoreComp. A locative PP follows the NP.

Examples:
```
bī æ dogg ðer in ðe gardən
"There is a dog in the garden."

bī s problem ðer wiþ ðe plæn
"There are problems with the plan."

di bī nō wotər ðer in ðe rivər
"There was no water in the river."
```

Note: `ðer` in this use is the expletive particle, identical in form to the locative adverb "there." Disambiguation is by syntax: the locative adverb occupies the adverb block, while the expletive `ðer` occupies the subject slot after the real NP.

---

## 19. Secondary Predicates and Resultatives

A secondary predicate (depictive or resultative) follows all CoreComps as a final AdjP or NP describing the state of the subject or object after the event.

```
[FiniteClause] [CoreComp*] [SecPred]
```

### 19.1 Depictive (subject-oriented)

```
ərajv lejt hī tajərd
"He arrived late, tired."

wörk hard šī hæpi
"She worked hard, happy."
```

### 19.2 Depictive (object-oriented)

```
sī klīrli ta hī šī juŋ
"She clearly saw him as young / saw him when he was young."
```

### 19.3 Resultative

The result state of the object:

```
pejnt kareföli ta ðe wol šī red
"She carefully painted the wall red."

hammer hard ta ðe nejl hī flæt
"He hammered the nail flat."
```

The resultative AdjP is always final. Its attachment (subject vs. object) is resolved by semantics; syntactically both are in the same position.

---

## 20. Scalar Focus Particles

Focus particles modify a single constituent and must immediately precede it.

| Form | Gloss | Notes |
|---|---|---|
| `onli` | only | restricts to one referent |
| `evən` | even | scalar surprise |
| `ōlsō` | also, too | additive |
| `ōlmost` | almost | approximative |
| `ǰəst` | just, merely | minimiser |

Examples:
```
rid onli ta ðis bük aj
"I read only this book."

onli šī ərajv örlī
"Only she arrived early."

evən hī help
"Even he helped."

ōlsō lajk ta it hī
"He also likes it."
```

Focus particles can precede any constituent: a subject NP, an object NP, an adverb, or a PP. Their position immediately before the target constituent is the sole scoping mechanism.

---

## 21. Reciprocals

Reciprocal meaning ("each other") is expressed with the dedicated NP `ič ðe äðər`:

```
sī klīrli ta ič ðe äðər ðej
"They clearly see each other."

help kindli ta ič ðe äðər wī
"We kindly help each other."
```

`ič ðe äðər` occupies the normal object slot and is always marked with `ta`.

---

## 22. Indirect Questions

An embedded question is introduced by `if` (for polar) or the wh-word directly (for content), inside a content clause position. The embedding verb is one that takes indirect questions: `æsk`, `wəndər`, `nō`, `tel`.

### 22.1 Embedded Polar

```
nō if kəm šī ðej
"They don't know whether she will come."

æsk if rejn it šī tu hī
"She asked him whether it was raining."
```

### 22.2 Embedded Content

The wh-word stays in situ, exactly as in direct questions, but without `ke`:

```
nō wer gō šī ðej
"They don't know where she went."

tel frankli wat sī klīrli ta it šī aj tu jū
"I frankly tell you what she clearly sees."
```

The absence of `ke` distinguishes embedded content questions from direct ones.

---

## 23. Cleft Sentences

Clefts place focus on a constituent using `bī ... ðæt`:

```
bī [FOCUS] ðæt [FiniteClause with gap]
```

Examples:
```
bī šī ðæt di rid ta it aj ðe bük
"It is she who read my book."

bī jesterdej ðæt di ərajv šī
"It was yesterday that she arrived."

bī in ðe park ðæt di sī ta hī wī
"It was in the park that we saw him."
```

The gap in the embedded clause corresponds to the focused element and is left empty (unlike relatives, which use a resumptive pronoun).

---

## 24. Conditional Types

All conditionals use `if` (or `unless` for negative). Tense and aspect in the protasis signal the type:

| Type | Protasis | Apodosis | Example |
|---|---|---|---|
| Open / factual | present | present or `wil` | `if rejn it rimejn hīr wī` |
| Counterfactual | `di` past | `wud` + verb | `if di nō it hī wud tel ta wī aj` |
| Past counterfactual | `dän di` past perf | `wud dän` + verb | `if dän di kəm šī wud dän help ta wī šī` |

New particles introduced:
- `wud` — counterfactual modal (would), occupies the Modal slot.

Examples:
```
if di hæv taj mätš aj wud gō tu ðe siti aj
"If I had more time, I would go to the city."

if dän di līv örlī šī wud dän ərajv ontajm šī
"If she had left early, she would have arrived on time."
```

---

## 25. Updated Formal EBNF

```ebnf
Sentence      := Clause ;

Clause        := CoordClause
               | SubClause
               | AskClause
               | ImperClause
               | HortClause
               | OptClause
               | CleftClause
               | FiniteClause ;

CoordClause   := Conj Clause Clause ;
SubClause     := SubConj Clause Clause ;
AskClause     := "ke" FiniteClause ;
ImperClause   := "du" FiniteClause | "not" "du" FiniteClause ;
HortClause    := "let" FiniteClause ;
OptClause     := "hop" FiniteClause ;
CleftClause   := "bī" FocusXP "ðæt" FiniteClause ;

FiniteClause  := VerbGroup (AdvP)* (ObjP | PercComp)? NP (CoreComp)* (SecPred)? ;
ObjP          := "ta" NP ;
PercComp      := "ta" NP BareV ;          (* perception verb complement *)
InfComp       := "tu" VerbGroup (AdvP)* (ObjP)? (CoreComp)* ;
VerbGroup     := (Modal)* ("di")? (Aspect)* ("not")? V ;
AdvP          := AdvWord | PP | DegreeP ;
DegreeP       := ("mor" | "les" | "most" | "līst" | "tu" | "evən" | "onli"
               | "ōlsō" | "ōlmost" | "ǰəst") (AdjP | AdvWord) ;
CoreComp      := PP | CP | RecipP | InfComp | BajP ;
CP            := "ðæt" FiniteClause ;
RecipP        := ("tu" | "for") NP ;
BajP          := "baj" NP ;               (* passive agent *)
SecPred       := AdjP | NP ;             (* secondary predicate, always final *)
FocusXP       := NP | PP | AdvWord ;

NP            := Pron | NBar | RelNP | CoordNP | WhPron | ExistNP | ReciprNP ;
NBar          := (Det)? ("s")? (AdjP)* N (PP)* ;
RelNP         := "ðæt" FiniteClause NBar ;
CoordNP       := Conj NP NP ;
ExistNP       := "ðer" ;                  (* expletive subject in existentials *)
ReciprNP      := "ič" "ðe" "äðər" ;

AdjP          := (DegAdv)* Adj (CompP)? ;
CompP         := "ðan" NP | "az" AdjP "az" NP ;  (* comparative standard *)
DegAdv        := "veri" | "tu" | "sō" | "mor" | "les" | "most" | "līst"
               | "enäf" | "almost" | "nīrli" ;

Det           := "æ" | "ðe" | "ðis" | "ðat"
               | "maj" | "jor" | "hiz" | "hör" | "its" | "aur" | "ðer"
               | "ol" | "evri" | "ič" | "sam" | "eni" | "nō" | "meni"
               | "fū" | "mätš" | "litəl" ;
Pron          := "aj" | "jū" | "hī" | "šī" | "it" | "wī" | "ðej" ;
WhPron        := "hū" | "wat" | "wer" | "wen" | "waj" | "hau" | "wij" ;

Conj          := "ænd" | "or" | "nor" | "bät" | "jet" | "sō" | "for" ;
SubConj       := "if" | "unless" | "wen" | "whajl" | "bifor" | "after"
               | "sins" | "until" | "bikoz" | "ðou" | "oldou" | "az"
               | "wæðer" | "ðæt" ;

Modal         := "wil" | "kan" | "möst" | "šöd" | "wud" ;
Aspect        := "iŋ" | "dän" | "jus" | "kon" ;
BareV         := V ;                      (* bare verb in perception complements *)
```

Note on `wen`: as a `WhPron` it appears inside a `ke`-question in the oblique slot; as a `SubConj` it is clause-initial. The parser distinguishes by position.

Note on `tu`: as a preposition it precedes NP (directional CoreComp); as an infinitival marker it precedes V; as a degree adverb it precedes AdjP. These are distinguished by what follows.

## 26. Quick Parse Examples

```
bajt hard ta æ dogg mæn
V    Adv  ta OBJ   SUBJ
"The man bites a dog hard."

ænd sī klīrli ta æ kar šī  rid slowli ta ðe bük aj
CONJ [clause-A]             [clause-B]
"She clearly sees a car and I slowly read the book."

if rejn hard it  rimejn in hām wī
SUBCONJ [sub-cl] [mat-cl]
"If it rains hard, we stay at home."

ke giv kindli ta wat hī tu šī
Q  V   Adv    ta WH  SUBJ RECIP
"What does he kindly give to her?"

ðæt lajk reeli ta it šī  æ dogg
REL [relative clause]     [head NBar]
"a dog that she really likes"

get enbrek ta ðe glas baj hī
PASS       ta OBJ      BAJ-AGENT
"The glass was broken by him."

bī æ dogg ðer in ðe gardən
COP OBJ   EXPL LOC
"There is a dog in the garden."

sī ta hī aj run
V  ta OBJ  BARE-V
"I saw him run."

want tu gō šī tu ðe markit
V    INF       DIR-COMP
"She wants to go to the market."

bī mor tajərd šī ðan hī
COP COMP-DEG AdjP SUBJ  COMP-STD
"She is more tired than he is."

pejnt kareföli ta ðe wol šī red
V     Adv      ta OBJ      SUBJ SEC-PRED
"She carefully painted the wall red."

bī šī ðæt di rid ta it aj ðe bük
CLEFT-FOC  COMP [embedded clause with gap]
"It is she who read my book."
```

