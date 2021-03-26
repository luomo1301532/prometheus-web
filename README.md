# prometheus-web
prometheus-web是一个将prometheus的配置文件可以进行api配置的插件，它遵循Resful风格。带给你全新的体验
## prometheus的困扰
prometheus是一个优秀的开源的服务监控系统和时间序列数据库，它被广泛应用在监控领域，他有完整的监控告警体系，却缺少对应的api。这使我不得不每次到服务器中修改它的配置文件，这体验真的很糟糕。prometheus-web因此而来，它将解决你在这些问题上的困扰
## 安装
### 1.jar包运行
你可以在发行版进行下载jar包

java -jar prometheus-web.jar --spring.profiles.active=prod --server.port=8091 --prometheus.rulesPath="/home/rules/" --prometheus.templatePath="/home/template" --prometheus.isCover=false --prometheus.isReload=true --prometheus.rulesPath="http://127.0.0.1:9090/-/reload"

参数说明

--spring.profiles.active 选择环境，这里选择生产环境运行就可。

--server.port 设置端口（默认为8091）

--prometheus.rulesPath 设置规则文件放置目录，即prometheus的告警规则存放目录（默认为/home/rules/）

--prometheus.templatePath 设置模板文件目录（默认为/home/template）

--prometheus.isCover 设置是否覆盖（默认false）

--prometheus.isReload 设置是否覆盖（默认true）

--prometheus.rulesPath 设置prometheus的热重启地址

### 2.docker运行
