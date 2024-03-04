class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        # Initialize left and right pointers, and max_area variable
        left, right = 0, len(height) - 1
        max_area = 0
        
        while left < right:
            # Calculate the width
            width = right - left
            # Calculate the height using the shorter of the two lines
            current_height = min(height[left], height[right])
            # Calculate the current area
            current_area = width * current_height
            # Update max_area if the current area is larger
            max_area = max(max_area, current_area)
            
            # Move the pointer pointing to the shorter line
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
                
        return max_area
