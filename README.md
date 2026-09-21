# The Unofficial Guide

Steven Bennett — corpus: `advice_threads`

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none, because the grader can't
> read it.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Week 1

## What This Does

This unofficial guide answers questions from a corpus of 23 campus advice threads. Each thread is a question with three to five student replies. The system can tell you things the threads actually contain, such as when large employers close internship applications, how far the printing quota goes, and which mornings laundry is free. It also names the thread it used.

## Chunking Strategy

**Chunk size:** one reply, about 105 to 254 characters (175 on average)
**Overlap:** 0

These threads are short reviews, so information is packed into one sentence replies. I split on the --- reply N --- markers already in the files and put the THREAD title on each reply so the chunk has a reference. I did not shrink the character window, because a smaller window would still cut a sentence.


## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: thread_bike_commute.txt#0 `` — produced by: chunker.py::split_documents``

```
THREAD: Is a bike worth it for a 20 minute walk commute?

Yeah. Cuts an 18 minute walk to about 6. The thing nobody mentions is storage — covered bike parking exists at three buildings and is full by 9am at all three.
```

**Chunk 2** — source: source: thread_first_year_regret.txt#1 `` — produced by: chunker.py::split_documents``

```
THREAD: Which meal plan tier is right?

Depends entirely on whether your building has a kitchen. Fenwick has kitchenettes, so people there go down a tier and cook two or three nights. Everywhere else, get the middle tier.
```

**Chunk 3** — source: thread_pass_fail.txt#3 `` — produced by: chunker.py::split_documents``

```
THREAD: When should you actually use the pass/fail option?

Two per year and eight across the degree. I hit the annual limit in second year and regretted spending one on an easy course.
```

**Chunk 4** — source: thread_professor_email.txt#1 `` — produced by: chunker.py::split_documents``

```
THREAD: Do professors actually answer email?

Office hours are dramatically more effective than email for anything that takes more than two sentences to answer. They're also usually empty.
```

**Chunk 5** — source: thread_sleep_schedule.txt#1 `` — produced by: chunker.py::split_documents``

```
THREAD: Everyone says fix your sleep. Does it actually matter?

The library being open until 2am is a trap. It's a resource, not a schedule.
```

## Sample Answer

On which mornings is laundry free in every dorm building?"
  (best distance 0.164, cutoff 0.65)

Laundry is free in every building on Tuesday and Wednesday mornings (Source: thread_laundry_timing.txt).

Sources retrieved: thread_commuting.txt, thread_laundry_timing.txt, thread_roommate_conflict.txt


**Question:**

On which mornings is laundry free in every dorm building?"

**Answer:**

```
Laundry is free in every building on Tuesday and Wednesday mornings (Source: thread_laundry_timing.txt).
```

**My relevance cutoff:**
THRESHOLD = 0.65

Two groups of best distances after the reply-boundary index. Questions my documents cover: 0.164, 0.200, 0.272, 0.388, 0.460. Questions from a different world entirely (OUT_OF_SCOPE): 0.819, 0.861, 0.898, 0.899, 0.905. The gap is between 0.460 and 0.819. I put the cutoff at 0.65.

| Question | In corpus? | Best distance |
|---|---|---|
| When do large employers close applications for the following summer? | yes | 0.272 |
| How many black-and-white pages does the $30 printing quota cover? | yes | 0.200 |
| On which mornings is laundry free in every dorm building? | yes | 0.164 |
| How many minutes is the walk from the east parking lot? | yes | 0.388 |
| What do students say happens if you ask for an extension on Wednesday for a Friday deadline? | yes | 0.460 |
| What is the capital of Mongolia? | no | 0.899 |
| How do I change the oil in a diesel engine? | no | 0.905 |
| Who won the 1994 World Cup? | no | 0.898 |
| What is the recommended dosage of ibuprofen for a headache? | no | 0.819 |
| How do I write a for loop in Rust? | no | 0.861 |

## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.** I asked Cursor to help write a chunking function that was compatible with the corpus. What came back first was a smaller character window, but that wasn't what I was looking for, so I requested it split on the `--- reply N ---` markers instead, with overlap 0, and I put the THREAD title on each reply for reference.

**2.** I asked what relevance cutoff to use. The first suggestion was to keep 0.6 which I thought was reasonable. However, I wanted to be sure so I ran all five test questions and all five OUT_OF_SCOPE questions. After looking at the best distances for each I decided to bump it up slightly to 0.65.


<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Week 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     week 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     week — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 |  |  |  |
| 2 |  |  |  |
| 3 |  |  |  |
| 4 |  |  |  |
| 5 |  |  |  |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
