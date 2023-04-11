---
title: "git repo mirror via github actions"
date: 2023-03-06
categories: [ devops-sre ]
---
## git repo mirror  
I needed a way to mirror a repo so that every time i pushed a new commit to one, it would go to the other.  Pretty simple and straight forward. A little google later and I have a github action that will do it for me and then ignore the job once it lands.  Otherwise the mirror workflow firees on the destination again.   

```
name: Mirroring

on: [push, delete]

jobs:
  to_github:
    runs-on: ubuntu-latest
    if: ${{ github.actor == 'ridingintraffic' }}  # <-- this is to make sure that the mirror only occurs on the source remote
    steps:                                              # <-- must use actions/checkout before mirroring!
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
      - uses: pixta-dev/repository-mirroring-action@v1
        with:
          target_repo_url:
            git@github.com:other-user/other-repo-wiki.git
          ssh_private_key:                              # <-- use 'secrets' to pass credential information.
            ${{ secrets.YOUR_SSH_PRIVATE_KEY }}
```