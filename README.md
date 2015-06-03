# quine-relay-compose
[Quine relay](https://github.com/mame/quine-relay) implemented with a network ring of Docker containers.
Based one the work of [David Gageot] (https://github.com/dgageot/quine-relay)
He uses kubernets. I addapted it to docker compose. 
Do to it's setup (exposing ports or better the lack of it) it only works 
out of the box on [Joyent Triton/ SDC-Docker] (https://www.joyent.com/developers/triton-faq)

spawn all docker containers:

docker-compose up. (go play a table top gome. Takes a while to spawn all the containers.)

Note: For Coal and probably trinton you need to set DOCKER_TSL_VERIFIY=1 otherwise compose does not talk to the remote docker.)

When done docker-compose multiplexes all docker logs so you can watch what goes on in each container.

So get your IP for the ruby container (Only one with a port exported: 8080)

Get that think going:

curl --data-binary @QR.rb http://(ruby_exported_ip):8080/run/ruby

Watch docker-compose output:
```
ruby_1       | ========================================
ruby_1       | ruby
ruby_1       | ruby QR.rb > QR.scala
ruby_1       | 151484
ruby_1       | http://scala:8080/run/scala
scala_1      | ========================================
scala_1      | scala
scala_1      | scalac QR.scala && scala QR > QR.scm
scala_1      | 93710
scala_1      | http://scheme:8080/run/scheme
scheme_1     | ========================================
scheme_1     | scheme
scheme_1     | gosh QR.scm > QR.sci
scheme_1     | 64816
scheme_1     | http://scilab:8080/run/scilab
scilab_1     | ========================================
scilab_1     | scilab
scilab_1     | scilab -nw -nb -f QR.sci > QR.bash
scilab_1     | 63434
scilab_1     | http://shell:8080/run/shell
shell_1      | ========================================
shell_1      | shell
shell_1      | bash QR.bash > QR.sl
shell_1      | 55342
shell_1      | http://slang:8080/run/slang
slang_1      | ========================================
slang_1      | slang
slang_1      | slsh QR.sl > QR.st
slang_1      | 42357
slang_1      | http://smalltalk:8080/run/smalltalk
smalltalk_1  | ========================================
smalltalk_1  | smalltalk
smalltalk_1  | gst QR.st > QR.spl
smalltalk_1  | 42285
smalltalk_1  | http://spl:8080/run/spl
spl_1        | ========================================
spl_1        | spl
spl_1        | splrun QR.spl > QR.sml
spl_1        | 38754
spl_1        | http://ml:8080/run/ml
ml_1         | ========================================
ml_1         | ml
ml_1         | mlton @MLton fixed-heap 200M -- QR.sml && ./QR > QR.sq
ml_1         | 310099
ml_1         | http://subleq:8080/run/subleq
subleq_1     | ========================================
subleq_1     | subleq
subleq_1     | ruby vendor/subleq.rb QR.sq > QR.tcl
subleq_1     | 36894
subleq_1     | http://tcl:8080/run/tcl
tcl_1        | ========================================
tcl_1        | tcl
tcl_1        | tclsh QR.tcl > QR.t
tcl_1        | 196678
tcl_1        | http://thue:8080/run/thue
thue_1       | ========================================
thue_1       | thue
thue_1       | ruby vendor/thue.rb QR.t > QR.unl
thue_1       | 196666
thue_1       | http://unlambda:8080/run/unlambda
unlambda_1   | ========================================
unlambda_1   | unlambda
unlambda_1   | ruby vendor/unlambda.rb QR.unl > QR.vala
unlambda_1   | 65555
unlambda_1   | http://vala:8080/run/vala
vala_1       | ========================================
vala_1       | vala
vala_1       | valac QR.vala && ./QR > QR.v
vala_1       | 46444
vala_1       | http://verilog:8080/run/verilog
verilog_1    | ========================================
verilog_1    | verilog
verilog_1    | iverilog -o QR QR.v && ./QR -vcd-none > QR.vb
verilog_1    | 36116
verilog_1    | http://vbasic:8080/run/vbasic
vbasic_1     | ========================================
vbasic_1     | vbasic
vbasic_1     | vbnc QR.vb && mono ./QR.exe > QR.ws
vbasic_1     | 570163
vbasic_1     | http://whitespace:8080/run/whitespace
whitespace_1 | ========================================
whitespace_1 | whitespace
whitespace_1 | ruby vendor/whitespace.rb QR.ws > QR.xslt
whitespace_1 | 35635
whitespace_1 | http://xslt:8080/run/xslt
xslt_1       | ========================================
xslt_1       | xslt
xslt_1       | xsltproc QR.xslt > QR.yorick
xslt_1       | 35392
xslt_1       | http://yorick:8080/run/yorick
yorick_1     | ========================================
yorick_1     | yorick
yorick_1     | yorick -batch QR.yorick > QR.azm
yorick_1     | 30784
yorick_1     | http://zoem:8080/run/zoem
zoem_1       | ========================================
zoem_1       | zoem
zoem_1       | zoem -i QR.azm > QR.+
zoem_1       | 28267
zoem_1       | http://aplus:8080/run/aplus
aplus_1      | ========================================
aplus_1      | aplus
aplus_1      | a+ QR.+ > qr.adb
aplus_1      | 27225
aplus_1      | http://ada:8080/run/ada
ada_1        | ========================================
ada_1        | ada
ada_1        | gnatmake qr.adb && ./qr > QR.als
ada_1        | 27047
ada_1        | http://afnix:8080/run/afnix
afnix_1      | ========================================
afnix_1      | afnix
afnix_1      | axi QR.als > QR.a68
afnix_1      | 26582
afnix_1      | http://algol68:8080/run/algol68
algol68_1    | ========================================
algol68_1    | algol68
algol68_1    | a68g QR.a68 > QR.ante
algol68_1    | 948817
algol68_1    | http://ante:8080/run/ante
ante_1       | ========================================
ante_1       | ante
ante_1       | ruby vendor/ante.rb QR.ante > QR.asy
ante_1       | 26356
ante_1       | http://asymptote:8080/run/asymptote
asymptote_1  | ========================================
asymptote_1  | asymptote
asymptote_1  | asy QR.asy > QR.dats
asymptote_1  | 26130
asymptote_1  | http://ats:8080/run/ats
ats_1        | ========================================
ats_1        | ats
ats_1        | atscc -o QR QR.dats && ./QR > QR.awk
ats_1        | 26013
ats_1        | http://awk:8080/run/awk
awk_1        | ========================================
awk_1        | awk
awk_1        | awk -f QR.awk > QR.bc
awk_1        | 188328
awk_1        | http://bc:8080/run/bc
bc_1         | ========================================
bc_1         | bc
bc_1         | BC_LINE_LENGTH=4000000 bc -q QR.bc > QR.bef
bc_1         | 2067776
bc_1         | http://befunge:8080/run/befunge
befunge_1    | ========================================
befunge_1    | befunge
befunge_1    | cfunge QR.bef > QR.Blc
befunge_1    | 694848
befunge_1    | http://blc8:8080/run/blc8
blc8_1       | ========================================
blc8_1       | blc8
blc8_1       | ruby vendor/blc.rb < QR.Blc > QR.boo
blc8_1       | 25735
blc8_1       | http://boo:8080/run/boo
boo_1        | ========================================
boo_1        | boo
boo_1        | booi QR.boo > QR.bf
boo_1        | 1155217
boo_1        | http://brainfuck:8080/run/brainfuck
brainfuck_1  | ========================================
brainfuck_1  | brainfuck
brainfuck_1  | bf QR.bf > QR.c
brainfuck_1  | 63537
brainfuck_1  | http://c:8080/run/c
c_1          | ========================================
c_1          | c
c_1          | gcc -o QR QR.c && ./QR > QR.cpp
c_1          | 47325
c_1          | http://cpp:8080/run/cpp
c_1          | [Worker: RequestDispatcher: Thread-12] ERROR Fluent - Unable to apply route
```
I did not spwan all 100 quine containers so it stops here as the next container is not running.





