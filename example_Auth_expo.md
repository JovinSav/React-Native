# Auth Key storing example

## **Expo lib for this**

```
npx expo install expo-secure-store
```

## **How to use**

- add to plugins in app.json

```javascript
[
  "expo-secure-store",
  {
    configureAndroidBackup: true,
    faceIDPermission:
      "Allow $(PRODUCT_NAME) to access your Face ID biometric data.",
  },
];
```

- in the file u need to use

```javascript
import * as SecureStore from "expo-secure-store";
```

- how to to store a values secure

```javascript
async function save(key, value) {
  await SecureStore.setItemAsync(key, value);
}
```

- How to access a value

```javascript
async function getValueFor(key) {
  let result = await SecureStore.getItemAsync(key);
  if (result) {
    return result;
  } else {
    console.log('No values stored under that key.');
    return null;
  }
}
```

- How to delete a value

```javascript
async function removeValue(key) {
  await SecureStore.deleteItemAsync(key);
}
```

## **Complete Authentication Example**

```javascript
// Store token after login
async function storeUserSession(userToken, userRole) {
  try {
    await SecureStore.setItemAsync('userToken', userToken);
    await SecureStore.setItemAsync('userRole', userRole);
    return true;
  } catch (error) {
    console.error('Error storing credentials:', error);
    return false;
  }
}

// Get user token for authenticated requests
async function getUserToken() {
  try {
    const token = await SecureStore.getItemAsync('userToken');
    return token;
  } catch (error) {
    console.error('Error retrieving token:', error);
    return null;
  }
}

// Check if user is logged in
async function isAuthenticated() {
  const token = await getUserToken();
  return token !== null;
}

// Logout user by removing credentials
async function logout() {
  try {
    await SecureStore.deleteItemAsync('userToken');
    await SecureStore.deleteItemAsync('userRole');
    return true;
  } catch (error) {
    console.error('Error during logout:', error);
    return false;
  }
}
```

## **Important Notes**

- SecureStore is only available on native platforms (iOS/Android), not on web
- Values are stored as strings, so objects need to be JSON stringified:
  ```javascript
  // Storing object
  await SecureStore.setItemAsync('userData', JSON.stringify({
    id: 123,
    username: 'johndoe',
    role: 'admin'
  }));
  
  // Retrieving object
  const userData = JSON.parse(await SecureStore.getItemAsync('userData'));
  ```
- There's a size limit of 2048 bytes per value
- For web support, consider using a wrapper that falls back to localStorage with encryption
