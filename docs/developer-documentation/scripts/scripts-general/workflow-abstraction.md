import CommandLineMenu from '../../../_shared-content/command-line-menu.md';


# Workflow abstraction

## Starting point

We start with a collection of markdown files containing terms and definitions. We want to create a “specification” from these markdownfiles. This is going to be an **`index.html`** file.

User Entry **Point** is a Command Line Menu:

<CommandLineMenu />

## End result

The end result is an **`index.html`** file that is “self containing”, in this case meaning that it has all the styling (CSS) and behaviour (JS) and data (a JS variable) inside.

## Menu option `[0] Add content`

Shows simple instructions on how to add content.

## Menu option `[1] Render specification`

Steps:
  |

- - -

<div className="size-big-centered">– BEGIN –</div>

<div className="size-big-centered">– 1 –</div>

### `create-term-index.js`

Read all the user-created **term files** (markdown).

Make an ordered list (JSON) of all the names of the terms files (“**term index**”).


<div className="size-big-centered">↓</div>
<div className="size-big-centered">– 2 –</div>


### `insert-term-index.js`

- Use content of `specs.json` (the **user config file** )
- Insert **term index** in this content
- Create a `specs-generated.json` (**system config file**) from this content.

<div className="size-big-centered">↓</div>
<div className="size-big-centered">– 3 –</div>

### `create-versions-index.js`

Create a directory with a version index (if it does not exist yet).

This page lists all available snapshots of this Spec-Up-T specification

#version #snapshot

<div className="size-big-centered">↓</div>
<div className="size-big-centered">– 4 –</div>

### `prepare-tref.js`

Prepare the markdown files that contain '**[[tref]]**'s as a definition. A '**[[tref]]**' is a term defined in another (“remote” or “external”) specification. The definition (already locally stored in local JSON) is inserted in the file.

The definition is prepended by an html comment stating that everything below is inserted and can safely be removed.

<div className="size-big-centered">↓</div>
<div className="size-big-centered">– 5 –</div>

### `fix-markdown-files.js`

Fix the markdown in the term files.

One blank line between paragraphs, prepend `~` to lines, etc

<div className="size-big-centered">↓</div>
<div className="size-big-centered">– 6 –</div>

### `index.js`

Create a &lt;script&gt; object that contains external data. A local copy of external data are inserted in the `index.html`

<div className="size-big-centered">– END –</div>

- - -

## Menu option `[8] Freeze specification`

Creates a snapshot of the current `index.html` and places it in the version index.

#version #snapshot

