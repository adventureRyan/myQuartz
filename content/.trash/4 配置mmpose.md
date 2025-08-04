## No module named `mmcv._ext`
[参考](https://github.com/open-mmlab/mmpose/issues/3014)

原因：pytorch 版本必须是 2.1.0，不能是 2.2.0 或者其他更高的版本。
解决办法：卸载旧的版本，重新装上 pytorch == 2.1.0

```bash
pip uninstall torch torchvision torchaudio
pip install torch==2.1.0 torchvision==0.16.0 torchaudio==2.1.0
pip uninstall mmcv
pip install mmcv==2.1.0 -f https://download.openmmlab.com/mmcv/dist/cu121/torch2.1/index.html
```

##  No module named 'pip' 
当使用命令：`pip install chumpy`，出现报错： `No module named 'pip'`
[参考](https://github.com/mattloper/chumpy/issues/50#issuecomment-1647054414)

解决办法：
```bash
pip install wheel
```


