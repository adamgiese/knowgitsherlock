---
title: The perils of git blame
tags:
  - search
  - solution
challenge: /posts/case-of-the-curried-chicken/
layout: solution
hashtag: #know-git-curried-chicken
---

Just to recap the challenge: we are looking to see who added the curare paste to the Curried Chicken recipe.

If you are looking to see who contributed a specific line to a file, your first instinct might be to go to `git blame`. You can either run `git blame` from the command line or use a git blame plugin for your editor of choice.

```bash
git blame recipes/curried-chicken.md
```

Take a look and see who is "blamed" for each line:

```bash
03e16372 (John Watson 2020-03-10 18:47:42 -0500  1) # Curried Chicken
5551b549 (Mrs. Hudson 2020-03-10 18:21:46 -0500  2)
03e16372 (John Watson 2020-03-10 18:47:42 -0500  3) ## Ingredients
5551b549 (Mrs. Hudson 2020-03-10 18:21:46 -0500  4)
03e16372 (John Watson 2020-03-10 18:47:42 -0500  5) - 4 chicken breasts
03e16372 (John Watson 2020-03-10 18:47:42 -0500  6) - 1/2 cup honey
03e16372 (John Watson 2020-03-10 18:47:42 -0500  7) - 1/4 cup mustard
03e16372 (John Watson 2020-03-10 18:47:42 -0500  8) - 4 tablespoons curare paste
03e16372 (John Watson 2020-03-10 18:47:42 -0500  9) - 4 tablespoons butter
03e16372 (John Watson 2020-03-10 18:47:42 -0500 10) - 2 tablespoons curry power
03e16372 (John Watson 2020-03-10 18:47:42 -0500 11) - 1/2 teaspoon salt
5551b549 (Mrs. Hudson 2020-03-10 18:21:46 -0500 12)
03e16372 (John Watson 2020-03-10 18:47:42 -0500 13) ## Instructions
5551b549 (Mrs. Hudson 2020-03-10 18:21:46 -0500 14)
03e16372 (John Watson 2020-03-10 18:47:42 -0500 15) 1. In a saucepan, combine the honey, mustard, curare paste, butter, curry power, and salt. Heat until it begins to bubble.
03e16372 (John Watson 2020-03-10 18:47:42 -0500 16) 2. Pour sauce over chicken and heat in oven for 375&deg;F for 30 minutes.
5551b549 (Mrs. Hudson 2020-03-10 18:21:46 -0500 17)
```

Taking a look at just line 8...

```bash
03e16372 (John Watson 2020-03-10 18:47:42 -0500  8) - 4 tablespoons curare paste
```

Oh no! John Watson turned criminal? This surely cannot be! You are right to be sceptical. Perhaps we can give Watson a chance to explain himself. Lets take a look at the commit message of the guilty commit:

```bash
git show 03e16372 --no-patch
```

```bash
commit 03e1637252548019bf81ff7645e4d4253adffda5
Author: John Watson <watson@knowgitsherlock.com>
Date:   Tue Mar 10 18:47:42 2020 -0500

    Remove trailing spaces from curried chicken recipe

```

So, it seems that Watson's changes were purely superficial -- he simply applied some style linting to Mrs. Hudson's recipe. So, who is the _real_ culprit? We can use the the `-w` flag to ignore the whitespace. This flag is the perfect tool for this particular job!

```bash
git blame -w recipes/curried-chicken.md
```

```bash
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500  1) # Curried Chicken
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500  2)
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500  3) ## Ingredients
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500  4)
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500  5) - 4 chicken breasts
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500  6) - 1/2 cup honey
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500  7) - 1/4 cup mustard
51055fe9 (Culverton Smith 2020-03-10 18:46:52 -0500  8) - 4 tablespoons curare paste
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500  9) - 4 tablespoons butter
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500 10) - 2 tablespoons curry power
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500 11) - 1/2 teaspoon salt
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500 12)
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500 13) ## Instructions
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500 14)
51055fe9 (Culverton Smith 2020-03-10 18:46:52 -0500 15) 1. In a saucepan, combine the honey, mustard, curare paste, butter, curry power, and salt. Heat until it begins to bubble.
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500 16) 2. Pour sauce over chicken and heat in oven for 375&deg;F for 30 minutes.
5551b549 (Mrs. Hudson     2020-03-10 18:21:46 -0500 17)
```

It seems that the devious Culverton Smith is behind this plot!

When using `git blame`, it is important to note that the “author” of a line is the one who has edited the line most recently, not necessarily the one who wrote the line.

## Additional Thoughts & Challenges

- In this case, using the `-w` flag to ignore white space changes made finding the update trivial. What if the stylistic changes that Watson made were _not_ white space? How could `git blame` have been used in this case?
- What tools other than `git blame` could be used to see who added the curare paste?
