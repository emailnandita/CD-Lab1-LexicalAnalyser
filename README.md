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
