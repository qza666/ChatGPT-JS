**是个人就可以看会的ChatGPT镜像站内置脚本的教程**
第一次写，所以勉强看看吧

打开你自己的镜像网站聊天界面，按F12,查看运行的JS文件
![image](https://github.com/qza666/ChatGPT-JS/assets/158817429/b4e5ad5f-6a05-4065-a84a-92dbb86f2a1f)
可以看到我这运行了两个js文件，记住其中一个的名字

访问它，访问方法：域名/文件名称
比如https://cs.com/list.js

复制它的内容，然后打开SSH工具，链接你的服务器
在服务器的root/下创建你刚刚打开的那个js文件
比如我创建的则是：root/list.js

然后打开你创建的文件
粘贴你刚刚复制的代码
然后再复制下面的代码，粘贴在最上面，保存关闭
```
async function loadAndExecuteScripts(urls) {
  for (let url of urls) {
    try {
      const response = await fetch(url);
      const script = await response.text();
      eval(script);
      console.log(`成功执行: ${url}`);
    } catch (error) {
      console.error(`在加载或执行脚本 ${url} 时发生错误:`, error);
    }
  }
}

(async function() {
  await loadAndExecuteScripts([
    'https://raw.githubusercontent.com/qza666/ChatGPT-JS/main/vue.global.prod.js',
    'https://raw.githubusercontent.com/qza666/ChatGPT-JS/main/ChatGPT.js'
  ]);

```

现在运行查看正在运行的Docker容器

```
docker ps
```
找到你网站的容器，比如我的是chatgpt-share-server

然后进入容器，进入命令可以将你docker ps的结果发给GPT，问问它
进入容器后记住下面这两个命令，ls是打印当前路径的所有文件
cd是进入文件夹
```
ls xx
cd xx
```
找到你网站的那个js文件，并记住文件的路径
我的是在app/resource/public/list.js
然后问GPT，我进入容器的命令是xxxxxxx，我现在需要将cd /路径的root/xxx.js挂载到容器的/app/resource/public/list.js（改为你的路径），我应该执行什么命令
GPT会告诉你怎么挂载，与挂载后的重启命令
你可以打开网站查看是否成功，比如https://cs.com/list.js（记得多刷新两下网页）
确定js文件修改成功了，就删除xx.js直接访问你的网站，如果有缓存，你可以使用访问浏览器打开试试

**命令我忘记了，所以你们问问GPT，抱歉抱歉**






