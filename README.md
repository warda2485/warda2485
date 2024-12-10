#include <stdio.h>
#include <stdlib.h>

// تعريف بنية العنصر في القائمة
typedef struct element {
    int val;
    struct element *suivant;
} element;

// إنشاء قائمة فارغة
element *creerListe() {
    return NULL;
}

// إضافة عنصر في بداية القائمة
element *ajouterEnDebut(element *liste, int valeur) {
    element *nouveau = (element*)malloc(sizeof(element));
    nouveau->val = valeur;
    nouveau->suivant = liste;
    return nouveau;
}

// ملء القائمة من جدول
element *chargerListe(int tab[], int taille, element *liste) {
    for (int i = taille - 1; i >= 0; i--) {
        liste = ajouterEnDebut(liste, tab[i]);
    }
    return liste;
}

// طباعة عناصر القائمة
void afficherListe(element *liste) {
    while (liste != NULL) {
        printf("%d -> ", liste->val);
        liste = liste->suivant;
    }
    printf("NULL\n");
}

// حذف العنصر الأخير
element *supprimerEnFin(element *liste) {
    if (liste == NULL || liste->suivant == NULL) {
        return NULL;
    }
    element *precedent = liste;
    while (precedent->suivant->suivant != NULL) {
        precedent = precedent->suivant;
    }
    free(precedent->suivant);
    precedent->suivant = NULL;
    return liste;
}

// تفريغ القائمة
void viderListe(element *liste) {
    while (liste != NULL) {
        element *temp = liste;
        liste = liste->suivant;
        free(temp);
    }
}

int main() {
    int tab[] = {1, 3, 5, 7, 8, 10, 9, 11, 13, 20};
    element *liste = creerListe();
    liste = chargerListe(tab, 10, liste);
    afficherListe(liste);

    element *L1 = supprimerEnFin(liste);
    afficherListe(L1);

    element *L2 = ajouterEnDebut(L1, 40);
    afficherListe(L2);

    viderListe(L2);

    return 0;
}
