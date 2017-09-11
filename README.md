# npm deleting private modules reproduction case

Simply check out this repo on a clean system (I force cleared the npm cache first)

## npm 5.4.1 is in use and there is a `private` package on disk, that is required by `package.json`

    $ npm -v
    5.4.1

    $ npm ls
    npm-v5-deletes-private-modules-reproduction-case@1.0.0 C:\Users\mike\Documents\npm-v5-deletes-private-modules-reproduction-case
    +-- i-am-installed-but-will-be-deleted-for-no-reason@1.0.0
    `-- lodash@4.17.4

## Installing anything deletes the `private` package

    $ npm install marked
    npm notice created a lockfile as package-lock.json. You should commit this file.
    + marked@0.3.6
    added 1 package and removed 1 package in 1.744s

# The `private` package is now destroyed and an error is produced about the unmet dependency

    $ npm ls
    npm-v5-deletes-private-modules-reproduction-case@1.0.0 C:\Users\mike\Documents\npm-v5-deletes-private-modules-reproduction-case
    +-- UNMET DEPENDENCY i-am-installed-but-will-be-deleted-for-no-reason@^1.0.0
    +-- lodash@4.17.4
    `-- marked@0.3.6

    npm ERR! missing: i-am-installed-but-will-be-deleted-for-no-reason@^1.0.0, required by npm-v5-deletes-private-modules-reproduction-case@1.0.0