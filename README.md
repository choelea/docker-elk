此仓库fork自https://github.com/deviantony/docker-elk， 具体文档细节参考原repository。 

## 前置条件
依赖一些软件:
 - git  安装 `yum install git`
 - docker  安装 `curl -fsSL get.docker.com -o get-docker.sh && sudo sh get-docker.sh`
 - docker-compose 安装 `curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`;
 - 开机启动Docker： `systemctl enable docker`
 - 启动docker： `systemctl start docker`
 - docker-compose 运行权限：`chmod +x /usr/local/bin/docker-compose`

## 下载
选择一个目录并进入目录，克隆此repo. (如果无法克隆，请手动上传。)

## 运行
进入docker-elk目录运行`docker-compose up`启动，大致会用到的命令如下：
 - `docker-compose up -d` 启动
 - `docker-compose up -d` 在后台启动
 - `docker-compose down` 关闭
 - `docker-compose down -v` 关闭并删除数据。 默认情况下，Elasticsearch数据保留在卷内。 为了完全关闭堆栈并删除所有持久数据，可以使用此命令


## 索引的生命周期管理
生命周期管理需要对应插件`curator` (extensions/curator). 启动curator的命令如下:

`docker-compose -f docker-compose.yml -f extensions/curator/curator-compose.yml up`。 

通过curator可以来按照指定规则删除历史索引数据；防止磁盘空间不够导致服务宕机。 主要有以下几个点需要配置：
 - 删除规则配置：`extensions/curator/config/delete_log_files_curator.yml`； 培训根据前缀过滤的前缀信息，默认是"logs-"
 - 配置`extensions/curator/curator-compose.yml`; 修改UNIT_COUNT 来设置保存多少天。

