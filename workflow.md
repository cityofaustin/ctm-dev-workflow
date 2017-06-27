# The Development Workflow

The end goal is for the commit history in `master` to tell a logical and descriptive story about the code

Before moving on, find 30 minutes to [watch Stephen Ball's _Deliberate Git_ talk](https://vimeo.com/72762735). This will help you understand how we can make our web development more efficient and sustainable by following this workflow.

This guide will cover 3 facets of the workflow:

1. Writing code
2. Generating a clean and thorough commit history
3. Reviewing and merging code into deployable branches via Pull Requests

## The coding process

### Always do your work in a feature branch

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

### Make incremental commits throughout your process

As part of your flow it's important to create separate commits for logical groups of code. For example, let's say you're doing some frontend work on a homepage, and as part of that effort you decide to replace a static styles.css stylesheet with a SASS pipeline. In that case you have at least two related but logically distinct sets of changes: The SASS structure and associated dependences, and then the UI changes that have to be made in the CSS and HTML. Once you had built the SASS pipeline you would want to create a commit for that change, probably titled something like "Implement SASS". Next you would move on to your UI updates and roll those into a subsequent commit (which likely touches some of the same files), perhaps called "Update homepage widget styling".

Along the way it is recommended that you incrementally commit your work-in-progress. For this you can use the `-m` flag in your commit to write a quick commit title directly from terminal. In the example above, when you created the `sass/` directory you might have run:  

```
$ git add sass/
$ git commit -m "wip create initial sass directory"
```

It's okay that your SASS work was incomplete up to that point. Again, the goal is to make many small commits that can later be combined into more cohesive groupings. Remember - it is always easier to combine tiny commits into a single commit than it is to break a single commit into smaller, more logical commits.

Then, once you have changes on `homepage.html`, you could follow the same process to isolate that work:  

```
$ git add homepage.html
$ git commit -m "wip initial homepage UI updates"
```

Even if you had already made changes to `homepage.html` and `sass/`, you can still _stage_ those changes and commit them separately by using `$ git add [thing(s)-you-want-to-stage]` instead of `$ git add .`, which assumes you want to include all of your local changes into a single commit. You can also add multiple individual things to a single commit. Let's say that after the pipeline was created you wanted to add a separate SASS file for footer styling. This would consist of at least 2 file changes - the `_footer.scss` styles and the `@import 'footer'` declaration in `styles.css`. Since those changes relate to a single logical item of work it makes sense for them to be in the same commit. To stage them both and commit you can do:  

```
$ git add _footer.scss
$ git add styles.css
```

OR you can add them both in a single declaration  

```
$ git add _footer.scss styles.css
```

Of course if those are your only local changes you could still do `$ git add .` but it's helpful to know all the different ways to go from local file changes to an update in the Git changelog.

### Push your commits to the remote

Even if you're not done working yet it's a good idea to push your changes to the GitHub remote. This allows you to get feedback on your work (if desired) and provides a safe backup of your code in case your local branch gets unwieldy.

```
$ git push origin my-feature
```

## The cleanup process

Once your code changes are complete it's time to turn the messy commit history into clear stories about the changes you made.

Follow the instructions in [rebase.md](rebase.md) to rewrite your commit history to provide titles and messages that will be useful for anyone else who might have to work on the app in the future.

## The review process

[Pull Requests](https://help.github.com/articles/about-pull-requests/) are the cornerstone of the development workflow. They allow us to get feedback on our changes, to isolate work-in-progress from deployed environments, and to 

Ultimately your commits from `my-feature` will need to get merged into `master` in order for them to be deployed to your application's `Production` environment.

### Merging code with Pull Requests

- Once your code and commit(s) are in the repository you can invite other developers to review it.
- If you want to compare it against a specific branch then you can open a [Pull Request](https://help.github.com/articles/about-pull-requests/).
- Once your code has been tested and reviewed you are ready to open a Pull Request for `my-feature` into `master`. Set `master` as the _base_ and `my-feature` as the _compare_ branch.
- The PR is the final opportunity to check for code conflicts or to have a team member review the changes.
- When the review is complete you can Accept & Merge the PR. This will add your new commits from `my-feature` into the history of `master`, and should trigger a CI deployment to your production server.
- If you need to make changes, return to `my-feature` and continue your development workflow. Any new commits should be squashed or fixed-up into the relevant original commit. Follow the [steps for performing an interactive rebase](http://www.rakeroutes.com/blog/deliberate-git/#using-git-rebase--i) in the *Deliberate Git* guide.



