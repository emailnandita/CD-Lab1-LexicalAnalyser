# CD-Lab1-LexicalAnalyser
CompilerDesign Lab1(Detect Token For Lexical Analyser)
#include <stdio.h>
#include <stdbool.h>
#include <string.h>
#include <stdlib.h>




bool isDelimeter(char* ch){
      if(ch[0]==',' || ch[0]==';' || ch[0]=='{' || ch[0]=='('){
        return true;
    }else{
        return false;
    }
}

bool isOperator(char* ch){
    if(ch[0] == '+' || ch[0] == '-' || ch[0] == '*' || ch[0] == '*')
    return(true);
    
    return(false);
    
}

bool isIdentifier(char* str, int size){
    for(int i = 0; i< size; i++){
         if(65<=(int)str[i] && str[i] <=90 || 97<=(int)str[i] && str[i]<=122){
          
          return true;
      }
      else{
        return false;
    }
    }
    
}

    
    
   

bool isKeyword(char* str){
    if(!strcmp(str, "if") || !strcmp(str, "else") || !strcmp(str, "float") || !strcmp(str, "double") || !strcmp(str, "int"))
    return(true);                               
    return(false);
}

bool isInteger(char* str){
    int i, len = strlen(str);
    if (len == 0)
    return(false);
    
    for (i = 0; i < len; i++) {
		if (str[i] != '0' && str[i] != '1' && str[i] != '2'
			&& str[i] != '3' && str[i] != '4' && str[i] != '5'
			&& str[i] != '6' && str[i] != '7' && str[i] != '8'
			&& str[i] != '9' || (str[i] == '-' && i > 0))
			return (false);
	}
	return (true);
}

bool isRealNo(char* str){
    int i, len = strlen(str);
    bool hasDecimal = false;
    
    if(len == 0)
    return(false);
    
    	for (i = 0; i < len; i++) {
		if (str[i] != '0' && str[i] != '1' && str[i] != '2'
			&& str[i] != '3' && str[i] != '4' && str[i] != '5'
			&& str[i] != '6' && str[i] != '7' && str[i] != '8'
			&& str[i] != '9' && str[i] != '.' || 
			(str[i] == '-' && i > 0))
			return (false);
		if (str[i] == '.')
			hasDecimal = true;
	}
	return (hasDecimal);
}

    
    


int main()
{
    
    char str[] = {'1'};
    int size=3;

 	printf("%d\n",isKeyword(str));
 	printf("%d\n",isDelimeter(str));
 	printf("%d\n",isOperator(str));
 	printf("%d\n",isIdentifier(str,size));
 	printf("%d\n",isInteger(str));
 	printf("%d\n",isRealNo(str));
 	
}



# LexicalAnalyser:
#include <stdio.h>
#include <string.h>

int array(char* a){
    int count = 1;
    for(int i = 1; i <= sizeof(a); i++){
        if(a[i] == ';'){
            count++;
        }
    }
    printf("No. of lines: %d\n",count);
}
int word(char * a){
    int count = 1;
    for(int i =1; i <= sizeof(a);i++){
        if(a[i] == ' ' || a[i] == ',' || a[i] == ';'){
            count++;
        }
    }
    printf("No. of words: %d\n",count);
}
int d(char * a){
	int count = 1;
	for(int i=1; i <= sizeof(a);i++){
		if(a[i] == ';' || a[i] == ','){
			count++;
		}
		
	}
	printf("No.of delimeters: %d\n",count);
}
int op(char * a){
	int count  =1;
	for(int i=1; i< sizeof(a); i++){
		if(a[i] == '+' || a[i] == '-' || a[i] == '*' || a[i] == '/'){
			count++;
		}
	}
	printf("No. of operators is: %d\n",count);
}

int keyword(char * str ){
	int count = 1;
	for(int i=1 ; i<sizeof(str); i++){
		  if(!strcmp(str , "if") || !strcmp(str, "else") || !strcmp(str, "float") || !strcmp(str, "double") || !strcmp(str, "int")){
		  
		  
	
			count++;
		}
	}
	
	printf("No. of keyword is %d\n",count);
	
}

int main()
{
    int n;
    printf("Enter the size of array: ");
    scanf("%d",&n);
    char arr[n];
    for(int i = 0; i < n;i++){
        scanf("%c",&arr[i]);
    }
    array(arr);
    word(arr);
    d(arr);
    op(arr);
    keyword(arr);

    return 0;
}

//Lab Checking for recursive descent parser for String "ab$";
#include <stdio.h>
#include <string.h>

char l[100];
int i = 0;

void S();

int main()
{
    char s[100] = "ab$";
    strcpy(l,s);
    S();
    if(l[i]=='$'){
        printf("Success\n");
    }else{
        printf("Not Successfull\n");
    }

    return 0;
}

void S(){
    if(l[i]=='a'){
        printf("a\n");
        i++;
        S();
    }else if(l[i]=='b'){
        printf("b\n");
        i++;
    }
    return;
}

//Lab Checking for recursive descent parser for String "id+id*id$"; 
#include <stdio.h>
#include <string.h>
char l[100];
int i = 0;

void E();
void EI();
void T();
void TI();
void F();

int main()
{
    char s[100] = "id+id*id$";
    strcpy(l,s);
    E();
    if(l[i]=='$'){
        printf("Success\n");
    }else{
        printf("Not Successfull\n");
    }

    return 0;
}

void E(){
    T();
    EI();
}

void EI(){
    if (l[i]=='+'){
        i++;
        T();
        EI();
    }else{
        return;
    }
}

void T(){
    F();
    TI();
}

void TI(){
    if (l[i]=='*'){
        i++;
        F();
        TI();
    }else{
        return;
    }
}

void F(){
    if (l[i]=='('){
        E();
        if (l[i]==')'){
            i++;
        }
    }else if(l[i]=='i'){
        i++;
        i++;
    }
}



