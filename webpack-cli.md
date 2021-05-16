<div style="text-align:center;">
   <h3>
     webpack 命令行接口使用总结
  </h3>
  <img src="./static/imgs/webpack-cli.jpg"/>
</div>

命令行接口中使用webpack的配置文件（默认是 `webpack.config.js` ）可以更加方面的配置和分发。传入命令行的所有参数都将被映射到配置文件中的相应参数。

#### 使用配置文件

```bash
webpack [--config webpack.config.js]
```

> 如果不使用 `-config` 选项，默认使用 `webpack.config.js` 文件。

如果要指定不名为`webpack.config.js` 的文件名，必要要加`--config` 选项，例如：

```sh
webpack --config example.config.js
```

#### 不使用配置文件

```sh
webpack <entry> [<entry>] -o <output>
```

#### 将构建结果输出为JSON

```sh
webpack --json
webpack --json > stats.json
```

不使用此配置项的时候，webpack将会直接打印出构建信息。

#### 环境选项

当配置文件导出的是函数时，环境参数可能会被传入。

```sh
webpack --env.production     # sets env.production == true
webpack --env.platform=web   # sets env.platform == "web"
```

`--env` 参数接受各种语法：

| 调用方式                                | 环境结果                  |
| --------------------------------------- | ------------------------- |
| `webpack --env prod`                    | `"prod"`                  |
| `webpack --env.prod`                    | `{prod: true}`            |
| `webpack --env.prod=1`                  | `{prod: 1}`               |
| `webpack --env.prod=foo`                | `{prod: "foo"}`           |
| `webpack --env.prod --env.min`          | `{prod: true, min: true}` |
| `webpack --env.prod --env min`          | `[{prod: true}, "min"]`   |
| `webpack --env.prod=foo --env.prod=bar` | `{prod: ["foo", "bar]}`   |

#### 配置选项

| 参数                   | 解释                                      | 输入类型 | 默认值                                  |
| ---------------------- | ----------------------------------------- | -------- | --------------------------------------- |
| `--config`             | 指定配置文件路径                          | string   | `webpack.config.js` 或 `webpackfile.js` |
| `--config-register,-r` | 在加载webpack配置之前预加载一个或多个模块 | array    |                                         |
| `--config-name`        | 要是用的配置名称                          | string   |                                         |
| `--env`                | 当配置是一个函数时，传递进去的环境变量    |          |                                         |
| `mode`                 | 使用的模式                                | string   | `production`                            |

