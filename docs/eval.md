# eval

- [bashでevalを使って変数内の文字列を評価・連結して実行する \- Qiita](https://qiita.com/curry_rohio/items/6ee94ada4c3d6ea63d1b)

---

- 変数内の文字列をコマンドとして扱う
  - 具体的には変数の解決、およびコマンドの実行をする

## sample

$b が解決され echoが実行されている

```bash
#/bin/bash

a=1
b='a=$a'
echo $b
echo "echo $b"
eval "echo $b"
```

```bash
$ sh evalstudy.sh
a=$a
echo a=$a
a=1
```

