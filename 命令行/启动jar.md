start.bat
```
@echo off
start javaw -jar -Xms512M -Xmx2048M xxx.jar  --spring.profiles.active=prod
exit
```


app.sh
```
#!/bin/sh
## chang here
SERVICE_DIR=.
SERVICE_NAME=jar名称
 
## java env
#export JRE_HOME=${JAVA_HOME}/jre

case $1 in
  start)
    procedure=`ps -ef | grep -w "${SERVICE_NAME}" |grep -w "java"| grep -v "grep" | awk '{print $2}'`
    if [ "${procedure}" = "" ];
    then
      echo "start ${SERVICE_NAME}..."
      exec nohup java -Xms512m -Xmx4096m -jar ${SERVICE_DIR}/${SERVICE_NAME}\.jar --spring.profiles.active=prod --server.port=8081 >${SERVICE_DIR}/log.log 2>&1 &
      echo "start success"
    else
      echo "${SERVICE_NAME} is start"
    fi
    ;;

  stop)
    procedure=`ps -ef | grep -w "${SERVICE_NAME}" |grep -w "java"| grep -v "grep" | awk '{print $2}'`
    if [ "${procedure}" = "" ];
    then
      echo "${SERVICE_NAME} is stop"
    else
      kill ${procedure}
      argprocedure=`ps -ef | grep -w "${SERVICE_NAME}" |grep -w "java"| grep -v "grep" | awk '{print $2}'`
			while [ "${argprocedure}" != "" ]; do
				echo "${SERVICE_NAME} is stoping..."
				sleep 2
				argprocedure=`ps -ef | grep -w "${SERVICE_NAME}" |grep -w "java"| grep -v "grep" | awk '{print $2}'`
			done;
			echo "${SERVICE_NAME} stop success"
		fi
		;;

  restart)
    $0 stop
    sleep 1
    $0 start
    ;;

  *)
    echo "usage: $0 [start|stop|restart]"
    ;;
esac
```