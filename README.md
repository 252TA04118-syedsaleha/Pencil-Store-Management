#include <stdio.h>
#include <string.h>

#define MAX_PENCILS 100

struct Pencil {
    int id;
    char brand[30];
    char name[40];
    char type[30];
    char color[20];
    char hardness[10];
    float price;
    int quantity;
    int sold;
};

struct Pencil pencils[MAX_PENCILS];
int pencilCount = 0;


/* Add pencil */
void addPencil() {

    if (pencilCount >= MAX_PENCILS) {
        printf("\nPencil storage is full!\n");
        return;
    }

    printf("\n========== ADD PENCIL ==========\n");

    printf("Enter Pencil ID: ");
    scanf("%d", &pencils[pencilCount].id);

    printf("Enter Brand: ");
    scanf(" %[^\n]", pencils[pencilCount].brand);

    printf("Enter Pencil Name: ");
    scanf(" %[^\n]", pencils[pencilCount].name);

    printf("Enter Pencil Type: ");
    scanf(" %[^\n]", pencils[pencilCount].type);

    printf("Enter Color: ");
    scanf(" %[^\n]", pencils[pencilCount].color);

    printf("Enter Hardness (HB/2B/4B/etc.): ");
    scanf("%s", pencils[pencilCount].hardness);

    printf("Enter Price: ");
    scanf("%f", &pencils[pencilCount].price);

    printf("Enter Quantity: ");
    scanf("%d", &pencils[pencilCount].quantity);

    pencils[pencilCount].sold = 0;

    pencilCount++;

    printf("\nPencil added successfully!\n");
}


/* Display one pencil */
void displayPencil(struct Pencil p) {

    printf("\n----------------------------------------\n");
    printf("Pencil ID : %d\n", p.id);
    printf("Brand     : %s\n", p.brand);
    printf("Name      : %s\n", p.name);
    printf("Type      : %s\n", p.type);
    printf("Color     : %s\n", p.color);
    printf("Hardness  : %s\n", p.hardness);
    printf("Price     : %.2f\n", p.price);
    printf("Stock     : %d\n", p.quantity);
    printf("Sold      : %d\n", p.sold);
}


/* Display all pencils */
void displayPencils() {

    int i;

    if (pencilCount == 0) {
        printf("\nNo pencil records available.\n");
        return;
    }

    printf("\n========== ALL PENCILS ==========\n");

    for (i = 0; i < pencilCount; i++) {
        displayPencil(pencils[i]);
    }
}


/* Search pencil by ID */
void searchPencil() {

    int id;
    int i;
    int found = 0;

    printf("\nEnter Pencil ID: ");
    scanf("%d", &id);

    for (i = 0; i < pencilCount; i++) {

        if (pencils[i].id == id) {

            printf("\n========== PENCIL FOUND ==========\n");
            displayPencil(pencils[i]);

            found = 1;
            break;
        }
    }

    if (!found) {
        printf("\nPencil not found!\n");
    }
}


/* Search pencil by brand */
void searchByBrand() {

    char brand[30];
    int i;
    int found = 0;

    printf("\nEnter Brand: ");
    scanf(" %[^\n]", brand);

    printf("\n========== BRAND SEARCH ==========\n");

    for (i = 0; i < pencilCount; i++) {

        if (strcmp(pencils[i].brand, brand) == 0) {

            displayPencil(pencils[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo pencils found for this brand.\n");
    }
}


/* Search by pencil type */
void searchByType() {

    char type[30];
    int i;
    int found = 0;

    printf("\nEnter Pencil Type: ");
    scanf(" %[^\n]", type);

    printf("\n========== TYPE SEARCH ==========\n");

    for (i = 0; i < pencilCount; i++) {

        if (strcmp(pencils[i].type, type) == 0) {

            displayPencil(pencils[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo pencils found of this type.\n");
    }
}


/* Search by hardness */
void searchByHardness() {

    char hardness[10];
    int i;
    int found = 0;

    printf("\nEnter Hardness (HB/2B/4B/etc.): ");
    scanf("%s", hardness);

    printf("\n========== HARDNESS SEARCH ==========\n");

    for (i = 0; i < pencilCount; i++) {

        if (strcmp(pencils[i].hardness, hardness) == 0) {

            displayPencil(pencils[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo pencils found with this hardness.\n");
    }
}


/* Search by price range */
void priceRange() {

    float minPrice, maxPrice;
    int i;
    int found = 0;

    printf("\nEnter Minimum Price: ");
    scanf("%f", &minPrice);

    printf("Enter Maximum Price: ");
    scanf("%f", &maxPrice);

    printf("\n========== PRICE RANGE ==========\n");

    for (i = 0; i < pencilCount; i++) {

        if (pencils[i].price >= minPrice &&
            pencils[i].price <= maxPrice) {

            displayPencil(pencils[i]);
            found = 1;
        }
    }

    if (!found) {
        printf("\nNo pencils found in this price range.\n");
    }
}


/* Find cheapest pencil */
void cheapestPencil() {

    int i;
    int cheap;

    if (pencilCount == 0) {
        printf("\nNo pencil records available.\n");
        return;
    }

    cheap = 0;

    for (i = 1; i < pencilCount; i++) {

        if (pencils[i].price < pencils[cheap].price) {
            cheap = i;
        }
    }

    printf("\n========== CHEAPEST PENCIL ==========\n");
    displayPencil(pencils[cheap]);
}


/* Find most expensive pencil */
void expensivePencil() {

    int i;
    int expensive;

    if (pencilCount == 0) {
        printf("\nNo pencil records available.\n");
        return;
    }

    expensive = 0;

    for (i = 1; i < pencilCount; i++) {

        if (pencils[i].price > pencils[expensive].price) {
            expensive = i;
        }
    }

    printf("\n========== MOST EXPENSIVE PENCIL ==========\n");
    displayPencil(pencils[expensive]);
}


/* Sell pencil */
void sellPencil() {

    int id;
    int amount;
    int i;
    int found = 0;

    printf("\nEnter Pencil ID: ");
    scanf("%d", &id);

    for (i = 0; i < pencilCount; i++) {

        if (pencils[i].id == id) {

            found = 1;

            printf("Enter Quantity to Sell: ");
            scanf("%d", &amount);

            if (amount <= 0) {
                printf("\nInvalid quantity!\n");
            }
            else if (amount > pencils[i].quantity) {
                printf("\nInsufficient stock!\n");
            }
            else {

                pencils[i].quantity -= amount;
                pencils[i].sold += amount;

                printf("\nSale completed successfully!\n");
                printf("Total Amount: %.2f\n",
                       amount * pencils[i].price);
            }

            break;
        }
    }

    if (!found) {
        printf("\nPencil not found!\n");
    }
}


/* Display low stock */
void lowStock() {

    int i;
    int found = 0;

    printf("\n========== LOW STOCK PENCILS ==========\n");

    for (i = 0; i < pencilCount; i++) {

        if (pencils[i].quantity <= 5) {

            printf("\nID       : %d", pencils[i].id);
            printf("\nBrand    : %s", pencils[i].brand);
            printf("\nName     : %s", pencils[i].name);
            printf("\nQuantity : %d\n", pencils[i].quantity);

            found = 1;
        }
    }

    if (!found) {
        printf("\nNo low-stock pencils found.\n");
    }
}


/* Calculate inventory value */
void inventoryValue() {

    int i;
    float total = 0;

    if (pencilCount == 0) {
        printf("\nNo pencil records available.\n");
        return;
    }

    for (i = 0; i < pencilCount; i++) {
        total += pencils[i].price *
                 pencils[i].quantity;
    }

    printf("\n========== INVENTORY VALUE ==========\n");
    printf("Total Inventory Value: %.2f\n", total);
}


/*
