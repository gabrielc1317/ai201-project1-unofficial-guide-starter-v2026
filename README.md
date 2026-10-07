# The Unofficial Guide

<!-- Replace this line with your name and which corpus you picked. -->

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does
I chose the campus_life corpus for this system, this system answers various questions a student who attends/lives at this specific university may have. From the corpus there are 88 documents, which are in the form of posts provided a mix of admin and students. It provides information about courses, workload and expectations, and information regarding situations students may be faced by and gives an understanding of the systems in place at the university regarding topics like enrollement, courses, housing, food, housing, etc. The system refuses to answer questions that ask about topics that are not regarded in any of the documents in the corpus, which is denoted by a cutoff distance of 0.6. Documents are chunked by paragraphs and a max of 450 characters, this allows the chunks to be independent and useful on its own. Each answer provides atleast 1 source document and also include a short verbatim quotation from the cited source so the supporting evidence can be checked directly.

<!-- Three or four sentences. Which corpus you picked, and the kinds of
     questions your system answers. Write it for someone who has never seen
     this repo.

     Milestone 5. -->

## Chunking Strategy

**Chunk size: 450 characters**
**Overlap: 0**
**split boundary: Paragraphs**

Most posts were short, i chose 450 and splitting by paragraphs so that each chunk would be complete thoughts on their own, and be able to provide information without having to rely on another chunk. 
<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: `admin_add_drop_deadline.txt#0` — produced by: `chunker.py::split_documents`

```
On the add/drop deadline

You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.

```

**Chunk 2** — source: `course_biol_160_exams.txt#0` — produced by: `chunker.py::split_documents`

```
BIOL 160 Cell Biology — assessment

Four unit tests and a cumulative final. Not curved.

The unit tests come fast, roughly every three weeks; falling behind once is very hard to recover from.
```

**Chunk 3** — source: `course_math_220_exams.txt#0` — produced by: `chunker.py::split_documents`

```
MATH 220 Linear Algebra — assessment

Two midterms and a cumulative final. Curved to a b- median.

The problem sets are the course; the lectures make sense afterwards rather than during.

```

**Chunk 4** — source: `dining_the_ridgeway_cafe.txt#0` — produced by: `chunker.py::split_documents`

```
The Ridgeway Café

Second-year here. Wait times: 10 to 15 minutes at 12:30, none after 2:00. The thing worth going for is the only place on campus with real espresso. The thing to know is that seating is tight; about 40 seats for a building of 900.

Hours are 7:00am to 4:00pm weekdays only. Costs declining balance only, no meal swipes.
```

**Chunk 5** — source: `housing_morrow_house.txt#0` — produced by: `chunker.py::split_documents`

```
Morrow House — what it's actually like

Just finished a year in this building. Built 1954, partially renovated 2008. Rooms are singles and doubles, hall bathrooms.

The good: cheapest housing tier by about $900 a year, and the singles are real singles.

The bad: known damp problem on the ground floor; two rooms were taken offline in 2024.

For each one, ask: could someone answer a question using only this,
without reading what came before or after?
```

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question: How many hours should I expect to commit to taking Data Structures every week?**

**Answer:**

```
Based on course_cs_210_workload.txt, you should expect to spend 8 to 10 hours a week outside of class. The document states, "People keep asking so: 8 to 10 hours a week outside class."

Sources retrieved: course_cs_210_workload.txt, course_cs_340.txt, course_cs_340_workload.txt, course_engl_205_workload.txt, course_stat_150_workload.txt

```

**My relevance cutoff: 0.6**
There is a clean gap betweeen in scope and out of scope questions, highest in corpus distance being 0.4424 while lowest out of corpus distance being 0.8246, this leaves a median of roughly 6.34.
<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->
| Question | In corpus? | Best distance |
|---|---|---:|
| Is withdrawing from a course the same as dropping it? | Yes | 0.4424 |
| I have 12 courses that are outside of my major I have to take. Can I do Pass/Fail for all of them? | Yes | 0.3504 |
| Will my dining dollars from spring transfer to fall classes? | Yes | 0.3213 |
| How many hours should I expect to commit to taking Data Structures every week? | Yes | 0.3602 |
| How often does the campus shuttle come on weekdays? | Yes | 0.4396 |
| What is the capital of Mongolia? | No | 0.8246 |
| How do I change the oil in a diesel engine? | No | 0.9340 |
| Who won the 1994 World Cup? | No | 0.8859 |
| What is the recommended dosage of ibuprofen for a headache? | No | 0.8442 |
| How do I write a for loop in Rust? | No | 0.8960 |


## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.**
When running the distances for the 5 in corpus questions and 5 out of corpus questions, i found it a bit tedious to run every single one, I asked the ai to build a quick function that i could paste in terminal to run all 10 of them and print the output neatly so that I can then read it.

**2.**
For milestone 4, i needed to put the questions and their distances in a table, from terminal they are in line form. I used AI to aggregate all of that and formulate it into the table format requested for this assignment neatly, while keeping all information unchanged. I checked from terminal to the table that was passted so I could verify that nothing was changed from terminal copy to AI output/reformat.

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->
## Run Log — Before

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1| Retrieved chunks contain the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 2| Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3| Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4| Revised: sampled chunks are independently useful | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 5| Every answer provides a direct quotation | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |


<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

### Real Output — Criterion 1

**Produced by:** `run_eval.py::main` using `store.py::search`

Question: `How many hours should I expect to commit to taking Data Structures every week?`

Best distance: `0.3602`

Sources retrieved:
`course_cs_210_workload.txt`, `course_cs_340.txt`, `course_cs_340_workload.txt`, `course_engl_205_workload.txt`, `course_stat_150_workload.txt`

Output:

> Based on `course_cs_210_workload.txt`, you should expect to commit 8 to 10 hours a week outside of class. The document states, "8 to 10 hours a week outside class."

The retrieved results included `course_cs_210_workload.txt`, which contained the information needed to answer the question.

---

### Real Output — Criterion 2

**Produced by:** `run_eval.py::main` using `generate.py`

Question: `Will my dining dollars from spring transfer to fall classes?`

Output:

> Based on `admin_dining_dollars.txt`, dining dollars do not roll over from the spring semester to the following autumn. The document states, "Whatever is left in May disappears."

The answer explicitly names `admin_dining_dollars.txt` as its source.

---

### Real Output — Criterion 3

**Produced by:** `run_eval.py::check_out_of_scope`

Cutoff: `0.6`

```
What is the capital of Mongolia?                         0.825  refused
How do I change the oil in a diesel engine?             0.934  refused
Who won the 1994 World Cup?                             0.886  refused
What is the recommended dosage of ibuprofen for a headache?  0.844  refused
How do I write a for loop in Rust?                      0.896  refused
```

The relevance gate refused `5 of 5` out-of-corpus questions.

---

### Real Output — Criterion 4

**Produced by:** `chunker.py::split_documents`

One of the sampled chunks:

```
source: housing_morrow_house.txt#1

Laundry costs $1.50 wash, $1.25 dry, coin or card. On noise: loud until about 1am on weekends, no enforced quiet hours.
```

This chunk can independently answer specific questions about laundry cost, payment method, or noise without needing the previous or following chunk.

I reviewed five sampled chunks and found `5 of 5` independently useful under the revised criterion.

---

### Real Output — Criterion 5

**Produced by:** `run_eval.py::main` using `generate.py`

Question: `Is withdrawing from a course the same as dropping it?`

Output:

> No, withdrawing from a course is not the same as dropping it; they are different processes with different dates.

> This information comes from `admin_withdrawal_deadline.txt`, which states: "Withdrawal is a different thing from dropping and has a different date."

The answer includes both the source filename and a direct quotation from the supporting document.

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->


| Criterion | Verdict  | How I decided |
|---|---|---|---|---|---|
| 1 | Retrieved chunks contain the answer | MET | all 3 runs came out 5/5 for correct answer
| 2| Every answer names a source | MET | all 3 runs named a source for each asnwer
| 3| Gate stops out-of-corpus questions | MET | all 3 runs rejected all 5 out of corpus questions.
| 4| Revised: sampled chunks are independently useful | MET | all 3 runs provided 5 chunks that could answer a definitive question
| 5| Every answer provides a direct quotation | MET | all 3 runs provided a direct quote for each answer.

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
