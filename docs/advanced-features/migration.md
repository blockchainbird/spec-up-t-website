---
sidebar_position: 100
---

# Migrate from Spec-Up

**Pre condition: You have a Spec-Up installation up and running**

## When do you need this?

You will need the instructions below if you have a **Spec-Up** installation and want to convert it to **Spec-Up-T**.

## Why would you want this?

Spec-Up-T has more features than Spec-Up.

## What you'll need

- A terminal / Command Line
- An editor, also called IDE (Integrated Development Environment). We recommend Visual Studio Code, but an editor in which you can quickly write Markdown is also good
- [Node.js](https://nodejs.org/en/download/):
  - When installing Node.js, you are recommended to check all checkboxes related to dependencies
  - Use Node.js version 18 or higher
  - If you are running a Spec-Up installation you already have Node.js installed
- A [webbrowser](https://en.wikipedia.org/wiki/Web_browser). You are probably reading this in a browser, so you already have one
- [Git](https://git-scm.com/). To host your specification on Github, you must also have Git installed on your local system. By the way, you can also create a specification (index.html) without hosting it on GitHub. But if you do so, the whole idea of a version-managed glossary using Git goes through the window.

:::note Non-technical Info

Non-technical explanation:

- Command Line: A text interface to type commands for your computer.
- IDE: A software where you can easily write, test, and debug code.
- Node.js: This makes Spec-Up and Spec-Up-T run
- Git: A system to track and manage changes in your code.

:::

## Save your data

Back-up Specs.json to specs-backup.json

Back-up package.json to package-backup.json

```
cp specs.json specs-backup.json
cp package.json package-backup.json
```

Be sure to get the latest specs.json [here](https://github.com/trustoverip/spec-up-t-starter-pack/blob/main/spec-up-t-boilerplate/specs.json) from the starter pack and save into the root of the repo.

## Modify your Spec-Up installation with Spec-Up-T install

We consider migration a task for the roles `developer` or `administrator`.

```
npm install spec-up-t 
```

It's about file management. It's in line with how static website generator generally work. So, be aware that you only organize your files in the migration process, you then configure your configuration files and you're good to go. Spec-Up-T will:

- create the `terms-index.json` in the root of the repo, by the command: `touch terms-index.json`
- if you haven't done before, run [updates](https://blockchainbird.github.io/spec-up-t-website/docs/administrative-and-maintenance-tasks/updating/#4-update)s firs; in brief:
        ```bash
        npm update
        node node_modules/spec-up-t/src/install-from-boilerplate/custom-update.js
        npm run custom-update
        ```

and then:

- `run npm menu` option 1 to generate the glossary in `index.html`
- creates `specs-generated.json` in the output directory, DON'T TOUCH

By hand you have to:

```
cd ./spec
pwd
touch terms-and-definitions-intro.md
```

This creates `terms-and-definitions-intro.md` in the `/spec` directory DON'T TOUCH this file further

### Feel free to reorganize the order of term in the glossary
Open the `terms-index.json` with a text editor in the root of the repo and change the order of terms. You can even throw terms out.

:::note Plan to change
`terms-index.json` will be a file that can't be editted by the user. We'll create the following process:
- a user bypasses a term file (that is in draft) using an `_` (underscore) as the first character of the file name
- a user create a custom order (default: alphabetically) by putting an order number as the first 3 characters of a filename. Example: `10_validator.md`, `15_autonomous-identifier.md`, etc.
  
This method is adopted from Docusaurus.
:::  

### Prepare specs.json


#### We copy the new specs.json structure for Spec-Up-T

```
{
    "specs": [
        {
            "title": "Spec-Up-T Starterpack",
            "spec_directory": "./spec",
            "spec_terms_directory": "terms-definitions", | <- choose your name! |
            "output_path": "./docs",
            "markdown_paths": [
                "intro.md",
            **| copy your .md files here, listed in specs.json-backup, excluding the terminology md files |**
            ],
            "logo": "https://raw.githubusercontent.com/blockchainbird/spec-up-t-starter-pack/main/spec-up-t-boilerplate/logo.svg",
            "logo_link": "https://github.com/blockchainbird/spec-up-t",
            "source": {
                "host": "github",
                "account": "blockchainbird",
                "repo": "spec-up-t-demo-on-documentation-website"
            },
            "external_specs": [
                {
                    "test-1": "https://blockchainbird.github.io/spec-up-xref-test-1/"
                },
                {
                    "test-2": "https://blockchainbird.github.io/spec-up-xref-test-2/"
                }
            ],
            "external_specs_repos": [
                {
                    "external_spec": "test-1",
                    "url": "https://github.com/blockchainbird/spec-up-xref-test-1",
                    "terms_dir": "spec/term-definitions"
                },
                {
                    "external_spec": "test-2",
                    "url": "https://github.com/blockchainbird/spec-up-xref-test-2",
                    "terms_dir": "spec/term-definitions"
                }
            ],
            "katex": false,
            "searchHighlightStyle": "ssi"
        }
    ]
}
```

**Be sure to get the latest specs.json [here](https://github.com/trustoverip/spec-up-t-starter-pack/blob/main/spec-up-t-boilerplate/specs.json)**

Copy your old order of files from `specs-backup.json` and add `terms-and-definitions-intro.md` somewhere in the list (you choose the order!)

#### Alter package.json

Be inspired by the [starterpack](https://github.com/trustoverip/spec-up-t-starter-pack/blob/main/package.spec-up-t.json) package.json file or any closely related spec-up-t based repo that you've already migrated.

> Example : take package.json from the already migrated *KERI specification* when you're in the work of migrating the *ACDC specification*

Follow the instructions here: [Update](https://blockchainbird.github.io/spec-up-t-website/docs/administrative-and-maintenance-tasks/updating)


#### Terms in their own directory

Why has Spec-Up-T put the term definitions in separate files and in a separate directory. The reasons briefly:
- a term def is an atomic piece of information we want to keep version controlled with git
- To be able `tref` and `xref` over glossaries
- levels and languages, with AI we're going to create a tree full of information based on the atomic files in English

To see more explanation, read the [Terminology Governance Guide](https://trustoverip.github.io/ctwg-terminology-governance-guide/).

You should place the terms in their own directory. This directory is defined in specs.json as `spec_terms_directory`.

Alter the configuration according to your wishes and place all term-files the directory. Also see [Organize your Terminology data](#organize-your-terminology-data)

#### Npm Install
Delete your `node_modules` directory and `package-lock.json` file.

Install Spec-Up-T and install all dependencies:
```
npm install
```
:::note Ignore warnings
During the process, you can ignore the npm warnings. 

Keeping up-to-date with warnings would demand a daily effort from programmers and maintainers. Things change so quickly but are hardly ever a breaking change.
:::

:::todo Optional extra check
Do the extra check with the "npm list" command to see whether your install or update command has worked as expected. Check the packages and their latest version numbers. 
:::

Go into the menu

```
npm run menu
```

Add new terms: option 6

Generate the specification

```
npm run menu
1
```

It can take some time, and you should see multiple lines of output during installation.

When the prompt is visible again, you should now have a Spec-Up-T install of your former Spec-Up install:

- a `specs.json` file of the Spec-Up-T structure
- a `spec/` directory with your markdown files
- a `node_modules` directory, and a `package-lock.json` file (these elements belong to the `npm` system together with the earlier processed, modified-by-hand `package.json`)

What you also should have is:

- a `docs` directory with a generated `index.html` file (which is the actual specification file that is the goal of it all).

### Add repo to Github

Follow the steps to take here if you want to use a different account or repo: [Add repo to Github](https://trustoverip.github.io/spec-up-t-website/docs/various-roles/admins-guide/updating/#copy-files-to-the-root-of-your-installation)

## Organize your Terminology data
- Split your Terms and Definition into separate files under a directory in `/spec` directory