# MATERI TUWEB 3 - PERTEMUAN 10
# IONIC PADA PLATFORM ANDROID & APLIKASI TERINTEGRASI

---

## 📋 INFORMASI MATA KULIAH

**Mata Kuliah**: Pemrograman Berbasis Perangkat Bergerak (MSIM4401)
**Pertemuan**: 10 (TUWEB 3)
**Pokok Bahasan**: Ionic pada Platform Android, Native API, Plugins, dan Aplikasi Terintegrasi
**Pendekatan**: Learning by Doing

---

## 🎯 TUJUAN PEMBELAJARAN

Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:

1. Memahami cara kerja Ionic pada platform Android
2. Melakukan instalasi dan konfigurasi Android development environment
3. Mengintegrasikan Native API dan Plugins ke dalam aplikasi Ionic
4. Mengakses data dari REST API eksternal
5. Membuild aplikasi Ionic menjadi file APK
6. Menjalankan aplikasi di perangkat Android nyata atau emulator
7. Memahami proses debugging aplikasi mobile
8. Membuat aplikasi terintegrasi dengan fitur native

---

## 📚 PRASYARAT

Sebelum memulai praktikum ini, pastikan Anda telah:

- ✅ Menyelesaikan Tuweb 1 (Pertemuan 6)
- ✅ Memahami dasar Ionic Framework dan Vue.js
- ✅ Memiliki komputer dengan spesifikasi:
  - RAM minimal 8GB (disarankan 16GB untuk emulator Android)
  - Storage kosong minimal 20GB
  - Sistem Operasi: Windows 10/11, macOS, atau Linux
- ✅ Koneksi internet yang stabil untuk download Android SDK

---

## 🛠️ PERSIAPAN LINGKUNGAN ANDROID

### Langkah 1: Instalasi Java Development Kit (JDK)

Android memerlukan JDK untuk proses build.

#### Untuk Windows:

1. **Download JDK**
   - Kunjungi: https://www.oracle.com/java/technologies/downloads/
   - Download **Java SE Development Kit 17** (versi LTS)
   - Pilih installer untuk Windows (contoh: `jdk-17_windows-x64_bin.exe`)

2. **Instalasi JDK**
   - Jalankan installer
   - Klik "Next"
   - Pilih lokasi instalasi (default: `C:\Program Files\Java\jdk-17\`)
   - Tunggu proses instalasi selesai
   - Klik "Close"

3. **Setting Environment Variable**

   **Langkah-langkah:**
   - Klik kanan "This PC" → Properties
   - Klik "Advanced system settings"
   - Klik tombol "Environment Variables"

   **Menambahkan JAVA_HOME:**
   - Di bagian "System variables", klik "New"
   - Variable name: `JAVA_HOME`
   - Variable value: `C:\Program Files\Java\jdk-17` (sesuaikan dengan lokasi instalasi)
   - Klik "OK"

   **Menambahkan ke PATH:**
   - Di "System variables", cari variable `Path`, klik "Edit"
   - Klik "New"
   - Tambahkan: `%JAVA_HOME%\bin`
   - Klik "OK" pada semua dialog

4. **Verifikasi Instalasi**
   ```bash
   java -version
   ```
   Output: `java version "17.0.x"`

   ```bash
   javac -version
   ```
   Output: `javac 17.0.x`

#### Untuk macOS:

```bash
# Menggunakan Homebrew
brew install openjdk@17

# Tambahkan ke PATH di ~/.zshrc atau ~/.bash_profile
echo 'export PATH="/usr/local/opt/openjdk@17/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

# Verifikasi
java -version
```

#### Untuk Linux (Ubuntu/Debian):

```bash
sudo apt update
sudo apt install openjdk-17-jdk

# Verifikasi
java -version
javac -version
```

---

### Langkah 2: Instalasi Android Studio

Android Studio menyediakan Android SDK yang diperlukan untuk build aplikasi.

1. **Download Android Studio**
   - Kunjungi: https://developer.android.com/studio
   - Download versi terbaru untuk OS Anda
   - File berukuran sekitar 1-2 GB

2. **Instalasi Android Studio**

   **Windows:**
   - Jalankan file installer (contoh: `android-studio-2023.x.x.xx-windows.exe`)
   - Klik "Next" pada welcome screen
   - Pilih komponen yang akan diinstall (biarkan semua tercentang)
   - Pilih lokasi instalasi (default atau custom)
   - Klik "Install"
   - Tunggu proses instalasi (bisa 10-30 menit)
   - Centang "Start Android Studio"
   - Klik "Finish"

3. **Setup Wizard Android Studio**

   Setelah Android Studio terbuka:

   **a. Import Settings**
   - Pilih "Do not import settings" (jika install pertama kali)
   - Klik "OK"

   **b. Data Sharing**
   - Pilih "Don't send" atau "Send" (sesuai preferensi)
   - Klik "Next"

   **c. Install Type**
   - Pilih **"Standard"** (recommended untuk pemula)
   - Klik "Next"

   **d. Select UI Theme**
   - Pilih "Light" atau "Darcula" (sesuai selera)
   - Klik "Next"

   **e. Verify Settings**
   - Akan menampilkan komponen yang akan didownload:
     - Android SDK
     - Android SDK Platform
     - Android Virtual Device
   - Total download sekitar 3-5 GB
   - Klik "Next"

   **f. License Agreement**
   - Baca setiap license
   - Pilih "Accept" untuk semua
   - Klik "Finish"

   **g. Downloading Components**
   - Proses download dan instalasi akan berjalan
   - Bisa memakan waktu 30 menit - 2 jam (tergantung internet)
   - Tunggu hingga selesai

   **h. Finish**
   - Klik "Finish"
   - Android Studio siap digunakan!

4. **Instalasi SDK Tools Tambahan**

   Setelah setup selesai:
   - Klik "More Actions" → "SDK Manager"

   **SDK Platforms:**
   - Centang "Show Package Details" di pojok kanan bawah
   - Expand "Android 13.0 (Tiramisu)" atau versi terbaru
   - Centang:
     - ✅ Android SDK Platform 33
     - ✅ Google APIs Intel x86 Atom System Image
   - Klik "Apply" → "OK"

   **SDK Tools:**
   - Klik tab "SDK Tools"
   - Centang:
     - ✅ Android SDK Build-Tools
     - ✅ Android SDK Command-line Tools
     - ✅ Android Emulator
     - ✅ Android SDK Platform-Tools
     - ✅ Google Play services
   - Klik "Apply" → "OK"
   - Tunggu proses instalasi

5. **Cek Lokasi Android SDK**

   Di SDK Manager, lihat "Android SDK Location":
   - Windows: biasanya `C:\Users\[Username]\AppData\Local\Android\Sdk`
   - macOS: `/Users/[Username]/Library/Android/sdk`
   - Linux: `/home/[Username]/Android/Sdk`

   **Catat path ini, akan digunakan nanti!**

---

### Langkah 3: Setting Environment Variable untuk Android

#### Windows:

1. **Buka Environment Variables** (seperti langkah JDK)

2. **Tambahkan ANDROID_HOME**
   - Variable name: `ANDROID_HOME`
   - Variable value: `C:\Users\[Username]\AppData\Local\Android\Sdk`
   - Ganti `[Username]` dengan username Windows Anda
   - Klik "OK"

3. **Update PATH**
   - Edit variable `Path`
   - Tambahkan:
     - `%ANDROID_HOME%\platform-tools`
     - `%ANDROID_HOME%\emulator`
     - `%ANDROID_HOME%\tools`
     - `%ANDROID_HOME%\tools\bin`

4. **Restart Command Prompt**

5. **Verifikasi**
   ```bash
   adb --version
   ```
   Seharusnya muncul versi adb (Android Debug Bridge)

#### macOS/Linux:

Tambahkan di `~/.zshrc` atau `~/.bash_profile`:

```bash
export ANDROID_HOME=$HOME/Library/Android/sdk  # macOS
# atau
export ANDROID_HOME=$HOME/Android/Sdk  # Linux

export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
```

Reload:
```bash
source ~/.zshrc  # atau source ~/.bash_profile
```

Verifikasi:
```bash
adb --version
```

---

### Langkah 4: Instalasi Gradle (Opsional, biasanya sudah include)

Gradle adalah build tool untuk Android.

**Cek apakah sudah terinstall:**
```bash
gradle --version
```

Jika belum, install:

**Windows:**
- Download dari: https://gradle.org/releases/
- Extract ke folder (contoh: `C:\Gradle`)
- Tambahkan `C:\Gradle\bin` ke PATH

**macOS:**
```bash
brew install gradle
```

**Linux:**
```bash
sudo apt install gradle
```

---

## 📱 MEMBUAT EMULATOR ANDROID

Emulator diperlukan untuk testing aplikasi tanpa perangkat fisik.

### Langkah 1: Membuat AVD (Android Virtual Device)

1. **Buka Android Studio**

2. **Akses AVD Manager**
   - Klik "More Actions" → "Virtual Device Manager"
   - Atau dari menu: Tools → Device Manager

3. **Create Virtual Device**
   - Klik tombol "Create Device"

4. **Pilih Hardware**
   - Category: Phone
   - Pilih device: **Pixel 5** (recommended)
   - Klik "Next"

5. **Pilih System Image**
   - Tab "Recommended"
   - Pilih: **Tiramisu (API 33)** atau versi terbaru
   - Jika ada tombol "Download", klik untuk download image (sekitar 1-2 GB)
   - Tunggu download selesai
   - Klik "Next"

6. **Verify Configuration**
   - AVD Name: biarkan default atau ganti (contoh: `Pixel_5_API_33`)
   - Startup orientation: Portrait
   - **Advanced Settings:**
     - RAM: 2048 MB atau lebih (jika RAM komputer cukup)
     - Internal Storage: 2048 MB
     - SD card: 512 MB
   - Klik "Finish"

7. **Jalankan Emulator (Test)**
   - Di AVD Manager, klik tombol ▶️ (Play) pada device yang baru dibuat
   - Tunggu emulator booting (pertama kali bisa 3-5 menit)
   - Jika berhasil, akan muncul layar Android

**Tips:**
- Jangan tutup emulator setelah dibuka, biarkan berjalan selama development
- Gunakan "Cold Boot" untuk booting penuh, "Quick Boot" untuk lebih cepat

---

## 🚀 PRAKTIKUM 1: BUILD APLIKASI IONIC KE ANDROID

### Persiapan

Kita akan menggunakan project dari Tuweb 1. Jika belum punya, buat project baru:

```bash
ionic start myApp tabs --type=vue
cd myApp
```

---

### Langkah 1: Menambahkan Platform Android

1. **Tambahkan Capacitor ke project**

   Capacitor adalah tool untuk membuild aplikasi web menjadi native mobile app.

   ```bash
   ionic integrations enable capacitor
   ```

   Atau jika sudah ada, skip langkah ini.

2. **Build project untuk production**

   ```bash
   ionic build
   ```

   **Penjelasan:**
   - Perintah ini akan mengkompilasi kode Vue/TypeScript menjadi HTML/CSS/JS
   - Hasil build ada di folder `dist/`
   - File-file ini yang akan di-package menjadi APK

   **Output:**
   ```
   ✔ Building...
   ✔ Copying web assets from dist to android/app/src/main/assets/public in 123 ms
   ```

3. **Tambahkan platform Android**

   ```bash
   npx cap add android
   ```

   **Penjelasan:**
   - `npx cap`: menjalankan Capacitor CLI
   - `add android`: menambahkan platform Android ke project
   - Akan membuat folder `android/` di project

   **Output:**
   ```
   ✔ Adding native android project in android in 45.32ms
   ✔ add in 45.45ms
   ✔ Copying web assets from dist to android/app/src/main/assets/public in 123.45ms
   ✔ Creating capacitor.config.json in 2.34ms
   ✔ copy android in 125.79ms
   ✔ Updating Android plugins in 4.56ms
   ✔ update android in 234.56ms
   ```

4. **Sync project dengan platform**

   Setiap kali ada perubahan di kode web, jalankan:
   ```bash
   npx cap sync
   ```

   **Penjelasan:**
   - Menyalin file web (dist/) ke folder android
   - Mengupdate plugin Capacitor
   - Memastikan kode web dan native sinkron

---

### Langkah 2: Membuka Project di Android Studio

1. **Buka project Android**

   ```bash
   npx cap open android
   ```

   Atau manual:
   - Buka Android Studio
   - File → Open
   - Pilih folder `android/` di dalam project Ionic Anda

2. **Gradle Sync**

   Android Studio akan otomatis melakukan Gradle Sync:
   - Mendownload dependencies
   - Mengkonfigurasi project
   - Proses ini bisa 2-10 menit (pertama kali)

   Jika ada error, klik "Try Again" atau "Sync Project with Gradle Files"

3. **Struktur Project Android**

   Di panel kiri, Anda akan melihat:
   ```
   android/
   ├── app/
   │   ├── src/
   │   │   └── main/
   │   │       ├── assets/
   │   │       │   └── public/  # File web Ionic
   │   │       ├── java/
   │   │       ├── res/          # Resources (icon, splash screen)
   │   │       └── AndroidManifest.xml
   │   └── build.gradle
   ├── build.gradle
   └── gradle/
   ```

---

### Langkah 3: Menjalankan di Emulator

1. **Pastikan emulator sudah berjalan**
   - Buka AVD Manager
   - Jalankan emulator yang sudah dibuat
   - Tunggu hingga home screen Android muncul

2. **Pilih device target**
   - Di toolbar Android Studio, akan ada dropdown device
   - Pilih emulator yang sedang berjalan (contoh: `Pixel 5 API 33`)

3. **Run aplikasi**
   - Klik tombol ▶️ (Run) di toolbar
   - Atau: Run → Run 'app'
   - Atau: `Shift + F10`

4. **Proses Build**
   - Gradle akan build project
   - Progress ada di panel "Build" di bawah
   - Proses pertama kali bisa 3-10 menit

5. **Aplikasi terbuka di emulator**
   - Jika berhasil, aplikasi akan otomatis install dan buka di emulator
   - Anda akan melihat aplikasi Ionic berjalan seperti aplikasi Android asli!

**Selamat! Aplikasi Ionic Anda sudah berjalan di Android!**

---

### Langkah 4: Build APK untuk Distribusi

Untuk membuat file APK yang bisa diinstall di perangkat manapun:

1. **Build → Build Bundle(s) / APK(s) → Build APK(s)**

2. **Tunggu proses build**
   - Progress di panel "Build"
   - Jika sukses, akan muncul notifikasi: "APK(s) generated successfully"

3. **Locate APK**
   - Klik "locate" pada notifikasi
   - Atau manual: `android/app/build/outputs/apk/debug/app-debug.apk`

4. **Install APK**
   - Copy file APK ke perangkat Android
   - Buka file APK di perangkat
   - Klik "Install"
   - (Mungkin perlu enable "Install from Unknown Sources")

**Catatan:**
- APK debug hanya untuk testing
- Untuk production, gunakan signed release APK

---

## 🔌 PRAKTIKUM 2: NATIVE API & PLUGINS

### Pengantar

Capacitor Plugins memungkinkan aplikasi Ionic mengakses fitur native perangkat seperti kamera, geolocation, storage, dll.

---

### Langkah 1: Menggunakan Plugin Geolocation

Mari kita buat fitur untuk mendapatkan lokasi pengguna.

1. **Install Plugin**

   ```bash
   npm install @capacitor/geolocation
   npx cap sync
   ```

2. **Buat halaman Location**

   Buat file `src/views/LocationPage.vue`:

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button default-href="/home"></ion-back-button>
        </ion-buttons>
        <ion-title>Geolocation</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <h2>Lokasi Saya</h2>

      <ion-card v-if="location">
        <ion-card-header>
          <ion-card-title>Koordinat</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <p><strong>Latitude:</strong> {{ location.latitude }}</p>
          <p><strong>Longitude:</strong> {{ location.longitude }}</p>
          <p><strong>Akurasi:</strong> {{ location.accuracy }} meter</p>
          <p><strong>Waktu:</strong> {{ locationTime }}</p>
        </ion-card-content>
      </ion-card>

      <ion-button expand="block" @click="getCurrentLocation" :disabled="loading">
        <ion-icon :icon="locateOutline" slot="start"></ion-icon>
        {{ loading ? 'Mengambil Lokasi...' : 'Dapatkan Lokasi' }}
      </ion-button>

      <ion-card v-if="error" color="danger">
        <ion-card-content>
          <strong>Error:</strong> {{ error }}
        </ion-card-content>
      </ion-card>

      <!-- Google Maps (iframe) -->
      <ion-card v-if="location">
        <ion-card-header>
          <ion-card-title>Peta</ion-card-title>
        </ion-card-header>
        <ion-card-content>
          <iframe
            :src="`https://maps.google.com/maps?q=${location.latitude},${location.longitude}&z=15&output=embed`"
            width="100%"
            height="300"
            style="border:0;"
            loading="lazy"
          ></iframe>
        </ion-card-content>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { Geolocation } from '@capacitor/geolocation';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonBackButton,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonButton,
  IonIcon
} from '@ionic/vue';
import { locateOutline } from 'ionicons/icons';

interface LocationData {
  latitude: number;
  longitude: number;
  accuracy: number;
}

const location = ref<LocationData | null>(null);
const locationTime = ref('');
const loading = ref(false);
const error = ref('');

const getCurrentLocation = async () => {
  loading.value = true;
  error.value = '';

  try {
    // Request permission
    const permission = await Geolocation.requestPermissions();

    if (permission.location === 'granted') {
      // Get current position
      const coordinates = await Geolocation.getCurrentPosition({
        enableHighAccuracy: true,
        timeout: 10000
      });

      location.value = {
        latitude: coordinates.coords.latitude,
        longitude: coordinates.coords.longitude,
        accuracy: coordinates.coords.accuracy
      };

      locationTime.value = new Date().toLocaleString('id-ID');
    } else {
      error.value = 'Izin lokasi ditolak. Harap aktifkan di pengaturan.';
    }
  } catch (err: any) {
    error.value = `Gagal mendapatkan lokasi: ${err.message}`;
    console.error('Error getting location:', err);
  } finally {
    loading.value = false;
  }
};
</script>

<style scoped>
h2 {
  margin-bottom: 20px;
}

ion-card p {
  margin: 8px 0;
}

iframe {
  border-radius: 8px;
}
</style>
```

3. **Tambahkan route**

```typescript
// router/index.ts
import LocationPage from '../views/LocationPage.vue';

{
  path: '/location',
  name: 'Location',
  component: LocationPage
}
```

4. **Tambahkan permission di AndroidManifest.xml**

   File: `android/app/src/main/AndroidManifest.xml`

   Tambahkan sebelum tag `<application>`:

```xml
<!-- Geolocation Permissions -->
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

5. **Sync dan Run**

```bash
npx cap sync
npx cap open android
```

6. **Test di emulator**
   - Di emulator, buka menu Extended Controls (ikon "...")
   - Pilih "Location"
   - Set lokasi manual atau gunakan GPX file
   - Klik tombol "Dapatkan Lokasi" di app

---

### Langkah 2: Menggunakan Plugin Camera

Mari buat fitur ambil foto.

1. **Install Plugin**

```bash
npm install @capacitor/camera
npx cap sync
```

2. **Buat halaman Camera**

   File: `src/views/CameraPage.vue`

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button default-href="/home"></ion-back-button>
        </ion-buttons>
        <ion-title>Camera</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <h2>Ambil Foto</h2>

      <ion-card v-if="photo">
        <img :src="photo" alt="Foto" />
        <ion-card-content>
          <p>Foto berhasil diambil!</p>
        </ion-card-content>
      </ion-card>

      <div v-else class="placeholder">
        <ion-icon :icon="cameraOutline" style="font-size: 80px; color: #ccc;"></ion-icon>
        <p>Belum ada foto</p>
      </div>

      <ion-button expand="block" @click="takePicture">
        <ion-icon :icon="cameraOutline" slot="start"></ion-icon>
        Ambil Foto
      </ion-button>

      <ion-button expand="block" fill="outline" @click="selectFromGallery">
        <ion-icon :icon="imagesOutline" slot="start"></ion-icon>
        Pilih dari Galeri
      </ion-button>

      <ion-button
        v-if="photo"
        expand="block"
        color="danger"
        fill="clear"
        @click="deletePhoto"
      >
        Hapus Foto
      </ion-button>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { Camera, CameraResultType, CameraSource } from '@capacitor/camera';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonBackButton,
  IonCard,
  IonCardContent,
  IonButton,
  IonIcon
} from '@ionic/vue';
import { cameraOutline, imagesOutline } from 'ionicons/icons';

const photo = ref<string | null>(null);

const takePicture = async () => {
  try {
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.DataUrl,
      source: CameraSource.Camera
    });

    photo.value = image.dataUrl || null;
  } catch (error) {
    console.error('Error taking photo:', error);
  }
};

const selectFromGallery = async () => {
  try {
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: false,
      resultType: CameraResultType.DataUrl,
      source: CameraSource.Photos
    });

    photo.value = image.dataUrl || null;
  } catch (error) {
    console.error('Error selecting photo:', error);
  }
};

const deletePhoto = () => {
  photo.value = null;
};
</script>

<style scoped>
.placeholder {
  text-align: center;
  padding: 60px 20px;
  background: #f5f5f5;
  border-radius: 8px;
  margin-bottom: 20px;
}

.placeholder p {
  color: #999;
  margin-top: 10px;
}

ion-card img {
  width: 100%;
  height: auto;
}

h2 {
  margin-bottom: 20px;
}
</style>
```

3. **Tambahkan permission di AndroidManifest.xml**

```xml
<!-- Camera Permissions -->
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

4. **Tambahkan route dan test!**

---

### Langkah 3: Storage (Menyimpan Data Lokal)

1. **Install Plugin**

```bash
npm install @capacitor/preferences
npx cap sync
```

2. **Contoh penggunaan:**

```typescript
import { Preferences } from '@capacitor/preferences';

// Simpan data
await Preferences.set({
  key: 'name',
  value: 'Anton Prafanto'
});

// Ambil data
const { value } = await Preferences.get({ key: 'name' });
console.log('Name:', value);

// Hapus data
await Preferences.remove({ key: 'name' });

// Hapus semua
await Preferences.clear();
```

3. **Implementasi di aplikasi To-Do**

   Edit `TodoPage.vue` dari Tuweb 1, tambahkan storage:

```typescript
import { Preferences } from '@capacitor/preferences';
import { onMounted } from 'vue';

// Load data saat component mounted
onMounted(async () => {
  const { value } = await Preferences.get({ key: 'todos' });
  if (value) {
    todos.value = JSON.parse(value);
  }
});

// Simpan setiap kali ada perubahan
const saveTodos = async () => {
  await Preferences.set({
    key: 'todos',
    value: JSON.stringify(todos.value)
  });
};

// Update method addTodo, toggleTodo, deleteTodo untuk memanggil saveTodos()
```

---

## 🌐 PRAKTIKUM 3: AKSES DATA DARI REST API

### Studi Kasus: Aplikasi Info Cuaca

Mari buat aplikasi yang mengambil data cuaca dari API.

---

### Langkah 1: Instalasi HTTP Client

```bash
npm install axios
```

---

### Langkah 2: Membuat Service API

Buat folder dan file baru: `src/services/weatherService.ts`

```typescript
import axios from 'axios';

const API_BASE_URL = 'https://api.open-meteo.com/v1';

export interface WeatherData {
  time: string[];
  temperature_2m: number[];
}

export interface WeatherResponse {
  latitude: number;
  longitude: number;
  hourly: WeatherData;
}

export const weatherService = {
  /**
   * Mendapatkan data cuaca berdasarkan koordinat
   */
  async getWeather(latitude: number, longitude: number): Promise<WeatherResponse> {
    try {
      const response = await axios.get(`${API_BASE_URL}/forecast`, {
        params: {
          latitude,
          longitude,
          hourly: 'temperature_2m,relative_humidity_2m,precipitation,weather_code',
          timezone: 'Asia/Jakarta'
        }
      });

      return response.data;
    } catch (error) {
      console.error('Error fetching weather:', error);
      throw error;
    }
  },

  /**
   * Mendapatkan cuaca kota tertentu (preset)
   */
  async getWeatherByCity(city: string): Promise<WeatherResponse> {
    const cities: { [key: string]: { lat: number; lon: number } } = {
      'jakarta': { lat: -6.2, lon: 106.8 },
      'samarinda': { lat: -0.5, lon: 117.15 },
      'balikpapan': { lat: -1.24, lon: 116.89 },
      'surabaya': { lat: -7.25, lon: 112.75 },
      'bandung': { lat: -6.9, lon: 107.6 },
    };

    const coords = cities[city.toLowerCase()];
    if (!coords) {
      throw new Error('Kota tidak ditemukan');
    }

    return this.getWeather(coords.lat, coords.lon);
  }
};
```

---

### Langkah 3: Membuat Halaman Weather

File: `src/views/WeatherPage.vue`

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button default-href="/home"></ion-back-button>
        </ion-buttons>
        <ion-title>Info Cuaca</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <!-- City Selector -->
      <div class="ion-padding">
        <ion-item>
          <ion-label>Pilih Kota</ion-label>
          <ion-select v-model="selectedCity" @ionChange="loadWeather">
            <ion-select-option value="jakarta">Jakarta</ion-select-option>
            <ion-select-option value="samarinda">Samarinda</ion-select-option>
            <ion-select-option value="balikpapan">Balikpapan</ion-select-option>
            <ion-select-option value="surabaya">Surabaya</ion-select-option>
            <ion-select-option value="bandung">Bandung</ion-select-option>
          </ion-select>
        </ion-item>
      </div>

      <!-- Loading -->
      <div v-if="loading" class="ion-padding ion-text-center">
        <ion-spinner></ion-spinner>
        <p>Memuat data cuaca...</p>
      </div>

      <!-- Error -->
      <ion-card v-if="error" color="danger">
        <ion-card-content>
          <strong>Error:</strong> {{ error }}
        </ion-card-content>
      </ion-card>

      <!-- Weather Data -->
      <div v-if="weatherData && !loading">
        <!-- Current Weather -->
        <ion-card>
          <ion-card-header>
            <ion-card-subtitle>Cuaca Saat Ini</ion-card-subtitle>
            <ion-card-title style="text-transform: capitalize;">
              {{ selectedCity }}
            </ion-card-title>
          </ion-card-header>
          <ion-card-content>
            <div class="current-temp">
              <ion-icon :icon="sunnyOutline" style="font-size: 48px; color: #FFA500;"></ion-icon>
              <h1>{{ currentTemp }}°C</h1>
            </div>
            <p><strong>Koordinat:</strong> {{ weatherData.latitude }}°, {{ weatherData.longitude }}°</p>
          </ion-card-content>
        </ion-card>

        <!-- Hourly Forecast -->
        <div class="ion-padding">
          <h3>Prakiraan Per Jam</h3>
          <ion-card v-for="(item, index) in hourlyForecast" :key="index">
            <ion-card-content>
              <ion-grid>
                <ion-row class="ion-align-items-center">
                  <ion-col size="6">
                    <strong>{{ formatTime(item.time) }}</strong>
                  </ion-col>
                  <ion-col size="6" class="ion-text-right">
                    <span style="font-size: 20px; font-weight: bold;">
                      {{ item.temp }}°C
                    </span>
                  </ion-col>
                </ion-row>
              </ion-grid>
            </ion-card-content>
          </ion-card>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import { weatherService, WeatherResponse } from '@/services/weatherService';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonButtons,
  IonBackButton,
  IonItem,
  IonLabel,
  IonSelect,
  IonSelectOption,
  IonCard,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonCardContent,
  IonSpinner,
  IonIcon,
  IonGrid,
  IonRow,
  IonCol
} from '@ionic/vue';
import { sunnyOutline } from 'ionicons/icons';

const selectedCity = ref('samarinda');
const weatherData = ref<WeatherResponse | null>(null);
const loading = ref(false);
const error = ref('');

const currentTemp = computed(() => {
  if (!weatherData.value) return 0;
  return weatherData.value.hourly.temperature_2m[0].toFixed(1);
});

const hourlyForecast = computed(() => {
  if (!weatherData.value) return [];

  // Ambil 12 jam pertama
  return weatherData.value.hourly.time.slice(0, 12).map((time, index) => ({
    time,
    temp: weatherData.value!.hourly.temperature_2m[index].toFixed(1)
  }));
});

const formatTime = (timeStr: string) => {
  const date = new Date(timeStr);
  return date.toLocaleString('id-ID', {
    day: 'numeric',
    month: 'short',
    hour: '2-digit',
    minute: '2-digit'
  });
};

const loadWeather = async () => {
  loading.value = true;
  error.value = '';

  try {
    weatherData.value = await weatherService.getWeatherByCity(selectedCity.value);
  } catch (err: any) {
    error.value = err.message || 'Gagal memuat data cuaca';
    console.error('Error loading weather:', err);
  } finally {
    loading.value = false;
  }
};

// Load initial data
loadWeather();
</script>

<style scoped>
.current-temp {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  margin: 20px 0;
}

.current-temp h1 {
  font-size: 48px;
  margin: 0;
  font-weight: bold;
}

h3 {
  margin-bottom: 15px;
  color: #333;
}

ion-card {
  margin: 10px 0;
}
</style>
```

---

### Langkah 4: Tambahkan Route dan Test

1. **Tambahkan route**

2. **Build dan run di Android**

```bash
ionic build
npx cap sync
npx cap open android
```

3. **Test aplikasi:**
   - Pilih kota
   - Lihat data cuaca muncul
   - Data diambil dari API real-time!

---

## 🎨 PRAKTIKUM 4: APLIKASI TERINTEGRASI LENGKAP

### Studi Kasus: Aplikasi "My Daily"

Kita akan membuat aplikasi yang menggabungkan semua fitur:
- To-Do List dengan Storage
- Weather Info dengan API
- Location dengan GPS
- Profile dengan Camera

---

### Struktur Aplikasi

```
MyDaily App
├── Home (Dashboard)
├── To-Do List
├── Weather
├── Location
└── Profile
```

---

### Langkah 1: Buat Halaman Home dengan Tabs

File: `src/views/HomePage.vue` (update)

```vue
<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>

      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="dashboard" href="/tabs/dashboard">
          <ion-icon :icon="homeOutline"></ion-icon>
          <ion-label>Home</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="todo" href="/tabs/todo">
          <ion-icon :icon="checkboxOutline"></ion-icon>
          <ion-label>Tugas</ion-label>
          <ion-badge v-if="pendingTodos > 0">{{ pendingTodos }}</ion-badge>
        </ion-tab-button>

        <ion-tab-button tab="weather" href="/tabs/weather">
          <ion-icon :icon="cloudOutline"></ion-icon>
          <ion-label>Cuaca</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="profile" href="/tabs/profile">
          <ion-icon :icon="personOutline"></ion-icon>
          <ion-label>Profil</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonPage,
  IonTabs,
  IonTabBar,
  IonTabButton,
  IonIcon,
  IonLabel,
  IonBadge,
  IonRouterOutlet
} from '@ionic/vue';
import {
  homeOutline,
  checkboxOutline,
  cloudOutline,
  personOutline
} from 'ionicons/icons';

const pendingTodos = ref(3); // Bisa diganti dengan data real
</script>
```

---

### Langkah 2: Dashboard

File: `src/views/DashboardPage.vue`

```vue
<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>My Daily App</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <!-- Greeting -->
      <ion-card>
        <ion-card-content>
          <h2>Halo, {{ userName }}! 👋</h2>
          <p>{{ greeting }}</p>
        </ion-card-content>
      </ion-card>

      <!-- Quick Stats -->
      <ion-grid>
        <ion-row>
          <ion-col size="6">
            <ion-card color="primary" button @click="router.push('/tabs/todo')">
              <ion-card-content class="stat-card">
                <ion-icon :icon="checkboxOutline" style="font-size: 32px;"></ion-icon>
                <h3>{{ todoStats.total }}</h3>
                <p>Tugas</p>
              </ion-card-content>
            </ion-card>
          </ion-col>
          <ion-col size="6">
            <ion-card color="success" button>
              <ion-card-content class="stat-card">
                <ion-icon :icon="checkmarkDoneOutline" style="font-size: 32px;"></ion-icon>
                <h3>{{ todoStats.completed }}</h3>
                <p>Selesai</p>
              </ion-card-content>
            </ion-card>
          </ion-col>
        </ion-row>
      </ion-grid>

      <!-- Current Weather -->
      <h3>Cuaca Hari Ini</h3>
      <ion-card button @click="router.push('/tabs/weather')">
        <ion-card-content>
          <ion-grid>
            <ion-row class="ion-align-items-center">
              <ion-col size="3">
                <ion-icon :icon="sunnyOutline" style="font-size: 48px; color: #FFA500;"></ion-icon>
              </ion-col>
              <ion-col>
                <h2>{{ currentWeather.temp }}°C</h2>
                <p>{{ currentWeather.city }}</p>
              </ion-col>
            </ion-row>
          </ion-grid>
        </ion-card-content>
      </ion-card>

      <!-- Quick Actions -->
      <h3>Aksi Cepat</h3>
      <ion-list>
        <ion-item button @click="router.push('/location')">
          <ion-icon :icon="locateOutline" slot="start"></ion-icon>
          <ion-label>Lihat Lokasi Saya</ion-label>
        </ion-item>

        <ion-item button @click="router.push('/camera')">
          <ion-icon :icon="cameraOutline" slot="start"></ion-icon>
          <ion-label>Ambil Foto</ion-label>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonCard,
  IonCardContent,
  IonGrid,
  IonRow,
  IonCol,
  IonIcon,
  IonList,
  IonItem,
  IonLabel
} from '@ionic/vue';
import {
  checkboxOutline,
  checkmarkDoneOutline,
  sunnyOutline,
  locateOutline,
  cameraOutline
} from 'ionicons/icons';

const router = useRouter();

const userName = ref('Anton');
const todoStats = ref({
  total: 8,
  completed: 3
});

const currentWeather = ref({
  temp: 28,
  city: 'Samarinda'
});

const greeting = computed(() => {
  const hour = new Date().getHours();
  if (hour < 12) return 'Selamat pagi! Semangat hari ini!';
  if (hour < 18) return 'Selamat siang! Tetap produktif!';
  return 'Selamat malam! Istirahat yang cukup ya!';
});

onMounted(() => {
  // Load data dari storage/API
});
</script>

<style scoped>
h2 {
  margin: 0;
  font-size: 24px;
}

h3 {
  margin: 20px 0 10px 0;
  color: #666;
}

.stat-card {
  text-align: center;
  padding: 15px;
}

.stat-card h3 {
  font-size: 32px;
  margin: 10px 0 5px 0;
  color: white;
}

.stat-card p {
  margin: 0;
  color: white;
  opacity: 0.9;
}
</style>
```

---

### Langkah 3: Update Router

File: `src/router/index.ts`

```typescript
import { createRouter, createWebHistory } from '@ionic/vue-router';
import { RouteRecordRaw } from 'vue-router';
import TabsPage from '../views/TabsPage.vue';

const routes: Array<RouteRecordRaw> = [
  {
    path: '/',
    redirect: '/tabs/dashboard'
  },
  {
    path: '/tabs/',
    component: TabsPage,
    children: [
      {
        path: '',
        redirect: '/tabs/dashboard'
      },
      {
        path: 'dashboard',
        component: () => import('@/views/DashboardPage.vue')
      },
      {
        path: 'todo',
        component: () => import('@/views/TodoPage.vue')
      },
      {
        path: 'weather',
        component: () => import('@/views/WeatherPage.vue')
      },
      {
        path: 'profile',
        component: () => import('@/views/ProfilePage.vue')
      }
    ]
  },
  // Routes lainnya (location, camera, dll)
  {
    path: '/location',
    component: () => import('@/views/LocationPage.vue')
  },
  {
    path: '/camera',
    component: () => import('@/views/CameraPage.vue')
  }
]

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes
})

export default router
```

---

## 🐛 DEBUGGING & TESTING

### Chrome DevTools untuk Android

1. **Enable USB Debugging di perangkat Android:**
   - Settings → About Phone
   - Tap "Build Number" 7x untuk enable Developer Options
   - Settings → Developer Options
   - Enable "USB Debugging"

2. **Connect perangkat ke komputer**

3. **Buka Chrome di komputer:**
   - URL: `chrome://inspect`
   - Perangkat Android akan muncul
   - Klik "inspect" pada aplikasi Anda

4. **Gunakan DevTools seperti biasa:**
   - Console untuk log
   - Network untuk monitoring API calls
   - Elements untuk inspect UI

---

### Logcat (Android Studio)

1. **Buka Android Studio**

2. **Window → Logcat** (atau panel di bawah)

3. **Filter log:**
   - Pilih device/emulator
   - Pilih app package
   - Filter by severity: Verbose, Debug, Info, Warn, Error

4. **Tambahkan log di kode:**

```typescript
console.log('Debug info:', data);
console.error('Error occurred:', error);
```

Log akan muncul di Logcat.

---

## 📦 BUILD RELEASE APK

Untuk distribusi ke pengguna.

### Langkah 1: Generate Signing Key

```bash
keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```

Isi informasi:
- Password keystore
- Nama, organisasi, dll.

**Simpan file `my-release-key.keystore` dengan aman!**

---

### Langkah 2: Konfigurasi Gradle

File: `android/app/build.gradle`

Tambahkan di bagian `android`:

```gradle
signingConfigs {
    release {
        storeFile file('my-release-key.keystore')
        storePassword 'password-anda'
        keyAlias 'my-key-alias'
        keyPassword 'password-anda'
    }
}

buildTypes {
    release {
        signingConfig signingConfigs.release
        minifyEnabled false
        proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
    }
}
```

---

### Langkah 3: Build Release

Di Android Studio:
1. **Build → Generate Signed Bundle / APK**
2. Pilih **APK**
3. **Next**
4. Pilih keystore file
5. Masukkan password
6. **Next**
7. Pilih **release**
8. **Finish**

APK release ada di: `android/app/release/app-release.apk`

---

## 📝 LATIHAN MANDIRI

### Latihan 1: Notifikasi Lokal

Install plugin:
```bash
npm install @capacitor/local-notifications
```

Implementasikan:
1. Notifikasi pengingat tugas
2. Notifikasi cuaca buruk
3. Notifikasi harian

### Latihan 2: Share

Implementasikan fitur share:
```bash
npm install @capacitor/share
```

Buat fitur:
- Share lokasi
- Share foto
- Share to-do list

### Latihan 3: Network Status

Deteksi koneksi internet:
```bash
npm install @capacitor/network
```

Tampilkan banner jika offline.

---

## 🎯 RANGKUMAN

Pada praktikum ini, Anda telah mempelajari:

### 1. **Android Development Environment**
- ✅ Instalasi JDK, Android Studio, Gradle
- ✅ Setup environment variables
- ✅ Membuat dan mengelola AVD (emulator)

### 2. **Build Android App**
- ✅ Menambahkan platform Android dengan Capacitor
- ✅ Build dan run di emulator
- ✅ Generate APK debug dan release

### 3. **Native Plugins**
- ✅ Geolocation untuk akses GPS
- ✅ Camera untuk foto
- ✅ Preferences untuk storage lokal

### 4. **REST API Integration**
- ✅ Menggunakan Axios untuk HTTP requests
- ✅ Membuat service layer
- ✅ Handling loading dan error states

### 5. **Aplikasi Terintegrasi**
- ✅ Tab-based navigation
- ✅ Dashboard dengan multiple widgets
- ✅ Integrasi semua fitur (storage, API, native)

---

## 📚 REFERENSI

1. **Capacitor Documentation**
   - https://capacitorjs.com/docs

2. **Capacitor Plugins**
   - https://capacitorjs.com/docs/plugins

3. **Android Developer Guide**
   - https://developer.android.com/guide

4. **Axios Documentation**
   - https://axios-http.com/docs/intro

---

## 📧 PENUTUP

Selamat! Anda telah menyelesaikan Praktikum 2!

**Pertemuan selanjutnya (Tuweb 3 - Pertemuan 14):**
- Project akhir: Aplikasi lengkap dengan semua fitur
- Best practices dan optimization
- Publishing ke Google Play Store

**Terus berlatih dan eksplorasi fitur-fitur lain!**

---

**Disusun oleh:**
Anton Prafanto, S.Kom, M.T.
Dosen Program Studi Informatika
Universitas Mulawarman
Tutor Universitas Terbuka

**Mata Kuliah:** Pemrograman Berbasis Perangkat Bergerak (MSIM4401)
**Tahun:** 2025
