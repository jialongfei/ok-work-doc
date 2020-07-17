# 复立速递接入文档





> 请注意：该文档暂未完结，请求地址暂不可访问，持续更新中...



> 为保护双方公司利益，防止其他用户恶意攻击，接口均不直接展示错误信息，只返回错误代码，具体错误原因接入方根据错误代码在文档底部的错误代码对照表中查阅





### 1.预创建订单



并非真正发单，用来验证是否可以发单并在成功时返回时效、计价等信息，也可用来验证地址以及时间是否在配送范围内。



请求方式：post

请求地址：https://okapi.okchexian.com/api/express/precreateorder



##### 请求参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>必选</td>
        <td>可为空</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>secret_key</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用于认证身份的秘钥，由复立方提供</td>
    </tr>
    <tr align="center">
        <td>user_address</td>
        <td>string(255)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户详细地址</td>
    </tr>
    <tr align="center">
        <td>weight</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">物品重量(单位:克)</td>
    </tr>
    <tr align="center">
        <td>is_appoint</td>
        <td>int(2)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">是否预约单(枚举值) <br>0:非预约单 <br>1:预约单</td>
    </tr>
    <tr align="center">
        <td>expect_time</td>
        <td>int(11)</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">期望送达时间(秒级时间戳) 预约单需必传</td>
    </tr>
    <tr align="center">
        <td>pay_type</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户支付方式(枚举值) <br>0:货到付款 <br>1:已支付</td>
    </tr>
    <tr align="center">
        <td>receive_user_money</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">代收金额(单位:分)</td>
    </tr>
    <tr align="center">
        <td>is_insured</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">是否保价(枚举值) <br>0:非保价 <br>1:保价</td>
    </tr>
    <tr align="center">
        <td>declared_value</td>
        <td>int(11)</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">保价金额(单位:分)</td>
    </tr>
    <tr align="center">
        <td>gratuity_fee</td>
        <td>int(11)</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">订单小费(单位:分) 不传或者传0为不加小费,最低不能少于100分</td>
    </tr>
    <tr align="center">
        <td>push_time</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">推单时间(秒级时间戳)</td>
    </tr>
    <tr align="center">
        <td>shop_name</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">店铺名称</td>
    </tr>
    <tr align="center">
        <td>shop_phone</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">店铺电话</td>
    </tr>
    <tr align="center">
        <td>shop_address</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">店铺地址</td>
    </tr>
    <tr align="center">
        <td>product_type</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">物品类型(枚举值) <br>1:快餐 <br>2:送药 <br>3:百货 <br>4:脏衣服收 <br>5:干净衣服派 <br>6:生鲜 <br>7:保单 <br>8:高端饮品 <br>9:现场勘验 <br>10:快递 <br>12:文件 <br>13:蛋糕 <br>14:鲜花 <br>15:电子数码 <br>16:服装鞋帽 <br>17:汽车配件 <br>18:珠宝 <br>20:披萨 <br>21:中餐 <br>22:水产 <br>27:专人直送 <br>32:中端饮品 <br>33:便利店 <br>34:面包糕点 <br>35:火锅 <br>36:证照 <br>99:其他</td>
    </tr>
</table>



##### 响应参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>result</td>
        <td>object/string</td>
        <td align="left">成功时返回json对象，失败时返回''空字符串</td>
    </tr>
    <tr align="center">
        <td>result.delivery_type</td>
        <td>int</td>
        <td align="left">0:预约送达单 1:立即单 3:预约上门单</td>
    </tr>
    <tr align="center">
        <td>result.expect_time</td>
        <td>int</td>
        <td align="left">预计送达(上门)时间</td>
    </tr>
    <tr align="center">
        <td>result.start_time</td>
        <td>int</td>
        <td align="left">预计开始配送的时间</td>
    </tr>
    <tr align="center">
        <td>result.promise_delivery_time</td>
        <td>int</td>
        <td align="left">预计配送时间(单位:分)</td>
    </tr>
    <tr align="center">
        <td>result.delivery_distance_meter</td>
        <td>string</td>
        <td align="left">配送距离</td>
    </tr>
    <tr align="center">
        <td>result.shop_pay_price</td>
        <td>int</td>
        <td align="left">配送费总额(单位:分)</td>
    </tr>
    <tr align="center">
        <td>result.gratuity_fee</td>
        <td>int</td>
        <td align="left">订单小费(单位:分)</td>
    </tr>
    <tr align="center">
        <td>result.push_time</td>
        <td>int</td>
        <td align="left">推单时间</td>
    </tr>    
    <tr align="center">
        <td>error_code</td>
        <td>string</td>
        <td align="left">错误代码，处理成功时返回null，否则是错误代码</td>
    </tr>
    <tr align="center">
        <td>error_info</td>
        <td>string</td>
        <td align="left">错误详情，不在这里展示，请根据错误代码在文档末尾中匹配具体错误信息</td>
    </tr>
</table>




成功示例

![成功示例](./precreateorder-success.png)



失败示例

![失败示例](./precreateorder-error.png)





### 2.创建订单



当接入方接收到订单时，可通过此接口进行订单的创建。订单状态通过回调的方式通知，接入方也可以在下单成功后，主动发起订单状态查询的请求，通过返回的结果对订单进行状态更新的操作。



请求方式：post

请求地址：https://okapi.okchexian.com/api/express/createorder



##### 请求参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>必选</td>
        <td>可为空</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>secret_key</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用于认证身份的秘钥，由复立方提供</td>
    </tr>
    <tr align="center">
        <td>callback_url</td>
        <td>string(255)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">回调地址(用于接收订单的接单和配送状态)</td>
    </tr>
    <tr align="center">
        <td>order_time</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户下单时间(秒级时间戳)</td>
    </tr>
    <tr align="center">
        <td>remark</td>
        <td>string(1024)</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">订单备注</td>
    </tr>
    <tr align="center">
        <td>is_appoint</td>
        <td>int(2)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">是否预约单(枚举值) <br>0:非预约单 <br>1:预约单</td>
    </tr>
    <tr align="center">
        <td>expect_time</td>
        <td>int(11)</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">期望送达时间(秒级时间戳) 预约单需必传</td>
    </tr>
    <tr align="center">
        <td>pay_type</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户支付方式(枚举值) <br>0:货到付款 <br>1:已支付</td>
    </tr>
    <tr align="center">
        <td>receive_user_money</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">代收金额(单位:分)</td>
    </tr>
    <tr align="center">
        <td>is_insured</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">是否保价(枚举值) <br>0:非保价<br> 1:保价</td>
    </tr>
    <tr align="center">
        <td>declared_value</td>
        <td>int(11)</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">保价金额(单位:分)</td>
    </tr>
    <tr align="center">
        <td>gratuity_fee</td>
        <td>int(11)</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">订单小费(单位:分) 不传或者传0为不加小费,最低不能少于100分</td>
    </tr>
    <tr align="center">
        <td>push_time</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">推单时间(秒级时间戳)</td>
    </tr>
    <tr align="center">
        <td>shop_name</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">店铺名称</td>
    </tr>
    <tr align="center">
        <td>shop_phone</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">店铺电话</td>
    </tr>
    <tr align="center">
        <td>shop_address</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">店铺地址</td>
    </tr>
    <tr align="center">
        <td>user_name</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户姓名</td>
    </tr>
    <tr align="center">
        <td>user_phone</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户电话</td>
    </tr>
    <tr align="center">
        <td>user_address</td>
        <td>string(255)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户地址</td>
    </tr>
    <tr align="center">
        <td>user_lng</td>
        <td>string(32)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户经度</td>
    </tr>
    <tr align="center">
        <td>user_lat</td>
        <td>string(32)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户纬度</td>
    </tr>
    <tr align="center">
        <td>city_name</td>
        <td>string(32)</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">发单城市</td>
    </tr>
    <tr align="center">
        <td>total_price</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用户订单总金额(单位:分)</td>
    </tr>
    <tr align="center">
        <td>product_name</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">物品名称</td>
    </tr>
    <tr align="center">
        <td>weight_gram</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">物品重量(单位:克)</td>
    </tr>
    <tr align="center">
        <td>product_num</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">物品个数</td>
    </tr>
    <tr align="center">
        <td>product_type_num</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">物品种类个数</td>
    </tr>
    <tr align="center">
        <td>product_num</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">物品数量</td>
    </tr>
    <tr align="center">
        <td>product_type</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">物品类型(枚举值) <br>1:快餐 <br>2:送药 <br>3:百货 <br>4:脏衣服收 <br>5:干净衣服派 <br>6:生鲜 <br>7:保单 <br>8:高端饮品 <br>9:现场勘验 <br>10:快递 <br>12:文件 <br>13:蛋糕 <br>14:鲜花 <br>15:电子数码 <br>16:服装鞋帽 <br>17:汽车配件 <br>18:珠宝 <br>20:披萨 <br>21:中餐 <br>22:水产 <br>27:专人直送 <br>32:中端饮品 <br>33:便利店 <br>34:面包糕点 <br>35:火锅 <br>36:证照 <br>99:其他</td>
    </tr>
</table>



##### 响应参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>result</td>
        <td>object/string</td>
        <td align="left">成功时返回json对象，失败时返回''空字符串</td>
    </tr>
    <tr align="center">
        <td>result.sf_order_id</td>
        <td>string</td>
        <td align="left">订单号</td>
    </tr>
    <tr align="center">
        <td>result.sf_bill_id</td>
        <td>string</td>
        <td align="left">运单号</td>
    </tr>
    <tr align="center">
        <td>result.shop_order_id</td>
        <td>int</td>
        <td align="left">商家订单号</td>
    </tr>
    <tr align="center">
        <td>result.push_time</td>
        <td>int</td>
        <td align="left">推单时间</td>
    </tr>
    <tr align="center">
        <td>result.total_price</td>
        <td>int</td>
        <td align="left">配送费总额(单位:分)</td>
    </tr>
    <tr align="center">
        <td>result.delivery_distance_meter</td>
        <td>int</td>
        <td align="left">配送距离</td>
    </tr>
    <tr align="center">
        <td>result.weight_gram</td>
        <td>int</td>
        <td align="left">商品重量</td>
    </tr>
    <tr align="center">
        <td>result.start_time</td>
        <td>int</td>
        <td align="left">起送时间(单位:分)</td>
    </tr>
    <tr align="center">
        <td>result.expect_time</td>
        <td>int</td>
        <td align="left">期望送达时间(单位:分)</td>
    </tr>
    <tr align="center">
        <td>result.total_pay_money</td>
        <td>int</td>
        <td align="left">支付费用(单位:分)</td>
    </tr>
    <tr align="center">
        <td>result.real_pay_money</td>
        <td>int</td>
        <td align="left">实际支付金额(单位:分)</td>
    </tr>
    <tr align="center">
        <td>result.coupons_total_fee</td>
        <td>int</td>
        <td align="left">优惠券总金额(单位:分)</td>
    </tr>
    <tr align="center">
        <td>result.settlement_type</td>
        <td>int</td>
        <td align="left">结算方式</td>
    </tr>
    <tr align="center">
        <td>error_code</td>
        <td>string</td>
        <td align="left">错误代码，处理成功时返回null，否则是错误代码</td>
    </tr>
    <tr align="center">
        <td>error_info</td>
        <td>string</td>
        <td align="left">错误详情，不在这里展示，请根据错误代码在文档末尾中匹配具体错误信息</td>
    </tr>
</table>




成功示例

![成功示例](./createorder-success.png)



失败示例

![失败示例](./createorder-error.png)





### 3.取消订单



当接入方需要取消配送时，可调用此接口对订单进行取消操作，同步返回结果。



请求方式：post

请求地址：https://okapi.okchexian.com/api/express/cancelorder



##### 请求参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>必选</td>
        <td>可为空</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>secret_key</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用于认证身份的秘钥，由复立方提供</td>
    </tr>
    <tr align="center">
        <td>order_id</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">订单ID</td>
    </tr>
    <tr align="center">
        <td>cancel_reason</td>
        <td>string(256)</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">取消原因</td>
    </tr>
    <tr align="center">
        <td>push_time</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">取消时间(秒级时间戳)</td>
    </tr>
</table>



##### 响应参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>result</td>
        <td>object/string</td>
        <td align="left">成功时返回json对象，失败时返回''空字符串</td>
    </tr>
    <tr align="center">
        <td>result.sf_order_id</td>
        <td>string</td>
        <td align="left">配送订单号</td>
    </tr>
    <tr align="center">
        <td>result.shop_order_id</td>
        <td>string</td>
        <td align="left">商家订单号</td>
    </tr>
    <tr align="center">
        <td>result.push_time</td>
        <td>string</td>
        <td align="left">推送时间</td>
    </tr>
    <tr align="center">
        <td>error_code</td>
        <td>string</td>
        <td align="left">错误代码，处理成功时返回null，否则是错误代码</td>
    </tr>
    <tr align="center">
        <td>error_info</td>
        <td>string</td>
        <td align="left">错误详情，不在这里展示，请根据错误代码在文档末尾中匹配具体错误信息</td>
    </tr>
</table>




成功示例

![成功示例](./cancelorder-success.png)



失败示例

![失败示例](./cancelorder-error.png)





### 4.催单



当订单为配送状态中，可通过该接口发起催单。



请求方式：post

请求地址：https://okapi.okchexian.com/api/express/reminderorder



##### 请求参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>必选</td>
        <td>可为空</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>secret_key</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用于认证身份的秘钥，由复立方提供</td>
    </tr>
    <tr align="center">
        <td>order_id</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">订单ID</td>
    </tr>
    <tr align="center">
        <td>push_time</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">推送时间(秒级时间戳)</td>
    </tr>
</table>



##### 响应参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>result</td>
        <td>object/string</td>
        <td align="left">成功时返回json对象，失败时返回''空字符串</td>
    </tr>
    <tr align="center">
        <td>result.sf_order_id</td>
        <td>string</td>
        <td align="left">配送订单号</td>
    </tr>
    <tr align="center">
        <td>result.shop_order_id</td>
        <td>string</td>
        <td align="left">商家订单号</td>
    </tr>
    <tr align="center">
        <td>result.push_time</td>
        <td>string</td>
        <td align="left">推送时间</td>
    </tr>
    <tr align="center">
        <td>error_code</td>
        <td>string</td>
        <td align="left">错误代码，处理成功时返回null，否则是错误代码</td>
    </tr>
    <tr align="center">
        <td>error_info</td>
        <td>string</td>
        <td align="left">错误详情，不在这里展示，请根据错误代码在文档末尾中匹配具体错误信息</td>
    </tr>
</table>




成功示例

![成功示例](./reminderorder-success.png)



失败示例

![失败示例](./reminderorder-error.png)





### 5.订单状态查询



此接口可获取到指定订单的状态信息，用来进行订单状态的查询。可通过此对订单进行状态补齐操作，当接收订单状态回调失败时，可主动查询订单状态。



请求方式：post

请求地址：https://okapi.okchexian.com/api/express/listorderfeed



##### 请求参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>必选</td>
        <td>可为空</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>secret_key</td>
        <td>string(64)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">用于认证身份的秘钥，由复立方提供</td>
    </tr>
    <tr align="center">
        <td>order_id</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">订单ID</td>
    </tr>
    <tr align="center">
        <td>push_time</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">推送时间(秒级时间戳)</td>
    </tr>
</table>



##### 响应参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>result</td>
        <td>object/string</td>
        <td align="left">成功时返回json对象，失败时返回''空字符串</td>
    </tr>
    <tr align="center">
        <td>result.sf_order_id</td>
        <td>string</td>
        <td align="left">配送订单号</td>
    </tr>
    <tr align="center">
        <td>result.shop_order_id</td>
        <td>string</td>
        <td align="left">商家订单号</td>
    </tr>
    <tr align="center">
        <td>result.create_time</td>
        <td>int</td>
        <td align="left">订单创建时间</td>
    </tr>
    <tr align="center">
        <td>result.push_time</td>
        <td>string</td>
        <td align="left">当前推送时间</td>
    </tr>
    <tr align="center">
        <td>result.feed</td>
        <td>array</td>
        <td align="left"><pre>
订单进度
'feed':[
    {
        "sf_order_id": 3171874687750684700,
        "shop_order_id": "1000007894570",
        "order_status": 1,
        "operator": "【门店生成订单】门店ID3241827460869",
        "operator_name": "",
        "operator_phone":"",
        "status_desc": "订单提交成功",
        "content": "订单号：3171874687750684673",
        "create_time": "2017-12-05 17:55:39"
    },
    {
        "sf_order_id": 3171874687750684700,
        "shop_order_id": "1000007894570",
        "order_status": 10,
        "operator": "lize",
        "operator_name": "lize_test",
        "operator_phone": 18811588750,
        "status_desc": "配送员已接单",
        "content": "配送员接单：lize，电话：18811588750",
        "create_time": "2017-12-05 18:04:53"
    },
    {
        "sf_order_id": 3171874687750684700,
        "shop_order_id": "1000007894570",
        "order_status": 10,
        "operator": "lize",
        "operator_name": "lize_test",
        "operator_phone": 18811588750,
        "status_desc": "配送员已接单",
        "content": "配送员接单：lize，电话：18811588750",
        "create_time": "2017-12-05 18:05:17"
    },
    {
        "sf_order_id": 3171874687750684700,
        "shop_order_id": "1000007894570",
        "order_status": 12,
        "operator": "lize",
        "operator_name": "lize_test",
        "operator_phone": 18811588750,
        "status_desc": "配送员已到店",
        "content": "配送员已到店：配送员：lize，配送员电话：18811588750",
        "create_time": "2017-12-05 18:05:50"
    },
    {
        "sf_order_id": 3171874687750684700,
        "shop_order_id": "1000007894570",
        "order_status": 14,
        "operator": "lize",
        "operator_name": "lize_test",
        "operator_phone": 18811588750,
        "status_desc": "配送员已取货",
        "content": "正在配送中：配送员：lize，配送员电话：18811588750",
        "create_time": "2017-12-05 18:06:17"
    },
    {
        "sf_order_id": 3171874687750684700,
        "shop_order_id": "1000007894570",
        "order_status": 17,
        "operator": "lize",
        "operator_name": "lize_test",
        "operator_phone": 18811588750,
        "status_desc": "配送员完成",
        "content": "配送员点击完成，配送员：，配送员电话：",
        "create_time": "2017-12-05 18:07:09"
    },
]
        </pre></td>
    </tr>
    <tr align="center">
        <td>error_code</td>
        <td>string</td>
        <td align="left">错误代码，处理成功时返回null，否则是错误代码</td>
    </tr>
    <tr align="center">
        <td>error_info</td>
        <td>string</td>
        <td align="left">错误详情，不在这里展示，请根据错误代码在文档末尾中匹配具体错误信息</td>
    </tr>
</table>




成功示例

![成功示例](./listorderfeed-success.png)



失败示例

![失败示例](./listorderfeed-error.png)





### 6.订单状态回调 （回调接口）



当订单状态发生变更时，会回调接入方的回调地址进行状态变更的通知。



请求方式：post

请求地址：接入方在创建订单时传递的回调地址



##### 回调参数列表

<table border="1px" align="center">
    <tr align="center">
        <td>参数名称</td>
        <td>类型</td>
        <td>必选</td>
        <td>可为空</td>
        <td>参数描述</td>
    </tr>
    <tr align="center">
        <td>sf_order_id</td>
        <td>bingint</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">配送订单号</td>
    </tr>
    <tr align="center">
        <td>shop_order_id</td>
        <td>string</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">商家订单号</td>
    </tr>
    <tr align="center">
        <td>order_status</td>
        <td>int</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">订单状态(枚举值)<br> 1:订单创建<br> 2:订单取消<br> 10:配送员接单<br> 12:配送员到店<br> 15:配送员配送中<br> 17:配送员完成订单</td>
    </tr>
    <tr align="center">
        <td>cancel_reason</td>
        <td>string</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">取消原因</td>
    </tr>
    <tr align="center">
        <td>status_desc</td>
        <td>string</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">状态描述</td>
    </tr>
    <tr align="center">
        <td>push_time</td>
        <td>int(11)</td>
        <td>Y</td>
        <td>N</td>
        <td align="left">状态变更时间(秒级时间戳)</td>
    </tr>
    <tr align="center">
        <td>operator_name</td>
        <td>string</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">配送员姓名</td>
    </tr>
    <tr align="center">
        <td>operator_phone</td>
        <td>string</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">配送员电话</td>
    </tr>
    <tr align="center">
        <td>rider_lng</td>
        <td>string</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">配送员位置经度</td>
    </tr>
    <tr align="center">
        <td>rider_lat</td>
        <td>string</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">配送员位置纬度</td>
    </tr>
    <tr align="center">
        <td>ex_id</td>
        <td>int</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">异常ID(枚举值) <br>4003:托寄物丢失或损坏 <br>1001:商家出货慢 <br>2010:顾客拒绝实名认证 <br>3004:实名认证校验失败 <br>1007:更改取货地址 <br>2001:顾客电话无法接通 <br>2004:更改期望送达时间 <br>2005:顾客拒收 <br>2008:顾客不在家 <br>2009:更改送货地址 <br>4001:配送地址错误 <br>4002:其他</td>
    </tr>
    <tr align="center">
        <td>ex_content</td>
        <td>string</td>
        <td>N</td>
        <td>Y</td>
        <td align="left">异常详情</td>
    </tr>
</table>





# 枚举字段速查表



##### order_status 订单状态

```
1  = 订单创建 
2  = 订单取消 
10 = 配送员接单 
12 = 配送员到店 
15 = 配送员配送中（已取货） 
17 = 配送员完成订单
```

##### product_type 物品类型

```
1  = 快餐
2  = 送药
3  = 百货
4  = 脏衣服收
5  = 干净衣服派
6  = 生鲜
7  = 保单
8  = 高端饮品
9  = 现场勘验
10 = 快递
12 = 文件
13 = 蛋糕
14 = 鲜花
15 = 电子数码
16 = 服装鞋帽
17 = 汽车配件
18 = 珠宝
20 = 披萨
21 = 中餐
22 = 水产
27 = 专人直送
32 = 中端饮品
33 = 便利店
34 = 面包糕点
35 = 火锅
36 = 证照
99 = 其他
```

##### ex_id 异常ID

```
4003 = 托寄物丢失或损坏
1001 = 商家出货慢
2010 = 顾客拒绝实名认证
3004 = 实名认证校验失败
1007 = 更改取货地址
2001 = 顾客电话无法接通
2004 = 更改期望送达时间
2005 = 顾客拒收
2008 = 顾客不在家
2009 = 更改送货地址
4001 = 配送地址错误
4002 = 其他
```



# 错误代码对照表

```
FL0010:接入方身份认证失败，通常是secret_key不正确
FL0020:参数错误
FL0030:
FL0040:
FL0050:
FL0060:
FL0070:
FL0080:
FL0090:
FL0100:
```


