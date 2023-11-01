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

- to simplify and keep the code tidy, i wrote the title as a multi-line string, rather than `cout`ing numerous lines
- since backslash is treated as the indicator of an escape character, i had to replace each with a double backslash in order to produce a single backslash in the output
- i found this easy, as i'm already very familiar with C++ syntax
- the ASCII art text was generated using https://patorjk.com/software/taag

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

- this task is mostly just making use of `cout` and `cin` as well as the `<<` and `>>` stream operators to assemble multiple parts of a single console line
- i was making sure to use `endl` rather than just `"\n"` because i think it reads more clearly and it ensures consistency across platforms
- i used the builtin function `int stoi(string)` to convert the age text input from the user into an integer
- again i found this task easy since i'm already familiar with C++

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

- similar to the previous challenge in that it primarily involves getting input from the user via `cin`, though this time i used `float stof(string)` to get a floating point number from the user's text input
- i could have used the `float powf(float, float)` function to square the number, but i used `num*num` instead since this is faster in a instance like this with a pre-determined integer power (i.e. 2)

## challenge 4
```
#include <iostream>

using namespace std;

void boxify_text(string text, int padding)
{
    int length = text.length() + 2 + (2 * padding);

    // first line of stars
    for (int i = 0; i < length; i++) cout << "*";
    cout << endl;

    // padding lines
    string padding_line = "*";
    for (int i = 0; i < length-2; i++) padding_line += " ";
    padding_line += "*";

    for (int i = 0; i < padding; i++) cout << padding_line << endl;

    // text
    cout << "*";
    for (int i = 0; i < padding; i++) cout << " ";
    cout << text;
    for (int i = 0; i < padding; i++) cout << " ";
    cout << "*" << endl;

    // padding lines
    for (int i = 0; i < padding; i++) cout << padding_line << endl;

    // second line of stars
    for (int i = 0; i < length; i++) cout << "*";
}

void main()
{
    string text;
    cout << "enter some text: ";
    cin >> text;

    int padding;
    cout << "how much padding? ";
    cin >> padding;

    boxify_text(text, padding);
    
}
```

- i split my box-making code off into its own function for modularity; it takes two arguments: the text to put in the box, and the padding amount
- the length of the string plus padding and box edges is stored as a local variable to simplify conditions on for loops later
- the code then passes over multiple for loops to do things like generating a whole line of stars for the top, generate a line of spaces bounded by stars (and then output that a number of times based on the padding amount), and output the padding around the actual text
- i used inline for loops for all of these loops, since each one only contains a single `cout << <something>;` statement, which considerably shortens the code and makes it easier to read
- i generated the padding line (i.e. line of spaces with a star at each end) as a string and then repeatedly outputted that string, rather than building the padding line again each time, avoiding the use of nested for loops
- i also discovered over the course of this challenge that `cin >>` supports automatically converting its result to an integer if the destination variable is an integer, which would slightly simplify some code in previous challenges

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

- my code is broken into three functions, one for fully capitalising a string, one for full decapitalising it, and one for capitalising it on only the first letter of a sentence
- the code primarily makes use of the builtin `char toupper(char)` and `char tolower(char)` functions to capitalise and decapitalise characters
- the first two functions are simple `for` loops where we loop over the input and add the capitalised/decapitalised letter to the output buffer, before we return this buffer at the end
- the latter function is more complex: 
	- we keep track of the current state of the text, with a local variable telling the program whether it is waiting to capitalise the first letter of a new sentence
	- while this flag is set, we check to see if the current character is an alphabetical letter, by comparing it to capital and lowercase 'A' and 'Z' (since alphabetical letters in the ASCII character set are laid out, very sensibly, contiguously, though capital and lowercase are separated). doing this with the `chr >= 'A' && chr <= 'Z'` condition format is great because it makes it easy to see what is actually being checked
	- if the flag is set and the current character is an alphabetical letter, we must capitalise it, add it to the output buffer, and clear the end-of-sentence flag
	- if the flag is set but there is no alphabetical letter (e.g. a space after a fullstop), we add the letter to the output buffer but don't clear the flag
	- otherwise, we just add the character to the output buffer, checking to see if the character we're adding is a fullstop, exclamation mark, or question mark, and if it is then we set the end-of-sentence flag
- the main problem i encountered was that `cin >> text` only gets up to the next whitespace character and puts it in text, meaning that strings with spaces in (i.e. most sentences written by normal people) would only get their first word read. this was fixed by using the `void getline(istream &, string)` function, which pulls an entire line up until it reads a newline character into the provided string variable

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
            else cout << "boiling";
            cout << endl;
        }
    }

    // tell the player they won
    cout << "you got it! the number was " << target_number << endl;
    cout << "it took you " << num_guesses << " guesses" << endl;
}
```

- this task was made a lot easier by the fact that the random function is already written for us, so just calling it with appropriate arguments was simple. however, since the function defined in main.h is not documented, it required a little bit of experimentation to prove whether or not the upper and lower bounds were inclusive (they are both inclusive)
- we can use a simple `while (true) { }` loop with a `break` statement when the player guesses the number
- inside this `while` loop we prompt the user for a guess with `cout` and `cin`, check how far away from the secret number it is, break if its equal, or otherwise give the user a hint as to how warm they are
	- we first calculate the absolute difference from the secret number to the user guess, making the following `if` statements much simpler
	- this was the trickiest part, since the description of the challenge talks about the player guessing **exactly 50 away** for the 'freezing' response for instance, and does not specify if the range of difference values covered by 'freezing' should therefore be 50-100 or 35-50. after somewhat clarifying with a tutor, i treated the challenge description as meaning **50 or more away** from the secret number
	- this did mean adjusting the 'boiling' range to also cover being 1 away from the secret number, previously i had an extra condition for being this close named 'super duper boiling'
	- i used a chain of inline `if...else if...else` statements to implement these ranges in order to keep the code concise and the conditions on the `if` statements simple, and to avoid nesting
- each iteration of the `while` loop also increments the guess counter variable
- when we escape the loop, the user is told what the number was and how many guesses they took to find it

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

- i made use of a `const vector<string>` to store the character classes, since it's easy to get the length of this data type
- i wrote a utility function which outputs a description of my character details struct. i could have written this as an overload of the `<<` operator, but chose not to for now
- my character details struct contains two fields, a name as a string, and a class ID as an integer (where the integer indexes the character class vector)
- when getting the user's player class, i used a simple `while (true) { }` loop, which prompts the user with the list of character classes each iteration, reads their input as an integer, and breaks only if the user's input was within the valid range
	- the user is also told if their input is valid or invalid, and which class they picked
- when getting the user's character name i used `getline` in order to ensure the player could enter multi-word names (like, maybe, 'Argoth the destroyer', or whatever)
- i initially had problems with this however, since `getline` would return nothing (leading to a blank character name), skipping immediately due to it detecting the trailing newline from the previous user input. i resolved this by using `cin.ignore()` just before `getline`, to tell it to ignore the trailing newline (as suggested by stack overflow)
- i used a pointer to my character details struct, rather than a reference, so that a character could be passed easily into functions such as the `describe_character` function, and written back to by those functions potentially

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

- my struct representing an inventory slot contains two fields: an item ID int, which indexes the `item_descriptions` vector (where -1 represents an empty slot), and an item description string
- i again used a `const vector<string>` to store the list of item descriptions, as it's easily expandable and has a useful `.size()` method
- i also developed a few utility functions:
	- a function which just gets an item description from an id (an unsigned int), and just contains a protective `if` statement to prevent indexing the item descriptions vector out of range
	- a `split_string` function which takes in a string and a char, and will use the `string.find` and `string.substr` methods to split the input into a `vector<string>` at the delimiting character. this method is only used once but is very important to the command processing code and makes sense to have it abstracted as a separate function for clarity and modularity
- the 'inventory' itself is managed by a class
	- this allows us to hide the actual backing data for the inventory, a `vector<inventory_slot>`, which can be protected by only allowing access through methods (the field is made private)
	- these methods allow for setting the contents of slots to particular item IDs, clearing slots, getting the contents of an inventory slot, setting the size of the inventory, and getting the size
	- each of these methods has the appropriate validation, including checking for indexing the inventory out of range
- the user is prompted for a positive integer to initialise the inventory size, in a loop which repeats until a valid input is received. the only new thing to note here is handling exceptions from the `stoi` function using a `try...catch` block
- after initialising the inventory, we start a main program loop in which commands are processed, this is a `while` loop predicated on the `continue_mainloop` variable which allows us to break out
- when getting the user's command input, i had some problems again with `getline` being tripped up by a trailing newline, but having multiple inputs previously seemed to cause unpredictable behaviour. i solved this by repeatedly calling `getline` until it manages to get some input (i.e. a string of length > 0)
- after the string is split at the space character, the only thing left is a lot of `if` statements to perform validation and branch depending upon the command entered
- depending on the command, we must check the number of arguments provided (by looking at the number of elements in the `split_command`), and check that the numerical values entered are valid and in range for what they're indexing (e.g. the inventory or the list of items)
- whenever a breaking condition is encountered, such as a 'set' command not having enough arguments, the `continue` keyword is used to skip back to the top of the loop and ask the user for a fresh command
- i tested my input validation with a variety of different inputs, (valid, invalid, and edge case), so i'm confident that it should catch all invalid inputs
- although i didn't have any real problems with this challenge besides the `getline` shenanigans, it was a more interesting challenge than previous ones
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

- the `Vector2` class itself is very simple, with `float x, y` variables. however, for some OOP practice i embedded `magnitude` and `distance` methods in the class, as well as a constructor which takes two `float`s for x and y
- the `magnitude` method does exactly what it sounds like, and its implementation uses the same approach of `x * x` instead of `powf(x, 2)` for a slight speed boost, and the `sqrt` function to complete Euclid's formula
- the `distance` method takes another `Vector2` as input and subtracts the self `Vector2` from it, before returning the magnitude of the resulting `Vector2`
- in order to do this subtraction, i wrote a set of operator overloads accepting `Vector2` types: adding, subtracting, multiplying and dividing two `Vector2`s, and also multiplying and dividing a `Vector2` by a `float`
- i also wrote a `<<` stream operator overload so that i could easily output my `Vector2` type to the console
- however, these operators created a problem: they need the `Vector2` class to be declared, including x and y fields, meanwhile the class methods, mainly the `distance` method require the operators to already be declared (subtraction specifically), leading to a dependency loop. i solved this by declaring the class as a stub, then defining the operators, then finally implementing the methods from the `Vector2` class. ideally these implementations would be done in a dedicated file (to form a pair of 'vector2.h' and 'vector2.cpp')
- as instructed by the challenge description, i also wrote a `GetDistanceBetweenPoints` function which simply calls the `Vector2::distance` method and returns the result
- the rest of the code back in `main` is just constructing a pair of `Vector2`s and calling `GetDistanceBetweenPoints` and outputting the result
- this was an interesting challenge! i've had practice writing operators and mathematical classes before so this was a reminder for me

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

- i came up with two `struct`s one for the marking information of each assessment, with the appropriate fields based on reading the CRG
- i had the idea of having the structs initialised with values equal to the maximum mark for those grades, meaning that to find the maximum marks for things (e.g. for finding percentage marks), i can just instantiate a new struct and read its default values
- i wrote a few utility functions:
	- one for adding up all the marks in the different challenges of the first criterion in assessment 1
	- one for getting the total, weighted score for assessment 1, using the 70-30 split as described by the CRG
	- one for getting the total, weighted score for assessment 2, using the 60-20-20 split as described by the CRG
	- one which abstracts away the process of getting a validated integer input from the user. this gets used **a lot** in `main`, and since we want to do a little `while` loop to repeat until we get valid input, it makes sense to have this as a self-contained function. it even supports having custom upper and lower bound limits and a specific prompt for the user
	- one which returns a number from 0-5 for which CRG band a percentage score falls into, based on the ranges defined in the CRG
- the rest of the program is lots of getting input from the user to populate the structs `a1g` and `a2g`. once all this is done, we can calculate extra information like the total assessment 1 criterion 1 score, the total percentage score of assessment 1, the total percetnage score of assessment 2, and the CRG grade bands for both of these and individual criteria within
- we can then output all of this information, nicely formatted to the user
- again, i tested this with various correct inputs (as well as checking the error checking with invalid inputs) and the output matched what was expected from what is written in the CRG