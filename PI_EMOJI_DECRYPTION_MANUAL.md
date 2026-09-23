# Field Manual for the Inversion of the SGA–Polyglot–Pi Emoji Transducer

## 0. Scope and assumed competencies

This document specifies the inverse transformation of a layered symbolic
channel. It assumes familiarity with positional notation, infinite streams,
finite-state transducers, substitution alphabets, Unicode extended grapheme
clusters, elementary set-valued inversion, and at least enough Romance and
Germanic lexicography to recognize a damaged codeword. Some acquaintance with
clock recovery, spectroscopic line identification, phase space, and selective
chemical separation will prevent several otherwise predictable mistakes. A
decoder who regards a displayed emoji as necessarily equivalent to one
Unicode scalar value should stop here and read Unicode Standard Annex #29
first.

The construction is not a single cipher. It is the composition

\[
E = E_{emoji} \circ E_{lexicon,K} \circ E_{SGA},
\]

where `K` is a 26-coordinate vector over the set `{1,2,3,4,5}`. Inversion must
therefore proceed right-to-left, like de-embedding cascaded two-port networks.
Attempting to read semantic content directly from the pictographs is category
error: the picture is merely a modulated carrier of an English Apple name, and
that name is merely the substrate from which one indexed character
precipitates.

## 1. Material that must survive transmission

Successful recovery requires all of the following:

1. The emoji ciphertext, including `-` and `//` delimiters.
2. The associated 26-digit language key.
3. The A–Z calibration matrix in Appendix A.
4. Apple's English emoji nomenclature from a compatible macOS generation.
5. Agreement that the pi stream begins with the integral digit `3`, not with
   the first fractional digit `1`.

The key is indexed by the ordinary alphabet, not by ciphertext position. If

```text
K = 21143343114522115543353232
```

then `K_A = 2`, `K_B = 1`, `K_C = 1`, and so forth. The digits name languages
under the invariant enumeration

```text
1 Spanish, 2 French, 3 German, 4 Italian, 5 Portuguese.
```

Calling `K` an “order” is convenient but algebraically imprecise: it is not a
permutation, because values may repeat.

## 2. Frame synchronization and segmentation topology

The ciphertext grammar is

```text
message      := plaintext_word ("//" plaintext_word)*
plaintext_word := emoji_pack ("-" emoji_pack)*
emoji_pack   := grapheme_cluster+
```

Thus `//` restores a plaintext space, while `-` separates the expansions of
adjacent plaintext letters. Treat both as zero-energy guard bands: neither
advances the pi clock nor contributes a symbol to the payload.

Within a pack, segment by Unicode extended grapheme cluster rather than code
point. For example, `❤️` consists of U+2764 followed by U+FE0F, flags are pairs
of regional indicators, and many people emoji contain variation selectors,
skin-tone modifiers, or U+200D ZERO WIDTH JOINER. Splitting any of these into
individual scalars destroys the lookup key.

Preserve every glyph exactly. Any mechanical segmenter must conform to Unicode
grapheme-breaking rules rather than counting scalar values. This distinction
is analogous to distinguishing a molecule from its constituent atoms: the
components matter, but the compound is the operative unit at this stage.

## 3. Carrier demodulation under a transcendental clock

Flatten the emoji clusters across every pack and plaintext word while retaining
the delimiter topology separately. Number the clusters globally from one. Now
generate the decimal digits of pi in this order:

```text
3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5, 8, 9, 7, 9, 3, ...
```

The decimal expansion is conceptually unbounded; a long message does not
authorize cycling a short table of digits. Convert each digit `d_i` to an
ordinal

\[
p_i = \begin{cases}
10, & d_i = 0 \\
d_i, & d_i \ne 0.
\end{cases}
\]

The special treatment of zero is forced by one-based indexing: there is no
zeroth character in the cipher's convention.

For emoji cluster `e_i`, obtain its exact English Apple name `A(e_i)`. Delete
U+0020 SPACE from the name, but do not indiscriminately normalize punctuation,
hyphens, ampersands, or other whitespace. The operation is a selective
reagent, not a universal solvent. Define

\[
N(e_i) = A(e_i).replace(" ", "").
\]

The recovered language character is the `p_i`-th character of `N(e_i)`, using
one-based ordinals. Concatenate recovered characters within the original
hyphen-delimited pack. Continue the pi stream across hyphens and double
slashes; never restart it at a pack or word boundary.

The emoji were selected randomly from the complete admissible ensemble.
Randomness is irrelevant to inversion because every admissible microstate
yields the same observable character at that pi position.

## 4. Inverting the polyglot codebook

After Section 3, each emoji pack has become one unaccented language codeword.
For a recovered word `w`, determine the source coordinate with

\[
C(w,K) = \{i \in [0,25] : W[K_i,i] = w\},
\]

where `W[language,letter]` is the calibration matrix in Appendix A. A singleton
candidate set yields the corresponding Latin letter. The equivalent SGA glyph
is obtained from the fixed transliteration in Section 5; transliterating that
glyph gives the same Latin letter, so the SGA layer contributes no additional
entropy.

The matrix is not guaranteed to be prefix-free or globally injective.
For certain randomly generated keys, two coordinates can select the same word
(for example, `uva` or `terra`). In that case `|C(w,K)| > 1`, and ciphertext
alone does not determine a unique letter. Retain every candidate, propagate the
branches through the rest of the message, and resolve them using orthographic,
syntactic, or semantic constraints. If two complete readings remain plausible,
the original is information-theoretically unrecoverable without the printed
SGA line or another side channel. This is a property of the codebook, not a
failure of the decoding procedure.

## 5. SGA back-transliteration

When an intermediate SGA rendering is required, apply the inverse fixed
substitution:

```text
ᔑ ʖ ᓵ ↸ ᒷ ⎓ ⊣ ⍑ ╎ ⋮ ꖌ ꖎ ᒲ リ 𝙹 !¡ ᑑ ∷ ᓭ ℸ̣ ⚍ ⍊ ∴ ̇/ || ⨅
A B C D E F G H I J K L M N O P  Q R S T  U V W X  Y  Z
```

These are Unicode lookalikes for graphical SGA forms, not a claim that SGA has
an ordinary standardized Unicode block. Beware especially of the multi-scalar
approximations for T and X and the two-character approximation for Y.

## 6. Worked inversion

Suppose the transmitted key is

```text
21143343114522115543353232
```

and the ciphertext is

```text
🀄️🎟️🔡🍝-👟🇧🇦🇳🇪❤️
```

There are two packs of four grapheme clusters. Using the uninterrupted first
eight pi digits gives the following ledger:

| i | pi | p | emoji | Apple name | name without spaces | recovered |
|---:|---:|---:|---|---|---|---|
| 1 | 3 | 3 | 🀄️ | mahjong tile red dragon | mahjongtilereddragon | h |
| 2 | 1 | 1 | 🎟️ | admission ticket | admissionticket | a |
| 3 | 4 | 4 | 🔡 | input symbol for lowercase letters | inputsymbolforlowercaseletters | u |
| 4 | 1 | 1 | 🍝 | spaghetti | spaghetti | s |
| 5 | 5 | 5 | 👟 | tennis shoe | tennisshoe | i |
| 6 | 9 | 9 | 🇧🇦 | flag of Bosnia & Herzegovina | flagofBosnia&Herzegovina | s |
| 7 | 2 | 2 | 🇳🇪 | flag of Niger | flagofNiger | l |
| 8 | 6 | 6 | ❤️ | red heart | redheart | a |

The packs therefore reduce to

```text
haus-isla
```

Under the supplied key, coordinate H selects language 3 (German), for which
the H-coordinate codeword is `haus`; coordinate I selects language 1
(Spanish), for which the I-coordinate codeword is `isla`. Hence

```text
haus/isla -> H/I -> ⍑-╎ -> HI
```

Case is not recoverable because comparison is case-insensitive and the
plaintext-to-SGA stage folds letters to lowercase.

## 7. Failure diagnostics

- **Readable words become nonsense after one point:** the pi stream was
  probably restarted after `-` or `//`; this is a clock-phase discontinuity.
- **A flag becomes two items:** Unicode scalars were confused with grapheme
  clusters.
- **Every extraction is displaced by one:** zero-based indexing was used, or
  the leading `3` of pi was omitted. In signal terms, the local oscillator is
  one tick out of phase.
- **Only names containing spaces fail:** indexing occurred before deleting
  U+0020 spaces.
- **An emoji has no matching name:** the sender and receiver probably have
  incompatible macOS emoji tables, or a variation selector was lost.
- **A recovered word maps to several letters:** preserve the candidate set;
  this is a genuine degeneracy, comparable to unresolved spectral lines.
- **Capitalization differs:** capitalization is outside the preserved state of
  this cipher.

The shortest correct summary is consequently: parse delimiters, segment
graphemes, dereference Apple names, delete spaces, project through pi ordinals,
invert the keyed lexical relation, and only then transliterate SGA.

## Appendix A. Polyglot calibration matrix

The columns retain the invariant excitation order `1 Spanish, 2 French,
3 German, 4 Italian, 5 Portuguese`. Rows are addressed by the Latin value of
the corresponding SGA glyph.

| Row | SGA | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|---|
| A | ᔑ | agua | arbre | apfel | barca | agua |
| B | ʖ | barco | bateau | boot | casa | barco |
| C | ᓵ | casa | chat | computer | dito | casa |
| D | ↸ | dedo | main | daumen | erba | dedo |
| E | ᒷ | estrella | etoile | erde | fuoco | estrela |
| F | ⎓ | fuego | feu | feuer | gatto | fogo |
| G | ⊣ | gato | glace | garten | hotel | gato |
| H | ⍑ | humo | hiver | haus | isola | homem |
| I | ╎ | isla | ile | insel | luna | ilha |
| J | ⋮ | luna | lune | katze | mano | lua |
| K | ꖌ | mesa | maison | licht | nave | mao |
| L | ꖎ | nube | neige | mond | occhio | navio |
| M | ᒲ | oro | oeil | nacht | pane | olho |
| N | リ | pan | pain | ohr | rosso | pao |
| O | 𝙹 | perro | pomme | pferd | sole | rio |
| P | !¡ | sol | soleil | regen | terra | sol |
| Q | ᑑ | tierra | terre | sonne | uva | terra |
| R | ∷ | uva | usine | tisch | vento | uva |
| S | ᓭ | viento | vent | uhr | zaino | vento |
| T | ℸ̣ | zapato | wagon | vogel | fiore | zebra |
| U | ⚍ | flor | xenon | wasser | latte | flor |
| V | ⍊ | leche | yacht | xylofon | mondo | leite |
| W | ∴ | mundo | zoo | yacht | cielo | mundo |
| X | ̇/ | cielo | fleur | zug | mare | ceu |
| Y | \|\| | campo | livre | blume | cane | mar |
| Z | ⨅ | playa | monde | himmel | porta | cao |
