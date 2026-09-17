# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in week 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next week costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
I picked 4 of 5 because one of my questions sits in a thread that does not
agree with itself. Large employers close in October. Smaller places hire
in February. If search brings back the wrong reply, that question misses
even when it found the right thread. 5 of 5 would pretend these threads
are cleaner than they are. Another thing: 3 of 5 would let a second miss
slide, and I do not want that.

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
I went with all 5 because the prompt already tells the model to name the
file. This unofficial guide is only useful if you can open that thread.
4 of 5 would treat a missing citation as fine. The thing that has to go
wrong is the model ignoring the instruction. That is a real miss. It is
not something I am planning around.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:**
The five out-of-scope questions are from a different world than these
advice threads. Capitals, engine oil, the World Cup. I think there should
be a clean gap. However, 5 of 5 would assume the embedder never
accidentally pulls a campus thread close to an unrelated question. 4 of 5
leaves room for one weird near miss without treating the gate as optional.

---

## 4. Something about your chunks

At least 4 of 5 chunks printed by `python app.py chunks -n 5` contain a
complete sentence that is not cut at either end. None of those five is
shorter than 40 characters.

**Why this target:**
These threads are 2 to 4 short replies. They run about 500 characters on
average. An 800-character window will either swallow a whole thread or
leave a tiny leftover at the end. A 2-character tail is not a thought. A
sentence cut in half cannot answer a question on its own. I said 4 of 5
because one sample might be a thread title plus the start of reply 1.

---

## 5. Your choice

For all 5 test questions, if the system answers (does not refuse), the
document it names is the thread that actually contains the expected fact.

**Why this target:**
Criterion 2 only checks that a source is named. Fenwick, the library, and
December show up in more than one thread. A confident answer can cite the
wrong file and still look cited. I think a wrong thread is worse than no
citation. That is the failure this corpus invites.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     WEEK 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in week 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
