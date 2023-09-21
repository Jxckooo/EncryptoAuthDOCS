# EncryptoAuth | Documentation

---

## Overview

`AuthLibrary` is a wrapper class for an authentication library that is designed to be portable across C, C++, C#, and compatible with both Windows and Linux.

## C# Usage

### Creating an Authenticator

To create an authenticator instance in C#, use the `Authenticator` class:

```csharp
string appId = "your_app_id";
string apiToken = "your_api_token";
string sha256 = "your_sha256_value";

using (AuthLibrary.Authenticator authenticator = new AuthLibrary.Authenticator(appId, apiToken, sha256))
{
    // Use the authenticator
    // Note: This will only start the tampering checks etc inside this using statement.
    // It is probably best to declare a null authenticator create the new object as soon as possible
    // in the application. This way, the tampering checks are always being done, checking if the HWID is banned, 
    // checking if the user is banned etc...
}

// Below is the other way
// E.g. WinForms

private AuthLibrary.Authenticator authenticator;

public Form1() {
    InitializeComponent();
    authenticator = AuthLibrary.Authenticator("your_app_id", "your_api_token", "your_sha256_value");
}
```

If you wanna access it in another form, consider passing it to that forms constructor and keeping the same instance across the whole application.

### Authenticating a User

To authenticate a user in C#, use the AuthenticateUser method:

```csharp
string username = "user123";
string password = "password123";
bool result = Convert.ToBoolean(authenticator.AuthenticateUser(username, password));

// If result is equal to true, success, otherwise failed.
```

### Registering a User

To register a user in C#, use the RegisterUser method:

```csharp
string username = "new_user";
string password = "new_password";
string email = "user@example.com";
string refCode = "ref123";

bool result = Convert.ToBoolean(authenticator.RegisterUser(username, password, email, refCode));

// If result is equal to true, success, otherwise failed.
```

### Logging User Activity

To log user activity in C#, use the LogUserActivity method:

```csharp 
string activity = "User logged in.";
bool result = Convert.ToBoolean(authenticator.LogUserActivity(activity));

// If result is equal to true, success, otherwise failed.
```

## C/C++ Usage

### Creating an Authenticator

In C/C++, you can create an authenticator using the following code:

```c
const char* appId = "your_app_id";
const char* apiToken = "your_api_token";
const char* sha256 = "your_sha256_value";

void* authenticator = CreateAuthenticator(appId, apiToken, sha256);

// Use the authenticator

DestroyAuthenticator(authenticator);
```

## Authenticating a User

To authenticate a user in C/C++, use the AuthenticateUser function:

```c
const char* username = "user123";
const char* password = "password123";
int result = AuthenticateUser(authenticator, username, password);
```

## Registering a User

To register a user in C/C++, use the RegisterUser function:

```c
const char* username = "new_user";
const char* password = "new_password";
const char* email = "user@example.com";
const char* refCode = "ref123";

int result = RegisterUser(authenticator, username, password, email, refCode);
```

## Logging User Activity

To log user activity in C/C++, use the LogUserActivity function:

```c
const char* activity = "User logged in.";
int result = LogUserActivity(authenticator, activity);
```

C++/CLI Usage (Windows Only)
If you are using C++/CLI on Windows, you can use the C++/CLI wrapper to interact with the library. This wrapper is specific to Windows.

C++/CLI Usage (Linux Only)
If you are using C++/CLI on Linux, you can use the Shared Library and Header file to interact with the library. Both libraries are the same, just built using different compilers.

Please note that you may need to adjust the code according to your project setup and library inclusion.
