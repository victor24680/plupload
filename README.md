【如何在TP框架下使用plupload上传插件】

1.下载TP框架和plupload插件源码（已下载）
1.1 下载地址
 TP框架下载地址：
 plupload下载地址：
 
 
 
2.使用方法

2.1-引入官方插件源码[plupload.full.min.js,jquery-1.10.2.min.js]

2.2.创建实例
     var uploader = new plupload.Uploader({ 
			browse_button : 'browse',
			url : '<{:U("Index/upload")}>',
			flash_swf_url : '/Public/js/Moxie.swf',
			silverlight_xap_url : '/Public/js/Moxie.xap',
			filters: {
			  	mime_types : [ 
				    { title : "图片文件", extensions : "jpg,gif,png" }
			  	]
			},
			init:{
				FileUpload:function(up,file,info){
					log('[FileUploaded] File:', file, "Info:", info);
				}
			}
	});
	
	2.3 初始化	
	uploader.init(); 
	
	
	
