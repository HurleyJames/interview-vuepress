# Bitmap

## 图片框架的三级缓存机制

1. **内存缓存**（优先加载，速度最快）：首次加载的时候通过网络加载，获取图片，然后保存到内存中和本地中；之后运行时，优先访问内存中的图片缓存；
2. **本地缓存**（次优先加载，速度快）：如果内存中没有，则访问本地的图片；
3. **网络缓存**（最后加载，速度慢，浪费流量）：如果本地还没有，就有可能是第一次访问，所以进行网络请求；

**三级缓存的原理**：内存作为一级缓存，本地作为二级缓存，网络加载为最后。其中，内存使用LruCache，其内部通过`LinkedHashMap`来持有外界缓存对象的强引用；对于本地缓存，使用DiskLruCache。而加载图片的时候，首先使用LRU方式进行寻找，找不到指定内容，就按照三级缓存的策略，再进行本地搜索，最后进行网络加载。

## LRU算法的原理

LRU（Least Recently Used）算法是近期最少使用算法，其核心思想是当缓存满时，会优先淘汰那些近期最少使用的缓存对象。采用LRU算法的缓存主要有以下两种：

* **LruCache（内存缓存）**：LruCache类是一个**线程安全**的**泛型类**：内部采用一个`LinkedHashMap`以强引用的方式存储外界的缓存对象，并提高`get`和`put`方法来完成缓存的获取和添加操作，当缓存满了就会移除较早使用的缓存对象，再添加新的
* **DiskLruCache（磁盘缓存）**：通过将缓存对象写入文件系统从而实现缓存效果。DiskLruCache的缓存添加的操作是通过Editor完成的，Editor表示一个缓存对象的编辑对象。

LruCache用于实现内存缓存，DiskLruCache用于实现存储设备缓存，两者相结合就可以实现一个有价值的ImageLoader。

## 实现ImageLoader

一个优秀的ImageLoader应该具备以下功能：

* **图片的同步加载**：以同步的方式向调用者提供所加载的图片（可能内存中、缓存中或者网络获取的）
* **图片的异步加载**：开启自己的线程加载图片
* **图片压缩**：降低OOM
* **内存缓存**
* **磁盘缓存**
* **网络获取**

### 同步加载和异步加载接口的设计

#### 同步加载

工作遵循以下几个步骤：首先尝试从内存缓存中读取图片，接着尝试从磁盘缓存中读取图片，最后才从网络中请求图片。这个过程是不能在主线车中调用的，否则会抛出异常。那么，这个执行环境的检查就是**通过检查当前线程的`Looper`是否为主线程的`Looper`，来判断当前线程是否为主线程。

#### 异步加载

异步加载也就是所谓的开启一个新的线程去加载图片。它会首先尝试从内存中读取图片，如果成功就直接返回结果，否则会在**线程池**中调用`loadBitmap`这个加载图片的方法。当图片加载成功后，图片的地址以及绑定的ImageView会封装成一个`LoaderResult`对象，然后通过`mainHandler`向主线程发送一个消息，这样就通知可以在主线程给ImageView显示图片了。所以，上面的核心是用到了**线程池**和**Handler**。

之所以使用线程池，是因为如果使用普通的线程去加载图片，那么随着列表的滑动，可能会产生大量的线程，这会降低效率。

## Android中缓存更新策略 <Badge text="Uncompleted"/>