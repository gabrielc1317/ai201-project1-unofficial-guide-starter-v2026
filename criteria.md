# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
For the corpus I chose (Campus_life). the documents are straight foward and many documents reinforce eachother, in a way establishing more concrete information to be retrieved. A minimum 80% success rate I feel is appropiate for this type of corpus

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
Answers should be determinstic and grounded in concrete evidence, to avoid any type of AI hallucination, there should be atleast one source document per answer, so that each answer can be reviewed by the objective data that it presents along with its answer (source document).

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
The documents in this corpus are realtively short and straightforward, when an out of scope question is inputted, 
I feel atleast 80% of the time it should be able to reject the question citing not enough information available. 
it could be complicated for it to 100% of the time reject every out of scope question, but 3 out of 5 is it a bit 
too forgiving for a system like this with this type of corpus.
<!-- What did your distances look like when you set the cutoff in Milestone 4?
     Was there a clean gap, or did the two groups overlap? -->

---

## 4. Something about your chunks

<!-- YOU WRITE THIS ONE.

     How would you know if your chunks were the right size? Name something
     countable or observable.

     Examples of the right shape — don't copy these, they should come from
     what you actually saw in Milestone 3:
       - "At least 4 of 5 sampled chunks read as a complete thought, with no
          sentence cut in half at either end."
       - "No chunk is shorter than 200 characters, since anything below that
          in my corpus turned out to be a heading with no content under it." -->
Chunks should contain enough context/information to be useful on its own. Chunks should be able to reinforce eachother
when there is overlapping information in the same context.

**Why this target:**
Most documents are very short, there were 88 documents and 88 chunks as a result with an average of 317 characters. 
Since most documents are straightforward, Each chunk should be informative on its own rather then depending on another chunk
for extra context. In my practice question, one chunk had enough info to answer the question, and a few other chunks
were retrieved that independently reinforced the answer.

 **Revised in unit 2:** Atleast 4 out of 5 sampled chunks should contain enough information to answer a specific question
 on its own without requiring the chunk around it.
         
         **Why revised:** My first critierion was what I wanted from my chunks, but it did not define how many chunks 
         should meet that standard, it wasn't a quantifiable criterion, so I couldn't give it a met or missed verdict.
         this new version keeps the same standard but makes it quantifiable and testable.


---

## 5. Your choice (Answer provides direct verifiable evidence)

<!-- YOU WRITE THIS ONE TOO.


     Pick something you actually care about getting right. It could be about
     speed, about refusals, about a particular kind of question your corpus
     handles badly, about source attribution being correct rather than merely
     present — anything, as long as it names a number or an observable
     outcome. -->
Eachh answer should provide a direct quotation (practically short) from the provided source chunk(s) that shows 
where the answer came from.


**Why this target:**
To make the answering as determinstic as possible, i feel it is neccesary to provide a direct quotation in the answer
from the provided source chunk(s), that shows exactly what information from the source was used to conjour the answer.


---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
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
