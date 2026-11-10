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
- what it means: On average over the five cities, the model gets about half of each city's validation photos right (0.4965 and 0.4918). The two seeds differ by about 0.005, so a change that improves the score by less than that could just be luck, and I should only believe a clearly bigger improvement. Per city the scores move even more between the seeds (for example Taipei 0.56 vs 0.51), so I should be careful with conclusions about one city based on a single run. Busan and Osaka are the weakest cities in both runs, and Tokyo is the strongest. I think Tokyo may be recognised more easily because it looks more different from the other cities, and the starter photos show it more clearly, but I have not tested this yet.

## 2026-11-06 balanced (Track A)
- changed: sample_weights draws every city equally often (each photo gets 1 / the number of photos of its city), instead of every photo once per round
- why: Busan and Osaka were the weakest cities, and Busan has far fewer training photos than Tokyo. I expected that drawing every city equally often would improve Busan and Osaka, maybe at the cost of Tokyo, and raise the average.
- validation: 0.5102 (before: 0.4965 seed 0, 0.4918 seed 1)
- what it means: It worked as I expected: Busan and Osaka improved a lot and Tokyo got worse, and the average went up by about 0.015, which is more than the 0.005 difference between the baseline seeds. Seoul also went down, which I did not expect. I am fairly but not completely sure, because it is only one run, and per city the scores moved a lot between seeds before.

## 2026-11-09 b1 (Track B)
- changed: first Track B model: the starter train_b.py with ResNet18 at 224, 4 epochs, and --balance (every city drawn equally often)
- why: I wanted a valid Track B submission without much risk, so I used the starter script and added only --balance, because drawing every city equally often had helped Busan and Osaka in Track A. I hoped it would give a similar improvement
- validation: 0.5005 (before: none, first Track B run)
- what it means: b1 scored 0.5005, which is only slightly above the Track A baseline and within about the same range as the seed difference, so I cannot say it is really better. Busan and Osaka improved and Tokyo got worse, the same pattern as in Track A balanced. It is a bit lower than Track A balanced (0.5102), maybe because it trained on fewer photos, but it is only one run. I hoped for a similar improvement, and it only partly happened.

## 2026-11-09 curated (Track A)
- rule, written before dropping: "I drop training photos that show nothing about the city: food, objects, art pieces, indoor photos (homes, malls, restaurants, metro), people, vehicle parts and plain text or logos. I keep normal street photos and buildings, even when they are not special."
- changed: 51 training photos dropped (28 Busan, 23 Osaka), chosen from the suspects sheets of balanced_seed0 (suspects_balanced_seed0_busan_00 and suspects_balanced_seed0_osaka_00); the recipe is the balanced one, unchanged
- why: In the photo sheets of Busan and Osaka I saw many photos that show nothing about the city, like food, indoor photos and art. I expected that the model would learn better from only photos that show the city, and that Busan and Osaka would improve a bit. I could only look at one sheet per city, so I did not expect a big change.
- validation: 0.5103 (before: 0.5102 balanced)
- what it means: It did not change anything I can measure: the score went from 0.5102 to 0.5103, which is far less than the 0.005 difference between seeds. Per city the scores moved a little, but Busan and Osaka did not clearly improve, and Seoul and Tokyo changed too even though I dropped nothing there, so these are probably just noise. I think 51 photos out of 44,257 is too few to see an effect. With more time I would look at many more photos, not only one sheet per city, and measure that

## Next
With one more week I would look at many more photos of Busan and Osaka, drop the ones that show nothing about the city, and measure that with several seeds. I would also try a different model and a bigger image size in Track B, and add photos of my own.
