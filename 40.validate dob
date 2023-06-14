%%
((0[1-9])|([1-2][0-9])|(3[0-1]))\/((0[1-9])|(1[0-2]))\/(19[0-9]{2}|2[0-9]{3}) printf("Valid DoB");
.* printf("Invalid DoB");
%%

int main()
{
 yylex();
 return 0;
}
int yywrap()
{}

Output:

G:\lex>flex dob.l

G:\lex>gcc lex.yy.c

G:\lex>a.exe
26/07/1995
Valid DoB


13\2\96
Invalid DoB
