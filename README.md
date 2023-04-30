# vscode-workspace-typescript-version

Reproduction details:

1. Open workspace from file `workspace.code-workspace`
2. Open `Package A/index.ts`
3. Allow typescript workspace version
4. TypeScript should work
5. Ctrl(Cmd) + Shift + P - `>Typescript: Select TypeScript Version...`
6. VSCode suggests `../.yarn/sdks/typescript/lib` (Notice the one parent `..` instead of two)
7. Select that option
8. VSCode will now not recognize the tsdk

If we manually change the workspace settings back to `"typescript.tsdk": "../../.yarn/sdks/typescript/lib"`, and reload the window, the tsdk will work normally again
