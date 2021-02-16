# Get started (beta, updating...)
## Python3 has many bugs and incomplete functions. It is recommended to use the [Written in Go](https://github.com/MoeClub/OneList/tree/master/Rewrite) version

## Required dependencies
```
# Install python3 by yourself
pip3 install tornado
```

## Log in through the URL below (right click to open a new tab)
[https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=78d4dc35-7e46-42c6-9023-2d39314433a5&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All](https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=78d4dc35-7e46-42c6-9023-2d39314433a5&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All)

## Initialize the configuration file
```
# 运行
python3 OneList.py

# Get the code field content in the browser address bar
# Paste and press enter, each code can only be used once
# This operation will automatically initialize the configuration file
```

## Custom profile
```
# config.json

{
    // OneDrive 中的某个需要列出的目录
    "RootPath": "/Document",
    // 网址中的子路径
    "SubPath": "/onedrive",
    // 目录刷新时间
    "FolderRefresh": 900,
    // 下载链接刷新时间
    "FileRefresh": 1200,
    // 认证令牌, 将会自动更新, 保持默认
    "RefreshToken": "",
    // 这个不用管, 保持默认
    "RedirectUri": "http://localhost/onedrive-login"
}
```

## Run
```
python3 app.py

# 默认监听 127.0.0.1:5288 , 可在 app.py 中自行更改.
```

## Show off (??)
[https://moeclub.org/onedrive/](https://moeclub.org/onedrive/)
