
# 各类模糊算法效果展示
为了测试这里用到两张图片
![272x272](http://upload-images.jianshu.io/upload_images/1916010-624c67fe495a5bda.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![3500x2625](http://upload-images.jianshu.io/upload_images/1916010-2d3799e0dd74ca80.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 第一张图片(272x272)
### Fast Blur

![](http://upload-images.jianshu.io/upload_images/1916010-a20be33f651bed00.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Fast Blur(JNI实现)
>之前用真机测试两个Fast Blur (在小图上)的时间差不多，这里可能是因为模拟器是x86的原因

![](http://upload-images.jianshu.io/upload_images/1916010-70429f00d2e3b254.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Box Blur
>只能设置奇数的radius

![](http://upload-images.jianshu.io/upload_images/1916010-c8ecd443e68925f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Gaussia Fast Blur


![](http://upload-images.jianshu.io/upload_images/1916010-bfde5f7d1c93bb1c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Stack Blur

![](http://upload-images.jianshu.io/upload_images/1916010-e6a979454e795676.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### RenderScript Blur
>主流的 目前速度也是最快的，不过radius只能设置0-25之间，时间是0-2ms浮动

![](http://upload-images.jianshu.io/upload_images/1916010-4fc8550a6d2c08ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### RenderScript Box 3x3
>radius 并不是模糊半径 而是进行模糊的次数，所以会更花时间

![](http://upload-images.jianshu.io/upload_images/1916010-e9179030c529dd3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### RenderScript Box 5x5
>radius 代表次数

![](http://upload-images.jianshu.io/upload_images/1916010-b656c3b09a5dd462.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### RenderScript Box Gaussia 5x5
>和上面方法一样 只是设置的具体转换数值不同

![](http://upload-images.jianshu.io/upload_images/1916010-f1c2253320784ccb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 第二张图片(3500x2625)
>缩放及模糊半径与上面一致

|Fast Blur|Box Blur|
|:------:|:--------:|
|![](http://upload-images.jianshu.io/upload_images/1916010-da33863c3722fcc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|![](http://upload-images.jianshu.io/upload_images/1916010-f873d893266b53b5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|Gaussia Fast Blur|Stack Blur|
|![](http://upload-images.jianshu.io/upload_images/1916010-32488ff41db9567e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|![](http://upload-images.jianshu.io/upload_images/1916010-ef271636e54ef1f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|RenderScript Blur|RenderScript Box 3x3|
|![](http://upload-images.jianshu.io/upload_images/1916010-d94435166b80a12c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|![](http://upload-images.jianshu.io/upload_images/1916010-db36a15bf1527c17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|RenderScript Box 5x5|RenderScript Box Gaussia 5x5|
|![](http://upload-images.jianshu.io/upload_images/1916010-879a08901ac518a6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|![](http://upload-images.jianshu.io/upload_images/1916010-870318be03c688a6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 这里开启Bitmap Filter 再看下效果
||NO FILTER|FILTER|
|:----:|:-------:|:-----:|
|Fast Blur|![](http://upload-images.jianshu.io/upload_images/1916010-da33863c3722fcc7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|![](http://upload-images.jianshu.io/upload_images/1916010-fc12d3436a986cef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|RenderScript Blur|![](http://upload-images.jianshu.io/upload_images/1916010-00424a2e8151e391.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|![](http://upload-images.jianshu.io/upload_images/1916010-5a1d23127baa25a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 表格统计
>这里第一个图(272x272)用A表示,第二个图(3500x2625)用B表示`()`表示模糊半径及缩放比例,每个测试三组测试数据已`(时间,内存)`展示,`crash`都是因为OOM了

|算法|(20,0.125)|(10,0.125)|(25,0.5)|(25,1)|(50,1)|
|:--:|:--------:|:-------:|:------:|:---:|:----:|
|FB|A`(2,720)`</br>B`(19,3804)`|A`(1,388)`</br>B`(17,3484)`|A`(22,4592)`</br>B`(380,37284)`|A`(102,13048)`</br>B`crash`|A`(115,10420)`</br>B`crash`|
|FB(C)|A`(1,96)`</br>B`(12,1120)`|A`(1,88)`</br>B`(9,1120)`|A`(9,1304)`</br>B `crash`|A`crash`</br>B`crash`|A`crash`</br>B`crash`|
|BB|A`(2,132)`</br>B`(26,1680)`|A`(2,132)`</br>B`(27,1684)`|A`(30,1956)`</br>B`(459,18016)`|A`(133,7812)`</br>B`crash`|A`(138,7820)`</br>B`crash`|
|GFB|A`(1,92)`</br>B`(16,1124)`|A`(1,96)`</br>B`(15,1128)`|B`(263,9008??18016)`|A`(87,5208)`</br>B`crash`|A`(88,5208)`</br>B`crash`|
|STB|A`(2,624)`</br>B`(18,3244)`|A`(2,344)`</br>B`(17,2924)`|A`(21,3340)`</br>B`(394,??)`|A`(95,13700)`</br>B`crash`|A`(116,15628)`</br>B`crash`|
|RSB|A`(1,52)`</br>B`(7,564)`|A`(1,48)`</br>B`(5,568)`|A`(6,652)`</br>B`(78,9008)`|A`(21,2604)`</br>B`(275,36116)`|不支持|
|RSB3x3|A`(3,48)`</br>B`(12,564)`|A`(1,48)`</br>B`(5,560)`|A`(15,652)`</br>B`(100,9008)`|A`(36,2604)`</br>B`(409,36120)`|A`(62,2604)`</br>B`(713,35888)`
|RSB5x5|A`(4,60)`</br>B`(17,560)`|A`(2,60)`</br>B`(9,560)`|A`(22,652)`</br>B`(191,9008)`|A`(59,2604)`</br>B`(661,35888)`|A`(122,2604)`</br>B`(1249,35888)`
|RSBG5x5|A`(4,44)`</br>B`(17,560)`|A`(2,56)`</br>B`(10,568)`|A`(22,652)`</br>B`(187,9008)`|A`(59,2604)`</br>B`(677,35892)`|A`(120,2604)`</br>B`(1268,35892)`


















