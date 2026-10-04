```
// Boyer-Moore Voting Algorithm
int candidate = -1;
int count = 0;

for (int i = 0; i < n; i++) {
  if (count == 0) {
    candidate = arr[i];
  }
  if (arr[i] == candidate) {
    count++;
  }
} else {
    count--;
  }
}

// Verify the candidate is indeed the majority
count = 0;
for (int i = 0; i < n; i++) {
  if (arr[i] == candidate) {
    count++;
  }
}
```