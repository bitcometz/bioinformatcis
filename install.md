# 目录
* [pip](#pip)
* [conda](#conda)

## pip
添加国内的源：
pip 后加参数 -i https://pypi.tuna.tsinghua.edu.cn/simple

永久使用：
Linux下：
修改 ~/.pip/pip.conf (没有就创建一个)， 修改 index-url至tuna，内容如下：
```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

## conda
conda源国内只有清华有，
修改源只需输入如下两行命令：
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
```
