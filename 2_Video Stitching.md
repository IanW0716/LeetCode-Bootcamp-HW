class Solution(object):
    def videoStitching(self, clips, time):
        """
        :type clips: List[List[int]]
        :type time: int
        :rtype: int
        """
        clips.sort(key=lambda x: x[0])  # Sort the clips based on their start time.
        total_clips = 0
        current_end, next_end = 0, 0
        i = 0
        while i < len(clips) and clips[i][0] <= current_end:
            # While there are clips that can extend the coverage without leaving a gap
            while i < len(clips) and clips[i][0] <= current_end:
                next_end = max(next_end, clips[i][1])  # Select the clip that extends the furthest.
                i += 1
            total_clips += 1  # We've chosen another clip.
            current_end = next_end  # Extend the coverage.
            if current_end >= time:  # If the entire duration is covered
                return total_clips
        return -1  # If we exit the loop without covering the entire duration.
