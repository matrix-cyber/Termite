---
name :  Termite 用法
---

# Usage

1. 以服务模式启动一个agent服务。

> $ ./agent -l 8888

2. 令管理端连接到agent并对agent进行管理。

> $ ./admin -c 127.0.0.1 -p 8888

3. 此时，admin端会得到一个内置的shell, 输入help指令可以得到帮助信息。

>> help

4. 通过show指令可以得到当前agent的拓扑情况。

>> show 
 0M
 +-- 1M
 由于当前拓扑中只有一个agent，所以展示结果只有 1M ,
  其中1 为节点的ID号，
  M为MacOS系统的简写，Linux为L，Windows简写为W。

5. 将新agent加入当前拓扑
> ./agent -c 127.0.0.1 -p 8888

6. 此时show指令将得到如下效果
 0M
 +-- 1M
 |   +-- 2M
  这表明，当前拓扑中有两个节点，其中由于2节点需要通过1节点才能访问，所以下挂在1节点下方。

7. 在2节点开启socks代理，并绑定在本地端口
>> goto 2
    将当前被管理节点切换为 2 号节点。
>> socks 1080
   此时，本地1080 端口会启动个监听服务，而服务提供者为2号节点。

8. 在1号节点开启一个shell并绑定到本地端口
>> goto 1
>> shell 7777
     此时，通过nc本地的 7777 端口，就可以得到一个 1 节点提供的 shell.

9. 将远程的文件下载至本地
>> goto 1
>> downfile 1.txt 2.txt
    将1 节点，目录下的 1.txt 下载至本地，并命名为2.txt

10. 上传文件至远程节点
>> goto 2
>> upfile 2.txt 3.txt
    将本地的 2.txt 上传至 2号节点的目录，并命名为3.txt

11. 端口转接
>> goto 2 
>> lcxtran 3388 10.0.0.1 3389
    以2号节点为跳板，将 10.0.0.1 的 3389 端口映射至本地的 3388 端口


# 更多支持
    http://rootkiter.com/toolvideo/toolmp4/1maintalk.mp4
    http://rootkiter.com/toolvideo/toolmp4/2socks.mp4
    http://rootkiter.com/toolvideo/toolmp4/3lcxtran.mp4
    http://rootkiter.com/toolvideo/toolmp4/4shell.mp4
    http://rootkiter.com/toolvideo/toolmp4/5file.mp4

# 联系作者
    rootkiter@rootkiter.com
