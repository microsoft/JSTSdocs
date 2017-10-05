# JavaScript & TypeScript documentation for VS 2017

This repository contains documentation for using the JavaScript and TypeScript languages in VS 2017.

The content is authored using FxDoc, which can be found at https://github.com/dotnet/docfx. See an overview at https://dotnet.github.io/docfx.

## Getting started

Use the below steps to get started quickly:

1. Download the latest DocFx release from https://github.com/dotnet/docfx/releases
2. Unzip the release, and place the directory containing the `docfx.exe` binary on your PATH
3. Edit the YAML and Markdown files in the repository
4. When done, from the root dir run `docfx .\docfx.json --serve`. This will build the site and start a simple web server
5. Open http://localhost:8080 in your browser to view
6. Once happy with your changes, open a pull request to merge them into `master` (including the built output under `./docs`)
7. Once merged, the site content in the `./docs` folder is served via GitHub pages on https://billti.github.io/jsdocs

## Authoring guidelines

 * Navigation does not render well if items are added to the top-level toc.yml file. All content for the site should be authored under the `./articles` directory.
 * Outline the entire content structure in the `./articles/toc.yml` file, following the pattern already in place. Having all navigation in one YAML file as nested items provides for a collapsable navigation tree on the left, rather than navigating to a new section when an item is selected.
 * Place all screen-shots and other images under the `./images` folder, and reference the file via relative paths (e.g. `../../images/foo.png`)
 * Using high-res screen clippings can result in rendering overly large images if using basic Markdown for them. This can be solved by using img tags directly in Markdown and specifying the desired width or height (e.g. `<img src="../../images/sample.png" width="375px"/>`).

## More info

Below is a list of useful links to reference when authoring content:

 * General MarkDown guidance: https://guides.github.com/features/mastering-markdown
 * The DocFx flavor of Markdown: https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html
 * Markdown guidance for Visual Studio docs: https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/styleguide/template.md
 * The tone to use in Visual Studio docs: https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/styleguide/voice-tone.md
 * Guidance for contributing to Visual Studio docs: https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/CONTRIBUTING.md

## Misc

 * In the docfx.json file, the output has been changed from the default `_site` directory to `docs`. This is to allow for simple viewing via GitHub pages. See [Publishing your GitHub pages site from a docs folder](https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/#publishing-your-github-pages-site-from-a-docs-folder-on-your-master-branch) for more info.
 