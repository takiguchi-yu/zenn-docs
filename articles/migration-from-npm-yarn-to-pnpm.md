---
title: "Migration from NPM/Yarn to PNPM"
emoji: "👋"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["npm","yarn","pnpm"]
published: false
---

# Migrating from NPM/Yarn to PNPM

プロジェクトで npm または yarn を使用している場合、pnpm への移行はそれほど難しくありません。以下は、npm、yarn、および pnpm のコマンドの比較です。

|npm command|Yarn command|pnpm equivalent|
|-|-|-|
|npm install|yarn|[pnpm install](https://pnpm.io/cli/install)|
|npm install [pkg]|yarn add [pkg]|[pnpm add [pkg]](https://pnpm.io/cli/add)|
|npm uninstall [pkg]|yarn remove [pkg]|[pnpm remove [pkg]](https://pnpm.io/cli/remove)|
|npm update|yarn upgrade|[pnpm update](https://pnpm.io/cli/update)|
|npm list|yarn list|[pnpm list](https://pnpm.io/cli/list)|
|npm run [scriptName]|yarn [scriptName]|[pnpm [scriptName]](https://pnpm.io/cli/run)|
|npx [command]|[yarn dlx [command]](https://yarnpkg.com/cli/dlx)|[pnpm dlx [command]](https://pnpm.io/cli/dlx)|
|[npm exec](https://docs.npmjs.com/cli/v8/commands/npm-exec)|[yarn exec [commandName]](https://yarnpkg.com/cli/exec)|[pnpm exec [commandName]](https://pnpm.io/cli/exec)|
|[npm init [initializer]](https://docs.npmjs.com/cli/v8/commands/npm-init)|yarn create [initializer]|[pnpm create [initializer]](https://pnpm.io/cli/create)|

# 参考

https://refine.dev/blog/pnpm-vs-npm-and-yarn/