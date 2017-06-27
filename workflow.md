# The Development Workflow

The end goal is for the commit history in `master` to tell a logical and descriptive story about the code

Before moving on, find 30 minutes to [watch Stephen Ball's _Deliberate Git_ talk](https://vimeo.com/72762735). This will help you understand how we can make our web development more efficient and sustainable by following this workflow.

### Here's how you do it

#### Always do your work in a feature branch

Remember the 1 rule to, uh, _rule_ them all? Yeah, anything on `master` is deployable. So your work-in-progress should not be done on `master`. That's where feature branching comes in.

1. Start with a clean `master` branch that's deployed on production.

   ```
   $ git checkout master
   $ git pull origin master
   ```

2. Create your feature branch using a semantically-descriptive name with hyphens as separators
   Good examples: `ci-integration` or `homepage-refactor`
   Bad examples: `matt` or  `updates`

   ```
   $ git checkout -b my-feature
   Switched to a new branch 'my-feature'
   ```

#### Make incremental commits throughout your process

As part of your flow it's important to create separate commits for logical groups of code. For example, let's say you're doing some frontend work on a homepage, and as part of that effort you decide to replace a static styles.css stylesheet with a SASS pipeline. In that case you have at least two related but logically distinct sets of changes: The SASS structure and associated dependences, and then the UI changes that have to be made in the CSS and HTML. Once you had built the SASS pipeline you would want to create a commit for that change, probably titled something like "Implement SASS". Next you would move on to your UI updates and roll those into a subsequent commit (which likely touches some of the same files), perhaps called "Update homepage widget styling". Remember - it is always easier to combine tiny commits into a single commit than it is to break a single commit into smaller, more logical commits.

Here's what that commit process would look like. Notice how there are 3 changes highlighted in the status:

- A modified `homepage.html`
- A modified `styles.css`
- A previously unknown and untracked `sass/` directory

```
$ git status
On branch my-feature
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   homepage.html
	modified:   styles.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	sass/

no changes added to commit (use "git add" and/or "git commit -a")
```

First, add your SASS change and confirm that those changes are staged for commit

```
$ git add sass/
$ git status
On branch my-feature
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   sass/_base.scss
	new file:   sass/_custom.scss
	new file:   sass/_uswds.scss
	new file:   sass/styles.css

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   homepage.html
	modified:   styles.css
```
What happened here is that you added the `sass/` directory to Git's version control system, but you have not done anything to the two files that were already being tracked.

Now you're ready to create the Commit that introduces `sass/` to version control.

```
$ git commit
```

If you've configured your default Git editor appropriately then the editor should open to a commit file. Write your commit title and message, then save and close the file to apply the commit.

_Remember to insert an empty line between your title and commit body!_

```
Add SASS pipeline to replace static CSS file

In order to leverage modern CSS techniques such as global variable assignment and precompiling I decided to introduce a SASS pipeline to my-feature. This came as a result of frustrations attempting to make changes to global elements and having to search for each place in the CSS where they were previously declared. For now I'm setting global variables for "padding-top", "line-height", and "light-gray" but these could be supplemented in the future.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch my-feature
# Changes to be committed:
#	new file:   sass/_base.scss
#	new file:   sass/_custom.scss
#	new file:   sass/_uswds.scss
#	new file:   sass/styles.css
#
# Changes not staged for commit:
#	modified:   homepage.html
#	modified:   styles.css
#
```

Once you save and close your commit message you should be returned to your shell, which should pick up where you left off with `$ git commit`

```
$ git commit
[my-feature dcd5bca] Add SASS pipeline to replace static CSS file
 4 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 sass/_base.scss
 create mode 100644 sass/_custom.scss
 create mode 100644 sass/_uswds.scss
 create mode 100644 sass/styles.css
```
And voilà, you've created a meaningful and deliberate commit for your SASS pipeline work. Now you can move on to the rest of the changes in a second commit

```
$ git status
On branch my-feature
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   homepage.html
	modified:   styles.css

no changes added to commit (use "git add" and/or "git commit -a")
```

You can either cherry-pick individual files to stage for commit, as we did with the SASS work, or if all the remaining changes belong in the same commit simply run `$ git add .` to stage all modifications. Then run `$ git commit` and follow the same process as above.

1. Switch your mind from "dev mode" to "writing mode"
   Once all your work is committed it's time to switch to push `my-feature` to the remote, which is probably called `origin`.

   First, double-check that you've successfully committed all of your changes.

   ```
   $ git status
   On branch my-feature
   nothing to commit, working tree clean
   ```

   Then, push `my-feature` to GitHub

   ```
   $ git push origin my-feature
   ```
   This will add `my-feature` to the GitHub remote so other developers can see your work. Keep in mind that throughout all this we have not touched the stable `master` branch, so we always have a clean and stable copy of the code that's live on `Production` that we can revert to at any time.


### Merging code with Pull Requests

- Once your code and commit(s) are in the repository you can invite other developers to review it.
- If you want to compare it against a specific branch then you can open a [Pull Request](https://help.github.com/articles/about-pull-requests/).
- Once your code has been tested and reviewed you are ready to open a Pull Request for `my-feature` into `master`. Set `master` as the _base_ and `my-feature` as the _compare_ branch.
- The PR is the final opportunity to check for code conflicts or to have a team member review the changes.
- When the review is complete you can Accept & Merge the PR. This will add your new commits from `my-feature` into the history of `master`, and should trigger a CI deployment to your production server.
- If you need to make changes, return to `my-feature` and continue your development workflow. Any new commits should be squashed into the relevant original commit. Follow the [steps for performing an interactive rebase](http://www.rakeroutes.com/blog/deliberate-git/#using-git-rebase--i) in the *Deliberate Git* guide.


### Deployment & CI<sup>2</sup>

1. `master` should auto-deploy to the production server
2. `dev` should auto-deploy to the testing server

---

<sup>1</sup> _This is not an official list of supported editors, it's just the editors I've used and have seen teammates use in the past. We should probably have a discussion around city-wide editor licensing._

<sup>2</sup> _This may vary by project and is just meant to serve as a baseline recommendation._
