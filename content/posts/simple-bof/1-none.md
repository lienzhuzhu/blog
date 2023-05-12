+++
title = "Simple Buffer Overflow 1 - No Protections Enabled"
date = "2023-05-11T23:58:43-05:00"
description = "Exploiting a buffer overflow vulnerability with no protections to consider."

tags = ["security","software","system",]
+++


In this post we will exploit a program vulnerable to buffer overflow 

Please check out the [series introduction](/blog/posts/simple-bof/0-overview) if you are unfamiliar with stack based buffer overflow.



```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int check_answer(char *ans) {

  int ans_flag = 0;
  char ans_buf[16];

  strcpy(ans_buf, ans);

  if (strcmp(ans_buf, "forty-two") == 0)
    ans_flag = 1;

  return ans_flag;

}

int main(int argc, char *argv[]) {

  if (argc < 2) {
    printf("Usage: %s <answer>\n", argv[0]);
    exit(0);
  }
  if (check_answer(argv[1])) {
    printf("Right answer!\n");
  } else {
    printf("Wrong answer!\n");
  }

}
```