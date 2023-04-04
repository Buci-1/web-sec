# Java 调试环境搭建

## 0x00 准备

- IDEA

## 0x01 远程调试

### 1. Tomcat 远程调试

#### 远程Tomcat配置：    

**方案一**：   
在./bin/catalina.sh 中添加 address 调试端口 9090
```
CATALINA_OPTS="-server -Xdebug -Xnoagent -Djava.compiler=NONE -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=9090" 

```
或者是
```
JAVA_OPTS="-agentlib:jdwp=transport=dt_socket,address=9090,suspend=n,server=y"
```
**方案二**：


修改./bin/startup.sh，在最后一行exec语句中添加 jpda

```
exec "$PRGDIR"/"$EXECUTABLE" jpda start "$@"
```
监听的端口可以在./bin/catalina.sh中修改

```
if [ -z "$JPDA_ADDRESS" ]; then
 JPDA_ADDRESS="0.0.0.0:9090"
```

重启服务即可

### 2. Jar 远程调试
```
-agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=9090
-agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=*:9090  //jdk9+
```

### IDEA配置：
https://blog.51cto.com/u_15127502/3518074
