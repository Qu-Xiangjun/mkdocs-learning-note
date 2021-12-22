# MkDocs 自定义主题

如果您想对现有主题进行一些调整，则无需从头开始创建自己的主题。对于只需要一些CSS和（或）JavaScript的小调整，您可以使用docs_dir。但是，对于更复杂的自定义（包括覆盖模板），您需要使用主题的custom_dir设置。

### 使用docs_dir

extra_css和extra_javascript配置选项可用于对现有主题进行调整和自定义。要使用它们，您只需要在[文档目录]中包含CSS或JavaScript文件。

例如，要更改文档中标题的颜色，请创建一个名为`extra.css`的文件，并将其放在文档Markdown旁边。 在该文件中添加以下CSS。

```CSS
h1 {
  color: red;
}
```

**Note**

如果您使用ReadTheDocs部署文档。 您需要明确列出要包含在配置中的CSS和JavaScript文件。为此，请将以下内容添加到mkdocs.yml中。

```
extra_css: [extra.css]
```

在进行这些更改之后，当你运行`mkdocs serve`后将能看到效果。运行该命令后将会，CSS所做的改变将自动更新。

**Note**

在页面内容之后，任何额外的CSS或JavaScript文件都将添加到生成的HTML文档中。如果您希望包含JavaScript库，则可以通过使用主题的custom_dir获得更好支持。



### 使用主题的custom_dir

主题的custom_dir配置选项可用于指向覆盖父主题目录中的文件。父主题将是主题中name配置选项定义的主题。 `custom_dir`中与父主题中的文件同名的任何文件都将替换父主题中同名文件。`custom_dir`中的任何其他文件都将添加到父主题中。 `custom_dir`的内容应该镜像父主题的目录结构。您可以包含模板，JavaScript文件，CSS文件，图像，字体或主题中包含的任何其他媒体文件。

**Note**

为此，主题的`name`设置必须设置为已知的已安装主题。 如果`name`设置被设置为`null`（或未定义[custom theme]）。

 例如，mkdocs主题([查看源代码])包含以下目录结构（部分）：

```YAML
- css\
- fonts\
- img\
  - favicon.ico
  - grid.png
- js\
- 404.html
- base.html
- content.html
- nav-sub.html
- nav.html
- toc.html
```

要覆盖该主题中包含的任何文件，请在`docs_dir`旁边创建一个新目录：

```Bash
mkdir custom_theme
```

然后将您的`mkdocs.yml`配置文件指向新目录：

```YAML
theme:
    name: mkdocs
    custom_dir: custom_theme/
```

要覆盖404错误页面（“找不到文件”），请将名为`404.html`的新模板文件添加到`custom_theme`目录中。 有关可以包含在模板中的内容的信息，请查看用于构建自定义主题的文档。

要覆盖favicon，您可以在`custom_theme/img/favicon.ico`中添加一个新的图标文件。

要包含JavaScript库，请将库复制到`custom_theme/js/`目录。

您的目录结构现在应如下所示：

```YAML
- docs/
  - index.html
- custom_theme/
  - img/
    - favicon.ico
  - js/
    - somelib.js
  - 404.html
- config.yml
```

**Note**

父主题中包含的（在`name`中定义）但不包括在`custom_dir`中的任何文件将继续使用。`custom_dir`只会覆盖/替换父主题中的文件。 如果要删除文件或从头开始构建主题，则应查看用于构建自定义主题的文档。

#### 覆盖模板块

内置主题在模板块中实现了许多部分，可以在`main.html`模板中单独覆盖。 只需在`custom_dir`中创建一个`main.html`模板文件，并在该文件中定义替换块。 只要确保`main.html`扩展`base.html`。 例如，要更改MkDocs主题的标题，替换的`main.html`模板将包含以下内容：

```Django
{% extends "base.html" %}

{% block htmltitle %}
<title>Custom title goes here</title>
{% endblock %}
```

在上面的例子中，将使用自定义`main.html`文件中定义的`htmltitle`块代替父主题中定义的默认`htmltitle`块。 您可以根据需要重新定义任意数量的块，只要这些块在父级中定义即可。 例如，您可以将Google Analytics脚本替换为不同服务的脚本，或者将搜索功能替换为您自己的搜索功能。 您需要查询正在使用的父主题，以确定可以覆盖的块。 MkDocs和ReadTheDocs主题提供以下块：

- `site_meta`：包含文档头中的元标记。

- `htmltitle`：包含文档头中的页面标题。

- `styles`：包含样式表的链接标记。

- `libs`：包含页眉中包含的JavaScript库（jQuery等）。

- `scripts`：包含应在页面加载后执行的JavaScript脚本。

- `analytics`：包含分析脚本。

- `extrahead`：`<head>`中的空块，用于插入自定义标记/脚本/等。

- `site_name`：包含导航栏中的站点名称。

- `site_nav`：包含导航栏中的站点导航。

- `search_box`：包含导航栏中的搜索框。

- `next_prev`：包含导航栏中的下一个和上一个按钮。

- `repo`：包含导航栏中的GitHub存储库链接。

- `content`：包含页面的页面内容和目录。

- `footer`：包含页脚。

您可能需要查看源模板文件，以确保您的修改将适用于站点的结构。 有关可在自定义块中使用的变量列表，请参见[模板变量]。 有关块的更完整说明，请参阅[Jinja文档]。

#### 组合custom_dir和模板块

将JavaScript库添加到`custom_dir`将使其可用，但不会将其包含在MkDocs生成的页面中。因此，需要从HTML添加链接到库。

启动上面的目录结构（截断）：

```YAML
- docs/
- custom_theme/
  - js/
    - somelib.js
- config.yml
```

一个指向`custom_theme/js/somelib.js`文件的链接需要添加到模板中。 由于`somelib.js`是一个JavaScript库，它在逻辑上会进入`libs`块。 但是，仅包含新脚本的新`libs`块将替换父模板中定义的块，并且将删除父模板中库的任何链接。 为了避免破坏模板，可以使用super block从块中调用`super`：

```Django
{% extends "base.html" %}

{% block libs %}
    {{ super() }}
    <script src="{{ base_url }}/js/somelib.js"></script>
{% endblock %}
```

请注意，base_url模板变量用于确保链接始终相对于当前页面。

现在生成的页面将包含指向模板提供的库的链接以及`custom_dir`中包含的库。`custom_dir`中包含的任何其他CSS文件也是如此。