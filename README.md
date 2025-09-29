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

I put this in version control so you can have a look: [db/schema.sql](./db/schema.sql).


## Adding Plugins

You can add plugins for roles and organisations, to make user permissions richer.
The `admin` plugin adds a `role` to users. `organization` adds, well, organisations.

Update the `auth.ts` file to add these:


```typescript
import { betterAuth } from "better-auth";
import { admin, organization } from "better-auth/plugins";
import Database from "better-sqlite3";

export const auth = betterAuth({
    database: new Database("./sqlite.db"),
    plugins: [
	    admin(), 
	    organization()
    ]
})
```

See the output in [db/schema-with-admin-and-organization.sql](./db/schema-with-admin-and-organization.sql).

