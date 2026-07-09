# pnpm — `options.hoistingLimits.get is not a function`

pnpm 11.3.0 crashes during install when the hoisted linker is used with `hoistingLimits: workspaces` in `pnpm-workspace.yaml`.

## Reproduction

```bash
pnpm install
```

## Expected

pnpm installs the single workspace package dependency successfully.

## Actual

pnpm crashes before linking dependencies:

```text
[ERROR] options.hoistingLimits.get is not a function

pnpm: options.hoistingLimits.get is not a function
    at addNode (.../pnpm.mjs:156783:71)
    at cloneTree (.../pnpm.mjs:156826:9)
    at hoist3 (.../pnpm.mjs:156278:24)
    at hoist2 (.../pnpm.mjs:157005:48)
    at _lockfileToHoistedDepGraph (.../pnpm.mjs:157093:16)
```

Using the isolated linker avoids the crash:

```bash
pnpm install --config.node-linker=isolated
```

## Versions

- pnpm: 11.3.0
- Node.js: 24.15.0
- OS: Linux x64

## Related Issue

To be filled after filing.
