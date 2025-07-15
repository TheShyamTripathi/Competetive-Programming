### Leetcode 557. Reverse Words in a String III [https://leetcode.com/problems/reverse-words-in-a-string-iii/]

```cpp
#include <sstream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    string reverseWords(string s) {
        // Create an input string stream from the input string `s`
        istringstream stream(s);

        // Vector to store each word extracted from the stream
        vector<string> words;
        string word;

        // Extract words from the stream using whitespace as a delimiter
        while (stream >> word) {
            words.push_back(word);
        }

        // Output string stream to build the final reversed-words string
        ostringstream revWords;

        // Iterate through each word
        for (size_t i = 0; i < words.size(); ++i) {
            // Reverse the current word in place
            reverse(words[i].begin(), words[i].end());

            // Append the reversed word to the output stream
            revWords << words[i];

            // Add a space after the word if it is not the last word
            if (i != words.size() - 1) {
                revWords << " ";
            }
        }

        // Convert the output stream to a string and return it
        string revWord = revWords.str();
        return revWord;
    }
};
```

---

### 🧠 Summary of what this code does:

* Splits the input string into individual words.
* Reverses each word **individually**.
* Rejoins the reversed words with a space.
* Returns the final string.

If you’d like to **also reverse the order of the words** (not just the characters), I can help you modify the code for that too.
