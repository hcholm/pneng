# Pneŋ Lexicon (v0.4)

[Overview](pneng.md) | [Orthography](pneng-orthography.md) | [Grammar](pneng-grammar.md) | [Lexicon](pneng-lexicon.md) | [Examples](pneng-examples.md) | [Sample Text](pneng-sample-text.md)

## Valency Tags

| Tag | Meaning |
|---|---|
| `I` | intransitive — no `ta` object |
| `T` | transitive — requires `ta` object |
| `A` | ambitransitive — both frames legal; transitive requires `ta` |
| `D` | ditransitive — theme with `ta`, recipient with `tu` or `for` |

## 1. Pronouns

Pronouns are invariant (no case morphology). Position signals role.

| Form | Gloss |
|---|---|
| `aj` | I / me |
| `jū` | you |
| `hī` | he / him |
| `šī` | she / her |
| `it` | it |
| `wī` | we / us |
| `ðej` | they / them |
| `self` | reflexive particle (follows pronoun: `aj self`) |

## 2. Determiners and Core Particles

| Form | Class | Gloss |
|---|---|---|
| `æ` | det | a / an (indefinite singular) |
| `ðe` | det | the (definite) |
| `ðis` | det | this (proximal) |
| `ðat` | det | that (distal) |
| `s` | num | plural marker (free particle, pre-adjectival) |
| `ta` | obj-marker | introduces direct object |

### Possessive Determiners

Occupy the Det slot. Incompatible with `æ`, `ðe`, `ðis`, `ðat` in the same NP.

| Form | Gloss |
|---|---|
| `maj` | my |
| `jor` | your |
| `hiz` | his |
| `hör` | her |
| `its` | its |
| `aur` | our |
| `ðer` | their |

### Quantifier Determiners

| Form | Gloss | Number |
|---|---|---|
| `ol` | all | plural or mass |
| `evri` | every | singular |
| `ič` | each | singular |
| `sam` | some | plural or mass |
| `eni` | any | plural or mass (questions/negatives) |
| `nō` | no, none | any |
| `meni` | many | plural |
| `fū` | few | plural |
| `mätš` | much | mass |
| `litəl` | little | mass |

## 3. Grammatical Particles

| Form | Class | Gloss | Notes |
|---|---|---|---|
| `di` | tense | past | pre-verbal |
| `wil` | modal | future / intentive | |
| `kan` | modal | can / ability | |
| `möst` | modal | must / obligation | |
| `šöd` | modal | should | |
| `wud` | modal | would (counterfactual) | |
| `iŋ` | aspect | progressive | |
| `dän` | aspect | completive / perfect | |
| `jus` | aspect | immediate recent past | |
| `kon` | aspect | continuative / still | |
| `not` | neg | negation | |
| `ke` | q-particle | polar / content question marker | clause-initial |
| `du` | imp-particle | imperative marker | clause-initial |
| `let` | hortative | let / first-person plural imperative | |
| `hop` | optative | wish / may | clause-initial; distinct from verb `hopən` |
| `tu` | infinitival | marks infinitival complement | precedes bare V; distinct from preposition `tu` (to) |
| `en-` | pass-prefix | passive participle prefix | written solid: `enrid`, `enbrek` |
| `baj` | pass-agent | introduces passive agent | follows subject in passive clause |
| `ov` | genitive | of; introduces possessor | post-nominal PP |
| `ðan` | comparative | than; introduces standard of comparison | |
| `az` | equative | as (in `az ... az`) | |
| `ič ðe äðər` | reciprocal | each other | fixed NP; takes `ta` as object |

Note: `hop` (optative particle) and `hopən` (verb "hope") are distinct lexical items.

## 4. Conjunctions and Linkers

### 4.1 Coordinating Conjunctions

| Form | Gloss |
|---|---|
| `ænd` | and |
| `or` | or |
| `nor` | nor |
| `bät` | but |
| `jet` | yet (adversative coord.) |
| `sō` | so |
| `for` | for (causal coord.) |

Note: `jet` (adversative conjunction "yet") is spelled differently from `jus` and the aspect particle to avoid collision.

### 4.2 Subordinating Conjunctions

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
| `ðæt` | that (complementizer / relativizer) |

### 4.4 Focus Particles

Focus particles immediately precede the constituent they scope over.

| Form | Gloss |
|---|---|
| `onli` | only |
| `evən` | even |
| `ōlsō` | also, too |
| `ōlmost` | almost |
| `ǰəst` | just, merely |



| Form | Gloss |
|---|---|
| `ðen` | then |
| `hauevr` | however |
| `ðerfor` | therefore |
| `minwhajl` | meanwhile |
| `fainli` | finally |
| `ferst` | first |
| `sekənd` | second |
| `þörd` | third |

## 5. Prepositions

`in, on, at, tu, fram, for, wiþ, wiþaut, undər, ovər, bifor, after, nīr, bitwīn, əməŋ, intu, ontu, duriŋ, əraund, akros, əloŋ, bihajnd, insajd, autsajd, əlong`

Note: `nīr` (near) is added here. `bifor` and `after` function as both prepositions (followed by NP) and subordinating conjunctions (followed by a clause); the parser distinguishes these by what follows.

## 6. Wh-Words and Degree Words

| Form | Gloss |
|---|---|
| `hū` | who |
| `wat` | what |
| `wer` | where |
| `wen` | when (wh-) |
| `waj` | why |
| `hau` | how |
| `wij` | which |
| `hau meni` | how many |
| `hau mätš` | how much |
| `mor` | more |
| `les` | less |
| `most` | most |
| `līst` | least |
| `veri` | very |
| `enäf` | enough |
| `tu` | too |
| `almost` | almost |
| `nīrli` | nearly |

Note on `wen`: as a wh-word it occupies an argument or adjunct slot inside a `ke`-question. As a subordinating conjunction it is clause-initial. These uses are syntactically distinct.

## 7. Adverbs

### 7.1 Temporal

`nau, tudej, jesterdej, tumoro, sūn, lejt, örlī, alredi, stil, ofen, somtajmz, seldəm, nevr, alwejz, tonajt`

### 7.2 Manner (bare)

`fast, hard, long, loud`

Note: bare manner adverbs are adjectives that double as adverbs. They do not require `-li`.

### 7.3 Manner (`-li` forms)

`slowli, kalmli, klīrli, kareföli, frankli, sörtenli, prababli, direktli, normali, usuəli, fajnali, genərali, mostli, partli, tugaðər, separətli, softli, frendli, sudənli, kindli`

Note: `-li` is a productive derivational suffix forming manner adverbs from adjectives. Any adjective can take `-li` to form an adverb.

### 7.4 Locative

`hīr, ðer, insajd, autsajd, up, daun, klōs, far`

## 8. Core Nouns

### People and Roles

`man, wuman, pörzən, čajld, pærənt, frend, nejbər, tīčər, student, doktər, nörs, līdər, wörkər, farmər, rajdər, siŋər, rajtər, rīdər, drajvər, ōnər, gest, hōst, kiŋ, kwīn`

### Nature

`sun, mūn, star, skaj, klaud, rejn, snō, wind, ston, sænd, trī, græs, flaur, līf, rivər, lejk, sī, lænd, hil, mauntən, forest, fīld`

### Animals

`dogg, kæt, börd, fīš, hors, wulf, foks, ber, snejk, maus, ræt, kau, pig, gōt, šīp, čikən, dak`

Note: `kæt` not `kætt` (no consonant doubling per orthography).

### Places

`hūs, hām, rūm, dōr, windou, rōd, strīt, siti, taun, vilij, markit, skūl, templ, stejšən, port, brij, park, gardən, farm, hospitəl, ofis, stor`

Note: `brij` (bridge), `strīt` (street), `skūl` (school) follow phonemic orthography.

### Objects

`bük, pen, pejpər, kī, bæg, boks, bed, čer, tejbəl, læmp, fōn, kæmrə, klok, kændəl, najf, spūn, glas, botəl, kup, plejt, pæn, tūl`

### Abstracts

`tajm, dej, najt, yīr, histori, ajdiə, plæn, lo, rūl, trūþ, laj, fīr, hōp, ǰoj, soro, pīs, wor, prejz, kost, vælju, rīzən, end, fajər, tæsk`

Note: `lo` (law), `laj` (lie), `fajər` (fire), `tæsk` (task) added.

## 9. Adjectives

`big, smol, loŋ, šort, red, blū, grīn, blæk, wajt, braun, jelow, kajnd, hard, soft, worm, kōld, hot, draj, wet, stroŋ, wīk, old, nū, juŋ, rič, pör, fast, slow, hæpi, sæd, æŋgri, tajərd, opən, šut, klīn, dörti, klīr, dim, brajt, dark, sejf, denjərəs, trū, fols, frī, bizi, empti, ful, frendli, frendli`

Note: `frend-li` here is the adjective "friendly"; when used as an adverb (post-verbal) it means "in a friendly manner." The `-li` suffix thus appears in both the base adjective and serves double duty for the derived adverb form — this is regular.

## 10. Verbs (Valency Marked)

| Form | Tag | Gloss | Notes |
|---|---|---|---|
| `bī` | I | be | takes predicate complement, not `ta` object |
| `sī` | T | see | |
| `hīr` | T | hear | |
| `lajk` | T | like | |
| `luv` | T | love | |
| `het` | T | hate | |
| `nō` | T | know | |
| `þiŋk` | A | think | |
| `belīv` | T | believe | |
| `want` | T | want | |
| `nīd` | T | need | |
| `hæv` | T | have | |
| `get` | T | get | |
| `giv` | D | give | |
| `send` | D | send | |
| `tel` | D | tell | |
| `æsk` | D | ask | |
| `šō` | D | show | |
| `mek` | T | make | |
| `dū` | T | do (verb) | distinct from `du` (imperative particle) |
| `bild` | T | build | |
| `brek` | A | break | |
| `opən` | A | open | |
| `klōz` | A | close | |
| `muv` | A | move | |
| `törn` | A | turn | |
| `start` | A | start | |
| `stop` | A | stop | |
| `finišt` | T | finish | |
| `grō` | A | grow | |
| `siŋk` | A | sink | |
| `bojl` | A | boil | |
| `rajd` | T | ride | |
| `drajv` | A | drive | |
| `wok` | I | walk | |
| `run` | I | run | |
| `swim` | I | swim | |
| `sit` | I | sit | |
| `stænd` | I | stand | |
| `slīp` | I | sleep | |
| `wejk` | I | wake | |
| `liv` | I | live | |
| `ərajv` | I | arrive | |
| `gō` | I | go | |
| `kəm` | I | come | |
| `entər` | I | enter | |
| `līv` | T | leave | note: `līv` (leave) vs `liv` (live) |
| `set` | A | set | as in "the sun sets" |
| `put` | T | put | |
| `tek` | T | take | |
| `fajnd` | T | find | |
| `lūz` | T | lose | |
| `hōld` | T | hold | |
| `kīp` | T | keep | |
| `drop` | T | drop | |
| `pej` | T | pay | |
| `baj` | T | buy | |
| `sel` | T | sell | |
| `īt` | T | eat | |
| `driŋk` | T | drink | |
| `kuk` | T | cook | |
| `rid` | T | read | PRICE vowel in past tense is same form: `di rid` |
| `rajt` | T | write | |
| `spel` | T | spell | |
| `stədi` | T | study | |
| `lörn` | T | learn | |
| `tīč` | T | teach | |
| `plæn` | T | plan | |
| `ūz` | T | use | |
| `help` | T | help | |
| `ǰojn` | T | join | |
| `mīt` | T | meet | |
| `folow` | T | follow | |
| `wejt` | I | wait | |
| `wäč` | T | watch | |
| `luk` | I | look | |
| `briŋ` | T | bring | |
| `kæri` | T | carry | |
| `fol` | I | fall | |
| `rajz` | I | rise | |
| `rejn` | I | rain | |
| `blō` | I | blow | |
| `šajn` | I | shine | |
| `börn` | A | burn | |
| `fīl` | T | feel | |
| `smel` | T | smell | |
| `saund` | I | sound | |
| `sīm` | I | seem (raising) | takes infinitival CoreComp |
| `əpīr` | I | appear (raising) | takes infinitival CoreComp |
| `hapən` | I | happen | |
| `wəndər` | T | wonder | takes indirect question complement |
| `desajd` | I | decide | subject-control; takes `tu` infinitival |
| `traj` | I | try | subject-control; takes `tu` infinitival |
| `fors` | T | force | object-control; takes `tu` infinitival |
| `get` | aux | passive auxiliary | used with `en-` participle; also full verb "get/obtain" (T) |
| `prejz` | T | praise | |
| `lift` | T | lift | |
| `pejnt` | T | paint | |
| `hæmər` | T | hammer | |
| `bikəm` | A | become | |
| `rimejn` | I | remain | |
| `rest` | I | rest | |
| `wörk` | I | work | |
| `plej` | I | play | |
| `siŋ` | I | sing | |
| `dæns` | I | dance | |
| `smajl` | I | smile | |
| `læf` | I | laugh | |
| `kraj` | I | cry | |
| `hopən` | I | hope (verb) | distinct from `hop` (optative particle) |
| `prej` | I | pray | |
| `sejv` | T | save | |
| `lajt` | T | light | |
| `kover` | T | cover | |
| `ōpən` | A | (see `opən`) | |

## 11. Valency Summary

| Tag | Frame | Example |
|---|---|---|
| `I` | `V [Adv] SUBJ` | `run fast hī` |
| `T` | `V [Adv] ta OBJ SUBJ` | `sī klīrli ta æ kar šī` |
| `A` | either frame | `opən slowli ðe dōr` / `opən kareföli ta ðe dōr aj` |
| `D` | `V [Adv] ta THEME SUBJ (tu/for RECIP)` | `giv kindli ta æ bük aj tu šī` |

`bī` takes a **predicate complement** (NP, AdjP, or PP) rather than a `ta`-marked object.
