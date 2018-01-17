### Understanding Git

#### Even the scary parts

---

### First, a bit about my journey so far

<!-- about me ?-->
---

### November 2015
#### Graduate Software Engineer @ Boeing

- Never used version control before |
- Very scared of git |
- Primarily used PyCharm tools |
- Used Bitbucket for code reviews |

Note:
bitbucket is similar to github in its pull request style. pycharm helped provide and abstraction and i never really needed to look at the git fundamentals.
Open github


---
![Git_commit](assets/image/git-commit.jpg)
---

![Git_commit_last_night](assets/image/commit-msg-last-night.jpg)
---
### July 2017
#### Software Engineer @ RedHat

- Worked on open source Beaker project |
- Use Gerrit for code reviews |
- Now less scared of git (i think...) |

Note:
Gerrit has a single commit CR model. open gerrit.

---

### Topics we'll cover...

- How Git's storage works
- what is a branch
- rebase Vs. merge

---

## Storage

---

### Blob

- Git's representation of the version of a file

![Blob](assets/image/blob.jpeg)

---

### Tree object

- Lists contents of directory
- Stores which filenames correspond to which blob, access modes...
- Points to the blob(s)

![0](assets/image/tree2.jpeg)

---

### Commit object

- Contains commit metadata
- Points to corresponding tree object
- Also points to any parent commit(s)

![Commit](assets/image/commit.jpeg)

Note:
So it can know the state of the files at the time of the commit. No parent means initial commit
---

- Subsequent commits point to corresponding parent


![Many-Commits](assets/image/many-commits.jpeg)

---

## Branch

---

### Git Branch

- A lightweight movable pointer to a commit
- When you add a commit, the pointer moves to new commit
- Can have multiple branches


![Git-branch](assets/image/git-branch.jpeg)

Note:
Also called refs or heads, Its like a post it note or a bookmark that says "im working here". Not stored in history. You can have more than one pointer - more than one branch

---

### Git Branch (cont.)

\> `git checkout -b my-feature master`

![head-ref](assets/image/head-ref.jpeg)

Note:
branched from master. HEAD ref points to active branch.

---

## Rebase & Merge

Note:
now armed with this knowledge lets take a look at rebase and merge and how they work

---
![push-force](assets/image/git-push-force.jpg)
---?image=assets/image/git-push-force.jpg&size=auto 90%

Note:
Dont do this.
---

### Situation after creating the branch

![branch1](assets/image/branch1.jpeg)

---

### Case 1: New commit in master

![master-new-commit](assets/image/master-new-commit.jpeg)

Note:
When you updated master by pulling
---

### Let's try merging

\> `git merge master`


![master-new-commit-merge](assets/image/master-new-commit-merge.jpeg)

Note:
The post it gets moved. You will hear the words fast forward merge for this scenario.
---

### Case 2: Both my-feature and master have new commits

![both-new-commit](assets/image/both-new-commits.jpeg)

---

### Lets try merging again

\> `git merge master`
![both-new-commit-merge](assets/image/both-new-commits-merge.jpeg)

Note:
F is a merge commit. see that it has 2 parents. it incorporates changes from both D and E

---

### After multiple commits & merges

![many-merges](assets/image/many-merges.jpeg)

Note:
we keep merging, and the git history gets littered with merge commits. Because i used gerrit, i was only allowed to have 1 commit per CR, and thats why i had to learn how to rebase.
---

### Case 2: Both my-feature and master have new commits

![both-new-commit](assets/image/both-new-commits.jpeg)

---

### Let's try rebasing this time
\> `git rebase master`

![both-new-commit-rebase](assets/image/both-new-commit-rebase.jpeg)

Note:
A new commit with same changes as E but a different parent. Old commit is garbage collected. pointer moves to new commit. git rebase also works with multiple commits.

---

### Rebase Vs. Merge
- Both achieve the same thing |
- Merge results in a "stitching pattern" |
- Rebase results in a "linear" history |

---

### Some Tips...
- Interactive rebase to amend old commit
\> `git rebase -i master`
- Pulling with rebase strategy
\> `git pull --rebase`
- "Squash"-ing commits with rebase


Note:
normally git pull uses merge, but you can specify that it use rebase instead

---

### Warning

Do not rebase public branches (that others have pushed more commits to).
It will seem like you've "lost" some commits (don't worry - you haven't),
and you will panic.

Note:
It is possible to recover from that. But you dont want to have to do the additional work.
---


### Motivation

git is very forgiving, and its very easy to get out of trouble for the most part.

- you cannot "lose" a commit |
- work on a branch and "test it out" |
- use reflog |

Note:
use cherry-pick

---


### Questions?

<br>

@fa[twitter gp-contact](@AnweshaChatte12)

@fa[github gp-contact](anchat1990)

@fa[medium gp-contact](@anweshachatterjee)

@fa[linkedin gp-contact](/chatterjeeanwesha)

---

### Thank you!
![i-know-git-rebase](assets/image/i-know-git-rebase.jpg)
