---
title: "NYU Science Journalism Twitter Bias"
date: 2022-03-06
description: "An exploration into science journalists who graduated from NYU, and whether male graduates tend to have more followers."
tags: ['data', 'code']
---

The verdict: Men and women who graduate from NYU's SHERP program tend to have a similar number of Twitter followers. Let me explain how I know that.

A few months ago, while dreaming up story ideas for a health journalism course at NYU, I came across a study about gender disparities—in a medical journal. In that paper, researchers quantified the influence that male and female medical researchers exert on Twitter. The main finding: female medical researchers have a lower number of Twitter followers compared to their male colleagues, and this gap tends to widen as women progress in their careers and are promoted to higher tenure ranks. The paper is called [“Gender Differences in Twitter Use and Influence Among Health Policy and Health Services Researchers,”](https://jamanetwork.com/journals/jamainternalmedicine/fullarticle/2753117) and it was published in JAMA Internal Medicine in 2019. The title might be a mouthful, but its findings are deep; its data substantive.

For this study, the researchers also analyzed the mean proportion of women who follow women, how many retweets an original tweet garners for men compared to women, and many other things. I highlight some of the surprising or important gender disparities in the table below.

| Variable                                     | Male        | Female       | p-value |
|----------------------------------------------|-------------|--------------|---------|
| Years with a Twitter acount                  | 5.1±2.6     | 4.5±2.5      | <.001   |
| What % of people that they follow are women? | 42.6±14.8   | 54.8±14.6    | <0.001  |
| Avg. number of retweets per original tweet   | 3.1±3.4     | 2.4±2.2      | 0.01    | 
| Number of Twitter followers                  | 1162±3056.2 | 567.5±1819.7 | <0.001  | 

After reading this study, I wondered if the same Twitter "bias" — namely, that women have fewer Twitter followers than men — also applies to other professional fields. As a journalist studying at NYU, I started to explore Twitter data for past graduates of the Science, Health and Environmental Reporting, or [SHERP](https://journalism.nyu.edu/graduate/programs/science-health-and-environmental-reporting/), program. This is a masters program for science journalists.

I found a Twitter list called “[SHERP Tweeters](https://twitter.com/i/lists/46864545)” that includes a limited subset of SHERP graduates extending back more than a decade. Then, I used Python and [Tweepy](https://www.tweepy.org/) (an open-source Python library for accessing the Twitter API) to collect public data from their accounts. This data was collected on October 10, 2020 and includes the number of each person’s followers, how many people they follow, their Twitter handle, and other basic information. Gender was inferred for each person based on pronouns listed in their public account; it is possible that some people have been mis-gendered, and I apologize if that’s the case.

With the data thus collected and tidied, I plotted two simple scatterplots. In the plots below, each dot represents a person in one of two datasets; the science journalist data that I collected, or the medical researcher data from that JAMA Internal Medicine paper. On the x-axis, I plotted the number of people that each individual is following. Then, on the y-axis, I plotted their number of followers. Overlaid on this scatterplot are regression lines, for both men and women, with a 95% confidence interval shown in a lower opacity. The scatterplots for the two datasets look very similar.

![A plot showing regressions of scatterplots of followers vs. following for SHERP and medical researchers](/img/post-1/sherp_twitter_regressions.png)

Next, I focused in on the SHERP dataset, and looked solely at differences in the number of followers for male versus female science journalists. The distribution of followers for male SHERP graduates appears bimodal; that is, most men have between 500 and 5,000 Twitter followers, but there is a second group that has between 7,000 and 12,000 followers. For female SHERP graduates, there is only one large peak in the data. The majority of female SHERPies have 1,000 followers or less.

![A density plot showing the distribution in followers for male and female SHERP graduates](/img/post-1/sherp_twitter_density.png)

A density plot — though pretty to look at — doesn't tell us whether or not a significant difference exists between the two groups. To answer that question, I used Python to perform a [bootstrapping](https://en.wikipedia.org/wiki/Bootstrapping_(statistics)) analysis.

What I found is that there is no statistically significant difference in the number of Twitter followers for male and female SHERP graduates. My null hypothesis was that the two genders have the same number of Twitter followers, and I was not able to reject that hypothesis, using an arbitrary p-value threshold of 0.05. My calculated p-value was 0.084.

I'm not comfortable making concrete claims based on a simple statistical test, anyway. The SHERP dataset has all sorts of problems; genders might be misassigned and not all SHERPies are on the list. My dataset is also quite a bit smaller than the medical researcher dataset, and why is 0.05 considered a typical p-value anyway? All I can say, for sure, is that the visual plots show marked differences between male and female science journalists, and their followings on Twitter.