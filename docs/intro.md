---
sidebar_position: 1
---

# Tutorial Intro

Let's discover **Spec-Up-T in less than 5 minutes**.

<video src={require('/static/video/installer-spec-up-t.mp4').default} controls muted autoplay loop></video>

## Getting Started

Get started by **creating a new site**.

### What you'll need

- [Node.js](https://nodejs.org/en/download/):
  - When installing Node.js, you are recommended to check all checkboxes related to dependencies.

## Generate a new site

Generate a new Spec-Up-T site.

```bash
npx create-spec-up-t my-spec-up-t-website
```

*my-spec-up-t-website* can be anything you want it to be (however it is recommended to not use spaces or special characters in directory names).

You can type this command into Command Prompt, Powershell, Terminal, or any other integrated terminal of your code editor.

This will create a working Spec-Up-T installation in a new directory called `my-spec-up-t-website`

- Go into this dir:

```bash
cd my-spec-up-t-website
```

You are now in this dir.

- Install all dependencies:

```
npm run install
```

Look up xrefs:

```
npm run xrefs
```

Now the references to external specs are generated.

Create index.html:

```
npm run render
```

Now an index.html file is created in the `docs` directory. This is the default directory, specified in the `specs.json` file.

Now you have a basic Spec-Up-T install with the following content:

- a `specs.json` file
- a `spec/` directory with a sample markdown files
- (and more)

The`specs.json` file **in the root folder of your repository** specifies configuration values used in the generation of your spec documents. The values in your `specs.json` file include things like where your spec's markdown files are located, where to output the generated spec document, and various metadata values used in rendering, such as the title, logo, and repo links for each of your specs. The following are the required/optional fields supported in the `specs.json` config file:

    - **`public_root`** _(PATH STRING, optional)_ - For some platforms and services where you may want to output your rendered spec, the pathing may differ from the directory structure of your local project. To account for this, you can use the `public_root` property to specify the insertion of a path segment to account for the different in pathing between your local renders and wherever you publish your spec to.
    - **`specs`** _(ARRAY, required)_ - the `specs` array contains descriptor objects for each of the specs you are generating in your project, and are composed of the following required and optional properties:
        - **`spec_directory`** _(STRING, required)_ - You must specify the **repo-root-relative** location of your spec's markdown file directory. You ****MUST**** name your spec's markdown file `spec.md` and locate it in your `spec_directory` for the tool to automatically find and use it for rendering. If you want to use a different name for the markdown file, or you have multiple markdown files you would like the tool to assemble into one document, you must specify them using the optional`markdown_paths` field described below. See the "multi-file" example in the spec-up repo.
        - **`title`** _(STRING, required)_ - You must add a title for your spec, which will be rendered in the generated document's H1 text and page title.
        - **`logo`** _(PATH/URI STRING, optional)_ - You may add a reference to a logo asset, either via a path to the asset or a URI
        - **`logo_link`** _(URI STRING, optional)_ - The URI you want your logo to point to in the rendered page.
        - **`markdown_paths`** _(ARRAY, optional)_ - If you want to name your spec's markdown file something other than `spec.md`, or you have multiple files you would like assembled into a single output document, you must specify their paths as array entries in the order you would like them assembled. The paths in this array are assumed to be based on the `spec_directory` you specified, so _DO NOT_ repeat the full root relative path.
        - **`katex`** _(BOOLEAN, optional)_ - To enable TeX support via KaTeX, set this property to `true`. After rendering, be sure to copy the `fonts/` subdirectory, containing the necessary web fonts.
        - **`output_path`** _(STRING, optional)_ - If you want the generated spec document to be output to a different location than the `spec_directory` you specified (e.g. the project root for GitHub Pages publishing) you can specify another root relative path (use `./` for root), and the tool will write the document file there instead.
        - **`source`** _(OBJECT, optional)_ - this object allows you to configure where repo-specific data is pulled from to power some of the more advanced repo-related features. To do this, specify the code hosting service by adding a service ID string to `host` (currently Spec-Up only supports `"github"`, but this is extensible), add the account/org the repo is located within via the `account` property, and add the repo name under the `repo` property. Here is an example configuration:

            ```
            {
                "host": "github",
                "account": "decentralized-identity",
                "repo": "sidetree"
            }
            ```

You're ready to start rendering specs as HTML sites locally and/or pushing them to github pages however you see fit to automate.

## Running the scripts locally

If your `spec.json` and `package.json` and `package-lock.json` files are in working order and in the root folder of the repo from which it will be deployed, Spec-up can be called by command line (from the root of your repo) in three different modes:

|command|behavior|
|---|---|
|`npm run edit`|after rendering, this will stay running and the `gulp` library will watch the source files in your spec directory/ies for changes and re-render any time you save a file. Opening these rendered files in a browser and refreshing them will keep you up to date.|
|`npm run render`|this renders the site once and does not keep a gulpy watch on the underlying files.|
|`npm run dev`|this enables debugging features.|

## Automation

The above scripts can easily be triggered by github actions.  See [this repo's example](https://github.com/decentralized-identity/spec-up/blob/master/.github/workflows/render-specs.yml)

## Troubleshooting

- WSL2 users are recommended to use the `bash` option rather than `PowerShell` in the terminal of Visual Studio Code.
- Some users have reported problems using spec-up with node versions 15+; to pin to an older version, simple run:

```
nvm install 14
nvm use 14
npm i npm@6.14.16 -g
```
