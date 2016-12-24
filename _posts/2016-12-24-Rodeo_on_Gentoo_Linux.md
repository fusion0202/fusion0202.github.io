---
layout: post
title: Python IDE:Rodeo on Gentoo Linux
---
　  
   
![Rodeo](http://blogs.c.yimg.jp/res/blog-4e-0e/igproj_fusion/folder/533738/83/20438583/img_0?1482460084)

  
### node.jsのインストール

Gentooパッケージの最新バージョン（unstable）をインストールする。  

/etc/portage/package.keywords/rodeoに以下を記述。  

    =net-libs/nodejs-7.2.0 ~amd64  
    =dev-libs/libuv-1.10.0 ~amd64  
    
これにより依存パッケージopensslが“bindist”フラグを無効にして再インストールされるのだが、関連パッケージ：qtnetworkとopensshの“bindist”フラグ”が有効になっているために、不整合が生じる。  
なので、  
/etc/portage/package.use/rodeoに以下のように記述。  

    =dev-qt/qtnetwork-5.6.2 -bindist
    =net-misc/openssh-7.3_p1-r7 -bindist
    >=dev-libs/openssl-1.0.2j -bindist    
    
以上の設定を行った後、

    sudo emerge openssh qtnetwork nodejs
    
　  
　  
  
### Rodeo実行に必須のPythonパッケージのインストール


jupyter、pip、pandasの３つが必要である。

/etc/portage/package.keywords/rodeoの設定：  

    =dev-python/jupyter_console-5.0.0 ~amd64
    =dev-python/traitlets-4.3.1 ~amd64
    =dev-python/prompt_toolkit-1.0.3 ~amd64
    =dev-python/jupyter-1.0.0-r1 ~amd64
    =dev-python/entrypoints-0.2.1 ~amd64
    =dev-python/notebook-4.2.3 ~amd64
    =dev-python/nbformat-4.1.0 ~amd64
    =dev-python/widgetsnbextension-1.2.6 ~amd64
    =dev-python/ipywidgets-5.2.2 ~amd64
    =dev-python/backports-shutil_get_terminal_size-1.0.0-r1 ~amd64
    =dev-python/ipykernel-4.5.0 ~amd64
    =dev-python/qtconsole-4.2.1 ~amd64
    =dev-python/ipyparallel-5.2.0 ~amd64
    =dev-python/nbconvert-4.2.0 ~amd64
    =dev-python/jupyter_client-4.4.0 ~amd64
    =dev-python/ipython_genutils-0.1.0 ~amd64
    =dev-python/jupyter_core-4.2.0 ~amd64　
 
　   
/etc/portage/package.use/rodeoの設定：  

    >=dev-python/numpy-1.10.4 lapack
    >=dev-lang/python-2.7.12:2.7 sqlite
    >=dev-lang/python-3.4.5 sqlite
    >=dev-libs/c-blosc-1.3.5 hdf5　
    
　  
以上の設定を行った後、

    sudo emerge jupyter dev-python/pip pandas
    
　  
   
### Rodeoのビルドと実行　
　  
Rodeoプロジェクトの (https://github.com/yhat/rodeo) にあるcontributing.mdを参考にした。  
以下のコマンドを順次実行する。

    sudo npm install electron-prebuilt -g  
    git clone https://github.com/yhat/rodeo.git  
    cd rodeo  
    npm install  
    npm run build  
    npm start  
 
 

