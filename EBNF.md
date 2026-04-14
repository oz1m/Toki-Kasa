# EBNF
---

```EBNF
sentence = [conjunction_part],
           [implicit_subject],          (* implicit subject is only allowed at the very beginning *)
           { movable_element },
           verbal_form,
           { movable_element },
           [interrogative_particle],
           end_punctuation;

conjunction_part = "" | (conjunction ",");
conjunction = "pi" | "ro" | "so" | "bo" | "ma" | "ta" | "fi";

(* === Movable elements (any order, as long as their marker is used) === *)
movable_element = explicit_subject | direct_object | indirect_object | verbal_reference;

implicit_subject = noun_phrase;          (* only valid if it is the first nominal element after the conjunction *)
explicit_subject = "ga", noun_phrase;

verbal_form = mood_particle, voice_modifier, noun, [local_clause];

direct_object  = "ke", noun_phrase;
indirect_object = "to", noun_phrase;

verbal_reference = "ko", local_clause;   (* everything after "ko" describes the verbal form of the sentence *)

mood_particle = "ni" | "nio" | "ki" | "kio";
voice_modifier = "" | "kea" | "toa";

(* === Interrogative particle (can appear anywhere; only once per sentence) === *)
interrogative_particle = "" | "ka";

end_punctuation = "." | ";";

(* === Noun phrase (full nominal with modifiers) === *)
noun_phrase = noun_form [local_clause];

(* === Local modifiers (adjectives and prepositions) === *)
local_clause = modifier { "da" modifier };   (* "da" resets the chain to the original head noun *)

modifier = adjective | preposition_form;

preposition_form = preposition, noun_phrase;   (* recursive: each preposition modifies only the noun phrase immediately following it *)

adjective = noun | (comparation noun "di" noun);

comparation = "mae" | "pae" | "kai";

(* === Basic nominal structure === *)
noun_form = [pointer], [number], [role] noun;

pointer = "tei" | "dea" | "ceo";
number  = count | "sai" | "cou";
role    = "gao" | "kao" | "rio" | "nia";

(* === Lexical categories (defined in the dictionary) === *)
noun        = "kao" | (* any base noun from the dictionary *);
preposition = (* any preposition from the dictionary *);
count       = /* any number from the dictionary (noe, doe, toe, …) */;
```

