## commitizen 环境配置

``` bash
# 安装 nvm
brew install nvm

# 安装 node
nvm install v8.16.0

# 切换 node 版本
nvm use v8.16.0

# 全局安装 commitizen
npm install -g commitizen

# 安装 change-log 定制化工具
npm install -g cz-conventional-changelog

# 配置 commit message
echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
```

## commit message 格式

### Header
Header部分只有一行，包括三个字段：`type`（必需）、`scope`（可选）和`subject`（必需）。

#### type
用于说明 commit 的类别，只允许使用下面7个标识。

* feat：新功能（feature）
* fix：修补bug
* docs：文档（documentation）
* style： 格式（不影响代码运行的变动）
* refactor：重构（即不是新增功能，也不是修改bug的代码变动）
* test：增加测试
* chore：构建过程或辅助工具的变动

如果`type`为`feat`和`fix`，则该 commit 将肯定出现在 Change log 之中。其他情况（`docs`、`chore`、`style`、`refactor`、`test`）不会出现在Change log中。

#### scope
`scope`用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

#### subject
`subject`是 commit 目的的简短描述，不超过50个字符。

### Body
Body 部分是对本次 commit 的详细描述，可以分成多行。下面是一个范例。

~~~
More detailed explanatory text, if necessary.  Wrap it to
about 72 characters or so.

Further paragraphs come after blank lines.

- Bullet points are okay, too
- Use a hanging indent
~~~

有两个注意点。
（1）使用第一人称现在时，比如使用change而不是changed或changes。
（2）应该说明代码变动的动机，以及与以前行为的对比。

### Footer
Footer 部分只用于两种情况。

#### 不兼容变动
如果当前代码与上一个版本不兼容，则 Footer 部分以`BREAKING CHANGE`开头，后面是对变动的描述、以及变动理由和迁移方法。

~~~
BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
~~~

#### 关闭 Issue
如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

~~~
Closes #234
~~~

也可以一次关闭多个 issue 。

~~~
Closes #123, #245, #992
~~~

### Revert
还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以`revert`:开头，后面跟着被撤销 Commit 的 Header。

~~~
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
~~~


Body部分的格式是固定的，必须写成`This reverts commit <hash>.`，其中的`hash`是被撤销 commit 的 SHA 标识符。

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的`Reverts`小标题下面。



## 生成Change log
如果你的所有 Commit 都符合 Angular 格式，那么发布新版本时， Change log 就可以用脚本自动生成（[例1](https://github.com/btford/grunt-conventional-changelog/blob/master/CHANGELOG.md)，[例2](https://github.com/karma-runner/karma/blob/master/CHANGELOG.md)）。

生成的文档包括以下三个部分。

* New features
* Bug fixes
* Breaking changes.

每个部分都会罗列相关的 commit ，并且有指向这些 commit 的链接。当然，生成的文档允许手动修改，所以发布前，你还可以添加其他内容。

[standard-version](https://github.com/conventional-changelog/standard-version)就是生成 Change log 的工具。

### 安装
~~~shell
$ npm i -g standard-version
~~~

### 使用
~~~shell
$ standard-version
~~~

### CLI帮助
~~~shell
$ standard-version --help
~~~

> 由于能力有限，若有错误与不当之处，请批评指正。
