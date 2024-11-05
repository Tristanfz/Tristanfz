- 👋 Hi, I’m @Tristanfz
- 👀 I’m interested in programming
- 🌱 I’m currently learning basic programming
- 💞️ I’m looking to collaborate on college assignment
- 📫 How to reach me IG: @tristanfz_
- 😄 Pronouns: he/him
- ⚡ Fun fact: i like coffee

<!---
Tristanfz/Tristanfz is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

#include <stdio.h>
#include <string.h>

#define MAX_CHARACTERS 10

// Struct untuk manusia dan hewan peliharaan
typedef struct {
    char nama[20];
    int energy;
    int loves;
} Human;

typedef struct {
    char nama[20];
    int energy;
    int loves;
} Pet;

// Daftar karakter
Human humans[MAX_CHARACTERS];
Pet pets[MAX_CHARACTERS];
int humanCount = 0, petCount = 0;

// Fungsi untuk menambah karakter
void addHuman(char *nama, int energy, int loves) {
    strcpy(humans[humanCount].nama, nama);
    humans[humanCount].energy = energy;
    humans[humanCount].loves = loves;
    humanCount++;
}

void addPet(char *nama, int energy, int loves) {
    strcpy(pets[petCount].nama, nama);
    pets[petCount].energy = energy;
    pets[petCount].loves = loves;
    petCount++;
}

// Fungsi aktivitas "petting" untuk meningkatkan loves pada Pet
void petting(char *petName) {
    for (int i = 0; i < petCount; i++) {
        if (strcmp(pets[i].nama, petName) == 0) {
            pets[i].loves += 10;
            printf("You are gaining %s's loves\n", pets[i].nama);
            return;
        }
    }
    printf("Pet with name %s not found.\n", petName);
}

// Fungsi untuk menampilkan atribut karakter
void showAttributes(char *name) {
    for (int i = 0; i < humanCount; i++) {
        if (strcmp(humans[i].nama, name) == 0) {
            printf("%s's Energy is %d\n", humans[i].nama, humans[i].energy);
            printf("%s's Loves is %d\n", humans[i].nama, humans[i].loves);
            return;
        }
    }
    for (int i = 0; i < petCount; i++) {
        if (strcmp(pets[i].nama, name) == 0) {
            printf("%s's Energy is %d\n", pets[i].nama, pets[i].energy);
            printf("%s's Loves is %d\n", pets[i].nama, pets[i].loves);
            return;
        }
    }
    printf("Character with name %s not found.\n", name);
}

// Fungsi untuk mengurutkan dan menampilkan pet berdasarkan loves
void showSortedPetsByLoves() {
    for (int i = 0; i < petCount - 1; i++) {
        for (int j = i + 1; j < petCount; j++) {
            if (pets[i].loves < pets[j].loves) {
                Pet temp = pets[i];
                pets[i] = pets[j];
                pets[j] = temp;
            }
        }
    }
    printf("Pets sorted by loves:\n");
    for (int i = 0; i < petCount; i++) {
        printf("%s - Loves: %d\n", pets[i].nama, pets[i].loves);
    }
}

// Fungsi utama untuk menjalankan simulasi
void simulation() {
    char command[50], name[20];
    while (1) {
        printf("Enter command: ");
        scanf("%s %s", command, name);

        if (strcmp(command, "PETTING") == 0) {
            petting(name);
        } else if (strcmp(command, "ATTR") == 0) {
            showAttributes(name);
        } else if (strcmp(command, "SHOW") == 0 && strcmp(name, "CAPPYBARA") == 0) {
            showSortedPetsByLoves();
        } else if (strcmp(command, "EXIT") == 0) {
            break;
        } else {
            printf("Invalid command!\n");
        }
    }
}

// Fungsi main
int main() {
    // Tambahkan karakter default
    addHuman("Diana", 60, 80);
    addHuman("Yuki", 55, 90);
    addPet("Capy", 50, 90);
    addPet("Milos", 40, 70);
    addPet("Snowy", 45, 85);

    // Jalankan simulasi
    simulation();
    return 0;
}
