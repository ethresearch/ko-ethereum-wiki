<!-- TITLE: Cryptocurrency Current Problems -->


The science of cryptography, which has existed to some degree for millennia but in a formal and systematized form for less than fifty years, can be most simply defined as the study of communication in an adversarial environment. In a similar vein, we can define cryptoeconomics as a field that goes one step further: the study of economic interaction in an adversarial environment. To distinguish itself from traditional economics, which certainly studies both economic interaction and adversaries, cryptoeconomics generally focuses on interactions that take place over network protocols. Particular domains of cryptoeconomics include:

1. オンライン上の信頼と評価のシステム
2. 暗号化されたトークンと暗号通貨と、より一般的なデジタルのアセット
3. 自動執行されるスマートコントラクト
4. コンセンサスアルゴリズム
5. アンチスパム・アンチ市民アタックのアルゴリズム
6. コンピューターのリソース売買のための利益が循環するマーケットプレイス
7. 分散形の社会福祉システム、互助システム
8. 分散形の政府(営利または非営利）

* Online trust and reputation systems
* Cryptographic tokens / cryptocurrencies, and more generally digital assets
* Self-executing "smart" contracts
* Consensus algorithms
* Anti-spam and anti-sybil attack algorithms
* Incentivized marketplaces for computational resources
* Decentralized systems for social welfare / mutual aid / basic income
* Decentralized governance (for both for-profit and non-profit entities)

The increasing prominence of cryptoeconomics in the last five years is to a large extent the result of the growth of cryptocurrencies and digital tokens, and brings a new, and interesting, dimension to cryptography. While before cryptography was, by and large, a purely computational and information-theoretic science, with strong guarantees built on security assumptions that are close to absolute, once money enters the picture the perfect world of mathematics must interact with a much more messy reality of human social structures, economic incentives, partial guarantees and known vulnerabilities that can only be mitigated, and not outright removed. While a cryptographer is used to assumptions of the form "this algorithm is guaranteed to be unbreakable provided that these underlying math problems remain hard", the world of cryptoeconomics must contend with fuzzy empirical factors such as the difficulty of collusion attacks, the relative quantity of altruistic, profit-seeking and anti-altruistic parties, the level of concentration of different kinds of resources, and in some cases even sociocultural circumstances.

In traditional applied cryptography, security assumptions tend to look something like this:

伝統的な暗号学では、セキュリティでは、これらのことを考えている。
1. 誰も 2^79以上のコンピューターステップを行うことが出来ない。

2. 

3. nをルートとして持つモジュロのコンポジットを取ることは困難であること。

4. 楕円曲線暗号のアルゴリズムの問題を2<sup>n/2</sup> 時間以上より速く解くことが出来ないこと。

1. No one can do more than 2<sup>79</sup> computational steps
2. Factoring is hard (ie. superpolynomial)
3. Taking nth roots modulo composites is hard
4. The elliptic curve discrete logarithm problem cannot be solved faster than in 2<sup>n/2</sup> time

暗号学に基づく経済では、一方で基本的なセキュリティに対しての要件に加えて:
1. どの個人も、全てのコンピュータリソースの25%以上を持って、システムを壊すことが出来ない
2. どの個人も、全ての資産の25%以上を持ってシステムを壊すことが出来ないこと。（Proof of stake)
3. ある種の保証を行うためのコンピュータリソースの総量に対して支払われるべき費用の総額が、納得できる額を遥かに超えてしまわないこと
4. 互助主義者や、間抜けものや、政治的、個人的にシステムに反対するものがいることは否定できないが、大多数のユーザーは、論理的に経済的な合理性を中心として行動するであろうこと。l
5. The number of users of a system is large, and users can appear or disappear at any time, although at least some users are persistent
6. Censorship is impossible, and any two nodes can send messages to each other relatively quickly.
7. It is trivial to generate a very large number of IP addresses, and one can purchase an unlimited amount of network bandwidth
8. Many users are anonymous, so negative reputations and debts are close to unenforceable

There will also be additional security assumptions specific to certain problems. Thus, quite often it will not even be possible to definitively say that a certain protocol is secure or insecure or that a certain problem has been solved. Rather, it will be necessary to create solutions that are optimized for particular empirical and social realities, and continue further and further optimizing them over time.


## 技術面について
## Technology

The decentralized consensus technology used in Bitcoin is impressive to a very large extent because of its simplicity. A 30-year-old problem in computer science was solved via a mechanism which is simple to implement, and so simple to understand that even some semi-technical teenagers can describe the entirety of how it works. However, at the same time the technology in its current form is very limited. The scalability in Bitcoin is very crude; the fact that every full node needs to process every transaction is a large roadblock to the future success of the platform, and a factor preventing its effective use in micropayments (arguably the one place where it is the most useful). Timestamping is flawed, and proof-of-computation algorithms are very limited in the types of computation that they can support. The fact that the original solution was so "easy", however, suggests that there is still a large opportunity to improve, and there are a number of directions in which improvement could be directed.

### 1. ブロックチェーンのスケーラビリティ

現在最も大きなブロックチェーンの問題は、
One of the largest problems facing the cryptocurrency space today is the issue of scalability. It is an often repeated claim that, while mainstream payment networks process something like 2000 transactions per second, in its current form the Bitcoin network can only process seven. On a fundamental level, this is not strictly true; simply by changing the block size limit parameter, Bitcoin can easily be made to support 70 or even 7000 transactions per second. However, if Bitcoin does get to that scale, we run into a problem: it becomes impossible for the average user to run a full node, and full nodes become relegated only to that small collection of businesses that can afford the resources. Because mining only requires the block header, even miners can (and in practice most do) mine without downloading the blockchain.

The main concern with this is trust: if there are only a few entities capable of running full nodes, then those entities can conspire and agree to give themselves a large number of additional bitcoins, and there would be no way for other users to see for themselves that a block is invalid without processing an entire block themselves. Although such a fraud may potentially be discovered after the fact, power dynamics may create a situation where the default action is to simply go along with the fraudulent chain (and authorities can create a climate of fear to support such an action) and there is a coordination problem in switching back. Thus, at the extreme, Bitcoin with 7000 transactions per second has security properties that are essentially similar to a centralized system like Paypal, whereas what we want is a system that handles 7000 TPS with the same levels of decentralization that cryptocurrency originally promised to offer.

Ideally, a blockchain design should exist that works, and has similar security properties to Bitcoin with regard to 51% attacks, that functions even if no single node processes more than `1/n` of all transactions where `n` can be scaled up to be as high as necessary, although perhaps at the cost of linearly or quadratically growing secondary inefficiencies and convergence concerns. This would allow the blockchain architecture to process an arbitrarily high number of TPS but at the same time retain the same level of decentralization that Satoshi envisioned.

**Problem**: create a blockchain design that maintains Bitcoin-like security guarantees, but where the maximum size of the most powerful node that needs to exist for the network to keep functioning is substantially sublinear in the number of transactions.

**Additional Assumptions and Requirements**:

* There exist a large number of miners in the network
* Miners may be using specialized hardware or unspecialized hardware. Specialized hardware should be assumed to be more powerful than unspecialized hardware by a large (eg. 10000) constant factor at specific tasks.
* Ordinary users will be using unspecialized hardware
* Ideally, after some number of blocks (perhaps logarithmic in the total size of the network) every transaction should require 51% of network hashpower to reverse. However, solutions where transactions can pay very small fees for a lower "level" of security are acceptable, though one should take care to avoid situations where an attacker can profit by performing one attack to reverse very many small transactions at the same time
* Ideally, the solution should work for and maintain as many properties as possible of a generalized account-based blockchain (eg. Ethereum), though solutions specific to currency, domain registrations or other specialized use caes are acceptable


### 2. タイムスタンプ


An important property that Bitcoin needs to keep is that there should be roughly one block generated every ten minutes; if a block is generated every day, the payment system becomes too slow, and if a block is generated every second there are serious centralization and network efficiency concerns that would make the consensus system essentially nonviable even assuming the absence of any attackers. To ensure this, the Bitcoin network adjusts difficulty so that if blocks are produced too quickly it becomes harder to mine a new block, and if blocks are produced too slowly it becomes easier.

However, this solution requires an important ingredient: the blockchain must be aware of time. In order to solve this problem, Bitcoin requires miners to submit a timestamp in each block, and nodes reject a block if the block's timestamp is either (i) behind the median timestamp of the previous eleven blocks, or (ii) more than 2 hours into the future, from the point of view of the node's own internal clock. This algorithm is good enough for Bitcoin, because time serves only the very limited function of regulating the block creation rate over the long term, but there are potential vulnerabilities in this approach, issues which may compound in blockchains where time plays a more important role.

**Problem**: create a distributed incentive-compatible system, whether it is an overlay on top of a blockchain or its own blockchain, which maintains the current time to high accuracy.

**Additional Assumptions and Requirements**

* All legitimate users have clocks in a normal distribution around some "real" time with standard deviation 20 seconds.
* No two nodes are more than 20 seconds apart in terms of the amount of time it takes for a message originating from one node to reach any other node.
* The solution is allowed to rely on an existing concept of "N nodes"; this would in practice be enforced with proof-of-stake or non-sybil tokens (see #9).
* The system should continuously provide a time which is within 120s (or less if possible) of the internal clock of >99% of honestly participating nodes. Note that this also implies that the system should be self-consistent to within about 190s.
* The system should exist without relying on any kind of proof-of-work.
* External systems may end up relying on this system; hence, it should remain secure against attackers controlling < 25% of nodes regardless of incentives.


### 3. ありとあらゆる Proof of Computation について

Perhaps the holy grail of the study zero-knowledge proofs is the concept of an arbitrary proof of computation: given a program P with input I, the challenge is to create a zero-knowledge proof that you ran P with input I and received output O, such that the proof can be verified quickly (ie. in polylogarithmic or ideally constant time) even if the original computation took a very large number of steps to complete. In an ideal setup, the proof would even hide the value of I, just proving that you ran P with some output with result O, and if I needs to be made public it can be embedded into the program. Such a primitive, if possible, would have massive implications for cryptocurrency:

1. ブロックチェーンのスケーラビリティは、マイナーが一連のトランザクションを含めねければ、一層簡単に解くことが出来る。
このようにして、コンピュテーションを行っているあらゆるノードにおいて、承認されなければならない。
コンピュテーションを証明するだけでなく、その証拠が新しい状態で合ったとして受け入れなければならない。
これは完全な解決策ではない、何故なら、それでもなお、データを出力する必要があるが、問題は強力な構成されたブロックよりも簡単に解決される。

1. The blockchain scalability problem would be much easier to solve. Instead of miners publishing blocks containing a list of transactions, they would be publishing a proof that they ran the blockchain state updater with some list of transactions and produced a certain output; thus, instead of transactions needing to be verified by every node in the network, they could be processed by one miner and then every other miner and user could quickly verify the proof of computation and if the proof turns out correct they would accept the new state. This is not a complete solution, because there would still be a need to transmit data, but the problem would be much easier with this powerful building block.
2. The blockchain privacy problem would be much easier to solve. The blockchain scalability solution above would hide the details behind individual transactions; it would only reveal the fact that all of them are legitimate, so transactions would be hidden from everyone but the sender and the receiver.
3. It would become computationally viable to use a Turing-complete consensus network as a generic distributed cloud computing system; if you have any computation you wanted done, you would be able to publish the program for miners and miners would be able to run the program for you and deliver the result alongside a proof of its validity.

There is a large amount of existing research on this topic, including a protocol known as "SCIP" (Succinct Computational Integrity and Privacy) that is already working in test environments, although with the limitation that a trusted third party is required to initially set up the keys; use of this prior work by both its original developers and others is encouraged.

**Problem**: create programs `POC_PROVE(P,I) -> (O,Q)` and `POC_VERIFY(P,O,Q) -> { 0, 1 }` such that `POC_PROVE` runs program `P` on input `I` and returns the program output `O` and a proof-of-computation `Q` and `POC_VERIFY` takes `P`, `O` and `Q` and outputs whether or not `Q` and `O` were legitimately produced by the `POC_PROVE` algorithm using `P`.

**Requirements And Additional Assumptions**

* The runtime of `POC_PROVE` should be in `O(n*polylog(n))` where `n` is the number of steps required to run the program.
* The runtime of `POC_VERIFY` should be either constant or logarithmic in the number of steps, and at most linear in the maximum memory usage of the program.
* The protocol should require no trusted third parties. If TTPs are required, the protocol should include a mechanism for simulating one efficiently using secure multiparty computation.


### 4. コードの不明瞭さ

どのようにシンプルに冗長に、双方のキーの暗号化のために、よくテストされたアルゴリズムに暗号化するかについては、
古くから我々は良く知ってきた。同じキーは暗号化と復号化に必要とされる場所で、そして、公開鍵暗号では、
同じ鍵は
しかしながら、他の種類の暗号化が潜在的にとても有用になりうる、しかし、現在我々は伝わる形のアルゴリズム、暗号化のためのプログラムだ。

2007年には、完璧なブラックボックスとなる暗号化が不可能であることが証明された。
ブラックボックス化されたアクセスをプログラムに対して持つことと、ブラックボックス化されたコードをプログラムに対してもつことには、違いがある。どれだけコードを難読化しようとも、難読化に対して抵抗のあるプログラムを創りあげることは出来る。
しかしながら、それは弱いレベルの難読化であり、難読化に対して区別ができるかどうか0としてを定義するのであれば、
もし同じインプットとアウトプットを持つプログラムが有るならば、0(A) = P と O(B)= Q であり、何もコンピューターリソースとして、
外部の世界のでのアクセスなしに
PがAから来たのかBから北のかを分かることは出来ない。

このような難読化の形式はより一層制限されているように見えるかもしれない、しかしながら多くのアプリケーションにとっては十分である。
発見的な引数について、

**問題**: 合理的に十分である難読化のアルゴリズムを作成することが難しいこと
**追加の前提と必要条件** 
* 2^80以上のランタイムが必要とされる
* アルゴリズムは、標準的な楕円曲線暗号化、もしくは10^8のコンピュテーションパワーに耐えうるAESの暗号化


For many years now we have known how to encrypt data. Simple, robust and well-tested algorithms exist for both symmetric key encryption, where the same key is needed to encrypt and decrypt, and public key encryption, where the encryption key and decryption key are different and one cannot be derived from the other. However, there is another kind of encryption that can potentially be very useful, but for which we currently have no viable algorithm: the encryption of programs. The holy grail is to create an obfuscator `O`, such that given any program P the obfuscator can produce a second program `O(P) = Q` such that `P` and `Q` return the same output if given the same input and, importantly, `Q` reveals no information whatsoever about the internals of `P`. One can hide inside of `Q` a password, a secret encryption key, or one can simply use `Q` to hide the proprietary workings of the algorithm itself.

## 5 Hash-Based Cryptography

現在、量子コンピュータは余りにも実現困難であるようにも見えなくなってきている。
全ての量子コンピューターもしくは"断熱型の量子コンピューター",は、
極端に限られたプログラムを極めて速い速度で解くことを得意としている。
しかしながら、起こりにくいこととはいえ、米軍は既に量子コンピューターを手に入れているかもしれない。
耐量子暗号化を目指す事が幾分高い優先度を持つと考えられる。

これまでは、全ての格子上の構造を必要とする有るごリムは、
個々のメンバーの長さよりも、合計がとても短く
しかしながら、その他のアルゴリズムは耐量子性がある、ハッシュのアルゴリズムだ
古典的なLANポート署名では164 nodes のマークルツリーを作成し、ルートを出版する。そしてハッシュの文書に基づいて選ばれた匿名の82 nodes のマークルツリーの証明を結合させる。
この署名は、一回の処理でｍバルク処理である。

ここでの疑問は、より良い方法はないだろうかということだ。
ハッシュのはしごのように知られている、420バイトまでの署名のサイズを許容するアプローチや、
他の海藻でのマークルツリーを用いることに依って、署名の数を増やすアルゴリズム、
そして、

しかしながら、これらの方法は不完全であり、もしハッシュに基づく暗号化が、競争力があるアルゴリズムのプロパティであるならば、より良いプロパティを得るために多大に改善する必要がある。

**問題** 署名のアルゴリズムは、セキュリティにおいての前提ではなく、ランダムな信頼出来るオラクルのプロパティに依拠している。
それは、古典的なコンピューター引退しての160bitsのセキュリティを維持しているプロパティである。
(例えば 80 vs 量子 Groverのアルゴリズムによって)最適化されたサイズと、他のプロパティとである。

**前提条件と、付加される前提**
* 2<sup>24</sup>以下に違いない署名を作り出すコンピューターパワーの努力、ハッシュが2<sup>8</sup>
* 署名のアルゴリズムがスケーラブルであるべきであり、ユーザー数の最大の増加で2xの増加ごとに定数のバイトを署名毎に追加することを犠牲に、もし可能であるならば、そのセットアップに掛かる時間は使用回数に対して直線的であるべきだ。

### 6. ASIC-Resistant Proof of Work
問題を解決するための一つの方法は、
特定化するのがとても困難であるコンピュテーションのタイプに基づいたProof of work のアルゴリズムを作成するということだ
あるアイディアでは、ハッシュのファンクションを"メモリー上に"生成し、より一層ASICが並行稼動することを難しくすることがある。
このアイディアはとてもシンプルだが、根本的に限られている。もし、関数がメモリー上でのみ動くのであれば、それはメモリーでしか承認出来ない。加えて、平行化を超えたアルゴリズムには
他のアプローチとしては、ランダムで、マニングのファンクションをブロックごとに生成いｓ，特定性を
ASICが理想的には、任意のコンピュテーションをシンプルなCPUである
**問題** 2つの `PoWProduce(data, diff) - > nonce` and `PoWVerify(datam nonce, diff) - > {0, 1}` をハッシュキャッシュの代わりとなるように提供することによって、経済的にメリットのない`PoWを作り出す`ためのASICを生み出すことに繋がってしまった。

**追加の前提条件と必要条件** : 
* `PoWの生成` `diff`に対してランタイムで直線的で無ければならない。
* `PoWの承認` `diff`に対して出来る限り多態的に対数的なランタイムを持たなければならない。
* `PoWの生成`を走らせることは`1`を返す値を生成し、それを`PoWの承認`を行う際に
最も効率的でなければならない、もしくは、最も効率的である状態に近くなければならない。
+ 


### 8. Proof of Stake

マイニングの中央集権化の解決策の他のアプローチには、マイニングを一切行わないことがある、そしてそれぞれのノードの重さを図る他のメカニズムによってコンセンサスに至る。
現在最も有名な代替案はProof of Stake である。即ち、"CPUパワーの1つのユニット"としてのコンセンサスのモデルを扱う代わりに、
1つの投票が、1津の通貨のユニットとしての1つのボートとなる。

とてもシンプルなProof of Stakeのアルゴリズムは、マイナーがマイニングする際に、
コインを持っているアドレスの秘密鍵を使って署名を行うことをマイナーに求める。ブロックが有効であったならば`sha256(PREVHAS + ADDRESS + TIMESTAMP) < = 2^256 * BALANCE / DIFFICULTY ` where Prevhashがハッシュの前のブロックにある。`Address`は、BalanceとTime stampを持つ署名者のアドレスであり、それは、秒単位での現在のunixtime を表示する。そして`DIfficulty`は署名が成功する度合いを規定するための調整可能なパラメーターである。

1見すると、このアルゴリズムは、基本的に全てのマイナーが秒単位でランダムな成功の機会をもっている、そして、あなたのアドレスはが2倍の金額を持っていれば、2倍の成功の確率を得ることが出来る。

しかしながらこのアルゴリズムには、1つの大きな欠点がある。:
それが`Nothing At Stake`問題だ。このフォークのイベントの後に、フォークが偶然であれ、悪意を持って過去の歴史に書き加えようとしたのであれ、そしてトランザクションをリバースさせようとしたのであれ、
全てのマイナーにとって最適化された戦略は、全てのチェーンをマインすることになる。すると、マイナーはどのフォークがブロックチェーンとして勝ったとしても、報酬を得ることが出来る。
このようにして、経済的に興味のあるマイナーの大多数がいたとしても、攻撃者はなにかの電子的な商品と引き換えにしてトランザクションを送ることが出来る。（通例は他の暗号通貨).そして商品を受け取ると、
その商品の売買のトランザクションの1つ前に有るブロックからフォークを始める。
誰もが全てのブロックを採掘しているが故に、全体のStakeの1％を所持している攻撃者であったとしても、攻撃が成功するかもしれない。

他にはLong-range attacksと呼ばれる問題が上がっている。
マイナーがメインチェーンの先頭の5つか10つ前のブロックをフォークを始めようとしているところ、よく起こることだ、しかし何百何千ものブロックを遡る。
もしアルゴリズムが不適切であるならば、攻撃者がとても前のブロックから始めることが出来るかもしれない。そして何十億ものブロックを将来のブロックとして彫り、（何故ならばProof of Workは必要ないため)

