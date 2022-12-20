# Praktikum_Komnum_2

> Kelompok C01>
> </br>
> Nama Anggota :
> </br>
>
> 1. Robby Ulung Pambudi (5025211042)
> 2. Sandyatama Fransisna Nugraha (5025211196)
> 3. Hanafi Stary

## Problem

Salah satu kelemahan dari metode Trapezoidal adalah kita harus menggunakan jumlah interval yang besar untuk memperoleh akurasi yang diharapkan. Buatlah sebuah program komputer untuk menjelaskan bagaimana metode Integrasi Romberg dapat mengatasi kelemahan tersebut.

## Penyelesaian

Integrasi Romberg adalah perluasan yang relatif mudah dari keluarga algoritma Newton-Cotes yang mendsarinya untuk memberikan perkiraan nilai integral yang lebih akurat. Integrasi Romberg sendiri mengadaptasi prilaku dari fungsi trapesium pada batas untuk menghasilkan estimasi integral.

Untuk memahami integrasi Romberg, kita harus memulai dengan implementasi rekursif dari aturan trapesium. Yaitu
$$\int_{a}^{b} f(x) dx = \lim_{m \to \infty } \sum_{i = 1}^{m} \frac{(c_{c+1} - c_{i}) \cdot (f(c_{i + 1}) + f(c_{i}))}{m}$$

Metode ini digunakan untuk memperbaiki hasil pendekatan integrasi metode trapesium pada rumus diatas, karena pada metode trapesium kesalahan metode trapesium `cukup` besar untuk polinom pangkat tinggi dan fungsi transeden.

Pada proses integrasi Romberg, mula-mula dihitung kuadratur dengan lebar langkah h pada proses integrasi Romberg, pertama kita hitung kuadratur dengan lebar langkah h dan 2h.

Misalkan $a = x_{0} < x_{1} < ... x_{n} = b$ merupakan partisi $[a,b]$. Suatu rumus berbentuk

$$
Q[f] = \sum_{i = 0}^{N} w_{i}f(x_{i}) = w_{0}f(x_{0}) + w_{1}f(x_1) + ... + w_{N}f(x_{N})
$$

Sedemikian hingga

$$
\int_{a}^{b} f(x) dx = Q[f] + E[f]
$$

fungsi diatas disebut rumus integral numerik atau kuadrat. Suku $E[f]$ disebut galat **Pemotongan Integral**. Nilai-nilai $[x_{i}]_{i = 0} ^{N}$ disebut simpul-simpul kuadratur dan nilai nilai $[w_{i}]_{i = 0} ^{N}$ disebut bobot.

Untuk menurunkan galat hampiran integral dari `O(h2)` menjadi `O(h2n + 2)` dapat digunakan ekstrapolasi Richardson seperti dinyatakan dalam teoream L

$$
Q = \frac{4^2 R_{k} (f_{k}h) - R_{k}(f_{k}2h)}{4^k -1} + O(h^{2k + 2})
$$

Jika didefinisikan barisan kuadratur ${I (i,j): i >= Bi -1 \times i >= 3}$ (Barisan aturan Boole Majemuk).

Maka Integrasi romberg untuk meningkatkan keakuratan hampiran integral dapat di tulis sebagai.

$$
I_{j, k} = \frac{4^k I_{j, k-1} - I_{j-1, k-1}}{4^k - 1}
$$

Maka Implementasi code program adalah sebagai berikut

```
import numpy as np

```

### Algortima

## Refrensi

[1]: https://wahyuz98.github.io/Wahyu_Zainur.github.io/INTEGRASI_NUMERIK/ 'Integrasi Numerik'
