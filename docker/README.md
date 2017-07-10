##### 存放各种docker image构建脚本或者快速启动的docker-compose文件。

##### 实现：一处构建，处处可用，方便健忘人士和减轻国内开发人员的负担。

-------

##### 这个库的作用？

1. 存放由于种种原因，导致官方image不好使，需要自己构建的docker image。
2. 存放使用过的应用的快速启动文件docker-compose。
3. 由于想在国内快速下载某些镜像，所以使用第三方构建平台创建镜像构建仓库，构建平台需要代码仓库。

### 注意事项

_一些compose内都是设置data挂载到本目录的，方便实现数据分离，但这些数据是忽略提交的，所以使时需要注意新建目录和给予权限。_