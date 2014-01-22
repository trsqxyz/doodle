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
