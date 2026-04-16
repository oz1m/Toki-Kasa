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
conjunction = "pai" | "roi" | "soi" | "boi" | "mai" | "tai" | "fai";

(* === Movable elements (any order, as long as their marker is used) === *)
movable_element = explicit_subject | direct_object | indirect_object | verbal_reference;

implicit_subject = noun_phrase;          (* only valid if it is the first nominal element after the conjunction *)
explicit_subject = "ga", noun_phrase;
direct_object  = "ke", noun_phrase;
indirect_object = "to", noun_phrase;

verbal_form = mood_particle, voice_modifier, root, [local_clause];

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

comparation = "mae" | "pae" | "tae" | "mao" | "pao" | "tao";

(* === Prepositions === *)
prepositional_phrase = preposition, noun;

(* === Basic nominal structure === *)
noun = modified_nominal | pronoun;

modified_nominal = [pointer], [number], [role], (root | interrogative_placeholder);

pronoun = [number], ("mi" | "tu" | "riu" | "ti");

pointer = "tei" | "dea" | "cae";
number  = count | "sai" | "coi";
role    = "gao" | "kao" | "tou" | "nia";

interrogative_placeholder = "kai";

count =
    [ million ],
    [ hundred_thousand ],
    [ ten_thousand ],
    [ thousand ],
    [ hundred ],
    [ ten ],
    [ unit ] ;

million         = [ digit ] , "tana";
hundred_thousand= [ digit ] , "dana";
ten_thousand    = [ digit ] , "gana";
thousand        = [ digit ] , "rana";
hundred         = [ digit ] , "kana";
ten             = [ digit ] , "sana";

unit            = digit ;

digit       = "noe" | "doe" | "toe" | "foe" | "koe"
            | "seo" | "teo" | "ceo" | "reo";

zero        = "nane" ;

preposition = base_preposition | negated_preposition ;

negated_preposition = base_preposition , "o" ;

base_preposition =
	  "de" | "nu" | "bi" | "cu" | "ca" | "sa" | "ge" | "pu"
    | "ne" | "gu" | "su" | "ru" | "be" | "ba" | "fu" | "ci" | "ku"
    | "fe" | "fa" | "ri"
    | "du" | "ra" ;

root = (* any base root from the dictionary *);
```

