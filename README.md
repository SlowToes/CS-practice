# Free Code Camp Guide
## JavaScript DSA Certification Projects

### 1. Panlindrome Checker
**Pre-requisites:**
1. While loops
1. Strings, char & arrays
1. Regular expressions

**Standard libraries used:**
1. isalnum() -> checks if a char is alphanumeric -> a-z, A-Z, 0-9
1. toLowerCase() -> to convert a char to lower case for comparison
1. test() -> reg exp function -> returns true if it finds a match -> patternToTestFor.test(string)

**Intuition:**
1. Use two pointers, one at start and one at end to check if they are the same.

**Approach:**
1. If a char is not alphanumeric we ignore and update our pointer.
1. Convert the char to lower case.
1. If they are the same, increment start and decrement end to continue checking.
1. Return false once they are not the same.

**Code explanation with comments:**

	function palindrome(str) {
 		let start = 0;
		let end = str.length - 1;  // declare "start" and "end" indexes for the str

		while (start < end)  // stops once pointers are in the middle
		{
			while (start < end && !isalnum(str[start]))  // if str[start] is not alphanumeric
			{
				start++;
			}

			while (end > start && !isalnum(str[end]))  // if str[end] is not alphanumeric
			{
				end--;;
			}

			if (str[start].toLowerCase() != str[end].toLowerCase())  // comparison
			{
				return false;
			}
			else 
			{
				start++;
				end--;
			}
		}
		return true;
	}

	// making the isalnum function
	// not needed if coding in other languages like C++ as this is already a standard function to use
 
	function isalnum(char) {
		return /[a-zA-Z0-9]/.test(char);
	}

### 2. Roman Numeral Converter
**Pre-requisites:**
1. Arrays
1. Math (Modulo)

**Standard libraries used:**
1. Math.floor() -> Rounds down to nearest integer

**Intuition:**
1. Brute force

**Approach:**
1. Create arrays that has the roman string for each numerical value in the ones, tens, hundreds and thousands place.
1. Get each individual number from the parameter and match it to the index of the arrays created in Step 1.

**Code explanation with comments:** 

	function convertToRoman(num) {
		const ones = ["", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"];
		const tens = ["", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"];
		const hundreds = ["", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"];
		const thousands = ["", "M", "MM", "MMM"];

		const roman = thousands[Math.floor(num / 1000)] + 
					  hundreds[Math.floor((num % 1000) / 100)] +
					  tens[Math.floor((num % 100) / 10)] + 
					  ones[Math.floor(num % 10)];

		/*
		1234/1000 = 1
		1234%1000 = 200 /100 = 2
		1234%100 = 34/10 = 3
		1234%10 = 4
		*/

		return roman;
	}

### 3. Caesars Cipher (ROT13)
**Pre-requisites:**
1. Strings & arrays

**Standard libraries used:**
1. charCodeAt() -> returns ascii value of a char
1. String.fromCharCode() -> returns char from ascii value
1. push() -> add value to the end of the array
1. join() -> joins back the elements of an array into a string -> default parameter is a ,

**Intuition:**
1. Use ASCII values to map the chars
1. Add or subtract 13 to the values to get the desired char

**Approach:**
1. Remap the ascii value of the given char by + / - 13
1. Convert the value back to a char and push the char into result array.
1. Join back the elements of the array to form a string.

**Code explanation with comments:**

	function rot13(str) {
		let result = [];
		for (let i = 0; i < str.length; i++)
		{
			let asciiNum = str[i].charCodeAt();

			if (asciiNum >= 65 && asciiNum <= 77)
			{
				result.push(String.fromCharCode(asciiNum + 13));
			}
			else if (asciiNum >= 78 && asciiNum <= 90)
			{
				result.push(String.fromCharCode(asciiNum - 13));
			}
			else // if the char is not a letter
			{
				result.push(str[i]);
			}
		}
		return result.join("");
	}



