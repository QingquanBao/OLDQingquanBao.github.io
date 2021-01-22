# 远程服务器构建Jupyter lab

## 基本操作

1. 安装好Jupyter lab ：）

2. 生成密码，记得复制，类似'sha1:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

   ```python
   from notebook.auth import passwd 
   passwd()
   ```

3. 配置

   先在终端生成配置文件`jupyter notebook --generate-config` ，进行修改`$ vim ~/.jupyter/jupyter_notebook_config.py ` 。参数如下

   ```shell
   c.NotebookApp.allow_remote_access = True
   c.NotebookApp.open_browser = False
   c.NotebookApp.ip='*'
   c.NotebookApp.password = u'sha1:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
   c.NotebookApp.port =54010
   ```

4. 运行`jupyter lab` or `jupyter notebook` 

## 服务器指定接口进入

以上是在google就能搜索到的常规操作，但笔者的服务器需要在特定接口范围内才能连接，直接在浏览器打开`https://server_ip:54010` 根本不work。后来使用[ssh tunnel](https://www.zsythink.net/archives/2450)的方法解决了。

具体而言，在完成以上操作后，本地新开一个终端窗口，输入

` ssh -L 8886:localhost:54010 -N -T -p given_port name@server_ip`

其中8886是本地端口，届时可以通过`https:localhost:8886` 直接远程打开Jupyter Lab；`given_port `是服务器指定的公网接口。