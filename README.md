# [Renovate discussion 38366](https://github.com/renovatebot/renovate/discussions/38366)

## Current behavior

Using the first rule to disable all updates:
```json
{
    "description": "Rule #1: The main rule to disable every update by default",
    "matchFileNames": [ "*" ],
    "matchPackageNames": [ "*" ],
    "matchUpdateTypes": [ "*" ],
    "enabled": false
},
```
Followed by a second rule to enable non-major updates for log4j from libs.versions.toml:
```json
{
    "description": "Rule #2: Enable non-major updates of all log4j packages in the libs.versions.toml file.",
    "matchFileNames": [ "/libs.versions.toml" ],
    "matchPackageNames": [ "/^org\\.apache\\.logging\\.log4j:log4j.*$/" ],
    "matchUpdateTypes": [ "minor", "patch" ],
    "enabled": true
}
```
seems to enable updates for all packages in that file.

When spliting the first rule into 3 separate rules:
```json
{
    "description": "Rule #1A: The main rule to disable every file update by default",
    "matchFileNames": [ "*" ],
    "enabled": false
},
{
    "description": "Rule #1B: The main rule to disable every package update by default",
    "matchPackageNames": [ "*" ],
    "enabled": false
},
{
    "description": "Rule #1C: The main rule to disable every update type by default",
    "matchUpdateTypes": [ "*" ],
    "enabled": false
},
```
There are no updates at all, not even for the log4j package defined in rule #2.

## Expected behavior

I would expect that the first rule (or the first 3 rules when split) would disable all updates in the whole repository, and that the second rule would then enable only non-major updates for log4j packages defined in libs.versions.toml.

## Link to the Renovate issue or Discussion

[Link to Renovate Discussion 38366.](https://github.com/renovatebot/renovate/discussions/38366)
