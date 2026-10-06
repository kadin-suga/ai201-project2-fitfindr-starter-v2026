# Acceptance criteria — FitFindr

Five criteria that say what "working" means for this agent, written in unit 3
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"The agent handles errors"* is an opinion.
*"When search returns nothing, the agent stops before calling the second tool,
in 5 of 5 tries"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter one. A reason that says something about your tools, your loop, or the
data earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

**Two are written for you. You write three.**

---

## 1. A matching query completes all three tools

Given a query that matches at least one listing, the agent completes all three
tool calls and returns a fit card — in at least 4 of 5 tries.

**Why this target:**
<!-- Why 4 of 5 and not 5 of 5? Something about your search, probably —
     "my search is a plain keyword match and some phrasings will miss" is a
     real answer. -->
My search is a plain keyword match and some phrasings will miss. 

---

## 2. An impossible query stops before the second tool

Given a query that matches no listings, the agent stops before calling
`suggest_outfit` and returns a message naming what to change — 5 of 5 tries.

**Why this target:**
<!-- Why is 5 of 5 reasonable here when criterion 1 isn't? What's different
     about this path? -->
Agent runs are fragile therefore sometimes fail multiple times before succeeding. So to verify that this is a true fault the agent must run 5 of 5 tries. Therefore 5 of 5 is reasonable here to verify that the reason why the agent stopped before calling `suggest_outfit` is not a state failure.

---

## 3. Something about state


<!-- YOU WRITE THIS ONE.

     How would you know that the item your search found is the same item the
     next tool received? Name something countable or observable.

     This is the criterion people find hardest, because state failure doesn't
     look like state failure — it looks like a tool problem. Something that
     compares session["selected_item"] against what actually reached
     suggest_outfit is the shape you're after. -->

Compare session["selected_item"] against what actually reached suggest_outfit is the output that is compared against the actual item. Check noticeable differences between the two items to verify that the model is acting on the same state.

**Why this target:**
This specific target is chosen to verify that the model is acting on the same item as the item returned by session["selected_item"]. Having this identification for the outputs of the models allows for easier debugging and verification of the model's behavior.


---

## 4. Something about the fit card

<!-- YOU WRITE THIS ONE.

     The fit card calls a model, so the same input can produce different words
     each time. That's not a bug — it's the nature of the tool. So what would
     make it acceptable?

     Think about what you'd actually be unhappy to see. A caption that never
     mentions the price? Two different items producing the same opening
     sentence? A card longer than a caption anyone would post? Any of those can
     be turned into a number. -->

Inside a fit card output, I would look for specific typographic glyph next to numeric numbers and count the sentence size of no more than 3 sentences to verify that the model has the expected output details as required. 


**Why this target:**
This target allows the model output be automatically verified for expected output details and it allows the model to be evaluated for its ability to produce consistent, accurate relevant output. Having to verify the fit card output to identify numeric values and sentence size is a reliable way to verify that the model is producing information that would be useful to the user.


---

## 5. Your choice

<!-- YOU WRITE THIS ONE TOO.

     Pick something you actually care about getting right. Speed, the empty
     wardrobe path, what happens when the model can't be reached, whether the
     search respects a price ceiling — anything, as long as it names a number
     or an observable outcome. -->

I would compare whether or not the model output matches the expected price requirements. This is through extracting the numeric value from the model output and comparing it to the expected price ceilling. If the model output does not match the expected price, the model is not producing the expected output and should be re-run for its ability to produce consistent, accurate relevant output.



**Why this target:**
This specific target allows the model output to be evaluated for matching the expected price requirements, as it ties equivalently to the user's expectations. If the model fails to match the expected price ceiling and outputs this response, the user would complain to the model provider and never use the model again. 


---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 4 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 4. Something about the fit card

         The fit card is different every time.

         **Why this target:** ...

         > **Revised in unit 4:** For 5 different items, the 5 fit cards share
         > no opening sentence.
         >
         > **Why revised:** "different" wasn't checkable — two cards that
         > differed by one word still counted. The new version is something I
         > can actually score.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said the empty search stops it 5 of 5 times, but I got 3 of 5,
            so 3 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
