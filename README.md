# forgotpassword
Password recovery actions with Flutterflow &amp; Supabase

Basic custom action code for password recovery in Supabase. 

```
Future changePassword(String? newPassword) async {
  final response = await SupaFlow.client.auth
      .updateUser(UserAttributes(password: newPassword));

  if (response.user != null) {
    return true;
  } else {
    return false;
  }
}
```

Custom action code to send errors returned by Supabase to a Flutterflow app state variable

```
Future<bool> changePasswordError(String? newPassword) async {
  try {
    final response = await SupaFlow.client.auth
        .updateUser(UserAttributes(password: newPassword));

    // Return true if the response contains a user
    return response.user != null;
  } catch (error) {
    // Handle errors if needed
    print('Error: $error');
    FFAppState().update(() {
      FFAppState().customError = 'Error: $error';
    });
    // Indicate that the password change failed
    return false;
  }
}
```
