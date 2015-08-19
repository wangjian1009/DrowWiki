##PopUp的实现方法
###说明：
popup是一种用于window中弹出所需window的方法，具体方式为向给定一个page上发送信息，设置相应操作，并以代码实现操作。
###举例说明：
####1.以购买爆弹弹窗提示花费钻石为例
```javascript
           create_popup("buy-conform")
                .set_data("message",buf)
                .add_action("ok", *this, &BattlePage::doBuyBombOk)
                .add_action("cancel",*this,&BattlePage::doBuyBombCancel)
                .show();
```
上例中以buy-conform这个page为基本，向page发送了buf这样的信息，使之显示在page中，并设定了两个按键“确定”和“取消”，使之关联相应的函数doBuyBombOk和doBuyBombCancel。除了show()函数外以上的每个函数均返回一个Drown::Popup &RGUIWindow的对象
buf的获得使用了函数：
```javascript
appendTipMessage(buf, sizeof(buf), COMMONSTRING_BUY_CONFIRM_BOMB，(uint32_t)gamedata->pveBombCost());
```
COMMONSTRING_BUY_CONFIRM_BOMB表示已经定义好的需要显示信息，第四个参数是信息中需要的数值数据。

对于doBuyBombOk和doBuyBombCancel这两个函数，都必须要有个形参Drow::Popup & popup，在函数中可使用popup获得某些需要的信息和操作，例如点击确定后退出弹出窗口可使用popup.hide()函数

####2.以商店购买商品和物品信息显示为例
set_data也可以传入其他类型的参数，购买物品和物品信息显示的方式如下：
```javascript
        SHOPITEM const * pShopItem = gamedata->shopItemAtIndex(item_index);

        if(pShopItem && !pShopItem->is_sold) {
            create_popup("buy-shop-item")
                .set_data(*pShopItem)
                .add_action("buy", *this, &MenuShopPage::doBuy)
                .show();
```
上例中，set_data获得了一个SHOPITEM的对象

```javascript
UI_PAGE_ITEM_INFO_TIP data;
    data.item_id = item_id;

    page.create_popup("item-tip-info")
        .set_data(data)
        .show();
```
上例中，set_data获得了一个UI_PAGE_ITEM_INFO_TIP的事件