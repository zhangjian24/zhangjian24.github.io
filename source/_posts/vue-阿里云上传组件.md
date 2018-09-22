---
title: vue-阿里云上传组件
copyright: true
top: 0
date: 2018-09-16 16:45:00
tags:
 - vue
 - 组件
 - 上传
categories:
 - 技术
 - 前端
password:
---

- [vue中文文档][1]
- [elementui文档][2]
- [elementui源码][3]

- 复用`elementUI`的`el-upload`，并覆盖`http-request`方法，实现自定义的上传行为；
- 通过`computed`的属性带入初始链接；
- 通过`prop.sync`/`update:prop`，回传链接；
- 用html的`audio`标签自动获取音频时长;

 {% asset_img vue-code.png vue-code %}


[1]: https://cn.vuejs.org/v2/guide/
[2]: http://element.eleme.io/#/
[3]: https://github.com/ElemeFE/element
[4]: http://static.zybuluo.com/zhangjian24/h29h0hfiqesag9i08x2wbxvw/sp180524_223524.png