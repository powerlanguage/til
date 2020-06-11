I often want to discard changes made to a file or group of files. For instance, in this case I want to discard the changes to `WikiPage.jsx`.

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   src/app/components/Wiki/styles.less
	modified:   src/app/pages/WikiPage.jsx
```

With bash I would use

```
git checkout -- *WikiPage*
```

The same command in zsh does not work:

```
git checkout -- *WikiPage*
zsh: no matches found: *WikiPage*
```

> This is related with how ZSH manage globbing characters to generate filenames. By default, ZSH will generate the filenames and throw an error before executing the command if it founds no matches.
> [source](https://superuser.com/questions/584249/using-wildcards-in-commands-with-zsh/584259#584259)

A quick fix is to wrap the wildcards in quotation marks.

```
git checkout -- "*WikiPage*"
```

A more permanent solution is to add `unsetopt NOMATCH` to `.zsh.rc`.

`unsetopt` is the zsh command for changing an option, rather than anything specific to this issue.

The zsh docs for `NOMATCH` say:

> If a pattern for filename generation has no matches, print an error, instead of leaving it unchanged in the argument list. This also applies to file expansion of an initial ‘~’ or ‘=’.
> [source](http://zsh.sourceforge.net/Doc/Release/Options.html)
