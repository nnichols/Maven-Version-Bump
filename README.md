# Maven Version Bump

A Shell Script to Bump the Version of Your Maven Projects / POMs

## SemVer and Maven

[SemVer](https://semver.org/) is a nice way to version your projects over time, but managing Maven artifact versions from the command line can be a pain.
While experimenting with Clojure's `tools.deps`, I was suddenly responsible for more artifact maintenance.
All too often, I ended up manually changing the project version in the POM and creating my CHANGELOG entries separately.
So, I adapted some previously used scripts to solve the problem for me.

## Usage

Add the `bin/verchg` shell script to your path, local `/bin` directory, etc and call it with one of the three following options from the directory that houses your `pom.xml`

* 'major'
* 'minor'
* 'bugfix'

For example:

```shell
$ ./bin/verchg 'minor'

[INFO] Scanning for projects...
[INFO]
[INFO] ---------------< com.my-org:awesome-app >-------------------------------
[INFO] Building com.my-org:awesome-app 0.3.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- versions-maven-plugin:2.8.1:set (default-cli) @ awesome-app ---
[INFO] Local aggregation root: /Users/nnichols/awesome-app
[INFO] Processing change of com.my-org:awesome-app:0.3.0 -> 0.4.0
[INFO] Processing com.my-org:awesome-app
[INFO]     Updating project com.my-org:awesome-app
[INFO]         from version 0.3.0 to 0.4.0
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  1.173 s
[INFO] Finished at: 2020-12-03T10:29:36-06:00
[INFO] ------------------------------------------------------------------------
Project is now at 0.4.0
```

### CHANGELOG

If you'd like to automatically update your `CHANGELOG.md` with each invocation, pull `bin/verchglog` instead.
It will scan for the relative path `doc/templates/` for a file `changelog_entry.txt`.
It will pre-pend this entry into your CHANGELOG, and `sed` any references to the variables to `${VER}` and `${DATE}`.

For example:

```
## v${VER} / ${DATE}

> This release ...

```

becomes

```
## v0.4.0 / 2020 Dec 03

> This release ...

```

## Licensing

Copyright © 2020-2021 [Nick A Nichols](https://nnichols.github.io/)

Distributed under the [MIT License](https://opensource.org/licenses/MIT)
