# How to Change Commit's Author
Sometimes you're working with more than one git account in your machine and forgot to changes default author commit in every repository, and all of that has been pushed into remote repository. After time flies, you relize that you're not supposed to be using wrong email in your repository.

Here's step by step how to change commit author name and email on previous commit.

First, open your Terminal, then enter directory that represent your remote repository.

Copy and Paste this script below into your terminal
```bash
#!/bin/sh

git filter-branch --env-filter '
OLD_EMAIL="example@mail.com"
CORRECT_NAME="Anonymous"
CORRECT_EMAIL="example@mail.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
Things you need consider are :
- `OLD_EMAIL` --> fill with email that want to be changed in your previous commit
- `CORRECT_NAME` --> fill with your real name (usually same with github username)
- `CORRECT_EMAIL` --> fill with your new email address

and then press Enter.


After completed, run this script below in your terminal
```bash
git push --force --tags origin 'refs/heads/*'
```

Done! Check your git-repository history. 
