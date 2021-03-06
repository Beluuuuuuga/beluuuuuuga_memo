AIに携わる方ならNumpyを常日頃触ってると思います。

今回は、.txt形式でNumpyデータを保存します。

## この記事を読んだら理解できること
①Numpy形式のデータを.txt形式で保存する方法

②.txt形式で保存する際の桁数などを設定する方法

## どういうときに使用するのか
深層学習・機械学習で学習した重み・バイアスを出力して使用するケース

最適化の数値計算の結果を出力するケース

## 環境
numpy 1.19.4


## デフォルトで保存
まずはデフォルトで保存します。

Numpy形式のデータを.txt形式で保存するためには`np.savetxt`メソッドを使用します。

```
# Numpyライブラリを保存
import numpy as np

# Numpyで2次元の行列を作成
np_sample = np.arange(10).reshape((2, 5)) # => [[0 1 2 3 4] [5 6 7 8 9]]

# 2次元の行列を.txt形式に出力
np.savetxt('np_sample_2d.txt', np_sample_2d)

# 1次元の行列を.txt形式に出力
np_sample_1d = np_sample_2d.ravel() # => [0 1 2 3 4 5 6 7 8 9]
np.savetxt('np_sample_1d.txt', np_sample_1d)
```


.txtの出力結果は以下のようになります。

```
# 2次元での出力結果：np_sample_2d.txt
0.000000000000000000e+00 1.000000000000000000e+00 2.000000000000000000e+00 3.000000000000000000e+00 4.000000000000000000e+00
5.000000000000000000e+00 6.000000000000000000e+00 7.000000000000000000e+00 8.000000000000000000e+00 9.000000000000000000e+00


# 1次元での出力結果：np_sample_1d.txt
0.000000000000000000e+00
1.000000000000000000e+00
2.000000000000000000e+00
3.000000000000000000e+00
4.000000000000000000e+00
5.000000000000000000e+00
6.000000000000000000e+00
7.000000000000000000e+00
8.000000000000000000e+00
9.000000000000000000e+00
```

保存する次元によって出力の形式も変化していることがわかります。


ちなみにデフォルトでNumpyのデータタイプを確認します。

データタイプを確認するためには属性である`.dtype`で確認します。

先ほどの2次元のNumpyデータはint型だったので、floatでも作成します。


```
# 2次元
# 整数
np_sample_2d = np.arange(10).reshape((2, 5)) # => [[0 1 2 3 4] [5 6 7 8 9]]

# 小数
np_sample_2d_float = np.arange(10.0).reshape((2, 5)) # => [[0 1 2 3 4] [5 6 7 8 9]]
```

```
# 出力結果
print(np_sample_2d.dtype) # => int32
print(np_sample_2d_float.dtype) # => float64
```

デフォルトではNumpyデータタイプでは、整数が32ビットで小数が64ビットであることが確認できました。


## データのケタ数（浮動小数点数）を指定して保存

整数・小数形式で保存します。

データのケタ数を変更して保存する場合(浮動小数点を変更)、`np.savetxt`メソッドの引数`fmt`で選択し、小数なしの整数なら`%d` 、小数ありなら`%f`です。


```
# 1次元の行列を整数で.txt形式に出力
np.savetxt('np_sample_1d_int.txt', np_sample_1d, fmt='%d')

# 1次元の行列を8ケタの小数で.txt形式に出力
np.savetxt('np_sample_1d_float_8.txt', np_sample_1d, fmt='%1.8f')

```


出力結果は以下のようになります。

```
# 整数での出力結果：np_sample_1d_int.txt
0
1
2
3
4
5
6
7
8
9


# 小数での出力結果：np_sample_1d_float_8.txt
0.00000000
1.00000000
2.00000000
3.00000000
4.00000000
5.00000000
6.00000000
7.00000000
8.00000000
9.00000000

```

浮動小数点が変更されて保存されているかと思います。


## まとめ

深層学習の重みやバイアスの保存の場合、浮動小数点数が精度に大きく関わります。

ビット数を削ることはいわゆる量子化といわれるものでTensorFlowなどの深層学習ライブラリでAPIとして用意されています。

深層学習など普段ビット数を意識することはないと思いますが、「いざ」というときのために是非取り組んでみてください。


## 資料
- [Setting the fmt option in numpy.savetxt](https://stackoverrun.com/ja/q/4637922)
- [NumPyにおける要素のデータ型dtypeの種類と指定方法](https://deepage.net/features/numpy-dtype.html)



↓次回と次のネタ

## numpy.ndarrayのバイナリ保存は違うコーナーで言う
③Numpy形式(numpy.ndarray)のデータ保存方法
=> npzとnpsの2つ
④次元の変換方法(reshapeとtranspose)

## numpy.ndarray<=>listデータ変換は違うコーナーで言う
③Numpy形式(numpy.ndarray)のデータ作成方法
④Pythonの配列形式(list)からNumpy形式(numpy.ndarray)の変換方法

作成：numpyデータ
変換：list<=>numpy.ndarray


