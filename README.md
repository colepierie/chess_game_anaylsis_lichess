# ChessGameAnalysis-Lichess
Analyzing the Chess Game Dataset (Lichess) from Kaggle. 


In chess, there is a general consensus among players that white has the strategic advantage over black since White plays first. Since 1851 statistics consistently show white winning slightly more with a win rate between 52% and 56% over black. This seems to align with our analysis as well. However, based on our analysis, there are some combinations of opening moves and formats which result in a higher win rate for black. Unfortunately, this analysis may prove to only be helpful for white when choosing their opening moves strategically.

We created a Tableau Dashboard which allows the user to search through the opening moves to see who has the highest win rate for each format.

## Intro to the Data Set

This data set contains over 20,000 games from a variety of users on the chess site “lichess.com”. While we retrieve the data from kaggle, the original source was taken using the Lichess API. Our goal was to focus on a few general questions: All things being equal, who wins more White or Black? And finally, which openings are best for White and Black?

## Python

To make things easier for ourselves, we dropped all non-rated games, leaving us with a little over 16,000 games still to analyze. The next step was to simplify the increment code column. This series contained the varied time formats that lichess has to offer. Since the increment is customizable, there's a near infinite amount of options that players can use for their games. While this is a great feature for the user, it's not as great for the analyst. To solve this, we created a loop that went through each input, and outputted the format that the increment would roughly fall under. The four formats are bullet(under 1 min.), blitz(1-9 min), rapid (10-20), and classical (above 20). We then created a new sub dataset that contained each individual player along with their rating, the difference of the rating between them and their opponent, and finally their “player level”. To create the “player level” column, we once again used a loop. For this, we used the player rating chart and assigned them a rating equal to their rating if it were a FIDE (the governing body of Chess) rating. After it was all said and done, we moved on to the actual analysis!

# Machine Learning

## Logistic Regression

We performed a Logistic regression on whether or not a players rating, the difference between their rating and their opponents, and the number of book moves in the game could reliably predict whether or not the player would either win/draw or lose the game. We ran two separate regressions, one on the players using white, and the other for players using black. After running the model, for both white and black, the model predicted the winner around 64% in the test data. While that is slightly better than a coin flip, it's not high enough to reliably predict going forward. It’s interesting that the color had nearly no effect on our data score, with white having a percentage of 64.3 and black with a percentage of 64.0. 

## Neural Network

The Sequential Neural Network model tested whether the below nine variables could reliably predict the winner of the match.

- Format
- Victory_status
- Opening_name
- Turns
- White_id
- White_rating
- Black_id
- Black_rating

After running the network with the nine input variables, 4 hidden nodes, and 500 epochs with the Adam optimizer enabled the best model predicted the winner with 66.53% accuracy and 59.71% loss of the test data.

This is not an accurate model so in an attempt to increase the accuracy of the model, we tested eight and twelve nodes with the same parameters. The best model for this test ended up still being the initial model with 4 nodes.

Conclusion
