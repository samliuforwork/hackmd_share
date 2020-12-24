# 12/19(六)linepay串接
###### tags: `龍哥`

### 步驟
1. linepay development
2. 使用postman，打出網站的request
3. 訂單model產生訂單編號，記得掛在 before_create (order.rb)
```
  private
  def generate_order_num
    self.num = SecureRandom.hex(5) unless num
  end
```
4. 安裝faraday套件
5. order_controller，以faraday用post方法打過去
```

    if @order.save
      resp = Faraday.post("#{ENV['line_pay_endpoint']}/v2/payments/request") do |req|
        req.headers['Content-Type'] = 'application/json'
        req.headers['X-LINE-ChannelId'] = ENV['line_pay_channel_id']
        req.headers['X-LINE-ChannelSecret'] = ENV['line_pay_channel_secret']
        req.body = {
          productName: "五百倍大平台", 
          amount: current_cart.total_price.to_i, 
          currency: "TWD", 
          confirmUrl: "http://localhost:3000/orders/confirm", 
          orderId: @order.num
        }.to_json
      end
```

6. 

