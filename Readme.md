## Development

### Requirements

- [node](https://nodejs.org/en/)
- [yarn](https://yarnpkg.com/)
- [python3](https://www.python.org/) >= 3.6 (to build zips)
- [web-ext](https://www.npmjs.com/package/web-ext) (for development ease)

### Setup

You will want to run `yarn` to install the development dependencies such as webpack first.

### Making changes

Just use your favorite text editor to edit the files.

You will want to run `yarn watch`.
This will run the webpack bundler in watch mode, transpiling the TypeScript to Javascript and updating bundles as you change the source.

Please note: You have to run `yarn watch` or `yarn build` (at least once) as it builds the actual script bundles.

### Running in Firefox

I recommend you install the [`web-ext`](https://www.npmjs.com/package/web-ext) tools from mozilla. It is not listed as a dependency by design at it causes problems with dependency resolution in yarn right now if installed in the same location as the rest of the dependencies.

If you did, then running `yarn webext` (additionally to `yarn watch`) will run the WebExtension in a development profile. This will use the directory `../GT.p` to keep a development profile. You might need to create this directory before you use this command. Furthermore `yarn webext` will watch for changes to the sources and automatically reload the extension.

Alternatively, you can also `yarn build`, which then builds an _unsigned_ zip that you can then install permanently in a browser that does not enforce signing (i.e. Nightly or the Unbranded Firefox with the right about:config preferences).

### Running in Chrome/Chromium/etc

You have to build the bundles first, of course.

Then put your Chrome into Developement Mode on the Extensions page, and Load Unpacked the directory of your downthemall clone.

### Making release zips

To get a basic unofficial set of zips for Firefox and chrome, run `yarn build`.

If you want to generate release builds like the ones that are eventually released in the extension stores, use `python3 util/build.py --mode=release`.

The output is located in `web-ext-artifacts`.

- `-fx.zip` are Firefox builds
- `-crx.zip` are Chrome/Chromium builds
- `-opr.zip` are Opera builds (essentially like the Chrome one, but without sounds)

### The AMO Editors tl;dr guide

1. Install the requirements.
2. `yarn && python3 util/build.py --mode=release`
3. Have a look in `web-ext-artifacts/dta-*-fx.zip`

### Patches

Before submitting patches, please make sure you run eslint (if this isn't done automatically in your text editor/IDE), and eslint does not report any open issues. Code contributions should favor typescript code over javascript code. External dependencies that would ship with the final product (including all npm/yarn packages) should be kept to a bare minimum and need justification.

Please submit your patches as Pull Requests, and rebase your commits onto the current `master` before submitting.

### Code structure

The code base is comparatively large for a WebExtension, with over 11K sloc of typescript.
It isn't as well organized as it should be in some places; hope you don't mind.

- `uikit/` - The base User Interface Kit, which currently consists of
  - the `VirtualTable` implementation, aka that interactive HTML table with columns, columns resizing and hiding, etc you see in the Manager, Select and Preferences windows/tabs
  - the `ContextMenu` and related classes that drive the HTML-based context menus
- `lib/` - The "backend stuff" and assorted library routines and classes.
- `windows/` - The "frontend stuff" so all the HTML and corresponding code to make that HTML into something interactive
- `style/` - CSS and images
