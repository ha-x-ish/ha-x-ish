#include <stdio.h>
#include <stdlib.h>

int compare(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

int min_subarray_length(int A[], int B[], int N) {
    int min_length = N;

    for (int i = 0; i < N; i++) {
        for (int j = i; j < N; j++) {
            int subarray_A[j - i + 1];
            int subarray_B[j - i + 1];

            for (int k = i; k <= j; k++) {
                subarray_A[k - i] = A[k];
                subarray_B[k - i] = B[k];
            }

            qsort(subarray_A, j - i + 1, sizeof(int), compare);
            qsort(subarray_B, j - i + 1, sizeof(int), compare);

            int equal = 1;
            for (int k = 0; k <= j - i; k++) {
                if (subarray_A[k] != subarray_B[k]) {
                    equal = 0;
                    break;
                }
            }

            if (equal) {
                min_length = (min_length < (j - i + 1)) ? min_length : (j - i + 1);
            }
        }
    }

    return min_length;
}

int main() {
    int T;
    scanf("%d", &T);

    for (int i = 0; i < T; i++) {
        int N;
        scanf("%d", &N);

        int A[N];
        for (int j = 0; j < N; j++) {
            scanf("%d", &A[j]);
        }

        int B[N];
        for (int j = 0; j < N; j++) {
            scanf("%d", &B[j]);
        }

        int min_length = min_subarray_length(A, B, N);
        printf("%d\n", min_length);
    }

    return 0;
}
