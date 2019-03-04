# softprops/shiplift [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 desc 」

[中文](./readme.md) | [english](https://github.com/softprops/shiplift)

---

## 校对 🀄️

<!-- doc-templite START generated -->
<!-- repo = 'softprops/shiplift' -->
<!-- commit = '79d65c286025c551a775c0964d168e6feb4b3409' -->
<!-- time = '2018-11-14' -->

| 翻译的原文 | 与日期        | 最新更新 | 更多                       |
| ---------- | ------------- | -------- | -------------------------- |
| [commit]   | ⏰ 2018-11-14 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/softprops/shiplift.svg
[commit]: https://github.com/softprops/shiplift/tree/79d65c286025c551a775c0964d168e6feb4b3409

<!-- doc-templite END generated -->

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

### 目录

<!-- START doctoc -->
<!-- END doctoc -->

# 升船机

[![Build Status](https://travis-ci.org/softprops/shiplift.svg)](https://travis-ci.org/softprops/shiplift) [![crates.io](http://meritbadge.herokuapp.com/shiplift)](https://crates.io/crates/shiplift) [![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)

> 用于机动的生锈界面[搬运工人](https://www.docker.com/)集装箱

## 安装

将以下内容添加到您的`Cargo.toml`文件

```toml
[dependencies]
shiplift = "0.3"
```

## 文档

找到他们[这里](https://softprops.github.io/shiplift).

## 用法

可以在此存储库中找到一些小的示例程序[示例目录](https://github.com/softprops/shiplift/tree/master/examples).

### 与主持人沟通

要使用升船机,您必须首先拥有一个可随时使用的码头守护程序.通常,此守护程序进程可通过名为 env var 指定的 URL 进行解析`DOCKER_HOST`.如果您使用的是 osx,[泊坞窗机](https://docs.docker.com/machine/)通常情况下,您已经设置了运行时所需的所有内容`docker-machine env {envid}`.

```rust
extern crate shiplift;
let docker = shiplift::Docker::new();
```

如果你想更明确,你可以提供一个主机的形式`url.Url`.

```rust
extern crate shiplift;
extern crate url;

use shiplift::Docker;
use url::Url;

let docker = Docker::host(Url::parse("http://yourhost").unwrap());
```

### 图片

如果您正在与 docker 容器进行交互,那么您可能还需要与 docker 图像信息进行交互.您可以与 docker 图像交互`docker.images()`.

```rust
extern crate shiplift;

use shiplift::Docker;

let docker = Docker.new();
let images = docker.images();
```

#### 列出主机 - 本地映像

```rust
for i in images.list(&Default::default()).unwrap() {
  println!("-> {:?}", i);
}
```

#### 找到远程图像

```rust
for i in image.search("rust").unwrap() {
  println!("- {:?}", i);
}
```

#### 通过拉动现有图像来创建新图像

```rust
use shiplift::PullOptions;
let output = images.pull(
  &PullOptions::builder().image("redis:2.8.18").build()
).unwrap();
for o in output {
  println!("{:?}", o);
}
```

### 从包含 Dockerfile 的目录的内容构建映像

以下相当于`docker build -t shiplift_test .`

```rust
use shiplift::BuildOptions;

let output = images.build(
     &BuildOptions::builder(".").tag("shiplift_test").build()
).unwrap();
for o in output {
    println!("{:?}", o);
}
```

#### 访问图像信息

```rust
let img = images.get("imagename");
```

##### 检查图像信息

```rust
println!("- {:?}", img.inspect().unwrap());
```

##### 获取图像历史记录

```rust
for h in img.history().unwrap() {
  println!("- {:?}", h);
}
```

###### 删除图像

```rust
println!("- {:?}", img.delete().unwrap());
```

### 集装箱

容器是图像的实例.要获得对此接口的访问权限`docker.containers()`

```rust
extern crate shiplift;

use shiplift::Docker;

let docker = Docker.new();
let containers = docker.containers();
```

#### 列出主机本地容器

```rust
for c in containers.list(&Default::default()).unwrap() {
  println!("- {:?}", c);
}
```

#### 获取容器参考

```rust
let container = containers.get("containerid");
```

#### 检查容器细节

```rust
println!("- {:?}", container.inspect());
```

#### 访问`top`信息

```rust
println!("- {:?}", container.top().unwrap());
```

#### 查看容器日志

(todoc)

#### 查看容器更改列表

```rust
for c in container.changes().unwrap() {
  println!("- {:?}", c);
}
```

#### 流容器统计

```rust
for stats in container.stats().unwrap() {
  println!("- {:?}", stats);
}
```

### 停止,启动,重启容器

```rust
container.stop();
container.start();
container.restart();
```

### 杂项

todoc

## 路线图

有计划在 0.4.0 中从 rustc-serialize 切换到 serde 进行序列化,这不应该对当前接口产生重大影响.

Doug Tangren(softprops)2015-2016
