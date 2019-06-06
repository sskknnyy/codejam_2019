## Dat Bae(14점, 20점)

#### Problem

연구 컨소시엄은 새로운 데이터 센터를 위해 새로운 데이터베이스 시스템을 구축했습니다.  
데이터베이스는 하나의 마스터 컴퓨터와 N 개의 worker 컴퓨터로 구성되며 0에서 N-1 까지 ID가 부여 됩니다.    
각 worker는 정확하게 1비트의 정보를 저장합니다. 이는 다소 낭비처럼 보입니다만, 이것은 매우 중요한 데이터입니다!

당신은 데이터베이스에 대한 다음의 절차을 평가하기 위해 고용되었습니다:

* TEST_STORE <bits>: The master reads in <bits>, which is a string of N bits, and sends the i-th bit to the i-th worker for storage. 
  
* TEST_STORE<bits> : 마스터는 N 비트 의 문자열 인 <bits>를 읽고 i 번째 비트를 i 번째 worker에게 저장용으로 보냅니다.
The master will then read the bits back from the workers and return them to the user, in the same order in which they were read in. 
그런 다음 마스터는 worker로부터 비트를 읽어 들이고 읽은 순서대로 사용자에게 반환합니다.

During normal operation, TEST_STORE should return the same string of bits that it read in, but unfortunately, B of the workers are broken!
정상적인 동작 중에 TEST_STORE는 읽는 비트와 동일한 문자열을 반환해야 하지만 불행히도 B 의 worker는 고장납니다!

The broken workers are correctly able to store the bits given to them, but whenever the master tries to read from a broken worker, no bit is returned. 
This causes the TEST_STORE operation to return only N-B bits, which are the bits stored on the non-broken workers (in ascending order of their IDs). 
For example, suppose N = 5 and the 0th and 3rd workers are broken (so B = 2). Then:
고장난 worker는 주어진 비트를 올바르게 저장할 수 있지만 마스터가 깨진 worker로부터 읽으려고 할 때마다 비트가 반환되지 않습니다. 
이로 인해 TEST_STORE작업은 N - B 비트만 반환합니다. 이 비트는 손상되지 않은 작업자에 저장된 비트 (해당 ID의 오름차순)입니다. 
예를 들어, N = 5이고 0 번째 및 3 번째 작업자가 파손되었다고 가정합니다 ( B = 2). 그때:

* TEST_STORE 01101 는 111을 리턴합니다.
* TEST_STORE 00110 은 010을 리턴합니다.
* TEST_STORE 01010 은 100을 리턴합니다.
* TEST_STORE 11010 또한 100을 리턴합니다.  

 
보안상의 이유로 데이터베이스는 지하 산악 도로에 숨겨져있어 TEST_STORE에 요청하는 것은 매우 오랜 시간이 걸립니다. 
당신은 최대 F만큼 TEST_STORE에 call 하여 어떤 worker가 고장 났는지 찾아내는 임무를 맡았습니다 .

#### Input and output  

이는 interactive 문제입니다. 우리의 FAQ에 있는 Interactive Problems 섹션에서 정보를 읽었는지 확인해야 합니다.  

처음에 프로그램은 테스트 케이스의 수를 나타내는 단일 정수 T 를 포함하는 단일 행을 읽어야 합니다.   
그런 다음 T 테스트 케이스 를 처리해야합니다.  

각 테스트 케이스에 대해 프로그램은 먼저 세 개의 정수 N , B , F가 포함된 한 줄을 읽습니다. 이 줄 에는 worker 수, 고장난 worker 수, 보낼 줄 수 (아래 설명 참조)가 표시됩니다.

Then you may send the judge up to F lines, each containing a string of exactly N characters, each either 0 or 1. Each time you send a line, the judge will check that you have not made more than F calls. If you have, the judge will send you a single line containing a single -1, and then finish all communication and wait for your program to finish. Otherwise, the judge will send a string of length N-B: the string returned by TEST_STORE, as described above.
그런 다음에 판사를 보낼 수 F의 각 정확히의 문자열을 포함하는 라인 N의 두 문자, 각각 0또는 1. 전화를 할 때마다 판사는 F 이상의 전화를 하지 않았는지 확인 합니다. 소지하고 계시다면 판사가 단일 전화 번호를 포함한 한 줄을 보내고 -1모든 통신을 끝내고 프로그램이 끝날 때까지 기다리십시오. 그렇지 않으면, 판사는 길이 N - B 의 문자열을 보낸다 : TEST_STORE위에 기술 된 바와 같이 반환 된 문자열 .

Once your program knows the index of the B broken workers, it can finish the test case by sending B space-separated integers: the IDs of the broken workers, in sorted order. This does not count as one of your F calls.
프로그램이 B 실업 상태의 근로자 의 지수를 알고 나면 B 공백으로 구분 된 정수 (부서진 근로자의 ID)를 정렬 된 순서 로 전송하여 테스트 사례를 완료 할 수 있습니다 . 이것은 F 콜 중 하나로 간주되지 않습니다 .

If the B integers are not exactly the IDs of the B broken workers, you will receive a Wrong Answer verdict, and the judge will send a single line containing -1, and then no additional communication. If your answer was correct, the judge will send a single line with 1, followed by the line that begins the next test case (or exit, if that was the last test case).
경우 B의 정수가 정확히의 ID가없는 B 깨진 노동자, 당신은 오답 판결을받을 것이며, 판사가 포함 된 한 줄 보내드립니다 -1한 다음 추가 통신. 답이 맞다면 판사는 한 줄을 보내고 1다음 테스트 케이스를 시작하는 라인 (또는 마지막 테스트 케이스 인 경우 종료) 을 보낸다 .

#### Limits  
시간 제한: 테스트셋당 20초.  
메모리 제한: 1GB.  
1 ≤ T ≤ 100.  
2 ≤ N ≤ 1024.  
1 ≤ B ≤ min(15, N-1).  

#### Test set 1 (Visible)  
F = 10.  
#### Test set 2 (Hidden)  
F = 5.  

#### Testing Tool  

이 테스트 도구를 사용하여 로컬 또는 서버에서 테스트 할 수 있습니다. 
로컬에서 테스트하려면 코드와 함께 도구를 실행해야합니다. 
당신은 우리의 인터랙티브 러너 를 사용할 수 있습니다 . 
자세한 내용은 FAQ 의 Interactive Problems 섹션을 참조하세요.

#### Local Testing Tool  

보다 나은 로컬 테스팅이 가능하도록 우리는 아래와 같은 스크립트를 제공합니다. 
설명은 내부에 포함되어 있습니다. 
더 나은 테스팅을 위해 더 많은 테스트 케이스를 추가하는 것이 좋습니다.
테스트 도구는 평가 시스템을 시뮬레이션하기 위한 것이지만 실제 판단 시스템 은 아니며 다르게 작동 할 수도 있습니다.  
당신의 코드가 테스트 도구를 통과했지만 실제 평가에서 실패한다면 여기에서 우리와 동일한 컴파일러를 사용하고 있는지 확인하세요.

Download testing_tool.py

#### Sample Interaction
The following interaction meets the limits for Test set 1.  
아래의 인터렉션은 테스트 세트 1의 한계를 충족시킵니다.

  t = readline_int()           // Reads 2 into t  
  n, b, f = readline_int_list()  // Reads 5, 2, 10 into n, b, f  
  printline 01101 to stdout    // The next four outputs match the example in  
                               // the problem statement.  
  flush stdout  
  response = readline_str()    // Reads 111 into response. (At this point, we  
                               // could determine the answer; the remaining  
                               // queries are just examples!)  
  printline 00110 to stdout  
  flush stdout  
  response = readline_str()    // Reads 010 into response  
  printline 01010 to stdout  
  flush stdout  
  response = readline_str()    // Reads 100 into response  
  printline 11010 to stdout  
  flush stdout  
  response = readline_str()    // Reads 100 into response  
  printline 0 3 to stdout      // Guesses the answer. Notice that we were  
                               // not required to use all 10 of our allowed  
                               // queries.  
  flush stdout  
  verdict = readline_int()     // Reads 1 into verdict. We got that test case  
                               // right!  
  n, b, f = readline_int_list()  // Reads 2, 1, 10 into n, b, f.  
  printline 01 to stdout       // 01 is a query, not a guess at the final  
                               // answer (if we wanted to guess that just  
                               // worker 1 were broken, we would have to  
                               // send 1 as we do below)  
  flush stdout  
  response = readline_str()    // Reads 1 into response.  
  printline 1 to stdout        // Makes a (bad) wild guess.  
  verdict = readline_str()     // Reads -1 into verdict.  
  exit                         // exits to avoid an ambiguous TLE error  