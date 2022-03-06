### <font size=3pt face="MV Boli" color="gray">By [码哥字节](https://mp.weixin.qq.com/s/2UiT-MVLIhnkdntmd6-Hjw)</font>

- 显示当前HEAD上的最近一次提交：
```git show```

- 修改commit message：
```git commit --amenf --only -m 'xxxxxx'```

- 意外做了一次hard reset，想找回内容
```git reflog```
然后从commit列表里```git reset --hard SHA1234```