
![http://i.imgur.com/o15drKg.jpg](http://i.imgur.com/o15drKg.jpg)
OrangePi Liteを買いました。名刺サイズながら最初からWifiが搭載されているやつです。


[早速wifiを有効化させるところまで纏めましたが](http://qiita.com/m0a/items/6608feb654c64ea45dd1)、Qiitaではいまいち人気がない様子。

気を取り直して、当初の目的であるOctoPrintを導入します。
ラズパイみたいな人気のやつの場合は最初からOctoPiというのがありまして
SDカードにイメージを入れるだけで全部入りの環境が手に入ります。

でもこいつは安いのが魅力。本体だけなら1200円くらいです。

OctoPiほどではないけどAnsibleをつかって全自動で構築まで持っていきましょう。
仮にSDが壊れても瞬時に復旧できるように。

# Ansibleって

自分のPCからOrangePiにsshアクセスして自動で必要なコマンドやファイルコピーを行って
環境を自動構築してくれるツールです。こいつを使えば、SDにイメージを焼く程にすぐには出来ませんが
待ってれば環境を作ってくれます。

# wifiの設定までは自動化出来ず。

ということで少なくともssh接続できるように
wifi経由でsshできる状態まで設定しておく必要があります。

その手順はQiitaに纏めましたのでご参照下さい
[OrangePi LiteのWIFI設定(armbian)](http://qiita.com/m0a/items/6608feb654c64ea45dd1)

固定Ipを使ったほうがいいでしょうね。

# Ansibleの準備

macであればbrewコマンドで簡単にインストールできます。
windowsの場合も最近はlinux環境があるそうなんで簡単じゃないでしょうか？
macなら以下で入ると思います。
 ```
 brew install ansible
 ```
windowsは自分で調べて下さい。ubuntu環境を手元に作れるはずです。


# 構築開始

必要なファイルをgitで取得します。

```
  ❯ git clone https://github.com/m0a/octoprint_armbian.git
  ❯ cd octoprint_armbian
```
接続するときのipを設定します

```
  ❯ cat hosts
[octoprint_server]
192.168.11.111
```
ここを自分の設定したOrangePiのipに変えて下さい

sudo時のパスワードを設定しておきます。
```
  ❯ cat group_vars/octoprint_server.yml
ansible_sudo_pass: p@ssword

octoprint_version: 1.3.0rc1
.......
%
```
p@sswordのところを適時変えて下さい

後はオプションでバージョンの変更をして下さい(octoprint_versionにTagを指定できます。)


コレで構築開始です。
```
  ❯ ansible-playbook -i hosts playbook.yml
```

あとは待つだけのはず。

OctoPrintとカメラの設定が終わります。
カメラは普通のUSBWEBカメラならなんでも良いかと思います。
俺はこいつを使っています。
[LOGICOOL ウェブカム HD画質 120万画素 C270](https://www.amazon.co.jp/LOGICOOL-%E3%82%A6%E3%82%A7%E3%83%96%E3%82%AB%E3%83%A0-HD%E7%94%BB%E8%B3%AA-120%E4%B8%87%E7%94%BB%E7%B4%A0-C270/dp/B003YUB660)


こんな画面になればokです。

{{<img "octoprint.jpg">}}

デフォルトでタイムラプスを取るように設定済みです。

{{<youtube "aNHr-nNFhQs">}}

なんだか久しぶりに触ったら色々機能が追加されてるみたいですね。色々いじりがいがありそうです。



