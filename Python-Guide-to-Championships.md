# README — **Python do Zero ao Amador PRO (GIGANTE)**

> Ordem **do mais fácil para o mais difícil**. Começa com lógica e I/O, passa por estruturas e padrões clássicos, e avança por DP otimizada, grafos avançados, strings pesadas, geometria, *flows*, FFT/NTT, fatoração rápida e técnicas *offline*. Foco em **Python 3.10+** para **Maratona SBC / OBI / ICPC nível amador–intermediário**.

---

## 📌 Mapa Geral (em ordem de dificuldade)

1. Fundamentos de Python & Lógica
2. I/O competitivo e *boilerplate*
3. Estruturas básicas (list/tuple/dict/set) + *idioms*
4. Complexidade e limites práticos
5. Padrões fáceis: prefix sums, *two-pointers*, *freq map*
6. Matemática básica (gcd/lcm/modpow/combinatória)
7. Estruturas médias: `heapq`, `deque`, DSU, Sparse Table
8. Fenwick/BIT e Segment Tree (+ *lazy*)
9. Grafos básicos: BFS/DFS/Topo/Dijkstra/0–1 BFS
10. Árvores básicas: Euler Tour, LCA, tamanhos de subárvore
11. Strings base: KMP, Z, *rolling hash*, Manacher
12. DP clássica: knapsack, LIS, moedas, edit distance
13. Geometria básica: ccw, interseção, *convex hull*
14. Padrões médios: janela monotônica, *sweep line*, compressão
15. DP otimizada: bitset, monotônica, D\&C, Knuth
16. Strings avançadas: Aho–Corasick, Suffix Array + LCP, Suffix Automaton
17. Árvores avançadas: centroid, DSU-on-tree, HLD (+SegTree)
18. Grafos avançados: SCC, pontes/articulações, Euleriano
19. *Matching* e *Flow*: Hopcroft–Karp, Dinic, Min-Cost Max-Flow
20. Matemática avançada: exgcd, CRT geral, Miller–Rabin, Pollard Rho
21. FFT/NTT e multiplicação polinomial
22. Algoritmos *offline*: Mo’s Algorithm (+ variações), DSU rollback (nota)
23. Interativo, *stress test*, *debug* e *checkers*
24. Templates finais de prova (curto e completo)

> **Nota honesta**: “tudo de Python” é infinito. Aqui você tem **quase tudo que cai** até níveis intermediários — pronto para copiar/colar e adaptar.

---

## 1) Fundamentos de Python & Lógica

```python
# Tipos e operadores
x:int = 7; y:float = 3.5; s:str = "Oi"; b:bool = True
x+y; x//2; x%2; x**3; x==y; 0 <= x < 10

# Strings
nome = input().strip()
print(f"Olá, {nome}")

# If/elif/else + ternário
n = int(input())
print("par" if n%2==0 else "ímpar")

# For/while + break/continue
for i in range(5):
    if i==3: continue
    if i==4: break
    print(i)

# Funções e parâmetros *args/**kwargs
from typing import Optional, List

def soma(a:int,b:int)->int: return a+b

def acum(x:int, acc:Optional[List[int]]=None):
    if acc is None: acc=[]
    acc.append(x); return acc

# Exceções
try:
    v = int(input())
except ValueError:
    print("inválido")
```

---

## 2) I/O competitivo e *boilerplate*

```python
import sys

def input():
    return sys.stdin.readline().rstrip()

# leitura massiva
all_ints = list(map(int, sys.stdin.buffer.read().split()))
# saída massiva
out = sys.stdout.write
```

Padrões:

```python
# T casos
T = int(input())
for _ in range(T):
    n = int(input()); a = list(map(int, input().split()))
    print(sum(a))

# Até EOF
for line in sys.stdin:
    if not line.strip(): continue
    x, y = map(int, line.split()); print(x+y)
```

Template curto de prova → ver seção 24.1.

---

## 3) Estruturas básicas + *idioms*

```python
# list/tuple/dict/set
arr=[3,1,4]; arr.sort(); arr.append(9)
d = {"a":1, "b":2}; d.get("c",0)
S = {1,2,2,3}; 2 in S  # True

# comprehensions
squares = [i*i for i in range(10) if i%2==0]
inv = {v:k for k,v in d.items()}

# slicing
b = arr[::-1]  # reverse

# sort com key (tupla)
pairs = [(2,"b"),(1,"c"),(1,"a")]
pairs.sort(key=lambda x: (x[0], x[1]))
```

---

## 4) Complexidade e limites práticos (regra de bolso)

| Classe           |        n típico | Exemplos                    |
| ---------------- | --------------: | --------------------------- |
| O(n), O(n log n) |         1e5–1e6 | sort, heap, prefixos        |
| O(n²)            | ≤ 5e4 (cuidado) | DP simples, duplo laço      |
| O(n³)            |           ≤ 500 | Floyd, DP cúbica            |
| O(2ⁿ)            |          n ≤ 20 | bitmask, meet-in-the-middle |

Dicas: evite `O(n²)` com `n≈1e5`; prefira `dict/set` para contagens.

---

## 5) Padrões fáceis (essenciais)

**Prefix sums**

```python
def prefix1d(a):
    p=[0]*(len(a)+1)
    for i,v in enumerate(a): p[i+1]=p[i]+v
    return p

def range_sum(p,l,r): return p[r+1]-p[l]
```

**Two-pointers / janela**

```python
def subarrays_leq_k(a,K):
    s=l=0; ans=0
    for r,x in enumerate(a):
        s+=x
        while s>K:
            s-=a[l]; l+=1
        ans += r-l+1
    return ans
```

**Frequências / contagem**

```python
from collections import Counter, defaultdict
cnt = Counter([1,2,2,3])
bag = defaultdict(int)
for x in [1,2,2,3]: bag[x]+=1
```

---

## 6) Matemática básica

```python
import math
MOD=1_000_000_007

def gcd(a,b): return math.gcd(a,b)

def lcm(a,b): return a//gcd(a,b)*b

def modpow(a,e,m=MOD): return pow(a,e,m)

def modinv(a,m=MOD): return pow(a, m-2, m)  # m primo
```

**Crivo + menor primo**

```python
def sieve(n):
    spf=list(range(n+1))
    for i in range(2,int(n**0.5)+1):
        if spf[i]==i:
            for j in range(i*i,n+1,i):
                if spf[j]==j: spf[j]=i
    return spf

def factorize(x, spf):
    fac={}
    while x>1:
        p=spf[x]; c=0
        while x%p==0: x//=p; c+=1
        fac[p]=fac.get(p,0)+c
    return fac
```

**Combinatória (pré-cálculo)**

```python
def build_fact(n, mod=MOD):
    fact=[1]*(n+1); invf=[1]*(n+1)
    for i in range(2,n+1): fact[i]=fact[i-1]*i%mod
    invf[n]=pow(fact[n],mod-2,mod)
    for i in range(n,0,-1): invf[i-1]=invf[i]*i%mod
    return fact,invf

def nCk(n,k,fact,invf,mod=MOD):
    if k<0 or k>n: return 0
    return fact[n]*invf[k]%mod*invf[n-k]%mod
```

---

## 7) Estruturas médias: heap/deque/DSU/Sparse Table

```python
import heapq
h=[]; heapq.heappush(h,(dist,no)); d,u=heapq.heappop(h)
```

```python
from collections import deque
q=deque([1,2]); q.appendleft(0); x=q.popleft()
```

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
```

**Sparse Table (RMQ idempotente)**

```python
import math

def build_st(a):
    n=len(a); K=(n).bit_length()
    st=[a[:]]
    k=1
    while (1<<k)<=n:
        prev=st[-1]; cur=[0]*(n-(1<<k)+1)
        half=1<<(k-1)
        for i in range(len(cur)):
            cur[i]=min(prev[i], prev[i+half])
        st.append(cur); k+=1
    return st

def rmq(st,l,r): # min no intervalo [l,r]
    k=(r-l+1).bit_length()-1
    return min(st[k][l], st[k][r-(1<<k)+1])
```

---

## 8) Fenwick (BIT) e Segment Tree (+ lazy)

```python
class Fenwick:
    def __init__(self,n): self.n=n; self.ft=[0]*(n+1)
    def add(self,i,v):
        while i<=self.n:
            self.ft[i]+=v; i+= i&-i
    def sum(self,i):
        s=0
        while i>0: s+=self.ft[i]; i-= i&-i
        return s
    def range_sum(self,l,r): return self.sum(r)-self.sum(l-1)
```

```python
class SegTree:
    def __init__(self,arr):
        n=1
        while n<len(arr): n<<=1
        self.n=n; self.st=[0]*(2*n)
        for i,v in enumerate(arr): self.st[n+i]=v
        for i in range(n-1,0,-1): self.st[i]=self.st[i<<1]+self.st[i<<1|1]
    def update(self,idx,val):
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

**Lazy (incremento em intervalo)**

```python
class SegLazy:
    def __init__(self,n):
        N=1
        while N<n: N<<=1
        self.N=N; self.st=[0]*(2*N); self.lz=[0]*(2*N)
    def _push(self,i,l,r):
        if self.lz[i]!=0 and l!=r:
            m=(l+r)//2
            for ch in (i<<1, i<<1|1): self.lz[ch]+=self.lz[i]
            self.st[i<<1]+= (m-l+1)*self.lz[i]
            self.st[i<<1|1]+= (r-m)*self.lz[i]
            self.lz[i]=0
    def _upd(self,i,l,r,ql,qr,val):
        if qr<l or r<ql: return
        if ql<=l and r<=qr:
            self.st[i]+= (r-l+1)*val; self.lz[i]+=val; return
        self._push(i,l,r); m=(l+r)//2
        self._upd(i<<1,l,m,ql,qr,val)
        self._upd(i<<1|1,m+1,r,ql,qr,val)
        self.st[i]=self.st[i<<1]+self.st[i<<1|1]
    def _qry(self,i,l,r,ql,qr):
        if qr<l or r<ql: return 0
        if ql<=l and r<=qr: return self.st[i]
        self._push(i,l,r); m=(l+r)//2
        return self._qry(i<<1,l,m,ql,qr)+self._qry(i<<1|1,m+1,r,ql,qr)
    def update(self,l,r,val): self._upd(1,0,self.N-1,l,r,val)
    def query(self,l,r): return self._qry(1,0,self.N-1,l,r)
```

---

## 9) Grafos básicos

Representação:

```python
n,m = map(int, input().split())
adj=[[] for _ in range(n)]
for _ in range(m):
    u,v = map(int, input().split())
    adj[u].append(v); adj[v].append(u)  # não-dirigido
```

BFS / DFS / Toposort:

```python
from collections import deque

def bfs(s,adj):
    dist=[-1]*len(adj); dist[s]=0; q=deque([s])
    while q:
        u=q.popleft()
        for v in adj[u]:
            if dist[v]==-1:
                dist[v]=dist[u]+1; q.append(v)
    return dist

def toposort(n,adj):
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
    return topo
```

Dijkstra / 0–1 BFS:

```python
import heapq

def dijkstra(s, adjw):
    INF=10**18; n=len(adjw)
    dist=[INF]*n; dist[s]=0
    pq=[(0,s)]
    while pq:
        d,u=heapq.heappop(pq)
        if d!=dist[u]: continue
        for v,w in adjw[u]:
            nd=d+w
            if nd<dist[v]:
                dist[v]=nd; heapq.heappush(pq,(nd,v))
    return dist

from collections import deque

def zero_one_bfs(s, g):  # g[u]: (v, w in {0,1})
    INF=10**18; n=len(g)
    dist=[INF]*n; dist[s]=0
    dq=deque([s])
    while dq:
        u=dq.popleft()
        for v,w in g[u]:
            nd=dist[u]+w
            if nd<dist[v]:
                dist[v]=nd
                (dq.appendleft if w==0 else dq.append)(v)
    return dist
```

---

## 10) Árvores básicas: Euler, LCA, subárvore

```python
def euler_tour(adj, root=0):
    n=len(adj); tin=[0]*n; tout=[0]*n; t=0; order=[]
    def dfs(u,p=-1):
        nonlocal t
        tin[u]=t; order.append(u); t+=1
        for v in adj[u]:
            if v==p: continue
            dfs(v,u)
        tout[u]=t-1
    dfs(root); return tin,tout,order
```

```python
def build_lca(adj, root=0):
    n=len(adj); LOG=n.bit_length()
    up=[[0]*n for _ in range(LOG)]; depth=[0]*n
    from collections import deque
    vis=[False]*n; vis[root]=True
    q=deque([root]); up[0][root]=root
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
        da=depth[a]-depth[b]; k=0
        while da:
            if da&1: a=up[k][a]
            da>>=1; k+=1
        if a==b: return a
        for k in range(LOG-1,-1,-1):
            if up[k][a]!=up[k][b]: a=up[k][a]; b=up[k][b]
        return up[0][a]
    return lca, depth
```

---

## 11) Strings base

**KMP / prefix-function**

```python
def prefix_function(s:str):
    n=len(s); pi=[0]*n
    for i in range(1,n):
        j=pi[i-1]
        while j>0 and s[i]!=s[j]: j=pi[j-1]
        if s[i]==s[j]: j+=1
        pi[i]=j
    return pi
```

**Z-function**

```python
def z_function(s:str):
    n=len(s); z=[0]*n; l=r=0
    for i in range(1,n):
        if i<=r: z[i]=min(r-i+1, z[i-l])
        while i+z[i]<n and s[z[i]]==s[i+z[i]]: z[i]+=1
        if i+z[i]-1>r: l,r=i,i+z[i]-1
    return z
```

**Rolling hash + Manacher** (palíndromos) — ver seção 16 para mais strings.

---

## 12) DP clássica

```python
# knapsack 0/1
def knapsack(W, w, v):
    dp=[0]*(W+1)
    for wi,vi in zip(w,v):
        for c in range(W, wi-1, -1):
            dp[c]=max(dp[c], dp[c-wi]+vi)
    return dp[W]

# LIS O(n log n)
import bisect

def lis_len(a):
    d=[]
    for x in a:
        i=bisect.bisect_left(d,x)
        if i==len(d): d.append(x)
        else: d[i]=x
    return len(d)

# moedas (maneiras)
def coin_ways(v, alvo):
    dp=[0]*(alvo+1); dp[0]=1
    for c in v:
        for s in range(c, alvo+1):
            dp[s]+=dp[s-c]
    return dp[alvo]
```

---

## 13) Geometria básica

```python
from typing import Tuple
Point=Tuple[int,int]

def cross(ax,ay,bx,by): return ax*by-ay*bx

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

# Convex hull (Monotone Chain)

def convex_hull(pts):
    pts=sorted(set(pts))
    if len(pts)<=1: return pts
    def cr(o,a,b): return (a[0]-o[0])*(b[1]-o[1])-(a[1]-o[1])*(b[0]-o[0])
    lo=[]
    for p in pts:
        while len(lo)>=2 and cr(lo[-2], lo[-1], p)<=0: lo.pop()
        lo.append(p)
    up=[]
    for p in reversed(pts):
        while len(up)>=2 and cr(up[-2], up[-1], p)<=0: up.pop()
        up.append(p)
    return lo[:-1]+up[:-1]
```

---

## 14) Padrões médios: janela monotônica, *sweep*, compressão

```python
from collections import deque
# janela máxima com deque monotônico

def sliding_max(a,k):
    dq=deque(); res=[]
    for i,x in enumerate(a):
        while dq and dq[0]<=i-k: dq.popleft()
        while dq and a[dq[-1]]<=x: dq.pop()
        dq.append(i)
        if i>=k-1: res.append(a[dq[0]])
    return res
```

```python
# sweep line de intervalos

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

**Compressão de coordenadas**

```python
def compress(vals):
    idx={v:i for i,v in enumerate(sorted(set(vals)))}
    return [idx[v] for v in vals], idx
```

---

## 15) DP otimizada: bitset, monotônica, D\&C, Knuth

**Bitset (subset-sum)**

```python
def subset_sum_possible(vals, S):
    bit=1
    for x in vals: bit |= (bit<<x)
    return (bit>>S)&1
```

**Monotônica (fila) e D\&C** — *esqueletos* para quando `argmin` é monótono e custo é quadrático:

```python
# D&C DP: resolve dp[l..r] usando ótimos em [optL..optR]
# Preencha custo(i,j) e estrutura conforme o problema.
```

**Knuth optimization** — quando `opt[i][j] ≤ opt[i][j+1]` e quadrangle inequality.

---

## 16) Strings avançadas

**Aho–Corasick (múltiplos padrões)**

```python
from collections import deque, defaultdict

def aho_build(patterns):
    trie=[defaultdict(int)]; out=[[]]; link=[0]
    for pid,p in enumerate(patterns):
        v=0
        for ch in p:
            if ch not in trie[v]:
                trie[v][ch]=len(trie); trie.append(defaultdict(int)); out.append([]); link.append(0)
            v=trie[v][ch]
        out[v].append(pid)
    q=deque()
    for ch,v in trie[0].items(): q.append(v)
    while q:
        v=q.popleft()
        for ch,u in trie[v].items():
            q.append(u); f=link[v]
            while f and ch not in trie[f]: f=link[f]
            link[u]=trie[f][ch] if ch in trie[f] else 0
            out[u]+=out[link[u]]
    return trie, link, out
```

**Suffix Array (SA) + LCP (Kasai)**

```python
def sa_build(s):
    n=len(s); k=1
    sa=list(range(n)); r=[ord(c) for c in s]; tmp=[0]*n
    while True:
        sa.sort(key=lambda i: (r[i], r[i+k] if i+k<n else -1))
        tmp[sa[0]]=0
        for i in range(1,n):
            tmp[sa[i]] = tmp[sa[i-1]] + ((r[sa[i-1]], r[sa[i-1]+k] if sa[i-1]+k<n else -1) < (r[sa[i]], r[sa[i]+k] if sa[i]+k<n else -1))
        r,tmp = tmp,r
        if r[sa[-1]]==n-1: break
        k<<=1
    return sa

def lcp_kasai(s, sa):
    n=len(s); rk=[0]*n
    for i,p in enumerate(sa): rk[p]=i
    lcp=[0]*(n-1); k=0
    for i in range(n):
        if rk[i]==n-1: k=0; continue
        j=sa[rk[i]+1]
        while i+k<n and j+k<n and s[i+k]==s[j+k]: k+=1
        lcp[rk[i]]=k
        if k: k-=1
    return lcp
```

**Suffix Automaton (SAM)** — aceitação de substrings em O(1) amort.

```python
class SAM:
    def __init__(self):
        self.link=[-1]; self.len=[0]; self.next=[{}]
        self.last=0
    def extend(self, ch):
        cur=len(self.len); self.len.append(self.len[self.last]+1)
        self.link.append(0); self.next.append({})
        p=self.last
        while p!=-1 and ch not in self.next[p]:
            self.next[p][ch]=cur; p=self.link[p]
        if p==-1: self.link[cur]=0
        else:
            q=self.next[p][ch]
            if self.len[p]+1==self.len[q]: self.link[cur]=q
            else:
                clone=len(self.len)
                self.len.append(self.len[p]+1)
                self.next.append(self.next[q].copy())
                self.link.append(self.link[q])
                while p!=-1 and self.next[p].get(ch, -1)==q:
                    self.next[p][ch]=clone; p=self.link[p]
                self.link[q]=self.link[cur]=clone
        self.last=cur
```

---

## 17) Árvores avançadas: centroid, DSU-on-tree, HLD

**Centroid Decomposition** — esqueleto:

```python
def centroid_decomp(adj):
    n=len(adj); used=[False]*n; sz=[0]*n
    def dfs_sz(u,p):
        sz[u]=1
        for v in adj[u]:
            if v==p or used[v]: continue
            dfs_sz(v,u); sz[u]+=sz[v]
    def find_cent(u,p,tot):
        for v in adj[u]:
            if v!=p and not used[v] and sz[v]>tot//2:
                return find_cent(v,u,tot)
        return u
    def solve(u):
        dfs_sz(u,-1); c=find_cent(u,-1,sz[u])
        used[c]=True
        # processa c como raiz do nível
        for v in adj[c]:
            if not used[v]: solve(v)
    solve(0)
```

**DSU on Tree (small-to-large)** — técnica para manter *freqs* por subárvore.

**HLD (Heavy-Light Decomposition)** com SegTree — caminhos/ranges em árvore com *queries* rápidas.

---

## 18) Grafos avançados: SCC, pontes/articulações, Euleriano

**SCC (Kosaraju)**

```python
def scc_kosaraju(n, adj):
    rg=[[] for _ in range(n)]
    for u in range(n):
        for v in adj[u]: rg[v].append(u)
    vis=[False]*n; order=[]
    def dfs1(u):
        vis[u]=True
        for v in adj[u]:
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

**Pontes e articulações (Tarjan)**

```python
def bridges_articulations(n, adj):
    timer=0; tin=[-1]*n; low=[-1]*n
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

**Caminho Euleriano (não-dir.)**: componente única e 0 ou 2 graus ímpares.

---

## 19) Matching & Flow

**Hopcroft–Karp (bipartido)** — esqueleto rápido para máximo emparelhamento.

**Dinic (máximo fluxo)**

```python
from collections import deque

class Dinic:
    def __init__(self,n):
        self.n=n; self.adj=[[] for _ in range(n)]
    def add_edge(self,u,v,c):
        self.adj[u].append([v,c,len(self.adj[v])])
        self.adj[v].append([u,0,len(self.adj[u])-1])
    def bfs(self,s,t,lev):
        for i in range(self.n): lev[i]=-1
        q=deque([s]); lev[s]=0
        while q:
            u=q.popleft()
            for v,c,rev in self.adj[u]:
                if c>0 and lev[v]<0:
                    lev[v]=lev[u]+1; q.append(v)
        return lev[t]>=0
    def dfs(self,u,t,f,lev,it):
        if u==t: return f
        i=it[u]
        while i<len(self.adj[u]):
            v,c,rev=self.adj[u][i]
            if c>0 and lev[u]+1==lev[v]:
                ret=self.dfs(v,t,min(f,c),lev,it)
                if ret>0:
                    self.adj[u][i][1]-=ret
                    self.adj[v][rev][1]+=ret
                    return ret
            i+=1; it[u]=i
        return 0
    def maxflow(self,s,t):
        flow=0; lev=[-1]*self.n
        while self.bfs(s,t,lev):
            it=[0]*self.n
            while True:
                pushed=self.dfs(s,t,10**18,lev,it)
                if pushed==0: break
                flow+=pushed
        return flow
```

**Min-Cost Max-Flow (SPFA/Johnson)** — esqueleto (omisso por extensão; incluir sob demanda).

---

## 20) Matemática avançada: exgcd, CRT geral, Miller–Rabin, Pollard Rho

**exgcd + inverso modular (geral)**

```python
def exgcd(a,b):
    if b==0: return (a,1,0)
    g,x1,y1 = exgcd(b, a%b)
    return (g, y1, x1 - (a//b)*y1)

def inv_mod(a,m):
    g,x,_=exgcd(a,m)
    if g!=1: return None
    return x%m
```

**CRT geral (módulos possivelmente não coprimos)**

```python
def crt_pair(a1,m1,a2,m2):
    g,x,y=exgcd(m1,m2)
    if (a2-a1)%g!=0: return (0,0)  # sem solução
    l=m1//g*m2
    k=((a2-a1)//g*x)% (m2//g)
    return ( (a1 + k*m1)%l , l )
```

**Miller–Rabin 64-bit**

```python
def is_probable_prime(n:int)->bool:
    if n<2: return False
    small=[2,3,5,7,11,13,17,19,23,29]
    for p in small:
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
    for a in [2,3,5,7,11,13]:
        if not check(a): return False
    return True
```

**Pollard Rho (fatorização prática)** — esqueleto curto.

---

## 21) FFT/NTT

**FFT (complexa) — multiplicação polinomial**

```python
# Use numpy se permitido (mais simples). Abaixo, esqueleto *puro* é longo; manter referência.
```

**NTT (mod 998244353)** — rápida e estável para inteiros.

---

## 22) Algoritmos offline: Mo’s Algorithm (+ variações)

**Mo’s 1D** — ordenar queries por bloco de L e R.

```python
# add/remove no, e mantenha resposta global.
```

**Variações**: com atualizações (Mo’s com tempo), em árvores (Euler + Mo’s), *Hilbert order*.

---

## 23) Interativo, *stress test*, *debug*, *checker*

Interativo (flush):

```python
import sys

def ask(q):
    print(q); sys.stdout.flush()
    return input().strip()
```

*Stress test* + gerador — ver também seção 24.3.

---

## 24) Templates finais

### 24.1 Template curto

```python
# -*- coding: utf-8 -*-
import sys
from typing import *
from collections import deque, Counter, defaultdict
import math, bisect, heapq

def input(): return sys.stdin.readline().rstrip()

def main():
    pass

if __name__=='__main__':
    # sys.setrecursionlimit(1_000_000)
    main()
```

### 24.2 Template completo (com utilidades)

```python
# -*- coding: utf-8 -*-
import sys, math, bisect, heapq, random
from typing import *
from collections import deque, Counter, defaultdict

INF=10**18; MOD=1_000_000_007

def input(): return sys.stdin.readline().rstrip()

def ints(): return list(map(int, input().split()))

def read_all_ints(): return list(map(int, sys.stdin.buffer.read().split()))

# gcd/lcm
from math import gcd

def lcm(a,b): return a//gcd(a,b)*b

def modpow(a,e,m=MOD): return pow(a,e,m)

def modinv(a,m=MOD): return pow(a, m-2, m)

# Fenwick
class BIT:
    def __init__(self,n): self.n=n; self.ft=[0]*(n+1)
    def add(self,i,v):
        while i<=self.n: self.ft[i]+=v; i+= i&-i
    def sum(self,i):
        s=0
        while i>0: s+=self.ft[i]; i-= i&-i
        return s

# DSU
class DSU:
    def __init__(self,n): self.p=list(range(n)); self.sz=[1]*n
    def find(self,x):
        while x!=self.p[x]: self.p[x]=self.p[self.p[x]]; x=self.p[x]
        return x
    def union(self,a,b):
        a,b=self.find(a),self.find(b)
        if a==b: return False
        if self.sz[a]<self.sz[b]: a,b=b,a
        self.p[b]=a; self.sz[a]+=self.sz[b]; return True

# Dijkstra

def dijkstra(s, adjw):
    dist=[INF]*len(adjw); dist[s]=0
    pq=[(0,s)]
    while pq:
        d,u=heapq.heappop(pq)
        if d!=dist[u]: continue
        for v,w in adjw[u]:
            nd=d+w
            if nd<dist[v]: dist[v]=nd; heapq.heappush(pq,(nd,v))
    return dist


def main():
    pass

if __name__=='__main__':
    # sys.setrecursionlimit(1_000_000)
    main()
```

---

### ✅ O que foi intencionalmente resumido

* FFT pura/NTT e Pollard Rho completos são longos; mantidos como **esqueletos**/referência. Se for usar em prova, vale preparar arquivos prontos localmente.
* Min-Cost Max-Flow completo idem (existe variação com SPFA/Johnson). Posso incluir a versão final se você preferir.

> **Dica final:** Foque nos **padrões** (prefix, janela, *hash*, BFS/Dijkstra, Fenwick/SegTree, KMP/Z, DP 1D/2D). Esses resolvem 70–80% das provas amadoras. Quando sobrar tempo, agregue os módulos avançados aqui mesmo para montar seu “caderno de código”.

---

# Parte II — **Avançado++ e Preparação Máxima** (continuação em ordem de dificuldade crescente)

> A partir daqui entram tópicos de **nível médio→alto** para te deixar hiper preparado. Mantemos a ordem geral do mais acessível para o mais exigente.

## 32) Multi‑source BFS, DAG‑Shortest/Longest

**Multi‑source BFS** (coloque várias fontes na fila com dist=0):

```python
from collections import deque

def multi_source_bfs(n, adj, fontes):
    dist=[-1]*n; q=deque()
    for s in fontes: dist[s]=0; q.append(s)
    while q:
        u=q.popleft()
        for v in adj[u]:
            if dist[v]==-1:
                dist[v]=dist[u]+1; q.append(v)
    return dist
```

**DAG shortest/longest** (toposort + DP):

```python
from collections import deque

def dag_shortest(n, adjw, s):
    indeg=[0]*n
    for u in range(n):
        for v,_ in adjw[u]: indeg[v]+=1
    q=deque([i for i in range(n) if indeg[i]==0])
    topo=[]
    while q:
        u=q.popleft(); topo.append(u)
        for v,_ in adjw[u]:
            indeg[v]-=1
            if indeg[v]==0: q.append(v)
    INF=10**18; dist=[INF]*n; dist[s]=0
    for u in topo:
        if dist[u]==INF: continue
        for v,w in adjw[u]:
            if dist[u]+w<dist[v]: dist[v]=dist[u]+w
    return dist
```

---

## 33) Fenwick avançado — k‑ésimo por soma prefixo

```python
class Fenwick:
    def __init__(self,n): self.n=n; self.ft=[0]*(n+1)
    def add(self,i,v):
        while i<=self.n: self.ft[i]+=v; i+= i&-i
    def sum(self,i):
        s=0
        while i>0: s+=self.ft[i]; i-= i&-i
        return s
    # retorna o menor idx i com sum(i) >= k (assume valores não-negativos)
    def kth(self,k):
        i=0; bit=1<< (self.n.bit_length())
        while bit:
            j=i|bit
            if j<=self.n and self.ft[j]<k:
                i=j; k-=self.ft[j]
            bit>>=1
        return i+1
```

---

## 34) Li Chao Tree (Convex Hull Trick dinâmico)

Minimiza `y = m*x + b` em ponto `x` (linhas inseridas online):

```python
class LiChao:
    class Line:
        __slots__=("m","b")
        def __init__(self,m,b): self.m=m; self.b=b
        def f(self,x): return self.m*x + self.b
    def __init__(self, X_MIN, X_MAX):
        self.X_MIN=X_MIN; self.X_MAX=X_MAX
        self.st={}
    def _add(self, i, l, r, nl):
        if i not in self.st: self.st[i]=nl; return
        lo, hi = self.st[i], nl
        mid=(l+r)//2
        if lo.f(mid) > hi.f(mid): lo,hi = hi,lo
        self.st[i]=lo
        if l==r: return
        if lo.f(l) > hi.f(l):
            self._add(i<<1, l, mid, hi)
        elif lo.f(r) > hi.f(r):
            self._add(i<<1|1, mid+1, r, hi)
    def add_line(self, m, b):
        self._add(1, self.X_MIN, self.X_MAX, LiChao.Line(m,b))
    def _qry(self, i, l, r, x):
        if i not in self.st: return 10**30
        cur=self.st[i].f(x)
        if l==r: return cur
        mid=(l+r)//2
        if x<=mid: return min(cur, self._qry(i<<1, l, mid, x))
        else:      return min(cur, self._qry(i<<1|1, mid+1, r, x))
    def query(self, x):
        return self._qry(1, self.X_MIN, self.X_MAX, x)
```

---

## 35) HLD — Heavy‑Light Decomposition (com SegTree)

Suporta *query* em caminho `u↔v` mapeando para intervalos contíguos.

```python
class HLD:
    def __init__(self, n, adj, root=0, vals=None):
        self.n=n; self.adj=adj; self.root=root
        self.par=[-1]*n; self.depth=[0]*n; self.sz=[1]*n
        self.heavy=[-1]*n; self.head=[0]*n; self.pos=[0]*n
        self.cur=0
        self._dfs(root)
        self._decomp(root, root)
        base=[0]*n
        if vals is not None:
            for v in range(n): base[self.pos[v]]=vals[v]
        self.seg=SegTree(base)
    def _dfs(self,u):
        max_sz=0
        for v in self.adj[u]:
            if v==self.par[u]: continue
            self.par[v]=u; self.depth[v]=self.depth[u]+1
            self._dfs(v); self.sz[u]+=self.sz[v]
            if self.sz[v]>max_sz: max_sz=self.sz[v]; self.heavy[u]=v
    def _decomp(self,u,h):
        self.head[u]=h; self.pos[u]=self.cur; self.cur+=1
        if self.heavy[u]!=-1: self._decomp(self.heavy[u], h)
        for v in self.adj[u]:
            if v!=self.par[u] and v!=self.heavy[u]:
                self._decomp(v, v)
    def query_path(self,u,v):  # soma no caminho
        res=0
        while self.head[u]!=self.head[v]:
            if self.depth[self.head[u]] < self.depth[self.head[v]]:
                u,v=v,u
            h=self.head[u]
            res+=self.seg.query(self.pos[h], self.pos[u])
            u=self.par[h]
        if self.depth[u]>self.depth[v]: u,v=v,u
        res+=self.seg.query(self.pos[u], self.pos[v])
        return res
    def update_point(self,u,val):
        self.seg.update(self.pos[u], val)
```

*(usa `SegTree` da seção anterior, de soma)*

---

## 36) Emparelhamento Bipartido — Hopcroft–Karp

```python
from collections import deque

def hopcroft_karp(G, U, V):  # G: adj de U->V com rótulos 0..U-1 e 0..V-1
    INF=10**9
    pairU=[-1]*U; pairV=[-1]*V; dist=[0]*U
    def bfs():
        q=deque()
        for u in range(U):
            if pairU[u]==-1: dist[u]=0; q.append(u)
            else: dist[u]=INF
        dmin=INF
        while q:
            u=q.popleft()
            if dist[u]>=dmin: continue
            for v in G[u]:
                pu=pairV[v]
                if pu==-1: dmin=dist[u]+1
                elif dist[pu]==INF:
                    dist[pu]=dist[u]+1; q.append(pu)
        return dmin!=INF
    def dfs(u):
        for v in G[u]:
            pu=pairV[v]
            if pu==-1 or (dist[pu]==dist[u]+1 and dfs(pu)):
                pairU[u]=v; pairV[v]=u; return True
        dist[u]=10**9; return False
    matching=0
    while bfs():
        for u in range(U):
            if pairU[u]==-1 and dfs(u): matching+=1
    return matching, pairU, pairV
```

---

## 37) Fluxo Máximo — Dinic (já acima) + **Min‑Cost Max‑Flow**

SSAP com potenciais (Johnson) + Dijkstra:

```python
import heapq

def mcmf(n, s, t):
    g=[[] for _ in range(n)]
    def add(u,v,c,w):  # capacidade c, custo w
        g[u].append([v,c,w,len(g[v])])
        g[v].append([u,0,-w,len(g[u])-1])
    def min_cost_max_flow():
        N=len(g); flow=0; cost=0
        INF=10**18
        h=[0]*N  # potenciais
        while True:
            dist=[INF]*N; dist[s]=0
            par=[(-1,-1)]*N
            pq=[(0,s)]
            while pq:
                d,u=heapq.heappop(pq)
                if d!=dist[u]: continue
                for i,(v,c,w,rev) in enumerate(g[u]):
                    if c>0 and dist[u]+w+h[u]-h[v]<dist[v]:
                        dist[v]=dist[u]+w+h[u]-h[v]
                        par[v]=(u,i)
                        heapq.heappush(pq,(dist[v],v))
            if dist[t]==INF: break
            for v in range(N):
                if dist[v]<INF: h[v]+=dist[v]
            # aumenta 1 caminho (ou o gargalo)
            f=INF; v=t
            while v!=s:
                u,i=par[v]; f=min(f, g[u][i][1]); v=u
            v=t
            while v!=s:
                u,i=par[v]
                g[u][i][1]-=f
                rev=g[u][i][3]
                g[v][rev][1]+=f
                cost+=f*g[u][i][2]
                v=u
            flow+=f
        return flow, cost
    return g, add, min_cost_max_flow
```

---

## 38) Hungarian (Assignment) — O(n³)

Minimiza custo em matriz quadrada `cost[n][n]`:

```python
def hungarian(cost):
    n=len(cost)
    u=[0]*(n+1); v=[0]*(n+1); p=[0]*(n+1); way=[0]*(n+1)
    for i in range(1,n+1):
        p[0]=i; j0=0
        minv=[10**18]*(n+1); used=[False]*(n+1)
        while True:
            used[j0]=True; i0=p[j0]; delta=10**18; j1=0
            for j in range(1,n+1):
                if used[j]: continue
                cur=cost[i0-1][j-1]-u[i0]-v[j]
                if cur<minv[j]: minv[j]=cur; way[j]=j0
                if minv[j]<delta: delta=minv[j]; j1=j
            for j in range(n+1):
                if used[j]: u[p[j]]+=delta; v[j]-=delta
                else: minv[j]-=delta
            j0=j1
            if p[j0]==0: break
        while True:
            j1=way[j0]; p[j0]=p[j1]; j0=j1
            if j0==0: break
    match=[0]*n
    for j in range(1,n+1):
        if p[j]>0: match[p[j]-1]=j-1
    return match, -v[0]
```

---

## 39) Eertree (Árvore Palindrômica)

Mantém todos os palíndromos distintos em O(n).

```python
class Eertree:
    def __init__(self):
        self.len=[-1,0]; self.link=[0,0]; self.next=[{} for _ in range(2)]
        self.s=[-1]; self.last=1
    def add(self, ch):
        s=self.s; s.append(ch)
        cur=self.last; curlen=0
        while True:
            curlen=self.len[cur]
            if s[-2-curlen]==ch: break
            cur=self.link[cur]
        if ch in self.next[cur]:
            self.last=self.next[cur][ch]; return
        self.len.append(self.len[cur]+2)
        self.link.append(0); self.next.append({})
        self.next[cur][ch]=len(self.len)-1
        if self.len[-1]==1:
            self.link[-1]=1; self.last=len(self.len)-1; return
        while True:
            cur=self.link[cur]; curlen=self.len[cur]
            if s[-2-curlen]==ch:
                self.link[-1]=self.next[cur][ch]; break
        self.last=len(self.len)-1
```

---

## 40) Suffix Automaton (extras úteis)

**Contagem de substrings distintas**: `sum(len[v] - len[link[v]])`.

```python
class SAM:
    def __init__(self):
        self.link=[-1]; self.len=[0]; self.next=[{}]; self.last=0
    def extend(self, ch):
        cur=len(self.len); self.len.append(self.len[self.last]+1)
        self.link.append(0); self.next.append({})
        p=self.last
        while p!=-1 and ch not in self.next[p]: self.next[p][ch]=cur; p=self.link[p]
        if p==-1: self.link[cur]=0
        else:
            q=self.next[p][ch]
            if self.len[p]+1==self.len[q]: self.link[cur]=q
            else:
                clone=len(self.len)
                self.len.append(self.len[p]+1)
                self.next.append(self.next[q].copy())
                self.link.append(self.link[q])
                while p!=-1 and self.next[p].get(ch,-1)==q:
                    self.next[p][ch]=clone; p=self.link[p]
                self.link[q]=self.link[cur]=clone
        self.last=cur
    def distinct_substrings(self):
        return sum(self.len[i]-self.len[self.link[i]] for i in range(1,len(self.len)))
```

---

## 41) Suffix Array + LCP (com RMQ para LCP rápido)

*(complementa a versão básica, permitindo LCP de qualquer par em O(1) após RMQ)*

---

## 42) FFT/NTT — Convolução Rápida

**NTT (mod 998244353, raiz 3)**

```python
MOD=998244353; G=3

def ntt(a, inv=False):
    n=len(a); j=0
    for i in range(1,n):
        bit=n>>1
        while j&bit: j^=bit; bit>>=1
        j^=bit
        if i<j: a[i],a[j]=a[j],a[i]
    len_=2
    while len_<=n:
        wlen=pow(G,(MOD-1)//len_,MOD)
        if inv: wlen=pow(wlen, MOD-2, MOD)
        for i in range(0,n,len_):
            w=1
            for j in range(i, i+len_//2):
                u=a[j]; v=a[j+len_//2]*w%MOD
                a[j]=(u+v)%MOD
                a[j+len_//2]=(u-v)%MOD
                w=w*wlen%MOD
        len_<<=1
    if inv:
        invn=pow(n, MOD-2, MOD)
        for i in range(n): a[i]=a[i]*invn%MOD

def convolution(a,b):
    n=1
    while n<len(a)+len(b)-1: n<<=1
    fa=a+[0]*(n-len(a)); fb=b+[0]*(n-len(b))
    ntt(fa); ntt(fb)
    for i in range(n): fa[i]=fa[i]*fb[i]%MOD
    ntt(fa, inv=True)
    return fa[:len(a)+len(b)-1]
```

---

## 43) Fatoração Rápida — Pollard Rho (com Miller–Rabin)

```python
import random

def is_probable_prime(n:int)->bool:
    if n<2: return False
    small=[2,3,5,7,11,13,17,19,23,29]
    for p in small:
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
    for a in [2,325,9375,28178,450775,9780504,1795265022]:  # bases 64‑bit
        if a%n and not check(a%n): return False
    return True

def pollard_rho(n):
    if n%2==0: return 2
    while True:
        c=random.randrange(1,n)
        f=lambda x: (x*x+c)%n
        x=y=random.randrange(0,n)
        d=1
        while d==1:
            x=f(x); y=f(f(y))
            d=math.gcd(abs(x-y), n)
        if d!=n: return d

def factor(n, fac):
    if n==1: return
    if is_probable_prime(n):
        fac.append(n); return
    d=pollard_rho(n)
    factor(d, fac); factor(n//d, fac)
```

---

## 44) Mo’s Algorithm — básico, com atualizações e em árvore

**Básico (1D, sem updates)**: ordenar por blocos de `L` e `R`.

```python
# mantenha add/remove e a resposta global; mover ponteiros l/r
```

**Com atualizações**: ordena por (blocL, blocR, tempo). **Em árvore**: Euler Tour + Mo’s.

---

## 45) DSU Rollback (para dividir e conquistar no tempo)

Esqueleto para processar *queries* offline adicionando/removendo arestas.

```python
class DSURoll:
    def __init__(self,n):
        self.p=list(range(n)); self.sz=[1]*n; self.st=[]
    def find(self,x):
        while x!=self.p[x]: x=self.p[x]
        return x
    def unite(self,a,b):
        a=self.find(a); b=self.find(b)
        if a==b: self.st.append((-1,-1)); return False
        if self.sz[a]<self.sz[b]: a,b=b,a
        self.p[b]=a; self.sz[a]+=self.sz[b]; self.st.append((a,b)); return True
    def rollback(self):
        a,b=self.st.pop()
        if a==-1: return
        self.p[b]=b; self.sz[a]-=self.sz[b]
```

---

## 46) Segment Tree Persistente (k‑ésimo em prefixo)

Estrutura clássica para *order statistics* em array estático (offline com compressão de coordenadas).

---

## 47) Geometria avançada — Rotating Calipers, PIP, Hierholzer

**Diâmetro da casca convexa (calipers)**

```python
def hull_diameter(h):  # h em sentido anti-horário
    n=len(h)
    if n<=1: return 0
    j=1; best=0
    for i in range(n):
        ni=(i+1)%n
        while True:
            nj=(j+1)%n
            cur=abs((h[ni][0]-h[i][0])*(h[nj][1]-h[j][1]) - (h[ni][1]-h[i][1])*(h[nj][0]-h[j][0]))
            nxt=abs((h[ni][0]-h[i][0])*(h[j][1]-h[nj][1]) - (h[ni][1]-h[i][1])*(h[j][0]-h[nj][0]))
            if nxt>cur: j=nj
            else: break
        dx=h[i][0]-h[j][0]; dy=h[i][1]-h[j][1]
        best=max(best, dx*dx+dy*dy)
    return best  # distância ao quadrado
```

**Point‑in‑Polygon (ray casting)**

```python
def point_in_poly(poly, p):
    x,y=p; inside=False
    n=len(poly)
    for i in range(n):
        x1,y1=poly[i]; x2,y2=poly[(i+1)%n]
        if (y1>y)!=(y2>y):
            xint = x1 + (y-y1)*(x2-x1)/(y2-y1)
            if xint>=x: inside=not inside
    return inside
```

**Caminho/ circuito Euleriano (Hierholzer)**

```python
def euler_undirected(n, edges):  # edges: lista de (u,v)
    g=[[] for _ in range(n)]
    for i,(u,v) in enumerate(edges):
        g[u].append((v,i)); g[v].append((u,i))
    used=[False]*len(edges); st=[0]; path=[]
    it=[0]*n
    while st:
        u=st[-1]
        while it[u]<len(g[u]) and used[g[u][it[u]][1]]: it[u]+=1
        if it[u]==len(g[u]): path.append(st.pop())
        else:
            v,e=g[u][it[u]]; it[u]+=1; used[e]=True; st.append(v)
    return path[::-1]
```

---

## 48) Dicas finais de performance (nível ninja)

* **Pypy** para laços puros; evite muita OO pesada e *attrs* dinâmicos dentro de laços quentes.
* **Local bindings**: `push=heapq.heappush` fora do laço; capturar `append=q.append` etc.
* **Evite TLE por E/S**: monte respostas num `list` e `"
  ".join`.
* **Testes aleatórios + verificação lenta**: garanta corretude antes de otimizar.

---

## 49) Checklists de prova (rápido)

* [ ] Lê exatamente o que o enunciado pede? (linhas, casos, EOF)
* [ ] Complexidade confirma com limites? (n, m, Q)
* [ ] Casos borda testados? (vazio, 1, máximo, repetidos)
* [ ] Saída formatada 100% igual? (espacos, quebras)
* [ ] Sementes fixas removidas? `random.seed(0)` só para *debug*.
