<div style="text-align:center;">
    <h1>
        windows terminal 配置文件使用说明
    </h1>
    <img src="./static/imgs/windows_termial.jpg" />
</div>

配置`Windows Terminal`的一种方法（当前是唯一的方法）是通过编辑`profiles.json`设置文件。可以通过点击下拉菜单的`设置`按钮使用默认编辑器编辑配置文件。

<div style="text-align:center;">
    <img src="./static/imgs/批注 2020-03-18 104111.jpg" />
</div>

该文件的完整路径是`C:\Users\Administrator\AppData\Local\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\profiles.json`。

从 [#2515](https://github.com/microsoft/terminal/pull/2515)开始，设置被拆分为两个文件：硬编码的`defaults.json`和`profiles.json`，其中包含用户设置。`defaults.json`文件仅作为默认设置的参考被提供。要查看``defaults.json``文件，请在按住Alt键的同时单击“设置”按钮。

可以在[此处](https://github.com/microsoft/terminal/blob/master/doc/cascadia/SettingsSchema.md)找到特定设置的详细信息。下面仅提供一般介绍。

设置分为四个标题：

1. 全局属性：设置被应用到整个应用，例如：默认的配置文件，初始大小等等。
2. keybindings：全局设置的子集，稍后会单独讨论。
3. Profiles：使用该配置文件打开选项卡时将应用于该选项卡的一组设置。—— 负责单个选项卡的行为
4. Schemes：配置文件可以使用的背景，文本等颜色集。—— 负责单个选项卡的外观

#### 全局设置

这些设置定义了启动默认值以及可能不会影响特定终端实例的应用程序范围的设置。

示例设置如下：

```json
"defaultProfile" : "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
"initialCols" : 120,
"initialRows" : 50,
"requestedTheme" : "system",
"keybindings" : []
...
```

这些全局属性可以存在于根json对象中，也可以存在于根属性`globals`下的对象中。

#### keybindings

这是一组用于调用各种命令的组合快捷键。每个命令可以具有多个键绑定。

> 👉按键绑定是全局设置的子字段，按键绑定以相同的方式应用于所有配置文件。

例如，这是默认按键绑定的示例：

```json
{
    "keybindings":
    [
        { "command": "closePane", "keys": ["ctrl+shift+w"] },
        { "command": "copy", "keys": ["ctrl+shift+c"] },
        { "command": "paste", "keys": ["ctrl+shift+v"] },
        { "command": "newTab", "keys": ["ctrl+shift+t"] },
        // etc.
    ]
}
```

keys也可以用单一字符串，不适用数组：

```json
{
    "keybindings":
    [
        { "command": "closePane", "keys": "ctrl+shift+w" },
        { "command": "copy", "keys": "ctrl+shift+c" },
        { "command": "newTab", "keys": "ctrl+shift+t" },
        // etc.
    ]
}
```

##### 解除绑定

如果默认按键绑定和其他应用的按键绑定冲突，可以使用如下方式解除绑定

```js
{
    "command" : null, "keys" : ["ctrl+shift+6"]
},
```



#### Profiles



