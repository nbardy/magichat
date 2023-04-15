## Magic Hat

A lisp dialogue for talking to multimodal LLMS

Example:

film.superprompt
```clojure
(let
 ^{:model "blip2"
   :model-args ["test_example.jpg"]}
 [people-count "How many people are in the image, answer zero if none?"
  subject (cond
            (= people-count 0) "What is in this image?"
            (= people-count 1) "Q: What does the person in this image look like?
                                 Notes: Add comments on the most interesting features, what is visualy stunning about this person?
                                 A:"
            (>= people-count 2) "Q: What does the person in this image look like?
                                 Notes: Add comments on the most interesting features, what is visualy stunning about this person?
                                 A:")
  total-caption (str "The Subject is {subject}")
  critique-caption "Critique the caption: {subject}"]
  "Given the following:
    caption
    {total-caption}

    critique caption:
    {critique-caption}

    Generate a final caption densely that describes the most interesting parts of the image in the simplest way.")
```

Call in python

```
import magichat

result = magichat.magic("film.superprompt")
```


### Features:
- LLM first, strings are by default sent to the server
- String Interpolation with a new type:
	{gen_resul} or {gen_result:fill} to include the query for the generation result
- Adopts a modern lisp syntax mostly inherited from Clojure(Works with CLJ syntax highlighting and with co-pilot as a result)

## Why?

This is mostly used as an embedded lang for small chains of prompts. A language designe for prompts first
with some helpers for chaining them. By using a new DSL we can introduce agressive defaults and do some simple examples in a small amount of code.

These are meant to be small embedded prompt recipes in a bigger python program. Not a new programming language.

