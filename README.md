# UnibitAssessment

import java.util.*;


public class Unibit
{


    // Finding pair for first target
    public static List<List<Integer>> findCombinations(int[] nums, int target) {
        List<List<Integer>> combinations = new ArrayList<>();
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    List<Integer> combination = new ArrayList<>();
                    combination.add(nums[i]);
                    combination.add(nums[j]);
                    combinations.add(combination);
                }
            }
        }
        return combinations;
    }

    // merging the arrays
    public static int[] mergeArrays(List<List<Integer>> arrays) {
        int totalLength = 0;
        for (List<Integer> array : arrays) {
            totalLength += array.size();
        }

        int[] mergedArray = new int[totalLength];
        int index = 0;
        for (List<Integer> array : arrays) {
            for (int num : array) {
                mergedArray[index++] = num;
            }
        }

        Arrays.sort(mergedArray);
        return mergedArray;
    }

    // finding combinations for second target
    public static List<List<Integer>> findTargetCombinations(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums); // Sort the array in ascending order
        backtrack(nums, target, 0, new ArrayList<>(), result);
        return result;
    }

    private static void backtrack(int[] nums, int target, int start, List<Integer> combination, List<List<Integer>> result) {
        if (target == 0 && combination.size() > 1) {
            result.add(new ArrayList<>(combination));
            return;
        }
        if (target < 0) {
            return;
        }
        for (int i = start; i < nums.length; i++) {
            if (i > start && nums[i] == nums[i - 1]) {
                continue; // Skip duplicates to avoid duplicate combinations
            }
            combination.add(nums[i]);
            backtrack(nums, target - nums[i], i + 1, combination, result);
            combination.remove(combination.size() - 1);
        }
    }

    public static void main(String[] args) {
        // Given sample input
        int[] nums = {1, 3, 2, 2, -4, -6, -2, 8};
        int target = 4;
        List<List<Integer>> twoDarray = findCombinations(nums,target);
        System.out.print("First combination for " +"'"+ target+"': ");
        System.out.println(twoDarray);

        int newTarget = target * 2;
        int [] sortedArray = mergeArrays(twoDarray);
        List<List<Integer>> targetCombinations = findTargetCombinations(sortedArray, newTarget);
        System.out.print("Second combination for " +"'"+ newTarget+"': ");
        System.out.println(targetCombinations);
    }
}

