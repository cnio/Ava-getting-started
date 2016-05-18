# Ava-getting-started
## 执行测试的几种形式
### npm test

```
// package.json
"scripts": {
"test": "ava"
},
```
效果如下
```
➜  Ava-api npm test    

> ava@1.0.0 test /home/joes/Apps/Ava-api
> ava


2 passed

```

### ava

全局安装Ava,输入ava效果如下
```
➜  Ava-api ava

   2 passed

   ```
### 文件形式
   ```
   $ ava test.js test2.js
   $ ava test-*.js
   ```
### 文件夹形式

   测试某文件夹下所有js文件,如下`test`为文件夹名,也可以是其他名字.
   ```
   $ ava test
   ```

   > Ava 会默认寻找当前路径下的名为`test.js`文件和名为`test`的文件夹,并执行测试任务.

## 可选项

- --init

    已经全局安装过ava的,执行`ava --init`将自动添加
        ```
"scripts": {"test": "ava"}
```
到`package.json`中. 并自动在项目中安装ava,相当于又执行
```
$ npm install ava --save-dev
```

- --verbose

    ```bash
    ➜  Ava-api ava -v
    
    ✔ foo
    ✔ bar
    
    2 tests passed
    
    ```

- --tap

    ```bash
    ➜  Ava-api ava -t 
    TAP version 13
    # foo
    ok 1 - foo
    # bar
    ok 2 - bar
    
    1..2
    # tests 2
    # pass 2
    # fail 0
    
    ```

- --watch

    ava将一直处于监听状态,测试文件稍有改变就会再次执行测试.

当然还有其他一些参数
```
Options
--init           Add AVA to your project
--fail-fast      Stop after first test failure
--serial, -s     Run tests serially
--require, -r    Module to preload (Can be repeated)
--tap, -t        Generate TAP output
--verbose, -v    Enable verbose output
--no-cache       Disable the transpiler cache
--match, -m      Only run tests with matching title (Can be repeated)
--watch, -w      Re-run tests when tests and source files change
--source, -S     Pattern to match source files so tests can be re-run (Can be repeated)
--timeout, -T    Set global timeout
```

注意，如果你本地安装的 AVA 可用的话 CLI 将会运行它，即使你的全局也安装了 AVA。
文件夹会被递归遍历，带上*.js参数的话全部文件都会被作为测试文件。名字为fixtures，helpers和node_modules的文件夹总会被忽略。所以把 helper 名字以_开头命名就可以一起放置在测试文件的目录下。

当使用npm test时你可以直接传参数npm test test2.js，但标志需要像这样传递npm test -- --verbose。

## 配置

所有的 CLI 选项都可以配置在package.json的ava属性中。你可以修改ava命令的默认行为，所以你不需要重复在命令行中输入相同的选项。
```bash
{
    "ava": {
    "files": [
    "my-test-folder/*.js",
    "!**/not-this-file.js"
    ],
    "source": [
    "**/*.{js,jsx}",
    "!dist/**/*"
    ],
    "match": [
    "*oo",
    "!foo"
    ],
    "failFast": true,
    "tap": true,
    "require": [
    "babel-register"
    ],
    "babel": "inherit"
    }
}
```
传递给 CLI 的参数总是比package.json中的配置优先级高。
