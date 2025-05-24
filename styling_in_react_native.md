# Styling in React Native (Basics)

Learn how to style components with React Native’s built-in APIs.

---

## 1. Inline Styles

You can pass a plain object directly to the `style` prop:

```jsx
<View style={{ padding: 16, backgroundColor: '#f0f0f0' }}>
  <Text style={{ fontSize: 18, color: '#333' }}>Hello!</Text>
</View>
```

Good for quick tweaks, but not optimal for reuse.

---

## 2. StyleSheet.create

Extract styles into a centralized object:

```jsx
import { StyleSheet, View, Text } from 'react-native';

const styles = StyleSheet.create({
  container: {
    padding: 16,
    backgroundColor: '#f0f0f0',
  },
  title: {
    fontSize: 18,
    color: '#333',
  },
});

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Hello!</Text>
    </View>
  );
}
```

`StyleSheet.create` also locks styles for performance.

---

## 3. Flexbox Layout

React Native uses Flexbox by default:

```jsx
const styles = StyleSheet.create({
  row: { flexDirection: 'row' },
  centered: { justifyContent: 'center', alignItems: 'center' },
});
```

- `flexDirection`: row | column  
- `justifyContent`: space distribution  
- `alignItems`: cross-axis alignment  

---

## 4. Layout Examples

Use Flexbox and fixed dimensions to create common layouts:

```jsx
import { View, Text, StyleSheet } from 'react-native';

function LayoutDemo() {
  return (
    <View style={styles.container}>
      <View style={styles.header}><Text>Header</Text></View>
      <View style={styles.content}>
        <View style={styles.left}><Text>Left</Text></View>
        <View style={styles.right}><Text>Right</Text></View>
      </View>
      <View style={styles.footer}><Text>Footer</Text></View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1 },
  header: {
    height: 60,
    backgroundColor: '#ddd',
    justifyContent: 'center',
    alignItems: 'center'
  },
  content: {
    flex: 1,
    flexDirection: 'row'
  },
  left: {
    flex: 1,
    backgroundColor: '#f9c2ff',
    justifyContent: 'center',
    alignItems: 'center'
  },
  right: {
    flex: 2,
    backgroundColor: '#c2f9ff',
    justifyContent: 'center',
    alignItems: 'center'
  },
  footer: {
    height: 50,
    backgroundColor: '#ddd',
    justifyContent: 'center',
    alignItems: 'center'
  }
});
```

---

## Container Size Examples

Examples of different container sizes:

```jsx
import { View, Text, StyleSheet, Dimensions } from 'react-native';
const { width, height } = Dimensions.get('window');

function ContainerSizes() {
  return (
    <View style={styles.wrapper}>
      <View style={styles.fullScreen}><Text>Full Screen</Text></View>
      <View style={styles.halfScreen}><Text>Half Screen</Text></View>
      <View style={styles.box}><Text>100×100 Box</Text></View>
      <View style={styles.percentageBox}><Text>80% Width</Text></View>
    </View>
  );
}

const styles = StyleSheet.create({
  wrapper: { flex: 1, padding: 16 },
  fullScreen: {
    flex: 1,
    backgroundColor: '#fde',
    justifyContent: 'center',
    alignItems: 'center',
  },
  halfScreen: {
    height: height / 2,
    backgroundColor: '#edf',
    justifyContent: 'center',
    alignItems: 'center',
    marginVertical: 8,
  },
  box: {
    width: 100,
    height: 100,
    backgroundColor: '#def',
    justifyContent: 'center',
    alignItems: 'center',
    marginVertical: 8,
  },
  percentageBox: {
    width: '80%',
    height: 50,
    backgroundColor: '#efd',
    justifyContent: 'center',
    alignItems: 'center',
    marginVertical: 8,
  },
});
```

---

## 5. Common Style Properties

- **Text**: `fontSize`, `fontWeight`, `color`, `textAlign`.  
- **View**: `padding`, `margin`, `borderRadius`, `backgroundColor`, `width`, `height`.  
- **Image**: `resizeMode` (cover/contain), `borderRadius`.  

Example:

```jsx
<Text style={{ fontWeight: 'bold', textAlign: 'center' }}>Bold centered</Text>
```

---

## 6. Percentages & Dimensions

- Percent values work for width/height: `{ width: '80%' }`.  
- Use `Dimensions` API for screen size:

```js
import { Dimensions } from 'react-native';
const { width, height } = Dimensions.get('window');
```

- `PixelRatio` helps with density-aware sizing.

---

## 7. Platform-Specific Styles

Use `Platform` module or style arrays:

```js
import { Platform, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  text: {
    ...Platform.select({
      ios: { fontFamily: 'Helvetica' },
      android: { fontFamily: 'Roboto' },
    }),
  },
});
```

Or:

```jsx
<Text style={[styles.text, Platform.OS === 'android' && { color: 'green' }]} />
```

---

## 8. Styling Libraries

- **styled-components/native**: familiar CSS-in-JS API.  
- **React Native Paper** / **NativeBase**: prebuilt component kits.  

---

## 9. Tips & Next Steps

- Group common values (colors, spacing) in a separate file.  
- Use theme/context for light/dark modes.  
- Explore Style Variables and responsive units.  

---

## 10. Organizing Styles

Use a clear folder/file structure and naming convention:

- Component-level styles  
  Keep styles next to each component:
  ```
  MyComponent/
  ├─ index.js
  └─ styles.js
  ```
  ```js
  // styles.js
  import { StyleSheet } from 'react-native';
  export default StyleSheet.create({
    container: { /* ... */ },
    title: { /* ... */ },
  });
  ```
  In `index.js`:
  ```js
  import styles from './styles';
  ```

- Screen-level styles  
  Group each screen similarly:
  ```
  screens/
  └─ HomeScreen/
     ├─ HomeScreen.js
     └─ styles.js
  ```

- Shared / theme styles  
  Centralize colors, spacing, typography:
  ```
  theme/
  ├─ colors.js
  ├─ spacing.js
  └─ styles.js
  ```

File-naming tips:
- Use `styles.js` or `<Component>.styles.js`
- Export a default StyleSheet
- Name style objects in camelCase (e.g., `container`, `headerTitle`)

---

## Resources

- Official docs: https://reactnative.dev/docs/style  
- Flexbox cheatsheet: https://flexboxfroggy.com  
- Styled-components: https://styled-components.com  

- React Native Directory (community components): https://reactnative.directory/  
- React Native Elements (free UI toolkit): https://reactnativeelements.com/  
- React Native Paper (Material Design): https://callstack.github.io/react-native-paper/  
- NativeBase (cross-platform UI kit): https://nativebase.io/  
- UI Kitten (customizable themeable components): https://akveo.github.io/react-native-ui-kitten/  
- Tailwind RN (utility-first styling): https://github.com/vadimdemedes/tailwind-rn  
- Expo Snack (live code examples & templates): https://snack.expo.dev/
