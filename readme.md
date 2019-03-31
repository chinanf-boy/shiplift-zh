# softprops/shiplift [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 操控[docker](https://www.docker.com/)容器的一个 Rust 接口 」

[中文](./readme.md) | [english](https://github.com/softprops/shiplift)

---

## 校对 ✅

<!-- doc-templite START generated -->
<!-- repo = 'softprops/shiplift' -->
<!-- commit = 'eb98b1916c0220e44e2d0f3c869c01a2dd037f60' -->
<!-- time = '2019-2-25' -->

| 翻译的原文 | 与日期       | 最新更新 | 更多                       |
| ---------- | ------------ | -------- | -------------------------- |
| [commit]   | ⏰ 2019-2-25 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/softprops/shiplift.svg
[commit]: https://github.com/softprops/shiplift/tree/eb98b1916c0220e44e2d0f3c869c01a2dd037f60

<!-- doc-templite END generated -->

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[If help, **buy** me coffee —— 营养跟不上了，给我来瓶营养快线吧! 💰](https://github.com/chinanf-boy/live-need-money)

---

# shiplift

[![Build Status](https://travis-ci.org/softprops/shiplift.svg)](https://travis-ci.org/softprops/shiplift) [![crates.io](http://meritbadge.herokuapp.com/shiplift)](https://crates.io/crates/shiplift) [![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE) [![Released API docs](https://docs.rs/shiplift/badge.svg)](http://docs.rs/shiplift) [![Master API docs](https://img.shields.io/badge/docs-master-green.svg)](https://softprops.github.io/shiplift)

操控[docker](https://www.docker.com/)容器的一个 Rust 接口

## 安装

将以下内容添加到您的`Cargo.toml`文件

```toml
[dependencies]
shiplift = "0.4"
```

## 用法

### 与主机沟通

要使用 shiplift，首先，您必须拥有一个可随时能用的 docker 守护程序。通常，此守护程序进程可通过名为`DOCKER_HOST`的环境变量，指定 URL 解析。

```rust
let docker = shiplift::Docker::new();
```

如果您希望更明确，可用一种`url.Url`形式提供一个主机。

```rust
use shiplift::Docker;
use url::Url;

let docker = Docker::host(Url::parse("http://yourhost").unwrap());
```

### 例子

可以在此存储库中的[示例目录](https://github.com/softprops/shiplift/tree/master/examples)，找到许多小的可运行示例程序。

- [containers：容器](https://github.com/softprops/shiplift/blob/master/examples/containers.rs) 》列出当前 Docker 主机上的 Docker 镜像
- [containercopyinto](https://github.com/softprops/shiplift/blob/master/examples/containercopyinto.rs) 》将字节切片作为文件复制到容器中（请参见“bytes”）。
- [containercreate](https://github.com/softprops/shiplift/blob/master/examples/containercreate.rs) 》返回用于创建新容器实例的生成器接口
- [containerdelete](https://github.com/softprops/shiplift/blob/master/examples/containerdelete.rs) 》删除容器实例
- [containerexec](https://github.com/softprops/shiplift/blob/master/examples/containerexec.rs) 》在容器中执行指定的命令
- [containerinspect](https://github.com/softprops/shiplift/blob/master/examples/containerinspect.rs) 》检查命名镜像的详细信息
- [containercopyfrom](https://github.com/softprops/shiplift/blob/master/examples/containercopyfrom.rs) 》从容器复制文件/文件夹。结果流是提取文件的压缩格式。

<br>

- [images：镜像](https://github.com/softprops/shiplift/blob/master/examples/images.rs) 》列出当前 Docker 主机上的 Docker 镜像
- [imagepull](https://github.com/softprops/shiplift/blob/master/examples/imagepull.rs) 》从现有镜像中提取并创建新的 Docker 镜像
- [imagesearch](https://github.com/softprops/shiplift/blob/master/examples/imagesearch.rs) 》按术语搜索 Docker 镜像
- [imagebuild](https://github.com/softprops/shiplift/blob/master/examples/imagebuild.rs) 》通过读取目标目录中的 docker file 生成新的镜像 build
- [imagedelete](https://github.com/softprops/shiplift/blob/master/examples/imagedelete.rs) 》删除镜像
- [imageinspect](https://github.com/softprops/shiplift/blob/master/examples/imageinspect.rs) 》从现有镜像中提取并创建新的 Docker 镜像

<br>

- [networks：网络](https://github.com/softprops/shiplift/blob/master/examples/networks.rs) 》列出当前 Docker 主机上的 Docker 镜像
- [networkcreate](https://github.com/softprops/shiplift/blob/master/examples/networkcreate.rs) 》返回用于创建新容器实例的生成器接口
- [networkdisconnect](https://github.com/softprops/shiplift/blob/master/examples/networkdisconnect.rs) 》断开容器与网络的连接
- [networkinspect](https://github.com/softprops/shiplift/blob/master/examples/networkinspect.rs) 》检查命名镜像的详细信息
- [networkconnect](https://github.com/softprops/shiplift/blob/master/examples/networkconnect.rs) 》将容器连接到网络
- [networkdelete](https://github.com/softprops/shiplift/blob/master/examples/networkdelete.rs) 》删除镜像

<br>

- [volumes](https://github.com/softprops/shiplift/blob/master/examples/volumes.rs) 》列出 Docker 卷
- [volumecreate](https://github.com/softprops/shiplift/blob/master/examples/volumecreate.rs) 》创建卷
- [volumedelete](https://github.com/softprops/shiplift/blob/master/examples/volumedelete.rs) 》删除卷

<br>

- [top](https://github.com/softprops/shiplift/blob/master/examples/top.rs) 》返回有关容器进程的信息的俯视图
- [events](https://github.com/softprops/shiplift/blob/master/examples/events.rs) 》返回 Docker 事件流
- [export](https://github.com/softprops/shiplift/blob/master/examples/export.rs) 》将此镜像导出到 tarball
- [信息-info](https://github.com/softprops/shiplift/blob/master/examples/info.rs)
- [记录-logs](https://github.com/softprops/shiplift/blob/master/examples/logs.rs)
- [状态-stats](https://github.com/softprops/shiplift/blob/master/examples/stats.rs)

## 更新计划

- give image pull chunked json a proper type

Doug Tangren（softprops）2015-2018
