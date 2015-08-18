##PopUp的实现方法
###说明：
popup是一种用于window中弹出所需window的方法，具体方式为向给定一个page上发送信息，设置相应操作，并以代码实现操作。
###举例说明：
1.以购买爆弹弹窗提示花费钻石为例
```javascript
           create_popup("buy-conform")
                .set_data("message",buf)
                .add_action("ok", *this, &BattlePage::doBuyBombOk)
                .add_action("cancel",*this,&BattlePage::doBuyBombCancel)
                .show();
```
上例中以buy-conform这个page为基本，向page发送了buf这样的信息，使之显示在page中，并设定了两个按键“确定”和“取消”，使之关联相应的相应函数doBuyBombOk和doBuyBombCancel，