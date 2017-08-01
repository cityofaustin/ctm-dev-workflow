# Continuous Integration

There are many ways that CoA applications can implement and benefit from CI, and how you choose to use it will depend on where your source code lives, how your content gets updated, and where your site is hosted. This section is a work-in-progress and will evolve and expand over time to cover more solutions.

For now, this document will focus on CI for _ColdFusion applications deployed to on-prem servers via our on-prem Enterprise GitHub_.

## Guidelines

As covered in [the workflow guide](../workflow.md), your application should have at least 2 core deployment branches: 1 for production and 1 for testing. You may have an additional testing branch that deploys to a server with slightly different permission and access controls than your main testing branch. This may be called `dev`.

The point of CI is that code updates are _automatically_ published to the appropriate server. Therefore the following automation should be configured:

- `master` should auto-deploy to your production environment
- `test` (or whatever you call it) should auto-deploy to your testing environment
- `dev` (or whatever you call it) should auto-deploy to your dev testing environment

It follows, then, that work _should never be done directly on these branches_. Instead, do your work in a feature branch, verify your changes locally, and then begin testing on the server(s).

## Updating branches

There are 2 ways to get your code updated to a `test` or `dev` branch. You can either merge changes in via a Pull Request or you can force-push your local changes to the desired branch.

Let's say you're working in a feature branch called `add-form-fields`. You've done your work locally and want to see how your feature branch behaves on your `test` server. You can push your changes up and merge `add-form-fields` into `test` via a PR, or you can use the "push _as_" feature to update `test` directly from the command line. Here's what that would look like:

```
$ git push origin add-form-fields:test
```

Notice the `:` between the two branch names? That reads as "_as_". So you're telling Git you want to push the code from `add-form-fields` _as_ the `test` branch. In some cases you might need to force-push if the history on `test` has deviated from the `master` branch you started with when you created `add-form-fields`. In that case, simply add the `—force` flag.

```
$ git push origin add-form-fields:test --force
```

## Tools

### Jenkins

[jenkins.md](jenkins.md)