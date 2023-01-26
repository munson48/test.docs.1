# Java Client Toolkit Setup

To fit into your application use case, certain boilerplate may be necessary. This page assumes knowledge of some core Java APIs.

## Authentication

When authentication is required by the server, use the login() method to attempt login. If the authentication state is not known in advance, attempt login and handle errors to determine what needs to occur.

```java
server.login();
```

Specifically, look for

- **CredentialExpiredException** Current user's password must be changed before login permitted
- **LoginException** User login failed, current user login credentials not authorized
- **IOException** Communications failure, unable to log in

### Logging in

```java
// example with password authentication
server.setAuthentication(new PasswordAuthentication("user", "password".toCharArray()));
server.login();
Authenticator.Permission permissions = svr.getPermissions(); // what permissionlevel does this user have?

// ...your applicaiton here...

// *ALWAYS* log out or sessions may get used up
server.logout();
```

## Boilerplate

To support certain security options, the following mechanics may be necessary.

### Mandating encrypted communications

If you want the JCT API communications to refuse to communicate over unencrypted mediums, you can set the security mode on the NAServer instance.

```java
server.setSecurityRequired(true);
```

### HTTPS



#### Hostname verification

A default hostnamer verifier does basic verification. If you desire stronger control over verification, you may substitute or extend ours.

See: [javax.net.ssl.HostnameVerifier](https://docs.oracle.com/javase/8/docs/api/javax/net/ssl/HostnameVerifier.html)

```java
HttpsURLConnection.setDefaultHostnameVerifier(new SSLManager.NaHostnameVerifier());
```

### 