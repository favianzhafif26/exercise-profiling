# Refleksi Module 5

### 1. What is the difference between the approach of performance testing with JMeter and profiling with IntelliJ Profiler in the context of optimizing application performance?
Perbedaan utama antara pengujian performa menggunakan JMeter dan IntelliJ Profiler terletak pada fungsinya. JMeter adalah aplikasi yang berfokus pada pengujian beban, memungkinkan pengguna untuk mengukur kinerja aplikasi di berbagai tingkat penggunaan. Sementara itu, IntelliJ Profiler adalah alat analisis kinerja kode yang membantu mendeteksi penggunaan CPU, konsumsi memori, dan aktivitas thread, sehingga lebih berorientasi pada optimasi kode dan pemecahan masalah performa aplikasi.

### 2. How does the profiling process help you in identifying and understanding the weak points in your application?
Profiling membantu mengidentifikasi metode yang berjalan lambat dan membebani program. Dengan profiler, kita dapat mengukur waktu eksekusi setiap metode atau fungsi dalam aplikasi, serta menentukan bagian kode yang paling lambat sehingga dapat dioptimalkan. Selain itu, profiler juga berperan dalam mendeteksi penggunaan memori dengan melacak alokasi dan konsumsi memori dalam aplikasi, membantu mencegah terjadinya kebocoran memori dan meningkatkan efisiensi program.

### 3. Do you think IntelliJ Profiler is effective in assisting you to analyze and identify bottlenecks in your application code?
Ya, IntelliJ Profiler sangat efektif dalam mengidentifikasi bottleneck dalam aplikasi. Dengan kemampuannya untuk mendeteksi metode dengan waktu eksekusi terlama, menemukan kebocoran memori, menganalisis performa thread, dan mengoptimalkan penggunaan CPU, profiler ini membantu meningkatkan efisiensi dan responsivitas aplikasi secara keseluruhan.

### 4. What are the main challenges you face when conducting performance testing and profiling, and how do you overcome these challenges?
Saya pertama kali melakukan performance testing dan profiling di IntelliJ, wajar jika merasa bingung dengan berbagai informasi teknis seperti stack trace, alokasi memori, serta grafik CPU dan memori. Untuk mengatasinya, saya bisa terus berlatih dengan profiler di IntelliJ dan memanfaatkan fitur flame graph, yang dirancang untuk membantu pengguna dengan lebih mudah mengidentifikasi masalah dalam kode. Seiring waktu, pemahaman saya terhadap data yang disajikan profiler akan semakin meningkat.

### 5. What are the main benefits you gain from using IntelliJ Profiler for profiling your application code?
Dengan IntelliJ Profiler, saya dapat dengan cepat mengidentifikasi bottleneck dan inefisiensi dalam kode berdasarkan waktu eksekusi setiap metode atau fungsi. Selain itu, saya juga bisa memantau alokasi memori secara real-time serta menganalisis aktivitas thread. Profiling di IntelliJ terasa intuitif dan mudah digunakan karena terintegrasi langsung dengan IntelliJ IDEA, sehingga proses analisis performa menjadi lebih efisien.

### 6. How do you handle situations where the results from profiling with IntelliJ Profiler are not entirely consistent with findings from performance testing using JMeter?

### 7. What strategies do you implement in optimizing application code after analyzing results from performance testing and profiling? How do you ensure the changes you make do not affect the application's functionality?
 1. Mengurangi N+1 Query Problem  
Diimplementasi pada:  
`StudentCourseRepository.findByStudentId(Long studentId)`  
`StudentService.getAllStudentsWithCourses()`  
Solusi:  
- Menggunakan `@EntityGraph` atau `JOIN FETCH` agar data mahasiswa dan mata kuliah diambil dalam satu query.  
- Mengurangi jumlah query yang dieksekusi saat mengambil daftar kursus untuk setiap mahasiswa.  

2. Memperbaiki Query JPQL  
Diimplementasi pada:  
`StudentRepository.findStudentWithHighestGpa()`  

Solusi:  
- Menghapus `LIMIT` yang tidak didukung dalam JPQL dan menggantinya dengan sorting + stream API (`findTopByOrderByGpaDesc().stream().findFirst()`).  
- Mencegah error saat menggunakan database yang tidak mendukung `LIMIT` dalam subquery JPQL.  

3. Optimasi String Processing 
Diimplementasi pada:  
`StudentService.joinStudentNames()`  

Solusi:  
- Mengganti concatenation dalam loop (`+=`) dengan `String.join()`, yang lebih efisien dalam mengelola memori dan performa.  

4. Optimasi Database
Diimplementasi pada:
Database Layer (tanpa perubahan kode, tetapi dengan konfigurasi tambahan)  

Solusi:  
- Menambahkan indexing pada kolom `student_id` dan `gpa` untuk mempercepat query.  

---

## JMeter Test CMD
/all-student
before:
![WhatsApp Image 2025-03-14 at 01 08 15_5b327863](https://github.com/user-attachments/assets/6aa7e2c2-8b88-41af-aba6-87b37fe9961c)

after:
![WhatsApp Image 2025-03-14 at 17 18 09_c78a7fdc](https://github.com/user-attachments/assets/0da1e36c-a532-4e39-b9c0-118bcadbc75b)

/all-student-name
before:
![WhatsApp Image 2025-03-14 at 01 09 40_440e1621](https://github.com/user-attachments/assets/55dabf69-7d3b-43e2-86eb-9963b25fcbd3)

after:
![WhatsApp Image 2025-03-14 at 17 22 02_39dae928](https://github.com/user-attachments/assets/5e6db564-73c2-41ce-b58b-a6bdd4c20c08)

/highest-gpa
before:
![WhatsApp Image 2025-03-14 at 01 10 26_4b864bed](https://github.com/user-attachments/assets/b3f0af47-6fa4-45e1-ad59-e802c2993b7b)

after:
![WhatsApp Image 2025-03-14 at 17 23 59_8c6af481](https://github.com/user-attachments/assets/48d06350-688e-4b81-9bce-3cd8e50642fb)

## JMeter Test App
/all-student
before:
![WhatsApp Image 2025-03-13 at 23 12 23_4e68199e](https://github.com/user-attachments/assets/9c696d3d-9834-457f-82b1-751cc8832c04)

after:
![WhatsApp Image 2025-03-14 at 17 13 47_c41eff50](https://github.com/user-attachments/assets/c9463c2e-b180-4ddc-af8a-78f6286c344c)

/all-student-name
before:
![WhatsApp Image 2025-03-13 at 23 18 49_93265c85](https://github.com/user-attachments/assets/3713f557-0b19-4bb9-8b34-37ca13cb9ea2)

after:
![WhatsApp Image 2025-03-14 at 17 21 09_1fac03fe](https://github.com/user-attachments/assets/b6915a5c-4082-48a1-9811-4d553730ee70)


/highest-gpa
before:
![WhatsApp Image 2025-03-13 at 23 26 33_1b535fa4](https://github.com/user-attachments/assets/849588c2-f356-4277-b101-bd635e2048ca)

after:
![WhatsApp Image 2025-03-14 at 17 23 12_1b7b0c7b](https://github.com/user-attachments/assets/4f25b738-986c-4435-acdc-2182f61b4775)

---
