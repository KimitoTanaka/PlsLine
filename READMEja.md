# plsline

![Python 3.8|3.9|3.10|3.11|3.12](https://img.shields.io/badge/python-3.8%7C3.9%7C3.10%7C3.11%7C3.12-blue?style=flat-square)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)<br><br>
**PlsLineはprintしたファイル・何行目に書いてあるかの位置・関数名・関数のtypeが追加でわかるPythonライブラリです。**

```python
--directory\file_name.py-line_number---type------var_name----------------------var
```


## 使用上の注意
printの中身を出力しますが、contentsは3つまでとなります。それ以上にするとエラーになります。複数回に分割して出力してください、ご了承ください。<br>
type等の取得は先頭1つだけを対象にしています。

```python
from plsline import printsimple as prints
#plslineでも出来ます
prints("one")
prints("one","two")
prints("one","two","three")

#printでは出来ますが同じことをplslineでやったらエラーになります
prints("one","two","three", "four")　　#error

#二つに分けてください
prints("one","two","three")
prints("four")
```

## 互換性

plslineはWindowsでしか動作確認をしていません。<br>
古いターミナルでcolorは正常に動作はしません、その場合はplssimpleかplsmonochromeをご使用ください。<br>
日本語の環境でしか動作の確認をしていません、var_name等の取得はencoding='utf-8'
使用しています。<br>
plslineを使用するにはPythonのバージョンは3.8以降が必要です。<br>

## Requirements
標準ライブラリーだけを使用しています。

```python
#使用しているimport一覧
from inspect import (
                    currentframe, 
                    getfile,
                    )
import re
import os
from time import sleep

```


<br>


# インストール方法
```
python -m pip install plsline
```
<br>

以下のコマンドを実行すると、ターミナルでplslineの出力をテストできます。




```
python -m plsline
```


# 使用法
printsimpleの使用例
<br>
simpleはファイル検索をしません、行とtypeを出力します、





```python
##importしてprintsimpleが使えるようにします[as] の後に好きな名前に変更できます、今回はsinpleなのでprintsにしています
from plsline import printsimple as prints


##値段の設定
view_material = True
price_apple = 500
prints(price_apple,view_print=view_material)

price_orange = 600
prints(price_orange,view_print=view_material) 


#合計値段を計算
buy = price_apple + price_orange

#確認のprint
prints(buy)


```
```python
#出力の結果
--0008---int--500
--0011---int--600
--0018---int--1100

```

8,11,18行目にあるのを示しています、




```python
##importしてprintcolorが使えるようにします[as] の後に好きな名前に変更できます、今回はcolorなのでprintcにしています
from plsline import printcolor as printc


##値段の設定
view_material = True
price_apple = 500
printc(price_apple,view_print=view_material)

price_orange = 600
printc(price_orange,view_print=view_material) 


#合計値段を計算
buy = price_apple + price_orange

#確認のprint
printc(buy,color="red")



```



```python

#{directory} {file_name} {type} {line_number} {var_name} {var}
#出力の結果
--admake\printcolor.py-0008---int------price_apple----------------------500
--admake\printcolor.py-0011---int------price_orange---------------------600
--admake\printcolor.py-0018---int------buy------------------------------1100

```







#### 引数一覧
|引数名|型|デフォルト値|内容|
|---|---|---|---|
|print_normal_content|-||printの一つ目の中身です|
|print_normal_content_sub|-||printの二つ目の中身です|
|print_normal_content_three|-||printの三つ目の中身です|
|view_print |bool|True|Trueの場合printします|
|line_fast_int|int|2|先頭に-を入れて通常のprintと見分けがつきやすいようにしています|
|line_end_int|int|0|最後に-を入れて目立たせることができます|
|line_int|int|3|ファイル名の後の-の数です|
|max_file_int|int|20|フォルダーとファイル名の最大文字数を設定します、|
|max_var_name_int|int|30|変数名の最大文字数を設定します|
|max_type_int|int|9|typeの最大文字数設定をします|
|sleep_time|int|0|出力したときに一時停止する時間を設定します、単位は秒数です|



#### color用引数 使用は名前か略称をお使いください
|名前|略称名|デフォルト値|内容|
|---|---|---|---|
|color|str|"white"|文字の色を変えます、対応一覧は下に別で書きました。|
|color_back|str|"black"|文字の背景の色を変えます、対応一覧は下に別で書きました。|
|colorreset|str|"\033[0m"|色をリセットします|
|help|bool|False|Tureにしてcontentsが空の場合対応色一覧を出力します printc(help=Ture)|


| 名前      | 略称 | 値         | 内容サンプル |
|--------|----|------------|--------------|
| black     | b    | "\033[30m" | <span style="color:black">black</span> |
| red       | r    | "\033[31m" | <span style="color:red">red</span> |
| green     | g    | "\033[32m" | <span style="color:green">green</span> |
| yellow    | y    | "\033[33m" | <span style="color:gold">yellow</span> |
| blue      | bl   | "\033[34m" | <span style="color:blue">blue</span> |
| magenta   | m    | "\033[35m" | <span style="color:magenta">magenta</span> |
| cyan      | c    | "\033[36m" | <span style="color:cyan">cyan</span> |
| white     | w    | "\033[37m" | <span style="color:gray;background-color:white">white</span> |
| reset     | r    | "\033[0m"  | <span style="color:inherit">reset</span> |

<br>


| 名前 (背景) | 略称 | 値         | 内容サンプル |
|-------------|------|------------|--------------|
| black_bg    | bb   | "\033[40m" | <span style="background-color:black;color:white"> black background </span> |
| red_bg      | rb   | "\033[41m" | <span style="background-color:red;color:white"> red background </span> |
| green_bg    | gb   | "\033[42m" | <span style="background-color:green;color:black"> green background </span> |
| yellow_bg   | yb   | "\033[43m" | <span style="background-color:gold;color:black"> yellow background </span> |
| blue_bg     | blb  | "\033[44m" | <span style="background-color:blue;color:white"> blue background </span> |
| magenta_bg  | mb   | "\033[45m" | <span style="background-color:magenta;color:white"> magenta background </span> |
| cyan_bg     | cb   | "\033[46m" | <span style="background-color:cyan;color:black"> cyan background </span> |
| white_bg    | wb   | "\033[47m" | <span style="background-color:white;color:black"> white background </span> |
| reset       | r    | "\033[0m"  | <span style="color:inherit;background-color:inherit">reset</span> |
<br>


## ライセンス MIT
商用利用が完全に認められて
ソースコードの複製、変更、頒布が可能です、
ソースコードの公開義務もありません、好きに使ってください。<br>
詳しくは別冊のLICENSEに書いてあるので見てください。


