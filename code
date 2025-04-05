#include <iostream>
#include <string>
#include <vector>
#include <cctype>

using namespace std;

// Define reserved keywords
vector<string> keywords = {"int", "if", "return", "for", "float", "double"};

// Check if the word is a reserved keyword
bool isKeyword(const string& word) {
    for (const auto& k : keywords) {
        if (word == k) return true;
    }
    return false;
}

// Display the token
void printToken(const string& value, const string& type) {
    cout << "<" << value << ", " << type << ">\n";
}

// Analyze the source code
void lexicalAnalyze(const string& code) {
    size_t i = 0;
    while (i < code.length()) {
        char ch = code[i];

        // Skip whitespace
        if (isspace(ch)) {
            i++;
            continue;
        }

        // Identifiers or Keywords
        if (isalpha(ch)) {
            string word;
            while (i < code.length() && (isalnum(code[i]) || code[i] == '_')) {
                word += code[i++];
            }
            if (isKeyword(word))
                printToken(word, "KEYWORD");
            else
                printToken(word, "IDENTIFIER");
            continue;
        }

        // Integer or Floating numbers
        if (isdigit(ch)) {
            string number;
            bool isFloat = false;
            while (i < code.length() && (isdigit(code[i]) || code[i] == '.')) {
                if (code[i] == '.') isFloat = true;
                number += code[i++];
            }
            printToken(number, isFloat ? "FLOAT" : "NUMBER");
            continue;
        }

        // Repeated operators (e.g., ++, --)
        if ((ch == '+' || ch == '-') && i + 1 < code.length() && code[i + 1] == ch) {
            printToken(string(2, ch), "OPERATOR");
            i += 2;
            continue;
        }

        // Single-character operators
        if (ch == '+' || ch == '-' || ch == '=' || ch == '<') {
            printToken(string(1, ch), "OPERATOR");
            i++;
            continue;
        }

        // Separators and Brackets
        if (ch == '(' || ch == ')' || ch == '{' || ch == '}' || ch == ';') {
            printToken(string(1, ch), "SEPARATOR");
            i++;
            continue;
        }

        // Unknown token
        printToken(string(1, ch), "UNKNOWN");
        i++;
    }
}

int main() {
    string code = "float pi = 3.14; for (int i = 0; i < 10; i++) { pi = pi + 1.0; } return pi;";
    lexicalAnalyze(code);
    return 0;
}
