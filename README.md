📱 KampusPost – React Native Ödev 4
Bu proje, BGP201 dersi kapsamında React Native kullanılarak geliştirilmiş bir mobil uygulamadır.
Uygulama; Login, Register ve Home ekranlarından oluşur.
Proje kapsamında:
Ekranlar arası geçiş (React Navigation)
Form yapısı ve kontrolü
Register ekranında şifre tekrar kontrolü
API’den veri çekip listeleme (FlatList)
Konsol / DevTools çıktılarının incelenmesi
uygulanmıştır.
Uygulama, PDF ödev yönergesi ile birebir uyumludur.
📌 İçindekiler
Projenin Amacı
Kullanılan Teknolojiler
Kurulum (Windows)
Ekran Görüntüleri
Kod Yapısı
App.tsx (Navigation)
LoginScreen
RegisterScreen
HomeScreen (API + FlatList)
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
Android Emulator / Fiziksel Cihaz	Test ortamı (Windows)
Bu proje, Windows işletim sistemi üzerinde Android Emulator veya USB ile bağlanan fiziksel Android cihaz kullanılarak çalıştırılabilir.
🚀 Kurulum (Windows için)
0. Ön Gereksinimler
Windows ortamında projeyi çalıştırmak için aşağıdakilerin kurulu olması gerekir:
Node.js ve npm
Git
Java Development Kit (JDK) (React Native CLI için)
Android Studio
Android SDK
Bir adet Android sanal cihaz (Android Emulator)
veya USB ile bağlı fiziksel Android telefon
Android Studio kurulumunda SDK ve Platform-Tools paketlerinin yüklü olduğundan emin olmalısın.
Ayrıca ortam değişkenlerinde ANDROID_HOME ayarı yapılmış olmalıdır (React Native resmi dokümantasyonuna uygun şekilde).
