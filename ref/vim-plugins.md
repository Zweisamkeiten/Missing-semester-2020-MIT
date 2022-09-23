## Vim 8 带来原生第三方包加载

Vim 8 于 9 月 12 日发布，添加了一个能够本地加载第三方包的新功能。

> 插件不断增长，并且可用的插件比以往任何时候都多。 保持 添加了插件管理包支持的集合。 这是 一种获取一个或多个插件的便捷方法，将它们放在一个目录中，然后 可能让他们更新。 Vim 会自动加载它们，或者仅在 想要的。

## 怎么运行的

如果您存储您的 `vim`配置在 `~/.vim`需要在此文件夹中创建一个新文件夹来保存插件。 这有点令人困惑 `~/.vim/pack/foo`. 文件夹 `foo`可以是任何东西。 你可以把它保持在 `foo`, 改成 `my-plugins`或者你喜欢的任何东西。 

```shell
mkdir -p ~/.vim/pack/plugins
```

在此文件夹中的另一个文件夹 `start`需要保存插件。 Vim 将拾取添加到此文件夹中的任何包并自动加载插件。

（可选）另一个文件夹 `opt`可以创建来保存未自动加载的包。 在 opt 文件夹中添加的包可以使用

```
:packadd packagename
```

这对于调试或临时插件可能很有用。

## 目录布局

包的目录布局如下所示。

```
.vim/pack/shapeshed/start/foobar/plugin/foo.vim    	  " always loaded, defines commands
.vim/pack/shapeshed/start/foobar/plugin/bar.vim    	  " always loaded, defines commands
.vim/pack/shapeshed/start/foobar/autoload/foo.vim  	  " loaded when foo command used
.vim/pack/shapeshed/start/foobar/doc/foo.txt       	  " help for foo.vim
.vim/pack/shapeshed/start/foobar/doc/tags          	  " help tags
.vim/pack/shapeshed/opt/fooextra/plugin/extra.vim  	  " optional plugin, defines commands
.vim/pack/shapeshed/opt/fooextra/autoload/extra.vim  	" loaded when extra command used
.vim/pack/shapeshed/opt/fooextra/doc/extra.txt  	    " help for extra.vim
.vim/pack/shapeshed/opt/fooextra/doc/tags  	          " help tags
```

在哪里 `foobar`和 `fooextra`是插件的名称。

除了 opt 文件夹之外，这些是现有软件包的默认文件夹，因此它们是兼容的。

## 管理包

vim 中的新功能没有添加任何用于管理插件的内容； 它只是加载它们。 如何管理插件取决于您。

管理包直接等同于使用 [Pathogen](https://github.com/tpope/vim-pathogen) 将插件文件夹移动到位，克隆 git 存储库或使用 git 子模块将包移动到 `start`文件夹都是选项。 虽然我不是 git 子模块的忠实粉丝，但我的 `~/.vim`文件夹是我的点文件的一部分，我发现 git 子模块对我有用。

以最简单的形式，您只需将插件移动到 `start`文件夹，它将自动加载。 如何管理它取决于您。

## 添加一个包

这是一个如何使用 Vim 对包和 git 子模块的本机方法添加包的示例。

```
cd ~/dotfiles
git submodule init
git submodule add https://github.com/vim-airline/vim-airline.git vim/pack/shapeshed/start/vim-airline
git add .gitmodules vim/pack/shapeshed/start/vim-airline
git commit
```

## 更新包

更新包也只是更新 git 子模块的一个例子。

```
git submodule update --remote --merge
git commit
```

## 删除一个包

删除一个包只是删除 git 子模块的一种情况。

```
git submodule deinit vim/pack/shapeshed/start/vim-airline
git rm vim/pack/shapeshed/start/vim-airline
rm -Rf .git/modules/vim/pack/shapeshed/start/vim-airline
git commit
```