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
    
ただし、これだけだと依存パッケージopensslが“bindist”フラグを無効にして再インストールされるのだが、関連パッケージ：qtnetworkとopensshの“bindist”フラグ”が有効になっているために、不整合が生じる。  
なので、  
/etc/portage/package.use/rodeoに以下のように記述。  

    =dev-qt/qtnetwork-5.6.2 -bindist
    =net-misc/openssh-7.3_p1-r7 -bindist
    >=dev-libs/openssl-1.0.2j -bindist
