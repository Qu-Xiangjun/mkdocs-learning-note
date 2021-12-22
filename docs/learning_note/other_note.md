# 其他技巧

### 部署技巧

当我们修改好文档时，需要执行`mkdocs gh-deploy`命令才能将其部署到GitHub Page上。

我们还可以采用`CI`持续集成工具在github上自动部署，即在根目录加上 .github/workflow目录，然后创建`ci.yml`文件，参考如下例子：

```YAML
name: ci 
on:
  push:
    branches: 
      - master # 监测的分支
jobs:
  deploy:
    runs-on: ubuntu-latest # 拉去虚拟环境镜像
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
        with:
          python-version: 3.x
      - run: pip install -r requirements.txt # 虚拟环境安装依赖
      - run: mkdocs gh-deploy --force # 会在虚拟环境部署站点，无需本地使用此命令
```

如此，在每次master分支push新东西都将引起一次CI持续集成的`action`，同时其中15行会再引起一次 gh-deploy `action`

![img](https://d37hhp00kf.feishu.cn/space/api/box/stream/download/asynccode/?code=Njg5YzM4NzE5OGUxN2Y3YThkMjgzYzU3YzY1MjNlOWJfTVVWRjQ2UUI2TEFiMVpXeXl0clN4S1A2YzBORjdnV1lfVG9rZW46Ym94Y25aSEhKTEZSck1Heks3cDBxMFBhemdkXzE2NDAxODg0MzQ6MTY0MDE5MjAzNF9WNA)