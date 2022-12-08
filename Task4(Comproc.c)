#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>
#include <pwd.h>
#include <string.h>
#include <stdlib.h>
#include <getopt.h>

int main(int argc, char **argv){
	char *login = getlogin();
	char buffer[127];
	char *close = "stop\n";
	char *str;
	int flag = 1;

	struct passwd *userinfo;
	uid_t userid = getuid();

	const char *short_options = "hb:";

	const struct option long_options[] = {
		{"help", 0, NULL, 'h'},
		{"buffer", 1, NULL, 'b'},
		{NULL, 0, NULL, 0}
	};
	int res;
	int option_index;

	while ((res = getopt_long(argc, argv, short_options, long_options, &option_index)) != -1){
		switch(res){
			case 'h': 
				printf("-b или --buffer задает значение буфера. Команда stopp останавливает работу программы.\n");
				break;
			case 'b':
				printf("Выбран размер буфера: %d\n", atoi(optarg));
				buffer[atoi(optarg)];
				break;
			case '?': default: {
				printf("Неизвестная команда...\n");				
				break;
			};			
		}
	}

	userinfo = getpwuid(userid);
	if (userinfo != NULL){
		printf("User: %s \n", userinfo -> pw_gecos);	
	}

	while (flag != 0){
		printf("%s$ ", login);
		fgets(buffer, sizeof(buffer), stdin);
		if (strncmp(buffer, close, strlen(buffer))  == 0){
			flag = 0;
			for (int i = 3; i > 0; i--){
				printf("Wait %d seconds...\n", i);
				sleep(1);
			}
			system("clear");
		}else{
			system(buffer);
		}
	}
	return 0;
}
