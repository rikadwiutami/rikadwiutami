#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <string.h>
#include "boolean.h"
#include "users.h"
#include "members.h"
#include "barang.h"
#include "transactions.h"

char *home[6] = {"\n\n\t\t\t\tBeranda\n\n",NULL,NULL,NULL,NULL,NULL};
char *kelolaLaporan[6] = {"\n\n\t\t\t\tBeranda","Kelola Transaksi","Kelola Laporan\n\n",NULL,NULL,NULL};													
char *kelolaPenjualan[6] = {"\n\n\t\t\t\tBeranda","Kelola Transaksi","Kelola Penjualan\n\n",NULL,NULL,NULL};	
char *kelolaPenyewaan[6] = {"\n\n\t\t\t\tBeranda","Kelola Transaksi","Kelola Penyewaan\n\n",NULL,NULL,NULL};	
char *kelolaPembelian[6] = {"\n\n\t\t\t\tBeranda","Kelola Transaksi","Kelola Pembelian\n\n",NULL,NULL,NULL};				
char *kelola_diskon[6] = {"\n\n\t\t\t\tBeranda","Kelola Diskon\n\n",NULL,NULL,NULL,NULL};
char *kelola_transaksi[6] = {"\n\n\t\t\t\tBeranda","Kelola Transaksi\n\n",NULL,NULL,NULL,NULL};														
char *kelola_barang[6] = {"\n\n\t\t\t\tBeranda","Kelola Barang\n\n",NULL,NULL,NULL,NULL};	
char *kelola_member[6] = {"\n\n\t\t\t\tBeranda","Kelola Member\n\n",NULL,NULL,NULL,NULL};	
char *kelola_user[6] = {"\n\n\t\t\t\tBeranda","Kelola User\n\n",NULL,NULL,NULL,NULL};
char *hapusDiskon[6] = {"\n\n   Beranda","Kelola Diskon","Hapus Diskon\n\n\n",NULL,NULL,NULL};
char *hapusUser[6] = {"\n\n   Beranda","Kelola User","Hapus User\n\n\n",NULL,NULL,NULL};
char *hapus[6] = {"\n\n   Beranda","Kelola Transaksi","Kelola Pembelian","Hapus Pembelian\n\n",NULL,NULL};									
char *laporan[6] = {"\n\n    Beranda","Kelola Transaksi","Laporan\n\n",NULL,NULL,NULL};
char *hapusJual[6] = {"\n\n   Beranda","Kelola Transaksi","Kelola Penjualan","Hapus Penjualan\n\n",NULL,NULL};									
char *hapusSewa[6] = {"\n\n   Beranda","Kelola Transaksi","Kelola Penyewaan","Hapus Data Penyewaan\n\n\n",NULL,NULL};																
char *tampilkanSewa[6] = {"\n\n    Beranda","Kelola Transaksi","Kelola Penyewaan","Tampilkan Penyewaan\n\n\n",NULL,NULL};																									
char *tampilkanBarang[6] = {"\n\n   Beranda","Kelola Barang","Tampilkan Barang\n\n\n",NULL,NULL,NULL};
char *ubahBarang[6] = {"\n\n   Beranda","Kelola Barang","Ubah Barang\n\n\n",NULL,NULL,NULL};
char *nonaktifBarang[6] = {"\n\n   Beranda","Kelola Barang","Nonaktifkan Barang\n\n\n",NULL,NULL,NULL};																	
char *aktifBarang[6] = {"\n\n   Beranda","Kelola Barang","Aktifkan Barang\n\n\n",NULL,NULL,NULL};
char *tampilkanMember[6] = {"\n\n    Beranda","Kelola Member","Tampilkan Member\n\n",NULL,NULL,NULL};
char *ubahMember[6] = {"\n\n   Beranda","Kelola Member","Ubah Member\n\n\n",NULL,NULL,NULL};	
char *ubahUser[6] = {"\n\n   Beranda","Kelola User","Ubah User\n\n\n",NULL,NULL,NULL};
char *hapusBarang[6] = {"\n\n   Beranda","Kelola Barang","Hapus Barang\n\n\n",NULL,NULL,NULL};
char *ubahDiskon[6] = {"\n\n   Beranda","Kelola Diskon","Ubah Diskon\n\n\n",NULL,NULL,NULL};
char *nonaktifDiskon[6] = {"\n\n   Beranda","Kelola Diskon","Noaktifkan Diskon\n\n\n",NULL,NULL,NULL};																	
char *aktifDiskon[6] = {"\n\n   Beranda","Kelola Diskon","Aktifkan Diskon\n\n\n",NULL,NULL,NULL};
char *hapusMember[6] = {"\n\n   Beranda","Kelola Member","Hapus Member\n\n\n",NULL,NULL,NULL};

void MenuAdmin(Users UserNow);
void MenuKasir(Users UserNow);
void MenuGudang(Users UserNow);
static int status = false, counterRow;
char ulangi;

int main(){
	Users UserNow;
	char ulangi;
	
	login:
	do{
		if(Login(&UserNow)){
			printf("\n\n  Login Berhasil\n");
			printf("\n  Klik enter untuk masuk ke halaman dashboard ..."); getch();
			system("cls");
			if(strcmp(UserNow.role,"Administrator")==0){
				MenuAdmin(UserNow);
				if(status==true) goto login;
			} else if (strcmp(UserNow.role,"Kasir")==0){
				MenuKasir(UserNow);			
				if(status==true) goto login;
			} else{
				MenuGudang(UserNow);			
				if(status==true) goto login;
			}
		} else {
			printf("\n\n  Username atau Password Salah!\n");
		}
		ulangiUlangi:		
		printf("\n  Ulangi Login [Y/T] : "); fflush(stdin); scanf("%c", &ulangi);
		if(ulangi=='t' || ulangi=='T' || ulangi=='y' || ulangi=='Y'){
			system("cls");
		} else {
			goto ulangiUlangi;			
		}
	} while(ulangi=='Y' || ulangi=='y'); 
	return 0;
}

void MenuAdmin(Users UserNow){
	int pilih;
	char ulangi;
	MarqueeText("\n\n\n\n\n\n\n\n\n\n\n\n\n\t\t\t\t\tSelamat Datang, ",13999900);	
	MarqueeText(UserNow.nama,13999900);
	system("cls");
	menuAdmin:
	Breadcrumb(home);		
	printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
	printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
	printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
	printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
	printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
	printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                1. Kelola User                     \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                2. Kelola Member                   \xb3\n");
    printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                3. Kelola Barang                   \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                4. Kelola Diskon                   \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                5. Kelola Transaksi                \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                6. Pedoman Pengguna                \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                7. Ubah Tampilan                   \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                8. Logout                          \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
    printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
    MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",1);
	printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
	system("cls");
	switch(pilih){
		case 1:
			menuUser:
			Breadcrumb(kelola_user);
            printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
			printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
			printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
			printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
		    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
		    printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                1. Tambah User                     \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                2. Tampilkan User                  \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                3. Ubah User                       \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                4. Hapus User                      \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                5. Cari User                       \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			system("cls");
			switch(pilih){
				case 0:
					goto menuAdmin;
				break;
				case 1:
					TambahUser();
				break;
				case 2:
					counterRow = 13;
					TampilkanUser('n',&counterRow);
					printf("\n");
				break;
				case 3:
					Breadcrumb(ubahUser);						
					UbahUser();
				break;
				case 4:
					Breadcrumb(hapusUser);			
					HapusUser();
					printf("\n");
				break;
				case 5:
					CariUser();
					printf("\n");
				break;
				default:
					goto menuUser;
				break;			
			}
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuUser;
		break;			
		case 2:
			menuMember:
			Breadcrumb(kelola_member);
            printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
			printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
			printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
			printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
		    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
		    printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                1. Tambah Member                   \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                2. Tampilkan Member                \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                3. Ubah Member                     \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                4. Hapus Member                    \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                5. Cari Member                     \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			system("cls");
			switch(pilih){
				case 0:
					goto menuAdmin;
				break;					
				case 1:
					TambahMember('y');
				break;
				case 2:
					Breadcrumb(tampilkanMember);
					counterRow = 13;						
					TampilkanMember('n', &counterRow);
					printf("\n");
				break;
				case 3:
					Breadcrumb(ubahMember);
					UbahMember();
				break;
				case 4:
					Breadcrumb(hapusMember);							
					HapusMember();
				break;
				case 5:
					CariMember();
					printf("\n");	
				break;
				default:
					goto menuMember;
				break;			
			}
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");
			goto menuMember;
		break;
		case 3:
			menuBarang:
			Breadcrumb(kelola_barang);
            printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
			printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
			printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
			printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
		    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
		    printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                1. Tambah Barang                   \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                2. Tampilkan Barang                \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                3. Ubah Barang                     \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                4. Hapus Barang                    \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                5. Cari Barang                     \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                6. Aktifkan Barang                 \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                7. Nonaktifkan Barang              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			system("cls");
			switch(pilih){
				case 0:
					goto menuAdmin;
				break;					
				case 1:
					TambahBarang('y');
				break;
				case 2:
					Breadcrumb(tampilkanBarang);
					counterRow = 13;				
					TampilkanBarang('n','t','t', &counterRow, 't','t');
					printf("\n");
				break;
				case 3:
					Breadcrumb(ubahBarang);						
					UbahBarang();
					printf("\n");
				break;
				case 4:
					Breadcrumb(hapusBarang);						
					HapusBarang();
				break;
				case 5:
					CariBarang();
					printf("\n");
				break;
				case 6:
					Breadcrumb(aktifBarang);
		            AktifkanBarang();
		        break;
	        	case 7:
					Breadcrumb(nonaktifBarang);
		            NonaktifkanBarang();
		        break;
				default:
					goto menuBarang;
				break;			
			}
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuBarang;
		break;
		case 4:
		    menuDiskon:
			Breadcrumb(kelola_diskon);
            printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
			printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
			printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
			printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
		    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
		    printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                1. Tambah Diskon                   \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                2. Tampilkan Diskon                \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                3. Ubah Diskon                     \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                4. Hapus Diskon                    \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                5. Cari Diskon                     \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                6. Aktifkan Diskon                 \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                7. Nonaktifkan Diskon              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");				
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			system("cls");
			switch(pilih){
				case 0:
					goto menuAdmin;
				break;					
				case 1:
					TambahDiskon();
				break;
				case 2:
					counterRow = 13;
					TampilkanDiskon('n', &counterRow);
					printf("\n");
				break;
				case 3:
					Breadcrumb(ubahDiskon);						
					EditDiskon();
				break;
				case 4:
					Breadcrumb(hapusDiskon);		
					HapusDiskon();
					printf("\n");
				break;
				case 5:
					CariDiskon();
					printf("\n");
				break;
				case 6:
					Breadcrumb(aktifDiskon);						
		            AktifkanDiskon();
		            printf("\n");
		        break;
	        	case 7:
					Breadcrumb(nonaktifDiskon);
		            NonaktifkanDiskon();
		            printf("\n");
		        break;
				default:
					goto menuBarang;
				break;			
			}
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuDiskon;
		break;
		case 5:
			menuTransaksi:
			Breadcrumb(kelola_transaksi);
            printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
			printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
			printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
			printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
		    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
		    printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                1. Pembelian                       \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                2. Penjualan                       \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                3. Penyewaan                       \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                4. Laporan                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");				
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			system("cls");
			switch(pilih){
				case 0:
					goto menuAdmin;
				break;					
				case 1:
				    menuTransaksibeli:
			    	Breadcrumb(kelolaPembelian);
         		   	printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
					printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
					printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
					printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
			 	    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
		 		    printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                1. Pembelian                       \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                2. Hapus Data Beli                 \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                3. Tampilkan Data Beli             \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
					MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
					printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
					system("cls");
					switch(pilih){
						case 0:
							goto menuTransaksi;
						break;					
						case 1:
			            	Pembelian();
		            	break;
				  		case 2:
			            	Breadcrumb(hapus);
							HapusBeli();
						break;
						case 3:
			            	counterRow = 13;
							TampilkanPembelian('n', &counterRow);
							printf("\n");
						break;
						default:
							goto menuTransaksibeli;
						break;							
					}
					printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
					printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
					system("cls");			
					goto menuTransaksibeli;
				break;
				case 2:
				    menuTransaksijual:
			    	Breadcrumb(kelolaPenjualan);
       		   	    printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
					printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
				 	printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
					printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
				    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
	 			    printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                1. Penjualan                       \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                2. Hapus Data Jual                 \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                3. Tampilkan Data Jual             \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                4. Retur Barang                    \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");							
					printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
					MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
					printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
					system("cls");
					switch(pilih){
						case 0:
							goto menuTransaksi;
							break;					
						case 1:
			            	Penjualan();
			            	printf("\n");
		            	break;
			  			case 2:
			            	Breadcrumb(hapusJual);					  				
							HapusJual();
						break;
						case 3:
							counterRow = 13;					
							TampilkanPenjualan('n','t', &counterRow);
							printf("\n");
						break;
						case 4:
							ReturBarang();
							printf("\n");
						break;
						default:
						    goto menuTransaksijual;
						break;
					}
					printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
					printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
					system("cls");			
					goto menuTransaksijual;
				break;
				case 3:
				    menuTransaksisewa:
				    Breadcrumb(kelolaPenyewaan);
       		   	    printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
					printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
				 	printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
					printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
				    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
	 			    printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                1. Penyewaan                       \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                2. Pengembalian                    \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                3. Hapus Data Sewa                 \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                4. Tampilkan Data Sewa             \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");							
					printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
					MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
					printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
					system("cls");
					switch(pilih){
						case 0:
							goto menuTransaksi;
						break;					
						case 1:
			            	Penyewaan();
			            	printf("\n");
		            	break;
			  			case 2:
							Pengembalian();
							printf("\n");
						break;
						case 3:
			            	Breadcrumb(hapusSewa);									
							HapusSewa('n','t');
						break;
						case 4:
							counterRow = 13;
			            	Breadcrumb(tampilkanSewa);
							TampilkanPenyewaan('n','t', &counterRow);
							printf("\n");
						break;
						default:
						    goto menuTransaksisewa;
						break;
					}
					printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
					printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
					system("cls");			
					goto menuTransaksisewa;
				break;
				case 4:
				    menuTransaksilapor:
				    Breadcrumb(kelolaLaporan);
       		   	    printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
					printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
				 	printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
					printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
				    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
	 			    printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                1. Laporan                         \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");
					printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
					printf("\t\t\t        \xb3                                                   \xb3\n");						
					printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
					MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
					printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
					system("cls");
					switch(pilih){
						case 0:
							goto menuTransaksi;
						break;					
						case 1:
							Breadcrumb(laporan);
			            	Laporan();
			            	printf("\n\n ");
						break;
						default:
						    goto menuTransaksilapor;
						break;
					}
					printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
					printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
					system("cls");			
					goto menuTransaksilapor;
				break;						
			}
		case 6:
			panduan("txt/ADMIN.txt");
			printf("\n   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuAdmin;
		break;
		case 7:
			system("cls");
		    printf("\t\t\t        \xb3             ====== TAMPILAN ======              \xb3\n");
			printf("\t\t\t        \xb3                                                 \xb3\n");
			printf("\t\t\t        \xb3                1. LIGHT MODE                    \xb3\n");
			printf("\t\t\t        \xb3                                                 \xb3\n");
			printf("\t\t\t        \xb3                2. DARK MODE                     \xb3\n");
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);		
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			switch(pilih){
				case 1:
					system("color F0");
				break;
				case 2:
					system("color 07");
				break;
				default:
			    	goto menuAdmin;
			    break;
			}
			printf("\n   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuAdmin;
		break;
		case 8:
			Logout(&UserNow, &status);
		break;
		default:
			goto menuAdmin;
		break;
	}	
}

void MenuKasir(Users UserNow){
	int pilih;
	MarqueeText("\n\n\n\n\n\n\n\n\n\n\n\n\n\t\t\t\t\tSelamat Datang, ",13999900);	
	MarqueeText(UserNow.nama,13999900);
	system("cls");
	menuKasir:
	Breadcrumb(home);		
    printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
	printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
	printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
	printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
    printf("\t\t\t        \xb3             ====== Menu Kasir ======              \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                1. Pembelian                       \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                2. Penjualan                       \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                3. Penyewaan                       \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                4. Laporan                         \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                5. Pedoman Pengguna                \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                6. Ubah Tampilan                   \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                7. Logout                          \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");				
	printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
	MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
	printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
	system("cls");
	switch(pilih){
		case 0:
	        goto menuKasir;
		break;					
		case 1:
		    menuTransaksibeli:
	    	Breadcrumb(kelolaPembelian);
   		   	printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
			printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
			printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
			printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
	 	    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
 		    printf("\t\t\t        \xb3             ====== Menu Kasir ======              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                1. Pembelian                       \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                2. Hapus Data Beli                 \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                3. Tampilkan Data Beli             \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			system("cls");
			switch(pilih){
				case 0:
					goto menuKasir;
				break;					
				case 1:
		           	Pembelian();
		       	break;
		  		case 2:
		           	Breadcrumb(hapus);
					HapusBeli();
				break;
				case 3:
		           	counterRow = 13;
					TampilkanPembelian('n', &counterRow);
					printf("\n");
				break;
				default:
					goto menuTransaksibeli;
				break;							
			}
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuTransaksibeli;
		break;
		case 2:
	   		menuTransaksijual:
	    	Breadcrumb(kelolaPenjualan);
       	    printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
			printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
	 		printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
			printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
		    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
		    printf("\t\t\t        \xb3             ====== Menu Kasir ======              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                1. Penjualan                       \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                2. Hapus Data Jual                 \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                3. Tampilkan Data Jual             \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                4. Retur Barang                    \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");							
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			system("cls");
			switch(pilih){
				case 0:
					goto menuKasir;
				break;					
				case 1:
			       	Penjualan();
			       	printf("\n");
		        break;
			  	case 2:
			       	Breadcrumb(hapusJual);					  				
					HapusJual();
				break;
				case 3:
					counterRow = 13;									
					TampilkanPenjualan('n','t', &counterRow);
					printf("\n");
				break;
				case 4:
					ReturBarang();
					printf("\n");
				break;
				default:
				    goto menuTransaksijual;
				break;
			}
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuTransaksijual;
		break;
		case 3:
		    menuTransaksisewa:
		    Breadcrumb(kelolaPenyewaan);
       	    printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
			printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
		 	printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
			printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
		    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
	 	    printf("\t\t\t        \xb3             ====== Menu Kasir ======              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                1. Penyewaan                       \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                2. Pengembalian                    \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                3. Hapus Data Sewa                 \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                4. Tampilkan Data Sewa             \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");							
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			system("cls");
			switch(pilih){
				case 0:
					goto menuKasir;
				break;					
				case 1:
		          	Penyewaan();
		       	break;
				case 2:
					Pengembalian();
					printf("\n");
				break;
				case 3:
			       	Breadcrumb(hapusSewa);									
					HapusSewa('n','t');
				break;
				case 4:
					counterRow = 13;
			       	Breadcrumb(tampilkanSewa);
					TampilkanPenyewaan('n','t', &counterRow);
				break;
				default:
				    goto menuTransaksisewa;
				break;
			}
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuTransaksisewa;
		break;
		case 4:
		    menuTransaksilapor:
		    Breadcrumb(kelolaLaporan);
       	    printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
			printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
		 	printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
			printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
		    printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
		    printf("\t\t\t        \xb3             ====== Menu Kasir ======              \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                1. Laporan                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");
			printf("\t\t\t        \xb3                0. Kembali                         \xb3\n");
			printf("\t\t\t        \xb3                                                   \xb3\n");						
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			system("cls");
			switch(pilih){
				case 0:
					goto menuKasir;
				break;					
				case 1:
					Breadcrumb(laporan);
	            	Laporan();
	            	printf("\n\n ");
				break;
				default:
				    goto menuTransaksilapor;
				break;
			}
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuTransaksilapor;
		break;
		case 5:
			panduan("txt/KASIR.txt");
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuKasir;
		break;
		case 6:
			system("cls");
		    printf("\t\t\t        \xb3             ====== TAMPILAN ======              \xb3\n");
			printf("\t\t\t        \xb3                                                 \xb3\n");
			printf("\t\t\t        \xb3                1. LIGHT MODE                    \xb3\n");
			printf("\t\t\t        \xb3                                                 \xb3\n");
			printf("\t\t\t        \xb3                2. DARK MODE                     \xb3\n");
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",2000000);		
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			switch(pilih){
				case 1:
					system("color F0");
				break;
				case 2:
					system("color 07");
				break;
				default:
				    goto menuKasir;
			    break;
			}
			printf("\n   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuKasir;
		break;
		case 7:
			Logout(&UserNow, &status);
		break;
		default:
			goto menuKasir;
		break;
	}
}

void MenuGudang(Users UserNow){
	int pilih;
	MarqueeText("\n\n\n\n\n\n\n\n\n\n\n\n\n\t\t\t\t\tSelamat Datang, ",13999900);	
	MarqueeText(UserNow.nama,13999900);
	system("cls");
	menuBarangGudang:
	Breadcrumb(kelola_barang);
    printf("\t\t\t        \xda\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xbf\n");
	printf("\t\t\t        \xb3             TOKO KOMPUTER JAYA HARTONO            \xb3\n");
	printf("\t\t\t        \xb3 Jl. Gegerkalong Hilir, Ciwaruga, Kec. Parongpong  \xb3\n");
	printf("\t\t\t        \xb3    Kabupaten Bandung Barat, Jawa Barat 40559      \xb3\n");
	printf("\t\t\t        \xb3\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xb3\n");
	printf("\t\t\t        \xb3             ====== Menu Admin ======              \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                1. Tambah Barang                   \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                2. Tampilkan Barang                \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                3. Ubah Barang                     \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                4. Hapus Barang                    \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                5. Cari Barang                     \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                6. Aktifkan Barang                 \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                7. Nonaktifkan Barang              \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                8. Pedoman Pengguna                \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                9. Ubah Tampilan                   \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xb3                10. Logout                          \xb3\n");
	printf("\t\t\t        \xb3                                                   \xb3\n");
	printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
	MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);
	printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
	system("cls");
	switch(pilih){
		case 0:
			goto menuBarangGudang;
		break;					
		case 1:
			TambahBarang('y');
		break;
		case 2:
			Breadcrumb(tampilkanBarang);
			counterRow = 12;						
			TampilkanBarang('n','t','t', &counterRow, 'y','t');
			printf(" ");
		break;
		case 3:
			Breadcrumb(ubahBarang);						
			UbahBarang();
			printf("\n ");
		break;
		case 4:
			HapusBarang();
		break;
		case 5:
			CariBarang();
			printf("\n\n ");
		break;
		case 6:
			Breadcrumb(aktifBarang);
	        AktifkanBarang();
	        printf("\n ");
	    break;
	  	case 7:
			Breadcrumb(nonaktifBarang);
	        NonaktifkanBarang();
	        printf("\n ");
	    break;
		case 8:
			panduan("txt/GUDANG.txt");
			printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuBarangGudang;
		break;
		case 9:
			system("cls");
		    printf("\t\t\t        \xb3             ====== TAMPILAN ======              \xb3\n");
			printf("\t\t\t        \xb3                                                 \xb3\n");
			printf("\t\t\t        \xb3                1. LIGHT MODE                    \xb3\n");
			printf("\t\t\t        \xb3                                                 \xb3\n");
			printf("\t\t\t        \xb3                2. DARK MODE                     \xb3\n");
			printf("\t\t\t        \xc0\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xd9\n");
			MarqueeText("\t\t\t        \xb3\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xdb\xb3\n",3999900);		
			printf("\t\t\t                           Pilih Menu : "); scanf("%d", &pilih);
			switch(pilih){
				case 1:
					system("color F0");
				break;
				case 2:
					system("color 07");
				break;
				default:
			    	goto menuBarangGudang;
			    break;
			}
			printf("\n   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
			printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
			system("cls");			
			goto menuBarangGudang;
		break;
		case 10:
			Logout(&UserNow, &status);
		break;	
		default:
			goto menuBarangGudang;
		break;			
	}
	printf("   \xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4\xc4 \n");
	printf("   Tekan Mana Saja Untuk Kembali . . . "); getch();
	system("cls");			
	goto menuBarangGudang;
}
