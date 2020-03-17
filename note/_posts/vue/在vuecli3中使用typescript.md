### 在vuecli3中使用typescript

##### 问题一

 Could not find a declaration file for module 'vue-xxx'.

解决办法

找到shims-vue-d.ts文件

加上declare module 'vue-xxx'即可



##### 问题二

 完美解决Cannot download "https://github.com/sass/node-sass/releases/download/binding.nod的问题



 npm i node-sass --sass_binary_site=https://npm.taobao.org/mirrors/node-sass/

##### 问题三

Cannot find module 'vue'.

因为默认脚手架的tsconfig配置问题，

改为module:commonjs

##### 问题四

Parameter 'h' implicitly has an 'any' type.

或者

cannot use namespace 'VNode' as a type

可以把tsconfig中 strict改为false,或者设置问题三那一步即可。