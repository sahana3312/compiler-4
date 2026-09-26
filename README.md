# compiler-4
# Ex. No : 4	
# RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
## Register Number :212225040356
## Date : 05.09.26


## AIM   
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.

## PROGRAM
  ```
variable_test.l
%{
#include "y.tab.h"
%}

%%

"int"       { return INT; }
"float"     { return FLOAT; }
"double"    { return DOUBLE; }

[a-zA-Z]    { return LETTER; }
[0-9]       { return DIGIT; }

[ \t]       ; /* Ignore spaces and tabs */
\n          { return 0; }
.           { return yytext[0]; }

%%

int yywrap() {
    return 1;
}


variable_test.y

%{
#include <stdio.h>
#include <stdlib.h>

int yylex();
void yyerror(const char *s);
%}

%token LETTER DIGIT INT FLOAT DOUBLE

%%

/* Declaration rule */
D : T L ';' {
    printf("\nValid variable declaration statement.\n");
    return 0;
}
;

/* Data types */
T : INT 
  | FLOAT 
  | DOUBLE
  ;

/* List of variables */
L : L ',' ID
  | ID
  ;

/* Identifier grammar: Starts with LETTER, followed by letters/digits */
ID : LETTER REST
   ;

REST : REST LETTER
     | REST DIGIT
     | /* empty */
     ;

%%

void yyerror(const char *s) {
    printf("\nInvalid variable declaration / invalid identifier structure!\n");
}

int main() {
    printf("Enter variable declaration statement (e.g., int a, b1, val2;):\n");
    yyparse();
    return 0;
}


```

## OUTPUT 
<img width="1036" height="482" alt="image" src="https://github.com/user-attachments/assets/f78b0520-654e-41d4-905f-9b9f7b5451c3" />


## RESULT
A  YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.

