# RxJava使用
1.传统的异步

1.1 、 Handler、Message、MessageQueue 、Looper
>每一个线程只有一个**MessageQueue**对象，**Looper**是MessageQueue对象的**管家**

>Looper 重要方法：**loop()**

1.2 、使用AsyncTask
>