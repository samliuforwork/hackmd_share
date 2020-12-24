# 10/30(五)Git remote & Ruby
###### tags: `龍哥`

### git clone url
指的是我要clone那個網址的東西，並且把歷史紀錄抓下來
會幫你做的事情如下：
1. 下載 ...(歷史紀錄)
2. git remote add origin xxxx 設定遠端節點　，可以用git remote -v來檢查

### fetch
捏、夾的意思
git fetch origin master
去遠端master抓最新的commit抓回來(並且更新master進度)
git merge origin master

### pull = fetch + merge

14:19

術語devise熟悉

Ruby
特點：運作速度很慢(twitter)、當看到紅寶石代表Ruby特有
    習慣的空格為兩個！
    
15:15 解講Rack

rackup
touch config.ru
rackup

# block
run Proc.new {
    [
        200,
        {"Content-Type" => "text/html"},
        ["hello rack7777777777777"]
    ]
}
### 狀態、Header、Body

HTTP狀態碼
https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81

網頁讀取方法有二
Get：輸入網址，進入網頁
Post:藉由表單

# block
run Proc.new {
    [
        200,
        {"Content-Type" => "text/html"},
        ["hello rack7777777777777"]
    ]
}
#PORT

class Cat
    def call(env)
    [
        200,
        {"Content-Type" => 'text/html'},
        ["Hello kitty #{env}"]
    ]
    end
end

kitty = Cat.new
run(kitty)

# call

use Rack::Auth::Basic do |username, password|
    username =="5xruby" && password == "my_password"
end

run Proc.new{
    [200, {"Content-Type"="text/html"}, ["hello, Rack!"]]
}