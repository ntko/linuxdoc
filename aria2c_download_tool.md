### Aria2c下载工具使用举例
#### 官方文档
[aria2c commands options](https://aria2.github.io/manual/en/html/aria2c.html "aria2c commands options")    

#### 下载一个文件到download目录
    aria2c -d ./download "http://host/image.iso"

#### 用每个host两个连接下载文件
    aria2c -x2 http://host/image.iso

#### 同时使用两个连接下载同一文件
    aria2c -s2 http://host/image.iso http://mirror1/image.iso http://mirror2/image.iso

#### 复杂示例下载Magnet Bittorrent URL:(注意要使用引号引用URL)
    aria2c -d ./download -l log.txt --bt-save-metadata=true "magnet:?xt=urn:btih:54dca0477d74d88ed051a9cd62fe5359151e7823&dn=elementaryos-0.4.1-stable.20180214.iso"

#### 复杂示例下载2个Bittorrent File:
    aria2c aria2c -d H:\ubantusetup H:\ubantusetup\ubuntu-18.04-desktop-amd64.iso.torrent H:\ubantusetup\ubuntu-18.04-live-server-amd64.iso.torrent
