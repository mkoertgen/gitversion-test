# gitversion-test

This repository is used to test a special edge case in GitVersion where the calculated version on a tag is not correct.
For the history

## History

- 0.1.0: Initial commit
- 0.2.0: Tag
- release/0.3.0: Stabilization Branch
- develop: Development Branch (from release/0.3.0)
- 0.2.1: Hotfix on main
- develop: Merged main/hotfix
- develop: Documentation

## Reproduce

```shell
# Checkout the tag
$ git checkout 0.2.1
Note: switching to '0.2.1'.

You are in 'detached HEAD' state. You can look around, make experimental
...
HEAD is now at 371f96c docs: hotfix on main
# Verify that version is calculated incorrectly on tag
$ gitversion
{
  "Major": 0,
  "Minor": 3,
  "Patch": 0,
  ...
  "SemVer": "0.3.0--no-branch-.1",  // <---- this is wrong!
  ...
  "FullSemVer": "0.3.0--no-branch-.1+1",
  "InformationalVersion": "0.3.0--no-branch-.1+1.Branch.-no-branch-.Sha.371f96c24405d9ace9917d70ea68a1341033aca9",
  ...
}

$ gitversion /diag > gitversion.log

# Checkout the main branch again
$ git switch main
# Verify that main == 0.2.1
$ git log
commit 371f96c24405d9ace9917d70ea68a1341033aca9 (HEAD -> main, tag: 0.2.1, origin/main)
Author: Marcel Körtgen <marcel.koertgen@gmail.com>
Date:   Wed Sep 13 17:55:59 2023 +0200

    docs: hotfix on main

# Verify that version is calculated correctly on main/master branch
$ gitversion
{
  "Major": 0,
  "Minor": 2,
  "Patch": 1,
  "FullBuildMetaData": "Branch.main.Sha.371f96c24405d9ace9917d70ea68a1341033aca9",
  "SemVer": "0.2.1", // <---- this is correct!
```

## Related Issues

- [[Bug] 5.12 bumps major based on the previous merges instead of the last tag and branch convention #3644](https://github.com/GitTools/GitVersion/issues/3644)
- [[Bug] 5.12.0 does not respect tag in Continuous Deployment mode #3614](https://github.com/GitTools/GitVersion/issues/3614)
- [[Bug] Build number in Azure DevOps wrong #3351](https://github.com/GitTools/GitVersion/issues/3351) (Closed)
- [[Bug] GitVersion mainline always returns latest version based on master branch history, even if building for an older commit #3206](https://github.com/GitTools/GitVersion/issues/3206)
- [[Bug] GitVersion increments version on tagged detached HEAD when coming from release branch #2478](https://github.com/GitTools/GitVersion/issues/2478) (Closed)
