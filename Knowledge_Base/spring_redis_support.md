Spring Redis requires Redis 2.6+, JDK 1.6+
Supports Jedis, JRedis, SRP and Lettuce
Configuration through traditional XML file:
```
	<!-- Redis Configurations -->
	<bean id="jedisPoolConfig" class="redis.clients.jedis.JedisPoolConfig" />					  
	<bean id="jedisConnectionFactory" class="org.springframework.data.redis.connection.jedis.JedisConnectionFactory">
	 	<property name="hostName" value="${redis.host}" />
		<property name="port" value="${redis.port}" />
		<property name="usePool" value="true" />
		<property name="poolConfig" ref="jedisPoolConfig" />
	 </bean>
	<bean id="redisTemplate" class="org.springframework.data.redis.core.RedisTemplate"
	 	   p:connection-factory-ref="jedisConnectionFactory"/>
```

Redis provides support for transactions through the multi, exec, and discard commands.

@Cacheable
@CachePut: allows you update the cache without interfering with the execution of the method.
@CacheEvit