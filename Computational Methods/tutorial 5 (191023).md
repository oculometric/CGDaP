1. for a 10 letter password, all uppercase alphanumeric, there are 26 + 10 possible characters per slot, so 36^10 possibilities
2. approx 31536000 seconds in a year, so 36^10/31536000 years to solve at 1 iteration per second, 115936023.594 years, 116 million years approx
3. 
```
Let real_password = input from user
Let check_password = ""

While check_password != real_password And check_password != "9999999999" Do
	If (check_password[0] = 'Z') Then
		check_password[1] // TODO
End While
```
4. Using a wordlist of commonly used words, or social engineering