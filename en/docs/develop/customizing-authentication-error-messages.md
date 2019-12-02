# Customizing Authentication Error Messages

WSO2 Identity Server has standard error messages for different
authentication errors that are encountered. See [Error Codes and
Descriptions](../../develop/error-codes-and-descriptions)
for more information on the standard error codes and descriptions of
those errors. There are three types of custom errors handled here:

-   Invalid credentials
-   Invalid User
-   Account Lock

!!! note
    Account Lock errors are returned only when account locking is
    enabled on the server. Refer [User Account Locking and Account
    Disabling](../../learn/user-account-locking-and-account-disabling)
    document to enable account locking.
    

Do the following to customize these error messages.

## Show Authentication Failure Reason in The Response

Add the following properties to the `deployment.toml` file found in the `<IS_HOME>/repository/conf` folder and enable the authenticator to be able to customize error messages.

``` toml
[authentication.authenticator.basic.parameters]
showAuthFailureReason = true
```

The following query parameters are sent to the web application from authentication endpoint.

-   errorCode
-   failedUsername
-   remainingAttempts

The error messages can be customized based on these query parameters in the jsp files as in  `         authenticationendpoint/login.jsp        `

### Mask the Error Response values

Mask the **user does not exist** error code **(17001)** with the
**invalid credentials** error code **(17002)**. Set
`maskUserNotExistsErrorCode` to `true` in the
`<IS_HOME>/repository/conf/deployment.toml` file.
```toml
[authentication.authenticator.basic.parameters] 
showAuthFailureReason = true
maskUserNotExistsErrorCode = true 
```

To omit error response parameters add the error parameters to be omitted
to `errorParamsToOmit` in the
`<IS_HOME>/repository/conf/deployment.toml` file. Applicable values
`errorCode,failedUsername,remainingAttempts,lockedReason`. By
default no error params will be omitted.

```toml
[authentication.authenticator.basic.parameters] 
showAuthFailureReason = true
errorParamsToOmit = "failedUsername,remainingAttempts" 
```