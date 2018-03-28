---
layout: post
title:  "js调整父层iframe的宽高"
date:   2016-07-06 04:10:03 +0700
categories: [python, codefights]
---

js控制上层iframe的属性，修改宽高为例。

```
    ///父层iframe
    <div id="game"><iframe width="300" height="600"></iframe></div>

    ///子层的js代码：获取父层宽高、修改父层宽高
    function parentIframe(type, width) {
        try {
            var gameId = window.parent.document.getElementById("game");
            var pIframe = gameId.getElementsByTagName('iframe')[0];

            if (type == 1) { ///set : 设置的宽度
            
                pIframe.width = width;
                pIframe.style.width = width + "px";
                
            } else { ///get ：获取宽度
                var w = parseInt(pIframe.style.width); ///先读去是否设置了style属性
                if (pIframe.style.width == "" || w < 0) {
                    w = pIframe.width; ///如果未设置style则取iframe的width属性
                }

                ///
                return w;
            }
        }
        catch (e) {
            //console.log(e);
            return 0;
        }
    }
    var pWidth = parentIframe();
    var timer = setInterval(function() {
        parentIframe();
    }, 50);
```
