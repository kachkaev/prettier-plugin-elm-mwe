# MWE for `prettier-plugin-elm`

This demo project tests how Prettier plugins work in various environments. It uses [`prettier-plugin-elm`](https://github.com/gicentre/prettier-plugin-elm).

## Getting started

1.  Install local dependencies

    ```bash
    # cd /path/to/mwe
    yarn install
    ```

1.  Check how a locally installed `prettier`+`prettier-plugin-elm` works from the command line

    ```bash
    yarn prettier ./demo.*
    ```

    Stdout should contain modified versions of `demo.(elm|js|md)`, which look identical to `formatted-demo.(elm|js|md)`.

    Alternatively, you can do

    ```bash
    yarn prettier --write ./demo.*

    ## view the diff
    git diff | cat

    ## reset demo.*
    git checkout -- .q
    ```

If all three files are be prettified as expected, plugins work.

## Testing Atom package

https://github.com/prettier/prettier-atom/issues/395

1.  Install dependencies:

    ```bash
    # cd /path/to/mwe
    yarn install
    ```

1.  If https://github.com/prettier/prettier/issues/4000 is still open, manually apply [this patch](https://github.com/kachkaev/prettier/commit/a5910f886d96cdaa748d2708da78de5a7d643d02) to `/path/to/mwe/node_modules/prettier/index.js` to help Prettier find installed plugins. Search for `externalPlugins = plugins` in this long file an replace the appropriate rows. Beware that `yarn install` in `/path/to/mwe` will reset these changes.

1.  Open a development version of Atom Prettier and start building it continuously (`yarn start build.watch`).

1.  Modify `getOptionsFromSettings()` in [`src/executePrettier/buildPrettierOptions.js`](https://github.com/prettier/prettier-atom/blob/master/src/executePrettier/buildPrettierOptions.js) so that it simply returns `{filepath: getCurrentFilePath(editor)}`.

1.  Open any of `demo.*` files in Atom and manually Prettify them (assuming this is done with the development version of `prettier-atom` after window reload). It should work, even for `demo.elm`.

1.  Activate `formatOnSave` in Prettier Atom package and witness that `demo.md` and `demo.js` files are being formatted on save, wile `demo.elm` does not. Details: https://github.com/prettier/prettier-atom/issues/395#issuecomment-374238950

```

```
