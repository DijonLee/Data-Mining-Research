Authors: Zhaoxiong Ding and Jovan-Gianni Lee
PSC 278W
Spring 2018

Sports, Reddit, and Nationalism

“Don’t invade Russia in the winter.” But could Napoleon have even marched to the outskirts of Moscow without nationalism? The French Revolution is arguably one of the most cited examples of the power of nationalism as a tool for state creation, military mobilization, and — ultimately — war.

So does nationalism cause interstate conflict? Despite the difficulty in testing for a casual relationship between these two phenomena, political scientists have widely used nationalism and its myriad effects as a tool to help explain international violence. Nationalism can “increase the enmity between countries, undermine international cooperation, motivate societies to fight costly wars, and cause governments to overestimate their relative military power” (Bertoli 2017). In fact, many theories of war are predicated upon nationalism, such as the theory that emerging democracies are more likely to go to war (Mansfield and Snyder 2007) and the theory that leaders can manipulate national sentiment to make conflict more likely.

Andrew Bertoli used international sporting events, specifically World Cup qualification, as a proxy of nationalism. His justification is threefold. First, international sporting events serve as aus thod to circumvent the measurement problem. It’s difficult to find aus asure of nationalism even today, much less one “that spans across countries and time” (Bertoli 2017), but many scholars agree that such sporting events serve to increase nationalism (Cha 2009; Markovits and Rensmann 2010). Sporting events also serve to increase the jingoism within a country, such as “reporters describing games in military terminology” (Bertoli 2017) and news reports comparing the outcome of matches to battles (Garland and Rowe 1999). The World Cup match between Chile and Italy in 1962 has been dubbed the “Battle of Santiago,” and even games in the European Cup have been described using such visceral phrases as “most impressive thrashing” (Murray 2003). Secondly, the most popular international sports event, the FIFA World Cup, also fits well into a regression discontinuity analysis, which provides casual power. Thirdly, there is no reason for sports to increase conflict any other way. One alternative explanation is that international sports events distract the nation, and politicians use the opportunity to pursue their own goals internationally. Bertoli believes this explanation is inconsistent with his data. In short, he asserts that the tight connection between sports and nationalism (which is supported by both political scientists and sociologists) makes the use of “sports as a source of nationalism” convincing (Bertoli 2017). 

While Bertoli dives into connection between sports and nationalism, I’m inspired to look for a model that connects sports to the behavior or emotion of the population and can scale down to an individual level. In many papers at least some appeal to the “wide variety of emotions” invoked by sports is made (Oshimi 2015, p. 17; Brimicombe and Cafe 2012). In fact, this strong connection between sports and emotion has a label: fan identification (Dimmock and Grove 2003). In addition, there exists literature connecting sports to a wide array of specific phenomena such as heart attacks, domestic violence, and national pride (Carroll et al 2002; Card and Dahl 2009). These topics boldly venture into sociology and psychology. Especially with national “pride.” This begs the question, in the age of the internet and big data, can we create a finerus tric?

To investigate the relationship between sports and the population with a more fine-grained metric weturned to Reddit comments and sentiment analysis. Gathering the comments from the city surround a sports team, what effect will wins and losses have on the population’s sentiment? Using Microsoft’s Cognitive Services,we can approach this problem computationally to give a relatively objective measure of the  “sentiment” of a comment. I’m not the first to use sentiment analysis on big data, others have used sentiment analysis on Twitter data during the World Cup tous asure emotion along several dimensions such as “anger, fear, joy, sadness, disgust, surprise, trust, and anticipation” (Yu and Wang 2015). But we do believe that we are fairly original in attempting to add a modicum of distance. Yu and Wang specifically filtered for tweets that were linked to the match via hashtags. As a result any connection between the events in the sports match and changes in sentiment can be directly explanation through links such as fan identification.we hope that by choosing the subreddit for each city instead of each team,wecan uncover more indirect and less studied connections.

Sentiment Analysis

The task of “finding the opinions of authors,” sentiment analysis is an area of intense research that has benefited in recent years from the large text datasets available from socialus dia (Feldman 2013). From cutting-edge models capable of detecting sarcasm to simple binary positive or negative classifiers, the field is wide and the quantification of emotion varied (Maynard and Greenwood 2014; Feldman 2013). Even among the popular sentiment analysis services there is considerable difference in the output format. Google returns “score” and “magnitude” as two separate dimensions, allowing for quantification of the difference between neutral and mixed documents; that is, documents that are largely unemotional versus documents that have strong but mixed emotional sentiment (Google CLP). The available approaches to sentiment analysis owe a lot of their heritage to natural language processing, and can be broadly grouped into 3 categories: statistical, syntactic, and semantic.

Syntactic approaches can be considered the most traditional and rely on identifying and tokenizing documents into progressively smaller pieces to build up understanding. From paragraphs to sentences to words to parts of speech, the location of words and their relationship to each other is the central tenet of syntactic approaches. Statistical Methods are powered by n-grams, the probability of a n specific words appearing in order. Comparisons between the efficacy between approaches are typically problem specific, and the distinctions are not always clear. Syntax and semantics, which may seem completely orthogonal concepts, can be intertwined (Scott 2006, p. 192). I’m no expert on either natural language processing nor sentiment analysis, sowepicked Microsoft’s service primarily because of their technical ability to process 2.5 million comments quickly. Microsoft’s Cognitive Service for Sentiment Analysis evaluates text input and returns a single sentiment score for each document, ranging from 0 (negative) to 1 (positive). In this sense all emotion is collapsed into a single dimension. While we lose the rich dimensionality supported by some models, this simplicity does make for easier data analysis. According to Microsoft, their service performs best on short documents, which the Reddit dataset is perfectly suited toward. 

On the other hand, one of the downsides of sentiment analysis and all natural language processing is their struggle to understand context. This shortcoming is heightened by Reddit comments, which by their hierarchical nature are related by context not only to the post they’re attached to but also to all their parent and surrounding comments. Unfortunately there is no way around this.
Reddit was only founded in 2005, and many of its city and country specific subreddits weren’t founded until around 2010. Thus,  in order to gather a large dataset we had to use sporting events that happened more often than quadrennial events such as the World Cup and Olympics. Even annual events such as the Super Bowl and NBA Finals would result in a small dataset. Due to the noise present in the comments and the distance we have placed between the experimental condition (the game) and the metric sentiment,we expect any present effects to be quite small compared to the natural variance within the comments of a subreddit on a day to day basis. We need as large of a dataset as possible. As such,we turned to the NBA, whose 82 games per team per year results in plenty of opportunities to investigate the effect of a win or loss on the local population.

Focusing on US cities (instead of countries) has additional benefits. Firstly, the US user base of Reddit is the largest of any country (Pew Research). Secondly, while Microsoft’s text analytics support multiple natural languages, it is possible for the distribution of sentiment scores to vary by language based on the model created for that language, thus biasing the results by language. Using only English obviates this potential bias.
Design

While Bertolli's regression discontinuity model enables him to potentially conclude causality,weam aiming for the lower goal of correlation via statistical testing. The NBA’s regular season does not provide the same opportunity as the World Cup for regression discontinuity due to the difficulty of find a cut-point. Rather,we picked the approach of a natural experiment.
The NBA has 30 teams. In order to investigate the effect of team wins and losses on the local population,we analyzed only comments from the city in which that NBA team’s stadium was located (and within 1 day of an NBA game).we excluded cities with multiple teams. New York City and Los Angeles both have 2 teams within their city borders (New York Knicks and Brooklyn Nets, Los Angeles Lakers and Los Angeles Clippers). Card and Dahl, when faced with multiple NFL teams within a state, also chose exclusion.we don't foresee any major issues. 
Within the calendar year 2014, the NBA played 1245 regular season games. The 2013-14 NBA regular season ended on April 16th, 2014, and the 2014-15 NBA regular season started on October 28th, 2014. Both seasons were regular in that there were no lockouts, new teams, or team relocations (other than a minor change in the Charlotte Bobcats renaming to the Charlotte Hornets). Since playoff games have greater viewership relative to the regular season and since not all teams play an equal amount of playoff games,we excluded the postseason (Nielsen). Additionally,we did not take into consideration the NBA Summer League, pre-season, or NBA D League. 

Reddit is a socialus dia platform in which users post to specific “subreddits,” a section of Reddit dedicated to a specific topic.we used the subreddit that each comment is posted to as aus asure of relevance. For each NBA team,we analyzed the comments of its city’s subreddit. There are also subreddits dedicated to each NBA team, such as “/r/thunder” for the Oklahoma City Thunder while “/r/okc” is the subreddit for Oklahoma City. Since we Want to investigate the effect of sports on the local population,we deliberately chose to use the city subreddit. In the 2014 Reddit dataset 2,763,528 comments belonged to the relevant subreddits.we delete all comments whose body had been deleted but still existed in the dataset.wethen deleted all comments that did not receive a sentiment score (some comments are considered too “objective” by the sentiment analyzer and given a perfectly neutral score of .5, they are considered unprocessed) (Microsoft). 


final dataset consisted of 2,070,514 comments. With 26 subreddits and 365 days, this gives us  about 218 comments per subreddit per day, my window of interest.

## INsert table here


Table 1: The subreddit associated with the host city of each team’s arena. Teams from New York City and Los Angeles were excluded. The number of subscribers (per subreddit) was accessed on 5/5/2018.
	
We  implicitly made the assumption that each subreddit is representative of its city. To support this assumption,we performed a Chi squared goodness-of-fit test on the number of subscribers against the population of the city. The result was not statistically significant. Of course, the subscribers to each subreddit are self-selected, so the sample is not necessarily random. If we do not consider a subreddit to be representative of its city, then my modelus rely investigates the connection between NBA games and sentiment of the corresponding subreddit, rather than local population —we believe this connection is still interesting in its own right.

Results

We first plotted the average sentiment per day over the course of the year. While this is not especially relevant to the sports-sentiment model we’re trying to build, it is interesting to note the rise in average sentiment around the day 300, which corresponds to October 28th, the start of the NBA regular season (the end of the previous season, April 16th, is day 105). Since there is only one year’s data, it is not clear what the correlation, if any, is.

## insert table here 


Figure 1: Average sentiment analysis over the course of 2014. Comments were binned by day and then a 10 day moving average was applied.

Next,we sifted through the comments in order to find all the comments within 1 day of an NBA game from that team’s subreddit. Since there exist back-to-back NBA games, the shortest duration between 2 consecutive games for the same team is 1 day. Because winning a game potentially biases a team to win the next game,we cannot include any data past the next game.we ignored whether a team was home or away; at least in the connection between NFL games and domestic violence, there is no statistically significant difference between home and away (Adubato 2015). To test for statistical significance we used 2-sample t-tests.We tested the sentiment scores in 4 ways: pre-win to post-win, pre-loss to post-loss, pre-win to pre-loss, and post-win to post-loss. For example, the Pre-Win to Post-Win result of a specific subreddit tests all the comments (and also the whole dataset at the end) that happened within the 24 hour period before their won game against all of the comments within the 24 hour period after their won game. Since this data is not experimental, the distinction between pre-win and pre-loss only exists in post hoc analysis. Of these 4 ways,we expected pre-win to pre-loss to have no significant difference (as there is no way of knowing if a team will win) and post-win to post-loss to have the most significance.

## Insert table here


Table 2: t-test p-values (rounded to 4 digits) on the sentiment scores of individual subreddits and whole dataset before and after wins and losses. Significant results (α=0.05) are in bold.
 
The statistical results are odd. In the whole dataset, the only non-significant result was pre-win to post-win, indicating that a win has no effect. The significant Pre-Loss to Post-Loss effect is more congruent with current literature; in NFL games wins were found to have no significant effect on domestic violence while losses (albeit upset losses only) did (Card and Dahl 2009). The Post-Loss to Post-Win result is also in-line with my hypothesis that game wins and losses have an effect on the local population’s sentiment (and furthermore than losses and wins have opposing effects, though this is not as clearly supported). However the troublesome result is that the Pre-Win to Pre-Loss test also significant. As noted earlier, this distinction should only exist in my post hoc analysis. If this effect is real it implies either that we can foresee the outcome of the game or there exists some process that influences both the sentiment of the population and the outcome of the game. While there exist unbiased predictors of game outcomes like Vegas odds, the extremely low p-value implies a predictive power far beyond (Card and Dahl 2009). Despite the sentiment scores’ bimodal distribution, the Central Limit Theorem should allow for the applicability of the 2 sample t-test still as the sample size of each comparison was large. The average number of comments within each t-test sample was 13,060; the fewest was okc’s, at 300 comments.

However, not all comments are of equal quality, as mentioned earlier there are comments in the dataset even after processing that are either extremely short or nonsensical to the sentiment analyzer. While the unprocessed comments and deleted comments are easy to identify and excluded from the dataset, there exists a spectrum of quality. Luckily, humans have voted on each comment. Reddit provides the vote total of each comment (the number of upvotes - number of downvotes).weran the same t-test after weighing each comment sentiment score by its vote total and we also ran the t-tests on the sentiment scores weighted by the vote total after applying either a square root or a logarithm to the vote total (to prevent outliers in vote total from affecting the sentiment scores too much). However the outliers in vote total exist in both ends. The results from the sqrt and log matched the non-weighted analysis in terms of number of significant subreddits in each category, though the specific subreddits changed.


Table 3: t-tests on sentiment scores in the same thod as Table 2. However, the values are now a linear combination of each comment’s vote total and sentiment score. Significant results (α=0.05) are highlighted in green.
## insert table

The results are again weird, and contradictory to the original, unweighted statistical analysis in many respects. The only result that is the same is the significance in the Post-Loss to Post-Win test, the test that we predicted to have the strongest result. The effect in the first two columns, which in Table 2 was in-line with Card and Dahl’s NFL analysis, is now reversed. Finally, the puzzling significance in between the pre-loss and pre-win data still remains, a result that we cannot explain. However, as a silver lining, this time there are only 3 individual subreddits in which this significance exists, instead of 9 subreddits in the unweighted analysis.

Figure 2: A scatter plot of all the comments within a day of a win. The X axis plots time relative to each comment’s respective game. The Y axis plots their sentiment score. The non-normal distribution of the sentiment scores is clearly visible.

Having explored only statistical p-values so far,we find it refreshing to take a look at the data itself.we don't expect to see any trends (if there exist any) in such a dense scatter plot, but a few phenomena emerge. The relatively less dense sections center around 9 am as most NBA games begin around 7:00 pm EST, so despite averaging over 1245 games, the time of day is relatively preserved.
Future Directions
Due to limitations in computational and financial resources,we only analyzed 2014. This dataset can easily be extended to 2011, 2012, 2013, 2015, 2016, and 2017. The results indicate that a 2 sample t-test may not be the most appropriate statistical test for the data. Microsoft’s sentiment analysis model returned a highly non-normal, bimodal distribution of scores. There exists a large band in the range of scores (from about .32 to .68) in which no data points exist. For a real-life dataset of more than 2 million comments, it is difficult to believe that this is by chance. Unfortunately there is no documentation of such behavior from Microsoft, sowe cannot ascertain if this is really a quirk of their model (which is valuable, proprietary intellectual property for them) or some real effect within the data.


Figure 3: Probability density function of sentiment scores
Figure 4: PDF of weighted sentiment (using vote total)

A further limitation of Microsoft’s service is its apparent over-focus on feature extraction such as emojis. Of the over 2 million comments, only 54 scored a perfect 1. Of these 54, every single one contained an emoji such as :). As an example, this comment was one of the lucky 54: "hrr" :P. All the lexicon-based approaches have this tendency (Yu and Wang 2015). 

Additionally,we would like to do nonparametric statistical testing such as bootstrapping in order to estimate the variance of the sample’s statistics. Though the Central Limit Theorem provides for the use of t-testing on non-normal data provided the sample size is large, the contradictory and unintuitive results do not provide a definitive understanding of the dataset. Another avenue for exploration is the tremendous portion of data between the end of the 2013-14 regular season in April and start of 2014-15 regular season in October. These comments are well outside the proximity of an NBA game and can be used to get aus asure of the baseline variance. Of the little over 2 million comments in the dataset, 1.2 million lie outside a day of the nearest NBA game. Paired analysis can be utilized to remove outside variables. For example, each game has a winner and loser. By analyzing the comments from the winning and losing subreddit together,we can eliminate differences in time (as they occur during the same day).

The search for a scalable model of sports and sentiment led us to sentiment analysis on Reddit comments around NBA games. While the statistical tests have not provided any definitive results,we believe this model is promising. By understanding the connection between sports and the sentiment of the local population better, we can explore new ways in which sports make populations more hawkish and states more susceptible to interstate conflict. And only by understanding sentiment better can we understand how national sentiment can be manipulated by leaders.

References

Adubato, Beth. “The Promise of Violence.” Journal of Sport and Social Issues, vol. 40, no. 1, 2015, pp. 22–37., doi:10.1177/0193723515594209.

Card, David, and Gordon B. Dahl. “Family Violence and Football: The Effect of Unexpected Emotional Cues on Violent Behavior*.” The Quarterly Journal of Economics, vol. 126, no. 1, 2011, pp. 103–143., doi:10.1093/qje/qjr001.

Carroll, D. “Admissions for Myocardial Infarction and World Cup Football: Database Survey.” Bmj, vol. 325, no. 7378, 2002, pp. 1439–1442., doi:10.1136/bmj.325.7378.1439.

Cha, Victor D. "A theory of sport and politics." The International Journal of the History of Sport 26.11 (2009): 1581-1610.

Dimmock, James A. & J. Robert Grove (2007) Relationship of Fan Identification to Determinants of Aggression, Journal of Applied Sport Psychology, 17:1, 37-47, DOI: 10.1080/10413200590907559

Feldman, Ronen. “Techniques and Applications for Sentiment Analysis.” Communications of the ACM, vol. 56, no. 4, 2013, p. 82., doi:10.1145/2436256.2436274.


Garland, Jon, and Mike Rowe. "War minus the shooting? Jingoism, the English press, and Euro 96." Journal of sport and social issues 23.1 (1999): 80-95.

Google Corporation. Cloud Natural Language API Documentation. https://cloud.google.com/natural-language/docs/sentiment-tutorial

Mansfield, Edward D., and Jack Snyder. Electing to fight: Why emerging democracies go to war. mit Press, 2007.

Markovits, Andrei S., and Lars Rensmann. Gaming the world: How sports are reshaping global politics and culture. Princeton University Press, 2010.

Maynard, Diana, and Mark A. Greenwood. "Who cares about Sarcastic Tweets? Investigating the Impact of Sarcasm on Sentiment Analysis." Lrec. 2014.

Microsoft Corporation. API Documentation Text Analytics 2.0. Microsoft Azure. https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis. Accessed 8 May 2018

Murray, Scott et al. "The greatest-ever European Cup thrashings." The Guardian [London] 6 Nov 2003

Nielsen Digital. NBA PLAYOFFS WHERE AMAZING MARKETING HAPPENS. Nielsen Data Analytics. http://www.nielsen.com/us/en/insights/news/2009/nba-playoffs-where-amazing-marketing-happens.html. Accessed 8 May 2018


Oshimi, Daichi. "Emotions of Sport Spectators." Sports Management and Sports Humanities. Springer, Tokyo, 2015. 17-30.

Pew Research Center. "Distribution of Reddit Users in The United States as of February 2016, by Gender." Statista - The Statistics Portal, Statista, www.statista.com/statistics/517155/reddit-user-distribution-usa-gender/, Accessed 8 May 2018

Scott, Michael Lee. Programming Language Pragmatics. Morgan Kaufmann Pub., 2006.

Yang Yu, Xiao Wang. “World Cup 2014 in the Twitter World: A big data analysis of sentiments in U.S. sports fans’ tweets” Computers in Human Behavior, Volume 48, 2015, Pages 392-400, ISSN 0747-5632, https://doi.org/10.1016/j.chb.2015.01.075.





