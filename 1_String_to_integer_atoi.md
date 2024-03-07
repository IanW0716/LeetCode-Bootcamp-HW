class Solution(object):
    def myAtoi(self, s):
        """
        :type s: str
        :rtype: int
        """
        # Define the maximum and minimum values for a 32-bit signed integer
        INT_MAX = 2**31 - 1
        INT_MIN = -2**31
        
        # Initialize the index, sign, and base for conversion
        i = 0
        sign = 1
        base = 0
        n = len(s)
        
        # Ignore leading whitespaces
        while i < n and s[i] == ' ':
            i += 1
        
        # Check for the sign
        if i < n and (s[i] == '-' or s[i] == '+'):
            sign = -1 if s[i] == '-' else 1
            i += 1
        
        # Convert the number and avoid non-digit characters
        while i < n and s[i].isdigit():
            # Check for overflow and clamp if necessary
            if base > INT_MAX // 10 or (base == INT_MAX // 10 and int(s[i]) > 7):
                return INT_MAX if sign == 1 else INT_MIN
            
            base = 10 * base + int(s[i])
            i += 1
        
        return base * sign
