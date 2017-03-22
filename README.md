
如何在TP框架下使用plupload上传插件
=
1.下载TP框架和plupload插件源码（已下载）
-
### 1.1 下载地址

 `plupload下载地址（官网下载）：`http://www.plupload.com/download/
 
 `TP下载地址（官网下载）：`http://www.thinkphp.cn/down.html
 
 `参考使用使用手册：`http://www.cnblogs.com/itjeff/p/4233888.html
 
2.使用方法[推荐放在页面底部操作JS文件
-
### 2.1-引入官方插件源码

`引入两个主要核心文件：[plupload.full.min.js,jquery-1.10.2.min.js]`

### 2.2.创建实例

```Js
var uploader = new plupload.Uploader({ //实例化一个plupload上传对象
        browse_button : 'browse',
        url : '<{:U("Index/upload")}>',//上传地址
	flash_swf_url : '/Public/js/Moxie.swf',
        silverlight_xap_url : '/Public/js/Moxie.xap',
        filters: {
                mime_types : [ //只允许上传图片文件
                    { title : "图片文件", extensions : "jpg,gif,png" }
                ]
        },
        init:{
                FileUpload:function(up,file,info){
                        log('[FileUploaded] File:', file, "Info:", info);
                }
        }
});
```

### 2.2.初始化文件
```Js
uploader.init(); //初始化
```
### 2.3.操作JS动作文件
```Js
//绑定添加队事件【FilesAdded：点击时需要触发的ID属性】
uploader.bind('FilesAdded',function(uploader,files){
	for(var i = 0, len = files.length; i<len; i++){
		var file_name = files[i].name; //获取图像文件名；
		//构造html来更新UI,files[i].id,图像ID号，一串加密的字符串；【具体见文档】
		//files[i].id【文件ID号】,
		
		//put here your code

		!function(i){
			previewImage(files[i],function(imgsrc){//imgsrc【图片地址】
			//编写自己的代码图片显示的地方			
			})
	    }(i);
	}
	uploader.start();//触发上传程序；(也可以在任意地方触发上传动作)
	return false;
});

//file为plupload事件监听函数参数中的file对象,callback为预览图片准备完成的回调函数
function previewImage(file,callback){
   if(!file || !/image\//.test(file.type)) return; //确保文件是图片
     if(file.type=='image/gif'){//gif使用FileReader进行预览,因为mOxie.Image只支持jpg和png
	var fr = new mOxie.FileReader();
	fr.onload = function(){
           callback(fr.result);
           fr.destroy();
	   fr = null;
	}
	fr.readAsDataURL(file.getSource());
      }else{
	  var preloader = new mOxie.Image();
	  preloader.onload = function() {
	     preloader.downsize( 300, 300 );//先压缩一下要预览的图片,宽300，高300
	     //得到图片src,实质为一个base64编码的数据
	     var imgsrc = preloader.type=='image/jpeg' ? preloader.getAsDataURL('image/jpeg',80) : preloader.getAsDataURL(); 
	     callback && callback(imgsrc); //callback传入的参数为预览图片的url
	     preloader.destroy();
	     preloader = null;
	  };
	  preloader.load( file.getSource() );
     }	
}
```

说明：
=
提供所需源码，上面为示例的Js核心源码
