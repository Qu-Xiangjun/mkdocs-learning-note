# MkDocs 配置主题

> [https://mkdocs.zimoapps.com/user-guide/styling-your-docs/](https://mkdocs.zimoapps.com/user-guide/styling-your-docs/)

> [Choosing Your Theme - MkDocs](https://www.mkdocs.org/user-guide/choosing-your-theme/)

MkDocs包括一些内置主题以及各种第三方主题，所有这些都可以使用额外的CSS或JavaScript轻松定制，或者覆盖主题的custom_dir。 您也可以为你的文档从头开始创建自己的自定义主题。

要使用MkDocs中包含的主题，只需将其添加到您的`mkdocs.yml`配置文件中。

```HTTP
theme: readthedocs
```

使用下面的 **内置主题** 中列出的任一一种替换掉`readthedocs`。

要创建新的自定义主题，请参阅自定义主题[custom theme]页面，或者更多地自定义现有主题，请参阅下面的 **自定义主题** 部分。

## 内置主题

### mkdocs

MkDocs的默认主题，使用修改过的Bootstrap构建而成，支持MkDocs的大部分功能。

![img](F:\Study\Term7\mkdocs-learning-note\docs\img\3-1.png)

除了默认的[主题配置选项]之外，`mkdocs`主题还支持以下选项：

- **highlightjs**：JavaScript库在代码块中突出显示源代码。 默认值：`True`。

- **hljs_style**：highlight.js库提供79种不同的[样式]（颜色变化），用于突出显示代码块中的源代码。 将其设置为所需样式的名称。 默认值：`github`。

- **hljs_languages**：them.默认情况下，highlight.js仅支持23种常用语言。在此列出额外需要支持的语言。

```YAML
theme:
    name: mkdocs
    highlightjs: true
    hljs_languages:
        - yaml
        - rust
```

- **shortcuts**：定义键盘快捷键。

```YAML
theme:
    name: mkdocs
    shortcuts:
        help: 191    # ?
        next: 78     # n
        previous: 80 # p
        search: 83   # s
```

所有值都是数字键代码。 最好使用所有键盘上都有的键。 您可以使用https://keycode.info/来确定给定的键的代码。

- **help**：显示一个列出键盘快捷键的帮助模式。默认：`191`（＆quest;）

- **next**：导航到“下一页”。 默认值：`78`（n）

- **previous**：导航到“上一页”。 默认值：`80`（p）

- **search**：显示搜索模式。 默认值：`83`（s）

- **navigation_depth**: 侧栏中导航树的最大深度: `2`.

- **nav_style**: 这将调整顶部导航栏的视觉样式；默认情况下，该选项设置为`primary`（默认），但也可以设置为`dark`或`light`

```YAML
theme:
    name: mkdocs
    nav_style: dark
```

- **locale**: 用于构建主题的区域设置（语言/位置）。如果您的区域设置还不受支持，它将返回默认设置。

此主题支持以下区域设置：

- `en`: English (default)

- `fr`: French

- `es`: Spanish

- `ja`: Japanese

- `pt_BR`: Portuguese (Brazil)

- `zh_CN`: Simplified Chinese

参考此处 [localizing your theme](https://www.mkdocs.org/user-guide/localizing-your-theme/) 获知更多

### readthedocs

[Read the Docs](https://readthedocs.org/)服务使用的默认主题的克隆，它提供与其父主题相同的受限制功能集。 与其父主题一样，仅支持两个级别的导航。

![img](F:\Study\Term7\mkdocs-learning-note\docs\img\3-2.png)

除了默认的[主题配置选项]之外，`readthedocs`主题还支持以下选项：

- **highlightjs**：使用[highlight.js](https://highlightjs.org/) JavaScript库在代码块中突出显示源代码。 默认值：`True`。

- **hljs_languages**：默认情况下，highlight.js仅支持23种常用语言。在此列出额外需要支持的语言。

```YAML
theme:
    name: readthedocs
    highlightjs: true
    hljs_languages:
        - yaml
        - rust
```

- **include_homepage_in_sidebar**：列出侧栏菜单中的主页。由于MkDocs要求在“nav”配置选项中列出主页，因此此设置允许在侧栏中包含或排除主页。请注意，站点名称/Logo始终链接到主页。默认：`True`。

- **prev_next_buttons_location**：`bottom`, `top`, `both` 和 `none`中的一个值。相应地显示“下一步”和“上一步”按钮。 默认值：`bottom`。

- **navigation_depth**：侧栏中导航树的最大深度。 默认值：`4`。

- **collapse_navigation**：仅包含当前页面侧栏中的页面部分标题。 默认值：`True`。

- **titles_only**：仅包含侧栏中的页面标题，不包括所有页面的所有节标题。 默认值：`False`。

- **sticky_navigation**：如果为True，则在滚动页面时使侧边栏与主页面内容一起滚动。 默认值：`True`。



## 第三方主题

可以在[MkDocscommunity wiki](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes)中找到第三方主题列表。 如果您已创建自己的，请随时将其添加到列表中。

如：material主题 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)