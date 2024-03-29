


# ============================= ■■■ １ Pythonについて

名前の由来はモンティ・パイソン

バージョンのあとにプロンプト

>>> if aa == 1:
...     print(aa)
... 
1
>>> 

## --------------- 対話モード
インデントは自分でスペースを入れる

プロンプトは 「>>>」と「...」

多重代入
a, b = 0, 1

## --------------- コーディングスタイル
コメントは独立行
1行79文字を超えない
インデントはタブは使わず、スペース4個

## --------------- 入力ヒストリ
.python_history に保存される

# ============================= ■■■ ２ テキストと数値演算

文字列リテラルの連結、複数行記述する場合は()でくくって書く
text = (
    "text "
    "text "
    "text "
)
## --------------- 文字列のスライス

文字列[開始位置:終了位置]

word = 'abcdefg'
sliced = word[2,5]

  |a|b|c|d|e|f|g|
  1 2 3 4 5 6 7 8
なので、word[2,5] は 'bcd'
マイナス値は、後ろから何個目かを表す
空欄は最初または最後

"""文字列""" または '''文字列''' では、文字列中の改行が反映される

## --------------- 繰り返し要素の数を求めるには len()

## --------------- フォーマット
数値:b		2進表示
数値:d		10進表示、ndでn桁表示
数値:x		16進表示
数値:%		％表示、数値は100倍したものを表示
数値:.5f	小数点以下5桁

文字列.format()形式

print("{0},{1},{2}".format(a,b,c))	インデックス番号を記載
print("{},{},{}".format(a,b,c))		インデックス番号を省略パターン
print("{a},{b},{c}".format(a=,b,c))	インデックス番号を記載

print("{:02d},{:02d},{:02d}".format(a,b,c))	フォーマット指定するときは、文字列の方に書く

# ============================= ■■■ ３ リスト操作
リスト定義は角括弧内にカンマ区切りで記述
インデックスで参照でき、先頭のインデックスはゼロ、末尾は-1

## --------------- リストのスライス
リスト[開始位置:終了位置] 
開始位置省略は先頭から、終了位置省略は最後までとなる

[1, 2, 3, 4]
0  1  2  3  4
           -1

## --------------- 
要素の追加は、リスト.append(値)
要素の参照後削除は、リスト.pop(インデックス)
要素数を求めるのは len(リスト)

## --------------- リストの入れ子
[リスト１, リスト2, リスト3]
長さは３になる
子どものリストは、それぞれ型、長さが違っても良い
参照は、リスト名[親インデックス][子インデックス]

## --------------- リストでスタックを作る(FILO)
append(値)で末尾に追加し、pop()で末尾から値の取り出しと削除を行う

## --------------- リストでキューを作る(FIFO)
append(値)で末尾に追加し、pop(0)で先頭から値の取り出しと削除を行う

## --------------- リスト内包
data = []
for i in [1,2,3]:
    for j in [1,2]:
        if i != j:
            data.append((i,j))
print(data)

内包表記すると、
print([(i,j) for i in [1,2,3] for j in [1,2] if i != j:])

# ============================= ■■■ ４ 判定と繰り返し
## --------------- if文
条件の and or

if 条件:
    処理
elif 条件:
    処理
else:
    処理

## --------------- 条件式
## --------------- 演算子

## --------------- 短絡演算子
整数値の評価はその数値そのもの、真偽判定は0なら偽、0以外なら真
0 and 1 は 0 を真偽判定して偽なので、そこで判定をやめ、最後の要素の評価値の0を返す
0 or 1 は 0 を真偽判定して偽なので次にいき、1を真偽判定して真なので、最後の要素の評価値の1を返す

## --------------- Noneとの比較
Noneとの比較は、isを使う
== でもできるが、最適ではない

## --------------- 真偽判定

## --------------- for文
for 変数 in リスト:
    処理
else:
    処理

range(end)
range(start, end)		endは含まれないので注意
range(start, end, step)

## --------------- 並べ替え

## --------------- ディクショナリ型
dict名.items()    キーと値のペアを取得

data = {'key1':100, 'key2':200}
for key,val in data.items()

dict型.items()	キーと値のペアのリスト
dict型.keys()	キーのリスト
dict型.values()	値のリスト

## --------------- enumerate()

iterable=反復可能体(リスト、タプル、ディクショナリ、文字列）

enumerate(反復可能体) でインデックスと値ペアのリストを返す

for i, c in enumerate(文字列):
    print(f'index={i}, char={c}')

## --------------- sorted(), reversed()
sorted(反復可能体)	昇順ソートした反復可能体を返す
reversed(反復可能体)	並びを逆順にした反復可能体を返す
list(文字列)		文字列を文字でバラしたリストを返す

## --------------- zip()
複数の反復可能体をまとめたリストを作る

zip([1, 2, 3], ['a', 'b', 'c'])
 → (1,'a'), (2,'b'), (3,'c')
 → 最終的には　list(zip()) とかしてlistに変換が必要

文字列 * 整数 = 文字列文字列・・・(整数個繰り返し）

# ============================= ■■■ ５ 関数
def 関数名(引数):
    global gval		
    return retval

リターン文がない場合は None が返される

## --------------- 変数で関数を参照
以下の形式で、関数を変数に入れて変数経由で呼び出せる
変数 = 関数名
変数() 

## --------------- 変数
global変数を書き換える場合 global 変数の宣言が関数内で必要、参照だけなら不要
関数内でglobalじゃない変数へ代入した場合、その変数はローカル変数として扱われる

## --------------- 位置引数とキーワード引数、デフォルト値
def func(arg, karg1=1, karg2=2):
    pass

引数名のない位置引数は最初に、その後キーワード引数を必要なものだけ続ける
func(0)
func(0, karg1=10, karg2=20)
func(0, karg2=20)

引数のデフォルト値は、関数定義(ロード)時点で評価される
デフォルト値を変数で指定した場合、ロード時の値となる

デフォルト値がリストの場合、デフォルト値としてのリストオブジェクトがstaticに確保されているため、
リストを操作すると、デフォルト値としてのリストオブジェクトが変更され、デフォルト値が変わってしまう

def func(number, listval=[]):
    listval.append(number)
    return listbval

func(3, [1, 2]) の場合、引数の[1,2]に3がappend(3)されてそれが返される。デフォルト値は変化なし

func(3) の場合、デフォルト値の[]自体にappend(3)が行われ、[3]が返される。
次にfuncが呼ばれた時のデフォルト値は、先程書き換えられているので[3]となる

## --------------- リスト、タプルを引数で渡す

def func(arg, *listarg, **dictarg):
    pass
func(1, 1,2,3,4, key1='a', key2='b')

arg = 1
listarg = [1,2,3,4]
dictarg = {key1:'a', key2:'b'}


def func(arg, arg2, arg3, arg4, arg5):
    pass
listvar = [1,2]
dictvar = {arg4: 3, arg5: 4}
func(1, *listvar, **dictvar)
 → func(1, 1,2, arg4=3, arg5=4)

## --------------- lambda式
1行の式だけで構成される関数を定義する

関数変数 = lambda 引数: 式

func = lambda a,b: a+b
func(1,2) は 1+2=3となる

## --------------- docstring
関数のコメント
def func(x, y):
    """関数の1行説明・要約
    
    1行開けて、詳細な説明
    """

print(func.__doc__) で参照できる

# ============================= ■■■ ６ その他コレクションの操作

## --------------- collection.deque
from collection import deque
que = deque(["val1", "val2"])
que.append("val3")		末端に追加
que.appendleft("val3")		先頭に追加
que.pop()			末端を
que.popleft()

## --------------- タプル
タプル：const配列みたいな、書き換え不可なリスト

sample_tuple = ('val1', 'val2', 'val2')		括弧付きで定義
sample_tuple = 'val1', 'val2', 'val2'		括弧省略
sample_tuple = 'val1',				要素が1つのとき、コンマ必要

sample_tuple = tuple(反復可能体)		ただのコンマ区切りは不可なの注意
sample_tuple = tuple(['val1', 'val2', 'val2'])

タプルとリスト
共通：lenで長さ取得、異なる型の要素で構成可
違い：listは追加変更可、タプルは変更不可

## --------------- set
セット：重複しないリスト、順番保証なし、和集合・差集合を演算できる

sample_set = set([1,2,3,4,5])	リストからset
sample_set = set((1,2,3,4,5))	タプルからset
sample_set = set("asddffgdfg")	文字列からset
sample_set.add(6)

和集合：set1とset2のすべての要素、ベン図の全体
set1 | set2 = s1.union(s1)

差集合：set1の要素からset2に含まれる要素を除いたもの、ベン図の左
set1 - set2 = s1.difference(s2)

積集合：set1とset2の両方にある要素、ベン図の中央
set1 & set2 = s1.intersection(s1)

対称差：set1とset2の片方にのみある要素、ベン図の左右
set1 ^ set2 = s1.symmetric_difference(s1)

## --------------- ディクショナリ

変数 = {キー1: 値1, キー2:値2, ...}

キーは不変体(const)である必要があるので、タプルはOKだけどリストはNG、数値もOK
文字列をキーにするとき、""でくくる

値 in dict_val は、キーに値と一致するものがあるかをチェックする
→ 値 in dict_val.keys() と同義
→ 値 in list(dict_val) も同義、list(dict_val) は keys のリストを返す

dict_val[キー] = 値	キーを追加・書き換え
del dict_val[キー]	キーを削除

内包表記   {キーの式: 値の式 for 変数 in 反復可能体}

   dict_val = {x: x+1 for x in range(10)}

## --------------- リスト

内包表記   {値の式 for 変数 in 反復可能体}

   list_val = {x*2 for x in range(10)}

# ============================= ■■■ ７ モジュール
-
## -------------- インポート
import モジュール名
モジュール名.関数名()

import モジュール名 as 別名
別名.関数名()

from モジュール名 import 関数名
関数名()

from モジュール名 import 関数名 as 別名
別名()

from モジュール名 import *
	先頭が_以外のすべてをimport
	__all__ というリストがあったらそのリストのラベルをimport

__name__  
	モジュール名が入る
   	メインモジュールなら、"__main__" になる
if __name__ == "__main__":
	main_func()

## --------------- __init__.py

package_name/__init__.py
という構成にすると、import package_name できるパッケージになる
他の *.py ファイルは、サブモジュールとなる

__init__.pyの中身
	同フォルダの *.py だけなら空ファイルで良い
	特定の py を読む場合
	from . import submodulename

	サブフォルダがある場合は、サブフォルダにも__init__.pyを置く

# ============================= ■■■ ８ ファイル入出力

## --------------- オープン
open(ファイル名, モード)

	"r"	読み込み専用(省略時デフォルト)
	"r+"	読み書き両用
	"w"	新規書き込み
	"a"	追加書き込み
	"rb","wb","ab"
		バイナリモード("b"はオプションなので単体では使用不可)

fp = open(ファイル名, "r")
s = fp.read()
  → ファイルの全行が改行'\n'区切りでsに読み込まれる

with open(ファイル名, "r") as fp:
    s = fp.read()
→ 終了や例外で自動的にクローズされる

## --------------- ファイルを1行ずつ読み込む場合
    for s in fp:
	or
    for s in list(fp):
	or
    for s in fp.readlines()

## --------------- ファイルを1文字ずつ読み込む場合
    for c in fp.read():

## --------------- ファイル書き込み
fp = open(ファイル名, "w")
fp.write(s)
fp.close()

## --------------- JSON書き込み
    json.dump(data, fp)		json.dump()はファイル書き込み
	or
    fp.write(json.dumps(data))	json.dumpos() は dump string

## --------------- JSON読み込み
    data = json.load(fp)		json.load()はファイル読み込み
	or
    data = json.loads(fp.read())	json.loads() は load string

# ============================= ■■■ ９ 例外処理

SyntaxError：構文エラー
ValueError：値が適切でない(型はあっていても値が範囲外でだめな場合など)
KeyError：ディクショナリでキーが存在しない
NameError：未定義の変数・関数参照(C言語のundefined symbolと同等)

raise ValueError(メッセージ文)	tryの中で任意のエラーを発生させる

try:
    ... 正常系処理
except TypeError:
    ... エラー処理
except (TypeError, NameError):	複数の場合はタプル形式
    ... エラー処理
finally:
    ... 共通処理()


# ============================= ■■■ １０ クラスとオブジェクト

## --------------- クラス定義・インスタンス定義

class クラス名:
    クラス変数名 = 値
    def __init__(self):			コンストラクタ
        ....
    def __del__(self):			デストラクタ
        ....
    def メソッド名(self):		通常のメソッド
	print(self.クラス変数名)	クラス変数の参照は self.クラス変数名
	self.メソッド名()		メソッドの呼び出しも self.メソッド名()
        ....

instance = クラス名()

class クラス名(基底クラス):	(基底クラス)をつけると派生クラスの定義になる

## --------------- 型の判定

isinstance(変数名, 型)
形には通常の型(int, strなど)が指定できる
変数名がクラスのインスタンスの場合、基底クラスも派生クラスもTrueが返る

type(変数名)
型を表す文字列を返す

# ============================= ■■■ １１ 標準ライブラリ

## ---------------
currect_work_directory = os.getcwd()
os.chdir("path")

## ---------------
glob.glob("wild_card")
 → 正規表現ではなく、shと同じワイルドカード

## --------------- 引数
sys.argv は [コマンド名, 引数1, 引数2...] に等しい

## --------------- argparserモジュール
import argparser

parser = argperse.Argmentparser()
parser.add_argment("--head")
perser.add_argment("body", nargs="+")  '+'は1個以上必須の意味
args = parser.parse_args()

Namespage(head='1', body=['2', '3'])
args.head = '1'
args.body = ['2', '3']

parser.add_argment("-h", "--head", type=int, default=10)

## --------------- mathモジュール
from math import log, pi
ログの計算：log(16, 2) は４，第１引数は第２引数の４乗だから、答えは４

## --------------- randomモジュール
import random

random.choice(range(10))
 → 0-10までのいずれかの値をランダムに選ぶ

random.random() は引数なしで、0-1までのランダム小数点値を返す
値の幅で倍してオフセットを加算して範囲を調整する
-1から1だと、幅２、開始位置-1なので２倍して－１する

## --------------- statistics(統計)モジュール
import statistics
data = [-1,-1,-1,-1,4]
statistics.mean(data) = 0	平均
statistics.median(data) = -1	中央値(ソートした時の中央値)

statistics.variance(data)	不偏分散(平均との２乗の差を(データ数－１)で割った値)
 = ((0-(-1))**2 + (0-(-1))**2 + (0-(-1))**2 + (0-(-1))**2 + (0-4)**2
 = (1**2 + 1**2 + 1**2 + 1**2 + 4**2) / (5-1)
 = 5

## --------------- urllib モジュール
import urllib.request import urlopen

with urllib.request.urlopen('url') as rs
	s = rs.read().decode()		バイナリモードなので、decode()が必要

## --------------- datetime モジュール
from datetime import datetime

dt = datetime(2000, 12, 31)
print(dt.strftime("%Y-%m-%d")		# string format time

dt1 = datetime(2001,1,1)
dt2 = datetime(2002,1,1)
diff = d12 - dt1
print(diff.days)
 → 365

## --------------- unittest モジュール
import unittest

class TestSample(unittest.TestCase):
    def test(self):
        actual = test_func()
	expected = 5
	self.assertEqual(actual, expected)

## --------------- pprint モジュール
import pprint
pprint.pprint(lines)
['line1',
 'line2',
 'line3']
 ※ pprint は括弧がつく

print(",\n".join(lines))
'line1',
'line2',
'line3'

import textwrap
print(textwrap.fill(", ".join(lines), width=24)
'line1',
'line2',
'line3'

## --------------- re モジュール（正規表現）
import re
re.sub(パターン、置換文字列、対象文字列)

特殊文字
  ()	カッコ内をグループ化
  [a-z]	小文字のアルファベット１文字
  ＋	直前の文字の１回以上繰り返し
  \1	１番目のグループ

r"" はraw文字列、\をただの文字として扱うため

# ============================= ■■■ １２ 仮想環境・サードパーティ

仮想環境作成時、バージョン指定可、フォルダ指定は必須、複数環境あっても互いに影響しない

仮想環境の作成
python3 -m venv venv_folder
仮想環境を有効化
source venv_folder/bin/activate

python3 -m pip install <package_name>
	or
pip install <package_name>

pip install <package_name>=<version_string>
バージョン指定でインストール

インストール済みの場合、バージョン指定なしでインストールしても最新にはならない

パッケージの一覧を表示
pip list

# ============================= ■■■ 模擬試験

## ----------------
3-1. Pythonの特徴に関する次の記述のうち、誤っているものはどれか。

  a) Pythonの特徴の一つが可読性の高さである。複雑な操作も単一文で表記可能であり、文のグルーピングが
     インデントで行われるためコードの見通しが良いなど、プログラムを小さく読みやすく書けるようになっている。
     ただ変数の宣言は必要であり行わないとエラーとなる。
	★参照前に値の代入が必要なだけ
  b) 機械学習、AI、データ分析の分野でPythonが用いられる理由の一つは、Numpyやpandas、scikit-learnなど
     機械学習向けのサードパーティ製パッケージやそれを用いた環境（Jupyter Notebookなど）が充実していることである。
  c) Pythonは柔軟な配列や集合、ディクショナリといった、高水準のデータ型を組み込みで持つ。
     データ型の一般性が高いためPythonの対応可能な問題領域はAwkやPerlと比較して広い。
  d) Pythonは簡単に使えるとはいえ本格的なプログラム言語であり、大きなプログラムを書くために提供された構造や
     サポート、エラーチェック機構が、シェルスクリプトなどに比べはるかに多く存在する。
  e) PythonはWindows、MacOS、Linuxなど多くの環境で動作する、拡張可能なフリーのオープンソースソフトウェアである。

## ----------------
3-2. Pythonインタープリタに関する次の記述のうち、誤っているものはどれか。

  a) Pythonモジュールを呼び出すには、「python -m モジュール名 [引数] …」という方法があり、
     例えば「python -m timeit -h」を実行すると、timeitモジュールの詳細が出力される。
	★python -m モジュール名 [引数] … でモジュールを実行
  b) インタープリタの起動方法として、「python -cmd コマンド [引数] …」という方法があり、
     例えば「python -cmd 'print("hello")'」を実行すると、「hello」が出力される。
	★python -c 'print("hello") が正解、-cmd は無い
  c) 対話モードの終了方法には、関数の入力によるものと、キー操作によるものとがある。
     前者の具体的な方法は、quit()の入力である。後者の具体的な方法は、ファイル終端キャラクタの入力である。
	★quit() または ファイル終端キャラクタ(Ctrl-D)で終了
  d) インタープリタがスクリプト名（スクリプトのファイル名）と続く引数群を知らされると、これらは文字列の
     リストとなる。import sys を実行することで、このリストにアクセスできる。
	★sys.argv リストに格納
  e) デフォルトでは、PythonのソースファイルはUTF-8でエンコードしてあるものとして扱われる。
	★デフォルトでソースファイルはUTF-8でエンコードされているものとして扱われる

## ----------------
7. 次の変数Zenに関して指定した場合、実行時にエラーとなるものはどれか。
Zen = 'SimpleIsBetterThanComplex'
Correct Answer: Zen[0] = 'J'

★文字列変数を配列のようにして文字参照できるが、イミュータブルなので書き換えるはできない

## ----------------
3-18. 次のコードの実行結果として正しいものはどれか。

a = [1,3,4,6,3,5]
a.insert(3, -1)
a.pop(4)
a.remove(3)
print(a)

  a) [1, 4, -1, 5]
  b) [1, 4, -1, 3, 5]
  c) [1, 4, 6, 5, 3]
  d) [1, 6, 3, 5, 3]
  e) [1, 6, 5]

★ remove(n) は、最初に見つかった1個だけを削除

## ----------------
19. 次の実行結果を得たい場合に、コードの【A】に入るものとして正しいものはどれか。
[実行結果]
[5, 25, 125]

[コード]
matrix = 【A】
power = [row[2] for row in matrix]
print(power)
Correct Answer: [[2, 3, 5], [4, 9, 25], [8, 27, 125]]

★row[2]を並べるので、３番目が5,25,125の２次元配列を探す

## ----------------★
3-19. コードAの1行目を代替するコードBがある。コードBの【A】～【C】のうち、【A】と【B】に入るものとして
      正しいものはどれか。

[ コードA ]
cubes = [ a ** 3 for a in range(5)]
print(cubes)

[ コードB ]
cubes = 【A】(【B】(【C】 a: a ** 3, range(5)))

  a) 【A】set　【B】loop
  b) 【A】dic　【B】loop
  c) 【A】dic　【B】map
  d) 【A】list　【B】loop
  e) 【A】list　【B】map

★ result = map(function, sequence) 指定した関数をシーケンスの全ての要素に適用し、結果を返す

    cubes = list(map(lambda a: a ** 3, range(5)))

## ----------------
3-21. 次のような結果を得たい場合に、コードの2行目（★印の行）を代替するものとして正しいものはどれか。

[ 実行結果 ]
[(1, 4, 7), (2, 5, 8), (3, 6, 9)]

[コード]
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
power = [tuple(row[i] for row in matrix) for i in range(3)] …★

print(power)

  a) power = zip[*matrix]
  b) power = zip(*matrix)
  c) power = zip(list(matrix))
  d) power = list(zip(*matrix))
  e) power = list(zip(matrix))

★matrixの各リストをzip関数にアンパックしてzipに渡し、行列の転置を行う
  zip関数の結果はイテレータなので、直接リストに変換する必要がある

## ----------------
23. 
データ構造に関する次の記述のうち誤っているものはどれか。

  a) タプルは変更不能（immutable）、リストと集合は変更可能（mutable）である。
  b) ディクショナリは変更不能（immutable）であるがキーの型は変更可能（mutable）であり、
     その値は一意でなければならない。
   → ★変更不能なのはタプル
  c) ディクショナリは、全要素が「キー」と「値」のペアであるという点で、リストやタプルと大きく異なる。
  d) 集合には、「順序を持たない」「同一の値の要素を重複して持つことができない」などの特徴がある。
  e) リスト、タプル、集合、ディクショナリには、反復可能（iterable）であるという共通点がある
## ----------------
24. 次のうち対話モードで入力したときに「True」が返されるのはどれか。
24
次のうち対話モードで入力したときに「True」が返されるのはどれか。
  a) (1, 2, 3, 4) > (1, 2, 5)
●b) 'PHP' < 'Perl' < 'Python'
  c) (1, 2) > (1, 2, -1)
  d) (10, 20) != (10.0, 20.0)
  e) (1, 2, ('bb', 'a')) > (1, 2, ('bcd', 'b'))

★文字列は文字単位で先頭から順に比較、大文字＜小文字 H<e<y で決まる
  リストも、要素を先頭から順に比較 
  要素が尽きたら、要素が多いほうが大きい判断

## ----------------
25. モジュールに関する次の記述のうち、誤っているものはどれか。
Correct Answer: あるモジュールがインポートされるときにインタープリタが検索する順序は、
★まずビルトインモジュール、
次にsys.path変数で得られるディレクトリ、
（スクリプトを実行しているディレクトリ、Pythonの標準ライブラリのディレクトリ、
  サイトパッケージのディレクトリ、および環境変数PYTHONPATHで指定されたディレクトリ）
最後にシンボリックリンクを置いてあるディレクトリである。

## ----------------
3-25. モジュールに関する次の記述のうち、正しいものはどれか。

  a) sys.pathが初期化されている場所は、PYTHONPATHとインストールごとのデフォルトであり、
     入力スクリプトのあるディレクトリは含まれない。
	★入力スクリプトのあるディレクトリも含まれる(先頭)
  b) あるモジュールがインポートされるときにインタープリタが検索する順序は、
     まずビルトインモジュール、次にsys.path変数で得られるディレクトリ、そしてシンボリックリンクを
     置いてあるディレクトリである。
	
  c) モジュール読み込みの高速化のため、Pythonはコンパイル済みのモジュールを「__python_cache__」
     ディレクトリにmodule.バージョン名.pyの名前でキャッシュする。
    	★__pycache__
  d) モジュールの中では、グローバル変数「__modname__」の値としてモジュール名（文字列）がセットされている。
	★モジュール名は __name__
  e) 実行中のスクリプトのあるディレクトリは、検索パスの最初、標準ライブラリのパスよりも前方に置かれる。
	★実行中のスクリプトがあるディレクトリは、Pythonのモジュール検索パス（sys.path）の最初に追加
	  標準ライブラリのパスよりも前方

## ----------------
import math
print('{1:.3f}, {0:.5f}'.format(math.pi, math.e))
Correct Answer: 2.718, 3.14159
★引っ掛け、順番指定が逆順に注意

## ----------------
29. エラーと例外に関する次の記述のうち誤っているものはどれか。
Answer Provided:
Pythonのエラーには２つの種類がある。構文エラーと例外である。構文エラーはパース上のエラーとも呼ばれる。

Correct Answer: パーサ（構文解釈器）は違反のある行を表示し、最後にエラーが検知された点を小さな矢印で示す。
エラーは矢印より後のトークンが原因である。
★通常、エラーは矢印より後ではなく前にある

## ----------------
35. 次の正規表現を用いたコードの【A】の部分に入れたときエラーとなるものはどれか。

import re
prog = re.compile('(K|S)us(a|u)n(a|o)(o|m)?g?i?(saya)?', re.IGNORECASE)
【A】
print(ret[0])
Answer Provided:
ret = prog.search('KUSANAGI')

Correct Answer: ret = prog.search('Kusaneiro')

★(o|m)?: 次にo
またはmが0回または1回出現します。?は前の文字が0回または1回出現することを意味します。
なので、'KUSANAGI'は、(o|m)?をスキップして次のg?i?でマッチする

## ----------------
37. 今日の日付を得たい場合、次のコード1行目の【A】に入る適切なものはどれか。

【A】
now = date.today()
print(now)
Answer Provided:
?import date

Correct Answer: from datetime import date
★モジュール名はdateime、関数はdate

## ----------------
39. 仮想環境とパッケージに関する次の記述のうち誤っているものはどれか。
Answer Provided:

Correct Answer: pip uninstall にパッケージ名を指定すると、その仮想環境からパッケージを削除できる。削除対象となるパッケージの複数指定はできない。
★ 複数指定が可能
   pip freeze は 今の環境を再現するための情報を出力する。一覧という意味ではlistと同じ
   これを保存して、別の環境で pip install -r *.txt を実行することで環境を再現することができる

## ----------------
その他
  ★リスト変数の真偽判定は、空ならFalse、中身があればTrue
  ★ 3 * "y" は "yyy"となる
  ★for文、else
  ★
## ----------------
## ----------------
## ----------------
## ----------------
## ----------------





25
モジュールに関する次の記述のうち、誤っているものはどれか。

モジュールとは、Pythonの定義や文が入ったファイルである。そのファイル名は、モジュール名に接尾辞「.py」を付けたものである。

あるモジュールがインポートされるときにインタープリタが検索する順序は、まずビルトインモジュール、次にsys.path変数で得られるディレクトリ、最後にシンボリックリンクを置いてあるディレクトリである。

sys.pathが初期化されている場所は、入力スクリプトのあるディレクトリ、PYTHONPATH、インストールごとのデフォルトである。

モジュール読み込みの高速化のため、Pythonはコンパイル済みのモジュールを「__pycache__」ディレクトリに、例えば「module.バージョン名.pyc」のような名前でキャッシュする。

Pythonには標準モジュールのライブラリが付属する。


26. 
モジュールが定義している名前を対話モードで確認したい。次のスクリプトの２行目【A】に入るものとして正しいものはどれか。

import sys
【A】


mod(systems)

mod(sys)

mod()

dir(mod)

dir(sys)

29. 
エラーと例外に関する次の記述のうち誤っているものはどれか。


Pythonのエラーには２つの種類がある。構文エラーと例外である。構文エラーはパース上のエラーとも呼ばれる。

文や式が構文的に正しくても、実行しようとするときにエラーが生じることがある。実行中に検知されるエラーは例外と呼ばれ、これは必ずしも致命的なものではない。

例外のほとんどはプログラムでは処理されず、その結果はエラーメッセージに現れる。エラーメッセージの最終行には、NameError、TypeErrorなど例外の型が記されている。

[Ctrl]+[C]キーなどでユーザーがプログラムに割り込みをかけると、KeyboardInterrupt例外が送出される。

パーサ（構文解釈器）は違反のある行を表示し、最後にエラーが検知された点を小さな矢印で示す。エラーは矢印より後のトークンが原因である。

32. 
クラスに関する次の記述のうち、誤っているものはどれか。


名前空間とは、名前とオブジェクトの対応付け（マッピング）のことである。名前空間で重要なのは、異なる名前空間同志の名前には一切の関わりがないということである。

関数のローカル名前空間は関数がコールされたときに作られ、関数から戻ったり関数内で処理されない例外を送出したりしたとき削除される。

スコープとは、ある名前空間から直接アクセスできる、プログラムテキスト上の範囲のことである。

クラスに__init__()メソッドが定義してあると、新規生成されたインスタンスに対して自動的に__init__()メソッドがコールされる。ただし__init__()メソッドに引数を与えることはできない。

クラスオブジェクトは２種類の操作をサポートする。属性参照とインスタンス化である。クラスのインスタンス化には関数の表記法が使われる。


36. 
statisticsモジュールを使って、データの平均、中央値、分散を求めたい。次のコードの【A】【B】【C】に入りうる組み合わせとして正しいものはどれか。

import statistics
data = [1,10,15,20,25,30,35]
rslt1 = statistics.【A】(data)
rslt2 = statistics.【B】(data)
rslt3 = statistics.【C】(data)
print(rslt1, rslt2, rslt3)


mean median variance

mean center scatter

average middle variance

balance median scatter

average median variance

38. 
loggingモジュールのメッセージの優先度として正しいものはどれか。左から順に優先度が高いものとする。


ERROR、CRITICAL、WARNING、INFO、DEBUG

ERROR、CRITICAL、WARNING、DEBUG、INFO

CRITICAL、ERROR、WARNING、DEBUG、INFO

CRITICAL、ERROR、WARNING、INFO、DEBUG

CRITICAL、WARNING、ERROR、INFO、DEBUG

39. 
仮想環境とパッケージに関する次の記述のうち誤っているものはどれか。


Pythonの仮想環境とは、特定バージョンのPythonのインストール実体を含む、独立に機能するディレクトリツリーおよびパッケージなどから成り立つものである。

仮想環境をアクティベートしたら、pipを使ってパッケージのインストール、アップグレード、リムーブができる。pipはデフォルトではPython Package Indexからパッケージをインストールする。

pip install --upgrade とすることで当該パッケージを最新バージョンにアップグレードすることができる。

pip uninstall にパッケージ名を指定すると、その仮想環境からパッケージを削除できる。削除対象となるパッケージの複数指定はできない。

pip listはその仮想環境にインストールされたすべてのパッケージを表示する。pip freezeも同様の働きをするが、出力形式が異なる。


## ----------------  ★★★★★★
1. Pythonの特徴に関する次の記述のうち、誤っているものはどれか。

   a) Pythonは柔軟な配列や集合、ディクショナリといった、非常に高水準のデータ型を組み込みで持つ。
      データ型の一般性が高いためPythonの対応可能な問題領域はAwkより広いが、Perlと比べると同程度である。
	★Perlよりも高水準
   b）Pythonは簡単に使えるとはいえ本格的なプログラム言語であり、大きなプログラムを書くために提供された
      構造やサポート、エラーチェック機構が、シェルスクリプトなどに比べはるかに多く存在する。
   c) PythonはWindows、MacOS、Linuxなど多くの環境で動作する、拡張可能なフリーのオープンソースソフトウェア
      である。
   d) Pythonでは、文のグルーピングはカッコで囲うことでなくインデントで行われるなど、プログラムを小さく
      読みやすく書けるという特徴がある。
   e) Pythonはインタープリタ言語であり、コンパイル等が必要でないため、プログラム開発における時間を節約してくれる。       インタープリタは対話的に使うことも可能である。
	★バイトコンパイルが行われるが、ここでは無視される

## ----------------  ★★★★★★
2. Pythonインタープリタに関する次の記述のうち、誤っているものはどれか。

  a) 標準入力がttyデバイスに接続された状態で起動した場合は、コマンドを対話的に読み込んで実行するが、
     引数にファイル名を与えたり、標準入力からファイルを与えて起動した場合は、このファイルに入った
     「スクリプト」を読み込んで実行する。
  b) インタープリタがスクリプト名（スクリプトのファイル名）と続く引数群を知らされると、
     これらは文字列のリストとなる。import listitems を実行することで、このリストにアクセスできる。
	★ インタープリタがスクリプト名と引数群を受け取ると、これらはsys.argvリストに保存されます。
  c) デフォルトの設定では、プライマリプロンプトの記号は「>>>」、セカンダリプロンプトの記号は「…」である。
  d) インタープリタを対話モードで起動すると、はじめにバージョンと著作権からはじまるメッセージが表示され、
     その後にプライマリプロンプトが表示される。
	★バージョンと著作権
  e) プログラムの冒頭で「# coding: （エンコーディング方式）」のようにすると、デフォルト以外の
     エンコーディングを使うことも可能である。
	★# coding: コーディング方式


## ----------------  ★★★★★★
3. 数値に関する次の記述のうち、正しいものはどれか。

  a) 演算を行うための「 + 」や「 - 」などの記号はオペランドと呼ばれ、演算の対象は演算子と呼ばれる。
	★オペランドは値、「 + 」や「 - 」は演算子
  b) 切り下げ除算を行って整数解を得たい場合（剰余を捨てたい場合）は「 / 」を使い、
     剰余のみ得たい場合は「 // 」を使う。
	★除算の整数解を得るには、演算子//を使う
  c) 変数は、定義（値の代入）や宣言がなされないまま使おうとするとエラーとなる。
	★使う前に値の代入が必要
  d) 整数はintという型を持つ。小数点を伴う数はfloatという型を持つ。除算は常にfloatを返す。
	★除算結果は常にfloat
  e) 対話モードでは、最後に表示した式を変数「**」（アスタリスク2つ）に代入してある。
	★最後に表示した式は変数「_」

## ---------------- ★★★★★★
7. 次の変数Zenに関して指定した場合、実行時にエラーとならないものはどれか。

Zen = 'BeautifulIsBetterThanUgly'

  a) Zen[1000:10000]
	スライスは範囲を超えてもOK
  b) Zen[50]
	添字は範囲を超えたらだめ
  c) Zen[10] = 'a'
	文字列の添字アクセスはイミュータブルで変更不可
  d) Zen['B']
	インデックスは整数値のみ
  e) Zen[1:10] + b
	スライスした文字列に変数bを加算、bが数値ならエラーになる
## ----------------
25. モジュールに関する次の記述のうち、誤っているものはどれか。

  a) パッケージとは、「ドット区切モジュール名」を使って、Pythonのモジュールを構築する方法である。
	★ドット区切モジュール名
  b) あるモジュールがインポートされるときにインタープリタが検索する順序は、
     まずビルトインモジュール、次にsys.path変数で得られるディレクトリである。
     シンボリックリンクを置いてあるディレクトリはモジュール検索パスに入らない。
	★検索パスは、ビルトインモジュール、次にsys.path変数ディレクトリ、
	  シンボリックリンクを置いてあるディレクトリ
  c) sys.pathが初期化されている場所は、入力スクリプトのあるディレクトリ、PYTHONPATHであり、
     インストールごとのデフォルトは含まれない。
	★ sys.pathは、入力スクリプトのあるディレクトリ、PYTHONPATH環境変数で指定されたディレクトリ、
	   インストールごとのデフォルト（標準ライブラリディレクトリなど）を含む
  d) Pythonはソースファイルの最終更新日時をコンパイル済みのバージョンと比較し、再コンパイルが必要か判断する。
     これは完全に自動的に行われる。
	★コンパイルは自動で行われる
  e) コンパイル済みのモジュールはプラットフォーム非依存なので、ひとつのライブラリを
     異なるアーキテクチャのシステム間で共有できる。
	★コンパイル済みのモジュールは異なるアーキテクチャのシステム間で共有できる

## ----------------
29. エラーと例外に関する次の記述のうち誤っているものはどれか。

  a) raise文を用いることで、指定の例外を意図的に発生させることができる。
     raiseの引数は送出する例外を示すものであり、例外インスタンスでも、Exceptionクラスの派生クラスである
     クラス（例外クラス）でも構わない。
	★raiseの引数は、例外インスタンスまたは例外クラス
  b) 発生した例外に値が付随することもあり、これを例外の引数と呼ぶ。except 節では、例外名の後に変数を
     指定することができる。この変数は例外インスタンスに結び付けられており、instance.args に例外インスタンス
     生成時の引数が格納される。
	★例外の引数は instance.args に格納
  c) [Ctrl]+[C]キーなどでユーザーがプログラムに割り込みをかけると、KeyError例外が送出される。
	★ [Ctrl]+[C]キーを押してプログラムに割り込みをかけると、KeyboardInterrupt例外が送出
  d) パーサ（構文解釈器）は違反のある行を表示し、最初にエラーが検知された点を小さな矢印で示す。
     エラーは矢印より前のトークンが原因である。
	★エラーは矢印より前
  e) 例外のほとんどはプログラムでは処理されず、その結果はエラーメッセージにあらわれる。
     エラーメッセージの最終行には、NameError、TypeErrorなど例外の型が記されている。
	★プログラムで補足しなくても、エラーメッセージで表示される

## ---------------- ★
39. 仮想環境とパッケージに関する次の記述のうち誤っているものはどれか。

  a) pip install でパッケージ名を指定し、そのパッケージ名の後ろに==とバージョン名を付けると、
     そのバージョンのパッケージをインストールできる。
	★pip install パッケージ名==バージョン
  b) pip install --upgradeとすることで、当該パッケージを最新バージョンにアップグレードすることができる。
	★pip install --upgrade パッケージ名
  c) 「pip list パッケージ名」で、ある特定のパッケージの詳細情報が表示される。
	★詳細表示は pip show パッケージ名
  d) pip uninstall にパッケージ名を指定すると、その仮想環境からパッケージを削除できる。
     削除対象となるパッケージの複数指定も可能である。
	★pip uninstall パッケージ名
  e) pip freezeはその仮想環境にインストールされたすべてのパッケージを、pip install向けの形式で出力する。
	★pip freeze の出力を保存して pip install の引数で指定して、環境を再現

## ----------------
3-39. 仮想環境とパッケージに関する次の記述のうち正しいものはどれか。

  a) pip install でパッケージ名を指定し、そのパッケージ名の後ろに「=」とバージョン名を付けると、
     そのバージョンのパッケージをインストールできる。
	★=ではなく==を使用する。
  b) 「pip upgrade パッケージ名」とすることで、当該パッケージを最新バージョンにアップグレードすることができる。
	★pip install --upgrade パッケージ名
  c) pip freezeはその仮想環境にインストールされたすべてのパッケージを表示する。
     pip listも同様の働きをするが、両者は出力形式が異なる。pip listはその仮想環境にインストールされた
     すべてのパッケージを、pip install向けの形式で出力する。
	★pip freeze 出力を pip install で利用できる
  d) pip uninstall にパッケージ名を指定すると、その仮想環境からパッケージを削除できる。
     削除対象となるパッケージの複数指定はできない。
	★複数指定できる
  e) 仮想環境を作成、管理するのに使われるスクリプトはpyvenvである。
	★これが正解だが非推奨、今は python3 -m venv <folder>

## ---------------- ★★★★★★★
1-40. 次の記述に関して誤っているものはどれか。

  a) 変数とモジュールの補完はインタープリタの起動時に自動で有効になっている。
  b) [Tab]キーを押すと補完機能が呼び出せる。
     この機能はPythonの文（命令）の名前、現在のローカル変数、使用できるモジュール名を検索するものである。
  c) デフォルト設定ではユーザーディレクトリの「.pyhistory」ファイルにヒストリが保存される。ヒストリは対話型インタープリタセッションで利用できる。

拡張された対話型インタープリタとしてbpythonがある。これはタブ補完、オブジェクト探索、高度なヒストリ管理などの機能を持つ。

bpythonに類似した拡張対話環境にIPythonがある。IPythonは「pip install ipython」でインストールでき、IPythonの対話モードはipythonコマンドで起動できる。


2- 40. 次の記述に関して誤っているものはどれか。

  a) デフォルト設定ではユーザーディレクトリの「.python_history」ファイルにヒストリが保存される。
     ヒストリは対話型インタープリタセッションで利用できる。
	★ヒストリはデフォルトでオン .python_history に保存
  b) [Tab]キーを押すと補完機能が呼び出せる。
     この機能はPythonの文（命令）の名前、現在のローカル変数、使用できるモジュール名を検索するものである。
  c) 拡張された対話型インタープリタとしてbpythonがある。これはタブ補完、オブジェクト探索、
     高度なヒストリ管理などの機能を持つ。
	★bpythonは拡張版
  d) bpythonに類似した拡張対話環境にIPythonがある。
     IPythonは「pip install ipython」でインストールでき、IPythonの対話モードはipythonコマンドで起動できる。
	★bpythonは強化拡張版、pip install でインストールできる
  e) 変数とモジュールの補完機能は、インタープリタの起動時には有効になっていないため設定が必要である。
	★補完機能は常にオン

## ----------------
3-40. 次の記述に関して正しいものはどれか。

  a) デフォルト設定ではユーザーディレクトリの「.pyhistory」ファイルにヒストリが保存される。
     ヒストリは対話型インタープリタセッションで利用できる。
	★.python_history
  b) [Ctrl]+[t]キーを押すと補完機能が呼び出せる。この機能はPythonの文（命令）の名前、
     現在のローカル変数、使用できるモジュール名を検索するものである。
	★[Tab]キー
  c) 拡張された対話型インタープリタとしてBythonがある。これはオブジェクト探索、高度なヒストリ管理などの機能を持つ
	★bpython ならある
  d) IPythonは「pip install ipython」でインストールできる。IPythonの対話モードはipythonコマンドで起動できる。
     終了時はdeactivateコマンドを実行すればよい。
	★deactivateは仮想環境を終了するコマンド
  e) 変数とモジュールの補完機能は、インタープリタの起動時に自動で有効になっている。
	★自動的に有効になる

