# Git, GitHub, and Version Control Quick Tutorial
Yi Fei Chung
2026-09-18

## What is Version Control and Git ?

- Git is a version control system
- “Track Changes” on steroids
- Ensuring reproducibility
- Ease of working collaboratively
  - With peers
  - With past and future self

## How to do Version Control?

- Use a hosting service like **GitHub**, Bitbucket, and GitLab
- Think of these as OneDrive, Google Drive or DropBox
- Good even for private solo projects
  - Track changes
  - Revert when you screw up
  - Publication ready
  - Personal website or ShinyApp

## The Pain! Prep work

- Create an account

  - Types of Account

- Check and install Git

  - What about Updates (not necessary now)

- Get your local Git to talk to Github

- A **Git repository** (commonly called a “repo”) is a digital container
  or project folder that tracks and stores the complete history of
  changes made to files over time.

## Make the **local** and the **remote** talk

There are a few ways to authenticate your local Git with GitHub (i.e.,
to allow your computer to communicate with your GitHub account):

- Method 1: Generating a personal access token through GitHub settings
  - Method 1a: Using HTTPS with personal access token
  - At GitHub.com, go to Settings \> Developer settings \> Personal
    access tokens \> Tokens (classic) \> Generate new token.
  - **Keep this page open** as you will need to copy the token to your
    clipboard.
  - Follow the r code below
- Method 2: Using the Rstudio “usethis” package
  - Follow the R code below
- Method 3: Using Git Bash / Terminal with SSH keys (not covered here)

``` r
if(!requireNamespace(c("usethis", "gitcreds"))){
  install.packages(c("usethis", "gitcreds"))
}
library(usethis)
library(gitcreds)
## Start with Method 2:

# generate a personal access token (PAT) for GitHub using the usethis package
# This is the same as going to GitHub.com and generating a token manually in 1a
usethis::create_github_token()

## Store the personal access token (PAT) 
## This step is the same for both Method 1 and Method 2 after you have generated the token

gitcreds::gitcreds_set()

## Then follow the instructions to paste your personal access token (PAT) into the prompt that appears in RStudio or your terminal. This will securely store your credentials for future Git operations.
```

\*\* GOOD NEWS \*\*: You only need to do this once per computer!!

## Core workflow in RStudio (main focus)

1.  **Create a new repository** in GitHub
2.  **Clone the repository** to your local machine using RStudio

``` r
# Using the usethis package to clone a GitHub repository to your local machine
# Replace "YOUR_USERNAME" and "YOUR_REPO" with your GitHub username
usethis::create_from_github(
  repo_spec = "YOUR_USERNAME/YOUR_REPO",
  destdir = "~/path/to/where/you/want/the/local/repo/",
  fork = FALSE)
```

3.  **Make changes** to your files in RStudio
4.  **Stage and commit** your changes in RStudio
5.  **Pull** any changes from the remote repository (if collaborating)
6.  **Push** your changes to the remote repository on GitHub

## Typical RStudio cycle

- Make a small change.
- Stage only relevant files.
- Commit with a concise message.
- Pull (if needed), then push.
- Repeat in small, understandable steps.

## Same workflow in VS Code and GitHub Desktop (brief)

- **VS Code**: Use Source Control panel for stage/commit/pull/push;
  integrated terminal for Git commands.
- **GitHub Desktop**: Use GUI for commit/sync/branching; open repository
  in editor for coding.
- The logic is still the same: **edit -\> stage -\> commit -\> pull -\>
  push -\> PR**.

## Using GitHub Copilot with Git/GitHub workflows

- Ask Copilot to draft functions, tests, or documentation from
  comments/prompts.
- Use Copilot Chat to explain code, suggest refactors, or generate
  commit message drafts.
- Keep commits small so Copilot-assisted changes are easy to review.
- Always review generated code before committing.

## Common commands

### Terminal (Git Bash)

``` bash
# Check current git version
git --version

# List current git configuration
git config --list

# Show path to git executable
which git

# Update git on Windows
git update-git-for-windows

# Update git on macOS (Homebrew)
brew upgrade git

# Useful daily workflow
git status
git add <file>
git commit -m "your message"
git pull --rebase
git push
```

### R (RStudio or VS Code)

``` r
# Check current git version
system("git --version")

# List current git configuration
system("git config --list")

# Create a GitHub personal access token (HTTPS)
usethis::create_github_token()

# Store GitHub personal access token
# (installs or updates credentials used by git)
gitcreds::gitcreds_set()

# Create local project from a GitHub repository
usethis::create_from_github(
  repo_spec = "https://github.com/YOU/YOUR_REPO.git",
  destdir = "~/path/to/where/you/want/the/local/repo/",
  fork = FALSE
)
```

## Quick best practices

- Commit often with meaningful messages.
- Keep one logical change per commit.
- Pull before push when collaborating.
- Resolve conflicts early.
- Use branches for new features or experiments.
