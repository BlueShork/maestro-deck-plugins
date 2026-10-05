# Maestro Deck plugin registry

`registry.json` is the catalogue shown on the **Plugins** page of
[Maestro Deck](https://github.com/BlueShork/maestro-deck). The app reads it from
`https://raw.githubusercontent.com/BlueShork/maestro-deck-plugins/main/registry.json`.

Only the maintainer edits this file. Each entry pins one version of one plugin:

| Field | Meaning |
|---|---|
| `id` | Plugin id, equal to `id` in the plugin's `manifest.json` (`^[a-z0-9][a-z0-9-]{0,31}$`). |
| `name`, `description` | Shown on the Plugins page. |
| `repo` | The plugin's GitHub repo. |
| `version` | The pinned version, equal to the manifest's `version`. |
| `minAppVersion` | Lowest Maestro Deck version that can run it. |
| `url` | https URL of the release's `plugin.zip`. |
| `sha256` | Hex sha256 of that `plugin.zip`. The app refuses any download that does not match it. |

## Publishing a plugin or an update

1. In the plugin repo, bump the version, then tag and push `vX.Y.Z`. The release workflow publishes `plugin.zip` and prints its sha256.
2. Here, add the entry or update `version`, `url` and `sha256`. Check the hash with
   `curl -sL <url> | shasum -a 256`.
3. Commit to `main`. Users see the plugin the next time they open the Plugins page.

The host API and the manifest format are documented in
[`docs/plugins.md`](https://github.com/BlueShork/maestro-deck/blob/main/docs/plugins.md).
