# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1.

<!-- Your criterion. It must name a number. -->
Test-set accuracy is at least 0.65 on all three seeds.


**Why this target:**
A model that ignores the text and always predicts PHYSICAL_WATER_FLOOD already scores 0.38 (86 of 227 posts), so a target like 0.50 would barely beat guessing. I chose 0.65 to require a clear improvement over that baseline. I didn't aim for 0.80 because the DIGITAL_OR_INFORMATION / COMMERCIAL_OR_PLATFORM_SATURATION boundary was hard even for me to label consistently, and with only about 33 test posts per seed, a few mistakes on those cases would be enough to sink a higher target.


---

## 2.

<!-- Your criterion. -->
On all three seeds, per-label F1 on the test set is at least 0.90 for PHYSICAL_WATER_FLOOD, and at least 0.65 for DIGITAL_OR_INFORMATION, COMMERCIAL_OR_PLATFORM_SATURATION, and SOCIAL_OR_ECONOMIC_INFLUX.


**Why this target:**
The labels aren't equally easy, so they get different targets. PHYSICAL_WATER_FLOOD is my largest label (86 posts, about 13 per test split), and its posts usually contain obvious words like rain, river, or hurricane, so I expect it to score high. DIGITAL_OR_INFORMATION and COMMERCIAL_OR_PLATFORM_SATURATION share my hardest boundary, AI content and apps, so I set them lower. COMMERCIAL_OR_PLATFORM_SATURATION and SOCIAL_OR_ECONOMIC_INFLUX are also my smallest labels (about 30 posts, only 4–5 per test split), and one wrong prediction can move their F1 by 0.15 or more.


---

## 3.

<!-- Your criterion. -->
On all three seeds, no more than 20% of the COMMERCIAL_OR_PLATFORM_SATURATION posts in the test set are predicted as DIGITAL_OR_INFORMATION.


**Why this target:**
This is my hardest boundary. With only about 5 COMMERCIAL_OR_PLATFORM_SATURATION posts per test split, each mistake is about 20%, so this allows 1 confusion per seed. I kept it this tight because a looser limit would contradict criterion 2: two confusions would push COMMERCIAL_OR_PLATFORM_SATURATION's recall to about 0.60, which is below its 0.65 F1 target.


---

## 4.

<!-- Your criterion. -->
On at least 30 of my flooding posts labeled independently by course staff using my label definitions, my labels match theirs on at least 70%.


**Why this target:**
With four labels, two people guessing would agree only about 25% of the time, so 70% shows that my definitions do real work. I expect near-total agreement on PHYSICAL_WATER_FLOOD, because its posts name rain, rivers, or storms. I don't set the bar higher because the DIGITAL_OR_INFORMATION / COMMERCIAL_OR_PLATFORM_SATURATION boundary, especially AI-generated books, music, and apps, was hard even for me, and I had to correct several of those labels myself.


---

## 5.

<!-- Your criterion. -->
On all three seeds, accuracy on the most-confident third of test predictions is at least 0.75, and at least 0.20 higher than accuracy on the least-confident third


**Why this target:**
On all three seeds, accuracy on the most-confident third of test predictions is at least 0.75, and at least 0.20 higher than accuracy on the least-confident third.

Why this target:
My overall accuracy target is 0.65, so the predictions the model is surest about should clearly beat that. 0.75 means its confident guesses are right about three times out of four. The 0.20 gap tests whether confidence means anything at all. If the sure and unsure thirds score about the same, I can't use confidence to decide which predictions to double-check. I expect the confident third to be mostly obvious PHYSICAL_WATER_FLOOD posts, and the unsure third to be DIGITAL_OR_INFORMATION / COMMERCIAL_OR_PLATFORM_SATURATION boundary cases.


---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
