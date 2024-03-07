class Solution(object):
    def palindromePairs(self, words):
        """
        :type words: List[str]
        :rtype: List[List[int]]
        """
        def is_palindrome(check):
            return check == check[::-1]

        words_dict = {word: i for i, word in enumerate(words)}
        result = []

        for i, word in enumerate(words):
            for j in range(len(word) + 1):
                prefix, suffix = word[:j], word[j:]
                
                # If prefix is palindrome, find reversed suffix in words
                if is_palindrome(prefix):
                    back = suffix[::-1]
                    if back != word and back in words_dict:
                        result.append([words_dict[back], i])

                # If suffix is palindrome, find reversed prefix in words
                if j != len(word) and is_palindrome(suffix):  # Avoid duplicates
                    front = prefix[::-1]
                    if front != word and front in words_dict:
                        result.append([i, words_dict[front]])

        return result
