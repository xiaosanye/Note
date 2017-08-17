[IOC]


# Retrofit2.0
## 异常信息
>Caused by: java.io.EOFException: End of input at line 1 column

>当出现以上异常时(这时指使用GsonConvertFactory进行解析json数据),并且请求结果无响应体body仅需要响应码时,很有可能就是因为gson解析出错导致的异常.

### 解决方案 

>**Retrofit是允许添加多个ConvertFactory的,也就是解析器.只需要自定义一个无响应体类型的解析器**

    创建一个无响应体类型NoBodyEntity,这个是必须的,
    因为Retrofit中的定义接口时Call是必须填入一个类型的.(不能使用Object)
    创建一个NoBodyConvertFactory用于解析返回类型是NoBodyEntity的response,
    实际上这里就是自己处理无响应体的response.
    最后快乐地使用response里的statusCode就可以了,可以忽略你不需要的响应体(本来也没有)

>**NoBodyEntity**
``` java
public class NoBodyEntity {
}
```

>**NoBodyConvertFactory**
``` java
/**
 * 代替gson converter转换无响应体的response
 */
public static class NobodyConverterFactory extends Converter.Factory {

    public static final NobodyConverterFactory create() {
        return new NobodyConverterFactory();
    }

    private NobodyConverterFactory() {
    }

    //将响应对象responseBody转成目标类型对象(也就是Call里给定的类型)
    @Override
    public Converter<ResponseBody, ?> responseBodyConverter(Type type, Annotation[] annotations,
                                                            Retrofit retrofit) {
        //判断当前的类型是否是我们需要处理的类型
        if (NoBodyEntity.class.equals(type)) {
            //是则创建一个Converter返回转换数据
            return new Converter<ResponseBody, NoBodyEntity>() {
                @Override
                public NoBodyEntity convert(ResponseBody value) throws IOException {
                    //这里直接返回null是因为我们不需要使用到响应体,本来也没有响应体.
                    //返回的对象会存到response.body()里.
                    return null;
                }
            };
        }
        return null;
    }

    //其它两个方法我们不需要使用到.所以不需要重写.
    @Override
    public Converter<?, RequestBody> requestBodyConverter(Type type,
                                                          Annotation[] parameterAnnotations, Annotation[] methodAnnotations, Retrofit retrofit) {
        return null;
    }

    @Override
    public Converter<?, String> stringConverter(Type type, Annotation[] annotations,
                                                Retrofit retrofit) {
        return null;
    }
}


```


### CSDN ：【一叶飘舟】
## [一、Retrofit Gson解析空字符串的问题](http://blog.csdn.net/jdsjlzx/article/details/51566536)








##  Retrofit请求数据对错误以及网络异常的处理
Retrofit本身会抛出HttpException，Gson解析会抛出解析异常。
