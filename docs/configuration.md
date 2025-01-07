# Configuration

Out of the box, gitreleaser has sane defaults. See the [configuration options][1] to configure it.

Put only the options to override in a configuration file. Here is a list of file names where gitreleaser looks for
configuration in the root of the project:

- `.gitreleaser.json`
- `.gitreleaser.ts`
- `.gitreleaser.js` (or `.cjs`; export the configuration object: `module.exports = {}`)
- `.gitreleaser.yaml` (or `.yml`)
- `.gitreleaser.toml`
- `package.json` (in the `gitreleaser` property)

Use `--config path/gitreleaser.json` to use another configuration file location.

An example `.gitreleaser.json`:

```json
{
  "$schema": "https://unpkg.com/gitreleaser@17/schema/gitreleaser.json",
  "git": {
    "commitMessage": "chore: release v${version}"
  },
  "github": {
    "release": true
  }
}
```

The configuration can also be stored in a `gitreleaser` property in `package.json`:

```json
{
  "name": "my-package",
  "devDependencies": {
    "gitreleaser": "*"
  },
  "gitreleaser": {
    "github": {
      "release": true
    }
  }
}
```

Typescript config files are supported, providing typing hints to the config:

```ts
import type { Config } from 'gitreleaser';

export default {
  git: {
    commit: true,
    tag: true,
    push: true
  },
  github: {
    release: true
  },
  npm: {
    publish: true
  }
} satisfies Config;
```

Or, use YAML in `.gitreleaser.yml`:

```yaml
git:
  requireCleanWorkingDir: false
```

TOML is also supported in `.gitreleaser.toml`:

```toml
[hooks]
"before:init" = "npm test"
```

## Configuration options

Gitreleaser has [plenty of options][2]. See the following tables for plugin configuration options:

- [Git][3]
- [npm][4]
- [GitHub][5]
- [GitLab][6]

## Setting options via CLI

Any option can also be set on the command-line, and will have highest priority. Example:

```bash
gitreleaser minor --git.requireBranch=main --github.release
```

Boolean arguments can be negated by using the `no-` prefix:

```bash
gitreleaser --no-npm.publish
```

Also plugin options can be set from the command line:

```bash
gitreleaser --no-plugins.@gitreleaser/keep-a-changelog.strictLatest
```

[1]: #configuration-options
[2]: ../config/gitreleaser.json
[3]: ./git.md#configuration-options
[4]: ./npm.md#configuration-options
[5]: ./github-releases.md#configuration-options
[6]: ./gitlab-releases.md#configuration-options
