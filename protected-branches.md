# Protecting the master branch

There's only one rule about branches: **anything in the `master` branch is always deployable**.

#### Work should _never_ be done in this branch.

Instead of working in master, changes should be merged in via Pull Requests from other feature branches or from a fork.

To this end, you should protect the `master` branch to encourage code reviews before changes are merged and deployed. This will prevent work from being performed directly on `master`, and will foster collaboration among CoA developers.

1. In your repository navigation to Settings > Branches
2. Under "Protected Branches" select `master`
3. Enable the following settings:
   1. Protect this branch
   2. Require pull request reviews before merging
   3. Dismiss stale pull request approvals when new commits are pushed
   4. Include administrators

Some developers have (rightly) expressed concern about this review process potentially delaying critical fixes from going in in response to a fire drill. Fret not! Owners of the repository and the Organization it lives in can always force the merge even if the PR hasn't been reviewed by a 3rd-party.