# Do Women's World Cup Matches Have More Goals Than Men's?

A hypothesis testing project comparing the average number of goals per match in men's and women's official FIFA World Cup matches since 2002.

## Question

Is the mean number of goals scored in women's FIFA World Cup matches the same as in men's?

- **Null hypothesis (H0):** The mean goals per match is the same for men's and women's World Cup matches.
- **Alternative hypothesis (H1):** The mean goals per match is different (two-sided).
- **Significance level:** 10% (alpha = 0.10)

## Data

- **Files:** `men_results.csv` and `women_results.csv` <!-- TODO: replace with your actual file names -->
- **Source:** <!-- TODO: where did the data come from? -->
- **Columns:** `date`, `home_team`, `away_team`, `home_score`, `away_score`, `tournament`
- **Scope used:** Matches where `tournament == "FIFA World Cup"` and `date >= 2002-01-01`

| Group | Matches | Mean goals per match |
|-------|---------|----------------------|
| Men's | 384 | 2.51 |
| Women's | 200 | 2.98 |

## Method

1. Converted `date` to datetime in both datasets.
2. Filtered each dataset to official FIFA World Cup matches on or after 2002-01-01 (exact match on the tournament name, so qualifiers are excluded).
3. Created a `total_goals` column (`home_score + away_score`) for each match.
4. Explored the distribution of `total_goals` for each group with histograms.
5. Ran a **two-sided Welch's t-test** using `pingouin`.

### Why this test?

- **Dependent variable:** `total_goals` (numeric).
- **Independent variable:** men's vs. women's matches (two independent groups).
- **Why a t-test:** The hypothesis is about means, and the two samples are fairly large.
- **Why Welch's:** The groups differ in size and spread, so equal variances are not assumed.
- **Why two-sided:** The null says the means are "the same" and no direction was specified in advance.
- **Assumption:** Each match is treated as independent (team form is ignored).

## Results

| Statistic | Value |
|-----------|-------|
| t | 2.81 |
| Degrees of freedom | 340.1 |
| p-value | 0.0052 |
| 95% CI of the difference | [0.14, 0.79] |
| Cohen's d | 0.26 |

```python
result_dict = {"p_val": 0.005196, "result": "reject"}
```

## Conclusion

Since the p-value (0.0052) is below the 10% significance level, we **reject** the null hypothesis. There is statistically significant evidence that the mean goals per match differs between men's and women's World Cup matches since 2002, with women's matches averaging about 0.47 more goals per match. The effect size is small (Cohen's d of about 0.26).


## How to Run

```bash
git clone https://github.com/Aayubb/<your-repo-name>.git
cd <your-repo-name>
pip install pandas numpy matplotlib pingouin
jupyter notebook
```

Then open `notebook.ipynb` and run all cells.


## Tools

Python, pandas, NumPy, Matplotlib, pingouin
