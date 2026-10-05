# DSA 4060 Week 3 Content-Based Recommender

## Student
- Name: Iranzi Innocent
- Student number: 670513

## Project overview
This project builds a content-based movie recommender from structured genre features. Each movie is a binary item profile. A user's ratings turn those profiles into a preference vector. Unseen movies are scored by how much of that preference they contain, and the already-watched movies are removed before the Top-N list is returned.

The recommender is personalized. Two users who watched the same movies but gave different ratings do not receive the same list, because the ratings are the weights.

## Dataset
The movies are a small teaching table created in the notebook, not MovieLens. Ten titles and five genre columns come from the Week 3 practical. One extra title, Paper Planets, was added for this submission. Running the notebook writes the full table to `movies.csv`.

Features are binary: 1 means the genre is present and 0 means it is absent. Ratings are explicit scores on a 1 to 5 scale.

## Methods
1. Build an item-feature matrix for Action, Comedy, Drama, Romance, and SciFi.
2. Weight each rated movie's features by the rating, then sum them into a user profile.
3. Divide the profile by its total so the values are proportions.
4. Score every movie with the sum of profile weight times genre indicator.
5. Remove movies the user has already rated and return the Top-N rows.

## How to run
1. Clone the repository.
2. Install packages: `pip install -r requirements.txt`
3. Open `content_based_lab.ipynb`.
4. Run all cells from top to bottom. The notebook creates the data in code and saves `movies.csv` beside itself.

## Key findings
- User A's profile is 50.0% Action and 35.7% SciFi. The unseen Top 3 is Space Warriors (0.857), City Detectives (0.571), and Broken Hearts (0.143).
- User B's profile is 43.8% Romance, 31.3% Drama, and 25.0% Comedy. That user does not receive User A's list.
- Paper Planets is Comedy and SciFi, a combination none of the original ten movies has. After it is added, it becomes User A's third recommendation because of the SciFi weight.
- The personal test user prefers Comedy (48.3%) and SciFi (27.6%). Galaxy Mission and Space Warriors tie for first because they have the same genre profile.
- Two users who rated Galaxy Mission, Love in Nairobi, and Final Battle with different scores received different Top 3 lists.

## Limitations
Only five binary genres are used, so two movies with the same genres cannot be separated. The score has no negative weights: a low rating still adds to a genre. A user with one rating gets an extreme profile, and a new movie can be scored only when its genres are known. Actors, directors, release year, language, and the story are ignored.

## Repository structure
- `content_based_lab.ipynb` is the full lab, with outputs kept visible.
- `movies.csv` is the 11-movie feature table, including Paper Planets.
- `requirements.txt` lists the Python packages.
- `.gitignore` keeps checkpoints, virtual environments, and secret files out of Git.
