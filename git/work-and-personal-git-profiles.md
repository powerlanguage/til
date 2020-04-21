I was committing work to this project from my work git profile rather than my personal one.

You can set git profile globally and per project in `.gitconfig`. I wanted a way to say "every git project in this directory should use this profile" without explicitly setting it in each one.

A solution was to create `~/.work.gitconfig` and conditionally append it to `.gitconfig` in certain directories using an `includeIf` statement in the global `.gitconfig`

The later information will overwrite any earlier duplicates. In my case this involved overwriting the `email` field when in a work repo.

```
# global git config
cat `~/.gitconfig`
[user]
	email = mypersonal@email.com
	name = Josh Wardle

# change workdirectory to the path of your work repos
[includeIf "gitdir:~/workdirectory/"]
    path = ~/.work.gitconfig

# work git config
cat ~/.work.gitconfig
[user]
    email = mywork@email.com
```

[source](https://stackoverflow.com/questions/8801729/is-it-possible-to-have-different-git-configuration-for-different-projects)
