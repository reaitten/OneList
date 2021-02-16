# OneDriveUploader - Written in GoLang
- Support International Edition, Personal Edition (Home Edition), China Edition (21Vianet).
- Support uploading files and folders to the specified directory, and maintain the directory structure before uploading.
- Support the use of command parameters to facilitate the call of external programs.
- Support custom upload block size.
- Support multi-thread upload (multiple files upload at the same time).
- Supports dynamic adjustment of the number of retries based on file size
- Support skipping files with the same name that already exist in the network disk.

## Authorization
### Log in through the URL below (right click to open a new tab)
#### International Edition, Personal Edition (Home Edition)
[https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=78d4dc35-7e46-42c6-9023-2d39314433a5&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All](https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=78d4dc35-7e46-42c6-9023-2d39314433a5&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All)
#### China Version (21Vianet)
[https://login.chinacloudapi.cn/common/oauth2/v2.0/authorize?client_id=dfe36e60-6133-48cf-869f-4d15b8354769&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All](https://login.chinacloudapi.cn/common/oauth2/v2.0/authorize?client_id=dfe36e60-6133-48cf-869f-4d15b8354769&response_type=code&redirect_uri=http://localhost/onedrive-login&response_mode=query&scope=offline_access%20User.Read%20Files.ReadWrite.All)

### Initialize the configuration file
```
# International Edition
OneDriveUploader -a "url"
# Personal Edition (Home Edition)
OneDriveUploader -ms -a "url"
# China Version (21Vianet)
OneDriveUploader -cn -a "url"

# Get the entire url content starting with http://loaclhost in the browser address bar
# Replace the obtained full url content with the three letters url in the command
# Each generated url can only be used once, please try again and get the url again
# This operation will automatically initialize the configuration file
# Prompt Init config file: '/path/to/auth.json' to succeed
```

## Usage
```
Usage of OneDriveUploader:
  -a string
        // Initialize authorization
        Setup and Init auth.json.
  -b string
        // Custom upload block size can improve network throughput, which is limited by disk performance and network speed.
        Set block size. [Unit: M; 5<=b<=60;] (default "10")
  -c string
        // Configuration file path
        Config file. (default "auth.json")
  -n string
        // When uploading a single file, rename it in the network disk
        Rename file on upload to remote.
  -r string
        // Upload to a directory in the network disk, default: root directory
        Upload to reomte path.
  -s string
        // *Required parameters, file or folder to upload
        Upload item.
  -t string
        // Number of threads, number of files uploaded at the same time. Default: 2
        Set thread num. (default "2")
  -f
        // switch (recommended)
        // Add the -f parameter to force reading the block size configuration and multi-thread configuration in auth.json.
        // Without the -f parameter, every time the current parameters are overwritten and saved to the auth.json configuration file.
        Force Read config form config file. [BlockSize, ThreadNum]
  -skip
        // switch
        // Skip uploading the file with the same name that already exists in the network disk. (The default is not skipped)
        Skip exist file on remote.
  -cn
        // switch
        // Authorize the Chinese version (21Vianet), this parameter is required.
        OneDrive by 21Vianet.
  -ms
        // switch
        // Authorized personal edition (home edition), this parameter is required.
        OneDrive by Microsoft.
```

## Configuration
```
{
     // authorization token
     "RefreshToken": "1234564567890ABCDEF",
     // Maximum number of threads. (Number of files uploaded at the same time)
     "ThreadNum": "2",
     // Maximum upload block size. (The maximum block size of each uploaded file. It is recommended to lower it if the network is not good. Unit: MB)
     "BlockSize": "10",
     // Maximum single file size. (Currently: the single file limit for the personal version (home version) is 100GB; the single file limit for other versions is 15GB, and Microsoft will gradually update it to 100GB. Unit: GB)
     "SigleFile": "100",
     // Cache refresh interval.
     "RefreshInterval": 1500,
     // If it is the Chinese version (21Vianet), this item should be true.
     "MainLand": false,
     // If it is a home version or a personal free version, this item should be true.
     "MSAccount": true
}
```

## 示例
```
# 一些示例:
# 将同目录下的 mm00.jpg 文件上传到 OneDrive 网盘根目录
OneDriveUploader -s "mm00.jpg"

# 将同目录下的 mm00.jpg 文件上传到 OneDrive 网盘根目录,并改名为 mm01.jpg
OneDriveUploader -s "mm00.jpg" -n "mm01.jpg"

# 将同目录下的 Download 文件夹上传到 OneDrive 网盘根目录
OneDriveUploader -s "Download" 

# 将同目录下的 Download 文件夹上传到 OneDrive 网盘Test目录中
OneDriveUploader -s "Download" -r "Test"

# 将同目录下的 Download 文件夹上传到 OneDrive 网盘Test目录中, 使用 10 线程
OneDriveUploader -t 10 -s "Download" -r "Test"

# 将同目录下的 Download 文件夹上传到 OneDrive 网盘Test目录中, 使用 15 线程, 并设置分块大小为 20M
OneDriveUploader -t 15 -b 20 -s "Download" -r "Test"

# 将同目录下的 Download 文件夹上传到 OneDrive 网盘Test目录中, 使用配置文件中的线程参数和分块大小参数
OneDriveUploader -f -c "/urs/local/auth.json" -s "Download" -r "Test"

# 将同目录下的 Download 文件夹上传到 OneDrive 网盘Test目录中, 使用配置文件中的线程参数和分块大小参数，并跳过上传网盘中已存在的同名文件
OneDriveUploader -f -c "/urs/local/auth.json" -skip -s "Download" -r "Test"
```
## Note
-After multiple attempts, no failed upload files. The exit code is 0.
-In the end, the failed upload files will be listed in detail. The exit code is 1.

## Client/Secret (~ 2299/12/31)
```
# International Edition: 78d4dc35-7e46-42c6-9023-2d39314433a5| ZudGl-p.m=LMmr3VrKgAyOf-WevB3p50
# Chinese version: dfe36e60-6133-48cf-869f-4d15b8354769| H0-1:6.Sb8:WCW/J-c]K@fddCt[i0EZ2
```
