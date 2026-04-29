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