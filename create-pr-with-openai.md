---
title: Turbocharging GitHub PR Creation with Python, OpenAI, and GitHub CLI
date-modified: 2023-07-18
---

Developers who push numerous PRs daily can understand the taxing effort it
takes to consistently pull-off comprehensive titles and descriptions. After
writing great commit messages there should be no need to again write the PR
description - it's essentially the same thing in a different format.

I decided to automate the process of creating PRs. Not only pushing code with
`gh pr create`, but also generating values for title and description.

Using `python` as a glue to combine Git, GitHub CLI (`gh`), and OpenAI's API, I
ended up with a simple script.

I chose to put it as `,pr-create` command. The comma (`,`) is just to make sure
my script does not clash with some other command.

## Script Overview

The complete script is [here in my dotfiles](https://github.com/argshook/dotfiles/blob/master/.argsdotfiles/bin/%2Cpr-create).

It's quite straightforward and easy to copy and use. Make sure `openai` and
`yaspin` python modules are installed. This can be done with a quick `pip
install openai yaspin`

`yaspin` is just for a spinner to indicate progress. Just because I wanted a
few sparks in my terminal. Adjust to fit your use case!

My script does 3 things:

1. Extracts the git log.
1. Summarizes the changes into a clear, concise title and description using
   OpenAI's `gpt-3.5-turbo` model.
1. Pushes a PR to GitHub using [`gh cli`](https://cli.github.com/) with the
   generated title and description.

### Extracting the Git Log

To obtain a history of changes, we first need to determine the base commit from
which the current branch diverged. This can be done using the `git merge-base`
command:

(python code):
```python
base_commit = subprocess.check_output(
    "git merge-base HEAD $(git show-ref --verify --quiet refs/heads/main && echo 'main' || echo 'master')",
    shell=True,
    universal_newlines=True
).strip()
```

After determining the base commit, then we use `git log --pretty` to format the
log:

```python
output = subprocess.check_output(
    f'git log --reverse --pretty=format:"* %s%n%w(0,4,4)%b" {base_commit}..HEAD',
    shell=True,
    universal_newlines=True
)
```

This command retrieves the git log from the base commit to the current `HEAD`,
formatting each commit as a list item and ensuring commit messages and bodies
are properly indented.

### Generating the Title and Description with OpenAI

The OpenAI `gpt-3.5-turbo` model is then used to generate a human-friendly
title and description based on the git log. Using OpenAI API is a breeze with
the official `openai` python module:

```python
response = openai.ChatCompletion.create(
    model='gpt-3.5-turbo',
    temperature=0.2,
    n=1,
    messages=[{'role': 'user', 'content': prompt}]
)
output = response.choices[0].message.content.strip().strip('"')
```

Here, `prompt` is a string that instructs to generate a PR title or description
from the git log. For instance, a `prompt` for the title might look like this:

```python
prompt = f"You are an expert software engineer preparing the title of a PR. Summarize key changes into a short (max 100 chars) PR title from git log:\n\n{text}\n\n"
```

Here `text` is the git log obtained in the previous step.

### Creating the Pull Request

Finally, we combine generated title and description to create a command for
GitHub CLI to create the PR:

```python
command = f'gh pr create --assignee @me --title {title} --body {body}'
```

Eventually this command is executed in the shell, creating the PR.

## Conclusion

By combining Python, OpenAI, and GitHub CLI, we've created a powerful tool that
streamlines PR creation. It frees us from the tedious process of manually
entering PR information and allows us to focus more on coding.

If you'd like to use or further explore this script, you can find the complete
version [here in my dotfiles repo](https://github.com/argshook/dotfiles/blob/master/.argsdotfiles/bin/%2Cpr-create).
