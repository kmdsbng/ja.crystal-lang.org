# 文字列 (String)

文字列 ([String](http://crystal-lang.org/api/String.html)) は UTF-8 の文字の不変 (イミュータブル) なシーケンスを表したものです。

通常、ダブルクォートで囲んだ UTF-8 文字の並びで文字列リテラルを記述します。

```crystal
"hello world"
```

文字列中のいくつかの文字はバックスラッシュを使って表します。

```crystal
"\"" # ダブルクォート
"\\" # バックスラッシュ
"\e" # エスケープ
"\f" # フォームフィード (改ページ)
"\n" # ニューライン (改行)
"\r" # キャリッジリターン (復帰)
"\t" # タブ
"\v" # 垂直タブ
```

バックスラッシュに続けて最大3つの数値を入力すると、8進数でコードポイントを指定することになります。

```crystal
"\101" # == "A"
"\123" # == "S"
"\12"  # == "\n"
"\1"   # コードポイント1の文字が1つだけの文字列
```

「*u*」に続けてバックスラッシュと16進数で4つの数値を入力することでコードポイントを示すこともできます。

```crystal
"\u0041" # == "A"
```

波カッコ (ブレース) を使うと、(0 から 10FFFF までの) 16進数を指定することも可能です。

```crystal
"\u{41}"    # == "A"
"\u{1F52E}" # == "🔮"
```

文字列は複数の行にまたがって記述することができます。

```crystal
"hello
      world" # "hello\n      world" と同じ
```

上記の例で、先頭と末尾の空白、および改行が結果の文字列にも入っていることに注目してください。これを避けたければ、複数行の文字列リテラルをバックスラッシュで結合することができます。

```crystal
"hello " \
"world, " \
"no newlines" # same as "hello world, no newlines"
```

また、改行の前のバックスラッシュは文字列リテラルの中に書くこともできます。

```crystal
"hello \
     world, \
     no newlines" # "hello world, no newlines" と同じ
```

この場合、先頭の空白が結果の文字列に含まれることはありません。

もし文字列にダブルクォートやカッコなどの文字が多く含まれている場合には、次のような形式でリテラルを書くこともできます。

```crystal
# ダブルクォートと入れ子のカッコを含む
%(hello ("world")) # "hello (\"world\")" と同じ

# ダブルクォートと入れ子の角カッコ (ブラケット) を含む
%[hello ["world"]] # "hello [\"world\"]" と同じ

# ダブルクォートと入れ子の波カッコ (ブレース) を含む
%{hello {"world"}} # "hello {\"world\"}" と同じ

# ダブルクォートと入れ子の山カッコ (アングルブラケット) を含む
%<hello <"world">> # "hello <\"world\">" と同じ
```

## 文字列埋め込み (String Interpolation)

文字列の中には式を埋め込むことが可能です。これを文字列埋め込み (文字列補完/String Interpolation
) といいます。

```crystal
a = 1
b = 2
"sum = #{a + b}"        # "sum = 3"
```

このとき、`#{...}` で囲まれた式に対して、`Object#to_s(IO)` が実行されます。
