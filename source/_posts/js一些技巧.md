---
title: js一些技巧
date: 2017-04-24 16:23:29
tags:
---
##### 统计数组
```
// 统计数组
var dataArr = [];
for (var i = 0; i < comSysArr.length;) {
    var isHave = false;
    for (var j = 0; j < dataArr.length;j++) {
        if (comSysArr[i].comSysTypeName == dataArr[j][0]) {
            isHave = true;
            if (comSysArr[i].buildYear == yearCurrunt) {      //当前的一年
                dataArr[j][3] += comSysArr[i].comSysCount - 0;
            } else if (comSysArr[i].buildYear == yearCurrunt - 1) {
                dataArr[j][2] += comSysArr[i].comSysCount - 0;
            } else if (comSysArr[i].buildYear == yearCurrunt - 2) {
                dataArr[j][1] += comSysArr[i].comSysCount - 0;
            }
            i++;
        }
    }
    if (!isHave) {
        dataArr.push([comSysArr[i].comSysTypeName, 0, 0, 0])
    }

}
var lengendText = [];
dataArr.forEach(function (item, index) {
    lengendText.push(item[0])
    item.shift()
})
arr0 = dataArr[0] == undefined ? [0, 0, 0] : dataArr[0];
arr1 = dataArr[1] == undefined ? [0, 0, 0] : dataArr[1];
arr2 = dataArr[2] == undefined ? [0, 0, 0] : dataArr[2];
arr3 = dataArr[3] == undefined ? [0, 0, 0] : dataArr[3];
arr4 = dataArr[4] == undefined ? [0, 0, 0] : dataArr[4];

// javascript 技巧
 var arr = [[123, 12], 1, [1, 123]];
    var arr1 = [];
    // 递归
    function fn(array) {
        for (var i = 0; i < array.length; i++) {
            if (typeof array[i] != 'number') {
                fn(array[i]);
            } else {
                arr1.push(array[i])
            }
        }
    }
    fn(arr);
    // 冒泡排序
    for (var j = 0; j < arr1.length; j++) {
        for (var i = 0; i < arr1.length - 1 - j; i++) {
            if (arr1[i] > arr1[i + 1]) {
                var temp = arr1[i];
                arr1[i] = arr1[i + 1];
                arr1[i + 1] = temp
            }
        }
    }
    // 统计出现的次数
    var arrCount = [];
    for (var i = 0; i < arr1.length; i++) {
        var isHave = false;
        for (var j = 0; j < arrCount.length; j++) {
            if (arrCount[j].name == arr1[i]) {
                isHave = true;
                arrCount[j].count++;
            }
        }
        if (!isHave) {
            var item = {
                name: arr1[i],
                count: 1
            };
            arrCount.push(item)
        }
    }



```