<<<<<<< HEAD
[TOC]

# Retrofit


### Retrofit入门
### Retrofit注解详解
### Gson与Converter
### RxJava与CallAdapter
### 自定义Converter
### 自定义CallAdapter
### 其它说明

http://www.jianshu.com/p/5b8b1062866b

# Retrofit入门
## 1.1、创建Retrofit实例

```java
Retrofit retrofit = new Retrofit.Builder()
        .baseUrl("http://localhost:4567/")
        .build();
```
>创建Retrofit实例时需要通过Retrofit.Builder,并调用baseUrl方法设置URL。
注： Retrofit2 的baseUlr 必须以 /（斜线） 结束，不然会抛出一个IllegalArgumentException,所以如果你看到别的教程没有以 / 结束，那么多半是直接从Retrofit 1.X 照搬过来的。

## 1.2、接口定义
1.2、接口定义

以获取指定id的Blog为例:
```java
public interface BlogService {
    @GET("blog/{id}")
    Call<ResponseBody> getBlog(@Path("id") int id);
}
```
**注意，这里是interface不是class，所以我们是无法直接调用该方法，我们需要用Retrofit创建一个BlogService的代理对象。**
```java
BlogService service = retrofit.create(BlogService.class);
```
拿到代理对象之后，就可以调用该方法啦。

## 1.3、接口调用
```java
Call<ResponseBody> call = service.getBlog(2);
// 用法和OkHttp的call如出一辙,
// 不同的是如果是Android系统回调方法执行在主线程
call.enqueue(new Callback<ResponseBody>() {
    @Override
    public void onResponse(Call<ResponseBody> call, Response<ResponseBody> response) {
        try {
            System.out.println(response.body().string());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void onFailure(Call<ResponseBody> call, Throwable t) {
        t.printStackTrace();
    }
});

链接：http://www.jianshu.com/p/308f3c54abdd
來源：简书
```

>打印结果:
```json
{   "code":200,
    "msg":"OK",
    "data":{"id":2,
            "date":"2016-04-15 03:17:50",
            "author":"怪盗kidou",
            "title":"Retrofit2 测试2",
            "content":"这里是 Retrofit2 Demo 测试服务器2"
            },
    "count":0,
    "page":0}
```


[你真的会用Retrofit2吗?Retrofit2完全教程](http://www.jianshu.com/p/308f3c54abdd)

[你真的会用Gson吗?Gson使用指南](http://www.jianshu.com/p/e740196225a4)
