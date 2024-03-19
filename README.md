# Convert-into-words
You're given an integer, convert these into words.  Input First line will contain an integer 'n'.  Constraints: 0 &lt;= num &lt; 106 Output Convert into words and output the string.

def int_to_words(num):
    # Define word representations for digits 0 to 19
    ones = ["", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine",
            "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen",
            "Seventeen", "Eighteen", "Nineteen"]
    
    # Define word representations for tens multiples
    tens = ["", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"]

    if num == 0:
        return "Zero"

    # Function to convert two-digit numbers into words
    def two_digits(n):
        if n < 20:
            return ones[n]
        else:
            return tens[n // 10] + (" " + ones[n % 10] if n % 10 != 0 else "")

    # Function to convert three-digit numbers into words
    def three_digits(n):
        if n < 100:
            return two_digits(n)
        else:
            return ones[n // 100] + " Hundred" + (" " + two_digits(n % 100) if n % 100 != 0 else "")

    # Define word representations for larger digit groups
    groups = ["", "Thousand", "Million", "Billion", "Trillion"]

    words = ""
    for i in range(len(groups)):
        if num % 1000 != 0:
            words = three_digits(num % 1000) + " " + groups[i] + " " + words
        num //= 1000
        if num == 0:
            break

    return words.strip()

# Input
n = int(input())

# Output
print(int_to_words(n))
