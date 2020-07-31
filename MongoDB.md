# 目录
* [安装](#安装)
    ** [安装mongodb](#安装mongodb)
    ** [安装pymongo](#安装pymongo)
* [设置](#设置)
* [例子](#例子)


## 安装


### 安装mongodb
用conda安装：
```
conda install -c anaconda mongodb
```
不建议的做法：把MongoDB的路径加入到PATH中
export PATH=/usr/local/mongodb/bin:$PATH

可以采取source的方法：
```
source activate /ifs/TJPROJ3/HWUS/USER/zhangjinbo/00.pipelines/00.conda/envs/mongodb_env
```
### 安装pymongo
类似我们最好是用python来操作数据库，因此需要先安装pymongo
```
pip3 install pymongo
```
天津集群的这个python3安装好了：
```
/ifs/TJPROJ3/HWUS/USER/zhangjinbo/00.pipelines/01.software/miniconda3/bin/python3
```

## 设置
配置存放个数据库存储目录
先创立一个文件：`/your_path/mongo.cfg`, 写入下面内容, 注意data到这个目录事先建立好
```
dbpath=/your_path/data
port=2009
```

然后执行：
```
mongod -f /your_path/mongo.cfg
```


## 例子

```python
import pymongo
## 链接数据库
client = pymongo.MongoClient(host='localhost', port=2009) ## 根据自己的端口设置

## 创立数据库，类似可以建micor_hw
db = client['my_database']
## 指定集合, 类似表格, 类似可以建16S, reseq
collection = db['students']
## 类似地只要我们再流程或者小脚本把项目的相关信息存储成类似地json文件即可加入到数据库里面
student = {
    'id': '20170101',
    'name': 'Jordan',
    'age': 20,
    'gender': 'male'
}
student1 = {
    'id': '20170101',
    'name': 'Mike',
    'age': 20,
    'gender': 'male'
}

student2 = {
    'id': '20170202',
    'name': 'Caven',
    'age': 21,
    'gender': 'male'
}
## 插入一个值
result = collection.insert_one(student)

## 插入多个值
result = collection.insert_many([student1, student2])
print(result)
print(result.inserted_ids)


## 查询
if collection.count_documents({'age': 20}) != 0:
    ## 多少个条目
    count = collection.count_documents({'age': 20})
    print('count:'+str(count))
    
    results = collection.find({'age': 20})
    print(results)
    for result in results:
        print(result)


## 删除
print('删除操作')
result = collection.delete_many({'name': 'Jordan'})
result = collection.delete_many({'name':  'Mike'})
result = collection.delete_many({'name':  'Caven'})


## 再次遍历所有
for i in collection.find():
    print(i)
```
