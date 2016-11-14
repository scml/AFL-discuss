# AFL-parcticeAFL 

http://lcamtuf.coredump.cx/afl/
這是AFL的正式網站

http://lcamtuf.coredump.cx/afl/QuickStartGuide.txt
http://lcamtuf.coredump.cx/afl/README.txt
Quick start guide

反正抓下AFL後就先編譯，或是用apt-get install(brew install)

3) Instrumenting programs for use with AFL
有source code的情況，然後對要檢查的c code做編譯，但需要用afp-gcc編譯。
$ cd c-code資料夾
$ CC=/path/to/afl/afl-gcc ./configure
$ make clean all

4) Instrumenting binary-only apps
如果是只有binary的情況（我還沒用過）
$ cd qemu_mode
$ ./build_qemu_support.sh

6) Fuzzing binaries
開始fuzzing
$  ./afl-fuzz -i testcase_dir -o findings_dir /path/to/program [...params...]

testcase 這是我最搞不懂的地方，我知道是放要fuzz的城市可以吃的input。但詳細是怎麼樣，還是一個謎對我來說。

7) Interpreting output
findings_dir(AFL output)
裡面有三個主要資料夾分別為
- queue/(每一個testcsse，然後跑每依次路徑的結果) - test cases for every distinctive execution path, plus all the
               starting files given by the user. This is the synthesized corpus
               mentioned in section 2.

               Before using this corpus for any other purposes, you can shrink
               it to a smaller size using the afl-cmin tool. The tool will find
               a smaller subset of files offering equivalent edge coverage.


  - crashes/ （造成crash的情況）- unique test cases that cause the tested program to receive a
               fatal signal (e.g., SIGSEGV, SIGILL, SIGABRT). The entries are 
               grouped by the received signal.

  - hangs/  （每一個test case，造成程式timeout） - unique test cases that cause the tested program to time out. Note
               that when default (aggressive) timeout settings are in effect,
               this can be slightly noisy due to latency spikes and other
               natural phenomena.

10) Crash triage
	我搞不太懂，這要去做什麼。反正是分析crash的步驟


https://www.evilsocket.net/2015/04/30/fuzzing-with-afl-fuzz-a-practical-example-afl-vs-binutils/
http://blog.csdn.net/youkawa/article/details/45696317
用了binutils來做fuzz，但我跟那個大陸人一樣，跑了抄久都沒有出現crash。
但是Simone在做的時候有出現錯誤，他也有將output貼出來，但我但不懂。



https://www.youtube.com/watch?v=Gh953wrJLjc
這個youtube的教學一分多鐘，有寫了一個簡單的c來做測試。我第一次在跑的時候有跑出crash，裡面是出現fooo這字串。
但後來又跑步出來了。


http://volatileminds.net/2015/06/29/basic-afl-usage.html
這用來用cap檔來當testcase，來測試tcpdump。但我個人是沒有實作。

http://www.floyd.ch/?cat=152
http://floyd.ch/download/introduction-fuzzing-with-afl.pdf
這人有講一個afl的speak，算是蠻清楚的啦。
對libtiff做fuzz。 我在afl的網站上找了一堆bmp的檔案來當testcase(http://lcamtuf.coredump.cx/afl/demo/) 我這次有用到afl-cmin(curpos mininize吧)把原本很多檔案挑到只剩6個，但真正跑的時候只有三個可以用。
總之，我又沒有跑出crash了。
但你可以對這個看一下，裡面的東西講的算蠻清楚。但說真的我到後來不知道他在做什麼，希望你能看懂。

https://spin.atomicobject.com/2015/08/23/fuzz-testing-american-fuzzy-lop/
這可以看看，但我沒有做。

https://github.com/tomviner/afl-fuzzing-demos （py-afl-fuzz)
這是你有傳給我的網站，我之前有也看過。
用法跟一般的afl-fuzz差不多，但是要在code裡面加上，
import afl
afl.start()

然後用py-afl-fuzz 取代 afl-fuzz:
$ py-afl-fuzz [options] -- /path/to/fuzzed/python/script [...]compound
/python-afl/py-afl-fuzz  -i json/afl_testcases/ -o /run/shm/json/afl_findings -- python json/demo.py

https://alexgaynor.net/2015/apr/13/introduction-to-fuzzing-in-python-with-afl/
這是我有一次問你input要放什麼的。


看來看去，大體上是這樣，其他就有一些是重复的。好像沒有很多但實際上花了蠻多時間研究來進入的（哭哭）

現在就是不知道要怎樣在深入了～.～




