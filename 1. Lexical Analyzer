#include <iostream>
#include <string>
#include <vector>

enum TokenType {
    INTEGER,
    PLUS,
    MINUS,
    MULTIPLY,
    DIVIDE,
    END
};

struct Token {
    TokenType type;
    std::string value;
};

class Lexer {
public:
    Lexer(const std::string& input) : input(input), position(0) {}

    Token getNextToken() {
        while (position < input.length()) {
            if (isspace(input[position])) {
                skipWhitespace();
                continue;
            }

            if (isdigit(input[position])) {
                return parseInteger();
            }

            if (input[position] == '+') {
                position++;
                return Token{PLUS, "+"};
            }

            if (input[position] == '-') {
                position++;
                return Token{MINUS, "-"};
            }

            if (input[position] == '*') {
                position++;
                return Token{MULTIPLY, "*"};
            }

            if (input[position] == '/') {
                position++;
                return Token{DIVIDE, "/"};
            }

            std::cerr << "Invalid character: " << input[position] << std::endl;
            exit(1);
        }

        return Token{END, ""};
    }

private:
    void skipWhitespace() {
        while (position < input.length() && isspace(input[position])) {
            position++;
        }
    }

    Token parseInteger() {
        std::string value;
        while (position < input.length() && isdigit(input[position])) {
            value += input[position];
            position++;
        }
        return Token{INTEGER, value};
    }

    std::string input;
    size_t position;
};

int main() {
    std::string input = "3 + 4 * 2 - 6 / 3";
    Lexer lexer(input);

    std::vector<Token> tokens;
    Token token = lexer.getNextToken();
    while (token.type != END) {
        tokens.push_back(token);
        token = lexer.getNextToken();
    }

    // Print the tokens
    for (const auto& token : tokens) {
        std::cout << "Token: Type = " << token.type << ", Value = " << token.value << std::endl;
    }

    return 0;
}
