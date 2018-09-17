# MacのBashをかっこよくする

## 対象者

細かいカスタマイズとかは考えないで  
とりあえずPowerlineを使ってみたい

## 元ネタ

https://techracho.bpsinc.jp/hachi8833/2017_12_06/49188

## Requirement

Powerlineは対応してないFontを利用すると文字が豆腐になってしまったりと   
問題があるので対応するFontのインストールが必要  
今回はFiraCodeをインストールする  

### Homebrewのインストール

インストール済みなら当然スキップ

[Homebrew](https://brew.sh/index_ja)

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### FiraCodeのインストール

リガチャ(合字)にも対応してるプログラム向きのフォント  
好みではない場合は次に紹介しているpowerline/fontを使えばいいと思う

[FiraCode](https://github.com/tonsky/FiraCode/wiki)

```
brew tap caskroom/fonts
brew cask install font-fira-code
```

### powerline/font

powerline公式？のフォント

[powerline/font](https://github.com/powerline/fonts)

```
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```

## powerline-goのインストール

といってもGolang製でReleaseがあるので  
[ここ](https://github.com/justjanne/powerline-go/releases)からバイナリをダウンロードするだけ  
Pathが通ってるところにおいたほうが楽だと思うので、  
`/usr/local/bin`以下に配置する


*2018/09/17時点での最新は1.11.0*

```bash
 curl -sL -o /usr/local/bin/powerline-go https://github.com/justjanne/powerline-go/releases/download/v1.11.0/powerline-go-darwin-amd64
```

## .bashrcに設定を記述

```bash
cat <<'_EOF_' >> ~/.bashrc
# setting powerline-go .bashrc
function _update_ps1() {
    PS1="$(powerline-go -error $?)"
}

if [ "$TERM" != "linux" ]; then
    PROMPT_COMMAND="_update_ps1; $PROMPT_COMMAND"
fi
_EOF_
```

あとはターミナルを再起動すればいけるはず！

