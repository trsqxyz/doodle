# 2.Python インタプリタを使う
## 引数の受け渡し
スクリプト名と引数を指定してインタプリタを起動した場合、スクリプト名やスクリプト名以後に指定した引数は、文字列のリストに変換されて sys モジュールの argv 変数に格納されます。 import sys することでこのリストにアクセスすることができます。 sys.argv には少なくとも一つ要素が入っています。スクリプト名も引数も指定しなければ sys.argv[0] は空の文字列になります。スクリプト名の代わりに '-' (標準入力を意味します) を指定すると、 sys.argv[0] は '-' になります。 -c command を使うと、 sys.argv[0] は '-c' になります。 -m module を使った場合、 sys.argv[0] はモジュールのフルパスになります。 -c command や -m module の後ろにオプションを指定した場合、 Python インタプリタ自体はこれらの引数を処理せず、 sys.argv を介して command や module から扱えるようになります

## 実行可能な Python スクリプト
`% chmod +x myscript.py`
でスクリプトに実行モードを与えることができる

## カスタマイズ用モジュール
Python はユーザーが Python をカスタマイズするための2つのフック、 sitecustomize と usercustomize を提供しています。 これがどのように動作しているかを知るには、まずはユーザーの site-packages ディレクトリの場所を見つける必要があります。 Python を起動して次のコードを実行してください:
>>>

>>> import site
>>> site.getusersitepackages()
'/home/user/.local/lib/python3.2/site-packages'

usercustomize.py をそのディレクトリーに作成して、そこでやりたいことをすべて書くことができます。 このファイルは自動インポートを無効にする -s オプションを使わない限り、全ての Python の起動時に実行されます。

sitecustomize モジュールも同じように動作しますが、一般的にコンピューターの管理者によって、グローバルの site-packages ディレクトリに作成され、 usercustomize より先にインポートされます。 詳細は site モジュールのドキュメントを参照してください。

# 3. 形式ばらない Python の紹介
## 3.1.1. 数
対話モードでは、最後に表示された結果は変数 _ に代入されます。このことを利用すると、 Python を電卓として使うときに、計算を連続して行う作業が多少楽になります。以下に例を示します:
>>>

>>> tax = 12.5 / 100
>>> price = 100.50
>>> price * tax
12.5625
>>> price + _
113.0625
>>> round(_, 2)
113.06

ユーザはこの変数を読取り専用の値として扱うべきです。この変数に明示的な代入を行ってはいけません — そんなことをすれば、同じ名前で元の特別な動作をする組み込み変数を覆い隠してしまうような、別のローカルな変数が生成されてしまいます。

## 3.3.2. 文字列
連続して並んでいる複数の 文字列リテラル (つまり、引用符に囲われた文字列) は自動的に連結されます。
この機能は特に、長い文字列を改行したいときに役に立ちます:
>>>

>>> text = ('Put several strings within parentheses '
            'to have them joined together.')
>>> text
'Put several strings within parentheses to have them joined together.'

# 4. その他の制御フローツール
## 4.2. for 文
ループ内部でイテレートしているシーケンスを修正する必要があれば (例えば選択されたアイテムを複製するために)、最初にコピーを作ることをお勧めします。シーケンスに対するイテレーションは暗黙にコピーを作りません。スライス記法はこれを特に便利にします:
>>>

>>> for w in words[:]:  # Loop over a slice copy of the entire list.
...     if len(w) > 6:
...         words.insert(0, w)
...
>>> words
['defenestrate', 'cat', 'window', 'defenestrate']

## 4.4. break 文と continue 文とループの else 節
for ループの次のイテレーションに戻る continue 文以降の処理は行われない

## 4.4.7. 引数リストのアンパック
引数がすでにリストやタプルになっていて、個別な固定引数を要求する関数呼び出しに渡すためにアンパックする必要がある場合には、逆の状況が起こります。例えば、組み込み関数 range() は引数 start と stop を別に与える必要があります。個別に引数を与えることができない場合、関数呼び出しを * 演算子を使って書き、リストやタプルから引数をアンパックします:
>>>

>>> list(range(3, 6))            # normal call with separate arguments
[3, 4, 5]
>>> args = [3, 6]
>>> list(range(*args))            # call with arguments unpacked from a list
[3, 4, 5]

同じやりかたで、 ** オペレータを使って辞書でもキーワード引数を渡すことができます:
>>>

>>> def parrot(voltage, state='a stiff', action='voom'):
...     print("-- This parrot wouldn't", action, end=' ')
...     print("if you put", voltage, "volts through it.", end=' ')
...     print("E's", state, "!")
...
>>> d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
>>> parrot(**d)
-- This parrot wouldn't VOOM if you put four million volts through it. E's bleedin' demised !

## 4.7.7. 関数のアノテーション
関数のアノテーション はユーザ定義関数に対する完全にオプションな任意のメタデータ情報です。 Python 自身と標準ライブラリの両方とも、あらゆる意味で関数アノテーションを利用しません; このセクションは単に文法を示します。サードパーティのプロジェクトは、ドキュメンテーションや型検査、その他の用途のために関数アノテーションを自由に使用することができます。

アノテーションは関数の __annotations__ 属性に辞書として格納され、関数の他の部分には何も影響がありません。パラメータアノテーションは、パラメータ名の後にコロンを続けることによって定義され、その後にアノテーションの値として評価される式が置かれます。戻り値アノテーションは、パラメータリストと def ステートメントの終わりを表すコロンの間に置かれたリテラル -> によって定義され、その後に式が続きます。次の例は無意味な位置引数とキーワード引数、そして戻り値アノテーションを持っています:
>>>

>>> def f(ham: 42, eggs: int = 'spam') -> "Nothing to see here":
...     print("Annotations:", f.__annotations__)
...     print("Arguments:", ham, eggs)
...
>>> f('wonderful')
Annotations: {'eggs': <class 'int'>, 'return': 'Nothing to see here', 'ham': 42}
Arguments: wonderful spam

## 4.8. 間奏曲: コーディングスタイル
慣習では CamelCase をクラス名に使い、 lower_case_with_underscores を関数名やメソッド名に使います

# 5. データ構造
## 5.3. タプルとシーケンス
>>> t = x, y, z #  tuple packing
>>> x, y, z = t #  tuple unpacking

## 5.4. 集合型
set() or {} 
  
# 6. モジュール
## 6.1. モジュールについてもうすこし
>>> from fibo import *
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377

この書き方ではアンダースコア (_) で始まるものを除いてすべての名前をインポートします。 殆どの場面で、 Python プログラマーはこの書き方を使いません。 未知の名前がインタープリターに読み込まれ、定義済みの名前を上書きしてしまう可能性があるからです。

一般的には、モジュールやパッケージから * を import するというやり方には賛同できません。というのは、この操作を行うとしばしば可読性に乏しいコードになるからです。しかし、対話セッションでキータイプの量を減らすために使うのは構わないでしょう。

ノート

実行効率上の理由で、各モジュールはインタープリタの 1 セッションごとに 1 回だけ import されます。従って、モジュールを修正した場合には、インタープリタを再起動させなければなりません – もしくは、その場で手直ししてテストしたいモジュールが 1 つだった場合には、例えば import imp; imp.reload(modulename) のように imp.reload() を使ってください。

## 6.1.3. "コンパイル"された Python ファイル
Python はソースの変更日時をコンパイル済みのものと比較し、コンパイル済みのものが最新でなくなり再コンパイルが必要になっていないかを確認します。これは完全に自動で処理されます。また、コンパイル済みモジュールはプラットフォーム非依存なため、アーキテクチャの異なるシステム間で同一のライブラリを共有することもできます。

## 6.2. 標準モジュール
sys.ps1 と sys.ps2 という変数は一次プロンプトと二次プロンプトに表示する文字列を定義しています

# 7. 入力と出力

# 8. エラーと例外

# 9. クラス

# 10. 標準ライブラリミニツアー
# 10.1. OS へのインターフェース
from os import * ではなく、 import os 形式を使うようにしてください。そうすることで、動作が大きく異なる組み込み関数 open() が os.open() で隠蔽されるのを避けられます。

# 11. 標準ライブラリミニツアー - その２
## リスト操作のためのツール
heapq モジュールは、通常のリストでヒープを実装するための関数を提供しています。ヒープでは、最も低い値をもつエントリがつねにゼロの位置に配置されます。ヒープは、毎回リストをソートすることなく、最小の値をもつ要素に繰り返しアクセスするようなアプリケーションで便利です。
>>>

>>> from heapq import heapify, heappop, heappush
>>> data = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
>>> heapify(data)                      # rearrange the list into heap order
>>> heappush(data, -5)                 # add a new entry
>>> [heappop(data) for i in range(3)]  # fetch the three smallest entries
[-5, 0, 1]



