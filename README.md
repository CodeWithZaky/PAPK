Berikut penjelasan kode untuk membantu Anda membuat presentasi di kuliah:

---

### **1. Pendahuluan**
Kode ini adalah program untuk **remote light control** menggunakan **ESP32** dan platform **Blynk**. Sistem memungkinkan pengguna untuk mengontrol relay melalui aplikasi Blynk dari perangkat seluler atau dashboard web.

---

### **2. Penjelasan Kode**

#### **Bagian Konfigurasi**
- **BLYNK_TEMPLATE_ID, BLYNK_TEMPLATE_NAME, BLYNK_AUTH_TOKEN**: 
  - Identifikasi proyek di server Blynk.
  - Token autentikasi digunakan untuk menghubungkan perangkat dengan aplikasi Blynk.
- **SSID dan Password WiFi**:
  - Informasi untuk menghubungkan ESP32 ke jaringan WiFi.

#### **Pin Definisi**
- **relay1_pin, relay2_pin, relay3_pin, relay4_pin**:
  - Pin GPIO ESP32 yang dihubungkan ke modul relay.
- **button1_vpin, button2_vpin, button3_vpin, button4_vpin**:
  - Virtual pins untuk komunikasi antara aplikasi Blynk dan ESP32.

#### **State Relai**
- Variabel `relay1_state`, `relay2_state`, `relay3_state`, dan `relay4_state` digunakan untuk melacak status ON/OFF masing-masing relay.

---

#### **3. Fungsi Utama**

**a. BLYNK_CONNECTED()**  
Fungsi ini dipanggil saat ESP32 berhasil terhubung ke server Blynk. ESP32 akan menyinkronkan status relay dengan aplikasi Blynk menggunakan:
```cpp
Blynk.syncVirtual(button1_vpin);
```

**b. BLYNK_WRITE()**  
Fungsi ini menangani perubahan status pada virtual pin yang berasal dari aplikasi Blynk. Contoh:
```cpp
BLYNK_WRITE(button1_vpin) {
  relay1_state = param.asInt(); // Membaca status (0 atau 1)
  digitalWrite(relay1_pin, relay1_state); // Mengatur relay
}
```
Setiap relay dikontrol melalui fungsi serupa.

**c. setup()**  
Konfigurasi awal:
1. **Serial.begin(115200)**: Untuk debugging.
2. **pinMode()**: Mengatur pin relay sebagai output.
3. **digitalWrite(HIGH)**: Memastikan semua relay mati saat perangkat dinyalakan.
4. **Blynk.begin()**: Menghubungkan ESP32 ke server Blynk.

**d. loop()**  
Fungsi utama yang berjalan terus-menerus:
1. **Blynk.run()**: Menjaga koneksi ke server Blynk.
2. **timer.run()**: Menjalankan fungsi yang dijadwalkan (meskipun saat ini belum ada fungsi timer di kode).

---

### **4. Alur Kerja Sistem**
1. **ESP32 Terhubung ke WiFi**:
   - Perangkat menghubungkan ke server Blynk dengan autentikasi token.
2. **Pengguna Mengontrol Relay**:
   - Melalui aplikasi Blynk, pengguna menekan tombol untuk mengaktifkan atau mematikan relay.
3. **ESP32 Merespons**:
   - Perubahan status tombol dikirim ke ESP32 melalui fungsi `BLYNK_WRITE()`, yang kemudian mengontrol relay.

---

### **5. Diagram Koneksi**
**ESP32 ke Modul Relay**:
- Relay 1: GPIO13
- Relay 2: GPIO12
- Relay 3: GPIO14
- Relay 4: GPIO27

---

### **6. Kelebihan Sistem**
1. **Kontrol Jarak Jauh**: Dapat mengontrol relay dari mana saja selama perangkat terhubung ke internet.
2. **Integrasi dengan Blynk**: Mudah diatur dan dikustomisasi.
3. **Fleksibel**: Dapat diperluas untuk mengontrol lebih banyak perangkat.

---

### **7. Kesimpulan**
Kode ini sederhana dan efisien untuk proyek **IoT Remote Light Control** menggunakan ESP32 dan Blynk. Anda dapat mengembangkan lebih lanjut dengan menambahkan fitur seperti timer atau pengontrol otomatis.

Semoga penjelasan ini membantu! Jika Anda memerlukan tambahan diagram atau ilustrasi untuk presentasi, beri tahu saya.
