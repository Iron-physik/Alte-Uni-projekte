# Projects in C at the HSD School (2018-2019)

### HSD 01 - Uni ID to Pharma check number Converter | C
A basic programm to convert the Uni-ID into a phamaceutic-Check-Number (PZN in german).

#### Flowchart
```mermaid
flowchart TD
    A[Read 6 digits of Uni-ID] --> B[Convert chars to integers]
    B --> C[Multiply each digit by weight: 2, 3, 4, 5, 6, 7]
    C --> D[Sum the weighted values]
    D --> E[Modulo 11]
    E --> F[Modulo 10 to get check digit]
    F --> G[Print PZN: JOS-XXXXXX-C]
```

#### Code Snippet
```c
  zsum1 = (nummer1-'0')*2;
  zsum2 = (nummer2-'0')*3;
  zsum3 = (nummer3-'0')*4;
  zsum4 = (nummer4-'0')*5;
  zsum5 = (nummer5-'0')*6;
  zsum6 = (nummer6-'0')*7;
  
  summe = (zsum1+zsum2+zsum3+zsum4+zsum5+zsum6);
  mod11 = summe%11;
  pruef = mod11%10;
```

---

### HSD 02 - Calculator for natural Logarithm | C
A basic programm to calculate the natural Logarithm ln(x) using an iterative series approximation.

#### Flowchart
```mermaid
flowchart TD
    A[Read Number of Iterations 'n'] --> B{i <= n?}
    B -- Yes --> C[Read Float 'x']
    C --> D{x > 0?}
    D -- Yes --> E[Calculate Argument Series 'addende']
    D -- No --> F[Print Error]
    E --> G[Iterate and Accumulate Result]
    G --> H[Print Output]
    H --> B
    B -- No --> I[End]
```

#### Code Snippet
```c
  while((sumcount<789749%10000)&&((addende>=1.0/789749)||(addende<=-1.0/789749))){
    ergebnis=ergebnis+addende;
    sumcount=sumcount+1;
    minus=minus*(-1);
    potenz=potenz*reiargument;
    addende=minus*potenz/sumcount;
  }
```

---

### HSD 03 - Cafeteria Programm | C
This is a basic programm to search a Weekly Menu of a cafeteria based on the date and then calculate the price depending if the costumer is student, teacher or guest.

#### Flowchart
```mermaid
flowchart TD
    A[Initialize Structs with Menu Items] --> B[Read Matriculation Number]
    B --> C[Read Customer Role 'S', 'B', 'G']
    C --> D{Valid Role?}
    D -- Yes --> E[Nested Loop: Find Main Dish without 'S' Allergen]
    E --> F[Loop: Find 'GreenCorner' Item]
    F --> G[Extract Prices from Struct based on Role]
    G --> H[Calculate Total Price]
    H --> I[Print Order & Price]
    D -- No --> J[Print Error]
```

#### Code Snippet
```c
  /*Suchschleife: find valid main dish*/
  for (aussen=0; aussen<11; aussen++){
      for (innen=0;innen<10; innen++){
          if ((jahr_best[9].tageskarte[aussen].hauptgericht==1)&&(jahr_best[9].tageskarte[aussen].kennzeichnung[innen]!= 'S')){
              g_gericht = jahr_best[9].tageskarte[aussen];
          }
      }
  }

  /*preisberechnung*/
  if (pruefung == 'S') preiswahl = 0;
  if (pruefung == 'B') preiswahl = 1;
  if (pruefung == 'G') preiswahl = 2;
```

---

### HSD Bonus Task: Search machine for Pixels in a image and Hue calculation | C

This Project was the Final Bonus excercise in the 1 semester C course I visited at the HSD in Düsseldorf.
The Goal of the project was to create a programm that can display and find Pixel RGB values along the left, upper and right border of a image, mapping them to my Uni-ID: 789749.

#### Flowchart
```mermaid
flowchart TD
    A[Read 5x3 EPS Image] --> B[Load RGB Pixels into 3D Array]
    B --> C[Flash LEDs representing ID: 789749]
    C --> D[Loop through all Pixels]
    D --> E[Find Min/Max RGB & Delta]
    E --> F[Calculate Hue Angle]
    F --> G{Hue between 6 and 36?}
    G -- Yes --> H[Accumulate Skin Hue]
    G -- No --> I[Continue]
    H --> J[Calculate Average Skin Hue]
    J --> K[Print Average to LCD]
```

#### Code Snippet
```c
  cmin = r < g ? r : g; //minimale farbwert berechnung rgb
  cmin = cmin < b ? cmin : b;
  
  cmax = r > g ? r : g; //maximale farbwert berechnung rgb
  cmax = cmax > b ? cmax : b;
  
  delta = cmax - cmin; //unterschied cmin <-> cmax
  
  if (delta == 0) {
    hue = -1;
  }
  else {
    if ( r == cmax ) {
      tmp = ( (float)g - b ) / delta;
    } else if ( g == cmax ) {
      tmp = 2 + ( (float)b - r ) / delta;
    } else {
      tmp = 4 + ( (float)r - g ) / delta;
    }
    tmp *= 60; // Winkel in Grad
```
