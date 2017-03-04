# 权限控制API
用于权限控制的API接口,支持RBAC权限控制,支持数据级（控制到行,列）权限控制.

# 介绍

以下讲到的类都是基于包:org.hswebframework.web.authorization

### 常用注解:
_点击名称,查看源代码注释获得使用说明_

| 注解名称       | 说明          | 
| ------------- |:-------------:| 
| [`@Authorize`](src/main/java/org/hswebframework/web/authorization/annotation/Authorize.java)    | RBAC方式权限控制注解 | 
| [`@RequiresExpression`](src/main/java/org/hswebframework/web/authorization/annotation/RequiresExpression.java)      | 表达式方式验证      | 
| [`@RequiresDataAccess`](src/main/java/org/hswebframework/web/authorization/annotation/RequiresDataAccess.java)      | 行级权限控制      | 
| [`@RequiresFieldAccess`](src/main/java/org/hswebframework/web/authorization/annotation/RequiresFieldAccess.java)      | 列级权限控制      | 

### 常用类
_点击名称,查看源代码注释获得使用说明_


| 类名       | 说明          | 
| ------------- |:-------------:| 
| [`Authorization`](src/main/java/org/hswebframework/web/authorization/Authorization.java)    | 用户的认证信息 | 
| [`AuthorizationHolder`](src/main/java/org/hswebframework/web/authorization/AuthorizationHolder.java)      | 用于获取当前登录用户的认证信息      | 


### Listener
api提供[AuthorizationListener](src/main/java/org/hswebframework/web/authorization/listener/AuthorizationListener.java)
来进行授权逻辑拓展，在授权前后执行可自定义的操作.如rsa解密帐号密码,验证码判断等。

默认事件列表():

| 类名       | 说明          | 
| ------------- |:-------------:| 
| [`AuthorizationDecodeEvent`](src/main/java/org/hswebframework/web/authorization/listener/event/AuthorizationDecodeEvent.java)    | 接收到请求参数时 | 
| [`AuthorizationBeforeEvent`](src/main/java/org/hswebframework/web/authorization/listener/event/AuthorizationBeforeEvent.java)      | 验证密码前触发      | 
| [`AuthorizationFailedEvent`](src/main/java/org/hswebframework/web/authorization/listener/event/AuthorizationFailedEvent.java)      | 授权验证失败时触发      | 
| [`AuthorizationSuccessEvent`](src/main/java/org/hswebframework/web/authorization/listener/event/AuthorizationSuccessEvent.java)      | 授权成功时触发      | 
| [`AuthorizationExitEvent`](src/main/java/org/hswebframework/web/authorization/listener/event/AuthorizationExitEvent.java)      | 用户注销时触发      | 

例子:

```java
@Component
public class CustomAuthorizationSuccessListener implements AuthorizationListener<AuthorizationSuccessEvent>{
        @Override
        public void on(AuthorizationSuccessEvent event) {
            Authorization authorization=event.getAuthorization();
            //....
            System.out.println(authorization.getUser().getName()+"登录啦");
        }
}
```