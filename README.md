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
 I used AI for checking my understanding about the repo and asked aobut the labeling my collected post which I did after I label everything by mymyself.
 Also I ask rewrite suff by passing my thought around criteria.  
- *What came back:*
It did label gint and label my post
- *What I changed:*
I verify my and AI's response on the post and revisit in some cases it was wrong and in some cases I was wrong, I corrected my labels. 

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
> Result form python baseline.py
| Measure | Baseline |
|---|---|
| Overall accuracy | 0.314 |
| Macro F1 | 0.120 |
| F1 — `COMMERCIAL_OR_PLATFORM_SATURATION` | 0.000 |
| F1 — `DIGITAL_OR_INFORMATION` | 0.478 |
| F1 — `PHYSICAL_WATER_FLOOD` | 0.000 |
| F1 — `SOCIAL_OR_ECONOMIC_INFLUX` | 0.000 |

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->
> python baseline.py --trained results.json

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy | 0.314 | 0.686 | +0.371 |
| Macro F1 | 0.120 | 0.400 | +0.280 |
| F1 — `COMMERCIAL_OR_PLATFORM_SATURATION` | 0.000 | 0.000 | +0.000 |
| F1 — `DIGITAL_OR_INFORMATION` | 0.478 | 0.786 | +0.307 |
| F1 — `PHYSICAL_WATER_FLOOD` | 0.000 | 0.812 | +0.812 |
| F1 — `SOCIAL_OR_ECONOMIC_INFLUX` | 0.000 | 0.000 | +0.000 |


**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->
Yes, I think trained model's will beat this baseline, as we expected using the example doing the finetunning will in most cases do better.

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->
Fine-tuning is better than the baseline, but only for the two labels with lots of training data. The two rare labels still score 0 because the model never predicts them.


---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

I am making my label shortcut to fit here
COMMERCIAL_OR_PLATFORM_SATURATION: COMM
DIGITAL_OR_INFORMATION: DIG
PHYSICAL_WATER_FLOOD: PHYS
SOCIAL_OR_ECONOMIC_INFLUX: SOC


| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Overall accuracy | ≥ 0.65 on all seeds | 0.686 | 0.714 | 0.686 | Met |
| 2. Per-label F1 | PHYS ≥ 0.90; DIG, COMM, SOC ≥ 0.65 | PHYS 0.812 · DIG 0.786 · COMM 0.000 · SOC 0.000 | PHYS 0.867 · DIG 0.800 · COMM 0.000 · SOC 0.000 | PHYS 0.812 · DIG 0.786 · COMM 0.000 · SOC 0.000 | Missed |
| 3. COMM → DIG confusion | ≤ 20% of COMM posts | 3/5 = 60% | 3/5 = 60% | 4/5 = 80% | Missed |
| 4. Agreement with another person | ≥ 70% on 30 posts | 80% |  | — | Met |
| 5. Confidence | Top third ≥ 0.75 and ≥ 0.20 above bottom third | 1.000 vs 0.364 (gap 0.636) | 0.909 vs 0.273 (gap 0.636) | 1.000 vs 0.182 (gap 0.818) | Met |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted | COMMERCIAL_OR_PLATFORM_SATURATION | DIGITAL_OR_INFORMATION | PHYSICAL_WATER_FLOOD | SOCIAL_OR_ECONOMIC_INFLUX |
|---|---|---|---|---|
| COMMERCIAL_OR_PLATFORM_SATURATION | 0 | 3 | 2 | 0 |
| DIGITAL_OR_INFORMATION | 0 | 11 | 1 | 0 |
| PHYSICAL_WATER_FLOOD | 0 | 0 | 13 | 0 |
| SOCIAL_OR_ECONOMIC_INFLUX | 0 | 2 | 3 | 0 |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->


3 real COMMERCIAL_OR_PLATFORM_SATURATION posts were called DIGITAL_OR_INFORMATION, and 0 went the other way (seed 42). A close second is SOCIAL_OR_ECONOMIC_INFLUX → PHYSICAL_WATER_FLOOD (3, 2 and 4 across seeds, 0 in reverse). The direction matters. The model hasn't learned a COMMERCIAL/DIGITAL boundary at all. It treats COMMERCIAL_OR_PLATFORM_SATURATION as a subset of DIGITAL because both are about apps, platforms and AI content, and DIGITAL has 2.5× more training examples. When a post sits near that line, the model picks the bigger label every time. Likewise, SOCIAL posts ("migrants flooding a city", "children flooding foster homes") are pulled into PHYSICAL, probably by place and crowd words that sound like literal floods. So the errors are one-way: the two small labels get absorbed into their bigger neighbours.
This is also the boundary I flagged as hardest to label myself. I ask one of my friend to label 30 example he score 80% of time and those 20% where also on the same borderline. 



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Overall accuracy | ≥ 0.65 on all 3 seeds | MET | 0.686 / 0.714 / 0.686, all above 0.65 |
| 2 | Per-label F1 | PHYS ≥ 0.90; DIG, COMM, SOC ≥ 0.65 | MISSED | DIG met (0.786–0.800). PHYS 0.812–0.867 < 0.90. COMM and SOC 0.000 on every seed |
| 3 | COMM → DIG confusion | ≤ 20% of COMM posts | MISSED | 3/5, 3/5, 4/5 = 60%, 60%, 80% |
| 4 | Labelling agreement | ≥ 70% | MET (revised criterion) | 28/30 = 93% on the staff set, see revision in criteria.md |
| 5 | Confidence | Top third ≥ 0.75 and ≥ 0.20 above bottom third | MET | Top 1.000 / 0.909 / 1.000; gaps 0.636 / 0.636 / 0.818 |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->

Criterion 2 (per-label F1): too few examples, plus undertraining.COMM and SOC have 22 and 21 training posts against 55–60 for the big two, and
only 5 test posts each. The model never predicts either label on any seed, so
the 0.000s aren't split noise. It is also undertrained: 158 posts ÷ batch 16 ×
3 epochs ≈ 30 updates, and its mean confidence when right is only 0.40–0.47
(chance is 0.25). PHYS misses 0.90 only on precision. Its recall is 13/13 on
every seed, but the rare-label posts get dumped into it.


---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** 28 / 30 = 93%

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
> Three of us ran the same session on the same day, different shoes, within 10 seconds of each other over 5 miles. I'm not saying shoes do nothing, but whatever they do was smaller than the noise between three people.
> *Staff said / I said:*
>analysis/hot_take
> *My call, and why:*
> Three runners, different shoes, within 10 seconds over 5 miles is a named comparison, and the conclusion rests on it. Under rule 1 the fact is load-bearing. Because of the last sentences I selected hot_take but after reviewing I agree that this post should be analysis. 
> *Which pile:*
Pile a 
**2.**
> *The post:*
>Just realised the shoes I set every PB in this year are the ones I bought by accident in the wrong size.
> *Staff said / I said:*
> reaction / hot_take
> *My call, and why:*
>It reports what just happened to the writer, and it doesn't make a general claim about shoes. 

> *Which pile:*
Pile c
**What the pattern in my disagreements tells me:**
I selected hot_take on short, recent posts even when there's a fact or a personal moment underneath.

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
