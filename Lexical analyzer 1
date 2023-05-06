#include <stdio.h>
#include <ctype.h>
#include <string.h>

#define MAX_IDENT_LENGTH 32

typedef enum {
    IDENTIFIER,
    CONSTANT,
    OPERATOR,
    UNKNOWN
} token_type;

typedef struct {
    token_type type;
    char value[MAX_IDENT_LENGTH + 1];
} token;

int is_operator(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/' || c == '%' || c == '=' || c == '<' || c == '>' || c == '&' || c == '|' || c == '!';
}

token get_token() {
    char c, lookahead;
    token t = { UNKNOWN, "" };
    int length = 0;

    while ((c = getchar()) != EOF) {
        if (isspace(c)) {
            // Ignore whitespace
            continue;
        } else if (c == '/') {
            // Check for comment
            lookahead = getchar();
            if (lookahead == '/') {
                while ((c = getchar()) != EOF && c != '\n') {
                    // Ignore single-line comment
                }
                continue;
            } else {
                // Not a comment, put back the lookahead
                ungetc(lookahead, stdin);
            }
        }

        if (isalpha(c)) {
            // Identifier
            t.type = IDENTIFIER;
            t.value[length++] = c;
            while ((c = getchar()) != EOF && (isalnum(c) || c == '_') && length < MAX_IDENT_LENGTH) {
                t.value[length++] = c;
            }
            t.value[length] = '\0';
            ungetc(c, stdin);
            break;
        } else if (isdigit(c)) {
            // Constant
            t.type = CONSTANT;
            t.value[length++] = c;
            while ((c = getchar()) != EOF && isdigit(c) && length < MAX_IDENT_LENGTH) {
                t.value[length++] = c;
            }
            t.value[length] = '\0';
            ungetc(c, stdin);
            break;
        } else if (is_operator(c)) {
            // Operator
            t.type = OPERATOR;
            t.value[length++] = c;
            if (c == '<' || c == '>' || c == '=' || c == '!') {
                // Check for two-character operators
                lookahead = getchar();
                if ((lookahead == '=' && c != '!') || (lookahead == '>' && c == '<')) {
                    t.value[length++] = lookahead;
                } else {
                    ungetc(lookahead, stdin);
                }
            }
            t.value[length] = '\0';
            break;
        } else {
            // Unknown token
            t.type = UNKNOWN;
            t.value[0] = c;
            t.value[1] = '\0';
            break;
        }
    }

    return t;
}

int main() {
    token t;

    while ((t = get_token()).type != UNKNOWN) {
        printf("%s: %s\n", t.type == IDENTIFIER ? "Identifier" : t.type == CONSTANT ? "Constant" : "Operator", t.value);
    }

    return 0;
}
