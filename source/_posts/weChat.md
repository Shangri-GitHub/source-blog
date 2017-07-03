---
title: weChat
date: 2017-04-18 11:01:44
tags: wechat
---
##### 统一使用微信的插件
``` javascript
    
    // 加载转圈
    var loading = weui.loading('加载中...');
    // 加载消失
    loading.hide
    
    // 自身的提示框(上面有对号图标)
     weui.toast('操作成功', 2000)
    
    // 自定义的toast提示框（只有文字提示）
     weui.toast('系统异常，请稍后再试！', {
         className: 'toast',
         duration: 2000,
     });

```
##### 下拉刷新 ([dropload插件](https://github.com/ximan/dropload))
```  javascript
function httprequest(code,name,me){
    // 拼接HTML //调用列表接口
	HttpUtils.get(API.listAll,{page:page,rows:size,loginCode:code,
			opName:name},function(data){
		var arrLen = data.rows.length;
		page++;
		if(arrLen < size){
			// 锁定
			me.lock();
			// 无数据
			me.noData();
		}
		// 为了测试，延迟1秒加载
		$("#movieTemplate").tmpl(data.rows).appendTo("#content");
		me.resetload();
	},function(){
		//alert('Ajax error!');
		// 即使加载出错，也得重置
		//me.resetload();
		weui.toast('系统异常，请稍后再试！', {
			className: 'toast',
			duration: 2000,
		});
     })
}
```
##### tab页的横向滚动 [iscroll插件详情](https://github.com/cubiq/iscroll)
```  javascript



  // preventDefault: true,
  preventDefault: false,//（把这句加上去哦）
  preventDefaultException: { tagName: /^(INPUT|TEXTAREA|BUTTON|SELECT|A)$/ },  //（这个后面加|A,因为iscroll阻止了A的默认事件）
  // tab 滚动
  var myscroll;
  function loaded() {
      setTimeout(function () {
          myscroll = new IScroll('#tabs', {
              scrollX: true,
              scrollY: false,
              click: true
          })
      }, 100)
  }
  window.addEventListener('load', loaded, false)

```