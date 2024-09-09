# LCS

public class LongestCommonSubsequence {

    // Method to find the length of the longest common subsequence
    public static int lcs(String s1, String s2) {
        int m = s1.length();
        int n = s2.length();

        // Create a 2D array to store lengths of LCS of substrings
        int[][] dp = new int[m + 1][n + 1];

        // Build the dp array from the bottom up
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1; // Characters match, increase LCS length
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]); // Characters don't match, take max
                }
            }
        }

        // Print the LCS
        printLCS(dp, s1, s2);

        // Return the length of LCS of s1[0..m-1] and s2[0..n-1]
        return dp[m][n];
    }

    // Method to print the longest common subsequence
    public static void printLCS(int[][] dp, String s1, String s2) {
        int i = s1.length();
        int j = s2.length();
        StringBuilder lcs = new StringBuilder();

        // Traverse the dp array from the bottom-right corner
        while (i > 0 && j > 0) {
            // If characters match, include them in the LCS
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                lcs.append(s1.charAt(i - 1));
                i--;
                j--;
            }
            // Move to the direction of the larger value
            else if (dp[i - 1][j] > dp[i][j - 1]) {
                i--;
            } else {
                j--;
            }
        }

        // Since the LCS is built backwards, reverse it
        System.out.println("Longest Common Subsequence: " + lcs.reverse().toString());
    }

    public static void main(String[] args) {
        String s1 = "AGGTAB";
        String s2 = "GXTXAYB";

        int length = lcs(s1, s2);
        System.out.println("Length of LCS: " + length);
    }
}
