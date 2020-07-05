### ubuntu

安装时，不要插网线，不要选更新，不然速度慢

装好后，设置，关于，更换阿里云软件源

卸载ubuntu sorftware center

```
sudo apt autoremove --purge snapd
```

安装新立德（ubuntu包管理工具）

```
sudo apt-get install synaptic
```



##### 来回安装系统报错invalid partition table

del 进入主板bios

f7 +回车 进入高级模式

system里选择下语言

启动里找到 Hard Drive BBS Priorities

选择一下盘符的启动顺序，然后回到首页，f10保存退出

