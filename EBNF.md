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

verbal_form = mood_particle, voice_modifier, root, [local_clause];

direct_object  = "ke", noun_phrase;
indirect_object = "to", noun_phrase;

verbal_reference = "ko", local_clause;   (* everything after "ko" describes the verbal form of the sentence *)

mood_particle = "ni" | "nio" | "ki" | "kio";
voice_modifier = "" | "kea" | "toa";

(* === Interrogative particle (can appear anywhere; only once per sentence) === *)
interrogative_particle = "" | "ka";

end_punctuation = "." | ";";

(* === Noun phrase === *)
local_clause = noun { description };

(* === Elements in the chain === *)
description = adjective 
        | prepositional_phrase
        | "da";

(* === Adjectives === *)
adjective = root 
          | (comparation root "di" local_clause);

comparation = "mae" | "pae" | "kai";

(* === Prepositions === *)
prepositional_phrase = preposition, noun;

(* === Basic nominal structure === *)
noun = modified_nominal | pronoun;

modified_nominal = [pointer], [number], [role], (root | interrogative);

pointer = "tei" | "dea" | "ceo";
number  = count | "sai" | "cou";
role    = "gao" | "kao" | "rio" | "nia";

interrogative = "kao";
pronoun = "mi" | "tu" | "riu" | "ti";

root = (* any base root from the dictionary *);
preposition = (* any preposition from the dictionary *);
count       = /* any number from the dictionary (noe, doe, toe, …) */;
```

