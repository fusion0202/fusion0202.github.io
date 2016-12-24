---
layout: post
title: Pyhthon IDE:Rodeo on Gentoo Linux
---

node.jsのインストール
=
Gentooパッケージの最新バージョン（unstable）をインストールする。
/etc/portage/package.keywords/rodeoに以下を記述。

  =net-libs/nodejs-7.2.0 ~amd64
  # required by net-libs/nodejs-7.2.0::gentoo
  # required by nodejs (argument)
  =dev-libs/libuv-1.10.0 ~amd64
