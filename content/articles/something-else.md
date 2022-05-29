---
author:
    name: Hamza Mogni

title: Data salaries at FAANG companies in 2022
description: Salary is a sensitive topic. Should it be? There are a lot of good reasons why salaries should be transparent
img: https://miro.medium.com/max/700/1*kIP5PxDTogpvm_AMdPwaFQ.png
alt: something else article
---

# Overview

Given a string `path`, which is an **absolute path** (starting with a slash `'/'`) to a file or directory in a Unix-style file system, convert it to the simplified **canonical path**.

In a Unix-style file system, a period `'.'` refers to the current directory, a double period `'..'` refers to the directory up a level, and any multiple consecutive slashes (i.e. `'//'`) are treated as a single slash `'/'`. For this problem, any other format of periods such as `'...'` are treated as file/directory names.

The **canonical path** should have the following format:

- The path starts with a single slash `'/'`.
- Any two directories are separated by a single slash `'/'`.
- The path does not end with a trailing `'/'`.
- The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period `'.'` or double period `'..'`)

Return *the simplified **canonical path***.

**Example 1:**

```
Input: path = "/home/"
Output: "/home"
Explanation: Note that there is no trailing slash after the last directory name.

```

**Example 2:**

```
Input: path = "/../"
Output: "/"
Explanation: Going one level up from the root directory is a no-op, as the root level is the highest level you can go.

```

**Example 3:**

```
Input: path = "/home//foo/"
Output: "/home/foo"
Explanation: In the canonical path, multiple consecutive slashes are replaced by a single one.

```

**Constraints:**

- `1 <= path.length <= 3000`
- `path` consists of English letters, digits, period `'.'`, slash `'/'` or `'_'`.
- `path` is a valid absolute Unix path.

# Solution

```cpp
		/**
     *  We parse the path by character, 
     *  each time we find a baslash
     *  we decide what to do according
     *  to the rules.
     * 
     *  Complexity:
     *      Time: o(n)
     *      Space: o(n)
     **/
    string simplifyPath(string path) {
        vector<string> parsedParts;

        string tmp = "",
                final = "";

        path += "/";

        // We split input path by the "/" character
        for (char chr: path) {
            if (chr == '/') {
                if (tmp == "." || tmp == "") {
                    tmp = "";
                } else if (tmp == "..") {
                    if (parsedParts.size()) {
                        parsedParts.pop_back();
                    }
                } else {
                    parsedParts.push_back(tmp);
                }
                
                tmp = "";
            } else {
                tmp += chr;
            }
        }

        // if we end up with empty path
        // then we are at the root of
        // our filesystem
        if (!parsedParts.size()) {
            return "/";
        }

        // we assemble the resolved path
        // and return it
        for (string part: parsedParts) {
            final += "/" + part;
        }
        return final;
    }
```
