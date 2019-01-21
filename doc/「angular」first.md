1. install
```bash
npm install -g @angular/cli
# 镜像安装
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm install
```

2. create
```bash
# 可以选择是否使用scss --style=scss
ng new my-app
# 设置默认样式格式
ng set default.styleExt scss
```

3. start
```bash
ng serve
# 或
npm start
```

4. build
```bash
ng build
# 或
npm build
```

5. 服务端渲染
[服务端渲染](https://www.cnblogs.com/laixiangran/p/8664480.html)

### 添加AppRoutingModule
```bash
ng generate module app-routing --flat --module=app
```

### 创建
```bash
# 组件
ng generate component [name]
ng g c [name]
# 服务 可以写路径放到对应文件夹
ng generate service [name] 
ng g s [name]
# 
```

## 架构

### （模块 NgModule module

#### @NgModule 元数据

---

##### NgModule metadata

* declarations（可声明对象表） —— 那些属于本 NgModule 的组件、指令、管道。

* exports（导出表） —— 那些能在其它模块的组件模板中使用的可声明对象的子集。

* imports（导入表） —— 那些导出了本模块中的组件模板所需的类的其它模块。

* providers —— 本模块向全局服务中贡献的那些服务的创建器。 这些服务能被本应用中的任何部分使用。（你也可以在组件级别指定服务提供商，这通常是首选方式。）

* bootstrap —— 应用的主视图，称为根组件。它是应用中所有其它视图的宿主。只有根模块才应该设置这个 bootstrap 属性。

`src/app/app.module.ts`
``` typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

`bind`  
```
          事件绑定
     (event) = "handler"      C
   ----------------------->   O
          属性绑定             M
D    [property] = "value"     P
O  <-----------------------   O
M         插值表达式            N
        {{value}}             E
   <-----------------------   N
        双向数据绑定            T
   [(ng-model)] = "property"  
   <---------------------->   
                              
```