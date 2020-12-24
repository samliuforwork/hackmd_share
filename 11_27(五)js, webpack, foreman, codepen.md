# 11/27(五)js, webpack, foreman, codepen
###### tags: `龍哥`

#### 題目發想
* 題目主要專注在活力展示，而不是創業解決產業痛點。

### JS
https://medium.com/@brianwu291/javascript%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-understanding-javascript-the-weird-part-1-execution-context-lexical-environment-55aebb71222d
#### 執行環境(runtime)
1. Browser，全域變數為window
2. node，全域變數為global

#### Stack
##### Stack overflow
> // execution context = EC
> var count = 0
> function hello(x) {
>   count += 1;
>   console.log(count)
>   hello()
> }
> hello(123);


#### 執行一個function時，會有execution content(EC)產生


#### 監聽器
```
btn.addEventListener("click", function(evt) {
  evt.preventDefault();
  //alert('hi');
})
```
* 按下去預設往某個地方走，因此下evt.preventDefault()使其不會執行預設行為

12:30

#### scope chain
* 當在找範圍，會一層一層的找
* ![](https://i.imgur.com/1Z9XmDs.png)

##### 下面兩大function的差異性，一個是變數(會有變數提昇問題)
1. > var a = function() {```

>   console.log(123)
> }
> 
2. > function b() {
>   console.log(123)
> }


### Ruby

#### 為什麼要使用webpack
* 以前若要使用前端套件，需要善心人士包好bootstrap這些，在去rubygem找下載貼在gemfile用。(rails 4, 5 常常這麼做)
* 安裝npm套件，npm install
* ![](https://i.imgur.com/DD9CkCR.png)

#### bin/webpack-dev-server
* Nodejs寫的，跑js會比rails還快
* 但是開兩個伺服器很麻煩
* ![](https://i.imgur.com/8kqe2UX.png)
1. RWX　　　　RWX　　RWX
2. ↑user(自己)　↑Group　↑others
3. 用二進位來看，2^2+2^1+2^0=7， 0^2+2^1+2^0=3，2^2+0^1+2^0 = 5
4. R = read, W = write, X = Execute
5. 若沒有看到三個x，則三個加x chmod +x ./aaaa
6. chmod 444(777) ./tt.rb

#### webpack是一個效能很好的打包器
* 可以把stylesheet裡面的檔案(除了打包檔)都包到JavaScript裡面的styles(自己新增的)
* ![](https://i.imgur.com/uVUInQi.png)
* 全部都交給webpack來管，這樣做對其來說
* ![](https://i.imgur.com/5wmmLmp.png)
* 改成pack是避免推上去後不見
* ![](https://i.imgur.com/cGjYu2G.png)
* 可以把JavaScript改名成Frontend，然後記得去上圖的路徑改名稱



#### 安裝foreman，以避免要開兩個伺服器
* 記得建立空白的Procfile
* foreman start(foreman s)
* ![](https://i.imgur.com/PuEpnmN.png)

* web123: bin/rails server
* webpack444: bin/webpack-dev-server


#### Tree shaking
* ![](https://i.imgur.com/jq0MFq8.png)
