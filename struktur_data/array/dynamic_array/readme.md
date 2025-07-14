## 📑 Daftar Isi: Dynamic Array C++

1. [Apa Itu Dynamic Array](#apa-itu-dynamic-array)
2. [Struktur Data DynamicArray](#struktur-data-dynamic-array)
3. [Manajemen Memori](#manajemen-memori)
   - [GrowArray](#growarray)
   - [ShrinkArray](#shrinkarray)
   - [reserve](#reserve)
   - [shrink_to_fit](#shrink_to_fit)
4. [Operasi Dasar](#operasi-dasar)
   - [push_back](#push_back)
   - [pop_back](#pop_back)
   - [InsertAt](#insertat)
   - [DeleteAt](#deleteat)
5. [Resize Array](#resize-array)
6. [Akses dan Utility](#akses-dan-utility)
   - [accesAtIndex](#accesatindex)
   - [front dan back](#front-dan-back)
   - [getsize dan getcapacity](#getsize-dan-getcapacity)
   - [clear](#clear)
   - [IsEmpty](#isempty)
7. [Pencarian](#pencarian)
   - [search](#search)


# Apa Itu Dynamic Array 
Dynamic array atau array dinamis adalah struktur data array yang ukurannya dapat berubah selama program berjalan. Berbeda dengan array statis yang kapasitasnya harus ditentukan saat deklarasi dan tidak bisa diubah, array dinamis memungkinkan penambahan elemen tanpa batasan ukuran awal. Hal ini membuatnya sangat cocok digunakan untuk menangani data real-time atau data dengan jumlah yang tidak diketahui sebelumnya.

Meskipun begitu, array dinamis tetap memiliki keterbatasan, yaitu biasanya hanya dapat menampung sekitar $10^5$ hingga $10^6$ elemen, tergantung pada batasan memori sistem dan metode alokasi yang digunakan (heap atau stack).

untuk di C++ kita mengenal vector sebagai array dinamis,nah disini kita akan bahas
bagaimana dynamic array pada vector bekerja.

# Struktur Data Dynamic Array
untuk dynamic array di cpp kita memakai class untuk mendeklarasikan sebuah array yang bersifat dinamis

```cpp
class DynamicArray{

}
```
Sebuah array dinamis umumnya memiliki dua access specifier, yaitu private dan public, untuk memisahkan data internal dan fungsi yang dapat diakses dari luar class
### Untuk `private`
Access specifier `private` berfungsi untuk menyembunyikan detail implementasi dari luar class dan menjaga integritas data. Dalam konteks array dinamis, biasanya terdapat tiga properti penting yang dideklarasikan sebagai `private`, yaitu:
```cpp
class DynamicArray{
    private:
        int* array;
        int size;
        int capacity;
}
```
acces specifier private memiliki property yaitu: 
1.`int* array` yaitu sebuah pointer array untuk menyimpan element array secara dinamis
2.`int size`,yaitu banyak element dalam satu array
3.`int capacity`,kapasitas maksimul yang dapat ditampung array

Tujuan properti tersebut disimpan sebagai private adalah untuk menjaga enkapsulasi dan integritas internal dari struktur data. Dengan demikian, hanya method dalam class yang boleh mengakses dan memodifikasi nilai-nilai ini, sehingga mencegah manipulasi langsung dari luar yang dapat menyebabkan inkonsistensi data atau perilaku tak terduga.
### Untuk `Public`
```cpp
class DynamicArray{
    public:
        DynamicArray(){
            capacity = 1;
            size = 0;
            array = new int[capacity];
        }
        DynamicArray(int capacity){
            this->capacity = capacity;
            array = new int[capacity];
            size = 0;
        }
}
```
Class DynamicArray memiliki dua buah constructor, salah satunya adalah default constructor. Constructor ini digunakan untuk menginisialisasi kondisi awal array saat objek pertama kali dibuat. Nilai-nilai yang diatur dalam default constructor antara lain:
1. `Capacity = 1` minimal kapasitas array pertama kali harus 1 element
2. `size` = 0,pada saay array dideklarasi banyak element dalam array harus 0
3. `array = new int[capacity]` mendeklarasikan sebuah array dengan kapasitas sebesar `capacity`