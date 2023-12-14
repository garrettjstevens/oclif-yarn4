oclif-yarn4
=================

Example for https://github.com/oclif/oclif/issues/1222.

Here are the steps I used to create this project:

```sh
npx oclif generate oclif-yarn4
# Select "ESM"
# Select "yarn"
# everything else is default
cd oclif-yarn4/
yarn set version berry
echo -e 'node:Linker: pnp\n' > .yarnrc.yml
cat << EOF >> .gitignore
.pnp.*
.yarn/*
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/sdks
!.yarn/versions
EOF
yarn install
```
### Problems

First of all, running `yarn build`, I get this error:
```
../../.yarn/berry/cache/@oclif-core-npm-3.13.1-06065c6868-10c0.zip/node_modules/@oclif/core/lib/cli-ux/styled/progress.d.ts:1:36 - error TS7016: Could not find a declaration file for module 'cli-progress'. '/home/me/.yarn/berry/cache/cli-progress-npm-3.12.0-d686625154-10c0.zip/node_modules/cli-progress/cli-progress.js' implicitly has an 'any' type.
  Try `npm i --save-dev @types/cli-progress` if it exists or add a new declaration (.d.ts) file containing `declare module 'cli-progress';`

1 import { Options, SingleBar } from 'cli-progress';
                                     ~~~~~~~~~~~~~~


Found 1 error.
```

If I add `"skipLibCheck": true` to `tsconf.json`, though, then I am able to build with no errors.

Running `bin/run.js` gives an `ERR_MODULE_NOT_FOUND` error, but that's to be expected with Yarn 4, since you need to run `yarn node` instead of `node` (see [here](https://yarnpkg.com/migration/pnp#call-your-scripts-through-yarn-node-rather-than-node)). Running `yarn node bin/run.js` works fine.

I see that `bin/dev.js` uses some extra flags on `node`, so I tried adding those same flags with `yarn node` like this: `yarn node --loader ts-node/esm --no-warnings=ExperimentalWarning bin/dev.js`, but I get this error.

```
node:internal/process/esm_loader:40
      internalBinding('errors').triggerUncaughtException(
                                ^
Error: Cannot find package '@oclif/core' imported from /home/me/Playground/oclif-yarn4/bin/dev.js
    at packageResolve (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/dist-raw/node-internal-modules-esm-resolve.js:757:9)
    at moduleResolve (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/dist-raw/node-internal-modules-esm-resolve.js:798:18)
    at Object.defaultResolve (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/dist-raw/node-internal-modules-esm-resolve.js:912:11)
    at /home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:218:35
    at entrypointFallback (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:168:34)
    at /home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:217:14
    at addShortCircuitFlag (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:409:21)
    at resolve (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:197:12)
    at nextResolve (node:internal/modules/esm/hooks:864:28)
    at Hooks.resolve (node:internal/modules/esm/hooks:302:30)
```

Thanks to [this comment](https://github.com/yarnpkg/berry/discussions/4044#discussioncomment-5200399), I was able to figure out that I could get it to work by running `yarn add --dev @esbuild-kit/esm-loader` and then running `yarn node --loader @esbuild-kit/esm-loader bin/dev.js`, but **only on Node 18.19**, since that's the only release of 18 that [this PR](https://github.com/nodejs/node/pull/43772) has been backported to.

As for `yarn test`, I get this error, and haven't been able to find any way around it:

```
(node:29104) ExperimentalWarning: The Node.js specifier resolution flag is experimental. It could change or be removed at any time.
(Use `node --trace-warnings ...` to show where the warning was created)
(node:29104) ExperimentalWarning: The Node.js specifier resolution flag is experimental. It could change or be removed at any time.
(Use `node --trace-warnings ...` to show where the warning was created)

✖ ERROR: Error: Cannot find package 'ts-node' imported from /home/me/.yarn/berry/cache/mocha-npm-10.2.0-87db25c7c5-10c0.zip/node_modules/mocha/lib/nodejs/esm-utils.js
    at packageResolve (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/dist-raw/node-internal-modules-esm-resolve.js:757:9)
    at moduleResolve (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/dist-raw/node-internal-modules-esm-resolve.js:798:18)
    at Object.defaultResolve (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/dist-raw/node-internal-modules-esm-resolve.js:912:11)
    at /home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:218:35
    at entrypointFallback (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:168:34)
    at /home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:217:14
    at addShortCircuitFlag (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:409:21)
    at resolve (/home/me/Playground/oclif-yarn4/.yarn/__virtual__/ts-node-virtual-ad0347338b/3/.yarn/berry/cache/ts-node-npm-10.9.1-6c268be7f4-10c0.zip/node_modules/ts-node/src/esm.ts:197:12)
    at nextResolve (node:internal/modules/esm/hooks:864:28)
    at Hooks.resolve (node:internal/modules/esm/hooks:302:30)
```
