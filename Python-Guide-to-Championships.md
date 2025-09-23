# README — **Python do Zero ao Amador PRO** (Maratona SBC / ICPC / OBI)

> Começa **do básico** e evolui até um nível **amador PRO** de competições. Foco em Python 3.10+, com exemplos prontos, padrões que mais caem e um **kit padrão** para copiar e colar. Inclui otimizações específicas de Python, estruturas clássicas e casos de prova.

---

## 📌 Sumário

1. [Lógica de Programação — Fundamentos](#1-lógica-de-programação--fundamentos)
2. [Estruturas de Dados Básicas](#2-estruturas-de-dados-básicas)
3. [Funções, Escopo, Erros Comuns](#3-funções-escopo-erros-comuns)
4. [Arquivos, Módulos, *Typing* opcional](#4-arquivos-módulos-typing-opcional)
5. [Entrada/Saída para Competições (I/O rápido)](#5-entradasaída-para-competições-io-rápido)
6. [Complexidade e Limites Práticos](#6-complexidade-e-limites-práticos)
7. [Técnicas Base que Mais Caem](#7-técnicas-base-que-mais-caem)
8. [Matemática de Competição](#8-matemática-de-competição)
9. [Estruturas Avançadas (heap, deque, Fenwick, SegTree)](#9-estruturas-avançadas-heap-deque-fenwick-segtree)
10. [Grafos](#10-grafos)
11. [Árvores](#11-árvores)
12. [Strings](#12-strings)
13. [Programação Dinâmica (DP)](#13-programação-dinâmica-dp)
14. [Backtracking](#14-backtracking)
15. [Geometria Computacional](#15-geometria-computacional)
16. [Padrões de Problema e Dicas de Prova](#16-padrões-de-problema-e-dicas-de-prova)
17. [Mini *Stress Test* / Gerador de Casos](#17-mini-stress-test--gerador-de-casos)
18. [⚙️ Otimizações e Truques de Performance no Python](#18-️-otimizações-e-truques-de-performance-no-python)
19. [🧰 Biblioteca Padrão Útil no Competitivo](#19--biblioteca-padrão-útil-no-competitivo)
20. [🧠 Tabelas de Complexidade por Estrutura](#20--tabelas-de-complexidade-por-estrutura)
21. [🧱 Compressão de Coordenadas e Diferenças](#21--compressão-de-coordenadas-e-diferenças)
22. [🧮 Extras de Matemática (Miller–Rabin, CRT, Ex-CRT)](#22--extras-de-matemática-miller–rabin-crt-ex-crt)
23. [🕸️ Grafos Avançados (SCC, Pontes, Articulações, Euleriano)](#23--grafos-avançados-scc-pontes-articulações-euleriano)
24. [🌳 Árvores Avançadas (LCA, Euler Tour, DP em árvore)](#24--árvores-avançadas-lca-euler-tour-dp-em-árvore)
25. [🧵 Pilha/Fila Monotônica, Janela Máxima, "Sweep Line"](#25--pilhafila-monotônica-janela-máxima-sweep-line)
26. [🧩 Busca Binária na Resposta (com *check*)](#26--busca-binária-na-resposta-com-check)
27. [🧵 DP Otimizada (Bitset, Monotônica, D\&C)](#27--dp-otimizada-bitset-monotônica-dc)
28. [🧪 Casos de Teste e Debug Rápido](#28--casos-de-teste-e-debug-rápido)
29. [🗣️ Interativo (esqueleto)](#29--interativo-esqueleto)
30. [📎 Padrões Resolvidos (Receitas)](#30--padrões-resolvidos-receitas)
31. [🧾 Template Geral de Competição](#31--template-geral-de-competição)

> **Nota honesta**: “tudo de Python” é infinito. Este guia cobre **o essencial + intermediário** (e alguns tópicos avançados) que **mais aparecem** em provas amadoras e etapas iniciais.

---

## 1) Lógica de Programação — Fundamentos

**Variáveis e tipos**

```python
x = 10            # int
y = 3.14          # float
s = "oi"          # str
b = True          # bool
```

**Operadores essenciais**

```python
a, b = 7, 3
a + b; a - b; a * b
a // b  # divisão inteira -> 2
a % b   # resto -> 1
a ** b  # potência -> 343
a == b; a != b; a < b <= 10
```

**Entrada/saída iniciais**

```python
nome = input().strip()
n = int(input())
print(f"Olá, {nome}! Você digitou {n}.")
```

**Condicionais**

```python
x = int(input())
if x > 0:
    print("positivo")
elif x == 0:
    print("zero")
else:
    print("negativo")

# Ternário
paridade = "par" if x % 2 == 0 else "ímpar"
```

**Repetições**

```python
# for contado
for i in range(5):  # 0..4
    print(i)

# while
i = 0
while i < 5:
    print(i)
    i += 1

# break / continue
for i in range(10):
    if i == 3: continue
    if i == 7: break
    print(i)
```

**Coleções básicas**

```python
lista = [1, 2, 3]
tupla = (1, 2, 3)            # imutável
conj = {1, 2, 2, 3}          # {1, 2, 3}
d = {"a": 1, "b": 2}
```

---

## 2) Estruturas de Dados Básicas

**Lista**

```python
arr = [5, 1, 4]
arr.append(9)
arr.sort()         # O(n log n)
arr.reverse()
arr2 = sorted(arr) # cria outra lista
```

**Dicionário**

```python
freq = {}
for x in [1,2,2,3,3,3]:
    freq[x] = freq.get(x, 0) + 1
# freq -> {1:1, 2:2, 3:3}
```

**Conjunto**

```python
visto = set()
visto.add(10)
print(10 in visto)  # True
```

**Comprehensions**

```python
quad = [x*x for x in range(5)]                 # [0,1,4,9,16]
pares = [x for x in range(10) if x % 2 == 0]   # [0,2,4,6,8]
freq = {c: s.count(c) for c in set("banana")}  # {'b':1,'a':3,'n':2}
```

---

## 3) Funções, Escopo, Erros Comuns

**Definição, retorno, parâmetros**

```python
def soma(a: int, b: int) -> int:
    return a + b

def media(*vals):
    return sum(vals) / len(vals)

def config(**opts):
    return opts.get("modo", "padrao")
```

**Cuidado com parâmetro padrão mutável**

```python
def ruim(x, acc=[]):        # EVITE
    acc.append(x)
    return acc

def bom(x, acc=None):       # OK
    if acc is None:
        acc = []
    acc.append(x)
    return acc
```

**Recursão simples**

```python
def fatorial(n: int) -> int:
    return 1 if n <= 1 else n * fatorial(n-1)
```

**Exceções**

```python
try:
    x = int(input())
except ValueError:
    print("entrada inválida")
else:
    print("ok")
finally:
    pass
```

---

## 4) Arquivos, Módulos, *Typing* opcional

```python
# ler arquivo inteiro
with open("in.txt") as f:
    dados = f.read()

# typing essencial
from typing import List, Dict, Optional, Tuple
A: List[int] = [1,2,3]
D: Dict[str, int] = {"a":1}
x: Optional[int] = None
Ponto = Tuple[int, int]
```

---

## 5) Entrada/Saída para Competições (I/O rápido)

```python
import sys

def input():
    return sys.stdin.readline().rstrip()

def ler_tudo_ints():
    return list(map(int, sys.stdin.buffer.read().split()))

# Saída volumosa:
out = sys.stdout.write
# out(f"{valor}\n")
```

Padrões frequentes:

```python
# T casos
T = int(input())
for _ in range(T):
    n = int(input())
    arr = list(map(int, input().split()))
    print(sum(arr))

# Até EOF
import sys
for line in sys.stdin:
    if not line.strip(): continue
    a, b = map(int, line.split())
    print(a + b)
```

---

## 6) Complexidade e Limites Práticos

| Complexidade     | n típico competitivo | Exemplos                    |
| ---------------- | -------------------: | --------------------------- |
| O(n), O(n log n) |              1e5–1e6 | sort, heap, prefixos        |
| O(n²)            |    ≤ 5e4 com cuidado | DP simples, dupla iteração  |
| O(n³)            |                ≤ 500 | Floyd, DP cúbica            |
| O(2ⁿ)            |               n ≤ 20 | bitmask, meet-in-the-middle |

Regras de bolso:

* Evite `O(n²)` para n ≈ 1e5.
* Prefira **iterar uma vez** e usar **hash (dict/set)** para contagem/busca.

---

## 7) Técnicas Base que Mais Caem

**Ordenação com *key***

```python
pares = [(3, "c"), (1, "a"), (2, "b")]
pares.sort(key=lambda p: (p[0], p[1]))
```

**Busca Binária**

```python
def bsearch(lo, hi, ok):
    while lo < hi:
        mid = (lo + hi)//2
        if ok(mid): hi = mid
        else: lo = mid + 1
    return lo
```

**`bisect` (índices em lista ordenada)**

```python
import bisect
a = [1,3,3,5]
i = bisect.bisect_left(a, 3)  # 1
j = bisect.bisect_right(a, 3) # 3
```

**Dois ponteiros / janela deslizante (valores não negativos)**

```python
def subarrays_soma_leq_k(a, K):
    s = l = 0
    ans = 0
    for r, x in enumerate(a):
        s += x
        while s > K:
            s -= a[l]; l += 1
        ans += (r - l + 1)
    return ans
```

**Prefix sums 1D/2D**

```python
def prefix1d(a):
    p = [0]*(len(a)+1)
    for i, v in enumerate(a): p[i+1] = p[i] + v
    return p

def sum_range(p, l, r):  # [l,r]
    return p[r+1]-p[l]
```

**Contagem / *hashing* com dict**

```python
from collections import Counter, defaultdict
cnt = Counter([1,2,2,3])               # {1:1, 2:2, 3:1}
bag = defaultdict(int)
for x in [1,2,2,3]: bag[x]+=1
```

---

## 8) Matemática de Competição

```python
import math
MOD = 10**9 + 7

def gcd(a,b): return math.gcd(a,b)

def lcm(a,b): return a//gcd(a,b)*b

def modpow(a,e,m=MOD): return pow(a,e,m)

def modinv(a,m=MOD): return pow(a, m-2, m)  # m primo
```

**Crivo + fatoração por menor primo**

```python
def sieve(n):
    spf = list(range(n+1))
    for i in range(2, int(n**0.5)+1):
        if spf[i] == i:
            for j in range(i*i, n+1, i):
                if spf[j] == j: spf[j] = i
    return spf

def factorize(x, spf):
    fac = {}
    while x > 1:
        p = spf[x]; c = 0
        while x % p == 0: x//=p; c+=1
        fac[p] = fac.get(p,0)+c
    return fac
```

**Combinatória (pré-processo)**

```python
def build_fact(n, mod=MOD):
    fact = [1]*(n+1); invf = [1]*(n+1)
    for i in range(2, n+1): fact[i] = fact[i-1]*i % mod
    invf[n] = pow(fact[n], mod-2, mod)
    for i in range(n, 0, -1): invf[i-1] = invf[i]*i % mod
    return fact, invf

def nCk(n,k,fact,invf,mod=MOD):
    if k<0 or k>n: return 0
    return fact[n]*invf[k]%mod*invf[n-k]%mod
```

**Bits / máscaras**

```python
def count_bits(x): return x.bit_count()
# enumerar subconjuntos de [0..m-1]
for mask in range(1<<m):
    pass
```

---

## 9) Estruturas Avançadas (heap, deque, Fenwick, SegTree)

**Heap mínimo (priority queue)**

```python
import heapq
h = []
heapq.heappush(h, (dist, no))
dist, u = heapq.heappop(h)
```

**Deque**

```python
from collections import deque
dq = deque([1,2,3])
dq.appendleft(0); dq.append(4)
x = dq.popleft()
```

**Fenwick (BIT)**

```python
class Fenwick:
    def __init__(self, n):
        self.n = n; self.ft = [0]*(n+1)
    def add(self, i, v):
        while i <= self.n:
            self.ft[i]+=v; i+= i&-i
    def sum(self, i):
        s=0
        while i>0: s+=self.ft[i]; i-= i&-i
        return s
    def range_sum(self,l,r): return self.sum(r)-self.sum(l-1)
```

**Segment Tree (soma)**

```python
class SegTree:
    def __init__(self, arr):
        self.n=1
        while self.n<len(arr): self.n<<=1
        self.st=[0]*(2*self.n)
        for i,v in enumerate(arr): self.st[self.n+i]=v
        for i in range(self.n-1,0,-1):
            self.st[i]=self.st[i<<1]+self.st[i<<1|1]
    def update(self, idx, val):
        i=self.n+idx; self.st[i]=val; i>>=1
        while i:
            self.st[i]=self.st[i<<1]+self.st[i<<1|1]; i>>=1
    def query(self,l,r):
        l+=self.n; r+=self.n; res=0
        while l<=r:
            if l&1: res+=self.st[l]; l+=1
            if not (r&1): res+=self.st[r]; r-=1
            l>>=1; r>>=1
        return res
```

> **Extra**: SegTree com *lazy propagation* (soma em intervalo + incremento) — versão curta:

```python
class SegLazy:
    def __init__(self, n):
        self.N=1
        while self.N<n: self.N<<=1
        self.st=[0]*(2*self.N)
        self.lz=[0]*(2*self.N)
    def _push(self, i, l, r):
        if self.lz[i]!=0 and l!=r:
            mid=(l+r)//2
            for ch in (i<<1, i<<1|1):
                self.lz[ch]+=self.lz[i]
            self.st[i<<1]+= (mid-l+1)*self.lz[i]
            self.st[i<<1|1]+= (r-mid)*self.lz[i]
            self.lz[i]=0
    def _upd(self, i,l,r,ql,qr,val):
        if qr<l or r<ql: return
        if ql<=l and r<=qr:
            self.st[i]+= (r-l+1)*val; self.lz[i]+=val; return
        self._push(i,l,r)
        m=(l+r)//2
        self._upd(i<<1,l,m,ql,qr,val)
        self._upd(i<<1|1,m+1,r,ql,qr,val)
        self.st[i]=self.st[i<<1]+self.st[i<<1|1]
    def _qry(self,i,l,r,ql,qr):
        if qr<l or r<ql: return 0
        if ql<=l and r<=qr: return self.st[i]
        self._push(i,l,r)
        m=(l+r)//2
        return self._qry(i<<1,l,m,ql,qr)+self._qry(i<<1|1,m+1,r,ql,qr)
    def update(self,l,r,val): self._upd(1,0,self.N-1,l,r,val)
    def query(self,l,r): return self._qry(1,0,self.N-1,l,r)
```

---

## 10) Grafos

**Representação**

```python
n, m = map(int, input().split())
adj = [[] for _ in range(n)]
for _ in range(m):
    u, v = map(int, input().split())
    adj[u].append(v); adj[v].append(u)  # não-dirigido
```

**BFS / DFS**

```python
from collections import deque
def bfs(s, adj):
    dist = [-1]*len(adj)
    q=deque([s]); dist[s]=0
    while q:
        u = q.popleft()
        for v in adj[u]:
            if dist[v]==-1:
                dist[v]=dist[u]+1; q.append(v)
    return dist
```

**Dijkstra (pesos ≥ 0)** / **0-1 BFS (pesos 0/1)**

```python
import heapq

def dijkstra(s, adjw):
    INF=10**18; n=len(adjw)
    dist=[INF]*n; dist[s]=0
    pq=[(0,s)]
    while pq:
        d,u = heapq.heappop(pq)
        if d!=dist[u]: continue
        for v,w in adjw[u]:
            nd=d+w
            if nd<dist[v]:
                dist[v]=nd; heapq.heappush(pq,(nd,v))
    return dist

from collections import deque

def zero_one_bfs(s, adj01):  # adj01[u]: (v, w in {0,1})
    INF=10**18; n=len(adj01)
    dist=[INF]*n; dist[s]=0
    dq=deque([s])
    while dq:
        u=dq.popleft()
        for v,w in adj01[u]:
            nd=dist[u]+w
            if nd<dist[v]:
                dist[v]=nd
                if w==0: dq.appendleft(v)
                else: dq.append(v)
    return dist
```

**Topológica (Kahn)**

```python
from collections import deque

def toposort(n, adj):
    indeg=[0]*n
    for u in range(n):
        for v in adj[u]: indeg[v]+=1
    q=deque([i for i in range(n) if indeg[i]==0])
    topo=[]
    while q:
        u=q.popleft(); topo.append(u)
        for v in adj[u]:
            indeg[v]-=1
            if indeg[v]==0: q.append(v)
    return topo  # len< n => ciclo
```

**MST (Kruskal + DSU)**

```python
class DSU:
    def __init__(self,n):
        self.p=list(range(n)); self.sz=[1]*n
    def find(self,x):
        while x!=self.p[x]:
            self.p[x]=self.p[self.p[x]]; x=self.p[x]
        return x
    def union(self,a,b):
        a,b=self.find(a),self.find(b)
        if a==b: return False
        if self.sz[a]<self.sz[b]: a,b=b,a
        self.p[b]=a; self.sz[a]+=self.sz[b]
        return True

def mst_kruskal(n, edges):       # edges: (w,u,v)
    edges.sort()
    dsu=DSU(n); cost=0; used=0
    for w,u,v in edges:
        if dsu.union(u,v):
            cost+=w; used+=1
            if used==n-1: break
    return cost if used==n-1 else None
```

**Bipartido (2-color)**

```python
def bipartido(adj):
    n=len(adj); cor=[-1]*n
    from collections import deque
    for s in range(n):
        if cor[s]!=-1: continue
        cor[s]=0; q=deque([s])
        while q:
            u=q.popleft()
            for v in adj[u]:
                if cor[v]==-1:
                    cor[v]=cor[u]^1; q.append(v)
                elif cor[v]==cor[u]:
                    return False
    return True
```

---

## 11) Árvores

**Raiz, pai, profundidade**

```python
def dfs_tree(u, p, adj, pai, prof):
    pai[u]=p
    for v in adj[u]:
        if v==p: continue
        prof[v]=prof[u]+1
        dfs_tree(v,u,adj,pai,prof)
```

**Diâmetro (2 BFS/DFS)**

```python
# 1) BFS de 0 acha extremo A; 2) BFS de A acha B; dist(A,B)=diâmetro
```

> (LCA completo em seção 24.)

---

## 12) Strings

**KMP (busca de padrão)**

```python
def prefix_function(s: str):
    n=len(s); pi=[0]*n
    for i in range(1,n):
        j=pi[i-1]
        while j>0 and s[i]!=s[j]: j=pi[j-1]
        if s[i]==s[j]: j+=1
        pi[i]=j
    return pi

def kmp_search(text, pat):
    pi=prefix_function(pat); j=0; res=[]
    for i,ch in enumerate(text):
        while j>0 and ch!=pat[j]: j=pi[j-1]
        if ch==pat[j]:
            j+=1
            if j==len(pat):
                res.append(i-j+1); j=pi[j-1]
    return res
```

> Extras: Z-function, *rolling hash* e Manacher — ver seção 12.1 abaixo.

**12.1) Extras de String**

```python
# Rolling hash (esqueleto)
BASE=911382323; MOD=10**9+7

def build_hash(s):
    n=len(s)
    p=[1]*(n+1); h=[0]*(n+1)
    for i,ch in enumerate(s):
        p[i+1]=p[i]*BASE%MOD
        h[i+1]=(h[i]*BASE+ord(ch))%MOD
    return p,h

def get_hash(h,p,l,r):  # [l,r)
    return (h[r]-h[l]*p[r-l])%MOD

# Manacher (maior palíndromo em O(n))

def manacher(s):
    s = "|"+"|".join(s)+"|"
    n=len(s); d=[0]*n; l=r=0
    for i in range(n):
        k = 1 if i>r else min(d[l+r-i], r-i+1)
        while i-k>=0 and i+k<n and s[i-k]==s[i+k]: k+=1
        d[i]=k; k-=1
        if i+k>r: l=i-k; r=i+k
    # d[i]-1 é raio no original sem barras
    return d
```

---

## 13) Programação Dinâmica (DP)

**Knapsack 0/1 (vetor 1D)**

```python
def knapsack(weights, values, W):
    dp=[0]*(W+1)
    for w,v in zip(weights,values):
        for c in range(W, w-1, -1):
            dp[c]=max(dp[c], dp[c-w]+v)
    return dp[W]
```

**LIS O(n log n)**

```python
import bisect

def lis_len(a):
    d=[]
    for x in a:
        i=bisect.bisect_left(d,x)
        if i==len(d): d.append(x)
        else: d[i]=x
    return len(d)
```

**Moedas (número de maneiras)**

```python
def moedas_maneiras(v, alvo):
    dp=[0]*(alvo+1); dp[0]=1
    for coin in v:
        for s in range(coin, alvo+1):
            dp[s]+=dp[s-coin]
    return dp[alvo]
```

**Edit distance (Levenshtein)**

```python
def edit_distance(a, b):
    n, m=len(a), len(b)
    dp=[[0]*(m+1) for _ in range(n+1)]
    for i in range(n+1): dp[i][0]=i
    for j in range(m+1): dp[0][j]=j
    for i in range(1,n+1):
        for j in range(1,m+1):
            if a[i-1]==b[j-1]:
                dp[i][j]=dp[i-1][j-1]
            else:
                dp[i][j]=1+min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])
    return dp[n][m]
```

---

## 14) Backtracking

**Permutações**

```python
def perms(a):
    a=sorted(a)
    used=[False]*len(a); cur=[]; res=[]
    def bt():
        if len(cur)==len(a):
            res.append(cur[:]); return
        prev=None
        for i,x in enumerate(a):
            if used[i] or x==prev: continue
            used[i]=True; cur.append(x)
            bt()
            cur.pop(); used[i]=False
            prev=x
    bt()
    return res
```

**N-Rainhas (esqueleto)**

```python
def n_queens(n):
    col=set(); d1=set(); d2=set(); pos=[-1]*n; ans=[]
    def bt(r=0):
        if r==n:
            ans.append(pos[:]); return
        for c in range(n):
            if c in col or (r-c) in d1 or (r+c) in d2: continue
            pos[r]=c; col.add(c); d1.add(r-c); d2.add(r+c)
            bt(r+1)
            col.remove(c); d1.remove(r-c); d2.remove(r+c)
    bt(); return ans
```

---

## 15) Geometria Computacional

**Base 2D**

```python
from typing import Tuple
Point = Tuple[int,int]

def cross(ax,ay,bx,by): return ax*by - ay*bx

def ccw(a:Point,b:Point,c:Point)->int:
    return cross(b[0]-a[0], b[1]-a[1], c[0]-a[0], c[1]-a[1])

def on_seg(a,b,p)->bool:
    return (min(a[0],b[0])<=p[0]<=max(a[0],b[0]) and
            min(a[1],b[1])<=p[1]<=max(a[1],b[1]))

def seg_inter(a,b,c,d)->bool:
    o1=ccw(a,b,c); o2=ccw(a,b,d)
    o3=ccw(c,d,a); o4=ccw(c,d,b)
    if o1==0 and on_seg(a,b,c): return True
    if o2==0 and on_seg(a,b,d): return True
    if o3==0 and on_seg(c,d,a): return True
    if o4==0 and on_seg(c,d,b): return True
    return (o1>0)!=(o2>0) and (o3>0)!=(o4>0)

def polygon_area(poly):
    s=0
    for i in range(len(poly)):
        x1,y1=poly[i]; x2,y2=poly[(i+1)%len(poly)]
        s+= x1*y2 - y1*x2
    return abs(s)/2
```

**Cascas convexas (Monotone Chain)**

```python
def convex_hull(pts):
    pts = sorted(set(pts))
    if len(pts)<=1: return pts
    def cross(o,a,b): return (a[0]-o[0])*(b[1]-o[1]) - (a[1]-o[1])*(b[0]-o[0])
    lower=[]
    for p in pts:
        while len(lower)>=2 and cross(lower[-2], lower[-1], p) <= 0:
            lower.pop()
        lower.append(p)
    upper=[]
    for p in reversed(pts):
        while len(upper)>=2 and cross(upper[-2], upper[-1], p) <= 0:
            upper.pop()
        upper.append(p)
    return lower[:-1]+upper[:-1]
```

---

## 16) Padrões de Problema e Dicas de Prova

**Pistas do enunciado → técnica provável**

* “Menor número de passos” → **BFS**
* “Distância mínima com pesos ≥ 0” → **Dijkstra**
* “Muitas queries de intervalo / soma” → **Fenwick/SegTree**
* “Quantas maneiras / módulo” → **DP + combinatória**
* “Substring / padrão” → **KMP / Z / hash**
* “Escolher intervalos sem sobrepor” → **Greedy por fim**

**Erros comuns a evitar**

* Índice 0 vs 1; intervalos `[l, r]` vs `[l, r)`.
* `O(n²)` com `n` grande.
* Esquecer casos-borda: `n=1`, vazios, repetidos, máximos.
* Saída com espaço/quebra **exatos**.

**Checklist antes de enviar**

* I/O confere com o enunciado?
* Complexidade cabe no limite?
* Testou casos pequenos/extremos?
* Evitou `float` quando **mod** é pedido?

---

## 17) Mini *Stress Test* / Gerador de Casos

```python
import random, sys

def fast_sol(arr):
    # TODO: coloque a versão rápida do seu problema
    return sum(arr)

def slow_sol(arr):
    # TODO: coloque uma versão lenta garantida correta
    return sum(arr)

def rand_case():
    n = random.randint(1, 30)
    return [random.randint(-50, 50) for _ in range(n)]

def main():
    for _ in range(1000):
        arr = rand_case()
        a = fast_sol(arr)
        b = slow_sol(arr)
        if a != b:
            print("Mismatch!", arr, a, b)
            sys.exit(0)
    print("OK")

if __name__ == "__main__":
    main()
```

---

## 18) ⚙️ Otimizações e Truques de Performance no Python

* Use **PyPy** quando disponível (melhor para laços pesados, estruturas puras de Python). Em algumas DPs com muita recursão, CPython + `pypy3` podem variar — teste local.
* **I/O**: substitua `input` por `sys.stdin.readline`; para *bulk*, use `sys.stdin.buffer.read()`.
* **`setrecursionlimit`** para DFS/recursões profundas:

```python
import sys
sys.setrecursionlimit(1_000_000)
```

* **Binding local** (micro): dentro do laço, capture funções em variáveis locais para evitar *lookup* repetido.

```python
push = heapq.heappush; pop = heapq.heappop
for ...:
    push(pq, x)
```

* **`join`** é mais rápido que múltiplos `print`:

```python
print("\n".join(map(str, ans)))
```

* Evite criar listas enormes sem necessidade; prefira **geradores** quando possível.

---

## 19) 🧰 Biblioteca Padrão Útil no Competitivo

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def f(n):
    if n<2: return n
    return f(n-1)+f(n-2)
```

```python
import itertools as it
# receitas comuns
pairs = list(it.pairwise([1,2,3,4]))   # [(1,2),(2,3),(3,4)]
prod  = list(it.product([0,1], repeat=3))
perms = list(it.permutations([1,2,3]))
combs = list(it.combinations([1,2,3], 2))
acc   = list(it.accumulate([1,2,3]))   # prefix sums
```

```python
from collections import Counter, defaultdict, deque
cnt = Counter("banana")
last = defaultdict(lambda: -1)
```

```python
import math
math.isclose(0.1+0.2, 0.3, rel_tol=1e-9, abs_tol=0.0)
```

---

## 20) 🧠 Tabelas de Complexidade por Estrutura

**Lista**

| Operação              | Custo aprox. |
| --------------------- | ------------ |
| `append`, `pop()`     | O(1) amort.  |
| `pop(0)`, `insert(i)` | O(n)         |
| `sort`/`sorted`       | O(n log n)   |
| `x in lista`          | O(n)         |

**`dict`/`set`**

| Operação       | Custo médio |
| -------------- | ----------- |
| `get/set/in`   | O(1)        |
| iteração total | O(n)        |

**`heapq`**

| Operação       | Custo    |
| -------------- | -------- |
| `heappush/pop` | O(log n) |
| `heapify`      | O(n)     |

**`deque`**

| Operação         | Custo |
| ---------------- | ----- |
| `append/popleft` | O(1)  |
| `appendleft/pop` | O(1)  |

---

## 21) 🧱 Compressão de Coordenadas e Diferenças

**Compressão** (mapear valores grandes para 0..k-1):

```python
def compress(vals):
    uniq = {v:i for i,v in enumerate(sorted(set(vals)))}
    return [uniq[v] for v in vals], uniq
```

**Array de diferenças (1D)** — atualizações em intervalo + reconstrução:

```python
def apply_updates(n, updates):
    # updates: (l,r,delta)
    diff=[0]*(n+1)
    for l,r,d in updates:
        diff[l]+=d; diff[r+1]-=d
    a=[0]*n; cur=0
    for i in range(n):
        cur+=diff[i]; a[i]=cur
    return a
```

**Prefixo 2D**

```python
def prefix2d(mat):
    n=len(mat); m=len(mat[0])
    p=[[0]*(m+1) for _ in range(n+1)]
    for i in range(1,n+1):
        s=0
        for j in range(1,m+1):
            s+=mat[i-1][j-1]
            p[i][j]=p[i-1][j]+s
    return p

def rect_sum(p, x1,y1,x2,y2):  # inclusivo
    return p[x2+1][y2+1]-p[x1][y2+1]-p[x2+1][y1]+p[x1][y1]
```

---

## 22) 🧮 Extras de Matemática (Miller–Rabin, CRT, Ex-CRT)

**Miller–Rabin determinístico para 64-bit**

```python
def is_probable_prime(n:int)->bool:
    if n<2: return False
    small_primes=[2,3,5,7,11,13,17,19,23,29]
    for p in small_primes:
        if n%p==0: return n==p
    d=n-1; s=0
    while d%2==0: d//=2; s+=1
    def check(a):
        x=pow(a,d,n)
        if x==1 or x==n-1: return True
        for _ in range(s-1):
            x=(x*x)%n
            if x==n-1: return True
        return False
    # bases suficientes p/ 2^64
    for a in [2, 3, 5, 7, 11, 13]:
        if not check(a): return False
    return True
```

**Chinês (CRT) — 2 módulos coprimos**

```python
def crt2(a1, m1, a2, m2):
    # resolve x ≡ a1 (mod m1), x ≡ a2 (mod m2)
    # supõe gcd(m1,m2)=1
    inv = pow(m1, -1, m2)
    return (a1 + (a2 - a1)*inv % m2 * m1) % (m1*m2)
```

---

## 23) 🕸️ Grafos Avançados (SCC, Pontes, Articulações, Euleriano)

**SCC (Kosaraju)**

```python
def scc_kosaraju(n, adj):
    g=adj
    rg=[[] for _ in range(n)]
    for u in range(n):
        for v in g[u]: rg[v].append(u)
    vis=[False]*n; order=[]
    def dfs1(u):
        vis[u]=True
        for v in g[u]:
            if not vis[v]: dfs1(v)
        order.append(u)
    for u in range(n):
        if not vis[u]: dfs1(u)
    comp=[-1]*n
    def dfs2(u,c):
        comp[u]=c
        for v in rg[u]:
            if comp[v]==-1: dfs2(v,c)
    c=0
    for u in reversed(order):
        if comp[u]==-1:
            dfs2(u,c); c+=1
    return c, comp
```

**Pontes e Articulações (Tarjan)**

```python
def bridges_articulations(n, adj):
    timer=0
    tin=[-1]*n; low=[-1]*n
    bridges=[]; arti=set()
    def dfs(u,p=-1):
        nonlocal timer
        tin[u]=low[u]=timer; timer+=1
        ch=0
        for v in adj[u]:
            if v==p: continue
            if tin[v]!=-1:
                low[u]=min(low[u], tin[v])
            else:
                dfs(v,u); ch+=1
                low[u]=min(low[u], low[v])
                if low[v]>tin[u]: bridges.append((u,v))
                if p!=-1 and low[v]>=tin[u]: arti.add(u)
        if p==-1 and ch>1: arti.add(u)
    for u in range(n):
        if tin[u]==-1: dfs(u)
    return bridges, sorted(arti)
```

**Caminho Euleriano (grafo não-dirigido)**

```python
def has_eulerian_path_undirected(deg, comp_is_single):
    odd = sum(d%2 for d in deg)
    if not comp_is_single: return False
    return odd in (0,2)
```

---

## 24) 🌳 Árvores Avançadas (LCA, Euler Tour, DP em árvore)

**LCA por *binary lifting***

```python
def build_lca(adj, root=0):
    n=len(adj); LOG=(n).bit_length()
    up=[[0]*n for _ in range(LOG)]
    depth=[0]*n
    import collections
    q=collections.deque([root])
    order=[root]; up[0][root]=root; depth[root]=0
    vis=[False]*n; vis[root]=True
    while q:
        u=q.popleft()
        for v in adj[u]:
            if vis[v]: continue
            vis[v]=True; up[0][v]=u; depth[v]=depth[u]+1
            q.append(v)
    for k in range(1,LOG):
        for v in range(n): up[k][v]=up[k-1][ up[k-1][v] ]
    def lca(a,b):
        if depth[a]<depth[b]: a,b=b,a
        da=depth[a]-depth[b]
        k=0
        while da:
            if da&1: a=up[k][a]
            da>>=1; k+=1
        if a==b: return a
        for k in range(LOG-1,-1,-1):
            if up[k][a]!=up[k][b]:
                a=up[k][a]; b=up[k][b]
        return up[0][a]
    return lca, depth
```

**Euler Tour (subárvore em intervalo)**

```python
def euler_tour(adj, root=0):
    n=len(adj); tin=[0]*n; tout=[0]*n; t=0
    order=[]
    def dfs(u,p=-1):
        nonlocal t
        tin[u]=t; order.append(u); t+=1
        for v in adj[u]:
            if v==p: continue
            dfs(v,u)
        tout[u]=t-1
    dfs(root)
    return tin, tout, order
```

**DP em árvore (tamanho de subárvore)**

```python
def subtree_sizes(adj, root=0):
    n=len(adj); sz=[1]*n
    def dfs(u,p=-1):
        for v in adj[u]:
            if v==p: continue
            dfs(v,u); sz[u]+=sz[v]
    dfs(root); return sz
```

---

## 25) 🧵 Pilha/Fila Monotônica, Janela Máxima, "Sweep Line"

**Janela Máxima (deque monotônica)**

```python
from collections import deque

def sliding_max(a, k):
    dq=deque(); res=[]
    for i,x in enumerate(a):
        while dq and dq[0]<=i-k: dq.popleft()
        while dq and a[dq[-1]]<=x: dq.pop()
        dq.append(i)
        if i>=k-1: res.append(a[dq[0]])
    return res
```

**Pilha Monotônica (próximo maior à direita)**

```python
def next_greater(arr):
    n=len(arr); ans=[-1]*n; st=[]
    for i,x in enumerate(arr):
        while st and arr[st[-1]]<x:
            ans[st.pop()]=i
        st.append(i)
    return ans
```

**Sweep line (intervalos)**

```python
def max_overlap(intervals):
    ev=[]
    for l,r in intervals:
        ev.append((l,1)); ev.append((r,-1))
    ev.sort()
    cur=best=0
    for _,d in ev:
        cur+=d; best=max(best,cur)
    return best
```

---

## 26) 🧩 Busca Binária na Resposta (com *check*)

**Exemplo**: minimizar maior soma de subarray em `k` partes.

```python
def can(a, k, lim):
    s=0; cuts=1
    for x in a:
        if x>lim: return False
        if s+x>lim:
            cuts+=1; s=x
        else: s+=x
    return cuts<=k

def minimize_largest_split_sum(a, k):
    lo, hi = max(a), sum(a)
    while lo<hi:
        mid=(lo+hi)//2
        if can(a,k,mid): hi=mid
        else: lo=mid+1
    return lo
```

---

## 27) 🧵 DP Otimizada (Bitset, Monotônica, D\&C)

**Subset sum com *bitset* usando `int`**

```python
def subset_sum_possible(vals, S):
    bit=1
    for x in vals:
        bit |= (bit<<x)
    return (bit>>S)&1
```

**DP com fila monotônica (otimização de janela)** — esqueleto clássico para `dp[i]=min(dp[i-1], dp[j]+c(i,j))` com `j` numa janela.

**Divide & Conquer DP** — avançado; útil quando o *argmin* é monótono.

---

## 28) 🧪 Casos de Teste e Debug Rápido

* Gere **aleatórios** + uma solução lenta para comparar (seção 17).
* Teste **bordas**: `n=1`, todos iguais, estritamente crescente/decrescente, valores máximos, zerados.
* Adicione `assert` para invariantes dentro de laços críticos.

---

## 29) 🗣️ Interativo (esqueleto)

```python
import sys

def ask(x):
    print(x)
    sys.stdout.flush()
    return input().strip()

# Uso: r = ask("? 5 7") ; processa resposta
```

---

## 30) 📎 Padrões Resolvidos (Receitas)

**Dois-sum** (índices 0-based):

```python
def two_sum(a, target):
    pos={}
    for i,x in enumerate(a):
        if target-x in pos: return (pos[target-x], i)
        pos[x]=i
    return None
```

**Longest substring sem repetir** (janela):

```python
def length_longest_unique(s):
    last={}; l=0; best=0
    for r,ch in enumerate(s):
        if ch in last and last[ch]>=l:
            l=last[ch]+1
        last[ch]=r
        best=max(best, r-l+1)
    return best
```

**BFS em grade**

```python
from collections import deque

def bfs_grid(grid):
    n=len(grid); m=len(grid[0])
    dist=[[-1]*m for _ in range(n)]
    D=[(1,0),(-1,0),(0,1),(0,-1)]
    q=deque()
    # adicionar fontes
    for i in range(n):
        for j in range(m):
            if grid[i][j]=='S':
                dist[i][j]=0; q.append((i,j))
    while q:
        x,y=q.popleft()
        for dx,dy in D:
            nx,ny=x+dx,y+dy
            if 0<=nx<n and 0<=ny<m and grid[nx][ny]!="#" and dist[nx][ny]==-1:
                dist[nx][ny]=dist[x][y]+1
                q.append((nx,ny))
    return dist
```

**Floyd–Warshall** (todas as pares):

```python
def floyd_warshall(dist):
    n=len(dist)
    for k in range(n):
        for i in range(n):
            for j in range(n):
                nd=dist[i][k]+dist[k][j]
                if nd<dist[i][j]: dist[i][j]=nd
    return dist
```

**Bellman–Ford** (detecta ciclos negativos):

```python
def bellman_ford(n, edges, s):  # edges: (u,v,w)
    INF=10**18
    dist=[INF]*n; dist[s]=0
    for _ in range(n-1):
        ch=False
        for u,v,w in edges:
            if dist[u]<INF and dist[u]+w<dist[v]:
                dist[v]=dist[u]+w; ch=True
        if not ch: break
    # ciclo negativo alcançável?
    neg=[False]*n
    for _ in range(1):
        for u,v,w in edges:
            if dist[u]<INF and dist[u]+w<dist[v]:
                neg[v]=True
    return dist, neg
```

---

## 31) 🧾 Template Geral de Competição

```python
# -*- coding: utf-8 -*-
import sys
from typing import *
from collections import deque, Counter, defaultdict
import math
import bisect
import heapq

# input rápido
def input():
    return sys.stdin.readline().rstrip()

def main():
    # Exemplo de leitura padrão:
    # n = int(input())
    # arr = list(map(int, input().split()))
    # print(sum(arr))
    pass

if __name__ == "__main__":
    # sys.setrecursionlimit(1_000_000)
    main()
```

---

### ✅ O que ficou de fora de propósito (avançado demais p/ amador)

* Suffix Array/Automaton completos, HLD + segtree pesados, Mo’s Algorithm com *Hilbert order*, Min-Cost Max-Flow, Dinic/HLPP, FFT/NTT, Pollard Rho, DP Convex Hull Trick formal.
* Se precisar de algum tópico destes, adicione uma seção nova neste README e cole o esqueleto — os *hooks* de integração já estão acima.
