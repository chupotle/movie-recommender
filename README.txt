Uses GroupLens dataset from https://grouplens.org/datasets/movielens/ - either ml-latest (-f/--full) or ml-latest-small (default).

Using the full dataset right now takes a significant amount of time now - around 25-30 seconds because the entire dataset needs to be read in from file each time the program is run.

usage: recommendmovie.py [-h] [-g] [-f] [-i] [-t] [-m] [-r [percent]]
                         [-p | -c | -e]
                         [user-id] [movies [movies ...]]

***you will have to download ml-latest on your own to use the "full"***

Given a User ID from the MovieLens database, predict the user's scores for
specified movies.

To reproduce results in the writeup, run the following:
For the RMSE calculations:

python3 recommendmovie.py -r
or the following if the above doesnt work
python recommendmovie.py -r

to generate the star predictions:
python3 recommendmovie.py -p -m 120 5 12 32 52 141 260 608 631 648 653 

python3 recommendmovie.py -c -m 120 5 12 32 52 141 260 608 631 648 653 

python3 recommendmovie.py -e -m 120 5 12 32 52 141 260 608 631 648 653 

or the following if the above doesnt work
python recommendmovie.py -p -m 120 5 12 32 52 141 260 608 631 648 653

python recommendmovie.py -c -m 120 5 12 32 52 141 260 608 631 648 653

python recommendmovie.py -e -m 120 5 12 32 52 141 260 608 631 648 653

and: 

python3 recommendmovie.py -p -m 448 1 2 3 5 10 12 16 19 20 21

python3 recommendmovie.py -c -m 448 1 2 3 5 10 12 16 19 20 21

python3 recommendmovie.py -e -m 448 1 2 3 5 10 12 16 19 20 21

or the following if the above doesnt work
python recommendmovie.py -p -m 448 1 2 3 5 10 12 16 19 20 21

python recommendmovie.py -c -m 448 1 2 3 5 10 12 16 19 20 21

python recommendmovie.py -e -m 448 1 2 3 5 10 12 16 19 20 21




positional arguments:
  user-id               The User ID from ratings.csv to predict ratings for.
  movies                A list of movies (Movielens IDs) to predict the ratings of.

optional arguments:
  -h, --help            show this help message and exit
  -g, --genres          Use tf-idf for genres as a weighting for collaborative
                        filtering.
  -f, --full            Use the full dataset rather than the small dataset.
  -i, --imdb		Specify that the IDs are IMDb IDs rather than
                        MovieLens IDs.
  -t, --tmdb            Specify that IDs are TMDb IDs rather than MovieLens IDs.
  -m, --movielens	Specify that the IDs are MovieLens IDs.
  -r [percent], --rmse [percent]
                        Run the cross-validation test routine to calculate
                        RMSE for each distance measure. If a percent is
                        specified, only that percent of users in the dataset
                        will be used for the routine, selected randomly
                        (default: 10).
  -p, --pearson         Use pearson correlation to calculate distances for
                        collaborative filtering (default).
  -c, --cosine          Use cosine similarity instead of Pearson correlation
                        to calculate distances for collaborative filtering.
  -e, --euclidean       Use euclidean distance instead of Pearson correlation
                        to calculate distances for collaborative filtering.


This program uses collaborative filtering to determine a predicted rating for each movie. The default is a score-based method which uses
the distance between users' rating vectors to compute a weighted sum of ratings for a particular movie. The genre-based method uses the
frequency with which users watch different genres to determine how different they are, which is used in the weighted sum. Since the
genre-based method doesn't take score into account, it is appreciably worse than the score-based method.

The cross-validation method is used for testing. It compares three distance measures - cosine similarity, Pearson correlation, and Euclidean distance