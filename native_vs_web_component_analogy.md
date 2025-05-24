# React Native vs Web React: Component Analogy

A quick reference showing how common React Native building blocks map to web React.

---

## View ↔ div

- **Native:**  
  ```jsx
  <View style={{ padding: 16, backgroundColor: '#eee' }}>
    {/* ... */}
  </View>
  ```
- **Web:**  
  ```jsx
  <div style={{ padding: '16px', backgroundColor: '#eee' }}>
    {/* ... */}
  </div>
  ```

---

## Text ↔ span / p

- **Native:**  
  ```jsx
  <Text style={{ fontSize: 18, color: '#333' }}>
    Hello, world!
  </Text>
  ```
- **Web:**  
  ```jsx
  <p style={{ fontSize: '18px', color: '#333' }}>
    Hello, world!
  </p>
  ```

---

## Image ↔ img

- **Native:**  
  ```jsx
  <Image source={{ uri: 'https://example.com/photo.jpg' }} style={{ width: 100, height: 100 }} />
  ```
- **Web:**  
  ```jsx
  <img src="https://example.com/photo.jpg" width="100" height="100" alt="" />
  ```

---

## ScrollView ↔ overflow:auto container

- **Native:**  
  ```jsx
  <ScrollView>
    {/* Scrollable content */}
  </ScrollView>
  ```
- **Web:**  
  ```jsx
  <div style={{ overflow: 'auto', height: '200px' }}>
    {/* Scrollable content */}
  </div>
  ```

---

## TextInput ↔ input

- **Native:**  
  ```jsx
  <TextInput
    placeholder="Enter text"
    style={{ borderWidth: 1, padding: 8 }}
  />
  ```
- **Web:**  
  ```jsx
  <input
    type="text"
    placeholder="Enter text"
    style={{ border: '1px solid #ccc', padding: '8px' }}
  />
  ```

---

## TouchableOpacity ↔ button / clickable div

- **Native:**  
  ```jsx
  <TouchableOpacity onPress={() => alert('Pressed!')}>
    <Text>Press me</Text>
  </TouchableOpacity>
  ```
- **Web:**  
  ```jsx
  <button onClick={() => alert('Pressed!')}>
    Press me
  </button>
  ```
