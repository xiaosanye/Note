#  okHttp

在Retrofit中，无论是发送数据和接收数据，都是通过OKHttp的RequestBody和ResponseBody来实现的。在实际项目中，有时候原始的RequestBody或是ResponseBody并不能满足我们的需求（如接口加密），就需要对它进行转换。

在Retrofit通过build()方法获得实例时，可以添加多个ConverterFactory，但要注意的是，添加的顺序是有影响的。

按照retrofit的逻辑，是从前往后进行匹配，如果匹配上，就忽略后面的，直接使用。

