### 建立一个django项目

- 查看 python版本

​		`python --version`或者python -V

- 进入到项目文件夹中，创建虚拟环境

  `python -m venv env`

- 激活虚拟环境

  `env\Scripts\activate.bat`

- 安装django

  `pip install django`

- 创建自己的项目

  `django-admin startproject my_chatbot`

- 进入到`my_chatbot`文件夹，运行服务

  `python manage.py runserver`

- 创建一个app

  `python manage.py startapp mychat`

- 注册app

  在settings.py中`INSTALLED_APPS`中注册

### django解决跨域问题

1. 安装django-cors-headers

   pip install django-cors-headers

2. INSTALLED_APPS 中添加 corsheaders

3. MIDDLEWARE 中添加 corsheaders.middleware.CorsMiddleware

​           位置尽量靠前，官方建议 ‘django.middleware.common.CommonMiddleware’ 上方

4. CORS_ORIGIN_ALLOW_ALL =Trus 布尔值  如果为True 白名单不启用
5. CORS_ALLOW_METHODS = (
       'DELETE',
       'GET',
       'OPTIONS',
       'PATCH',
       'POST',
       'PUT',
       )
6. CORS_ALLOW_HEADERS = (
          'accept-encoding',
          'authorization',
          'content-type',
          'dnt',
          'origin',
          'user-agent',
          'x-csrftoken',
          'x-requested-with',
      )



### JWT(Json Web Token)

特点：

- 可以通过 URL, POST 参数或者在 HTTP header 发送，因此数据量小，传输速度快。
- 严格的结构化。它自身(在 payload 中)就包含了所有与用户相关的验证消息，如用户可访问路由、访问有效期等信息，服务器无需再去连接数据库验证信息的有效性，并且 payload 支持为你的应用而定制化。
- 支持跨域验证，可以应用于单点登录。

组成：

header，payload，signature

1. header：

   1. 声明类型，这里是 jwt
   2. 声明加密的算法 通常直接使用 HMAC SHA256

   ```
   {  "alg": "HS256",  "typ": "JWT"}
   ```

2. Payload 有效载荷

​		这部分就是我们存放信息的地方了，你可以把有效信息放在这里。这些有效信息分为三部分：

			1. 标准中注册的声明
			1. 公共的声明
			1. 私有的声明

**标准中注册的声明** (建议但不强制使用)：

- iss: 该 JWT 的签发者，一般是服务器，是否使用是可选的；
- iat(issued at): 在什么时候签发的(UNIX时间)，是否使用是可选的；
- exp(expires): 什么时候过期，这里是一个Unix时间戳，是否使用是可选的；
- aud: 接收该JWT的一方，是否使用是可选的；
- sub: 该JWT所面向的用户，userid，是否使用是可选的；
  其他还有：
- nbf (Not Before)：如果当前时间在nbf里的时间之前，则Token不被接受；一般都会留一些余地，比如几分钟，是否使用是可选的；
- jti: jwt 的唯一身份标识，主要用来作为一次性 token，从而回避重放攻击。

**公共的声明**：
公共的声明可以添加任何的信息，一般添加用户的相关信息或其他业务需要的必要信息.但不建议添加敏感信息，因为该部分在客户端可解密。

**私有的声明**：
私有声明是提供者和消费者所共同定义的声明，一般不建议存放敏感信息，因为base64是对称解密的，意味着该部分信息可以归类为明文信息。

3. Signature 签名

优点：

- 因为 json 的通用性，所以JWT是可以进行跨语言支持的，像 JAVA, JavaScript, NodeJS, PHP 等很多语言都可以使用。
- 因为有了 payload 部分，所以 JWT 可以在自身存储一些其他业务逻辑所必要的非敏感信息。
- 便于传输，jwt 的构成非常简单，字节占用很小，所以它是非常便于传输的。
- 它不需要在服务端保存会话信息, 所以它易于应用的扩展。

安全相关：

- 不应该在 jwt 的 payload 部分存放敏感信息，因为该部分是客户端可解密的部分。
- 保护好 secret 私钥，该私钥非常重要。
- 如果可以，请使用 https 协议。



django 缓存

报错机制

csrf

cors

XSS攻击：Cross-Site Scripting（跨站脚本攻击）简称XSS

------

celery

​	核心：

​		程序中的阻塞

​		实时反馈不行

### celery的简单测试

安装celery包，安装eventlet包（可先不安装，如果在win环境下测试失败再安装此包）

​	pip install celery

​	pip install eventlet

创建一个task.py文件，写入

```python
from celery import Celery

# 如果有密码：broker='redis://:[password]@127.0.0.1:6379/1',backend也需设置
app = Celery('wxm', broker='redis://:@127.0.0.1:6379/1', backend='redis://:@127.0.0.1:6379/2')


@app.task()
def task_test(a, b):
    print('task is running.....')
    return a + b

```

在task.py目录下进入到终端中，执行：

​	celery -A task worker -l info -P eventlet（如果未安装eventlet包，则-P eventlet 不需要写）

不关闭终端，切换另一个终端到task.py目录下进入到python中执行下面代码，会发现celery执行成功。

```python
from task import task_test
res=task_test.delay(10, 30)
res.result
```

### django中使用celery

1. 创建celery配置文件
   1. 项目同名目录下创建celery.py

   2. ```
      - proj/
        - manage.py
        - proj/
          - __init__.py
          - settings.py
          - urls.py
          - celery.py
      ```

   3. celery.py下写入

      ```python
      from celery import Celery
      import os
      
      os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'djangoProject.settings')
      app = Celery('blog')
      # 此处引用的是settings.py中的celery设置
      app.config_from_object('django.conf:settings', namespace='CELERY')
      app.autodiscover_tasks()
      ```

   4. 在settings.py中写入配置

      ```django
      # celery设置
      # CELERY_TIMEZONE = "Australia/Tasmania"
      # CELERY_TASK_TRACK_STARTED = True
      # CELERY_TASK_TIME_LIMIT = 30 * 60
      # 如果redis有密码，则redis://:mypwd@127.0.0.1:6379/10
      CELERY_BROKER_URL = "redis://:@127.0.0.1:6379/10"
      CELERY_RESULT_BACKEND = "redis://:@127.0.0.1:6379/1"
      ```

2. 在各个app下创建tasks.py ，集中定义对应的worker函数，写入：

   ```python
   # 此处根据项目情况写编写worker要执行的函数，如果有返回值并在settings.py中设置了存储情况，则返回值存储在相应的地方
   from utils.sms import YunTongXin
   from djangoProject.celery import app
   
   
   @app.task
   def send_msm_c(phone, code):
       """ 省略"""
       return res
   
   ```

3. 在视图函数中调用worker要执行的函数，推送具体worker函数

   ```python
   from .tasks import send_msm_c
   def sms_view(request):
       send_msm_c.delay(phone,ran_num)
   ```

4. 在项目目录下打开终端，启动worker

   ```
    celery -A djangoProject worker -l info -P eventlet
   ```

5. 应当注意，在正式上线的时候应当将django settings中的debug改为False，否则会造成内存泄漏

```
UserWarning: Using settings.DEBUG leads to a memory leak, never use this setting in production environments! warnings.warn('''Using settings.DEBUG leads to a memory
```



6. 在正式上线环境下启动celery

```
nohup celery -A projectname worker -P gevent -c 1000>celery.log 2>&1 &
```

<img src="C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221026150423195.png" alt="image-20221026150423195" style="zoom: 50%;" />

### 缓存

**方案1：cache_page**

​	优点：简单

​	缺点：

​		1. 无法按照具体的访客身份，进行针对性的存储，例如：存储的是主访问自身博客的数据，访客到访时可能会读取到博主触发的缓存，反过来也一样

​		2. 删除缓存成本过高，封装性比较高，直接调用，不利于清除缓存

**方案2：局部-cache.set/get**

​	优点：灵活，存储成本最优，删除成本低

​	缺点：代码实现成本较高

​	案例：

​		模型类中，定义classmethod

```python
class Topic

	@classmethod
    def get_topic_list(cls):
        if cache:
            return cache
        data=cls.objects.filter()
        # cache in再缓存
        return
        
```

​			

**方案3：自定义缓存装饰器**

### 公钥和私钥的创建

1. 在ubuntu终端输如openssl

2. 生成私钥

   ```
   genrsa -out app_private_key.pem 2048
   ```

3. 获取公钥

   ```
   rsa -in app_private_key.pem -pubout -out app_public_Key.pem
   ```

4. 在当前目录下生成了公钥和私钥app_private_key.pem，app_public_Key.pem

### 不同请求的情况

get：

 	1. 获取全部
 	2. 获取单条数据（查看，返回的内容包含了其他的数据）
 	3. 获取单条数据（编辑，只返回数据模型中的数据）
 	 1. 处理方式：另外添加一个api
 	 2. 处理方式：返回较全的数据，由前端筛选

### DUP和 TCP

 1. DUP(Data User Protocol)用户数据报协议，是一个无连接的简单的面向数据报的简单传输层协议

    常见的有：语音通话、视频通话、实时游戏画面等

 2. TCP(Transmission Control Protocol)传输控制协议，是面向连接的协议，在收发数据前，必须和对方建立可靠的协议，然后再进行收发数据。

    常见的有：网站、手机app数据获取

### restful规范（建议）

1. #### API与用户的通信协议，总是使用HTTPs协议。

2. #### 域名

   https://api.example.com                        尽量将API部署在专用域名（会存在跨域问题）

   https://example.org/api/                        API很简单

3. #### 版本

   URL，如：https://api.example.com/v1/
   请求头                                                  跨域时，引发发送多次请求

4. #### 路径

   视网络上任何东西都是资源，均使用名词表示（可复数）

   https://api.example.com/v1/zoos
   https://api.example.com/v1/animals
   https://api.example.com/v1/employees

5. #### 请求方式

   GET ：      从服务器取出资源（一项或多项）
   POST    ：在服务器新建一个资源
   PUT      ： 在服务器更新资源（客户端提供改变后的完整资源）
   PATCH  ：在服务器更新资源（客户端提供改变的属性）
   DELETE ：从服务器删除资源

6. #### 过滤

   通过在url上传参的形式传递搜索条件

   https://api.example.com/v1/zoos?limit=10：指定返回记录的数量
   https://api.example.com/v1/zoos?offset=10：指定返回记录的开始位置
   https://api.example.com/v1/zoos?page=2&per_page=100：指定第几页，以及每页的记录数
   https://api.example.com/v1/zoos?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序
   https://api.example.com/v1/zoos?animal_type_id=1：指定筛选条件

7. ####  状态码

   200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）。
   201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。
   202 Accepted - [*]：表示一个请求已经进入后台排队（异步任务）
   204 NO CONTENT - [DELETE]：用户删除数据成功。
   400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。
   401 Unauthorized - [*]：表示用户没有权限（令牌、用户名、密码错误）。
   403 Forbidden - [*] 表示用户得到授权（与401错误相对），但是访问是被禁止的。
   404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。
   406 Not Acceptable - [GET]：用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。
   410 Gone -[GET]：用户请求的资源被永久删除，且不会再得到的。
   422 Unprocesable entity - [POST/PUT/PATCH] 当创建一个对象时，发生一个验证错误。
   500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功。

8. #### 错误处理

   如果状态码是4xx，就应该向用户返回出错信息。一般来说，返回的信息中将error作为键名，出错信息作为键值即可。
           {
               error: "Invalid API key"
           }

9. #### 返回结果

   针对不同操作，服务器向用户返回的结果应该符合以下规范。
           GET /collection：返回资源对象的列表（数组）
           GET /collection/resource：返回单个资源对象
           POST /collection：返回新生成的资源对象
           PUT /collection/resource：返回完整的资源对象
           PATCH /collection/resource：返回完整的资源对象
           DELETE /collection/r esource：返回一个空文档

10. #### Hypermedia API：

    RESTful API最好做到Hypermedia，即返回结果中提供链接，连向其他API方法，使得用户不查文档，也知道下一步应该做什么。比如，当用户向api.example.com的根目录发出请求，会得到这样一个文档。
            {"link": {
              "rel":   "collection https://www.example.com/zoos",
              "href":  "https://api.example.com/zoos",
              "title": "List of zoos",
              "type":  "application/vnd.yourformat+json"
            }}

### drf 框架

1. #### 认证

   1. 从路由开始：BookView对象调用as_view()方法，该方法会return一个view视图，实际上cbv模式映射为fbv模式
      		`path('book/', views.BookView.as_view())`

   2. APIView重写了dispach方法，首先将客户端传来的request（原生request）进行了’加工‘（丰富）
      		1. 加工时对request加入了验证类的对象（authenticators），若全局未设置DEFAULT_AUTHENTICATION_CLASSES，采用默认的DEFAULT_AUTHENTICATION_CLASSES；否则采用自己设置的认证对象；authenticators的获取方式为从视图对象中的authentication_classes参数获取，若全局未设置DEFAULT_AUTHENTICATION_CLASSES，采用默认的DEFAULT_AUTHENTICATION_CLASSES；用户需要自定authentication_classes，其中需要包含需authenticate方法，该方法需要返回一个元组

   3. 对加工的request进行initial初始化，进行认证、权限和限流
      		self.perform_authentication(request)
              self.check_permissions(request)
              self.check_throttles(request)

         		1. 认证会执行新request中的request.user，user为Request中的方法
         		2. user方法中对用户进行验证，如果已经登录则返回一个元组，其实采用的就是用户自定authentication_classes中的authenticate方法，如果验证不通过就报错抛出异常。
         		3. 认证会有三种情况
         	1. 认证成功。返回自己设置的request.user,request.auth
         	2. 认证成功。返回默认设置的request.user=AnonymousUser,request.auth=None
         	3. 认证失败
         	 		4. 路由分发

   4. 认证
      全局使用，在settings.py中设置：

      ```python
      REST_FRAMEWORK = {
      # 认证
      'DEFAULT_AUTHENTICATION_CLASSES': ['api.utils.authenticates.Authentication'],
      # 默认返回的user和auth
      'UNAUTHENTICATED_USER': (lambda: '匿名用户'),
      'UNAUTHENTICATED_TOKEN': None,
      }
      # 局部使用，可以在局部定义或者在不使用认证的类中加入空验证类
      authentication_classes = []
      ```

2. #### 权限

   1. 使用：
      	1. 类，必须继承BasePermission，必须实现has_permission方法
      	2. 返回值 Ture或者Fasle
   2. 全局使用，在settings.py中设置：
       'DEFAULT_PERMISSION_CLASSES': ['api.utils.permission.AdminPermission'],
   3. 局部
       permission_classes = [权限类,]

3. #### 限流

   1. 使用：

      ```python
      class UserThrottle(SimpleRateThrottle):
      	scope = 'user'
      	# 缓存的key，对于登录用户key为用户名
      	def get_cache_key(self, request, view):
      		return request.user.username
      class VisitorThrottle(SimpleRateThrottle):
      	scope = 'visitor'
      	# 缓存的key，对于游客用户key为ip
          def get_cache_key(self, request, view):
              return self.get_ident(request)
      ```

   2. 全局使用，在settings.py中设置：

     ```
     # 限流
     'DEFAULT_THROTTLE_CLASSES': ['api.utils.throttle.UserThrottle'],
     # 频率设置
     'DEFAULT_THROTTLE_RATES': {
     	'visitor': '2/day',  # 针对游客的访问频率进行限制，实际上，drf只是识别首字母，为了提高代码的维护性，建议写完整单词
     	'user': '5/day',  # 针对会员的访问频率进行限制，
     }
     ```

   3. 局部
       throttle_classes = [VisitorThrottle,]

4. #### 版本

   1. 在url中：http://127.0.0.1:8000/api/v1/order/
      	**全局设置：**

      		1. 在settings.py中 设置
   		
      	 ```python
      	 # 版本控制
      	 
      	 'DEFAULT_VERSIONING_CLASS':'rest_framework.versioning.URLPathVersioning',
      	 'DEFAULT_VERSION': 'v1',
      	 'ALLOWED_VERSIONS': ['v1', 'v2', 'v3'],
      	 'VERSION_PARAM': 'version',  # 'v
      	 ```
   		
      		2. 在路由中设置
      	 ```python
      	 re_path(r'^(?P<version>[v1|v2]+)/order/$',OrderView.as_view()),
      	 re_path(r'^(?P<version>[v1|v2]+)/order/(?P<id>[0-9]+)/$', OrderView.as_view()),
      	 ```

   2. 在url中通过get传参：（不常用）
       http://127.0.0.1:8000/api/order/version=v1/
       全局中设置：

     ```python
     # 版本控制
     DEFAULT_VERSION': 'v1',
     'ALLOWED_VERSIONS': ['v1', 'v2', 'v3'],
     'VERSION_PARAM': 'version',  # 'v
     # 在视图函数中增加
     from rest_framework.versioning import QueryParameterVersioning
     versioning_class = QueryParameterVersioning
     ```

5. #### 解析器

   1. 前戏： django: request.POST中获取request.body的数据，需要满足条件：

      1. 请求头要求：如果请求头中的content_type：application/x-www-form-urlencoded，request.POST中才有值，（去request.body中去解析）

      2. 数据格式要求：

         name=alex&age=18&gender=man

      3. 如form表单和ajax提交的满足以上两点
         如果不满足，则body中有值，post中没有值，可以通过json.loads(request.body)获

   2. rest_framework 解析器
      在视图类中定义parser_classes=[JSONParser,]，则允许用户发送JSON格式

      1. a.content-type:application/json
      2. b.{'name':'alex',age:19}

   3. 获取请求数据的源码流程：

                  1. 获取用户请求
                  2. 获取用户请求体
                  3. 根据用户请求头和parser_classes=[JSONParser,]中指出的请求头进行比较
                  4. JSONParser对象去请求体中
                  5. 获得request.data

   4. 全局中配置

      ```python
      # 解析器
      'DEFAULT_PARSER_CLASSES': [
      'rest_framework.parsers.JSONParser',
      'rest_framework.parsers.FormParser',
      'rest_framework.parsers.MultiPartParser'
      ]
      ```

6. #### 序列化器

   1. 序列化器应创建序列化类，继承serializers.Serializer

      ```python
      class UserViewSerializer(serializers.Serializer):
          username = serializers.CharField(max_length=32)
          password = serializers.CharField(max_length=32)
          # 对于choices定义的字段可以在source中用get_字段名_display来显示字段而不是数字
          user_type = serializers.CharField(source='get_user_type_display')
          # 对于使用外键约束的字段，可以用source指定显示的内容
          group=serializers.CharField(source='group.title')
          # 对于多对多的限制字段，可用SerializerMethodField自定义显示，并重写get_字段名函数
          role=serializers.SerializerMethodField() 
          def get_role(self,row):
              role_obj_list=row.role.all()
              ret=[]
              # for item in role_obj_list:
              #     ret.append({'id':item.id,'title':item.title})
              for item in role_obj_list:
              ret.append(item.title)
              return ret
      ```

   2. 继承serializers.ModelSerializer类

      ```python
      class UserViewSerializer(serializers.ModelSerializer):
          group=serializers.HyperlinkedIdentityField(view_name='gp')
          class Meta:
              model=UserInfo
              fields='__all__'
              # extra_kwargs={
              #     'password':{'min_length':6},
              # }
              depth=1
      ```


### Redis

#### 主从复制

主机数据更新后根据配置和策略， 自动同步到备机的 master/slaver 机制，Master 以写为主，Slave 以读为主，主从复制节点间数据是全量的。

优点：

- 读写分离，性能扩展
- 容灾快速恢复

具体操作：

1. 创建/myredis文件夹
2. 复制redis.conf配置文件到文件夹中
3. 配置一主两从，创建三个配置文件
   - redis6379.conf
   - redis6380.conf
   - redis6381.conf

4. 在三个配置文件中写入

   include /myredis/redis.conf

   pidfile /var/run/redis_6379.pid

   port 6379

   dbfilename dump6379.rdb

5. 启动三个redis配置文件

   redis-server redis6379.conf

   redis-server redis6380.conf

   redis-server redis6381.conf

   进入到redis服务查看主从信息：info replication

   在从机上执行slaveof 主机id 端口号 slaveof 127.0.0.1 6379

复制原理

- Slave 启动成功连接到 master 后会发送一个 sync 命令；

- Master 接到命令启动后台的存盘进程，同时收集所有接收到的用于修改数据集命令，在后台进程执行完毕之后，master 将传送整个数据文件到 slave，以完成一次完全同步。

- 全量复制：slave 服务器在接收到数据库文件数据后，将其存盘并加载到内存中。

- 增量复制：Master 继续将新的所有收集到的修改命令依次传给 slave，完成同步。

- 但是只要是重新连接 master，一次完全同步（全量复制) 将被自动执行。



一主多仆

薪火相传

反客为主

​	slaveof no one

​	反客为主只有在薪火相传模式下才有。

哨兵模式

- 反客为主的自动版，能够后台自动监控主机是否故障，如果故障了根据投票数自动将从库转换为主库。
- 配置
  1. 自定义的/myredis目录下新建sentinel.conf，文件名不能错
  2. 在sentinel.conf中写入`sentinel monitor mymaster 127.0.0.1 6379 1`。其中mymaster为监控对象起的服务器名称，1 为至少有多少个哨兵同意迁移的数量
  3. 启动哨兵`redis-sentinel /myredis/sentinel.conf`

- 缺点：

  复制延迟：由于所有的写操作都是先在Master上操作，然后同步更新到Slave上，所以从Master同步到Slave机器有一定的延迟，当系统很繁忙的时候，延迟问题会更加严重，Slave机器数量的增加也会使这个问题更加严重。

- 故障恢复

  新主登基：

  从下面的主服务的所有从服务李米娜挑选一个从服务，将其转换成主服务。选择条件依次为：

  1. 选择优先级考前的，在 redis.conf 中默认 replica-priority 100，值越小优先级越高

  2. 选择偏移量最大的，偏移量：指获得原主机数据最全的。

  3. 选择runid最小的从服务：每个 redis 实例启动后都会随机生成一个 40 位runid。

  群仆俯首：

  挑选出新的主服务之后sentinel向原主服务的从服务发送slaveof新主服务的命令，复制新master。

  旧主俯首：

  当已下线的服务重新上线时，sentinel会向其发送slaveof命令，让其成为新主的从。

#### 集群

Redis 集群（包括很多小集群）实现了对 Redis 的水平扩容，即启动 N 个 redis 节点，将整个数据库分布存储在这 N 个节点中，每个节点存储总数据的 1/N，即一个小集群存储 1/N 的数据，每个小集群里面维护好自己的 1/N 的数据。

Redis 集群通过分区（partition）来提供一定程度的可用性（availability）： 即使集群中有一部分节点失效或者无法进行通讯， 集群也可以继续处理命令请求。

该模式的 redis 集群特点是：分治、分片。

集群连接：redis-cli -c -p 6379 采用集群策略连接，设置数据会自动切换到相应的写主机.

**查询集群信息**

`cluster nodes`

**redis cluster如何分配6个节点：**

- 一个集群至少要有三个主节点。
- 选项 –cluster-replicas 1 ：表示我们希望为集群中的每个主节点创建一个从节点。
- 分配原则尽量保证每个主数据库运行在不同的 IP 地址，每个从库和主库不在一个 IP 地址上。

**slots**

一个 Redis 集群包含 16384 个插槽（hash slot），数据库中的每个键都属于这 16384 个插槽的其中一个。集群使用公式 CRC16 (key) % 16384 来计算键 key 属于哪个槽， 其中 CRC16 (key) 语句用于计算键 key 的 CRC16 校验和 。

集群中的每个节点负责处理一部分插槽。 举个例子， 如果一个集群可以有主节点， 其中：

节点 A 负责处理 0 号至 5460 号插槽。
节点 B 负责处理 5461 号至 10922 号插槽。
节点 C 负责处理 10923 号至 16383 号插槽。

**在集群中录入值**

在 redis-cli 每次录入、查询键值，redis 都会计算出该 key 应该送往的插槽，如果不是该客户端对应服务器的插槽，redis 会报错，并告知应前往的 redis 实例地址和端口。

redis-cli 客户端提供了 –c 参数实现自动重定向。如 redis-cli -c –p 6379 登入后，再录入、查询键值对可以自动重定向。不在一个 slot 下的键值，是不能使用 mget,mset 等多键操作。

多键操作可以加{}定义组的概念，从而使key中{}相同内容的键值对放到一个slot

`mset name{user} 'wxm' age{user} 20`

**查询集群中的值**(只能看自己插槽中的值)

`cluster keyslot k1`

`cluster countkeysinslot slot`

`cluster getkeysinslot slot nums`

**故障恢复**

- 如果主节点下线？从节点能否自动升为主节点？注意：cluster-node-timeout 15000 设置了15 秒超时。从节点会自动升为主节点

- 主节点恢复后，主从关系会如何？主节点回来变成从机。


- 如果所有某一段插槽的主从节点都宕掉，redis 服务是否还能继续？

  - 如果某一段插槽的主从都挂掉，而 cluster-require-full-coverage 为 yes ，那么整个集群都挂掉。

  - 如果某一段插槽的主从都挂掉，而 cluster-require-full-coverage 为 no ，那么，该插槽数据全都不能使用，也无法存储。


**redis集群优点**

- 实现扩容

- 分摊压力

- 无中心配置相对简单

**redis集群不足**

- 多键操作是不被支持的。

- 多键的 Redis 事务是不被支持的，lua 脚本不被支持。

- 由于集群方案出现较晚，很多公司已经采用了其他的集群方案，而代理或者客户端分片的方案想要迁移至 redis cluster，需要整体迁移而不是逐步过渡，复杂度较大。

#### 应用问题

##### 缓存穿透

key 对应的数据在数据源并不存在，每次针对此 key 的请求从缓存获取不到，请求都会压到数据源（数据库），从而可能压垮数据源。比如

用一个不存在的用户 id 获取用户信息，不论缓存还是数据库都没有，若黑客利用此漏洞进行攻击可能压垮数据库。

**缓存穿透发生的条件：**

- 应用服务器压力变大
- redis 命中率降低
- 一直查询数据库，使得数据库压力太大而压垮

其实 redis 在这个过程中一直平稳运行，崩溃的是我们的数据库（如 MySQL）。

缓存穿透发生的原因：黑客或者其他非正常用户频繁进行很多非正常的 url 访问，使得 redis 查询不到数据库

**解决方案：**

一个一定不存在缓存及查询不到的数据，由于缓存是不命中时被动写的，并且出于容错考虑，如果从存储层查不到数据则不写入缓存，这将导致整个不存在的数据每次请求都要到存储层去查询，失去了缓存的意义。

- 对空值缓存：如果一个查询返回的数据为空（不管是数据是否不存在），我们仍然把这个空结果（null）进行缓存，设置空结果的过期时间会很短，最长不超过五分钟。

- 设置可访问的名单（白名单）：使用 bitmaps 类型定义一个可以访问的名单，名单 id 作为 bitmaps 的偏移量，每次访问和 bitmap 里面的 id 进行比较，如果访问 id 不在 bitmaps 里面，进行拦截，不允许访问。

- 采用布隆过滤器：布隆过滤器（Bloom Filter）是 1970 年由布隆提出的。它实际上是一个很长的二进制向量 (位图) 和一系列随机映射函数（哈希函数）。布隆过滤器可以用于检索一个元素是否在一个集合中。它的优点是空间效率和查询时间都远远超过一般的算法，缺点是有一定的误识别率和删除困难。

- 进行实时监控：当发现 Redis 的命中率开始急速降低，需要排查访问对象和访问的数据，和运维人员配合，可以设置黑名单限制服务。

##### 缓存击穿

key 对应的数据存在，但在 redis 中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端数据库加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端数据库压垮。

- 数据库访问压力瞬时增加，数据库崩溃
- redis 里面没有出现大量 key 过期
- redis 正常运行

缓存击穿发生的原因：redis 某个 key 过期了，大量访问使用这个 key（热门 key）。

**解决方案：**

- 预先设置热门数据：在 redis 高峰访问之前，把一些热门数据提前存入到 redis 里面，加大这些热门数据 key 的时长。

- 实时调整：现场监控哪些数据热门，实时调整 key 的过期时长。

- 使用锁：

  - 就是在缓存失效的时候（判断拿出来的值为空），不是立即去 load db。

  - 先使用缓存工具的某些带成功操作返回值的操作（比如 Redis 的 SETNX）去 set 一个 mutex key。

  - 当操作返回成功时，再进行 load db 的操作，并回设缓存，最后删除 mutex key；

  - 当操作返回失败，证明有线程在 load db，当前线程睡眠一段时间再重试整个 get 缓存的方法。

##### 缓存雪崩

key 对应的数据存在，但在 redis 中过期，此时若有大量并发请求过来，这些请求发现缓存过期一般都会从后端数据库加载数据并回设到缓存，这个时候大并发的请求可能会瞬间把后端数据库压垮。

缓存雪崩与缓存击穿的区别在于这里针对很多 key 缓存，前者则是某一个 key 正常访问。

**解决方案：**

- 构建多级缓存架构：nginx 缓存 + redis 缓存 + 其他缓存（ehcache 等）。

- 使用锁或队列：用加锁或者队列的方式来保证不会有大量的线程对数据库一次性进行读写，从而避免失效时大量的并发请求落到底层存储系统上，该方法不适用高并发情况。

- 设置过期标志更新缓存：记录缓存数据是否过期（设置提前量），如果过期会触发通知另外的线程在后台去更新实际 key 的缓存。

- 将缓存失效时间分散开：比如可以在原有的失效时间基础上增加一个随机值，比如 1-5 分钟随机，这样每一个缓存的过期时间的重复率就会降低，就很难引发集体失效的事件。


### 分布式锁

随着业务发展的需要，原单体单机部署的系统被演化成分布式集群系统后，由于分布式系统多线程的特点以及分布在不同机器上，这将使原单机部署情况下的并发控制锁策略失效，单纯的 Java API 并不能提供分布式锁的能力。为了解决这个问题就需要一种跨 JVM 的互斥机制来控制共享资源的访问，这就是分布式锁要解决的问题！

分布式锁主流解决方案：

- 基于数据库实现分布式锁

- 基于缓存（Redis 等）

- 基于 Zookeeper

根据实现方式，分布式锁还可以分为类 CAS 自旋式分布式锁以及 event 事件类型分布式锁：

- 类 CAS 自旋式分布式锁：询问的方式，类似 java 并发编程中的线程获询问的方式尝试加锁，如 mysql、redis。

- 另外一类是 event 事件通知进程后续锁的变化，轮询向外的过程，如 zookeeper、etcd


每一种分布式锁解决方案都有各自的优缺点：

- 性能：redis 最高

- 可靠性：zookeeper 最高

setnx：通过该命令尝试获得锁，没有获得锁的线程会不断等待尝试。

set key ex 3000nx：设置过期时间，自动释放锁，解决当某一个业务异常而导致锁无法释放的问题。但是当业务运行超过过期时间时，开辟监控线程增加该业务的运行时间，直到运行结束，释放锁。

uuid：设置 uuid，释放前获取这个值，判断是否自己的锁，防止误删锁，造成没锁的情况。

### 多数据库

django支持项目连接多个数据库

#### 读写分离

##### django端配置

```
192.168.1.2      master   [写]
192.168.2.12     slave    [读]
```

- py.settings中配置

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'myblog',
        'USER': 'root',
        'PASSWORD': '940328',
        'HOST': '127.0.0.1',
        'PORT': '3306'
    },
    'bak': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'myblog',
        'USER': 'root',
        'PASSWORD': '940328',
        'HOST': '127.0.0.1',
        'PORT': '3306'
    }
}
```

- 生成数据库表

```
python manage.py makemigrations
python manage.py migrate --databases=bak
```

- 开发中使用（指定orm操作时使用哪个数据库）

```
UserProfile.objects.using('bak').filter(phone=phone).first()
my_object.save(using='legacy_users')
```

- 编写router类，简化【开发中指定数据库】

```python
class DemoRouter:
    route_app_labels = {'auth', 'contenttypes'}
    def db_for_rad(self, model, **hints):
        return 'bak'
        if model._meta.app_label in self.route_app_labels:
            return 'auth_db'
        return None
    def db_for_write(self, model, **hints):
         if model._meta.model_name =='UserInfo':
        	return 'default'
        return None
```

- 在settings.py中配置创建的路由类

```
DATABASE_ROUTERS = ['path.to.DemoRouter']
```

#### 分库(多app)

100张表，50张表-A数据库，50张表B数据库。根据app划分

- 命令

  ```python
  python manage.py makemigrations
  python manage.py migrate app01 --databases=bak
  python manage.py migrate app02 --databases=default
  ```

- 路由

```python
class DemoRouter:
    route_app_labels = {'auth', 'contenttypes'}
    def db_for_rad(self, model, **hints):
            return 'default'
        return 'bak'
    def db_for_write(self, model, **hints):
         	return 'default'
        return 'bak'
```

#### 分库（单app)

- 命令

```
python manage.py makemigrations
```

- 路由

```python
class DemoRouter:
    def allow_migrate(self,db,app_label, model_name=None, **hints)
    	# python manage.py migrate app01 --databasae=dafault
        # python manage.py migrate app01 --databasae=bak
    	# Ture -->生成到数据库
        # False -->不生成到数据库
    	if db=='bak':
            if model_name in ['role','depart']:
                return True 
            else:
                return False
        if db=='default':
            if model_name in ['userinfo']:
				return True 
            else:
                return False
       
```

- settings.py中配置

```
DATABASE_ROUTERS = ['path.to.DemoRouter']
```

注意事项：

- 分库，表拆分到不同数据库

```
django不支持
尽可能的将有关联的表放到一个数据库
```

- 为什么表拆分到不同的库

```
对于简单的应用，只用一个数据库就可以了
对于大量数据的应用，将数据库拆分或者读写分离
```

### mysql的主从复制

#### 为什么需要主从复制

1. 在业务复杂的系统中，有这个一个场景，有一句sql语句需要锁表，导致暂时不能使用读的服务，那么就很影响运行中的业务，使用主从复制，让主库负责写，从库负责读，这样，即使主库出现锁表的情景，通过读从库也可以保证业务的正常运行。
2. 做数据的热备
3. 架构的扩展。业务量越来越大。I/O访问频率过大，单机无法满足，此时做多库的储存，降低磁盘I/O的访问频率，提高单个机器的I/O性能。

#### mysql的主从复制

mysql主从复制是指数据可以从一个mysql数据库服务器主节点复制到一个或多个从节点。mysql默认采用的是异步复制方式，这样从节点不用一直访问主服务器来更新自己的数据，数据的更新可以在远程连接上进行，从节点可以复制主数据库中的所有数据库或者特定的数据库。

#### mysql复制原理

1. master服务器将数据的改变记录二进制binlog日志，当master上的数据发生改变时，则将其变化写进二进制日志中；
2. slave服务器会在一定时间间隔内对master二进制日志进行探索其是否发生改变，如果发生改变，则开始一个I/OThread请求master二进制事件。
3. 同时主节点为每个I/O线程启动一个dump线程，用于向其发送二进制事件，并保存到至从节点本地的中继日志中，从节点将启动sql线程从中继日志中读取二进制日志，在本地存放，使得其数据和主节点保持一致，最后I/OThread和SQLThread将进入睡眠状态，等待下一次被唤醒。

**概括：**

- 从库会生成两个线程，一个I/O线程，一个sql线程
- I/O线程回去请求主库的binlog，并将得到的binlog写到本地的relay-log（中继日志）文件中
- 主库会生成一个log dump线程，用来给从库I/O线程传binlog
- SQL线程，会读取relay-log文件中的日志，并解析成sql语句逐一执行。

**注意：**

- master需开启binlog，通常为了数据安全，slave也开启binlog
- mysql复制至少需要两个mysql服务，也可以在一台服务器开启多个服务
- 最好确保master和slave服务器上的mysql版本相同（如不同，则保证master版本低于slave版本）
- master和slave两节点时间同步

五种架构

- 一主一从
- 一主多从
- 主主复制
- 多主一从
- 联级复制

#### 读写分离

mysql的读写分离基本原理是让master数据库处理写操作，slave数据库处理读操作。master将写操作的变更同步到各个slave节点。

mysql读写分离能提高系统性能的原因在于：

1. 物理服务器增加，机器处理能力提升，拿硬件换性能。
2. 主从只负责各自的读和写，极大程度缓解x锁和s锁争用。
3. slave可以配置myiasm引擎。提升查询性能以及节约系统开销。
4. master直接写是并发的，slave通过主库发送来的binlog恢复数据是异步的。
5. slave可以单独设置一些参数来提升其读的性能。
6. 增加冗余，提高可读性。

### django日志

日志是指程序在运行过程中，对状态、时间、错误等的记录。即把运行过程中产生的信息输出或保存起来，供开发者查阅。

Django使用Python内置的logging模块处理日志。一份日志配置由`Loggers`、`Handlers`、`Filters`、`Formatters`四部分组成。

**Loggers**

`Logger`即**记录器**，是日志系统的入口。**它有三个重要的工作**：

- 向应用程序（也就是你的项目）公开几种方法，以便运行时记录消息
- 根据传递给Logger的消息的严重性，确定出需要处理的消息
- 将需要处理的消息传递给所有感兴趣的处理器（`Handler`）

每一条写入logger的消息都是一条日志记录。每一条日志记录也包含**级别**，代表对应消息的严重程度。常用的级别如下：

- `DEBUG`：排查故障时使用的低级别系统信息，通常开发时使用
- `INFO`：一般的系统信息，并不算问题
- `WARNING`：描述系统发生的小问题的信息，但通常不影响功能
- `ERROR`：描述系统发生的大问题的信息，可能会导致功能不正常
- `CRITICAL`：描述系统发生严重问题的信息，应用程序有崩溃风险

简单示例：在setting.py中配置

```python
LOGGING = {
    # 版本
    'version': 1,
    # 是否禁用已经存在的日志器
    'disable_existing_loggers': False,
    # 日志信息显示的格式
    'formatters': {
        'standard': {
            'format':'%(levelname)s %(asctime)s %(module)s %(lineno)d %(message)s',
            # 'format': '%(levelname)s %(asctime)s %(module)s %(lineno)d %(message)s',
            'datefmt': '%Y-%m-%d %H:%M:%S'
        },
    },
    # 过滤器
    'filters': {
        # django在debug模式下才输出日志
        'require_debug_true': {
            '()': 'django.utils.log.RequireDebugTrue',
        },
    },
    # 日志处理方法
    'handlers': {
        # 标准输出
        'console': {
            'level': 'INFO',
            'filters': ['require_debug_true'],
            'class': 'logging.StreamHandler',
            'formatter': 'standard'
        },
        # 自定义handler，向文件中输出日志
        'file': {
            level': 'DEBUG',
            'class': 'logging.handlers.TimedRotatingFileHandler',
            'filename': os.path.join(BASE_DIR, 'logs/test.log'),  # 日志文件的位置
            # 'maxBytes': 300 * 1024 * 1024,
            # 保存时间30天
            'when': 'midnight',
            'backupCount': 10,
            'formatter': 'standard'
        },
    },
    # 日志器
    'loggers': {
        # 定义了一个名为django的日志器
        'django': {
            'handlers': ['console', 'file'],  # 可以同时向终端与文件中输出日志
            'propagate': False,  # 是否继续传递日志信息
            'level': 'INFO',  # 日志器接收的最低日志级别
        },
    }
}
```

### websocket

**轮询**：ajax轮询 的原理，让浏览器隔个几秒就发送一次请求，询问服务器是否有新信息。

**长轮询**：long poll 其实原理跟 ajax轮询 差不多，都是采用轮询的方式，不过采取的是阻塞模型（一直打电话，没收到就不挂电话），也就是说，客户端发起连接后，如果没消息，就一直不返回Response给客户端。直到有消息才返回，返回完之后，客户端再次建立连接，周而复始。

**WebSocket协议**是基于TCP的一种新的协议。WebSocket最初在HTML5规范中被引用为TCP连接，作为基于TCP的套接字API的占位符。它实现了浏览器与服务器全双工(full-duplex)通信。其本质是保持TCP连接，在浏览器和服务端通过Socket进行通信。

- 连接，客户端发起

- 握手，客户端发送一个消息，后端接收到消息再做一些特殊处理并返回。服务端支持websocket

  - 客户端向服务端发送

    ```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
    Origin: http://example.com
    
    ```

  - 服务端接收

    ```
    x3JJHMbDL1EzLkh9GBhXDw== 与 magic string 进行拼接
    magic sting ='258EAFA5-E914-47DA-95CA-C5AB0DC85B11'
    v1='x3JJHMbDL1EzLkh9GBhXDw=='+'258EAFA5-E914-47DA-95CA-C5AB0DC85B11'
    v2=hmac1(v1)
    v3=base64(v2) # 密文
    ```

    ```
    # 对请求头中的sec-websocket-key进行加密
    response_tpl = "HTTP/1.1 101 Switching Protocols\r\n" \
          "Upgrade:websocket\r\n" \
          "Connection: Upgrade\r\n" \
          "Sec-WebSocket-Accept: 密文
          "WebSocket-Location: ws://%s%s\r\n\r\n"
    ```

- 收发数据（加密）

  - 先获取第二个字节，8位      10001010

  - 在获取第二个字节的后7位     0001010 -> payload len

    - =127，2字节，8个字节             其他字节（4字节 masking key +数据）。
    - =126，2字节，2个字节             其他字节（4字节 masking key +数据）。
    - <=125，2字节                            其他字节（4字节 masking key +数据）。

  - 获取masking key，然后对数据进行解密

    ```
    var DECODED = "";
    for (var i = 0; i < ENCODED.length; i++) {
        DECODED[i] = ENCODED[i] ^ MASK[i % 4];
    }
    ```

    ```
    0                   1                   2                   3
     0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
    +-+-+-+-+-------+-+-------------+-------------------------------+
    |F|R|R|R| opcode|M| Payload len |    Extended payload length    |
    |I|S|S|S|  (4)  |A|     (7)     |             (16/64)           |
    |N|V|V|V|       |S|             |   (if payload len==126/127)   |
    | |1|2|3|       |K|             |                               |
    +-+-+-+-+-------+-+-------------+ - - - - - - - - - - - - - - - +
    |     Extended payload length continued, if payload len == 127  |
    + - - - - - - - - - - - - - - - +-------------------------------+
    |                               |Masking-key, if MASK set to 1  |
    +-------------------------------+-------------------------------+
    | Masking-key (continued)       |          Payload Data         |
    +-------------------------------- - - - - - - - - - - - - - - - +
    :                     Payload Data continued ...                :
    + - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
    |                     Payload Data continued ...                |
    +---------------------------------------------------------------+
    ```

    

- 断开连接

django框架

django默认不支持websocket，需要安装组件：

```
pip install channels
```

配置：

setting.py中配置

```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myblog.apps.MyblogConfig',
    'mainsite.apps.MainsiteConfig',
    'channels',

]
```

```
ASGI_APPLICATION = "mysite.asgi.application"
```

修改asgi.py文件

```python
import os
from django.core.asgi import get_asgi_application
from channels.routing import ProtocolTypeRouter, URLRouter
from . import routing



os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')

# application = get_asgi_application()


application = ProtocolTypeRouter({
    'http':get_asgi_application(),
    'websocket': URLRouter(routing.websocket_urlpatterns)
})
```

在settings.py同级目录下创建routing.py文件，与urls.py文件类似，相当于是websocket的路由分发

```python
from django.urls import re_path
from myblog.views import consumers

websocket_urlpatterns=[
    re_path(r'ws/(?P<group>\w+)/$',consumers.ChatConsumer.as_asgi())
]
```



在应用下创建consumers.py来处理聊天业务逻辑

```python
from channels.generic.websocket import WebsocketConsumer
from channels.exceptions import StopConsumer


class ChatConsumer(WebsocketConsumer):
    def websocket_connect(self, message):
        self.accept()

    def websocket_receive(self, message):
        print(message)
        self.send('不要回复')

    def websocket_disconnect(self, message):
        raise StopConsumer()

```

聊天室

- 访问地址看到聊天室的页面，http请求

- 让客户端主动向服务端发起websocket连接，服务端接收到连接后通过（握手）。

  - 客户端

    ```js
    var socket = new WebSocket('ws://127.0.0.1:8000/room/123/')
    ```

    

