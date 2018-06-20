---
layout: post
title: Two sums continued...
category: leetcode
---

Leetcode has a few variations of the [Two Sum problem]({{ site.baseurl }}/two-sums/).

## Two Sum II - Input array is sorted
This solution beats 56.40% of other C++ implementations and was just adapted from the first solution to be a 1-based index but doesn't really take into account that the input numbers array is sorted in ascending order.
```cpp
vector<int> twoSum(vector<int>& numbers, int target) {
    vector<int> ans;
    unordered_map<int, int> myMap;
    for(int i = 0; i < numbers.size(); i++){
	    auto temp = myMap.find(numbers[i]);
	    if (temp == myMap.end()){
		    myMap[target - numbers[i]] = i;
	    } else {
		    int ind1 = temp->second;
			ans.push_back(ind1 + 1);
			ans.push_back(i + 1);
			break;
        };
    };
    return ans;
}
```
Using the knowledge that the input is sorted in ascending order, we can try having an index for the front of the array and an index for the back of the array. The sum of these two will produce a value that is either: equal to the target, greater than the target or less than the target. If the sum is equal to the target, we can stop and return the two indices. If the sum is greater than the target, we can move the back index to the left (decrement) to make the sum smaller; otherwise we can move to front index to the right (increment) to make the sum larger. Theoretically, this is also O(n) time where n is the length of the array, however we are actually iterating through n/2 elements of the array at most which makes a different in the practical runtime. This solution beats 99.69% of the submission runtimes.
```cpp
vector<int> twoSum(vector<int>& numbers, int target) {
    int frontIndex = 0;
    int backIndex = numbers.size() - 1;
    vector<int> ans;
    
    while (frontIndex != backIndex) {
        int sum = numbers[frontIndex] + numbers[backIndex];
        if (sum == target){
            ans.push_back(frontIndex+1);
            ans.push_back(backIndex+1);
            return ans;
        } else if (sum > target){
            backIndex--;
        } else{
            frontIndex++;
        }
    }
}
```
## Two Sum III - Data structure design
The initial attempt of this solution is a relative slow implementation: beats only 6.16% of implementations.<br>
Runtime O(n), Space O(n); I know this isn't the fastest implementation but I'm not motivated enough to work on a better implementation at the moment. Maybe one day? 
```cpp
class TwoSum {
public:

    // Add the number to an internal data structure.
    void add(int number) {
        myMap[number]++;
    }

    // Find if there exists any pair of numbers which sum is equal to the value.
    bool find(int value) {
        for (const auto& temp : myMap) {
            const auto num = value - temp.first;
            if (myMap.count(num) && (num != temp.first || temp.second > 1)) {
                return true;
            }
        }
        return false;
    }

private:
    unordered_map<int, int> myMap;
};

/**
 * Your TwoSum object will be instantiated and called as such:
 * TwoSum obj = new TwoSum();
 * obj.add(number);
 * bool param_2 = obj.find(value);
 */
```
## Two Sum IV - Input is a BST
