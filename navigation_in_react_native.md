# Navigation in React Native (React Navigation)

A step-by-step guide to install and configure navigation in your React Native app.

---

## 1. Install Dependencies

```bash
npm install @react-navigation/native
npm install react-native-screens react-native-safe-area-context
npm install @react-navigation/native-stack
# iOS only (after install):
cd ios && pod install && cd ..
```

Or with Yarn:

```bash
yarn add @react-navigation/native react-native-screens react-native-safe-area-context @react-navigation/native-stack
```

---

## 2. Wrap with NavigationContainer

In `App.js`, import and wrap your navigators:

```jsx
import * as React from 'react';
import { NavigationContainer } from '@react-navigation/native';

export default function App() {
  return (
    <NavigationContainer>
      {/* Navigators go here */}
    </NavigationContainer>
  );
}
```

---

## 3. Create a Stack Navigator

```jsx
import { createNativeStackNavigator } from '@react-navigation/native-stack';
const Stack = createNativeStackNavigator();

function HomeScreen({ navigation }) {
  return (
    /* your UI */
    <Button
      title="Go to Details"
      onPress={() => navigation.navigate('Details')}
    />
  );
}
function DetailsScreen() {
  return (/* details UI */);
}

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

---

## 4. Bottom Tab Navigator

Install:

```bash
npm install @react-navigation/bottom-tabs
```

Usage:

```jsx
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
const Tab = createBottomTabNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator>
        <Tab.Screen name="Home" component={HomeScreen} />
        <Tab.Screen name="Settings" component={SettingsScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```

---

## 5. Passing Parameters

```js
// Navigate with params
navigation.navigate('Details', { itemId: 42 });

// Read in DetailsScreen
function DetailsScreen({ route }) {
  const { itemId } = route.params;
  // ...
}
```

---

## 6. Sharing State & Variables Across Screens

### A. Using React Context

1. Create and export a context in `App.js`:
   ```jsx
   import React, { createContext, useState } from 'react';
   export const AppContext = createContext();
   ```
2. Wrap your navigator with the provider:
   ```jsx
   export default function App() {
     const [user, setUser] = useState({ name: '' });
     return (
       <AppContext.Provider value={{ user, setUser }}>
         <NavigationContainer>
           {/* ...navigators */}
         </NavigationContainer>
       </AppContext.Provider>
     );
   }
   ```
3. Consume context in any screen:
   ```jsx
   import React, { useContext } from 'react';
   import { AppContext } from './App';

   function ProfileScreen() {
     const { user, setUser } = useContext(AppContext);
     // use or update `user` here
   }
   ```

### B. Other Approaches

- **Route params:** pass data via `navigation.navigate('Screen', { data })` (see “Passing Parameters”).  
- **Global stores:** use Redux, MobX or Zustand for larger apps.

---

## 7. Next Steps

- Explore drawer navigation: `@react-navigation/drawer`  
- Customize headers, screen options and animations  
- Deep linking: https://reactnavigation.org/docs/deep-linking
