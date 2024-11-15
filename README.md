# Tugas4_PenghitungHari
 Tugas 4 - Cahya Hayyuni 2210010118

# 1. Deskripsi Program
Aplikasi ini menghitung jumlah hari dalam bulan tertentu pada tahun tertentu yang dipilih oleh pengguna.

- Input: Pengguna memilih bulan dari JComboBox dan memasukkan tahun menggunakan JSpinner.
- Penggunaan JCalendar: Untuk mempermudah pengguna memilih bulan dan tahun.
- Output: Setelah tombol ditekan, aplikasi menampilkan jumlah hari dalam bulan yang dipilih.
  
# 2. Komponen GUI: 
JFrame, JPanel, JLabel, JComboBox, JSpinner, JButton, JCalendar
- JPanel: Untuk menampung komponen lain.
- JLabel: Berfungsi sebagai label untuk elemen input dan output.
- JComboBox: Untuk memilih bulan.
- JSpinner: Untuk memasukkan tahun.
- JCalendar: Untuk mempermudah pengguna memilih bulan dan tahun secara visual.
- JButton: Tombol untuk menghitung jumlah hari, menghitung selisih hari, hapus dan keluar

- Button Hitung

private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
    buttonHitung.addActionListener((ActionEvent e) -> {
        MenghitungHari();
    });
    }  

- Button Hitung Selisih Hari

private void calculateDifferenceButtonActionPerformed(java.awt.event.ActionEvent evt) {                                                          
    // Event listener untuk tombol "Hitung Selisih Hari"
        buttonSelisih.addActionListener((ActionEvent e) -> {
            SelisihHari();
        });
    
    }      

- Button Hapus

private void btnHapusActionPerformed(java.awt.event.ActionEvent evt) {                                         
    // Event listener untuk tombol "Hapus"
        buttonHapus.addActionListener((ActionEvent e) -> {
            Hapus();
        });
    
    }      

Metode Hapus() di panggil

// Metode untuk menghapus atau mereset pilihan
    private void Hapus() {
        // Reset bulan ke Januari
        comboBulan.setSelectedIndex(0);

        // Reset tahun ke tahun default (misalnya 2023)
        spinnerTahun.setValue(2023);

        // Reset JCalendar ke tanggal hari ini
        jCalendar.setCalendar(Calendar.getInstance());

        // Kosongkan hasil pada JLabel
        labelHasil.setText("Jumlah hari: ");
    }

- Button Keluar

   private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
    System.exit(0);       
    } 

# 3. Logika Program: 
Penggunaan API tanggal (LocalDate), Perhitungan hari dalam bulan, Perhitungan tahun kabisat

# 4. Events:
• ActionListener untuk tombol Hitung

 private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
    buttonHitung.addActionListener((ActionEvent e) -> {
        MenghitungHari();
    });
    }

Penjelasan Kode :
ActionListener pada buttonHitung Saat tombol ditekan, metode MenghitungHari() akan dipanggil.

 private void MenghitungHari() {
        //Mengambil nilai bulan dari JComboBox
        int month = comboBulan.getSelectedIndex() + 1; // ComboBox menggunakan indeks dari 0, jadi ditambah 1
        // Mengambil nilai tahun dari JSpinner
        int year = (int) spinnerTahun.getValue();

        // Juga mengatur tanggal JCalendar sesuai dengan bulan dan tahun yang dipilih
        Calendar selectedDate = jCalendar.getCalendar();
        selectedDate.set(Calendar.MONTH, month - 1); // Calendar.MONTH menggunakan indeks dari 0
        selectedDate.set(Calendar.YEAR, year);
        jCalendar.setCalendar(selectedDate); // Menampilkan bulan dan tahun yang dipilih di JCalendar

        // Membuat objek YearMonth berdasarkan bulan dan tahun yang dipilih
        YearMonth yearMonth = YearMonth.of(year, month);

        // Menghitung jumlah hari dalam bulan tersebut
        int daysInMonth = yearMonth.lengthOfMonth();
        
        // Mendapatkan hari pertama dan hari terakhir dalam bulan tersebut
        LocalDate firstDay = yearMonth.atDay(1);
        LocalDate lastDay = yearMonth.atEndOfMonth();

        // Menampilkan hasil jumlah hari, hari pertama, dan hari terakhir pada JLabel
        labelHasil.setText(String.format(
            "Jumlah hari: %d, Hari pertama: %s, Hari terakhir: %s", 
            daysInMonth, firstDay.getDayOfWeek(), lastDay.getDayOfWeek()
        ));
     
    }


Metode MenghitungHari():
- comboBulan.getSelectedIndex() mendapatkan indeks bulan yang dipilih (dengan Januari sebagai indeks 0), lalu menambahkan 1 agar sesuai dengan bulan kalender (Januari = 1).
- spinnerTahun.getValue() mengambil nilai tahun yang dipilih.
- Menghitung jumlah hari: YearMonth.of(year, month) membuat objek YearMonth untuk bulan dan tahun yang dipilih. Metode lengthOfMonth() kemudian digunakan untuk mendapatkan jumlah hari pada bulan tersebut.
- Hasil jumlah hari ditampilkan di labelHasil.
  
• ChangeListener pada JSpinner untuk input tahun

private void SpinnerTahunStateChanged(javax.swing.event.ChangeEvent evt) {                                          
    spinnerTahun.addChangeListener((ChangeEvent e) -> {
        BulanTahun();
    });
    }   

Listener untuk mengubah bulan dan tahun pada JCalendar saat ComboBox atau Spinner berubah

private void cmbBoxBulanItemStateChanged(java.awt.event.ItemEvent evt) {                                             
        // Listener untuk mengubah bulan dan tahun pada JCalendar saat ComboBox atau Spinner berubah
        comboBulan.addItemListener((ItemEvent e) -> {
            BulanTahun();
        });
    }    

Metode BulanTahun() akan di panggil

private void BulanTahun() {
        int month = comboBulan.getSelectedIndex(); // Indeks bulan ComboBox mulai dari 0
        int year = (int) spinnerTahun.getValue();

        // Mengatur JCalendar untuk bulan dan tahun yang dipilih
        Calendar selectedDate = Calendar.getInstance();
        selectedDate.set(Calendar.YEAR, year);
        selectedDate.set(Calendar.MONTH, month); // Calendar.MONTH juga mulai dari 0
        selectedDate.set(Calendar.DAY_OF_MONTH, 1);
        jCalendar.setCalendar(selectedDate); // Memperbarui tampilan JCalendar
    }

# 5. Variasi:
• Tampilkan informasi tambahan seperti hari pertama dan terakhir dalam bulan tersebut

 // Mendapatkan hari pertama dan hari terakhir dalam bulan tersebut
        LocalDate firstDay = yearMonth.atDay(1);
        LocalDate lastDay = yearMonth.atEndOfMonth();

• Integrasikan fitur untuk menghitung selisih hari antara dua tanggal

 private void calculateDifferenceButtonActionPerformed(java.awt.event.ActionEvent evt) {                                                          
    // Event listener untuk tombol "Hitung Selisih Hari"
        buttonSelisih.addActionListener((ActionEvent e) -> {
            SelisihHari();
        });
    
    }

Metode SelisihHari() akan di panggil

private void SelisihHari() {
        // Mendapatkan tanggal awal dan akhir dari JCalendar
        Calendar startCal = jCalendarAwal.getCalendar();
        Calendar endCal = jCalendarAkhir.getCalendar();

        // Konversi Calendar ke LocalDate
        LocalDate startDate = startCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
        LocalDate endDate = endCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();

        // Menghitung selisih hari menggunakan ChronoUnit.DAYS
        long daysBetween = ChronoUnit.DAYS.between(startDate, endDate);

        // Menampilkan hasil selisih hari pada JLabel
        labelHasilSelisih.setText("Selisih hari antara dua tanggal: " + daysBetween + " hari");
    }
    

# Hasil Gambar Project Ketika di Run
![](https://github.com/AyaComel/Tugas4_PenghitungHari/blob/main/Tugas4.png).

## Indikator Penilaian:

| No  | Komponen         |  Persentase  |
| :-: | --------------   |   :-----:    |
|  1  | Komponen GUI     |    10    |
|  2  | Logika Program   |    20    |
|  3  | Event            |    20    |
|  4  | Kesesuaian UI    |    20    |
|  5  | Memenuhi Variasi |    40    |
|     | TOTAL        | 100 |

## Pembuat

Nama  : Cahya Hayyuni
NPM   : 2210010118
