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

    // first line of stars
    for (int i = 0; i < length + 4; i++) cout << "*";
    cout << endl;

    // text
    cout << "* " << text << " *" << endl;

    // second line of stars
    for (int i = 0; i < length + 4; i++) cout << "*";
}
```

this just gets the length of the input from the user and repeatedly outputs a star based on that (with spacing at the ends) for the first and last lines. bracketless for loops since they each contain only one line. then inserting the user's input between, with stars at each end to form the box.

## challenge 5
```
#include <iostream>
#include <cctype>
#include <string>

using namespace std;

// capitalise the next text character of a sentence after a sentence end
string sentence_caps(string str)
{
	string output;
	bool capitalise_next = true;
	for (char c : str)
	{
		if (capitalise_next && c != ' ')
		{
			// capitalise this character, clear flag
			output += toupper(c);
			capitalise_next = false;
		}
		else
		{
			// decapitalise this character
			output += tolower(c);

			// if at the end of a sentence, set capitalise flag
			if (c == '.' || c == '!' || c == '?') capitalise_next = true;
		}
	}

	return output;
}

// capitalise whole string, char by char
string all_upper(string str)
{
	string output;
	for (char c : str)
	{
		output += toupper(c);
	}
	return output;
}

// decapitalise whole string, char by char
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
    // pick the number
    int target_number = random(1, 100);

    int num_guesses = 0;

    while (true)
    {
        // get input from user
        num_guesses++;
        string str_guess;
        cout << "enter a guess: ";
        cin >> str_guess;
        int user_guess = stoi(str_guess);
        
        if (user_guess == target_number) break;
        else
        {
            // respond based on how far away the user is
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

    // tell the player they won
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

// define the possible classes of character
const vector<string> character_classes = { "Samauri", "Archer", "Knight", "Wizard" };

// struct to store the character
struct character_details
{
    string name;
    int class_id;
};

// output a description of the player's character details
void describe_character(character_details* player_character)
{
    cout << "Player details:" << endl;
    cout << "  Name  - " << player_character->name << endl;
    cout << "  Class - " << character_classes[player_character->class_id] << endl;
}

void main()
{   
    int character_class_index = -1;
    // get user input until the user picks a valid class
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

    // get the player name from the user
    cout << "Please enter your name: ";
    string name;
    cin.ignore();
    getline(cin, name);

    // insert these values into a struct
    character_details* player_character = new character_details();
    player_character->name = name;
    player_character->class_id = character_class_index;

    cout << endl;

    // describe the character
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

// struct holding the contents of an inventory slot
struct inventory_slot
{
    int item_id = -1;
    string item_description = "Empty";
};

// define descriptions of item IDs
const vector<string> item_descriptions = {"Sword", "Shield", "Bottle", "Golden Rune", "Gun", "Cobblestone"};

// get the name of an item from its id
string item_description_for_id(unsigned int id)
{
    if (id >= item_descriptions.size()) return "";
    return item_descriptions[id];
}

// split a string into a vector<string> at a delimiting char
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

// class which safely handles the inventory
class inventory_manager
{
private:
    // backing data
    vector<inventory_slot> inventory;

public:
    // set the contents of an inventory slot
    bool set_slot(unsigned int slot, unsigned int item_id)
    {
        if (slot >= inventory.size()) return false;

        inventory[slot].item_id = item_id;
        inventory[slot].item_description = item_description_for_id(item_id);

        return true;
    }

    // make an inventory slot empty
    bool clear_slot(unsigned int slot)
    {
        if (slot >= inventory.size()) return false;

        inventory[slot].item_id = -1;
        inventory[slot].item_description = "Empty";

        return true;
    }

    // get the contents of an inventory slot
    inventory_slot get_slot(unsigned int slot)
    {
        if (slot >= inventory.size()) return inventory_slot{ -2, "" };

        return inventory[slot];
    }

    // set the size of the inventory. clears the inventory in the process
    void set_size(unsigned int size)
    {
        inventory.clear();
        for (int i = 0; i < size; i++)
            inventory.push_back(inventory_slot());
    }

    // get the size of the inventory
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

    // prompt the user for inventory size, until they behave (input a valid number)
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

    // init inventory
    im.set_size((unsigned int)inventory_size);
    cout << "Inventory initialised with " << inventory_size << " slots." << endl << endl;

    // start mainloop where we process commands
    bool continue_mainloop = true;
    cin.ignore();
    while (continue_mainloop)
    {
        // get the user input
        string command;
        while (command.size() < 1)
        {
            cout << "> ";
            getline(cin, command);
        }
        cout << endl;

        // split input at space
        vector<string> split_command = split_str(command, ' ');

        // if the user didnt enter a command, try again
        if (split_command.size() == 0)
        {
            cout << "Enter a command." << endl << endl;
            continue;
        }

        // handle view command
        if (split_command[0] == "view")
        {
            // try again if the user didn't give enough arguments
            if (split_command.size() < 2)
            {
                cout << "'view' needs an argument: view <slot to view>" << endl << endl;
                continue;
            }

            // try to get the argument as an int, try again if it isn't valid
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

            // respond to the command
            cout << "Inventory slot " << slot_to_view << " information:" << endl;
            cout << "  Contents: " << slot_data.item_description << endl << endl;
        }
        // handle show_all command
        else if (split_command[0] == "show_all")
        {
            cout << "Inventory:" << endl;
            for (int i = 0; i < im.get_size(); i++)
            {
                cout << "  Slot " << i << ": " << im.get_slot(i).item_description << endl;
            }
            cout << endl;
        }
        // handle set command
        else if (split_command[0] == "set")
        {
            // if the user didn't give enough arguments, try again
            if (split_command.size() < 3)
            {
                cout << "'set' needs two arguments: set <slot to set> <item id>" << endl << endl;
                continue;
            }

            // try to get the slot and item ids, try again if invalid
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
            
            // try to set the slot, if it was out of range, try again
            bool result = im.set_slot(slot_to_set, item_id);
            if (!result)
            {
                cout << "Slot to view must be an index in the inventory." << endl << endl;
                continue;
            }
        }
        // handle items command
        else if (split_command[0] == "items")
        {
            for (int i = 0; i < item_descriptions.size(); i++)
            {
                cout << "  " << i << ": " << item_description_for_id(i) << endl;
            }
            cout << endl;
        }
        // handle exit command
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
main.h
```
#pragma once

#include <cmath>

// Vector2 class stub
class Vector2
{
public:
	float x, y;

	float magnitude();
	float distance(Vector2);

	Vector2(float, float);
};

// Vector2-related operator overloads
Vector2 operator+(Vector2 a, Vector2 b) { return Vector2(a.x + b.x, a.y + b.y); }
Vector2 operator-(Vector2 a, Vector2 b) { return Vector2(a.x - b.x, a.y - b.y); }
Vector2 operator*(Vector2 a, Vector2 b) { return Vector2(a.x * b.x, a.y * b.y); }
Vector2 operator/(Vector2 a, Vector2 b) { return Vector2(a.x / b.x, a.y / b.y); }
Vector2 operator*(Vector2 a, float scalar) { return Vector2(a.x * scalar, a.y * scalar); }
Vector2 operator/(Vector2 a, float scalar) { return Vector2(a.x / scalar, a.y / scalar); }

// including stream output
ostream& operator<<(ostream& stream, Vector2 v)
{
	stream << "(" << v.x << ", " << v.y << ")";
	return stream;
}

// get the magnitude of a Vector2
float Vector2::magnitude()
{
	return sqrt((x * x) + (y * y));
}

// get the distance between two Vector2 points
float Vector2::distance(Vector2 other)
{
	return (other - *this).magnitude();
}

// initialise the Vector2
Vector2::Vector2(float _x, float _y)
{
	x = _x;
	y = _y;
}

// get the distance between points, by just calling the Vector2 method
float GetDistanceBetweenPoints(Vector2 a, Vector2 b)
{
	return a.distance(b);
}
```

main.cpp
```
#include <iostream>

using namespace std;

#include "main.h"

void main()
{
    // get user input
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

    // construct these values into Vector2s
    Vector2 v_a = Vector2(xComponents[0], yComponents[0]);
    Vector2 v_b = Vector2(xComponents[1], yComponents[1]);

    // output the distance between them
    cout << "The distance between " << v_a << " and " << v_b << " is " << GetDistanceBetweenPoints(v_a, v_b) << endl;
    
}
```
i decided to write operator overrides for the main four (+ - * /) for my `Vector2` class. this enabled my methods to use simpler looking maths. i wrote two methods inside the class, `float magnitude()` which returns the magnitude of the instance, and `float distance(Vector2 other)` which subtracts `other` from the self instance (resulting in the vector from `other` to `this`), and returning the magnitude of this. i did this because it's nicer to have methods embedded in a class like this, but i wrapped this in the `float GetDistanceBetweenPoints(Vector2 a, Vector2 b)` function as instructed. declaring operators required the `Vector2` class and its properties to be defined, however it's methods use the operators, creating a dependency loop. to solve this, i first wrote a minimal class definition with the method stubs and fields, then the operators, then finally the implementations of the `Vector2` methods.

## challenge 10
```
#include <iostream>

using namespace std;

struct assessment_1_grades
{
    int c1_task_1 = 5;
    int c1_task_2 = 5;
    int c1_task_3 = 5;
    int c1_task_4 = 10;
    int c1_task_5 = 10;
    int c1_task_6 = 10;
    int c1_task_7 = 10;
    int c1_task_8 = 15;
    int c1_task_9 = 15;
    int c1_task_10 = 15;

    int c1 = 100;

    int c2 = 100;
};

struct assessment_2_grades
{
    int c1 = 100;
    int c2 = 100;
    int c3 = 100;
};

int get_assessment_1_c1_total(assessment_1_grades a1g)
{
    return a1g.c1_task_1
        + a1g.c1_task_2
        + a1g.c1_task_3
        + a1g.c1_task_4
        + a1g.c1_task_5
        + a1g.c1_task_6
        + a1g.c1_task_7
        + a1g.c1_task_8
        + a1g.c1_task_9
        + a1g.c1_task_10;
}

/*
* Returns a number between 0 and 100 for the overall grade on assignment 1
*/
float calculate_assessment_1_grade(assessment_1_grades a1g)
{
    return (0.7f * a1g.c1) + (0.3 * a1g.c2);
}

/*
* Returns a number between 0 and 100 for the overall grade on assignment 2
*/
float calculate_assessment_2_grade(assessment_2_grades a2g)
{
    return (0.6f * a2g.c1) + (0.2f * a2g.c2) + (0.2f * a2g.c3);
}

/*
* Repeatedly prompts the user for input until they behave (put in a value within the required range)
*/
int get_integer_input_from_user(string prompt, int min, int max)
{
    int r_val = min - 1;
    while (true)
    {
        cout << prompt;
        cin >> r_val;

        if (r_val < min || r_val > max)
        {
            cout << "The number you entered was out of range. Try again." << endl;
        }
        else
        {
            return r_val;
        }
    }
}

/*
* Returns a CRG band based on the percentage mark provided
*/
int get_band(float percentage)
{
    if (percentage < 30) return 0;
    if (percentage < 40) return 1;
    if (percentage < 50) return 2;
    if (percentage < 60) return 3;
    if (percentage < 70) return 4;
    return 5;
}

void main()
{
    assessment_1_grades a1g_max;
    assessment_2_grades a2g_max;

    assessment_1_grades a1g;
    assessment_2_grades a2g;

    // get assessment 1 data
    
    cout << "Please enter your marks for assessment 1, criterion 1:" << endl;

    a1g.c1_task_1 = get_integer_input_from_user("Challenge 1: ", 0, a1g_max.c1_task_1);
    a1g.c1_task_2 = get_integer_input_from_user("Challenge 2: ", 0, a1g_max.c1_task_2);
    a1g.c1_task_3 = get_integer_input_from_user("Challenge 3: ", 0, a1g_max.c1_task_3);
    a1g.c1_task_4 = get_integer_input_from_user("Challenge 4: ", 0, a1g_max.c1_task_4);
    a1g.c1_task_5 = get_integer_input_from_user("Challenge 5: ", 0, a1g_max.c1_task_5);
    a1g.c1_task_6 = get_integer_input_from_user("Challenge 6: ", 0, a1g_max.c1_task_6);
    a1g.c1_task_7 = get_integer_input_from_user("Challenge 7: ", 0, a1g_max.c1_task_7);
    a1g.c1_task_8 = get_integer_input_from_user("Challenge 8: ", 0, a1g_max.c1_task_8);
    a1g.c1_task_9 = get_integer_input_from_user("Challenge 9: ", 0, a1g_max.c1_task_9);
    a1g.c1_task_10 = get_integer_input_from_user("Challenge 10: ", 0, a1g_max.c1_task_10);

    a1g.c1 = get_assessment_1_c1_total(a1g);

    a1g.c2 = get_integer_input_from_user("Enter your mark for assessment 1, criterion 2: ", 0, a1g_max.c2);

    cout << endl;

    // get assessment 2 data

    a2g.c1 = get_integer_input_from_user("Enter your mark for assessment 2, criterion 1: ", 0, a2g_max.c1);

    a2g.c2 = get_integer_input_from_user("Enter your mark for assessment 2, criterion 2: ", 0, a2g_max.c2);

    a2g.c3 = get_integer_input_from_user("Enter your mark for assessment 2, criterion 3: ", 0, a2g_max.c3);

    cout << endl;
    
    // generate breakdown of assessment 1

    float a1_mark = calculate_assessment_1_grade(a1g);
    float a2_mark = calculate_assessment_2_grade(a2g);

    cout << "Assessment 1:" << endl;
    cout << "  Overall mark: " << a1_mark << "%" << endl;
    cout << "  Overall CRG band: " << get_band(a1_mark) << endl;
    cout << endl;
    cout << "  Criterion 1 mark: " << a1g.c1 << endl;
    cout << "  Criterion 1 CRG band: " << get_band(a1g.c1) << endl;
    cout << "  Criterion 1 details:" << endl;
    cout << "    Challenge 1: " << a1g.c1_task_1 << " / " << a1g_max.c1_task_1 << endl;
    cout << "    Challenge 2: " << a1g.c1_task_2 << " / " << a1g_max.c1_task_2 << endl;
    cout << "    Challenge 3: " << a1g.c1_task_3 << " / " << a1g_max.c1_task_3 << endl;
    cout << "    Challenge 4: " << a1g.c1_task_4 << " / " << a1g_max.c1_task_4 << endl;
    cout << "    Challenge 5: " << a1g.c1_task_5 << " / " << a1g_max.c1_task_5 << endl;
    cout << "    Challenge 6: " << a1g.c1_task_6 << " / " << a1g_max.c1_task_6 << endl;
    cout << "    Challenge 7: " << a1g.c1_task_7 << " / " << a1g_max.c1_task_7 << endl;
    cout << "    Challenge 8: " << a1g.c1_task_8 << " / " << a1g_max.c1_task_8 << endl;
    cout << "    Challenge 9: " << a1g.c1_task_9 << " / " << a1g_max.c1_task_9 << endl;
    cout << "    Challenge 10: " << a1g.c1_task_10 << " / " << a1g_max.c1_task_10 << endl;
    cout << endl;
    cout << "  Criterion 2 mark: " << a1g.c2 << endl;
    cout << "  Criterion 2 CRG band: " << get_band(a1g.c2) << endl;
    cout << endl;
    cout << endl;

    // generate breakdown of assessment 2

    cout << "Assessment 2:" << endl;
    cout << "  Overall mark: " << a2_mark << "%" << endl;
    cout << "  Overall CRG band: " << get_band(a2_mark) << endl;
    cout << endl;
    cout << "  Criterion 1 mark: " << a2g.c1 << endl;
    cout << "  Criterion 1 CRG band: " << get_band(a2g.c1) << endl;
    cout << endl;
    cout << "  Criterion 2 mark: " << a2g.c2 << endl;
    cout << "  Criterion 2 CRG band: " << get_band(a2g.c2) << endl;
    cout << endl;
    cout << "  Criterion 3 mark: " << a2g.c3 << endl;
    cout << "  Criterion 3 CRG band: " << get_band(a2g.c3) << endl;
    cout << endl;
}
```
this task was mostly lots of structure design and a lot of output. i wrote several utility functions to do things like getting the mark band for a given mark in a more self-contained way. one of these functions was one which repeatedly prompts the user for input until they enter a value within range, which would have been a useful function from about challenge 4 onwards. i tested this with various correct and incorrect inputs, and it appeared to give correct results according to the CRG.