---
layout: post
title:  "linuz下centos忘记密码提示‘鉴定错误’解决方案"
date:   2016-05-22 04:10:03 +0700
categories: [python, codefights]
---

1. 重启centos系统，在读秒的界面按键盘的上下选择键；
2. 出现界面，在此界面上按“e”键；
3. 出现界面，选择界面中的类似kernel开头的第二项的项目；
4. 出现界面，在此按“e”键，出现下面的画面：
5. 键盘输入（其实是加入“single”）：
  - 例：kernel/boot/vmlinuz-2.4.18-14 single ro root=LABEL=/
  vmlinuz根据上一界面的第二项版本为准
6. 按回车键，返回界面；
7. 到此你就可以按“b”键了；
8. shell界面打开后，在后面输入（重置密码）：passwd root
9. 回车，就重新输入新密码。密码是看不见的。
10. 再输入（重启系统）：#reboot
