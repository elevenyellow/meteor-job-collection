#### NEXT

* Decaffeinated this project by carefully using [decaffeinate-project.org](http://decaffeinate-project.org) on the files. Now is required to create an instance of the class with `new Job`, just calling `Job` does not work anymore.

#### 1.5.2

* Fixed issue where errors from `getWork()` calls within `processJobs()` weren't being correctly annotated when passed to the `errorCallback` function. Thanks @bjarketrux.
* Updated dependencies, including test changes for Sinon 2.0 and fibers 2.0
* Documentation improvements

#### 1.5.1

* Fixed issue introduced in 1.5.0 which caused `processJobs()` with arrays of jobType strings to fail a new type check.  Thanks @danielparas!

#### 1.5.0

* Added `errorCallback` option to `job.processJobs()`. This gives workers a way to log network and other errors and do something other than write them to `console.error` (the default and previous behavior).
* Fixed an intermittent unit test failure due to a race condition in a prior test.
* Fixed a deprecation warning on “Job constructor should work without "new"” unit test
* Changed npm prepublish test to prepare test so that coffee-script compile still works on npm install
* Added additional node.js versions to TravisCI tests
* Switch TravisCI to use "trusty" image instead of "precise" to resolve node-gyp build issues for nodejs 7.9
* Updated npm dependencies

#### 1.4.0

* Added support for new "callbackStrict" option to `processJobs()`. When `true` (default `false`) `processJobs()` will throw an error if a worker function calls its callback more than once. Previously it only wrote a message to stderr in all cases. That functionality is preserved with this change.
* Fixed race condition in `processJobs()` that could cause `Job.getWork()` to run after the queue is paused or stopped, leading to a zombie job on the server.
* Added support for new optional `repeatRetries` job document attribute.

#### 1.3.3

* Fixed error affecting all of the *Jobs functions which caused them to only process the first 256 jobs in the provided list of Id values.
* Updated npm dependencies

#### 1.3.2

* Documentation update to support new server-side delayDeps option on `job.done()`.
* Updated npm dependencies

#### 1.3.1

* Don't automatically set the default value of the `repeatId` option to `job.done()` to maintain compatibility with older servers.

#### 1.3.0

* Added ability for workers to specify a timeout for running jobs, so that if they crash or lose connectivity the job can fail and be restarted. Providing a falsy value of option `pollInterval` when calling `Job.processJobs()` will now disable polling in favor of using `q.trigger` exclusively.
* Fixed bug where `q.trigger()` caused a `getWork()` call, even when the queue is paused.
* Added `repeatId` option to `job.done()` which when `true` will cause the successful return value of a repeating job to be the `_id` of the newly scheduled job.
* Added new methods `job.ready()` and `jc.readyJobs()` to move jobs from waiting to ready.

#### 1.2.0

* Added optional `collectionName` parameter to `setDDP`, enabling multiple DDP connections to be used by providing a mapping between collection names and connections.
* Bumped npm deps

#### 1.1.1

* Fixed bug that could cause JobQueue to grab more jobs than configured when `q.trigger()` or very short pollIntervals are used.
* Bumped npm deps

#### 1.1.0

* Added support for using a later.js object as `job.repeat({ schedule: {...} })`
* Bumped npm deps

#### 1.0.0

* j.startJobs and j.stopJobs have been renamed to j.startJobServer and j.shutdownJobServer respectively. The old versions will now generate deprecation warnings.
* Updated README to reflect name change to job-collection and fix broken links to Atmosphere
* Deprecated Job.makeJob(root, doc) in favor of "new Job(root, doc)" constructor signature.
* Added value getters for job.doc, job.type and job.data.
* Added `jq.trigger()` method to provide a mechanism to trigger `getWork` using an alternative method to `pollInterval`
* j.refresh() is now chainable
* Added Fiber support for non-Meteor node.js clients. See `Job.setDDP(ddp, [Fiber])`
* Job constructor now supports supplying an object for `root` if that object has a string attribute named `root`.

#### 0.0.15

* `.fail()` now takes an error object instead of a string, just like `.done()`
* Bumped coffee-script and chai versions
* Fixed broken tests

#### 0.0.14

* Changed validity check in `setDDP`, since ddp npm package no longer does login.

#### 0.0.13

* Remove job_class.js from .gitignore. It causes problems with npm

#### 0.0.12

* Added `until` option for `job.repeat()`, `job.retry()`, job.restart() and job.rerun().
* Added `job.foreverDate` to indicate a Date that will never come
* Added support for the `created` field in a job document

#### 0.0.11

* Updated documentation to reflect a change in the default value of `cancelRepeats` on `job.save()`

#### 0.0.10

* Added support for new `backoff` option to `job.retry()`. Doc improvements.

#### 0.0.9

* Fixed bug in processJobs that caused crash on Meteor.client side. Doc improvements.

#### 0.0.8

* Fixed case where Meteor.setImmediate wasn't being used when available. Documentation improvements

#### 0.0.7

* Erroneous npm publish... no changes from 0.0.6

#### 0.0.6

* Documentation improvements

#### 0.0.5

* Added links to jobCollection on Atmosphere. Fixed a couple of typos.

#### 0.0.4

* Added class constants for DDP Method names and permission levels.

#### 0.0.3

* Numerous small API refinements. Improved docs. Added unit tests for jobQueue.

#### 0.0.2

* Numerous small API refinements. Improved docs. Added extensive unit tests.

#### 0.0.1

* Changed tons of stuff, added documentation

#### 0.0.0

* Initial version
