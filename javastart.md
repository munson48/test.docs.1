# Java Client Toolkit

Getting started with the Java Client Toolkit (JCT)

## Basics

The JCT functionality focuses on the `NAServer`, your point of contact for the majority of features you will use to interact with a NetAcquire server. NAServer instances are singletons on a per-hostname/address basis.

```java
try {
    try ( NAServer svr = NAServer.getServer("172.20.0.20")) {
        NA_System system = svr.getSystem();
        String state = system.GetEntityState();
        System.out.println(state);
    }
} catch (Exception e) {
    e.printStackTrace();
}
```

## JDK8

Use of JCT requires JDK8. Due to the use of certain components of the Java framework, Java versions 9 and higher are not yet supported.