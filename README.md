# 33149

## Current behavior

In `terraform` we use modules stored in git repositories.

Example
`tf-role-aws-rds` calls the following module:
```hcl 
module "asg_security_group" {
  source = "git::https://github.com/ricardoleal/package-repo.git?ref=1.0.0"
}
```
We are getting the following WARN:
```
❯ npx renovate
(node:78322) [DEP0040] DeprecationWarning: The `punycode` module is deprecated. Please use a userland alternative instead.
(Use `node --trace-deprecation ...` to show where the warning was created)
 INFO: Repository started (repository=ricardoleal/minimal-reproduction-template)
       "renovateVersion": "37.440.7"
 INFO: Dependency extraction complete (repository=ricardoleal/minimal-reproduction-template, baseBranch=main)
       "stats": {
         "managers": {"terraform": {"fileCount": 1, "depCount": 1}},
         "total": {"fileCount": 1, "depCount": 1}
       }
 WARN: Error updating branch: update failure (repository=ricardoleal/minimal-reproduction-template, branch=renovate/pin-dependencies)
(node:78322) TimeoutNegativeWarning: -1000 is a negative number.
Timeout duration was set to 1.
```

Strange fact if we change module definition to `?ref=tags/1.0.0` renovate do the update correctly for `?ref=1.0.0` but after that keep giving the same WARN and don't create the branch and MR.

This was tested in private gitlab and this public github

## Expected behavior

Create branch and merge request

## Link to the Renovate issue or Discussion

https://github.com/renovatebot/renovate/discussions/33149#

