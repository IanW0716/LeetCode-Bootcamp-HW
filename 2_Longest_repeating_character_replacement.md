class Solution(object):
    def characterReplacement(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        # Initialize a dictionary to keep track of character frequencies within the window
        char_count = {}
        left = 0
        maxf = 0  # Max frequency of a character within the window
        max_length = 0

        for right in range(len(s)):
            char_count[s[right]] = char_count.get(s[right], 0) + 1
            maxf = max(maxf, char_count[s[right]])

            # If the window size minus the most frequent character count is greater than k,
            # it means we cannot make all the characters in the window the same using k or fewer operations.
            # Thus, we shrink the window from the left.
            if (right - left + 1) - maxf > k:
                char_count[s[left]] -= 1
                left += 1

            # Update the max_length of the window
            max_length = max(max_length, right - left + 1)
        
        return max_length
