# Lerna script bug sample

## Configuration
- node 14
- npm 6
- useNx: true in lerna.json

## Setup

```
npm install
npm run test
```

## Expected
```
> nx-npm-script-name-bug@1.0.0 test /dev/nx-task-name-bug
> lerna run script:with:colon

lerna notice cli v5.1.6
lerna info Executing command in 1 package: "npm run script:with:colon"
lerna info run Ran npm script 'script:with:colon' in '@mybug/module-with-colon-script' in 0.3s:

> @mybug/module-with-colon-script@1.0.0 script:with:colon /dev/nx-task-name-bug/packages/module-with-colon-script
> echo This Works!

This Works!
lerna success run Ran npm script 'script:with:colon' in 1 package in 0.3s:
lerna success - @mybug/module-with-colon-script
```

## Actual
```
> nx-npm-script-name-bug@1.0.0 test /dev/nx-task-name-bug
> lerna run script:with:colon

lerna notice cli v5.1.6
Error: Cannot find configuration for task @mybug/module-with-colon-script:script
    at getExecutorNameForTask (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/utils.js:123:15)
    at getExecutorForTask (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/utils.js:129:22)
    at getCustomHasher (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/utils.js:136:25)
    at TasksSchedule.<anonymous> (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/tasks-schedule.js:112:62)
    at Generator.next (<anonymous>)
    at /dev/nx-task-name-bug/node_modules/tslib/tslib.js:118:75
    at new Promise (<anonymous>)
    at Object.__awaiter (/dev/nx-task-name-bug/node_modules/tslib/tslib.js:114:16)
    at TasksSchedule.hashTask (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/tasks-schedule.js:111:24)
    at TasksSchedule.<anonymous> (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/tasks-schedule.js:59:24)
Unexpected error:
Error: Unable to load hasher for task "@mybug/module-with-colon-script:script"
    at getCustomHasher (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/utils.js:141:15)
    at TasksSchedule.<anonymous> (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/tasks-schedule.js:112:62)
    at Generator.next (<anonymous>)
    at /dev/nx-task-name-bug/node_modules/tslib/tslib.js:118:75
    at new Promise (<anonymous>)
    at Object.__awaiter (/dev/nx-task-name-bug/node_modules/tslib/tslib.js:114:16)
    at TasksSchedule.hashTask (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/tasks-schedule.js:111:24)
    at TasksSchedule.<anonymous> (/dev/nx-task-name-bug/node_modules/nx/src/tasks-runner/tasks-schedule.js:59:24)
    at Generator.next (<anonymous>)
    at /dev/nx-task-name-bug/node_modules/tslib/tslib.js:118:75
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! nx-npm-script-name-bug@1.0.0 test: `lerna run script:with:colon`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the nx-npm-script-name-bug@1.0.0 test script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /.npm/_logs/2022-06-30T16_10_59_095Z-debug.log
```
