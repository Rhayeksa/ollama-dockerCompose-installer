# 🚀 Ollama Docker Compose Installer

Repository ini menyediakan **Docker Compose file** untuk menjalankan [Ollama](https://ollama.com/) di dalam container.  
File ini sudah mendukung **default environment variable**, sehingga fleksibel untuk berbagai kebutuhan.

---

## 📦 Fitur
- Menjalankan Ollama dengan **1 perintah**.
- Mendukung **persistensi data model** ke folder host.
- Variabel dapat dikonfigurasi lewat **`.env` file**.
- Port API bisa diubah sesuai kebutuhan.
- Opsi GPU NVIDIA sudah disiapkan (tinggal diaktifkan).

---

## 🛠️ Prasyarat
- [Docker](https://docs.docker.com/get-docker/)  
- [Docker Compose](https://docs.docker.com/compose/install/)  
- (Opsional) [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) jika ingin menggunakan GPU.

---

## 📂 Struktur
```
.
├── docker-compose.yml
├── .env (opsional)
└── README.md
```

---

## ⚙️ Konfigurasi

### 🔹 Variabel Default
Pada `docker-compose.yml` terdapat variabel berikut:

| Variabel        | Default Value | Deskripsi                          |
|-----------------|---------------|------------------------------------|
| `OLLAMA_VERSION` | `latest`      | Versi image Ollama                 |
| `OLLAMA_PORT`    | `11434`       | Port API Ollama                    |
| `OLLAMA_DIR`     | `./`          | Direktori data untuk model Ollama  |

### 🔹 Contoh `.env`
Jika ingin menyesuaikan konfigurasi, buat file `.env` di folder yang sama:

```env
OLLAMA_VERSION=latest
OLLAMA_PORT=12345
OLLAMA_DIR=/home/user/ollama_data/
```

---

## 🚀 Cara Menjalankan

1. Clone repository ini:
   ```bash
   git clone https://github.com/username/ollama-docker.git
   cd ollama-docker
   ```

2. (Opsional) Buat file `.env` jika ingin override default variabel.

3. Jalankan service:
   ```bash
   docker compose up -d
   ```

4. Periksa log:
   ```bash
   docker logs -f ollama_0_11_6
   ```

5. Uji koneksi API:
   ```bash
   curl http://localhost:11434/api/tags
   ```

---

## 🔧 GPU NVIDIA (Opsional)
Jika server memiliki GPU NVIDIA, aktifkan konfigurasi berikut di `docker-compose.yml`:

```yaml
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
```

Pastikan sudah menginstal [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html).

---

## 📝 Lisensi
MIT License. Silakan gunakan dan modifikasi sesuai kebutuhan.

---

## 💡 Catatan
- Default API berjalan di `http://localhost:11434`
- Data model akan tersimpan di folder sesuai `OLLAMA_DIR`
- Jika `OLLAMA_DIR=./` maka data akan ada di `.ollama/` di direktori project
- Pertama kali menjalankan model, Ollama akan mengunduh data → mungkin memakan waktu

---
