# FitFindr

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, every
> command, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> python app.py listings --full -n 6      # read the data (Milestone 1)
> python app.py fields                    # what you can filter on
> python app.py ask 'vintage graphic tee under $30'
> ```
>
> All three tools are stubs, so that last command will do nothing useful yet.
> That's the starting position.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     This is your submission. Fill each section in as you finish the milestone
     it belongs to — don't leave it all to the end.

     Unit 3 asks for the first five sections. Unit 4 adds the five below them.
     Leave the unit 4 sections alone until then; they're here so you know
     what's coming.

     Everything is pasted as TEXT. No screenshots, no images, no video links.
     A typed block of output gets full credit; a picture of the same output
     gets none.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 3 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Three or four sentences: what a user asks for, and what they get back. -->
The user requests an outfit based on description and max price of their choice. Where the outfit is found through the data acquired from the AI agent. Thhe data is appropriately displayed in a json output from the AI agent. 


---

## Tool Inventory

<!-- Four lines per tool. This is worth 2 points and it's the single most
     common place students lose them.

     "Returns a list" earns NOTHING. The description has to say what is IN
     the list.

     The empty case isn't optional either — it's the thing your loop branches
     on, and if you don't decide it here you'll discover it as a crash in
     Milestone 5. -->

### `search_listings`


- **What it does:**
Search the listings data for items matching a description, and optionally a size and a price ceiling. Where it finds items matching the criteria.
- **Inputs:** <!-- name and type each: `max_price` (float), not "a price" -->
- description (str), size (str), max_price (float)
- **Returns:**
- A list of dictionaries, each representing an item with its details. The most accurate matches are returned first.
- **When it has nothing:**
- Returns an empty list.

### `suggest_outfit`

- **What it does:**
- Suggests an outfit based on the user's search results.
- **Inputs:**
- new_item (dict), wardrobe (list of dicts)
- **Returns:**
- A list of dictionaries, each representing an item with its details.
- **When it has nothing:**
- Returns an empty list.

### `create_fit_card`

- **What it does:**
- Creates an accurate caption based on the potential find. 
- **Inputs:**
- outfit (string), new_item (list of dict)
- **Returns:**
- A string representing the find with an accurate caption.
- **When it has nothing:**
- Returns an empty string.

---

## Planning Loop

<!-- Your branch rule, stated as a rule — the condition AND both paths — plus
     the file and function that holds it.

     Like this:
       "If search_listings returns an empty list, put a message in the session
        and stop. Otherwise take the first result and go to suggest_outfit."
        — agent.py::run_agent

     The grader checks your code against what you claim here, so the file and
     function have to be real. -->

**Branch rule:**
If the create_fit_card returns an empty caption or the outfit is empty, then it should show "No caption can be generated". Otherwise continue to genereate() 

**Where it lives:** `agent.py::run_agent`

**How the query is parsed:** <!-- regex, string splitting, or asking the model — say which -->
The query is parsed using string splitting. Then the parser extracts the outfit and new items details.

**What moves through the session:** <!-- which fields, in what order -->
the session stores the original query, parsed search results, and the generated fit card. If no listings match, an error message it stored.

---

## Sample Run

<!-- Two things go here.

     1. One FULL query and its output, pasted as text.
     2. Your three per-tool terminal tests — the command and what it printed. -->

**One full query**

```
$ python app.py ask '...'

python app.py ask 'ventage jeans under $40'

```

**The three tools, tested one at a time**

```
$ python -c "from tools import search_listings; print(search_listings('graphic tee', max_price=30))"

```
python -c "from tools import search_listings; print(search_listings('vintage jeans', max_price=40))"

```
$ python -c "from tools import suggest_outfit; ..."

```
python -c "from tools import suggest_outfit; 
print(suggest_outfit(
  [{"id": "lst_002",
    "title": "Y2K Baby Tee — Butterfly Print",
    "description": "Super cute early 2000s baby tee with butterfly graphic. Fitted crop length. Tag says medium but fits like a small.",
    "category": "tops",
    "style_tags": ["y2k", "vintage", "graphic tee", "cottagecore"],
    "size": "S/M",
    "condition": "excellent",
    "price": 18.00,
    "colors": ["white", "pink", "purple"],
    "brand": null,
    "platform": "depop"}], [
      {
        "id": "w_001",
        "name": "Baggy straight-leg jeans, dark wash",
        "category": "bottoms",
        "colors": ["dark blue", "indigo"],
        "style_tags": ["denim", "streetwear", "baggy"],
        "notes": "High-waisted, sits above the hip"
      },
      {
        "id": "w_002",
        "name": "Wide-leg khaki trousers",
        "category": "bottoms",
        "colors": ["khaki", "tan"],
        "style_tags": ["earth tones", "minimal", "wide-leg"],
        "notes": null
      },))"

```
$ python -c "from tools import create_fit_card; ..."

python -c "from tools import create_fit_card; print(create_fit_card(
  'jeans and brown sneakers', 
  [{"id": "lst_002",
    "title": "Y2K Baby Tee — Butterfly Print",
    "description": "Super cute early 2000s baby tee with butterfly graphic. Fitted crop length. Tag says medium but fits like a small.",
    "category": "tops",
    "style_tags": ["y2k", "vintage", "graphic tee", "cottagecore"],
    "size": "S/M",
    "condition": "excellent",
    "price": 18.00,
    "colors": ["white", "pink", "purple"],
    "brand": null,
    "platform": "depop")}])"

```

---

## How I Used AI

<!-- Two specific moments. What you asked, what came back, what you changed.

     "I used Claude to help me code" is not enough.

     "I gave Claude my search_listings spec. It returned None on no match
     instead of an empty list, so I changed it" is the level we want. -->

**Moment 1**

- *What I asked for:*
- I used codex to gain clarity on certain points of the questions like what does "what moves through the session means"
- *What came back:*
- It gave me a example on how to answer the question
- *What I changed:*
- I was able to think through the problem differently and show the whole process of how the code interacted with the input.

**Moment 2**

- *What I asked for:*
- I used codex to clarify what is the purpose of branch rule.
- *What came back:*
- It gave me an explanation of what branch rule is and how it works. As well as providing me an example of how to create it.
- *What I changed:*
- I changed my solution to include the if-else like structure to the thoughts I had already written down.

<!-- ═══════════════════════ UNIT 4 — THE TEST ═══════════════════════

     Don't fill these in during unit 3.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Run Log — Before

<!-- Five criteria, five tries each, in this exact format.

     Five, because your criteria are written out of five. Mark each try PASS
     or FAIL, count the passes, and read that count against your target — a
     row targeting 4 of 5 with three PASS cells is MISSED (3/5).

     `python run_eval.py --label before` runs everything and writes the table
     into results/. Paste it here and fill in the verdicts. -->

| Criterion | Target | Try 1 | Try 2 | Try 3 | Try 4 | Try 5 | Verdict |
|---|---|---|---|---|---|---|---|
| 1. Matching query completes all three tools | At least 4/5 complete | FAIL | FAIL | FAIL | FAIL | FAIL | MISSED (0/5) |
| 2. Impossible query stops before the second tool | 5/5 stop with a useful change message | FAIL | FAIL | FAIL | FAIL | FAIL | MISSED (0/5) |
| 3. State passes the selected item correctly | Not tested in this run | NOT TESTED | NOT TESTED | NOT TESTED | NOT TESTED | NOT TESTED | NOT TESTED |
| 4. Fit card meets its stated format | Not tested in this run | NOT TESTED | NOT TESTED | NOT TESTED | NOT TESTED | NOT TESTED | NOT TESTED |
| 5. Price requirement is respected | Not tested in this run | NOT TESTED | NOT TESTED | NOT TESTED | NOT TESTED | NOT TESTED | NOT TESTED |

**Real output from one try**, pasted as text, naming the file and function
that produced it:

```
Source: `results/run_2026-09-30_2047_before.md`, produced by
`run_eval.py::main`, which called `agent.py::run_agent`.

Query: `vintage graphic tee under $30`
Wardrobe: example

stopped early: yes — The planning loop isn't built yet — see the TODO in agent.py.
selected_item: (none)
search_results: 0
```

---

## Verdicts and Diagnoses

<!-- MET or MISSED per criterion against LAST UNIT's target, plus a sentence on
     how you decided.

     Then, for every miss: which of the four places it happened — a tool, the
     loop's branch, the session, or the model's output — AND the mechanism.

     Not a diagnosis:  "The fit card was bad."
     A diagnosis:      "The fit card criterion missed on 2 of 5 items. Both had
                        an empty brand field. My prompt puts the brand in the
                        first sentence, so the card opened with a blank and read
                        like a fragment. The tool worked; the prompt assumed a
                        field that isn't always there."

     Look for a pattern. Three misses on the same tool is one problem, not
     three. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Matching query completes all three tools in at least 4/5 tries | 4/5 | MISSED (0/5) | Every matching-query try stopped with the planning-loop TODO message, so the tools never completed. The failure was in the loop before the tools were called. |
| 2 | Impossible query stops before `suggest_outfit` in 5/5 tries and explains what to change | 5/5 | MISSED (0/5) | The runs stopped before searching because the loop was still a stub. The error did not tell the user what to change. The failure was in the loop branch/message. |
| 3 | State passes the selected item correctly | Not tested | NOT TESTED | The before scenarios did not compare `session["selected_item"]` with the item sent to `suggest_outfit`. |
| 4 | Fit card meets its stated format | Not tested | NOT TESTED | No fit cards were generated because the loop stopped early. |
| 5 | Price requirement is respected | Not tested | NOT TESTED | The before scenarios did not evaluate a fit card's price requirement. |

**Diagnoses**

Criteria 1 and 2 show the same underlying problem: `agent.py::run_agent` had
not been implemented, so it returned the starter TODO error before calling
`search_listings()`. This is one loop problem rather than separate tool
failures.

Criteria 3–5 were not tested by the existing before scenarios. They need
additional scenarios in `scenarios.py` before they can be scored honestly.



---

## Loop Trace

<!-- One full run, printed step by step, with the MCP call visible in it.

     `python app.py ask '...' --trace` once you've added the trace.step()
     calls in Milestone 2.

     Worth pasting BOTH the happy path and the empty-search path. The empty
     one should be visibly shorter, because it stops. If your two traces are
     the same length, your branch isn't working — and this is the fastest way
     anyone will ever find that out. -->

**Happy path**

```
[1] parse_query
      in:  vintage blue dress shirt max price of $100
      out: dict with keys: description, size, max_price
[2] search_listings (via MCP)
      in:  dict with keys: description, size, max_price
      out: 7 items: Vintage Levi's 501 Jeans — Medium Wash, Graphic Tee — 2003 Tour Bootleg Style, Oversized Crewneck Sweatshirt — Vintage Navy … +4 more
      →    7 match(es)
[3] select_item
      out: Vintage Levi's 501 Jeans — Medium Wash ($38.0, depop)
Warning: there are non-text parts in the response: ['thought_signature'], returning concatenated text result from text parts. Check the full candidates.content.parts accessor to get the full model response.
[4] suggest_outfit
      in:  Vintage Levi's 501 Jeans — Medium Wash ($38.0, depop)
      out: Based on your current wardrobe and the addition of the **Vintage Levi's 501 Jeans (Medium Wash)**, here are tw…
      →    10 wardrobe item(s)
Warning: there are non-text parts in the response: ['thought_signature'], returning concatenated text result from text parts. Check the full candidates.content.parts accessor to get the full model response.
[5] create_fit_card
      in:  Vintage Levi's 501 Jeans — Medium Wash ($38.0, depop)
      out: Nothing beats the lived-in comfort and perfect straight-leg fit of these Vintage Levi's 501s. Whether I'm thro…

  Found:    Vintage Levi's 501 Jeans — Medium Wash — $38.0 on depop

  Outfit:   Based on your current wardrobe and the addition of the **Vintage Levi's 501 Jeans (Medium Wash)**, here are two thrifted-style outfit suggestions that blend your existing streetwear, minimal, and vintage aesthetics:

### Outfit 1: Effortless 90s Streetwear (Casual & Cool)
*This look plays on proportions by pairing the fitted basic with the classic, straight-leg fit of the new 501s, finished off with classic streetwear staples.*

* **Top:** White ribbed tank top (fitted)
* **Bottoms:** Vintage Levi's 501 Jeans — Medium Wash
* **Outerwear:** Vintage black denim jacket (worn over the shoulders or open)
* **Shoes:** Chunky white sneakers
* **Accessories:** Black crossbody bag & Brown leather belt (tucked into the denim for a nice contrast)
* **Vibe:** Clean, casual 90s off-duty model aesthetic.

### Outfit 2: Grunge-Infused Contrast (Edgy & Cozy)
*This outfit utilizes the contrast between the medium-wash vintage denim and darker, chunkier pieces for a more textured, transitional weather look.*

* **Top:** Oversized grey crewneck sweatshirt (you can do a half-tuck or let it drape casually)
* **Bottoms:** Vintage Levi's 501 Jeans — Medium Wash
* **Shoes:** Black combat boots (letting the hems of the 501s sit nicely over the tops of the boots)
* **Accessories:** Black crossbody bag & Brown leather belt
* **Vibe:** Utilitarian, slightly grunge, and effortlessly comfortable.

  Fit card: Nothing beats the lived-in comfort and perfect straight-leg fit of these Vintage Levi's 501s. Whether I'm throwing them on with a crisp white tank for an effortless 90s off-duty look or pairing them with an oversized crewneck for a grunge-infused aesthetic, this medium-wash staple brings that ultimate vintage streetwear vibe. Snagged these on Depop for just $38.00, and they are easily about to become my most-worn denim.

2 model calls this session, 896 prompt + 452 output tokens
```

**Empty search**

```
python app.py ask 'v' --trace[1] parse_query
      in:  v
      out: dict with keys: description, size, max_price
[2] search_listings (via MCP)
      in:  dict with keys: description, size, max_price
      out: [] (empty)
      →    0 match(es)
[3] branch
      →    search returned []: stopping before suggest_outfit

  Nothing in the listings matched description 'v'.
Things to change: try broader words — 'jacket' finds more than 'cropped corduroy jacket'.

0 model calls this session
(base) ksuga@Mac ai201-project2-fitfindr-starter-v2026 % python app.py ask '' --trace
Ask for something, or press Enter on an empty line to quit.

> ^C
0 model calls this session
(base) ksuga@Mac ai201-project2-fitfindr-starter-v2026 % python app.py ask '' --trace
Ask for something, or press Enter on an empty line to quit.

>
0 model calls this session
```

**On the MCP move:** <!-- what changed in your code, and whether anything
behaved differently afterwards. If the rewire didn't work, say exactly where it
broke — the error text and the last thing that worked. That earns the point in
full. -->
I moved `search_listings` to MCP. I added the tool to `mcp_server.py` and changed
  `agent.py::_search()` to call `mcp_client.call_tool("search_listings", ...)`.
  The matching query still returned listings, and the impossible query still
  returned an empty list and stopped before `suggest_outfit()`.

  When the MCP server was unavailable, the call failed with
  `[exact error message]`. The last thing that worked was the local
  `search_listings()` function. The fallback then called the local function, so
  the agent still completed its search behavior.


---

## The Improvement

<!-- What you changed, why your diagnosis pointed at it, and the after-run in
     the same table format. One change, measured properly.

     `python run_eval.py --label after` -->

**What I changed:**
I implemented the planning loop in `agent.py::run_agent`. It now parses the
query, stores the parsed values in the session, calls `search_listings()`, and
branches when the search returns an empty list. If results exist, it stores the
first item in `session["selected_item"]`, passes the session values to
`suggest_outfit()`, and then passes the outfit and item to

**Which failure it was meant to fix:**
This was meant to fix Criteria 1 and 2. Before the change, the loop returned
“The planning loop isn't built yet” before calling any tools. The matching path
could not complete, and the impossible-query path did not search or provide
useful suggestions to the user.

### Run Log — After

| Criterion | Target | Try 1 | Try 2 | Try 3 | Try 4 | Try 5 | Verdict |
|---|---|---|---|---|---|---|---|
| 1. matching query completes |  |   |   |   |   |   |  |
| 2. impossible query stops early |  |   |   |   |   |   |  |
| empty wardrobe _(diagnostic — not one of your five)_ |  |   |   |   |   |   |  |

**Did it help, and how do I know:**

<!-- If it made things worse, say that. Honestly reported, that earns full
     credit and is more interesting than one that worked. -->
It improved the matching query path, fixed the impossible query path, and diagnosed the empty wardrobe issue.


---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped where
     you did. "I ran out of time" is fine if it's true. Pretending nothing is
     left is not. -->
I was able to complete all the necesary criteria and requirments of the tools.


<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 3

       [ ] criteria.md has five numbered criteria, each with a target
       [ ] Each criterion has a reason underneath it
       [ ] All five unit 3 sections above have real content
       [ ] Tool Inventory: all three tools, inputs WITH TYPES, a specific
           return value, and the empty case
       [ ] Planning Loop names the branch rule and agent.py::run_agent
       [ ] Sample Run: one full query plus the three per-tool tests, as text
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN, you submit the same one
           next unit

     SUBMISSION CHECKLIST — unit 4

       [ ] mcp_server.py exists with one tool registered
           (or a written record of exactly where the rewire broke)
       [ ] Run Log — Before, five criteria, five tries each
       [ ] Real output pasted underneath, naming file and function
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, naming a place AND a mechanism
       [ ] Loop Trace, with the MCP call visible in it
       [ ] All three failure modes triggered and handled
       [ ] One improvement, with Run Log — After in the same format
       [ ] What's Still Broken
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository. Your commit history is what
     shows your criteria existed before your results did.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
