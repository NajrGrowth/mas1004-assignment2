# Log

One entry for each recipe, selection or Track B model you train, newest at
the bottom. The numbers come from `experiments.csv`. "Why" and "what it means"
are in your own words: your agent asks you for them and does not make them up.
End the log with your plan for what to try next.

<!-- The form of an entry:

## <date> <tag> (Track A or B)
- changed: what is different from the run before
- why: your reason
- validation: 0.000 (before: 0.000)
- what it means: what you think the result says
-->

## 2026-11-03 baseline (Track A)
- changed: nothing; this is the starting recipe, run twice with seeds 0 and 1
- why: The teacher suggested it. I ran it twice with different seeds to see how much the score changes just by chance, so I know how big a change has to be before it means something. It also gives me a starting score to compare my later changes with.
- validation: 0.4965 (seed 0), 0.4918 (seed 1) (before: none, first run)
- what it means: The model gets about half of the validation photos right (0.4965 and 0.4918). The two seeds differ by about 0.005, so a change that improves the score by less than that could just be luck, and I should only believe a clearly bigger improvement. Per city the scores move even more between the seeds (for example Taipei 0.56 vs 0.51), so I should be careful with conclusions about one city based on a single run. Busan and Osaka are the weakest cities in both runs, and Tokyo is the strongest. I think Tokyo may be recognised more easily because it looks more different from the other cities, and the starter photos show it more clearly, but I have not tested this yet.
