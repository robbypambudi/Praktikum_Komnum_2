# Praktikum_Komnum_2

> Kelompok C01
> </br>
> Nama Anggota :
> </br>
>
> 1. Robby Ulung Pambudi (5025211042)
> 2. Sandyatama Fransisna Nugraha (5025211196)
> 3. Hanafi Satriyo Utomo Setiawan (5025211195)

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
from tabulate import tabulate

def trapezoidal(f, a, b, n):

    h = (b - a) / n
    x = a

    In = f(a)
    for k in range(1, n):
        x = x + h
        In += 2*f(x)

    return (In + f(b))*h*0.5


def romberg(f, a, b, p):

    I = np.zeros((p, p))
    for k in range(0, p):
        I[k, 0] = trapezoidal(f, a, b, 2**k)

        for j in range(0, k):
            # Romberg formula
            I[k, j+1] = (4**(j+1) * I[k, j] - I[k-1, j]) / (4**(j+1) - 1)
    return I

if __name__ == '__main__':

    def f(x):
        f = eval(func)
        return f

    func = input("Masukkan fungsi: ")
    p_rows = (int (input("Masukkan jumlah baris: ")))
    upper = (int (input("Masukkan batas atas: ")))
    lower = (int (input("Masukkan batas bawah: ")))

    I = romberg(f, upper, lower, p_rows)
    solution = I[p_rows-1, p_rows-1]
    solution = round(solution, 4)
    print("Tabel Hasil:")
    print(tabulate(I, tablefmt="fancy_grid"))
    print("Hasil: ", solution)
```

#### Input

```
Masukkan fungsi: np.sin(x)
Masukkan jumlah baris: 4
Masukkan batas atas: 0
Masukkan batas bawah: 3
```

#### Output

Tabel Hasil:
```
╒═════════╤═════════╤═════════╤══════╕
│ 0.21168 │ 0       │ 0       │ 0    │
├─────────┼─────────┼─────────┼──────┤
│ 1.60208 │ 2.06555 │ 0       │ 0    │
├─────────┼─────────┼─────────┼──────┤
│ 1.89583 │ 1.99374 │ 1.98895 │ 0    │
├─────────┼─────────┼─────────┼──────┤
│ 1.96662 │ 1.99021 │ 1.98998 │ 1.99 │
╘═════════╧═════════╧═════════╧══════╛
```
Hasil: 1.99

## Refrensi
 1.  [Integrasi Numerik by Wahyu_Zainur](https://wahyuz98.github.io/Wahyu_Zainur.github.io/INTEGRASI_NUMERIK)

2. [Tugas Romberg by Riyanhidayat0811](https://riyanhidayat0811.github.io/Tugas/Romberg/)