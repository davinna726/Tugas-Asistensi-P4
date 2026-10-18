# Tugas-Asistensi-P4
1.Dibuat fungsi updateHarga yang menerima pointer ke Barang dan harga baru. Karena yang dikirim adalah alamat barang (pass by reference), fungsi mengubah harga di data aslinya lewat operator panah, sehingga perubahannya tetap ada setelah fungsi selesai.
```c
void updateHarga(Barang *b, int hargaBaru) { 
    b->harga = hargaBaru; 
}
```

2.Dibuat fungsi updateNama dengan parameter pointer Barang dan nama baru. Nama berupa array karakter, jadi tidak bisa diganti dengan tanda =. Penggantiannya memakai strcpy dari <string.h>.
```c
void updateNama(Barang *b, char namaBaru[]) {
    strcpy(b->nama, namaBaru);
}
```

3.Pada beliBarang, setelah total dihitung, program memeriksa dulu apakah m bukan NULL, baru memeriksa m->poin >= 1000. Jika ya, total dikurangi 10% dan poin member dikurangi 1000 lewat pointer.
```c
int total = b->harga * qty;
if (m != NULL && m->poin >= 1000) {
    total = total - total / 10;   // diskon 10%
    m->poin -= 1000;
}
```
4.Tugas bonus
```c
#include <stdio.h>
#include <string.h>

typedef struct { char nama[50]; int harga; int stock; } Barang;
typedef struct { char nama[50]; int poin; } Member;

void cekBarang(Barang db[], int ukuran) {
    printf("\n--- Katalog Barang ---\n");
    for(int i=0; i<ukuran; i++) {
        printf("%d. %s - Rp%d (Stok: %d)\n", i+1, db[i].nama, db[i].harga, db[i].stock);
    }
}
void cekMember(Member db[], int ukuran) {
    printf("\n--- Data Member ---\n");
    for(int i=0; i<ukuran; i++) {
        printf("%d. %s - Poin: %d\n", i+1, db[i].nama, db[i].poin);
    }
}
void beliBarang(Barang *b, Member *m, int qty) {
    if (b->stock >= qty) {
        b->stock -= qty;
        int total = b->harga * qty;
        printf("\n[TRANSAKSI] %d %s Terjual. Total: Rp%d\n", qty, b->nama, total);
        if (total >= 20000 && m != NULL) {
            m->poin += 100;
            printf("  -> Member %s mendapat +100 Poin!\n", m->nama);
        }
    } else {
        printf("\n[GAGAL] Stok %s (Tersisa: %d) tidak cukup untuk dibeli sebanyak %d!\n", b->nama, b->stock, qty);
    }
}

int main() {
    Barang dbBarang[5] = { {"Sabun", 5000, 10}, {"Sampo", 15000, 5}, {"Roti", 12000, 8}, {"Susu", 25000, 15}, {"Kopi", 22000, 20} };
    Member dbMember[2] = { {"Anisa", 500}, {"Budi", 100} };

    printf("=== SELAMAT DATANG DI MINIMARKET ===\n");

    while (1) {
        printf("\n[1] Lihat Barang | [2] Beli Barang | [3] Cek Member | [4] Keluar\n");
        printf("Pilihan: ");
        int pilihan;
        scanf("%d", &pilihan);

        if (pilihan == 4) {
            printf("Terima kasih sudah berbelanja!\n");
            break;
        }

        switch (pilihan) {
            case 1:
                cekBarang(dbBarang, 5);
                break;
            case 2: {
                int noBarang, qty, noMember;
                cekBarang(dbBarang, 5);
                printf("Nomor barang (1-5): ");
                scanf("%d", &noBarang);
                printf("Jumlah: ");
                scanf("%d", &qty);
                printf("Nomor member (1-2, 0 jika bukan member): ");
                scanf("%d", &noMember);
                if (noBarang < 1 || noBarang > 5 || qty < 1 || noMember < 0 || noMember > 2) {
                    printf("\n[GAGAL] Input tidak valid!\n");
                } else {
                    Member *m = (noMember == 0) ? NULL : &dbMember[noMember - 1];
                    beliBarang(&dbBarang[noBarang - 1], m, qty);
                }
                break;
            }
            case 3:
                cekMember(dbMember, 2);
                break;
            default:
                printf("\nPilihan tidak ada, coba lagi.\n");
        }
    }
    return 0;
}
```
