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
# Run
python3 OneList.py

# Get the code field content in the browser address bar
# Paste and press enter, each code can only be used once
# This operation will automatically initialize the configuration file
```

## Custom profile
```
# config.json

{
    // A directory in OneDrive that needs to be listed
     "RootPath": "/Document",
    // Sub path in URL
    "SubPath": "/onedrive",
    // Catalog refresh time
    "FolderRefresh": 900,
    // Download link refresh time
    "FileRefresh": 1200,
    // Authentication token, will be automatically updated, keep the default
    "RefreshToken": "",
    // Don't worry about this, keep the default
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
