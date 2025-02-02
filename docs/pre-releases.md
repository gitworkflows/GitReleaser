# Manage pre-releases

With gitreleaser, it's easy to create pre-releases: a version of your software that you want to make available, while
it's not in the stable semver range yet. Often "alpha", "beta", and "rc" (release candidate) are used as identifier for
pre-releases.

An example. The `awesome-pkg` is at version 1.3.0, and work is done for a new major update. To publish the latest beta
of the new major version:

```bash
gitreleaser major --preRelease=beta
```

This will tag and release version `2.0.0-beta.0`. Notes:

- A normal `npm install` of `awesome-pkg` will still be at version 1.3.0.
- The [npm tag][1] will be "beta", install it using `npm install awesome-pkg@beta`
- A GitHub release will be marked as a "Pre-release".

The above command is actually a shortcut for:

```bash
gitreleaser premajor --preReleaseId=beta --npm.tag=beta --github.preRelease
```

Consecutive beta releases (`2.0.0-beta.1` and so on):

```bash
gitreleaser --preRelease
```

And when ready to release the next phase (e.g. release candidate, in this case `2.0.0-rc.0`):

```bash
gitreleaser --preRelease=rc
```

And eventually, for `2.0.0`:

```bash
gitreleaser major
```

<img src="./assets/gitreleaser-prerelease.gif?raw=true" height="524">

When all commits since the latest major tag should be added to the changelog, use `--git.tagExclude`:

```bash
gitreleaser major --git.tagExclude='*[-]*'
```

This will find the latest major matching tag, excluding the pre-release tags, which normally include `-` in their name.

Let's go back to when the latest release was `2.0.0-rc.0`. We added new features, which we don't want in the v2 release
yet, but instead in a later v2.1. A new pre-release id can be made for the minor release after in `2.1.0-alpha.0`:

```bash
gitreleaser preminor --preRelease=alpha
```

Use `--preReleaseBase=1` to start counting at `1`. The first example at `1.3.0` will now bump to `2.0.0-beta.1` instead:

```bash
gitreleaser major --preRelease=beta --preReleaseBase=1
```

Notes:

- Pre-releases work in tandem with [recommended bumps][2].
- You can still override individual options, e.g. `gitreleaser --preRelease=rc --npm.tag=next`.
- See [semver.org][3] for more details about semantic versioning.

[1]: https://docs.npmjs.com/cli/dist-tag
[2]: https://github.com/gitreleaser/conventional-changelog
[3]: http://semver.org
