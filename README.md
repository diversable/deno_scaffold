# deno_scaffold

Note: If you haven't yet installed Deno on your machine, see the installation instructions at the bottom of this document, or go read up on Deno here: 
Deno Website: https://deno.land/
Deno Manual: https://deno.land/manual/introduction


This repo is intended as a quick way to set up a [Deno](https://deno.land/) project with some "best practices" described in the Deno manual (eg. https://deno.land/manual/linking_to_external_code and https://deno.land/manual/linking_to_external_code/integrity_checking)

--- Open to pull requests which will make this starter template easier to use - anything that helps you get up and running quickly without regard to the type of project being implemented (CLI, web server, etc) ---


## "Best Practices" - from the [Deno Manual](https://deno.land/manual/introduction)

### The ./src/deps/ts file: Working with ES Module Dependencies Easily

For reference, read the Deno Manual's section on ["Linking to External Code"](https://deno.land/manual/linking_to_external_code):

The Deno manual recommends creating a "./src/deps.ts" file to store your project's dependencies in. In this scaffold, the full suite of Deno's native testing utilities have been re-exported from deps.ts to allow quick access in your own test files.
Just import them in your test files like this:
```js
// in *.test.ts or *.test.js, using ES modules style syntax...
import { assertEquals, runTests, test } from "./deps.ts";

assertEquals("hello", "hello");
assertEquals("world", "world");

console.log("I asserted correctly! 🎉");

// your test code 
```

NOTE: Deno recommends versioning your imports so that your projects don't unexpectedly break if you need to re-load your code. For example, note the version number in the following URL import from Deno's standard library:
```js
import { Response } from "https://deno.land/std@0.53.0/http/server.ts";
```
In this repo, the export in `deps.ts` is not versioned, so that this template doesn't continually become outdated as updates are made to Deno. 
In general, though, following the advice to version your imports/re-exports will make your life easier :)

### Caching dependencies locally

A ./deno_dir file has been added in which you can cache your dependencies locally (rather than in the global, default deno cache, which differs dpending on your OS). 

To download remote dependencies & update the dependency cache, type the following command into your terminal:
```bash
DENO_DIR=./deno_dir deno cache src/deps.ts
```

This will also help others collaborate on your projects with you :)
For more info, see the [Deno Manual's notes on dependency caching](https://deno.land/manual/linking_to_external_code)

### Integrity checking & lock files

There is a lock.json file included at the root of this repo, similar to a lock file you would find in a node.js project. 
In Deno, the lock file is not automatically generated (at this point in Deno's development, anyway). 

However, you can create/update a lock file any time you choose using the following command:
```bash
# Create/update the lock file "lock.json".
deno cache --lock=lock.json --lock-write src/deps.ts
```
For more info, refer to the Deno Manual's section on ["Integrity Checking and Lock Files"](https://deno.land/manual/linking_to_external_code/integrity_checking).

To run your code, remember that Deno is a secure runtime; you need to explicitly enable permissions to allow things like network & file access. 
The available permissions are:
Permissions list
The following permissions are available:


- -A, --allow-all Allow all permissions. This disables all security.
- --allow-env Allow environment access for things like getting and setting of environment variables.
- --allow-hrtime Allow high resolution time measurement. High resolution time can be used in timing attacks and fingerprinting.
- --allow-net=\<allow-net> Allow network access. You can specify an optional, comma separated list of domains to provide a whitelist of allowed domains.
- --allow-plugin Allow loading plugins. Please note that --allow-plugin is an unstable feature.
- --allow-read=\<allow-read> Allow file system read access. You can specify an optional, comma separated list of directories or files to provide a whitelist of allowed file system access.
- --allow-run Allow running subprocesses. Be aware that subprocesses are not run in a sandbox and therefore do not have the same security restrictions as the deno process. Therefore, use with caution.
- --allow-write=\<allow-write> Allow file system write access. You can specify an optional, comma separated list of directories or files to provide a whitelist of allowed file system access.

### Getting Going

#### [Installation Instructions](https://deno.land/#installation)

Deno installation instructions, straight from the Deno homepage:

"""
Deno ships as a single executable with no dependencies. You can install it using the installers below, or download a release binary from the releases page.

Shell (Mac, Linux):
`curl -fsSL https://deno.land/x/install/install.sh | sh`

PowerShell (Windows):
`iwr https://deno.land/x/install/install.ps1 -useb | iex`

Homebrew (Mac):
`brew install deno`

Chocolatey (Windows):
`choco install deno`

Scoop (Windows):
`scoop install deno`

Build and install from source using Cargo
`cargo install deno`
"""


Check out what's in available already in the Deno runtime by reading the [API Docs](https://doc.deno.land/https/github.com/denoland/deno/releases/latest/download/lib.deno.d.ts).

For 3rd party libraries from the quickly-evolving Deno ecosystem, see here: https://deno.land/x


Happy Coding!!!
