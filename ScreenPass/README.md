After Week 1 in the NFL, I took notice to a lot of screen passes, specifically a lot that were going for negative yards (13% in 2023, comp to 11% in 2022). On average yards per screen:

2022: 5.39
2023: 5.07

Using @nflfastR, I found what features predict screen pass success:


About 10% of screen passes go for no yards
However, after the “no-gain” area, it's a equivalent likelihood from 2-7 yards.
A screen pass, as a density, fits right in between the normal-ness of a run, and the highly skewed pass.

[screenpasses_2022v2023_density.png]
[screenpasses_pass_run_2022density.png]


Looking at it through teams, in the 2022 season 2 teams stood out:
- The Titans were extraordinarily good at 9.9 yards per screen, but only ran it 41 times, compared to the 60-70 average (Detroit next at 7.1)
- The Jets were awful, at 2.95 yards per screen, 0.7 lower than the next lowest team


Through 3 weeks, 2023 shows the Titans still near the top, and the Jets have turned it around, with the Giants averaging negative yards per screen so far. 

[screenpasses_team.png]


Defensively, last year Pittsburgh was great at the screen, with 1.7 yards given per screen, 1.4 yards lower than the next team, but teams did not run it against them (only 29, 8 fewer than the next).

In 2023, Dallas reigns supreme, with 8 screens at < 1 yard per screen given.

[screenpasses_team_def.png]

Checking out some other variables for 2022, screens showed to be especially ineffective on 3rd down, via yards gained and expected points added (5.0 and -0.35 respectively). Additionally, it was more effective when ran in 2nd and 10-15 situations, with an average of 7.5 yards gained, and a 0.24 EPA.

Situations with at least 50 occurrences:

[screenpasses_down_ydstogo.png]

Location wise, most screen passes were ran from opposite sides, so if the ball started near or at the left hash, the screen was ran to the right (nearly 60% of all screen passes, as opposite to the same side being only about 30%), but it showed to be as effective as same side screens. 

Location did matter with where the team ran it area of the field wise, where it was significantly more effective from a team’s own 20-40 (0.06 epa), then it is on the opponents 40-20 (-0.12 epa).

[screenpasses_area_of_field.png]

The most relevant feature came with air yards, where the data shows a quick 1-2 (technically -1 and -2, yard dump off were significantly more effective than another. With both having EPAs of around 0.1 and 6 yards per screen, compared to more negative air yards (-3 to -6, at about -0.1).

Some other insignificant features: 
Shotgun: most screens were run in shotgun
Score Difference / Win Probability: winning or losing, on average did not change the averages
number of blitzers: a TBD on this one, but FTN’s data had this highly skewed towards 0, which I am assuming is non-defensive line players
Number of pass rushers: skewed highly towards 4, but no big difference if at 3-6. 


Finally, I ran a logistic regression on the 2023 screens, to see if I could predict a successful screen pass, defined as a screen pass that produced a positive EPA (Expected Points Added).  It produced about a 65% accuracy, which is not amazing, but a result 15% better than an average is significant given the randomness of the sport.


Model Features and their values (all significant):
- Intercept (starting probability): 0.46
- 3rd down (1/0): -1.01 
- if yards to go to the 1st was greater than 10: -0.55
- air_yards: +0.09 (more negative = worse)
- if it occurred between the possession’s teams own 20-40: +0.31

Lets look at the film to see what we can find whats potentially missing from our model: 


Denver vs Kansas City Week 14 2022- Marlon Mack's 66 yard screen pass to the house, mostly because of Kansas City's heavy blitz, had them out of position, and a couple missed tackles later, was in the endzone. The model predicts a success here of only 33%, mainly because of the amount of air yards (5). Given some tracking data, we could use some advanced features, such as players between receiver and endzone

https://twitter.com/Broncos/status/1602076235122630658

Kansas City vs SF, Week 7 2022 - McKinnon runs for a 34 yard screen pass. It seems like more of a play to get into better FG position (up 5 at opponent 38), which this model wouldnt  take into consideration, but ends up getting the first down when 9ers are over-eager on blocks. A feature like player speed / elusive score could also play a big factor into this model if added.

https://twitter.com/Titans/status/1589432742818811905
