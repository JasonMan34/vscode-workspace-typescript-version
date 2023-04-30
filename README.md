# vscode-workspace-typescript-version

Reproduction details:

1. Open workspace file `workspace.code-workspace`
2. Open `Package A/index.ts`
3. TypeScript doesn't work
4. Cmd(Ctrl) + Shift + P - `>Typescript: Select TypeScript Version...`
5. Cannot select the root-level `.yarn/sdks/typescript/lib` option

If you manually change the workspace settings to point to the tsdk through parents, weird things happen:

1. Manually change the workspace settings, set: `"typescript.tsdk": "../../.yarn/sdks/typescript/lib",`
2. Open `Package A/index.ts`
3. Cmd(Ctrl) + Shift + P - `>Typescript: Select TypeScript Version...`
4. VSCode suggests `../.yarn/sdks/typescript/lib` (Notice the one parent `..` instead of two)
5. Select that option, and everything works!
6. Reload the window (Cmd(Ctrl) + Shift + P - `>Developer: Reload Window`)
7. VSCode will not recognize the tsdk again
8. Cmd(Ctrl) + Shift + P - `>Typescript: Select TypeScript Version...`
9. VSCode suggests `.yarn/sdks/typescript/lib` (Notice no parent now!)
10. Select that option, and everything works!
11. Reload the window (Cmd(Ctrl) + Shift + P - `>Developer: Reload Window`)
12. VSCode will not recognize the tsdk, and we're back to stage 1

Oddly, enough this flow makes everything work, but surely it's a bug:

1. Manually change the workspace settings, set: `"typescript.tsdk": "../../.yarn/sdks/typescript/lib",`
2. Open `Package A/index.ts`
3. Cmd(Ctrl) + Shift + P - `>Typescript: Select TypeScript Version...`
4. VSCode suggests `../.yarn/sdks/typescript/lib` (Notice the one parent `..` instead of two)
5. Select that option, and **before closing the window, manually change the workspace settings tsdk again to have two parents in the path** - set: `"typescript.tsdk": "../../.yarn/sdks/typescript/lib",`
6. Now the typescript is loaded correctly and doesn't break between reloads
