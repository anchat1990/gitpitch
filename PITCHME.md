### Understanding Git

#### Even the scary parts

Note:
This is a story of how I overcame my fear of git, and pushed myself to go
further than the basic commands.

---

### First, a bit about my journey so far

Note:
but first I'd like to tell you about my git journey so far
---

### November 2015
#### Graduate Software Engineer @ Boeing

- Never used version control before |
- Very scared of git |
- Primarily used PyCharm tools |
- Used Bitbucket for code reviews |

Note:
bitbucket is similar to github in its pull request style.
pycharm helped provide an abstraction and i never really needed to look at the
git fundamentals. Github allows more than one commit to be associated with a
pull request !Open github! My commit messages were pretty bad too but not as bad
as these...

---
![Git_commit](assets/image/git-commit.jpg)
---

![Git_commit_last_night](assets/image/commit-msg-last-night.jpg)
---
### July 2017
#### Software Engineer @ Red Hat

- Worked on open source beaker-project |
- Use Gerrit for code reviews |
- Less scared of git (I think...) |

Note:
Gerrit has a single commit CR model. Dan said i cant have merge commits in my CRs
, so i need to reluctantly learn rebase.
!open gerrit! In order to understand rebase I needed to understand how
git works under the hood. So...

---

### May 2018

#### Developer @ REA Group

-   Work on www.realestate.com.au/buy |
-   Use Github for code review |
-   First time pairing - multiple people on the same branch |
-   Large team - lots of rebasing! |
-   Now a git cowbow |
-   (not really) |

Note:
trickier operations in git with multiple team members.
Source tree.

---

### Topics we'll cover...

- How git's storage works
- What is a branch
- Rebase Vs. merge

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
the pointer to tree and blobs means it can know the state of the files at the
time of the commit, and it can recreate it from knowledge of the commit itself.
No parent means initial commit. More than one means merge commit.
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


![branch](assets/image/branch1.jpeg)

Note:
Also called refs or heads, Its like a post it note or a bookmark that says
"im working here". Not stored in history. You can have more than one pointer -
more than one branch

---

### Git Branch (cont.)

\> `git checkout -b my-feature master`

![head-ref](assets/image/head-ref.jpeg)

Note:
branched from master. HEAD ref points to active branch. Now armed with this
knowledge of gits storage and branches lets take a look at rebase and merge and
how they work

---

## Rebase & Merge

Note:
Lets find out how to use rebase and merge - what to do, what not to do


---?image=assets/image/git-push-force.jpg&size=auto 90%

Note:
Dont do this.
---

### Situation after creating the branch

\> `git checkout -b my-feature master`

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
F is a merge commit. The merge commit "ties together" history of both branches.
see that it has 2 parents. it incorporates changes from both D and E

---

### After multiple commits & merges

![many-merges](assets/image/many-merges.jpeg)

Note:
we keep merging, and the git history gets littered with merge commits.
Because i used gerrit, i was only allowed to have 1 commit per CR, and thats why
i had to learn how to rebase.
---

### Case 2: Both my-feature and master have new commits

![both-new-commit](assets/image/both-new-commits.jpeg)

---

### Let's try rebasing this time
\> `git rebase master`

![both-new-commit-rebase](assets/image/both-new-commit-rebase.jpeg)

Note:
A new commit with same changes as E but a different parent. Old commit is garbage collected.
pointer moves to new commit. git rebase also works with multiple commits.

---

### Rebase Vs. Merge
- Both achieve the same thing |
- Merge results in a "stitching pattern" |
- Rebase results in a "linear" history |

Note:
Merge is non destructive. The reason why rebase was of special interest to me
was because of the gerrit code review model that i was talking about before.  

---

### Some Tips...
- Interactive rebase to amend/squash/fixup old commits
<br>
\> `git rebase -i master`

---

## Demo time!


Note:
demo* sha1 of the merge commits vs rebased commits
then * see reflog to reset * show log `git log --graph --oneline --all` * rerere
who else gets a bit anxious when they see this message?

---

### Warning

Do not rebase public branches (Branches that others are working on too) without warning your pair!
It will seem like your histories have diverged and it gets messy.

Note:
When you rebase and force push you are rewriting history.
If anyone else is working on a branch, it will be confusing as their changes are based on a different commit to what you have now pushed up, even though it looks like the same commit message. Lastly...
---


### Don't be Scared!

Git is very forgiving, and it's possible to get out of trouble for the most part.

- You cannot "lose" a commit |
- Work on a branch and "test it out" |
- Use reflog |

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
