# webp
GNU Emacs30.0.50に含まれる`java/INSTALL`にしたがってパッチを適用したwebpモジュール)のレポジトリ。

# 作成した手順
1. [Google Gitのwebp](https://android.googlesource.com/platform/external/webp/)をclone


```bash
$: git clone https://android.googlesource.com/platform/external/webp/
```

2. デフォルトの`main`ブランチからコミット`a76694a1`をチェックアウトして[^1]、修正用ブランチ`my/main`をcut

```bash
$: cd webp
$: git checkout a76694a1
$: git checkout -b my/main
```

3. `java/INSTALL`にしたがいpatchを適用

```bash
$: patch -p1 < PATCH_FOR_WEBP.patch
```

4. 上記patch ファイルとpatch適用後ファイルをcommitして空レポジトリにpush

```bash
$: git add -A
$: git commit -m 'nanika commit messages...'
$: gh repo create my-libwebp --public
$: git remote add mine https://github.com/JIBUN/my-webp.git
$: git branch -M my/main
$: git push -u mine my/main
```
[^1]: 全然思い出せませんが`nougat-*`とかでも問題ないような気がします。なんでこのコミットを使っているかというと、ImageMagickのサブモジュールとの競合を解決しようとあれこれ試していた際に、ImageMagick版の`webp`のバージョン(`v1.1.0`だったか?)の直前バージョン`v1.0.3`まで試した際の名残りです。なので今となっては特に意味はありません。
