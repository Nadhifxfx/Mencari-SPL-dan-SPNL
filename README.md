# Mencari SPL dan SPNL
Nama : Nadhif Fathur Rahman      
Kelas : TIF22A      
NIM : 23422027

# Soal
**Persamaan Non Linier**            
3 + x³ - x = 4            
**Persamaan Linier**            
2x - 4 = 8

Intruksi :
- Carilah Solusi dari 2 soal diatas (metode bebas)
-  Buatlah Program untuk mencari solusi diatas
-  Dan tunjukkan nilai x di setiap iterasinya

# Solusi 
1. **Metode Secant** adalah suatu teknik numerik yang digunakan untuk mencari akar dari persamaan non-linear. Pada contoh persamaan non linear 3 + x^3 - x = 4, kita implementasikan metode Secant menggunakan dua nilai awal, x^0 dan x^1 untuk mendekati akar. Proses iteratif dilakukan hingga mencapai konvergensi dengan toleransi yang ditentukan atau mencapai batas maksimum iterasi.

    Berikut adalah implementasi dalam Python:
```python
def secant_method(func, x0, x1, tol, max_iter):
    iterasi = 0
    
    while iterasi < max_iter:
        x2 = x1 - (func(x1) * (x1 - x0)) / (func(x1) - func(x0))
        
        print(f"Iterasi {iterasi + 1}: x = {x2}")
        
        if abs(x2 - x1) < tol:
            return x2, iterasi + 1
        
        x0, x1 = x1, x2
        iterasi += 1
    
    raise ValueError("Metode Secant tidak konvergen dalam jumlah iterasi yang ditentukan.")

# Fungsi persamaan non-linear
def f(x):
    return 3 + x**3 - x - 4

# Nilai awal
x0_secant = 1.0
x1_secant = 2.0

# Toleransi dan maksimum iterasi
toleransi = 1e-6
max_iter = 100

# Solusi menggunakan metode Secant
solusi_secant, iterasi_secant = secant_method(f, x0_secant, x1_secant, toleransi, max_iter)

print("\nMetode Secant:")
print("Solusi: x =", solusi_secant)
print("Jumlah total iterasi:", iterasi_secant)
```
Output:
```
Iterasi 1: x = 1.1666666666666665
Iterasi 2: x = 1.2531120331950207
Iterasi 3: x = 1.3372064458416562
Iterasi 4: x = 1.323850096387641
Iterasi 5: x = 1.324707936532088
Iterasi 6: x = 1.3247179653538177
Iterasi 7: x = 1.3247179572446703

Metode Secant:
Solusi: x = 1.3247179572446703
Jumlah total iterasi: 7
```
2. **Metode Eliminasi Gauss** adalah teknik yang digunakan untuk menyelesaikan sistem persamaan linear. Pada kasus ini dengan satu persamaan 2x - 4 = 8 kita dapat menerapkan metode ini untuk menemukan nilai x. Prosesnya melibatkan iterasi untuk mengeliminasi variabel dalam persamaan, sehingga kita dapat mengisolasi nilai x.

    Berikut adalah implementasi dalam Python:
```python
def elimination_gauss(coefficients, constants):
    n = len(coefficients)
    
    # Lakukan eliminasi
    for i in range(n):
        pivot = coefficients[i][i]
        ratio = constants[i] / pivot
        
        # Hitung nilai x
        constants[i] = ratio
        for j in range(n):
            coefficients[i][j] /= pivot
        
        # Eliminasi variabel di bawah baris i
        for k in range(i+1, n):
            ratio = coefficients[k][i]
            constants[k] -= ratio * constants[i]
            for j in range(n):
                coefficients[k][j] -= ratio * coefficients[i][j]

    # Hitung nilai x dari baris terakhir
    x = constants

    return x

# Persamaan linear: 2x - 4 = 8
coefficients = [[2]]
constants = [8]

# Solusi menggunakan metode Eliminasi Gauss
solusi_gauss = elimination_gauss(coefficients, constants)

print("Metode Eliminasi Gauss:")
print("Solusi: x =", solusi_gauss[0])
```
Output:
```
Metode Eliminasi Gauss:
Solusi: x = 4.0
