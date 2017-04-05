---
layout: post
title: "CTCI Questions 1.1 (Array and Strings)"
date: 2017-04-03 17:10:00
author: SungHoon Ko
categories: CTCI
tags: ctci algorithm ch1
---

### 1.1 Implement an algorithm to determine if a string has all unique characters. What if you cannot use additional data structures?

#### 1.1 문자열에 포함된 문자들이 전부 유일한지를 검사하는 알고리즘을 구현하라. 다른 자료구조를 사용할 수 없는 상황이라면 어떻게 하겠는가?

첫번째 문제 풀이

처음에는 문제가 의도하는게 뭔지 감도 오지 않았다.
시작이 반이라고 했던가...
그래도 이렇게 시작했으니 150 문제 모두 잘 풀어 보았으면 좋겠다.
한가지 명심할 것은 절대로 답을 미리 보면 안된다.
이번 첫 번째 문제가 그랬는데, 해결법을 보고나니 그 프레임에서 벗어나질 못한다.
결국 문제를 푸는 핵심 가치인 생각해서 해결하는 능력이 현저히 떨어진다.

본 문제는 오로지 해답을 찾는 것에만 집중했다.
시간/공간 성능은 고려하지 않았으며, 문자열은 ASCII Code 로만 한정 했다.

{% highlight C++ %}
// 전달된 문자열은 ASCII 코드라고 가정 한다.
bool is_unique_string(const char* str, int len)
{
    // 문자열의 길이가 255 (ASCII) 를 초과 하면 중복된 문자가 포함되어 있다
    if (len > 255)
        return false;

    bool check_unique[256];
    for (int i = 0; i < 256; i++) {
        check_unique[i] = false;
    }

    for (int i = 0; i < len; i++) {
        unsigned char ch = str[i];
        if (check_unique[ch]) {
            return false;
        }

        check_unique[ch] = true;
    }

    return true;
}

int main() {
    string mystr;

    cout << "Input ASCII code : ";
    getline(cin, mystr);
    cout << endl;

    bool result = is_unique_string(mystr.c_str(), mystr.length());
    cout << (result ? "All string is unique!!" : "Not unique...");

    cout << endl;

    return 0;
}
{% endhighlight %}
