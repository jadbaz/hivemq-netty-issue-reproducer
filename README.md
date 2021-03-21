# HiveMQ Client JDK 9+ Netty Warnings Reproducer
Issue at [hivemq/hivemq-mqtt-client/issues/473](https://github.com/hivemq/hivemq-mqtt-client/issues/473)

## Output with different JDKs
### JDK 8
```
> Task :Main.main()
13:03:10.724 [main] DEBUG io.netty.util.internal.logging.InternalLoggerFactory - Using SLF4J as the default logging framework
13:03:10.739 [main] DEBUG io.netty.util.NetUtil - -Djava.net.preferIPv4Stack: false
13:03:10.739 [main] DEBUG io.netty.util.NetUtil - -Djava.net.preferIPv6Addresses: false
13:03:11.669 [main] DEBUG io.netty.util.NetUtil - Loopback interface: lo (Software Loopback Interface 1, 127.0.0.1)
13:03:11.692 [main] DEBUG io.netty.util.internal.PlatformDependent - Platform: Windows
13:03:11.695 [main] DEBUG io.netty.util.internal.PlatformDependent0 - -Dio.netty.noUnsafe: false
13:03:11.695 [main] DEBUG io.netty.util.internal.PlatformDependent0 - Java version: 8
13:03:11.696 [main] DEBUG io.netty.util.internal.PlatformDependent0 - sun.misc.Unsafe.theUnsafe: available
13:03:11.698 [main] DEBUG io.netty.util.internal.PlatformDependent0 - sun.misc.Unsafe.copyMemory: available
13:03:11.698 [main] DEBUG io.netty.util.internal.PlatformDependent0 - java.nio.Buffer.address: available
13:03:11.699 [main] DEBUG io.netty.util.internal.PlatformDependent0 - direct buffer constructor: available
13:03:11.700 [main] DEBUG io.netty.util.internal.PlatformDependent0 - java.nio.Bits.unaligned: available, true
13:03:11.701 [main] DEBUG io.netty.util.internal.PlatformDependent0 - jdk.internal.misc.Unsafe.allocateUninitializedArray(int): unavailable prior to Java9
13:03:11.701 [main] DEBUG io.netty.util.internal.PlatformDependent0 - java.nio.DirectByteBuffer.<init>(long, int): available
13:03:11.701 [main] DEBUG io.netty.util.internal.PlatformDependent - sun.misc.Unsafe: available
13:03:11.702 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.tmpdir: C:\Users\jad.baz\AppData\Local\Temp (java.io.tmpdir)
13:03:11.702 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.bitMode: 64 (sun.arch.data.model)
13:03:11.705 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.maxDirectMemory: 3790077952 bytes
13:03:11.705 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.uninitializedArrayAllocationThreshold: -1
13:03:11.707 [main] DEBUG io.netty.util.internal.CleanerJava6 - java.nio.ByteBuffer.cleaner(): available
13:03:11.708 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.noPreferDirect: false
13:03:11.710 [main] DEBUG io.netty.util.NetUtil - Failed to get SOMAXCONN from sysctl and file \proc\sys\net\core\somaxconn. Default: 200

BUILD SUCCESSFUL in 4s
3 actionable tasks: 1 executed, 2 up-to-date
```

### JDK 9+
```
> Task :Main.main()
13:01:52.726 [main] DEBUG io.netty.util.internal.logging.InternalLoggerFactory - Using SLF4J as the default logging framework
13:01:52.736 [main] DEBUG io.netty.util.NetUtil - -Djava.net.preferIPv4Stack: false
13:01:52.736 [main] DEBUG io.netty.util.NetUtil - -Djava.net.preferIPv6Addresses: false
13:01:53.691 [main] DEBUG io.netty.util.NetUtil - Loopback interface: lo (Software Loopback Interface 1, 127.0.0.1)
13:01:53.714 [main] DEBUG io.netty.util.internal.PlatformDependent - Platform: Windows
13:01:53.718 [main] DEBUG io.netty.util.internal.PlatformDependent0 - -Dio.netty.noUnsafe: false
13:01:53.718 [main] DEBUG io.netty.util.internal.PlatformDependent0 - Java version: 11
13:01:53.721 [main] DEBUG io.netty.util.internal.PlatformDependent0 - sun.misc.Unsafe.theUnsafe: available
13:01:53.722 [main] DEBUG io.netty.util.internal.PlatformDependent0 - sun.misc.Unsafe.copyMemory: available
13:01:53.724 [main] DEBUG io.netty.util.internal.PlatformDependent0 - java.nio.Buffer.address: available
13:01:53.724 [main] DEBUG io.netty.util.internal.PlatformDependent0 - direct buffer constructor: unavailable
java.lang.UnsupportedOperationException: Reflective setAccessible(true) disabled
	at io.netty.util.internal.ReflectionUtil.trySetAccessible(ReflectionUtil.java:31) ~[netty-common-4.1.48.Final.jar:4.1.48.Final]
	at io.netty.util.internal.PlatformDependent0$4.run(PlatformDependent0.java:225) ~[netty-common-4.1.48.Final.jar:4.1.48.Final]
	at java.security.AccessController.doPrivileged(Native Method) ~[?:?]
	at io.netty.util.internal.PlatformDependent0.<clinit>(PlatformDependent0.java:219) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at io.netty.util.internal.PlatformDependent.isAndroid(PlatformDependent.java:289) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at io.netty.util.internal.PlatformDependent.<clinit>(PlatformDependent.java:92) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at io.netty.util.NetUtil$1.run(NetUtil.java:260) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at io.netty.util.NetUtil$1.run(NetUtil.java:253) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at java.security.AccessController.doPrivileged(Native Method) ~[?:?]
	at io.netty.util.NetUtil.<clinit>(NetUtil.java:253) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at com.hivemq.client.internal.util.InetSocketAddressUtil.create(InetSocketAddressUtil.java:32) [hivemq-mqtt-client-1.2.1.jar:?]
	at com.hivemq.client.internal.mqtt.MqttClientTransportConfigImpl.<clinit>(MqttClientTransportConfigImpl.java:34) [hivemq-mqtt-client-1.2.1.jar:?]
	at com.hivemq.client.internal.mqtt.MqttRxClientBuilderBase.<init>(MqttRxClientBuilderBase.java:46) [hivemq-mqtt-client-1.2.1.jar:?]
	at com.hivemq.client.internal.mqtt.MqttRxClientBuilderBase$Choose.<init>(MqttRxClientBuilderBase.java:216) [hivemq-mqtt-client-1.2.1.jar:?]
	at com.hivemq.client.mqtt.MqttClient.builder(MqttClient.java:59) [hivemq-mqtt-client-1.2.1.jar:?]
	at Main.main(Main.java:5) [main/:?]
13:01:53.739 [main] DEBUG io.netty.util.internal.PlatformDependent0 - java.nio.Bits.unaligned: available, true
13:01:53.740 [main] DEBUG io.netty.util.internal.PlatformDependent0 - jdk.internal.misc.Unsafe.allocateUninitializedArray(int): unavailable
java.lang.IllegalAccessException: class io.netty.util.internal.PlatformDependent0$6 cannot access class jdk.internal.misc.Unsafe (in module java.base) because module java.base does not export jdk.internal.misc to unnamed module @48793bef
	at jdk.internal.reflect.Reflection.newIllegalAccessException(Reflection.java:361) ~[?:?]
	at java.lang.reflect.AccessibleObject.checkAccess(AccessibleObject.java:591) ~[?:?]
	at java.lang.reflect.Method.invoke(Method.java:558) ~[?:?]
	at io.netty.util.internal.PlatformDependent0$6.run(PlatformDependent0.java:335) ~[netty-common-4.1.48.Final.jar:4.1.48.Final]
	at java.security.AccessController.doPrivileged(Native Method) ~[?:?]
	at io.netty.util.internal.PlatformDependent0.<clinit>(PlatformDependent0.java:326) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at io.netty.util.internal.PlatformDependent.isAndroid(PlatformDependent.java:289) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at io.netty.util.internal.PlatformDependent.<clinit>(PlatformDependent.java:92) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at io.netty.util.NetUtil$1.run(NetUtil.java:260) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at io.netty.util.NetUtil$1.run(NetUtil.java:253) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at java.security.AccessController.doPrivileged(Native Method) ~[?:?]
	at io.netty.util.NetUtil.<clinit>(NetUtil.java:253) [netty-common-4.1.48.Final.jar:4.1.48.Final]
	at com.hivemq.client.internal.util.InetSocketAddressUtil.create(InetSocketAddressUtil.java:32) [hivemq-mqtt-client-1.2.1.jar:?]
	at com.hivemq.client.internal.mqtt.MqttClientTransportConfigImpl.<clinit>(MqttClientTransportConfigImpl.java:34) [hivemq-mqtt-client-1.2.1.jar:?]
	at com.hivemq.client.internal.mqtt.MqttRxClientBuilderBase.<init>(MqttRxClientBuilderBase.java:46) [hivemq-mqtt-client-1.2.1.jar:?]
	at com.hivemq.client.internal.mqtt.MqttRxClientBuilderBase$Choose.<init>(MqttRxClientBuilderBase.java:216) [hivemq-mqtt-client-1.2.1.jar:?]
	at com.hivemq.client.mqtt.MqttClient.builder(MqttClient.java:59) [hivemq-mqtt-client-1.2.1.jar:?]
	at Main.main(Main.java:5) [main/:?]
13:01:53.741 [main] DEBUG io.netty.util.internal.PlatformDependent0 - java.nio.DirectByteBuffer.<init>(long, int): unavailable
13:01:53.741 [main] DEBUG io.netty.util.internal.PlatformDependent - sun.misc.Unsafe: available
13:01:53.742 [main] DEBUG io.netty.util.internal.PlatformDependent - maxDirectMemory: 4263510016 bytes (maybe)
13:01:53.742 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.tmpdir: C:\Users\jad.baz\AppData\Local\Temp (java.io.tmpdir)
13:01:53.743 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.bitMode: 64 (sun.arch.data.model)
13:01:53.744 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.maxDirectMemory: -1 bytes
13:01:53.745 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.uninitializedArrayAllocationThreshold: -1
13:01:53.747 [main] DEBUG io.netty.util.internal.CleanerJava9 - java.nio.ByteBuffer.cleaner(): available
13:01:53.747 [main] DEBUG io.netty.util.internal.PlatformDependent - -Dio.netty.noPreferDirect: false
13:01:53.749 [main] DEBUG io.netty.util.NetUtil - Failed to get SOMAXCONN from sysctl and file \proc\sys\net\core\somaxconn. Default: 200

BUILD SUCCESSFUL in 13s
3 actionable tasks: 1 executed, 2 up-to-date

```