## challenge 1

```
#include <iostream>

using namespace std;

void main()
{
    string title = 
        "  ________    _         _                  _________    __  _________\n"
        " /_  __/ /_  (_)____   (_)____   ____ _   / ____/   |  /  |/  / ____/\n"
        "  / / / __ \\/ / ___/  / / ___/  / __ `/  / / __/ /| | / /|_/ / __/   \n"
        " / / / / / / (__  )  / (__  )  / /_/ /  / /_/ / ___ |/ /  / / /___   \n"
        "/_/ /_/ /_/_/____/  /_/____/   \\__,_/   \\____/_/  |_/_/  /_/_____/   \n";

    cout << title << endl;
    
}
```

i had to make sure to replace all backslashes with double-backslashes (i.e. escape character backslash). i used a multi-line string to keep it tidy.

## challenge 2
```
#include <iostream>
#include <string>

using namespace std;

void main()
{
    string name;
    string username;
    string clan_tag;
    int age;

    cout << "please enter your name: ";
    cin >> name;

    cout << "hello, " << name << "!" << endl;

    cout << "please enter your clan tag: ";
    cin >> clan_tag;

    cout << "please enter your username: ";
    cin >> username;

    cout << "please enter your age: ";
    string age_str;
    cin >> age_str;
    age = stoi(age_str);

    cout << "player details:" << endl;
    cout << "-------------------------------------------------" << endl;
    cout << "name       : " << name << endl;
    cout << "username   : [" << clan_tag << "]" << username << endl;
    cout << "age        : " << age << endl;
}
```

this is mostly just lots of `cout` and `cin`, the only issue i had was that I missed out the `<< endl` on a lot of lines initially, meaning the output would be all crushed onto one line.

## challenge 3
```
#include <iostream>
#include <string>

using namespace std;

void main()
{
    string num_str;
    cout << "enter a number to square: ";
    cin >> num_str;

    float num = stof(num_str);

    float sqr = num * num;
    cout << num << " squared is " << sqr;
}
```

simply getting input from the user with `cin`, nothing super difficult with this, just using the builtin `stof` method to get a float and squaring it, then outputting it again.

## challenge 4
```
#include <iostream>

using namespace std;

void main()
{
    string text;
    cout << "enter some text: ";
    cin >> text;

    int length = text.length();

    for (int i = 0; i < length + 4; i++)
        cout << "*";
    cout << endl;
    cout << "* " << text << " *" << endl;
    for (int i = 0; i < length + 4; i++)
        cout << "*";
}
```

this just gets the length of the input from the user and repeatedly outputs a star based on that (with spacing at the ends) for the first and last lines. bracketless for loops since they each contain only one line. then inserting the user's input between, with stars at each end to form the box.

## challenge 5
```
#include <iostream>
#include <cctype>
#include <string>

using namespace std;

string sentence_caps(string str)
{
	string output;
	bool capitalise_next = true;
	for (char c : str)
	{
		if (capitalise_next && c != ' ')
		{
			output += toupper(c);
			capitalise_next = false;
		}
		else
		{
			output += tolower(c);
			if (c == '.' || c == '!' || c == '?') capitalise_next = true;
		}
	}

	return output;
}

string all_upper(string str)
{
	string output;
	for (char c : str)
	{
		output += toupper(c);
	}
	return output;
}

string all_lower(string str)
{
	string output;
	for (char c : str)
	{
		output += tolower(c);
	}
	return output;
}

void main()
{
	cout << "enter some text: ";
	string text;
	getline(cin, text);

	cout << "Sentence case: " << sentence_caps(text) << endl;
	cout << "Lower case: " << all_lower(text) << endl;
	cout << "Upper case: " << all_upper(text) << endl;
}
```

i wrote three functions, one for capitalising the first letter of sentences, one for capitalising all letters, and one for lowercasing all letters. the only complex one is the first of these, which keeps track of whether the next character should be uppercase (this state is set when a '.' '!' or '?' is encountered) and will keep this state until it finds a alphabetical character (i.e. not a space) to capitalise.
i had one problem, which was that `cin >> text` will only pull the first word from the input from the user; i solved this by using `getline(cin, text)` instead.

## challenge 6
```
#include "main.h"

#include <string>

using namespace std;

void main()
{
    int target_number = random(1, 100);

    int num_guesses = 0;

    while (true)
    {
        num_guesses++;
        string str_guess;
        cout << "enter a guess: ";
        cin >> str_guess;
        int user_guess = stoi(str_guess);
        
        if (user_guess == target_number) break;
        else
        {
            int difference = abs(user_guess - target_number);
            if (difference >= 50) cout << "freezing";
            else if (difference >= 35) cout << "colder";
            else if (difference >= 25) cout << "cold";
            else if (difference >= 15) cout << "warm";
            else if (difference >= 10) cout << "warmer";
            else if (difference >= 5) cout << "hot";
            else if (difference >= 2) cout << "boiling";
            else cout << "super duper boiling";
            cout << endl;
        }
    }

    cout << "you got it! the number was " << target_number << endl;
    cout << "it took you " << num_guesses << " guesses" << endl;
}
```

i was somewhat unsure of what ranges should be labelled with "freezing", "colder", etc, since the challenge does not specify (it specifies exact points where "freezing" should be outputted). this meant i had to add an extra range for being less than 2 away from the target number, which i labelled "super duper boiling". the rest of the ranges are "freezing" if distance from target number is greater or equal to 50, "cold" if greater or equal to 25 but less than 50, etc.

