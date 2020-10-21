# An Unfortunate Encounter Involving freopen
### By [Shane "Treasure" Xue](https://smits-society.github.io/contributors/shane-xue)

The other day I wrote a short piece of code to implement the prime numbers sieve. It was not a particularly efficient piece of code, but it was good enough.

However, I encountered a problem when I tried to write the numbers into a txt file with C library I/O facilities. It seemed that the notepad could not interpret the encoding, yielding unreadable text.

This is the code:

```cpp
#include <iostream>
#include <cmath>
#include <vector>
#include <cstdlib>
#include <cstdio>
using namespace std;

//#define ULL unsigned long long int;
//#define U unsigned;

const unsigned long long int MAX = 100000;
bool siever[MAX] = {0};
//vector<unsigned long long int> primes;

template<typename IntTp>
bool isprime(IntTp a) {
    if (a % 2 ==0){
        if (a == 2) return true;
            else return false;
                }
            if (a == 1) return false;
            int sra = sqrt(a);
            for (int i = 2; i <= sra; i++) {
                if (a % i == 0) return false;
            }
            return true;
        }

void sieve(void){
	for(unsigned i = 2 ; i < MAX ; i++){
		if(siever[i] == (false)) {
			//primes.push_back(i);
			//if(!isprime(i)) printf("%d is not a prime!\n",i);
			//else 
			printf("%d ",i);
			//cout<<i<<" ";
        }
		for(unsigned kill = 2 * i ; kill <= MAX ; kill += i){
			siever[kill]=true;
		}
	}
}


int main (){
	freopen("prime_numbers.txt","w",stdout);
    sieve();
    //system("pause");
    return 0;
}

```

So what I did was I opened the file with sublime text. It was readable. I happened to have noticed that Sublime could decipher all kinds of encoding, so I quickly figured out that if I could change the encoding, one way or the other, I could get I file that is readable by the human.

But what encoding _did_ I have? After some research I figured out that, because my system language was Chinese, the encoding was obviously Chinese too.

So I used the "chcp" directive (a system directive) to change the active code page. This is the code:

```cpp
#include <iostream>
#include <cmath>
#include <vector>
#include <cstdlib>
#include <cstdio>
using namespace std;

//#define ULL unsigned long long int;
//#define U unsigned;

const unsigned long long int MAX = 100000;
bool siever[MAX] = {0};
//vector<unsigned long long int> primes;

template<typename IntTp>
bool isprime(IntTp a) {
    if (a % 2 ==0){
        if (a == 2) return true;
            else return false;
                }
            if (a == 1) return false;
            int sra = sqrt(a);
            for (int i = 2; i <= sra; i++) {
                if (a % i == 0) return false;
            }
            return true;
        }

void sieve(void){
	for(unsigned i = 2 ; i < MAX ; i++){
		if(siever[i] == (false)) {
			//primes.push_back(i);
			//if(!isprime(i)) printf("%d is not a prime!\n",i);
			//else 
			printf("%d ",i);
			//cout<<i<<" ";
        }
		for(unsigned kill = 2 * i ; kill <= MAX ; kill += i){
			siever[kill]=true;
		}
	}
}


int main (){
    system("chcp 65001"); //Vital line: changes active encoding to UTF-8
	  freopen("prime_numbers.txt","w",stdout);
    sieve();
    //system("pause");
    return 0;
}

```

The result was fairly good; at least it gave me something that I could read. However, the problems of this solution is also fairly noticable: it changes the configuration of _all_ programs that might be run through cmd. This may cause unexpected mistakes--though it usually doesn't. However, it's biggest limitation was that it also printed "active code page number" into the txt file. Solving this would not be too hard for me; all I have to do is to slow the stream of control down a bit, possibilly using sleeping facilities or letting the line of control do some easy calculating.

I have also used fstreams to do the work, and bad encoding did not occur. However, c programers or those who are used to using freopen() and do not have very limited time can still choose to apply this solution.
