# Compter le nombre de caractère
```C
#include <stdio.h>  
  
int count_char(FILE *file) {    
	long size;  
	  
	fichier = fopen("file.txt", "r");  
	if (fichier == NULL) {  
		printf("Erreur lors de l'ouverture du fichier.\n");  
		return 1;  
	}  
	  
	// Aller à la fin du fichier  
	fseek(file, 0, SEEK_END);  
	  
	// Obtenir la position actuelle (taille du fichier)  
	taille = ftell(file);  
	  
	// Revenir au début du fichier  
	rewind(file); 
	
	printf("Nombre de caracteres : %ld\n", size);  
	  
	fclose(file);  
	return 0;  
}
```
# Compter le nombre de ligne
Ce code lit chaque caractère du fichier un par un et incrémente le compteur quand un saut de ligne est trouvé.
```C
int count_lines(FILE *file) {
	int count = 0;
	int c;
	
	while ((c = fgetc(file)) != EOF) {
		if (c == '\n')
		count++;
	}
	
	rewind(file);
	return count + 1; // +1 Pour la dernière ligne
}
```
