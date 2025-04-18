---
sidebar_position: 1
---

import CommandLineMenu from '../_shared-content/command-line-menu.md';

# Command Line Menu

You don't have to be a command-line wizard to use Spec-Up-T. There's a menu, so all you have to do is type in a number.

Still, it can be confusing. And if you're used to a regular application you control with your mouse, it takes some getting used to.

## Start command line menu

:::info
Currently, the menu is only tested on MacOs and has not been tested on Windows OS.
:::

:::info
Some of these menu items are available in the GitHub Web-based version (based on Github Actions). But since GitHub Actions cannot be interactive, the “Configure” option for example is not available. That, you will have to do manually.
:::

Assuming you already [installed](../getting-started/local-installation/installation.md) Spec-Up-T, here you find further instructions.

To start, run this command in the terminal:

```bash
npm run menu
```

You will now see this menu:

<CommandLineMenu />

These menu options act as shortcuts to the below commands, such as `npm run render` and others. You can choose between using the menu or entering the direct commands yourself.

### `[0] Add content`

Gives info on how to add content.

### `[1] Render specification`

**Creates the specification, an index.html, in the `docs` directory, as specified in the `specs.json` file.**

To view the `index.html` file, you can:

- Open it via `file:///` in your file manager or
- Access it via HTTP by placing it on a web server.

The easiest way is to double-click the file in your file manager, which should open it in your browser.

By the way, there are **three** modes for rendering the specification:

| Command | Behavior |
|---|---|
| **`npm run edit`** | Renders the site and watches for changes, re-rendering automatically when you save a file. |
| **`npm run render`** | Renders the site once without watching for changes. |
| **`npm run dev`** | Enables debugging features. |

### `[2] Export to PDF`

**Creates a PDF. The PDF will be created in the same directory as the `index.html` file.**

### `[3] Collect external references (cache, faster)`

Also runs [1].

:::info
External references (`xrefs`) are references to external glossaries (specifications).
:::

The info will be taken from the local cache. This only works if there is a cache already, so the first time you run this, it will do the same as option [4]

### `[4] Collect external references (no cache, slower)`

Also runs [1].

:::info
External references (`xrefs`) are references to external glossaries (specifications).

You need a [GitHub Token](../getting-started/github-token.md) when looking up `xref`'s.
:::

### `[5] Add, remove or view xref source`

**See an overview of all external references, or add or delete**

### `[6] Configure`

Configure a new installation.

### `[7] Open documentation website`

This command will redirect to the documentation website (the site you are reading right now).

### `[8] Freeze specification`

**Makes a copy of the `index.html` file and adds a version number to the file name.**

Example: `index-v1.html`, `index-v2.html` etc. These files are placed in the same folder as the `index.html` but in a subfolder called `versions`.

### `[Q] Quit`

This command will take you out of the menu.
