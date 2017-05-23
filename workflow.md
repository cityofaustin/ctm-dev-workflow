# Basic application development guidelines

1. Each repo should have 2 core branches and any number of additional feature branches

   - `master` 
      There's only one rule: **anything in the `master` branch is always deployable**. Work should never be done in this branch. Changes should be merged in via Pull Request.
   - `dev` 
      This is not meant to be a stable branch, but instead a way for developers to test their work in an environment that more closely matches `Prod`. As a result, it might be regularly destroyed and re-cloned from `master`.
   - Feature branches - These are branches that are actively being worked on. They should contain descriptive names that inform anyone browsing the repo what work is being done. For example, `add-uswds` would be a better name than `matts-frontend` for a feature branch that adds the U.S. Web Design Standards to the project.

2. Create a README (see the [template](README.md) in this repo)

3. Doing work:
   Starting with a clean `master` branch that's deployed on production and a `dev` branch cloned from that clean master branch...

   1. Create your feature branch 
      ```
      # First, make sure you're in master
      $ git checkout master
      Your branch is up-to-date with 'origin/master'.

      # Create the feature branch
      $ git checkout -b my-feature
      Switched to a new branch 'my-feature'
      ```

   2. … Do your work ...

   3. Once your work is complete it's time to add and commit your changes to the branch. Refer to the *Writing Commit Messages* section of the [CoA Git Guide](http://pages.austintexas.io/guides/developer-guide/git/) for best practices.

      ```
      # Add all of your changes to commit
      $ git add .

      # Commit the changes and open your Git default text editor to supply a commit message
      $ git commit

      # Push to the feature branch
      $ git push origin my-feature
      ```

4. Merging code with Pull Requests

   - Once your code and commit(s) are in the repository you can invite other developers to review it.
   - If you want to compare it against a specific branch then you can open a [Pull Request](https://help.github.com/articles/about-pull-requests/).
   - Once your code has been tested and reviewed you are ready to open a Pull Request for `my-feature` into `master`.
   - The PR is the final opportunity to check for code conflicts or to have a team member review the changes.
   - When the review is complete you can Accept & Merge the PR. This will add your new commits from `my-feature` into the history of `master`, and should trigger a CI deployment to your production server.

5. Commit cleanup

   1. If you need to make changes, return to `my-feature` and continue your development workflow. Any new commits should be squashed into the relevant original commit. Follow the [steps for performing an interactive rebase](http://www.rakeroutes.com/blog/deliberate-git/#using-git-rebase--i) in the *Deliberate Git* guide.

6. Deployment & CI

   1. `master` should auto-deploy to the production server
   2. `dev` should auto-deploy to the testing server