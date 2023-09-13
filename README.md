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

## Related Issues

- [[Bug] 5.12 bumps major based on the previous merges instead of the last tag and branch convention #3644](https://github.com/GitTools/GitVersion/issues/3644)
- [[Bug] 5.12.0 does not respect tag in Continuous Deployment mode #3614](https://github.com/GitTools/GitVersion/issues/3614)
- [[Bug] Build number in Azure DevOps wrong #3351](https://github.com/GitTools/GitVersion/issues/3351) (Closed)
- [[Bug] GitVersion mainline always returns latest version based on master branch history, even if building for an older commit #3206](https://github.com/GitTools/GitVersion/issues/3206)
- [[Bug] GitVersion increments version on tagged detached HEAD when coming from release branch #2478](https://github.com/GitTools/GitVersion/issues/2478) (Closed)
