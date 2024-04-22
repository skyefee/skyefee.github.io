下载
 `//从10.10.10.10机器上/opt/soft下载nginx-0.5.38.tar.gz文件到本地/opt/soft/目录中。`
`scp root@10.10.10.10:/opt/soft/nginx-0.5.38.tar.gz /opt/soft/`

上传
`//上传本地目录到远程机器指定目录`
`scp -r /opt/soft/mongodb root@10.10.10.10:/opt/soft/scptest`