Redis Starter 的使用
===

> Author: larry.koo  Date: 2017-11-09


### 功能介绍

基于 Spring-Boot-Data-Redis 实现的版本
支持 Redis3.x 原生集群和单机方式连接
强依赖与 SpringBoot 1.4 +

### 如何使用

**Maven依赖：**

```java
<dependency>
    <groupId>cn.sxw.commons.data.redis</groupId>
    <artifactId>sxw-commons-data-redis-starter</artifactId>
    <version>2.0.0-SNAPSHOT</version>
</dependency>
```

**配置 application.yml**

```yml
## 自定义的多 Redis 驱动配置，配置属性与 Spring-Data-Redis 一致
sxw.redis:
  instances:
    ## 集群配置
    exam-cluster:   ## 该名称为实例唯一ID,初始化时使用
      cluster:
        nodes: 192.168.2.100:7002,192.168.2.101:7002,192.168.2.102:7002
        max-redirects: 5
      pool:
        max-active: 8
        max-wait: 3000
        max-idle: 8
        min-idle: 0
      timeout: 3000
     ## 单机配置
    exam-single:
      database: 1
      host: localhost
      port: 6379
      pool:
        max-active: 8
        max-wait: 3000
        max-idle: 8
        min-idle: 0
      timeout: 3000
```

**初始化操作**

> 备注：返回的RedisTemplate 对象可根据自己的需求进行重载实现和配置序列化等等操作

```java
/**
 * @author larry.koo
 * @description 自定义多 Redis 数据源驱动
 * @date 2017/11/8 21:32
 * @slogon 站在巨人的肩膀上
 * @since 1.0.0
 */
@Configuration
public class MainConfig {

    @Autowired
    private CustomRedisProperties customRedisProperties;

    @Bean("redisTemplateSingle")
    @Qualifier("redisTemplateSingle")
    public RedisTemplate redisTemplateSingle() {
        // 其中 findById("ID") 的中的 ID 即为 yml 配置的实例唯一 ID 定义
        return RedisConfigBuilder.create(customRedisProperties.findById("exam-single")).build();
    }

    @Bean("redisTemplateCluster")
    @Qualifier("redisTemplateCluster")
    public RedisTemplate redisTemplateCluster() {
        return RedisConfigBuilder.create(customRedisProperties.findById("exam-cluster")).build();
    }
}
```

**数据操作, 基于 Spring 的依赖注入，按名称注入使用**

```java
/**
 * 单机调用操作对象注入
 */
@Autowired
private RedisTemplate redisTemplateSingle;

/**
 * 集群调用操作对象注入
 */
@Autowired
private RedisTemplate redisTemplateCluster;
```