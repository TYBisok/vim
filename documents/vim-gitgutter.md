# vim-gitgutter

用来在 Vim 编辑器的 gutter 中展示 git diff。该插件会标识当前行的操作状态，包括添加(added)、修改(modified)和删除(removed)。

效果：

![](../images/vim-gitgutter/screeshot.png)

* 259 行，<span style="color: #e4c54f;">`~`</span> 表示当前行被修改了
* 262 行，<span style="color: #f00;">`-`</span> 表示下面被删除了一行
* 269 行 - 282 行，<span style="color: #0f0;">`+`</span> 表示这些行为新增

## 特点

* 逐行展示 git diff
* 异步运行 git diff
* 保证实时更新标识符（+/-/～）
* 修改的代码块之间可快速跳转
* 可分别对代码块执行 stage/undo/review 等操作
* 可与 index 或者其他 commits 之间进行 diff 操作

...

还有很多特点不想写了。。。

## 缺点

* 只支持 git，不支持其他版本管理工具。如果使用其他版本管理工具，建议修改为 git 管理 （大误，😂；使用其他工作做版本管理的小伙伴请使用 [vim-signify](https://github.com/mhinz/vim-signify)。

## 安装

建议使用 [vim-plug](./vim-plug.md) 来管理该插件。

在安装之前，请先检查当前使用的 Vim 是否支持 signs 功能，检测方法为在打开的 Vim 中，在命令模式中输入：

```vimscript
:echo has('signs')
```

如果结果为 `1`，表示当前版本支持 signs 功能；如果为 0，表示当前版本不支持，应该安装一个更高版本的 Vim 编辑器。

signs 功能主要用来在 Vim 的 gutter(vim column) 中标识当前的调试、版本 diff 等状态，这里不展开介绍，想要了解更多的请跳转 [Vim documentation: sign](http://vimdoc.sourceforge.net/htmldoc/sign.html)

## Getting started

### 设置 updatetime

Vim 中的 updatetime 用来定义更新时间，默认为 4000ms；这样会使得文件在修改之后，diff sign 更新的特别慢，所以建议在 `.vimrc` 中将此选项的默认时间设置的小一点：

```vimscript
" set the default value of updatetime to 100ms
set updatetime=100
```

### 激活设置

可以通过下面的命令切换 vim-gitgutter 的状态：

```vimscript
:GitGutterDisable " 禁用
:GitGutterEnable " 开启
:GitGutterToggle " 切换
```

可以通过下面的命令切换 signs 的状态：

```vimscript
:GitGutterSignsEnable " 开启
:GitGutterSignsDisable " 禁用
:GitGutterSignsToggle " 切换
```

上面的命令比较长，可以通过定义快捷键来映射上面的命令，例如：

```vimscript
" map <leader>ggd :GitGutterDisable " 禁用 vim-gitgutter
" map <leader>gge :GitGutterEnable " 开启 vim-gitgutter
map <leader>ggt :GitGutterToggle " 切换是否开启 vim-gitgutter
```

快捷键越多，我们需要记忆的东西就越多，会形成不必要的负担。因此这里推荐只配置一个 toggle 的快捷键。

### snappy

为了保持 Vim 的优雅简洁，当一个文件的需改超过 500 处时，vim-gitgutter 会关闭 diff signs；当修改小于 500 处时再展示。如果要修改该配置的默认值，可通过如下配置：

```vimscript
let g:gitgutter_max_signs = 800
```

### Hunks

vim-gitgutter 会将每一处修改标记为一个 **代码块对象**，并且提供了跳转、预览、暂存和撤销的操作。vim-gitgutter 将这些代码块对象称为 **hunks**。

#### 跳转

* `]c` 跳转到下一个 hunks
* `[c]` 跳转到上一个 hunks

自定义快捷键：

```vimscript
nmap ]h <Plug>GitGutterNextHunk
nmap [h <Plug>GitGutterPrevHunk
```

#### 暂存（stage）/ 撤销（undo）/ 预览（preview）

* `<Leader>hs` 暂存（stage）焦点所在的 hunk
* `<leader>hu` 撤销（undo）焦点所在的 hunk
* `<leader>hp` 预览（preview）焦点所在的 hunk

自定义快捷键的方式如下：

```vimscript
nmap <Leader>ha <Plug>GitGutterStageHunk
nmap <Leader>hr <Plug>GitGutterUndoHunk
nmap <Leader>hv <Plug>GitGutterPreviewHunk
```

## 其他

除以上的特性和配置之外，vim-gitgutter 还提供了其他很多配置，具体请参考 [vim-gitgutter#customition](https://github.com/airblade/vim-gitgutter#customisation) 部分。

作者自己比较喜欢功能最小化，即一个插件只要满足自己的需求即可，其他更高级酷炫的功能，对于自己来说可能帮助提升效率的空间不大，反而有可能会消耗更多的性能。作者感觉上面这些功能已经满足了作者对于 git diff 相关操作的需要，其他各种颜色配置、高亮和提示符更改已经超出了我对这些操作的需要，因此不再做更多的介绍。如果有需要，各位小伙伴可以自行阅读 vim-gitgutter 的 README 进行配置。

## Author Info 🦋

* [GitHub](https://github.com/Tao-Quixote)
* Email: <web.taox@gmail.com>