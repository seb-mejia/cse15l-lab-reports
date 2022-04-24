https://docs.google.com/document/d/14SJ2qRuxBCfOXxI1-dPo3KTOvd4bmM0K25GyVtfXLrU/edit

## Code change 1:

**Code change diff:**

![diff 1](https://user-images.githubusercontent.com/90715607/164960400-4367a775-5e8f-4909-9a6c-48b4eb565db8.PNG)

**Failure-inducing input:**

https://github.com/TheSeb72/markdown-parser/blob/main/far%20apart.md

**Symptom:**

![OutOfMemoryError](https://user-images.githubusercontent.com/90715607/164957021-ec8d6fb6-a2c4-4034-9f63-0c4f362637f3.PNG)

**Explanation:**

In the original code, we always add the characters (the website) between the parentheses () to toReturn, and set currentIndex to the character after the parentheses. However, in the fixed code, we only add the website if the parentheses DIRECTLY FOLLOW the brackets. If the parentheses do not directly follow the brackets, then we simply increase the current index ```currentIndex++;``` until the parentheses are reached. Otherwise, the code is gonna keep endlessly searching and adding websites until a memory error is caused.

## Code change 2:

**Code change diff:**

![diff 2](https://user-images.githubusercontent.com/90715607/165000513-d76891b4-e738-4920-87c9-752f06664ad8.PNG)

**Failure-inducing input:**

https://github.com/TheSeb72/markdown-parser/blob/main/Image%20reference

**Symptom:**

![Symptom 2](https://user-images.githubusercontent.com/90715607/165000402-14dbb760-a15d-4250-80f1-2dbf8f3fe3c9.PNG)

**Explanation:**

Although this is an image reference, the code is treating it like it's a website just because there are parentheses and brackets. We know that an image reference begins with "!", so we can set a condition preventing image references being read. Simply check that there is no "!" before the instance of an open bracket.

## Code change 3:

**Code change diff:**
