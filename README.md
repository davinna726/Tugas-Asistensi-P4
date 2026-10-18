# Tugas-Asistensi-P4
1.Dibuat fungsi updateHarga yang menerima pointer ke Barang dan harga baru. Karena yang dikirim adalah alamat barang (pass by reference), fungsi mengubah harga di data aslinya lewat operator panah, sehingga perubahannya tetap ada setelah fungsi selesai.
‘’’
void updateHarga(Barang *b, int hargaBaru) {
    b->harga = hargaBaru;
}
‘’’


2.Dibuat fungsi updateNama dengan parameter pointer Barang dan nama baru. Nama berupa array karakter, jadi tidak bisa diganti dengan tanda =. Penggantiannya memakai strcpy dari <string.h>.
void updateNama(Barang *b, char namaBaru[]) {
    strcpy(b->nama, namaBaru);
}


3.Pada beliBarang, setelah total dihitung, program memeriksa dulu apakah m bukan NULL, baru memeriksa m->poin >= 1000. Jika ya, total dikurangi 10% dan poin member dikurangi 1000 lewat pointer.
int total = b->harga * qty;
if (m != NULL && m->poin >= 1000) {
    total = total - total / 10;   // diskon 10%
    m->poin -= 1000;
}


