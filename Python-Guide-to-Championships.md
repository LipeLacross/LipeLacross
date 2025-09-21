
# README — **Python do Zero ao Amador PRO** (Maratona SBC / ICPC / OBI)

> Estrutura pensada para começar **bem básico** (lógica de programação) e ir **ficando mais difícil** até as técnicas que mais caem em campeonatos amadores. Tudo com exemplos em **Python 3.10+**.

---

## 📌 Sumário rápido

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

*(Opcional)* **LCA (Binary Lifting)** — útil em níveis seguintes, mas geralmente acima do amador iniciante.

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

**Z-function** (alternativa a KMP) e **hashing de string** são úteis para problemas de substrings.

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

## Template Geral de Competição (cole no início dos seus códigos)

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
    main()
```
