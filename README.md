# 32PR
# 32 Практика
```
import java.util.ArrayList;
import java.util.List;

public class JohnsonTrotter {

    private static int findMobile(int[] perm, boolean[] direction) {
        int mobile = -1;
        int mobileValue = 0;

        for (int i = 0; i < perm.length; i++) {
            int neighborIndex = direction[i] ? i - 1 : i + 1;

            if (neighborIndex >= 0 && neighborIndex < perm.length &&
                perm[i] > perm[neighborIndex] && perm[i] > mobileValue) {
                mobile = i;
                mobileValue = perm[i];
            }
        }

        return mobile;
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    private static void swap(boolean[] arr, int i, int j) {
        boolean temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static List<int[]> generatePermutations(int n) {

        int[] perm = new int[n];
        boolean[] direction = new boolean[n]; 

        for (int i = 0; i < n; i++) {
            perm[i] = i + 1; 
            direction[i] = true; 
        }

        List<int[]> result = new ArrayList<>();
        result.add(perm.clone());

        int mobileIndex;
        while ((mobileIndex = findMobile(perm, direction)) != -1) {
            int neighborIndex = direction[mobileIndex] ? mobileIndex - 1 : mobileIndex + 1;

            swap(perm, mobileIndex, neighborIndex);
            swap(direction, mobileIndex, neighborIndex);

            for (int i = 0; i < perm.length; i++) {
                if (perm[i] > perm[neighborIndex]) {
                    direction[i] = !direction[i];
                }
            }

            result.add(perm.clone());
        }

        return result;
    }

    public static void main(String[] args) {
        int n = 4; 
        List<int[]> permutations = generatePermutations(n);

        for (int[] perm : permutations) {
            for (int num : perm) {
                System.out.print(num + " ");
            }
            System.out.println();
        }
    }
}
```
