# Ouvrir un fichier
Pour ouvrir un fichier on utilisera la fonction `fopen()` et on utilisera `fclose()` pour fermer le fichier.
```C
#include <stdio.h>

int main() {
	// Ouverture du fichier 'fichier' en mode read
	FILE *file = fopen("fichier", "r");
	fclose(file);
	return 0;
}
```

# Getline
La fonction `getline()` est très pratique car elle permet de lire une ligne entière sans avoir à s'occuper de la taille du buffer à allouer.
Si on passe un `lineptr = NULL` getline va l'allouer tout seul à la bonne taille et si lineptr n'est pas NULL et qu'il n'y a pas assez d'espace getline va le realloc tout seul. 
```C
#include <stdio.h>

// Lecture d'un fichier jusqu'a la fin

int main() {
	// Ouverture du fichier 'fichier' en mode read
	FILE *file = fopen("fichier", "r");
	char *lineptr = NULL;
	size_t size = 0;
	while (getline(&lineptr, &size, file) != -1) {
		printf("%s\n", lineptr);
		free(lineptr);
		lineptr = NULL;
	}
	free(lineptr);
	fclose(file);
	return 0;
}
```
Il ne faut pas oublier de `free(lineptr)` à la fin pour éviter les mémory leaks (même si getline échoue).