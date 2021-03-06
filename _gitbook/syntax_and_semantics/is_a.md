# is_a?

`is_a?` という擬似メソッドを使うと、ある他の型を継承、もしくはインクルードしていることを判定できます。例をあげます。

```crystal
a = 1
a.is_a?(Int32)          #=> true
a.is_a?(String)         #=> false
a.is_a?(Number)         #=> true
a.is_a?(Int32 | String) #=> true
```

これが擬似メソッドである理由は、[if 変数.is_a?(...)](if_varis_a.html) で説明したように、このメソッドはコンパイラによって参照され、それによって型情報を設定することができるためです。また、コンパイル時に知っておく必要のある[型](type_grammar.html)を引数として指定することも可能です。
