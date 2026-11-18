# git_mentorship

## what it is

a practice area for the basic Git workflow: make a branch, change a file, commit, push, open a pull request, merge, and fix a conflict. the folder has no code, only text files to change:

| file | what it is |
| --- | --- |
| `teddy.txt` | the mentor's practice file, one line of text |
| `EricText1.txt` | a mentee's practice file, one short line |
| `CONTRIBUTING.md` | the generic fork, branch, commit, push, pull request steps |
| `.gitattributes` | line-ending normalization (`* text=auto`) |

the history in this repository shows the exercise as it was done: a text file created on a branch, a pull request merged from branch `eric`, and later commits that edit the files.

## when to use it

- your first week with Git, with a mentor who reviews your pull request.
- to see what a small pull request history looks like (`git log --oneline --graph`).

when not to use it:

- you only need to read code or run tests: use https://github.com/ClasherGeek77/pytest_web_boilerplate
- you want a team workflow with CI: use https://github.com/ClasherGeek77/katalon_api_boilerplate (it has a GitHub Actions history on its `legacy` branch)

## what you need

- Git, from https://git-scm.com/downloads (any current version).
- a GitHub account, and a fork of this repository if you do not have write access.
- no other install.

## quick start, in this order

do the steps in the folder, with your own file name instead of `yourname.txt`:

```bash
git clone https://github.com/<your-user>/qa_training.git
cd qa_training/git_mentorship
git checkout -b yourname/add-file
echo "hello from yourname" > yourname.txt
git add yourname.txt
git commit -m "add yourname.txt"
git push -u origin yourname/add-file
```

then, on GitHub:

1. open a pull request from your branch to `main` (the default branch of this repository on GitHub).
2. ask the mentor to review it, then merge it.
3. back in the terminal, update your copy: `git checkout main && git pull`.

second round, on purpose with a conflict:

1. create two branches from `main`, both editing line 1 of the same file.
2. merge the first one, then merge the second: Git stops with a conflict.
3. open the file, keep the lines you want, delete the `<<<<<<<`, `=======` and `>>>>>>>` markers, then `git add` the file and `git commit`.

you should see your branch in the pull request list, then your file on `main` after the merge. not run here: it needs a GitHub fork and a reviewer.

## how to read the code

- run `git log --oneline --graph --all` in this repository and find the pull request merge commits.
- run `git show <commit>` on the commit that created `teddy.txt` to see what a one-file change looks like.
- the commits come from the original small practice repository; the folder keeps all of them.

## if it breaks

| symptom | cause | fix |
| --- | --- | --- |
| `Permission denied` or `403` on `git push` | you cloned the original repository without write access | fork it on GitHub, clone your fork |
| `failed to push some refs ... non-fast-forward` | the remote branch has commits you do not have | `git pull --rebase`, then push again |
| `CONFLICT (content)` on merge | two branches changed the same lines | edit the file, remove the markers, `git add`, `git commit` |
| `Please tell me who you are` | no name or email set | `git config --global user.name "Your Name"` and `git config --global user.email "you@example.com"` |
| `git checkout main` says the branch does not exist | the default branch has another name | run `git branch -a` and use the name you see |

## next

- Git inside a real test project: https://github.com/ClasherGeek77/pytest_web_boilerplate
- the rest of this training repo: https://github.com/ClasherGeek77/qa_training
- the Katalon exercises: https://github.com/ClasherGeek77/qa_training/tree/HEAD/api_automation_katalon and https://github.com/ClasherGeek77/qa_training/tree/HEAD/web_automation_katalon
