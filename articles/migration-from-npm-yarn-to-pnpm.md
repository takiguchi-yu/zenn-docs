---
title: "Migration from NPM/Yarn to PNPM"
emoji: "ð"
type: "idea" # tech: æè¡è¨äº / idea: ã¢ã¤ãã¢
topics: ["npm","yarn","pnpm"]
published: false
---

# Migrating from NPM/Yarn to PNPM

ãã­ã¸ã§ã¯ãã§ npm ã¾ãã¯ yarn ãä½¿ç¨ãã¦ããå ´åãpnpm ã¸ã®ç§»è¡ã¯ããã»ã©é£ããããã¾ãããä»¥ä¸ã¯ãnpmãyarnãããã³ pnpm ã®ã³ãã³ãã®æ¯è¼ã§ãã

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

# åè

https://refine.dev/blog/pnpm-vs-npm-and-yarn/