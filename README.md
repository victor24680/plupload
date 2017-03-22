
如何在TP框架下使用plupload上传插件
=
1.下载TP框架和plupload插件源码（已下载）
-
### 1.1 下载地址

 `plupload下载地址（官网下载）：`http://www.plupload.com/download/
 
 `TP下载地址（官网下载）：`http://www.thinkphp.cn/down.html
 
 `插件使用手册：`http://www.cnblogs.com/itjeff/p/4233888.html
 
2.使用方法
-
### 2.1-引入官方插件源码

`引入两个主要核心文件：[plupload.full.min.js,jquery-1.10.2.min.js]`

### 2.2.创建实例

```Js
var uploader = new plupload.Uploader({ //实例化一个plupload上传对象
        browse_button : 'browse',
        url : '<{:U("Index/upload",array("param"=>5))}>',
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

### 2.2.创建实例
	
	
