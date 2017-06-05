# Application Development Guidelines

## Setting up your local environment

1. Install one of the CTM supported code editors<sup>1</sup>
   - Atom
   - Coda
   - Dreamweaver
   - Eclipse
   - Netbeans
   - Sublime
   - TextMate
2. Set your editor as the default Git editor, and tell Git to wait for you to to supply a commit title and body before proceeding with a Commit or a Rebase
   Instructions: [Mac](https://help.github.com/articles/associating-text-editors-with-git/#platform-mac) | [Windows](https://help.github.com/articles/associating-text-editors-with-git/#platform-windows) | [Linux](https://help.github.com/articles/associating-text-editors-with-git/#platform-linux)
3. Quit and re-launch your shell

## Setting up your repository

### Branching

Each repo should have at least 2 core branches and any number of additional feature branches

- `master` - There's only one rule: **anything in the `master` branch is always deployable**. Work should never be done in this branch. Changes should be merged in via Pull Request. `master` deploys to `Production`.
- `dev` - This is not meant to be a stable branch, but instead a way for developers to test their work in an environment that more closely matches `Production`. As a result, it might be regularly destroyed and re-cloned from `master`.
- `test` - This is a pre-production environment with database permissions and access that match those on `Production`. This distinction from `dev` might not always apply to all feature branches. The important thing is that the environments are sufficiently documented in your `README`.
- Feature branches - These are branches that are actively being worked on. They should contain descriptive names that inform anyone browsing the repo what work is being done. For example, `add-uswds` would be a better name than `matts-frontend` for a feature branch that adds the U.S. Web Design Standards to the project.

### README

A thoughtful and thorough `README` makes it easy for your peers to quickly understand how your application works and how to contribute to it. Start with [this template](README.md) and modify as appropriate for your project. This repo contains [a robust example](examples/alt-cityspace.md) from the CitySpace project for reference as you decide what to put into yours.

## Doing work

#### Assumptions:

1. You have already set up your GitHub account(s) and have _write_ access to the repo you want to work on
2. You're using _Windows_ or _OS X_
   (If you're running _Linux_ this workflow is still equally applicable, but some system configurations might require different steps or in some cases might not be achievable, but you already knew that because you're a Linux person :stuck_out_tongue:)
3. You understand the basics of a command line interface and have a shell installed on your computer (likely _Terminal_ if you're on OS X or _CMD.exe_ if you're on Windows)


#### Developing

1. Start with a clean `master` branch that's deployed on production and a `dev` branch cloned from that clean master branch.

2. Create your feature branch, making sure your base is the current `master` state

   1. Make sure master is up-to-date

      ```
      $ git checkout master
      $ git pull
      ```

   2. Create your feature branch, using a semantically-descriptive name with hyphens as separators
      Good examples: `ci-integration` `homepage-refactor`
      Bad examples: `matt` `bug-fixes`

      ```
      $ git checkout -b my-feature
      Switched to a new branch 'my-feature'
      ```

3. Do your work...

   -  Create separate commits for logical groups of code. For example, let's say you're doing some frontend work on a homepage, and as part of that effort you decide to replace a static styles.css stylesheet with a SASS pipeline. In that case you have at least two related but logically distinct sets of changes: The SASS structure and associated dependences, and then the UI changes that have to be made in the CSS and HTML. Once you had built the SASS pipeline you would want to create a commit for that change, probably titled something like "Implement SASS". Next you would move on to your UI updates and roll those into a subsequent commit (which likely touches some of the same files), perhaps called "Update homepage widget styling". Remember - it is always easier to combine tiny commits into a single commit than it is to break a single commit into smaller, more logical commits.

      Here's what that commit process would look like

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
      Now you're ready to create your Commit for the SASS changes

      ```
      $ git commit
      ```

      If you've configured your default Git editor appropriately then the editor should open to a commit file. Write your commit title and message, then save and close the file to apply the commit. Remember to insert an empty line between your title and commit body.

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

4. Once all your work is committed it's time to push `my-feature` to the remote, which is probably called `origin`.
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
