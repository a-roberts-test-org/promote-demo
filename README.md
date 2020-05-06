# Example source repository to be promoted using GitOps

Note the directory structure - this is a *source repository* and not a GitOps repository.

This can be promoted into an existing remote GitOps repository with, for example:

```
./services promote --from config --to https://github.com/a-roberts/gitops.git --service myservice
```

https://github.com/a-roberts/gitops-devops.git is a *GitOps* repository.

So what happens here, with the promote?

https://docs.google.com/document/d/102LiAQBc0Mb3ZNSguL1ZhCojvEXOGGtzUdub-e58Mog/edit# outlines the design in more detail, but specifically (for the local "source to GitOps" repository), this happens:

A pull request will be created against the GitOps repository, whereby you will see the `config/deploy.yaml` contents are now in the GitOps repository's `/environments/*environment name*/services/*service name*/base/config` folder. 

In the GitOps repository, is assumed there'll be only one folder under `environments` for now, otherwise you'll have to provide a `--env` flag which I've yet to fully implement and document. If the GitOps repository has `environments/stage`, that would be used as the target folder.

If there are several, you can add `--env prod` for example, and then `environments/prod` will be used as the target folder instead. It is important to note this target folder only exists on the GitOps repository, not your source application's repository.
