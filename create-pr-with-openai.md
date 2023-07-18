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

If you want to use it, make sure `openai` and `yaspin` python modules are
available. This can be done with a quick `pip install openai yaspin`

`openai` is used to receive completion from [OpenAI](https://openai.com/) API
and `yaspin` is for a spinner to indicate progress. Just because I wanted a few
sparks in my terminal. Adjust to fit your use case!

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

Once we have `base_commit`, then we use it in `git log --pretty` to retrieve and format the log:

```python
output = subprocess.check_output(
    f'git log --reverse --pretty=format:"* %s%n%w(0,4,4)%b" {base_commit}..HEAD',
    shell=True,
    universal_newlines=True
)
```

This command also formats each commit as a list item, ensuring commit messages
and bodies are properly indented.

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
prompt = f"You are an expert software engineer preparing the title of a PR. Summarize key changes into a short (max 100 chars) PR title from git log:\n\n{log}"
```

Here `log` is the git log obtained in the previous step.

### Creating the Pull Request

Finally, we combine generated title and description to create a command for
GitHub CLI to create the PR:

```python
command = f'gh pr create --assignee @me --title {title} --body {body}'
```

Eventually this command is executed in the shell, creating the PR.

## Conclusion

By combining Python, OpenAI, and GitHub CLI, I now have a great tool to speed up PR creation. Once i'm ready to push changes to GitHub, all is needed is to run `,pr-create`.

After typing hundreds of PR titles and descriptions, this little trick feels like an incredible time saver.

Granted, titles and descriptions aren't always on-point. Nonetheless, it's much easier to quickly edit a few logic mistakes in text instead of starting from empty text field. 

If you'd like to use or further explore this script, you can find the complete
version [here in my dotfiles repo](https://github.com/argshook/dotfiles/blob/master/.argsdotfiles/bin/%2Cpr-create).
