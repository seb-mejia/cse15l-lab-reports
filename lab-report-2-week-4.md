https://docs.google.com/document/d/14SJ2qRuxBCfOXxI1-dPo3KTOvd4bmM0K25GyVtfXLrU/edit

## Code change 1:

**Code change diff:**

![diff 1](https://user-images.githubusercontent.com/90715607/164960400-4367a775-5e8f-4909-9a6c-48b4eb565db8.PNG)

**Failure-inducing input:**

https://github.com/TheSeb72/markdown-parser/blob/main/far%20apart.md

**Symptom:**

![OutOfMemoryError](https://user-images.githubusercontent.com/90715607/164957021-ec8d6fb6-a2c4-4034-9f63-0c4f362637f3.PNG)

**Explanation:**

In the original code, we always add the characters (the website) between the parentheses () to toReturn, and set currentIndex to the character after the parentheses. However, in the fixed code, we only add the website if the parentheses DIRECTLY FOLLOW the brackets. If the parentheses do not directly follow the brackets, then we simply increase the current index ```currentIndex++;``` until the parentheses are reached.

## Code change 2:
