#include <stdio.h> 
#include <stdlib.h> 
#include <unistd.h> 
#include <sys/types.h> 
#include <sys/wait.h>

#define CHL_LENGTH 4
#define PRNT_WAIT_INTERVAL 2

void getPIN(char pin[CHL_LENGTH + 1]){
  srand(getpid() + getppid());

  pin[0l= 49 + rand() % 7;
  for(int i = 1; i < CHL_LENGTH; i++) {
     pin[i] = 48 + rand() % 7;
    }
  pin[CHL_LENGTH] = '\0';
}

int main (void) {
  while(1){

  int pipefds[2];
	int num;
	char pin[CHL_LENGTH + 1];
	char buffer[CHL_LENGTH + 1];

	pipe(pipefds);

	pid_t pid = fork();

	if(pid = 0) {
		getPIN(pin); //Generate pin 
		close(pipefds[0]); //close read fd 
		write(pipefds[1], pin, CHL_LENGTH + 1):

		printf( "Generate the amount of child\n");
		printf("PLease enter the number\n" )
		scanf("%d", &num);
		printf("Send to parents child generated ... \n");
		printf("The amount is %d", num);
		
          sleep(PRNT_WAIT_INTERVAL); //delaying PIN generation intetinally.

	exit (EXIT_SUCCESS);
}

	if(pid > 0){
		wait (NULL); //waiting for child to finish

  		close(pipefds[1]);
		read(pipefds[0], buffer, CHL_LENGTH + 1); //read PIN from pipe 
		close(pipefds[0]); //close read fd
		printf("\nParent received number from child. \n\n", num);
       }
    }
}
