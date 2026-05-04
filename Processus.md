# Fork :

La fonction `fork` permet de créer un nouveau processus enfant, voici comment l'utiliser :

```C
#include <sys/wait.h>
#include <unistd.h>

int main() {
	pid_t pid = fork();
	
	if (pid < 0) {
		return 1; // Erreur dans la création du processus enfant
	}
	
	if (pid == 0) {
		// Code executé par l'enfant
	} else {
		// Code du père
	}
	
	return 0;
}
```

`fork()` retourne 0 dans le processus nouvellement créé et le PID du processus créé dans le parent.

# Pipe :

La fonction Pipe permet de créer des flux d'entrée et de sortie utilisables pour communiquer entre deux processus.
Il faut lui passer un tableau d'entiers qui deviendront des files descriptor.
Le premier file descriptor `fd[0]` sera utilisé pour la lecture et le second `fd[1]` sera utilisé pour l'écriture.
Si on veut faire en sorte que chaque processus puisse envoyer et recevoir il faudra utiliser la fonction Pipe deux fois.
```C
#include <sys/wait.h>
#include <unistd.h>

int main() {

	int fd[2];
	if (pipe(fd) == -1) {
		return 1; // Erreur dans la création du Pipe
	}
	pid_t pid = fork();
	if (pid < 0) {
		return 1; // Erreur dans la création du Processus Fils
	}
	
	return 0;
}

```

Il ne faut pas oublier de close les files descriptor quand on en a plus besoin.