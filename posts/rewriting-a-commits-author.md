—
title: 
tags:
  - search
  - challenge
layout: challenge
hashtag: #know-git-rewrite-commit-authors
—

- In _The Case of the Curried Chicken_, the challenge was created by editing the author of various commits. How was this accomplished?

- First, I created all of the commits with my “default” user account
- Next, I created git aliases to rewrite those.
- Then, using `git rebase`, stepped through each of the commits whose authors need changing and ran the command.
