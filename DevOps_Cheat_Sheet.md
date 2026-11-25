# CHEAT SHEET DEVOPS
## Terminal, Git, GitHub, Docker & Docker Compose

Dokumentasi perintah fundamental yang dipelajari untuk mengelola project, version control, container, dan persiapan deployment.

---

# 1. TERMINAL / COMMAND LINE

Terminal digunakan untuk berinteraksi dengan sistem operasi melalui perintah.

## Navigasi folder

| Command | Fungsi |
|---|---|
| `pwd` | Menampilkan direktori aktif |
| `ls` | Melihat isi folder |
| `ls -la` | Melihat seluruh file termasuk hidden files |
| `cd nama-folder` | Masuk ke folder |
| `cd ..` | Naik satu folder |
| `cd ~` | Kembali ke Home |
| `cd /path/folder` | Masuk ke direktori tertentu |

## Mengelola file dan folder

| Command | Fungsi |
|---|---|
| `mkdir nama-folder` | Membuat folder |
| `mkdir -p folder/subfolder` | Membuat folder bertingkat |
| `touch nama-file` | Membuat file kosong |
| `cat nama-file` | Membaca isi file |
| `nano nama-file` | Mengedit file menggunakan Nano |
| `cp file tujuan` | Menyalin file |
| `mv file tujuan` | Memindahkan atau mengganti nama file |
| `rm nama-file` | Menghapus file |
| `rm -r nama-folder` | Menghapus folder dan isinya |

**Perhatian:** `rm` menghapus file. Periksa nama file sebelum menjalankan perintah.

## Shortcut Nano

| Shortcut | Fungsi |
|---|---|
| `Control + O` | Menyimpan file |
| `Enter` | Mengonfirmasi nama file |
| `Control + X` | Keluar dari Nano |
| `Control + W` | Mencari teks |

---

# 2. GIT FUNDAMENTALS

Git adalah version control system untuk melacak perubahan source code.

## Konfigurasi Git

### Melihat versi Git

```bash
git --version
```

### Mengatur nama developer

```bash
git config --global user.name "Nama Kamu"
```

### Mengatur email

```bash
git config --global user.email "email@example.com"
```

### Melihat konfigurasi

```bash
git config --list
```

---

## Membuat Repository

### Menginisialisasi Git

```bash
git init
```

Fungsi: membuat repository Git lokal di folder saat ini.

### Mengganti nama branch utama menjadi main

```bash
git branch -M main
```

Fungsi: mengatur nama branch utama menjadi `main`.

### Melihat status repository

```bash
git status
```

Fungsi: melihat file yang berubah, belum di-stage, atau sudah di-stage.

---

## Git Workflow

### 1. Memeriksa perubahan

```bash
git status
```

### 2. Melihat detail perubahan

```bash
git diff
```

Fungsi: melihat perbedaan antara file yang diedit dengan versi terakhir yang di-commit.

### 3. Memasukkan file ke staging

```bash
git add nama-file
```

Contoh:

```bash
git add README.md
```

### Memasukkan semua perubahan

```bash
git add .
```

Fungsi: memasukkan perubahan di folder project ke staging.

### 4. Menyimpan perubahan

```bash
git commit -m "Pesan commit"
```

Contoh:

```bash
git commit -m "Add Docker configuration"
```

Fungsi: menyimpan snapshot perubahan ke riwayat repository lokal.

### 5. Melihat riwayat commit

```bash
git log
```

### Riwayat ringkas

```bash
git log --oneline
```

### Riwayat seluruh branch berbentuk grafik

```bash
git log --oneline --all --graph
```

---

## Membatalkan Perubahan

### Membatalkan perubahan file yang belum di-stage

```bash
git restore nama-file
```

Contoh:

```bash
git restore README.md
```

Fungsi: membuang perubahan pada file yang belum masuk staging.

**Perhatian:** perubahan yang dibatalkan tidak otomatis dapat dipulihkan.

### Mengeluarkan file dari staging

```bash
git restore --staged nama-file
```

Fungsi: mengeluarkan file dari staging tetapi tetap mempertahankan editan di file.

---

# 3. GIT BRANCH DAN MERGE

Branch digunakan untuk mengembangkan fitur tanpa langsung mengubah branch utama.

## Melihat branch

```bash
git branch
```

## Membuat branch

```bash
git branch nama-branch
```

## Berpindah branch

```bash
git switch nama-branch
```

## Membuat dan langsung berpindah branch

```bash
git switch -c nama-branch
```

Contoh:

```bash
git switch -c feature-profile
```

## Kembali ke main

```bash
git switch main
```

## Menggabungkan branch

```bash
git merge nama-branch
```

Contoh:

```bash
git switch main
git merge feature-profile
```

Fungsi: menggabungkan perubahan dari branch `feature-profile` ke branch yang sedang aktif, dalam contoh ini `main`.

## Menghapus branch lokal

```bash
git branch -d nama-branch
```

Fungsi: menghapus branch yang sudah selesai digabung.

---

# 4. GITHUB — REMOTE REPOSITORY

GitHub adalah platform penyimpanan repository Git secara online.

## Melihat koneksi remote

```bash
git remote -v
```

## Menghubungkan Git lokal dengan GitHub

```bash
git remote add origin URL-REPOSITORY
```

Contoh:

```bash
git remote add origin https://github.com/USERNAME/devops-learning.git
```

Fungsi: menghubungkan repository lokal dengan repository GitHub.

`origin` adalah nama alias untuk remote repository.

## Upload pertama ke GitHub

```bash
git push -u origin main
```

Fungsi:
- Mengirim commit lokal ke GitHub.
- Mengatur branch lokal agar tracking ke branch remote.

Setelah push pertama berhasil, biasanya cukup:

```bash
git push
```

## Mengambil perubahan dari GitHub

```bash
git pull
```

Fungsi: mengambil perubahan dari remote dan mengintegrasikannya ke branch lokal yang aktif.

## Mengambil perubahan tanpa merge

```bash
git fetch
```

Fungsi: mengambil informasi dan commit terbaru dari remote tanpa langsung menggabungkannya ke branch aktif.

## Clone repository

```bash
git clone URL-REPOSITORY
```

Contoh:

```bash
git clone https://github.com/USERNAME/devops-learning.git
```

Fungsi: menyalin repository GitHub ke komputer lokal, termasuk riwayat Git.

---

# 5. GITIGNORE

`.gitignore` menentukan file atau folder yang tidak perlu dilacak Git.

## Membuat file

```bash
touch .gitignore
```

## Membuka file

```bash
nano .gitignore
```

## Contoh isi .gitignore

```gitignore
# macOS
.DS_Store

# Environment
.env
.env.*
!.env.example

# Python
__pycache__/
*.pyc
.venv/
venv/

# Node.js
node_modules/

# Logs
*.log

# IDE
.vscode/
.idea/
```

## Memeriksa perubahan

```bash
git status
```

## Menyimpan .gitignore ke Git

```bash
git add .gitignore
git commit -m "Add gitignore configuration"
git push
```

**Penting:** `.gitignore` tidak otomatis berhenti melacak file yang sebelumnya sudah di-commit.

Jangan mengupload:
- Password
- API Key
- Access Token
- Private Key
- File `.env` yang berisi rahasia

---

# 6. WORKFLOW GIT SEHARI-HARI

Urutan dasar saat coding:

```bash
git status
git diff
git add .
git commit -m "Update project"
git push
```

Penjelasan:

1. `git status` — cek kondisi repository.
2. `git diff` — periksa perubahan.
3. `git add .` — masukkan perubahan ke staging.
4. `git commit` — simpan snapshot.
5. `git push` — upload ke GitHub.

Jika bekerja dengan repository yang dikerjakan bersama:

```bash
git pull
```

Sebaiknya ambil perubahan terbaru sebelum memulai pekerjaan, terutama jika orang lain juga mengubah branch yang sama.

---

# 7. DOCKER FUNDAMENTALS

Docker digunakan untuk mengemas dan menjalankan aplikasi dalam container.

## Memeriksa Docker

### Versi Docker

```bash
docker --version
```

### Informasi Docker Engine

```bash
docker info
```

### Container yang sedang berjalan

```bash
docker ps
```

### Semua container, termasuk yang berhenti

```bash
docker ps -a
```

### Melihat image

```bash
docker images
```

---

# 8. DOCKER IMAGE

Image adalah template/paket aplikasi yang digunakan untuk membuat container.

## Download image

```bash
docker pull nginx
```

Fungsi: mengunduh image Nginx dari Docker registry.

## Download image spesifik

```bash
docker pull nginx:latest
```

## Melihat image

```bash
docker images
```

## Menghapus image

```bash
docker rmi nama-image
```

Contoh:

```bash
docker rmi nginx
```

Image tidak dapat dihapus jika masih digunakan container, kecuali container terkait dihapus terlebih dahulu.

---

# 9. DOCKER CONTAINER

Container adalah instance yang dibuat dari Docker Image.

## Membuat dan menjalankan container

```bash
docker run image
```

## Menjalankan container di background

```bash
docker run -d image
```

`-d` = detached mode, container berjalan di background.

## Memberikan nama container

```bash
docker run -d --name nama-container image
```

Contoh:

```bash
docker run -d --name nginx-practice nginx
```

## Mapping port

```bash
docker run -d -p HOST-PORT:CONTAINER-PORT image
```

Contoh:

```bash
docker run -d --name nginx-practice -p 8080:80 nginx
```

Artinya:
- Port 8080 pada Mac.
- Port 80 pada container Nginx.

Website diakses melalui:

```text
http://localhost:8080
```

## Menghentikan container

```bash
docker stop nama-container
```

## Menjalankan kembali container yang berhenti

```bash
docker start nama-container
```

## Restart container

```bash
docker restart nama-container
```

## Menghapus container

```bash
docker rm nama-container
```

## Menghapus container secara paksa

```bash
docker rm -f nama-container
```

`-f` = force, menghentikan jika container masih berjalan dan menghapusnya.

## Melihat log

```bash
docker logs nama-container
```

## Mengikuti log secara realtime

```bash
docker logs -f nama-container
```

Tekan `Control + C` untuk keluar dari tampilan log.

## Masuk ke container

```bash
docker exec -it nama-container sh
```

Jika container memiliki Bash:

```bash
docker exec -it nama-container bash
```

## Menjalankan perintah di dalam container

```bash
docker exec nama-container command
```

Contoh:

```bash
docker exec nginx-practice ls
```

---

# 10. DOCKERFILE

Dockerfile adalah file instruksi untuk membangun Docker Image sendiri.

## Instruksi Dockerfile

### FROM

```dockerfile
FROM python:3.12-slim
```

Menentukan base image.

### WORKDIR

```dockerfile
WORKDIR /app
```

Menentukan direktori kerja di dalam image/container.

### COPY

```dockerfile
COPY main.py .
```

Menyalin file dari build context ke image.

### RUN

```dockerfile
RUN pip install requests
```

Menjalankan perintah ketika image sedang dibangun.

### EXPOSE

```dockerfile
EXPOSE 8000
```

Mendokumentasikan port aplikasi yang digunakan.

### CMD

```dockerfile
CMD ["python", "main.py"]
```

Menentukan perintah default ketika container dijalankan.

### ENV

```dockerfile
ENV APP_ENV=production
```

Mengatur environment variable pada image/container.

---

# 11. DOCKER BUILD

Membangun image dari Dockerfile.

## Build image

```bash
docker build -t nama-image .
```

Contoh:

```bash
docker build -t my-python-app .
```

Penjelasan:
- `docker build` = membangun image.
- `-t` = memberi nama/tag image.
- `my-python-app` = nama image.
- `.` = build context berupa folder saat ini.

## Build dengan tag versi

```bash
docker build -t my-python-app:1.0 .
```

## Memeriksa image

```bash
docker images
```

---

# 12. DOCKER VOLUME

Volume digunakan untuk menyimpan data agar tetap ada meskipun container dihapus.

## Membuat volume

```bash
docker volume create nama-volume
```

Contoh:

```bash
docker volume create belajar-data
```

## Melihat daftar volume

```bash
docker volume ls
```

## Melihat detail volume

```bash
docker volume inspect nama-volume
```

## Menggunakan volume

```bash
docker run -v nama-volume:/path-container image
```

Contoh:

```bash
docker run --rm -v belajar-data:/data alpine sh -c "echo 'Data Docker saya tetap tersimpan' > /data/catatan.txt"
```

## Membaca data dari volume

```bash
docker run --rm -v belajar-data:/data alpine cat /data/catatan.txt
```

## Menghapus volume

```bash
docker volume rm nama-volume
```

## Menghapus volume yang tidak digunakan

```bash
docker volume prune
```

**Peringatan:** penghapusan volume dapat menyebabkan data hilang permanen.

---

# 13. BIND MOUNT

Bind mount menghubungkan folder komputer host ke direktori container.

## Sintaks

```bash
docker run -v HOST-PATH:CONTAINER-PATH image
```

Contoh:

```bash
docker run -d --name web-practice -p 8080:80 -v "$PWD:/usr/share/nginx/html:ro" nginx
```

Penjelasan:
- `$PWD` = direktori saat ini pada Mac.
- `/usr/share/nginx/html` = folder website di container.
- `:ro` = read-only.

Bind mount sering digunakan saat development agar perubahan file di komputer langsung terlihat di container.

---

# 14. DOCKER NETWORK

Docker Network memungkinkan container berkomunikasi satu sama lain.

## Melihat network

```bash
docker network ls
```

## Membuat network

```bash
docker network create app-network
```

## Memeriksa network

```bash
docker network inspect app-network
```

## Menghubungkan container ke network

```bash
docker network connect app-network nama-container
```

## Memutuskan container dari network

```bash
docker network disconnect app-network nama-container
```

## Menghapus network

```bash
docker network rm app-network
```

## Menjalankan container di network

```bash
docker run -dit --name net-test-1 --network app-network busybox sh
```

## Tes komunikasi antarcontainer

```bash
docker exec net-test-1 ping -c 4 net-test-2
```

Container dalam user-defined network dapat menggunakan nama container atau nama service untuk berkomunikasi, selama DNS/network tersebut mendukung dan container terhubung.

---

# 15. DOCKER COMPOSE

Docker Compose digunakan untuk mengelola beberapa container melalui file konfigurasi YAML.

File utama:

```text
compose.yaml
```

## Contoh compose.yaml

```yaml
services:

  web:
    image: nginx:latest
    container_name: compose-web
    ports:
      - "8082:80"
    restart: unless-stopped

  redis:
    image: redis:7
    container_name: compose-redis
    restart: unless-stopped
```

## Menjalankan seluruh service

```bash
docker compose up
```

## Menjalankan di background

```bash
docker compose up -d
```

## Menghentikan dan menghapus container serta network project

```bash
docker compose down
```

## Menghentikan service

```bash
docker compose stop
```

## Menjalankan service kembali

```bash
docker compose start
```

## Melihat status service

```bash
docker compose ps
```

## Melihat log

```bash
docker compose logs
```

## Melihat log realtime

```bash
docker compose logs -f
```

## Melihat log service tertentu

```bash
docker compose logs web
```

## Restart seluruh service

```bash
docker compose restart
```

## Restart service tertentu

```bash
docker compose restart web
```

## Download image yang dibutuhkan

```bash
docker compose pull
```

## Build image dari Dockerfile

```bash
docker compose build
```

## Build ulang dan menjalankan service

```bash
docker compose up -d --build
```

## Menjalankan perintah di service

```bash
docker compose exec nama-service command
```

Contoh:

```bash
docker compose exec redis redis-cli ping
```

Output:

```text
PONG
```

## Menghapus project dan volume

```bash
docker compose down -v
```

**Peringatan:** `-v` dapat menghapus volume dan data persisten milik project.

---

# 16. DOCKER COMMAND CHEAT SHEET

| Kebutuhan | Command |
|---|---|
| Cek versi | `docker --version` |
| Cek engine | `docker info` |
| Container aktif | `docker ps` |
| Semua container | `docker ps -a` |
| Daftar image | `docker images` |
| Download image | `docker pull nginx` |
| Build image | `docker build -t app .` |
| Run container | `docker run image` |
| Run background | `docker run -d image` |
| Mapping port | `docker run -p 8080:80 image` |
| Stop | `docker stop container` |
| Start | `docker start container` |
| Restart | `docker restart container` |
| Delete container | `docker rm container` |
| Delete paksa | `docker rm -f container` |
| Logs | `docker logs container` |
| Realtime logs | `docker logs -f container` |
| Masuk container | `docker exec -it container sh` |
| Create volume | `docker volume create data` |
| List volume | `docker volume ls` |
| Create network | `docker network create app-network` |
| List network | `docker network ls` |
| Inspect network | `docker network inspect app-network` |

---

# 17. DOCKER COMPOSE CHEAT SHEET

| Kebutuhan | Command |
|---|---|
| Run project | `docker compose up` |
| Run background | `docker compose up -d` |
| Build + run | `docker compose up -d --build` |
| Stop project | `docker compose stop` |
| Start project | `docker compose start` |
| Remove project | `docker compose down` |
| Remove + volume | `docker compose down -v` |
| Status | `docker compose ps` |
| Logs | `docker compose logs` |
| Realtime logs | `docker compose logs -f` |
| Restart | `docker compose restart` |
| Build | `docker compose build` |
| Pull image | `docker compose pull` |
| Execute command | `docker compose exec service command` |

---

# 18. WORKFLOW DEVELOPER

## Workflow Git

```bash
git status
git pull
# Coding
git diff
git add .
git commit -m "Update application"
git push
```

## Workflow Docker

```bash
docker pull nginx
docker images
docker run -d --name nginx-practice -p 8080:80 nginx
docker ps
docker logs nginx-practice
docker stop nginx-practice
docker start nginx-practice
docker rm nginx-practice
```

## Workflow Dockerfile

```bash
# Coding source code dan Dockerfile

docker build -t my-app .
docker images
docker run -d --name my-app-container -p 8000:8000 my-app
docker ps
docker logs my-app-container
```

## Workflow Docker Compose

```bash
# Membuat compose.yaml

docker compose up -d
docker compose ps
docker compose logs
docker compose stop
docker compose start
docker compose down
```

---

# 19. ISTILAH YANG WAJIB DIPAHAMI

| Istilah | Arti |
|---|---|
| Repository | Tempat penyimpanan source code dan riwayat Git |
| Commit | Snapshot perubahan yang tersimpan di Git |
| Branch | Cabang pengembangan |
| Merge | Menggabungkan perubahan branch |
| Remote | Repository Git di lokasi lain |
| GitHub | Platform repository online |
| Push | Mengirim commit ke remote |
| Pull | Mengambil dan menggabungkan perubahan remote |
| Clone | Menyalin repository |
| Image | Template/paket aplikasi Docker |
| Container | Instance image yang dijalankan |
| Dockerfile | Instruksi membangun image |
| Volume | Penyimpanan data persisten Docker |
| Bind Mount | Menghubungkan folder host ke container |
| Network | Jaringan komunikasi antarcontainer |
| Docker Compose | Mengelola banyak service/container |
| Port Mapping | Menghubungkan port host ke port container |
| Build Context | File/folder yang tersedia bagi proses build |
| Environment Variable | Variabel konfigurasi aplikasi |
| Registry | Tempat menyimpan dan mendistribusikan image |

---

# 20. URUTAN PEMBELAJARAN SELANJUTNYA

1. Git & GitHub Fundamentals — selesai.
2. Docker Image & Container — selesai.
3. Dockerfile — selesai.
4. Docker Volume — selesai.
5. Docker Network — selesai.
6. Docker Compose — sedang dipelajari.
7. Membuat FastAPI.
8. PostgreSQL.
9. Menggabungkan API + PostgreSQL dengan Docker Compose.
10. Environment variables dan keamanan.
11. GitHub Actions (CI/CD).
12. Linux Ubuntu Server.
13. SSH ke VPS.
14. Deployment aplikasi.
15. Domain dan DNS.
16. Nginx Reverse Proxy.
17. HTTPS / SSL.
18. Monitoring, logging, backup, dan maintenance.

---

## Prinsip penting

- Selalu cek `git status` sebelum commit.
- Commit harus memiliki pesan yang jelas.
- Jangan mengupload `.env`, password, token, atau API key.
- Jangan menghapus Docker Volume tanpa memastikan datanya tidak dibutuhkan.
- Gunakan `docker ps` untuk memeriksa container.
- Gunakan `docker logs` ketika aplikasi error.
- Gunakan Docker Compose untuk aplikasi multi-container.
- Gunakan GitHub untuk menyimpan dan mengelola source code.
- Jangan menjalankan perintah yang tidak dipahami pada server production.


# CHEAT SHEET DEVOPS
## Terminal, Git, GitHub, Docker & Docker Compose

Dokumentasi perintah fundamental yang dipelajari untuk mengelola project, version control, container, dan persiapan deployment.

---

# 1. TERMINAL / COMMAND LINE

Terminal digunakan untuk berinteraksi dengan sistem operasi melalui perintah.

## Navigasi folder

| Command | Fungsi |
|---|---|
| `pwd` | Menampilkan direktori aktif |
| `ls` | Melihat isi folder |
| `ls -la` | Melihat seluruh file termasuk hidden files |
| `cd nama-folder` | Masuk ke folder |
| `cd ..` | Naik satu folder |
| `cd ~` | Kembali ke Home |
| `cd /path/folder` | Masuk ke direktori tertentu |

## Mengelola file dan folder

| Command | Fungsi |
|---|---|
| `mkdir nama-folder` | Membuat folder |
| `mkdir -p folder/subfolder` | Membuat folder bertingkat |
| `touch nama-file` | Membuat file kosong |
| `cat nama-file` | Membaca isi file |
| `nano nama-file` | Mengedit file menggunakan Nano |
| `cp file tujuan` | Menyalin file |
| `mv file tujuan` | Memindahkan atau mengganti nama file |
| `rm nama-file` | Menghapus file |
| `rm -r nama-folder` | Menghapus folder dan isinya |

**Perhatian:** `rm` menghapus file. Periksa nama file sebelum menjalankan perintah.

## Shortcut Nano

| Shortcut | Fungsi |
|---|---|
| `Control + O` | Menyimpan file |
| `Enter` | Mengonfirmasi nama file |
| `Control + X` | Keluar dari Nano |
| `Control + W` | Mencari teks |

---

# 2. GIT FUNDAMENTALS

Git adalah version control system untuk melacak perubahan source code.

## Konfigurasi Git

### Melihat versi Git

```bash
git --version
```

### Mengatur nama developer

```bash
git config --global user.name "Nama Kamu"
```

### Mengatur email

```bash
git config --global user.email "email@example.com"
```

### Melihat konfigurasi

```bash
git config --list
```

---

## Membuat Repository

### Menginisialisasi Git

```bash
git init
```

Fungsi: membuat repository Git lokal di folder saat ini.

### Mengganti nama branch utama menjadi main

```bash
git branch -M main
```

Fungsi: mengatur nama branch utama menjadi `main`.

### Melihat status repository

```bash
git status
```

Fungsi: melihat file yang berubah, belum di-stage, atau sudah di-stage.

---

## Git Workflow

### 1. Memeriksa perubahan

```bash
git status
```

### 2. Melihat detail perubahan

```bash
git diff
```

Fungsi: melihat perbedaan antara file yang diedit dengan versi terakhir yang di-commit.

### 3. Memasukkan file ke staging

```bash
git add nama-file
```

Contoh:

```bash
git add README.md
```

### Memasukkan semua perubahan

```bash
git add .
```

Fungsi: memasukkan perubahan di folder project ke staging.

### 4. Menyimpan perubahan

```bash
git commit -m "Pesan commit"
```

Contoh:

```bash
git commit -m "Add Docker configuration"
```

Fungsi: menyimpan snapshot perubahan ke riwayat repository lokal.

### 5. Melihat riwayat commit

```bash
git log
```

### Riwayat ringkas

```bash
git log --oneline
```

### Riwayat seluruh branch berbentuk grafik

```bash
git log --oneline --all --graph
```

---

## Membatalkan Perubahan

### Membatalkan perubahan file yang belum di-stage

```bash
git restore nama-file
```

Contoh:

```bash
git restore README.md
```

Fungsi: membuang perubahan pada file yang belum masuk staging.

**Perhatian:** perubahan yang dibatalkan tidak otomatis dapat dipulihkan.

### Mengeluarkan file dari staging

```bash
git restore --staged nama-file
```

Fungsi: mengeluarkan file dari staging tetapi tetap mempertahankan editan di file.

---

# 3. GIT BRANCH DAN MERGE

Branch digunakan untuk mengembangkan fitur tanpa langsung mengubah branch utama.

## Melihat branch

```bash
git branch
```

## Membuat branch

```bash
git branch nama-branch
```

## Berpindah branch

```bash
git switch nama-branch
```

## Membuat dan langsung berpindah branch

```bash
git switch -c nama-branch
```

Contoh:

```bash
git switch -c feature-profile
```

## Kembali ke main

```bash
git switch main
```

## Menggabungkan branch

```bash
git merge nama-branch
```

Contoh:

```bash
git switch main
git merge feature-profile
```

Fungsi: menggabungkan perubahan dari branch `feature-profile` ke branch yang sedang aktif, dalam contoh ini `main`.

## Menghapus branch lokal

```bash
git branch -d nama-branch
```

Fungsi: menghapus branch yang sudah selesai digabung.

---

# 4. GITHUB — REMOTE REPOSITORY

GitHub adalah platform penyimpanan repository Git secara online.

## Melihat koneksi remote

```bash
git remote -v
```

## Menghubungkan Git lokal dengan GitHub

```bash
git remote add origin URL-REPOSITORY
```

Contoh:

```bash
git remote add origin https://github.com/USERNAME/devops-learning.git
```

Fungsi: menghubungkan repository lokal dengan repository GitHub.

`origin` adalah nama alias untuk remote repository.

## Upload pertama ke GitHub

```bash
git push -u origin main
```

Fungsi:
- Mengirim commit lokal ke GitHub.
- Mengatur branch lokal agar tracking ke branch remote.

Setelah push pertama berhasil, biasanya cukup:

```bash
git push
```

## Mengambil perubahan dari GitHub

```bash
git pull
```

Fungsi: mengambil perubahan dari remote dan mengintegrasikannya ke branch lokal yang aktif.

## Mengambil perubahan tanpa merge

```bash
git fetch
```

Fungsi: mengambil informasi dan commit terbaru dari remote tanpa langsung menggabungkannya ke branch aktif.

## Clone repository

```bash
git clone URL-REPOSITORY
```

Contoh:

```bash
git clone https://github.com/USERNAME/devops-learning.git
```

Fungsi: menyalin repository GitHub ke komputer lokal, termasuk riwayat Git.

---

# 5. GITIGNORE

`.gitignore` menentukan file atau folder yang tidak perlu dilacak Git.

## Membuat file

```bash
touch .gitignore
```

## Membuka file

```bash
nano .gitignore
```

## Contoh isi .gitignore

```gitignore
# macOS
.DS_Store

# Environment
.env
.env.*
!.env.example

# Python
__pycache__/
*.pyc
.venv/
venv/

# Node.js
node_modules/

# Logs
*.log

# IDE
.vscode/
.idea/
```

## Memeriksa perubahan

```bash
git status
```

## Menyimpan .gitignore ke Git

```bash
git add .gitignore
git commit -m "Add gitignore configuration"
git push
```

**Penting:** `.gitignore` tidak otomatis berhenti melacak file yang sebelumnya sudah di-commit.

Jangan mengupload:
- Password
- API Key
- Access Token
- Private Key
- File `.env` yang berisi rahasia

---

# 6. WORKFLOW GIT SEHARI-HARI

Urutan dasar saat coding:

```bash
git status
git diff
git add .
git commit -m "Update project"
git push
```

Penjelasan:

1. `git status` — cek kondisi repository.
2. `git diff` — periksa perubahan.
3. `git add .` — masukkan perubahan ke staging.
4. `git commit` — simpan snapshot.
5. `git push` — upload ke GitHub.

Jika bekerja dengan repository yang dikerjakan bersama:

```bash
git pull
```

Sebaiknya ambil perubahan terbaru sebelum memulai pekerjaan, terutama jika orang lain juga mengubah branch yang sama.

---

# 7. DOCKER FUNDAMENTALS

Docker digunakan untuk mengemas dan menjalankan aplikasi dalam container.

## Memeriksa Docker

### Versi Docker

```bash
docker --version
```

### Informasi Docker Engine

```bash
docker info
```

### Container yang sedang berjalan

```bash
docker ps
```

### Semua container, termasuk yang berhenti

```bash
docker ps -a
```

### Melihat image

```bash
docker images
```

---

# 8. DOCKER IMAGE

Image adalah template/paket aplikasi yang digunakan untuk membuat container.

## Download image

```bash
docker pull nginx
```

Fungsi: mengunduh image Nginx dari Docker registry.

## Download image spesifik

```bash
docker pull nginx:latest
```

## Melihat image

```bash
docker images
```

## Menghapus image

```bash
docker rmi nama-image
```

Contoh:

```bash
docker rmi nginx
```

Image tidak dapat dihapus jika masih digunakan container, kecuali container terkait dihapus terlebih dahulu.

---

# 9. DOCKER CONTAINER

Container adalah instance yang dibuat dari Docker Image.

## Membuat dan menjalankan container

```bash
docker run image
```

## Menjalankan container di background

```bash
docker run -d image
```

`-d` = detached mode, container berjalan di background.

## Memberikan nama container

```bash
docker run -d --name nama-container image
```

Contoh:

```bash
docker run -d --name nginx-practice nginx
```

## Mapping port

```bash
docker run -d -p HOST-PORT:CONTAINER-PORT image
```

Contoh:

```bash
docker run -d --name nginx-practice -p 8080:80 nginx
```

Artinya:
- Port 8080 pada Mac.
- Port 80 pada container Nginx.

Website diakses melalui:

```text
http://localhost:8080
```

## Menghentikan container

```bash
docker stop nama-container
```

## Menjalankan kembali container yang berhenti

```bash
docker start nama-container
```

## Restart container

```bash
docker restart nama-container
```

## Menghapus container

```bash
docker rm nama-container
```

## Menghapus container secara paksa

```bash
docker rm -f nama-container
```

`-f` = force, menghentikan jika container masih berjalan dan menghapusnya.

## Melihat log

```bash
docker logs nama-container
```

## Mengikuti log secara realtime

```bash
docker logs -f nama-container
```

Tekan `Control + C` untuk keluar dari tampilan log.

## Masuk ke container

```bash
docker exec -it nama-container sh
```

Jika container memiliki Bash:

```bash
docker exec -it nama-container bash
```

## Menjalankan perintah di dalam container

```bash
docker exec nama-container command
```

Contoh:

```bash
docker exec nginx-practice ls
```

---

# 10. DOCKERFILE

Dockerfile adalah file instruksi untuk membangun Docker Image sendiri.

## Instruksi Dockerfile

### FROM

```dockerfile
FROM python:3.12-slim
```

Menentukan base image.

### WORKDIR

```dockerfile
WORKDIR /app
```

Menentukan direktori kerja di dalam image/container.

### COPY

```dockerfile
COPY main.py .
```

Menyalin file dari build context ke image.

### RUN

```dockerfile
RUN pip install requests
```

Menjalankan perintah ketika image sedang dibangun.

### EXPOSE

```dockerfile
EXPOSE 8000
```

Mendokumentasikan port aplikasi yang digunakan.

### CMD

```dockerfile
CMD ["python", "main.py"]
```

Menentukan perintah default ketika container dijalankan.

### ENV

```dockerfile
ENV APP_ENV=production
```

Mengatur environment variable pada image/container.

---

# 11. DOCKER BUILD

Membangun image dari Dockerfile.

## Build image

```bash
docker build -t nama-image .
```

Contoh:

```bash
docker build -t my-python-app .
```

Penjelasan:
- `docker build` = membangun image.
- `-t` = memberi nama/tag image.
- `my-python-app` = nama image.
- `.` = build context berupa folder saat ini.

## Build dengan tag versi

```bash
docker build -t my-python-app:1.0 .
```

## Memeriksa image

```bash
docker images
```

---

# 12. DOCKER VOLUME

Volume digunakan untuk menyimpan data agar tetap ada meskipun container dihapus.

## Membuat volume

```bash
docker volume create nama-volume
```

Contoh:

```bash
docker volume create belajar-data
```

## Melihat daftar volume

```bash
docker volume ls
```

## Melihat detail volume

```bash
docker volume inspect nama-volume
```

## Menggunakan volume

```bash
docker run -v nama-volume:/path-container image
```

Contoh:

```bash
docker run --rm -v belajar-data:/data alpine sh -c "echo 'Data Docker saya tetap tersimpan' > /data/catatan.txt"
```

## Membaca data dari volume

```bash
docker run --rm -v belajar-data:/data alpine cat /data/catatan.txt
```

## Menghapus volume

```bash
docker volume rm nama-volume
```

## Menghapus volume yang tidak digunakan

```bash
docker volume prune
```

**Peringatan:** penghapusan volume dapat menyebabkan data hilang permanen.

---

# 13. BIND MOUNT

Bind mount menghubungkan folder komputer host ke direktori container.

## Sintaks

```bash
docker run -v HOST-PATH:CONTAINER-PATH image
```

Contoh:

```bash
docker run -d --name web-practice -p 8080:80 -v "$PWD:/usr/share/nginx/html:ro" nginx
```

Penjelasan:
- `$PWD` = direktori saat ini pada Mac.
- `/usr/share/nginx/html` = folder website di container.
- `:ro` = read-only.

Bind mount sering digunakan saat development agar perubahan file di komputer langsung terlihat di container.

---

# 14. DOCKER NETWORK

Docker Network memungkinkan container berkomunikasi satu sama lain.

## Melihat network

```bash
docker network ls
```

## Membuat network

```bash
docker network create app-network
```

## Memeriksa network

```bash
docker network inspect app-network
```

## Menghubungkan container ke network

```bash
docker network connect app-network nama-container
```

## Memutuskan container dari network

```bash
docker network disconnect app-network nama-container
```

## Menghapus network

```bash
docker network rm app-network
```

## Menjalankan container di network

```bash
docker run -dit --name net-test-1 --network app-network busybox sh
```

## Tes komunikasi antarcontainer

```bash
docker exec net-test-1 ping -c 4 net-test-2
```

Container dalam user-defined network dapat menggunakan nama container atau nama service untuk berkomunikasi, selama DNS/network tersebut mendukung dan container terhubung.

---

# 15. DOCKER COMPOSE

Docker Compose digunakan untuk mengelola beberapa container melalui file konfigurasi YAML.

File utama:

```text
compose.yaml
```

## Contoh compose.yaml

```yaml
services:

  web:
    image: nginx:latest
    container_name: compose-web
    ports:
      - "8082:80"
    restart: unless-stopped

  redis:
    image: redis:7
    container_name: compose-redis
    restart: unless-stopped
```

## Menjalankan seluruh service

```bash
docker compose up
```

## Menjalankan di background

```bash
docker compose up -d
```

## Menghentikan dan menghapus container serta network project

```bash
docker compose down
```

## Menghentikan service

```bash
docker compose stop
```

## Menjalankan service kembali

```bash
docker compose start
```

## Melihat status service

```bash
docker compose ps
```

## Melihat log

```bash
docker compose logs
```

## Melihat log realtime

```bash
docker compose logs -f
```

## Melihat log service tertentu

```bash
docker compose logs web
```

## Restart seluruh service

```bash
docker compose restart
```

## Restart service tertentu

```bash
docker compose restart web
```

## Download image yang dibutuhkan

```bash
docker compose pull
```

## Build image dari Dockerfile

```bash
docker compose build
```

## Build ulang dan menjalankan service

```bash
docker compose up -d --build
```

## Menjalankan perintah di service

```bash
docker compose exec nama-service command
```

Contoh:

```bash
docker compose exec redis redis-cli ping
```

Output:

```text
PONG
```

## Menghapus project dan volume

```bash
docker compose down -v
```

**Peringatan:** `-v` dapat menghapus volume dan data persisten milik project.

---

# 16. DOCKER COMMAND CHEAT SHEET

| Kebutuhan | Command |
|---|---|
| Cek versi | `docker --version` |
| Cek engine | `docker info` |
| Container aktif | `docker ps` |
| Semua container | `docker ps -a` |
| Daftar image | `docker images` |
| Download image | `docker pull nginx` |
| Build image | `docker build -t app .` |
| Run container | `docker run image` |
| Run background | `docker run -d image` |
| Mapping port | `docker run -p 8080:80 image` |
| Stop | `docker stop container` |
| Start | `docker start container` |
| Restart | `docker restart container` |
| Delete container | `docker rm container` |
| Delete paksa | `docker rm -f container` |
| Logs | `docker logs container` |
| Realtime logs | `docker logs -f container` |
| Masuk container | `docker exec -it container sh` |
| Create volume | `docker volume create data` |
| List volume | `docker volume ls` |
| Create network | `docker network create app-network` |
| List network | `docker network ls` |
| Inspect network | `docker network inspect app-network` |

---

# 17. DOCKER COMPOSE CHEAT SHEET

| Kebutuhan | Command |
|---|---|
| Run project | `docker compose up` |
| Run background | `docker compose up -d` |
| Build + run | `docker compose up -d --build` |
| Stop project | `docker compose stop` |
| Start project | `docker compose start` |
| Remove project | `docker compose down` |
| Remove + volume | `docker compose down -v` |
| Status | `docker compose ps` |
| Logs | `docker compose logs` |
| Realtime logs | `docker compose logs -f` |
| Restart | `docker compose restart` |
| Build | `docker compose build` |
| Pull image | `docker compose pull` |
| Execute command | `docker compose exec service command` |

---

# 18. WORKFLOW DEVELOPER

## Workflow Git

```bash
git status
git pull
# Coding
git diff
git add .
git commit -m "Update application"
git push
```

## Workflow Docker

```bash
docker pull nginx
docker images
docker run -d --name nginx-practice -p 8080:80 nginx
docker ps
docker logs nginx-practice
docker stop nginx-practice
docker start nginx-practice
docker rm nginx-practice
```

## Workflow Dockerfile

```bash
# Coding source code dan Dockerfile

docker build -t my-app .
docker images
docker run -d --name my-app-container -p 8000:8000 my-app
docker ps
docker logs my-app-container
```

## Workflow Docker Compose

```bash
# Membuat compose.yaml

docker compose up -d
docker compose ps
docker compose logs
docker compose stop
docker compose start
docker compose down
```

---

# 19. ISTILAH YANG WAJIB DIPAHAMI

| Istilah | Arti |
|---|---|
| Repository | Tempat penyimpanan source code dan riwayat Git |
| Commit | Snapshot perubahan yang tersimpan di Git |
| Branch | Cabang pengembangan |
| Merge | Menggabungkan perubahan branch |
| Remote | Repository Git di lokasi lain |
| GitHub | Platform repository online |
| Push | Mengirim commit ke remote |
| Pull | Mengambil dan menggabungkan perubahan remote |
| Clone | Menyalin repository |
| Image | Template/paket aplikasi Docker |
| Container | Instance image yang dijalankan |
| Dockerfile | Instruksi membangun image |
| Volume | Penyimpanan data persisten Docker |
| Bind Mount | Menghubungkan folder host ke container |
| Network | Jaringan komunikasi antarcontainer |
| Docker Compose | Mengelola banyak service/container |
| Port Mapping | Menghubungkan port host ke port container |
| Build Context | File/folder yang tersedia bagi proses build |
| Environment Variable | Variabel konfigurasi aplikasi |
| Registry | Tempat menyimpan dan mendistribusikan image |

---

# 20. URUTAN PEMBELAJARAN SELANJUTNYA

1. Git & GitHub Fundamentals — selesai.
2. Docker Image & Container — selesai.
3. Dockerfile — selesai.
4. Docker Volume — selesai.
5. Docker Network — selesai.
6. Docker Compose — sedang dipelajari.
7. Membuat FastAPI.
8. PostgreSQL.
9. Menggabungkan API + PostgreSQL dengan Docker Compose.
10. Environment variables dan keamanan.
11. GitHub Actions (CI/CD).
12. Linux Ubuntu Server.
13. SSH ke VPS.
14. Deployment aplikasi.
15. Domain dan DNS.
16. Nginx Reverse Proxy.
17. HTTPS / SSL.
18. Monitoring, logging, backup, dan maintenance.

---

## Prinsip penting

- Selalu cek `git status` sebelum commit.
- Commit harus memiliki pesan yang jelas.
- Jangan mengupload `.env`, password, token, atau API key.
- Jangan menghapus Docker Volume tanpa memastikan datanya tidak dibutuhkan.
- Gunakan `docker ps` untuk memeriksa container.
- Gunakan `docker logs` ketika aplikasi error.
- Gunakan Docker Compose untuk aplikasi multi-container.
- Gunakan GitHub untuk menyimpan dan mengelola source code.
- Jangan menjalankan perintah yang tidak dipahami pada server production.

