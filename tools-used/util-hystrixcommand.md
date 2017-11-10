# HystrixCommand 线程池工具的配置和使用

> Author: larry.koo  Date: 2017--03-31

---

### 基于 SpringBoot 的 AutoConfiguration yaml 配置如下

**yaml 配置项**

```java
sxw:
    hystrix:
        command-prop:
          metricsRollingStatisticalWindowBuckets: 10 // default => statisticalWindowBuckets: 10 = 10 buckets in a 10 second window so each bucket is 1 second
          circuitBreakerRequestVolumeThreshold: 20 // default => statisticalWindowVolumeThreshold: 20 requests in 10 seconds must occur before statistics matter
          circuitBreakerSleepWindowInMilliseconds: 5000 // default => sleepWindow: 5000 = 5 seconds that we will sleep before trying again after tripping the circuit
          circuitBreakerErrorThresholdPercentage: 50// default => errorThresholdPercentage = 50 = if 50%+ of requests in 10 seconds are failures or latent then we will trip the circuit
          circuitBreakerForceOpen: false  // default => forceCircuitOpen = false (we want to allow traffic)
          circuitBreakerForceClosed: false  // default => ignoreErrors = false
          executionTimeoutInMilliseconds: 1000 // default => executionTimeoutInMilliseconds: 1000 = 1 second
          executionTimeoutEnabled: true
          executionIsolationStrategy: "THREAD"
          executionIsolationThreadInterruptOnTimeout: true
          executionIsolationThreadInterruptOnFutureCancel: false
          metricsRollingPercentileEnabled: true
          requestCacheEnabled: true
          fallbackIsolationSemaphoreMaxConcurrentRequests: 10
          fallbackEnabled: true
          executionIsolationSemaphoreMaxConcurrentRequests: 10
          requestLogEnabled: true
          circuitBreakerEnabled: true
          metricsRollingPercentileWindow: 60000 // default to 1 minute for RollingPercentile
          metricsRollingPercentileWindowBuckets: 6 // default to 6 buckets (10 seconds each in 60 second window)
          metricsRollingPercentileBucketSize: 100 // default to 100 values max per bucket
          metricsHealthSnapshotIntervalInMilliseconds: 500
        thread-pool-prop:
          coreSize: 10 // size of thread pool
          keepAliveTimeMinutes: 1 // minutes to keep a thread alive (though in practice this doesn't get used as by default we set a fixed size)
          maxQueueSize: -1 // size of queue (this can't be dynamically changed so we use 'queueSizeRejectionThreshold' to artificially limit and reject)
          queueSizeRejectionThreshold: 5 // number of items in queue
          threadPoolRollingNumberStatisticalWindowInMilliseconds: 10000 // milliseconds for rolling number
          threadPoolRollingNumberStatisticalWindowBuckets: 10 // number of buckets in rolling number (10 1-second buckets)
```

> 备注：以上为默认配置信息，项目中使用时，如果该项配置没有改变，无须进行配置

**SpringBoot项目中使用**

```java
/**
 * 将配置对象注入
 */
@Autowired
private MyHystrixCustomProperties properties;

/**
 * sayHello under protection of Hystrix
 *
 * @param name
 * @return <code>"Hello " + name + "!"</code>
 */
public static Object sayHello(final String groupKey, final String commandKey) {

    return ThreadHelper.execute(new HystrixBaseCommand(properties, groupKey, commandKey) {
        @Override
        protected String run() throws Exception {
            System.out.println("==========Hello:" + name);
            return String.format("Hello %s!", name);
        }
    });
}
```

\*\*调用方式\*\*

```java
/**
 * call async
 *
 * @param name
 * @return
 */
public static Future<Object> sayHello1(final String groupKey, final String commandKey) {
    return ThreadHelper.queue(new HystrixBaseCommand(properties, groupKey, commandKey) {
        @Override
        protected String run() throws Exception {
            sleep(500);
            System.out.println("==========Hello1:" + name);
            return String.format("Hello %s!", name);
        }
    });
}
```



