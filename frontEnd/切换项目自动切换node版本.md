### 背景

pnpm 在我们组已经被大规模使用，不同 pnpm 版本的 lockfile 存在巨大差异。如果使用不同版本的 pnpm 管理依赖，可能会导致 lockfile 被频繁修改，进而造成团队协作时的合并冲突或者依赖版本不一致的问题

### 目标

1. 解决 lockfile 被频繁修改问题
    
2. 规范尽可能简单且不易出错
    
3. 规范尽可能现代化
    

### 解决思路

1. 移除全局的 pnpm，原因：不同 pnpm 版本 的 lockfile 存在巨大差异，所以不应存在全局的 pnpm
    
2. yarn 只能使用全局版本，原因是 yarn v1 版本已不再更新，lockfile 也不会发生变化
    

### 解决方案

1. 废弃 nvm，原因：nvm 过于古老，配置复杂，切换 node 版本慢
    
2. yarn 安装
    
    1. 安装：brew install yarn
        
3. node 版本管理 fnm（[https://github.com/Schniz/fnm](https://github.com/Schniz/fnm)）
    

1. 安装：brew install fnm
    
2. 自动切换 node 版本：在 ~/.zshrc 中添加 eval "$(fnm env --use-on-cd)"
    

1. pnpm 版本管理：corepack（[https://nodejs.cn/api/corepack.html](https://nodejs.cn/api/corepack.html)）
    

### corepack 使用

1. 开启 corepack：corepack enable
    
2. 本地终端 corepack 安装 pnpm、yarn 加速：在 ~/.zshrc 下添加，export COREPACK_NPM_REGISTRY=https://registry.npmmirror.com
    
3. 在 package.json 中添加 "packageManager": "pnpm@9.0.0"
    

### 疑问解答：

为什么 yarn 要全局安装？

corepack 只支持 node 14.19.0、16.9.0 及以上版本，低版本的项目需要使用全局 yarn 来完成安装

corepack 还处在实验性阶段为什么要使用？

corepack 已经历了近 3 年的迭代，Vue.js 等大型项目都已采用 corepack 方案