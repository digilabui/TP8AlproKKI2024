# Tugas Pendahuluan 8
```bash
Nama    : [Kaera Yukio || CHANGE ME]
NPM     : [2306839344 || CHANGE ME]
```
---
## Teori (40%)
1. Keunggulan dan Kelemahan Linked List

    Jelaskan dengan detail mengenai kelebihan dan kelemahan **Linked List** dibandingkan dengan struktur data lainnya seperti **Array**. Sertakan contoh penerapan nyata di mana Linked List akan lebih preferable untuk digunakan dibandingkan Array.

2. Jenis Operasi di Linked List

    Sebagai seorang programmer, kalian akan sering diminta untuk melakukan operasi seperti insert, delete, dan search pada Linked List. Jelaskan algoritma untuk ketiga operasi tersebut beserta kompleksitas waktunya (worst case & average case).

3. Bagaimana cara melakukan reverse pada Linked List? Jelaskan dengan lengkap!

## Programming (Case Study, 60%)
Kalian diminta oleh Andi untuk melanjutkan program mengenai pengelolaan data mahasiswa dengan menggunakan **Single Linked List**. Program ini digunakan untuk menyimpan data mahasiswa dengan informasi berikut:
- Nama (String)
- NPM (Integer)
- IPK (Float)

Program ini sudah memiliki beberapa fungsi bawaan yang dibuat oleh Andi, namun kalian harus mengisi beberapa fungsi penting yang belum sempat diimplementasikan, sebab saat ini Andi belum sempat untuk meneruskannya, namun deadline sudah di depan mata. Oleh karena itu, bantulah Andi menyelesaikan pekerjaannya!
### Kode
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Struktur Node untuk menyimpan data mahasiswa
typedef struct Node {
    char name[50];
    int npm;
    float ipk;
    struct Node* next;
} Node;

// Fungsi untuk membuat node baru (provided)
Node* createNode(char* name, int npm, float ipk) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    strcpy(newNode->name, name);
    newNode->npm = npm;
    newNode->ipk = ipk;
    newNode->next = NULL;
    return newNode;
}

// Fungsi untuk mencetak daftar mahasiswa (provided)
void displayStudents(Node* head) {
    if (head == NULL) {
        printf("Daftar mahasiswa kosong.\n");
        return;
    }
    Node* temp = head;
    printf("Daftar Mahasiswa:\n");
    while (temp != NULL) {
        printf("Nama: %s, NPM: %d, IPK: %.2f\n", temp->name, temp->npm, temp->ipk);
        temp = temp->next;
    }
}

// Fungsi untuk menambahkan mahasiswa (provided)
void addStudent(Node** head, char* name, int npm, float ipk) {
    Node* newNode = createNode(name, npm, ipk);
    if (*head == NULL || (*head)->npm > npm) {
        newNode->next = *head;
        *head = newNode;
        return;
    }
    Node* current = *head;
    while (current->next != NULL && current->next->npm < npm) {
        current = current->next;
    }
    newNode->next = current->next;
    current->next = newNode;
}

// Fungsi untuk menghitung rata-rata IPK (TODO:1)
float calculateAverageGPA(Node* head);

// Fungsi untuk mencari mahasiswa berdasarkan NPM (TODO:2)
Node* searchStudent(Node* head, int npm);

// Fungsi untuk menghapus mahasiswa berdasarkan NPM (TODO:3)
void deleteStudent(Node** head, int npm);

// Fungsi untuk menghapus semua data mahasiswa (TODO:4)
void deleteAllStudents(Node** head);

// Fungsi utama (provided)
int main() {
    Node* head = NULL;
    int choice, npm;
    float ipk;
    char name[50];

    while (1) {
        printf("\nMenu:\n");
        printf("1. Tambah Mahasiswa\n");
        printf("2. Tampilkan Daftar Mahasiswa\n");
        printf("3. Cari Mahasiswa Berdasarkan NPM\n");
        printf("4. Hapus Mahasiswa Berdasarkan NPM\n");
        printf("5. Hitung Rata-rata IPK\n");
        printf("6. Hapus Semua Data Mahasiswa\n");
        printf("7. Keluar\n");
        printf("Pilihan: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Masukkan Nama: ");
                scanf(" %[^\n]", name);
                printf("Masukkan NPM: ");
                scanf("%d", &npm);
                printf("Masukkan IPK: ");
                scanf("%f", &ipk);
                addStudent(&head, name, npm, ipk);
                printf("Mahasiswa berhasil ditambahkan.\n");
                break;
            case 2:
                displayStudents(head);
                break;
            case 3:
                printf("Masukkan NPM untuk dicari: ");
                scanf("%d", &npm);
                Node* found = searchStudent(head, npm);
                if (found != NULL) {
                    printf("Mahasiswa ditemukan: Nama: %s, NPM: %d, IPK: %.2f\n", found->name, found->npm, found->ipk);
                } else {
                    printf("Mahasiswa dengan NPM %d tidak ditemukan.\n", npm);
                }
                break;
            case 4:
                printf("Masukkan NPM untuk dihapus: ");
                scanf("%d", &npm);
                deleteStudent(&head, npm);
                break;
            case 5:
                printf("Rata-rata IPK: %.2f\n", calculateAverageGPA(head));
                break;
            case 6:
                deleteAllStudents(&head);
                printf("Semua data mahasiswa telah dihapus.\n");
                break;
            case 7:
                deleteAllStudents(&head);
                printf("Keluar dari program.\n");
                return 0;
            default:
                printf("Pilihan tidak valid.\n");
        }
    }
}
```
### Spesifikasi Tugas
1. **Fungsi calculateAverageGPA (15%)**
    - Implementasikan fungsi untuk menghitung rata-rata IPK dari semua mahasiswa di dalam linked list.
    - Jika daftar mahasiswa kosong, maka kembalikan nilai 0.0 dan print pesan "Daftar mahasiswa kosong."
    - Jelaskan logikanya dengan menggunakan ilustrasi (boleh gambar, boleh text, dibebaskan asal memberikan visualisasi yang baik!)

2. **Fungsi searchStudent (15%)**
    - Implementasikan fungsi untuk mencari mahasiswa berdasarkan NPM.
    - Fungsi ini harus mengembalikan pointer ke node mahasiswa jika ditemukan. Jika tidak, maka kembalikan NULL dan print pesan "Mahasiswa dengan NPM <NPM> tidak ditemukan."
    - Jelaskan logikanya dengan menggunakan ilustrasi (boleh gambar, boleh text, dibebaskan asal memberikan visualisasi yang baik!)

3. **Fungsi deleteStudent (15%)**
    - Implementasikan fungsi untuk menghapus mahasiswa berdasarkan NPM.
    - Jika mahasiswa dengan NPM tertentu tidak ditemukan, print pesan "Mahasiswa dengan NPM <NPM> tidak ditemukan."
    - Jelaskan logikanya dengan menggunakan ilustrasi (boleh gambar, boleh text, dibebaskan asal memberikan visualisasi yang baik!)

#### Note! Perhatikan 3 cases di mana:
    - Node yang dihapus adalah node pertama (head).
    - Node yang dihapus berada di tengah linked list.
    - Node yang dihapus adalah node terakhir.

4. **Fungsi deleteAllStudents (15%)**
    - Implementasikan fungsi untuk menghapus seluruh mahasiswa dalam linked list.
    - Pastikan seluruh node dihapus dengan memanfaatkan `free()` function.
    - Setelah semua data dihapus, print pesan "Semua data mahasiswa telah dihapus."

