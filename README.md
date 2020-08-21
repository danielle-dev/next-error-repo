# Repo to reproduce error after update Next.js from v8 to v9

I created this repository to debug an error we got in [`gva-cms`](https://github.com/gravitybv/gva-cms) after upgrading [`Next.js`](https://nextjs.org/) from v8 to v9.

When running `npm run dev` and `npm run build` we get the same error. The error stack however is a little different. See below.

## Error after `npm run dev`

```
Error: Cannot find module 'webpack'
Require stack:
- /Users/danielle/development/gva-cms/node_modules/@next/react-dev-overlay/lib/middleware.js
- /Users/danielle/development/gva-cms/node_modules/next/dist/server/hot-reloader.js
- /Users/danielle/development/gva-cms/node_modules/next/dist/server/next-dev-server.js
- /Users/danielle/development/gva-cms/node_modules/next/dist/server/next.js
- /Users/danielle/development/gva-cms/.yalc/@tjuna/cms-core/lib/server.js
- /Users/danielle/development/gva-cms/server/index.ts
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:980:15)
    at Function.Module._load (internal/modules/cjs/loader.js:862:27)
    at Module.require (internal/modules/cjs/loader.js:1040:19)
    at require (internal/modules/cjs/helpers.js:72:18)
    at Object.<anonymous> (/Users/danielle/development/gva-cms/node_modules/@next/react-dev-overlay/src/middleware.ts:14:1)
    at Module._compile (internal/modules/cjs/loader.js:1151:30)
    at Module._extensions..js (internal/modules/cjs/loader.js:1171:10)
    at Object.require.extensions.<computed> [as .js] (/Users/danielle/development/gva-cms/node_modules/ts-node/src/index.ts:529:44)
    at Module.load (internal/modules/cjs/loader.js:1000:32)
    at Function.Module._load (internal/modules/cjs/loader.js:899:14)
```

## Error after `npm run build`

```
(node:13068) UnhandledPromiseRejectionWarning: Error: Cannot find module 'webpack'
Require stack:
- /Users/danielle/development/gva-cms/node_modules/@next/react-refresh-utils/ReactRefreshWebpackPlugin.js
- /Users/danielle/development/gva-cms/node_modules/next/dist/build/webpack-config.js
- /Users/danielle/development/gva-cms/node_modules/next/dist/build/index.js
- /Users/danielle/development/gva-cms/node_modules/next/dist/cli/next-build.js
- /Users/danielle/development/gva-cms/node_modules/next/dist/bin/next
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:980:15)
    at Function.Module._load (internal/modules/cjs/loader.js:862:27)
    at Module.require (internal/modules/cjs/loader.js:1040:19)
    at require (internal/modules/cjs/helpers.js:72:18)
    at Object.<anonymous> (/Users/danielle/development/gva-cms/node_modules/@next/react-refresh-utils/ReactRefreshWebpackPlugin.js:3:19)
    at Module._compile (internal/modules/cjs/loader.js:1151:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:1171:10)
    at Module.load (internal/modules/cjs/loader.js:1000:32)
    at Function.Module._load (internal/modules/cjs/loader.js:899:14)
    at Module.require (internal/modules/cjs/loader.js:1040:19)
(node:13068) UnhandledPromiseRejectionWarning: Unhandled promise rejection. This error originated either by throwing inside of an async function without a catch block, or by rejecting a promise which was not handled with .catch(). To terminate the node process on unhandled promise rejection, use the CLI flag `--unhandled-rejections=strict` (see https://nodejs.org/api/cli.html#cli_unhandled_rejections_mode). (rejection id: 1)
(node:13068) [DEP0018] DeprecationWarning: Unhandled promise rejections are deprecated. In the future, promise rejections that are not handled will terminate the Node.js process with a non-zero exit code.
```

# Isolating the issue in this repo

## Setup

This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

## Debug steps taken
- Install npm globally (didn't expect this to work, but was recommended on several StackOverflow issues, e.g. [this one](https://stackoverflow.com/questions/29492240/error-cannot-find-module-webpack))
- Rebuild node_modules
- Upgrade npm for `gva-cms` and `cms-core`, according to this [thread](https://github.com/vercel/next.js/issues/9590#issuecomment-560541692)
