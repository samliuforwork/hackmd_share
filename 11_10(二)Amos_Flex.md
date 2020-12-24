# 11/10(二)Amos_Flex
###### tags: `amos`

#### 課程規劃
* 今明天講HTML、CSS基礎切版
* 三天 講RWD+Bootstraps

## 額外觀念指令

* dir=rtl (direction = right to left)，html裡語言而非CSS
* 如何讓文字直排
https://developer.mozilla.org/zh-CN/docs/Web/CSS/writing-mode



## Flex
### 主軸
display:flex
* flex-flow:方向跟折行的縮寫，裡面包含flex-wrap與flex-direction
* flex-wrap:可以設定當元素超出容器時該怎麼顯示，控制換列以及交叉軸的方向
* flex-direction:控制方向，預設為語言的方向(通常華文為語言由左至右時，於是我們常看到的就是左至右)，但可以控制資料(主軸)的方向。 row-reverse; column-reverse
![](https://i.imgur.com/33qM8AK.png)

            display: flex;
            flex-direction: column
            其實這樣跟一開始一樣..........，不必要這樣弄
* main-axis    主軸：指的是資料的方向
* cross-axis   交叉軸：垂直於主軸

justify-content:指定主軸的對齊與分布，flex-end對齊主軸的終點位置。

1. space-around剩餘的空間分配給子項目的左右兩側，每個子項目所分配到的左右兩邊空間大小皆相同。

                .item1, .item2, .item3{
                    margin-left: auto;
                    margin-right:auto;
                }

                上下兩個code等同

                justify-content: space-around;

2. space-evenly則是剩餘的空間分配，使得每子項目間隔平均
```
            .item2{
                margin-left: auto;
                margin-right:auto;
            }
            
            上下兩個code等同
            
            justify-content: space-between;
```
3. space-between為貼齊父層邊緣，並平分剩餘空間

### 當考慮了多列畫面
使畫面分割成多個列的情況

* align-items:控制子物件在彈性列row之中的交叉軸位置
圖中示範align-items:end
![](https://i.imgur.com/jYyfw47.png)
* align-self:假如我們已經在父元素上設定 align-item，但要其中一個內容物的位置需要調整成其他對齊方式，這時我們就可以針對該元素設定 align-self 來覆寫原本 align-item 的屬性。
* align-content:控制彈性列的位置

### 13:44

### 調整子層的順序
order:只要比0大，就會往終點方向移動；比0小則往起點移動，當多個子項目的順序時需要比較order值大小(order:3 > order:2 > order:1)


* flex-basis:基本值，所控制的是物件主軸的長度，控制主軸上，優先權會蓋過寬與高
* flex-shrik:收縮值，當超出父層時會自己萎縮，大多用到0,1
* flex-grow:伸展值，剩餘空間分配給主軸的長度

* vertical-align:只對inline物件有作用，包括inline-block，可以解決inline對齊baseline而有小空白的問題。
![](https://i.imgur.com/4kcwZuQ.png)

![](https://i.imgur.com/GuegZKJ.png)

 

