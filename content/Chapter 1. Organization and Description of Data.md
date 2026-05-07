## First: What do all these terms mean?

| Term                 | Meaning                                             | Simple Example                              |
| -------------------- | --------------------------------------------------- | ------------------------------------------- |
| **Data**             | Raw numbers or facts we collect                     | Ages of 5 students: 18, 19, 18, 20, 22      |
| **Population**       | The *entire* group we care about                    | All 10,000 students at your university      |
| **Sample**           | A smaller piece of the population we actually study | 50 students you surveyed                    |
| **Mean**             | The "average" — add everything up, divide by count  | (2+4+6)÷3 = **4**                           |
| **Median**           | The middle number when data is sorted               | Sorted: 2, 4, **6**, 8, 10 → median = **6** |
| **Mode**             | The number that appears most often                  | 2, 4, 4, 6 → mode = **4**                   |
| **Range**            | Biggest value minus smallest value                  | 2, 5, 9, 12 → range = 12−2 = **10**         |
| **Variance/Std Dev** | How "spread out" the data is                        | We'll see this soon!                        |

---

## 1.1 Introduction: What *is* Statistics?

**Statistics** is just a toolbox for:
1. Collecting data ✓
2. Organizing it ✓
3. Summarizing it ✓
4. Making smart decisions from it ✓

**Two main branches:**

| Type | What it does | Example |
|------|-------------|---------|
| **Descriptive Statistics** | Summarizes *your* data | "The average test score was 78%" |
| **Inferential Statistics** | Uses a sample to guess about the whole population | "Based on 100 voters, we predict the election result" |

> ✓ **Key takeaway**: Descriptive = describe what you *have*. Inferential = infer what you *don't have*.

---

## 1.2 The Mean (The "Average")

The **mean** is what most people call "the average."

\boxed{\text{Sample mean: } \bar{x} = \frac{\sum x_i}{n} \quad \text{Population mean: } \mu = \frac{\sum x_i}{N}}

**How to compute it:**
1. Add up all your numbers
2. Count how many numbers you have
3. Divide step 1 by step 2

**Example**: Find the mean of: 5, 2, 6, 8, 7, 8

| Step | Work | Result |
|------|------|--------|
| Add them up | 5+2+6+8+7+8 | 36 |
| Count them | How many numbers? | 6 |
| Divide | 36 ÷ 6 | **6** |

✓ **Answer**: $\bar{x} = 6$

> ✓ **Tip**: The mean uses *every* number. One weird value (like 100 in a list of 5s) can pull the mean way up or down.

---

## 1.3 The Median (The "Middle")

The **median** is the number right in the middle *after you sort the data*.

**How to find it:**
1. Sort your data from smallest → largest
2. Find the middle position: $\frac{n+1}{2}$
3. Pick that value (or average the two middle ones if you have an even count)

**Example A (odd count)**: Salaries: $240, 310, 320, \boxed{370}, 410, 480, 530$

| Step | Work |
|------|------|
| Sorted? | ✓ Yes |
| Count (n) | 7 |
| Middle position | (7+1)÷2 = **4th** value |
| Median | **$370** ✓ |

**Example B (even count)**: Ages: 17, 18, 18, 19, 19, 20, 21, 22, 22, 23

| Step | Work |
|------|------|
| Count (n) | 10 |
| Middle positions | 5th and 6th values |
| Values | 19 and 20 |
| Median | (19+20)÷2 = **19.5** ✓ |

> ✓ **Why use median?** It ignores extreme values. If one billionaire joins a room of teachers, the *mean* income skyrockets, but the *median* barely moves.

---

## 1.4 The Mode (The "Most Frequent")

The **mode** is simply the value that shows up most often.

**Example**: GPA  3.6, 3.2, 2.8, **3.6**, 3.8, **3.6**, 2.9

| Value | How many times? |
|-------|----------------|
| 2.8 | 1 |
| 2.9 | 1 |
| 3.2 | 1 |
| **3.6** | **3** ← most frequent! |
| 3.8 | 1 |

✓ **Mode = 3.6**

**Important notes**:
| Situation | What happens? |
|-----------|--------------|
| All values appear once | **No mode** |
| Two values tie for most frequent | **Bimodal** (two modes) |
| Data is categories (not numbers) | Mode *still works*; mean/median don't |

> ✓ **Mode is the only measure that works for non-numbers**: "Senior, Junior, **Senior**, Sophomore, **Senior**" → mode = Senior ✓

---

## Comparing Mean, Median, Mode

| Feature | Mean | Median | Mode |
|---------|------|--------|------|
| **Uses all data?** | ✓ Yes | ✗ No | ✗ No |
| **Affected by outliers?** | ✓ Very much | ✗ Barely | ✗ Not at all |
| **Works for categories?** | ✗ No | ✗ No | ✓ Yes |
| **Always exists?** | ✓ Yes | ✓ Yes | ✗ Sometimes no mode |
| **Best for skewed data?** | ✗ No | ✓ Yes | Maybe |

**Real example**: Patient survival days: 3, 15, 46, 64, 126, **623**

| Measure | Value | Why it matters |
|---------|-------|---------------|
| Mean | 146.2 days | Pulled up by that one 623-day survivor |
| Median | 55 days | More "typical" — half survived less, half more |
| Mode | None | All values appear once |

> ✓ **Takeaway**: When data is skewed (lopsided), **median is usually safer** than mean.

---

## 1.5 Measures of Dispersion (How "Spread Out" Is the Data?)

Two datasets can have the *same mean* but look totally different:

| Sample A | Sample B |
|----------|----------|
| 66, 66, 66, 67, 67, 67, 68, 69 | 43, 44, 50, 54, 67, 90, 91, 97 |
| Mean = 67 | Mean = 67 |
| Values clustered tightly | Values spread way out |

That's why we need **dispersion measures**.

---

### 1.5.1 Range (Simplest Spread Measure)

\boxed{\text{Range} = \text{Largest value} - \text{Smallest value}}

**Example**: Data: 13, 23, 11, 17, 25, 18, 14, 24
- Largest = 25, Smallest = 11
- Range = 25 − 11 = **14** ✓

> ✗ **Warning**: Range only uses two numbers. One weird outlier can make it huge.

---

### 1.5.2 Mean Absolute Deviation (MAD)

**Idea**: On average, how far is each number from the mean?

**Steps**:
1. Find the mean ($\bar{x}$)
2. For each value: subtract the mean, take absolute value |x − $\bar{x}$|
3. Average those absolute differences

**Example**: Data: 6, 10, 7, 14, 8

| Step | Work | Result |
|------|------|--------|
| Mean | (6+10+7+14+8)÷5 | $\bar{x}$ = **9** |
| Differences | \|6−9\|=3, \|10−9\|=1, \|7−9\|=2, \|14−9\|=5, \|8−9\|=1 | 3, 1, 2, 5, 1 |
| Sum of absolutes | 3+1+2+5+1 | 12 |
| MAD | 12 ÷ 5 | **2.4** ✓ |

> ✓ **Interpretation**: "On average, values are about 2.4 units away from the mean."

---

### 1.5.3 Variance and Standard Deviation (The Gold Standard)

These are the most important spread measures.

$$\boxed{\text{Sample variance: } s^2 = \frac{\sum (x_i - \bar{x})^2}{n-1} \quad \text{Sample std dev: } s = \sqrt{s^2}}$$

**Why square the differences?**
- Prevents positives/negatives from canceling out
- Gives more weight to big deviations (which is usually what we want)

**Why divide by (n−1) for samples?**
- Makes the estimate "unbiased" — a technical fix so our sample better represents the population ✓

**Worked Example**: Data: 21, 17, 13, 25, 9, 19, 6, 10

| Step | Work | Result |
|------|------|--------|
| **1. Find mean** | (21+17+13+25+9+19+6+10) ÷ 8 | $\bar{x}$ = **15** |
| **2. Differences** | 21−15=6, 17−15=2, 13−15=−2, ... | 6, 2, −2, 10, −6, 4, −9, −5 |
| **3. Square them** | 6²=36, 2²=4, (−2)²=4, ... | 36, 4, 4, 100, 36, 16, 81, 25 |
| **4. Sum squares** | 36+4+4+100+36+16+81+25 | **302** |
| **5. Variance** | 302 ÷ (8−1) = 302÷7 | $s^2$ ≈ **43.14** |
| **6. Std Dev** | √43.14 | $s$ ≈ **6.57** ✓ |

> ✓ **Interpretation**: "Typical values are about 6.6 units away from the mean of 15."

**Shortcut formula** (easier for calculators):
$$\boxed{s^2 = \frac{\sum x_i^2 - \frac{(\sum x_i)^2}{n}}{n-1}}$$

---

### 1.5.4 Interpreting Standard Deviation: Two Rules

#### Chebyshev's Theorem (Works for *any* data) (k ≥ 1)
$$\boxed{\text{At least } \left(1 - \frac{1}{k^2}\right) \times 100\% \text{ of data lies within } k \text{ standard deviations of the mean}}$$

| k (std devs) | Minimum % of data |
| ------------ | ----------------- |
| 1.5          | ≥ 55.6%           |
| 2            | ≥ 75%             |
| 3            | ≥ 88.9%           |

**Example**: Mean = 70, Std Dev = 1.5, k = 3
- Interval: 70 ± 3(1.5) = 70 ± 4.5 → **(65.5, 74.5)**
- ✓ At least 88.9% of values fall between 65.5 and 74.5

#### Empirical Rule (Only for bell-shaped/normal data)
| Distance from Mean | % of Data |
|-------------------|-----------|
| ±1 std dev | ≈ 68% |
| ±2 std devs | ≈ 95% |
| ±3 std devs | ≈ 99.7% |

**Example**: Test scores: Mean = 480, Std Dev = 90 (bell-shaped)
- 68% of scores: 480 ± 90 → **(390, 570)**
- 95% of scores: 480 ± 180 → **(300, 660)** ✓

> ✓ **Key**: Use Empirical Rule *only* if data looks like a bell curve. Otherwise, use Chebyshev.

---

### 1.5.5 Interquartile Range (IQR) — The "Middle 50%"

**Quartiles** split sorted data into 4 equal parts:
- Q₁ = 25th percentile (first quartile)
- Q₂ = 50th percentile = **median**
- Q₃ = 75th percentile (third quartile)

$\boxed{\text{IQR} = Q_3 - Q_1}$

**Why use IQR?** It ignores the top and bottom 25%, so outliers don't mess it up.

**Example**: Test scores (sorted): 2, 3, 5, 6, 8, 10, 12, 15, 18, 20 (n=10)

| Step | Work | Result |
|------|------|--------|
| Position of Q₁ | (10+1)/4 = 2.75 → between 2nd & 3rd values | |
| Q₁ value | 3 + 0.75(5−3) = **4.5** | |
| Position of Q₃ | 3(10+1)/4 = 8.25 → between 8th & 9th values | |
| Q₃ value | 15 + 0.25(18−15) = **15.75** | |
| IQR | 15.75 − 4.5 | **11.25** ✓ |

> ✓ **Interpretation**: The middle 50% of scores span 11.25 points.

---

## 1.6 Numerical Summary of Grouped Data (When Data Has Frequencies)

Sometimes data comes like this:

| Score (x) | Frequency (f) |
|-----------|---------------|
| 0 | 1 |
| 1 | 2 |
| 2 | 6 |
| 3 | 12 |
| 4 | 3 |
| 5 | 1 |
| **Total** | **25** |

This means: one student scored 0, two scored 1, six scored 2, etc.

### 1.6.1 Mean for Grouped Data
$$\boxed{\bar{x} = \frac{\sum (f_i \cdot x_i)}{\sum f_i}}$$

| x | f | f·x |
|---|---|-----|
| 0 | 1 | 0 |
| 1 | 2 | 2 |
| 2 | 6 | 12 |
| 3 | 12 | 36 |
| 4 | 3 | 12 |
| 5 | 1 | 5 |
| | **Σf=25** | **Σfx=67** |

$\bar{x} = 67 ÷ 25 = \boxed{2.68}$ ✓

### 1.6.2–1.6.4 Median, Mode, Variance for Grouped Data
- **Median**: Find which group contains the middle position, then interpolate
- **Mode**: The value with the highest frequency (here: **3**, with f=12)
- **Variance**: Use $\sum f_i(x_i - \bar{x})^2$ in the numerator, divide by n−1

> ✓ **Tip**: Grouped data formulas are *approximations* — we assume all values in a group are at the group's midpoint.

---

## 1.7 Frequency Distributions & Histograms (Organizing Big Data)

When you have lots of raw numbers, group them into **classes**.

**Example**: 50 employee salaries (raw): 405, 510, 520, ..., 560

**Step 1: Find range**
- Min = 300, Max = 880 → Range = 580

**Step 2: Pick class width** (try ~100)
- Classes: 301–400, 401–500, 501–600, 601–700, 701–800, 801–900

**Step 3: Count frequencies**

| Salary Class | Frequency |
|--------------|-----------|
| 301–400 | 4 |
| 401–500 | 8 |
| 501–600 | 16 |
| 601–700 | 10 |
| 701–800 | 7 |
| 801–900 | 5 |

**Histogram**: Bars for each class, height = frequency. Bars touch (because data is continuous).

| Class Limits | Class Boundaries | Midpoint |
|--------------|------------------|----------|
| 301–400 | 300.5–400.5 | 350.5 |
| 401–500 | 400.5–500.5 | 450.5 |

> ✓ **Boundaries** fix gaps: 400.5 is the *real* cutoff between first and second class.

### 1.7.1 "Less Than" Method
Instead of "301–400", write:
- 301 to <400
- 401 to <500
- etc.

Better for data with decimals (e.g., wages like $12.25).

---

## 1.8–1.12: Mean, Median, Mode, Variance for *Grouped* Data
![[Grouped data operations.pdf]]

When data is already in classes (like the salary table above), use these formulas:

### Mean for Grouped Data
$$\boxed{\bar{x} \approx \frac{\sum (f_i \cdot m_i)}{\sum f_i}}$$
where $m_i$ = midpoint of class i

### Median for Grouped Data
$$\boxed{\text{Median} = L + \left(\frac{\frac{n}{2} - F}{f_m}\right) \cdot c}$$
- L = lower boundary of median class
- n = total frequency
- F = cumulative frequency *before* median class
- fₘ = frequency *of* median class
- c = class width

### Mode for Grouped Data = Modal Class
The class with the highest frequency. Sometimes use its midpoint as the mode estimate.

### Variance for Grouped Data
$\boxed{s^2 \approx \frac{\sum f_i(m_i - \bar{x})^2}{n-1}}$

> In statistics, unless a dataset is explicitly defined as the entire population, it is standard practice to calculate the **Sample Variance**, which divides by n−1.
### IQR for Grouped Data
Find Q₁ and Q₃ using the median formula, then IQR = Q₃ − Q₁.
> **Remember**: IQR is similar to median, but we subtract 0.5 from numerator in the formula.

---

## 🧠 Summary: Chapter 1 in One Place

| Concept | Formula / Idea | When to Use |
|---------|---------------|-------------|
| **Mean** | $\bar{x} = \frac{\sum x}{n}$ | Data is symmetric, no extreme outliers |
| **Median** | Middle value (sorted) | Data is skewed or has outliers |
| **Mode** | Most frequent value | Categorical data, or finding "typical" category |
| **Range** | Max − Min | Quick, rough sense of spread |
| **MAD** | Avg of \|x − mean\| | Simple spread measure (less common) |
| **Variance** | $s^2 = \frac{\sum (x-\bar{x})^2}{n-1}$ | Foundation for advanced stats |
| **Std Dev** | $s = \sqrt{s^2}$ | Most common spread measure (same units as data) |
| **IQR** | Q₃ − Q₁ | Spread of middle 50%; robust to outliers |
| **Grouped Mean** | $\frac{\sum f \cdot m}{\sum f}$ | Data already in frequency table |
| **Histogram** | Bars for classes | Visualize distribution shape |

**Key Rules**:
$$\boxed{\text{Chebyshev: } \ge \left(1-\frac{1}{k^2}\right)\times100\% \text{ within } k \text{ std devs (any data)}}$$
$$\boxed{\text{Empirical: } \approx 68\%/95\%/99.7\% \text{ within 1/2/3 std devs (bell-shaped only)}}$$

---

## ✅ How to Solve / Understand Any Problem in This Topic

1. **Identify the data type**:
   - ✓ Raw numbers? → Use ungrouped formulas
   - ✓ Already in a frequency table? → Use grouped formulas
   - ✓ Categories (not numbers)? → Only mode works

2. **Decide: Center or Spread?**
   - Center → Mean, Median, or Mode (use comparison table above)
   - Spread → Range, IQR, or Std Dev (IQR for skewed data)

3. **Check for outliers or skew**:
   - ✓ If skewed/outliers present → Prefer **median** and **IQR**
   - ✓ If symmetric → Mean and std dev are fine

4. **For grouped data**:
   - ✓ Always use class *midpoints* in calculations
   - ✓ Remember: results are *approximations*

5. **When interpreting std dev**:
   - ✓ Bell-shaped? → Use Empirical Rule (68-95-99.7)
   - ✓ Not sure? → Use Chebyshev (always safe, but conservative)

6. **Final verification checklist**:
   - ✓ Did I sort the data before finding median/Q₁/Q₃?
   - ✓ For sample std dev, did I divide by **n−1** (not n)?
   - ✓ For grouped data, did I use frequencies correctly?
   - ✓ Does my answer make sense? (e.g., std dev can't be negative)

> **Bold takeaway**: **There's no single "best" measure**. The right choice depends on your data's shape and your question. When in doubt, report *both* mean/median and std dev/IQR — that tells the full story. ✓