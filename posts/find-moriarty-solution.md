---
title: An introduction to git grep
tags:
  - search
  - solution
challenge: /posts/find-moriarty
layout: solution
hashtag: #know-git-find-moriarty
---

In addition to all of its tools for version control, `git` comes with some great tools for debugging! One of these is `git grep`, and it is the _perfect_ tool for challenges such as these. If you are unfamiliar with [grep](https://en.wikipedia.org/wiki/Grep), it stands for "globally search a regular expression and print" and is used for finding strings within a codebase.

Looking back at the challenges: how can we find the stories in which Moriarty is mentioned by name? A first attempt may look something like this:

```bash
git grep Moriarty
```

If you were to run this on your codebase, you'll get your answer -- but it'll be accompanied by the complete context of each line that Moriarty is mentioned! If you want to only get the filenames, you can use the `--files-with-matches` flag (abbreviated to `-l`).

```bash
git grep --files-with-matches Moriarty
git grep -l Moriarty # same
```

You might notice that not all of the filenames returned are part of the Holmes canon -- in fact, if your repository is up-to-date, the file that generated this page will be included! As the original challenge said, the original text is available in the `holmes` directory. We can use <a href='https://css-tricks.com/git-pathspecs-and-how-to-use-them/'>pathspecs</a> to narrow the focus of the command.

```bash
git grep -l Moriarty -- holmes
```

Perfect! This was my solution to the first challenge. The second part of the challenge is to determine where Moriarty is mentioned only a single time. We can do this by replacing the flag in the solution for the first solution: rather than using the `--files-with-matches` flag, we can use the `--count` flag.

```bash
git grep --count Moriarty -- holmes
git grep -c Moriarty -- holmes # same
```

This will print out all of the files that contain Moriarty's name, as well as the number of times it appears in each file.
