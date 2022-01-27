---
title: Grasshopperをgitしたい
thumb: /img/2021/ghx-diff.png
outline: git_rhino_ghxは研究室内でgrasshopperのスパゲッティが量産されるのを解決したく始めたgrasshopperをGit/ Githubで管理しようというプロジェクトです。grasshopperはsave asからxml形式の.ghxでも保存できるのですが、それをパースして、どうにか管理することを試みています。
---


[git_rhino_ghx](https://github.com/ail-and-colleagues/git_rhino_ghx)は
研究室内でgrasshopperのスパゲッティが量産されるのを解決したく始めたgrasshopperをGit/ Githubで管理しようというプロジェクトです。
grasshopperはsave asからxml形式の.ghxでも保存できるのですが、それをパースして、どうにか管理することを試みています。

ざっくりと言えば、Grasshopperにて、外部のgrasshopper(.gh/ .ghx)を関数のように呼び出すことのできる[hops](https://developer.rhino3d.com/guides/compute/hops-component/)をgitで管理しつつ、そのサポートを[git_rhino_ghx](https://github.com/ail-and-colleagues/git_rhino_ghx)に含まれるghx_diff.pyとghx_to_dot.pyで行うことを試行しています。hopsのみで良いのでは、と思うかもしれませんが：
- .ghxではコンポーネント一つをざっくり50行くらい使って記述しているのでdiffがうまくとれない
- 保存時のビューを変更しただけ、コンポーネントを移動しただけ、でも更新されてしまうので意味のある履歴が埋もれる
など、実は管理上の問題があります。[git_rhino_ghx](https://github.com/ail-and-colleagues/git_rhino_ghx)の二つのプログラムはこのあたりをなんとかしようと試作したものです。

なお、[hops](https://developer.rhino3d.com/guides/compute/hops-component/)を用いるとコンポーネントの集まり（モジュール）に対する入出力を整理するマインドが芽生えるように思います。スパゲッティに対してはそれだけで一定の効果がありそうです。

## ghx_diff.py
ghx_diff.pyでは、.ghxのdiffをとる目的で作られています。ファイル名(.ghx)と前(left)・後(right)のブランチ名を指定すると次図のような差分:diffの表現された.ghxを
*{target\_file\_name}*(*{left\_branch\_name}*\_to\_*{right\_branch\_name}*)\_diff.ghx
として出力します。例えば、conflictした際に、これを使って採用版を作ったのち、
**git checkout --ours *target\_file.ghx***
を発行すれば競合を解決できるかと思います。

![Test](/img/2021/ghx-diff.png "Test")

## ghx_to_dot.py
ghx_to_dot.pyはちょこっとした比較用に使うイメージで作られています。次図のようにコンポーネントの関係性をグラフとして表し、.pngで保存します。大凡どのような処理であったか、あるいは、add/stagingするべき変更なのか、など判断に使えると思っています。コンポーネントにはhashを付記できる（次図でいうpanelなどのコンポーネント名の左の「58b80...」など）ので、grasshopperでありがちな：
- 同じ見た目のgh_pythonが複数存在してわからなくなる
- internalizeやset valueした値が気づかないうちに更新されていた

などをチェックすることもできるかと思います。

![Test](/img/2021/ghx-dot.png "Test")


グラフとして表す処理には、[pydot](https://github.com/pydot/pydot)を使っています。dot言語はデータをグラフとして表現するために用いられる言語の一種で、[Graphviz](https://graphviz.org/)などを使って可視化できます([pydot](https://github.com/pydot/pydot)は[Graphviz](https://graphviz.org/)を介さず直接可視化できます)。加戸は以前、[伝統木造構法で設計された四脚門の部材関係をグラフ化するという研究](http://papers.cumincad.org/cgi-bin/works/paper/caadria2019_273)でもdot言語/[Graphviz](https://graphviz.org/)を使ったのですが、ノードのレイアウトも自動的に行ってくれる点で、結構便利で楽しいツールだと思っています。

### ...
加戸はgrasshopper、Git/Githubともにnewbieなのでもう少し使いながらバージョンアップをしていくことを予定しています。

## 関連
- Version control (grasshopper forum)[https://www.grasshopper3d.com/forum/topics/version-control](https://www.grasshopper3d.com/forum/topics/version-control)
- Grasshopperの可読性を高めるには[https://blog.syntegrate.jp/2021/02/12/gh_readability/](https://blog.syntegrate.jp/2021/02/12/gh_readability/)


