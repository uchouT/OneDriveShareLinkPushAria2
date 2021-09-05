# OneDriveShareLinkPushAria2
Extract download URLs from OneDrive or SharePoint share links and push them to aria2, even on systems without a GUI.

从OneDrive或SharePoint共享链接提取下载URL并将其推送到aria2，即使在无图形界面的系统中依然可以使用。

# 依赖
requests==2.25.1

pyppeteer==0.2.5

# 特点
目前本程序支持的下载方式：
* xxx-my.sharepoint.com 下载链接的下载
  * 无下载密码的多文件推送
  * 有下载密码的多文件推送
  * 嵌套文件夹的文件推送
  * 任意选择文件推送
  * 多于30个文件列表的查看（下载方式规划中）
* xxx.sharepoint.com 下载链接的下载
* xxx-my.sharepoint.cn 下载链接的下载(理论上支持)

**注意：Aria2本身不支持HTTP POST型的下载链接，而OneDrive文件夹打包下载为HTTP POST型的下载链接，所以本程序将不会支持OneDrive文件夹打包下载**

## 无密码的链接

以 https://gitaccuacnz2-my.sharepoint.com/:f:/g/personal/mail_finderacg_com/EheQwACFhe9JuGUn4hlg9esBsKyk5jp9-Iz69kqzLLF5Xw?e=FG7SHh 这个下载链接为例

此时需要使用无密码的下载代码，也就是[main.py](../main.py)，打开这个文件，可以看到有一些全局变量：
* OneDriveShareURL: 下载地址，此处应该填写 https://gitaccuacnz2-my.sharepoint.com/:f:/g/personal/mail_finderacg_com/EheQwACFhe9JuGUn4hlg9esBsKyk5jp9-Iz69kqzLLF5Xw?e=FG7SHh
* aria2Link: aria2 的rpc地址，如果是本机，一般是 `http://localhost:端口号/jsonrpc`
* aria2Secret: aria2 的密码
* isDownload: 是否下载，如果是`False`，只输出文件列表
* downloadNum: 要下载的文件列表，-1表示全部下载

如果想要下载第二个文件，则需要`downloadNum="2"`

如果想要下载第二、第三个文件，则需要`downloadNum="2-3"`

如果想要下载第二、第三、第四、第七个文件，则需要`downloadNum="2-4,7"`

以此类推

修改好后，确保目标aria2处于开启状态，执行`python3 main.py`

## 有密码的链接


以 https://jia666-my.sharepoint.com/:f:/g/personal/1025_xkx_me/EsqNMFlDoyZKt-RGcsI1F2EB6AiQMBIpQM4Ka247KkyOQw?e=oC1y7r 这个下载链接为例

此时需要使用有密码的下载代码，也就是[havepassword.py](../havepassword.py)，打开这个文件，可以看到有一些全局变量（重复的不再赘述）：
* OneDriveSharePwd: OneDrive链接的密码
  
使用方法和上面类似。

# 注意
使用前，使用 `git clone https://github.com/gaowanliang/OneDriveShareLinkPushAria2.git` 将项目整个克隆，才能使用，havepassword.py依赖于main.py，如果要使用需要密码的版本，需要 `pip install pyppeteer`