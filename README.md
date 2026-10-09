# apm: Renovate updates the apm.yml copies that APM deploys

## Current behavior

[`apm.yml`](apm.yml) installs the `with-dependencies` skill from [MPV/renovate-apm-demo1](https://github.com/MPV/renovate-apm-demo1/tree/master/skills/with-dependencies). That skill's directory has an `apm.yml` of its own, which pins mattpocock's `grill-me` skill at `v1.0.0`.

`apm install` copied that file to [`.claude/skills/with-dependencies/apm.yml`](.claude/skills/with-dependencies/apm.yml), and [`apm.lock.yaml`](apm.lock.yaml) lists the copy under the dependency's `deployed_files`.

The apm manager matches every `apm.yml`, so Renovate extracts the copy as a project of its own and opens an update for `grill-me` that edits only the copy. The next `apm install` restores the copy from the package and undoes the update.

The root `apm.yml` pins a bare commit, which Renovate skips, so the copy is the only file with an update.

## Expected behavior

Renovate leaves `.claude/skills/with-dependencies/apm.yml` alone, because `apm.lock.yaml` lists it as a file that APM deployed.

## Link to the Renovate issue or Discussion

Not posted yet. The draft is MPV/renovate#24.
