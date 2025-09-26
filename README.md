# better-auth-lab
Trying BetterAuth.

## Installation
It is a bit of a time-sink on Windows, since it wants to build the binaries for SQLite when installing. To do so
it needs `node-gyp` and a compiler toolchain and some settings. When it fails you will get error messages but not a lot of
useful information.

In the end I found it easier to do it on Ubuntu. I just had to upgrade it to a recent version of Node (24).

```
    npm install
```

## Generating the schema
Then to generate the schema for the database:

```
    npx @better-auth/cli generate --output db/schema.sql
```

I put this in version control so you can have a look.



