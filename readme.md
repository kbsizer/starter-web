# Git Complete (Udemy Course by Jason Taylor)


### Working out autocrlf issues

Key Question: What is the deal with "warning: LF will be replaced by CRLF"??

#### Example 1: A commit with "autocrlf" set to "true"

```
$ git commit -am "Adding another line"
warning: LF will be replaced by CRLF in hipster.txt.
The file will have its original line endings in your working directory.
[master warning: LF will be replaced by CRLF in hipster.txt.
The file will have its original line endings in your working directory.
f5435f9] Adding another line
warning: LF will be replaced by CRLF in hipster.txt.
The file will have its original line endings in your working directory.
 1 file changed, 3 insertions(+)
```
#### Changing the value of "autocrlf"
```
$ git config --global core.autocrlf false
```
#### Example 2: A commit with "autocrlf" set to "false"

```
$ git commit -am "Adding a third line, after autocrlf change"
warning: LF will be replaced by CRLF in hipster.txt.
The file will have its original line endings in your working directory.
[master warning: LF will be replaced by CRLF in hipster.txt.
The file will have its original line endings in your working directory.
323e0b5] Adding a third line, after autocrlf change
warning: LF will be replaced by CRLF in hipster.txt.
The file will have its original line endings in your working directory.
 1 file changed, 2 insertions(+)
```
### Github instructions on Line Endings with Windows OS

Main article: https://help.github.com/articles/dealing-with-line-endings/

Recommended setting:
```
$ git config --global core.autocrlf true
```
#### Steps to refresh/convert/sync local files after changing line endings:

1. Save your current files in Git, so that none of your work is lost.
```
$ git add . -u
$ git commit -m "Saving files before refreshing line endings"
```
2. Remove every file from Git's index.
```
$ git rm --cached -r .
```
3. Rewrite the Git index to pick up all the new line endings.
```
$ git reset --hard
```
4. Add all your changed files back, and prepare them for a commit. This is your chance to inspect which files, if any, were unchanged.
```
$ git add .
```
Note: At this point, you will probably see a lot of messages that read "warning: CRLF will be replaced by LF in file."  

5. Commit the changes to your repository.
```
$ git commit -m "Normalize all the line endings"
```

#### Results

Good news: The above seems to have done the trick:  Edit/commit/push resulted in no "CRLF" warnings.

Bad news: I do not understand what we just did.

Bad news: Making lined ending commits to the shared/remote repository seems like a Bad Thing.  I don't want to update a zillion files and/or trigger a bunch of Jenkins jobs to resolve my line terminator warnings.

I believe I saw another solution... something about deleting local files, setting line terminator properties, then pulling everything down again.  
