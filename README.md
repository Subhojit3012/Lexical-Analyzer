# Lexical-Analyzer
This project implements a lexical analyzer that scans source code and converts it into a sequence of tokens. It identifies lexemes such as keywords, identifiers, operators, and literals while ignoring whitespace and comments. The generated tokens serve as input for further compiler or interpreter phases.


#include <iostream>
#include <cctype>
#include <string>
#include <unordered_set>

using namespace std;

// List of keywords
unordered_set<string> keywords = {
    "int", "float", "double", "char", "if", "else",
    "for", "while", "return", "void"
};

bool isKeyword(const string& str) {
    return keywords.find(str) != keywords.end();
}

bool isOperator(char ch) {
    string operators = "+-*/=%";
    return operators.find(ch) != string::npos;
}

bool isSeparator(char ch) {
    string separators = "(),;{}";
    return separators.find(ch) != string::npos;
}

int main() {
    string input;
    cout << "Enter a line of code:\n";
    getline(cin, input);

    int i = 0;
    while (i < input.length()) {

        // Skip whitespace
        if (isspace(input[i])) {
            i++;
            continue;
        }

        // Identifier or Keyword
        if (isalpha(input[i]) || input[i] == '_') {
            string word;
            while (isalnum(input[i]) || input[i] == '_') {
                word += input[i++];
            }

            if (isKeyword(word))
                cout << word << " : Keyword\n";
            else
                cout << word << " : Identifier\n";
        }

        // Number
        else if (isdigit(input[i])) {
            string number;
            while (isdigit(input[i])) {
                number += input[i++];
            }
            cout << number << " : Number\n";
        }

        // Operator
        else if (isOperator(input[i])) {
            cout << input[i] << " : Operator\n";
            i++;
        }

        // Separator
        else if (isSeparator(input[i])) {
            cout << input[i] << " : Separator\n";
            i++;
        }

        // Unknown character
        else {
            cout << input[i] << " : Unknown\n";
            i++;
        }
    }

    return 0;
}
