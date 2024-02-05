#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>
// deklarasi tipe data dengan nama datacs
typedef struct
{
    char nama[50];
} datacs;

// deklarasi isi dari sebuah queue
typedef struct
{
    int first;
    int last;
    datacs data[10];
} queue;
// prosedur membuat queue
void createEmpty(queue *Q)
{
    (*Q).first = -1;
    (*Q).last = -1;
}

// fungsi mengecek apakah queue kosong atau tidak

int isEmpty(queue Q)
{
    int hasil = 0;
    if (Q.first == -1)
    {
        hasil = 1;
    }
    return hasil;
}

// fungsi mengecek apakah queue penuh atau tidak
int isFull(queue Q)
{
    int hasil = 0;
    if (Q.first == 10)
    {
        hasil = 1;
    }
    return hasil;
}
// prosedur menambah data baru di queue

void add(queue *Q, char nama[])
{
    if (isEmpty(*Q) == 1)
    {
        (*Q).first = 0;
        (*Q).last = 0;
        strcpy((*Q).data[0].nama, nama);
    }
    else
    {
        if (isFull(*Q) != 1)
        {
            (*Q).last = (*Q).last + 1;
            strcpy((*Q).data[(*Q).last].nama, nama);
        }
        else
        {
            printf("Queue Penuh\n");
        }
    }
}
// prosedur menghapus data di queue

void del(queue *Q, int cs, int layani)
{
    if (layani <= cs)
    {
        if ((*Q).last == 0)
        {
            (*Q).first = -1;
            (*Q).last = -1;
        }
        else
        {
            // Menggeser elemen kedepan
            int i;
            strcpy((*Q).data[layani - 1].nama, (*Q).data[cs].nama);
            for (i = cs + 1; i <= (*Q).last; i++)
            {
                strcpy((*Q).data[i - 1].nama, (*Q).data[i].nama);
            }
            (*Q).last = (*Q).last - 1;
        }
        printf("#######\n");
        printf("####### Pengunjung di Costumer Service %d \n", layani);
        printf("####### Telah Dilayani\n");
        printf("#######\n");
        printf("########################################\n");
        getchar();
    }
    else
    {
        printf("#######\n");
        printf("####### Gagal Dilayani \n", cs);
        printf("####### Banyak Costumer Service Hanya %d \n");
        printf("#######\n");
        printf("########################################\n");
        getchar();
    }
}

// prosedur menampilkan isi queue
void printQueue(queue Q)
{
    if (isEmpty(Q) == 0)
    {
        int i;
        for (i = Q.first; i <= Q.last; i++)
        {
            printf("%s", Q.data[i].nama);
        }
        printf("\n");
    }
    else
    {
        printf("Queue Kosong\n");
    }
}
// program utama

int main()
{
    char nama[20];
    int pilih, cs;
    int layani;

    system("cls");
    printf("########################################\n");
    printf("####### #######\n");
    printf("####### COSTUMER SERVICE BNI #######\n");
    printf("####### BANK INI ITU #######\n");
    printf("####### #######\n");
    printf("########################################\n");
    printf("#######\n");
    printf("####### Masukkan Banyak \n");
    printf("####### Costumer Servive : ");
    scanf("%d", &cs);
    // pengecekan jumlah max CS
    if (cs > 5 || cs < 1)
    {
        printf("#######\n");
        printf("####### Jumlah Costumer \n");
        printf("####### Servive Max. 5\n");
        printf("####### \n");
        printf("########################################\n");
        getchar();
    }
    else
    {
        queue Q;
        createEmpty(&Q);
        do
        {
            system("cls");
            printf("########################################\n");
            printf("####### #######\n");
            printf("####### COSTUMER SERVICE BNI #######\n");
            printf("####### BANK INI ITU #######\n");
            printf("####### #######\n");
            printf("########################################\n");
            printf("####### #######\n");
            printf("####### 1. Datangi CS #######\n");
            printf("####### 2. Layani Pengunjung #######\n");
            printf("####### 3. Lihat Pengunjung #######\n");
            printf("####### 4. Keluar #######\n");
            printf("####### #######\n");
            printf("########################################\n");
            printf("####### \n");
            printf("####### Masukkan Pilihan : ");
            scanf("%d", &pilih);

            switch (pilih)
            {
            case 1:
                // penambahan data baru
                printf("####### \n");
                printf("####### Masukkan Nama \n");
                printf("####### Pengunjung : ");
                scanf("%s", &nama);
                add(&Q, nama);
                printf("#######\n");
                printf("####### Pengunjung Berhasil Didata\n");
                printf("####### \n");
                printf("########################################\n");
                getchar();
                break;

            case 2:
                // penghapusan data

                if (Q.first == -1)
                {
                    printf("#######\n");
                    printf("####### Tidak Ada Pengunjung\n");
                    printf("####### \n");
                    printf("########################################\n");
                }
                else
                {
                    printf("#######\n");
                    printf("####### Nomor Costumer Servive\n");
                    printf("####### Yang Akan Melayani : ");
                    scanf("%d", &layani);
                    del(&Q, cs, layani);
                }
                getchar();
                break;

            case 3:
                // menampilkan data
                printQueue(Q);
                getchar();
                break;

            case 4:
                // keluar program
                system("exit");
                break;

            default:
                printf("####### \n");
                printf("####### MAAF MENU TIDAK ADA \n");
                printf("####### DALAM PILIHAN \n");
                printf("####### \n");
                printf("########################################\n");
                break;
            }
        } while (pilih != 4);
    }
}