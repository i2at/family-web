# 一、环境搭建

1. ## 切换淘宝镜像：

  ```bash
  npm install -g cnpm --registry=https://registry.npm.taobao.org
  ```

2. ## 以管理员权限运行cmd

3. ## 安装依赖：

  ```bash
  cnpm  install
  ```

4. ## 如果报错，执行下面命令，然后 cnpm install再安装：

  ```bash
  npm install --save node-sass --registry=https://registry.npm.taobao.org --disturl=https://npm.taobao.org/dist --sass-binary-site=http://npm.taobao.org/mirrors/node-sass
  ```

5. ## 如果之前安装失败，先清理缓存：

  ```bash
  npm rebuild node-sass
  npm uninstall node-sass
  ```

**日期：2022/3/31**

------



# 二、前后端调试

1、修改请求网关地址

```vue
/**
 * 开发环境
 */
;(function () {
  window.SITE_CONFIG = {};

  // api接口请求地址
  window.SITE_CONFIG['baseUrl'] = 'http://localhost:88/api';

  // cdn地址 = 域名 + 版本号
  window.SITE_CONFIG['domain']  = './'; // 域名
  window.SITE_CONFIG['version'] = '';   // 版本号(年月日时分)
  window.SITE_CONFIG['cdnUrl']  = window.SITE_CONFIG.domain + window.SITE_CONFIG.version;
})();
```

2、基础服务

- 创建基础管理模块
- 前后端调试
- 完善方式管理、账号管理细节信息。
- 修改版式。

![](https://cdn.jsdelivr.net/gh/willxwu/CDN@main/images/202204041737051.png)



3、新建成员管理微服务

- 处理校验、日期时间、性别枚举、版式等等细节问题。

![](https://cdn.jsdelivr.net/gh/willxwu/CDN@main/images/202204042123909.png)

**日期：2022/4/5**

------

