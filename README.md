# prometheus-web
prometheus-web是一个将prometheus的配置文件可以进行api配置的插件，它遵循Resful风格。带给你全新的体验
## prometheus的困扰
prometheus是一个优秀的开源的服务监控系统和时间序列数据库，它被广泛应用在监控领域，他有完整的监控告警体系，却缺少对应的api。这使我不得不每次到服务器中修改它的配置文件，这体验真的很糟糕。prometheus-web因此而来，它将解决你在这些问题上的困扰
## 安装
### 1.jar包运行
#### 你可以在发行版进行下载jar包

java -jar prometheus-web.jar --spring.profiles.active=prod --server.port=8091 --prometheus.rulesPath="/home/rules/" --prometheus.templatePath="/home/template" --prometheus.isCover=false --prometheus.isReload=true --prometheus.rulesPath="http://127.0.0.1:9090/-/reload"

#### 参数说明

--spring.profiles.active 选择环境，这里选择生产环境运行就可。

--server.port 设置端口（默认为8091）

--prometheus.rulesPath 设置规则文件放置目录，即prometheus的告警规则存放目录（默认为/home/rules/）

--prometheus.templatePath 设置模板文件目录（默认为/home/template）

--prometheus.isCover 设置是否覆盖（默认false）

--prometheus.isReload 设置是否自动热重启（默认true）

--prometheus.rulesPath 设置prometheus的热重启地址

### 2.docker运行
docker run -p 8091:8091 -v （prometheus的告警规则存放目录）:/home/rules -v （模板文件目录）:/home/template --name prometheus-web -e "IS_COVER=（是否覆盖）" -e "RELOAD_URL=（prometheus的热重启地址）"  -e "IS_RELOAD=（是否自动热重启）" -d registry.cn-hangzhou.aliyuncs.com/lzqhh/prometheus-web:v1.0

## 使用
### 1.添加规则

![image](https://user-images.githubusercontent.com/48502494/112595173-ff796c00-8e44-11eb-84b6-531d91c2a1bf.png)
![image](https://user-images.githubusercontent.com/48502494/112595353-45cecb00-8e45-11eb-8e16-12efddcbb800.png)

添加规则时，必要传参id和templateName，id是你在规则中的唯一标识，templateName是你的模板文件名，如上图，其它字段与你的模板内容一一对应即可生成相应规则，模板的功能强大，像上图它可以根据list生成多条规则，你可以自由的定制。（模板文件需要放在你设置的模板文件目录内）（注意如果你没有开启覆盖，当id相同时会提示id冲突错误，当开启覆盖后，id相同，会覆盖之前配置的规则）（如果你没有开启自动热启动，项目不会自动热启动使规则生效，你需要自己热启动prometheus使之生效）

### 2.修改规则

![image](https://user-images.githubusercontent.com/48502494/112596323-9e529800-8e46-11eb-8f86-93b561ced6dd.png)

修改规则时，必要传参id和templateName。同添加规则。它会根据id来修改配置规则。

### 3.删除规则

![image](https://user-images.githubusercontent.com/48502494/112596739-2cc71980-8e47-11eb-8342-523f6a1205e0.png)

删除规则时/{idList},支持批量删除，但不建议你这么做，因为它不具备事件回滚功能。

## 感谢支持
如果你觉得prometheus解决了你的问题，请给一个星，感谢您的支持。当星到1k时，我将开源源码。有任何问题请给我留言。
