## Merge Forward

We use the same setup from Spring Boot to create issues when merging fixes forward. Please see https://github.com/spring-projects/spring-boot/wiki/Working-with-Git-branches.

## Preventing incorrect merges between branches

Since the history of the branches are synced, it is possible to apply a fast-forward merge from a newer branch into an older branch (6.2.x into 5.8.x for example) without any conflicts, and this has caused some problems in the past (see [gh-15028](https://github.com/spring-projects/spring-security/issues/15028)).

Because of that, we created a `pre-push` hook that verifies if the version present in the `gradle.properties` file matches the name of the branch.

### Setup

1. Make sure that you are using [Git Worktree](https://git-scm.com/docs/git-worktree)
2. Run `git config core.hooksPath` to find where Git will look for hooks for that repository. One suggestion is to have it in the parent worktree folder, something like:
```
spring-security
|   .git-hooks <-- here
│   5.8.x
│   6.2.x
|___main
   |__.git
   |__...
```
3. Go to the hooks folder you found:
```bash
cd spring-security/.git-hooks
```
4. Create a symlink for the [`pre-push` script](https://github.com/spring-projects/spring-security/tree/main/git/hooks) into `spring-security/.git-hooks`:
```bash
ln -s ../main/git/hooks/pre-push pre-push
```

And that's it. Now if you try to push your changes and the version from `gradle.properties` does not match the branch name, you will see an error with a message similar to: _"Branch name 6.2.x does not match the version prefix '6.3' in gradle.properties. Make sure you are pushing to the right branch."_