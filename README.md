📱 KampusPost – React Native Ödev 4
Bu proje, BGP201 dersi kapsamında React Native kullanılarak geliştirilmiş bir mobil uygulamadır.
Uygulama; Login, Register ve Home ekranlarından oluşur.
Proje kapsamında:
Ekranlar arası geçiş
Form yapısı ve kontrolü
Register ekranında şifre tekrar kontrolü
API’den veri çekip listeleme
Konsol / DevTools çıktılarının incelenmesi
uygulanmıştır.
Uygulama, PDF ödev yönergesi ile birebir uyumludur.
📌 İçindekiler
Projenin Amacı
Kullanılan Teknolojiler
Kurulum
Ekran Görüntüleri
Kod Yapısı
App.tsx
LoginScreen
RegisterScreen
HomeScreen
Konsol / DevTools Çıktıları
Proje Klasör Yapısı
Sonuç
🎯 Projenin Amacı
Bu ödevde amaç:
React Navigation ile ekranlar arası geçiş yapmak
Login / Register form yapısını oluşturmak
Register ekranında şifre tekrar kontrolü yapmak
API’den veri çekip Home ekranında FlatList ile listelemek
DevTools / Console çıktılarıyla veri akışını gözlemlemek
🧩 Kullanılan Teknolojiler
Teknoloji	Açıklama
React Native v0.82	Mobil uygulama geliştirme
@react-navigation/native	Navigation container
@react-navigation/native-stack	Stack navigator
react-native-screens	Navigation performansı
react-native-safe-area-context	Güvenli alan yönetimi
Android Emulator / Fiziksel Cihaz	Test ortamı
Bu proje, Windows işletim sistemi üzerinde Android Emulator veya USB ile bağlanan fiziksel Android cihaz kullanılarak çalıştırılabilir.
🚀 Kurulum
0. Ön Gereksinimler
Windows ortamında projeyi çalıştırmak için aşağıdakilerin kurulu olması gerekir:
Node.js ve npm
Git
Java Development Kit
Android Studio
Android SDK
Bir adet Android sanal cihaz
veya USB ile bağlı fiziksel Android telefon
Android Studio kurulumunda SDK ve Platform-Tools paketlerinin yüklü olduğundan emin olmalısın.
Ayrıca ortam değişkenlerinde ANDROID_HOME ayarı yapılmış olmalıdır
1. Projeyi İndirme
git clone <proje-github-linki>
cd KampusPost
2. Bağımlılıkların Yüklenmesi
npm install
npm install @react-navigation/native @react-navigation/native-stack
npm install react-native-screens react-native-safe-area-context
Tüm komutları Windows Terminal veya PowerShell üzerinden proje klasörü içinde çalıştırmalısın.
3. Metro Bundler Başlatma
Ayrı bir terminal penceresinde:
npx react-native start
4. Uygulamayı Android’de Çalıştırma
Android Emulator veya USB ile bağlı gerçek cihaz açıkken:
npx react-native run-android
Bu komut:
Android uygulamasını derler
Emulator veya bağlı cihaza yükler
Uygulamayı otomatik olarak başlatır
iOS tarafı Windows’ta desteklenmediği için npx react-native run-ios komutu Windows’ta çalışmaz. Bu proje Windows’ta Android üzerinden test edilmiştir.
🖼 Ekran Görüntüleri
Aşağıdaki ekran görüntüleri proje çıktısını göstermektedir:
Login Ekranı
Register Ekranı
Şifreler Uyuşmuyor Uyarısı
HomeScreen – API’den gelen post listesinin gösterimi
Login & HomeScreen Konsol Çıktıları

🧱 Kod Yapısı
🧭 App.tsx
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

import LoginScreen from './components/LoginScreen';
import RegisterScreen from './components/RegisterScreen';
import HomeScreen from './components/HomeScreen';

const Stack = createNativeStackNavigator();

const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Login">
        <Stack.Screen name="Login" component={LoginScreen} options={{ title: 'Giriş' }} />
        <Stack.Screen name="Register" component={RegisterScreen} options={{ title: 'Kayıt Ol' }} />
        <Stack.Screen name="Home" component={HomeScreen} options={{ title: 'Ana Sayfa' }} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};

export default App;
🔐 LoginScreen
import React, { useState } from 'react';
import { View, Button, StyleSheet } from 'react-native';
import { useNavigation } from '@react-navigation/native';
import CustomInput from './CustomInput';

const LoginScreen = () => {
  const navigation = useNavigation<any>();

  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  const onLoginPress = () => {
    console.log('Login values:', { email, password });
    navigation.navigate('Home');
  };

  const onRegisterPress = () => {
    navigation.navigate('Register');
  };

  return (
    <View style={styles.container}>
      <CustomInput placeholder="E-posta" value={email} onChangeText={setEmail} />
      <CustomInput placeholder="Şifre" value={password} onChangeText={setPassword} secureTextEntry />

      <Button title="Giriş Yap" onPress={onLoginPress} />
      <Button title="Kayıt Ol" onPress={onRegisterPress} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', padding: 16 },
});

export default LoginScreen;
📝 RegisterScreen
import React, { useState } from 'react';
import { View, Button, StyleSheet, Alert } from 'react-native';
import CustomInput from './CustomInput';

const RegisterScreen = () => {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [passwordAgain, setPasswordAgain] = useState('');

  const onRegisterPress = () => {
    if (password !== passwordAgain) {
      Alert.alert('Hata', 'Şifreler uyuşmuyor!');
      return;
    }

    console.log('Kayıt başarılı', { email, password });
  };

  return (
    <View style={styles.container}>
      <CustomInput placeholder="E-posta" value={email} onChangeText={setEmail} />
      <CustomInput placeholder="Şifre" value={password} onChangeText={setPassword} secureTextEntry />
      <CustomInput placeholder="Şifre Tekrar" value={passwordAgain} onChangeText={setPasswordAgain} secureTextEntry />

      <Button title="Kayıt Ol" onPress={onRegisterPress} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', padding: 16 },
});

export default RegisterScreen;
🏠 HomeScreen – API + FlatList
import React, { useEffect, useState } from 'react';
import { View, Text, StyleSheet, ActivityIndicator, FlatList } from 'react-native';

const HomeScreen = () => {
  const [posts, setPosts] = useState<any[]>([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const fetchPosts = async () => {
      const response = await fetch('https://jsonplaceholder.typicode.com/posts');
      const data = await response.json();
      setPosts(data);
      console.log('Posts:', data);
      setLoading(false);
    };

    fetchPosts();
  }, []);

  if (loading) {
    return (
      <View style={styles.center}>
        <ActivityIndicator />
        <Text>Yükleniyor...</Text>
      </View>
    );
  }

  return (
    <View style={styles.container}>
      <FlatList
        data={posts}
        keyExtractor={(item) => item.id.toString()}
        renderItem={({ item }) => (
          <View style={styles.postItem}>
            <Text style={styles.title}>{item.title}</Text>
            <Text>{item.body}</Text>
          </View>
        )}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16 },
  center: { flex: 1, justifyContent: 'center', alignItems: 'center' },
  postItem: { marginBottom: 16 },
  title: { fontSize: 16, fontWeight: 'bold', marginBottom: 4 },
});

export default HomeScreen;
🧪 Konsol / DevTools Çıktıları
Örnek loglar:
Login values: { email: 'betultest.com', password: '123456' }

Posts: (100) [...]
Bu loglar, login formundan dönen değerleri ve HomeScreen’de API’den çekilen post listesini doğrulamak için kullanılmıştır.
📂 Proje Klasör Yapısı
KampusPost
│── App.tsx
│── package.json
│── index.js
│── tsconfig.json
│
└── components
     ├── LoginScreen.tsx
     ├── RegisterScreen.tsx
     ├── HomeScreen.tsx
     └── CustomInput.tsx
✅ Sonuç
Bu proje ile:
React Native’de temel ekran yapısı
Navigation kullanımı
Form yönetimi ve validasyon
API entegrasyonu ve FlatList ile listeleme
Windows ortamında Android Emulator / cihaz üzerinde çalıştırma
başarıyla uygulanmıştır.
