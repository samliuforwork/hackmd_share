# 11/02(一)Ruby-Block
###### tags: `龍哥`

Ruby的block無法單獨存在，必須依附在某段程式後面，可以放任何數量的程式碼
通常用於開發套件或好用的函式，不是參數
(註：但JS的block可以單獨存在)

Ruby的Block呈現方式為：do end以及{}
Block的執行與否，需看依附的宿主

yield = 將控制權轉讓給block，並且可以把數個值、程式順道讓出來，通常以｜ｘ｜去接值；另一方面，Block在完成執行後也會回傳最後一行執行的結果。


p比puts還多資訊，nil也會顯示，p會有回傳值pus沒有

y(a) , y(1)定義方法時，由我們所定義的a為參數，而回傳至參數內的1為引數

$-全域變數符號

# 11:56am

map-對陣列每個參數的做運算
select-根據回傳的值，回傳符合條件相應的結果

def hello
    p yield
end

hello{
    return 2
}

若在上面的例子中，多加入了return則會將控制權交還給hello，並且繼續往下走，因此最後得出什麼都沒有的結果，通常用在規格設定上，若規格不符合根本不用往下看code。

keyword argument:這麼做的方法是可以不用記憶參數的名稱順序
def xyz(a: , b:, c:)
    p a, b, c
end

xyz(c: 3, a: 100, b: 2)

# 13:53

{}與do end的差別
結合率：{}　＞ do end

## Block無法單獨存在，但物件化之後就可以單獨存在
call是實體方法
Proc是一種class
Pro.new 後面接Block並且將其物化
Pro.new 沒有小括號()

## Lambda
Lambda會做出一Proc
Proc(像是Block)不會在意引數數量多寡，Lambda(像方法)如果引數數量不對則會出錯誤

# 15:29
a, b = 1, 2, 3, 4 (只會顯示a=1, b=2)
a, *b = 1, 2, 3, 4

* - 多個元素收成一個陣列
** - 後面的hash收起來

link_to介紹
https://apidock.com/rails/ActionView/Helpers/UrlHelper/link_to

# 物件導向
透過容易理解的方式將程式碼放置於適當的地方

Class Cat 預設已經繼承了Object這個Class
.class 找出是哪個class生的
.superclass 找出上層類別

kitty → cat → animal → object → basicobject

### Modual
做好的模組，可以加裝在想加的class上
![](https://i.imgur.com/4K7FdRf.png)
所有的方塊都是Class

.ancestors 印出方法搜尋路徑

### Modual與Class的差別 
1. Module不能new出新的實體
2. Module無法繼承

A = Modual.new{

}

看右圖，右上那個是一個名為Modual的Class，由他所生出的modual是符合藍色差別的。( 1. Module不能new出新的實體2. Module無法繼承)

