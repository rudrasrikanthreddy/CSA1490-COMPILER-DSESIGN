%%
[0-9]+ {printf("\nValid digit \n");} 
.* printf("\nInvalid digit\n");
%%
int yywrap(){}
int main()											
{
yylex();
return 0;
}
Output:
G:\lex>flex digit_or_not.l

G:\lex>gcc lex.yy.c

G:\lex>a.exe
23
Valid digit

h56
Invalid digit
