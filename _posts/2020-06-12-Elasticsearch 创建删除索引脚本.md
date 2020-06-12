## shell 脚本，批量添加与删除索引
- 复制内容，新建文件`es.sh`粘贴进去，修改`es_http_url`的值为`网关http地址`
- 添加文件执行权限`chmod +x es.sh`
- 创建当日索引，./es.sh 0
- 创建昨天索引，./es.sh -1

```bash

#!/bin/bash
echo ....$(date +"%Y-%m-%d")定时任务开始....
es_http_url=http://192.168.1.1:9200
# 第2个参数为es访问地址，需带http/https
if [[ ${2} != "" ]]
then
  es_http_url=${2}
fi

createFun(){
  # 创建索引，默认创建第二天的索引，命令行第1个参数为0时创建今天的索引，命令行第1个参数为n时创建n天后的索引
  day=$(date -d "1 days" +%Y_%m_%d)
  if [[ ${1} != "" ]]
  then
    day=$(date -d "${1} days" +%Y_%m_%d)
  fi
  
  createIndexFun demo1_$day '{"index_patterns":["demo1_*"],"settings":{"index.number_of_shards":"4","index.number_of_replicas":"1","refresh_interval":"30s"},"mappings":{"demo":{"properties":{"field1":{"type":"long"},"field2":{"type":"keyword"},"field3":{"type":"text"},"field4":{"type":"integer"}}}}}'
  createIndexFun demo2_$day '{"index_patterns":["demo2_*"],"settings":{"index.number_of_shards":"4","index.number_of_replicas":"1","refresh_interval":"30s"},"mappings":{"demo":{"properties":{"field1":{"type":"long"},"field2":{"type":"keyword"},"field3":{"type":"text"},"field4":{"type":"integer"}}}}}'
  createIndexFun demo3_$day '{"index_patterns":["demo3_*"],"settings":{"index.number_of_shards":"4","index.number_of_replicas":"1","refresh_interval":"30s"},"mappings":{"demo":{"properties":{"field1":{"type":"long"},"field2":{"type":"keyword"},"field3":{"type":"text"},"field4":{"type":"integer"}}}}}'
  createIndexFun demon_$day '{"index_patterns":["demon_*"],"settings":{"index.number_of_shards":"4","index.number_of_replicas":"1","refresh_interval":"30s"},"mappings":{"demo":{"properties":{"field1":{"type":"long"},"field2":{"type":"keyword"},"field3":{"type":"text"},"field4":{"type":"integer"}}}}}'
}

createIndexFun(){
  index=${1}
  data=${2}
  isExist=$(curl $es_http_url/$index)
  if [[ $(echo $isExist | grep "index_not_found_exception") == "" ]]
  then
     echo 索引$index已经创建，无需重复创建
  else
      echo 创建索引 $index 开始
      createIndex=$(curl -XPUT  $es_http_url/$index?pretty -H 'Content-type':'application/json' -d$data)
      if [[ $(echo createIndex | grep "error") != "" ]]
      then
          echo 创建索引 $index 失败，createIndex
      else
          echo 创建索引 $index 成功
      fi
  fi
}

deleteFun(){
  # 默认删除365天前的索引
  day=$(date -d "365 days ago" +%Y_%m_%d)
  if [[ ${1} != "" ]]
  then
    day=$(date -d "${1} days ago" +%Y_%m_%d)
  fi
  
  deleteIndexFun demo1_$day
  deleteIndexFun demo2_$day
  deleteIndexFun demo3_$day
  deleteIndexFun demon_$day
}

deleteIndexFun(){
  index=${1}
  echo 删除索引 $index 开始
  deleteIndex=$(curl -XDELETE  $es_http_url/$index)
  if [[ $(echo $deleteIndex | grep "error") != "" ]]
  then
      echo 删除索引 $index 失败，$deleteIndex
  else
      echo 删除索引 $index 成功
  fi
}

# 第1个参数为创建${1}天后的索引
param1=""
if [[ ${1} != "" ]]
  then
    param1=${1}
  fi
createFun $param1
deleteFun

```
