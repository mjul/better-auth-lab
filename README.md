# better-auth-lab

Trying BetterAuth version 1.6.

See the commit history for Better Auth 1.3, its database schemas are preserved in the `db_v1_3` directory.



## Installation

It is a bit of a time-sink on Windows, since it wants to build the binaries for SQLite when installing. To do so
it needs `node-gyp` and a compiler toolchain and some settings. When it fails you will get error messages but not a lot of
useful information.

In the end I found it easier to do it on Ubuntu. I just had to upgrade it to a recent version of Node (24).

```
    pnpm install
```

## Generating the schema

Now let's generate the schema for the database.

Previously, before version 1.5, it had a command-line tool that we would put under `devDependencies` in `package.json`.
Now with the newer versions we just run it like this:

```bash
    pnpm dlx auth@latest generate --output db/schema.sql
```

I put this in version control so you can have a look: [db/schema.sql](./db/schema.sql).

It requires a BETTER_AUTH_SECRET environment variable to be set, you can generate one with `pnpm` and save it in `.env`:

```bash
    pnpm dlx auth@latest secret
```



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

Now generate the schema like above:

```bash
    pnpm dlx auth@latest generate --output db/schema-with-admin-and-organization.sql
```


See the output in [db/schema-with-admin-and-organization.sql](./db/schema-with-admin-and-organization.sql).

