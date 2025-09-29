#include <iostream>
#include <string>
#include <vector>
#include <cctype>

using namespace std;

// Mengecek apakah huruf adalah vokal
bool isVowel(char c) {
    c = tolower(c);
    return c == 'a' || c == 'i' || c == 'u' || c == 'e' || c == 'o';
}

vector<string> generateCandidates(string base, char firstChar) {
    vector<string> results;
    string vowels = "aeiou";

    for (char v1 : vowels) {
        for (char v2 : vowels) {
            for (char v3 : vowels) {
                string candidate = "";
                candidate += firstChar;
                candidate += base[0];
                candidate += v1;
                candidate += base[1];
                candidate += v2;
                candidate += base[2];
                candidate += v3;
                candidate += base[3];
                results.push_back(candidate);
            }
        }
    }
    return results;
}

int main() {
    string kode;
    cout << "Masukkan kode sandi: ";
    cin >> kode;

    if (kode.length() < 1) {
        cout << "Kode terlalu pendek untuk diproses." << endl;
        return 1;
    }

    string asciiStr = kode.substr(2, 2);
    int asciiCode = stoi(asciiStr);
    char firstChar = static_cast<char>(asciiCode);

    string left = kode.substr(0, 2);
    string right = kode.substr(4);
    string gabungan = left + right;


    string tanpaVokal = string(gabungan.rbegin(), gabungan.rend());


    cout << "\nHuruf pertama kata asli: " << firstChar << endl;
    cout << "Kata tanpa vokal: " << tanpaVokal << endl;
    cout << "\nKemungkinan kata asli:\n";

    vector<string> kemungkinan = generateCandidates(tanpaVokal, firstChar);
    for (const string& kata : kemungkinan) {
        cout << "- " << kata << endl;
    }

    return 0;
}
