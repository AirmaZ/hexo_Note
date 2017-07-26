---
title: 关于git提交时换行符冲突问题的解决办法
date: 2017-07-19 11:13:26
tags: other
categories: other
---

## 修改配置 ##
1. #### 修改git配置 ####
  - 打开cmd。
  - 输入`git config --global core.autocrlf input`(pull时不转换，push转换成unix换行符)
  - 输入`git config --global core.safecrlf true`（不允许提交包含混乱换行符的文件）
2. #### 修改IDE的换行符编码 ####
  - eclipse：
    + 打开`Windows -> Preference -> General -> workspace`，
    + 将`New text file line delimiter` 设置为 `other：unix`
  - idea和webstorm：
    + 打开`file-setting-Editor-code style`
    + 将`line separator`设置为`unix and OS X(\n)`.
  - 其他编辑器或者ide自行百度如何修改换行符编码
3. #### 检查git配置是否修改成功 ####
  - 输入`git config --global core.autocrlf`查看值是否为`input`
  - 输入`git config --global core.safecrlf`查看值是否为`true`

## 将目前的文件的换行符批量转换 ##

若修改配置后git不允许你commit，并提示`CRLF would be replaced by LF XXX`，则说明你当前的文件已经是windows和unix换行符乱用的情况了。则需要对文件进行批量换行符转换（以eclipse为例）：

1. 需要一个人pull最新的代码，然后进eclipse
2. 选择目录或者文件夹，然后点击`file-Convert Line Delimiters To`-`Unix`
3. 选择Select All将所有文件的换行符转换
4. commit所有文件并push到仓库。
5. 其他所有人删掉代码重新拉项目