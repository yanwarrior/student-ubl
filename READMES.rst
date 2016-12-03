Student UBL
===========

Package API sederhana untuk mengakses data student dari resource dalam format json yang dapat diimplementasikan sebagai authentication untuk aplikasi lain yang membutuhkan informasi tentang student UBL (Mahasiswa BL).

Instalasi
---------
Instalasi sangat mudah, hanya menggunakan PIP untuk menginstal dari repositori::
    
    pip install student-ubl


QuickStart
----------
Contoh berikut adalah bagaimana menggunakan API dasar yaitu API Biodata student. pada contoh di bawah kita akan mengambil informasi tentang biodata student UBL::
    
    >>> from student_ubl.student import FacadeStudentUBL
    >>>
    >>> mahasiswa = FacadeStudentUBL()
    >>> mahasiswa.authenticated(nim='student nim', password='student password')
    >>> 
    >>> # cek apakah yang login mahasiswa UBL ?
    >>> biodata.is_student()
    True
    >>>
    >>> # ambil profile mahasiswa dalam format json
    >>> biodata.get_profile('json')
        '{
      "biodata": {
        "telpon": "021-657544",
        "tempat_lahir": "Jakarta",
        "fakultas": "Fakultas Teknologi Informasi",
        "no._sttb": "XXX 009766",
        "nama_lengkap": "Yanwar Solahudin",
        "nim": "1111503007",
        "peminatan": "",
        "tanggal_yudisium": "",
        "program_studi": "Teknik Informatika",
        "jenis_kelamin": "Pria",
        "tanggal_wisuda": "",
        "nama_orang_tua": "Steven",
        "tanggal_sttb": "26-04-2010",
        "tanggal_lahir": "03-11-1992",
        "tanggal_lulus_teori": "",
        "agama": "Islam",
        "alamat": "Jl.XXXX"
      }
    }'

Untuk mendapatkan output built-in dictionary, hilangkan saja format 'json'. secara default formatnya adalah dictionary python::

    >>> biodata.get_profile()
    
    {'agama': 'Islam',
     'alamat': 'Jl.XXXX',
     'fakultas': 'Fakultas Teknologi Informasi',
     'jenis_kelamin': 'Pria',
     'nama_lengkap': 'Yanwar Solahudin',
     'nama_orang_tua': 'Steven',
     'nim': '1111503007',
     'no._sttb': 'XXX 009766',
     'peminatan': '',
     'program_studi': 'Teknik Informatika',
     'tanggal_lahir': '03-11-1992',
     'tanggal_lulus_teori': '',
     'tanggal_sttb': '26-04-2010',
     'tanggal_wisuda': '',
     'tanggal_yudisium': '',
     'telpon': '021-58902355',
     'tempat_lahir': 'Jakarta'}



API Akademik
------------
Terdapat fitur api akademik yang digunakan untuk mencari tahun ajaran, nilai semester dan hsk. berikut adalah contoh penggunaan API untuk akademik::

    >>> akademik = mahasiswa.akademik_api()
    >>> akademik
    <student_ubl.student.AkademikAPI object at 0x0000000002DD9DD8>

Tahun Ajaran
^^^^^^^^^^^^
Data tahun ajaran kita butuhkan untuk mengakses nilai semester. tahun ajaran terdiri dari tahun studi dan semester. untuk mendapatkan data tahun ajaran dari resource, kita bisa menggunakan method `get_tahun_ajaran(reult_format)`::

```python
>>> akademik.get_tahun_ajaran()
{'semester': {'E': 'Genap', 'O': 'Gasal'},
 'tahun_ajarn': ['20092010',
                 '20102011',
                 '20112012',
                 '20122013',
                 '20132014',
                 '20142015',
                 '20152016',
                 '20162017']}
```

**Catatan**: Untuk mengubah data hasil diatas menjadi json format, tambahkan parameter `json` pada method tersebut.

### Nilai Semester
Setelah kita memperoleh data tahun ajaran, kita sekarang bisa mengabil nilai 
semester berdasarkan semester dan tahun studi. misalnya kita akan mengambil 
data nilai semester di tahun **2015-2016** pada semester **ganjil**::

```python
>>> akademik.get_tahun_ajaran()

{'BA011': {'absen': 100,
         'final': 82,
         'kel': 'AB',
         'matakuliah': 'Bahasa Inggris Lanjutan',
         'mid': 85,
         'no': 8,
         'tgs': 76,
         'tinjauan_nilai': 'Blm dimulai'},
'KP043': {'absen': 100,
         'final': 68,
         'kel': 'AE',
         'matakuliah': 'Keamanan Komputer',
         'mid': 85,
         'no': 4,
         'tgs': 100,
         'tinjauan_nilai': 'Blm dimulai'},
'KP045': {'absen': 86,
         'final': 69,
         'kel': 'AD',
         'matakuliah': 'Kecerdasan Tiruan',
         'mid': 80,
         'no': 1,
         'tgs': 80,
         'tinjauan_nilai': 'Blm dimulai'},
'KP301': {'absen': 93,
         'final': 77,
         'kel': 'AA',
         'matakuliah': 'Oracle : Introduction SQL dan PL/SQL',
         'mid': 89,
         'no': 5,
         'tgs': 100,
         'tinjauan_nilai': 'Blm dimulai'},
'PG119': {'absen': 100,
         'final': 90,
         'kel': 'AB',
         'matakuliah': 'Mobile Programming',
         'mid': 75,
         'no': 2,
         'tgs': 85,
         'tinjauan_nilai': 'Blm dimulai'},
'PG130': {'absen': 100,
         'final': 90,
         'kel': 'AB',
         'matakuliah': 'Java Web Programming',
         'mid': 90,
         'no': 3,
         'tgs': 90,
         'tinjauan_nilai': 'Blm dimulai'},
'UM013': {'absen': 100,
         'final': 85,
         'kel': 'AE',
         'matakuliah': 'Metodologi Riset',
         'mid': 75,
         'no': 6,
         'tgs': 50,
         'tinjauan_nilai': 'Blm dimulai'},
'UM021': {'absen': 100,
         'final': 70,
         'kel': 'XM',
         'matakuliah': 'Pendidikan Pancasila',
         'mid': 53,
         'no': 7,
         'tgs': 90,
         'tinjauan_nilai': 'Blm dimulai'}}
```
    
**Catatan**: Untuk mengubah data hasil diatas menjadi json format, tambahkan parameter `json` pada method tersebut.

### HSK Online
Untuk mendapatkan nilai HSK online, kita bisa menggunakan method `get_hsk`:

    >>> akademik.get_hsk()
    
    [{'index_prestasi': {'am': 3.0, 'hm': 'b', 'k': 3.0, 'm': 9.0},
      'kode': 'kp002',
      'matakuliah': 'algoritma dan struktur data 1*',
      'no': 1},
     {'index_prestasi': {'am': 2.0, 'hm': 'c', 'k': 3.0, 'm': 6.0},
      'kode': 'kp003',
      'matakuliah': 'algoritma dan struktur data 2*',
      'no': 2},
     {'index_prestasi': {'am': 2.0, 'hm': 'c', 'k': 3.0, 'm': 6.0},
      'kode': 'kp011',
      'matakuliah': 'arsitektur komputer',
      'no': 3},
     {'index_prestasi': {'am': 3.0, 'hm': 'b', 'k': 2.0, 'm': 6.0},
      'kode': 'ba001',
      'matakuliah': 'bahasa indonesia',
      'no': 4},
     {'index_prestasi': {'am': 4.0, 'hm': 'a', 'k': 2.0, 'm': 8.0},
      'kode': 'ba003',
      'matakuliah': 'bahasa inggris',
      'no': 5},

     {.......},
     {.......},]

**Catatan**: Untuk mengubah data hasil diatas menjadi json format, tambahkan parameter **'json'** pada method tersebut.


License
-------
The MIT License (MIT) Copyright © 2016 Yanwar Solahudin, yanwarsolah@gmail.com

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.