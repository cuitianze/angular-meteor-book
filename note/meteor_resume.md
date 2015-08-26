## 基于Meteor官网教程改进版
- （完成个人简历系统，将比官网上的demo更有成就感）



## 创建应用
- `meteor create resume-system` 创建Meteor项目
- `cd resume-system` 进入项目根目录
- `meteor` 安装Meteor依赖包
- 不妨打开http://localhost:3000看看app的运行吧
- `rm -rf *` 删除原始生成文件

## 在模板中定义视图
- `meteor add urigo:angular` 安装angular-meteor package
- 主体html,使用ng-include指令引入模板**特别要小心哦,双引号里面还有单引号哦，相当于一个解析式。
```
<head>
    <title>银河系最酷炫狂拽叼炸天的简历系统</title>
</head>
<body ng-app="resume" ng-include="'addResume.ng.html'" ng-controller="addResumeController">
</body>
```
- 新建ng模板。模板的名字也要以.ng.html为后缀，这样就不会把文件中的{{}}解析为Blaze模板，而会作为Angular的模板。
```
<div class="container">
    <header>
        <h1>我的简历</h1>
    </header>

    <ul ng-repeat="person in persons">
        <li>{{person.name}}</li>
        <li>{{person.hobby}}</li>
    </ul>
</div>
```


