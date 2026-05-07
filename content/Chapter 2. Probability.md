## First: What do all these terms mean?

| Term | Meaning | Example |
|------|---------|---------|
| **Random experiment** | A process with uncertain results that you can repeat | Tossing a coin, rolling a die |
| **Outcome** | One possible result of an experiment | Getting "Heads" on a coin toss |
| **Sample space (S)** | The complete list of ALL possible outcomes | For a coin: S = {Heads, Tails} |
| **Event** | A collection of one or more outcomes | "Getting an even number" when rolling a die = {2, 4, 6} |
| **Probability P(A)** | A number between 0 and 1 telling how likely event A is | P(Heads) = 0.5 means 50% chance |
| **Mutually exclusive** | Two events that cannot happen at the same time | Getting Heads AND Tails on one coin toss — impossible! |
| **Independent events** | One event doesn't affect the chance of the other | Tossing a coin twice: first toss doesn't change second toss |

---

## 2.1. Introduction

Probability is just a way to talk about **uncertainty** using numbers. Instead of saying "it might rain," we say "there's a 70% chance of rain."

> ✓ **Key idea**: Probability helps us make smarter decisions when we don't know what will happen next.

---

## 2.2. Random Experiment, Outcomes, and Sample Space

### Definitions with immediate examples:

🔹 **Random experiment**: Any process where the result is uncertain but you can list what *could* happen.

> Example: Rolling a six-sided die. You don't know the result, but you know it must be 1, 2, 3, 4, 5, or 6.

🔹 **Outcome**: One specific result.

> Example: Rolling a "4" is one outcome.

🔹 **Sample space (S)**: The complete menu of all possible outcomes.

> Example: For one die roll: \boxed{S = \{1, 2, 3, 4, 5, 6\}}

🔹 **Event**: Any group of outcomes you care about.

> Example: "Rolling an even number" = {2, 4, 6}. This is an event.

### Quick comparison table:

| Concept | What it is | Coin Toss Example | Die Roll Example |
|---------|-----------|------------------|----------------|
| Experiment | The action | Toss once | Roll once |
| Outcome | One result | Heads | 3 |
| Sample Space | All results | {H, T} | {1,2,3,4,5,6} |
| Event | What you're watching for | "Get Heads" | "Get odd number" = {1,3,5} |

---

## 2.3. Three Ways to Think About Probability

### 2.3.1. Classical Probability (The "Fair Game" Method)

$$\boxed{P(A) = \frac{\text{Number of outcomes that make A happen}}{\text{Total number of possible outcomes}}}$$

> Example: What's the chance of rolling a 5 on a fair die?
> - Outcomes that work: {5} → 1 outcome
> - Total outcomes: {1,2,3,4,5,6} → 6 outcomes
> - $\boxed{P(5) = \frac{1}{6} \approx 0.167}$

### 2.3.2. Relative Frequency (The "Let's Test It" Method)

$$\boxed{P(A) \approx \frac{\text{Times A happened}}{\text{Total times we tried}}}$$

> Example: You flip a coin 100 times and get Heads 48 times.
> - $\boxed{P(\text{Heads}) \approx \frac{48}{100} = 0.48}$
> - ✓ The more you test, the closer you get to the true probability!

### 2.3.3. Subjective Probability (The "Expert Guess" Method)

This is when you use experience, not math, to estimate chance.

> Example: A doctor says, "Based on my experience, there's a 40% chance this treatment will work."

### Comparison Table:

| Method | When to Use | Pros | Cons |
|--------|------------|------|------|
| **Classical** | Fair games, cards, dice | Exact, simple | Only works when all outcomes are equally likely |
| **Relative Frequency** | Real-world data, experiments | Based on actual results | Needs lots of data; can change with more testing |
| **Subjective** | Unique situations, expert opinion | Flexible, practical | Depends on the person; not repeatable |

---

## 2.4. Probability Postulates (The Rules Probability Must Follow)

These are the "laws" all probabilities obey:

$\boxed{0 \leq P(A) \leq 1}$
> ✓ Probability is always between 0 (impossible) and 1 (certain).

$\boxed{P(S) = 1}$
> ✓ The chance that *something* in the sample space happens is 100%.

$\boxed{\text{If A and B can't happen together: } P(A \text{ or } B) = P(A) + P(B)}$
> ✓ For mutually exclusive events, just add the probabilities.

> Example: Rolling a die. P(rolling a 1) = 1/6, P(rolling a 2) = 1/6.
> Since you can't roll both at once: $\boxed{P(1 \text{ or } 2) = \frac{1}{6} + \frac{1}{6} = \frac{1}{3}}$

---

## 2.5. Classical Probability Formula (Again, Because It's Important!)

$\boxed{P(A) = \frac{n(A)}{n(S)}}$

Where:
- n(A) = number of outcomes in event A
- n(S) = total outcomes in sample space

> Example: Drawing one card from a standard 52-card deck. What's P(drawing a Queen)?
> - Queens in deck: 4 → n(A) = 4
> - Total cards: 52 → n(S) = 52
> - $\boxed{P(\text{Queen}) = \frac{4}{52} = \frac{1}{13} \approx 0.077}$

---

## 2.6. Consequences of the Postulates (Useful Shortcuts)

### Addition Rule for Mutually Exclusive Events:

$\boxed{P(A \cup B) = P(A) + P(B) \quad \text{(when A and B can't both happen)}}$

> Example: In a drawer: 3 red sock pairs, 2 black, 4 brown (9 total).
> P(black) = 2/9, P(brown) = 4/9
> $\boxed{P(\text{black or brown}) = \frac{2}{9} + \frac{4}{9} = \frac{6}{9} = \frac{2}{3}}$

### General Addition Rule (when events CAN overlap):

$\boxed{P(A \cup B) = P(A) + P(B) - P(A \cap B)}$

> Why subtract? Because if A and B overlap, we counted the overlap twice!

---

## 2.7. Counting Principle, Permutation, and Combination

### 2.7.1. Permutation (Order MATTERS)

$\boxed{_nP_r = \frac{n!}{(n-r)!}}$

> Example: 3 friends (Ana, Ben, Cal) line up for a photo. How many orders?
> - n = 3 people, r = 3 spots
> - $\boxed{_3P_3 = \frac{3!}{(3-3)!} = \frac{6}{1} = 6}$ orders
> - List them: ABC, ACB, BAC, BCA, CAB, CBA ✓

### 2.7.2. Combination (Order DOESN'T Matter)

$\boxed{_nC_r = \frac{n!}{r!(n-r)!}}$

> Example: Same 3 friends. How many ways to pick a 2-person committee?
> - Order doesn't matter: {Ana, Ben} is same as {Ben, Ana}
> - $\boxed{_3C_2 = \frac{3!}{2!(3-2)!} = \frac{6}{2 \cdot 1} = 3}$ committees
> - List them: {A,B}, {A,C}, {B,C} ✓

### Permutation vs. Combination — Quick Guide:

| Question to Ask | If YES → Use | If NO → Use |
|----------------|--------------|-------------|
| Does the ORDER of selection matter? | Permutation | Combination |
| Example: "Who gets 1st, 2nd, 3rd place?" | ✓ Permutation | |
| Example: "Pick 3 people for a team" | | ✓ Combination |

---

## 2.8. Probability Rules

### 2.8.1. Conditional Probability

$\boxed{P(A|B) = \frac{P(A \cap B)}{P(B)}}$

Read as: "Probability of A GIVEN THAT B already happened"

> Example: Box has 3 black chips, 2 white. Pick two without replacement.
> Given first was black, what's P(second is white)?
> - After picking 1 black: 2 black, 2 white remain (4 total)
> - $\boxed{P(\text{White}|\text{First was Black}) = \frac{2}{4} = 0.5}$

### 2.8.2. Multiplication Rule

$\boxed{P(A \cap B) = P(A) \cdot P(B|A)}$

> Example: Same box. P(First black AND second white)?
> - P(First black) = 3/5
> - P(Second white | First black) = 2/4 = 1/2
> -$\boxed{P(\text{Black then White}) = \frac{3}{5} \cdot \frac{1}{2} = \frac{3}{10} = 0.3}$

### 2.8.3. Multiplication Rule for INDEPENDENT Events

$\boxed{\text{If A and B independent: } P(A \cap B) = P(A) \cdot P(B)}$

> Example: Flip a fair coin twice. P(Heads both times)?
> - Tosses don't affect each other → independent
> - $\boxed{P(H \text{ and } H) = 0.5 \cdot 0.5 = 0.25}$

### 2.8.4. Law of Total Probability

$\boxed{P(A) = P(A|B_1)P(B_1) + P(A|B_2)P(B_2) + \dots}$

> Use when event A can happen through different "paths" (B₁, B₂, …)

> Example: 70% of students are freshmen (F), 30% are seniors (S).
> P(pass exam | F) = 0.6, P(pass | S) = 0.9
> What's overall P(pass)?
> $\boxed{P(\text{pass}) = (0.6)(0.7) + (0.9)(0.3) = 0.42 + 0.27 = 0.69}$

---

## 2.9. Bayes' Theorem (Updating Beliefs with New Evidence)

$\boxed{P(B|A) = \frac{P(A|B) \cdot P(B)}{P(A)}}$

> This flips conditional probability: from "P(A if B)" to "P(B if A)"

### 🎯 FULL WORKED EXAMPLE (Tiny Numbers, Every Step):

**Scenario**: A disease affects 1% of people. A test is 95% accurate:
- If you HAVE the disease, test says "positive" 95% of the time
- If you DON'T have it, test says "negative" 95% of the time (so 5% false positive)

**Question**: You test positive. What's the chance you actually have the disease?

**Step 1: Define events**
- D = has disease, ~D = no disease
- + = test positive, - = test negative

**Step 2: Write what we know**
- P(D) = 0.01 (1% have disease)
- P(+|D) = 0.95 (test catches disease 95% of time)
- P(+|~D) = 0.05 (false positive rate)

**Step 3: Find P(+) using Law of Total Probability**
$\boxed{P(+) = P(+|D)P(D) + P(+|~D)P(~D)}$
= (0.95)(0.01) + (0.05)(0.99)
= 0.0095 + 0.0495 = 0.059

**Step 4: Apply Bayes' Theorem**
$\boxed{P(D|+) = \frac{P(+|D) \cdot P(D)}{P(+)}}$
= $\frac{(0.95)(0.01)}{0.059} = \frac{0.0095}{0.059} ≈ 0.161$

**Answer**: Even with a positive test, there's only about a **16% chance** you have the disease! ✓

> ✓ **Key takeaway**: Rare diseases + imperfect tests = many false alarms. Bayes helps you think clearly.

---

## 2.10. Joint and Marginal Probabilities (Two-Way Tables)

### Definitions:
- **Joint probability**: P(A and B) — chance both happen together
- **Marginal probability**: P(A) alone — found by adding across a row or column

### Example Table (420 employees surveyed):

| | University Grad | Not Grad | **Total** |
|---|----------------|----------|-----------|
| **Smoker** | 35 | 130 | **165** |
| **Non-smoker** | 80 | 175 | **255** |
| **Total** | **115** | **305** | **420** |

- Joint: P(Smoker AND Grad) = 35/420 ≈ 0.083
- Marginal: P(Smoker) = 165/420 ≈ 0.393 (add the row)
- Marginal: P(Grad) = 115/420 ≈ 0.274 (add the column)

### Conditional from the table:
$$\boxed{P(\text{Grad}|\text{Smoker}) = \frac{P(\text{Grad and Smoker})}{P(\text{Smoker})} = \frac{35/420}{165/420} = \frac{35}{165} ≈ 0.212}$$

> ✓ Among smokers, only ~21% are graduates.

---

## 📋 SUMMARY: Chapter 2 in One Place

| Concept                                | Formula / Rule                                    |             When to Use              |
| -------------------------------------- | ------------------------------------------------- | :----------------------------------: |
| **Classical Probability**              | $\boxed{P(A) = \frac{n(A)}{n(S)}}$                | Fair games, equally likely outcomes  |
| **Addition Rule (mutually exclusive)** | $\boxed{P(A \cup B) = P(A) + P(B)}$               |     Events can't happen together     |
| **General Addition Rule**              | $\boxed{P(A \cup B) = P(A) + P(B) - P(A \cap B)}$ |         Events might overlap         |
| **Conditional Probability**            | $\boxed{P(A\|B) = \frac{P(A \cap B)}{P(B)}}$      |  You know B happened; what about A?  |
| **Multiplication Rule**                | $\boxed{P(A \cap B) = P(A) \cdot P(B\|A)}$        |    Finding "A and B" in sequence     |
| **Independent Events**                 | $\boxed{P(A \cap B) = P(A) \cdot P(B)}$           |  One event doesn't affect the other  |
| **Bayes' Theorem**                     | $\boxed{P(B\|A) = \frac{P(A\|B)P(B)}{P(A)}}$      |  Updating beliefs with new evidence  |
| **Permutation**                        | $\boxed{_nP_r = \frac{n!}{(n-r)!}}$               |   Order matters (ranks, sequences)   |
| **Combination**                        | $\boxed{_nC_r = \frac{n!}{r!(n-r)!}}$             | Order doesn't matter (teams, groups) |

**Bold Takeaways**:
- **Probability is always between 0 and 1**.
- **"Or" usually means ADD (but subtract overlap)**.
- **"And" usually means MULTIPLY (but check independence!)**.
- **Bayes' Theorem flips the condition: P(A|B) ↔ P(B|A)**.
- **Permutation = order matters; Combination = order doesn't**.

✓ **Verification tip**: If your probability is <0 or >1, you made a mistake!

---

## 🛠️ How to Solve / Understand Any Problem in This Topic

1. **Identify the experiment**: What are we doing? (Roll die? Draw card? Survey people?)
2. **List the sample space S**: What are ALL possible outcomes?
3. **Define the event A**: What specific outcome(s) are we looking for?
4. **Check the method**:
   - Equally likely outcomes? → Use **Classical** formula
   - Have real data? → Use **Relative Frequency**
   - Expert opinion only? → Use **Subjective**
5. **Check for overlap**:
   - "A or B"? → Use Addition Rule (subtract overlap if needed)
   - "A and B"? → Use Multiplication Rule (check independence first!)
6. **Given new info?** → Use **Conditional Probability** or **Bayes' Theorem**
7. **Counting outcomes?** → Ask: "Does order matter?" → Permutation or Combination
8. **Two-way table?** → Joint = cell/total; Marginal = row or column total/total
9. **Calculate** using the boxed formulas above
10. **Verify**: Is your answer between 0 and 1? Does it make intuitive sense? ✓

> 💡 **Pro tip**: Draw a picture (Venn diagram, tree diagram, or table) — it makes everything clearer!

---

**You now have the toolkit for Chapter 2!** Start with tiny examples, verify each step, and remember: probability is just organized common sense with numbers. 🎲📊