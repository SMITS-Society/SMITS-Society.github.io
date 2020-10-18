#An Unfortunate Encounter Involving freopen



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
    system("chcp 65001");
	  freopen("prime_numbers.txt","w",stdout);
    sieve();
    //system("pause");
    return 0;
}

```
