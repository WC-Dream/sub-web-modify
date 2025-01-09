# sub-web-modify
[本项目](https://suburl.v1.mk)重制[原项目](https://github.com/CareyWang/sub-web)CSS样式，兼容nodejs最新版本（可直接一键部署至Vercel），解决大部分布局细节问题，增加“暗黑模式”，默认自动切换亮/暗模式（点击“太阳/月亮”图标可手动切换），增加“高级功能”点击显示/隐藏，添加短链接选择/自定义功能，增加近百条远程配置，新增[sub-web聚合API](https://github.com/youshandefeiyang/sub-web-api)，增加从短链接中获取订阅信息并返回至前端界面，增加上传自定义远程配置/JS进阶排序节点/JS进阶筛选节点等功能，感兴趣的朋友可以自建API服务，增加URL传参设置自定义后端<br/>
## 效果预览：
![avatar](https://raw.githubusercontent.com/youshandefeiyang/webcdn/main/sub-web-modify.GIF)
### 使用方法：
建议使用Docker一键部署:
```
docker run -d --restart unless-stopped --privileged=true -p 8090:80 --name sub-web-modify youshandefeiyang/sub-web-modify
```
访问地址举例:
```
http://192.168.10.1:8090/?backend=https://url.v1.mk
```



使用方法【以Linux为例】：
1.安装 node 和 yarn 和 git

2.终端执行 cd /home && git clone https://github.com/youshandefeiyang/sub-web-modify.git && chmod -R 755 sub-web-modify && cd sub-web-modify && yarn install && yarn build

3.build成功后，需要安装nginx并正确配置，以下为nginx server部分配置，可以参考一下【这块建议新手使用宝塔面板等自动化运维工具，直接将网站目录更改为/home/sub-web-modify/dist即可】！

server {
    listen 80;
    server_name 你的域名或IP;
    root /home/sub-web-modify/dist;
    index index.html index.htm;
    error_page 404 /index.html;
    gzip on; #开启gzip压缩
    gzip_min_length 1k; #设置对数据启用压缩的最少字节数
    gzip_buffers 4 16k;
    gzip_http_version 1.0;
    gzip_comp_level 6; #设置数据的压缩等级,等级为1-9，压缩比从小到大
    gzip_types text/plain text/css text/javascript application/json application/javascript application/x-javascript application/xml; #设置需要压缩的数据格式
    gzip_vary on;
    location ~* \.(css|js|png|jpg|jpeg|gif|gz|svg|mp4|ogg|ogv|webm|htc|xml|woff)$ {
        access_log off;
        add_header Cache-Control "public,max-age=30*24*3600";
    }
}
4.如需进一步修改前端，请在/home/sub-web-modify下执行 yarn serve 进行调试即可
