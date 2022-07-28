---
title: 建築学生向けのpointnet
thumb: /img/2022/theta-sample.png
outline: ゼミのネタとして作成した点群処理のネットワークpointnetで分類を行うサンプルです。pointnetのサンプルはkerasのチュートリアルをはじめ数多く公開されているのですが、python初心者語で書く・とりあえず動かすところまでで躓かないをモットーに改めて作成してみたものをせっかくなので建築学生向け（？）として公開してみます。
---


Repository: [pointnet_cla](https://github.com/ail-and-colleagues/pointnet_cla)は三次元点群を[pointnet](https://arxiv.org/abs/1612.00593)を使って分類（**cla**ssificaiton）するサンプルです。学習用のデータも三次元メッシュを操作できるライブラリ[trimesh](https://trimsh.org/index.html)を使ってply形式のデータとして生成するところも含めています。このあたりも含めて、建築学生含む情報分野が専門でない人向けに：

* データセットが簡単に用意できる
* 保守性はさておき読みやすい
* とりあえず動かしやすい

ように作成したつもりです。ゼミで使ってみた限り（そういえばwindowsのみです）手順通りで問題なく動作するのを確認しています。

また、trimeshで作成している学習用データの部分を自前のデータに移し替えて使う想定で、RhinocerosのGrasshopperで3D isovistな三次元点群を出力するサンプル「export_3D_isovist_pointcoud.gh」も置いてあります。これを使うと、[Repository(pointnet_cla](https://github.com/ail-and-colleagues/pointnet_cla))のsidenoteに付記したように、建築作品A~Xを視界の広がりにもとづき分類する、といった学習もできるかと思います。

使い方などは[Repository(pointnet_cla](https://github.com/ail-and-colleagues/pointnet_cla))のほうに書いてありますので確認ください。


作成中