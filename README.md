# dev_summary
**经验总结**

订单或支付页，实现客户挽留弹框 前提使用vue框架 监听用户的离开事件：


1.  监听手机返回键
使用popState事件监听history 的state变化；

    window.addEventListener('popstate', this.onPopState);
    
    // 初入页面就给history添加state记录, 这样用户点击了返回键就可以监听到popState事件变化了
    
    window.history.pushState(this.pageIndex++, 'current');
    
// 以下是部分代码
// 其中pageIndex很重要，用于记录当前页面state变化次数（如果当前页面A可跳转到B页面，再从B页面跳回，此state会+1-1+1，变为2次；但pageIndex的话，生命周期只在当前页面，所以跳回后也是1）
   
<pre><code>
...
askForStay () {
        var _this = this;
        const msg = '超过订单支付时效后，订单将被取消，请您尽快完成支付哦！';
        MessageBox({
          message: msg,
          title: '确认放弃支付吗？',
          confirmButtonText: '继续支付',
          cancelButtonText: '狠心放弃',
          showCancelButton: true
        }).then((res) => {
          if (res === 'confirm') {
            window.history.pushState(_this.pageIndex++, 'current');
          } else {
            history.back();
            _this.pageIndex = 0;
          }
        });
      },
      onPopState (ev) {
        if (this.pageIndex > 0) {
          this.askForStay();
          this.pageIndex--;
        } else {
          history.back();
        }
      }
    },
    created () {
      if (!device.isHrt && window.history && window.history.pushState) {
        window.addEventListener('popstate', this.onPopState);
        window.history.pushState(this.pageIndex++, 'current');
      }
</code></pre>



    


2.  beforeRouterLeave，beforeRouterEnter 判断用户的去留： enter前 的地址和leave的地址是否一致；
如果页面简单，且跳转固定的话，可以使用此方法
3.  
 
