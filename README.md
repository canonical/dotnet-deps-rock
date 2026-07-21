# dotnet-deps rock

This repository contains the `dotnet-deps` rock. Each supported track is
maintained in its own branch.

## Table of Contents

- [Setup Instructions](#setup-instructions)
- [Directory Structure](#directory-structure)
- [Building the Rock](#building-the-rock)

## Setup Instructions

### 1. Repository setup

Check GitHub's documentation on [creating a repository from a template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)

#### 1.1. Create secrets, if needed

> [!IMPORTANT]
> If your repository is **internal** or **private**, you need to create the
> following secrets in your repository:
>
> - `REPO_CLONER_TOKEN`: use a [fine grained token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-fine-grained-personal-access-token) with `read:content` and
> `read:metadata` permissions. **Make sure the token's "resource owner" is _canonical_**, and has access to the right repositories (not just public in this case).
> Also, please note that fine-grained tokens have an expiration date. So if and when experiencing CI problems checking out the repository, make sure the token is still valid.

### 2. Customize the Template

This template comes with a basic setup to get you started. Here's what you need to customize:

- **Track branches**: The branch name is the track, for example `9.0-25.04` or `10.0-26.04`.
- **`rockcraft.yaml`**: Each track branch contains its recipe at the repository root. See the [Rockcraft reference](https://documentation.ubuntu.com/rockcraft/en/stable/reference/rockcraft.yaml/).
- **`.github/workflows`**: Shared workflow implementations live on `main`. Track branches contain callers that reuse those workflows.
- **`CODEOWNERS`**: Optional, but recommended. Read more about [CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners).

## Directory Structure

The `main` branch contains shared repository files and reusable workflows. A
track branch contains the rock recipe at its root:

```
rockcraft.yaml                # Rock project file for this track
spread/                       # Track-specific integration tests
.gitignore
CODEOWNERS                    
README.md
SECURITY.md
```

## Building, testing and uploading the Rock

To build, test and upload a track, commit changes to its track branch and check
the GitHub actions. The branch workflows call the reusable workflows from
`main`.

> [!NOTE]
> Before committing your `rockcraft.yaml`, it is recommended that you `pack` it
> with [Rockcraft](https://snapcraft.io/rockcraft) run a smoke test locally.
> Check the [Rockcraft documentation](https://documentation.ubuntu.com/rockcraft) to learn more.

## Sync with template

A `Makefile` is provided to sync the repository with the latest template changes. To do so, simply run:

```bash
make sync-with-template
```
