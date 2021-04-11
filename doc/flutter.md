## 使用镜像
```
# 打开文件

subl ~/.bash_profile

# 添加环境变量

# flutter镜像
#国内用户需要设置
export PUB_HOSTED_URL=https://pub.flutter-io.cn
#国内用户需要设置
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
export PATH=～/flutter/bin:$PATH

# 使用新环境变量

source ~/.bash_profile



rm -rf ~/Library/Developer/Xcode/DerivedData/ModuleCache

rm -rf ~/Library/Preferences/com.apple.Xcode.plist
```

## 基础命令
```
# 在指定目录下创建一个Flutter项目
flutter create <output directory>

# 查看设备列表
flutter devices

# 在指定设备下运行Flutter项目
flutter run [options]
# options
-h,–help  打印命令用法
-d,–device-id <driverId> 指定设备id运行, all 则对所有设备执行操作
-v,–verbose 打印版本信息
–suppress-analytics 阻止命令运行时分析报告

# 打包
flutter packages <command>
# command
cache     Work with the Pub system cache
get       获取packages
outdated  分析packages看看哪个是可以升级的
publish   发布当前packages到pub.dev网站
run       从package中运行可执行包
version       ZZZZ打印pub的版本
```