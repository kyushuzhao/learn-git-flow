## Git Flow
---
使用`Git Flow`的目的是为了更好的进行版本管理和持续集成，有些细节并不一定要遵循这个模型，可以根据团队规模进行简单的调整，适合的才是最好的。

### ![A successful Git branching model](./assets/git-model.png)

### 模型解析
#### 主要分支

远端仓库中拥有两个主要分支，具有无限的生命周期：

* master：`origin/master` 源代码 `HEAD` 总是反映*生产就绪*状态的分支
* develop: `origin/develop` 源代码  `HEAD` 始终反映了下一版本中最新交付的开发更改的状态

![main-branches](/Users/joker/Github/learn-git-flow/assets/main-branches.png)

> 当 `develop` 分支中的源代码稳定达到发版要求并准备发版时，合并当前版本代码至`master`， 然后使用版本号进行标记。这时 `master` 就是一个新的生产版本，当然我们也可以配置 `git hook` 的脚本自动构建并推送到我们的生产服务器

#### 辅助分支

针对上面的 `Git Flow` 模型我们在**主要分支**上扩展了**辅助分支**，用以辅助解决并行开发团队成员间的配合与快速迭代过程中的 `bug` 修复以及功能追踪的问题，这些分支都有特定的目的并不是永久存在的，最终会被删除：

* Feature branches：功能分支

* Release branches：发布分支

* Hotfix branches：热修复分支

##### Feature Branches

由 `develop` 分支检出，必须合并回 `develop`，命名约定：

> 格式：`feature-` + 功能描述，如果通过 `issue` 管理 建议加上 `issue号`前缀

功能分支主要用于为即将发布或将来的版本开发新功能，功能分支只要处于开发阶段，就会一直存在，但最终会合并回 `develop` 分支（将新功能添加到即将发布的版本中）或者丢弃(需求彻底作废时)。

![Git Flow](/Users/joker/Github/learn-git-flow/assets/fb.png)

##### Release Branches

* 创建发布
由 `develop` 分支检出，必须合并回 `develop` 和 `master`，命名约定：

  > 格式：`release-` + `版本号` 例如：release-1.0.1

  发布分支为预发布的生产版本，每个发布分支都分配了一个版本号，允许修复小错误并为发布准备元数据	（版本号、构建日期等）

* 完成发布

  当 `release` 分支达到发版标准时，合并至 `master` 分支，并在 `master` 打上对应版本的 `tag` 号标识，最后将发布分支上 所做的更改合并回 `develop` 分支，以便将来的版本也包含在 `release` 分支上做的错误修复


#### 参考建议

[为什么使用Git?](https://git.wiki.kernel.org/index.php/GitSvnComparsion)

[A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/#decentralized-but-centralized)
