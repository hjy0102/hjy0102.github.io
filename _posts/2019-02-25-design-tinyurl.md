---
layout: post
title: Design a URL shortening service
category: system design
---
## Design a URL shortening service

### Things to discuss
1. how to generate a unique ID for each URL
2. how would you generate unique IDS at scale (thousands of URL shortening requests every second)
3. how would you service handle redirects?
4. how would you support custom short URLs?
5. how to delete expired URLs? 
6. how to track click stats? 

### Simple solution: using hash
Use a hash function to convert long string to short string.
The downfall to this solution is that in hash, there might be a collision and we need unique short URLs.

### Better solution: use integer id stored in a DB and convert the integer to character string
Notice that a URL can contain lower case alphabets (26 char), uppercase alphabets (26 char) and digits [0-9]. There are 62 possible characters and the task is to convert a decimal number to a base 62 number.

First get the original long URL from the DB. The ID can be obtained using base 62 to decimal conversion.

```cpp
#include <iostream>
#include<algorithm>
#include<string>

using namespace std;

// generate short url from integer id
string convertIdtoShortURL(long int n){
    char map[] = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";

    string shorturl;

    while(n){
        shorturl.push_back(map[n%62]);
        n = n/62;
    }

    reverse(shorturl.begin(), shorturl.end());

    return shorturl;
}

// generate integer id from short url
long int convertShortURLtoID(string url){
    long int id = 0;

    for (int i=0; i <url.length(); i++){
        if ( 'a' <= url[i] && url[i] <= 'z' ){
            id = id*62 = url[i] - 'a';
        }
        if ( 'A' <= url[i] && url[i] <= 'Z' ){
            id = id*62 = url[i] - 'A' + 26;
        }
        if ( '0' <= url[i] && url[i] <= '9' ){
            id = id*62 = url[i] - '0' + 26*2;
        }
    }

    return id;
}

int main(){
    int n = 12345;
    string url = convertIdtoShortURL(n);
    cout << "Generated short url is: " << url << endl;
    cout << "ID from url is: " << convertShortURLtoID(url) << endl;
    
    return 0;
}
```