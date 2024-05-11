maven添加本地jar到仓库

```
mvn install:install-file -Dfile=D:\zzg\dev\atg-sdk-java-RELEASE20210526122214.jar -DgroupId=com.alibaba -DartifactId=atg-sdk-java -Dversion=RELEASE20210526122214 -Dpackaging=jar
```


对应下面的

```
<dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>atg-sdk-java</artifactId>
   <version>RELEASE20210526122214</version>
</dependency>
```