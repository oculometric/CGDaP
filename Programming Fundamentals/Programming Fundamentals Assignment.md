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

simply getting input from the user with `cin`, nothing super difficult with this, just using the builtin `stof` function to get a float and squaring it, then outputting it again.

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

## challenge 7

```
#include <iostream>
#include <string>
#include <vector>

using namespace std;

const vector<string> character_classes = { "Samauri", "Archer", "Knight", "Wizard" };

struct character_details
{
    string name;
    int class_id;
};

void describe_character(character_details* player_character)
{
    cout << "Player details:" << endl;
    cout << "  Name  - " << player_character->name << endl;
    cout << "  Class - " << character_classes[player_character->class_id] << endl;
}

void main()
{   
    int character_class_index = -1;
    while (true)
    {
        cout << "Select a class from the list below, by entering its number: " << endl;
        for (int i = 0; i < character_classes.size(); i++)
            cout << i+1 << ": " << character_classes[i] << endl;
        cout << endl;
        cout << "> ";

        string str;
        cin >> str;
        character_class_index = stoi(str)-1;

        if (character_class_index >= character_classes.size() || character_class_index < 0)
        {
            cout << "Invalid selection. Please enter a choice between 1 and " << character_classes.size() << " inclusive." << endl;
        }
        else
        {
            cout << "You selected " << character_classes[character_class_index] << endl;
            break;
        }
    }

    cout << endl;

    cout << "Please enter your name: ";
    string name;
    cin.ignore();
    getline(cin, name);

    character_details* player_character = new character_details();
    player_character->name = name;
    player_character->class_id = character_class_index;

    cout << endl;

    describe_character(player_character);
}
```
i made use of a `vector<string>` for storing the character classes as this makes it easier to get its length (and thus easier to extend). i wrote a short dedicated function for displaying the character details for clarity. i used a simple `while` loop when inputting character class, which breaks when the player selects a valid class. when the player inputs their name, i wanted to make sure that the player could input a name in multiple parts (i.e. with a space in the middle) so i used `getline(cin, name)`. however, i initially had problems with this as it would appear to skip over without waiting for user input. with the help of stack overflow i discovered this is because `getline` was seeing the trailing newline from the user's previous input and deciding to stop reading characters (thus causing `name` to be blank); the solution to this was to add a `cin.ignore()` before `getline` to ignore the trailing whitespace. i used a pointer to my struct containing character data, rather than a simple object, since it might make it easier to pass the structure back and forwards to other functions (such as the `describe_character` function).

## challenge 8
```
#include <iostream>
#include <string>
#include <vector>

using namespace std;

struct inventory_slot
{
    int item_id = -1;
    string item_description = "Empty";
};

vector<string> item_descriptions = {"Sword", "Shield", "Bottle", "Golden Rune", "Gun", "Cobblestone"};

string item_description_for_id(unsigned int id)
{
    if (id >= item_descriptions.size()) return "";
    return item_descriptions[id];
}

vector<string> split_str(string str, char c)
{
    vector<string> result;
    size_t offset = 0;
    while (offset < str.length())
    {
        size_t next = str.find(c, offset);
        if (next == -1) next = str.length();
        string segment = str.substr(offset, next-offset);
        if (segment.length() > 0) result.push_back(segment);
        offset = next + 1;
    }
    return result;
}

class inventory_manager
{
private:
    vector<inventory_slot> inventory;

public:
    bool set_slot(unsigned int slot, unsigned int item_id)
    {
        if (slot >= inventory.size()) return false;

        inventory[slot].item_id = item_id;
        inventory[slot].item_description = item_description_for_id(item_id);

        return true;
    }

    bool clear_slot(unsigned int slot)
    {
        if (slot >= inventory.size()) return false;

        inventory[slot].item_id = -1;
        inventory[slot].item_description = "Empty";

        return true;
    }

    inventory_slot get_slot(unsigned int slot)
    {
        if (slot >= inventory.size()) return inventory_slot{ -2, "" };

        return inventory[slot];
    }

    void set_size(unsigned int size)
    {
        inventory.clear();
        for (int i = 0; i < size; i++)
            inventory.push_back(inventory_slot());
    }

    int get_size()
    {
        return inventory.size();
    }
};

void main()
{
    inventory_manager im;

    string result;
    int inventory_size = -1;

    while (true)
    {
        cout << "Enter the size of the inventory: ";
        cin >> result;
        try
        {
            inventory_size = stoi(result);
        }
        catch (exception e)
        {
            cout << "Enter a number for the inventory size." << endl << endl;
            continue;
        }
        if (inventory_size > 0) break;
        else cout << "The inventory must have at least 1 slot." << endl << endl;
    }

    im.set_size((unsigned int)inventory_size);
    cout << "Inventory initialised with " << inventory_size << " slots." << endl << endl;

    bool continue_mainloop = true;
    cin.ignore();
    while (continue_mainloop)
    {
        string command;
        while (command.size() < 1)
        {
            cout << "> ";
            getline(cin, command);
        }
        cout << endl;

        vector<string> split_command = split_str(command, ' ');

        if (split_command.size() == 0)
        {
            cout << "Enter a command." << endl << endl;
            continue;
        }

        if (split_command[0] == "view")
        {
            if (split_command.size() < 2)
            {
                cout << "'view' needs an argument: view <slot to view>" << endl << endl;
                continue;
            }

            int slot_to_view = stoi(split_command[1]);
            if (slot_to_view < 0)
            {
                cout << "Slot to view must be an index in the inventory." << endl << endl;
                continue;
            }
            inventory_slot slot_data = im.get_slot((unsigned int)slot_to_view);
            if (slot_data.item_id == -2)
            {
                cout << "Slot to view must be an index in the inventory." << endl << endl;
                continue;
            }
            cout << "Inventory slot " << slot_to_view << " information:" << endl;
            cout << "  Contents: " << slot_data.item_description << endl << endl;
        }
        else if (split_command[0] == "show_all")
        {
            cout << "Inventory:" << endl;
            for (int i = 0; i < im.get_size(); i++)
            {
                cout << "  Slot " << i << ": " << im.get_slot(i).item_description << endl;
            }
            cout << endl;
        }
        else if (split_command[0] == "set")
        {
            if (split_command.size() < 3)
            {
                cout << "'set' needs two arguments: set <slot to set> <item id>" << endl << endl;
                continue;
            }
            int slot_to_set = stoi(split_command[1]);
            if (slot_to_set < 0)
            {
                cout << "Slot to set must be an index in the inventory." << endl << endl;
                continue;
            }
            int item_id = stoi(split_command[2]);
            if (item_id < 0 || item_id >= item_descriptions.size())
            {
                cout << "Item ID must be within the list of valid item IDs." << endl << endl;
                continue;
            }
            bool result = im.set_slot(slot_to_set, item_id);
            if (!result)
            {
                cout << "Slot to view must be an index in the inventory." << endl << endl;
                continue;
            }
        }
        else if (split_command[0] == "items")
        {
            for (int i = 0; i < item_descriptions.size(); i++)
            {
                cout << "  " << i << ": " << item_description_for_id(i) << endl;
            }
            cout << endl;
        }
        else if (split_command[0] == "exit")
        {
            continue_mainloop = false;
        }
        else
        {
            cout << "Enter a valid command." << endl << endl;
        }
    }
}
```
i wrapped my list of inventory slots in a class in order to make managing it cleaner. the actual `vector` holding the inventory slots is private, and the class simply exposes methods with appropriate input validation to the rest of the program. once the inventory size is configured, the program enters a main loop, containing the command processing code. i wrote a simple function to split a string at a delimiting character, abstracting away the splitting of the user's input (e.g. `set 3 6`) into its constituent parts (`set`, `3`, `6`). throughout the command processing code, there is input validation, checking if the command has been given the right number of arguments, checking if those arguments are in range, and responding accordingly (before continuing to the start of the loop again to get fresh user input). i tested my input validation with a variety of different inputs, (valid, invalid, and edge case).

## challenge 9
``` main.h
#include <cmath>

class Vector2
{
public:
	float x, y;

	float magnitude();
	float distance(Vector2);

	Vector2(float, float);
};

Vector2 operator+(Vector2 a, Vector2 b) { return Vector2(a.x + b.x, a.y + b.y); }
Vector2 operator-(Vector2 a, Vector2 b) { return Vector2(a.x - b.x, a.y - b.y); }
Vector2 operator*(Vector2 a, Vector2 b) { return Vector2(a.x * b.x, a.y * b.y); }
Vector2 operator/(Vector2 a, Vector2 b) { return Vector2(a.x / b.x, a.y / b.y); }
Vector2 operator*(Vector2 a, float scalar) { return Vector2(a.x * scalar, a.y * scalar); }
Vector2 operator/(Vector2 a, float scalar) { return Vector2(a.x / scalar, a.y / scalar); }

ostream& operator<<(ostream& stream, Vector2 v)
{
	stream << "(" << v.x << ", " << v.y << ")";
	return stream;
}


float Vector2::magnitude()
{
	return sqrt((x * x) + (y * y));
}

float Vector2::distance(Vector2 other)
{
	return (other - *this).magnitude();
}

Vector2::Vector2(float _x, float _y)
{
	x = _x;
	y = _y;
}

float GetDistanceBetweenPoints(Vector2 a, Vector2 b)
{
	return a.distance(b);
}
```

``` main.cpp
#include <iostream>

using namespace std;

#include "main.h"

void main()
{
    float xComponents[2] = { 0.0f, 0.0f };
    float yComponents[2] = { 0.0f, 0.0f };

    for(int i = 0; i < 2; i++)
    {
        cout << "Please enter the X component of vector " << (i + 1) << ": ";
        cin >> xComponents[i];

        cout << "Please enter the Y component of vector " << (i + 1) << ": ";
        cin >> yComponents[i];

        cout << std::endl;
    }

    Vector2 v_a = Vector2(xComponents[0], yComponents[0]);
    Vector2 v_b = Vector2(xComponents[1], yComponents[1]);

    cout << "The distance between " << v_a << " and " << v_b << " is " << GetDistanceBetweenPoints(v_a, v_b) << endl;
    
}
```
i decided to write operator overrides for the main four (+ - * /) for my `Vector2` class. this enabled my methods to use simpler looking maths. i wrote two methods inside the class, `float magnitude()` which returns the magnitude of the instance, and `float distance(Vector2 other)` which subtracts `other` from the self instance (resulting in the vector from `other` to `this`), and returning the magnitude of this. i did this because it's nicer to have methods embedded in a class like this, but i wrapped this in the `float GetDistanceBetweenPoints(Vector2 a, Vector2 b)` function as instructed. declaring operators required the `Vector2` class and its properties to be defined, however it's methods use the operators, creating a dependency loop. to solve this, i first wrote a minimal class definition with the method stubs and fields, then the operators, then finally the implementations of the `Vector2` methods.

## challenge 10
