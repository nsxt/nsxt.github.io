---
layout: post
title: "CTCI Questions 1.2 (Array and Strings)"
date: 2017-04-04 19:17:00
author: SungHoon Ko
categories: CTCI
tags: ctci algorithm ch1
---

### 1.2 Implement a function void reverse(char* str) in C or C++ which reverses a null-terminated string.

#### 1.2 널 문자로 끝나는 문자열을 뒤집는 reverse(char* str) 함수를 C 나 C++ 로 구현하라.

문제 해결하고 코딩하고 테스트 까지 모두 대략 30분 정도 소요되었다.

뒤집는 문자열중 Null 문자까지 뒤집는 바람에 Null 문자가 가장 앞에 위치하는 버그를 수정했다.
그리고 new 동적 할당 받은 임시 버퍼를 삭제하지 않아 Memory Leak 이 발생하여 수정 하였다.

현재의 구현으로는 새로운 버퍼를 생성하여 사용하고 있는데, 전달된 문자열 버퍼와 임시 변수로 추가 메모리 할당 없이 문자열을 뒤집는 방법도 있다. 일단 문제 해결방법에 대한 나의 접근법과 생각을 기록하고 해답과 비교해야 되겠다.

현재는 꾸준한 문제 풀기와 고민을 통해서 생각을 코드로 쏟아내는것에 적응 하는 것이 최우선 목표이다.

`꾸준히 하다 보면 편해지고 편해지면 또 흥미도 올라가는 법이다.`

- reverse 함수 구현
{% highlight C++ %}
void reverse(char* str) {
    if (str == nullptr) return;

    // 문자열의 길이를 알아낸다.
    int str_len = 0;
    do {
        if (str[str_len++] == '\0') break;
    } while (1);

    if (str_len <= 1) return;

    char* temp_str = new char[str_len];

    // null 문자는 뒤집기 대상에서 제외
    str_len--;
    for (int i = 0, j = str_len - 1; i < str_len; i++, j--) {
        temp_str[i] = str[j];
    }

    memcpy(str, temp_str, str_len);

    // 최종적으로 null 문자 삽입
    str[str_len] = '\0';

    delete[] temp_str;
}
{% endhighlight %}


- main 함수
{% highlight C++ %}
int main() {
    string mystr;
    cout << "Input strings : ";
    getline(cin, mystr);
    cout << endl;

    // 입력받은 문자열을 정적 배열로 복사
    // 문자열의 길이는 ASCII 문자 80 개로 제한 한다.
    char arr_str[80];
    memset(arr_str, 0, sizeof(char) * 80);

    memcpy(arr_str, mystr.c_str(), mystr.length());
    reverse(arr_str);

    cout << "Result : " << arr_str;

    return 0;
}
{% endhighlight %}


- 실행결과
{% highlight Markdown %}
Input strings : 123456789ABCDEFGH
Result : HGFEDCBA987654321
{% endhighlight %}
