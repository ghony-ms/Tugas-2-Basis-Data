1. Membuat database rumah sakit
```sql
CREATE DATABASE IF NOT EXISTS rumahsakit
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_general_ci;
```
```sql
USE rumahsakit;
```

2. Membuat tabel administrator, dokter, dan admin
```sql
CREATE TABLE administrator (
  id_admin     VARCHAR(10)  PRIMARY KEY,
  nama_admin   VARCHAR(100) NOT NULL,
  waktu_jaga   VARCHAR(50)
) ENGINE=InnoDB;
```
```sql
CREATE TABLE dokter (
  id_dokter     VARCHAR(10)  PRIMARY KEY,
  nama_dokter   VARCHAR(100) NOT NULL,
  alamat_dokter TEXT,
  no_hp         VARCHAR(20),
  spesialis     VARCHAR(50),
  tanggal_lahir DATE,
  waktu_kerja   VARCHAR(50)
) ENGINE=InnoDB;
```
```sql
CREATE TABLE pasien (
  id_pasien     VARCHAR(10)  PRIMARY KEY,
  nama_pasien   VARCHAR(100) NOT NULL,
  jenis_kelamin ENUM('L','P'),
  alamat_pasien TEXT
) ENGINE=InnoDB;
```

3. Membuat tabel penghubung: pasien_dokter
```sql
CREATE TABLE pasien_dokter (
  id            INT AUTO_INCREMENT PRIMARY KEY,
  id_dokter     VARCHAR(10),
  id_pasien     VARCHAR(10),
  waktu_periksa DATETIME,
  resep         TEXT,
  FOREIGN KEY (id_dokter) REFERENCES dokter(id_dokter)
    ON DELETE CASCADE ON UPDATE CASCADE,
  FOREIGN KEY (id_pasien) REFERENCES pasien(id_pasien)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;
```

4. Membuat tabel penghubung: daftar
```sql
CREATE TABLE daftar (
  id_daftar INT AUTO_INCREMENT PRIMARY KEY,
  id_pasien VARCHAR(10),
  id_admin  VARCHAR(10),
  FOREIGN KEY (id_pasien) REFERENCES pasien(id_pasien)
    ON DELETE CASCADE ON UPDATE CASCADE,
  FOREIGN KEY (id_admin)  REFERENCES administrator(id_admin)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;
```

5. Membuat tabel penghubung: dokter_admin
```sql
CREATE TABLE dokter_admin (
  id_data   INT AUTO_INCREMENT PRIMARY KEY,
  id_dokter VARCHAR(10),
  id_admin  VARCHAR(10),
  FOREIGN KEY (id_dokter) REFERENCES dokter(id_dokter)
    ON DELETE CASCADE ON UPDATE CASCADE,
  FOREIGN KEY (id_admin)  REFERENCES administrator(id_admin)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE=InnoDB;
```
