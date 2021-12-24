# Course Schedule IV
## https://leetcode.com/problems/course-schedule-iv

There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course ai first if you want to take course bi.

For example, the pair [0, 1] indicates that you have to take course 0 before you can take course 1.
Prerequisites can also be indirect. If course a is a prerequisite of course b, and course b is a prerequisite of course c, then course a is a prerequisite of course c.

You are also given an array queries where queries[j] = [uj, vj]. For the jth query, you should answer whether course uj is a prerequisite of course vj or not.

Return a boolean array answer, where answer[j] is the answer to the jth query.

![Course Schedule IV](example.JPG?raw=true)

# Implementation : Floyd Warshall Algorithm O(n^3)
```java
class Solution {
    public List<Boolean> checkIfPrerequisite(int n, int[][] prerequisites, int[][] queries) {
        boolean[][] connected = new boolean[n][n];
        for (int[] p : prerequisites)
            connected[p[0]][p[1]] = true; // p[0] -> p[1]
        for (int k = 0; k < n; k++)
            for (int i = 0; i < n; i++)
                for (int j = 0; j < n; j++)
                    connected[i][j] = connected[i][j] || connected[i][k] && connected[k][j];
        List<Boolean> result = new ArrayList<>();
        for (int[] q : queries)
            result.add(connected[q[0]][q[1]]);
        return result;
    }
}
```

# References :
https://www.youtube.com/watch?v=oNI0rf2P9gE (Abdul Bari, Floyd Warshall : All Pairs Shortest Path Algorithm)

https://leetcode.com/problems/course-schedule-iv/discuss/660509/JavaPython-FloydWarshall-Algorithm-Clean-code-O(n3)
