# What is it?

Flowdocs allows you to quickly describe all possible outcomes of a given feature / screen / function.
It can describe the very top level of business logic as well as low level interactions within the code itself.
It's easily maintainable, especially with git version control.
Applicable for new features descriptions: just make changes in the given piece of logic and push it to the repo. Anyone can see the diff and easily understand what exactly need to be changed.
You can use the same approach to describe client-side UI features as well as server-side logic.
Multiple instances of the code Flowdocs can be easily interconnected.

# How it works

Let's say we have a mobile app, that is connected to api server. In the given case our goal is to discribe authentication process.

***

## Artboards

![Artboards](./assets/artboards.png)

***

## Client side

## Legend

```
|  - scene
>  - action
/  - initial state
=  - result
?  - if else statement
~  - request to server
```
## Scenes

### Login
```
/ "Login" button is disabled until "email" and "password" inputs are filled
> Enter email and password; tap "LOG IN"
  ? email is malformed
    = snackbar message "Email is malformed"
  ? password is incorrect
    = snackbar message "Incorrect password"
  ? else
    = show loading indicator
    ~ signIn
> tap "Forgot Your Password?"
  | PasswordRecovery
> tap social authentication buttons
  ~ socialAuth
```

### PasswordRecovery
```
/ "RESET PASSWORD" button disabled until email input filled
> enter email, tap "RESET PASSWORD"
  ~ recoverPassword
> tap "CANCEL"
  | SignIn
```

### SignUp
```
/ "SIGN UP" button disabled until "email" and "password" inputs are filled
> Enter email and password; tap "SIGN UP"
  ? email malformed
    = snackbar message "Email is malformed"
  ? password incorrect
    = snackbar message "Incorrect password"
  ? else
    = show loading indicator
    ~ signUp
> tap "Forgot password"
  | PasswordRecovery
> tap social authentication buttons
  ~ socialAuth
```

***

## Server side

## Legend
```
$  - function, that can be induced only by server
?  - if/else statement
{} - incoming data
=  - result
~  - response/call to client
```

## Api methods

### signIn
```
{
  email,
  password,
}
? email invalid
  ~ snackbar message "Email is invalid"
? password invalid
  ~ snackbar message "Password is invalid"
? else
  = find user by email in database
    ? user not found
      ~ snackbar message "Email not found"
    ? password incorrect
      ~ snackbar message "Email not found"
    ? else
      $ openUserSession
```

### openUserSession
```
...
```

### signUp
```
{
  email,
  password,
}
? email invalid
  ~ snackbar message "Email is invalid"
? password invalid
  ~ snackbar message "Password is invalid"
? else
  = find user by email in database
    ? user found
      ~ snackbar message "User with this email already exists"
    ? else
      $ createNewUser
```

### createNewUser
```
...
```

***

