---
layout: post
title:  "Linux下centos忘记密码，提示‘鉴定错误’"
date:   2016-05-22 04:10:03 +0700
categories: [python, codefights]
---

1. 重启，在读秒的界面按键盘的上下选择键；
2. 在此界面上按“e”键，出现界面；
3. 选择界面中类似kernel开头的第二项；
4. 在此按“e”键，出现界面：
5. 键盘输入：kernel/boot/vmlinuz-2.4.18-14 single ro root=LABEL=/
  - vmlinuz的版本以3中的显示为准；
  - 按回车键，返回界面；
6. 到此你就可以按“b”键了；
7. 在新出现的界面输入：passwd root
8. 重置密码；
9. 再输入（重启，并以root身份登录）：#reboot
