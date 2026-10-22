# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->
Community: Hacker News posts that use the word "flooding." On HN the word
rarely means water. It more often describes a market, a platform, or an
information space being overwhelmed. My classifier sorts each post by which
sense of "flooding" it uses: `PHYSICAL_WATER_FLOOD` (Actual water flooding, extreme rain, coastal flooding, or flood events), `COMMERCIAL_OR_PLATFORM_SATURATION` (Too many products, apps, ads, or commercial listings on a platform or market), `SOCIAL_OR_ECONOMIC_INFLUX` (a surge of people,
money, labor, investors, or applications), and `DIGITAL_OR_INFORMATION` (Disinformation, spam, bots, scams, fake content, or online systems being overwhelmed)


---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `PHYSICAL_WATER_FLOOD`

**Definition:**
A post describing water overflowing, covering, or inundating land or places, usually because of heavy rainfall, rivers, storms, coastal surges, or other water-related events. Includes actual flooding, flood warnings, and predictions of flooding.
**Example 1:**
> Flooding of US Coast, Caused by Global Warming, Has Begun 

**Example 2:**
> China's Three Gorges Dam could collapse (flooding 400M)

### `COMMERCIAL_OR_PLATFORM_SATURATION`

**Definition:**
A post describing a large quantity of products, advertisements, listings, or commercial content entering a marketplace or online platform, potentially overwhelming users, reducing quality, or making it difficult to find legitimate products.

**Example 1:**
> Cheap junk flooding Amazon has brand names like MOFFBUZW 
**Example 2:**
> Meta Is Flooding the Market with Smartglasses. Privacy Advocates Are Up in Arms 

### `SOCIAL_OR_ECONOMIC_INFLUX`

**Definition:**
A post describing a large or sudden increase in people, workers, migrants, investors, money, applications, or other social or economic activity entering a place, organization, or system, often with an emphasis on its effects or perceived burden.
**Example 1:**
> AI note takers are flooding Zoom calls as workers opt to skip meetings 

**Example 2:**
> Money Flooding Out of Canada at Fastest Pace in Developed World 

### `DIGITAL_OR_INFORMATION`

**Definition:**
A post describing a large or overwhelming amount of digital content or information being distributed, such as disinformation, misinformation, spam, bots, fake news, or online messages. The term “flooding” is used metaphorically to describe the spread or volume of information.

**Example 1:**
> China is flooding Taiwan with disinformation 

**Example 2:**
> Please stop flooding our projects with AI slop to furnish your CV 

### The hardest boundary

**Which two labels:**
DIGITAL_OR_INFORMATION and COMMERCIAL_OR_PLATFORM_SATURATION

**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->
Those two are the hardest boundary since for example if the post contains something like amazon, products, ads, or disinformation. My decision rule is label the post according to what is being flooded: information/content or commercial products/listings. 

---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**
The collection of posts comes from Hacker News using (https://hn.algolia.com/api/v1/search). 

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->

Actually I went and labelled all the post manually first and then use AI to double check, when there was mismatch I look at it carefully. In majority of cases both AI and my lables matched but In some instant AI was incorrectly labeling it and in some instant I did label incorrectly. I double check it and individual which were different. 

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| COMMERCIAL_OR_PLATFORM_SATURATION | 32 | 14.09 |
| SOCIAL_OR_ECONOMIC_INFLUX | 30 | 13.21 |
| PHYSICAL_WATER_FLOOD | 86 | 37.88 |
| DIGITAL_OR_INFORMATION | 79 | 34.81 |
| **Total** |  | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:*
> The dangerous trend of inexperienced individuals flooding the tech market As the demand for technology continues to grow, so does the influx of people entering the tech field. However, this surge in interest has also led to a saturation of the market with individuals who may not have the necessary skills and experience to excel in the field.<p>In recent years, we&#x27;ve seen a rise in the number of people who have no prior experience in technology but claim to be experts in the field after completing a short course in a specific technology. These so-called &quot;experts&quot; are often referred to as &quot;cloud-washed&quot; or &quot;bootcamp graduates&quot; and lack the depth of knowledge and understanding that comes with years of experience.<p>Additionally, we&#x27;re seeing a trend of people calling themselves &quot;data scientists&quot; after completing a three-week course in Python. These individuals may have a basic understanding of the language, but they do not have the necessary skills and experience to truly be considered data scientists.<p>The tech field is not for everyone, and it&#x27;s important for individuals to carefully consider their skills and experience before entering the market. It&#x27;s also crucial for companies to properly vet candidates and ensure that they have the necessary experience and expertise to succeed in their roles.<p>In short, the tech field may be saturated with inexperienced individuals, but that doesn&#x27;t mean it&#x27;s not a worthwhile pursuit for those with the skills and experience to excel. It&#x27;s important to do your research and carefully consider your options before entering the market.
> *Could have been:*
> COMMERCIAL_OR_PLATFORM_SATURATION
> *I chose, because:*
SOCIAL_OR_ECONOMIC_INFLUX
Beside other things it states people entering job market
**2.**
> *The post:*
> Stop flooding us with AI-based grant applications, begs NIH 
> *Could have been:*
> COMMERCIAL_OR_PLATFORM_SATURATION
> *I chose, because:*
DIGITAL_OR_INFORMATION
Because AI-generated volume

**3.**
> *The post:*
>People are flooding AI chatbots with health questions. Microsoft Mayo Clinic 
> *Could have been:*
>DIGITAL_OR_INFORMATION
> *I chose, because:*
SOCIAL_OR_ECONOMIC_INFLUX, 
because people's surge of questions is the boarderline. 
---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**
Model: distilbert-base-uncased
Device used was device: mps  (Apple Silicon GPU (MPS))
torch:  2.14.1

**Settings:** <!-- epochs, learning rate, batch size, seed -->
I did not change these:
EPOCHS = 3
LEARNING_RATE = 2e-5
BATCH_SIZE = 16
SEED = 42

**Anything I changed from the defaults, and why:**
No, I did not change anything for the default value.

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->
For training: 
COMMERCIAL_OR_PLATFORM_SATURATION 22
DIGITAL_OR_INFORMATION 55
PHYSICAL_WATER_FLOOD 60
SOCIAL_OR_ECONOMIC_INFLUX 21

For Validation:
COMMERCIAL_OR_PLATFORM_SATURATION 5
DIGITAL_OR_INFORMATION 12
PHYSICAL_WATER_FLOOD 13
SOCIAL_OR_ECONOMIC_INFLUX 4

For test
COMMERCIAL_OR_PLATFORM_SATURATION 5
DIGITAL_OR_INFORMATION 12
PHYSICAL_WATER_FLOOD 13
SOCIAL_OR_ECONOMIC_INFLUX 5


---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
